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
ms.openlocfilehash: 9e6e078859bb580794477328099b66d14009bdca
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221409"
---
# <a name="create-update-schedules"></a>Vytvoření plánů aktualizací

Plány aktualizací můžete spravovat pomocí Azure Portal nebo nových modulů rutin PowerShellu.

Pokud chcete vytvořit plán aktualizace prostřednictvím Azure Portal, přečtěte si téma [Plánování nasazení aktualizace](https://docs.microsoft.com/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

Modul AZ. Automation teď podporuje konfiguraci správy aktualizací pomocí Azure PowerShell. [1.7.0 verzí](https://www.powershellgallery.com/packages/Az/1.7.0) modulu přidává podporu rutiny [New-AzAutomationUpdateManagementAzureQuery](/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0) , která umožňuje používat značky, umístění a uložená hledání ke konfiguraci plánů aktualizací pro flexibilní skupinu počítačů.

## <a name="example-script"></a>Ukázkový skript

Následující ukázkový skript ilustruje použití označování a dotazování k vytvoření dynamických skupin počítačů, na které můžete použít plány aktualizací. Provádí následující akce. Můžete se podívat na implementace konkrétních akcí při vytváření vlastních skriptů.

- Vytvoří plán aktualizace Azure Automation, který spouští každou sobotu v 8:00.
- Vytvoří dotaz pro počítače, které splňují tato kritéria:
  - Nasazené v `westus`umístění `eastus`, nebo `eastus2` v Azure
  - Mít pro ně použitou značkushodnotounastavenouna`Owner``JaneSmith`
  - Mít pro ně použitou značkushodnotounastavenouna`Production``true`
- Použije plán aktualizace na počítače s dotazem a nastaví dvakrát hodinový interval aktualizace.

Před spuštěním ukázkového skriptu se budete muset přihlásit pomocí rutiny [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Po spuštění skriptu budete muset zadat následující informace:

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

## Next steps

See examples of how to implement [common policies in Azure](./common-policies.md) that can help manage your servers.

> [!div class="nextstepaction"]
> [Common policies in Azure](./common-policies.md)
