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
ms.openlocfilehash: 7073df6b697da49429d4086d9f8f3f113583e52d
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557087"
---
# <a name="operational-compliance-in-azure"></a>Provozní dodržování předpisů v Azure

Provozní dodržování předpisů je druhou disciplínou v jakémkoli směrném plánu cloudové správy.

![Směrný plán cloudové správy](../../_images/manage/management-baseline.png)

Zlepšení provozního dodržování předpisů snižuje pravděpodobnost výpadku souvisejícího s nekonzistentní konfigurací nebo ohrožení zabezpečení souvisejícího se systémy, které nejsou správně opraveny.

Pro jakékoli podnikové prostředí je v následující tabulce uvedeno navrhované minimum pro všechny směrné plány správy.

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
- Funkci Hybrid Runbook Worker služby Automation
- Služby Microsoft Update nebo Windows Server Update Services (WSUS) pro počítače s Windows

Další informace najdete v tématu [Řešení Update Management](https://docs.microsoft.com/azure/automation/automation-update-management).

> [!WARNING]
> Než začnete používat správu aktualizací, musíte do Log Analytics a Azure Automation nasadit (angl. „onboard“) virtuální počítače nebo celé předplatné.
> U onboardingu existují dva přístupy – jednoho z nich byste se měli držet, než budete se správou aktualizací pokračovat:
>
> - [Jeden virtuální počítač](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
> - [Celé předplatné](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)

### <a name="manage-updates"></a>Správa aktualizací

Použití zásady pro skupinu prostředků:

1. Přejděte na [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Vyberte jeden z uvedených **účtů služby Automation**.
3. V navigaci na portálu najděte část **Správa konfigurace**.
4. K řízení stavu a provozního dodržování předpisů spravovaných virtuálních počítačů se dá použít Inventář, Správa změn a Konfigurace stavu.

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

Azure Policy se používá v rámci procesů zásad správného řízení. Je ale také vysoce užitečná v rámci procesů správy cloudu. Kromě auditování a napravování prostředků Azure může Azure Policy auditovat nastavení uvnitř počítače. Ověřování se provádí pomocí rozšíření Konfigurace hosta a prostřednictvím klienta. Toto rozšíření prostřednictvím klienta ověřuje nastavení, jako například:

- Konfigurace operačního systému
- Konfigurace nebo přítomnost aplikací
- Nastavení prostředí

Konfigurace hosta Azure Policy momentálně jenom audituje nastavení uvnitř počítače. Neaplikuje konfigurace.

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

Azure Blueprints umožňuje cloudovým architektům a centrálním oddělením IT definovat opakovatelnou sadu prostředků Azure, která implementuje a dodržuje standardy, vzory a požadavky organizace. Vývojářským týmům Azure Blueprints umožňuje rychle vytvářet nová prostředí s důvěrou, že je vytvářejí v souladu s předpisy organizace, a s využitím sady předdefinovaných komponent – třeba síťových – ke zrychlení vývoje a distribuce.

Podrobné plány představují deklarativní způsob, jak orchestrovat nasazení různých šablon prostředků a dalších artefaktů jako:

- Přiřazení rolí
- Přiřazení zásad
- Šablony Azure Resource Manageru
- Skupiny prostředků

Použitím podrobného plánu je možné vynutit provozní dodržování předpisů v prostředí, pokud to ještě neudělal tým zásad správného řízení cloudu.

### <a name="create-a-blueprint"></a>Vytvoření podrobného plánu

Vytvoření podrobného plánu:

::: zone target="chromeless"

1. Přejděte na **Blueprints – Začínáme**.
1. V části **Vytvořit podrobný plán** vyberte **Vytvořit**.
1. Vyfiltrujte seznam podrobných plánů a vyberte odpovídající podrobný plán.
1. Zadejte **Název podrobného plánu** a vyberte odpovídající **Umístění definice**.
1. Klikněte na **Další: Artefakty >>** a zkontrolujte artefakty, které jsou součástí podrobného plánu.
1. Klikněte na **Uložit koncept**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Přejděte na [Blueprints – Začínáme](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. V části **Vytvořit podrobný plán** vyberte **Vytvořit**.
1. Vyfiltrujte seznam podrobných plánů a vyberte odpovídající podrobný plán.
1. Zadejte **Název podrobného plánu** a vyberte odpovídající **Umístění definice**.
1. Klikněte na **Další: Artefakty >>** a zkontrolujte artefakty, které jsou součástí podrobného plánu.
1. Klikněte na **Uložit koncept**.

::: zone-end

### <a name="publish-a-blueprint"></a>Publikování podrobného plánu

Publikování artefaktů podrobného plánu v předplatném:

::: zone target="chromeless"

1. Přejděte na **Blueprints – Definice podrobných plánů**.
1. Vyberte podrobný plán, který jste vytvořili v předchozích krocích.
1. Zkontrolujte definici podrobného plánu a vyberte **Publikovat podrobný plán**.
1. Zadejte číslo **Verze** (například 1.0) a případné **Poznámky ke změnám** a pak vyberte **Publikovat**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Přejděte na [Blueprints – Definice podrobných plánů](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Vyberte podrobný plán, který jste vytvořili v předchozích krocích.
1. Zkontrolujte definici podrobného plánu a vyberte **Publikovat podrobný plán**.
1. Zadejte číslo **Verze** (například 1.0) a případné **Poznámky ke změnám** a pak vyberte **Publikovat**.

### <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Architektura přechodu na cloud: Průvodce rozhodováním ohledně konzistence prostředků](../../decision-guides/resource-consistency/index.md)
- [Ukázky podrobných plánů založené na standardech](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
