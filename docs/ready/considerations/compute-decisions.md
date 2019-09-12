---
title: Rozhodnutí o návrhu výpočtů připravených na Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Rozhodnutí o návrhu výpočtů připravených na Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bd31f07a24a17a50953eff54856118e9b22d054e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819384"
---
# <a name="compute-design-decisions"></a>Rozhodnutí o návrhu výpočtů

Určení požadavků na výpočty pro hostování vašich úloh je klíčový aspekt přípravy na přechod do cloudu. Výpočetní produkty a služby Azure podporují širokou škálu výpočetních scénářů a funkcí pro úlohy. Způsob, jakým u cílového prostředí nakonfigurujete podporu výpočetních požadavků, závisí na zásadách správného řízení, technických a obchodních požadavcích vašich úloh.

## <a name="identify-compute-services-requirements"></a>Zjištění požadavků na výpočetní služby

V rámci vyhodnocení a přípravy cílového prostředí musíte identifikovat všechny výpočetní prostředky, které bude vaše cílové prostředí muset podporovat. Součástí tohoto procesu je posouzení všech aplikací a služeb, ze kterých jsou tvořeny vaše úlohy, a určení požadavků na výpočty a hostování. Po zjištění a zdokumentování těchto požadavků můžete pro cílové prostředí vytvořit zásady, které na základě potřeb vašich úloh určují, jaké typy prostředků jsou povolené.

Pro každou aplikaci nebo službu, kterou nasadíte do cílového prostředí, použijte jako výchozí bod následující rozhodovací strom, který vám pomůže určit požadavky na výpočetní služby:

![Rozhodovací strom výpočetních služeb Azure](../../_images/ready/compute-decision-tree.png)

> [!NOTE]
> Další informace o posouzení výpočetních možností pro jednotlivé aplikace nebo služby najdete v [příručce Aplikační architektura v Azure](/azure/architecture/guide/technology-choices/compute-overview).

### <a name="key-questions"></a>Klíčové otázky

Zodpovězení následujících otázek týkajících se vašich úloh vám pomůže při rozhodování na základě rozhodovacího stromu výpočetních služeb Azure:

- **Vytváříte nové aplikace a služby, nebo migrujete z existujících místních úloh?** Vývoj nových aplikací v rámci přechodu do cloudu vám umožní plně využít moderní cloudové technologie pro hostování od fáze návrhu dále.
- **Pokud migrujete existující úlohy, dokážou využít výhod moderních cloudových technologií?** Migrace místních úloh vyžaduje analýzu: Můžete existující aplikace a služby snadno optimalizovat tak, aby využívaly moderní cloudové technologie, nebo bude pro vaše úlohy lepší migrace metodou *lift and shift*?
- **Dokážou vaše aplikace nebo služby využívat kontejnery?** Pokud jsou vaše aplikace dobrými kandidáty na hostování v kontejnerech, můžete vyžít efektivitu prostředků, škálovatelnost a funkce orchestrace, které nabízí služba [Azure Container Services](https://azure.microsoft.com/product-categories/containers). K trvalém uložení kontejnerizovaných aplikací lze využít služby [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) a [Azure Files](/azure/storage/files/storage-files-introduction).
- **Jsou vaše aplikace založené na webu nebo rozhraní API a využívají PHP, ASP.NET, Node. js nebo podobné technologie?** Webové aplikace je možné nasadit na spravované instance [Azure App Service](/azure/app-service/overview), takže pro účely hostování nemusíte provozovat virtuální počítače.
- **Budete potřebovat úplnou kontrolu nad operačním systémem a hostitelským prostředím vaší úlohy?** Pokud potřebujete mít kontrolu nad hostitelským prostředím včetně operačního systému, disků, místně běžícího softwaru a dalších konfigurací, můžete k hostování aplikací a služeb použít službu [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines). Kromě volby velikosti virtuálních počítačů a úrovní výkonu bude mít vaše rozhodnutí týkající se virtuálního diskového úložiště vliv na výkon a smlouvy SLA související s úlohami založenými na infrastruktuře jako službě (IaaS). Další informace najdete v dokumentaci k [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview).
- **Budou vaše úlohy zahrnovat funkce HPC (High Performance Computing)?** Služba [Azure Batch](/azure/batch/batch-technical-overview) zajišťuje plánování úloh a automatické škálování výpočetních prostředků jako službu platformy, což usnadňuje provozování rozsáhlých paralelních a HPC aplikací v cloudu.
- **Budou vaše aplikace používat architekturu mikroslužeb?** Aplikace, které používají architekturu založenou na mikroslužbách, mohou využívat několik optimalizovaných výpočetních technologií. Pro soběstačné úlohy řízené událostmi lze pomocí služby [Azure Functions](/azure/azure-functions/functions-overview) vytvořit škálovatelné bezserverové aplikace, které nepotřebují infrastrukturu. Pro aplikace, které vyžadují větší kontrolu nad prostředím, ve kterém běží mikroslužby, můžete použít služby kontejneru, mezi které patří [Azure Container Instances](/azure/container-instances/container-instances-overview), [Azure Kubernetes](/azure/aks/intro-kubernetes) a [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).

> [!NOTE]
> Většina výpočetních služeb Azure se používá v kombinaci s Azure Storage. V [pokynech pro rozhodování o úložišti](./storage-guidance.md) najdete informace související s úložištěm.

## <a name="common-compute-scenarios"></a>Běžné výpočetní scénáře

Následující tabulka obsahuje několik běžných scénářů a doporučené výpočetní služby pro jejich obsluhu:

| **Scénář** | **Výpočetní služba** |
| --- | --- |
| Potřebuji během několika sekund zřídit virtuální počítače s Linuxem a Windows s konfigurací podle svého výběru. | [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines) |
| Potřebuji dosáhnout vysoké dostupnosti prostřednictvím automatického škálování a vytváření tisíců virtuálních počítačů během několika minut. | [Škálovací sady virtuálních počítačů](https://azure.microsoft.com/services/virtual-machine-scale-sets) |
| Chci zjednodušit nasazení, správu a provoz Kubernetes. | [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service) |
| Potřebuji zrychlit vývoj aplikací pomocí bezserverové architektury řízené událostmi. | [Azure Functions](https://azure.microsoft.com/services/functions) |
| Potřebuji vyvíjet mikroslužby a orchestrovat kontejnery ve Windows a Linuxu. | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) |
| Chci rychle vytvářet cloudové aplikace pro web a mobilní zařízení pomocí plně spravované platformy. | [Azure App Service](https://azure.microsoft.com/services/app-service) |
| Chci kontejnerizovat aplikace a snadno spouštět kontejnery jediným příkazem. | [Azure Container Instances](https://azure.microsoft.com/services/container-instances) |
| Potřebuji plánovat úlohy a spravovat výpočty v cloudovém měřítku s možností škálování na desítky, stovky nebo tisíce virtuálních počítačů. | [Azure Batch](https://azure.microsoft.com/services/batch) |
| Potřebuji vytvářet vysoce dostupné škálovatelné cloudové aplikace a rozhraní API, které mi pomohou soustředit se na aplikace, a ne na hardware. | [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services) |

## <a name="regional-availability"></a>Regionální dostupnost

Azure vám umožní dodávat služby v měřítku, jaké potřebujete, abyste mohli oslovit zákazníky a partnery,  _ať jsou kdekoli_. Klíčovým faktorem při plánování cloudového nasazení je určení, která oblast Azure bude hostovat prostředky vašich úloh.

Některé výpočetní možnosti, například Azure App Service, jsou všeobecně dostupné ve většině oblastí Azure. Některé výpočetní služby jsou však podporované jen ve vybraných oblastech. Některé typy virtuálních počítačů a jejich přidružené typy úložišť mají omezenou regionální dostupnost. Než se rozhodnete, ve kterých oblastech nasadíte výpočetní prostředky, doporučujeme na [stránce oblastí](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=azure-vmware-cloudsimple,cloud-services,batch,container-instances,app-service,service-fabric,functions,kubernetes-service,virtual-machine-scale-sets,virtual-machines)  zjistit nejnovější stav regionální dostupnosti.

Další informace o globální infrastruktuře Azure najdete na  [stránce oblastí Azure](https://azure.microsoft.com/global-infrastructure/regions). Můžete si také prohlédnout  [produkty dostupné podle oblastí](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all), kde najdete konkrétní podrobnosti o celkových službách dostupných v jednotlivých oblastech Azure.

## <a name="data-residency-and-compliance-requirements"></a>Požadavky na rezidenci dat a dodržování předpisů

Na vaše úlohy se budou často vztahovat právní a smluvní požadavky týkající se datového úložiště. Tyto požadavky se mohou lišit v závislosti na sídle vaší organizace, jurisdikci, ve které se ukládají a zpracovávají soubory a data, a příslušném obchodním sektoru. Mezi datové povinnosti, které je potřeba zvážit, patří klasifikace dat, umístění dat a individuální zodpovědnosti za ochranu dat v rámci sdíleného modelu odpovědnosti. Mnohá výpočetní řešení závisejí na propojených prostředcích úložiště. Tento požadavek může mít také vliv na rozhodování ohledně výpočetních prostředků. Tyto požadavky jsou rozebrány v dokumentu white paper o  [zajištění odpovídající rezidence dat a zabezpečení s využitím Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Součástí vašeho úsilí o dodržování předpisů může být kontrola nad tím, kde jsou fyzicky umístěny vaše výpočetní prostředky. Oblasti Azure jsou uspořádané do skupin označovaných jako zeměpisné oblasti.  [Zeměpisná oblast Azure](https://azure.microsoft.com/global-infrastructure/geographies)  zaručuje, že se v rámci příslušných zeměpisných a politických hranic dodržují požadavky na rezidenci dat, suverenitu, dodržování předpisů a odolnost. Pokud vaše úlohy podléhají suverenitě dat nebo jiným požadavkům na dodržování předpisů, musíte prostředky úložiště nasadit do oblastí ve vyhovující geografické oblasti Azure.

## <a name="establish-controls-for-compute-services"></a>Stanovení kontrolních mechanismů pro výpočetní služby

Při přípravě cílového prostředí můžete stanovit kontrolní mechanismy, které omezují, jaké prostředky mohou jednotliví uživatelé nasazovat. Tyto kontrolní mechanismy vám pomohou s řízením nákladů a omezením rizik zabezpečení a zároveň umožní vývojářům a IT týmům nasazovat a konfigurovat prostředky potřebné pro podporu vašich úloh.

Po zjištění a zdokumentování požadavků na cílové prostředí můžete pomocí [Azure Policy](/azure/governance/policy/overview) určit výpočetní prostředky, které uživatelé mohou vytvářet. Kontrolní mechanismy mohou mít formu [povolení nebo zákazu vytváření různých typů výpočetních prostředků](/azure/governance/policy/samples/allowed-resource-types). Uživatele můžete například omezit tak, aby mohli vytvářet jen prostředky Azure App Service nebo Azure Functions. Pomocí zásad můžete také řídit přípustné možnosti při vytváření prostředku, například [omezit, jaké cenové úrovně virtuálních počítačů lze zřídit](https://docs.microsoft.com/azure/governance/policy/samples/allowed-skus-storage) nebo [povolit jen konkrétní image virtuálních počítačů](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

Zásady mohou být vymezené na prostředky, skupiny prostředků, předplatná a skupiny pro správu. Tyto zásady můžete začlenit do definic [Azure Blueprint](/azure/governance/blueprints/overview) a opakovaně je používat v rámci svého cloudu.

