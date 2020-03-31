---
title: Obchodní rizika konzistence prostředků
description: Rozhraní pro přijetí v cloudu pro Azure vám pomůže pochopit typické přijetí oboru konzistence prostředků v rámci strategie zásad správného řízení v cloudu.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3eff0f6130adc35d8c087d385d42b06e141f3c64
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433501"
---
# <a name="resource-consistency-motivations-and-business-risks"></a>Motivace konzistence prostředků a obchodní rizika

Tento článek popisuje důvody, proč zákazníci obvykle přijímají pravidla konzistence prostředků v rámci strategie zásad správného řízení cloudu. Poskytuje taky několik příkladů potenciálních obchodních rizik, která můžou řídit příkazy zásad.

<!-- markdownlint-disable MD026 -->

## <a name="resource-consistency-relevancy"></a>Relevanci konzistence prostředků

Při nasazení prostředků a úloh Cloud nabízí větší flexibilitu a flexibilitu nad většinou tradičních místních datových center. Tyto potenciální cloudové výhody se ale také přidávají spárováním s potenciálními nevýhodami správy, které mohou vážně ohrozit úspěšnost vašeho cloudového přijetí. Jaké prostředky jste nasadili? Jaké týmy vlastní prostředky? Máte dostatek prostředků pro podporu úloh? Jak poznáte, jestli jsou úlohy v pořádku?

Konzistence prostředků je zásadní, aby se zajistilo, že se prostředky nasazují, aktualizují a konfigurují konzistentně a že se tyto přerušení minimalizují a odpravují ve chvíli, kdy je to možné.

V rámci oboru konzistence prostředků je potřeba identifikovat a zmírnit obchodní rizika související s provozními aspekty nasazení v cloudu. Konzistence prostředků zahrnuje monitorování aplikací, úloh a výkonu prostředků. Zahrnuje také úlohy potřebné pro splnění požadavků na škálování, poskytování možností zotavení po havárii, zmírnění narušení výkonu smlouva SLA (SLA) a proaktivní Vyhněte se porušením smlouvy SLA prostřednictvím automatizované nápravy.

Počáteční testovací nasazení nemusí vyžadovat mnohem déle než přijetí některých standardů pojmenovávání a označování, které podporují vaše požadavky na konzistenci prostředků. Vzhledem k tomu, že vaše cloudové přijetí je nasazené a nasazujete složitější a klíčové prostředky, je potřeba investovat do oboru konzistence prostředků rychle zvyšovat.

## <a name="business-risk"></a>Obchodní riziko

Obor konzistence prostředků se pokusí adresovat základní provozní rizika. Spolupracujte se svými podnikovými a IT týmy a Identifikujte tato rizika a sledujte, co je pro vás důležité při plánování a implementaci cloudových nasazení.

Rizika se budou lišit v rámci organizace, ale následující slouží jako běžné rizika, která můžete použít jako výchozí bod pro diskuze v rámci svého týmu zásad správného řízení v cloudu:

- **Zbytečné provozní náklady.** Zastaralé nebo nepoužívané prostředky nebo prostředky, které jsou v době nízké poptávky nadměrné, doplňte zbytečné provozní náklady.
- **Nezřízené prostředky.** Prostředky, které jsou vyšší než očekávaná poptávka, můžou způsobit přerušení v chodu, protože cloudové prostředky jsou zahlcené poptávkou.
- **Správa neefektivity.** Nedostatečná metadata pro pojmenování a označování, která jsou přidružená k prostředkům, můžou vést k tomu, že zaměstnanci IT mají potíže při hledání prostředků pro úlohy správy nebo při identifikaci vlastnictví a účetní informace související s prostředky. Výsledkem je Správa neefektivity, která může zvýšit náklady a zpomalit jejich odezvu na přerušení služeb nebo jiné provozní problémy.
- **Přerušování firmy.** Přerušení služeb, které vedou k porušení smluv o úrovni služeb (SLA) vaší organizace, můžou vést ke ztrátě obchodních a jiných finančních dopadů na vaši společnost.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat obchodní rizika, která by mohla být zavedena aktuálním plánem přijetí cloudu.

Jakmile bude navázáno porozumění reálným obchodním rizikům, je dalším krokem vytvoření dokumentu tolerance firmy pro rizika a indikátory a klíčové metriky pro monitorování této tolerance.

> [!div class="nextstepaction"]
> [Pochopení ukazatelů, metrik a tolerance rizik](./metrics-tolerance.md)
