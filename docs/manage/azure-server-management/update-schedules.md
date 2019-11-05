---
title: Vytvoření plánů aktualizací
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vytvoření plánů aktualizací
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5bb3e37073c3c5d7f401f6d6c706314172eecf88
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565268"
---
# <a name="create-update-schedules"></a>Vytvoření plánů aktualizací

Plány aktualizací můžete spravovat pomocí Azure Portal nebo nových modulů rutin PowerShellu.

Pokud chcete vytvořit plán aktualizace prostřednictvím Azure Portal, přečtěte si téma [Plánování nasazení aktualizace](https://docs.microsoft.com/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

Modul AZ. Automation teď podporuje konfiguraci správy aktualizací pomocí Azure PowerShell. [1.7.0 verze](https://www.powershellgallery.com/packages/Az/1.7.0) modulu přidává podporu rutiny [New-AzAutomationUpdateManagementAzureQuery](https://docs.microsoft.com/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0) . Tato rutina vám umožní pomocí značek, umístění a uložených hledání nakonfigurovat plány aktualizací pro flexibilní skupinu počítačů.

## <a name="example-script"></a>Ukázkový skript

Ukázkový skript v této části ukazuje použití značek a dotazování k vytváření dynamických skupin počítačů, na které můžete použít plány aktualizací. Provádí následující akce. Můžete se podívat na implementace konkrétních akcí při vytváření vlastních skriptů.

- Vytvoří plán aktualizace Azure Automation, který spouští každou sobotu v 8:00.
- Vytvoří dotaz pro počítače, které splňují tato kritéria:
  - Nasazené v `westus`, `eastus`nebo `eastus2` umístění Azure
  - Pro ně je použita značka `Owner` s hodnotou nastavenou na `JaneSmith`
  - Pro ně je použita značka `Production` s hodnotou nastavenou na `true`
- Aplikuje plán aktualizace na počítače s dotazem a nastaví dvakrát hodinový interval aktualizace.

Před spuštěním ukázkového skriptu se budete muset přihlásit pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Po spuštění skriptu zadejte následující informace:

- ID cílového předplatného
- Cílová skupina prostředků
- Název vašeho pracovního prostoru Log Analytics
- Název účtu Azure Automation

```powershell

    <#
        .SYNOPSIS
            This script orchestrates the deployment of the solutions and the agents.
        .Parameter SubscriptionName
        .Parameter WorkspaceName
        .Parameter AutomationAccountName
        .Parameter ResourceGroupName

    #>

    param (
        [Parameter(Mandatory=$true)]
        [string]$SubscriptionId,

        [Parameter(Mandatory=$true)]
        [string]$ResourceGroupName,

        [Parameter(Mandatory=$true)]
        [string]$WorkspaceName,

        [Parameter(Mandatory=$true)]
        [string]$AutomationAccountName,

        [Parameter(Mandatory=$false)]
        [string]$scheduleName = "SaturdayCritialSecurity"
    )

    Import-Module Az.Automation

    $startTime = ([DateTime]::Now).AddMinutes(10)
    $schedule = New-AzAutomationSchedule -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -StartTime $startTime `
        -Name $scheduleName `
        -Description "Saturday patches" `
        -DaysOfWeek Saturday `
        -WeekInterval 1 `
        -ForUpdateConfiguration

    # Using AzAutomationUpdateManagementAzureQuery to create dynamic groups.

    $queryScope = @("/subscriptions/$SubscriptionID/resourceGroups/")

    $query1Location =@("westus", "eastus", "eastus2")
    $query1FilterOperator = "Any"
    $ownerTag = @{"Owner"= @("JaneSmith")}
    $ownerTag.add("Production", "true")

    $DGQuery = New-AzAutomationUpdateManagementAzureQuery -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Scope $queryScope `
        -Tag $ownerTag

    $AzureQueries = @($DGQuery)

    $UpdateConfig = New-AzAutomationSoftwareUpdateConfiguration -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Schedule $schedule `
        -Windows `
        -Duration (New-TimeSpan -Hours 2) `
        -AzureQuery $AzureQueries `
        -IncludedUpdateClassification Security,Critical
```

## <a name="next-steps"></a>Další kroky

Podívejte se na příklady implementace [běžných zásad v Azure](./common-policies.md) , které vám pomůžou se správou vašich serverů.

> [!div class="nextstepaction"]
> [Běžné zásady v Azure](./common-policies.md)
