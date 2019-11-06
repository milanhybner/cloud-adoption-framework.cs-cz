---
title: Úvod do provozního modelu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznámení s provozním modelem architektury přechodu na cloud
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: operating-model
ms.openlocfilehash: d9e26d82dd0332c338567bf962094a39f2ef84b4
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564523"
---
# <a name="establish-an-operating-model-for-the-cloud"></a>Vytvoření provozního modelu pro cloud

Přechod na cloud je iterativní činnost zaměřená na operace, které v cloudu provádíte. Cloudová strategie tvoří rámec digitální transformace, která slouží jako vodítko pro obchodní programy, jak různé týmy zpracovávají projekty přechodu. K zajištění úspěchu každého z těchto důležitých prvků napomáhá plánování a připravenost. Všechny kroky přechodu na cloud odpovídají skutečným projektům se spravovatelnými cíli, časovými osami a rozpočty.

Tyto snahy o přechod se relativně snadno sledují a měří, a to i v případě, že zahrnují více projektovaných iterací a vydaných verzí. Každá fáze životního cyklu přechodu je důležitá. V každé fázi se můžou vyskytnout překážky obchodního, kulturního nebo technologického charakteru. Každá fáze ale do značné míry závisí na základním provozním modelu.

**Pokud přechod popisuje to, co děláte, provozní model definuje na základní úrovni, kdo a jak, aby byl přechod možný.**

Satya Nadella říká: **„Kultura si dá strategii k snídani.“** Provozní model je ztělesněním kultury IT zachyceným v mnoha měřitelných procesech. Pokud je základem cloudu silný provozní model, kultura aktivuje strategii, a tím se urychlí přechod a realizace obchodních hodnot. Pokud je naopak přechod úspěšný, ale není k dispozici provozní model, může být návrat působivý, ovšem jeho trvání je velmi krátké. Pro dlouhodobý úspěch je důležité, aby se přechod a provozní modely rozvíjely souběžně.

## <a name="establish-your-operating-model"></a>Vytvoření vašeho provozního modelu

Aktuální provozní modely je možné škálovat, aby podporovaly přechod na cloud. Moderní provozní model vám pomůže odebrat netechnické problémy blokující přechod na cloud.

Tato část architektury přechod na cloud poskytuje praktický provozní model, který pomáhá při netechnickém rozhodování. Tento provozní model se skládá ze tří metodologií, které pomůžou při vytváření vlastního provozního modelu cloudu:

- [Řízení:](../govern/index.md) Zajistěte konzistenci v rámci úsilí o přechod. Srovnejte požadavky na zásady správného řízení a dodržování předpisů, abyste udržovali dobře spravované prostředí v rámci cloudu.
- [Správa:](../manage/index.md) Srovnejte probíhající procesy provozní správy technologií kvůli maximalizaci dosažené hodnoty a minimalizaci přerušení služeb.
- [Uspořádání:](../organize/index.md) Jak zraje provozní model, zraje i organizace různých týmů a možností podporujících provozní model.

## <a name="align-operating-models"></a>Srovnání provozních modelů

Cloud a digitální ekonomika odhalily potřebu několika provozních modelů. Tato potřeba někdy vychází z nutnosti podporovat několik veřejných cloudů. Častěji je ale tato potřeba důsledkem přechodu z místní verze na cloudovou. V obou scénářích je třeba srovnat provozní modely z hlediska maximálního výkonu a minimální redundance.

Analytici predikují přechod na více cloudů s velkými objemy. Mnozí zákazníci směřují k této predikci. Zákazníci ale bohužel informují o značných výzvách v souvislosti s provozem více cloudů. Duplicitní prostředky, procesy, dovednosti a technologie vedou ke zvyšování nákladů, a ne k úsporám slibovaných predikcemi týkajícími se cloudů. Zákazníkům se doporučuje přejít na specializovaný provozní model, aby tento trend zvrátili. Při srovnávání provozních modelů by měl vždy existovat jeden **obecný provozní model**. Další **specializované provozní modely** by se využily pro specifické scénáře pro podporu odchylek od standardního modelu.

- **Obecný provozní model:** Obecný provozní model je srovnán s jednou veřejnou nebo privátní cloudovou platformou. Provoz této platformy definuje provozní standardy, zásady a procesy. Tento provozní model by měl být primárním prostředkem tvořícím základ dopředné cloudové strategie. V tomto modelu je cílem využít primárního poskytovatele cloudu pro hromadný přechod na cloud.

- **Specializovaný provozní model:** Specifické obchodní výsledky mohou lépe korespondovat s alternativním poskytovatelem cloudu. V případě existence důležitého obchodního případu jsou pro nového poskytovatele cloudu použity standardy, zásady a procesy z obecného provozního modelu, následně jsou ale upraveny, aby korespondovaly se specializovaným případem použití.

Pokud je zvolenou primární platformou Azure, najdete cenné informace pro vytvoření provozního modelu v příručkách a osvědčených postupech v částech provozního modelu uvedených výše. Tato struktura ale zohledňuje i skutečnost, že ne všichni naši čtenáři se rozhodli používat Azure jako primární platformu. Abychom vyšli vstříc této širší cílové skupině, je možné aplikovat teoretický obsah každé části na provozní modely veřejných či privátních cloudů s podobnými výsledky.

## <a name="next-steps"></a>Další kroky

Zásady správného řízení jsou obvyklým prvním krokem k vytvoření provozního modelu pro cloud.

> [!div class="nextstepaction"]
> [Další informace o zásadách správného řízení cloudu](../govern/index.md)
