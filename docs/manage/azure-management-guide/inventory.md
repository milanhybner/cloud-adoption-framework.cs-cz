---
title: Inventarizace a získání přehledu v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zjistěte, jak u prostředí pro správu Azure nastavit inventarizaci, monitorování, generování sestav a upozornění.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 8b7902910de3df729524b1625fe83b0681eeef5b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556781"
---
# <a name="inventory-and-visibility-in-azure"></a>Inventarizace a získání přehledu v Azure

_Inventarizace a získání přehledu_ je první ze tří disciplín ve směrném plánu cloudové správy.

![Směrný plán cloudové správy](../../_images/manage/management-baseline.png)

Tato disciplína je na prvním místě, protože při rozhodování o operacích je nezbytné shromažďovat správná provozní data. Týmy pro správu cloudu musí pochopit, co se spravuje a jak dobře tyto prostředky fungují. Tento článek popisuje různé nástroje, které poskytují inventarizaci i přehled stavu spuštění inventarizace.

V následující tabulce je pro jednotlivá podniková prostředí uvedeno navrhované minimum pro jakýkoli směrný plán správy.

|Proces  |Nástroj  |Účel  |
|---------|---------|---------|
|Monitorování stavu služeb Azure|Azure Service Health|Stav, výkon a diagnostika pro služby běžící v Azure|
|Centralizace protokolů|Log Analytics|Centrální protokolování pro všechny účely získání přehledu|
|Centralizace monitorování|Azure Monitor|Centrální monitorování provozních dat a trendů|
|Inventář virtuálních počítačů a sledování změn|Azure Change Tracking a služba Inventory|Inventarizace virtuálních počítačů a monitorování změn na úrovni hostovaného operačního systému|
|Service Health|Protokol aktivit Azure|Monitorování změn na úrovni předplatného|
|Monitorování hostovaného operačního systému|Azure Monitor pro virtuální počítače|Monitorování změn a výkonu virtuálních počítačů|
|Monitorování sítě|Azure Network Watcher|Monitorování změn a výkonu sítě|
|Monitorování systému DNS|DNS Analytics|Zabezpečení, výkon a operace systému DNS|

::: zone target="docs"

## <a name="azure-service-health"></a>Azure Service Health

::: zone-end
::: zone target="chromeless"

## <a name="azure-service-healthtabazureservicehealth"></a>[Azure Service Health](#tab/AzureServiceHealth)

::: zone-end

Azure Service Health poskytuje přizpůsobené zobrazení stavu služeb a oblastí Azure, které využíváte. Informace o aktivních problémech se odešle do služby Service Health, aby vám pomohla porozumět dopadu na vaše prostředky. Pravidelné aktualizace vám umožní sledovat, jak se problém řeší.

Publikujeme do Service Health také události plánované údržby, takže se dozvíte o změnách, které by mohly ovlivnit dostupnost vašich prostředků. Po nastavení upozornění služby Service Health můžete být informováni o problémech služby, plánované údržbě nebo dalších změnách, které mohou mít vliv na používané služby a oblasti Azure.

Azure Service Health zahrnuje:

- **Stav Azure:** Globální přehled o stavu služeb Azure
- **Stav služeb:** Přizpůsobený přehled o stavu vašich služeb Azure
- **Stav prostředků:** Podrobnější přehled o stavu jednotlivých prostředků

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Vytvoření upozornění služby Service Health:

1. Přejděte do služby **Service Health**.
2. Vyberte **Upozornění na stav**.
3. Vytvořte upozornění na stav služby.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete nastavit upozornění služby Service Health, přejděte na [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

### <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Service Health](https://docs.microsoft.com/azure/service-health).

## <a name="log-analytics"></a>Log Analytics

::: zone-end
::: zone target="chromeless"

## <a name="log-analyticstablog-analytics"></a>[Log Analytics](#tab/Log-Analytics)

::: zone-end

[Pracovní prostor Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) představuje jedinečné prostředí pro ukládání dat protokolů platformy Azure Monitor. Každé pracovní prostředí má vlastní úložiště dat a konfiguraci. Zdroje dat a řešení jsou nakonfigurovány tak, aby ukládaly svoje data do konkrétních pracovních prostorů. Řešení Azure pro monitorování vyžadují připojení všech serverů k pracovním prostorům, aby mohla data ukládat a přistupovat k nim.

::: zone target="chromeless"

### <a name="action"></a>Akce

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2Fworkspaces]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci k vytváření pracovních prostorů Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace).

## <a name="azure-monitor"></a>Azure Monitor

::: zone-end
::: zone target="chromeless"

## <a name="azure-monitortabazure-monitor"></a>[Azure Monitor](#tab/Azure-Monitor)

::: zone-end

Azure Monitor poskytuje jedno společné centrum pro všechna data monitorování a diagnostiky v Azure. Můžete ho použít k získání přehledu o prostředcích. Pomocí Azure Monitoru můžete najít a vyřešit problémy a optimalizovat výkon. Můžete také pochopit chování zákazníků.

- **Monitorování a vizualizace metrik.** Metriky jsou číselné hodnoty dodávané prostředky Azure, které nabízejí informace o stavu vašich systémů. Grafy můžete přizpůsobit pro řídicí panely a ke generování sestav používat sešity.

- **Dotazování a analýza protokolů.** Mezi protokoly patří protokoly aktivit a diagnostické protokoly z Azure. Shromažďujte další protokoly pro vaše cloudové nebo místní prostředky z jiných řešení pro monitorování a správu. Log Analytics slouží jako centrální úložiště pro agregaci všech těchto dat. Odtud můžete spouštět dotazy, které vám pomůžou řešit potíže nebo vizualizovat data.

- **Nastavení upozornění a akcí.** Upozornění vás aktivně informují o kritických stavech. Na základě triggerů z metrik, protokolů nebo problémů se stavem služby je možné provádět opravné akce. Můžete nastavit různá oznámení a akce a odesílat data do vašich nástrojů pro správu IT služeb.

::: zone target="chromeless"

### <a name="action"></a>Akce

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

 Zahájení monitorování pro:

- [Aplikace](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Containers](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Virtual Machines](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Sítě](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Pokud chcete monitorovat jiné prostředky, vyhledejte další řešení na webu Azure Marketplace.

Pokud chcete prozkoumat Azure Monitor, přejděte na [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

### <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

## <a name="onboard-solutions"></a>Nasazení řešení

::: zone-end
::: zone target="chromeless"

## <a name="onboard-solutionstabconfigure-solutions"></a>[Nasazení řešení](#tab/Configure-solutions)

::: zone-end

Pokud chcete povolit řešení, musíte nakonfigurovat pracovní prostor Log Analytics. Nasazené virtuální počítače Azure a místní servery získají řešení z pracovních prostorů Log Analytics, k nimž jsou připojeny.

Existují dva přístupu k nasazení:

- [Jeden virtuální počítač](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
- [Celé předplatné](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)

Jednotlivé články vás provedou postupem nasazení následujících řešení:

- Update Management
- Change Tracking a Inventory
- Protokol aktivit Azure
- Azure Log Analytics Agent Health
- Posouzení antimalwaru
- Azure Monitor pro virtuální počítače
- Azure Security Center

Každé z výše uvedených řešení vám pomohou zajistit inventarizaci a získání přehledu.
