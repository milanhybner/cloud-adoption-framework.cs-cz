---
title: Backlog iterace a vydání
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak vytvořit iteraci a nevyřízené položky pro uspořádání úkolů.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8e3ed4ff6457c0e9d00777f94c812097f0b742e9
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429397"
---
# <a name="manage-change-in-an-incremental-migration-effort"></a>Správa změn v průběhu přírůstkové migrace

V tomto článku se předpokládá, že procesy migrace jsou z povahy věcí přírůstkové a běží paralelně s [procesem řízení](../../../govern/index.md). Stejné pokyny se ale můžou použít k naplnění počátečních úkolů ve struktuře členění práce pro účely tradičního kaskádového řízení změn.

## <a name="release-backlog"></a>Backlog vydání

*Backlog vydání* se skládá z řady prostředků (mimo jiné virtuálních počítačů, databází, souborů a aplikací), které se musí migrovat předtím, než se úloha uvolní pro produkční využití v cloudu. Během každé iterace tým přechodu na cloud zdokumentuje a odhadne úsilí potřebné k přesunu jednotlivých prostředků do cloudu. Podívejte se na část Backlog iterace, která následuje.

## <a name="iteration-backlog"></a>Backlog iterace

*Backlog iterace* je podrobný seznam prací, které jsou potřeba k migraci určitého počtu prostředků ze stávajícího digitálního aktiva do cloudu. Položky tohoto seznamu jsou často uložené jako pracovní položky v agilním nástroji pro správu, jako je Azure DevOps.

Před zahájením první iterace určí tým přechodu na cloud dobu trvání iterace, která je obvykle od dvou do čtyř týdnů. Tento časový úsek je důležitý k vytvoření počátečního a koncového období pro každou sadu potvrzených aktivit. Udržování konzistentních spouštěcích oken usnadňuje měření rychlosti (tempa migrace) a přizpůsobení měnícím se obchodním potřebám.

Před každou iterací tým kontroluje backlog vydání a odhadne úsilí a priority prostředků, které se mají migrovat. Pak potvrdí doručení určitého počtu dohodnutých migrací. Po schválení týmem přechodu na cloud se seznam aktivit stane *aktuálním backlogem iterace*.

Během každé iterace členové týmu pracují jako samoorganizovaný tým, který plní závazky v rámci aktuálního backlogu iterace.

## <a name="next-steps"></a>Další kroky

Jakmile se backlog iterace definuje a přijme týmem přechodu na cloud, je možné dokončit [schválení správy změn](./approve.md).

> [!div class="nextstepaction"]
> [Schválení změn architektury před migrací](./approve.md)
