---
title: Specializace podle platformy pro správu cloudu v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vylepšete operace správy cloudu specifické pro jednotlivé platformy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0386a8c30758cce6c1c3d23bfa73d1f90e919692
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556968"
---
# <a name="platform-specialization-for-cloud-management"></a>Specializace podle platformy pro správu cloudu

Podobně jako vylepšený směrný plán správy je specializace podle platformy rozšířením nad rámec standardního směrného plánu správy. Níže se můžete podívat na vizuální odrážkový seznam způsobů, jak se dá směrný plán správy rozšířit. Tento článek se zabývá možností specializace podle platformy.

![Rozšíření směrného plánu správy cloudu](../../_images/manage/beyond-the-baseline.png)

- **Provoz úloh:** Největší investice do provozu jednotlivých úloh. Nejvyšší stupeň odolnosti. Doporučuje se pro přibližně 20 % úloh, které vytvářejí největší obchodní hodnoty. Obvykle je vyhrazené jenom pro nejdůležitější úlohy pro firmu.
- **Provoz platforem:** Investice do provozu se rozloží mezi mnoho úloh. Vylepšení odolnosti mají vliv na všechny úlohy, které využívají definovanou platformu. Doporučuje se pro přibližně 20 % nejdůležitějších platforem. Obvykle je vyhrazené pro úlohy střední až vysoké důležitosti.
- **Vylepšený směrný plán správy:** Nejnižší relativní investice do provozu. Mírně vylepšené firemní závazky pomocí dalších nástrojů a procesů pro nativní cloudové operace.

Pro provoz úloh i platforem budou potřebné změny v principech návrhu a architektury. Tyto změny můžou nějakou dobu trvat a můžou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení firemních závazků.

Následující tabulka popisuje několik běžných procesů, nástrojů a potenciálních dopadů ve vylepšených směrných plánech správy u zákazníků.

|Proces  |Nástroj  |Účel  |Doporučená úroveň správy  |
|---------|---------|---------|---------|
|Vylepšení návrhu systémů|Rozhraní architektury Azure|Vylepšení návrhu architektury platformy za účelem vylepšení provozu|
|Automatizace nápravy|Azure Automation|Reakce na rozšířené údaje o platformě pomocí automatizace specifické pro platformu|Provoz platforem|
|Katalog služeb|Centrum spravovaných aplikací|Poskytnutí samoobslužného katalogu schválených řešení, která vyhovují standardům organizace|Provoz platforem|
|Výkon kontejnerů|Azure Monitor pro kontejnery|Monitorování a diagnostika kontejnerů|Provoz platforem|
|Výkon dat PaaS|Azure SQL Analytics|Monitorování a diagnostika databází PaaS|Provoz platforem|
|Výkon dat IaaS|Kontrola stavu SQL Serveru|Monitorování a diagnostika databází IaaS|Provoz platforem|

## <a name="high-level-process"></a>Proces na vysoké úrovni

Specializace podle platformy zahrnuje disciplinované provádění následujících čtyř procesů v iterativním přístupu. Každý proces je podrobněji vysvětlený v dalších oddílech tohoto článku.

- **Vylepšení návrhu systémů:** Vylepšete návrh běžných systémů (nebo platforem), aby se efektivně minimalizovala přerušení.
- **Automatizace nápravy:** Některá vylepšení nejsou nákladově efektivní. V takových případech může být vhodnější automatizovat nápravu a snížit dopad přerušení.
- **Škálování řešení:** Po vylepšení návrhu systémů a automatizované nápravy je možné tyto změny škálovat v celém prostředí prostřednictvím katalogu služeb.
- **Průběžné vylepšování:** Pomocí různých nástrojů pro monitorování se dají zjistit přírůstková vylepšení, která se můžou řešit při dalším průchodu fázemi navrhování systémů, automatizace a škálování.

::: zone target="docs"

## <a name="improve-system-design"></a>Vylepšení návrhu systémů

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Vylepšení návrhu systémů](#tab/SystemsDesign)

::: zone-end

Vylepšení návrhu systémů představuje nejúčinnější přístup k vylepšení provozu jakékoliv běžné platformy. Díky vylepšením návrhu systémů se může zvýšit stabilita a můžou se snížit přerušení běžného chodu firmy. Návrh jednotlivých systémů je mimo rozsah pohledu na prostředí, který prezentujeme v rámci této řady článků o přechodu na cloud. Jako doplněk k těmto článkům nabízí rozhraní architektury Azure osvědčené postupy pro zlepšení odolnosti a návrhu specifického systému. Tato vylepšení návrhu se dají použít pro návrh systémů platformy nebo konkrétní úlohy.

Rozhraní architektury Azure se zaměřuje na vylepšení pěti pilířů návrhu systémů:

- **Škálovatelnost:** Běžné prostředky platformy se škálují za účelem zvládnutí zvýšené zátěže.
- **Dostupnost:** Zvyšuje se doba provozu a snižují se přerušení běžného chodu firmy.
- **Odolnost:** Vylepšuje se doba zotavení, aby se snížila doba přerušení.
- **Zabezpečení:** Aplikace a data se chrání před externími hrozbami.
- **Správa:** Provádějí se provozní procesy specifické pro běžné prostředky dané platformy.

Většina přerušení běžného chodu firmy vyplývá z určité formy technického dluhu nebo nedostatku v architektuře. U stávajících nasazení se vylepšení návrhu systémů dají vnímat jako splátky technického dluhu. U nových nasazení můžete na vylepšení návrhu systémů nahlížet jako na možnost, jak technickému dluhu předejít. V další části o automatizované nápravě se podíváme na způsoby, jak se vypořádat s technickým dluhem, který se nedá nebo by se neměl řešit.

Přečtěte si také další informace o [rozhraní architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) a vylepšování návrhu systémů.

V průběhu vylepšování návrhu systémů se můžete k tomuto článku vracet a hledat nové příležitosti k vylepšování a škálování těchto vylepšení v celém svém prostředí.

::: zone target="docs"

## <a name="automated-remediation"></a>Automatizovaná náprava

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Automatizovaná náprava](#tab/AutomatedRemediation)

::: zone-end

Některé formy technického dluhu se nedají vyřešit. Řešení by například mohlo být příliš nákladné. Nebo by šlo řešení naplánovat, ale byl by to projekt na příliš dlouhou dobu. Může se stát, že přerušení běžného chodu firmy na ni nemá významný dopad nebo že prioritou firmy je spíše rychlé zotavení než investice do odolnosti.

Pokud vyřešení technického dluhu není požadovaným postupem, je obvykle dalším požadovaným krokem automatizovaná náprava. Ta se obvykle zajišťuje pomocí služeb Azure Automation a Azure Monitor, které detekují trendy a poskytují automatizovanou nápravu.

Další rady k automatizované nápravě najdete v tomto článku o [službě Azure Automation a upozorněních](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Škálování řešení pomocí katalogu služeb

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Škálování řešení pomocí katalogu služeb](#tab/ServiceCatalog)

::: zone-end

Základním kamenem specializace podle platformy a provozu platforem je dobře spravovaný katalog služeb. Jeho prostřednictvím se vylepšení návrhu systémů a nápravy škálují do celého prostředí. Týmy pro cloudové platformy a automatizaci cloudu společně vytvářejí opakovatelná řešení pro nejběžnější platformy v jakémkoliv prostředí. Pokud se ale tato řešení konzistentně nepoužívají, může správa cloudu v podstatě poskytnout jenom nabídku směrného plánu.

Aby se maximalizovalo přijetí jakékoliv optimalizované platformy a minimalizovala se režie spojená s její údržbou, měla by se přidat do katalogu služeb v Azure. Každou aplikaci v katalogu služeb je možné nasadit pro interní použití prostřednictvím katalogu nebo nabídnout externím uživatelům přes Marketplace.

Pokyny k publikování do katalogu služeb najdete v řadě článků o [publikování do katalogu služeb](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Nasazení aplikací z katalogu služeb

1. Na webu Azure Portal vyhledejte **Centrum spravovaných aplikací (Preview)** .
2. V navigaci portálu klikněte v části **Procházet** na **Aplikace katalogu služeb**.
3. Klikněte na **+ Přidat** a zvolte definici aplikace z katalogu služeb vaší společnosti.

Zobrazí se tu veškeré spravované aplikace, které vaše společnost obsluhuje.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Správa aplikací v katalogu služeb

1. Na webu Azure Portal vyhledejte **Centrum spravovaných aplikací (Preview)** .
2. V navigaci portálu klikněte v části **Služba** na **Aplikace katalogu služeb**.

Zobrazí se tu veškeré spravované aplikace, které vaše společnost obsluhuje.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Průběžné vylepšování

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvementtabcontinuousimprovement"></a>[Průběžné vylepšování](#tab/ContinuousImprovement)

::: zone-end

Specializace podle platformy i provoz platforem jsou silně závislé na smyčkách zpětné vazby mezi týmy přechodu, platforem, automatizace a správy. Zhmotnění těchto smyček zpětné vazby v datech umožňuje každému týmu přijímat moudrá rozhodnutí. Aby provoz platforem dosáhl dlouhodobých firemních závazků, je důležité využívat poznatky a přehledy specifické pro centralizovanou platformu. Vzhledem k tomu, že nejběžnějšími centrálně spravovanými platformami jsou kontejnery a SQL Server, nabízíme vám níže několik článků, které vám pomůžou začít se shromažďováním dat za účelem průběžného vylepšování.

[Výkon kontejnerů](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
[Výkon databází PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
[Výkon databází IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
