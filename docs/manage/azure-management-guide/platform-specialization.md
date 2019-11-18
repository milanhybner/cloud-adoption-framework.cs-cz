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
ms.openlocfilehash: 8c3954627ee991f43c2b8d3a94dbd77746d3d4b2
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752936"
---
# <a name="platform-specialization-for-cloud-management"></a>Specializace podle platformy pro správu cloudu

Podobně jako vylepšený směrný plán správy je specializace podle platformy rozšířením nad rámec standardního směrného plánu správy. Následující obrázek a seznam ukazují tři možnosti rozšíření směrného plánu správy. Tento článek se zabývá možnostmi specializace podle platformy.

![Rozšíření směrného plánu správy cloudu](../../_images/manage/beyond-the-baseline.png)

- **Provoz úloh:** Největší investice do provozu na úlohu a nejvyšší stupeň odolnosti. Provoz úloh doporučujeme pro přibližně 20 % úloh, které vytvářejí největší obchodní hodnoty. Tato specializace je obvykle vyhrazená jen pro nejdůležitější úlohy firmy.
- **Provoz platforem:** Investice do provozu se rozloží mezi mnoho úloh. Vylepšení odolnosti mají vliv na všechny úlohy, které využívají definovanou platformu. Doporučujeme provoz platforem pro přibližně 20 % platforem, které jsou nejdůležitější. Tato specializace je obvykle vyhrazená pro úlohy střední až vysoké důležitosti.
- **Vylepšený směrný plán správy:** Relativně nejnižší investice do provozu. Tato specializace mírně vylepšuje firemní závazky pomocí dalších nástrojů a procesů pro nativní cloudové operace.

Pro provoz úloh i platforem jsou potřebné změny v principech návrhu a architektury. Tyto změny mohou nějakou dobu trvat a mohou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení firemních závazků.

Tato tabulka ukazuje několik běžných procesů, nástrojů a potenciálních dopadů ve vylepšených směrných plánech správy u zákazníků.

|Proces  |Nástroj  |Účel  |Navržená úroveň správy  |
|---------|---------|---------|---------|
|Vylepšení návrhu systémů|Rozhraní architektury Azure|Vylepšení návrhu architektury platformy za účelem vylepšení provozu|neuvedeno|
|Automatizace nápravy|Azure Automation|Odezva na rozšířené údaje o platformě s využitím automatizace specifické pro platformu|Provoz platforem|
|Katalog služeb|Centrum spravovaných aplikací|Poskytnutí samoobslužného katalogu schválených řešení, která vyhovují standardům organizace|Provoz platforem|
|Výkon kontejnerů|Azure Monitor pro kontejnery|Monitorování a diagnostika kontejnerů|Provoz platforem|
|Výkon dat architektury PaaS (platforma jako služba)|Azure SQL Analytics|Monitorování a diagnostika databází PaaS|Provoz platforem|
|Výkon dat architektury IaaS (infrastruktura jako služba)|Kontrola stavu SQL Serveru|Monitorování a diagnostika databází IaaS|Provoz platforem|

## <a name="high-level-process"></a>Proces na vysoké úrovni

Specializace podle platformy zahrnuje disciplinované provádění následujících čtyř procesů v iterativním přístupu. Každý proces je podrobněji vysvětlený v dalších oddílech tohoto článku.

- **Vylepšení návrhu systémů:** Vylepšete návrh běžných systémů nebo platforem, aby se efektivně minimalizovala přerušení.
- **Automatizace nápravy:** Některá vylepšení nejsou nákladově efektivní. V takových případech může být vhodnější automatizovat nápravu a snížit dopad přerušení.
- **Škálování řešení:** Po vylepšení návrhu systémů a automatizované nápravy je možné tyto změny škálovat v celém prostředí prostřednictvím katalogu služeb.
- **Průběžné vylepšování:** Ke zjištění přírůstkových vylepšení můžete použít jiné nástroje pro monitorování. Tato vylepšení se dají řešit v dalším kroku návrhu systémů, automatizace a škálování.

::: zone target="docs"

## <a name="improve-system-design"></a>Vylepšení návrhu systémů

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Vylepšení návrhu systémů](#tab/SystemsDesign)

::: zone-end

Vylepšení návrhu systémů představuje nejúčinnější přístup k vylepšení provozu jakékoliv běžné platformy. Díky vylepšením návrhu systémů se může zvýšit stabilita a snížit přerušení běžného chodu firmy. Návrh jednotlivých systémů nespadá do pohledu na prostředí, který v rámci architektury přechodu na cloud pro Azure prezentujeme.

Jako doplněk k těmto článkům nabízí rozhraní architektury Azure osvědčené postupy pro zlepšení odolnosti a návrhu konkrétního systému. Tato vylepšení návrhu se dají použít pro návrh systémů platformy nebo konkrétní úlohy.

Rozhraní architektury Azure se zaměřuje na vylepšení pěti pilířů návrhu systémů:

- **Škálovatelnost:** Škálování běžných prostředků platformy za účelem zvládnutí zvýšené zátěže
- **Dostupnost:** Zvyšování doby provozu a snižování přerušení běžného chodu firmy
- **Odolnost:** Vylepšování doby zotavení, aby se zkrátila doba přerušení
- **Zabezpečení:** Ochrana aplikací a dat před externími hrozbami
- **Správa:** Provozní procesy specifické pro běžné prostředky dané platformy

Většinu přerušení běžného chodu firmy způsobují technické dluhy a chyby architektury. U stávajících nasazení se vylepšení návrhu systémů dají vnímat jako splátky technického dluhu. U nových nasazení na ně můžeme pohlížet jako na způsob, jak se technickým dluhům vyhnout.

Následující karta **Automatizovaná náprava** ukazuje způsoby, jak se vypořádat s technickým dluhem, který se nedá nebo by se neměl řešit.

Přečtěte si také další informace o [rozhraní architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) a vylepšování návrhu systémů.

V průběhu vylepšování návrhu systémů se můžete k tomuto článku vracet a hledat nové příležitosti k vylepšování a škálování těchto vylepšení v celém svém prostředí.

::: zone target="docs"

## <a name="automated-remediation"></a>Automatizovaná náprava

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Automatizovaná náprava](#tab/AutomatedRemediation)

::: zone-end

Některé formy technického dluhu se nedají vyřešit. Řešení by například mohlo být příliš nákladné nebo by šlo naplánovat, ale byl by to projekt na příliš dlouhou dobu. Je možné, že přerušení běžného chodu nemá významný obchodní dopad. Nebo že prioritou firmy je spíše rychlé zotavení než investice do odolnosti.

Pokud vyřešení technického dluhu není požadovaným postupem, je obvykle dalším požadovaným krokem automatizovaná náprava. Ta se obvykle zajišťuje pomocí služeb Azure Automation a Azure Monitor, které detekují trendy a poskytují automatizovanou nápravu.

Další rady k automatizované nápravě najdete v tématu věnovaném [upozorněním a službě Azure Automation](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Škálování řešení pomocí katalogu služeb

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Škálování řešení pomocí katalogu služeb](#tab/ServiceCatalog)

::: zone-end

Základem specializace podle platformy a provozu platforem je dobře spravovaný katalog služeb. Jeho prostřednictvím se vylepšení návrhu systémů a nápravy škálují do celého prostředí.

Týmy pro cloudové platformy a automatizaci cloudu společně vytvářejí opakovatelná řešení pro nejběžnější platformy v jakémkoliv prostředí. Pokud se ale tato řešení konzistentně nepoužívají, může správa cloudu v podstatě poskytnout jenom nabídku směrného plánu.

Aby se maximalizovalo přijetí jakékoliv optimalizované platformy a minimalizovala se režie spojená s její údržbou, měli byste tuto platformu doplnit do katalogu služeb v Azure. Každou aplikaci v katalogu služeb je možné nasadit pro interní použití prostřednictvím katalogu nebo nabídnout externím uživatelům přes Marketplace.

Pokyny k publikování do katalogu služeb najdete v řadě článků o [publikování do katalogu služeb](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Nasazení aplikací z katalogu služeb

1. Na webu Azure Portal přejděte do **Centra spravovaných aplikací (Preview)** .
2. V podokně **Procházet** vyberte **Aplikace katalogu služeb**.
3. Klikněte na **+ Přidat** a zvolte definici aplikace z katalogu služeb vaší společnosti.

Zobrazí se tu veškeré spravované aplikace, které vaše společnost obsluhuje.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Správa aplikací v katalogu služeb

1. Na webu Azure Portal přejděte do **Centra spravovaných aplikací (Preview)** .
1. V podokně **Služba** vyberte **Aplikace katalogu služeb**.

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

Specializace podle platformy i provoz platforem jsou silně závislé na smyčkách zpětné vazby mezi týmy přechodu, platforem, automatizace a správy. Zhmotnění těchto smyček zpětné vazby v datech pomáhá každému týmu v přijímání moudrých rozhodnutí. Aby provoz platforem dosáhl dlouhodobých firemních závazků, je důležité využívat poznatky a přehledy specifické pro centralizovanou platformu.

Dvěma nejčastějšími centrálně spravovanými platformami jsou kontejnery a SQL Server. Tyto články vám pomůžou začít se shromažďováním dat pro průběžné vylepšování na těchto platformách:

- [Výkon kontejnerů](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Výkon databází PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Výkon databází IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
