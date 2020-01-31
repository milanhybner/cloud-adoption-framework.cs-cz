---
title: Nastavení základních upozornění
description: Naučte se používat služby Azure Server Management Services k nastavení výstrah a oznámení, která vám pomůžou zajistit, aby vaši týmy IT věděli o případných problémech.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e24932b074f69f83aff583d560399d884c6c5b0e
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807950"
---
# <a name="set-up-basic-alerts"></a>Nastavení základních upozornění

Klíčovou součástí správy prostředků je upozornění, když dojde k problémům. Výstrahy proaktivně upozorňují na kritické podmínky na základě triggerů z metrik, protokolů nebo problémů se stavem služby. V rámci připojování služeb pro správu Azure serveru můžete nastavit výstrahy a oznámení, které vám pomůžou zajistit, aby vaši týmy IT věděli o všech problémech.

## <a name="azure-monitor-alerts"></a>Výstrahy Azure Monitor

Azure Monitor nabízí funkce [upozorňování](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) , které vám upozorní na to, že se něco pokazilo, prostřednictvím e-mailu nebo zprávy. Tyto možnosti jsou založené na běžné platformě pro monitorování dat, která zahrnuje protokoly a metriky vygenerované vašimi servery a dalšími prostředky. Pomocí běžné sady nástrojů v Azure Monitor můžete analyzovat data kombinovaná z několika prostředků a používat je k aktivaci výstrah. Tyto triggery můžou zahrnovat:

- Hodnoty metriky.
- Dotazy na hledání protokolu
- Události protokolu aktivit.
- Stav základní platformy Azure.
- Testuje dostupnost webu.

Podrobnější popis zdrojů dat monitorování, které tato služba shromažďuje, najdete v [seznamu Azure monitor zdrojů dat](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) .

Podrobnosti o ručním vytváření a správě výstrah pomocí Azure Portal najdete v [dokumentaci k Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Automatizované nasazení doporučených výstrah

V této příručce doporučujeme vytvořit sadu 15 výstrah pro základní monitorování infrastruktury. V [úložišti GitHub sady Azure Alert Toolkit](https://github.com/Microsoft/manageability-toolkits)najdete skripty pro nasazení.

Tento balíček vytvoří výstrahy pro:

- Nedostatek místa na disku
- Nedostatek dostupné paměti
- Vysoké využití procesoru
- Neočekávaná vypnutí
- Poškozené systémy souborů
- Běžné chyby hardwaru

Balíček používá jako příklad hardware serveru HP. Změňte nastavení v přidruženém konfiguračním souboru tak, aby odráželo váš hardware výrobce OEM. Do konfiguračního souboru můžete také přidat další čítače výkonu. Chcete-li nasadit balíček, spusťte soubor New-CoreAlerts. ps1.

## <a name="next-steps"></a>Další kroky

Přečtěte si o operacích a mechanismech zabezpečení, které podporují vaše probíhající operace.

> [!div class="nextstepaction"]
> [Průběžná správa a zabezpečení](./ongoing-management-overview.md)
