---
title: Příklady běžných Azure Policy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Příklady běžných Azure Policy
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 40849abab5616343ae49400a126e2d1cf4c0a34f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833255"
---
# <a name="common-azure-policy-examples"></a>Příklady běžných Azure Policy

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) vám může pomáhat při použití zásad správného řízení pro vaše cloudové prostředky. Tato služba vám může přispět k vytváření guardrails, která zajistí dodržování požadavků zásad správného řízení na úrovni společnosti. Zásady vytvoříte pomocí rutin Azure Portal nebo PowerShellu. Tento článek popisuje příklady rutin PowerShellu.

> [!NOTE]
> Při Azure Policy nejsou zásady vynucování (**deployIfNotExists**) automaticky nasazeny do stávajících virtuálních počítačů. Náprava se vyžaduje, aby tyto virtuální počítače zůstaly v souladu s dodržováním předpisů. Další informace najdete v tématu napravení nevyhovujících [prostředků pomocí Azure Policy](https://docs.microsoft.com/en-us/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Příklady běžných zásad

V následujících částech jsou popsány některé běžně používané zásady.

### <a name="restrict-resource-regions"></a>Omezení oblastí prostředků

Právní předpisy a dodržování předpisů budou často záviset na kontrole fyzického umístění, kde jsou prostředky nasazeny. Pomocí integrovaných zásad můžete uživatelům povolit vytváření prostředků jenom v seznamu povolených oblastí Azure. Tuto zásadu můžete najít na portálu tak, že na stránce definice zásad vyhledáte "umístění".

Nebo můžete spustit tuto rutinu a najít zásadu:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*location*") }
```

Následující skript ukazuje, jak přiřadit zásadu. Chcete-li použít skript, změňte `$SubscriptionID` hodnotu tak, aby odkazovala na předplatné, ke kterému chcete zásadu přiřadit. Před spuštěním skriptu se budete muset přihlásit pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) .

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{"listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyparam
```

Stejný skript můžete použít k aplikování dalších zásad popsaných v tomto článku. Stačí nahradit identifikátor GUID na řádku, který je `$AllowedLocationPolicy` nastaven identifikátorem GUID zásady, kterou chcete použít.

### <a name="block-certain-resource-types"></a>Blokovat určité typy prostředků

Další běžná předdefinovaná zásada, která se používá k řízení nákladů, vám umožní blokovat určité typy prostředků. Tuto zásadu můžete najít na portálu tak, že na stránce definice zásad vyhledáte "povolené typy prostředků".

Nebo můžete spustit tuto rutinu a najít zásadu:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

Jakmile určíte zásadu, kterou chcete použít, můžete upravit ukázku prostředí PowerShell v části [omezit oblasti prostředků](#restrict-resource-regions) , aby se zásady přiřazují.

### <a name="restrict-vm-size"></a>Omezení velikosti virtuálního počítače

Azure nabízí rozsáhlou škálu velikostí virtuálních počítačů pro podporu různých typů úloh. K řízení rozpočtu můžete vytvořit zásadu, která umožňuje ve svých předplatných pouze podmnožinu velikostí virtuálních počítačů.

### <a name="deploy-antimalware"></a>Nasazení antimalwarového programu

Pomocí této zásady můžete nasadit rozšíření Microsoft IaaSAntimalware s výchozí konfigurací na virtuální počítače, které nejsou chráněné antimalwarem.

Identifikátor GUID zásad je `2835b622-407b-4114-9198-6f7064cbe0dc`.

Následující skript ukazuje, jak přiřadit zásadu. Chcete-li použít skript, změňte `$SubscriptionID` hodnotu tak, aby odkazovala na předplatné, ke kterému chcete zásadu přiřadit. Před spuštěním skriptu se budete muset přihlásit pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) .

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location “eastus” with the value you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Další kroky

Přečtěte si o dalších dostupných nástrojích a službách pro správu serveru.

> [!div class="nextstepaction"]
> [Služby a nástroje pro správu serveru Azure](./tools-services.md)
