---
title: Centralizované operace správy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pokyny k centralizaci operací správy
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b8e4e37ba9a771937b11f08f1abae45de2f818ab
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/02/2019
ms.locfileid: "71804727"
---
# <a name="centralize-management-operations"></a>Centralizované operace správy

U většiny organizací používá jeden tenant Azure Active Directory (Azure AD) pro všechny uživatele zjednodušené operace správy a snižuje náklady na údržbu, protože všechny úlohy správy můžou být určitými uživateli, skupinami uživatelů nebo instančními objekty v rámci této služby. tenant. Pokud je to možné, doporučujeme použít jenom jednoho tenanta Azure AD pro vaši organizaci.

Existují však situace, které mohou vyžadovat organizaci, aby udržovala více tenantů služby Azure AD. Například může být vyžadováno více klientů v důsledku:

- Zcela nezávislé pobočky.
- Provoz nezávisle v různých geografických oblastech.
- Právní předpisy nebo požadavky na dodržování předpisů.
- Získání jiných organizací (někdy dočasná až do definování strategie dlouhodobé konsolidace tenanta).

V případech, kdy se vyžaduje architektura s více klienty, poskytuje [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) způsob, jak centralizovat a zjednodušit operace správy. Pro [správu delegovaných prostředků Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management)můžete připojit předplatné z několika tenantů, což umožňuje určeným uživatelům v tenantovi spravovat [funkce pro správu mezi klienty](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) centralizovaným a škálovatelným způsobem.

Řekněme například, že vaše organizace má jednoho tenanta, *tenanta a*. Vaše organizace pak získá dva další klienty, *tenanta B* a *tenanta C*a máte obchodní důvody, které vyžadují, abyste je zachovali jako samostatné klienty.

Vaše organizace chce použít stejné definice zásad, postupy pro zálohování a procesy zabezpečení ve všech klientech. Vzhledem k tomu, že už máte uživatele (včetně skupin uživatelů a instančních objektů), které jsou zodpovědné za provádění těchto úkolů v rámci tenanta a, můžete začlenit všechna předplatná v rámci tenanta B a tenanta C, aby je tito uživatelé v Tenantovi a mohli provádět. provádění. Tenant A pak se bude spravovat jako tenant pro tenanta B a tenanta C.

![Uživatelé v Tenantovi A spravují prostředky v Tenantovi B a tenant C.](../_images/manage/enterprise-azure-lighthouse.jpg)

Další informace najdete v tématu [Azure Lighthouse v podnikových scénářích](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
