---
title: Cost Management metriky, ukazatele a tolerance rizik
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vysvětlení služby Cost Management ve vztahu k zásadám správného řízení v cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: be1d4456ac8924c87241089c637fa3aacc38fb47
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027509"
---
# <a name="cost-management-metrics-indicators-and-risk-tolerance"></a>Cost Management metriky, ukazatele a tolerance rizik

Tento článek je určený k tomu, aby vám pomohla při stanovení tolerance podnikového rizika v souvislosti s Cost Management. Definování metrik a indikátorů vám pomůže vytvořit obchodní případ pro investici do splatnosti Cost Management disciplíny.

## <a name="metrics"></a>Metriky

Cost Management se obecně zaměřuje na metriky související s náklady. V rámci analýzy rizik budete chtít shromažďovat data týkající se vašich současných a plánovaných výdajů na cloudové úlohy, abyste zjistili, kolik rizika čelíte a jakým způsobem je důležité zajistit, aby se v rámci řízení nákladů na vaše cloudové strategie.

Následují příklady užitečných metrik, které byste měli shromáždit, abyste mohli vyhodnotit toleranci rizik v rámci Cost Management disciplíny:

- **Roční Útrata:** Celkové roční náklady za služby poskytované poskytovatelem cloudu.
- **Měsíční útrata:** Celkové měsíční náklady na služby poskytované poskytovatelem cloudu.
- **Předpověď oproti skutečnému poměru:** Poměr porovnání předpovědi a skutečné útraty (měsíčně nebo roční).
- **Poměr tempa přijetí (MOM):** Procento rozdílů v cloudových nákladech od měsíce do měsíce.
- **Akumulované náklady:** Celková časově rozlišená denní útrata začíná od začátku měsíce.
- **Trendy útraty:** Trend útraty na základě rozpočtu.

## <a name="risk-tolerance-indicators"></a>Indikátory tolerance rizik

Během předčasného malého nasazení, jako je vývoj a testování nebo experimentální první pracovní vytížení, Cost Management pravděpodobně relativně nízké riziko. Při nasazení většího objemu prostředků se riziko zvýší a tolerance firmy se bude nejspíš odmítat. Kromě toho, protože více týmů pro přijetí cloudu má možnost konfigurovat nebo nasazovat prostředky do cloudu, roste riziko a sníží se jejich tolerance. Naopak rostoucí obor Cost Management převezme uživatele z fáze pro přijetí do cloudu, aby mohli nasadit pokročilejší nové technologie.

V počátečních fázích přijetí cloudu budete pracovat s vaší firmou a určit základní hodnoty tolerance rizik. Jakmile budete mít směrný plán, budete muset určit kritéria, která aktivují investici v oboru Cost Management. Tato kritéria budou pravděpodobně pro každou organizaci odlišná.

Po zjištění [obchodních rizik](./business-risks.md)budete pracovat s vaší firmou a identifikovat srovnávací testy, které by mohly způsobit zvýšení těchto rizik. Tady je několik příkladů toho, jak se metriky, jako jsou uvedené výše, porovnávají s tolerancí standardních hodnot rizik, aby bylo jasné, že je potřeba další investovat do Cost Management.

- **Řízený závazek (nejběžnější):** Společnost, která se zavazuje k útratě $X 000000 tento rok na dodavatele cloudu. Potřebují Cost Management disciplínu, aby firma nepřekročila své cíle útraty o více než 20% a aby využívala alespoň 90% tohoto závazku.
- **Procentuální hodnota triggeru:** Společnost s cloudovou útratou, která je pro produkční systémy stabilní. Pokud se tyto změny zvýší o více než _x%_ , bude se cost management disciplína převažovat za moudrou.
- **Nadřízená aktivační událost:** Společnost, která se domnívá jejich nasazená řešení, je nadřízená. Cost Management je prioritní investování, dokud nedokáže předvést správné sblížení zřizování a využití prostředků.
- **Aktivační událost měsíčních výdajů:** Společnost, která se věnuje $x 000 za měsíc, se považují za proměnlivou cenu. Pokud útrata překročí tuto částku v daném měsíci, bude muset investovat do Cost Management.
- **Aktivační událost roční útraty:** Společnost s IT R & D rozpočet, který umožňuje vytrávit $X za rok na experimentování s cloudem za 1000. Můžou provozovat produkční úlohy v cloudu, ale budou se i nadále považovat za experimentální řešení, pokud rozpočet nepřekročí tuto částku. Po převzetí služeb se budou muset považovat za rozpočet jako investici do produkčního prostředí a úzce spravovat výdaje.
- **Provozní náklady – nepříznivé (Neběžné):** Jako společnost se Averse na provozní výdaje a před nasazením úlohy pro vývoj/testování bude nutné, aby byly na svém místě Cost Management kontroly.

## <a name="next-steps"></a>Další postup

Pomocí [šablony pro správu cloudu](./template.md), metriky dokumentů a indikátory tolerance, které odpovídají aktuálnímu plánu přijetí do cloudu.

Projděte si ukázkové zásady Cost Management jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

> [!div class="nextstepaction"]
> [Kontrola ukázkových zásad](./policy-statements.md)