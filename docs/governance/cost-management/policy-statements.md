---
title: Cost Management ukázkové příkazy zásad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cost Management ukázkové příkazy zásad
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fc8a691b446b5c40534e7189cb9d381aabd5f402
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828146"
---
# <a name="cost-management-sample-policy-statements"></a>Cost Management ukázkové příkazy zásad

Jednotlivé příkazy zásad cloudu jsou pokyny pro řešení konkrétních rizik zjištěných během procesu posouzení rizik. Tyto příkazy by měly poskytnout stručné shrnutí rizik a plánů, které je třeba řešit. Každá definice příkazu by měla obsahovat tyto informace:

- **Obchodní riziko.** Souhrn rizika, které tato zásada bude řešit.
- **Prohlášení o zásadách.** Jasné souhrnné vysvětlení požadavků zásad.
- **Možnosti návrhu.** Užitečná doporučení, specifikace nebo další pokyny, které mohou týmy IT a vývojáři použít při implementaci těchto zásad.

Následující vzorové příkazy zásad řeší běžná obchodní rizika související s náklady. Tyto příkazy jsou příklady, na které můžete odkazovat při konceptech příkazů zásad, které řeší potřeby vaší organizace. Tyto příklady se nepovažují za podrobné a některé možnosti zásad se týkají každého identifikovaného rizika. Pracujte úzce s podnikáním a týmy IT a Identifikujte nejlepší zásady pro Vaši jedinečnou sadu rizik.

## <a name="future-proofing"></a>Budoucí kontrola

**Obchodní riziko:** Aktuální kritéria, která neopravňují k investicím do Cost Managementho pravidla od týmu zásad správného řízení. V budoucnu ale předpokládáme takovou investici.

**Prohlášení o zásadách:** Všechny prostředky nasazené do cloudu byste měli přidružit pomocí fakturační jednotky a aplikace nebo úlohy. Tato zásada zajistí, že budoucí Cost Management úsilí bude platit.

**Možnosti návrhu:** Informace o vytvoření budoucího základu služby Proofing Foundation najdete v diskusích souvisejících s vytvářením MVP pro řízení v rámci [akčních průvodců](../journeys/index.md) , které jsou součástí návodu k zavedení cloudu.

## <a name="budget-overruns"></a>Přetečení rozpočtu

**Obchodní riziko:** Samoobslužné nasazení vytváří riziko přetrávení.

**Prohlášení o zásadách:** Jakékoli nasazení cloudu musí být přidělené fakturační jednotce se schváleným rozpočtem a mechanismem pro rozpočtové limity.

**Možnosti návrhu:** V Azure je možné řídit rozpočet pomocí [Azure cost management](/azure/cost-management/manage-budgets)

## <a name="underutilization"></a>Nízkého využití

**Obchodní riziko:** Společnost se předplatila pro cloudové služby nebo učinila roční závazek na výdaje na určitou částku. Existuje riziko, že se nepoužije sjednaná částka, což vede ke ztrátě investic.

**Prohlášení o zásadách:** Každá fakturační jednotka s přiděleným rozpočtem cloudu bude každoročně odpovídat na nastavení rozpočtů, čtvrtletní úpravu rozpočtů a měsíčně k přidělení času pro kontrolu plánovaných a skutečných výdajů. Prodiskutujte všechny odchylky větší než 20% s vedoucím fakturační jednotky měsíčně. Pro účely sledování přiřaďte všechny prostředky k fakturační jednotce.

**Možnosti návrhu:**

- V Azure je možné spravovat plánované srovnání skutečné útraty prostřednictvím [Azure cost management](/azure/cost-management/quick-acm-cost-analysis)
- Existuje několik možností, jak seskupit prostředky podle fakturační jednotky. V Azure je vhodné zvolit [model konzistence prostředků](../../decision-guides/resource-consistency/index.md) ve spojení s týmem zásad správného řízení a použít pro všechny prostředky.

## <a name="overprovisioned-assets"></a>Nadřízená aktiva

**Obchodní riziko:** V tradičních místních datacentrech je běžné nasazení prostředků s dodatečným plánováním kapacity pro růst ve vzdálené budoucnosti. Cloud může škálovat rychleji než tradiční zařízení. Ceny prostředků v cloudu se také účtují na základě technické kapacity. Existuje riziko, že starý místní postup uměle nepřímým využitím cloudových výdajů.

**Prohlášení o zásadách:** Všechny prostředky nasazené do cloudu musí být zaregistrované v programu, který může monitorovat využití a nahlásit veškerou kapacitu vyšší než 50% využití. Všechny prostředky nasazené do cloudu musí být logického typu seskupené nebo označené tak, aby členové týmu zásad správného řízení mohli zajišťovat pracovníka úlohy týkající se jakékoli optimalizace převedených prostředků.

**Možnosti návrhu:**

- V Azure vám [Azure Advisor](/azure/advisor/advisor-cost-recommendations) může poskytnout doporučení pro optimalizaci.
- Existuje několik možností, jak seskupit prostředky podle fakturační jednotky. V Azure je vhodné zvolit [model konzistence prostředků](../../decision-guides/resource-consistency/index.md) ve spojení s týmem zásad správného řízení a použít pro všechny prostředky.

## <a name="overoptimization"></a>Přeoptimalizace

**Obchodní riziko:** Efektivní správa nákladů vytváří nová rizika. Optimalizace útraty je pro výkon systému invertovaná. Při snižování nákladů existuje riziko, že dojde k převýšení útraty a k výrobě nekvalitních uživatelských prostředí.

**Prohlášení o zásadách:** Jakékoli assety, které přímo ovlivňují prostředí zákazníka, musí být identifikovány prostřednictvím seskupování nebo označování. Než optimalizujete všechny prostředky, které mají vliv na uživatelské prostředí, musí tým zásad správného řízení pro Cloud upravit optimalizaci na základě minimálně 90 dnů trendů využití. Zdokumentujte všechny sezónní nebo řízené shluky řízený událostmi, které se považují za optimalizaci prostředků.

**Možnosti návrhu:**

- V Azure můžou [funkce přehledů Azure monitor](/azure/azure-monitor/insights/vminsights-performance) pomáhat s analýzou využití systému.
- K dispozici je několik možností seskupování a označování prostředků na základě rolí. V Azure byste měli zvolit [model konzistence prostředků](../../decision-guides/resource-consistency/index.md) ve spojení s týmem zásad správného řízení a použít ho u všech prostředků.

## <a name="next-steps"></a>Další postup

Použijte ukázky uvedené v tomto článku jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

Pokud chcete začít vyvíjet vlastní příkazy zásad týkající se Cost Management, Stáhněte si [šablonu cost management](./template.md).

Pokud chcete zrychlit přijetí této disciplíny, vyberte [akčního Průvodce zásad správného řízení](../journeys/index.md) , který nejlépe zarovnává vaše prostředí. Pak upravte návrh tak, aby zahrnoval konkrétní podniková rozhodnutí o zásadách.

Sestavování rizik a tolerance, zavedení procesu řízení a komunikace Cost Management dodržování zásad.

> [!div class="nextstepaction"]
> [Vytváření procesů dodržování zásad](./compliance-processes.md)
