---
title: Průvodce zásadami správného řízení pro komplexní firmy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Průvodce zásadami správného řízení pro komplexní firmy
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 63b66858c023ff85e1ff6f8adc811540f3034e2d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026246"
---
# <a name="governance-guide-for-complex-enterprises"></a>Průvodce zásadami správného řízení pro komplexní firmy

## <a name="overview-of-best-practices"></a>Přehled osvědčených postupů

Tento průvodce zásadami správného řízení sleduje zážitky fiktivní společnosti napříč různými fázemi vyspělosti zásad správného řízení. Vychází ze zkušeností skutečných zákazníků. Navrhované osvědčené postupy vycházejí z omezení a potřeb fiktivní společnosti.

Jako rychlý výchozí bod tento přehled na základě osvědčených postupů definuje MVP (Minimum Viable Product) pro zásady správného řízení. Kromě toho obsahuje také odkazy na fáze vylepšení zásad správného řízení, které s tím, jak se objevují nová obchodní nebo technická rizika, implementují další osvědčené postupy.

> [!WARNING]
> Tento MVP představuje základní výchozí bod vycházející z několika předpokladů. Dokonce i tato minimální sada osvědčených postupů je založená na firemních zásadách, které se řídí jedinečnými obchodními riziky a úrovněmi tolerance k rizikům. Pokud chcete zjistit, jestli pro vás platí tyto předpoklady, přečtěte si [delší příběh](./narrative.md), který následuje po tomto článku.

### <a name="governance-best-practices"></a>Osvědčené postupy pro zásady správného řízení

Tyto osvědčené postupy slouží jako základ, pomocí kterého můžou organizace rychle a konzistentně přidávat do různých předplatných Azure ochranné mantinely zásad správného řízení.

### <a name="resource-organization"></a>Organizace prostředků

Následující diagram znázorňuje hierarchii MVP zásad správného řízení pro organizaci prostředků.

![Diagram organizace prostředků](../../../_images/govern/resource-organization.png)

Jednotlivé aplikace by se v hierarchii skupin pro správu, předplatných a skupin prostředků měly nasazovat do vhodné oblasti. Při plánování nasazení tým zásad správného řízení v cloudu vytvoří v hierarchii potřebné uzly pro týmy přechodu na cloud.

1. Pro každou obchodní jednotku definujte skupinu pro správu s podrobnou hierarchií, která odráží geografii a typ prostředí (například produkční nebo neprodukční).
1. Pro každou jedinečnou kombinaci obchodní jednotky, geografie, prostředí a kategorie aplikací vytvořte předplatné.
1. Pro každou aplikaci vytvořte samostatnou skupinu prostředků.
1. Na všech úrovních této hierarchie seskupení používejte [konzistentní terminologii](../../../ready/considerations/naming-and-tagging.md).

![Diagram organizace prostředků velké firmy](../../../_images/govern/large-enterprise-resource-organization.png)

Tyto vzory poskytují prostor k růstu bez zbytečného komplikování hierarchie.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

<!-- See comments for suggestion to possibly add here -->

## <a name="incremental-governance-improvements"></a>Postupné vylepšování zásad správného řízení

Po nasazení tohoto MVP je možné do prostředí rychle začlenit další vrstvy zásad správného řízení. Tady je několik možných způsobů vylepšení MVP za účelem splnění konkrétních obchodních potřeb:

- [Standardní hodnoty zabezpečení pro chráněná data](./security-baseline-improvement.md)
- [Konfigurace prostředků pro klíčové aplikace](./resource-consistency-improvement.md)
- [Ovládací prvky pro službu Cost Management](./cost-management-improvement.md)
- [Ovládací prvky pro průběžné multicloudové vylepšování](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Co tyto pokyny poskytují?

V MVP se zavádí postupy a nástroje z disciplíny [zrychlení nasazení](../../deployment-acceleration/index.md) kvůli možnosti rychlého použití firemních zásad. Konkrétně MVP používá Azure Blueprints, Azure Policy a skupiny pro správu Azure k použití několika základních firemních zásad, jak je definováno v příběhu této fiktivní společnosti. Tyto firemní zásady se použijí pomocí šablon Azure Resource Manageru a zásad Azure pro vytvoření základních hodnot pro identitu a zabezpečení.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvements-to-governance-practices"></a>Postupné vylepšování postupů správného řízení

V průběhu času se toto MVP zásad správného řízení využije k postupnému vylepšování osvědčených postupů zásad správného řízení. Jak přechod postupuje, obchodní riziko se zvyšuje. Pro zajištění správy těchto rizik se přizpůsobí různé disciplíny v rámci modelu zásad správného řízení architektury přechodu na cloud. Pozdější články v této sérii se zaměří na změny firemních zásad ovlivňující fiktivní společnost. K těmto změnám dochází ve čtyřech disciplínách:

- Standardní hodnoty identit – jak se závislosti migrace v příběhu mění.
- Cost Management – jak se přechod škáluje.
- Standardní hodnoty zabezpečení – jak se nasazují chráněná data.
- Konzistence prostředků – jak provoz IT začíná podporovat klíčové úlohy.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-improvement-large.png)

## <a name="next-steps"></a>Další kroky

Teď když jste se seznámili s MVP zásad správného řízení a máte představu o změnách zásad správného řízení, které budou následovat, přečtěte si doprovodný příběh, ve kterém najdete další kontext.

> [!div class="nextstepaction"]
> [Přečíst doprovodný příběh](./narrative.md)
