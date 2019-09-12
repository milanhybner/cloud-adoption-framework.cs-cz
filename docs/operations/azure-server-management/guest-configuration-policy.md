---
title: Zásada konfigurace hosta
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zásada konfigurace hosta
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d51cef67c96057b1929ed8cc86396f20338e932b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833216"
---
# <a name="guest-configuration-policy"></a>Zásada konfigurace hosta

Rozšíření [Konfigurace hosta](/azure/governance/policy/concepts/guest-configuration) Azure Policy umožňuje auditovat nastavení konfigurace na virtuálním počítači. Konfigurace hosta se momentálně podporuje jenom na virtuálních počítačích Azure.

Seznam zásad konfigurace hosta můžete najít tak, že na stránce Azure Policyho portálu vyhledáte kategorii "konfigurace hostů". Seznam můžete také najít spuštěním této rutiny v okně PowerShellu:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Funkce konfigurace hosta se pravidelně aktualizuje, aby podporovala další sady zásad. Pravidelně kontrolujte nové podporované zásady a vyhodnoťte, jestli jsou vhodné pro vaše potřeby.

<!-- TODO: Update these links when available. 

By default, we recommend enabling the following policies:

- [Preview]: Audit to verify password security settings are set correctly inside Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Nasazení

K nasazení těchto zásad můžete použít následující ukázkový skript prostředí PowerShell:

- Ověřte, že je správně nastavené nastavení zabezpečení hesla v počítačích se systémem Windows a Linux.
- Ověřte, že se certifikáty na virtuálních počítačích s Windows neblíží vypršení platnosti.

 Před spuštěním tohoto skriptu se budete muset přihlásit pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Po spuštění skriptu budete muset zadat název předplatného, na které chcete zásady použít.

```powershell
#Assign Guest Configuration policy.
param (
    [Parameter(Mandatory=$true)]
    [string]$SubscriptionName
)

$Subscription = Get-AzSubscription -SubscriptionName $SubscriptionName
$scope = "/subscriptions/" + $Subscription.Id

$PasswordPolicy = Get-AzPolicySetDefinition -Name "3fa7cbf5-c0a4-4a59-85a5-cca4d996d5a6"
$CertExpirePolicy = Get-AzPolicySetDefinition -Name "b6f5e05c-0aaa-4337-8dd4-357c399d12ae"

New-AzPolicyAssignment -Name "PasswordPolicy" -DisplayName "[Preview]: Audit that password security settings are set correctly inside Linux and Windows machines" -Scope $scope -PolicySetDefinition $PasswordPolicy -AssignIdentity -Location eastus

New-AzPolicyAssignment -Name "CertExpirePolicy" -DisplayName "[Preview]: Audit that certificates are not expiring on Windows VMs" -Scope $scope -PolicySetDefinition $CertExpirePolicy -AssignIdentity -Location eastus
```

## <a name="next-steps"></a>Další postup

Naučte se, jak [Povolit sledování změn a upozorňování](./enable-tracking-alerting.md) na důležité změny souboru, služby, softwaru a registru.

> [!div class="nextstepaction"]
> [Povolit sledování a upozorňování na kritické změny](./enable-tracking-alerting.md)
