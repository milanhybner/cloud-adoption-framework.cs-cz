---
title: 'Inovace v cloudu: měření'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do cloudových inovací – měření obsahu
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 00928171c3bfba1638a7e8e43ea08df4745754d2
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557645"
---
# <a name="measure-for-customer-impact"></a>Měření dopadu zákazníka

Existuje několik způsobů, jak změřit dopad na zákazníky. Tento článek vám pomůže definovat míry, které vám můžou pomoci ověřit hypotézu vytvořenou při pokusu o [sestavení pomocí zákaznických soucit](./build.md).

## <a name="strategic-metrics"></a>Strategické metriky

Během [fáze strategie](../../strategy/index.md) životního cyklu přijetí do cloudu se čtenáři provedou vytvořením a dokumentací [motivace](../../strategy/motivations.md) a [obchodních výsledků](../../strategy/business-outcomes/index.md). Tyto cvičení poskytují sadu metrik, které se mají použít jako test dopadu na zákazníky. Po úspěšném provedení inovace budou výsledky zarovnány s cíli strategie.

Než začnete vytvářet metriky učení, definujte malý počet strategických metrik, které mají vliv na inovace. Obecně platí, že tyto strategické metriky se budou sjednotit do jedné nebo více následujících oblastí výsledků: [flexibilita firmy](../../strategy/business-outcomes/agility-outcomes.md), [zapojení zákazníků](../../strategy/business-outcomes/engagement-outcomes.md), [dosah zákazníků](../../strategy/business-outcomes/reach-outcomes.md), [finanční dopad](../../strategy/business-outcomes/fiscal-outcomes.md)nebo v případě provozní inovace: [řešení Výkon](../../strategy/business-outcomes/fiscal-outcomes.md).

Zdokumentujte si dohodnuté metriky a sledujte dopad často. Ale neočekáváme, že výsledky v žádné z těchto metrik se objeví pro několik iterací. V tématu [závazek na iteraci](./index.md#commitment-to-iteration) zarovnejte očekávání.

Vedle motivů a metriky obchodních výsledků se zbývající část tohoto článku zaměřuje na metriky učení, které jsou navržené tak, aby se s nimi mohli pracovat transparentním zjišťováním a s cílem zaměřit se na zákazníky. V tématu [závazek k transparentnosti](./index.md#commitment-to-transparency) zarovnává očekávání.

## <a name="learning-metrics"></a>Metriky učení

Pokud se zákazníkům sdílí první verze jakéhokoli minimálního životaschopného produktu (MVP), přednostně na konci první iterace vývoje nebude mít žádný dopad na strategické metriky. Několik iterací později může být tým stále působit potíže ke změně chování, které je dostatečné pro materiály, které mají vliv na strategické metriky. Během výukových procesů, jako jsou cykly sestavení-měření – učení, je doporučeno, aby tým přijal metriky učení. Tyto metriky je možné snadněji sledovat a využít v příležitostech k učení.

### <a name="customer-flow-and-learning-metrics"></a>Metriky toku a kurzu zákazníků

Pokud řešení MVP ověřuje hypotézu zaměřenou na zákazníka, řešení bude na určitou změnu řídit chování zákazníka. Toto chování v různých zákaznických kohortyech vyhodnotí obchodní výsledky. Naštěstí měnící se chování zákazníka je často proces s více kroky. Každý krok nabízí možnost měřit dopad, aby se tým přijetí mohl dozvědět a vytvořit lepší řešení.

Naučíte se, jak se mění chování zákazníka, pomocí mapování požadovaného toku vytvořeného řešením MVP.

![Tok zákazníka, který se používá k určení metrik učení](../../_images/innovate/customer-flow-learning-metrics.png)

Ve většině případů bude mít tok zákazníka snadno definovaný počáteční bod a ne více než dva koncové body. Mezi počátečním a koncovým bodem je celá řada výukových metrik, které se mají použít jako míry ve smyčce zpětné vazby:

1. **Počáteční bod – počáteční aktivační událost:** Výchozím bodem je scénář, který aktivuje potřebu tohoto řešení. Když je řešení sestavené pomocí zákaznického soucitu, měl by počáteční Trigger inspirovat zákazníka, aby si vyzkoušel řešení MVP.
2. **Splnění zákaznických potřeb:** Předpoklad se ověří, když je potřeba splnit zákazníka pomocí řešení.
3. **Postup řešení:** Každý krok nutný k přesunutí zákazníka z počáteční triggeru do úspěšného výsledku je krok řešení. Každý krok vytvoří výukovou metriku na základě rozhodnutí zákazníků o přechodu k dalšímu kroku.
4. **Dosažené individuální přijetí:** Při příštím výskytu triggeru se zákazník vrátí do řešení, aby se znovu vyvolala nutnost obdržet jednotlivé přijetí.
5. **Indikátor výsledku podniku:** Když se zákazník chová způsobem, který pozitivně přispívá k definovanému obchodnímu výsledku, je pozorován indikátor obchodní výsledek.
6. **Skutečná inovace:** V případě, že se v požadovaném měřítku vyskytuje "indikátory obchodních výsledků" a "individuální přijetí", nastala skutečná inovace.

Každý krok toku zákazníka generuje metriky učení. Po každé iteraci (nebo vydané verzi) se testuje nová verze hypotézy. Ve stejnou dobu jsou pro řešení testovány, aby odrážely úpravy v hypotéze. Když zákazníci dostanou předepsané cesty v jakémkoli kroku, zaznamená se kladná metrika. Když se zákazníci odchylují od předepsané cesty k uspokojení jejich potřeby, zaznamená se záporná metrika.

Tyto čítače zarovnání a odchylky vytvářejí metriky učení. Každý z nich by měl být zaznamenán a sledován jako tým pro přijetí cloudu, který vede k realizaci obchodních výsledků a skutečným inovacím. V dalším článku se [naučíte](./learn.md) , jak využít tyto metriky k seznámení a sestavování lepších řešení.

### <a name="grouping-and-observing-customer-partners"></a>Seskupení a sledování zákaznických partnerů

První měření pro definování metrik učení je definice partnera pro zákazníky. Každý zákazník, který se účastní inovačních cyklů, je stejný jako partner zákazníka. Aby bylo možné přesně měřit chování, je důležité definovat partnery zákazníka v kohorta modelu. V tomto modelu se zákazníci seskupí, aby lépe pochopili, jak reagují na změny v rámci MVP. Partneři zákazníka se často seskupují na základě datových bodů, jako jsou tyto:

- **Experiment nebo skupina s fokusem:** Seskupení založené na zákaznících v konkrétní experimentu k testování změn v průběhu času.
- **Segment:** Seskupení zákazníků podle velikosti společnosti
- **Svislá:** Seskupení zákazníků podle vertikálního odvětví, které představují.
- **Jednotlivé demografické údaje:** Seskupení na základě osobních demografických údajů, jako je věk nebo fyzické umístění.

Tento typ seskupení umožňuje ověřování metrik výukových kurzů napříč různými částmi zákazníků, kteří se na vás při inovacích rozhodnou o partnerovi. Všechny následné metriky by se měly dodržovat na základě definovatelné skupiny zákazníků.

## <a name="next-steps"></a>Další kroky

Jak se shromažďují metriky výukového programu, tým se může začít [učit se se zákazníky](./learn.md).

> [!div class="nextstepaction"]
> [Seznamte se se zákazníky](./learn.md)

Některé z konceptů v tomto článku se sestavují na témata, která se poprvé popisují v [rámci štíhlého spuštění](http://theleanstartup.com/book), zapsaná službou Eric obnovení aplikace.
