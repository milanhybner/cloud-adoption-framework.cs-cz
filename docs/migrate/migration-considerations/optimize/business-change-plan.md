---
title: Vývoj plánu pro změnu podniku
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak vám plán pro obchodní změnu může pomáhat s implementací širšího plánu přijetí uživateli.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: fd8db03a28c5372ad5ca796607a079ffdcbe4f92
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355283"
---
# <a name="business-change-plan"></a>Plán obchodních změn

Tradičně IT dohlíží na vydání nových sad funkcí. Při významné transformaci, jako je migrace datového centra nebo migrace do cloudu, by bylo možné použít podobný vzor jako přijetí vedením IT. Tradiční přístup ale může přijít o příležitosti realizace další obchodní hodnoty. Z tohoto důvodu je před povýšením migrované sady funkcí do produkčního prostředí navržená implementace širšího přístupu k přijetí uživateli. Tento článek popisuje způsoby, při kterých plán obchodních změn přispívá ke standardnímu plánu přijetí uživateli.

## <a name="traditional-user-adoption-approach"></a>Tradiční přístup k přijetí uživateli

Plány přijetí uživateli se zaměřují na to, jak uživatelé přijímají novou technologii nebo se dané technologií přizpůsobí. Tento přístup je pro seznámení uživatelů s novými nástroji časem osvědčený. V typickém plánu přijetí uživateli se IT zaměřuje na instalaci, konfiguraci, údržbu a školení spojené s technickými změnami, které jsou uvedeny do podnikového prostředí.

I když se můžou přístupy lišit, jsou ve většině plánů přijetí uživateli přítomné obecné motivy. Tyto motivy jsou obvykle založené na přístupu pomocí řízení rizik a usnadnění, který odpovídá postupnému vylepšování. Easonova matice znázorněná na obrázku níže představuje hnací mechanismy za těmito motivy v rámci spektra typů přijetí.

![Easonova matice týkající se aspektů přijetí uživateli](../../../_images/migrate/eason-matrix.jpg)

*Easonova matice týkající se typů přijetí uživateli.*

Tyto motivy často vycházejí z předpokladu, že zavedení nových řešení pro uživatele by se mělo zaměřit hlavně na řízení rizik a usnadnění změny. Navíc se IT zaměřuje hlavně na riziko změny technologie a usnadnění této změny.

## <a name="create-business-change-plans"></a>Vytvoření plánů pro změnu podniku

Plán obchodních změn se dívá dál za technickou změnu a předpokládá, že každá vydaná verze v rámci procesu migrace vyvolává určitou úroveň změny obchodních procesů. Dívá se před a za technické změny. Následující otázky pomůžou účastníkům podívat se na přijetí uživateli z perspektivy obchodní změny, aby se maximalizoval obchodní dopad:

**Otázky proti směru toku.** Otázky proti směru toku zkoumají dopady nebo změny, které nastanou před přijetím uživateli:

- Byl očekávaný [obchodní výsledek](../../../strategy/business-outcomes/index.md) kvantifikován?
- Mapuje se obchodní dopad na definované [metriky učení](../../../strategy/learning-metrics.md)?
- Které obchodní procesy a týmy využívají výhody tohoto technického řešení?
- Kdo v podniku může nejlépe poskytnout zkušené uživatele pro testování a zpětnou vazbu?
- Byli ovlivnění vedoucí pracovníci zapojeni do stanovení priorit a plánování migrace?
- Existují nějaké kritické události nebo data pro firmu, které by mohly být touto změnou ovlivněné?
- Maximalizuje plán obchodních změn dopad, ale zároveň minimalizuje narušení chodu firmy?
- Očekává se výpadek? Bylo období výpadku sděleno koncovým uživatelům?

**Otázky po směru toku.** Po dokončení přijetí může obchodní změna začít. To je bohužel místo, kde mnoho plánů přijetí uživateli končí. Otázky po směru toku pomáhají týmu cloudové strategie zachovat si zaměření na transformaci po dokončení technické změny:

- Reagují obchodní uživatelé na změny dobře?
- Byl s přijetím technické změny udržen předpokládaný výkon?
- Mění se obchodní procesy nebo prostředí pro zákazníky předpokládanými způsoby?
- Jsou k realizaci metrik učení nutné další změny?
- Odpovídají změny cílovým obchodním výsledkům? Pokud ne, proč?
- Jsou pro příspěvek k obchodním výsledkům nutné další změny?
- Byly v důsledku této změny pozorovány negativní účinky?

Plán obchodních změn se mezi společnostmi liší. Cílem těchto otázek je pomáhat lépe integrovat podnikání do změny spojené s každou vydanou verzí. Když se díváte na jednotlivé vydané verze ne jako na technologickou změnu, ale místo toho jako na plán obchodních změn, můžou být obchodní výsledky lépe dosažitelné.

## <a name="next-steps"></a>Další kroky

Po popsání a naplánování obchodní změny je možné začít s [obchodním testováním](./business-test.md).

> [!div class="nextstepaction"]
> [Pokyny pro obchodní testování (UAT) během migrace](./business-test.md)

## <a name="references"></a>Odkazy

<!-- cSpell:ignore Eason -->

- Eason, K. (1988) _informační technologie a organizační změna_, New York: Taylor a Francis.
