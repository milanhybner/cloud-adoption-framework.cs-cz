---
title: Strategie migrace aplikací pro sálové počítače
description: Naučte se strategie, jako je opětovné hostování, vyřazení, opětovné sestavení nebo nahrazení aplikací pro migraci z sálových prostředí do Azure.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 52dbbd594a95f86c1bdb49ac76a7b178d8a71b13
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171408"
---
# <a name="mainframe-application-migration"></a>Migrace mainframových aplikací

Když migrujete aplikace z sálových prostředí do Azure, většina týmů bude postupovat podle toho, co je to možné, kdykoliv a kdykoli je to možné, a pak zahájit postupné nasazení, kde se aplikace přepíší nebo nahradí.

Migrace aplikací obvykle zahrnuje jednu nebo více následujících strategií:

- Opětovné **hostování:** Můžete přesunout existující kód, programy a aplikace z sálového počítače a potom znovu zkompilovat kód pro spuštění v emulátoru sálového počítače hostovaném v instanci cloudu. Tento přístup obvykle začíná přesunem aplikací do cloudového emulátoru a pak migruje databázi do cloudové databáze. U dat a převodů souborů se vyžadují některé strojírenství a refaktoring.

    Alternativně můžete znovu hostovat s použitím tradičního poskytovatele hostingu. Jednou z hlavních výhod cloudu je správa infrastruktury. Můžete najít poskytovatele Datacenter, který bude hostovat vaše úlohy vašeho sálového počítače. Tento model může koupit čas, snížit zámek dodavatele v a vydávat průběžné úspory nákladů.

- **Vyřadit z provozu:** Všechny aplikace, které už nepotřebujete, by měly být před migrací vyřazené.

- **Znovu sestavit:** Některé organizace mají možnost zcela přepsát programy pomocí moderních technik. S ohledem na zvýšení nákladů a složitost tohoto přístupu není to tak běžné jako přístup výtahu a posunutí. Často po tomto typu migrace dává smysl začít nahrazovat moduly a kód pomocí transformačních modulů kódu.

- **Nahradit:** Tento přístup nahrazuje sálové funkce pomocí ekvivalentních funkcí v cloudu. Software jako služba (SaaS) je jedna možnost, která používá řešení vytvořené speciálně pro podnikovou práci, jako jsou finance, lidské zdroje, výroba nebo plánování podnikových zdrojů. Kromě toho je teď k dispozici mnoho aplikací specifických pro konkrétní odvětví pro řešení problémů, které vlastní Sálová řešení používala k předchozímu řešení.

Měli byste zvážit, že naplánujete úlohy, které chcete zpočátku migrovat, a pak určíte tyto požadavky na přesun přidružených aplikací, starších základů kódu a databází.

## <a name="mainframe-emulation-in-azure"></a>Emulace sálového počítače v Azure

Azure Cloud Services můžou emulovat tradiční Sálová prostředí, takže můžete znovu použít stávající kód a aplikace pro sálové počítače. Mezi běžné serverové součásti, které je možné emulovat, patří systémy OLTP (online Transaction Processing), Batch a ingestování dat.

### <a name="oltp-systems"></a>Systémy OLTP

Mnoho sálových počítačů má OLTP systémy, které zpracovávají tisíce nebo miliony aktualizací pro velký počet uživatelů. Tyto aplikace často používají zpracování transakcí a software pro zpracování obrazovky, jako je CICS (Customer Information Control System), systémy pro správu informací (IMS) a procesor terminálových rozhraní (TIP).

Při přesouvání OLTPch aplikací do Azure jsou emulátory pro monitorování transakčního zpracování transakcí (TP) k dispozici pro spuštění jako infrastruktura jako služba (IaaS) pomocí virtuálních počítačů v Azure. Funkce pro zpracování obrazovky a formuláře mohou být implementovány také webovými servery. Tento přístup je možné kombinovat s databázovými API, jako jsou objekty ADO (ActiveX Data Objects), rozhraní ODBC (Open Database Connectivity) a připojení k databázi Java (JDBC) pro přístup k datům a transakce.

### <a name="time-constrained-batch-updates"></a>Časově omezené aktualizace dávek

Mnoho sálových systémů provádí měsíční nebo roční aktualizace milionů záznamů účtů, jako jsou ty, které se používají v bankovnictví, pojišťovnictví a státní správě. Sálové počítače zpracovávají tyto typy úloh tím, že nabízejí systémy pro zpracování dat s vysokou propustností. Dávkové úlohy pro sálové počítače jsou obvykle sériové a závisí na počtu vstupně-výstupních operací za sekundu (IOPS) poskytovaných páteřním základem pro výkon.

Cloudová prostředí Batch využívají paralelní výpočetní a vysokorychlostní sítě pro výkon. Pokud potřebujete optimalizovat výkon služby Batch, Azure nabízí různé možnosti COMPUTE, úložiště a sítě.

### <a name="data-ingestion-systems"></a>Systémy přijímání dat

Sálové počítače ingestují velké dávky dat z maloobchodních, finančních služeb, výroby a dalších řešení pro zpracování. V Azure můžete k kopírování dat do a z umístění úložiště použít jednoduché nástroje příkazového řádku, jako je [AzCopy](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy) . Můžete také použít službu [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/introduction) , která vám umožní ingestovat data z různorodých úložišť dat a vytvářet a plánovat pracovní postupy řízené daty.

Kromě prostředí emulace poskytuje Azure platformu jako službu (PaaS) a analytické služby, které mohou rozšiřovat stávající Sálová prostředí.

## <a name="migrate-oltp-workloads-to-azure"></a>Migrace úloh OLTP do Azure

Přístup ke zvedání a posunu je možnost bez kódu pro rychlou migraci stávajících aplikací do Azure. Každá aplikace je migrována tak, jak je, což přináší výhody cloudu bez rizik nebo nákladů na provádění změn kódu. Tento přístup podporuje použití emulátoru pro monitorování TRANSAKČNÍho zpracování transakcí v Azure.

Monitory TP jsou k dispozici od různých dodavatelů a běží na virtuálních počítačích, jako je možnost infrastruktura jako služba (IaaS) v Azure. Následující diagramy před a po ukazují migraci online aplikace, kterou zajišťuje IBM DB2, systému správy relačních databází (DBMS) v rámci sálového počítače IBM z/OS. DB2 pro z/OS používá k ukládání dat a indexovaného sekvenčního přístupu (ISAM) pro ploché soubory (VSAM) soubory metody přístupu k virtuálnímu úložišti. Tato architektura také používá CICS pro monitorování transakcí.

!["Zvednutí a posunutí" migrace sálového prostředí do Azure pomocí softwaru pro emulaci](../../_images/mainframe-migration/mainframe-vs-azure.png)

V Azure se prostředí emulace používají ke spuštění Správce TRANSAKČNÍho programu a dávkových úloh, které používají JCL. V datové vrstvě je DB2 nahrazuje [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), i když je možné použít také Microsoft SQL Server, DB2 LUW nebo Oracle Database. Emulátor podporuje rychlé zprávy, VSAM a SEQ. Nástroje pro správu systému z sálového počítače jsou nahrazené službami Azure a softwarem od jiných dodavatelů, kteří se spouštějí na virtuálních počítačích.

Funkce pro zpracování obrazovky a zadávání formulářů se běžně implementují pomocí webových serverů, které se dají kombinovat s databázovými rozhraními API, jako jsou ADO, ODBC a JDBC, pro přístup k datům a transakce. Přesné řádky komponent Azure IaaS, které se mají použít, závisí na operačním systému, který dáváte přednost. Příklad:

- Virtuální počítače založené na Windows: Internet Information Server (IIS) spolu s ASP.NET pro zpracování obrazovky a obchodní logiku. Použijte ADO.NET pro přístup k datům a transakce.

- Virtuální počítače se systémem Linux: aplikační servery založené na jazyce Java, které jsou k dispozici, například Apache Tomcat pro zpracování obrazovky a obchodní funkce založené na jazyce Java. Použijte JDBC pro přístup k datům a transakce.

## <a name="migrate-batch-workloads-to-azure"></a>Migrace úloh služby Batch do Azure

Operace dávkového zpracování v Azure se liší od typického prostředí Batch na sálových počítačích. Dávkové úlohy sálového počítače jsou obvykle sériové a závisí na počtu IOPS poskytovaných páteřním základem pro výkon. Cloudová prostředí Batch využívají paralelní výpočetní a vysokorychlostní sítě pro výkon.

Pokud chcete optimalizovat výkon služby Batch pomocí Azure, zvažte možnosti [výpočtů](https://docs.microsoft.com/azure/virtual-machines/windows/overview), [úložiště](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction), [sítě](https://azure.microsoft.com/blog/maximize-your-vm-s-performance-with-accelerated-networking-now-generally-available-for-both-windows-and-linux)a [monitorování](https://docs.microsoft.com/azure/azure-monitor/overview) podle následujících pokynů.

### <a name="compute"></a>Compute

Použije

- Virtuální počítače s nejvyšší taktovou rychlostí. Sálové aplikace jsou často s jedním vláknem a sálové procesory mají velmi vysokou rychlost.

- Virtuální počítače s velkou kapacitou paměti umožňující ukládání dat a pracovních oblastí aplikace do mezipaměti.

- Virtuální počítače s vyšší hustotou vCPU, aby využívaly vícevláknové zpracování, pokud aplikace podporuje více vláken.

- Paralelní zpracování, protože Azure se snadno škáluje pro paralelní zpracování a poskytuje více výpočetní výkon pro dávkovou práci.

### <a name="storage"></a>Úložiště

Použije

- [Azure Premium SSD](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage) nebo [Azure Ultra SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-ultra-ssd) pro maximální počet dostupných IOPS.

- Prokládání více disků za účelem většího počtu IOPS na velikost úložiště.

- Vytváření oddílů pro úložiště pro rozprostření v/v přes několik zařízení úložiště Azure.

### <a name="networking"></a>Sítě

- K minimalizaci latence použijte [urychlené síťové sítě Azure](https://docs.microsoft.com/azure/virtual-network/create-vm-accelerated-networking-powershell) .

### <a name="monitoring"></a>Monitorování

- Pomocí nástrojů pro monitorování, [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview), [Azure Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview)a dokonce i v protokolech Azure můžete správcům umožnit monitorovat jakýkoli výkon dávkových běhů a vyhnout se kritickým bodům.

## <a name="migrate-development-environments"></a>Migrace vývojových prostředí

Distribuované architektury cloudu spoléhají na jinou sadu vývojářských nástrojů, které poskytují výhody moderních postupů a programovacích jazyků. Pro usnadnění tohoto přechodu můžete použít vývojové prostředí s jinými nástroji, které jsou určeny k emulaci prostředí IBM z/OS. V následujícím seznamu jsou uvedeny možnosti od společnosti Microsoft a jiných dodavatelů:

| Komponenta        | Možnosti Azure                                                                                                                                  |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| z/OS             | Windows, Linux nebo UNIX                                                                                                                      |
| CICS             | Služby Azure nabízené společností Micro Focus, Oracle, GT software (Fujitsu), TmaxSoft, Raincode a NTT data nebo přepište pomocí Kubernetes |
| IMS              | Služby Azure, které nabízí Micro Focus a Oracle                                                                                  |
| Pracovník        | Služby Azure z Raincode a TmaxSoft; nebo COBOL, C nebo Java nebo namapujte na funkce operačního systému               |
| JCL              | JCL, PowerShell nebo jiné nástroje pro skriptování                                                                                                   |
| COBOL            | COBOL, C nebo Java                                                                                                                            |
| Len          | Přírodní, COBOL, C nebo Java                                                                                                                  |
| FORTRAN a PL/I | FORTRAN, PL/I, COBOL, C nebo Java                                                                                                           |
| REXX a PL/I    | REXX, PowerShell nebo jiné nástroje pro skriptování                                                                                                  |

## <a name="migrate-databases-and-data"></a>Migrace databází a dat

Migrace aplikace obvykle zahrnuje opětovné hostování datové vrstvy. Můžete migrovat SQL Server, open source a další relační databáze na plně spravovaná řešení v Azure, jako je například [Azure SQL Database Managed instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), [Azure Database Service for PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview)a [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) s [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).

Můžete například migrovat, pokud Datová vrstva sálového počítače používá:

- Databázi IBM DB2 nebo databáze IMS použijte Azure SQL Database, SQL Server, DB2 LUW nebo Oracle Database v Azure.

- VSAM a další ploché soubory, pro Azure SQL, SQL Server, DB2 LUW nebo Oracle používejte indexované soubory s použitím indexovaných sekvenčních přístupových metod (ISAM).

- Skupiny datumů generace (GDGs), migrujte na soubory v Azure, které používají zásady vytváření názvů a přípony názvů souborů, které poskytují podobnou funkci GDGs.

Datová vrstva IBM zahrnuje několik klíčových součástí, které je nutné také migrovat. Když například migrujete databázi, migrujete také kolekci dat obsažených ve fondech, z nichž každá obsahuje dbextents, která jsou VSAM sady dat z/OS. Migrace musí zahrnovat adresář, který identifikuje umístění dat ve fondech úložiště. Plán migrace musí také zvážit protokol databáze, který obsahuje záznam o operacích provedených v databázi. Databáze může mít jednu, dvě (duální nebo alternativní) nebo čtyři (duální a alternativní) protokoly.

Migrace databáze zahrnuje i tyto součásti:

- **Správce databáze:** Poskytuje přístup k datům v databázi. Správce databáze běží ve vlastním oddílu v prostředí z/OS.
- **Žadatel o aplikaci:** Akceptuje žádosti od aplikací před jejich předáním aplikačnímu serveru.
- **Online adaptér prostředků:** Zahrnuje součásti žadatele aplikace pro použití v transakcích CICS.
- **Adaptér prostředků Batch:** Implementuje součásti žadatele aplikace pro dávkové aplikace z/OS.
- **Interaktivní SQL (ISQL):** Spouští se jako aplikace CICS a rozhraní, které umožňuje uživatelům zadat příkazy SQL nebo příkazy operátoru.
- **CICS aplikace:** Spouští se pod kontrolou CICS pomocí dostupných prostředků a zdrojů dat v CICS.
- **Aplikace Batch:** Spustí logiku procesu bez interaktivní komunikace s uživateli, například vytvoří hromadnou aktualizaci dat nebo generuje sestavy z databáze.

## <a name="optimize-scale-and-throughput-for-azure"></a>Optimalizace škálování a propustnosti pro Azure

Obecně řečeno, sálové počítače se škálují nahoru, zatímco Cloud škáluje. Pro optimalizaci škálování a propustnosti aplikací pro sálové počítače, které běží na Azure, je důležité pochopit, jak můžou sálové počítače oddělit a izolovat aplikace. V rámci sálového počítače z/OS používá funkce označované jako logické oddíly (LPARS) k izolaci a správě prostředků konkrétní aplikace v jediné instanci.

Například sálové počítače můžou používat jeden logický oddíl (LPAR) pro oblast CICS s přidruženými COBOL programy a samostatné LPAR pro DB2. Další LPARs se často používají pro vývoj, testování a přípravná prostředí.

V Azure je obvyklejší používat k tomuto účelu samostatné virtuální počítače. Architektury Azure obvykle nasazují virtuální počítače pro aplikační vrstvu, samostatnou sadu virtuálních počítačů pro datovou vrstvu, další sadu pro vývoj a tak dále. Jednotlivé úrovně zpracování je možné optimalizovat pomocí nejvhodnějšího typu virtuálních počítačů a funkcí pro toto prostředí.

Kromě toho může každá úroveň také poskytovat vhodné služby pro zotavení po havárii. Například provozní a databázové virtuální počítače mohou vyžadovat rychlé obnovení nebo zahřívání, zatímco virtuální počítače pro vývoj a testování podporují studenou obnovu.

Následující obrázek ukazuje možné nasazení Azure pomocí primární a sekundární lokality. V primární lokalitě se produkční, pracovní a testovací virtuální počítače nasazují s vysokou dostupností. Sekundární lokalita je určena pro zálohování a zotavení po havárii.

![Možné nasazení Azure pomocí primární a sekundární lokality](../../_images/mainframe-migration/migration-backup-dr.png)

## <a name="perform-a-staged-mainframe-to-azure"></a>Provedení dvoufázové sálového počítače do Azure

Přesunutí řešení z sálového počítače do Azure může zahrnovat *dvoufázové* migrace, při které se některé aplikace přesunou jako první, a jiné zůstávají na sálovém počítači dočasně nebo trvale. Tento přístup obvykle vyžaduje systémy, které aplikacím a databázím umožňují vzájemnou spolupráci mezi sálovými a Azure.

Běžným scénářem je přesun aplikace do Azure a zachování dat používaných aplikací na sálovém počítači. Konkrétní software se používá k tomu, aby aplikace v Azure měly přístup k datům z sálového počítače. V rámci široké škály řešení je zajištěna integrace mezi Azure a stávajícími sálovými prostředími, Podpora hybridních scénářů a migrace v průběhu času. Na svou cestu vám může pomáhat partneři Microsoftu, nezávislí dodavatelé softwaru a systémové integrátory.

Jednou z možností je [Microsoft Host Integration Server](https://docs.microsoft.com/host-integration-server), řešení, které poskytuje architekturu distribuované relační databáze (DRDA), která se vyžaduje pro aplikace v Azure pro přístup k datům v DB2, která zůstávají na sálovém počítači. Další možnosti pro integraci z sálového počítače do Azure zahrnují řešení od IBM, Attunity, Codit, dalších dodavatelů a možností open source.

## <a name="partner-solutions"></a>Partnerská řešení

Pokud zvažujete migraci v rámci sálového počítače, máte k dispozici partnerský ekosystém, který vám pomůže.

Azure poskytuje prověřenou, vysoce dostupnou a škálovatelnou infrastrukturu pro systémy, které se aktuálně spouštějí na sálových počítačích. Některé úlohy je možné migrovat pomocí relativního snadného. Další úlohy, které závisí na starším systémovém softwaru, jako je CICS a IMS, se dají znovu hostovat pomocí partnerských řešení a migrovat do Azure v čase. Bez ohledu na to, jakou možnost provedete, jsou k dispozici Microsoft a naši partneři, které vám pomůžou s optimalizací pro Azure při údržbě funkcí softwaru sálového počítače.

## <a name="learn-more"></a>Další informace

Další informace najdete v následujících zdrojích:

- [Začínáme s Azure](https://docs.microsoft.com/azure)

- [Nasazení IBM DB2 pureScale v Azure](https://azure.microsoft.com/resources/deploy-ibm-db2-purescale-on-azure)

- [Dokumentace k Host Integration Server](https://docs.microsoft.com/host-integration-server)
