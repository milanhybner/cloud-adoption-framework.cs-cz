---
title: 'Průvodce inovacemi Azure: Příprava na zpětnou vazbu od zákazníků'
description: Příprava na zpětnou vazbu od zákazníků
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: c78eae75bca30cac541a997fa9d4901b03b277c0
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808358"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Průvodce inovacemi Azure: Příprava na zpětnou vazbu od zákazníků

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Příprava na zpětnou vazbu od zákazníků

::: zone-end

Přijetí uživateli, jejich zapojení i udržení má hlavní vliv na to, zda bude inovace úspěšná. Proč?

Pokud chceme vytvořit nové inovativní řešení, nemůžeme jen dát uživatelům to, co chtějí (nebo co si myslí, že chtějí). Je potřeba zformulovat hypotézu, kterou můžeme otestovat, a na jejímž základě bude možné řešení vylepšovat. Testování je dvojího druhu.

- **Kvantitativní (zpětná vazba z testování):** Tato zpětná vazba měří akce, které chceme vidět.
- **Kvalitativní (zpětná vazba od zákazníků):** Tato zpětná vazba nám slovy zákazníků ukáže, co dané metriky znamenají.

Před integrací smyček zpětné vazby musíte pro své řešení mít sdílené úložiště. Prostřednictvím centralizovaného úložiště budete schopní zaznamenávat veškerou příchozí zpětnou vazbu k vašemu projektu a reagovat na ni. [GitHub](https://github.com) je základna opensourcového softwaru. Představuje také jednu z nejvyužívanějších platforem pro hostování úložišť zdrojového kódu pro komerčně vyvíjené aplikace. Pokud s úložišti začínáte a potřebujete pomoc, zkuste si přečíst článek o [vytváření úložišť GitHub](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml).

Všechny následující nástroje v Azure umožňují integraci (nebo jsou kompatibilní) s projekty hostovanými na GitHubu:

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Kvantitativní zpětná vazba pro webové aplikace](#tab/Quantitative-Apps)

Application Insights je monitorovací nástroj, který téměř v reálném čase poskytuje kvantitativní zpětnou vazbu k využití vašich aplikací. Tato zpětná vazba vám může pomoct s otestováním a ověřením vaší aktuální hypotézy za účelem zformování další funkce nebo uživatelského scénáře v backlogu.

### <a name="action"></a>Akce

Pokud chcete zobrazit kvantitativní data aplikací, postupujte takto:

1. Přejděte do služby **Application Insights**.
   - Pokud se vaše aplikace v seznamu nezobrazí, vyberte **Přidat** a podle zobrazených výzev zahajte konfiguraci služby Application Insights.
   - Pokud je požadovaná aplikace v seznamu uvedená, vyberte ji.
1. V podokně **Přehled** najdete několik statistik o aplikaci. Pokud chcete vytvořit vlastní řídicí panel pro data, která jsou pro vaši hypotézu relevantnější, vyberte **Řídicí panel aplikací**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to Application Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete zobrazit data týkající se vašich aplikací, přejděte na web [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Další informace

- [Nastavení služby Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Začínáme s Application Insights služby Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Vytvoření řídicího panelu telemetrie](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Kvantitativní zpětná vazba pro rozhraní API](#tab/Quantitative-APIs)

Propojená ekonomika mění způsob, jakým podniky provádí inovace. Trhy a jednotlivá odvětví procházejí nebývale rychlými změnami. Tyto změny mají mnoho podob a firmy se tak musí potýkat s takzvaným _inovátorským dilematem_ – jak rychlé tempo pro změny stanovit, aby se nestřetly se stávajícími obchodními aktivitami.

Podniky využívají rozhraní API externě za účelem proměňování interakcí se zákazníky a partnery. Na interní úrovni pak rozhraní API slouží k bezproblémovému propojování různých částí podniku. Ekonomika rozhraní API stojí na čtyřech pilířích: sociální média, mobilní řešení, analytika a cloud. Aplikace a služby je možné rychle a levně propojit a vytvořit tak rozšířenou hodnotovou nabídku.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Pokud chcete zaznamenávat kvantitativní data vašich rozhraní API, postupujte takto:

1. Přejděte na **Služby API Management**.
2. V seznamu vyberte požadované rozhraní API.
3. V části **Monitorování** vyberte **Nastavení diagnostiky**.

Pokud chcete zobrazit kvantitativní data vašich rozhraní API, postupujte takto:

1. Přejděte na **Služby API Management**.
2. V seznamu vyberte požadované rozhraní API.
3. V části **Monitorování** vyberte **Aplikace**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete otevřít služby API Management, přejděte na web [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Další informace

- [Získání zpětné vazby k rozhraním API s využitím služby Azure Monitor](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor)

## <a name="qualitative-feedbacktabqualitative"></a>[Kvalitativní zpětná vazba](#tab/Qualitative)

Zpětná vazba se zaznamenává jako uživatelské scénáře v backlogu (neboli na panelu). Tady můžete také sledovat související práce jako úlohy s praktickým využitím. Azure Boards je možné přímo integrovat do GitHubu, což vám umožní bezproblémovou spolupráci mezi správou zpětné vazby a související práce a libovolným zdrojovým kódem.

::: zone target="docs"

### <a name="action"></a>Akce

Azure Boards a Azure Pipelines vyžadují portál nezávislý na GitHubu a Azure.
Pokud chcete s některým z těchto nástrojů začít, přejděte na [Azure DevOps](https://dev.azure.com).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Pokud chcete vytvořit projekt DevOps, postupujte takto:

1. Přejděte do **Azure DevOps Projects**.
2. Vyberte **Vytvořit projekt DevOps**.
3. Vyberte **Modul runtime, architektura a služba**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Projects" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Další informace

Tyto články vám pomůžou centralizovat a spravovat zpětnou vazbu s využitím Azure Boards a GitHubu:

- [Začínáme se službou Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/?view=azure-devops)
- [Azure Boards a GitHub](https://docs.microsoft.com/azure/devops/boards/github?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Uzavření smyčky pomocí kanálů](#tab/pipelines)

Reakcí na zpětnou vazbu nemusí vždy být přidání funkce, kterou zákazník žádal. Každý datový bod by ale měl vést ke změně. Může se jednat jak o změnu ve vašem myšlení, tak o technickou změnu, která se ale naprosto liší od toho, co bylo požadováno. Prostřednictvím kanálů a nástrojů nasazení, jako je Azure Pipelines, můžete jakékoli změny vždy rychle publikovat a pravidelně je sdílet se zákazníkem.

### <a name="action"></a>Akce

Aktuální nasazení zobrazíte v kanálu takto:

1. Přejděte na **App Services**.
2. V seznamu vyberte požadovanou aplikaci.
3. V části **Nasazení** podokna App Services vyberte **Deployment Center**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete aplikaci zobrazit ve službě App Service, přejděte na web [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Další informace

Začínáme s vytvářením kanálů nasazení:

- [Vytvoření prvního kanálu](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [Úkoly uvolnění v GitHubu](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
