---
title: Automatizace připojování
description: Pomocí ukázkových souborů k registraci můžete zvážit automatizaci nasazení služby Azure Server Management Services, aby se zlepšila efektivita.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4281638b7badf9b672ba3a38d2daa847b7604e7e
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356388"
---
# <a name="automate-onboarding"></a>Automatizace připojování

Pro zlepšení efektivity nasazení služeb správy serveru Azure zvažte možnost automatizace nasazení, jak je popsáno v předchozích částech tohoto návodu. Skript a ukázkové šablony, které jsou uvedené v následujících oddílech, představují počáteční body pro vývoj vlastní automatizace procesů připojování.

V těchto pokynech se podporuje úložiště GitHub s ukázkovým kódem, [CloudAdoptionFramework](https://aka.ms/caf/manage/automation-samples). Úložiště poskytuje příklady skriptů a šablon Azure Resource Manager, které vám pomůžou automatizovat nasazení služeb Azure Server Management Services.

Ukázkové soubory ukazují, jak používat rutiny Azure PowerShell k automatizaci následujících úloh:

- Vytvořte [pracovní prostor Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access). (Nebo použijte existující pracovní prostor, pokud splňuje požadavky. Podrobnosti najdete v tématu [plánování pracovních prostorů](./prerequisites.md#log-analytics-workspace-and-automation-account-planning).

- Vytvořte účet Automation. (Nebo použijte existující účet, pokud splňuje požadavky. Podrobnosti najdete v tématu [plánování pracovních prostorů](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

- Propojte účet Automation s pracovním prostorem Log Analytics. Pokud se připojujete pomocí Azure Portal, tento krok není povinný.

- Pro pracovní prostor povolte Update Management a Change Tracking a inventář.

- Zprovoznění virtuálních počítačů Azure pomocí Azure Policy. Zásada nainstaluje agenta Log Analytics a Microsoft Dependency Agent na virtuální počítače Azure.

- Připojování místních serverů instalací agenta Log Analytics.

V této ukázce se používají soubory popsané v následující tabulce. Můžete je přizpůsobit tak, aby podporovaly vlastní scénáře nasazení.

| Název souboru | Popis |
|-----------|-------------|
| New-AMSDeployment. ps1 | Hlavní a orchestrující skript, který automatizuje registraci. Vytvoří skupiny prostředků a účty umístění, pracovního prostoru a Automation, pokud už neexistují. Tento skript PowerShellu vyžaduje stávající předplatné. |
| Pracovní prostor – AutomationAccount. JSON | Správce prostředků šablona, která nasazuje pracovní prostor a prostředky účtu služby Automation. |
| WorkspaceSolutions.json | Správce prostředků šablona umožňující požadovaná řešení v pracovním prostoru Log Analytics |
| ScopeConfig.json | Správce prostředků šablona, která používá model výslovných přihlášení pro místní servery s řešením Change Tracking. Použití modelu výslovných výslovných přihlášení je volitelné. |
| Enable-VMInsightsPerfCounters.ps1 | PowerShellový skript, který umožňuje přehledy virtuálních počítačů pro servery a nakonfiguruje čítače výkonu. |
| Sledování změn ve-FileList. JSON | Správce prostředků šablona definující seznam souborů, které budou Change Tracking monitorovány. |

Pomocí následujícího příkazu spusťte New-AMSDeployment. ps1:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Další kroky

Naučte se, jak nastavit základní výstrahy pro upozorňování týmu na události a problémy správy klíčů.

> [!div class="nextstepaction"]
> [Nastavení základních výstrah](./setup-alerts.md)
