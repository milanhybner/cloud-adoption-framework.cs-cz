---
title: Ukázkové zásady akcelerace nasazení – příkazy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ukázkové zásady akcelerace nasazení – příkazy
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4a2b1666332ca884dfb95b2b2372f3b5518bd635
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030304"
---
# <a name="deployment-acceleration-sample-policy-statements"></a>Ukázkové zásady akcelerace nasazení – příkazy

Jednotlivé příkazy zásad cloudu jsou pokyny pro řešení konkrétních rizik zjištěných během procesu posouzení rizik. Tyto příkazy by měly poskytnout stručné shrnutí rizik a plánů, které je třeba řešit. Každá definice příkazu by měla obsahovat tyto informace:

- **Technické riziko.** Souhrn rizika, které tato zásada bude řešit.
- **Prohlášení o zásadách.** Jasné souhrnné vysvětlení požadavků zásad.
- **Možnosti návrhu.** Užitečná doporučení, specifikace nebo další pokyny, které mohou týmy IT a vývojáři použít při implementaci těchto zásad.

Následující ukázkové příkazy zásad řeší běžná obchodní rizika související s konfigurací. Tyto příkazy jsou příklady, na které můžete odkazovat při konceptech příkazů zásad, které řeší potřeby vaší organizace. Tyto příklady se nepovažují za podrobné a některé možnosti zásad se týkají každého identifikovaného rizika. Pracujte úzce s podnikáním a týmy IT a Identifikujte nejlepší zásady pro Vaši jedinečnou sadu rizik.

## <a name="reliance-on-manual-deployment-or-configuration-of-systems"></a>Spoléhání na Ruční nasazení nebo konfiguraci systémů

**Technické riziko:** Spoléhání se na lidský zásah během nasazování nebo konfigurace zvyšuje pravděpodobnost lidské chyby a snižuje opakovatelnost a předvídatelnost nasazení a konfigurace systémů. Obvykle to vede k pomalejšímu nasazování systémových prostředků.

**Prohlášení o zásadách:** Všechny prostředky nasazené do cloudu by se měly nasadit pomocí šablon nebo skriptů pro automatizaci, kdykoli to bude možné.

**Možné možnosti návrhu:** [Azure Resource Manager šablony](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) poskytují přístup k nasazení prostředků do Azure prostřednictvím infrastruktury jako kódu. V rámci [stavebních bloků Azure](https://github.com/mspnp/template-building-blocks/wiki) získáte nástroj příkazového řádku a sadu správce prostředků šablon navržených tak, aby se zjednodušilo nasazení prostředků Azure.

## <a name="lack-of-visibility-into-system-issues"></a>Nedostatečné viditelnosti systémových problémů

**Technické riziko:** Nedostatečné monitorování a Diagnostika pro obchodní systémy zabraňují provozním pracovníkům v identifikaci a oprava problémů před výpadkem systému a můžou významně prodloužit dobu potřebnou k tomu, aby se výpadek mohl správně vyřešit.

**Prohlášení o zásadách:** Implementují se tyto zásady:

- Pro všechny produkční systémy a komponenty budou identifikovány klíčové metriky a diagnostické míry a monitorovací a diagnostické nástroje budou na tyto systémy pravidelně sledovány provozními pracovníky.
- Operace budou zvážit použití nástrojů pro monitorování a diagnostiku v neprodukčních prostředích, jako je například fázování a kontrola, které identifikují problémy se systémem před tím, než dojde v produkčním prostředí.

**Možné možnosti návrhu:** [Azure monitor](https://docs.microsoft.com/azure/azure-monitor), která také zahrnuje Log Analytics a Application Insights, poskytuje nástroje pro shromažďování a analýzu telemetrie, které vám pomůžou pochopit, jak vaše aplikace provádí a aktivně identifikují problémy, které mají vliv na ně. prostředky, na kterých jsou závislé.

## <a name="configuration-security-reviews"></a>Revize zabezpečení konfigurace

**Technické riziko:** V průběhu času můžou nové bezpečnostní hrozby nebo obavy zvýšit riziko neoprávněného přístupu k zabezpečeným prostředkům.

**Prohlášení o zásadách:** Procesy zásad správného řízení cloudu musí zahrnovat čtvrtletní kontrolu s týmy správy konfigurací, které identifikují škodlivé aktéry nebo vzorce používání, které by měly být znemožněny konfigurací cloudového prostředku.

**Možné možnosti návrhu:** Navažte čtvrtletní kontrolu zabezpečení, která zahrnuje členy týmu zásad správného řízení a pracovníky IT zodpovědné za konfiguraci cloudových aplikací a prostředků. Projděte si stávající data a metriky zabezpečení a zaveďte mezery v aktuálních zásadách a nástrojích akcelerace nasazení a aktualizujte zásady tak, aby opravily všechna nová rizika.

## <a name="next-steps"></a>Další postup

Použijte ukázky uvedené v tomto článku jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

Pokud chcete začít vyvíjet vlastní příkazy zásad související se správou identit, Stáhněte si [šablonu směrného plánu identity](./template.md).

Pokud chcete zrychlit přijetí této disciplíny, vyberte [akčního Průvodce zásad správného řízení](../guides/index.md) , který nejlépe zarovnává vaše prostředí. Pak upravte návrh tak, aby zahrnoval konkrétní podniková rozhodnutí o zásadách.

Sestavování rizik a tolerance, zavedení procesu řízení a komunikace s dodržováním zásad zrychlení nasazení.

> [!div class="nextstepaction"]
> [Vytváření procesů dodržování zásad](./compliance-processes.md)