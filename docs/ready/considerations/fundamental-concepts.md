---
title: Základní koncepty Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Poznejte základní koncepty a termíny používané v Azure a zjistěte, jak spolu tyto koncepty vzájemně souvisejí.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 894c4c7431533aa29ad7fcc1cd08046651987f10
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239790"
---
# <a name="azure-fundamental-concepts"></a>Základní koncepty Azure

Poznejte základní koncepty a termíny používané v Azure a zjistěte, jak spolu tyto koncepty vzájemně souvisejí.

## <a name="azure-terminology"></a>Terminologie Azure

Než začnete vyvíjet úsilí o přechod do cloudu Azure, je užitečné poznat následující definice:

- **Prostředek:** Entita, která je spravovaná pomocí Azure. Příkladem mohou být virtuální počítače Azure, virtuální sítě a účty úložiště.
- **Předplatné:** Logický kontejner pro vaše prostředky. Každý prostředek Azure je přidružený jen k jednomu předplatnému. Vytvoření předplatného je prvním krokem při přechodu na Azure.
- **Účet Azure:** E-mailová adresa, kterou zadáte při vytváření předplatného Azure, je účet Azure pro předplatné. Strana přidružená k tomuto e-mailovému účtu zodpovídá za měsíční náklady, které nabíhají za prostředky v tomto předplatném. Při vytváření účtu Azure zadáváte kontaktní informace a platební údaje, jako je platební karta. Stejný účet Azure (e-mailovou adresu) můžete použít pro několik předplatných. Každé předplatné je přidružené jen k jednomu účtu Azure.
- **Správce účtu:** Strana přidružená k e-mailové adrese, která se používá k vytvoření předplatného Azure. Správce účtu zodpovídá za platby za všechny náklady vzniklé prostředky předplatného.
- **Azure Active Directory (Azure AD):** Cloudová služba pro správu identit a přístupu od Microsoftu. Azure AD umožňuje vašim zaměstnancům se přihlásit a získat přístup k prostředkům.
- **Tenant Azure AD:** Vyhrazená a důvěryhodná instance služby Azure AD. Tenant Azure AD se automaticky vytvoří, když si vaše organizace poprvé zaregistruje předplatné cloudových služeb Microsoftu, jako je Microsoft Azure, Microsoft Intune nebo Office 365. Tenant Azure představuje jednu organizaci.
- **Adresář služby Azure AD:** Každý tenant služby Azure AD má jeden, vyhrazený a důvěryhodný adresář. Tento adresář obsahuje uživatele, skupiny a aplikace tenanta. Slouží k provádění funkcí správy identit a přístupu pro prostředky tenanta. Adresář může být přidružen k několika předplatným, ale každé předplatné je přidruženo jen k jednomu adresáři.
- **Skupiny prostředků:** Logické kontejnery, které slouží k seskupení souvisejících prostředků v rámci předplatného. Každý prostředek může existovat jen v jedné skupině prostředků.
- **Skupiny pro správu:** Logické kontejnery, které používáte pro jedno nebo více předplatných. Definováním hierarchie skupin pro správu, předplatných, skupin prostředků a prostředků můžete efektivně spravovat přístup, zásady a dodržování předpisů prostřednictvím dědičnosti.
- **Oblast:** Sada datacenter Azure, která je nasazená v hraničním prostředí definovaném pro latenci. Datacentra jsou propojena prostřednictvím vyhrazené oblastní sítě s nízkou latencí. Většina prostředků Azure se provozuje v konkrétní oblasti Azure.

## <a name="azure-subscription-purposes"></a>Účely předplatného Azure

Předplatné Azure slouží k několika účelům. Předplatné Azure je:

- **Právní smlouvu.** Každé předplatné je přidružené k některé [nabídce Azure](https://azure.microsoft.com/support/legal/offer-details) (například k bezplatné zkušební verzi nebo průběžným platbám). Každá nabídka má konkrétní sazby, výhody a související podmínky a ujednání. Nabídku Azure si zvolíte při vytváření předplatného.
- **Platební smlouva.** Při vytváření předplatného zadáváte platební údaje pro toto předplatné, například číslo platební karty. Náklady, které nabíhají za prostředky nasazené v tomto předplatném, se každý měsíc spočítají a fakturují daným způsobem platby.
- **Hranice stupnice.** Pro předplatné jsou definované limity měřítka. Prostředky předplatného nemůžou překročit nastavené limity škálování. Existuje například limit počtu virtuálních počítačů, které můžete v jednom předplatném vytvořit.
- **Hranice správy.** Předplatné může fungovat jako hranice správy, zabezpečení a zásad. Azure poskytuje pro splnění těchto potřeb také jiné mechanismy, například skupiny pro správu, skupiny prostředků a řízení přístupu na základě role.

## <a name="azure-subscription-considerations"></a>Aspekty předplatného Azure

Při vytváření předplatného Azure činíte několik důležitých rozhodnutí:

- **Kdo zodpovídá za placení předplatného?** Strana přidružená k e-mailové adrese, kterou jste zadali při vytváření předplatného, je správcem účtu předplatného. Strana přidružená k této e-mailové adrese zodpovídá za platby za všechny náklady vzniklé prostředky předplatného.
- **O kterou nabídku Azure mám zájem?** Každé předplatné je přidružené ke konkrétní [nabídce Azure](https://azure.microsoft.com/support/legal/offer-details). Můžete zvolit nabídku Azure, která nejlépe splňuje vaše potřeby. Pokud například plánujete použít předplatné ke spouštění neprodukčních úloh, můžete zvolit nabídku Průběžné platby dle aktuálního využití pro vývoj/testování nebo nabídku Enterprise pro vývoj/testování.

> [!NOTE]
> Při registraci Azure si můžete všimnout slovního spojení *vytvoření účtu Azure*. Účet Azure vytvoříte při vytváření předplatného Azure a jeho přidružení k e-mailovému účtu.

## <a name="azure-administrative-roles"></a>Role pro správu Azure

Azure definuje tři typy rolí pro správu předplatných, identit a prostředků:

- Role klasického správce předplatného
- Role řízení přístupu na základě rolí (RBAC) Azure
- Role správce služby Azure AD (Azure Active Directory)

Role správce účtu předplatného Azure je přiřazená k e-mailovému účtu, který jste použili k vytvoření předplatného Azure. Správce účtu je fakturační vlastník předplatného. Správce účtu může podrobnosti předplatného spravovat v [Centru účtů Azure](https://account.azure.com/Subscriptions).

K e-mailovému účtu, který jste použili k vytvoření předplatného Azure, je standardně přiřazená rovněž role správce služby předplatného. Správce služby má k předplatnému oprávnění, které je ekvivalentní roli vlastníka založené na RBAC. Správce služby má také úplný přístup k webu Azure Portal. Správce účtu může změnit správce služby na odlišný e-mailový účet.

Při vytváření můžete předplatné Azure přidružit k existujícímu tenantovi Azure AD. V opačném případě se vytvoří nový tenant Azure AD s přidruženým adresářem. Role globálního správce v adresáři služby Azure AD je přiřazená k e-mailovému účtu, který jste použili k vytvoření předplatného služby Azure AD.

E-mailový účet lze přidružit k několika předplatným Azure. Správce účtu může předplatné převést na jiný účet.

Podrobný popis rolí definovaných v Azure najdete v článku [Role klasického správce předplatného, role Azure RBAC a role správce Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

## <a name="subscriptions-and-regions"></a>Předplatná a oblasti

Každý prostředek Azure je logicky přidružený jen k jednomu předplatnému. Při vytváření prostředku zvolíte, do jakého předplatného Azure se má tento prostředek nasadit. Později můžete prostředek přesunout do jiného předplatného.

Předplatné není vázané na konkrétní oblast Azure. Každý prostředek Azure je ale nasazený jen v jedné oblasti. Prostředky, které jsou přidružené ke stejnému předplatnému, můžete mít ve více oblastech.

> [!NOTE]
> Většina prostředků Azure se nasazuje do konkrétní oblasti. Určité typy prostředků se ale považují za globální prostředky, například zásady, které nastavíte pomocí služby Azure Policy.

## <a name="related-resources"></a>Související materiály

Následující materiály obsahují podrobné informace o konceptech rozebraných v tomto článku:

- [Jak funguje Azure?](../../getting-started/what-is-azure.md)
- [Správa přístupu k prostředkům v Azure](../../govern/resource-consistency/resource-access-management.md)
- [Přehled Azure Resource Manageru](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)
- [Řízení přístupu k prostředkům Azure na základě role (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Představení služby Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)
- [Přiřazení nebo přidání předplatného Azure do tenanta Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)
- [Topologie pro Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies)
- [Předplatná, licence, účty a tenanti pro cloudové nabídky Microsoftu](/office365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings)

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte základním konceptům Azure, se dozvíte, jak [škálovat s využitím několika předplatných Azure](../azure-best-practices/scaling-subscriptions.md).

> [!div class="nextstepaction"]
> [Škálování s využitím několika předplatných Azure](../azure-best-practices/scaling-subscriptions.md)
