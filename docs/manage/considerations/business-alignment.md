---
title: Zarovnání firmy – Správa a provoz v cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zarovnání firmy – Správa a provoz v cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9c6884d57b9238f58921b14ec3ddbbe3623506af
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558139"
---
# <a name="create-business-alignment-in-cloud-management"></a>Vytváření obchodních zarovnání v Cloud managementu

V místních prostředích IT prostředky (aplikace, virtuální počítače, hostitelé virtuálních počítačů, disky, servery, zařízení a zdroje dat) spravuje IT, aby podporovaly operace s úlohami. V těchto případech je zatížení kolekcí IT prostředků, které podporují určitou obchodní operaci. V místních prostředích zajišťuje Správa IT procesy pro minimalizaci výpadků těchto IT prostředků, a to při pokusu o minimalizaci výpadků obchodních operací podpory. Při přechodu do cloudu se Správa a operace posunou o bit a vytvoří příležitost pro vývoj těsnějšího zarovnání firmy.

## <a name="business-vernacular"></a>Obchodní Vernacular

Prvním krokem při vytváření zarovnání firmy je zarovnání termínu. Správa IT, jako je většina inženýrských povolání, zahrnuje spravedlivý bit žargonu nebo vysoce technických podmínek. Tyto výrazy mohou vést k nejasnostem u obchodních zúčastněných stran a obtížně mapovat služby správy na obchodní hodnotu.

Naštěstí procesů pro vývoj strategie přijetí do cloudu a plánu přijetí do cloudu vytvoří situaci, kdy je vhodné přemapování podmínek. Vytvoří také skvělou příležitost k přemýšlení závazků na provozní správu ve spolupráci s firmou. Následující série článků vás prostřednictvím tohoto nového přístupu projde v rámci tří konkrétních podmínek, které můžou zlepšit konverzace s podnikovými účastníky:

- **[Závažnost](./criticality.md)** : mapování úloh na obchodní procesy. Nepostradatelné řazení pro zaměření investic
- **[Dopad](./impact.md)** : Zjistěte dopad potenciálních výpadků na podporu při vyhodnocování návratnosti investic do správy cloudu.
- **[Závazek](./commitment.md)** : vývoj skutečných partnerství díky tvorbě a dokumentování smluv **s podnikáním**.

> [!NOTE]
> Pod každým z těchto podmínek jsou klasické IT, jako jsou SLA, RTO a RPO. Mapování podnikání a podmínek IT jsou podrobněji popsány v článku o závazku.

## <a name="ops-management-planning-workbook"></a>Sešit plánování správy OPS

Aby bylo možné v důsledku této konverzace zachytit rozhodnutí, je [sešit správy OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k dispozici v našem úložišti GitHub. V tomto sešitu se neprovádí smlouva SLA ani výpočty nákladů. Slouží jenom jako vodítko k zachycení těchto měr a návratnosti předpovědi při snaze vyhnout se ztrátám.

Případně můžou být tyto stejné úlohy a přidružené prostředky označené přímo v Azure, pokud už jsou tato řešení nasazená v cloudu.

## <a name="next-steps"></a>Další kroky

Začněte vytvářet obchodní zarovnání tím, že definujete [kritickou úlohu](./criticality.md).

> [!div class="nextstepaction"]
> [Definování závažnosti úloh](./criticality.md)
