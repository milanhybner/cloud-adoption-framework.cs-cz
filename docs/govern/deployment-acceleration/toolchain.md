---
title: Nástroje pro akceleraci nasazení v Azure
description: Podívejte se, jak můžou Azure Native Tools pomoci při vyspělých zásadách a procesech, které podporují pravidla správy akcelerace nasazení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b6fac6af93c68f22561b578cfe598bc9d847c902
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434499"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Nástroje pro akceleraci nasazení v Azure

[Akcelerace nasazení](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na způsoby vytváření zásad správného řízení konfigurace nebo nasazení prostředků. V pěti oborech zásad správného řízení cloudu zahrnuje obor akcelerace nasazení zarovnání nasazení a konfigurace. Může se to provádět ručními aktivitami nebo pomocí plně automatizovaných aktivit DevOps. V obou případech zůstanou tyto zásady převážně stejné.

Cloudové starají, strážci cloudu a cloudové architekty s cílem zásad správného řízení mají za následek, že budou investovat spoustu času v oboru akcelerace nasazení, který kodifikovaly zásady a požadavky v rámci více úsilí o přijetí v cloudu. Nástroje v tomto sada nástrojů jsou důležité pro tým zásad správného řízení cloudu a měla by být vysoká priorita na cestě výuky pro tým.

Následuje seznam nástrojů Azure, které mohou pomoci při vyspělosti zásad a procesů, které podporují tento obor řízení.

|  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Skupiny pro správu Azure](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) | [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Graf prostředků Azure](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
|Implementace podnikových zásad     |Ano |Ne  |Ne  |Ne | Ne |Ne |
|Použití zásad v rámci předplatných     |Požaduje se |Ano  |Ne  |Ne | Ne |Ne |
|Nasazení definovaných prostředků     |Ne |Ne  |Ano  |Ne | Ne |Ne |
|Vytváření plně vyhovujících prostředí      |Požaduje se |Požaduje se  |Požaduje se  |Ano | Ne |Ne |
|Zásady auditu      |Ano |Ne  |Ne  |Ne | Ne |Ne |
|Dotazování prostředků Azure      |Ne |Ne  |Ne  |Ne |Ano |Ne |
|Sestava nákladů na prostředky      |Ne |Ne  |Ne  |Ne |Ne |Ano |

Níže najdete další nástroje, které mohou být požadovány pro splnění konkrétních cílů akcelerace nasazení. Tyto nástroje se často používají mimo tým zásad správného řízení, ale stále se považují za aspekty zrychlení nasazení jako v rámci disciplíny.

|  | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure DevOps](https://docs.microsoft.com/azure/devops/index) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
|Ruční nasazení (jeden Asset)     | Ano | Ano  | Ne  | Neefektivně | Ne | Ano |
|Ruční nasazení (úplné prostředí)     | Neefektivně | Ano | Ne  | Neefektivně | Ne | Ano |
|Automatizované nasazení (celé prostředí)     | Ne  | Ano  | Ne  | Ano  | Ne | Ano |
|Aktualizace konfigurace jednoho prostředku     | Ano | Ano | Neefektivně | Neefektivně | Ne | Ano – při replikaci |
|Aktualizuje konfiguraci celého prostředí.     | Neefektivně | Ano | Ano | Ano  | Ne | Ano – při replikaci |
|Spravovat posun konfigurace     | Neefektivně | Neefektivně | Ano  | Ano  | Ne | Ano – při replikaci |
|Vytvoření automatizovaného kanálu pro nasazení kódu a konfigurace prostředků (DevOps)     | Ne | Ne | Ne | Ano | Ne | Ne |

Kromě nativních nástrojů Azure, které jsou uvedené výše, je běžné, že zákazníci můžou pomocí nástrojů třetích stran usnadnit akceleraci nasazení a nasazení DevOps.
