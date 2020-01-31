---
title: Nástroje pro konzistenci prostředků v Azure
description: Nástroje pro konzistenci prostředků v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a2f553285f9d44085cc816c2db34f76fcb02235d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805179"
---
# <a name="resource-consistency-tools-in-azure"></a>Nástroje pro konzistenci prostředků v Azure

[Konzistence prostředků](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na způsoby vytváření zásad souvisejících s provozní správou prostředí, aplikací nebo úloh. V pěti oborech zásad správného řízení cloudu zahrnuje obor konzistence prostředků monitorování aplikací, úloh a výkonu prostředků. Zahrnuje také úlohy, které jsou potřeba pro splnění požadavků na škálování, napravení narušení SLA výkonu a proaktivní zamezení narušení SLA výkonu prostřednictvím automatizované nápravy.

Následuje seznam nástrojů Azure, které mohou pomoci při vyspělosti zásad a procesů, které podporují tento obor řízení.

| Nástroj | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Nasazení prostředků                             | Ano | Ano | Ano | Ano | Ne  | Ne | Ne |
| Správa prostředků                             | Ano | Ano | Ano | Ano | Ne  | Ne | Ne |
| Nasazení prostředků pomocí šablon             | Ne  | Ano | Ne  | Ano | Ne  | Ne | Ne |
| Nasazení orchestrace prostředí          | Ne  | Ne  | Ano | Ne  | Ne  | Ne | Ne |
| Definování skupin prostředků                       | Ano | Ano | Ano | Ne  | Ne  | Ne | Ne |
| Správa úloh a vlastníků účtů           | Ano | Ano | Ano | Ne  | Ne  | Ne | Ne |
| Správa podmíněného přístupu k prostředkům       | Ano | Ano | Ano | Ne  | Ne  | Ne | Ne |
| Konfigurace uživatelů RBAC                         | Ano | Ne  | Ne  | Ne  | Ano | Ne | Ne |
| Přiřazení rolí a oprávnění k prostředkům | Ano | Ano | Ano | Ne  | Ano | Ne | Ne |
| Definování závislostí mezi prostředky        | Ne  | Ano | Ano | Ne  | Ne  | Ne | Ne |
| Použít řízení přístupu                         | Ano | Ano | Ano | Ne  | Ano | Ne | Ne |
| Posouzení dostupnosti a škálovatelnosti          | Ne  | Ne  | Ne  | Ano | Ne  | Ne | Ne |
| Použití značek u prostředků                      | Ano | Ano | Ano | Ne  | Ne  | Ne | Ne |
| Přiřadit pravidla Azure Policy                    | Ano | Ano | Ano | Ne  | Ne  | Ne | Ne |
| Použít automatizovanou nápravu                  | Ne  | Ne  | Ne  | Ano | Ne  | Ne | Ne |
| Správa fakturace                               | Ano | Ne  | Ne  | Ne  | Ne  | Ne | Ne |
| Plánování prostředků pro zotavení po havárii         | Ano | Ano | Ano | Ne  | Ne  | Ano | Ano |
|Obnovení dat během výpadku nebo porušení SLA     | Ne | Ne  | Ne  | Ne  | Ne  | Ano | Ano |
|Obnovení aplikací a dat během výpadku nebo porušení SLA     | Ne | Ne  | Ne  | Ne  | Ne  | Ano | Ano |

Spolu s těmito nástroji a funkcemi pro konzistenci prostředků budete muset monitorovat nasazené prostředky pro problémy s výkonem a stavem. [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) je výchozím řešením monitorování a vytváření sestav v Azure. Azure Monitor poskytuje funkce pro monitorování vašich cloudových prostředků. V tomto seznamu se dozvíte, která funkce řeší běžné požadavky na monitorování.

| Nástroj | [Azure Portal](https://azure.microsoft.com/features/azure-portal) | [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) | [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview) | [Rozhraní REST API pro Azure Monitor](https://docs.microsoft.com/rest/api/monitor) |
|----------------------------------------------------|--------------|----------------------|---------------|------------------------|
| Protokolovat data telemetrie virtuálních počítačů                 | Ne           | Ne                   | Ano           | Ne                     |
| Protokolovat data telemetrie virtuální sítě              | Ne           | Ne                   | Ano           | Ne                     |
| Data telemetrie služby log PaaS Services                   | Ne           | Ne                   | Ano           | Ne                     |
| Protokolování dat telemetrie aplikace                     | Ne           | Ano                  | Ne            | Ne                     |
| Konfigurace sestav a výstrah                       | Ano          | Ne                   | Ne            | Ano                    |
| Plánování běžných sestav nebo vlastní analýzy        | Ne           | Ne                   | Ne            | Ne                     |
| Vizualizace a analýza dat protokolů a výkonu     | Ano          | Ne                   | Ne            | Ne                     |
| Integrace s místním nasazením nebo řešením monitorování třetích stran     | Ne           | Ne                   | Ne            | Ano                    |

Při plánování nasazení budete muset zvážit, kde jsou uložená data protokolování a jak integrovat cloudové [služby vytváření sestav a monitorování](../../decision-guides/logging-and-reporting/index.md) s vašimi stávajícími procesy a nástroji.

> [!NOTE]
> Organizace také používají nástroje DevOps třetích stran ke sledování úloh a prostředků. Další informace najdete v tématu [integrace nástrojů DevOps](https://azure.microsoft.com/products/devops-tool-integrations).

## <a name="next-steps"></a>Další kroky

Naučte se vytvářet, přiřazovat a spravovat [definice zásad](https://docs.microsoft.com/azure/governance/policy) v Azure.
