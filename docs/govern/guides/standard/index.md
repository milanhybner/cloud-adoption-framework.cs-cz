---
title: Průvodce zásadami správného řízení pro standardní firmy
description: Průvodce zásadami správného řízení pro standardní firmy
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dc52ce58bf6ecb62723674c1c4ecfb12f72d07ca
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806216"
---
# <a name="standard-enterprise-governance-guide"></a>Průvodce zásadami správného řízení pro standardní firmy

## <a name="overview-of-best-practices"></a>Přehled osvědčených postupů

Tento průvodce zásadami správného řízení sleduje zážitky fiktivní společnosti napříč různými fázemi vyspělosti zásad správného řízení. Vychází ze zkušeností skutečných zákazníků. Osvědčené postupy vycházejí z omezení a potřeb fiktivní společnosti.

Jako rychlý výchozí bod tento přehled na základě osvědčených postupů definuje MVP (Minimum Viable Product) pro zásady správného řízení. Kromě toho obsahuje také odkazy na fáze vylepšení zásad správného řízení, které s tím, jak se objevují nová obchodní nebo technická rizika, implementují další osvědčené postupy.

> [!WARNING]
> Tento MVP představuje základní výchozí bod vycházející z několika předpokladů. Dokonce i tato minimální sada osvědčených postupů je založená na firemních zásadách, které se řídí jedinečnými obchodními riziky a úrovněmi tolerance k rizikům. Pokud chcete zjistit, jestli pro vás platí tyto předpoklady, přečtěte si [delší příběh](./narrative.md), který následuje po tomto článku.

### <a name="governance-best-practices"></a>Osvědčené postupy pro zásady správného řízení

Tyto osvědčené postupy slouží jako základ, pomocí kterého můžou organizace rychle a konzistentně do předplatných přidávat ochranné mantinely zásad správného řízení.

### <a name="resource-organization"></a>Organizace prostředků

Následující diagram znázorňuje hierarchii MVP zásad správného řízení pro organizaci prostředků.

![Diagram organizace prostředků](../../../_images/govern/resource-organization.png)

Jednotlivé aplikace by se v hierarchii skupin pro správu, předplatných a skupin prostředků měly nasazovat do vhodné oblasti. Při plánování nasazení tým zásad správného řízení v cloudu vytvoří v hierarchii potřebné uzly pro týmy přechodu na cloud.

1. Jedna skupina pro správu pro každý typ prostředí (například produkční, vývojové a testovací)
2. Dvě předplatná, jedno pro produkční a druhé pro neprodukční úlohy
3. Na všech úrovních této hierarchie seskupení by se měla používat [konzistentní terminologie](../../../ready/azure-best-practices/naming-and-tagging.md).
4. Skupiny prostředků by se měly nasadit způsobem, který bere v úvahu životní cyklus jejich obsahu: všechno, co se vyvíjí dohromady, se také dohromady spravuje a vyřazuje z provozu. Další informace o osvědčených postupech pro skupiny prostředků [najdete tady](../../../decision-guides/resource-consistency/index.md).
5. [Výběr oblasti](../../../decision-guides/regions/index.md) je mimořádně důležitý a musí se zvážit, aby bylo možné v případě převzetí služeb při selhání nebo navrácení služeb po obnovení použít sítě, monitorování, auditování a také potvrzení, že [požadované skladové položky jsou dostupné v upřednostňovaných oblastech](https://azure.microsoft.com/global-infrastructure/services).

Tady je příklad použití tohoto vzoru:

![Příklad organizace prostředků pro středně velkou firmu](../../../_images/govern/mid-market-resource-organization.png)

Tyto vzory poskytují prostor k růstu bez zbytečného komplikování hierarchie.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Iterativní vylepšování zásad správného řízení

Po nasazení tohoto MVP je možné do prostředí rychle začlenit další vrstvy zásad správného řízení. Tady je několik možných způsobů vylepšení MVP za účelem splnění konkrétních obchodních potřeb:

- [Standardní hodnoty zabezpečení pro chráněná data](./security-baseline-improvement.md)
- [Konfigurace prostředků pro klíčové aplikace](./resource-consistency-improvement.md)
- [Ovládací prvky pro službu Cost Management](./cost-management-improvement.md)
- [Ovládací prvky pro vývoj s více cloudy](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Co tyto pokyny poskytují?

V MVP se zavádí postupy a nástroje z disciplíny [zrychlení nasazení](../../deployment-acceleration/index.md) kvůli možnosti rychlého použití firemních zásad. Konkrétně MVP používá Azure Blueprints, Azure Policy a skupiny pro správu Azure k použití několika základních firemních zásad, jak je definováno v příběhu této fiktivní společnosti. Tyto firemní zásady se použijí pomocí šablon Resource Manageru a zásad Azure pro vytvoření základních hodnot pro identitu a zabezpečení.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Postupné vylepšování postupů správného řízení

V průběhu času se toto MVP zásad správného řízení využije k vylepšování postupů správného řízení. Jak přechod postupuje, obchodní riziko se zvyšuje. Pro zajištění správy těchto rizik se změní různé disciplíny v rámci modelu zásad správného řízení architektury přechodu na cloud. Pozdější články v této sérii se zaměří na postupné vylepšování firemních zásad ovlivňujících fiktivní společnost. K těmto vylepšením dochází ve třech disciplínách:

- Cost Management – jak se přechod škáluje.
- Standardní hodnoty zabezpečení – jak se nasazují chráněná data.
- Konzistence prostředků – jak provoz IT začíná podporovat klíčové úlohy.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-improvement.png)

## <a name="next-steps"></a>Další kroky

Teď když jste se seznámili s MVP zásad správného řízení a máte představu o vylepšeních zásad správného řízení, která budou následovat, přečtěte si doprovodný příběh, ve kterém najdete další kontext.

> [!div class="nextstepaction"]
> [Přečíst doprovodný příběh](./narrative.md)
