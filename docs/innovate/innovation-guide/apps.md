---
title: 'Průvodce inovacemi Azure: Zapojení přes aplikace'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se inovovat zapojením přes aplikace pomocí Azure.
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: df91d44d9b1efc2196b8b322c247dd39ef3d0d1e
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769346"
---
::: zone target="docs"

# <a name="azure-innovation-guide-engage-through-apps"></a>Průvodce inovacemi Azure: Zapojení přes aplikace

::: zone-end

::: zone target="chromeless"

# <a name="engage-through-apps"></a>Zapojení přes aplikace

::: zone-end

Inovace prostřednictvím aplikací zahrnuje jak modernizaci vašich stávajících aplikací, které jsou hostovány místně, tak i vytváření aplikací nativních pro cloud pomocí kontejnerů nebo bezserverových technologií. Pokud jde o modernizaci aplikací, Azure poskytuje služby PaaS, jako je Azure App Service, pro snadnou modernizaci stávajících webových aplikací a aplikací rozhraní API napsaných v .NET, .NET Core, Javě, Node.js, Ruby, Pythonu nebo PHP pro nasazení v Azure. Pomocí spravovaných služeb, jako je Azure Kubernetes Services, Azure Container Instances a Web App for Containers, je u modelu kontejneru otevřeného standardu vytváření mikroslužeb nebo kontejnerizace existujících aplikací a jejich nasazení snadné. Bezserverové technologie, jako je Azure Functions a Azure Logic Apps, používají model založený na využití (platíte za to, co používáte) a pomáhají vám soustředit se spíše na vytváření vaší aplikace než na nasazení a správu infrastruktury.

<!-- markdownlint-disable MD025 -->

# <a name="deliver-value-fastertabdelivervaluefaster"></a>[Rychlejší uvedení do provozu](#tab/DeliverValueFaster)

Jednou z výhod cloudových řešení je schopnost rychleji získávat zpětnou vazbu a začít poskytovat hodnotu koncovému uživateli. Nezáleží na tom, zda je koncovým uživatelem externí zákazník nebo uživatel ve vaší vlastní společnosti, čím rychleji získáte zpětnou vazbu ke svým aplikacím, tím lépe.

## <a name="azure-app-service"></a>Azure App Service

Azure App Service poskytuje vašim aplikacím hostitelské prostředí, které odstraňuje zátěž spojenou se správou infrastruktury a opravami chyb operačního systému. Poskytuje automatizaci škálování, aby byly splněny požadavky uživatelů, a současně je vázáno limity, které definujete, aby náklady zůstaly pod kontrolou.

Azure App Service poskytuje prvotřídní podporu jazyků, jako jsou ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP nebo Python. Pokud potřebujete hostovat další zásobník modulu runtime, služba Web App for Containers umožňuje rychle a snadno hostovat kontejner Dockeru v prostředí Azure App Service a hostovat tak vlastní zásobník kódu v prostředí, které je mimo server.

### <a name="action"></a>Akce

Konfigurace nebo monitorování nasazení služby Azure App Service:

1. Přejděte na **App Services**.
2. Nakonfigurujte novou službu: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících služeb: Ze seznamu hostovaných aplikací vyberte požadovanou aplikaci.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Azure Cognitive Services vám umožňuje začlenit pokročilé inteligentní funkce přímo do vaší aplikace pomocí skupiny rozhraní API, díky nimž budete moci využívat výhod algoritmů AI a Machine Learning podporovaných společností Microsoft.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Konfigurace nebo monitorování nasazení služby Azure Cognitive Service:

1. Přejděte na **Cognitive Services**.
2. Nakonfigurujte novou službu: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících služeb: Ze seznamu hostovaných služeb vyberte požadovanou službu.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-bot-services"></a>Azure Bot Service

Služby Azure Bot Service rozšiřují vaši standardní aplikaci o rozhraní přirozeného bota, který využívá AI a Machine Learning k vytvoření nové interakce pro vaše zákazníky.

### <a name="action"></a>Akce

Konfigurace nebo monitorování nasazení služeb Azure Bot Service:

1. Přejděte na **Služby Bot Service**.
2. Nakonfigurujte novou službu: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících služeb: Ze seznamu hostovaných služeb vyberte požadovaného bota.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FbotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-devops"></a>Azure DevOps

Při inovaci nakonec zjistíte, že směřujete k DevOps. Microsoft již dlouho má místní produkt s názvem Team Foundation Server (TFS). Během inovační cesty Microsoft vyvinul cloudovou službu Azure DevOps, která poskytuje nástroje pro vytváření a vydávání verzí a která podporuje mnoho jazyků a cílů pro vaše vydané verze. [Azure DevOps](https://docs.microsoft.com/azure/devops)

## <a name="visual-studio-app-center"></a>Visual Studio App Center

S rostoucí popularitou mobilních aplikací roste i potřeba platformy, která může poskytovat automatizované testování na skutečných zařízeních s různými konfiguracemi. Visual Studio App Center poskytuje nejen místo, kde můžete testovat aplikace v systémech iOS, Android, Windows a macOS, ale i monitorovací platformu, která s využitím Azure Application Insights umožňuje rychle a snadno analyzovat vaši telemetrii. Další informace najdete v článku, který se zabývá [přehledem sady služeb Visual Studio App Center](https://docs.microsoft.com/appcenter).

Visual Studio App Center také poskytuje službu oznámení, která umožňuje použít jediné volání k odeslání oznámení do vaší aplikace napříč platformami, aniž byste museli kontaktovat každou službu oznámení samostatně. Další informace najdete v článku o službě [Visual Studio App Center Push (ACP)](https://docs.microsoft.com/appcenter/push).

### <a name="read-more"></a>Další informace

- [Přehled služby App Service](https://docs.microsoft.com/azure/app-service/overview)
- [Web Apps for Containers: Spuštění vlastního kontejneru](https://docs.microsoft.com/azure/app-service/containers/quickstart-docker)
- [Seznámení s Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [Azure pro vývojáře na platformě .NET a .NET Core](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)
- [Dokumentace k sadě Azure SDK pro Python](https://docs.microsoft.com/azure/python)
- [Azure pro cloudové vývojáře v Javě](https://docs.microsoft.com/azure/java/?view=azure-java-stable)
- [Vytvoření webové aplikace v PHP v Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-php)
- [Dokumentace k sadě Azure SDK pro JavaScript](https://docs.microsoft.com/azure/javascript)
- [Dokumentace k sadě Azure SDK pro Go](https://docs.microsoft.com/azure/go)
- [Řešení DevOps](https://azure.microsoft.com/solutions/devops)

# <a name="cloud-native-appstabcloudnative"></a>[Aplikace nativní pro cloud](#tab/CloudNative)

<!-- markdownlint-disable MD026 -->

## <a name="what-are-cloud-native-applications"></a>Co jsou aplikace nativní pro cloud?

Aplikace nativní pro cloud jsou sestavovány od základů a jsou optimalizované pro cloudové škálování a výkon. Jsou volně propojené na základě architektury s mikroslužbami, používají spravované služby, lze je sledovat a využívají výhody průběžného doručování s cílem dosáhnout spolehlivost a rychlejší uvedení na trh. Obecně platí, že jsou přenosné a mohou běžet v dynamických prostředích, jako jsou veřejné, soukromé a hybridní cloudy. Aplikace nativní pro cloud jsou obvykle sestavené pomocí jednoho nebo více následujících přístupů:

- Mikroslužby
- Bez serveru
- Kontejner

## <a name="microservices"></a>Mikroslužby

Mikroslužby představují styl architektury softwaru, ve kterém se aplikace sestavují z malých nezávislých modulů, které spolu vzájemně komunikují pomocí dobře definovaných kontraktů API. Tyto moduly služeb jsou samostatné stavební bloky, které jsou tak malé, aby implementovaly jedinou funkci. Mikroslužby vám usnadňují:

- Nezávislé sestavování služeb
- Autonomní škálování služeb
- Použití nejvhodnějších přístupů pro nasazení a programovací jazyk
- Izolaci oblastí s chybami
- Rychlejší uvedení do provozu

### <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

Zřizování, upgrade a škálování prostředků clusteru na vyžádání provádějte pomocí plně spravované služby Kubernetes. AKS usnadňuje nasazení a správu kontejnerových aplikací. Nabízí Kubernetes bez serveru, integrované prostředí kontinuální integrace a průběžného doručování (CI/CD) a zabezpečení a zásady správného řízení na podnikové úrovni. Spojte své vývojové a provozní týmy na jediné platformě a umožněte jim rychle vytvářet, dodávat a škálovat aplikace bez obav.

#### <a name="action"></a>Akce

Konfigurace nebo monitorování služeb Azure Kubernetes Service:

1. Přejděte na **Služby Kubernetes**.
2. Nakonfigurujte novou službu: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících služby: Ze seznamu vyberte požadovanou službu Kubernetes.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FmanagedClusters]" submitText="Go to Kubernetes Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="event-based-solutions"></a>Řešení založená na událostech

### <a name="azure-functions"></a>Azure Functions

Azure Functions poskytuje platformu pro spouštění malých kousků kódu (neboli funkcí) v cloudu. Funkce mohou být způsobem, jak spustit refaktoring kódu do architektury mikroslužeb.

Modul runtime Azure Functions podporuje mnoho jazyků, včetně C #, Javy, JavaScriptu a Pythonu. Úplný seznam najdete v článku, který pojednává o [podporovaných jazycích v Azure Functions](https://docs.microsoft.com/azure/azure-functions/supported-languages).

Další výhodou funkcí je to, že je mohou spouštět různé akce a události, jako jsou HTTPTrigger, TimerTrigger a triggery z jiných služeb Azure, například Blob storage, EventGrid a ServiceBus. Další informace o triggerech a vazbách najdete v tématu o [koncepcích triggerů a vazeb Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

#### <a name="action"></a>Akce

Konfigurace nebo monitorování nasazení Azure Functions:

1. Přejděte na **Aplikace funkcí**.
2. Nakonfigurujte novou aplikaci: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících aplikací: Ze seznamu aplikací funkcí vyberte požadovanou aplikaci.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="serverless-solutions"></a>Bezserverová řešení

Sestavujte aplikace nativní pro cloud bez zřizování a správy infrastruktury s použitím plně spravované platformy, která pro vás zajišťuje škálování, dostupnost a výkon. Mezi výhody bezserverových řešení Azure patří:

- Zrychlení vývoje
- Zvýšení výkonu týmů
- Posílení vlivu organizace

### <a name="azure-logic-apps"></a>Azure Logic Apps

Integrujte data a aplikace místo psaní složitého integračního kódu mezi různorodými systémy. Vizuálně vytvářejte bezserverové pracovní postupy s využitím služby Azure Logic Apps a používejte vlastní rozhraní API, bezserverové funkce nebo integrované konektory SaaS (software jako služba), včetně Salesforce, Microsoft Office 365 a Dropboxu.

#### <a name="action"></a>Akce

Konfigurace nebo monitorování služby Azure Logic Apps:

1. Přejděte na **Logic Apps**.
2. Nakonfigurujte novou aplikaci: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících aplikací: V seznamu vyberte požadovanou aplikaci logiky.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2Fworkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-api-management"></a>Bezserverová správa rozhraní API

Publikujte, zabezpečte, transformujte, udržujte a monitorujte rozhraní API s využitím plně spravované služby Azure API Management, která nabízí model využití navržený a implementovaný tak, aby byl přirozený pro bezserverové aplikace.

#### <a name="action"></a>Akce

Konfigurace nebo monitorování služeb API Management:

1. Přejděte na **Služby API Management**.
2. Nakonfigurujte novou službu: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících služby: Ze seznamu vyberte požadovanou službu.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="containers"></a>Containers

Za účelem modernizace portfolia aplikací poskytuje Azure různé služby kontejnerů, které migrují vaše stávající aplikace metodou „lift and shift“ do kontejnerů a také sestavují aplikace mikroslužeb nativní pro cloud, aby z nich uživatelé mohli rychleji získat užitek. K vývoji, aktualizaci a nasazení kontejnerových aplikací použijte ucelené vývojářské nástroje a nástroje CI/CD. Spravujte kontejnery ve velkém měřítku pomocí plně spravované služby orchestrace kontejnerů Kubernetes, která se integruje s Azure Active Directory. Ať už se nacházíte v kterékoli fázi inovace aplikace, zrychlete vývoj kontejnerizovaných aplikací a současně splňte požadavky na zabezpečení.

### <a name="azure-container-instances"></a>Azure Container Instances

Spouštějte kontejnery Dockeru na vyžádání ve spravovaném bezserverovém prostředí Azure. Azure Container Instances (ACI) je řešení pro libovolný scénář, který může fungovat na izolovaných kontejnerech bez orchestrace. Díky spouštění úloh v ACI se můžete soustředit na navrhování a sestavování aplikací a nemusíte spravovat infrastrukturu, na které běží.

### <a name="action"></a>Akce

Konfigurace nebo monitorování řešení Container Instances:

1. Přejděte na **Instance kontejnerů**.
2. Nakonfigurujte novou instanci kontejneru: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících instancí kontejnerů: Ze seznamu vyberte požadovanou instanci kontejneru.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FcontainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-red-hat-openshift"></a>Azure Red Hat OpenShift

Azure Red Hat OpenShift poskytuje flexibilní samoobslužné nasazení plně spravovaných clusterů OpenShift. Zajistěte dodržování předpisů a soustřeďte se na vývoj aplikací, zatímco hlavní uzel, aplikační uzly a uzly infrastruktury bude opravovat, aktualizovat a monitorovat Microsoft a Red Hat. Můžete si zvolit vlastní registry, sítě, úložiště nebo řešení CI/CD. Případně můžete rychle začít využívat integrovaná řešení s automatizovanou správou zdrojového kódu, sestaveními kontejnerů a aplikací, nasazeními, škálováním, správou stavu a dalšími funkcemi.

**Přejděte na [Úvod do Azure Red Hat OpenShift](https://docs.microsoft.com/azure/openshift/intro-openshift)** .

# <a name="isolate-points-of-failuretabisolatepointsoffailure"></a>[Izolaci oblastí s chybami](#tab/IsolatePointsOfFailure)

Jakmile začnete přecházet z počáteční fáze testování, vyhodnoťte způsoby, jak izolovat a odstranit body selhání. Vzhledem k distribuované povaze cloudové platformy Azure můžete svou aplikaci navrhnout tak, aby minimalizovala chyby a zároveň zlepšovala výkon.

## <a name="azure-front-door"></a>Azure Front Door

Azure Front Door poskytuje škálovatelný a zabezpečený vstupní bod, který můžete použít k doručování své aplikace po celém světě. Azure Front Door kombinuje optimalizaci provozu za účelem dosažení nejlepšího výkonu a okamžitého globálního převzetí služeb při selhání. Pokud chcete zajistit ukončování protokolu TLS (Transport Layer Security), tzv. přesměrování zpracování SSL, nebo zpracování jednotlivých požadavků HTTP/HTTPS na úrovni aplikace, použijte raději službu Azure Front Door místo Traffic Manageru.

### <a name="action"></a>Akce

Konfigurace nebo monitorování front doorů:

1. Přejděte na **Front Doory**.
2. Nakonfigurujte nový front door: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících front doorů: Ze seznamu vyberte požadovaný front door.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ffrontdoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="traffic-manager"></a>Traffic Manager

Traffic Manager poskytuje vyrovnávání zatížení založené na DNS, které lze směrovat na základě různých pravidel. To pomáhá zajistit odolnost v případě selhání nasazených služeb. Traffic Manager můžete také umístit do zásobníku, aby používal směrování na základě chyb i směrování na základě výkonu a poskytoval tak nejlepší možné prostředí založené na geografii.

### <a name="action"></a>Akce

Konfigurace nebo monitorování profilů služby Traffic Manager:

1. Přejděte na **Profily služby Traffic Manager**.
2. Nakonfigurujte nový profil: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících profilů: Ze seznamu vyberte požadovaný profil.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ftrafficmanagerprofiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-content-delivery-network"></a>Azure Content Delivery Network

Azure nabízí distribuovanou síť pro doručování obsahu (CDN), která vám umožňuje zajistit včasné doručování prostředků tím, že je uloží do mezipaměti blízko vašim koncovým uživatelům. Toto ukládání do mezipaměti pomáhá zlepšit zkušenosti vašich zákazníků. Během stahování obsahu také zabraňuje problémům způsobeným problémy se sítí, ke kterým dochází mezi koncovým bodem CDN a datacentrem, které je hostitelem vaší aplikace. Síť pro doručování obsahu mohou také používat aplikace, které nejsou hostovány v Azure.

### <a name="action"></a>Akce

Konfigurace nebo monitorování profilů CDN:

1. Přejděte na **Profily CDN**.
2. Nakonfigurujte nový profil: klikněte na odkaz **Přidat +** a postupujte podle pokynů.
3. Správa existujících profilů: Ze seznamu vyberte požadovaný profil.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.cdn%2Fprofiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="read-more"></a>Další informace

- [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
- [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)
- [Content Delivery Network](https://docs.microsoft.com/azure/cdn)