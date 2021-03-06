---
title: Metodologie zásad správného řízení pro Cloud
description: Využijte přírůstkový přístup ke správě na základě minimální životaschopného produktu (MVP) k podpoře podnikových zásad a rychlému přesunu do cloudového přijetí.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: f7ec10f54231e401799abb81d72efb3cc3657959
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430961"
---
# <a name="cloud-governance-methodology"></a>Metodologie zásad správného řízení pro Cloud

Přechod na cloud je cesta, ne cíl. A tuto cestu lemují zřetelné milníky a hmatatelné obchodní výhody. V okamžiku, kdy firma tuto cestu teprve nastupuje, se ale neví, jaký bude finální stav přechodu na cloud. Zásady správného řízení v cloudu vytvářejí ochranné mantinely, které firmu na této cestě bezpečně provázejí.

Rozhraní pro přijetí do cloudu poskytuje příručky pro zásady správného řízení, které popisují prostředí fiktivních společností, která jsou založená na zkušenostech reálných zákazníků. Každý průvodce provádí zákazníka všemi aspekty zásad správného řízení jejich přechodu na cloud.

## <a name="envision-an-end-state"></a>Vize koncového stavu

Cesta bez cíle je pouhé bloudění. Než začnete s prvním krokem, je důležité, abyste navázali přibližnou vizi koncového stavu. Následující infografika poskytuje referenční rámec koncového stavu. Není to výchozí bod, ale zobrazuje váš potenciální cíl.

![Infografika modelu zásad správného řízení architektury přechodu na cloud](../_images/operational-transformation-govern-highres.png)

Model zásad správného řízení architektury přechodu na cloud identifikuje nejdůležitější části této cesty. Každá oblast souvisí s jiným typem rizik, kterým firmy při využívání většího počtu cloudových služeb čelí. Průvodce zásadami správného řízení v rámci této architektury identifikuje nutné akce pro tým zásad správného řízení v cloudu. Jednotlivé principy modelu zásad správného řízení architektury přechodu na cloud jsou popsány podrobněji. Obecně mezi ně patří:

**Podnikové zásady:** Podnikové zásady jednotky zásad správného řízení cloudu Průvodce zásadami správného řízení se soustředí na konkrétní aspekty firemních zásad:

- **Obchodní rizika:** Identifikace a porozumění podnikovým rizikům.
- **Zásady a dodržování předpisů:** Převod rizik na příkazy zásad, které podporují požadavky na dodržování předpisů.
- **Procesy:** Zajištění dodržování uvedených zásad.

**Pět oborů řízení cloudu:** Tyto disciplíny podporují podnikové zásady. Každá z disciplín chrání firmu před potenciálními nástrahami:

- Cost Management
- Standardní hodnoty zabezpečení
- Konzistence prostředků
- Standardní hodnoty identit
- Zrychlení nasazení

Firemní zásady slouží jako včasný varovný systém pro detekci potenciálních problémů. Disciplíny pomáhají společnostem spravovat rizika a vytvářet ochranné mantinely.

## <a name="grow-to-the-end-state"></a>Růst až do koncového stavu

Vzhledem k tomu, že požadavky zásad správného řízení se budou v průběhu cesty přechodu na cloud měnit, vyžaduje to jiný přístup k zásadám správného řízení. Firmy *před provedením prvního kroku* už nemohou čekat, až malý tým nastaví ochranné mantinely a vytvoří plány pro každý úsek cesty. Obchodní výsledky se očekávají mnohem rychleji a bez problémů. Zásady správného řízení IT se také musí rychle přizpůsobovat a držet krok s obchodními požadavky, aby zůstaly relevantní i během přechodu na cloud a nedošlo ke vzniku „stínového IT“.

Přístup využívající **inkrementální zásady správného řízení** umožňuje všechny tyto vlastnosti zajistit. Inkrementální zásady správného řízení využívají malou sadu firemních zásad, procesů a nástrojů k vytvoření základu pro přechod a zásady správného řízení. Tento základ se označuje jako **MVP (Minimum Viable Product)** . MVP umožňuje týmu zásad správného řízení rychle začlenit zásady správného řízení do implementací v průběhu celého trvání přechodu na cloud. MVP je možné během procesu přechodu na cloud vytvořit kdykoli. Je ale dobrým zvykem, jak co nejdříve přijmout MVP.

Možnost rychle reagovat na měnící se rizika umožňuje týmu zásad správného řízení v cloudu pracovat novými způsoby. Členové týmu zásad správného řízení v cloudu se mohou jako průzkumníci zapojit do týmu cloudové strategie, zajistit si náskok před týmy přechodu na cloud, vytyčovat trasy a rychle vytvářet ochranné mantinely pro správu rizik souvisejících s plány přechodu. Tyto vrstvy zásady správného řízení za běhu se označují jako **iterace zásad správného řízení**. Při použití tohoto přístupu má vývoj strategie zásad správného řízení vždy o krok náskok před týmy přechodu na cloud.

Následující diagram ukazuje jednoduchou realizaci MVP zásad správného řízení a tři iterace zásad správného řízení. V průběhu jednotlivých iterací se definují další firemní zásady pro zmírnění nových rizik. Disciplína zrychlení nasazení potom tyto změny aplikuje napříč jednotlivými nasazeními.

![Příklad postupného vylepšování zásad správného řízení](../_images/govern/incremental-governance-example.png)

> [!NOTE]
> Zásady správného řízení nepředstavují náhradu klíčových funkcí, jako jsou zabezpečení, využití sítě, identity, finance, DevOps nebo provoz. Postupně bude docházet k interakcím se členy s různými funkcemi a k závislosti na nich. Tito členové by měli být do týmu zásad správného řízení v cloudu zahrnuti, aby se urychlilo rozhodování a zvýšila akceschopnost.

## <a name="next-steps"></a>Další kroky

Pomocí [nástroje test zásad správného řízení](https://cafbaseline.com) architektury cloudu pro kontrolu a poznáte cestu k transformaci ve vaší organizaci na šesti klíčových doménách, jak je definováno v rozhraní.

> [!div class="nextstepaction"]
> [Posouzení cesty transformace](./benchmark.md)
