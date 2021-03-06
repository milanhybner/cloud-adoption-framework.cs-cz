---
title: Správa přístupu k prostředí Azure
description: Zjistěte, jak pro vaše prostředí Azure nastavit řízení přístupu s využitím řízení přístupu na základě role (RBAC).
author: LijuKodicheraJayadevan
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 5fedbb5164da05b166d8a42d8d1ceaf43ee95185
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80354450"
---
<!-- cSpell:ignore LijuKodicheraJayadevan -->

# <a name="manage-access-to-your-azure-environment-with-role-based-access-controls"></a>Správa přístupu k prostředí Azure s využitím řízení přístupu na základě role

Správa přístupu uživatelů k prostředkům a předplatným Azure představuje důležitou součást strategie zásad správného řízení Azure. Jedním z vhodných postupů je přidělování přístupových práv a oprávnění, která jsou založená na skupinách. Práce se skupinami namísto jednotlivých uživatelů zjednodušuje správu zásad přístupu, umožňuje jednotnou správu přístupu napříč týmy a snižuje riziko chyb při konfiguraci. Hlavní metodou správy přístupu v Azure je řízení přístupu na základě role (RBAC).

Řízení přístupu na základě role (RBAC) poskytuje podrobnou správu přístupu k prostředkům v Azure. Pomáhá spravovat, kdo a v jakém rozsahu má přístup k prostředkům Azure a co může s těmito prostředky dělat.

Při plánování strategie řízení přístupu udělte uživatelům nejnižší úroveň oprávnění, kterou ke své práci potřebují. Následující obrázek ukazuje navrhovaný způsob přiřazování rolí RBAC.

![Diagram znázorňující role RBAC](./media/manage-access/role-examples.png)

Při plánování metodologie řízení přístupu doporučujeme spolupracovat s lidmi, kteří ve vaší organizaci mají na starost zabezpečení a dodržování předpisů, správu IT a podnikovou architekturu.

Architektura přechodu na cloud nabízí další tipy, jak v rámci nasazení cloudu [používat řízení přístupu na základě rolí](../considerations/roles.md).

::: zone target="chromeless"

## <a name="actions"></a>Akce

**Udělení přístupu ke skupině prostředků:**

Udělení přístupu uživatele skupině prostředků:

1. Přejděte do části **Skupiny prostředků**.
1. Vyberte skupinu prostředků.
1. Vyberte **Řízení přístupu (IAM)** .
1. Vyberte **+ Přidat** > **Přidat přiřazení role**.
1. Vyberte roli a potom přiřaďte přístup uživateli, skupině nebo instančnímu objektu.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources/Subscriptions/ResourceGroups]" submitText="Go to resource groups" ::: form-end

**Udělení přístupu k předplatnému:**

Udělení přístupu uživatele předplatnému:

1. Přejděte do části **Předplatná**.
1. Vyberte předplatné.
1. Vyberte **Řízení přístupu (IAM)** .
1. Vyberte **+ Přidat** > **Přidat přiřazení role**.
1. Vyberte roli a potom přiřaďte přístup uživateli, skupině nebo instančnímu objektu.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to subscriptions" ::: form-end

::: zone-end

::: zone target="docs"

## <a name="grant-resource-group-access"></a>Udělení přístupu ke skupině prostředků

Udělení přístupu uživatele skupině prostředků:

1. Přejděte do části [Skupiny prostředků](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups).
1. Vyberte skupinu prostředků.
1. Vyberte **Řízení přístupu (IAM)** .
1. Vyberte **+ Přidat** > **Přidat přiřazení role**.
1. Vyberte roli a potom přiřaďte přístup uživateli, skupině nebo instančnímu objektu.

## <a name="grant-subscription-access"></a>Udělení přístupu k předplatnému

Udělení přístupu uživatele předplatnému:

1. Přejděte do části [Předplatná](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Vyberte předplatné.
1. Vyberte **Řízení přístupu (IAM)** .
1. Vyberte **+ Přidat** > **Přidat přiřazení role**.
1. Vyberte roli a potom přiřaďte přístup uživateli, skupině nebo instančnímu objektu.

## <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Co je řízení přístupu na základě role (RBAC)?](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Architektura přechodu na cloud: Použití řízení přístupu na základě rolí](../considerations/roles.md)

::: zone-end
