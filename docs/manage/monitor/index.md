---
title: Průvodce monitorováním cloudu
description: Seznamte se s Azure Monitorem, System Center Operations Managerem a doporučenou strategií pro monitorování jednotlivých modelů cloudového nasazení.
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 4303a51a1a6df47e07e22f3de87639230f4a4c71
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79091440"
---
# <a name="cloud-monitoring-guide-introduction"></a>Průvodce monitorováním cloudu: Úvod

Cloud zásadně mění způsob, jakým podniky získávají a používají technologické prostředky. V minulosti podniky přebíraly vlastnictví všech úrovní technologií od infrastruktury až po software a také zodpovědnost za ně. V současnosti cloud nabízí podnikům možnost zřizovat a využívat prostředky podle potřeby.

Přestože cloud nabízí takřka neomezenou flexibilitu, co se možností návrhu týče, podniky hledají prověřené a konsistentní metodiky pro osvojení cloudových technologií. Jednotlivé podniky přitom pro přechod na cloud mají různé cíle a časové rámce. To znamená, že nalezení jednoho řešení, které by fungovalo pro všechny, je téměř nemožné.

![Diagram strategií přechodu na cloud](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Digitální transformace také nabízí příležitost modernizovat infrastrukturu, úlohy a aplikace. V závislosti na obchodní strategii a cílech se pravděpodobnou součástí migrace z místního prostředí do plného provozu v cloudu stává přechod na model hybridního cloudu. V rámci této cesty musí IT týmy přejít na cloud a začít ho rychle využívat. Musí se ale také seznámit s efektivním monitorováním aplikací a služeb migrovaných do Azure a dál zajišťovat efektivní provoz IT a DevOps.

Zainteresované strany chtějí využívat nástroje pro správu a cloudové monitorování softwaru jako služby (SaaS). Potřebují vědět, co služby a řešení nabízejí pro zajištění kompletní transparentnosti, snížení nákladů a omezení zaměření na infrastrukturu a údržbu tradičních softwarových nástrojů pro provoz IT.

Oddělení IT ale často dává přednost využití nástrojů, do kterých už výrazně investovalo. Tento přístup podporuje představu, že procesy operací služeb budou monitorovat oba modely cloudu. Konečným cílem potom je přechod na nabídku založenou na SaaS. It preferuje tento přístup nejenom proto, že změna plánování, zdrojů a financování chce svůj čas. Důvodem jsou také nejasnosti, které produkty nebo služby Azure jsou pro zajištění přechodu vhodné nebo dostupné.

Cílem této příručky je poskytnout podrobné referenční informace, které pomohou podnikovým správcům IT, osobám zodpovědným za klíčová obchodní rozhodnutí a architektům a vývojářům aplikací seznámit se s těmito body:

* Monitorovací platformy Azure s přehledem a porovnáním jejich funkcí.
* Nejvhodnější řešení pro monitorování hybridních a privátních úloh a úloh nativních pro Azure.
* Doporučený způsob kompletního monitorování pro infrastrukturu a aplikace. Tento přístup zahrnuje nasaditelná řešení pro migraci těchto běžných úloh do Azure.

Tato příručka není praktický článek zaměřený na použití nebo konfiguraci jednotlivých řešení a služeb Azure, ale na tyto zdroje odkazuje, když to jde a je to vhodné. Po jejím přečtení porozumíte tomu, jak úspěšně provozovat úlohy s využitím osvědčených postupů a vzorů.

Pokud Azure Monitor a System Center Operations Manager neznáte a chcete se s nimi blíže seznámit a pochopit, čím jsou tak jedinečné a jaké jsou mezi nimi rozdíly, projděte si [přehled našich monitorovacích platforem](./platform-overview.md).

## <a name="audience"></a>Cílová skupina

Tato příručka je určená primárně pro podnikové správce, provozní oddělení IT, oddělení dodržování předpisů a zabezpečení IT, architekty aplikací a pracovníky zodpovědné za vývoj a provoz aplikací.

## <a name="how-this-guide-is-structured"></a>Uspořádání příručky

Tento článek je součástí série článků. Následující články by se měly číst společně a v uvedeném pořadí:

* Úvod (tento článek)
* [Strategie monitorování pro modely cloudového nasazení](./cloud-models-monitor-overview.md)
* [Shromažďování vhodných dat](./data-collection.md)
* [Upozorňování](./alerting.md)

## <a name="products-and-services"></a>Produkty a služby

K dispozici je několik softwarových produktů a služeb, které pomáhají s monitorováním a správou různých prostředků hostovaných v Azure, ve vaší firemní síti nebo v dalších poskytovatelích cloudu. Jsou to tyto:

* System Center Operations Manager
* Azure Monitor, který teď zahrnuje Log Analytics a Application Insights
* Azure Policy a Azure Blueprints
* Azure Automation
* Azure Logic Apps
* Azure Event Hubs

Tato první verze příručky se věnuje aktuálním monitorovacím platformám: Azure Monitor a System Center Operations Manager. Popisuje také doporučenou strategii monitorování jednotlivých modelů cloudového nasazení. Zahrnuje také první sadu doporučení pro monitorování, která se zaměřuje na shromažďování dat a upozorňování.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Strategie monitorování pro modely cloudového nasazení](./cloud-models-monitor-overview.md)
