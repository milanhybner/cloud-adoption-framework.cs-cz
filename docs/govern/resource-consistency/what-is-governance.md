---
title: Co jsou zásady správného řízení cloudových prostředků?
description: Přečtěte si o procesu správy, monitorování a auditování prostředků Azure, abyste splnili cíle a požadavky vaší organizace.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: fdf63fd86b69a1c42276e5847d53deb71fcd2530
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706570"
---
<!-- markdownlint-disable MD026 -->

# <a name="cloud-resource-governance"></a>Zásady správného řízení prostředků cloudu?

V článku [Jak funguje Azure?](../../getting-started/what-is-azure.md)jste se dozvěděli, že Azure je kolekce serverů a síťových hardwarových počítačů, které používají virtualizovaný hardware a software jménem uživatelů. Azure umožňuje vývoj aplikací a oddělení IT ve vaší organizaci tak, aby se usnadnilo vytváření, čtení, aktualizace a odstraňování prostředků podle potřeby.

Ale přestože neomezeným prostředkům může vývojářům pružnější práci zvýšit, může to vést k neočekávaným nákladům. Například vývojový tým může být schválen pro nasazení sady prostředků pro testování, ale nezapomeňte je odstranit při dokončení testování. Tyto prostředky budou i nadále používat náklady, i když již nebudou schváleny nebo nutné.

Řešení je zásad správného řízení přístupu k prostředkům. **Zásad správného řízení** je nepřetržitý proces správy, monitorování a auditování používání prostředků Azure pro splnění cílů a požadavků vaší organizace.

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ii94]

<!-- markdownlint-enable MD034 -->

Tyto požadavky jsou pro každou organizaci jedinečné, takže to znamená, že každý přístup k zásadám správného řízení není užitečný. Místo toho je až do každé organizace navržený model zásad správného řízení pomocí dvou základních nástrojů zásad správného řízení Azure: **řízení přístupu na základě role (RBAC)** a **zásady prostředků**.

RBAC definuje role a role definují operace povolené pro každého uživatele přiřazeného k této roli. Role **vlastníka** například povoluje všechny operace (vytváření, čtení, aktualizace a odstraňování) prostředku, zatímco role **Čtenář** umožňuje pouze operace čtení. Role je možné definovat široce a použít na mnoho typů prostředků nebo jsou definované efektivněji a použít je jenom pro několik typů prostředků.

Zásady prostředků definují pravidla pro vytváření prostředků. Například zásada prostředku může omezit SKU virtuálního počítače na konkrétní předschválenou velikost. Další zásada prostředků může vyhovět použití značky pro přiřazené nákladové středisko, když se požadavek vytvoří pro vytvoření prostředku.

Při konfiguraci těchto nástrojů je důležité rovnováhu mezi zásadami správného řízení a pružností organizace. Přísnější zásady správného řízení, což je méně agilních vašich vývojářů a pracovníků IT. Omezující zásada zásad správného řízení může vyžadovat více ručních kroků, jako je vyžadování vývojářů vyplnit formulář nebo odeslat e-mail členovi týmu zásad správného řízení za účelem ručního vytvoření prostředku. Tým zásad správného řízení má konečnou kapacitu a může se stát kritickým týmem, což vede k tomu, že vývojové týmy čekají na jejich vytvoření v neproduktivním prostředí, nebo nepotřebné prostředky, které mají za následek nabíhání nákladů před jejich odstraněním.

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte konceptu zásad správného řízení prostředků cloudu, se dozvíte víc o tom, jak se spravuje přístup k prostředkům v Azure.

> [!div class="nextstepaction"]
> [Informace o přístupu k prostředkům v Azure](./resource-access-management.md)
