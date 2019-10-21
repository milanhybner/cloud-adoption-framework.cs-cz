---
title: Průvodce monitorováním cloudu – shromažďování správných dat
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vyberte, kdy použít Azure Monitor nebo System Center Operations Manager v Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 3d8d6b656f6bfe8072b53dccc05a67479aa36f24
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548576"
---
# <a name="cloud-monitoring-guide-collecting-the-right-data"></a>Průvodce monitorováním cloudu: shromažďování správných dat

Tento článek popisuje některé předpoklady pro shromažďování dat monitorování v cloudové aplikaci.

Chcete-li sledovat stav a dostupnost vašeho cloudového řešení, je nutné nakonfigurovat nástroje pro monitorování, aby shromáždily úroveň signálů, které jsou založeny na předvídatelných stavech selhání. Tyto signály představují příznaky selhání, nikoli příčinu. Nástroje pro monitorování používají metriky a v případě pokročilé diagnostiky a analýzy hlavní příčiny také používají protokoly.

Plánování monitorování a migrace je pečlivě plánováno. Začněte tím, že zahrnete vlastníka monitorovací služby, manažera provozu a další související pracovníky v průběhu plánovací fáze a v rámci cyklu vývoje a vydaných verzí pokračujete v jejich zapojení. Jejich fokus bude vyvíjet konfiguraci monitorování, která je založená na následujících kritériích:

- Co je to složení služby a tyto závislosti se ještě dnes monitorují? Pokud ano, máte k dispozici několik nástrojů? Existuje možnost konsolidovat, aniž byste museli zavádět rizika?
- Jaká je smlouva SLA služby a jak se dá změřit a ohlásit?
- Jak by měl být řídicí panel služby při vyvolání incidentu stejný? Co má řídicí panel vypadat jako vlastník služby a tým tuto službu podporuje?
- Jaké metriky produkuje prostředek, který potřebuji monitorovat?  
- Jak bude vlastník služby, týmy podpory a další pracovníci Hledat v protokolech?

Způsob odpovědi na tyto otázky a kritéria pro upozorňování určují, jak budete používat monitorovací platformu. Pokud migrujete z existující monitorovací platformy nebo sady nástrojů pro monitorování, použijte migraci jako příležitost k opětovnému vyhodnocení vámi shromažďovaných signálů. To znamená, že při migraci nebo integraci s cloudovou monitorovací platformou, jako je Azure Monitor, je potřeba vzít v úvahu několik cenových faktorů. Mějte na paměti, že je potřeba monitorovat data. Musíte mít shromážděná optimalizovaná data, abyste vám poskytli přehled o celkovém stavu služby v 10 000. Instrumentace definovaná k identifikaci reálných incidentů by měla být co nejjednodušší, předvídatelná a spolehlivá.

## <a name="develop-a-monitoring-configuration"></a>Vývoj konfigurace monitorování

Vlastník a tým monitorovací služby obvykle řídí společnou sadu aktivit pro vývoj konfigurace monitorování. Tyto činnosti začínají v počátečních fázích plánování, pokračují v testování a ověřování v neprodukčním prostředí a rozšiřuje se na nasazení v produkčním prostředí. Konfigurace monitorování jsou odvozeny ze známých režimů selhání, výsledků testů simulovaných selhání a zkušeností uživatelů v organizaci (oddělení služeb, provozu, inženýrů a vývojářů). Takové konfigurace předpokládají, že služba již existuje, migruje se do cloudu a nebyla přenavržena.

Sledujte stav a dostupnost těchto služeb včas v procesu vývoje, pro výsledky kvality na úrovni služby. Pokud sledujete návrh této služby nebo aplikace jako dodatečně, vaše výsledky nebudou úspěšné.

Chcete-li urychlit vyřešení incidentu, vezměte v úvahu následující doporučení:

- Definujte řídicí panel pro každou součást služby.
- Použijte metriky, které vám pomohou diagnostikovat a identifikovat řešení problému, pokud nelze odkrýt hlavní příčinu.
- Využijte možnosti procházení podrobností řídicího panelu nebo podporu přizpůsobení zobrazení pro upřesnění.
- Pokud potřebujete podrobné protokoly, měly by mít metriky na cíl kritéria hledání. Pokud ne, Vylepšete metriky pro další incident.

Přechodu Tato sada principů poskytuje informace téměř v reálném čase a lepší správu vaší služby.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Strategie upozorňování](./alerting.md)
