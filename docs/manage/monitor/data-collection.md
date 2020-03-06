---
title: Shromažďování dat monitorování v cloudu
description: Naučte se sledovat stav a dostupnost vašeho cloudového řešení, abyste mohli shromažďovat správná data monitorování.
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 3b537caf193601057da458b07cb62bdba64a7b6b
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341102"
---
# <a name="cloud-monitoring-guide-collect-the-right-data"></a>Průvodce monitorováním cloudu: shromáždění správných dat

Tento článek popisuje některé předpoklady pro shromažďování dat monitorování v cloudové aplikaci.

Chcete-li sledovat stav a dostupnost vašeho cloudového řešení, je nutné nakonfigurovat nástroje pro monitorování, aby shromáždily úroveň signálů, které jsou založeny na předvídatelných stavech selhání. Tyto signály představují příznaky selhání, nikoli příčinu. Nástroje pro monitorování využívají metriky a pro pokročilou diagnostiku a analýzu hlavní příčiny protokolů.

Plánování monitorování a migrace je pečlivě plánováno. Začněte tím, že zahrnete vlastníka monitorovací služby, manažera provozu a další související pracovníky v průběhu plánovací fáze a v rámci cyklu vývoje a vydaných verzí pokračujete v jejich zapojení. Jejich fokus bude vyvíjet konfiguraci monitorování, která je založená na následujících kritériích:

- Jaké je složení služby? Jsou tyto závislosti sledovány ještě dnes? Pokud ano, máte k dispozici několik nástrojů? Existuje možnost konsolidovat, aniž byste museli zavádět rizika?
- Jaká je smlouva SLA služby a jak se dá změřit a ohlásit?
- Jak by měl být řídicí panel služby při vyvolání incidentu stejný? Co má řídicí panel vypadat jako vlastník služby a pro tým, který podporuje službu?
- Jaké metriky produkuje prostředek, který potřebuji monitorovat?  
- Jak bude vlastník služby, týmy podpory a další pracovníci Hledat v protokolech?

Způsob odpovědi na tyto otázky a kritéria pro upozorňování určují, jak budete používat monitorovací platformu. Pokud migrujete z existující monitorovací platformy nebo sady nástrojů pro monitorování, použijte migraci jako příležitost k opětovnému vyhodnocení vámi shromažďovaných signálů. To platí hlavně teď, když při migraci nebo integraci s cloudovou platformou monitorování, jako je Azure Monitor, je potřeba vzít v úvahu několik cenových faktorů. Mějte na paměti, že je potřeba monitorovat data. Musíte mít shromážděná optimalizovaná data, abyste vám poskytli přehled o celkovém stavu služby v 10 000. Instrumentace definovaná k identifikaci reálných incidentů by měla být co nejjednodušší, předvídatelná a spolehlivá.

## <a name="develop-a-monitoring-configuration"></a>Vývoj konfigurace monitorování

Vlastník a tým monitorovací služby obvykle řídí společnou sadu aktivit pro vývoj konfigurace monitorování. Tyto činnosti začínají v počátečních fázích plánování, pokračují v testování a ověřování v neprodukčním prostředí a rozšiřuje se na nasazení v produkčním prostředí. Konfigurace monitorování jsou odvozeny ze známých režimů selhání, výsledků testů simulovaných selhání a zkušeností uživatelů v organizaci (oddělení služeb, provozu, inženýrů a vývojářů). Takové konfigurace předpokládají, že už služba existuje, migruje se do cloudu a ještě není znovu navržená.

Pro výsledky kvality na úrovni služby Sledujte stav a dostupnost těchto služeb včas v procesu vývoje. Pokud sledujete návrh této služby nebo aplikace jako dodatečně, vaše výsledky nebudou úspěšné.

Chcete-li urychlit vyřešení incidentu, vezměte v úvahu následující doporučení:

- Definujte řídicí panel pro každou součást služby.
- Použijte metriky, které vám pomůžou diagnostikovat a identifikovat řešení nebo řešení problému, pokud se hlavní příčina nedá zjistit.
- Využijte možnosti procházení podrobností řídicího panelu nebo podporu přizpůsobení zobrazení pro upřesnění.
- Pokud potřebujete podrobné protokoly, měly by mít metriky na cíl kritéria hledání. Pokud metriky pomohly, vylepšete je pro další incident.

Přechodu Tato sada principů vám může poskytnout přehled o prověřování prakticky v reálném čase a lepší správu vaší služby.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Strategie upozorňování](./alerting.md)
