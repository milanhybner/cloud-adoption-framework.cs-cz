---
title: Nástroje pro základní hodnoty zabezpečení v Azure
description: Podívejte se, jak můžou Azure Native Tools pomoci při vyspělých zásadách a procesech, které podporují obor zásad správného řízení standardních hodnot zabezpečení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: db3be7ca7577cb8b42f4efc556b88b25d6e1f23e
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425835"
---
# <a name="security-baseline-tools-in-azure"></a>Nástroje pro základní hodnoty zabezpečení v Azure

[Základní úroveň zabezpečení](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na způsoby vytváření zásad, které chrání síť, prostředky a nejdůležitější data, která se budou nacházet v řešení poskytovatele cloudu. V rámci pěti oborů řízení cloudu zahrnuje základní pravidla zabezpečení klasifikaci digitálních nemovitostí a dat. Zahrnuje taky dokumentaci k rizikům, obchodním tolerancím a strategiím zmírňování, které souvisejí s bezpečností dat, prostředků a sítí. Z technického hlediska tato disciplína zahrnuje také zapojení do rozhodnutí týkajících se [šifrování](../../decision-guides/encryption/index.md), [požadavků na síť](../../decision-guides/software-defined-network/index.md), [strategií hybridních identit](../../decision-guides/identity/index.md)a nástrojů pro [automatizaci vynucování](../../decision-guides/policy-enforcement/index.md) zásad zabezpečení napříč [skupinami prostředků](../../decision-guides/resource-consistency/index.md).

Následující seznam nástrojů Azure může pomoci při vyspělosti zásad a procesů, které podporují standardní hodnoty zabezpečení.

| Nástroj | [Azure Portal](https://azure.microsoft.com/features/azure-portal) a [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Použití řízení přístupu k prostředkům a vytváření prostředků   | Ano                             | Ne              | Ano      | Ne           | Ne                    | Ne            |
| Zabezpečení virtuálních sítí                                    | Ano                             | Ne              | Ne       | Ano          | Ne                    | Ne            |
| Šifrování virtuálních jednotek                                     | Ne                              | Ano             | Ne       | Ne           | Ne                    | Ne            |
| Šifrování úložiště a databází PaaS                         | Ne                              | Ano             | Ne       | Ne           | Ne                    | Ne            |
| Správa služby hybridní identity                            | Ne                              | Ne              | Ano      | Ne           | Ne                    | Ne            |
| Omezit povolené typy prostředku                         | Ne                              | Ne              | Ne       | Ano          | Ne                    | Ne            |
| Vynutilit omezení geografického regionu                          | Ne                              | Ne              | Ne       | Ano          | Ne                    | Ne            |
| Monitorování stavu zabezpečení sítí a prostředků          | Ne                              | Ne              | Ne       | Ne           | Ano                   | Ano           |
| Detekovat škodlivou aktivitu                                  | Ne                              | Ne              | Ne       | Ne           | Ano                   | Ano           |
| Bezchybná detekce slabých míst                        | Ne                              | Ne              | Ne       | Ne           | Ano                   | Ne            |
| Konfigurace zálohování a zotavení po havárii                     | Ano                             | Ne              | Ne       | Ne           | Ne                    | Ne            |

Úplný seznam nástrojů a služeb zabezpečení Azure najdete v tématu [služby a technologie zabezpečení dostupné v Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Zákazníkům je také běžné používat nástroje třetích stran pro usnadnění činností standardních hodnot zabezpečení. Další informace najdete v článku [integrace řešení zabezpečení v Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Kromě nástrojů zabezpečení obsahuje [Centrum zabezpečení Microsoftu](https://www.microsoft.com/trustcenter/guidance/risk-assessment) obsáhlé doprovodné materiály, sestavy a související dokumentaci, která vám může pomoci při rozhodování o posouzení rizik v rámci procesu plánování migrace.
