---
title: 'Standardní zásady správného řízení podniku: Předčítání za strategii zásad správného řízení'
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak vytvořit případ použití pro zásady správného řízení během provozu standardní podnikové cloudové cesty.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3781bb50f8d2ad76efd606f8d6914582cee0754c
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434223"
---
# <a name="standard-enterprise-governance-guide-the-narrative-behind-the-governance-strategy"></a>Standardní příručka pro zásady správného řízení podniku: mluvený komentář za strategií zásad správného řízení

Následující komentáře popisují případ použití pro zásady správného řízení během cesty k [podnikovému přijetí ve standardní podnikové síti](./index.md). Před implementací cesty je důležité pochopit předpoklady a odůvodnění, které se projeví v tomto mluveném komentáři. Pak můžete strategii zásad správného řízení lépe sjednotit na cestu vaší organizace.

## <a name="back-story"></a>Příběh zpátky

Rada ředitelů zahájila rok s plány, aby oživit podnikání několika způsoby. Poskytují vedoucím ke zlepšení zkušeností zákazníků, aby získali podíl na trhu. Jsou také doručovány do nových produktů a služeb, které budou svou firmu namísťovat jako vedoucí vedoucí v oboru. Zahájily se také paralelní úsilí, aby se snížilo množství odpadů a snížilo zbytečné náklady. I když zastrašování, akce panelu a vedoucího ukazují, že se toto úsilí zaměřuje na co největší kapitál při budoucím růstu.

V minulosti se CIO společnosti z těchto strategických konverzací vyloučil. Vzhledem k tomu, že je budoucí vize vnitřně propojená s technickým růstem, má v tabulce místo, které vám pomůžou s těmito velkými plány. Nyní se očekává, že se doručí novému způsobu. Tým není připravený na tyto změny a je nejspíš bojovat s výukovou křivkou.

## <a name="business-characteristics"></a>Obchodní charakteristika

Společnost má následující obchodní profil:

- Všechny prodeje a operace se nacházejí v jedné zemi s nízkým procentem globálních zákazníků.
- Firma funguje jako jediná obchodní jednotka a rozpočet se zarovnává s funkcemi, včetně prodejů, marketingu, provozu a IT.
- Podniková zobrazení jsou většinou velká a nákladové středisko.

## <a name="current-state"></a>Aktuální stav

Tady je aktuální stav operací IT a cloudových operací společnosti:

- Pracuje se dvěma hostovanými prostředími infrastruktury. Jedno prostředí obsahuje produkční prostředky. Druhé prostředí obsahuje zotavení po havárii a některé prostředky pro vývoj a testování. Tato prostředí jsou hostována dvěma různými poskytovateli. Odkazuje na tato dvě datová centra jako prod. a v uvedeném pořadí.
- Vstoupili do cloudu migrací všech e-mailových účtů koncových uživatelů do sady Office 365. Tato migrace byla dokončena před šesti měsíci. Několik dalších prostředků IT bylo nasazeno do cloudu.
- Vývojové týmy pro aplikace pracují s kapacitou pro vývoj a testování, kde se dozvíte o možnostech nativního cloudu.
- Tým business intelligence (BI) experimentuje s velkými objemy dat v cloudu a získávání dat na nových platformách.
- Společnost má uvolněnou zásadu, která uvádí, že osobní zákaznická data a finanční data nejdou hostovat v cloudu, což omezuje kritické aplikace v aktuálních nasazeních.
- Investice do IT jsou řízeny hlavně pomocí kapitálových výdajů. Tyto investice jsou plánovány ročně. V posledních několika letech zahrnovaly investice více než základní požadavky na údržbu.

## <a name="future-state"></a>Budoucí stav

Následující změny se odhadují v následujících několika letech:

- CIO prohlíží zásady osobních údajů a finančních dat, aby bylo možné budoucí cíle stavu.
- Vývoj aplikací a týmy BI chtějí uvolnit cloudová řešení do provozu v příštích 24 měsících na základě vize pro zákaznickou zapojení a nové produkty.
- Tento rok IT tým dokončí vyřazení úloh zotavení po havárii datacentra DR pomocí migrace 2 000 virtuálních počítačů do cloudu. Očekává se, že se v následujících pěti letech vyprodukuje odhadované ceny za 25M USD.
    ![místní náklady a náklady na Azure, které demonstrují vrácení $25M USD za další pět let](../../../_images/govern/calculator-small-to-medium-enterprise.png)
- Společnost plánuje změnu způsobu jejich investic tím, že přemístí potvrzené kapitálové výdaje jako provozní náklady v rámci IT. Tato změna zajistí větší náklady a umožní jí zrychlit další plánované úsilí.

## <a name="next-steps"></a>Další kroky

Společnost vyvinula podnikové zásady pro vytvoření obrazce implementace zásad správného řízení. Podniková zásada se řídí mnoha technickými rozhodnutími.

> [!div class="nextstepaction"]
> [Kontrola počátečních podnikových zásad](./initial-corporate-policy.md)
