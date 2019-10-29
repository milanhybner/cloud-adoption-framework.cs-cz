---
title: Cílová zóna s Terraformu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se používat Terraformu k sestavování zón odpočívadl.
author: arnaudlh
ms.author: arnaul
ms.date: 10/16/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b540e2f4ea2a9c7f091a5505a19ad61eac05c971
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049767"
---
# <a name="use-terraform-to-build-your-landing-zones"></a>Použití Terraformu k sestavení zón odpočívadla

Kromě služeb Azure Native Services často zákazníci a partneři používají Terraformu Hashicorp k nasazení zón vykládku. V této části se dozvíte, jak pomocí cílové zóny prototypů nasadit základní protokolování, monitorování účtů a možnosti zabezpečení pro předplatné Azure.

## <a name="purpose-of-the-landing-zone"></a>Účel cílové zóny

Platforma pro nasazení v cloudu pro Terraformu má omezené sady odpovědností a funkcí, které vynutily protokolování, monitorování účtů a zabezpečení. Tuto cílovou zónu jsme navrhli pomocí standardních komponent, které se nazývají Terraformu moduly, aby se vynutila konzistence napříč prostředky nasazenými v prostředí.

## <a name="using-standard-modules"></a>Použití standardních modulů

Opakované použití komponent je základní princip infrastruktury jako kódu. Moduly jsou instrumentované při definování standardů a konzistence napříč nasazeními prostředků v rámci a napříč prostředími. Sada modulů použitá k nasazení této první zóny je k dispozici v oficiálním [registru terraformu](https://registry.terraform.io/search?q=aztfmod).

## <a name="architecture-diagram"></a>Diagram architektury

První cílová zóna nasadí do vašeho předplatného tyto komponenty:

![Základní cílová zóna pomocí Terraformu](../../_images/ready/foundations-terraform-landingzone.png)

## <a name="capabilities"></a>Možnosti

Nasazené komponenty a jejich účel jsou následující:

| Součást | zodpovědní |
|---------|---------|
| Skupiny prostředků | Základní skupiny prostředků, které jsou potřeba pro základ |
| Protokolování aktivit | Auditování všech aktivit předplatného a archivace: </br> – Účet úložiště </br> -Event Hubs |  
| Protokolování diagnostiky | Protokol všech operací se uchovává po dobu určitého počtu dnů: </br> – Účet úložiště </br> -Event Hubs |
| Log Analytics | Ukládá všechny protokoly operací. </br> Nasazení běžných řešení pro hloubkové osvědčené postupy pro aplikace: </br> - NetworkMonitoring </br> - ADAssessment </br> – ADReplication </br> - AgentHealthAssessment </br> - DnsAnalytics </br> - KeyVaultAnalytics
| Security Center | Výstrahy a hygieny zabezpečení odeslané na e-mail a telefonní číslo |

## <a name="use-this-blueprint"></a>Použití tohoto podrobného plánu

Předtím, než použijete cílovou zónu Foundation rozhraní pro přijetí do cloudu, přečtěte si následující předpoklady, rozhodnutí a pokyny k implementaci.

## <a name="assumptions"></a>Předpoklady

Při definování této počáteční cílové zóny byly zváženy následující předpoklady nebo omezení. Pokud tyto předpoklady odpovídají vašim omezením, můžete podrobný plán použít k vytvoření první cílové zóny. Plán lze také rozšířit a vytvořit tak podrobný plán cílové zóny, který vyhovuje vašim jedinečným omezením.

- **Omezení předplatného:** Toto úsilí o přijetí pravděpodobně nepřekračuje [limity předplatného](https://docs.microsoft.com/azure/azure-subscription-service-limits). Dva běžné indikátory jsou překročení 25 000 virtuálních počítačů nebo 10 000 vCPU.
- **Dodržování předpisů:** Pro tuto cílovou zónu nejsou potřeba žádné požadavky na dodržování předpisů od jiných výrobců.
- **Složitost architektury:** Složitost architektury nevyžaduje další produkční odběry.
- **Sdílené služby:** V Azure nejsou žádné sdílené služby, které vyžadují, aby se toto předplatné zpracovalo jako paprskový v architektuře hvězdicové architektury.

Pokud tyto předpoklady odpovídají vašemu současnému prostředí, může být tento plán dobrým způsobem, jak začít vytvářet cílovou zónu.

## <a name="design-decisions"></a>Rozhodnutí o návrhu

V zóně pro vykládku Terraformu jsou zastoupena tato rozhodnutí:

| Součást | Rozhodnutí | Alternativní přístupy |
| --- | --- | --- |
|Protokolování a monitorování | Bude použit pracovní prostor Azure Monitor Log Analytics. Dojde k zřízení účtu úložiště diagnostiky i centra událostí. |         |
|Síť | Není k dispozici síť, která bude implementována v jiné cílové zóně. |[Rozhodnutí o síti](../considerations/network-decisions.md) |
|Identita | Předpokládá se, že předplatné je už přidružené k instanci Azure Active Directory. | [Osvědčené postupy správy identit](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) |
| Zásady | V této cílové zóně se v současné době předpokládá, že se nepoužívají žádné zásady Azure. | |
|Návrh předplatného | Neuvedeno – Navrženo pro jedno produkční předplatné. | [Škálování předplatných](../considerations/scaling-subscriptions.md) |
| Skupiny pro správu | Neuvedeno – Navrženo pro jedno produkční předplatné. |[Škálování předplatných](../considerations/scaling-subscriptions.md) |
| Skupiny prostředků | Neuvedeno – Navrženo pro jedno produkční předplatné. | [Škálování předplatných](../considerations/scaling-subscriptions.md) |
| Data | Nevztahuje se | [Výběr správné možnosti SQL Server v dokumentaci k Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) a [Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Úložiště|Nevztahuje se|[Pokyny k Azure Storage](../considerations/storage-guidance.md) |
| Standardy pro vytváření názvů | Při vytvoření prostředí se vytvoří také jedinečná předpona. Tato předpona používá prostředky, které vyžadují globálně jedinečný název (například účty úložiště). Vlastní název se připojí s náhodnou příponou. Použití značky je udělené podle pokynů v následující tabulce. | [Osvědčené postupy pojmenování a označování](../considerations/naming-and-tagging.md) |
| Správa nákladů | Nevztahuje se | [Sledování nákladů](../azure-best-practices/track-costs.md) |
| Služby Compute | Nevztahuje se | [Možnosti služby Compute](../considerations/compute-decisions.md) |

### <a name="tagging-standards"></a>Standardy označování

U všech prostředků a skupin prostředků se musí vyskytovat následující sada minimálních značek:

| Název značky | Popis | Klíč | Ukázková hodnota |
|--|--|--|--|
| Organizační jednotka | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni | BusinessUnit | FINANCE, MARKETING, {název produktu}, CORP, SHAREd |
| Nákladové středisko | Účetní nákladové středisko přidružené tomuto prostředku| CostCenter | Číslo |
| Zotavení po havárii | Obchodní důležitost aplikace, úlohy nebo služby | DR | SE ZAPNUTÝM DR, BEZ DR |
| Prostředí | Prostředí nasazení aplikace, úlohy nebo služby |  ENV | Prod, vývoj, QA, fáze, testování, školení |
| Jméno vlastníka | Vlastník aplikace, úlohy nebo služby| Vlastník | e-mail |
| Typ nasazení | Definuje způsob údržby prostředků. | Typ nasazení | Ruční, Terraformu |
| Version | Verze nasazeného podrobného plánu | version | v 0,1 |
| Název aplikace | Název přidružené aplikace, služby nebo úlohy přidružené k prostředku | ApplicationName | název aplikace |

## <a name="customize-and-deploy-your-first-landing-zone"></a>Přizpůsobení a nasazení první cílové zóny

Můžete [klonovat cílovou zónu terraformu Foundation](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready). Můžete snadno začít s cílovou zónou úpravou proměnných Terraformu. V našem příkladu používáme **blueprint_foundations. sandbox. auto. tfvars**, takže terraformu automaticky nastaví hodnoty v tomto souboru za vás.

Pojďme se podívat na různé oddíly proměnných.

V tomto prvním objektu vytvoříme dvě skupiny prostředků v `southeastasia` oblasti s názvem "-hub-Core-s" a "-hub-Core-SEK" společně s předponou přidanou za běhu.

```hcl
resource_groups_hub = {
    HUB-CORE-SEC    = {
        name = "-hub-core-sec"
        location = "southeastasia"
    }
    HUB-OPERATIONS  = {
        name = "-hub-operations"
        location = "southeastasia"
    }
}
```

Dále určíme oblasti, ve kterých můžeme nastavit základ. Zde `southeastasia` budou použity k nasazení všech prostředků.

```hcl
location_map = {
    region1   = "southeastasia"
    region2   = "eastasia"
}
```

Pak určíme dobu uchovávání protokolů operací a protokolů předplatného Azure. Tato data budou uložená v samostatných účtech úložiště a v centru událostí, jejichž názvy jsou náhodně vygenerované, protože musí být jedinečné.

```hcl
azure_activity_logs_retention = 365
azure_diagnostics_logs_retention = 60
```

Do tags_hub určíme minimální sadu značek, které budou aplikovány na všechny vytvořené prostředky.

```hcl
tags_hub = {
    environment     = "DEV"
    owner           = "Arnaud"
    deploymentType  = "Terraform"
    costCenter      = "65182"
    BusinessUnit    = "SHARED"
    DR              = "NON-DR-ENABLED"
}
```

Pak zadáte název Log Analytics a sadu řešení, která budou analyzovat nasazení. Tady jsme zachovali monitorování sítě, AD Assessment a replikaci, DNS Analytics a Key Vault Analytics.

```hcl

analytics_workspace_name = "lalogs"

solution_plan_map = {
    NetworkMonitoring = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/NetworkMonitoring"
    },
    ADAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADAssessment"
    },
    ADReplication = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADReplication"
    },
    AgentHealthAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/AgentHealthAssessment"
    },
    DnsAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/DnsAnalytics"
    },
    KeyVaultAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/KeyVaultAnalytics"
    }
}

```

Dále jsme nakonfigurovali parametry výstrahy pro Azure Security Center.

```hcl
# Azure Security Center Configuration
security_center = {
    contact_email   = "joe@contoso.com"
    contact_phone   = "+6500000000"
}
```

## <a name="getting-started"></a>Začínáme

Po kontrole konfigurace můžete nasadit konfiguraci, protože byste nasadili prostředí Terraformu. Doporučujeme však použít Rover, což je kontejner Docker, který umožňuje nasazení ze systému Windows, Linux nebo MacOS. Můžete začít s [úložištěm GitHub Rover](https://github.com/aztfmod/rover).

## <a name="next-steps"></a>Další kroky

Základní cílová zóna definuje základy pro komplexní prostředí způsobem rozloženého. Tato edice poskytuje sadu velmi jednoduchých možností, které lze rozšířit o:

- Přidání dalších modulů do podrobného plánu.
- Vrstvení dalších zón pro vykládku nad ní.

Rozvětvení zón je dobrým zvykem pro odkládací systémy, správu verzí jednotlivých komponent, které používáte, a umožňující rychlou inovaci a stabilitu pro nasazení infrastruktury jako kódu.

Budoucí referenční architektury demonstrují tento koncept pro topologii hvězdicové topologie.

> [!div class="nextstepaction"]
> [Kontrola ukázky cílové zóny v rámci použití Terraformu](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready)
