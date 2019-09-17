---
title: Nastavení základních upozornění
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nastavení základních upozornění
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5b11a97e78d5fcd1b2a2cc866f5a7062bc6a2977
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029019"
---
# <a name="set-up-basic-alerts"></a>Nastavení základních upozornění

Klíčovou součástí správy prostředků je upozornění, když dojde k problémům. Upozornění vás aktivně informují o kritických stavech. Můžou být založené na triggerech z metrik, protokolů nebo problémů se stavem služby. V rámci připojování služeb pro správu Azure serveru můžete nastavit upozornění a oznámení, která vám pomůžou udržet vaše týmy IT vědět o případných problémech.

## <a name="azure-monitor-alerts"></a>Výstrahy Azure Monitor

Azure Monitor nabízí [](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) možnosti upozorňování, které vám upozorní e-mailem nebo zasíláním zpráv, když dojde k chybě. Tyto možnosti jsou založené na běžné platformě pro monitorování dat, která zahrnuje protokoly a metriky vygenerované vašimi servery a dalšími prostředky. Tato platforma umožňuje analyzovat data kombinovaná z několika prostředků pomocí běžné sady nástrojů v Azure Monitor, kterou můžete použít k aktivaci výstrah. Tyto triggery můžou zahrnovat:

- Hodnoty metriky.
- Dotazy na hledání protokolu
- Události protokolu aktivit.
- Stav základní platformy Azure.
- Testuje dostupnost webu.

Podrobnější popis zdrojů dat monitorování shromažďovaných touto službou najdete v [seznamu Azure monitor zdrojů dat](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) .

Podrobnosti o ručním vytváření a správě výstrah pomocí portálu najdete v [dokumentaci k Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Automatizované nasazení doporučených výstrah

V této příručce doporučujeme povolit sadu 15 výstrah pro základní monitorování infrastruktury. Skripty pro nasazení najdete v [úložišti GitHub v sadě Azure Alert Toolkit](https://github.com/Microsoft/manageability-toolkits).

Tento balíček vytváří výstrahy pro nedostatek místa na disku, nedostatek dostupné paměti, vysokého využití procesoru, neočekávaného vypnutí, poškozených systémů souborů a běžných selhání hardwaru. Balíček používá jako příklad hardware serveru HP. Měli byste změnit nastavení v přidruženém konfiguračním souboru tak, aby odráželo váš hardware výrobce OEM. Do konfiguračního souboru můžete také přidat další čítače výkonu. Chcete-li nasadit balíček, spusťte soubor New-CoreAlerts. ps1.

## <a name="next-steps"></a>Další kroky

Přečtěte si o operacích a mechanismech zabezpečení, které podporují vaše probíhající operace.

> [!div class="nextstepaction"]
> [Průběžná správa a zabezpečení](./ongoing-management-overview.md)
