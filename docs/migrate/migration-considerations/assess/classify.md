---
title: Klasifikace úloh před migrací
description: Klasifikujte své úlohy během hodnocení předmigrace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/03/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8f912891bf90d0ecef29727d7d7a067d442234fc
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79095332"
---
# <a name="workload-classification-before-migration"></a>Klasifikace úloh před migrací

Při každé iteraci každého procesu migrace se migrace jednoho nebo více úloh do produkčního prostředí bude migrovat a zvýšit. Před některou z těchto migračních aktivit je důležité klasifikovat jednotlivé úlohy. Klasifikace pomáhá objasnit požadavky zásad správného řízení, zabezpečení, provozu a správy dat.

Následující doprovodné materiály staví na navrhovaných požadavcích na označování, které jsou uvedené v [článku standardy pojmenování a označování](../../../ready/azure-best-practices/naming-and-tagging.md#metadata-tags) , přidáním důležitých [operací](../../../manage/considerations/criticality.md#criticality-scale) a prvků [zásad správného řízení](../../../govern/guides/complex/prescriptive-guidance.md#resource-tagging) .

V tomto článku doporučujeme přidat k vašim existujícím standardům označování důležitost a citlivost dat. Každý z těchto datových bodů pomůže týmům porozumět tomu, které úlohy mohou vyžadovat dodatečnou pozornost nebo podporu.

## <a name="data-sensitivity"></a>Citlivost dat

Jak je uvedeno v článku o [klasifikaci dat](../../../govern/policy-compliance/data-classification.md), klasifikace dat měří dopad na to, že by se mohlo jednat o nevrácenou datovou firmu nebo zákazníkům. Týmy pro řízení a zabezpečení využívají citlivost dat nebo klasifikaci dat jako indikátor bezpečnostních rizik. Během hodnocení by tým pro přijetí v cloudu měl vyhodnotit klasifikaci dat pro každou úlohu zaměřenou na migraci a sdílet tuto klasifikaci s podpůrnými týmy. Úlohy, které se týkají výhradně v "veřejných datech", nemusí mít žádný dopad na podporu týmů. Vzhledem k tomu, že se data přesunou dál k "vysoce důvěrnému" konci spektra, budou mít členové zásad správného řízení i týmy zabezpečení pravděpodobně zájem o účast na posouzení úlohy.

Pokud chcete definovat následující položky, pracujte s týmy zabezpečení a zásad správného řízení.

- Jasný proces sdílení všech úloh v nevyřízených položkách s citlivými daty.
- Porozumění požadavkům zásad správného řízení a směrnému plánu zabezpečení potřebnému pro různé úrovně citlivosti dat.
- Pro návrh předplatného, hierarchie skupin pro správu nebo požadavky na cílovou zónu mohou mít vliv na citlivost dat.
- Všechny požadavky pro testování klasifikace dat, které mohou zahrnovat konkrétní nástroje nebo definovaný obor klasifikace.

## <a name="mission-criticality"></a>Závažnost poslání

Jak je uvedeno v článku o [kritickém zatížení úloh](../../../manage/considerations/criticality.md), závažnost úlohy představuje míru toho, jak významně bude ovlivněná činnost podniku během výpadku. Tento datový bod pomáhá provozním a bezpečnostním týmům vyhodnocovat rizika týkající se výpadků a porušení. Během hodnocení by tým pro přijetí v cloudu měl vyhodnotit kritickou náročnost pro každou úlohu zaměřenou na migraci a sdílet tuto klasifikaci s podpůrnými týmy. Úlohy typu "nízká" nebo "nepodporované" budou mít pravděpodobně malý dopad na podpůrné týmy. Jak však úlohy přistupují ke klíčovým postupům "kritickým" nebo "jednotkám kritickým", jejich provozní závislosti se stanou zjevné.

Pracujte s týmy zabezpečení a provozu co nejdříve, abyste mohli definovat následující položky:

- Jasný proces sdílení všech úloh v backlogu s požadavky na podporu.
- Porozumění požadavkům na konzistenci správy provozu a prostředků u různých různých úrovní závažnosti.
- V případě návrhu předplatného, hierarchií skupin pro správu nebo požadavků na cílovou zónu může být ovlivněná jakákoli kritická náročnost.
- Všechny požadavky na dokumentaci týkající se závažnosti, které mohou zahrnovat konkrétní provoz nebo sestavy využití, finanční analýzy nebo jiné nástroje.

## <a name="next-steps"></a>Další kroky

Jakmile jsou úlohy správně klasifikované, je mnohem snazší tyto [obchodní priority snadno sjednotit](./business-priorities.md).

> [!div class="nextstepaction"]
> [Sladění obchodních priorit](./business-priorities.md)
