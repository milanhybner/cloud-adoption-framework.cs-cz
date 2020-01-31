---
title: Provedení migrace
description: Seznamte se s přehledem článků popisujících různé aktivity, které mohou být součástí migrace úloh v Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 62100df7a32ca904454e0df2d7be8c1a860fd611
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802272"
---
# <a name="execute-a-migration"></a>Provedení migrace

Po vyhodnocení se úloha dá migrovat do cloudu. Tato série článků popisuje různé aktivity, které mohou být součástí migrace.

## <a name="objective"></a>Cíl

Cílem migrace je migrovat jednu úlohu do cloudu.

## <a name="definition-of-done"></a>Definice *dokončení*

Fáze migrace je dokončená, když je úloha připravená k testování v cloudu, a to včetně všech závislých prostředků, které jsou pro její fungování potřeba. Během procesu optimalizace se úloha připravuje pro produkční využití.

Tato definice *dokončení* se může lišit v závislosti na vašich procesech testování a vydávání. Další článek v této sérii se věnuje [rozhodování ohledně modelu zvýšení úrovně](./promotion-models.md) a pomůže vám pochopit, kdy je nejvhodnější přenést migrovanou úlohu do produkčního prostředí.

## <a name="accountability-during-migration"></a>Odpovědnost během migrace

Za celý proces migrace odpovídá tým přechodu na cloud. Členové týmu cloudové strategie však mají několik povinností, které jsou uvedené v následující části.

## <a name="responsibilities-during-migration"></a>Povinnosti během migrace

Kromě odpovědnosti na nejvyšší úrovni existují akce, za které musí nést přímou odpovědnost určitý jednotlivec nebo skupina. Následuje několik aktivit, které vyžadují přiřazení k odpovědné straně:

- **Nápravné akce:** Vyřešte případné problémy s kompatibilitou, které brání dokončení migrace úlohy do cloudu.
  - Jak je popsáno v článku s požadavky popisujícím [technickou složitost a správu změn](../prerequisites/technical-complexity.md), měli byste předem přijmout rozhodnutí, kterým určíte, jak má tato aktivita proběhnout. Zejména byste se měli rozhodnout, jestli nápravné akce provede tým přechodu na cloud během stejného sprintu jako vlastní migraci. Případně se můžete rozhodnout, aby se k dokončení nápravných akcí použil model vlny nebo továrny v oddělené iteraci. Pokud odpověď na tuto základní procesní otázku neznají všichni členové týmu, může být rozumné si znovu projít část věnovanou [požadavkům](../prerequisites/index.md).
- **Replikace:** Vytvořte kopii jednotlivých prostředků v cloudu a synchronizujte virtuální počítače, data a aplikace s prostředky v cloudu.
  - V závislosti na modelu zvýšení úrovně se mohou k dokončení této aktivity vyžadovat různé nástroje.
- **Staging:** Jakmile se dokončí replikace a ověření všech prostředků úlohy, dá se úloha převést do fáze obchodního testování a realizace plánu obchodních změn.

## <a name="next-steps"></a>Další kroky

Když máte obecný přehled o procesu migrace, jste připraveni [rozhodnout o modelu zvýšení úrovně](./promotion-models.md).

> [!div class="nextstepaction"]
> [Rozhodnutí o modelu zvýšení úrovně](./promotion-models.md)
