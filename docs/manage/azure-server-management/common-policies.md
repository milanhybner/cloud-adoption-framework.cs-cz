---
title: Příklady běžných Azure Policy
description: Pomocí architektury cloudového prostředí pro Azure zajistíte dodržování požadavků zásad správného řízení vytvořením zásad pomocí rutin PowerShellu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: cdaf9eaba2c7f8df6430dc3ef359e146515437fb
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356407"
---
# <a name="common-azure-policy-examples"></a>Příklady běžných Azure Policy

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) vám může pomáhat při použití zásad správného řízení pro vaše cloudové prostředky. Tato služba vám může přispět k vytváření guardrails, která zajistí dodržování požadavků zásad správného řízení na úrovni společnosti. Zásady vytvoříte pomocí rutin Azure Portal nebo PowerShellu. Tento článek popisuje příklady rutin PowerShellu.

> [!NOTE]
> Při Azure Policy nejsou zásady vynucování (**deployIfNotExists**) automaticky nasazeny do stávajících virtuálních počítačů. Náprava se vyžaduje, aby byly virtuální počítače v souladu s předpisy. Další informace najdete v tématu [napravení nevyhovujících prostředků pomocí Azure Policy](https://docs.microsoft.com/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Příklady běžných zásad

V následujících částech jsou popsány některé běžně používané zásady.

### <a name="restrict-resource-regions"></a>Omezení oblastí prostředků

Právní předpisy a dodržování zásad často závisí na kontrole fyzického umístění, kde jsou prostředky nasazeny. Pomocí předdefinovaných zásad můžete uživatelům povolit vytváření prostředků jenom v určitých povolených oblastech Azure.

Tuto zásadu na portálu najdete tak, že na stránce definice zásad vyhledáte "umístění". Nebo spuštěním této rutiny vyhledejte zásadu:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*location*") }
```

Následující skript ukazuje, jak přiřadit zásadu. Změňte hodnotu `$SubscriptionID` tak, aby odkazovala na předplatné, ke kterému chcete zásadu přiřadit. Před spuštěním skriptu se přihlaste pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) .

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{"listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyParam
```

Tento skript můžete použít také k použití dalších zásad, které jsou popsány v tomto článku. Stačí nahradit GUID na řádku, který nastaví `$AllowedLocationPolicy` identifikátorem GUID zásady, kterou chcete použít.

### <a name="block-certain-resource-types"></a>Blokovat určité typy prostředků

K blokování určitých typů prostředků se taky dá použít další společná předdefinovaná zásada, která se používá k řízení nákladů.

Pokud chcete najít tuto zásadu na portálu, vyhledejte na stránce definice zásad "povolené typy prostředků". Nebo spuštěním této rutiny vyhledejte zásadu:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

Jakmile určíte zásadu, kterou chcete použít, můžete upravit ukázku prostředí PowerShell v části [omezit oblasti prostředků](#restrict-resource-regions) , aby se zásady přiřazují.

### <a name="restrict-vm-size"></a>Omezení velikosti virtuálního počítače

Azure nabízí rozsáhlou škálu velikostí virtuálních počítačů pro podporu různých úloh. K řízení rozpočtu můžete vytvořit zásadu, která umožňuje ve svých předplatných pouze podmnožinu velikostí virtuálních počítačů.

### <a name="deploy-antimalware"></a>Nasazení antimalwarového programu

Pomocí této zásady můžete nasadit rozšíření Microsoft *IaaSAntimalware* s výchozí konfigurací na virtuální počítače, které nejsou chráněné antimalwarem.

Identifikátor GUID zásad je `2835b622-407b-4114-9198-6f7064cbe0dc`.

Následující skript ukazuje, jak přiřadit zásadu. Chcete-li použít skript, změňte hodnotu `$SubscriptionID` tak, aby odkazovala na předplatné, ke kterému chcete zásadu přiřadit. Před spuštěním skriptu se přihlaste pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) .

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location "eastus" with the value that you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Další kroky

Seznamte se s dalšími dostupnými nástroji a službami pro správu serveru.

> [!div class="nextstepaction"]
> [Služby a nástroje pro správu serveru Azure](./tools-services.md)
