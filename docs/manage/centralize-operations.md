---
title: Centralizace operací správy
description: Naučte se centralizovat operace správy pomocí jednoho Azure Active Directory tenanta pro všechny uživatele. Centralizovaná správa usnadňuje operace správy a snižuje náklady na údržbu.
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 12b1a578c98a2c870306d9bc5b3587477adbb3d3
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430355"
---
<!-- cSpell:ignore jenhayes -->

# <a name="centralize-management-operations"></a>Centralizace operací správy

U většiny organizací používá jeden tenant Azure Active Directory (Azure AD) pro všechny uživatele zjednodušení operací správy a snižuje náklady na údržbu. Důvodem je to, že všechny úlohy správy můžou být určenými uživateli, skupinami uživatelů nebo instančními objekty v rámci tohoto tenanta.

Pokud je to možné, doporučujeme, abyste pro vaši organizaci používali jenom jednoho tenanta Azure AD. Některé situace ale můžou vyžadovat, aby organizace udržovala více tenantů Azure AD z následujících důvodů:

- Jsou to zcela nezávislé pobočky.
- Pracují nezávisle v různých geografických oblastech.
- Platí určité zákonné požadavky nebo požadavky na dodržování předpisů.
- Existují i akvizice jiných organizací (někdy dočasné, dokud není definovaná strategie dlouhodobé konsolidace tenanta).

Když se vyžaduje architektura s více klienty, [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) poskytuje způsob, jak centralizovat a zjednodušit operace správy. Pro [správu delegovaných prostředků Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management)se dá připojit předplatné z více tenantů. Tato možnost umožňuje konkrétním uživatelům ve správě tenanta provádět funkce pro [správu mezi klienty](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) centralizovaným a škálovatelným způsobem.

Řekněme například, že vaše organizace má jednoho tenanta, *tenanta a*. Organizace pak získá dva další klienty, *tenanta B* a *tenanta C*a máte obchodní důvody, které vyžadují, abyste je zachovali jako samostatné klienty.

Vaše organizace chce použít stejné definice zásad, postupy pro zálohování a procesy zabezpečení ve všech klientech. Vzhledem k tomu, že už máte uživatele (včetně skupin uživatelů a instančních objektů), které jsou zodpovědné za provádění těchto úkolů v rámci tenanta a, můžete začlenit všechna předplatná v rámci tenanta B a tenanta C, aby je tito uživatelé v Tenantovi a mohli provádět. provádění. Tenant A pak se bude spravovat jako tenant pro tenanta B a tenanta C.

![Uživatelé v Tenantovi A spravují prostředky v Tenantovi B a tenant C.](../_images/manage/enterprise-azure-lighthouse.jpg)

Další informace najdete v tématu [Azure Lighthouse v podnikových scénářích](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
