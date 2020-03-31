---
title: Architektura úloh před migrací
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak definovat novou architekturu před tím, než začne migrace do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e5211d263e2833b8cef41d3f8b3cc1d709b89d39
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432893"
---
# <a name="architect-workloads-prior-to-migration"></a>Architektura úloh před migrací

Tento článek navazuje na proces posouzení. Popisuje aktivity spojené s definováním architektury úlohy v rámci dané iterace. V článku o [přírůstkové racionalizaci](../../../digital-estate/rationalize.md) jsme si řekli, že určité architektonické předpoklady jsou součástí každé obchodní transformace, která vyžaduje migraci. V tomto článku najdete vysvětlení těchto předpokladů, dozvíte se o některých překážkách, kterým se můžete vyhnout, a zjistíte, jaké jsou příležitosti ke zrychlení obchodní hodnoty tím, že tyto předpoklady zpochybníte. Tento inkrementální model architektury umožňuje týmům rychlejší posun, aby rychleji dosáhly obchodních výsledků.

## <a name="architecture-assumptions-prior-to-migration"></a>Architektonické předpoklady před migrací

Následující předpoklady jsou typické při každé migraci:

- **IaaS.** Často se předpokládá, že migrační úlohy spočívají primárně v přesunu virtuálních počítačů z fyzického do cloudového datacentra prostřednictvím migrace IaaS, která vyžaduje minimální opakovaný vývoj nebo konfiguraci. Tato metoda se označuje jako migrace _výtahu a posunutí_ . (Výjimky viz níže.)
- **Konzistence architektury.** Změny základní architektury prováděné při migraci celou operaci výrazně komplikují. Ladění změněného systému na nové platformě přináší řadu proměnných, které můžou být obtížně oddělitelné. Proto by se při migraci měly provádět jen malé změny úloh a všechny změny musí být důkladně otestovány.
- **Test vyřazení.** Migrace a hostování prostředků s sebou nesou provozní a případně i kapitálové výdaje. U migrovaných úloh se předpokládá, že bylo zkontrolováno a ověřeno jejich průběžné používání. Volba vyřazení nepoužívaných prostředků přináší okamžitou úsporu nákladů.
- **Změna velikosti prostředků.** Předpokládá se, že jen některé místní prostředky plně využívají přidělené zdroje. Před migrací se předpokládá, že změníte velikost prostředků, aby odpovídaly požadavkům na jejich skutečné využití.
- **Požadavky na provozní kontinuitu a zotavení po havárii (BCDR).** Předpokládá se, že před plánovaným vydáním má firma pro úlohu sjednanou smlouvu SLA. Tyto požadavky budou pravděpodobně vyžadovat jenom dílčí změny architektury.
- **Prostoje při migraci.** Výpadek způsobený přesunem úlohy do produkčního prostředí může mít na firmu nepříznivý vliv. Někdy je u řešení, která vyžadují přechod s minimálním výpadkem, potřeba změnit architekturu. Předpokládá se, že před plánováním vydání verze budou všeobecně známy požadavky týkající se výpadků.

## <a name="roadblocks-that-can-be-avoided"></a>Překážky, kterým se lze vyhnout

Z výčtů předpokladů mohou vznikat překážky, které zpomalují průběh migrace nebo jsou později příčinou vzniku problematických bodů. Tady jsou některé překážky, na které byste si před vydáním verze měli dát pozor:

- **Placení technických dluhů.** Některé zastaralé úlohy s sebou nesou vysoký technický dluh. Ten může dlouhodobě způsobovat problémy spočívající v rostoucích nákladech na hostování u poskytovatelů cloudu. Pokud technický dluh nepřirozeně zvyšuje náklady na hostování, je potřeba zvážit alternativní architektury.
- **Vzorce uživatelských přenosů.** Stávající řešení můžou záviset na existujících vzorcích síťového směrování. Tyto vzorce můžou výrazně zpomalovat výkon. Navíc zavedení nového řešení hybridních sítí WAN může trvat týdny nebo měsíce. Proto je potřeba se na tyto překážky v procesu tvorby architektury včas připravit tím, že vezmete v úvahu vzorce přenosů dat a změny základních služeb infrastruktury.

## <a name="accelerate-business-value"></a>Zrychlit obchodní hodnotu

Některé scénáře můžou vyžadovat jinou architekturu než předpokládá strategie změny hostitele IaaS. Tady je několik příkladů:

- Alternativy PaaS. Nasazení PaaS snižuje náklady na hostování a zkracuje také čas potřebný k migraci určitých úloh. Seznam možných přístupů, které mohou mít prospěch z převodu na PaaS, najdete v článku o [vyhodnocování prostředků](./evaluate.md).
- Skriptovaná nasazení / DevOps. Pokud se pro úlohu používá nasazení DevOps nebo jiné způsoby skriptovaného nasazení, můžou být náklady na změnu těchto skriptů nižší než náklady na migraci prostředku.
- Nápravná opatření. Nápravná opatření potřebná k přípravě úlohy k migraci mohou být rozsáhlá. V některých případech je proto rozumnější modernizovat řešení než napravovat skryté problémy s kompatibilitou.

Ve všech uvedených scénářích je nejlepším možným řešením alternativní architektura.

## <a name="next-steps"></a>Další kroky

Jakmile definujete novou architekturu, [můžete vypočítat přesný odhad nákladů](./estimate.md).

> [!div class="nextstepaction"]
> [Odhad cloudových nákladů](./estimate.md)
