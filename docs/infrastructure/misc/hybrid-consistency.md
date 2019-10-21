---
title: Vytvoření konzistentního hybridního cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Definování přístupu pro vytvoření konzistence hybridního cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5b2de64af3d7e48a38fd1f125fc5f8b37b190dd2
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547199"
---
# <a name="create-hybrid-cloud-consistency"></a>Vytvoření konzistentního hybridního cloudu

Tento článek vás provede vysokou úrovní přístupů k vytvoření konzistence hybridního cloudu.

Modely hybridního nasazení během migrace můžou snížit rizika a přispívat k plynulému přechodu na infrastrukturu. Cloudové platformy nabízejí nejvyšší úroveň flexibility, když se dostane do obchodních procesů. Mnoho organizací je váhají, aby se přechod do cloudu provedl. Místo toho mají přednost před tím, než budou mít plnou kontrolu nad nejcitlivější data. Místní servery bohužel neumožňují stejnou míru inovace jako Cloud. Hybridní cloudové řešení nabízí rychlost inovace cloudu a kontrolu nad místní správou.

## <a name="integrate-hybrid-cloud-consistency"></a>Integrujte konzistenci hybridního cloudu

Použití hybridního cloudového řešení umožňuje organizacím škálovat výpočetní prostředky. Eliminuje také nutnost provádět obrovské kapitálové výdaje za účelem zpracování krátkodobých špiček v poptávce. Změny vaší firmy mohou řídit nutnost uvolnit místní prostředky pro citlivá data nebo aplikace. Zrušení zřízení cloudových prostředků je jednodušší, rychlejší a levnější. Platíte jenom za prostředky, které vaše organizace dočasně používá, a nemusíte kupovat a spravovat další prostředky. Tento přístup snižuje množství zařízení, která by mohla zůstat nečinná po dlouhou dobu. Hybridní cloud computing přináší všechny výhody flexibility cloud computingu, škálovatelnosti a cenovou efektivitu s nejnižšími možnými riziky při expozici dat.

na![Creatingte konzistenci hybridního cloudu napříč identitami, správou, zabezpečením, daty, vývojem a DevOps ](../../_images/hybrid-consistency.png)
*Obrázek 1 – vytváření hybridní konzistence cloudu napříč identitami, správou, zabezpečením, daty, vývojem a DevOps*

Skutečné hybridní cloudové řešení musí poskytovat čtyři komponenty, z nichž každý přináší významné výhody:

- **Společná identita pro místní a cloudové aplikace:** Tato součást zlepšuje produktivitu uživatelů tím, že poskytuje uživatelům jednotné přihlašování (SSO) ke všem jejich aplikacím. Zároveň zajišťuje konzistenci jako aplikace a uživatele mezi hranicemi sítě nebo cloudu.
- **Integrovaná správa a zabezpečení v rámci hybridního cloudu:** Tato součást poskytuje soudržný způsob, jak monitorovat, spravovat a zabezpečovat prostředí, což umožňuje zvýšenou viditelnost a kontrolu.
- **Konzistentní datová platforma pro datové centrum a Cloud:** Tato součást vytváří přenositelnost dat v kombinaci s bezproblémovým přístupem k místním i cloudovým datovým službám pro zajištění podrobného přehledu o všech zdrojích dat.
- **Sjednocený vývoj a DevOps v cloudových i místních datových centrech:** Tato součást umožňuje přesouvat aplikace mezi těmito dvěma prostředími podle potřeby. Produktivita vývojářů se zlepšuje, protože obě umístění nyní mají stejné vývojové prostředí.

Tady jsou některé příklady těchto komponent z perspektivy Azure:

- Azure Active Directory (Azure AD) funguje s místní službou Active Directory, která poskytuje společnou identitu pro všechny uživatele. Jednotné přihlašování v místním prostředí a prostřednictvím cloudu usnadňuje uživatelům bezpečný přístup k aplikacím a potřebným prostředkům. Správci mohou spravovat zabezpečení a řízení zásad správného řízení a také pružně upravovat oprávnění, aniž by to ovlivnilo uživatelské prostředí.
- Azure poskytuje integrované služby pro správu a zabezpečení jak v cloudu, tak i v místní infrastruktuře. Mezi tyto služby patří integrovaná sada nástrojů, která se používá k monitorování, konfiguraci a ochraně hybridních cloudů. Tento komplexní přístup ke správě konkrétně řeší problémy reálného světa, které čelí organizacím, které berou v úvahách hybridní cloudové řešení.
- Azure Hybrid Cloud nabízí běžné nástroje, které zajistí bezproblémový a efektivně zabezpečený přístup ke všem datům. Datové služby Azure se kombinují s Microsoft SQL Server a vytvářejí konzistentní datovou platformu. Konzistentní hybridní cloudový model umožňuje uživatelům pracovat s provozními i analytickými daty. Stejné služby jsou k dispozici místně a v cloudu pro datové sklady, analýzu dat a vizualizaci dat.
- Cloudové služby Azure v kombinaci s Azure Stack místním prostředí poskytují jednotný vývoj a DevOps. Konzistence v cloudu i v místním prostředí znamená, že váš tým DevOps může sestavovat aplikace, které běží v některém prostředí, a může je snadno nasadit do správného umístění. Můžete také znovu použít šablony v rámci hybridního řešení, které může dále zjednodušit DevOps procesy.

## <a name="azure-stack-in-a-hybrid-cloud-environment"></a>Azure Stack v hybridním cloudovém prostředí

Azure Stack je hybridní cloudové řešení, které umožňuje organizacím provozovat služby konzistentní s Azure ve svém datovém centru. Nabízí zjednodušené prostředí pro vývoj, správu a zabezpečení, které je konzistentní s veřejným cloudovým službám Azure. Azure Stack je rozšířením Azure. Můžete ji použít ke spouštění služeb Azure z místních prostředí a pak přejít do cloudu Azure, pokud je to potřeba.

Pomocí Azure Stack můžete nasazovat a provozovat IaaS i PaaS pomocí stejných nástrojů a nabízet stejné prostředí jako veřejný cloud Azure. Správa Azure Stack, ať už prostřednictvím portálu webového uživatelského rozhraní nebo prostřednictvím PowerShellu, má konzistentní vzhled a chování správců IT a koncových uživatelů s Azure.

Azure a Azure Stack otevřít nové hybridní případy použití pro zákaznické i interní obchodní aplikace:

- **Hraniční a odpojená řešení.** Aby zákazníci mohli řešit požadavky na latenci a připojení, můžou data místně zpracovávat v Azure Stack a pak je agregovat v Azure pro další analýzy. Můžou používat běžnou aplikační logiku napříč oběma. Mnohé zákazníky mají zájem o tento hraniční scénář v různých kontextech, jako jsou produkční podlahová místa, přepravní lodí a hřídele.
- **Cloudové aplikace, které vyhovují různým předpisům.** Zákazníci můžou vyvíjet a nasazovat aplikace v Azure s plnou flexibilitou pro nasazení místně na Azure Stack, aby splňovaly zákonné požadavky nebo požadavky zásad. Nevyžadují se žádné změny kódu. Mezi příklady aplikací patří globální audit, finanční vykazování, obchodování s cizím systémem Exchange, hraní online her a generování sestav výdajů. Zákazníci někdy v závislosti na obchodních a technických požadavcích nasadí různé instance stejné aplikace do Azure nebo Azure Stack. I když Azure splňuje většinu požadavků, Azure Stack v případě potřeby doplňují přístup k nasazení.
- **Model cloudové aplikace v místním prostředí.** Zákazníci můžou použít webové služby, kontejnery, bez serveru a architektury mikroslužeb k aktualizaci a rozšiřování existujících aplikací nebo sestavování nových. V rámci Azure v cloudu můžete používat konzistentní procesy DevOps a Azure Stack v místním prostředí. Existuje rostoucí podíl na modernizaci aplikací, a to i pro klíčové klíčové aplikace.

Azure Stack se nabízí přes dvě možnosti nasazení:

- **Azure Stack integrované systémy:** Azure Stack integrované systémy jsou nabízeny prostřednictvím Microsoftu a hardwarových partnerů k vytvoření řešení, které poskytuje inovace s využitím cloudového tempa s jednoduchou správou. Vzhledem k tomu, že Azure Stack se nabízí jako integrovaný systém hardwaru a softwaru, získáte flexibilitu a kontrolu nad tím, jak stále probíhá přijímání inovací z cloudu. Azure Stack rozsahy integrovaných systémů je velikost od 4 do 12 uzlů. Jsou společně podporovány hardwarovým partnerem a společností Microsoft. Pomocí Azure Stack integrovaných systémů můžete povolit nové scénáře pro produkční úlohy.
- **Azure Stack Development Kit:** Microsoft Azure Stack Development Kit je nasazení Azure Stack s jedním uzlem. Můžete ji použít k vyhodnocení a získání informací o Azure Stack. Můžete také použít sadu jako vývojářské prostředí, kde můžete vyvíjet pomocí rozhraní API a nástrojů, které jsou konzistentní s Azure. Azure Stack Development Kit není určený pro použití jako produkční prostředí.

## <a name="azure-stack-one-cloud-ecosystem"></a>Azure Stack ekosystém pro jeden Cloud

Azure Stack iniciativ můžete urychlit pomocí kompletního ekosystému Azure:

- Azure zajišťuje, že většina aplikací a služeb, které jsou certifikované pro Azure, budou fungovat na Azure Stack. Několik výrobců ISV rozšiřuje svá řešení na Azure Stack. Tito výrobci softwaru zahrnují Bitnami, Docker, kemp technologie, Pivoted Cloud Foundry, Red Hat Enterprise Linux a SUSE Linux.
- Můžete se rozhodnout, že budete Azure Stack doručovat a provozovat jako plně spravovanou službu. Několik partnerů bude mít v Azure nabídky spravované služby a brzy Azure Stack. Mezi tyto partnery patří Tieto, Yourhosting, revera, pohonné a NTT. Tito partneři dodávají spravované služby pro Azure prostřednictvím programu Cloud Solution Provider (CSP). Rozšiřují své nabídky tak, aby zahrnovaly hybridní řešení.
- Jako příklad kompletního a plně spravovaného hybridního cloudového řešení Avanade nabízí nabídku vše v jednom. Zahrnuje cloudové transformační služby, software, infrastrukturu, nastavení a konfiguraci a průběžné spravované služby. Díky tomu můžou zákazníci využívat Azure Stack stejně jako s Azure ještě dnes.
- Poskytovatelé můžou přispět k urychlení iniciativ pro moderní aplikace tím, že pro zákazníky sestavují ucelená řešení Azure. Přinášejí hloubkové sady Azure dovedností, znalosti domén a odvětví a zpracovávají odbornost, jako je DevOps. Každý Azure Stack Cloud je příležitostí pro poskytovatele návrhu řešení a vedoucí a ovlivnění nasazení systému. Můžou také přizpůsobit zahrnuté možnosti a poskytovat provozní činnosti. Mezi příklady poskytovatelů patří Avanade, DXC, Dell EMC Services, in konzultační skupina, HPE Pointnext a PwC (dřív PricewaterhouseCoopers).
