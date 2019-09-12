---
title: 'Příručka zásad správného řízení pro komplexní podniky: Několik vrstev zásad správného řízení'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Příručka zásad správného řízení pro komplexní podniky: Několik vrstev zásad správného řízení'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a0a2674a91b963154d757eb35290b8aeead5c503
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908563"
---
# <a name="governance-guide-for-complex-enterprises-multiple-layers-of-governance"></a>Příručka zásad správného řízení pro komplexní podniky: Několik vrstev zásad správného řízení

Když velké podniky vyžadují více vrstev zásad správného řízení, je potřeba mít k dispozici vyšší úrovně složitosti, které se musí přihlédnout do správného řízení MVP a pozdější vylepšení zásad správného řízení.

Mezi běžné příklady takových složitosti patří:

- Distribuované funkce zásad správného řízení.
- Podniková IT oddělení IT podporují IT organizace.
- Podniková podpora geograficky distribuovaných IT organizací.

Tento článek popisuje některé způsoby, jak tento typ složitosti Procházet.

## <a name="large-enterprise-governance-is-a-team-sport"></a>Velký podnikový zásad správného řízení je tým Sport

Velké zavedené podniky mají často týmy nebo zaměstnance, kteří se soustředí na disciplíny uvedené v celé této příručce. Tato příručka ukazuje jeden ze způsobů, jak vytvořit zásady správného řízení pro tým sport.

V mnoha velkých společnostech je pět oborů řízení cloudu, které je možné přijmout, blokovat. Vývoj zkušeností v cloudu v rámci identity, zabezpečení, provozu, nasazení a konfigurace v podniku trvá určitou dobu. Komplexní implementace zásad správného řízení IT a zabezpečení IT může zpomalit inovace v měsících nebo dokonce i rocích. Vyvážením podnikových potřeb a zásad správného řízení musí chránit stávající prostředky, jemná.

Díky schopnostem cloudu můžete odebrat blokování k inovacím, ale zvýšit rizika. V této příručce ke zásadám správného řízení jsme ukázali, jak se jako příklad společnosti vytvořila guardrails pro správu rizik. Namísto využívání každého oboru, který je nezbytný k ochraně prostředí, tým zásad správného řízení cloudu vede přístup na základě rizik, který umožňuje řídit, co se dá nasadit, zatímco ostatní týmy sestavují nezbytné životní prostředí cloudu. Nejdůležitějším způsobem, protože každý tým dosáhne splatnosti cloudu, zásady správného řízení uplatní komplexní řešení. V případě, že se každý tým vystavuje a přičítá k celkovému řešení, může tým zásad správného řízení v cloudu otevřít brány a povolit další inovace a přijetí do i.

Tento model znázorňuje nárůst partnerství mezi týmem zásad správného řízení cloudu a stávajícími podnikovými týmy (zabezpečení, zásady správného řízení, sítě, identita a další). Příručka se spustí s MVP pro dodržování zásad správného řízení a roste do holistický koncového stavu prostřednictvím iterací zásad správného řízení.

## <a name="requirements-to-supporting-such-a-team-sport"></a>Požadavky na podporu takového týmu sportu

Prvním požadavkem na model zásad správného řízení Multilayer je pochopit hierarchii zásad správného řízení. Odpověď na následující otázky vám pomůžou pochopit obecnou hierarchii zásad správného řízení:

- Jak je cloudové účetnictví (fakturace za cloudové služby) přidělené napříč obchodními jednotkami?
- Jak se přiřazují zodpovědnosti zásad správného řízení v podniku a v každé obchodní jednotce?
- Jaké typy prostředí má každá z těchto jednotek IT spravovat?

## <a name="central-governance-of-a-distributed-governance-hierarchy"></a>Centrální řízení zásad distribuované hierarchie zásad správného řízení

Nástroje, jako jsou skupiny pro správu, umožňují firemnímu IT vytvořit strukturu hierarchie, která odpovídá hierarchii zásad správného řízení. Nástroje, jako jsou plány Azure, mohou použít prostředky na různé vrstvy této hierarchie. Pro skupiny pro správu, předplatná nebo skupiny prostředků se dají použít verze Azure modrotisky a různé verze. Každá z těchto konceptů je podrobněji popsána v článku MVP pro řízení.

Důležitým aspektem každého z těchto nástrojů je možnost použít pro hierarchii více modrotisky. To umožňuje zásad správného řízení být vrstvený proces. Následuje příklad této hierarchické aplikace zásad správného řízení:

- **Podniková IT oddělení:** Podnik IT vytvoří sadu standardů a zásad, které se vztahují na veškeré přijetí v cloudu. Tato možnost je vyhodnocena v podrobném plánu. Společnost IT pak vlastní hierarchii skupiny pro správu a zajišťuje tak, že se ve všech předplatných v hierarchii použije verze standardních hodnot.
- **Oblastní nebo organizační jednotka:** Různé IT týmy můžou použít další vrstvu zásad správného řízení vytvořením vlastního podrobného plánu. Tyto modrotisky by vytvořily doplňkové zásady a standardy. Po rozvinutí podnik může použít tyto plány na příslušné uzly v rámci hierarchie skupiny pro správu.
- **Týmy pro přijetí v cloudu:** Podrobné rozhodnutí a implementaci aplikací nebo úloh je možné provést v rámci každého týmu pro přijetí cloudu v rámci kontextu požadavků zásad správného řízení. V některých případech může tým také požádat o další šablony konzistence prostředků Azure, aby se urychlilo úsilí o přijetí.

Podrobnosti o implementaci zásad správného řízení na jednotlivých úrovních budou vyžadovat koordinaci mezi jednotlivými týmy. Vylepšení zásad správného řízení MVP a zásad správného řízení popsaných v této příručce vám mohou pomoci při zarovnávání této koordinace.

