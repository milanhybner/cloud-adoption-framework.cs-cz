---
title: Průvodce rozhodováním ohledně vynucování zásad
description: Využijte architekturu přechodu na cloud pro Azure a seznamte se s předplatnými vynucování zásad jako základní prioritou návrhu při migraci do Azure.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9d480b98fc69e899185ea9633ebf00725557e908
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433174"
---
# <a name="policy-enforcement-decision-guide"></a>Průvodce rozhodováním ohledně vynucování zásad

Definování zásad organizace není efektivní, pokud je nejde vynucovat v celé organizaci. Klíčovým aspektem plánování migrace do jakéhokoli cloudu je určení nejlepší kombinace nástrojů, které poskytuje cloudová platforma, a stávajících IT procesů pro zajištění maximalizace dodržování zásad napříč všemi cloudovými aktivy.

![Diagram možností vynucování zásad od nejjednodušších po nejsložitější, které odpovídají rychlým odkazům níže](../../_images/decision-guides/decision-guide-policy-enforcement.png)

Přejít na: [Osvědčené postupy směrného plánu](#baseline-best-practices) | [Monitorování dodržování zásad](#policy-compliance-monitoring) | [Vynucování zásad](#policy-enforcement) | [Zásady pro celou organizaci](#cross-organization-policy) | [Automatizované vynucování](#automated-enforcement)

S tím, jak se budou rozšiřovat vaše cloudová aktiva, budete muset čelit odpovídající potřebě udržovat a vynucovat zásady pro větší sadu prostředků a předplatných. S rozšiřováním vašich aktiv a zvyšováním požadavků vaší organizace na zásady bude potřeba rozšířit rozsah procesů vynucování zásad, aby se zajistilo konzistentní dodržování zásad a rychlá detekce jejich porušení.

Pro méně rozsáhlá cloudová aktiva jsou obvykle dostačující mechanismy vynucování zásad na úrovni prostředku nebo předplatného, které poskytuje platforma. Rozsáhlejší nasazení ospravedlňují širší rozsah vynucování a můžou vyžadovat sofistikovanější mechanismy vynucování, které zahrnují standardy nasazení, seskupování a organizaci prostředků a integraci vynucování zásad se systémy protokolování a generování sestav.

Primárními faktory při určování rozsahu procesů vynucování zásad jsou [požadavky vaší organizace na zásady správného řízení v cloudu](../../govern/index.md), velikost a povaha cloudových aktiv a způsob, jakým [návrh předplatného](../subscriptions/index.md) odráží vaši organizaci. Rozšíření rozsahu vynucování může ospravedlnit zvýšení velikosti aktiv nebo větší potřeba centrální správy vynucování zásad.

## <a name="baseline-best-practices"></a>Osvědčené postupy směrného plánu

V případě jednoho předplatného a jednoduchých cloudových nasazení je možné řadu firemních zásad vynucovat pomocí funkcí nativních pro prostředky a předplatná v Azure. Konzistentní používání modelů popsaných v [průvodcích rozhodováním](../index.md) architektury přechodu na cloud vám může pomoct stanovit základní úroveň dodržování zásad bez zvláštních investic do vynucování zásad. Mezi tyto funkce patří:

- [Šablony nasazení](../resource-consistency/index.md) umožňují zřizovat prostředky se standardizovanou strukturou a konfigurací.
- [Standardy pro vytváření značek a názvů](../resource-tagging/index.md) můžou pomoct s uspořádáním operací a podporou účetních a obchodních požadavků.
- Prostřednictvím [softwarově definovaných sítí](../software-defined-network/index.md) je možné implementovat správu provozu a síťová omezení.
- [Řízení přístupu na základě role](../identity/index.md) může zabezpečit a izolovat vaše prostředky.

Začněte s plánováním vynucování zásad v cloudu tím, že prozkoumáte, jak vám používání standardních modelů popsaných v těchto průvodcích může pomoct splnit požadavky vaší organizace.

## <a name="policy-compliance-monitoring"></a>Monitorování dodržování zásad

Pokud se nechcete spoléhat jen na mechanismy vynucování zásad, které poskytuje platforma Azure, prvním krokem je zajistit možnost ověření, jestli jsou cloudové aplikace a služby v souladu se zásadami organizace. To zahrnuje implementaci oznamovacích funkcí, které upozorní odpovědné strany v případě, že prostředek přestane dodržovat předpisy. Důležitou součástí firemní strategie vynucování zásad je efektivní [protokolování a generování sestav](../logging-and-reporting/index.md) stavu dodržování předpisů ze strany cloudových úloh.

Jakmile se vaše cloudová aktiva začnou rozšiřovat, další nástroje, jako je [Azure Security Center](https://docs.microsoft.com/azure/security-center), vám můžou poskytnout integrované zabezpečení a detekci hrozeb a pomoct s implementací centralizované správy zásad a upozorňování pro místní i cloudové prostředky.

## <a name="policy-enforcement"></a>Vynucování zásad

V Azure můžete uplatňovat konfigurační nastavení a pravidla vytváření prostředků, která vám pomůžou zajistit dodržování zásad, na úrovni skupiny pro správu, předplatného nebo skupiny prostředků.

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) je služba Azure umožňující vytvářet, přiřazovat a spravovat zásady. Tyto zásady vynucují na vašich prostředcích různá pravidla a účinky, aby tyto prostředky zůstaly kompatibilní s vašimi firemními standardy a smlouvami o úrovni služeb. Azure Policy vyhodnocuje prostředky z hlediska nedodržování přiřazených zásad. Například můžete chtít omezit velikost skladových položek virtuálních počítačů ve vašem prostředí. Po implementaci odpovídajících zásad se u nových i stávajících prostředků bude vyhodnocovat dodržování předpisů. Se správnými zásadami je možné zajistit dodržování předpisů u stávajících prostředků.

## <a name="cross-organization-policy"></a>Zásady pro celou organizaci

Když se vaše cloudová aktiva začnou rozšiřovat napříč mnoha předplatnými, která budou vyžadovat vynucování, budete se muset zaměřit na strategii vynucování pro všechna cloudová aktiva, abyste zajistili konzistenci zásad.

Váš [návrh předplatného](../subscriptions/index.md) musí počítat s tím, že zásady souvisejí s organizační strukturou. Kromě toho, že [skupiny pro správu Azure](../../ready/azure-best-practices/organize-subscriptions.md) pomáhají s podporou složitého uspořádání v rámci návrhu předplatného, je možné je také využít k přiřazování pravidel Azure Policy napříč několika předplatnými.

## <a name="automated-enforcement"></a>Automatizované vynucování

Zatímco standardizované šablony nasazení jsou efektivní v menším měřítku, služba [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) umožňuje rozsáhlou standardizovanou orchestraci zřizování a nasazování řešení Azure. Úlohy napříč několika předplatnými je možné nasadit s konzistentním nastavením zásad pro všechny vytvořené prostředky.

K zajištění funkcí hybridního monitorování pro IT prostředí, ve kterých se integrují cloudové a místní prostředky, možná budete muset použít systémy protokolování a generování sestav. Vaše vlastní systémy monitorování provozu nebo systémy třetích stran můžou nabízet další možnosti vynucování zásad. V případě rozsáhlejších nebo vyspělejších cloudových aktiv zvažte, jak tyto systémy co nejlépe integrovat s cloudovými prostředky.

## <a name="next-steps"></a>Další kroky

Vynucování zásad je pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
