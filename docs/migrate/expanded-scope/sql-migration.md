---
title: Urychlení migrace migrací instance SQL Server
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrace celých instancí SQL Server může urychlit úsilí migrace úloh.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e499e499cf1639bf9ce1118dcb93254268e9cb54
ms.sourcegitcommit: 3c325764ad8229b205d793593ff344dca3a0579b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/23/2019
ms.locfileid: "75328918"
---
# <a name="accelerate-migration-by-migrating-multiple-databases-or-entire-sql-servers"></a>Urychlení migrace migrací více databází nebo celých serverů SQL

Migrace celých instancí SQL Server může urychlit úsilí migrace úloh. Následující doprovodné materiály rozšiřují rozsah [příručky migrace do Azure](../azure-migration-guide/index.md) tím, že migrují instanci SQL Server mimo úsilí s možností migrace zaměřené na úlohy. Tento přístup může naplnit migraci více úloh pomocí jedné migrace na platformě dat. Většina úsilí požadovaná v tomto rozsahu rozšíření probíhá během procesu migrace požadavků, posuzování, migrace a optimalizace.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Je tento rozšířený obor pro vás nejvhodnější?

Přístup doporučený v [Průvodci migrací Azure](../azure-migration-guide/index.md) je migrace každé struktury dat spolu s přidruženými úlohami v rámci jedné snahy migrace. Iterativní přístup k migraci omezuje zjišťování, posuzování a další úlohy, které můžou vytvářet blokování a zpomalit vrácení obchodních hodnot.

Některé datové struktury ale můžete migrovat efektivněji prostřednictvím samostatné migrace dat na platformě. Tady je několik příkladů:

- **Konec služby:** Rychlé přesunutí instance SQL Server jako izolované iterace v rámci větší snahy migrace se může vyhnout problémům s ukončením služby. Tato příručka vám pomůže integrovat migraci SQL Server v širším procesu migrace. Pokud však migrujete nebo upgradujete SQL Server nezávisle na jakémkoli jiném úsilí při přijímání v cloudu, může SQL Server se v článcích [Přehled konce životnosti](/sql/sql-server/end-of-support/sql-server-end-of-life-overview) nebo [SQL serverch článků v dokumentaci k migraci](/sql/sql-server/migrate/index) poskytnout jasný návod.
- **SQL Server služby:** Struktura dat je součástí širšího řešení, které vyžaduje SQL Server běžící na virtuálním počítači. To je běžné pro řešení, která používají SQL Server služby, jako je SQL Server Reporting Services, služba SSIS (SQL Server Integration Services) nebo SQL Server Analysis Services.
- **Vysoce hustota, databáze s nízkým využitím:** Instance SQL Server má vysokou hustotu databází. Každá z těchto databází má nedostatečné objemy transakcí a vyžaduje malým způsobem výpočetních prostředků. Měli byste zvážit další moderní řešení, ale přístup k infrastruktuře jako služby (IaaS) může mít za následek výrazné snížení provozních nákladů.
- **Celkové náklady na vlastnictví:** V případě potřeby můžete použít [výhody hybridního využití Azure](https://azure.microsoft.com/pricing/hybrid-benefit) na ceníkovou cenu, která vytvoří nejnižší náklady na vlastnictví pro instance SQL Server. To je zvlášť běžné pro zákazníky, kteří hostují SQL Server ve scénářích s více cloudy.
- **Akcelerátor migrace:** Migrace instance SQL Server typu "zvednutí a posunutí" může přesunout několik databází v jedné iteraci. Tento přístup někdy umožňuje budoucím iteracím soustředit se přesněji na aplikace a virtuální počítače, což znamená, že můžete migrovat více úloh v rámci jedné iterace.
- **Migrace VMware:** Společná místní architektura zahrnuje aplikace a virtuální počítače na virtuálním hostiteli a databáze na holé počítače. V tomto scénáři můžete migrovat celé SQL Server instance pro podporu migrace hostitele VMware do Azure VMware Service. Další informace najdete v tématu [migrace hostitele VMware](./vmware-host.md).

Pokud se u této migrace neuplatní žádné z výše uvedených kritérií, může být nejlepší pokračovat se [standardním procesem migrace](../index.md). Ve standardním procesu jsou datové struktury postupně migrovány společně s jednotlivými úlohami.

Pokud tato příručka zarovnává s vašimi kritérii, pokračujte v tomto rozšířeném průvodci oboru jako úsilí v rámci [standardního procesu migrace](../index.md). Během fáze předpoklady můžete integrovat úsilí do celkového plánu přijetí.

## <a name="suggested-prerequisites"></a>Doporučené požadavky

Před provedením SQL Server migrace začněte s rozšířením digitální nemovitosti tím, že zahrnete datovou nemovitost. Datová nemovitost zaznamenává inventář datových assetů, které zvažujete pro migraci. Následující tabulky popisují přístup k záznamu majetku.

### <a name="server-inventory"></a>Inventář serverů

Následuje příklad inventarizace serveru:

|SQL Server|Účel|Verze|[Závažnost](../../manage/considerations/criticality.md)|[Hlediska](../../govern/policy-compliance/data-classification.md)|Počet databází|SSIS|SSRS|SSAS|Cluster|Počet uzlů|
|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|Základní aplikace|2016|Klíčové|Vysoce důvěrné|40|Nevztahuje se|Nevztahuje se|Nevztahuje se|Ano|3|
|SQL-02|Základní aplikace|2016|Klíčové|Vysoce důvěrné|40|Nevztahuje se|Nevztahuje se|Nevztahuje se|Ano|3|
|SQL-03|Základní aplikace|2016|Klíčové|Vysoce důvěrné|40|Nevztahuje se|Nevztahuje se|Nevztahuje se|Ano|3|
|SQL – 04|BI|2012|Vysoký|CZK|6|Nevztahuje se|Důvěrné informace|Ano – multidimenzionální datová krychle|Ne|1\. místo|
|SQL-05|Integrace|2008 R2|Nízký|Obecné|20|Ano|Nevztahuje se|Nevztahuje se|Ne|1\. místo|

### <a name="database-inventory"></a>Inventář databáze

Následuje příklad inventáře databáze pro jeden z výše uvedených serverů:

|Server|databáze|[Závažnost](../../manage/considerations/criticality.md)|[Hlediska](../../govern/policy-compliance/data-classification.md)|Výsledky Data Migration Assistant (DMA)|Řešení potíží s DMA|Cílová platforma|
|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|DB-1|Klíčové|Velmi důvěrné|Kompatibilita|Nevztahuje se|Databáze SQL Azure|
|SQL-01|DB-2|Vysoký|Důvěrné informace|Je vyžadována Změna schématu.|Změny implementovány|Databáze SQL Azure|
|SQL-01|DB-3|Vysoký|Obecné|Kompatibilita|Nevztahuje se|Spravovaná instance Azure SQL|
|SQL-01|DB-4|Nízký|Velmi důvěrné|Je vyžadována Změna schématu.|Naplánované změny|Spravovaná instance Azure SQL|
|SQL-01|DB-5|Klíčové|Obecné|Kompatibilita|Nevztahuje se|Spravovaná instance Azure SQL|
|SQL-01|DB-6|Vysoký|Důvěrné informace|Kompatibilita|Nevztahuje se|Databáze SQL Azure|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrace s plánem přijetí do cloudu

Po dokončení tohoto procesu zjišťování ho můžete zahrnout do [plánu přijetí do cloudu](../../plan/template.md). V rámci plánu přijetí do cloudu přidejte každou instanci SQL Server, kterou chcete migrovat, jako samostatnou [úlohu](../../plan/workloads.md). V rámci každé úlohy je možné jednotlivé databáze a služby (SSIS, SSAS, SSRS) přidat jako [prostředky](../../plan/workloads.md). Chcete-li přidat úlohy a prostředky hromadně do plánu přijetí, přečtěte si téma [Přidání a úprava pracovních položek v aplikaci Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Po zahrnutí úloh a prostředků do plánu můžete vy a váš tým pokračovat se standardním procesem migrace pomocí plánu přijetí. Když se tým přijetí přesune do procesů hodnocení, migrace a optimalizace, probere faktor změny v následujících oddílech.

## <a name="assessment-process-changes"></a>Změny procesu posouzení

Pokud může být libovolná databáze v plánu migrována na datovou platformu PaaS (Platform as a Service), použijte k vyhodnocení kompatibility vybrané databáze možnost DMA. Pokud databáze vyžaduje převody schématu, měli byste tyto převody v rámci procesu hodnocení dokončit, abyste se vyhnuli přerušení kanálu migrace.

### <a name="suggested-action-during-the-assessment-process"></a>Navrhovaná akce během procesu posouzení

Pro databáze, které je možné migrovat do řešení PaaS, se během procesu hodnocení dokončí následující akce.

- **Vyhodnotit pomocí DMA:** Pomocí Data Migration Assistant můžete detekovat problémy s kompatibilitou, které mohou ovlivnit funkčnost databáze ve vaší cílové Azure SQL Database spravované instanci. Pomocí DMA můžete doporučit vylepšení výkonu a spolehlivosti a přesunout schéma, data a neobsažené objekty ze zdrojového serveru na cílový server. Další informace najdete v tématu [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview).
- **Opravit a převést:** Na základě výstupu DMA převeďte zdrojové schéma dat, aby se opravily problémy s kompatibilitou. Otestujte schéma převedených dat pomocí závislých aplikací.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Během migrace si můžete vybrat z mnoha různých nástrojů a přístupů. Každý přístup ale následuje jednoduchý proces: migrace schématu, dat a objektů. Pak synchronizujte data s cílovým zdrojem dat.

Cíl a zdroj datových struktur a služeb můžou tyto dva kroky udělat raději. V následujících částech se dozvíte, co nejlépe vyberu podle rozhodnutí o migraci.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhovaná akce během procesu migrace

Navrhovaná cesta k migraci a synchronizaci používá kombinaci následujících tří nástrojů. Následující oddíly popisují složitější možnosti migrace a synchronizace, které umožňují širší škálu cílových a zdrojových řešení.

|Možnost migrace|Účel|
|---------|---------|
|[Azure Database Migration Service](https://docs.microsoft.com/sql/dma/dma-overview)|Podporuje online migrace (minimální výpadky) a offline (jednou) škálování na Azure SQL Database spravovanou instanci. Podporuje migraci z: SQL Server 2005, SQL Server 2008 a SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 a SQL Server 2017.|
|[Transakční replikace](https://docs.microsoft.com/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Transakční replikace do spravované instance Azure SQL Database je podporovaná pro migrace z: SQL Server 2012 (SP2 CU8, SP3 nebo novější), SQL Server 2014 (RTM CU10 nebo novější nebo SP1 CU3 nebo novější), SQL Server 2016, SQL Server 2017.|
|[Hromadné načtení](https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql)|Použijte hromadnou zátěž do Azure SQL Database spravované instance pro data uložená v: SQL Server 2005, SQL Server 2008 a SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 a SQL Server 2017.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Doprovodné materiály a kurzy pro navrhovaný proces migrace

Volba nejlepšího návodu k migraci pomocí Azure Database Migration Service je závislá na zdrojové a cílové platformě, kterou si zvolíte. Následující tabulka obsahuje odkazy na kurzy pro každý standardní přístup k migraci SQL Database pomocí Azure Database Migration Service.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|SQL Server|Databáze SQL Azure|Database Migration Service|Offline|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Databáze SQL Azure|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL Database – spravovaná instance|Database Migration Service|Offline|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL Database – spravovaná instance|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server VP|Azure SQL Database (nebo spravovaná instance)|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Doprovodné materiály a kurzy pro různé služby pro ekvivalentní řešení PaaS

Po přesunu databází z instance SQL Server do Azure Database Migration Service se schéma a data dají znovu hostovat v rámci řady řešení PaaS. Na tomto serveru ale můžou pořád běžet jiné požadované služby. Následující tři kurzy vám pomůžou při přesunu SSIS, SSAS a SSRS na ekvivalentní PaaS služby v Azure.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|Služba SSIS (SQL Server Integration Services)|Prostředí Azure Data Factory Integration runtime|Azure Data Factory|Offline|[Kurz](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Services – tabulkový model|Azure Analysis Services|SQL Server Data Tools|Offline|[Kurz](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|SQL Server Reporting Services|Server sestav Power BI|Power BI|Offline|[Kurz](https://docs.microsoft.com/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Doprovodné materiály a kurzy pro migraci z SQL Server do instance služby IaaS of SQL Server

Po migraci databází a služeb do instancí PaaS můžete stále mít datové struktury a služby, které nejsou kompatibilní s PaaS. Pokud stávající omezení brání migraci datových struktur nebo služeb, může vám následující kurz pomáhat při migraci různých prostředků v portfoliu dat do řešení Azure IaaS.

Pomocí tohoto postupu můžete migrovat databáze nebo jiné služby na instanci SQL Server.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|SQL Server jedné instance|SQL Server na IaaS|Řadu|Offline|[Kurz](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Změny procesu optimalizace

Během optimalizace můžete provést testování, optimalizaci a zvýšení úrovně pro každou strukturu dat, službu nebo instanci SQL Server. Toto je největší dopad na odchylku od modelu migrace podle zatížení.

V ideálním případě migrujete závislé úlohy, aplikace a virtuální počítače v rámci stejné iterace jako instance SQL Server. Když dojde k ideálnímu scénáři, můžete otestovat zatížení spolu se zdrojem dat. Po otestování můžete zvýšit úroveň struktury dat na produkční prostředí a proces synchronizace ukončit.

Teď se podíváme na scénář, ve kterém existuje významná časová prodleva mezi migrací databáze a migrací úloh. Bohužel to může být největší změna procesu optimalizace během migrace řízené mimo úlohy. Když migrujete více databází jako součást migrace SQL Server, mohou být tyto databáze v cloudu i v místním prostředí pro více iterací současně. Během této doby je potřeba zachovat synchronizaci dat, dokud nebudou závislé prostředky migrovány, testovány a povýšeny.

Dokud nebudou povýšeny všechny závislé úlohy, váš tým zodpovídá za podporu synchronizace dat ze zdrojového systému do cílového systému. Tato synchronizace spotřebovává šířku pásma sítě, cloudové náklady a nejdůležitější údaje, čas uživatelů. Tato náročná režie může snížit správné zarovnání plánu přijetí v rámci úlohy migrace SQL Server a všech závislých úloh a aplikací.

### <a name="suggested-action-during-the-optimization-process"></a>Navrhovaná akce během procesu optimalizace

Během optimalizačních procesů proveďte každou iteraci následující úkoly, dokud nebudou všechny datové struktury a služby povýšeny na produkční prostředí.

1. Ověří synchronizaci dat.
2. Otestujte všechny migrované aplikace.
3. Optimalizujte strukturu aplikace a dat a vylaďte náklady.
4. Propagujte aplikace na produkční prostředí.
5. Testujte pro pokračující místní provoz v místní databázi.
6. Ukončí synchronizaci všech dat povýšených v produkčním prostředí.
7. Ukončete původní zdrojovou databázi.

Až do kroku 5 projdete, nebudete moci ukončit databáze a synchronizaci. Dokud všechny databáze v instanci SQL Server neprošly všemi sedmi kroky, měli byste s místní instancí SQL Server zacházet jako s produkčním prostředím. Veškerá synchronizace by měla být zachována.

## <a name="next-steps"></a>Další kroky

Vraťte se ke [kontrolnímu seznamu pro rozšířený rozsah](./index.md) a ověřte si, že vaše metoda migrace plně vyhovuje.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
