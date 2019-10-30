---
title: Migrace prostředků
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrace prostředků
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 345811e62442341091cf91b3e52870ec454784bf
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549253"
---
# <a name="migrate-assets-infrastructure-apps-and-data"></a>Migrace prostředků (infrastruktury, aplikací a dat)

V této fázi použijete výstup z fáze posouzení a zahájíte migraci prostředí. Tento návod vám pomůže identifikovat vhodné nástroje pro dosažení stavu „hotovo“, včetně nativních nástrojů, nástrojů třetích stran a nástrojů pro správu projektů.

<!-- markdownlint-disable MD025 -->

# <a name="native-migration-toolstabtools"></a>[Nativní nástroje pro migraci](#tab/Tools)

V následujících oddílech jsou popsané nativní nástroje Azure, které jsou k dispozici pro provedení migrace nebo které s ní můžou pomoct. Informace o volbě správných nástrojů, které podporují migraci, najdete v [průvodci rozhodováním o migračních nástrojích pro architekturu přechodu na cloud](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Služba Azure Migrate poskytuje jednotné a rozšiřitelné prostředí pro migraci. Služba Azure Migrate poskytuje centrální, vyhrazené prostředí pro sledování migrace v rámci fází posuzování a migrace do Azure. Nabízí možnost používat nástroje podle vašeho výběru a sledovat průběh migrace v rámci těchto nástrojů.

Služba Azure Migrate poskytuje následující funkce:

1. Rozšířené možnosti posuzování a migrace:
    - Posouzení počítačů Hyper-V
    - Vylepšené posouzení počítačů VMware
    - Migrace virtuálních počítačů VMware do Azure bez agentů
1. Sjednocené posouzení, migrace a sledování průběhu
1. Rozšiřitelný přístup s integrací nezávislých výrobců softwaru (například Cloudamize)

Pokud chcete provést migraci pomocí služby Azure Migrate, postupujte následovně:

1. Vyberte **Všechny služby** a vyhledejte Azure Migrate. Pokračujte výběrem položky **Azure Migrate**.
1. Zahajte projekt migrace tak, že vyberete **Přidat nástroj**.
1. Vyberte předplatné, skupinu prostředků a geografii pro hostování migrace.
1. Zvolte **Vybrat nástroj pro posouzení** > **Azure Migrate: Server Assessment** >  **Další**.
1. Vyberte **Zkontrolovat a přidat nástroje** a ověřte konfiguraci. Kliknutím na **Přidat nástroje** spusťte úlohu pro vytvoření projektu migrace a zaregistrování vybraných řešení.

<!-- TODO: TBA -->

### <a name="read-more"></a>Další informace

- [Kurz služby Azure Migrate – Migrace fyzických nebo virtualizovaných serverů do Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)

## <a name="azure-site-recovery"></a>Azure Site Recovery

Služba Azure Site Recovery může spravovat migraci místních prostředků do Azure. Může také spravovat a orchestrovat zotavení po havárii pro místní počítače a virtuální počítače Azure pro účely provozní kontinuity a zotavení po havárii (BCDR).

Následující kroky popisují obecný proces použití Site Recovery k migraci:

> [!TIP]
> V závislosti na vašem scénáři se tyto kroky můžou mírně lišit. Další informace najdete v článku [Migrace místních počítačů do Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure).

### <a name="prepare-azure-site-recovery-service"></a>Příprava služby Azure Site Recovery

1. Na webu Azure Portal vyberte **+Vytvořit prostředek > Nástroje pro správu > Backup a Site Recovery**.
1. Pokud jste si ještě nevytvořili trezor pro obnovení, vytvořte pomocí průvodce prostředek **Trezor služby Recovery Services**.
1. V nabídce **Prostředek** vyberte **Site Recovery > Připravit infrastrukturu > Cíl ochrany**.
1. V části **Cíl ochrany** vyberte, co chcete migrovat.
    1. **VMware:** Vyberte **Do Azure > Ano, pomocí VMware vSphere Hypervisoru**.
    1. **Fyzický počítač:** Vyberte **Do Azure > Nevirtualizované nebo jiné**.
    1. **Hyper-V:** Vyberte **Do Azure > Ano, pomocí Hyper-V**. Pokud jsou virtuální počítače Hyper-V spravované nástrojem VMM, vyberte **Ano**.

### <a name="configure-migration-settings"></a>Konfigurace nastavení migrace

1. Podle potřeby nastavte zdrojové prostředí.
1. Nastavte cílové prostředí.
    1. Klikněte na **Připravit infrastrukturu > Cíl** a vyberte předplatné Azure, které chcete použít.
    1. Zadejte model nasazení Resource Manager.
    1. Site Recovery zkontroluje, že máte minimálně jednu kompatibilní síť a účet úložiště Azure.
1. Nastavte zásadu replikace.
1. Povolte replikaci.
1. Spusťte zkušební migraci (zkušební převzetí služeb).

### <a name="migrate-to-azure-using-failover"></a>Migrace do Azure pomocí převzetí služeb

1. V části **Nastavení > Replikované položky** vyberte počítač a pak **Převzetí služeb při selhání**.
1. V části **Převzetí služeb při selhání** vyberte **Bod obnovení**, ke kterému se mají převzít služby při selhání. Vyberte nejnovější bod obnovení.
1. Podle potřeby nakonfigurujte nastavení šifrovacího klíče.
1. Vyberte **Před spuštěním převzetí služeb při selhání vypnout počítač**. Služba Site Recovery se před aktivací převzetí služeb pokusí vypnout virtuální počítače. Převzetí služeb při selhání bude pokračovat i v případě, že se vypnutí nepovede. Průběh převzetí služeb můžete sledovat na stránce Úlohy.
1. Zkontrolujte, že se virtuální počítač Azure zobrazuje v Azure podle očekávání.
1. V části **Replikované položky** klikněte pravým tlačítkem na virtuální počítač a zvolte **Dokončit migraci**.
1. Podle potřeby proveďte kroky po migraci (podle relevantních informací v tomto návodu).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.RecoveryServices]" submitText="Create a Recovery Services vault" :::

::: zone-end

::: zone target="docs"

Další informace naleznete v tématu:

- [Migrace místních počítačů do Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure)

::: zone-end

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service (DMS) je plně spravovaná služba, která umožňuje bezproblémovou migraci z více databázových zdrojů na datové platformy Azure s minimální dobou vyřazení z provozu (online migrace). Azure Database Migration Service provede všechny požadované kroky. Projekty migrace můžete iniciovat s jistotou, že proces bude využívat osvědčené postupy doporučené Microsoftem.

### <a name="create-an-azure-database-migration-service-instance"></a>Vytvoření instance služby Azure Database Migration Service

Pokud službu Azure Database Migration Service používáte poprvé, budete muset zaregistrovat poskytovatele prostředků pro své předplatné Azure:

1. Vyberte **Všechny služby**, potom **Předplatná** a zvolte cílové předplatné.
1. Vyberte **Poskytovatelé prostředků**.
1. Vyhledejte klíčové slovo `migration` a pak napravo od **Microsoft.DataMigration** vyberte **Zaregistrovat**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

Po registraci poskytovatele prostředků můžete vytvořit instanci služby Azure Database Migration Service.

1. Vyberte **+Vytvořit prostředek** a na Marketplace vyhledejte **Azure Database Migration Service**.
1. Dokončete **průvodce vytvořením služby migrace** a vyberte **Vytvořit**.

Služba je teď připravená migrovat podporované zdrojové databáze (například SQL Server, MySQL, PostgreSQL nebo MongoDb).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Další informace naleznete v tématu:

- [Přehled služby Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview)
- [Vytvoření instance služby Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal)
- [Služba Azure Migrate na webu Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade)
- [Azure Portal: Vytvoření projektu migrace](https://portal.azure.com/#create/Microsoft.AzureMigrate)

::: zone-end

## <a name="data-migration-assistant"></a>Data Migration Assistant

Nástroj Data Migration Assistant (DMA) pomáhá s upgradem na moderní datovou platformu tím, že detekuje problémy s kompatibilitou, které můžou mít vliv na funkce databází ve vaší nové verzi SQL Serveru nebo službě Azure SQL Database. Nástroj DMA doporučuje vylepšení výkonu a spolehlivosti pro cílové prostředí a umožňuje přesunout vaše schéma, data a neobsažené objekty ze zdrojového serveru na cílový server.

> [!NOTE]
> Pro velké migrace (s ohledem na počet a velikost databází) doporučujeme použít službu Azure Database Migration Service, která dokáže migrovat databáze ve velkém měřítku.
>

Pokud chcete začít pracovat s nástrojem Data Migration Assistant, postupujte podle těchto kroků.

1. Stáhněte si nástroj Data Migration Assistant z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595).
1. Kliknutím na ikonu **New (+)** (Nové (+)) vytvořte posouzení a jako typ projektu vyberte **Assessment** (Posouzení).
1. Vyberte typ zdrojového a cílového serveru. Klikněte na možnost **Vytvořit**.
1. Podle potřeby nakonfigurujte možnosti posouzení (doporučujeme ponechat všechna výchozí nastavení).
1. Přidejte databáze, které chcete posoudit.
1. Kliknutím na **Next** (Další) spusťte posouzení.
1. Podívejte se na výsledky v rámci sady nástrojů Data Migration Assistant.

V případě velkého podniku doporučujeme postupovat podle článku o [posouzení podnikových prostředků a konsolidaci posuzujících sestav pomocí nástroje DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports). Podle něj můžete posoudit více serverů, sloučit sestavy a pak analyzovat výsledky pomocí poskytovaných sestav Power BI.

Další informace, včetně podrobných kroků použití, najdete v těchto článcích:

- [Přehled nástroje Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview)
- [Posouzení podnikových prostředků a konsolidace posuzujících sestav pomocí nástroje DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports)
- [Analýza konsolidovaných posuzujících sestav vytvořených nástrojem Data Migration Assistant pomocí Power BI](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport)

## <a name="sql-server-migration-assistant"></a>Pomocník s migrací SQL Serveru

Pomocník s migrací Microsoft SQL Serveru (SSMA) je nástroj určený k automatizaci migrace databází na SQL Server z aplikace Microsoft Access, DB2, MySQL, Oracle a SAP ASE. Obecný postup je shromáždit, posoudit a pak zkontrolovat pomocí těchto nástrojů informace. Vzhledem k rozdílům v procesu pro jednotlivé zdrojové systémy ale doporučujeme, abyste si prostudovali podrobnou [dokumentaci pro Pomocníka s migrací SQL Serveru](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant).

Další informace naleznete v tématu:

- [Přehled Pomocníka s migrací SQL Serveru](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant)

## <a name="database-experimentation-assistant"></a>Pomocník pro experimentování s databázemi

Pomocník pro experimentování s databázemi (DEA) je nové řešení testování A/B pro upgrady SQL Serverů. Pomůže vám při vyhodnocování cílové verze SQL pro danou sadu funkcí. Tyto analytické metriky můžou využít zákazníci, kteří upgradují z předchozích verzí SQL Serveru (SQL Server 2005 a vyšší) na libovolnou novější verzi SQL Serveru.

Pomocník pro experimentování s databázemi obsahuje následující aktivity pracovního postupu:

- **Zachycení:** Prvním krokem při testování A/B SQL Serveru je zachycení trasování na vašem zdrojovém serveru. Zdrojovým serverem je obvykle produkční server.
- **Přehrání:** Druhým krokem při testování A/B SQL Serveru je přehrání zachyceného trasovacího souboru na vašich cílových serverech. Pak se z přehrání shromáždí rozsáhlá trasování pro analýzu.
- **Analýza:** Posledním krokem je vygenerování analytické sestavy pomocí trasování z přehrání. Analytická sestava vám může pomoct získat přehled o dopadech chystané změny na výkon.

Další informace naleznete v tématu:

- [Přehled Pomocníka pro experimentování s databázemi](https://docs.microsoft.com/sql/dea/database-experimentation-assistant-overview)

## <a name="cosmos-db-data-migration-tool"></a>Nástroj pro migraci dat Cosmos DB

Nástroje pro migraci dat Azure Cosmos DB může importovat data z různých zdrojů do kolekcí a tabulek Azure Cosmos DB. Můžete importovat ze souborů JSON, CSV, SQL, MongoDB, služby Azure Table Storage, Amazon DynamoDB a dokonce i z kolekcí rozhraní SQL API služby Azure Cosmos DB. Nástroj pro migraci dat můžete použít také při migraci z kolekce s jedním oddílem do kolekce s více oddíly pro rozhraní SQL API.

Další informace naleznete v tématu:

- [Nástroj pro migraci dat Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/import-data)

<!-- markdownlint-disable MD025 -->

# <a name="third-party-migration-toolstabthird-party-tools"></a>[Nástroje pro migraci od třetích stran](#tab/third-party-tools)

S procesem migrace vám může pomoct několik nástrojů a služeb od nezávislých výrobců softwaru. Každý z nich nabízí různé výhody a silné stránky. Mezi tyto nástroje patří:

## <a name="cloudamize"></a>Cloudamize

Cloudamize je služba nezávislého výrobce softwaru, která pokrývá všechny fáze strategie migrace.

[Další informace](https://www.cloudamize.com)

## <a name="zerto"></a>Zerto

Zerto poskytuje zpracování replikace virtuálních počítačů pro prostředí Microsoft Hyper-V i VMware vSphere.

[Další informace](https://www.zerto.com/solutions/use-cases/data-center-migration-software)

## <a name="carbonite"></a>Carbonite

Carbonite poskytuje řešení pro migraci serverů a dat, které umožňuje migrovat sady funkcí do nebo z libovolného fyzického, virtuálního nebo cloudového prostředí nebo mezi nimi.

[Další informace](https://www.carbonite.com/data-protection/data-migration-software)

## <a name="movere"></a>Movere

Movere je řešení pro zjišťování, které poskytuje data a přehledy potřebné k naplánování migrace do cloudu a k průběžné optimalizaci, monitorování a analýze IT prostředí.

[Další informace](https://www.movere.io)

## <a name="cosmos-db-partners"></a>Partneři služby Cosmos DB

Můžete si vybrat z široké nabídky zkušených partnerů v oblasti integrace systémů a příslušných nástrojů, které podporují vaše migrace Azure Cosmos DB pro vaše požadavky na databázi NoSQL.

[Další informace](https://docs.microsoft.com/azure/cosmos-db/partners-migration-cosmosdb#migration-tools)

Pokud chcete vyhledat organizace nabízející předem připravená partnerská technologická řešení, která by vyhovovala vašemu scénáři migrace, a získat více informací o dalších nástrojích a podpůrných službách pro migraci od třetích stran, navštivte [centrum pro migraci do Azure](https://azure.microsoft.com/migration/support).

V [průvodci migrací databází do Azure](https://datamigration.microsoft.com) najdete řadu možností migrace databáze a podrobné pokyny k nativním nástrojům a nástrojům partnerů.

# <a name="project-management-toolstabproject-management-tools"></a>[Nástroje pro řízení projektů](#tab/project-management-tools)

Pokud projekty nikdo nesleduje a neřídí, je pravděpodobnější, že se dostanou do problémů. Myslíme si, že v zájmu zajištění úspěšného výsledku je důležité, abyste použili nějaký nástroj pro řízení projektů. K dispozici je mnoho různých nástrojů a projektoví manažeři ve vaší organizaci už možná mají nějaký oblíbený.

Azure DevOps je navrhovaným nástrojem pro správu projektů během migrace do cloudu. Aby bylo možné zrychlit využití Azure DevOps, architektura přechodu na cloud zahrnuje nástroj pro automatické nasazení šablony projektu. Tato šablona obsahuje úlohy, které se během migrace obvykle spouštějí. Pomocí [těchto pokynů](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/template) šablonu nasadíte. Pak můžete šablonu upravit tak, aby odrážela [úlohy](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/workloads) a [aktiva](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/assets), které se mají migrovat.

Microsoft také nabízí následující nástroje pro řízení projektů, které můžou ve spolupráci poskytovat širší možnosti:

- [Microsoft Planner](https://tasks.office.com): Poskytuje jednoduchý vizuální způsob, jak organizovat týmovou práci.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): Poskytuje funkce pro řízení projektů a portfolia, správu kapacit zdrojů, finanční řízení a správu časových rozvrhů a plánů.
- [Microsoft Teams](https://products.office.com/microsoft-teams): Nástroj pro týmovou spolupráci a komunikaci. Aplikace Teams se také může v zájmu vylepšení spolupráce integrovat s Plannerem a dalšími nástroji.
- [Azure DevOps](https://dev.azure.com): Šablona plánování architektury přechodu na cloud není pro použití Azure DevOps nutná. Službu můžete použít bez šablony a spravovat svou infrastrukturu jako kód nebo používat pracovní položky a panely k řízení projektů. Zkušenější organizace můžou využívat možnosti CI/CD.

Nejedná se o jediné dostupné nástroje. V komunitě projektových manažerů se široce používá mnoho dalších nástrojů od třetích stran.

## <a name="set-up-for-devops"></a>Nastavení pro DevOps

Přechod na cloudové technologie představuje pro organizaci skvělou příležitost nachystat se na DevOps a CI/CD. I v případě, že vaše organizace spravuje jenom infrastrukturu, můžete začít spravovat infrastrukturu jako kód a díky použití oborových vzorů a postupů pro DevOps zvyšovat svou agilitu prostřednictvím kanálů CI/CD. To vám umožní rychlejší adaptaci na změny, růst, vydání produktů i obnovení.

[Azure DevOps](https://dev.azure.com) poskytuje všechny požadované funkce a integraci s místním prostředím, Azure i jinými cloudy. Další informace najdete [tady](https://azure.microsoft.com/services/devops). Další školení najdete v článku o [rychlém zprovoznění CI a CD s Azure DevOps](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html).

# <a name="cost-managementtabmanagecost"></a>[Správa nákladů](#tab/ManageCost)

Při a po migraci prostředků do cloudového prostředí je důležité provádět pravidelnou analýzu nákladů. To vám pomůže vyhnout se neočekávaným poplatkům za využití, protože proces migrace může přinášet zvýšené požadavky na využití služeb. Můžete také podle potřeby měnit velikost prostředků, aby byly náklady v rovnováze s vytížením (podrobnější informace najdete v oddílu o **[optimalizaci a transformaci](./optimize-and-transform.md)** ).
