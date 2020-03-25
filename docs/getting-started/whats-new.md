---
title: Co je nového
description: Přečtěte si o nejnovějších aktualizacích rozhraní pro přijetí Microsoft Cloud pro Azure.
author: JanetCThomas
ms.author: janet
ms.date: 03/09/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c7b3a4d946eac1b5296f4d37d50872105ce756ea
ms.sourcegitcommit: 25cd1b3f218d0644f911737a6d5fd259461b2458
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80225951"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Co je nového v rozhraní Microsoft Cloud pro přijímání pro Azure

Tady je seznam posledních změn, které byly provedeny v rozhraní pro přijetí do cloudu.

Tato architektura je postavená na spolupráci se zákazníky, partnery a interními týmy Microsoftu. Nový a aktualizovaný obsah se uvolní, jakmile bude k dispozici. Tyto verze umožňují testování, ověřování a upřesnění pokynů spolu s námi. Doporučujeme, abyste s námi spolupracujeme s vytvářením architektury pro přijetí cloudu pro Azure.

## <a name="march-20-2020"></a>20. března 2020

Přidali jsme Doporučené doprovodné materiály, které zahrnují nástroje, programy a obsah zařazené do kategorií, aby bylo možné úspěšně nasazovat aplikace na Kubernetes, od ověření konceptu až po produkční prostředí a za ním i škálováním a optimalizací.

### <a name="kubernetes"></a>Kubernetes

| Článek                                                                                     | Popis                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Vývoj a nasazení aplikací](../innovate/kubernetes/application-development.md) | **Nový článek** Poskytuje kontrolní seznamy, prostředky a osvědčené postupy pro plánování vývoje aplikací, konfiguraci kanálů DevOps a implementaci technologie spolehlivosti pro Kubernetes. |
| [Návrh a operace clusteru](../innovate/kubernetes/cluster-design-operations.md) | **Nový článek** Poskytuje kontrolní seznamy, prostředky a osvědčené postupy pro konfiguraci clusteru, návrh sítě, škálovatelnost budoucích prostředků, kontinuitu podnikových procesů a zotavení po havárii pro Kubernetes. |
| [Zabezpečení clusteru a aplikací](../innovate/kubernetes/cluster-application-security.md) | **Nový článek** Poskytuje kontrolní seznamy, prostředky a osvědčené postupy pro plánování, produkci a škálování zabezpečení Kubernetes. |

## <a name="march-2-2020"></a>2\. března 2020

V reakci na zpětnou vazbu týkající se kontinuity přístupu k migraci prostřednictvím několika oddílů rozhraní pro přijetí do cloudu, včetně strategie, plánování, připravenosti a migrace, jsme udělali následující aktualizace. Tyto aktualizace jsou navržené tak, aby vám usnadnily pochopení plánování a přijetí dalších informací, když budete pokračovat v cestě k migraci.

### <a name="strategy-updates"></a>Aktualizace strategií

| Článek                                                                       | Popis                                                                                                                                    |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [Vyvážení portfolia](../strategy/balance-the-portfolio.md)                 | Přesunuli jsme tento článek, aby se zobrazil dříve v metodologii strategie. Díky tomu budete mít v životním cyklu dříve promyšlený postup. |
| [Vyvážení&nbsp;konkurenčních priorit&nbsp;](../strategy/balance-competing-priorities.md) | **Nový článek**: popisuje rovnováhu priorit mezi metodologiemi, které vám pomůžou vaši strategii informovat.                                         |

### <a name="plan-updates"></a>Plánování aktualizací

| Článek                                                             | Popis                                                                                                                                                                           |
|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Posouzení&nbsp;nejlepší&nbsp;praxi](../plan/contoso-migration-assessment.md) | Tento článek byl přesunut do nového oddílu "osvědčené postupy" metodologie plánování. Díky tomu budete mít přehled o postupu hodnocení místních prostředí dříve v životním cyklu. |

### <a name="ready-updates"></a>Připravené aktualizace

| Článek                                                                   | Popis                                                                                                              |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| [Jaké&nbsp;&nbsp;&nbsp;cílovou&nbsp;zónu?](../ready/landing-zone/index.md)                 | **Nový článek**: definuje termín odpočívadla zóna.                                                                          |
| [První cílová zóna](../ready/landing-zone/first-landing-zone.md)         | **Nový článek**: rozbalí porovnání různých zón pro vykládku.                                                     |
| [Migrovat cílovou zónu](../ready/landing-zone/migrate-landing-zone.md)     | Byla oddělena definice architektury pro přijetí cloudu z výběru první cílové zóny.         |
| [Zóna odpočívadla terraformu](../ready/landing-zone/terraform-landing-zone.md) | Přesunuli jsme se do nové metodiky "cílová zóna" v rámci připravené metodologie, aby se Terraformu v konverzaci na cílové zóně. |

### <a name="migration-updates"></a>Aktualizace migrace

| Článek                                                                                          | Popis                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Přehled](../migrate/azure-migration-guide/index.md)                                            | Aktualizováno jasným popisem příručky a méně kroky.                                                                                                        |
| [Místa](../migrate/azure-migration-guide/assess.md)                                             | Byl přidán oddíl "náročné předpoklady", který demonstruje, jak tato úroveň hodnocení funguje s přístupem k přírůstkovým vyhodnocením uvedeným v metodologii plánování. |
| [Klasifikace během vyhodnocování procesů](../migrate/migration-considerations/assess/classify.md) | **Nový článek**: popisuje důležitost klasifikace každého assetu a zatížení před migrací.                                                                    |
| [Migrace](../migrate/azure-migration-guide/migrate.md)                                           | Přidání odkazu na UnifyCloud v možnostech nástrojů třetích stran v reakci na zpětnou vazbu na konferencích vrstvy 1.                                                         |
| [Testování,&nbsp;optimalizace&nbsp;a&nbsp;zvýšení úrovně](../migrate/azure-migration-guide/optimize-and-transform.md)        | Název tohoto článku byl zarovnaný k ostatním návrhům zlepšování procesu.                                                                                           |
| [Vyhodnotit přehled](../migrate/migration-considerations/assess/index.md)                           | Aktualizováno k ilustraci, že posouzení v této fázi se zaměřuje na posouzení technického přizpůsobení konkrétního zatížení a souvisejících prostředků.                               |
| [Kontrolní seznam pro plánování](../migrate/migration-considerations/prerequisites/planning-checklist.md)    | Aktualizováno, aby se vyjasnila důležitost operací při plánování migrace, abyste zajistili správnou spravovanou úlohu po migraci.                  |
