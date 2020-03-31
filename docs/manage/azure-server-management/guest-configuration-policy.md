---
title: Zásada konfigurace hosta
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak pomocí rozšíření konfigurace hosta Azure Policy auditovat nastavení konfigurace ve virtuálním počítači Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2dd8bd0ff7c991fd2141a3bfa44581e5c3e4af42
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434111"
---
# <a name="guest-configuration-policy"></a>Zásada konfigurace hosta

Pomocí rozšíření [Konfigurace hosta](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) Azure Policy můžete auditovat nastavení konfigurace na virtuálním počítači. Konfigurace hosta se momentálně podporuje jenom na virtuálních počítačích Azure.

Seznam zásad konfigurace hosta najdete tak, že na stránce Azure Policyového portálu vyhledáte "konfigurace hosta". Nebo spuštěním této rutiny v okně PowerShellu Najděte seznam:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Funkce konfigurace hosta se pravidelně aktualizuje, aby podporovala další sady zásad. Pravidelně kontrolujte nové podporované zásady a vyhodnoťte, jestli budou užitečné.

<!-- TODO: Update these links when available. 

By default, we recommend that you enable the following policies:

- [Preview]: Audit to verify that password-security settings are correct on Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Nasazení

Pomocí následujícího ukázkového skriptu PowerShellu nasaďte tyto zásady na:

- Ověřte, že je správně nastavené nastavení zabezpečení hesla v počítačích se systémem Windows a Linux.
- Ověřte, že se certifikáty na virtuálních počítačích s Windows neblíží vypršení platnosti.

 Před spuštěním tohoto skriptu se přihlaste pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Po spuštění skriptu musíte zadat název předplatného, na které chcete zásady použít.

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

## <a name="next-steps"></a>Další kroky

Naučte se, jak [Povolit sledování změn a upozorňování](./enable-tracking-alerting.md) na důležité změny souboru, služby, softwaru a registru.

> [!div class="nextstepaction"]
> [Povolit sledování a upozorňování na kritické změny](./enable-tracking-alerting.md)
