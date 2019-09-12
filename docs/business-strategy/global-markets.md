---
title: Pochopení dopadu globálních rozhodnutí o trhu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vysvětlení konceptu globálních trhů
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: ca1e18bdc8da300667b721e673bb1fc0388b4bdf
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825052"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-will-global-market-decisions-affect-the-transformation-journey"></a>Jak budou globální rozhodnutí na trhu ovlivňovat cestu transformace?

Cloud otevírá nové příležitosti, které se budou provádět na globálním měřítku. Překážky globálních operací se významně snižují díky tomu, že společnosti umožňují nasazovat prostředky na trh, aniž by museli investovat do nových datových center silně. To bohužel přináší značnou složitost z technického a právního výhledu.

## <a name="data-sovereignty"></a>Suverenita dat

Řada geopolitických oblastí stanovila pravidla pro svrchovanost dat. Tyto předpisy omezují, kde mohou být data uložená, jaká data mohou opustit zemi původu a jaká data je možné shromažďovat o občanůch této oblasti. Než začnete pracovat s cloudovým řešením v cizí geografické oblasti, měli byste pochopit, jak tento poskytovatel cloudu zpracovává svrchovanost dat. Další informace o přístupu k Azure pro jednotlivé geografické oblasti [najdete tady](https://azure.microsoft.com/global-infrastructure/geographies). Další informace o dodržování předpisů v Azure najdete v tématu [Ochrana osobních údajů v Microsoftu na webu Microsoft](https://www.microsoft.com/trustcenter/privacy) Trust Center.

Zbývající část tohoto článku předpokládá, že právní poradce kontroloval a schválil provoz v cizí zemi.

## <a name="business-units"></a>Obchodní jednotky

Je důležité porozumět tomu, které obchodní jednotky pracují v cizích zemích a kterých zemích jsou ovlivněny. Tyto informace budou sloužit k návrhu řešení pro hostování, fakturaci a nasazení poskytovateli cloudu.

## <a name="employee-usage-patterns"></a>Vzorce používání zaměstnanců

Je důležité pochopit, jak globální uživatelé přistupují k aplikacím, které nejsou hostované ve stejné zemi jako uživatel. Globální sítě WAN (sítě WAN) často směrují uživatele na základě stávajících síťových smluv. V tradičním místním světě některá omezení omezují návrh sítě WAN. Tato omezení můžou vést ke zhoršení uživatelského prostředí, pokud je před přijetím cloudu správně nerozumíte.

V modelu cloudu se v komoditních připojeních k Internetu otevírá i mnoho nových možností. Komunikace s rozšiřováním zaměstnanců napříč různými geografickými oblastmi může přispět k návrhu řešení WAN v týmu, kteří vytvářejí pozitivní uživatelské prostředí **a** můžou snižovat náklady na síť.

## <a name="external-user-usage-patterns"></a>Vzorce používání externích uživatelů

Je stejně důležité pochopit vzory využití externích uživatelů, jako jsou zákazníci nebo partneři. Podobně jako vzorce používání zaměstnanců můžou vzory využívání externích uživatelů negativně ovlivnit výkon nasazení v cloudu. Když se v cizí zemi nachází velká nebo důležitá uživatelská základna, může být vhodné zahrnout do celkového návrhu řešení strategii globálního nasazení.

## <a name="next-steps"></a>Další postup

Po uskutečnění a předání celosvětového rozhodnutí na trhu je tým připraven zahájit [vytváření technických standardů](../digital-estate/index.md) na základě těchto metrik.
Výsledkem bude [nevyřízené položky transformace nebo nevyřízené položky migrace](..//migrate/migration-considerations/prerequisites/technical-complexity.md).

> [!div class="nextstepaction"]
> [Posouzení digitální nemovitosti](../digital-estate/index.md)
