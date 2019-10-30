---
title: 'Průvodce inovacemi Azure: Příprava na zpětnou vazbu od zákazníků'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Příprava na zpětnou vazbu od zákazníků
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: ec17c66fa92abc292a19a8e74c215111d8638a05
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769370"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Průvodce inovacemi Azure: Příprava na zpětnou vazbu od zákazníků

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Příprava na zpětnou vazbu od zákazníků

::: zone-end

Přijetí uživateli, jejich zapojení i udržení má hlavní vliv na to, zda bude inovace úspěšná. Proč?

Pokud chceme vytvořit nové a inovativní řešení, nemůžeme jen dát zákazníkovi to, co chce (nebo co si myslí, že chce). Je potřeba zformulovat hypotézu, kterou můžeme otestovat, a na jejímž základě bude možné řešení vylepšovat. Testování je dvojího druhu. Kvantitativní testování (zpětná vazba z testování) představuje akce, které chceme vidět. Kvalitativní testování (zpětná vazba od zákazníků) nám pak slovy zákazníků ukáže, co dané metriky znamenají. Společně pak formují další hypotézu a další vylepšování řešení. V jádru této metodologie představují takové smyčky zpětné vazby základ [procesu sestavení, vyhodnocení a poučení](../considerations/adoption.md).

Ještě než se pustíte do integrace smyček zpětné vazby, je nezbytně nutné vytvořit pro vaše řešení sdílené úložiště. Prostřednictvím centralizovaného úložiště budete schopní zaznamenávat veškerou příchozí zpětnou vazbu a reagovat na ni.  [GitHub](https://github.com/) je základna opensourcového softwaru. Představuje také jednu z nejvyužívanějších platforem pro hostování úložiště zdrojového kódu sloužícího komerčně vyvíjeným aplikacím. Pokud s úložišti začínáte a potřebujete pomoc, zkuste si přečíst článek o [vytváření úložišť v GitHubu](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml).

Všechny níže uvedené nástroje Azure umožňují integraci (nebo kompatibilitu) s projekty hostovanými v GitHubu:

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Kvantitativní zpětná vazba pro webové aplikace](#tab/Quantitative-Apps)

Application Insights je monitorovací nástroj, který vám v téměř reálném čase umožňuje provádět kvantitativní zpětnou vazbu o využití vašich aplikací. Tuto zpětnou vazbu potom můžete použít k testování a ověřování aktuální hypotézy za účelem formování další funkce nebo uživatelského scénáře v backlogu.

### <a name="action"></a>Akce

Pokud chcete zobrazit kvantitativní data aplikací, postupujte takto:

1. Přejděte na **App Insights**.
2. Pokud aplikaci nevidíte v seznamu, klikněte na odkaz **Přidat +** a postupujte podle výzev, pomocí kterých zahájíte konfiguraci nástroje App Insights.
3. Pokud se požadovaná aplikace nachází v seznamu, vyberte ji.
4. V podokně **Přehled** najdete několik statistik o aplikaci. Pomocí odkazu **Řídicí panel aplikací** můžete vytvořit vlastní řídicí panel pro prohlížení dat, která jsou pro vaši hypotézu relevantní.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to App Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete zobrazit data týkající se vašich aplikací, přejděte na web [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Další informace

- [Nastavení služby Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Začínáme s App Insights služby Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Vytvoření řídicího panelu telemetrie](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Kvantitativní zpětná vazba pro rozhraní API](#tab/Quantitative-APIs)

Propojená ekonomika mění způsob, jakým podniky provádí inovace.  Trhy a jednotlivá odvětví procházejí nebývale rychlými změnami. Tyto změny mají mnoho podob a firmy se tak musí potýkat s takzvaným **inovátorským dilematem** – jak rychlé tempo pro změny stanovit, aby se nestřetly se stávajícími obchodními aktivitami.

Podniky využívají rozhraní API externě za účelem proměňování interakcí se zákazníky a jejich partnery. Na interní úrovni pak rozhraní slouží k hladkému propojování jejich jednotlivých částí. Ekonomika rozhraní API stojí na čtyřech pilířích: sociální média, mobilní řešení, analytika a cloud. Aplikace a služby je možné rychle a levně propojit a vytvořit tak rozšířenou hodnotovou nabídku.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Pokud chcete zaznamenávat kvantitativní data vašich rozhraní API, postupujte takto:

1. Přejděte do **služby API Management**.
2. V seznamu vyberte požadované rozhraní API.
3. V části **Monitorování** vyberte **Nastavení diagnostiky**.

Pokud chcete zobrazit kvantitativní data vašich rozhraní API, postupujte takto:

1. Přejděte do **služby API Management**.
2. V seznamu vyberte požadované rozhraní API.
3. V části **Monitorování** vyberte **Aplikace**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete otevřít službu API Management, přejděte na web [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Další informace

Přečtěte si článek, ve kterém se dozvíte, [jak pomocí služby Azure Monitor získat zpětnou vazbu k rozhraním API](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor).

## <a name="qualitative-feedbacktabqualitative"></a>[Kvalitativní zpětná vazba](#tab/Qualitative)

Zpětná vazba se zaznamenává jako uživatelské scénáře v backlogu (neboli na panelu). Zde můžete také sledovat související práce jako úlohy s praktickým využitím. Funkci Azure Boards je možné přímo integrovat do GitHubu, což vám umožní bezproblémovou spolupráci mezi správou zpětné vazby a související práce a libovolným zdrojovým kódem.

::: zone target="docs"

### <a name="action"></a>Akce

Azure Boards a Azure Pipelines vyžadují portál nezávislý na GitHubu a Azure.
Pokud chcete s některým z těchto nástrojů začít, přejděte na [Azure DevOps](https://dev.azure.com/).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Pokud chcete vytvořit projekt DevOps, postupujte takto:

1. Přejděte na **projekt Azure DevOps**.
2. Klikněte a **Vytvořit projekt DevOps**.
3. Zvolte **Modul runtime, architektura a služba**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Project" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Další informace

Odkazy níže vám pomůžou centralizovat a spravovat zpětnou vazbu s využitím spojení Azure Boards s GitHubem:

- [Začínáme se službou Azure Boards](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)
- [Azure Boards a GitHub](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Uzavření smyčky pomocí kanálů](#tab/pipelines)

Reakce na zpětnou vazbu nemusí vždy přinést funkci, kterou zákazník žádal. Každý datový bod by ale měl vést ke změně. Může se jednat jak o posun ve vašem myšlení, tak o technickou změnu, která se ale naprosto liší od toho, co bylo požadováno. Prostřednictvím kanálů a nástrojů nasazení, jako je Azure Pipelines, můžete jakékoli změny vždy rychle publikovat a pravidelně je sdílet se zákazníkem.

Postup zobrazení aktivních nasazení souvisejících s vašimi aplikacemi hostovanými v Azure je následující:

### <a name="action"></a>Akce

Aktuální nasazení zobrazíte v kanálu takto:

1. Přejděte na **App Service**.
2. V seznamu vyberte požadovanou aplikaci.
3. V části **Nasazení** podokna App Services zvolte **Deployment Center**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Pokud chcete aplikaci zobrazit ve službě App Service, přejděte na web [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Další informace

Následující odkazy vám pomůžou začít s vytvářením kanálů nasazení:

- [Vytvoření prvního kanálu](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [Úkoly uvolnění v GitHubu](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
