---
title: Aspekty cílových zón Azure
description: Zjistěte, jakým způsobem cílové zóny poskytují základní stavební bloky libovolného prostředí přechodu na cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/20/2019
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 5eb0dc016bcfe7778727b5a61e392e3dd3581539
ms.sourcegitcommit: 238e7a06b56950cebdcc8f75924849fc995e6ff2
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173369"
---
# <a name="landing-zone-considerations"></a>Aspekty cílových zón

Cílové zóny jsou základní stavební bloky libovolného prostředí přechodu na cloud. Termín *cílová zóna* se používá k označení prostředí, které je zřízené a připravené k hostování úloh v cloudovém prostředí, jako je Azure. Plně funkční cílová zóna je finálním produktem všech iterací metodologie připravené na architekturu přechodu na cloud.

![Aspekty cílových zón](../../_images/ready/landing-zone-considerations.png)

Na tomto obrázku vidíte hlavní aspekty implementace nasazení jakékoli cílové zóny. Tyto aspekty jde rozdělit na tři kategorie nebo typy aspektů: hostování, základy Azure a zásady správného řízení.

## <a name="hosting-considerations"></a>Aspekty hostování

Všechny cílové zóny poskytují strukturu pro možnosti hostování. Tato struktura je vytvořená explicitně prostřednictvím kontrol zásad správného řízení nebo přirozeně přijetím služeb v rámci cílové zóny. Následující články vám můžou pomoct přijmout rozhodnutí, která se pak projeví v podrobném plánu nebo jiných automatizačních skriptech, které vytvářejí cílovou zónu:

- **[Rozhodnutí o výpočetních prostředcích.](./compute-options.md)** Slaďte možnosti výpočetních prostředků s účelem cílové zóny, abyste minimalizovali provozní složitost. Toto rozhodnutí je možné vynutit pomocí sad nástrojů automatizace, jako jsou iniciativy Azure Policy a podrobné plány cílové zóny.
- **[Rozhodnutí o úložišti.](./storage-options.md)** Zvolte si nejvhodnější řešení úložiště Azure pro podporu požadavků vašich úlohy.
- **[Rozhodnutí o síti.](./networking-options.md)** Zvolte síťové služby, nástroje a architektury, které podporují požadavky vaší organizace na možnosti připojení, zásady správného řízení a úlohy.
- **[Rozhodnutí o databázích.](./data-options.md)** Určete, která databázová technologie je nejvhodnější pro vaše požadavky na úlohy.

## <a name="azure-fundamentals"></a>Základy Azure

Každá cílová zóna je součástí širšího řešení pro uspořádání prostředků v cloudovém prostředí. Základy Azure jsou základními stavebními bloky pro uspořádání.

- **[Základní koncepty Azure.](./fundamental-concepts.md)** Seznámíte se se základními koncepty a termíny používanými při uspořádání prostředků v Azure a také s tím, jak tyto koncepty vzájemně souvisejí.
- **[Průvodce rozhodováním ohledně konzistence prostředků](../../decision-guides/resource-consistency/index.md)** Jakmile pochopíte základy, může vám průvodce rozhodováním o uspořádání prostředků pomoct přijmout rozhodnutí, která ovlivní podobu cílové zóny.

## <a name="governance-considerations"></a>Požadavky na zásady správného řízení

Metodologie řízení architektury přechodu na cloud ustavují proces pro řízení prostředí jako celku. Existuje ale řada případů použití vyžadujících rozhodnutí o zásadách správného řízení, která je třeba provést pro jednotlivé cílové zóny. V mnoha scénářích se směrné plány zásad správného řízení vynucují na úrovni jednotlivých cílových zón, i když jsou vytvořené holisticky. Platí to pro prvních několik cílových zón, které organizace nasadí.

Následující články pomáhají při rozhodování týkajícím se zásad správného řízení v souvislosti s touto cílovou zónou. Jednotlivá rozhodnutí můžete zapracovat do směrných plánů zásad správného řízení.

- **Požadavky na náklady.** Na základě motivace organizace pro přechod na cloud a provozních závazků učiněných ohledně jejího prostředí můžou různé konfigurace správy nákladů vyžadovat pro tuto cílovou zónu změnu.
- **Rozhodnutí o monitorování.** V závislosti na provozních požadavcích pro tuto cílovou zónu je možné nasadit různé monitorovací nástroje. Článek o rozhodnutích týkajících se monitorování pomůže určit nejvhodnější nástroje pro nasazení.
- **Použití řízení přístupu na základě role.** [Řízení přístupu na základě role (RBAC)](../considerations/roles.md) v Azure nabízí jemně odstupňovanou správu přístupu na základě skupin pro prostředky uspořádané podle uživatelských rolí.
- **Rozhodnutí o zásadách.** [Ukázky Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/samples) poskytují předem připravené podrobné plány dodržování předpisů, každý s předdefinovanými iniciativami zásad. Rozhodnutí o zásadách jsou zdrojem informací pro výběr nejlepšího podrobného plánu nebo iniciativy zásad na základě vašich požadavků a omezení.
- **[Vytvoření konzistentního hybridního cloudu.](./hybrid-consistency.md)** Budete mít možnost vytvořit hybridní cloudová řešení, která vaší organizaci poskytnou výhody cloudových inovací a současně si zachovávají řadu výhod správy v místním prostředí.
