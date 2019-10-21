---
title: Urychlení migrace pomocí migrace SQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Urychlení migrace pomocí migrace SQL
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4af94af91874ac666f45a917eed003b3cf881c51
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558217"
---
# <a name="accelerate-migration-with-a-sql-migration"></a>Urychlení migrace pomocí migrace SQL

Migrace celých instancí SQL Server může urychlit úsilí migrace úloh. Následující pokyny rozšiřují rozsah [příručky migrace do Azure](../azure-migration-guide/index.md) tím, že migrují SQL Server mimo úsilí zaměřené na úlohy migrace. Tento přístup může naplnit migraci více úloh pomocí jedné migrace na platformě dat.

## <a name="general-scope-expansion"></a>Obecné rozšíření rozsahu

Většina úsilí požadovaná v tomto rozsahu rozšíření proběhne během procesu migrace požadavků, posouzení, migrace a optimalizace.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Je tento rozšířený obor pro vás nejvhodnější?

Doporučený postup, který je popsaný v [Průvodci migrací do Azure](../azure-migration-guide/index.md) , je migrace každé struktury dat spolu s přidruženými úlohami v rámci jedné snahy migrace. Iterativní přístup k migraci omezuje zjišťování, posuzování a další úlohy, které můžou vytvářet blokování a zpomalit vrácení obchodních hodnot.

Některé datové struktury ale můžete migrovat efektivněji prostřednictvím samostatné migrace dat na platformě. Následuje několik příkladů, které mohou vést k použití tohoto rozšířeného rozsahu:

- **Konec služby:** Rychlé přesunutí instance SQL Server, aby se předešlo problémům s koncovými službami, je použití tohoto průvodce mimo standardní úsilí při migraci.
- **SQL Server služby:** Struktura dat je součástí širšího řešení, které vyžaduje SQL Server běžící na virtuálním počítači. To je běžné pro řešení, která využívají SQL Server služby, jako je SQL Server Reporting Services, služba SSIS (SQL Server Integration Services) nebo SQL Server Analysis Services.
- **Vysoce hustota, databáze s nízkým využitím:** SQL Server má vysokou hustotu databází. Každá z těchto databází má nízké objemy transakcí a vyžaduje malé výpočetní prostředky. Měli byste zvážit další moderní řešení, ale přístup k IaaS může vést k výraznému snížení provozních nákladů.
- **Celkové náklady na vlastnictví:** V případě potřeby je možné [využít výhody hybridního využití Azure](https://azure.microsoft.com/pricing/hybrid-benefit) na ceníkové ceny pro SQL servery, které vytvářejí nejnižší náklady na vlastnictví. To je zvlášť běžné pro zákazníky, kteří hostují SQL Server ve scénářích s více cloudy.
- **Akcelerátor migrace:** Migrace navýšení a posunutí instance SQL Server může přesunout několik databází v jedné iteraci. Tento přístup někdy umožňuje budoucím iteracím lépe se zaměřit na aplikace a virtuální počítače a migrovat více úloh v rámci jedné iterace.
- **Migrace VMware:** Společná místní architektura zahrnuje aplikace a virtuální počítače na virtuálním hostiteli a databázích na holém počítači. Při migraci této společné architektury se v této příručce může vyhodnotit migrace hostitele VMWare do Azure VMWare Service (AVS), která umožňuje migrovat celé SQL Server instance, aby podporovaly tyto virtuální hostitele. Pokyny pro bezplatné informace najdete v tématu [migrace hostitele VMware](./vmware-host.md).

Pokud se u této migrace neuplatní žádné z výše uvedených kritérií, může být nejlepší pokračovat se [standardním procesem migrace](../index.md). Ve standardním procesu se datové struktury migrují postupně spolu s jednotlivými úlohami.

Pokud tato příručka zarovnává s vašimi kritérii, pokračujte v tomto rozšířeném průvodci oboru jako úsilí v rámci [standardního procesu migrace](../index.md). Během fáze předpoklady se úsilí dá integrovat do celkového plánu přijetí.

## <a name="suggested-prerequisites"></a>Doporučené požadavky

Před provedením SQL Server migrace začněte s rozšířením **digitální nemovitosti** tím, že zahrnete datovou nemovitost. V datovém majetku se zaznamenávají inventáře datových assetů, které se považují za migraci. Následující tabulky popisují přístup k záznamu majetku.

### <a name="server-inventory"></a>Inventář serverů

Následuje příklad inventáře serverů pro SQL Server:

|SQL Server|Účel|Version|[Závažnost](../../manage/considerations/criticality.md)|[Hlediska](../../govern/policy-compliance/data-classification.md)|Počet databází|SSIS|SSRS|SSAS|Cluster|Počet uzlů|
|---------|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|Základní aplikace|2016|Kritická poslání|Vysoce důvěrné|40|Nevztahuje se|Nevztahuje se|Nevztahuje se|Ano|3|
|SQL-02|Základní aplikace|2016|Kritická poslání|Vysoce důvěrné|40|Nevztahuje se|Nevztahuje se|Nevztahuje se|Ano|3|
|SQL-03|Základní aplikace|2016|Kritická poslání|Vysoce důvěrné|40|Nevztahuje se|Nevztahuje se|Nevztahuje se|Ano|3|
|SQL – 04|BI|2012|Vysoký|CZK|6|Nevztahuje se|Přehled|Ano – multidimenzionální datová krychle|Ne|1\. místo|
|SQL-05|Integrace|2008 R2|Nízký|Obecné|20|Ano|Nevztahuje se|Nevztahuje se|Ne|1\. místo|

### <a name="database-inventory"></a>Inventář databáze

Následuje příklad inventáře databáze pro jeden z výše uvedených serverů SQL:

|Server|Databáze|[Závažnost](../../manage/considerations/criticality.md)|[Hlediska](../../govern/policy-compliance/data-classification.md)|Výsledky DMA|Řešení potíží s DMA|Cílová platforma|
|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|DB-1|Kritická poslání|Vysoce důvěrné|Kompatibility|Nevztahuje se|Azure SQL Database|
|SQL-01|DB-2|Vysoký|Přehled|Je vyžadována Změna schématu.|Změny implementovány|Azure SQL Database|
|SQL-01|DB-1|Vysoký|Obecné|Kompatibility|Nevztahuje se|Spravovaná instance Azure SQL|
|SQL-01|DB-1|Nízký|Vysoce důvěrné|Je vyžadována Změna schématu.|Naplánované změny|Spravovaná instance Azure SQL|
|SQL-01|DB-1|Kritická poslání|Obecné|Kompatibility|Nevztahuje se|Spravovaná instance Azure SQL|
|SQL-01|DB-2|Vysoký|Přehled|Kompatibility|Nevztahuje se|Azure SQL Database|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrace s plánem přijetí do cloudu

Po dokončení zjišťování můžete plán zahrnout do [plánu přijetí do cloudu](../../plan/template.md). V rámci plánu přijetí do cloudu přidejte každou instanci SQL Server, kterou chcete migrovat, jako samostatnou [úlohu](../../plan/workloads.md). V rámci každé úlohy je možné jednotlivé databáze a služby (SSIS, SSAS, SSRS) přidat jako [prostředky](../../plan/workloads.md). Chcete-li přidat úlohy a prostředky hromadně do plánu přijetí, přečtěte si téma [Přidání a úprava pracovních položek v aplikaci Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Po zahrnutí úloh a prostředků do plánu může tým pokračovat se standardním procesem migrace s využitím plánu přijetí k seznámení s úsilím. Když se tým přijetí přesune do procesů hodnocení, migrace a optimalizace, měly by se v rámci úsilí přihlédnout k následujícím změnám.

## <a name="assessment-process-changes"></a>Změny procesu posouzení

Pokud je možné každou databázi v plánu migrovat na datovou platformu PaaS (Platform as a Service), použijte k vyhodnocení kompatibility vybrané databáze Data Migration Assistant. Pokud databáze vyžaduje převody schématu, doporučujeme, abyste tyto převody dokončili v rámci procesu hodnocení, aby nedošlo k přerušení kanálu migrace.

### <a name="suggested-action-during-the-assessment-process"></a>Navrhovaná akce během procesu posouzení

Pro databáze, které je možné migrovat do řešení PaaS, by se během procesu hodnocení dokončily následující akce.

- **Vyhodnotit pomocí Data Migration Assistant:** Pomocí Data Migration Assistant můžete detekovat problémy s kompatibilitou, které mohou ovlivnit funkčnost databáze v cílové Azure SQL Database spravované instance, doporučit vylepšení výkonu a spolehlivosti a přesunout schéma, data a neobsažené objekty. ze zdrojového serveru na cílový server. Další informace najdete v tématu [Data Migration Assistant](/sql/dma/dma-overview).
- **Opravit a převést:** Na základě výstupu Data Migration Assistant převeďte zdrojové schéma dat, aby bylo možné problémy s kompatibilitou opravit. Otestujte schéma převedených dat pomocí závislých aplikací.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Během migrace existuje více možností nástroje a přístupu. Každý přístup ale následuje jednoduchý proces: migrace schématu, dat a objektů. Synchronizovat data s cílovým zdrojem dat.

Cíl a zdroj datových struktur a služeb můžou tyto dva kroky udělat raději. V následujících částech najdete informace o nejvhodnějším výběru podle rozhodnutí o migraci.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhovaná akce během procesu migrace

Navrhovaná cesta k migraci a synchronizaci používá kombinaci následujících tří nástrojů. Následující oddíly popisují složitější možnosti migrace a synchronizace, které umožňují širší škálu cílových a zdrojových řešení.

|Možnost migrace|Účel|
|---------|---------|
|[Azure Database Migration Service](/sql/dma/dma-overview)|Azure DMS podporuje online (minimální výpadky) a offline (jednorázové) migrace ve velkém měřítku na Azure SQL Database Managed instance z SQL Server 2005, SQL Server 2008 a SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 a SQL Server 2017.|
|[Transakční replikace](/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Transakční replikace do spravované instance Azure SQL Database je podporovaná pro migrace z: SQL Server 2012 (SP2 CU8, SP3 nebo novější), SQL Server 2014 (RTM CU10 nebo novější nebo SP1 CU3 nebo novější), SQL Server 2016, SQL Server 2017|
|[Hromadné načtení](/sql/t-sql/statements/bulk-insert-transact-sql)|Pro data uložená v SQL Server 2005, SQL Server 2008 a SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 a SQL Server 2017 použijte hromadnou zátěž pro Azure SQL Database spravovanou instanci.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Doprovodné materiály a kurzy pro navrhovaný proces migrace

Výběr nejvhodnějších pokynů pro migraci pomocí DMS závisí na zdrojové a cílové platformě, kterou si zvolíte. V následující tabulce jsou popsány kurzy pro každý standardní přístup k migraci databáze SQL pomocí DMS.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|DMS|Stav|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Stav|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server VP|Azure SQL Database (nebo spravovaná instance)|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Doprovodné materiály a kurzy pro různé služby pro ekvivalentní řešení PaaS

Po přesunu databází z SQL serveru do DMS se dá schéma a data znovu hostovat v rámci řady řešení PaaS. Na tomto serveru ale můžou pořád běžet jiné požadované služby. Následující tři kurzy vám pomůžou při přesunu SSIS, SSAS a SSRS na ekvivalentní PaaS služby v Azure.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|Služba SQL Server Integration Service|Data Factory Integration Runtime|Azure Data Factory|Stav|[Kurz](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|Služba Analysis Services SQL Server – tabulkový model|Služba Azure Analysis|SSDT|Stav|[Kurz](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|Služba SQL Server Reporting Service|Power BI Server pro sestavy|Power BI|Stav|[Kurz](/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Doprovodné materiály a kurzy pro migraci z SQL Server do instance služby IaaS of SQL Server

Po migraci databází a služeb do instancí PaaS může stále docházet k datovým strukturám a službám, které nejsou kompatibilní s PaaS. Pokud stávající omezení brání migraci datových struktur nebo služeb, může vám následující kurz pomáhat při migraci různých prostředků v portfoliu dat do řešení Azure IaaS.

Tento přístup se dá použít k migraci databází na SQL Server nebo jiných službách spuštěných ve zdrojovém SQL serveru.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|SQL Server jedné instance|SQL Server na IaaS|Řadu|Stav|[Kurz](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Změny procesu optimalizace

Během optimalizace je možné každou strukturu dat, službu nebo instanci SQL Server testovat, optimalizovat a zvýšit na produkční prostředí. Toto je největší dopad na odchylku od modelu migrace úloh.

V ideálním případě se závislé úlohy, aplikace a virtuální počítače migrují v rámci stejné iterace jako instance SQL Server. V případě, že k tomuto ideálnímu scénáři dojde, lze zatížení testovat spolu se zdrojem dat. Po otestování se datová struktura dá zvýšit na produkční prostředí a proces synchronizace může být ukončený.

Největší změnou procesu optimalizace během migrace s neřízenými úlohami bohužel přichází v případě, že mezi migrací databáze a migrací zatížení je významná časová prodleva. Když se v rámci migrace SQL Server migruje víc databází, můžou se tyto databáze v cloudu i v místním prostředí pro několik iterací koexistovat. Během tohoto časového období je nutné zachovat synchronizaci dat, dokud nebudou závislé prostředky migrovány, testovány a povýšeny.

Dokud nebudou povýšeny všechny závislé úlohy, tým bude zodpovědný za podporu synchronizace dat ze zdrojového systému do cílového systému. Tato synchronizace spotřebovává šířku pásma sítě, cloudové náklady a nejvýznamnější a nejdůležitější dobu potřebnou pro obyvatele. Tato náročná režie se omezí řádným zarovnáním plánu přijetí v rámci úlohy migrace SQL Server a všech závislých úloh nebo aplikací.

### <a name="suggested-action-during-the-optimization-process"></a>Navrhovaná akce během procesu optimalizace

Během procesu optimalizace by se měly všechny tyto úlohy dokončit v každé iteraci, dokud se všechny datové struktury a služby nezvýší na produkční prostředí.

1. Ověří synchronizaci dat.
2. Otestujte všechny migrované aplikace.
3. Optimalizujte strukturu aplikace a dat a vylaďte náklady.
4. Propagujte aplikace na produkční prostředí.
5. Testujte pro pokračující místní provoz v místní databázi.
6. Ukončí synchronizaci všech dat povýšených v produkčním prostředí.
7. Ukončete původní zdrojovou databázi.

Dokud krok 5 projde, databáze a synchronizace se nedají ukončit. Dokud všechny databáze v SQL Server neprošly kroky 1-7, místní SQL Server by se měla považovat za produkční prostředí a musí se zachovat veškerá synchronizace.

## <a name="next-steps"></a>Další kroky

Vraťte se ke [kontrolnímu seznamu pro rozšířený rozsah](./index.md) a ověřte si, že vaše metoda migrace plně vyhovuje.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
