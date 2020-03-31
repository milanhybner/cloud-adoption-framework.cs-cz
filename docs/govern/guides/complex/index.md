---
title: Průvodce zásadami správného řízení pro komplexní firmy
description: Využijte možnost sledovat fiktivní komplexní firmu při definování minimálního realizovatelného produktu (MVP) na základě osvědčených postupů, a to v různých fázích vyspělosti zásad správného řízení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 45c32c1d6f4a20f956748da935303eb2e8b60552
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434462"
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

1. Pro každou obchodní jednotku definujte skupinu pro správu s podrobnou hierarchií, která odráží nejprve geografii, a pak typ prostředí (například produkční nebo neprodukční prostředí).

1. Vytvořte produkční předplatné a neprodukční předplatné pro každou jedinečnou kombinaci diskrétní obchodní jednotky nebo zeměpisné oblasti. Vytváření více předplatných vyžaduje pečlivé zvážení. Další informace najdete v [Průvodci rozhodováním ohledně předplatného](../../../decision-guides/subscriptions/index.md).

1. Na všech úrovních této hierarchie seskupení používejte [konzistentní terminologii](../../../ready/azure-best-practices/naming-and-tagging.md).

1. Skupiny prostředků by se měly nasadit způsobem, který bere v úvahu životní cyklus jejich obsahu. Prostředky, které jsou vyvíjené společně, spravované společně a společně vyřazené, patří do stejné skupiny prostředků. Další informace o osvědčených postupech pro použití skupin prostředků [najdete tady](../../../decision-guides/resource-consistency/index.md).

1. [Výběr oblasti](../../../migrate/azure-best-practices/multiple-regions.md) je mimořádně důležitý a musí se zvážit, aby bylo možné v případě převzetí služeb při selhání nebo navrácení služeb po obnovení použít sítě, monitorování, auditování a také potvrzení, že [požadované skladové položky jsou dostupné v upřednostňovaných oblastech](https://azure.microsoft.com/global-infrastructure/services).

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
