---
title: Provozní dodržování předpisů v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zajištění firemní stability zlepšením provozního dodržování předpisů
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b5a94ab41bff26371621acc5e62ae19d9fd02e5c
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565490"
---
# <a name="operational-compliance-in-azure"></a>Provozní dodržování předpisů v Azure

_Provozní dodržování předpisů_ je druhou disciplínou v jakémkoli směrném plánu cloudové správy.

![Směrný plán cloudové správy](../../_images/manage/management-baseline.png)

Zlepšení provozního dodržování předpisů snižuje pravděpodobnost výpadku souvisejícího s nekonzistentní konfigurací nebo ohrožení zabezpečení souvisejícího se systémy, které jsou nesprávně opraveny.

V této tabulce je pro jednotlivá podniková prostředí uvedeno navrhované minimum pro směrný plán správy.

|Proces  |Nástroj  |Účel  |
|---------|---------|---------|
|Správa oprav|Update Management|Správa a plánování aktualizací|
|Vynucování zásad|Azure Policy|Vynucování zásad pro zajištění dodržování předpisů na úrovni prostředí a hostů|
|Konfigurace prostředí|Azure Blueprint|Automatizované dodržování předpisů pro základní služby|

::: zone target="docs"

## <a name="update-management"></a>Update Management

::: zone-end
::: zone target="chromeless"

## <a name="update-managementtabupdatemanagement"></a>[Správa aktualizací](#tab/UpdateManagement)

::: zone-end

Počítače spravované pomocí Update Managementu používají k provádění posuzovacích a aktualizačních nasazení následující konfigurace:

- Agenta Microsoft Monitoring Agent (MMA) pro Windows nebo Linux
- Konfiguraci požadovaného stavu (DSC) PowerShellu pro Linux
- Azure Automation Hybrid Runbook Worker
- Služby Microsoft Update nebo Windows Server Update Services (WSUS) pro počítače s Windows

Další informace najdete v tématu [Řešení Update Management](https://docs.microsoft.com/azure/automation/automation-update-management).

> [!WARNING]
> Než začnete používat Update Management, musíte do Log Analytics a Azure Automation nasadit virtuální počítače nebo celé předplatné.
>
> Existují dva přístupu k nasazení:
>
> - [Jeden virtuální počítač](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
> - [Celé předplatné](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)
>
> Před pokračováním v práci s řešením Update Management byste měli podle jednoho postupovat.

### <a name="manage-updates"></a>Správa aktualizací

Použití zásady pro skupinu prostředků:

1. Přejděte do služby [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Vyberte **Účty služby Automation** a zvolte jeden z uvedených účtů.
1. Přejděte na **Správu konfigurace**.
1. K řízení stavu a provozního dodržování předpisů spravovaných virtuálních počítačů se dá použít **Inventář**, **Správa změn** a **Konfigurace stavu**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Azure Policy

::: zone-end
::: zone target="chromeless"

## <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

::: zone-end

Azure Policy se používá v rámci procesů zásad správného řízení. Je také vysoce užitečná v rámci procesů správy cloudu. Azure Policy může auditovat a napravovat prostředky Azure a také může auditovat nastavení uvnitř počítače. Ověřování se provádí pomocí rozšíření Konfigurace hosta a prostřednictvím klienta. Toto rozšíření prostřednictvím klienta ověřuje nastavení, jako například:

- Konfigurace operačního systému
- Konfigurace nebo přítomnost aplikací
- Nastavení prostředí

Konfigurace hosta Azure Policy momentálně audituje jenom nastavení uvnitř počítače. Neaplikuje konfigurace.

::: zone target="chromeless"

### <a name="action"></a>Akce

Přiřazení předdefinované zásady ke skupině pro správu, předplatnému nebo skupině prostředků

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

### <a name="apply-a-policy"></a>Použití zásady

Použití zásady pro skupinu prostředků:

1. Přejděte do části [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Vyberte **Přiřadit zásadu**.

### <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Azure Policy – Konfigurace hosta](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration)
- [Architektura přechodu na cloud: Průvodce rozhodováním ohledně vynucování zásad](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprint

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

::: zone-end

Pomocí Azure Blueprints můžou cloudoví architekti a centrální skupiny informačních technologií definovat opakující se sadu prostředků Azure. Tyto prostředky implementují standardy, vzory a požadavky organizace a vyhovují jim.

Pomocí Azure Blueprints můžou vývojové týmy rychle sestavit a vytvořit nová prostředí. Týmy můžou taky důvěřovat, že provádějí sestavení v rámci dodržování předpisů organizace. Využívají k tomu sadu integrovaných komponent, jako jsou sítě, aby urychlili vývoj a doručování.

Podrobné plány představují deklarativní způsob, jak orchestrovat nasazení různých šablon prostředků a dalších artefaktů jako:

- Přiřazení rolí
- Přiřazení zásad
- Šablony Azure Resource Manageru
- Skupiny prostředků

Použitím podrobného plánu je možné vynutit provozní dodržování předpisů v prostředí, pokud toto vynucení neudělal tým zásad správného řízení cloudu.

### <a name="create-a-blueprint"></a>Vytvoření podrobného plánu

Vytvoření podrobného plánu:

::: zone target="chromeless"

1. Přejděte na **Blueprints – Začínáme**.
1. V podokně **Vytvořit podrobný plán** vyberte **Vytvořit**.
1. Vyfiltrujte seznam podrobných plánů a vyberte odpovídající podrobný plán.
1. Do pole **Název podrobného plánu** zadejte název podrobného plánu.
1. Vyberte **Umístění definice** a zvolte příslušné umístění.
1. Vyberte **Další: Artefakty >>** a zkontrolujte artefakty, které jsou součástí podrobného plánu.
1. Vyberte **Uložit koncept**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Přejděte na [Blueprints – Začínáme](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. V podokně **Vytvořit podrobný plán** vyberte **Vytvořit**.
1. Vyfiltrujte seznam podrobných plánů a vyberte odpovídající podrobný plán.
1. Do pole **Název podrobného plánu** zadejte název podrobného plánu.
1. Vyberte **Umístění definice** a zvolte příslušné umístění.
1. Vyberte **Další: Artefakty >>** a zkontrolujte artefakty, které jsou součástí podrobného plánu.
1. Vyberte **Uložit koncept**.

::: zone-end

### <a name="publish-a-blueprint"></a>Publikování podrobného plánu

Publikování artefaktů podrobného plánu v předplatném:

::: zone target="chromeless"

1. Přejděte na **Podrobné plány – Definice podrobných plánů**.
1. Vyberte podrobný plán, který jste vytvořili v předchozích krocích.
1. Zkontrolujte definici podrobného plánu a vyberte **Publikovat podrobný plán**.
1. Do pole **Verze** zadejte verzi, např. „1.0“.
1. Do pole **Poznámky ke změnám** zadejte své poznámky.
1. Vyberte **Publikovat**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Přejděte na [Podrobné plány – Definice podrobných plánů](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Vyberte podrobný plán, který jste vytvořili v předchozích krocích.
1. Zkontrolujte definici podrobného plánu a vyberte **Publikovat podrobný plán**.
1. Do pole **Verze** zadejte verzi, např. „1.0“.
1. Do pole **Poznámky ke změnám** zadejte své poznámky.
1. Vyberte **Publikovat**.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Architektura přechodu na cloud: Průvodce rozhodováním ohledně konzistence prostředků](../../decision-guides/resource-consistency/index.md)
- [Ukázky podrobných plánů založené na standardech](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
