---
title: Optimalizace migrovaných úloh
description: Optimalizace migrovaných úloh
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 87235584bc9da0f1a9e5124408b587eec864af48
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801881"
---
# <a name="optimize-migrated-workloads"></a>Optimalizace migrovaných úloh

Úloha a její podpůrné prostředky se po dokončení migrace do cloudu musí připravit. Teprve potom je možné převést je do produkčního prostředí. V tomto procesu aktivity připraví úlohu, nastaví velikost závislých prostředků a připraví firmu na okamžik, kdy migrované cloudové úlohy přejdou do fáze produkčního využití.

Cílem optimalizace je připravit migrovanou úlohu k převedení do fáze produkčního využití.

## <a name="definition-of-done"></a>Definice *dokončení*

Proces optimalizace je hotový ve chvíli, kdy úloha je správně nakonfigurovaná, má správnou velikost a využívá se v produkčním prostředí.

## <a name="accountability-during-optimization"></a>Odpovědnost během optimalizace

Za celý proces optimalizace odpovídá tým přechodu na cloud. Za aktivity v rámci tohoto procesu by ale také měli odpovídat členové týmu cloudové strategie, týmu cloudového provozu a týmu zásad správného řízení v cloudu.

## <a name="responsibilities-during-optimization"></a>Povinnosti během optimalizace

Kromě odpovědnosti na nejvyšší úrovni existují akce, za které musí nést přímou odpovědnost určitý jednotlivec nebo skupina. Následuje několik aktivit, které vyžadují přiřazení k odpovědné straně:

- **Obchodní testování:** Vyřešte případné problémy s kompatibilitou, které brání dokončení migrace úlohy do cloudu.
  - Do testování migrované úlohy by se měli v rámci firmy významně zapojit zkušení uživatelé. V závislosti na stupni požadované optimalizace se může vyžadovat několik testovacích cyklů.
- **Plán obchodních změn:** Vývoj plánu pro přijetí ze strany uživatelů, změny obchodních procesů a úpravy klíčových ukazatelů výkonu nebo metrik učení v důsledku migrace.
- **Srovnávací testy a optimalizace:** Studie obchodního testování a automatizovaného testování s cílem porovnat výkon. Tým přechodu na cloud na základě využití zpřesní velikost nasazených prostředků s cílem vyvážit náklady a výkon na jedné straně a očekávané produkční požadavky na straně druhé.
- **Připravenost pro produkční prostředí:** Připravte úlohu a prostředí tak, aby se zajistila podpora průběžného produkčního využití úlohy.
- **Zvýšení úrovně:** Na migrovanou a optimalizovanou úlohu přesměrujte produkční provoz. Tato aktivita představuje dokončení cyklu vydání.

Kromě základních aktivit existuje také několik paralelních aktivit, které vyžadují specifická přiřazení a realizační plány:

- **Vyřazení z provozu:** Obecně platí, že úspory nákladů v souvislosti s migrací se dají realizovat, když se předchozí produkční prostředky vyřadí z provozu a vhodným způsobem zlikvidují.
- **Retrospektiva:** Každé vydání vytváří příležitost pro hlubší poučení vzdělávání a změnu způsobu myšlení se zaměřením na růst. Po dokončení každého cyklu vydání by tým přechodu na cloud měl vyhodnotit procesy využité během migrace a identifikovat možná zlepšení.

## <a name="next-steps"></a>Další kroky

Když máte obecný přehled o procesu optimalizace, jste připraveni zahájit tento proces [vytvořením plánu obchodních změn pro kandidátskou úlohu](./business-change-plan.md).

> [!div class="nextstepaction"]
> [Plán obchodních změn](./business-change-plan.md)
