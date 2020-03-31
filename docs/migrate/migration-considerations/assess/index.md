---
title: Ověření předpokladů posouzení před zahájením migrace
description: Využijte architekturu přechodu na cloud pro Azure k seznámení s tím, jak ověřit předpoklady posouzení před zahájením migrace do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b9e39f4f0c86239c3c1d249fdb08dbce2c9f4daa
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429441"
---
# <a name="validate-assessment-assumptions-before-migration"></a>Ověření předpokladů posouzení před zahájením migrace

Řada z vašich stávajících úloh je ideálními kandidáty pro migraci do cloudu, ale ne každý prostředek je kompatibilní s cloudovými platformami a ne všem úlohám přinese hostování v cloudu výhody. Díky [plánování digitálních aktiv](../../../digital-estate/index.md) můžete vygenerovat celkový [backlog migrace](../prerequisites/technical-complexity.md#migration-backlog-aligning-business-priorities-and-timing) potenciálních úloh, které se mají migrovat. Toto plánování je však úlohou nejvyšší úrovně. Spoléhá na předpoklady týmu cloudové strategie a nezabývá se hlouběji technickými aspekty.

Z toho důvodu je důležité před migrací úlohy do cloudu posoudit jednotlivé prostředky přidružené k dané úloze z hlediska vhodnosti k migraci. Během tohoto posuzování by váš tým přechodu na cloud měl vyhodnotit technickou kompatibilitu, požadovanou architekturu, očekávaní z hlediska výkonu a velikosti a závislosti, aby se zajistila možnost efektivního nasazení migrovaných úloh do cloudu.

Proces *posouzení* je prvním ze čtyř inkrementálních aktivit, ke kterým dochází v rámci iterace. Jak je popsáno v článku s požadavky popisujícím [technickou složitost a správu změn](../prerequisites/technical-complexity.md), měli byste předem přijmout rozhodnutí, kterým určíte, jak má tato fáze proběhnout. Zejména byste se měli rozhodnout, jestli posouzení provede tým přechodu na cloud během stejného sprintu jako vlastní migraci. Případně se můžete rozhodnout, aby se k dokončení posouzení použil model vlny nebo továrny v oddělené iteraci. Pokud odpověď na tuto základní procesní otázku neznají všichni členové týmu, může být rozumné si znovu projít část [Požadavky](../prerequisites/index.md).

## <a name="objective"></a>Cíl

Posouzení kandidáta na migraci, vyhodnocení úlohy, souvisejících prostředků a závislostí před migrací

## <a name="definition-of-done"></a>Definice *dokončení*

Tento proces je dokončený, jakmile se o jednotlivých kandidátech na migraci zjistí následující:

- Je definovaná cesta z místního prostředí do cloudu, včetně zvoleného přístupu k propagaci produkčního prostředí.
- Dokončily se všechny požadované procesy schválení, změn, odhadu nákladů nebo ověřování, aby tým přechodu na cloud mohl provést migraci.

## <a name="accountability-during-assessment"></a>Odpovědnost během posuzování

Za celý proces posouzení odpovídá tým přechodu na cloud. Členové týmu cloudové strategie však mají několik povinností, které jsou uvedené v následující části.

## <a name="responsibilities-during-assessment"></a>Povinnosti během posuzování

Kromě odpovědnosti na nejvyšší úrovni existují akce, za které musí nést přímou odpovědnost určitý jednotlivec nebo skupina. Následuje několik aktivit, které vyžadují přiřazení k odpovědné straně:

- **Obchodní priorita:** Tým rozumí účelu migrace této úlohy, včetně zamýšlených dopadů na firmu.
  - Konečnou odpovědnost za tuto aktivitu by měl nést některý ze členů týmu cloudové strategie pod vedením týmu přechodu na cloud.
- **Sladění účastníků:** Tým sladí očekávání a priority s interními účastníky a identifikuje kritéria úspěchu migrace. Jak vypadá úspěch po migraci?
- **Zpřesněná racionalizace:** Vyhodnotí se počáteční předpoklady týkající se racionalizace. Měl se pro migraci této konkrétní úlohy použít jiný [racionalizační přístup](../../../digital-estate/rationalize.md)?
- **Rozhodnutí ohledně modernizace:** Měly se bez ohledu na rozhodnutí týkající se racionalizace, různé prostředky v rámci této úlohy modernizovat, aby se mohla využít řešení založená na PaaS?
- **Náklady:** Vytvořil se odhad nákladů na cílovou architekturu a upravil se podle něj celkový rozpočet.
- **Podpora migrace:** Tým se rozhodl, jak se provede technická část migrace, a přijal také rozhodnutí ohledně podpory partnerů nebo Microsoftu.
- **Vyhodnocení:** U úlohy se vyhodnotí kompatibilita a závislosti.
  - Tato aktivita by se měla přiřadit odborníkovi na danou problematiku, který zná architekturu a operace kandidátské úlohy.
- **Architektura:** Tým se shodl na konečném stavu architektury pro migrovanou úlohu.
- **Migrační nástroje:** V závislosti na modernizaci a přístupů k architektuře se k automatizaci migrace dá použít celá řada migračních nástrojů. Bude (v závislosti na navržené architektuře) tato migrace využívat nejlepší [migrační nástroje](../../../decision-guides/migrate-decision-guide/index.md)?
- **Sladění backlogů:** Tým přechodu na cloud zkontroluje požadavky a zaváže se k migraci kandidátské úlohy. Po přijetí závazku se odpovídajícím způsobem aktualizuje backlog vydaných verzí a backlog iterací.
- **Strukturovaný rozpis prací nebo plán prací:** Tým vytvoří plán hlavních milníků, který stanoví cíle po dokončení procesů plánování, implementace a kontroly.
- **Konečné schválení:** Všichni potřební schvalovatelé plán zkontrolovali a schválili přístup k migraci prostředku.
  - Abyste se vyhnuli překvapením v pozdějších fázích procesu, měl by se schvalovacího procesu účastnit alespoň jeden představitel firmy.

> [!CAUTION]
> Tento úplný seznam povinností a akcí může zajistit podporu rozsáhlých a složitých migrací, které zahrnují více rolí s různými úrovněmi odpovědnosti a vyžadují podrobný schvalovací proces. Méně rozsáhlé a jednodušší migrace nemusí vyžadovat všechny zde popsané role a akce. Pokud chcete určit, které z těchto aktivit vám přinesou výhody, a které ne, doporučujeme vašemu týmu přechodu na cloud a týmu cloudové strategie v rámci první migrace úloh využít tento úplný proces. Po ověření a otestování úlohy může tým tento proces vyhodnotit a zvolit, které akce se mají použít v budoucnu.

## <a name="next-steps"></a>Další kroky

Když máte obecný přehled o procesu posuzování, jste připraveni zahájit proces posouzení [Klasifikací úloh](./classify.md).

> [!div class="nextstepaction"]
> [Klasifikace úloh](./classify.md)
