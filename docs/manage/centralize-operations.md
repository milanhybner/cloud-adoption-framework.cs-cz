---
title: Centralizace operací správy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pokyny k centralizaci operací správy
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b88a1541a2f96dbd4b8d63572e44d493bce8cc45
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979962"
---
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
