---
title: Refaktoring aplikace migrací do Azure App Service a Azure SQL Database
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak Contoso přesouvá hostování místní aplikace migrací do webové aplikace Azure App Service a databáze Azure SQL Serveru.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: c94ad845571c5007f14773268d383764cdc89a6c
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025050"
---
# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-database"></a>Refaktoring místní aplikace do webové aplikace Azure App Service a databáze SQL Azure

Tento článek ukazuje, jak fiktivní společnost Contoso v rámci migrace do Azure refaktoruje dvouúrovňovou aplikaci Windows .NET, která běží na virtuálních počítačích VMware. Front-endový virtuální počítač aplikace se bude migrovat do webové aplikace Azure App Service a databáze aplikace do databáze Azure SQL.

Aplikace SmartHotel360 použitá v tomto příkladu je k dispozici jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s partnery ve firmě, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Contoso roste a vzniká tak tlak na místních systémy a infrastrukturu.
- **Zvýšení efektivity.** Společnost Contoso se potřebuje zbavit zbytečných postupů a zjednodušit procesy pro vývojáře i uživatele. Potřebuje IT k tomu, aby neztrácela čas ani peníze, byla rychlá a dokázala rychleji reagovat na požadavky zákazníků.
- **Zvýšení agility.**  IT ve společnosti Contoso musí pohotověji reagovat na potřeby firmy. K zajištění úspěchu v globální ekonomice je nutné, aby IT dokázalo rychleji reagovat na změny na trhu. Nesmí stát v cestě a nesmí se stát obchodní překážkou.
- **Škálování** Contoso se úspěšně rozšiřuje a IT musí poskytovat systémy, které jsou schopné rozvíjet se stejným tempem.
- **Snížení nákladů.** Společnost Contoso chce minimalizovat náklady na licencování.

## <a name="migration-goals"></a>Cíle migrace

Tým pro přechod společnosti Contoso na cloud přesně specifikoval cíle této migrace. Tyto cíle se použily k určení nejlepší metody migrace.

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Aplikace** | Aplikace v Azure bude nadále stejně důležitá, jako je dnes.<br/><br/> Měla by mít stejné výkonové možnosti, jako má v současnosti ve VMware.<br/><br/> Tým nechce do této aplikace investovat. Prozatím správci jednoduše bezpečně přesunou tuto aplikaci do cloudu.<br/><br/> Tým chce přestat podporovat Windows Server 2008 R2, na kterém tato aplikace aktuálně běží.<br/><br/> Tým také chce přejít z SQL Serveru 2008 R2 na moderní databázovou platformu PaaS a minimalizovat tak nutnost správy.<br/><br/> Contoso chce využít investici do licencování SQL Serveru a Software Assurance, kdykoli je to možné.<br/><br/> Navíc chce zmírnit kritický prvek způsobující selhání ve webové vrstvě.
**Omezení** | Tato aplikace se skládá z aplikace v ASP.NET a služby WCF běžící na stejném virtuálním počítači. Chtějí ji rozdělit do dvou webových aplikací s využitím Azure App Service.
**Azure** | Společnost Contoso chce přesunout aplikaci do Azure, ale nechce ji spouštět na virtuálních počítačích. Contoso chce používat služby Azure PaaS pro webovou i datovou vrstvu.
**DevOps** | Společnost Contoso chce přejít na model DevOps a pro buildy a kanály verzí využívat Azure DevOps.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Návrh řešení

Po dokončení podrobné specifikace cílů a požadavků Contoso navrhne a zkontroluje řešení nasazení a určí proces migrace včetně služeb Azure, které se k migraci využijí.

### <a name="current-app"></a>Aktuální aplikace

- Místní aplikace SmartHotel360 je rozvrstvená na dva virtuální počítače (WEBVM a SQLVM).
- Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com** (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) spuštěný na virtuálním počítači.
- Společnost Contoso má místní datacentrum (contoso-datacenter) s místním řadičem domény (**contosodc1**).
- Po dokončení migrace se místní virtuální počítače v datacentru Contoso vyřadí z provozu.

### <a name="proposed-solution"></a>Navrhované řešení

- Pro databázovou vrstvu aplikace společnost Contoso porovnala Azure SQL Database s SQL Serverem na základě informací v [tomto článku](https://docs.microsoft.com/azure/sql-database/sql-database-features). Rozhodla se využít Azure SQL Database, a to hned z několika důvodů:
  - Azure SQL Database je spravovaná relační databázová služba. Zajišťuje předvídatelný výkon na několika úrovních služeb, a to s téměř nulovou správou. Mezi její další výhody patří dynamická škálovatelnost bez výpadků, integrovaná inteligentní optimalizace a globální škálovatelnost a dostupnost.
  - Společnost Contoso může použít odlehčený nástroj Data Migration Assistant (DMA) k vyhodnocení a migraci místní databáze do Azure SQL.
  - Prostřednictvím programu Software Assurance může společnost Contoso vyměnit stávající licence za snížené sazby pro SQL Database, a to pomocí programu Zvýhodněné hybridní využití Azure pro SQL Server. Výsledné úspory by mohly dosáhnout až 30 %.
  - SQL Database poskytuje funkce zabezpečení, jako je funkce Always Encrypted, dynamické maskování dat a detekce hrozeb a zabezpečení na úrovni řádků.
- Pro webovou vrstvu aplikace se společnost Contoso rozhodla použít Azure App Service. Tato služba PaaS umožňuje nasazení aplikace jenom s několika konfiguračními změnami. Contoso k provedené této změny využije Visual Studio a nasadí dvě webové aplikace. Jednu pro web a druhou pro službu WCF.
- Pro splnění požadavků na kanál DevOps se společnost Contoso rozhodla pro správu zdrojového kódu (SCM) použít Azure DevOps s úložišti Git. K sestavení kódu se použije automatizované sestavování a vydávání a kód se nasadí do Azure App Service.

### <a name="solution-review"></a>Revize řešení

Společnost Contoso vyhodnotí vytvořený návrh tím, že sestaví seznam pro a proti.

<!-- markdownlint-disable MD033 -->

**Aspekty** | **Podrobnosti**
--- | ---
**Výhody** | Pro migraci do Azure nebude potřeba měnit kód aplikace SmartHotel360.<br/><br/> Společnost Contoso může využít své investice do Software Assurance pomocí programu Zvýhodněné hybridní využití Azure pro SQL Server i Windows Server.<br/><br/> Po dokončení migrace už nebude nutné podporovat Windows Serveru 2008 R2. [Další informace](https://support.microsoft.com/lifecycle).<br/><br/> Contoso může nakonfigurovat webovou vrstvu aplikace s využitím několika instancí, takže už nebude kritickým prvkem způsobujícím selhání.<br/><br/> Databáze už nebude záviset na zastarávajícím SQL Serveru 2008 R2.<br/><br/> SQL Database podporuje dané technické požadavky. Společnost Contoso vyhodnotila místní databázi pomocí Data Migration Assistanta a zjistila, že je kompatibilní.<br/><br/> Azure SQL Database má integrovanou odolnost proti chybám, kterou Contoso nemusí nastavovat. Tím se zajistí, že datová vrstva už nebude jediným bodem převzetí služeb při selhání.
**Nevýhody** | Azure App Service podporuje pro každou webovou aplikaci jenom jedno nasazení. To znamená, že se musí zřídit dvě webové aplikace (jedna pro web a druhá pro službu WCF).<br/><br/> Pokud společnost Contoso k migraci své databáze použije Data Migration Assistanta, a ne službu Azure Database Migration Service, nebude mít připravenou infrastrukturu pro migraci databází ve velkém měřítku. Společnost Contoso bude muset vytvořit další oblast, aby se zajistilo převzetí služeb při selhání, když primární oblast není k dispozici.

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Navrhovaná architektura

![Architektura scénáře](media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Proces migrace

1. Společnost Contoso zřídí instanci SQL Azure a migruje do ní databázi SmartHotel360.
2. Společnost Contoso zřídí a nakonfiguruje webové aplikace a nasadí do nich aplikaci SmartHotel360.

    ![Proces migrace](media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[Data Migration Assistant (DMA)](/sql/dma/dma-overview?view=ssdt-18vs2017) | Společnost Contoso využije DMA k vyhodnocení a detekci problémů s kompatibilitou, které mohou ovlivnit fungování databáze v Azure. DMA vyhodnotí paritu funkcí mezi zdroji a cíli SQL a doporučí vylepšení výkonu a spolehlivosti. | Tento nástroj je zdarma ke stažení.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Inteligentní, plně spravovaná relační cloudová databázová služba | Náklady závisejí na funkcích, propustnosti a velikosti. [Další informace](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Tvorba výkonných cloudových aplikací s využitím plně spravované platformy | Náklady závisejí na velikosti, umístění a využití. [Další informace](https://azure.microsoft.com/pricing/details/app-service/windows).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Poskytuje kanál průběžné integrace a průběžného nasazování (CI/CD) pro vývoj aplikací. Součástí tohoto kanálu je úložiště Git pro správu kódu aplikace, systém sestavování pro vytváření balíčků a dalších artefaktů buildu a systém Release Management pro nasazování změn ve vývojových, testovacích a produkčních prostředích.

## <a name="prerequisites"></a>Požadavky

Contoso k realizaci tohoto scénáře potřebuje:

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Vytvořená předplatná Contoso z dřívějšího článku. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.
**Infrastruktura Azure** | [Přečtěte si víc](./contoso-migration-infrastructure.md) o tom, jak společnost Contoso nastavuje infrastrukturu Azure.

<!--markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Contoso provede migraci takto:

> [!div class="checklist"]
>
> - **Krok 1: Zřízení instance služby SQL Database v Azure.** Společnost Contoso zřídí instanci SQL v Azure. Po dokončení migraci webu aplikace do Azure bude na tuto instanci odkazovat webová aplikace služby WCF.
> - **Krok 2: Migrace databáze s využitím DMA.** Společnost Contoso migruje databázi aplikace pomocí Data Migration Assistanta.
> - **Krok 3: Zřízení webových aplikací.** Společnost Contoso zřídí dvě webové aplikace.
> - **Krok 4: Nastavení služby Azure DevOps.** Contoso vytvoří nový projekt Azure DevOps a naimportuje úložiště Git.
> - **Krok 5: Konfigurace připojovacích řetězců.** Contoso nakonfiguruje připojovací řetězce tak, aby webová aplikace webové vrstvy, webová aplikace služby WCF a instance SQL mohly vzájemně komunikovat.
> - **Krok 6: Nastavení kanálů buildu a verze.** V posledním kroku společnost Contoso vytvoří kanály buildu a verze pro vytvoření aplikace a nasadí je do dvou samostatných webových aplikací.

## <a name="step-1-provision-an-azure-sql-database"></a>Krok 1: Zřízení Azure SQL Database

1. Správci Contoso se rozhodují vytvořit SQL Database v Azure.

    ![Zřízení SQL](media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. Zadají název databáze, který odpovídá databázi spuštěné na místním virtuálním počítači (**SmartHotel.Registration**). Umístí tuto databázi do skupiny prostředků ContosoRG. Jedná se o skupinu prostředků, kterou používají pro produkční prostředky v Azure.

    ![Provision SQL](media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. V primární oblasti nastaví novou instanci SQL Serveru (**sql-smarthotel-eus2**).

    ![Zřízení SQL](media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. Nastaví cenovou úroveň tak, aby odpovídala potřebám jejich serveru a databáze. A rozhodnou se ušetřit prostřednictvím programu Zvýhodněné hybridní využití Azure, protože už mají licenci SQL Serveru.
5. K nastavení velikosti využijí nákupní model založený na virtuálních jádrech a nastaví omezení pro očekávané požadavky.

    ![Zřízení SQL](media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. Potom vytvoří instanci databáze.

    ![Zřízení SQL](media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. Po vytvoření instance otevřou databázi a poznamenají si podrobnosti, které potřebují při migraci pomocí Data Migration Assistanta.

    ![Zřízení SQL](media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Potřebujete další pomoc?**

- [Pomoc](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) se zřizováním SQL Database
- [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) o omezeních prostředků virtuálních jader

## <a name="step-2-migrate-the-database-with-dma"></a>Krok 2: Migrace databáze s využitím DMA

Správci Contoso budou migrovat databázi SmartHotel360 pomocí DMA.

### <a name="install-dma"></a>Instalace DMA

1. Tento nástroj si stáhnou z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) do místního virtuálního počítače s SQL Serverem (**SQLVM**).
2. Na tomto virtuálním počítači spustí instalační program (DownloadMigrationAssistant.msi).
3. Před dokončením průvodce na stránce **Finish** (Dokončit) vyberou **Launch Microsoft Data Migration Assistant** (Spustit Microsoft Data Migration Assistanta).

### <a name="migrate-the-database-with-dma"></a>Migrace databáze s využitím DMA

1. V DMA vytvoří nový projekt (**SmartHotelDB**) a vyberou **Migration** (Migrace).
2. Jako typ zdrojového serveru vyberou **SQL Server** a jako typ cílového serveru zvolí **Azure SQL Database**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-1.png)

3. V podrobnostech o migraci doplní **SQLVM** jako zdrojový server a databázi **SmartHotel.Registration**.

     ![DMA](media/contoso-migration-refactor-web-app-sql/dma-2.png)

4. Zobrazí se jim chyba, která zdánlivě souvisí s ověřováním. Po prozkoumání ale zjistí, že problém způsobuje tečka (.) v názvu databáze. Jako alternativní řešení se rozhodnou zřídit novou databázi SQL s použitím názvu **SmartHotel-Registration**. Při opětovném spuštění DMA už mohou vybrat **SmartHotel-Registration** a pokračovat v průvodci.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-3.png)

5. V části **Vybrat objekty** vyberou databázové tabulky a vygenerují skript SQL.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-4.png)

6. Jakmile DMA vytvoří tento skript, vyberou **Nasadit schéma**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-5.png)

7. DMA potvrdí, že nasazení proběhlo úspěšně.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-6.png)

8. Teď zahájí vlastní migraci.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-7.png)

9. Po dokončení migrace mohou správci Contoso ověřit, jestli je databáze spuštěná v instanci SQL Azure.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-8.png)

10. Přebytečnou databázi SQL nazvanou **SmartHotel.Registration** odstraní na webu Azure Portal.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-9.png)

## <a name="step-3-provision-web-apps"></a>Krok 3: Zřízení webových aplikací

Migrace databáze je dokončená a teď správci Contoso mohou zřídit dvě webové aplikace.

1. Na portálu vyberou **Webová aplikace**.

    ![Webová aplikace](media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. Zadají název aplikace (**SHWEB-EUS2**), spustí ji ve Windows a umístí ji do produkční skupiny prostředků **ContosoRG**. Vytvoří novou webovou aplikaci a plán služby Azure App Service.

    ![Webová aplikace](media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. Po zřízení webové aplikace tento proces zopakují a vytvoří webovou aplikaci pro službu WCF (**SHWCF-EUS2**).

    ![Webová aplikace](media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. Když jsou hotoví, přejdou na adresu aplikací a ověří jejich úspěšné vytvoření.

## <a name="step-4-set-up-azure-devops"></a>Krok 4: Nastavení služby Azure DevOps

Contoso pro tuto aplikaci potřebuje sestavit kanály a infrastrukturu DevOps. Správci Contoso k tomuto účelu vytvoří nový projekt DevOps, naimportují kód a potom nastaví kanály buildu a verze.

1. V účtu Azure DevOps společnosti Contoso vytvoří nový projekt (**ContosoSmartHotelRefactor**) a pro správu verzí vyberou **Git**.

    ![Nový projekt](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. Naimportují úložiště Git, ve kterém je v současné době uložený kód aplikace. Je ve [veřejném úložišti](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) a můžete si ho stáhnout.

    ![Stažení kódu aplikace](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. Po naimportování kódu k tomuto úložišti připojí sadu Visual Studio a naklonují kód pomocí Team Exploreru.

    ![Připojení k projektu](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. Když je úložiště ve vývojářském počítači naklonované, otevřou pro tuto aplikaci soubor řešení. Webová aplikace a služba wcf mají v tomto souboru samostatný projekt.

    ![Soubor řešení](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Krok 5: Konfigurace připojovacích řetězců

Správci společnosti Contoso musí zajistit, aby spolu webové aplikace a databáze mohly komunikovat. Proto v kódu a ve webových aplikacích nakonfigurují připojovací řetězce.

1. Ve webové aplikaci pro službu WCF (**SHWCF-EUS2**) > **Nastavení** > **Nastavení aplikace** přidají nový připojovací řetězec nazvaný **DefaultConnection**.
2. Připojovací řetězec se načte z databáze **SmartHotel-Registration** a měl by se aktualizovat s využitím správných přihlašovacích údajů.

    ![Připojovací řetězec](media/contoso-migration-refactor-web-app-sql/string1.png)

3. Pomocí sady Visual Studio otevřou projekt **SmartHotel.Registration.wcf** ze souboru řešení. Oddíl **connectionStrings** souboru web.config pro SmartHotel.Registration.Wcf služby WCF by se měl aktualizovat s využitím tohoto připojovacího řetězce.

     ![Připojovací řetězec](media/contoso-migration-refactor-web-app-sql/string2.png)

4. Oddíl **client** souboru web.config pro SmartHotel.Registration.Web by se měl změnit tak, aby odkazoval na nové umístění služby WCF. Je to adresa URL webové aplikace WCF, která je hostitelem příslušného koncového bodu služby.

    ![Připojovací řetězec](media/contoso-migration-refactor-web-app-sql/strings3.png)

5. Po provedení změn v kódu musí správci tyto změny potvrdit. Pomocí Team Exploreru v sadě Visual Studio je potvrdí a sesynchronizují.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Krok 6: Nastavení kanálů buildu a verze v Azure DevOps

Správci společnosti Contoso teď nakonfigurují Azure DevOps, aby mohli provést proces sestavení a vydání.

1. V Azure DevOps zvolí **Build a verze** > **Nový kanál**.

    ![Nový kanál](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. Vyberou **Git Azure Repos** a relevantní úložiště.

    ![Git a úložiště](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. V části **Vybrat šablonu** vyberou šablonu ASP.NET pro svůj build.

     ![Šablona ASP.NET](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Pro tento build se použije název **ContosoSmartHotelRefactor-ASP.NET-CI**. Vyberou **Save & Queue** (Uložit a zařadit do fronty).

     ![Uložit a zařadit do fronty](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Tím se aktivuje první build. Vyberou číslo buildu, aby mohli celý proces sledovat. Po dokončení si mohou projít zpětnou vazbu k tomuto procesu, vybrat **Artefakty** a projít si výsledky buildu.

    ![Zkontrolovat](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. Výsledky buildu obsahuje složka **Drop**.

    - Dva soubory ZIP jsou balíčky obsahující aplikace.
    - Tyto soubory se využívají v kanálu verze k nasazení do služby Azure App Service.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. Vyberou **Vydané verze** >  **+Nový kanál**.

    ![Nový kanál](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. Vyberou šablonu nasazení pro Azure App Service.

    ![Šablona nasazení Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. Kanál verze pojmenují **ContosoSmartHotel360Refactor** a jako název pro **fázi** zadají název webové aplikace WCF (SHWCF-EUS2).

    ![Prostředí](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. V rámci fází pro konfiguraci nasazení služby WCF vyberou **1 úloha, 1 úkol**.

    ![Nasazení WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. Ověří, že předplatné je vybrané a autorizované, a vyberou **název služby App Service**.

     ![Výběr názvu služby App Service](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. V kanálu > **Artifacts** vyberou **+Add an artifact** (Přidat artefakt) a vyberou, že budou sestavovat s využitím kanálu **ContosoSmarthotel360Refactor**.

     ![Sestavení](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. Zkontrolují, že ikona blesku na artefaktu je zaškrtnutá, aby byla povolená aktivační událost průběžného nasazování.

     ![Ikona blesku](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. Aktivační událost průběžného nasazování by měla být nastavená na **Enabled** (Povoleno).

    ![Povolené průběžné nasazování](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Teď přejdou zpátky k fázi 1 úloha, 1 úkol a vyberou **Deploy Azure App Service** (Nasadit Azure App Service).

    ![Nasazení Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. V poli **Select a file or folder** (Vybrat soubor nebo složku) vyhledají soubor **SmartHotel.Registration.Wcf.zip**, který se vytvořil při sestavování buildu, a potom vyberou **Save** (Uložit).

    ![Uložení WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. Výběrem **Pipeline** > **Stages** **+Add** (Kanál > Fáze +Přidat) přidají prostředí pro **SHWEB-EUS2**. Vyberou jiné nasazení Azure App Service.

    ![Přidání prostředí](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. Zopakují tento proces a publikují soubor webové aplikace (**SmartHotel.Registration.Web.zip**) do správné webové aplikace.

    ![Publikování webové aplikace](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

19. Po uložení se kanál verze bude zobrazovat následujícím způsobem.

     ![Souhrn kanálu verze](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

20. Přejdou zpátky k **buildu** a vyberou **Triggers** > **Enable continuous integration** (Aktivační události > Povolit kontinuální integraci). Tím je kanál povolený, takže při potvrzení změn v kódu dojde ke kompletnímu sestavení a vydání.

    ![Povolení kontinuální integrace](./media/contoso-migration-refactor-web-app-sql/pipeline20.png)

21. Vyberou **Save & Queue** (Uložit a zařadit do fronty) pro spuštění kompletního kanálu. Aktivuje se nový build, který zase vytvoří první vydanou verzi aplikace v Azure App Service.

    ![Uložení kanálu](./media/contoso-migration-refactor-web-app-sql/pipeline21.png)

22. Správci Contoso mohou proces zpracování kanálu buildu a verze sledovat z Azure DevOps. Po dokončení sestavování se začne vydávat.

    ![Sestavení a vydání aplikace](./media/contoso-migration-refactor-web-app-sql/pipeline22.png)

23. Po dokončení zpracování kanálu jsou oba weby nasazené a aplikace je zprovozněná online.

    ![Dokončení vydání](./media/contoso-migration-refactor-web-app-sql/pipeline23.png)

V tomto okamžiku je aplikace úspěšně migrovaná do Azure.

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace společnost Contoso potřebuje provést tyto kroky čištění:

- Odebrat místní virtuální počítače z inventáře vCenter
- Odebrat virtuální počítače z úloh místního zálohování
- Aktualizovat interní dokumentaci tak, aby obsahovala nová umístění pro aplikaci SmartHotel360 Zobrazit databázi jako spuštěnou v databázi Azure SQL a front-end jako spuštěný ve dvou webových aplikacích
- Zkontrolovat všechny prostředky, které s vyřazenými virtuálními počítači spolupracují, a aktualizovat veškeré související nastavení nebo dokumentaci tak, aby odrážely novou konfiguraci

## <a name="review-the-deployment"></a>Revize nasazení

Teď, když má prostředky migrované do Azure, společnost Contoso potřebuje plně zprovoznit a zabezpečit novou infrastrukturu.

### <a name="security"></a>Zabezpečení

- Contoso potřebuje zajistit, že nová databáze **SmartHotel-Registration** je zabezpečená. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Společnost Contoso by měla zejména aktualizovat webové aplikace, aby využívaly SSL s certifikáty.

### <a name="backups"></a>Zálohování

- Contoso si potřebuje projít požadavky na zálohování pro Azure SQL Database. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Contoso se také potřebuje dozvědět víc o správě zálohování a obnovení SQL Database. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) o automatickém zálohování
- Společnost Contoso by měla zvážit implementaci skupin převzetí služeb při selhání a zajistit tak regionální převzetí služeb při selhání pro databázi. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Pro zajištění odolnosti musí Contoso zvážit nasazení webové aplikace v hlavní oblasti Východní USA 2 a v oblasti Střední USA. Společnost Contoso může nakonfigurovat Traffic Manager, aby zajistila převzetí služeb při selhání v případě regionálních výpadků.

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- Po nasazení všech prostředků by společnost Contoso měla na základě [plánování infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging) přiřadit značky Azure.
- Veškeré licencování je součástí nákladů na služby PaaS, které společnost Contoso spotřebovává. Náklady se odečtou ze smlouvy EA.
- Contoso povolí službu Azure Cost Management licencovanou Cloudynem, dceřinou společností Microsoftu. Jedná se o multicloudové řešení správy nákladů, které pomáhá využívat a spravovat Azure a další cloudové prostředky. [Další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management

## <a name="conclusion"></a>Závěr

V tomto článku společnost Contoso refaktorovala aplikaci SmartHotel360 v Azure migrací jejího front-endového virtuálního počítače do dvou webových aplikací služby Azure App Service. Databáze aplikace se migrovala do databáze SQL Azure.
