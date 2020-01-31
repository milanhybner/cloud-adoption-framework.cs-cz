---
title: Změna architektury aplikace na kontejner Azure a službu Azure SQL Database
description: Přečtěte si, jak Contoso mění architekturu aplikace na kontejnery Windows v Azure a Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 3727c6bac138dae12ec976683ba2b5954bbd9163
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807542"
---
# <a name="rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a>Změna architektury místní aplikace na kontejner Azure a službu Azure SQL Database

Tento článek ukazuje, jak fiktivní společnost Contoso v rámci migrace do Azure mění architekturu dvouúrovňové aplikace Windows .NET, která běží na virtuálních počítačích VMware. Contoso migruje front-endový virtuální počítač aplikace do kontejneru Windows v Azure a databázi aplikace do databáze Azure SQL.

Aplikace SmartHotel360 použitá v tomto příkladu je k dispozici jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT ve společnosti Contoso těsně spolupracoval s obchodními partnery, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Contoso roste, čímž vzniká tlak na místní systémy a infrastrukturu.
- **Zvýšení efektivity.** Společnost Contoso se potřebuje zbavit zbytečných postupů a zjednodušit procesy pro vývojáře i uživatele. Potřebuje IT k tomu, aby neztrácela čas ani peníze, byla rychlá a dokázala rychleji reagovat na požadavky zákazníků.
- **Zvýšení agility.** IT ve společnosti Contoso musí pohotověji reagovat na potřeby firmy. K zajištění úspěchu v globální ekonomice je nutné, aby IT dokázalo rychleji reagovat na změny na trhu. Nesmí stát v cestě a nesmí se stát obchodní překážkou.
- **Škálování** Contoso se úspěšně rozšiřuje a IT musí poskytovat systémy, které jsou schopné rozvíjet se stejným tempem.
- **Snížení nákladů.** Společnost Contoso chce minimalizovat náklady na licencování.

## <a name="migration-goals"></a>Cíle migrace

Tým pro přechod společnosti Contoso na cloud přesně specifikoval cíle této migrace. Tyto cíle se použily k určení nejlepší metody migrace.

<!-- markdownlint-disable MD033 -->

**Cíle** | **Podrobnosti**
--- | ---
**Požadavky na aplikaci** | Aplikace v Azure bude nadále stejně důležitá, jako je dnes.<br/><br/> Měla by mít stejné výkonové možnosti, jako má v současnosti ve VMware.<br/><br/> Společnost Contoso chce přestat podporovat Windows Server 2008 R2, na kterém teď tato aplikace běží, a je ochotná do ní investovat.<br/><br/> Contoso chce přejít z SQL Serveru 2008 R2 na moderní databázovou platformu PaaS a minimalizovat tak nutnost správy.<br/><br/> Contoso chce využít investici do licencování SQL Serveru a Software Assurance, kdykoli je to možné.<br/><br/> Contoso chce mít možnost vertikálně navýšit kapacitu webové vrstvy aplikace.
**Omezení** | Tato aplikace se skládá z aplikace v ASP.NET a služby WCF běžící na stejném virtuálním počítači. Contoso ji chce rozdělit do dvou webových aplikací s využitím Azure App Service.
**Požadavky na Azure** | Společnost Contoso chce přesunout aplikaci do Azure, spouštět ji v kontejneru a prodloužit tak její životní cyklus. Při implementaci aplikace v Azure nechce začínat úplně od začátku.
**DevOps** | Společnost Contoso chce přejít na model DevOps a pro buildy kódu a verzí využívat Azure DevOps Services.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Návrh řešení

Po dokončení podrobné specifikace cílů a požadavků Contoso navrhne a zkontroluje řešení nasazení a určí proces migrace, včetně služeb Azure, které se k migraci využijí.

### <a name="current-app"></a>Aktuální aplikace

- Místní aplikace SmartHotel360 je rozvrstvená na dva virtuální počítače (WEBVM a SQLVM).
- Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com** (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) spuštěný na virtuálním počítači.
- Contoso má místní datacentrum (contoso-datacenter) s místním řadičem domény (**contosodc1**).
- Po dokončení migrace budou místní virtuální počítače v datacentru společnosti Contoso vyřazeny z provozu.

### <a name="proposed-architecture"></a>Navrhovaná architektura

- Pro databázovou vrstvu aplikace společnost Contoso porovnala Azure SQL Database s SQL Serverem na základě informací v [tomto článku](https://docs.microsoft.com/azure/sql-database/sql-database-features). Rozhodla se využít Azure SQL Database, a to hned z několika důvodů:
  - Azure SQL Database je spravovaná relační databázová služba. Zajišťuje předvídatelný výkon na několika úrovních služeb, a to s téměř nulovou správou. Mezi její další výhody patří dynamická škálovatelnost bez výpadků, integrovaná inteligentní optimalizace a globální škálovatelnost a dostupnost.
  - Společnost Contoso využije jednoduchý nástroj Data Migration Assistant (DMA) k vyhodnocení a migraci místní databáze do Azure SQL.
  - Prostřednictvím programu Software Assurance může společnost Contoso vyměnit stávající licence za snížené sazby pro SQL Database, a to pomocí programu Zvýhodněné hybridní využití Azure pro SQL Server. Výsledné úspory by mohly dosáhnout až 30 %.
  - SQL Database poskytuje několik funkcí zabezpečení, včetně funkce Always Encrypted, dynamického maskování dat a detekce hrozeb a zabezpečení na úrovni řádků.
- Webovou vrstvu aplikace se společnost Contoso rozhodla převést do kontejneru Windows s využitím služeb Azure DevOps.
  - Contoso nasadí aplikaci s využitím služby Azure Service Fabric a image kontejneru Windows převezme ze služby Azure Container Registry (ACR).
  - Prototyp pro rozšíření aplikace o analýzu mínění se ve službě Service Fabric bude implementovat jako jiná služba připojená ke Cosmos DB. Bude načítat informace z tweetů a zobrazovat je v aplikaci.
- Při implementaci kanálu DevOps společnost Contoso pro správu zdrojového kódu (SCM) použije Azure DevOps s úložišti Git. K sestavování kódu a jeho nasazení do služeb Azure Container Registry a Azure Service Fabric se budou používat automatizované buildy a vydání.

    ![Architektura scénáře](./media/contoso-migration-rearchitect-container-sql/architecture.png)

### <a name="solution-review"></a>Revize řešení

Společnost Contoso vyhodnotí vytvořený návrh sestavením seznamu výhod a nevýhod.

<!-- markdownlint-disable MD033 -->

**Aspekty** | **Podrobnosti**
--- | ---
**Výhody** | Pro migraci do Azure Service Fabric bude potřeba měnit kód aplikace SmartHotel360. Pokud se ale pro tyto změny použijí nástroje sady Service Fabric SDK, požadované úsilí bude minimální.<br/><br/> Díky přechodu na Service Fabric může společnost Contoso začít vyvíjet mikroslužby, které se dají do aplikace rychle přidávat bez ohrožení původního základu kódu.<br/><br/> Kontejnery Windows nabízejí stejné výhody jako kontejnery obecně. Vylepšují flexibilitu, přenositelnost a možnosti řízení.<br/><br/> Contoso může využít své investice do Software Assurance pomocí programu Zvýhodněné hybridní využití Azure pro SQL Server i Windows Server.<br/><br/> Po dokončení migrace už nebude potřeba podporovat Windows Server 2008 R2. [Další informace](https://support.microsoft.com/lifecycle).<br/><br/> Contoso může nakonfigurovat webovou vrstvu aplikace s využitím několika instancí, takže už nebude kritickým prvkem způsobujícím selhání.<br/><br/> Už nebude záviset na zastarávajícím SQL Serveru 2008 R2.<br/><br/> SQL Database podporuje technické požadavky společnosti Contoso. Správci Contoso vyhodnotili místní databázi pomocí Data Migration Assistanta a zjistili, že je kompatibilní.<br/><br/> SQL Database má integrovanou odolnost proti chybám, kterou Contoso nemusí nastavovat. Tím se zajistí, že datová vrstva už nebude jediným bodem převzetí služeb při selhání.
**Nevýhody** | Kontejnery jsou složitější než ostatní možnosti migrace. Křivka osvojování znalostí by mohla být pro Contoso problémem. Zavádějí zcela novou úroveň složitosti, která má i přes tuto strmou křivku řadu předností.<br/><br/> Provozní tým ve společnosti Contoso navýšit své znalosti, aby chápal Azure, kontejnery a mikroslužby pro aplikaci a dokázal je podporovat.<br/><br/> Pokud společnost Contoso používá Data Migration Assistant místo Azure Database Migration Service k migraci databáze, nebude mít infrastrukturu připravenou pro migraci databází se škálováním.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migrace

1. Společnost Contoso zřídí cluster služby Azure Service Fabric pro Windows.
2. Zřídí instanci SQL Azure a migruje do ní databázi SmartHotel360.
3. Společnost Contoso převede virtuální počítač webové vrstva na kontejner Docker s využitím nástrojů sady Service Fabric SDK.
4. Připojí cluster Service Fabric a ACR a nasadí aplikaci pomocí služby Azure Service Fabric.

    ![Proces migrace](./media/contoso-migration-rearchitect-container-sql/migration-process.png)

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[Data Migration Assistant (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Vyhodnocuje a detekuje problémy s kompatibilitou, které by mohly ovlivnit fungování databází v Azure. DMA vyhodnotí paritu funkcí mezi zdroji a cíli SQL a doporučí vylepšení výkonu a spolehlivosti. | Tento nástroj je zdarma ke stažení.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Poskytuje inteligentní, plně spravovanou relační cloudovou databázovou službu. | Náklady závisejí na funkcích, propustnosti a velikosti. [Další informace](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Ukládá image pro všechny typy kontejnerových nasazení. | Náklady závisí na funkcích, úložišti a délce využití. [Další informace](https://azure.microsoft.com/pricing/details/container-registry).
[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) | Sestavuje a provozuje vždy funkční, škálovatelné distribuované aplikace. | Náklady závisejí na velikosti, umístění a době trvání výpočetních uzlů. [Další informace](https://azure.microsoft.com/pricing/details/service-fabric).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Poskytuje kanál průběžné integrace a průběžného nasazování (CI/CD) pro vývoj aplikací. Součástí tohoto kanálu je úložiště Git pro správu kódu aplikace, systém sestavování pro vytváření balíčků a dalších artefaktů buildu a systém Release Management pro nasazování změn ve vývojových, testovacích a produkčních prostředích.

## <a name="prerequisites"></a>Požadavky

Contoso k realizaci tohoto scénáře potřebuje:

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Firma Contoso vytvořila předplatná v dřívějším článku v této sérii. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.
**Infrastruktura Azure** | [Přečtěte si víc](./contoso-migration-infrastructure.md) o tom, jak společnost Contoso nastavila infrastrukturu Azure.
**Požadavky na vývojáře** | Společnost Contoso potřebuje na vývojářské pracovní stanici následující nástroje:<br/><br/> - [Visual Studio 2017 Community Edition: verze 15,5](https://www.visualstudio.com)<br/><br/> – Povolené úlohy .NET<br/><br/> - [Git](https://git-scm.com)<br/><br/> - [Service Fabric SDK v 3.0 nebo novější](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)<br/><br/> - [Docker CE (Windows 10) nebo Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) nastavený pro použití kontejnerů Windows

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Contoso spustí migraci tímto způsobem:

> [!div class="checklist"]
>
> - **Krok 1: zřízení instance SQL Database v Azure** Společnost Contoso zřídí instanci SQL v Azure. Po dokončení migrace front-endového virtuálního počítače do kontejneru Azure bude instance kontejneru s front-endem aplikace odkazovat na tuto databázi.
> - **Krok 2: Vytvořte Azure Container Registry (ACR).** Společnost Contoso zřídí firemní registr kontejnerů pro image kontejnerů Docker.
> - **Krok 3: zřízení Service Fabric Azure** Zřídí se cluster služby Service Fabric.
> - **Krok 4: Správa certifikátů Service fabricu** Contoso nastaví certifikáty pro přístup Azure DevOps Services ke clusteru.
> - **Krok 5: migrace databáze pomocí DMA.** Migruje databázi aplikace pomocí Data Migration Assistanta.
> - **Krok 6: nastavte Azure DevOps Services.** Contoso vytvoří nový projekt v Azure DevOps Services a naimportuje kód do úložiště Git.
> - **Krok 7: převod aplikace** Contoso převede aplikaci do kontejneru s využitím nástrojů Azure DevOps a sady SDK.
> - **Krok 8: nastavte sestavení a vydání.** Contoso nastaví kanály buildu a verze pro vytvoření aplikace a její publikování v ACR a clusteru služby Service Fabric.
> - **Krok 9: rozšíříte aplikaci.** Po zveřejnění společnost Contoso aplikaci rozšíří, aby využila výhod možností Azure, a pomocí kanálu ji bude znovu publikovat v Azure.

## <a name="step-1-provision-an-azure-sql-database"></a>Krok 1: zřízení Azure SQL Database

Správci společnosti Contoso zřídí databázi SQL Azure.

1. Rozhodnou se vytvořit **SQL Database** v Azure.

    ![Zřízení SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

2. Zadají název databáze, který odpovídá databázi spuštěné na místním virtuálním počítači (**SmartHotel.Registration**). Umístí tuto databázi do skupiny prostředků ContosoRG. Jedná se o skupinu prostředků, kterou používají pro produkční prostředky v Azure.

    ![Zřízení SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

3. V primární oblasti nastaví novou instanci SQL Serveru (**sql-smarthotel-eus2**).

    ![Zřízení SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

4. Nastaví cenovou úroveň tak, aby odpovídala potřebám serveru a databáze. A rozhodnou se ušetřit prostřednictvím programu Zvýhodněné hybridní využití Azure, protože už mají licenci SQL Serveru.
5. K nastavení velikosti využijí nákupní model založený na virtuálních jádrech a nastaví omezení pro očekávané požadavky.

    ![Zřízení SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

6. Potom vytvoří instanci databáze.

    ![Zřízení SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

7. Po vytvoření instance otevřou databázi a poznamenají si podrobnosti, které potřebují při migraci pomocí Data Migration Assistanta.

    ![Zřízení SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)

**Potřebujete další pomoc?**

- [Pomoc](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) se zřizováním SQL Database
- [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) o omezeních prostředků virtuálních jader

## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a>Krok 2: vytvoření ACR a zřízení kontejneru Azure

Kontejner Azure se vytvoří pomocí exportovaných souborů z webového virtuálního počítače. Kontejner je umístěný ve službě v Azure Container Registry (ACR).

1. Správci Contoso vytvoří na webu Azure Portal službu Container Registry.

     ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

2. Zadají název registru (**contosoacreus2**) a umístí ho v primární oblasti, a to ve skupině prostředků, kterou využívají pro prostředky infrastruktury. Povolí přístup pro uživatele s oprávněními správce a nastaví ho jako SKU úrovně Premium, aby bylo možné používat geografickou replikaci.

    ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)

## <a name="step-3-provision-azure-service-fabric"></a>Krok 3: zřízení Service Fabric Azure

Kontejner SmartHotel360 poběží v clusteru služby Azure Service Fabric. Správci společnosti Contoso vytvoří cluster Service Fabric následujícím způsobem:

1. Vytvoří prostředek služby Service Fabric z Azure Marketplace.

     ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

2. Na kartě **Základní informace** pro cluster zadají jedinečný název DS a přihlašovací údaje pro přístup k místnímu virtuálnímu počítači. Prostředek umístí do skupina produkčních prostředků (**ContosoRG**) v primární oblasti Východní USA 2.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png)

3. V části **Konfigurace typu uzlu** zadají název typu uzlu, nastavení stálosti, velikost virtuálního počítače a koncové body aplikace.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png)

4. V části **Vytvořit trezor klíčů** ve své skupině prostředků infrastruktury vytvoří nový trezor klíčů pro uložení certifikátu.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png)

5. V části **Zásady přístupu** povolí přístup k virtuálním počítačům pro nasazení trezoru klíčů.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png)

6. Zadají název tohoto certifikátu.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png)

7. Na stránce se souhrnem zkopírují odkaz, který se používá ke stažení certifikátu. Potřebují ho pro připojení ke clusteru Service Fabric.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png)

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png)

8. Po úspěšném ověření zřídí cluster.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png)

9. V Průvodci importem certifikátu naimportují stažený certifikát do vývojářských počítačů. Tento certifikát se používá k ověření pro cluster.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png)

10. Po zřízení clusteru se připojí k Service Fabric Exploreru.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png)

11. Musí vybrat správný certifikát.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png)

12. Service Fabric Explorer načte a správce společnosti Contoso může začít spravovat cluster.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png)

## <a name="step-4-manage-service-fabric-certificates"></a>Krok 4: Správa certifikátů Service Fabric

Contoso potřebuje certifikáty clusteru pro umožnění přístupu Azure DevOps Services ke clusteru. Správci Contoso je nastaví.

1. Otevřou Azure Portal a přejdou ke službě Key Vault.
2. Otevřou certifikáty a zkopírují kryptografický otisk certifikátu vytvořený během procesu zřizování.

    ![Zkopírování kryptografického otisku](./media/contoso-migration-rearchitect-container-sql/cert1.png)

3. Zkopírují ho do textového souboru pro pozdější referenci.
4. Teď přidají klientský certifikát, který se stane klientským certifikátem správce v clusteru. To sadě Azure DevOps Services umožňuje připojit se ke clusteru pro nasazení aplikace v kanálu verze. Otevřou proto Key Vault na portálu a vyberou **Certifikáty** > **Vygenerovat nebo importovat**.

    ![Generování klientského certifikátu](./media/contoso-migration-rearchitect-container-sql/cert2.png)

5. Zadají název certifikátu a do pole **Předmět** zadají rozlišující název X. 509.

     ![Název certifikátu](./media/contoso-migration-rearchitect-container-sql/cert3.png)

6. Certifikát po vytvoření stáhnou do místního prostředí ve formátu PFX.

     ![Stažení certifikátu](./media/contoso-migration-rearchitect-container-sql/cert4.png)

7. Nyní se vrátí zpátky k seznamu certifikátů ve službě Key Vault a zkopírují kryptografický otisk klientského certifikátu, který byl právě vytvořen. Uloží ho do textového souboru.

     ![Kryptografický otisk klientského certifikátu](./media/contoso-migration-rearchitect-container-sql/cert5.png)

8. Pro nasazení Azure DevOps Services musí zjistit hodnotu Base64 tohoto certifikátu. Použijí k tomu místní vývojářskou pracovní stanici a PowerShell. Výstup vloží do textového souboru pro pozdější použití.

    ```powershell
    [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx"))
    ```

     ![Hodnota Base64](./media/contoso-migration-rearchitect-container-sql/cert6.png)

9. Nakonec nový certifikát přidají do clusteru Service Fabric. Udělají to tak, že cluster otevřou na portálu a vyberou **Zabezpečení**.

     ![Přidání klientského certifikátu](./media/contoso-migration-rearchitect-container-sql/cert7.png)

10. Vyberou **Přidat** > **Klientský certifikát správce** a vloží kryptografický otisk do nového klientského certifikátu. Potom vyberou **Přidat**. Tento proces může trvat až 15 minut.

     ![Přidání klientského certifikátu](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a>Krok 5: migrace databáze pomocí DMA

Správci Contoso teď mohou migrovat databázi SmartHotel360 pomocí DMA.

### <a name="install-dma"></a>Instalace DMA

1. Tento nástroj si stáhnou z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) do místního virtuálního počítače s SQL Serverem (**SQLVM**).
2. Na tomto virtuálním počítači spustí instalační program (DownloadMigrationAssistant.msi).
3. Před dokončením průvodce na stránce **Finish** (Dokončit) vyberou **Launch Microsoft Data Migration Assistant** (Spustit nástroj Microsoft Data Migration Assistant).

### <a name="configure-the-firewall"></a>Konfigurace firewallu

Aby se mohli připojit k Azure SQL Database, správci společnosti Contoso nastaví pravidlo brány firewall pro povolení přístupu.

1. Ve vlastnostech databáze **Brána firewall a virtuální sítě** umožní přístup ke službám Azure a přidají pravidlo pro IP adresu klienta místního virtuálního počítače s SQL Serverem.
2. Vytvoří se pravidlo brány firewall na úrovni serveru.

    ![Brána firewall](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

**Potřebujete další pomoc?**

[Seznamte se](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) s vytvářením a správou pravidel brány firewall pro Azure SQL Database.

### <a name="migrate"></a>Migrace

Správci společnosti Contoso teď migrují databázi.

1. V DMA vytvoří nový projekt (**SmartHotelDB**) a vyberou **Migration** (Migrace).
2. Jako typ zdrojového serveru vyberou **SQL Server** a jako typ cílového serveru zvolí **Azure SQL Database**.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

3. V podrobnostech o migraci doplní **SQLVM** jako zdrojový server a databázi **SmartHotel.Registration**.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

4. Zobrazí se jim chyba, která zdánlivě souvisí s ověřováním. Po prozkoumání ale zjistí, že problém způsobuje tečka (.) v názvu databáze. Jako alternativní řešení se rozhodnou zřídit novou databázi SQL s použitím názvu **SmartHotel-Registration**. Při opětovném spuštění DMA už mohou vybrat **SmartHotel-Registration** a pokračovat v průvodci.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

5. V části **Vybrat objekty** vyberou databázové tabulky a vygenerují skript SQL.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

6. Jakmile DMA vytvoří tento skript, vyberou **Nasadit schéma**.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

7. DMA potvrdí, že nasazení proběhlo úspěšně.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

8. Teď zahájí vlastní migraci.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

9. Po dokončení migrace mohou správci Contoso ověřit, jestli je databáze spuštěná v instanci SQL Azure.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

10. Přebytečnou databázi SQL nazvanou **SmartHotel.Registration** odstraní na webu Azure Portal.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)

## <a name="step-6-set-up-azure-devops-services"></a>Krok 6: nastavení Azure DevOps Services

Contoso pro tuto aplikaci potřebuje sestavit kanály a infrastrukturu DevOps. Správci Contoso k tomuto účelu vytvoří nový projekt Azure DevOps, naimportují kód a potom nastaví kanály buildu a verze.

1. V účtu Azure DevOps společnosti Contoso vytvoří nový projekt (**ContosoSmartHotelRearchitect**) a pro správu verzí vyberou **Git**.
![Nový projekt](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

2. Naimportují úložiště Git, ve kterém je v současné době uložený kód aplikace. Je ve [veřejném úložišti](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) a můžete si ho stáhnout.

    ![Stažení kódu aplikace](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

3. Po naimportování kódu k tomuto úložišti připojí sadu Visual Studio a naklonují kód pomocí Team Exploreru.

4. Když je úložiště ve vývojářském počítači naklonované, otevřou pro tuto aplikaci soubor řešení. Webová aplikace a služba wcf mají v tomto souboru samostatný projekt.

    ![Soubor řešení](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a>Krok 7: převod aplikace na kontejner

Místní aplikace je tradiční třívrstvá aplikace:

- Obsahuje WebForms a službu WCF, která se připojuje k SQL Serveru.
- Používá Entity Framework k integraci s daty v SQL Database a zpřístupňuje ji prostřednictvím služby WCF.
- Aplikace WebForms komunikuje se službou WCF.

Správci společnosti Contoso převedou aplikaci na kontejner pomocí sady Visual Studio a nástrojů SDK Tools, a to následujícím způsobem:

1. Pomocí sady Visual Studio si projdou otevřený soubor řešení (SmartHotel. Registration. sln) v adresáři **SmartHotel360-internal-booking-apps\src\Registration**místního úložiště. Zobrazí se dvě aplikace. Webový front-end SmartHotel.Registring.Web a aplikace služby WCF SmartHotel.Registration.WCF.

    ![Kontejner](./media/contoso-migration-rearchitect-container-sql/container2.png)

2. Pravým tlačítkem myši na kliknou na webovou aplikaci > **Přidat** > **Podpora orchestrátoru kontejnerů**.
3. V části **Přidat podporu orchestrátoru kontejnerů** vyberou **Service Fabric**.

    ![Kontejner](./media/contoso-migration-rearchitect-container-sql/container3.png)

4. Tento proces zopakují i pro aplikaci SmartHotel.Registration.WCF.
5. Potom zkontrolují, jak se řešení změnilo.

    - Nová aplikace má název **SmartHotel.RegistrationApplication/**
    - Obsahuje dvě služby: **SmartHotel. Registration. WCF** a **SmartHotel. Registration. Web**.

    ![Kontejner](./media/contoso-migration-rearchitect-container-sql/container4.png)

6. Sada Visual Studio vytvořila soubor Docker a stáhla požadované image místně do vývojářského počítače.

    ![Kontejner](./media/contoso-migration-rearchitect-container-sql/container5.png)

7. Sada Visual Studio vytvořila a otevřela soubor manifestu (**ServiceManifest.xml**). Tento soubor říká službě Service Fabric, jak nakonfigurovat kontejner při jeho nasazení do Azure.

    ![Kontejner](./media/contoso-migration-rearchitect-container-sql/container6.png)

8. Jiný soubor manifestu (**ApplicationManifest.xml) obsahuje konfigurační aplikace pro kontejnery.

    ![Kontejner](./media/contoso-migration-rearchitect-container-sql/container7.png)

9. Otevřou soubor **ApplicationParameters/Cloud.xml** a aktualizují připojovací řetězec pro připojení aplikace k databázi Azure SQL. Tento připojovací řetězec je umístěný v databázi na webu Azure Portal.

    ![Připojovací řetězec](./media/contoso-migration-rearchitect-container-sql/container8.png)

10. Potvrdí aktualizovaný kód a nasdílejí změny do Azure DevOps Services.

    ![Potvrzení](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a>Krok 8: kanály sestavení a vydání v Azure DevOps Services

Správci společnosti Contoso teď nakonfigurují Azure DevOps Services, aby mohli provést proces sestavení a vydání a zprovoznit postupy DevOps.

1. V Azure DevOps zvolí **Build and release** > **Nový kanál**.

    ![Nový kanál](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

2. Vyberou **Git Azure DevOps Services** a relevantní úložiště.

    ![Git a úložiště](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

3. V části **Vybrat šablonu** vyberou prostředky infrastruktury s podporou Dockeru.

     ![Fabric a Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)

4. V poli Akce nastaví **Build an image** (Sestavit image) a nakonfigurují úlohu tak, aby využívala zřízenou službu ACR.

     ![Registr](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

5. V úloze **Push images** nakonfigurují image, která se nabídne do ACR, a vyberou, že se má zahrnout nejnovější značka.
6. V části **Triggers** (Aktivační události) povolí kontinuální integraci a přidají hlavní větev.

    ![Aktivační události](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

7. Výběrem **Uložit a zařadit do fronty** spustí build.
8. Po úspěšném sestavení přejdou ke kanálu verzí. V Azure DevOps Services zvolí **Vydání** > **Nový kanál**.

    ![Kanál verze](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)

9. Vyberou šablonu **nasazení Azure Service Fabric** a pojmenují fázi (**SmartHotelSF**).

    ![Prostředí](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

10. Zadají název kanálu (**ContosoSmartHotel360Rearchitect**). Pro fázi si vyberou **1 úloha, 1 úkol** pro konfiguraci nasazení služby Service Fabric.

    ![Fáze a úkol](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

11. Potom vyberou **Nové** a přidají nové připojení clusteru.

    ![Nové připojení](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

12. V části **Add Service Fabric service connection** (Přidat připojení služby Service Fabric) nakonfigurují toto připojení a nastavení ověřování, která bude služba Azure DevOps Services využije k nasazení aplikace. Koncový bod clusteru se dá najít na webu Azure Portal. Jako předponu přidají **tcp://** .

13. Informace o certifikátu, které zjistili, zadají do polí **Kryptografický otisk certifikátu serveru** a **Klientský certifikát**.

    ![Certifikát](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

14. Vyberou kanál > **Přidat artefakt**.

     ![Artefakt](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

15. Vyberou projekt a kanál buildu a použijí nejnovější verzi.

     ![Build](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

16. Všimněte si, že ikona blesku na artefaktu je zaškrtnutá.

     ![Stav artefaktu](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

17. Dál si všimněte, že je povolená aktivace průběžného nasazování.
   ![Povolené průběžné nasazování](./media/contoso-migration-rearchitect-container-sql/pipeline14.png)

18. Vyberou **Uložit** > **Vytvořit novou vydanou verzi**.

    ![Vydání](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

19. Po dokončení nasazení SmartHotel360 poběží ve službě Service Fabric.

    ![Publikování](./media/contoso-migration-rearchitect-container-sql/publish4.png)

20. Pro připojení k aplikaci směrují provoz na veřejnou IP adresu nástroje pro vyrovnávání zatížení Azure před uzly Service Fabric.

    ![Publikování](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a>Krok 9: rozšiřování aplikace a opětovné publikování

Když jsou databáze a aplikace SmartHotel360 spuštěné v Azure, Contoso chce tuto aplikaci rozšířit.

- Vývojáři společnosti Contoso využívají vytváření prototypů nové aplikace .NET Core, která se spustí v clusteru Service Fabric.
- Tato aplikace se bude využívat k vyžádání údajů o mínění z Cosmos DB.
- Tato data budou ve formě tweetů, která se zpracovávají pomocí bezserverové funkce Azure a rozhraní API pro analýzu textu v Azure Cognitive Services.

### <a name="provision-azure-cosmos-db"></a>Zřízení Azure Cosmos DB

V prvním kroku zřídí správci společnosti Contoso databázi Azure Cosmos.

1. Vytvoří prostředek Azure Cosmos DB z Azure Marketplace.

    ![Rozšíření](./media/contoso-migration-rearchitect-container-sql/extend1.png)

2. Zadají název databáze (**contososmarthotel**), vyberou rozhraní SQL API a umístí prostředek pro skupiny produkčních prostředků v primární oblasti Východní USA 2.

    ![Rozšíření](./media/contoso-migration-rearchitect-container-sql/extend2.png)

3. V části **Začínáme** vyberou **Data Explorer** a přidají novou kolekci.
4. V části **Přidat kolekci** zadají příslušná ID a nastaví propustnost a kapacitu úložiště.

    ![Rozšíření](./media/contoso-migration-rearchitect-container-sql/extend3.png)

5. Na portálu otevřou tuto novou databázi > **Kolekce** > **Dokumenty** a vyberou **Nový dokument**.
6. Do okna dokumentu vloží následující kód JSON. Toto jsou ukázková data ve formě jednoho tweetu.

    ```json
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500,
            "hashtags": [
                ""
            ]
    }
    ```

    ![Rozšíření](./media/contoso-migration-rearchitect-container-sql/extend4.png)

7. Vyhledají ověřovací klíč a koncový bod Cosmos DB. Aplikace je využívá pro připojení ke kolekci. V databázi vyberou **Klíče** a zkopírují URI a primární klíč do Poznámkového bloku.

    ![Rozšíření](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a>Aktualizace aplikace zjišťování mínění

Když je služba Cosmos DB zřízená, správci Contoso mohou nakonfigurovat aplikaci tak, aby se k ní připojovala.

1. V sadě Visual Studio otevřou soubor ApplicationModern\ApplicationParameters\cloud.xml v Průzkumníku řešení.

    ![Aplikace zjišťování mínění](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

2. Doplní následující dva parametry:

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Aplikace zjišťování mínění](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a>Opětovné publikování aplikace

Po rozšíření aplikace ji správci společnosti Contoso znovu publikují do Azure pomocí kanálu.

1. Potvrdí kód a nasdílejí ho do Azure DevOps Services. Tím se aktivují kanály buildu a verze.

2. Po dokončení sestavení a nasazení SmartHotel360 poběží ve službě Service Fabric. Konzola pro správu Service Fabric teď zobrazuje tři služby.

    ![Opětovné publikování](./media/contoso-migration-rearchitect-container-sql/republish3.png)

3. Mohou se teď těmito službami proklikat a vidí, že aplikace SentimentIntegration je spuštěná.

    ![Opětovné publikování](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace společnost Contoso potřebuje provést tyto kroky čištění:

- Odebrat místní virtuální počítače z inventáře vCenter
- Odebrat virtuální počítače z úloh místního zálohování
- Aktualizovat interní dokumentaci tak, aby obsahovala nová umístění pro aplikaci SmartHotel360 Zobrazit databázi jako spuštěnou v databázi Azure SQL a front-end jako spuštěný ve službě Service Fabric
- Zkontrolovat všechny prostředky, které s vyřazenými virtuálními počítači spolupracují, a aktualizovat veškeré související nastavení nebo dokumentaci tak, aby odrážely novou konfiguraci

## <a name="review-the-deployment"></a>Kontrola nasazení

Teď, když má prostředky migrované do Azure, společnost Contoso potřebuje plně zprovoznit a zabezpečit novou infrastrukturu.

### <a name="security"></a>Zabezpečení

- Správci Contoso potřebují zajistit, že nová databáze **SmartHotel-Registration** je zabezpečená. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Měli by zejména aktualizovat kontejner, aby využíval SSL s certifikáty.
- Měli by zvážit použití služby Key Vault k ochraně tajných kódů pro aplikace Service Fabric. [Další informace](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups"></a>Zálohování

- Společnost Contoso potřebuje zkontrolovat požadavky na zálohování databáze Azure SQL Database. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Správci Contoso by měli zvážit implementaci skupin převzetí služeb při selhání a zajistit tak regionální převzetí služeb při selhání pro databázi. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Pro SKU ACR úrovně Premium mohou využít výhody geografické replikace. [Další informace](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Contoso musí zvážit nasazení webové aplikace v hlavní oblasti Východní USA 2 a v oblasti Střední USA, až bude dostupná funkce Web App for Containers. Správci Contoso mohou nakonfigurovat Traffic Manager, aby zajistili převzetí služeb při selhání v případě regionálních výpadků.
- Databáze Cosmos DB se zálohuje automaticky. Contoso si o tomto procesu [čte](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore), aby se dozvěděla víc.

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- Po nasazení všech prostředků by společnost Contoso měla na základě [plánování infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging) přiřadit značky Azure.
- Veškeré licencování je součástí nákladů na služby PaaS, které společnost Contoso spotřebovává. Náklady se odečtou ze smlouvy EA.
- Společnost Contoso povolí službu Azure Cost Management licencovanou společností Cloudyn, dceřinou společností Microsoftu. Jedná se o multicloudové řešení správy nákladů, které pomáhá využívat a spravovat Azure a další cloudové prostředky. Přečtěte si [další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management.

## <a name="conclusion"></a>Závěr

V tomto článku společnost Contoso refaktorovala aplikaci SmartHotel360 v Azure migrací jejího front-endového virtuálního počítače do služby Service Fabric. Databáze aplikace se migrovala do databáze SQL Azure.
