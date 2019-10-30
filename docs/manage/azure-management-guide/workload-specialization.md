---
title: Specializace podle úloh pro správu cloudu v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vylepšete operace správy cloudu specifické pro jednotlivé úlohy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 51bdf23ccb2262202dfa095c5e9b57f727d11d3b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556985"
---
# <a name="workload-specialization-for-cloud-management"></a>Specializace podle úloh pro správu cloudu

Specializace podle úloh je založená na konceptech popsaných v tématu [Specializace podle platformy](./platform-specialization.md).

![Rozšíření směrného plánu správy cloudu](../../_images/manage/beyond-the-baseline.png)

- **Provoz úloh:** Největší investice do provozu jednotlivých úloh. Nejvyšší stupeň odolnosti. Doporučuje se pro přibližně 20 % úloh, které vytvářejí největší obchodní hodnoty. Obvykle je vyhrazené jen pro nejdůležitější úlohy firmy.
- **Provoz platforem:** Investice do provozu se rozloží mezi mnoho úloh. Vylepšení odolnosti mají vliv na všechny úlohy, které využívají určenou platformu. Doporučuje se pro přibližně 20 % nejdůležitějších platforem. Obvykle je vyhrazené pro úlohy střední až vysoké důležitosti.
- **Rozšířený směrný plán správy:** Nejnižší relativní investice do provozu. Mírně vylepšené firemní závazky pomocí dalších nástrojů a procesů pro nativní cloudové operace.

## <a name="high-level-process"></a>Proces na vysoké úrovni

Specializace podle úloh zahrnuje disciplinované provádění následujících čtyř procesů na základě iterativního přístupu. Podrobné vysvětlení jednotlivých procesů najdete v tématu [Specializace podle platformy](./platform-specialization.md).

- **Vylepšení návrhu systémů:** Vylepšete návrh konkrétních úloh a efektivně tak minimalizujte přerušení.
- **Automatizace nápravných opatření:** Některá vylepšení nejsou nákladově efektivní. V takových případech může být vhodnější automatizovat nápravná opatření a snížit dopad přerušení.
- **Škálování řešení:** Po vylepšení návrhu systémů a automatizované nápravy je možné tyto změny škálovat v celém prostředí prostřednictvím katalogu služeb.
- **Průběžné vylepšování:** Pomocí různých nástrojů pro monitorování se dají zjistit přírůstková vylepšení, která můžete řešit při dalším průchodu fázemi navrhování systémů, automatizace a škálování.

## <a name="cultural-change"></a>Kulturní změna

Specializace podle úloh často podněcuje kulturní změnu. IT v tradičním pojetí vytváří procesy zaměřené na směrný plán správy, rozšířené možnosti směrných plánů a provoz platforem. Nabídky spadající do těchto typů lze škálovat v celém prostředí. Specializace podle úloh se ve svém provádění velmi podobá specializaci podle platformy. Na rozdíl od běžných platforem se ale specializace požadovaná jednotlivými úlohami příliš často neškáluje.

V případech, které vyžadují specializaci podle úloh, provozní správa běžně vystoupí mimo rámec perspektivy centrálního IT. Přístup navržený v architektuře přechodu na cloud zahrnuje distribuci funkcí správy cloudu.

V rámci tohoto modelu se provozní úlohy (jako je monitorování, nasazení, DevOps a další funkce zaměřené na inovace) přesunou pod organizaci vývoje aplikací nebo obchodních jednotek. Tým pro cloudovou platformu a hlavní tým pro monitorování cloudu i nadále zajišťují směrný plán správy v rámci celého prostředí. Tyto centralizované týmy také vedou a instruují týmy specializované podle úloh ohledně operací spojených s příslušnými úlohami. Odpovědnost za každodenní provoz ale nese tým pro správu cloudu, jehož řízení nespadá do oblasti IT. Tento typ distribuovaného řízení je jedním z primárních ukazatelů vyspělosti vedoucího centra cloudu.

## <a name="beyond-platform-specialization---application-insights"></a>Nad rámec specializace podle platformy – Application Insights

Aby bylo možné zajistit přesný provoz úloh, je potřeba znát konkrétní úlohy podrobněji. Během fáze průběžného vylepšování se nástroj Application Insights stane nezbytným doplňkem sady nástrojů pro správu cloudu.

|Monitorování aplikace|Application Insights|Monitorování a diagnostika pro aplikace| |Výkon, dostupnost, využití|Application Insights|Pokročilé monitorování aplikací pomocí řídicího panelu aplikace, složených map, využití a trasování|

### <a name="deploy-application-insights"></a>Nasazení služby Application Insights

1. Na webu Azure Portal vyhledejte **Application Insights**.
2. Kliknutím na **+ Přidat** vytvořte prostředek Application Insights pro monitorování živé webové aplikace.
3. Postupujte podle výzev na obrazovce.

Doprovodné materiály ke konfiguraci monitorování aplikace najdete v [centru Application Insights služby Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/azure-monitor-app-hub).

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Monitorování výkonu, dostupnosti a využití

1. Na webu Azure Portal vyhledejte **Application Insights**.
2. V seznamu vyberte jeden z prostředků Application Insights.

V navigaci nástroje Application Insights najdete řadu možností pro monitorování výkonu, dostupnosti, využití a závislostí. Každé z těchto zobrazení dat aplikací vám dá jasnou představu o smyčce zpětné vazby průběžného vylepšování.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
