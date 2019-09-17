---
title: Správa přístupu k prostředkům v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Vysvětlení konstrukcí správy přístupu k prostředkům v Azure: Azure Resource Manager, předplatná, skupiny prostředků a prostředky'
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 46c6de1ecaba5b8278138114b6aa27a2608bfb74
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029838"
---
# <a name="resource-access-management-in-azure"></a>Správa přístupu k prostředkům v Azure

Zásady [správného řízení cloudu](../index.md) popisují pět oborů zásad správného řízení cloudu, které zahrnují správu prostředků. [Co je Správa přístupu k prostředkům](./index.md) dále vysvětluje, jak se Správa přístupu k prostředkům vejde do oboru správy prostředků. Než přejdete na Další informace o návrhu modelu zásad správného řízení, je důležité pochopit ovládací prvky pro správu přístupu k prostředkům v Azure. Konfigurace těchto ovládacích prvků pro řízení přístupu k prostředkům tvoří základ vašeho modelu zásad správného řízení.

Začněte tím, že se podíváte na to, jak se prostředky nasazují v Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Co je prostředek Azure?

V Azure pojem _prostředek_ odkazuje na entitu spravovanou Azure. Například virtuální počítače, virtuální sítě a účty úložiště se označují jako prostředky Azure.

![Diagram](../../_images/govern/design/governance-1-9.png)
*obrázku prostředku 1 – prostředek.*

## <a name="what-is-an-azure-resource-group"></a>Co je skupina prostředků Azure?

Každý prostředek v Azure musí patřit do [skupiny prostředků](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Skupina prostředků je jen logická konstrukce, která seskupuje více prostředků dohromady, aby se mohla spravovat jako jediná entita. Například prostředky, které sdílejí podobný životní cyklus, například prostředky pro [n-vrstvou aplikaci](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) , lze vytvořit nebo odstranit jako skupinu.

![Diagram skupiny prostředků obsahující zdroj](../../_images/govern/design/governance-1-10.png)
*obrázku 2 – skupina prostředků obsahuje prostředek.*

Skupiny prostředků a prostředky, které obsahují, jsou přidružené k **předplatnému**Azure.

## <a name="what-is-an-azure-subscription"></a>Co je předplatné Azure?

Předplatné Azure je podobné jako skupina prostředků v tom, že je to logická konstrukce, která seskupuje skupiny prostředků a jejich prostředky dohromady. Předplatné Azure je ale také přidružené k ovládacím prvkům, které používá Azure Resource Manager. Co to znamená? Podívá se na Azure Resource Manager, kde se dozvíte o vztahu mezi ním a předplatným Azure.

![Diagram předplatného](../../_images/govern/design/governance-1-11.png)
Azure na*obrázku 3 – předplatné Azure*

## <a name="what-is-azure-resource-manager"></a>Co je Azure Resource Manager?

[Jak Azure funguje?](../../getting-started/what-is-azure.md) zjistili jste, že Azure obsahuje "front-end" s mnoha službami, které orchestrují všechny funkce Azure. Jedna z těchto služeb je [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager)a tato služba je hostitelem rozhraní API RESTful, které klienti používají ke správě prostředků.

![Diagram Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
*Obrázek 4-Azure Resource Manager.*

Následující obrázek ukazuje tři klienty: [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Portal](https://portal.azure.com)a [Azure CLI](https://docs.microsoft.com/cli/azure):

![Diagram klientů Azure připojujících se k rozhraní Azure Resource Manager](../../_images/govern/design/governance-1-13.png)
API*Obrázek 5 – klienti Azure se připojují k rozhraní Azure Resource Manager RESTful API.*

I když se tito klienti připojují k Azure Resource Manager pomocí rozhraní API RESTful, Azure Resource Manager nezahrnuje funkce pro správu prostředků přímo. Většina typů prostředků v Azure ale má svého vlastního [**poskytovatele prostředků**](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#terminology).

![Poskytovatelé](../../_images/govern/design/governance-1-14.png)
prostředků Azure *– Obrázek 6 – poskytovatelé prostředků Azure.*

Když klient odešle požadavek na správu konkrétního prostředku, Azure Resource Manager se připojí k poskytovateli prostředků pro daný typ prostředku a dokončí požadavek. Pokud například klient odešle požadavek na správu prostředku virtuálního počítače, Azure Resource Manager se připojí k poskytovateli prostředků **Microsoft. COMPUTE** .

![Azure Resource Manager připojení k poskytovateli](../../_images/govern/design/governance-1-15.png)
prostředků Microsoft. COMPUTE*Obrázek 7 – Azure Resource Manager se k poskytovateli prostředků **Microsoft. COMPUTE** připojí ke správě prostředku zadaného v žádosti klienta.*

Azure Resource Manager vyžaduje, aby klient pro účely správy prostředku virtuálního počítače určil identifikátor pro předplatné i skupinu prostředků.

Teď, když máte přehled o tom, jak Azure Resource Manager funguje, se vraťte na diskuzi o tom, jak je předplatné Azure přidružené k ovládacím prvkům používaným Azure Resource Manager. Předtím, než může být požadavek na správu prostředků proveden Azure Resource Manager, je zaškrtnuta sada ovládacích prvků.

Prvním ovládacím prvkem je, že požadavek musí provést ověřený uživatel a Azure Resource Manager má důvěryhodný vztah s [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory) k zajištění funkce identity uživatele.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
*Obrázek 8-Azure Active Directory.*

Ve službě Azure AD se uživatelé segmentují do **tenantů**. Tenant je logická konstrukce, která představuje zabezpečenou a vyhrazenou instanci služby Azure AD, která je obvykle přidružená k organizaci. Každé předplatné je přidruženo k tenantovi služby Azure AD.

![Tenant Azure AD přidružený k předplatnému](../../_images/govern/design/governance-1-17.png)
na*obrázku 9 – tenant služby Azure AD, který je přidružený k předplatnému.*

Každá žádost klienta o správu prostředku v konkrétním předplatném vyžaduje, aby uživatel měl účet v přidruženém tenantovi Azure AD.

Dalším ovládacím prvkem je kontrola, zda má uživatel dostatečná oprávnění k vytvoření žádosti. Oprávnění jsou přiřazena uživatelům pomocí [řízení přístupu na základě role (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![Uživatelé přiřazení rolí](../../_images/govern/design/governance-1-18.png)
*RBAC na obrázek 10. Každému uživateli v tenantovi je přiřazena jedna nebo více rolí RBAC.*

Role RBAC určuje sadu oprávnění, které může uživatel provést na konkrétním prostředku. Při přiřazení role uživateli se tato oprávnění uplatní. Například [integrovaná role **vlastníka** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) umožňuje uživateli provádět jakoukoli akci s prostředkem.

Dalším ovládacím prvkem je kontrola, jestli je požadavek povolený v nastavení zadaném pro [zásady prostředků Azure](https://docs.microsoft.com/azure/governance/policy). Zásady prostředků Azure určují operace, které jsou povolené pro konkrétní prostředek. Například zásada prostředků Azure může určit, že uživatelé smějí nasadit jenom určitý typ virtuálního počítače.

![Obrázek 11 o](../../_images/govern/design/governance-1-19.png)
zásadách*prostředků Azure Zásady prostředků Azure.*

Dalším ovládacím prvkem je kontrola, že požadavek nepřekračuje [limit předplatného Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits). Každé předplatné má například limit 980 skupin prostředků v rámci předplatného. Pokud se po dosažení limitu přijme žádost o nasazení další skupiny prostředků, bude zamítnutá.

![](../../_images/govern/design/governance-1-20.png)
Omezení*prostředků Azure na obrázku 12. Omezení prostředků Azure.*

Posledním ovládacím prvkem je kontrola, zda je požadavek v rámci finančního závazku přidruženého k předplatnému. Pokud například požadavek slouží k nasazení virtuálního počítače, Azure Resource Manager ověří, zda má předplatné dostatek informací o platbách.

![Finanční závazek, který je přidružený k](../../_images/govern/design/governance-1-21.png)
předplatnému*na obrázku 13. Finanční závazek je spojený s předplatným.*

## <a name="summary"></a>Souhrn

V tomto článku jste se dozvěděli o správě přístupu k prostředkům v Azure pomocí Azure Resource Manager.

## <a name="next-steps"></a>Další kroky

Teď, když už víte, jak spravovat přístup k prostředkům v Azure, přejděte k tématu Postup návrhu modelu zásad správného řízení [pro jednoduchou úlohu](./governance-simple-workload.md) nebo pro [více týmů](./governance-multiple-teams.md) , které tyto služby používají.

> [!div class="nextstepaction"]
> [Přehled zásad správného řízení](../index.md)
