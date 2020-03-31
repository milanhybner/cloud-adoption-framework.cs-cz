---
title: Obchodní zarovnání v Cloud managementu
description: Pomocí architektury cloudu pro přijetí v Azure se dozvíte, jak lépe spravovat cloudové operace a rozvíjet užší obchodní zarovnání.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 432e974a304741a64e0cd7da9577ecec5e35d57e
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434054"
---
# <a name="create-business-alignment-in-cloud-management"></a>Vytváření obchodních zarovnání v Cloud managementu

V místních prostředích IT prostředky (aplikace, virtuální počítače, hostitelé virtuálních počítačů, disky, servery, zařízení a zdroje dat) spravuje IT, aby podporovaly operace s úlohami. V těchto případech je zatížení kolekcí IT prostředků, které podporují určitou obchodní operaci. Za účelem podpory podnikových operací poskytuje Správa IT procesy, které jsou navržené tak, aby minimalizovaly přerušení těchto prostředků. Když se organizace přesune ke cloudu, Správa a provoz se přenáší do provozu a vytvoří příležitost k vývoji těsnějšího zarovnání firmy.

## <a name="business-vernacular"></a>Obchodní Vernacular

Prvním krokem při vytváření zarovnání firmy je zajištění toho, aby se zajistilo zarovnání termínu. Správa IT, jako je většina inženýrských povolání, amassed kolekci žargonu nebo vysoce technické výrazy. Tyto výrazy mohou vést k nejasnostem u obchodních zúčastněných stran a obtížně mapovat služby správy na obchodní hodnotu.

Naštěstí proces vývoje strategie přijetí do cloudu a plánu přijetí do cloudu vytvoří ideální příležitost k přemapování těchto podmínek. Proces také vytvoří příležitosti k přemýšlení závazků na provozní správu ve spolupráci s firmou. Následující série článků vás provedou tímto novým přístupem v rámci tří konkrétních podmínek, které mohou pomoci vylepšit konverzace mezi podnikovými účastníky:

- **[Závažnost](./criticality.md):** Mapování úloh na obchodní procesy. Nepostradatelné řazení pro zaměření investic
- **[Dopad](./impact.md):** Pochopíte dopad potenciálních výpadků na podporu při vyhodnocování návratnosti investic do správy cloudu.
- **[Závazek](./commitment.md):** vývoj skutečných partnerství díky tvorbě a dokumentování smluv *s podnikáním*.

> [!NOTE]
> Základem těchto podmínek je klasický pojem IT, jako je například smlouva SLA, RTO a RPO. Mapování konkrétního podnikání a jeho podmínek je podrobněji popsáno v článku o [závazku](./commitment.md) .

## <a name="ops-management-planning-workbook"></a>Sešit plánování správy OPS

K tomu, aby bylo možné zachytit rozhodnutí z této konverzace o sbližování termínů, je [sešit správy OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k dispozici na našem webu GitHubu. V tomto sešitu se neprovádí smlouva SLA ani výpočty nákladů. Slouží pouze k tomu, aby pomohly zachytit taková opatření a vracet předpovědi při výpadku ztrát.

Případně můžou být tyto stejné úlohy a přidružené prostředky označené přímo v Azure, pokud už jsou tato řešení nasazená v cloudu.

## <a name="next-steps"></a>Další kroky

Začněte vytvářet obchodní zarovnání tím, že definujete [kritickou úlohu](./criticality.md).

> [!div class="nextstepaction"]
> [Definování závažnosti úloh](./criticality.md)
