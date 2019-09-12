---
title: Automatizace zprovoznění a konfigurace výstrah
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Automatizace zprovoznění a konfigurace výstrah
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 86997d8c433c23d6ecbe5d3ac124623d318099c0
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833086"
---
# <a name="automate-onboarding"></a>Automatizace připojování

Pro zlepšení efektivity nasazení služeb správy serveru Azure zvažte automatizaci nasazení služeb správy pomocí doporučení popsaných v předchozích částech tohoto návodu. Skript a ukázkové šablony, které jsou k dispozici v následujících částech, představují počáteční body pro vývoj vlastní automatizace procesů připojování.

## <a name="onboarding-by-using-automation"></a>Připojování pomocí automatizace

Tato příručka obsahuje podporu úložiště GitHub Sample Code [CloudAdoptionFramework](https://aka.ms/CAF/manage/automation-samples), která poskytuje ukázkové skripty a šablony pro Azure Resource Manager, které vám pomůžou automatizovat nasazení služby Azure Server Management Services.

Tyto ukázkové soubory ilustrují použití rutin Azure PowerShell k automatizaci následujících úloh:

1. Vytvořte [pracovní prostor Log Analytics](/azure/azure-monitor/platform/manage-access) (nebo použijte existující pracovní prostor, pokud splňuje požadavky&mdash;, viz [plánování pracovního prostoru](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

2. Vytvořte účet Automation (nebo použijte existující účet, pokud splňuje požadavky&mdash;, viz [plánování pracovního prostoru](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

3. Propojit účet Automation s pracovním prostorem Log Analytics (není nutné při připojování prostřednictvím portálu)

4. Povolí Update Management a Change Tracking a inventář pro pracovní prostor.

5. Připojení virtuálních počítačů Azure pomocí Azure Policy (zásada nainstaluje agenta Log Analytics a Dependency Agent na virtuálních počítačích Azure).

6. Připojování místních serverů instalací agenta Log Analytics.

Soubory popsané v následující tabulce se v této ukázce používají a můžete je přizpůsobit tak, aby podporovaly vlastní scénáře nasazení.

| Název souboru | Popis |
|-----------|-------------|
| New-AMSDeployment. ps1 | Hlavní a orchestrující skript, který automatizuje registraci. Tento skript PowerShellu vyžaduje stávající předplatné, ale pokud neexistují, vytvoří se skupiny prostředků, umístění, pracovní prostor a účty Automation. |
| Pracovní prostor – AutomationAccount. JSON | Správce prostředků šablona, která nasazuje pracovní prostor a prostředky účtu služby Automation. |
| WorkspaceSolutions.json | Správce prostředků šablona umožňující vaše požadovaná řešení v pracovním prostoru Log Analytics |
| ScopeConfig.json | Správce prostředků šablona, která používá model výslovných přihlášení pro místní servery s řešením Change Tracking. Použití modelu výslovných výslovných přihlášení je volitelné. |
| Enable-VMInsightsPerfCounters.ps1 | Skript prostředí PowerShell, který umožňuje VMInsight pro servery a nakonfiguruje čítače výkonu. |
| ChangeTracking-Filelist.json | Správce prostředků šablona definující seznam souborů, které budou Change Tracking monitorovány. |

New-AMSDeployment. ps1 můžete spustit pomocí následujícího příkazu:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Další postup

Naučte se, jak nastavit základní výstrahy pro upozorňování týmu na události a problémy správy klíčů.

> [!div class="nextstepaction"]
> [Nastavení základních výstrah](./setup-alerts.md)
