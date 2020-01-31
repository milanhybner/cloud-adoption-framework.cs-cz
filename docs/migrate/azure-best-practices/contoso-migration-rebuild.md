---
title: Opětovné sestavení místní aplikace do Azure
description: Přečtěte si, jak Contoso opětovně sestaví aplikaci do Azure pomocí služeb Azure App Service, Azure Kubernetes Service, Cosmos DB, Azure Functions a Azure Cognitive Services.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: e2904356871eec65b516b7a02c356c679ab86b33
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807491"
---
# <a name="rebuild-an-on-premises-app-on-azure"></a>Opětovné sestavení místní aplikace v Azure

Tento článek ukazuje, jak fiktivní společnost Contoso v rámci migrace do Azure opětovně sestaví dvouvrstvou aplikaci platformy Windows .NET, která běží na virtuálních počítačích VMware. Contoso migruje virtuální počítač front-endu aplikace do webové aplikace služby Azure App Service. Back-end aplikace je sestaven pomocí mikroslužeb nasazených do kontejnerů spravovaných službou Azure Kubernetes Service (AKS). Web komunikuje se službou Azure Functions, která poskytuje funkci pro zpracování fotek domácích zvířat.

Aplikace SmartHotel360 použitá v tomto příkladu je k dispozici jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s partnery ve firmě, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Společnost Contoso roste a chce na webech společnosti Contoso zákazníkům poskytovat diferencovaná prostředí.
- **Agilita.** K zajištění úspěchu v globální ekonomice je nutné, aby společnost Contoso dokázala reagovat rychleji, než jak dochází ke změnám na trhu.
- **Škálování** Společnost Contoso úspěšně roste a její tým IT musí poskytovat systémy, které jsou schopné růst stejným tempem.
- **Snížení nákladů.** Společnost Contoso chce minimalizovat náklady na licencování.

## <a name="migration-goals"></a>Cíle migrace

Tým společnosti Contoso pro přechod do cloudu specifikoval požadavky na aplikace u této migrace. Tyto požadavky se použily k určení nejlepší metody migrace:

- Aplikace v Azure bude nadále stejně důležitá, jako je dnes. Měla by dobře fungovat a snadno se škálovat.
- Aplikace by neměla používat komponenty infrastruktury jako služby (IaaS). Všechno by mělo být sestavené tak, aby se používal model PaaS nebo bezserverové služby.
- Sestavení aplikací by se měla spouštět v cloudových službách a kontejnery by se měly nacházet v privátním celopodnikovém registru kontejnerů v cloudu.
- Služba rozhraní API používaná pro fotky domácích zvířat by měla být při běžném používání přesná a spolehlivá, protože rozhodnutí učiněná v aplikaci musí být respektována v příslušných hotelech. Každé domácí zvíře s povoleným přístupem se může v hotelech ubytovat.
- Kvůli splnění požadavků na kanál DevOps bude společnost Contoso používat Azure DevOps pro správu zdrojového kódu a úložiště Git. K sestavování kódu a nasazování do služeb Azure App Service, Azure Functions a AKS bude použito automatizované sestavování a vydávání verzí.
- Pro back-endové mikroslužby a front-endový web jsou potřeba různé kanály CI/CD.
- Back-endové služby mají jiný cyklus vydávání verzí než front-endová webová aplikace. Aby se tento požadavek splnil, nasadí dva různé kanály.
- Společnost Contoso potřebuje, aby úplné nasazení front-endového webu schvaloval management, a kanál CI-CD musí tuto možnost poskytovat.

## <a name="solution-design"></a>Návrh řešení

Po specifikaci cílů a požadavků společnost Contoso navrhne a zkontroluje řešení nasazení a určí proces migrace včetně služeb Azure, které se budou k migraci používat.

### <a name="current-app"></a>Aktuální aplikace

- Místní aplikace SmartHotel360 je rozvrstvená na dva virtuální počítače (WEBVM a SQLVM).
- Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com** (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) spuštěný na virtuálním počítači.
- Contoso má místní datacentrum (contoso-datacenter) s místním řadičem domény (**contosodc1**).
- Po dokončení migrace budou místní virtuální počítače v datacentru společnosti Contoso vyřazeny z provozu.

### <a name="proposed-architecture"></a>Navrhovaná architektura

- Front-end aplikace je nasazen jako Azure App Service webová aplikace v primární oblasti Azure.
- Služba Azure Functions poskytuje funkci pro odesílání fotek domácích zvířat a web tuto funkci používá.
- Funkce pro odesílání fotek domácích zvířat používá rozhraní API pro počítačové zpracování obrazu služby Azure Cognitive Services a databázi Cosmos DB.
- Back-end webu je sestaven pomocí mikroslužeb. Ty budou nasazeny do kontejnerů spravovaných službou Azure Kubernetes Service (AKS).
- Kontejnery budou sestaveny pomocí Azure DevOps a nasdíleny do registru kontejnerů Azure Container Registry (ACR).
- Prozatím společnost Contoso nasadí webovou aplikaci a kód funkce ručně pomocí sady Visual Studio.
- Mikroslužby budou nasazeny pomocí skriptu PowerShellu, který volá nástroje příkazového řádku Kubernetes.

    ![Architektura scénáře](./media/contoso-migration-rebuild/architecture.png)

### <a name="solution-review"></a>Revize řešení

Společnost Contoso vyhodnotí vytvořený návrh sestavením seznamu výhod a nevýhod.

<!-- markdownlint-disable MD033 -->

**Aspekty** | **Podrobnosti**
--- | ---
**Výhody** | Použití modelu PaaS a bezserverového řešení pro kompletní nasazení významně zkracuje čas potřebný pro správu, kterou společnost Contoso musí poskytovat.<br/><br/> Přechod na architekturu s mikroslužbami umožní společnosti Contoso řešení postupně snadno rozšiřovat.<br/><br/> Nové funkce je možné zprovoznit online, aniž by došlo k narušení základů kódu existujících řešení.<br/><br/> Webová aplikace bude nakonfigurována s několika instancemi bez kritického prvku způsobujícího selhání.<br/><br/> Bude povolené automatické škálování, aby aplikace mohla zpracovávat různé objemy přenosů dat.<br/><br/> Díky přechodu na služby PaaS může společnost Contoso vyřadit z provozu zastaralá řešení spouštěná v operačním systému Windows Server 2008 R2.<br/><br/> Databáze Cosmos DB má integrovanou odolnost proti chybám, která nevyžaduje žádné konfigurování ze strany společnosti Contoso. To znamená, že datová vrstva už nebude jediným bodem převzetí služeb při selhání.
**Nevýhody** | Kontejnery jsou složitější než ostatní možnosti migrace. Křivka osvojování znalostí by mohla být pro společnost Contoso problémem. Zavádějí zcela novou úroveň složitosti, která má i přes tuto strmou křivku řadu předností.<br/><br/> Provozní tým ve společnosti Contoso musí získat nové znalosti, aby porozuměl Azure, kontejnerům a mikroslužbám pro aplikaci a dokázal je podporovat.<br/><br/> Společnost Contoso nemá plně implementované DevOps pro celé řešení. To musí společnost Contoso brát v úvahu také při nasazování služeb do AKS, Azure Functions a Azure App Service.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migrace

1. Společnost Contoso zřídí služby ACR, AKS a databázi Cosmos DB.
2. Zřídí infrastrukturu pro nasazení včetně webové aplikace služby Azure App Service, účtu úložiště, funkce a rozhraní API.
3. Po vytvoření infrastruktury sestaví image kontejnerů mikroslužeb pomocí služby Azure DevOps, která je nasdílí do ACR.
4. Společnost Contoso tyto mikroslužby nasadí do AKS pomocí skriptu PowerShellu.
5. Nakonec nasadí příslušnou funkci a webovou aplikaci.

    ![Proces migrace](./media/contoso-migration-rebuild/migration-process.png)

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Zjednodušuje správu, nasazení a provoz prostředí Kubernetes. Poskytuje plně spravovanou službu orchestrace kontejnerů Kubernetes. | AKS je bezplatná služba. Platíte jenom za virtuální počítače a spotřebované přidružené prostředky úložišť a síťové prostředky. [Další informace](https://azure.microsoft.com/pricing/details/kubernetes-service).
[Azure Functions](https://azure.microsoft.com/services/functions) | Urychluje vývoj pomocí bezserverového výpočetního prostředí založeného na událostech. Umožňuje škálování na vyžádání. | Platíte jenom za spotřebované prostředky. Plán se účtuje v závislosti na využití prostředků za sekundu a počtu spuštění. [Další informace](https://azure.microsoft.com/pricing/details/functions).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Ukládá image pro všechny typy kontejnerových nasazení. | Náklady závisí na funkcích, úložišti a délce využití. [Další informace](https://azure.microsoft.com/pricing/details/container-registry).
[Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Využijte možnost rychlého sestavení, nasazení a škálování webových, mobilních a API aplikací na podnikové úrovni, které běží na libovolné platformě. | Plány služby App Service se účtují po sekundách. [Další informace](https://azure.microsoft.com/pricing/details/app-service/windows).

## <a name="prerequisites"></a>Požadavky

Tady je seznam toho, co Contoso k realizaci tohoto scénáře potřebuje:

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Společnost Contoso vytvořila předplatná v jednom z předchozích článků. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.
**Infrastruktura Azure** | [Přečtěte si](./contoso-migration-infrastructure.md) o tom, jak společnost Contoso nastavila infrastrukturu Azure.
**Požadavky na vývojáře** | Společnost Contoso potřebuje na vývojářské pracovní stanici následující nástroje:<br/><br/> - [Visual Studio 2017 Community Edition: verze 15,5](https://www.visualstudio.com)<br/><br/> Povolené úlohy .NET<br/><br/> [Git](https://git-scm.com)<br/><br/> [Azure PowerShell](https://azure.microsoft.com/downloads)<br/><br/> [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)<br/><br/> [Docker CE (Windows 10) nebo Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) nastavený pro použití kontejnerů Windows.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Contoso provede migraci takto:

> [!div class="checklist"]
>
> - **Krok 1: zřízení AKS a ACR.** Společnost Contoso zřídí spravovaný cluster služby AKS a registr kontejnerů Azure pomocí PowerShellu.
> - **Krok 2: sestavení kontejnerů Docker.** Nastaví kontinuální integraci (CI) pro kontejnery Dockeru pomocí Azure DevOps a nasdílí je do ACR.
> - **Krok 3: nasaďte back-end mikroslužby.** Nasadí zbývající infrastrukturu, kterou budou používat back-endové mikroslužby.
> - **Krok 4: nasazení front-endové infrastruktury** Nasadí front-endovou infrastrukturu včetně úložiště objektů blob pro fotky domácích zvířat, databáze Cosmos DB a rozhraní API pro počítačové zpracování obrazu.
> - **Krok 5: migrace back-endu.** Nasadí mikroslužby, spustí je ve službě AKS a provede migraci back-endu.
> - **Krok 6: publikování front-endu.** Publikují aplikaci SmartHotel360 do služby App Service a aplikaci funkcí, která bude volána službou pro domácí zvířata.

## <a name="step-1-provision-back-end-resources"></a>Krok 1: zřízení prostředků back-endu

Správci společnosti Contoso spuštěním skriptu nasazení vytvoří spravovaný cluster Kubernetes pomocí služby AKS a registru kontejnerů Azure Container Registry (ACR).

- Pokyny v této části používají úložiště **SmartHotel360-Azure-backend**.
- Úložiště **SmartHotel360-Azure-backend** v GitHubu obsahuje veškerý software pro tuto část nasazování.  

### <a name="ensure-prerequisites"></a>Zajištění požadavků

1. Než začnete, správci společnosti Contoso zajistěte, aby byl veškerý požadovaný software nainstalovaný na vývojovém počítači, který používají pro nasazení.
2. Úložiště naklonují místně do tohoto počítače pro vývoj pomocí Gitu: `git clone https://github.com/Microsoft/SmartHotel360-Azure-backend.git`

### <a name="provision-aks-and-acr"></a>Zřízení AKS a ACR

Správci společnosti Contoso zřídí tyto služby takto:

1. Otevřou složku pomocí Visual Studio Code a přesune se do adresáře **/Deploy/k8s** , který obsahuje skript **gen-AKS-env. ps1**.

2. Spuštěním tohoto skriptu vytvoří spravovaný cluster Kubernetes pomocí služeb AKS a ACR.

   ![AKS](./media/contoso-migration-rebuild/aks1.png)

3. V otevřeném souboru aktualizují parametr $location na **eastus2** a soubor uloží.

   ![AKS](./media/contoso-migration-rebuild/aks2.png)

4. V editoru Visual Studio Code vyberou **Zobrazit** > **Integrovaný terminál** a otevřou integrovaný terminál.

   ![AKS](./media/contoso-migration-rebuild/aks3.png)

5. V integrovaném terminálu PowerShellu se přihlásí do Azure pomocí příkazu Connect-AzureRmAccount. [Přečtěte si další informace](https://docs.microsoft.com/powershell/azure/get-started-azureps) o tom, jak začít používat PowerShell.

   ![AKS](./media/contoso-migration-rebuild/aks4.png)

6. Ověří Azure CLI tak, že spustí příkaz **az login** a postupem podle pokynů provedou ověření pomocí webového prohlížeče. [Přečtěte si další informace](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) o přihlašování pomocí Azure CLI.

   ![AKS](./media/contoso-migration-rebuild/aks5.png)

7. Spustí následující příkaz a předají název skupiny prostředků ContosoRG, název clusteru služby AKS smarthotel-aks-eus2 a název nového registru.

   ```PowerShell
   .\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2
   ```

   ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. Azure vytvoří další skupinu prostředků, která obsahuje prostředky pro cluster služby AKS.

   ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. Po dokončení nasazování nainstalují nástroj příkazového řádku **kubectl**. V Azure CloudShell je tento nástroj už nainstalovaný.

   ```console
   az aks install-cli
   ```

10. Spuštěním příkazu **kubectl get nodes** ověří připojení ke clusteru. Tento uzel má stejný název jako virtuální počítač v automaticky vytvořené skupině prostředků.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. Spuštěním následujícího příkazu spustí řídicí panel Kubernetes:

    ```console
    az aks browse --resource-group ContosoRG --name smarthotelakseus2
    ```

12. Otevře se záložka prohlížeče s řídicím panelem. Toto je tunelové připojení pomocí Azure CLI.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)

## <a name="step-2-configure-the-back-end-pipeline"></a>Krok 2: Konfigurace kanálu back-endu

### <a name="create-an-azure-devops-project-and-build"></a>Vytvoření projektu Azure DevOps a sestavení

Společnost Contoso vytvoří projekt Azure DevOps, nakonfiguruje sestavení CI, aby se vytvořil kontejner, a pak ho nasdílí do ACR. Pokyny v této části používají úložiště [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).

1. Na webu visualstudio.com vytvoří novou organizaci (**contosodevops360.visualstudio.com**) a nakonfigurují jí tak, aby používala Git.

2. Vytvoří nový projekt (**SmartHotelBackend**) pomocí Gitu pro správu verzí a agilních nástrojů pro pracovní postup.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png)

3. Naimportují [úložiště GitHub](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png)

4. V části **Pipelines** (Kanály) vyberou **Build** (Sestavení) a z úložiště vytvoří nový kanál. Jako zdroj použijí Azure Repos Git.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png)

5. Rozhodnou se začít s prázdnou úlohou.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)

6. Jako kanál buildu vyberou **Hosted Linux Preview** (Verze Preview hostovaného Linuxu).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png)

7. V **1. fázi** přidají úlohu **Docker Compose**. Tato úloha sestaví Docker Compose.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png)

8. Postup zopakují a přidají další úlohu **Docker Compose**. Tato úloha nasdílí kontejnery do registru ACR.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)

9. Vyberou první úlohu (pro sestavení) a nakonfigurují sestavení s předplatným Azure, autorizací a registrem ACR.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

10. Určí cestu k souboru **docker-compose.yaml** ve složce **src** v úložišti. Vyberou sestavení image služby a zahrnutí nejnovější značky. Když se akce změní na **Build service images** (Sestavit image služeb), změní se název úlohy Azure DevOps na **Build services automatically** (Sestavovat služby automaticky).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

11. Nyní nakonfigurují druhou úlohu Dockeru (pro nasdílení). Vyberou předplatné a registr ACR **smarthotelacreus2**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

12. Znovu zadají soubor do souboru docker-compose.yaml, vyberou **Push service images** (Nasdílet image služeb) a zahrnou nejnovější značku. Když se akce změní na **Push service images** (Nasdílet image služeb), změní se název úlohy Azure DevOps na **Push services automatically** (Sdílet služby automaticky).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

13. Když jsou úlohy Azure DevOps nakonfigurované, uloží společnost Contoso kanál buildu a spustí proces sestavení.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

14. Když chtějí zkontrolovat postup, vyberou úlohu sestavení.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

15. Po dokončení sestavení zobrazí registr ACR nová úložiště, která se naplní kontejnery používanými mikroslužbami.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)

### <a name="deploy-the-back-end-infrastructure"></a>Nasazení back-endové infrastruktury

S vytvořeným clusterem služby AKS a sestavenými imagemi Dockeru teď správci společnosti Contoso nasadí zbývající infrastrukturu, kterou budou používat back-endové mikroslužby.

- Pokyny v této části používají úložiště [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- Ve složce **/deploy/k8s/arm** je jediný skript pro vytvoření všech položek.

Postup nasazení:

1. Otevřou Developer Command Prompt a použijí příkaz „az login“ pro příslušné předplatné Azure.
2. Zadáním následujícího příkazu nasadí pomocí souboru deploy.cmd prostředky Azure do skupiny prostředků ContosoRG a oblasti EUS2:

    ```console
    .\deploy.cmd azuredeploy ContosoRG -c eastus2
    ```

    ![Nasazení back-endu](./media/contoso-migration-rebuild/backend1.png)

3. Na webu Azure Portal si poznamenají připojovací řetězec pro každou databázi pro pozdější použití.

    ![Nasazení back-endu](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a>Vytvoření back-endového kanálu verze

Teď udělají správci společnosti Contoso následující:

- Nasadí kontroler příchozího přenosu dat NGINX a povolí tak příchozí přenos dat do těchto služeb.
- Nasadí mikroslužby do clusteru služby AKS.
- Jako první krok aktualizují připojovací řetězce na mikroslužby pomocí Azure DevOps. Pak nakonfigurují nový kanál verze Azure DevOps k nasazení těchto mikroslužeb.
- Pokyny v této části používají úložiště [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- V tomto článku se nevztahují některá nastavení konfigurace (například Active Directory B2C). Další informace o těchto nastaveních najdete v úložišti výše.

Vytvoří kanál:

1. Pomocí sady Visual Studio aktualizují soubor **/deploy/k8s/config_local.yml** a přidají do něj informace o připojení databází, které si poznamenali dříve.

    ![Připojení databází](./media/contoso-migration-rebuild/back-pipe1.png)

2. Otevřou Azure DevOps a v projektu SmartHotel360 v části **Releases** (Vydané verze), vyberou **+New Pipeline** (+Nový kanál).

    ![Nový kanál](./media/contoso-migration-rebuild/back-pipe2.png)

3. Vyberou **Empty Job** (Prázdná úloha) pro spuštění kanálu bez šablony.
4. Zadají názvy fáze a kanálu.

      ![Název fáze](./media/contoso-migration-rebuild/back-pipe4.png)

      ![Název kanálu](./media/contoso-migration-rebuild/back-pipe5.png)

5. Přidají artefakt.

     ![Přidání artefaktu](./media/contoso-migration-rebuild/back-pipe6.png)

6. Jako typ zdroje vyberou **Git** a určí projekt, zdroj a hlavní větev pro aplikaci SmartHotel360.

    ![Nastavení artefaktu](./media/contoso-migration-rebuild/back-pipe7.png)

7. Vyberou odkaz na úlohu.

    ![Odkaz na úlohu](./media/contoso-migration-rebuild/back-pipe8.png)

8. Přidají novou úlohu Azure PowerShellu, aby mohli spustit skript PowerShellu v prostředí Azure.

    ![PowerShell v Azure](./media/contoso-migration-rebuild/back-pipe9.png)

9. Vyberou předplatné Azure pro úlohu a z úložiště Git vyberou skript **deploy.ps1**.

    ![Spuštění skriptu](./media/contoso-migration-rebuild/back-pipe10.png)

10. Do skriptu přidají argumenty. Skript odstraní veškerý obsah clusteru (s výjimkou **příchozího přenosu dat** a **kontroleru příchozího přenosu**) a nasadí mikroslužby.

    ![Argumenty skriptu](./media/contoso-migration-rebuild/back-pipe11.png)

11. Upřednostňovanou verzi Azure PowerShellu nastaví na nejnovější verzi a kanál uloží.

12. Vrátí se zpátky na stránku **Releases** (Vydané verze) a ručně vytvoří novou verzi.

    ![Nová verze](./media/contoso-migration-rebuild/back-pipe12.png)

13. Vytvořenou verzi vyberou a v části **Actions** (Akce) vyberou **Deploy** (Nasadit).

      ![Nasazení verze](./media/contoso-migration-rebuild/back-pipe13.png)

14. Po dokončení nasazení spustí pomocí Azure Cloud Shellu následující příkaz, který zkontroluje stav služeb: **kubectl get services**.

## <a name="step-3-provision-front-end-services"></a>Krok 3: zřízení front-endové služby

Správci společnosti Contoso potřebují nasadit infrastrukturu, kterou budou používat front-endové aplikace. Vytvoří kontejner úložiště objektů blob pro ukládání obrázků domácích zvířat, databázi Cosmos pro ukládání dokumentů s informacemi o domácích zvířatech a rozhraní API pro počítačové zpracování obrazu pro web.

Pokyny v této části používají úložiště [SmartHotel360-public-web](https://github.com/Microsoft/SmartHotel360-public-web).

### <a name="create-blob-storage-containers"></a>Vytvoření kontejnerů služby Blob Storage

1. Na webu Azure Portal otevřou vytvořený účet úložiště a vyberou **Objekty blob**.
2. Vytvoří nový kontejner (**Pets** – domácí zvířata) s úrovní veřejného přístupu nastavenou na kontejner. Uživatelé budou do tohoto kontejneru odesílat fotky svých domácích zvířat.

    ![Objekt blob úložiště](./media/contoso-migration-rebuild/blob1.png)

3. Vytvoří druhý nový kontejner s názvem **settings** (nastavení). Do tohoto kontejneru se umístí soubor se všemi nastaveními front-endové aplikace.

    ![Objekt blob úložiště](./media/contoso-migration-rebuild/blob2.png)

4. Poznamenají si podrobnosti o přístupu k účtu úložiště do textového souboru pro budoucí referenci.

    ![Objekt blob úložiště](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-a-cosmos-database"></a>Zřízení databáze Cosmos

Správci společnosti Contoso zřídí databázi Cosmos, která se bude používat pro informace o domácích zvířatech.

1. Vytvoří prostředek **Azure Cosmos DB** v Azure Marketplace.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. Zadají název (**contosomarthotel**), vyberou rozhraní SQL API a umístí ho do produkční skupiny prostředků ContosoRG v hlavní oblasti Východní USA 2.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. Do databáze přidají novou kolekci s výchozí kapacitou a propustností.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)

4. Poznamenají si informace o připojení k databázi pro budoucí referenci.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)

### <a name="provision-computer-vision"></a>Zřízení počítačového zpracování obrazu

Správci společnosti Contoso zřídí rozhraní API pro počítačové zpracování obrazu. Toto rozhraní API bude voláno funkcí, aby se vyhodnotily obrázky odeslané uživateli.

1. Vytvoří instanci **Computer Vision** pro počítačové zpracování obrazu v Azure Marketplace.

     ![Computer Vision](./media/contoso-migration-rebuild/vision1.png)

2. Zřídí rozhraní API (**smarthotelpets**) ve skupině produkčních prostředků ContosoRG v hlavní oblasti Východní USA 2.

    ![Computer Vision](./media/contoso-migration-rebuild/vision2.png)

3. Uloží nastavení připojení rozhraní API do textového souboru pro pozdější referenci.

     ![Computer Vision](./media/contoso-migration-rebuild/vision3.png)

### <a name="provision-the-azure-web-app"></a>Zřízení webové aplikace Azure

Správci společnosti Contoso zřídí webovou aplikaci pomocí webu Azure Portal.

1. Na portálu vyberou **Webová aplikace**.

    ![Webová aplikace](media/contoso-migration-rebuild/web-app1.png)

2. Zadají název aplikace (**smarthotelcontoso**), spustí ji ve Windows a umístí ji do produkční skupiny prostředků **ContosoRG**. Vytvoří novou instanci Application Insights pro monitorování aplikací.

    ![Název webové aplikace](media/contoso-migration-rebuild/web-app2.png)

3. Když to budou mít hotové, přejdou na adresu aplikace a ověří, jestli se vytvořila úspěšně.

4. Nyní na webu Azure Portal vytvoří přípravný slot pro kód. Kanál se nasadí do tohoto slotu. Tím se zajistí, že kód nebude umístěn do produkčního prostředí, dokud správci nevydají příslušnou verzi.

    ![Přípravný slot webové aplikace](media/contoso-migration-rebuild/web-app3.png)

### <a name="provision-the-azure-function-app"></a>Zřízení aplikace funkcí Azure

Správci společnosti Contoso zřídí na webu Azure Portal aplikaci funkcí.

1. Vyberou **Function App**.

   ![Vytvoření aplikace funkcí](./media/contoso-migration-rebuild/function-app1.png)

2. Zadají název aplikace (**smarthotelpetchecker**). Aplikaci umístí do produkční skupiny prostředků **ContosoRG**. Jako hostitelské místo nastaví **Plán Consumption** a umístí aplikaci do oblasti Východní USA 2. Vytvoří se nový účet úložiště společně s instancí Application Insights pro monitorování.

   ![Nastavení aplikace funkcí](./media/contoso-migration-rebuild/function-app2.png)

3. Po nasazení aplikace přejdou na adresu aplikace a ověří, jestli se vytvořila úspěšně.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Krok 4: nastavení kanálu front-endu

Správci společnosti Contoso vytvoří dva různé projekty pro front-endový web.

1. V Azure DevOps vytvoří projekt **SmartHotelFrontend**.

   ![Front-endový projekt](./media/contoso-migration-rebuild/function-app1.png)

2. Do nového projektu naimportují úložiště Git [SmartHotel360 front end](https://github.com/Microsoft/SmartHotel360-public-web.git).

3. Pro aplikaci funkcí vytvoří další projekt Azure DevOps (SmartHotelPetChecker) a naimportují úložiště Git [PetChecker](https://github.com/sonahander/SmartHotel360-PetCheckerFunction) do tohoto projektu.

### <a name="configure-the-web-app"></a>Konfigurace webové aplikace

Teď můžou správci společnosti Contoso nakonfigurovat webovou aplikaci tak, aby používala prostředky společnosti Contoso.

1. Připojí se k projektu Azure DevOps a naklonují úložiště místně do počítače pro vývoj.
2. V sadě Visual Studio otevřou příslušnou složku a zobrazí všechny soubory v úložišti.

    ![Soubory v úložišti](./media/contoso-migration-rebuild/configure-webapp1.png)

3. Podle potřeby aktualizují změny konfigurace.

    - Když se webová aplikace spustí, hledá nastavení aplikace **SettingsUrl**.
    - Tato proměnná musí obsahovat adresu URL odkazující na konfigurační soubor.
    - Ve výchozím nastavení se použije nastavení veřejného koncového bodu.

4. Aktualizují soubor config-sample.json/sample.json.

    - Toto je konfigurační soubor pro web při použití veřejného koncového bodu.
    - Upraví oddíly **urls** a **pets_config** s použitím hodnot koncových bodů rozhraní API služby AKS, účtů úložišť a databáze Cosmos.
    - Adresy URL by se měly shodovat s názvem DNS nové webové aplikace, kterou společnost Contoso vytvoří.
    - V případě společnosti Contoso je to **smarthotelcontoso.eastus2.cloudapp.azure.com**.

    ![Nastavení souboru JSON](./media/contoso-migration-rebuild/configure-webapp2.png)

5. Po aktualizaci souboru tento soubor přejmenují na **smarthotelsettingsurl** a odešlou ho do úložiště objektů blob, které vytvořili dříve.

    ![Přejmenování a odeslání](./media/contoso-migration-rebuild/configure-webapp3.png)

6. Soubor vyberou, aby získali adresu URL. Tuto adresu URL používá aplikace při načítání konfiguračních souborů.

    ![Adresa URL aplikace](./media/contoso-migration-rebuild/configure-webapp4.png)

7. V souboru **appsettings.Production.json** aktualizují hodnotu **SettingsURL** na adresu URL nového souboru.

    ![Aktualizace adresy URL](./media/contoso-migration-rebuild/configure-webapp5.png)

### <a name="deploy-the-website-to-azure-app-service"></a>Nasazení webu do služby Azure App Service

Správci společnosti Contoso teď můžou web publikovat.

1. Otevřou Azure DevOps a v projektu **SmartHotelFrontend** v části **Builds and Releases** (Sestavení a vydané verze) vyberou **+New Pipeline** (+Nový kanál).
2. Jako zdroj vyberou **Azure DevOps Git**.
3. Vyberou šablonu **ASP.NET Core**.
4. Prohlédnou si kanál a zkontrolují, že jsou vybrané možnosti **Publish Web Projects** (Publikovat webové projekty) a **Zip Published Projects** (Zipovat publikované projekty).

    ![Nastavení kanálu](./media/contoso-migration-rebuild/vsts-publishfront2.png)

5. V části **Triggers** (Aktivační události) povolí kontinuální integraci a přidají hlavní větev. Tím je zajištěno, že pokaždé, když bude mít dané řešení nový kód, který se zapíše do hlavní větve, spustí se kanál buildu.

    ![Nepřetržitá integrace](./media/contoso-migration-rebuild/vsts-publishfront3.png)

6. Výběrem **Save & Queue** (Uložit a zařadit do fronty) spustí sestavení.
7. Po dokončení sestavení nakonfigurují kanál verze pomocí **nasazení Azure App Service**.
8. Zadají název pracovní fáze **Staging**.

    ![Název prostředí](./media/contoso-migration-rebuild/vsts-publishfront4.png)

9. Přidají artefakt a vyberou sestavení, které právě nakonfigurovali.

     ![Přidání artefaktu](./media/contoso-migration-rebuild/vsts-publishfront5.png)

10. Vyberou ikonu blesku na artefaktu a povolí průběžné nasazování.

    ![Nepřetržité nasazování](./media/contoso-migration-rebuild/vsts-publishfront6.png)
11. V části **Environment** (Prostředí) vyberou **1 job, 1 task** (1 úloha, 1 úkol) v části **Staging** (Pracovní fáze).
12. Po výběru předplatného a názvu aplikace otevřou úlohu **Deploy Azure App Service** (Nasadit službu Azure App Service). Nasazení je nakonfigurované tak, aby používalo slot pro nasazení **Staging**. Tím se v tomto slotu automaticky sestaví kód pro kontrolu a schválení.

     ![Slot](./media/contoso-migration-rebuild/vsts-publishfront7.png)

13. V části **Pipeline** (Kanál) přidají novou fázi.

    ![Nové prostředí](./media/contoso-migration-rebuild/vsts-publishfront8.png)

14. Vyberou **Azure App Service deployment with slot** (Nasazení služby Azure App Service se slotem) a prostředí pojmenují **Prod**.
15. Vyberou **1 job, 2 task** (1 úloha, 2 úkoly) a vyberou předplatné, název služby aplikace a slot **Staging**.

    ![Název prostředí](./media/contoso-migration-rebuild/vsts-publishfront10.png)

16. Odeberou položku **Deploy Azure App Service to Slot** (Nasadit službu Azure App Service do slotu) z kanálu. Byla tam umístěna v předchozích krocích.

    ![Odebrání z kanálu](./media/contoso-migration-rebuild/vsts-publishfront11.png)

17. Kanál uloží. V kanálu vyberou **Post-deployment conditions** (Podmínky po nasazení).

    ![Po nasazení](./media/contoso-migration-rebuild/vsts-publishfront12.png)

18. Povolí **Post-deployment approvals** (Schválení po nasazení) a přidají vedoucího vývoje jako schvalovatele.

    ![Schválení po nasazení](./media/contoso-migration-rebuild/vsts-publishfront13.png)

19. V kanálu buildu ručně spustí sestavení. Tím se aktivuje nový kanál verze, který nasadí web do přípravného slotu. V případě společnosti Contoso je adresa URL slotu `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Po dokončení sestavení a nasazení verze do slotu pošle Azure DevOps e-mail s žádostí o schválení vedoucímu vývoje.

21. Vedoucí vývoje vybere **View approval** (Zobrazit schválení) a může žádost schválit nebo odmítnout na portálu Azure DevOps.

    ![E-mail s žádostí o schválení](./media/contoso-migration-rebuild/vsts-publishfront14.png)

22. Vedoucí vývoje připojí poznámku a žádost schválí. To spustí výměnu přípravného slotu (**Staging**) za produkční slot (**Prod**) a přesune sestavení do produkčního prostředí.

    ![Schválení a výměna slotů](./media/contoso-migration-rebuild/vsts-publishfront15.png)

23. Kanál výměnu dokončí.

    ![Dokončení výměny slotů](./media/contoso-migration-rebuild/vsts-publishfront16.png)

24. Tým zkontroluje produkční slot (**Prod**) a ověří, že je webová aplikace v produkčním prostředí na adrese `https://smarthotelcontoso.azurewebsites.net/`.

### <a name="deploy-the-petchecker-function-app"></a>Nasazení aplikace funkcí PetChecker

Správci společnosti Contoso nasadí aplikaci následujícím způsobem.

1. Připojí se k projektu Azure DevOps a do počítače pro vývoj místně naklonují úložiště.
2. V sadě Visual Studio otevřou příslušnou složku a zobrazí všechny soubory v úložišti.
3. Otevřou soubor **src/PetCheckerFunction/local.settings.json** a přidají nastavení aplikace pro úložiště, databázi Cosmos a rozhraní API pro počítačové zpracování obrazu.

    ![Nasazení funkce](./media/contoso-migration-rebuild/function5.png)

4. Potvrdí kód, synchronizují ho zpátky do Azure DevOps a nasdílí tak své změny.
5. Přidají nový kanál buildu a jako zdroj vyberou **Azure DevOps Git**.
6. Vyberou šablonu **ASP.NET Core (.NET Framework)** .
7. Přijmou výchozí nastavení šablony.
8. V části **Triggers** (Aktivační události) pak vyberou **Enable continuous integration** (Povolit kontinuální integraci) a výběrem **Save & Queue** (Uložit a umístit do fronty) spustí sestavení.
9. Po úspěšném vytvoření sestavení sestaví kanál buildu a přidají **Azure App Service deployment with slot** (Nasazení služby Azure App Service se slotem).
10. Prostředí pojmenují jako **Prod** a vyberou předplatné. V poli **App type** (Typ aplikace) nastaví **Function App** (Aplikace funkcí) a jako název služby aplikace zadají **smarthotelpetchecker**.

    ![Function App](./media/contoso-migration-rebuild/petchecker2.png)

11. Přidají artefakt **Build** (Sestavení).

    ![Artefakt](./media/contoso-migration-rebuild/petchecker3.png)

12. Povolí **Continuous deployment trigger** (Aktivace průběžného nasazování) a vyberou **Save** (Uložit).
13. Výběrem **Queue new build** (Zařadit nové sestavení do fronty) spustí úplný kanál CI/CD.
14. Jakmile je funkce nasazená, zobrazí se na webu Azure Portal se stavem **Running** (Spuštěno).

    ![Nasazení funkce](./media/contoso-migration-rebuild/function6.png)

15. Přejdou do aplikace a otestují, že aplikace Pet Checker na adrese [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets) funguje podle očekávání.

16. Vyberou avatara pro odesílání obrázků.

    ![Nasazení funkce](./media/contoso-migration-rebuild/function7.png)

17. První fotku, kterou chtějí zkontrolovat, je fotka malého psa.

    ![Nasazení funkce](./media/contoso-migration-rebuild/function8.png)

18. Aplikace vrátí zprávu o přijetí.

    ![Nasazení funkce](./media/contoso-migration-rebuild/function9.png)

## <a name="review-the-deployment"></a>Kontrola nasazení

Teď, když jsou prostředky migrované do Azure, potřebuje společnost Contoso plně zprovoznit a zabezpečit novou infrastrukturu.

### <a name="security"></a>Zabezpečení

- Společnost Contoso musí zajistit bezpečnost nových databází. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Aplikaci je nutné aktualizovat, aby používala protokol SSL s certifikáty. Instance kontejneru by se měla znovu nasadit, aby reagovala na portu 443.
- Společnost Contoso by měla zvážit použití služby Key Vault k ochraně důvěrných dat aplikací využívajících Service Fabric. [Další informace](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups-and-disaster-recovery"></a>Zálohování a zotavení po havárii

- Společnost Contoso potřebuje zkontrolovat požadavky na zálohování databáze Azure SQL Database. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Společnost Contoso by měla zvážit implementaci skupin pro převzetí služeb SQL při selhání a zajistit tak regionální převzetí služeb při selhání databáze. [Další informace](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Společnost Contoso může použít geografickou replikaci skladové položky ACR Premium. [Další informace](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Databáze Cosmos DB se zálohuje automaticky. Společnost Contoso může získat [další informace](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) o tomto procesu.

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- Po nasazení všech prostředků by společnost Contoso měla na základě [plánování infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging) přiřadit značky Azure.
- Veškeré licencování je součástí nákladů na služby PaaS, které společnost Contoso spotřebovává. Náklady se odečtou ze smlouvy EA.
- Společnost Contoso povolí službu Azure Cost Management licencovanou společností Cloudyn, dceřinou společností Microsoftu. To je multicloudové řešení pro řízení nákladů, které pomáhá s využitím a správou Azure a dalších cloudových prostředků. Přečtěte si [další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management.

## <a name="conclusion"></a>Závěr

V tomto článku společnost Contoso znovu sestaví aplikaci SmartHotel360 v Azure. Front-endový virtuální počítač s místní aplikací je znovu sestaven pro webové aplikace služby Azure App Service. Back-end aplikace je sestaven pomocí mikroslužeb nasazených do kontejnerů spravovaných službou Azure Kubernetes Service (AKS). Společnost Contoso rozšíří funkce aplikace o aplikaci pro odesílání fotek domácích zvířat.

## <a name="suggested-skills"></a>Navrhované dovednosti

Microsoft Learn je nový přístup ke studiu. Připravenosti na nové dovednosti a úkoly, které souvisejí s přechodem do cloudu, není snadné dosáhnout. Microsoft Learn poskytuje efektivnější přístup k praktické výuce, který vám umožní dosáhnout vašich cílů rychleji. Získávejte body, nové úrovně a dovednosti!

Tady je několik příkladů přizpůsobených studijních cest na Microsoft Learn, které jsou v Azure v souladu s aplikací contoso SmartHotel360.

[Nasazení webu do Azure pomocí Azure App Service](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service/): webové aplikace v Azure umožňují publikování a správu webu snadno, aniž byste museli pracovat s podkladovým serverem, úložištěm nebo síťovými prostředky. Místo toho se můžete soustředit na funkce webu a spolehnout se, že zabezpečený přístup k vašemu webu poskytne robustní platforma Azure.

[Zpracování a klasifikace imagí pomocí služeb Azure pro rozpoznávání](https://docs.microsoft.com/learn/paths/classify-images-with-vision-services/)hlasu: Azure Cognitive Services nabízí předem sestavené funkce, které ve vašich aplikacích umožní funkce počítačové vize. Naučte se používat služby rozpoznávání zraku ke zjišťování tváře, značek a klasifikace obrázků a identifikaci objektů.
