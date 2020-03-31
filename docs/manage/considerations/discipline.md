---
title: Úrovně správy ve správě cloudu
description: Naučte se, jak omezit možnosti správy cloudu na konzistentní sadu procesů a nástrojů, které můžete nabízet pro úlohy hostované v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ccb7a6e428075a69532238f25fd89e825f2a4b35
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80426347"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Úroveň správy napříč obory pro správu cloudu

Klíče ke správné správě v jakémkoli prostředí představují konzistenci a opakující se procesy. K dispozici jsou nekonečné možnosti pro věci, které je možné provést v Azure. Podobně existují dlouhé přístupy ke správě cloudu. Aby se zajistila konzistence a opakovatelnost, je důležité tyto možnosti zúžit na konzistentní sadu procesů a nástrojů pro správu, které se budou nabízet pro úlohy hostované v cloudu.

## <a name="suggested-management-levels"></a>Navrhované úrovně správy

Vzhledem k tomu, že se úlohy v portfoliu IT liší, je pravděpodobné, že pro každou úlohu bude stačit jedna úroveň správy. Abychom vám pomohli podpořit celou řadu úloh a obchodních závazků, doporučujeme, aby tým operací cloudu nebo provozním týmem na platformě vyvázal několik úrovní správy provozu.

![Správa úrovní správy a zralosti v rámci architektury pro přijetí v cloudu](../../_images/manage/cloud-management-maturity.png)

Jako výchozí bod zvažte vytvoření úrovní správy, které jsou uvedeny v předchozím diagramu a navržena v následujícím seznamu:

- **Standardní hodnoty správy:** Směrný plán správy cloudu (nebo standardní hodnota správy) je definovaná sada nástrojů, procesů a konzistentní ceny, které slouží jako základ pro veškerou správu cloudu v Azure. Pokud chcete vytvořit směrný plán správy cloudu a určit, které nástroje se mají do vaší firmy zahrnout, Projděte si seznam v části obory pro správu cloudu.
- **Rozšířené základní hodnoty:** Řada úloh může vyžadovat vylepšení standardních hodnot, které nemusí být nutně specifická pro jednu platformu nebo úlohu. I když tato vylepšení nejsou nákladově efektivní pro každou úlohu, měly by se provádět běžné procesy, nástroje a řešení pro všechny úlohy, které mohou zdůvodnit náklady na dodatečnou podporu pro správu.
- **Specializace platformy:** V jakémkoli daném prostředí jsou některé běžné platformy používány různými úlohami. Toto obecné společné architektury se nemění, když firmy přijímají Cloud. Specializace platformy je zvýšená úroveň správy, která se vztahuje na data a odbornosti v oblasti architektury za účelem zajištění vyšší úrovně provozní správy. Příklady specializace platforem zahrnují funkce správy, které jsou specifické pro SQL Server, kontejnery, služby Active Directory nebo jiné služby, které je možné lépe spravovat prostřednictvím konzistentních, opakujících se procesů, nástrojů a architektur.
- **Specializace úloh:** Pro úlohy, které jsou skutečně důležité, může dojít k výraznému snížení nákladů na správu této úlohy. Specializace úloh používá telemetrii úloh k určení pokročilejších přístupů ke každodenní správě. Stejná data často označují vylepšení automatizace, nasazení a návrhu, která by vedla k větší stabilitě, spolehlivosti a odolnosti nad rámec toho, co je možné jenom v provozní správě.
- **Nepodporované:** Stejně důležité je, abyste komunikovali s běžnými procesy správy, které se nebudou dodávat prostřednictvím oborů správy cloudu pro úlohy klasifikované jako nepodporované nebo nepostradatelné.

Organizace se také mohou rozhodnout, že [externí funkce související s jednou nebo více z těchto úrovní správy k poskytovateli služeb](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Tito poskytovatelé služeb můžou využít [Azure Lighthouse](https://azure.com/lighthouse) k zajištění větší přesnosti a transparentnosti.

Zbývající články v této sérii popisují řadu procesů, které se běžně vyskytují v rámci každého z těchto oborů.
V rámci paralelní [příručky Azure Management](../azure-management-guide/index.md) demonstruje nástroje, které můžou podporovat jednotlivé procesy. Pokud potřebujete pomoc s vytvářením standardních hodnot správy, začněte s průvodcem pro správu Azure. Po vytvoření směrného plánu vám tato série článků a doprovodné osvědčené postupy mohou pomoci tuto základnu rozšířit a definovat další úrovně podpory správy.

## <a name="cloud-management-disciplines"></a>Obory pro správu cloudu

Každá navrhovaná úroveň správy se může volat v nejrůznějších oborech pro správu cloudu. Mapování je ale navržené tak, aby bylo snazší najít navrhované procesy a nástroje pro zajištění vhodné úrovně správy cloudu.

Ve většině případů se výše popsaná *úroveň správy základní úrovně* skládá z procesů a nástrojů z následujících oborů. V každém případě se zvýrazní několik procesů a nástrojů, které demonstrují *Rozšířené funkce standardních hodnot*.

- **Inventář a viditelnost:** Standardní hodnota správy by měla zahrnovat způsob inventarizace assetů a vytváření viditelnosti stavu spuštění každého assetu.
- **Provozní dodržování předpisů:** Běžnou správou konfigurace, velikosti, nákladů a výkonu assetů je klíč pro udržení očekávání výkonu a standardních hodnot správy.
- **Ochrana a obnovení:** Minimalizace provozních přerušení a urychlení obnovení vám může přispět k tomu, abyste se vyhnuli ztrátám a výnosům z výkonu. Zjišťování a obnovení jsou zásadními aspekty tohoto oboru v rámci všech standardních hodnot správy.

Úroveň specializace platformy pro správu se přebírá z procesů a nástrojů, které jsou zarovnané na provozní obory platformy. Podobně platí, že úroveň specializace úlohy správy se vyžádá z procesů a nástrojů, které jsou zarovnané na provozní pravidla úloh.

## <a name="next-steps"></a>Další kroky

Dalším krokem k definování jednotlivých úrovní správy cloudu je porozumění [inventarizaci a viditelnosti](./inventory.md).

> [!div class="nextstepaction"]
> [Možnosti inventarizace a viditelnosti](./inventory.md)
