---
title: Průvodce monitorováním cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přehled Azure Monitoru a System Center Operations Manageru
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: d2f699596d6464deba81690827de00bab4a33520
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026314"
---
# <a name="cloud-monitoring-guide-introduction"></a>Průvodce monitorováním cloudu: Úvod

Cloud představuje zásadní posun ve způsobu, jakým podniky pořizují a využívají technologické prostředky. V minulosti podniky přebíraly vlastnictví všech úrovní technologií od infrastruktury až po software a také zodpovědnost za ně. V současnosti cloud nabízí podnikům možnost zřizovat a využívat prostředky podle potřeby.

Přestože cloud nabízí takřka neomezenou flexibilitu, co se možností návrhu týče, podniky hledají prověřené a konsistentní metodologie pro osvojení cloudových technologií. Jednotlivé podniky přitom pro přechod na cloud mají různé cíle a časové rámce. To znamená, že nalezení jednoho řešení, které by fungovalo pro všechny, je téměř nemožné.

![Diagram strategií přechodu na cloud](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Digitální transformace také nabízí příležitost modernizovat infrastrukturu, úlohy a aplikace. V závislosti na obchodní strategii a cílech pravděpodobnou součástí migrace z místního prostředí do plného provozu v cloudu je přechod na model hybridního cloudu. V rámci této cesty musí IT týmy přejít na cloud a začít ho rychle využívat. Musí se ale také seznámit s efektivním monitorováním aplikací a služeb migrovaných do Azure a dál zajišťovat efektivní provoz IT a DevOps.

Zainteresované strany chtějí využívat nástroje pro správu a cloudové monitorování softwaru jako služby (SaaS). Potřebují vědět, co služby a řešení nabízejí pro zajištění kompletní transparentnosti, snížení nákladů a menšího zaměření na infrastrukturu a údržbu tradičních softwarových nástrojů pro provoz IT.

IT ale často dává přednost využití nástrojů, do kterých už výrazně investovalo. To podporuje představu, že procesy operací služeb budou monitorovat oba modely cloudu. Konečným cílem potom je přechod na nabídku založenou na SaaS. Tato volba není způsobená jenom tím, že změna plánování, zdrojů a financování chce svůj čas. Důvodem jsou také nejasnosti, které produkty nebo služby Azure jsou pro zajištění přechodu vhodné nebo dostupné.

Cílem této příručky je poskytnout podrobné referenční informace, které pomohou podnikovým správcům IT, osobám zodpovědným za klíčová obchodní rozhodnutí a architektům a vývojářům aplikací seznámit se s těmito body:

* Monitorovací platformy Azure s přehledem a porovnáním jejich funkcí.
* Nejvhodnější řešení pro monitorování hybridních a privátních úloh a úloh nativních pro Azure.
* Doporučený způsob monitorování pro infrastrukturu a aplikace jako celek. Zahrnuje nasaditelná řešení pro tyto běžné úlohy migrace do Azure.

Tato příručka není praktický průvodce použitím nebo konfigurací jednotlivých řešení a služeb Azure, ale na tyto zdroje odkazuje, když to jde a je to vhodné. Po přečtení této příručky porozumíte tomu, jak úspěšně provozovat úlohy s využitím doporučených postupů a vzorů.

Pokud Azure Monitor a System Center Operations Manager neznáte a chtěli byste se s nimi nejdřív blíže seznámit a pochopit, čím jsou tak jedinečné a jaké jsou mezi nimi rozdíly, projděte si [přehled našich monitorovacích platforem](./platform-overview.md).

## <a name="audience"></a>Cílová skupina

Tato příručka je primárně určená pro podnikové správce, provozní oddělení IT, oddělení dodržování předpisů a zabezpečení IT, architekty aplikací a pracovníky zodpovědné za vývoj a provoz aplikací.

## <a name="how-this-guide-is-structured"></a>Uspořádání příručky

Tento článek je součástí série článků. Následující články by se měly číst společně a v uvedeném pořadí:

* Úvod (tento článek)
* [Strategie monitorování pro modely cloudového nasazení](./cloud-models-monitor-overview.md)
* [Shromažďování správných dat](./data-collection.md)
* [Upozorňování](./alerting.md)

## <a name="products-and-services"></a>Produkty a služby

K dispozici je nabídka softwaru a služeb pro monitorování a správu různých prostředků hostovaných v Azure, vaší firemní sítě nebo dalších poskytovatelů cloudu. Jsou to tyto:

* System Center Operations Manager
* Azure Monitor, který teď zahrnuje Log Analytics a Application Insights
* Azure Policy a Azure Blueprints
* Azure Automation
* Azure Logic Apps
* Azure Event Hubs

Tato první verze průvodce se zaměřuje na naše aktuální monitorovací platformy, Azure Monitor a System Center Operations Manager, a popisuje doporučenou strategii monitorování jednotlivých modelů cloudového nasazení. Zahrnuje také první sadu doporučení pro monitorování, která se zaměřuje na shromažďování dat a upozorňování.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Strategie monitorování pro modely cloudového nasazení](./cloud-models-monitor-overview.md)
