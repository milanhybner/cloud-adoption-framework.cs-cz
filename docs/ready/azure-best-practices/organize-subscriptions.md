---
title: Uspořádání a správa několika předplatných Azure
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak vytvořit hierarchii skupiny pro správu, která zjednodušuje správu předplatných a prostředků.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e874c518537232104d9bbddbdf8e84841239e56b
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359774"
---
# <a name="organize-and-manage-multiple-azure-subscriptions"></a>Uspořádání a správa několika předplatných Azure

Pokud máte jen několik předplatných, je poměrně snadné je spravovat nezávisle. Pokud ale máte mnoho předplatných, vytvořte hierarchii skupin pro správu, která vám pomůžou spravovat vaše předplatná a prostředky.

## <a name="azure-management-groups"></a>Skupiny pro správu Azure

Skupiny pro správu Azure umožňují efektivní správu přístupu, zásad a dodržování předpisů u předplatných organizace. Každá skupina pro správu je kontejnerem pro jedno nebo více předplatných.

Skupiny pro správu jsou uspořádány v jedné hierarchii. Tuto hierarchii definujete v tenantovi Azure Active Directory (Azure AD), která se bude zarovnávat se strukturou a potřebami vaší organizace. Nejvyšší úroveň se označuje jako *kořenová skupina pro správu*. V hierarchii můžete definovat až šest úrovní skupin pro správu. Každé předplatné je obsaženo pouze v jedné skupině pro správu.

Azure poskytuje čtyři úrovně oboru správy:

- Skupiny pro správu
- Předplatná
- Skupiny prostředků
- Zdroje a prostředky

Jakýkoli přístup nebo zásady použité na jedné úrovni v hierarchii se dědí úrovněmi pod ní. Vlastník prostředku nebo vlastník předplatného nemůže zděděné zásady změnit. Toto omezení pomáhá zlepšit zásady správného řízení.

> [!NOTE]
> Dědičnost značek zatím není podporována, ale bude brzy k dispozici.

Tento model dědičnosti umožňuje uspořádat odběry ve vaší hierarchii tak, aby každý odběr odpovídal příslušným zásadám a bezpečnostním mechanismům zabezpečení.

![Čtyři úrovně rozsahu pro uspořádání prostředků Azure](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Všechna přiřazení přístupu nebo zásad v kořenové skupině pro správu se použijí pro všechny prostředky v rámci příslušného adresáře. Pečlivě zvažte, které položky v tomto oboru definujete. Zahrňte pouze ta přiřazení, která potřebujete.

## <a name="create-your-management-group-hierarchy"></a>Vytvoření hierarchie skupiny pro správu

Při definování hierarchie skupiny pro správu nejprve vytvořte kořenovou skupinu pro správu. Pak přesuňte všechna existující předplatná v adresáři do kořenové skupiny pro správu. Nová předplatná se vždy vytvoří v kořenové skupině pro správu. Později je můžete přesunout do jiné skupiny pro správu.

Když přesunete předplatné do existující skupiny pro správu, zdědí to zásady a přiřazení rolí z hierarchie skupiny pro správu nad ním. Po navázání více předplatných pro vaše úlohy Azure můžete vytvořit další odběry, které budou obsahovat služby Azure, které sdílejí jiné předplatné.

Pokud očekáváte, že prostředí Azure budete rozšiřovat, měli byste vytvořit skupiny pro správu pro produkční a nevýrobní prostředí a použít příslušné zásady a řízení přístupu na úrovni skupiny pro správu. Nové odběry zdědí příslušné ovládací prvky při jejich přidání do každé skupiny pro správu.

![Příklad hierarchie skupiny pro správu](../../_images/ready/management-group-hierarchy-v2.png)

## <a name="example-use-cases"></a>Příklad případů použití

Tady je několik základních příkladů využití skupin pro správu k oddělení různých úloh:

- **Výroba vs. nevýrobní úlohy:** Pomocí skupin pro správu snadněji spravujte různé role a zásady mezi produkčním a neproduktivním předplatným. Například předplatná pro vývojáře můžou udělit vývojářům přístup, zatímco v produkčních vývojářích máte jenom přístup čtenářů.
- **Interní služby a externí služby:** Podniky mají často různé požadavky, zásady a role pro interní služby a externí služby pro zákazníky.

## <a name="related-resources"></a>Související prostředky

Další informace o organizování a správě prostředků Azure najdete v následujících zdrojích.

- [Uspořádání prostředků s využitím skupin pro správu Azure](https://docs.microsoft.com/azure/governance/management-groups)
- [Zvýšení úrovně přístupu pro správu všech předplatných Azure a skupin pro správu](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin)
- [Přesun prostředků Azure do jiné skupiny prostředků nebo jiného předplatného](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources)

## <a name="next-steps"></a>Další kroky

Přečtěte si téma týkající se [doporučených konvencí pro tvorbu názvů a značek](./naming-and-tagging.md), které byste měli při nasazování prostředků Azure dodržovat.

> [!div class="nextstepaction"]
> [Doporučené konvence pro tvorbu názvů a značek](./naming-and-tagging.md)
