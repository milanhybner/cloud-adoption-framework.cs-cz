---
title: Návrh zásad správného řízení pro jednoduchou úlohu
description: Pokyny pro konfiguraci řízení zásad správného řízení Azure, aby uživatel mohl nasadit jednoduchou úlohu.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a1edb7395751f8a91899fc8ef88f53bc056914ac
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803853"
---
# <a name="governance-design-for-a-simple-workload"></a>Návrh zásad správného řízení pro jednoduchou úlohu

Cílem těchto pokynů je pomoci při seznámení s procesem navrhování modelu zásad správného řízení prostředků v Azure za účelem podpory jednoho týmu a jednoduchého zatížení. Podíváte se na sadu hypotetických požadavků zásad správného řízení a potom si Projděte několik ukázkových implementací, které tyto požadavky splňují.

V rámci základní fáze přijetí je naším cílem nasazení jednoduché úlohy do Azure. Výsledkem je následující požadavky:

- Správa identit pro jediného **vlastníka pracovního vytížení** , který zodpovídá za nasazení a údržbu jednoduchého zatížení. Vlastník úlohy vyžaduje oprávnění k vytváření, čtení, aktualizaci a odstraňování prostředků i oprávnění k delegování těchto práv jiným uživatelům v systému správy identit.
- Spravujte všechny prostředky pro jednoduchou úlohu jako jednu jednotku správy.

## <a name="azure-licensing"></a>Licencování Azure

Než začnete navrhovat náš model zásad správného řízení, je důležité pochopit, jakým způsobem má Azure licenci. Důvodem je to, že účty pro správu spojené s vaší licencí Azure mají nejvyšší úroveň přístupu k prostředkům Azure. Tyto účty pro správu tvoří základ modelu zásad správného řízení.

> [!NOTE]
> Pokud má vaše organizace existující [smlouva Enterprise Microsoftu](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) , která nezahrnuje Azure, je možné Azure přidat prostřednictvím peněžního závazku od začátku. Další informace najdete v tématu [licencování Azure pro podnik](https://azure.microsoft.com/pricing/enterprise-agreement).

Když se do smlouva Enterprise vaší organizace přidalo Azure, ve vaší organizaci se zobrazila výzva k vytvoření **účtu Azure**. Během procesu vytváření účtu se vytvořil **vlastník účtu Azure** a také tenant Azure Active Directory (Azure AD) s **globálním účtem správce** . Tenant Azure AD je logická konstrukce, která představuje zabezpečenou, vyhrazenou instanci Azure AD.

![účtu Azure pomocí Správce účtů Azure a globálního správce Azure AD](../../_images/govern/design/governance-3-0.png)
*Obrázek 1 – účet Azure se správcem účtů a globálním správcem služby Azure AD.*

## <a name="identity-management"></a>Správa identit

Azure AD důvěřuje Azure [AD](https://docs.microsoft.com/azure/active-directory) jenom za účelem ověřování uživatelů a autorizaci uživatelských přístupů k prostředkům, takže Azure AD je náš systém pro správu identit. Globální správce Azure AD má nejvyšší úroveň oprávnění a může provádět všechny akce související s identitou, včetně vytváření uživatelů a přiřazování oprávnění.

Náš požadavek je Správa identit pro jednoho **vlastníka pracovního vytížení** , který zodpovídá za nasazení a údržbu jednoduchého zatížení. Vlastník úlohy vyžaduje oprávnění k vytváření, čtení, aktualizaci a odstraňování prostředků i oprávnění k delegování těchto práv jiným uživatelům v systému správy identit.

Náš globální správce Azure AD vytvoří účet **vlastníka úlohy** pro vlastníka úlohy:

![globální správce Azure AD vytvoří účet vlastníka úlohy](../../_images/govern/design/governance-1-2.png)
*Obrázek 2 – globální správce Azure AD vytvoří uživatelský účet vlastníka úlohy.*

Nemůžete přiřadit oprávnění k přístupu k prostředkům, dokud se tento uživatel nepřidá do **předplatného**, takže to provedete v následujících dvou částech.

## <a name="resource-management-scope"></a>Obor správy prostředků

S rostoucím počtem prostředků nasazených vaší organizací roste i složitost řízení těchto prostředků. Azure implementuje hierarchii logických kontejnerů, aby vaše organizace mohla spravovat vaše prostředky ve skupinách na různých úrovních členitosti, označované taky jako **Scope**.

Nejvyšší úroveň rozsahu správy prostředků je úroveň **předplatného** . Předplatné vytvoří **vlastník účtu**Azure, který zřídí finanční závazek a zodpovídá za vyplácení všech prostředků Azure přidružených k předplatnému:

![vlastník účtu Azure vytvoří předplatné](../../_images/govern/design/governance-1-3.png)
*Obrázek 3 – vlastník účtu Azure vytvoří předplatné.*

Po vytvoření předplatného přidružuje **vlastník účtu** Azure klientovi Azure AD k předplatnému a tento TENANT Azure AD se použije k ověřování a autorizaci uživatelů:

![vlastník účtu Azure přidruží klienta Azure AD k předplatnému](../../_images/govern/design/governance-1-4.png)
*Obrázek 4 – vlastník účtu Azure přidruží k předplatnému tenanta Azure AD.*

Možná jste si všimli, že k předplatnému není aktuálně přidružený žádný uživatel, což znamená, že nikdo nemá oprávnění ke správě prostředků. Ve skutečnosti je vlastníkem předplatného **vlastník účtu** a má oprávnění provést jakoukoli akci s prostředkem v předplatném. V praktických případech je však **vlastníkem účtu** více, než je pravděpodobně finanční osoba ve vaší organizaci a neodpovídá za vytváření, čtení, aktualizaci a odstraňování prostředků – tyto úlohy bude provádět **vlastník úlohy**. Proto je nutné přidat **vlastníka úlohy** do předplatného a přiřadit oprávnění.

Vzhledem k tomu, že **vlastník účtu** je aktuálně jediným uživatelem s oprávněním k přidání **vlastníka úlohy** do předplatného, přidá **vlastníka úlohy** do předplatného:

![vlastník účtu Azure přidá do předplatného * * vlastníka úlohy * *](../../_images/govern/design/governance-1-5.png)
*Obrázek 5 – vlastník účtu Azure přidá vlastníka úlohy do předplatného.*

**Vlastník účtu** Azure uděluje oprávnění **vlastníkovi úlohy** přiřazením role [řízení přístupu na základě role (RBAC)](https://docs.microsoft.com/azure/role-based-access-control) . Role RBAC určuje sadu oprávnění, které má **vlastník úlohy** pro konkrétní typ prostředku nebo sadu typů prostředků.

Všimněte si, že v tomto příkladu přiřadil **vlastník účtu** [předdefinovanou roli **vlastníka** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner):

![má uživatel * * vlastník úlohy * * přiřazenou předdefinovanou roli vlastníka](../../_images/govern/design/governance-1-6.png)
*Obrázek 6 – vlastníkem úlohy byla přiřazena předdefinovaná role vlastníka.*

Předdefinovaná role **vlastníka** uděluje všem oprávněním **vlastníka úlohy** v oboru předplatného.

> [!IMPORTANT]
> **Vlastník účtu** Azure zodpovídá za finanční závazek spojený s předplatným, ale **vlastník úlohy** má stejná oprávnění. **Vlastník účtu** musí důvěřovat **vlastníkovi úlohy** za účelem nasazení prostředků, které jsou v rámci rozpočtu předplatného.

Další úrovní rozsahu správy je úroveň **skupiny prostředků** . Skupina prostředků je logický kontejner pro prostředky. Operace použité na úrovni skupiny prostředků se vztahují na všechny prostředky ve skupině. Také je důležité si uvědomit, že oprávnění pro každého uživatele jsou zděděná od další úrovně, pokud se v tomto oboru explicitně nezmění.

Pro ilustraci tohoto problému se podívejme na to, co se stane, když **vlastník úlohy** vytvoří skupinu prostředků:

![* * vlastník úlohy * * vytvoří skupinu prostředků](../../_images/govern/design/governance-1-7.png)
*Obrázek 7 – vlastník úlohy vytvoří skupinu prostředků a zdědí integrovanou roli vlastníka v oboru skupiny prostředků.*

Předdefinovaná role **vlastníka** znovu uděluje všem oprávněním **vlastníka úlohy** v oboru skupiny prostředků. Jak je popsáno výše, tato role dědí z úrovně předplatného. Pokud se tomuto uživateli v tomto oboru přiřadí jiná role, vztahuje se jenom na tento obor.

Nejnižší úroveň rozsahu správy je na úrovni **prostředků** . Operace použité na úrovni prostředků se vztahují jenom na samotný prostředek. Znovu jsou oprávnění na úrovni prostředků zděděná z oboru skupiny prostředků. Podívejme se například na to, co se stane, když **vlastník úlohy** nasadí [virtuální síť](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) do skupiny prostředků:

![* * vlastník úlohy * * vytvoří prostředek](../../_images/govern/design/governance-1-8.png)
*Obrázek 8 – vlastník úlohy vytvoří prostředek a zdědí integrovanou roli vlastníka v oboru prostředků.*

**Vlastník úlohy** dědí roli vlastníka v oboru prostředků, což znamená, že vlastník úlohy má všechna oprávnění pro virtuální síť.

## <a name="implement-the-basic-resource-access-management-model"></a>Implementace základního modelu řízení přístupu k prostředkům

Pojďme se podívat, jak implementovat dříve navržený model zásad správného řízení.

Aby bylo možné začít, vaše organizace vyžaduje účet Azure. Pokud má vaše organizace existující [smlouva Enterprise Microsoftu](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) , která nezahrnuje Azure, je možné Azure přidat prostřednictvím peněžního závazku od začátku. Další informace najdete v tématu [licencování Azure pro podnik](https://azure.microsoft.com/pricing/enterprise-agreement).

Po vytvoření účtu Azure určíte osobu ve vaší organizaci, která bude **vlastníkem účtu**Azure. Ve výchozím nastavení se vytvoří tenant Azure Active Directory (Azure AD). Váš **vlastník účtu** Azure musí [vytvořit uživatelský účet](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) pro osobu ve vaší organizaci, která je **vlastníkem úlohy**.

Dále musí **vlastník účtu** Azure [Vytvořit předplatné](https://docs.microsoft.com/partner-center/create-a-new-subscription) a [k němu přidružit tenanta Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory) .

Nakonec, když se vytvoří předplatné a přidruží se k němu tenant Azure AD, můžete [do předplatného přidat **vlastníka úlohy** pomocí předdefinované role **vlastníka** ](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#to-assign-a-user-as-an-administrator).

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Nasazení základní úlohy do Azure](../../infrastructure/virtual-machines/basic-workload.md)
> [!div class="nextstepaction"]
> [Informace o přístupu k prostředkům pro více týmů](./governance-multiple-teams.md)
