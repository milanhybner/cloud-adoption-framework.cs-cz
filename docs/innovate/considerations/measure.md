---
title: Měření dopadu zákazníků
description: Definujte požadovaný tok zákazníka a vytvořte metriky učení, které měří chování zákazníků a jejich přijetí.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: fe1bed4da302041998ec09efd2224be3d94fe3aa
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356721"
---
# <a name="measure-for-customer-impact"></a>Měření dopadu na zákazníky

Existuje několik způsobů, jak změřit dopad na zákazníky. Tento článek vám pomůže definovat metriky pro ověření hypotézy, které vyplývají z úsilí při [sestavování pomocí zákaznických soucit](./build.md).

## <a name="strategic-metrics"></a>Strategické metriky

Během [fáze strategie](../../strategy/index.md) životního cyklu přijetí do cloudu prověříme [podněty](../../strategy/motivations.md) a [obchodní výsledky](../../strategy/business-outcomes/index.md). Tyto postupy poskytují sadu metrik, podle kterých se má testovat dopad na zákazníky. Po úspěšném dokončení inovace se můžete podívat na výsledky, které jsou zarovnané k vašim strategickým cílům.

Před vytvořením metriky učení definujte malý počet strategických metrik, které mají mít vliv na inovace. Obecně se tyto strategické metriky rovnají s jednou nebo více z následujících oblastí výsledků: [flexibilita firmy](../../strategy/business-outcomes/agility-outcomes.md), [zapojení zákazníků](../../strategy/business-outcomes/engagement-outcomes.md), [dosah zákazníků](../../strategy/business-outcomes/reach-outcomes.md), [finanční dopad](../../strategy/business-outcomes/fiscal-outcomes.md)nebo v případě provozní inovace: [výkon řešení](../../strategy/business-outcomes/fiscal-outcomes.md).

Zdokumentujte dohodnuté metriky a sledujte jejich dopad často. Ale neočekáváme, že výsledky v žádné z těchto metrik se objeví pro několik iterací. Další informace o nastavení a zarovnání očekávání v rámci zúčastněných stran naleznete v tématu [závazek na iteraci](./index.md#commitment-to-iteration).

V důsledku motivace a metriky obchodních výsledků se zbývající část tohoto článku zaměřuje na metriky učení, které jsou navržené pro zajištění transparentního zjišťování a iterací zaměřených na zákazníky. Další informace o těchto aspektech najdete v tématu [závazek k transparentnosti](./index.md#commitment-to-transparency).

## <a name="learning-metrics"></a>Metriky učení

Pokud se zákazníkům sdílí první verze jakéhokoli minimálního životaschopného produktu (MVP), přednostně na konci první iterace vývoje nebude mít žádný dopad na strategické metriky. V pozdějších iteracích může být tým stále působit potíže, aby bylo možné změnit chování, které je dostatečně důležité pro materiál a ovlivnit strategické metriky. Během výukových procesů, jako jsou cykly sestavení-měření – učení, doporučujeme týmu, aby přijal metriky učení. Tyto metriky sledují a učí příležitosti.

### <a name="customer-flow-and-learning-metrics"></a>Metriky toku a kurzu zákazníků

Pokud řešení MVP ověřuje hypotézu zaměřenou na zákazníka, řešení bude na určitou změnu řídit chování zákazníka. Tyto změny chování v rámci zákaznických kohorty by měly zlepšit výsledky podnikání. Mějte na paměti, že změna chování zákazníka je obvykle proces s více kroky. Vzhledem k tomu, že každý krok poskytuje příležitost k měření dopadu, tým přijetí může průběžně učit a sestavovat lepší řešení.

Naučíte se, jak se projeví změny v chování zákazníků, pomocí mapování toku, který doufáme, že se vám v řešení MVP dozvíte.

![Tok zákazníka, který se používá k určení metrik učení](../../_images/innovate/customer-flow-learning-metrics.png)

Ve většině případů bude mít tok zákazníka snadno definovaný počáteční bod a ne více než dva koncové body. Mezi počátečním a koncovým bodem je celá řada výukových metrik, které se mají použít jako míry ve smyčce zpětné vazby:

1. **Počáteční bod – počáteční Trigger:** Výchozím bodem je scénář, který aktivuje potřebu tohoto řešení. Když je řešení sestavené pomocí zákaznického soucitu, měl by počáteční Trigger inspirovat zákazníka, aby si vyzkoušel řešení MVP.
2. **Splnění zákaznických potřeb:** Předpoklad se ověří, když je potřeba splnit zákazníka pomocí řešení.
3. **Postup řešení:** Tento pojem odkazuje na kroky, které jsou potřeba k přesunutí zákazníka z počáteční triggeru do úspěšného výsledku. Každý krok vytvoří výukovou metriku na základě rozhodnutí zákazníka o přechodu k dalšímu kroku.
4. **Dosažené individuální přijetí:** Při příštím výskytu triggeru se zákazník vrátí do řešení, aby získal jejich potřebnou potřebu, bylo dosaženo individuálního přijetí.
5. **Indikátor výsledku podniku:** Když se zákazník chová způsobem, který přispívá k definovanému obchodnímu výsledku, je pozorován indikátor obchodní výsledek.
6. **Skutečná inovace:** Když se *indikátory obchodních výsledků* a *individuální přijetí* vyskytují v požadovaném měřítku, provedete skutečné inovace.

Každý krok toku zákazníka generuje metriky učení. Po každé iteraci (nebo vydané verzi) se testuje nová verze hypotézy. Ve stejnou dobu jsou pro řešení testovány, aby odrážely úpravy v hypotéze. Když zákazníci dostanou předepsané cesty v jakémkoli kroku, zaznamená se kladná metrika. Když se zákazníci odchylují od předepsané cesty, zaznamená se záporná metrika.

Tyto čítače zarovnání a odchylky vytvářejí metriky učení. Každý z nich by měl být zaznamenán a sledován jako tým pro přijetí cloudu, který je zaměřený na obchodní výsledky a pravdivé inovace. V [informacích o zákaznících](./learn.md)probereme způsoby, jak tyto metriky použít pro seznámení a vytváření lepších řešení.

### <a name="grouping-and-observing-customer-partners"></a>Seskupení a sledování zákaznických partnerů

První měření v části Definování metrik učení je definice zákaznického partnera. Všichni zákazníci, kteří se účastní inovačních cyklů, jsou jako partneři zákazníka. Pro přesné měření chování byste měli použít model kohorta k definování zákaznických partnerů. V tomto modelu se zákazníci seskupí za účelem zostření vaší reakce na změny v rámci MVP. Tyto skupiny typicky připomínají následující:

- **Experiment nebo skupina s fokusem:** Seskupení zákazníků na základě jejich účasti v konkrétním experimentu navrženém k testování změn v průběhu času.
- **Segment:** Seskupení zákazníků podle velikosti společnosti
- **Svislá:** Seskupení zákazníků podle *vertikálního odvětví* , které představují.
- **Jednotlivé demografické údaje:** Seskupení na základě osobních demografických údajů, jako je věk a fyzické umístění.

Tyto typy seskupení vám pomůžou ověřit metriky učení napříč různými částmi těchto zákazníků, kteří se na vás během vaší inovace rozhodnou o partnerovi. Všechny následné metriky by měly být odvozené od seskupení zákazníka.

## <a name="next-steps"></a>Další kroky

Jak se shromažďují metriky učení, tým se může začít [učit se zákazníky](./learn.md).

> [!div class="nextstepaction"]
> [Seznamte se se zákazníky](./learn.md)

<!-- cSpell:ignore Ries -->

Některé z konceptů v tomto článku se sestavují na témata, která se poprvé popisují v [rámci štíhlého spuštění](http://theleanstartup.com/book), zapsaná službou Eric obnovení aplikace.
