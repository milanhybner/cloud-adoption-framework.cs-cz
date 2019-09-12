---
title: Navázat iterace a plány vydaných verzí
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Navázat iterace a plány vydaných verzí
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 0dbef36d3909f11c1616d2e44c63227959c4ff56
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833775"
---
# <a name="establish-iterations-and-release-plans"></a>Navázat iterace a plány vydaných verzí

Agilní a další iterační metodologie jsou postaveny na konceptech iterací a vydání. Tento článek popisuje přiřazení iterací a vydání během plánování. Tato přiřazení umožňují snazší konverzaci mezi členy týmu cloudové strategie. Přiřazení také zarovnají technické úkoly způsobem, který může tým pro přijetí cloudu spravovat během implementace.

## <a name="establish-iterations"></a>Navázat iterace

V iterativním přístupu k technické implementaci můžete plánovat technické úsilí v rámci časových intervalů pro opakované použití. Iterace mají za týden časové bloky z jednoho týdne do šesti týdnů. Konsensu navrhne, aby dva týdny byly průměrnou dobou trvání iterace většiny týmů pro přijetí cloudu. Ale volba doby trvání iterace závisí na typu technického úsilí, administrativní režii a předvolbách týmu.

Pokud chcete začít s započetím úsilí na časovou osu, doporučujeme, abyste definovali sadu iterací, které budou posledních 6 až 12 měsíců.

## <a name="understand-velocity"></a>Princip rychlosti

Zarovnání úsilí k iteracím a vydáním vyžaduje porozumění rychlosti. Rychlost je množství práce, která může být dokončena v určité iteraci. Při prvotním plánování je rychlost odhadovaná. Po několika iteracích se rychlost stávají vysoce hodnotným indikátorem závazků, které tým může bez obav dělat.

Rychlost měření můžete měřit v abstraktních výrazech, jako jsou body scénáře. Můžete ji také změřit ve více jednotkách jako hodiny. Pro většinu iterativních rozhraní doporučujeme použít abstraktní měření, abyste se vyhnuli problémům v přesnosti a vnímání. Příklady v tomto článku znázorňují rychlost v hodinách na Sprint. Tato reprezentace usnadňuje pochopení tématu.

**Příklad:** Tým pro přijetí cloudu s pěti osobami se zavázal do dvou týdnů sprintů. Vzhledem k aktuálním závazkům, jako jsou schůzky a podpora jiných procesů, může každý člen týmu konzistentně přispět 20 hodin týdně na úsilí o přijetí. Pro tento tým je počáteční odhad rychlosti 100 hodin na Sprint.

## <a name="iteration-planning"></a>Plánování iterace

Zpočátku můžete naplánovat iterace tím, že vyhodnocujete technické úkoly na základě prioritních nevyřízených položek. Týmy pro přijetí cloudu odhadnou úsilí potřebné k dokončení různých úkolů. Tyto úlohy jsou následně přiřazeny k první dostupné iteraci.

Během plánování iterací týmy pro přijetí v cloudu ověřují a upřesňují odhady. To tak, aby se všechny dostupné rychlosti nerovnaly konkrétním úlohám. Tento proces pokračuje pro každou úlohu s upřednostněním, dokud se všechna snaha nebude zarovnávat s prognózou iterací.

V tomto procesu tým ověřuje úkoly přiřazené k dalšímu sprintu. Tým aktualizuje své odhady na základě konverzace týmu o jednotlivých úkolech. Tým potom přidá každou odhadovanou úlohu do dalšího sprintu, dokud se nesplní dostupná rychlost. Nakonec tým odhadne další úkoly a přidá je do další iterace. Tým provede tyto kroky, dokud nedojde k vyčerpání rychlosti této iterace.

Předchozí proces pokračuje, dokud nebudou všechny úkoly přiřazeny k iteraci.

**Příklad:** Vytvořme si předchozí příklad. Předpokládejme, že každá migrace zatížení vyžaduje 40 úloh. Také předpokládá, že každý úkol bude mít průměrnou hodinu. Kombinovaný odhad je přibližně 40 hodin na migraci zatížení. Pokud tyto odhady zůstávají v souladu se všemi 10 z úloh s prioritou, budou tyto úlohy trvat 400 hodin.

Rychlost definovaná v předchozím příkladu naznačuje, že migrace prvních 10 úloh bude trvat čtyři iterace, což je dva měsíce od kalendářního času. První iterace se skládá z 100 úloh, které vedou k migraci dvou úloh. V další iteraci bude podobná kolekce 100 úloh výsledkem migrace tří úloh.

> [!WARNING]
> Předchozí počty úkolů a odhadů se používají výhradně jako příklad. Technické úkoly jsou zřídka nekonzistentní. Tento příklad by se neměl zobrazovat jako odraz doby potřebné k migraci úlohy.

## <a name="release-planning"></a>Plánování vydání

V rámci přijetí do cloudu je vydaná verze definovaná jako kolekce dodávek, které tvoří dost obchodních hodnot, aby bylo možné snížit riziko narušení podnikových procesů.

Při uvolnění změn souvisejících s úlohou do produkčního prostředí se vytvoří nějaké změny v obchodních procesech. V ideálním případě jsou tyto změny bezproblémové a firmy se dohlíží na hodnotu změn bez jakýchkoli podstatných výpadků provozu. Riziko narušení chodu společnosti se ale vyskytuje bez jakýchkoli změn a nemělo by se přitom považovat za lehce.

Aby se změna ujistila podle potenciální návratnosti, měl by se tým cloudové strategie účastnit plánování vydávání verzí. Po zarovnání úkolů na sprinty může tým určit hrubou časovou osu, kdy bude každá úloha připravena na produkční verzi. Tým cloudové strategie si vyhodnotí časování každé vydané verze. Tým pak identifikuje bod inflexe mezi rizikovou a obchodní hodnotou.

**Příklad:** Pokračujeme v předchozím příkladu, tým cloudové strategie zkontroloval plán iterace. Kontrola identifikovala dva body vydání. V průběhu druhé iterace bude celkem pět úloh připraveno k migraci. Tyto pět úloh budou poskytovat významnou obchodní hodnotu a aktivují se první vydání. Další vydání bude následovat po dvou iteracích později, až budou další pět úloh připravené k vydání.

## <a name="assign-iteration-paths-and-tags"></a>Přiřazení cest a značek iterace

Pro zákazníky, kteří spravují plány přijetí cloudu v Azure DevOps, se předchozí procesy projeví přiřazením cesty iterace ke každému úkolu a uživatelskému scénáři. Doporučujeme také označit jednotlivé úlohy pomocí konkrétní verze. Označení a přiřazení kanálu pro automatické naplňování sestav Timeline.

## <a name="next-steps"></a>Další kroky

[Odhadnout časové osy](./timelines.md) pro správné sdělování očekávání.

> [!div class="nextstepaction"]
> [Odhadnout časové osy](./timelines.md)
