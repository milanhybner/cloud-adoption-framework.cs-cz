---
title: Zásady správného řízení, zabezpečení a dodržování předpisů v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zjistěte, jak pro vaše prostředí Azure nastavit zásady správného řízení, zabezpečení a dodržování předpisů.
author: tvuylsteke
ms.author: kfollis
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 7a305e1bd3ef8f3f7325905c523d9fe5ded2fc60
ms.sourcegitcommit: 3655aa7f3e80249e0b2b562cd40dd750afc82043
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/20/2019
ms.locfileid: "74251319"
---
# <a name="governance-security-and-compliance-in-azure"></a>Zásady správného řízení, zabezpečení a dodržování předpisů v Azure

Při vytváření podnikových zásad a plánování strategie zásad správného řízení můžete pomocí nástrojů a služeb, jako jsou Azure Policy, Azure Blueprints a Azure Security Center, prosazovat a automatizovat rozhodnutí organizace v zásad správného řízení. Než začnete s plánováním zásad správného řízení, identifikujte pomocí [nástroje Governance Benchmark](https://cafbaseline.com) možné mezery v přístupu vaší organizace k zásadám správného řízení. Další informace o vývoji procesů zásad správného řízení najdete v [pokynech pro zásady správného řízení Architektury přechodu na cloud pro Azure](../../govern/index.md).

# <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

Azure Blueprints umožňuje cloudovým architektům a centrálním oddělením IT definovat opakovatelnou sadu prostředků Azure, která implementuje a dodržuje standardy, vzory a požadavky organizace. Vývojářským týmům Azure Blueprints umožňuje rychle vytvářet nová prostředí s důvěrou, že je vytvářejí v souladu s předpisy organizace, a s využitím sady předdefinovaných komponent – třeba síťových – ke zrychlení vývoje a distribuce.

Podrobné plány představují deklarativní způsob, jak orchestrovat nasazení různých šablon prostředků a dalších artefaktů jako:

- Přiřazení rolí
- Přiřazení zásad
- Šablony Azure Resource Manageru
- Skupiny prostředků

## <a name="create-a-blueprint"></a>Vytvoření podrobného plánu

Vytvoření podrobného plánu:

::: zone target="chromeless"

1. Přejděte na **Blueprints – Začínáme**.
1. V části **Vytvořit podrobný plán** vyberte **Vytvořit**.
1. Vyfiltrujte seznam podrobných plánů a vyberte odpovídající podrobný plán.
1. Zadejte **Název podrobného plánu** a vyberte odpovídající **Umístění definice**.
1. Klikněte na **Další: Artefakty >>** a zkontrolujte artefakty, které jsou součástí podrobného plánu.
1. Klikněte na **Uložit koncept**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Přejděte na [Blueprints – Začínáme](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. V části **Vytvořit podrobný plán** vyberte **Vytvořit**.
1. Vyfiltrujte seznam podrobných plánů a vyberte odpovídající podrobný plán.
1. Zadejte **Název podrobného plánu** a vyberte odpovídající **Umístění definice**.
1. Klikněte na **Další: Artefakty >>** a zkontrolujte artefakty, které jsou součástí podrobného plánu.
1. Klikněte na **Uložit koncept**.

::: zone-end

## <a name="publish-a-blueprint"></a>Publikování podrobného plánu

Publikování artefaktů podrobného plánu v předplatném:

::: zone target="chromeless"

1. Přejděte na **Blueprints – Definice podrobných plánů**.
1. Vyberte podrobný plán, který jste vytvořili v předchozích krocích.
1. Zkontrolujte definici podrobného plánu a vyberte **Publikovat podrobný plán**.
1. Zadejte číslo **Verze** (například _1.0_) a případné **Poznámky ke změnám** a pak vyberte **Publikovat**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Přejděte na [Podrobné plány – Definice podrobných plánů](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Vyberte definici podrobného plánu, kterou jste vytvořili v předchozích krocích.
1. Zkontrolujte definici podrobného plánu a vyberte **Publikovat podrobný plán**.
1. Zadejte číslo **Verze** (například _1.0_) a případné **Poznámky ke změnám** a pak vyberte **Publikovat**.

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Architektura přechodu na cloud: Průvodce rozhodováním ohledně konzistence prostředků](../../decision-guides/resource-consistency/index.md)
- [Ukázky podrobných plánů založené na standardech](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end

# <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

Azure Policy je služba, která slouží k vytváření, přiřazování a správě zásad. Tyto zásady vynucují na vašich prostředcích pravidla, aby tyto prostředky dodržovaly předpisy vyplývající z vašich firemních standardů a ze smluv o úrovni služeb. Azure Policy prohledává vaše prostředky s cílem identifikovat prostředky, které nedodržují předpisy vyplývající z implementovaných zásad. Například můžete mít zásadu, která ve vašem prostředí povoluje pouze určitou velikost virtuálních počítačů. Když tuto zásadu implementujete, vyhodnotí stávající virtuální počítače ve vašem prostředí i všechny nové virtuální počítače, které jsou nasazené. Vyhodnocení zásad pro vás vygeneruje události dodržování předpisů, které můžete použít k monitorování a generování sestav.

Vezměte v úvahu běžné zásady pro:

- Vynucování označování prostředků a skupin prostředků
- Omezení oblastí pro nasazené prostředky
- Omezení nákladných skladových položek pro určité prostředky
- Auditování využití důležitých volitelných funkcí, jako jsou disky spravované v Azure

::: zone target="chromeless"

## <a name="action"></a>Akce

Přiřazení předdefinované zásady ke skupině pro správu, předplatnému nebo skupině prostředků

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

## <a name="apply-a-policy"></a>Použití zásady

Použití zásady pro skupinu prostředků:

1. Přejděte do části [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Vyberte **Přiřadit zásadu**.

## <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Architektura přechodu na cloud: Průvodce rozhodováním ohledně vynucování zásad](../../decision-guides/policy-enforcement/index.md)

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center hraje důležitou roli ve strategii správného řízení. Pomůže vám udržovat si přehled o zabezpečení, protože:

- Poskytuje jednotný přehled o zabezpečení úloh.
- Shromažďuje, prohledává a analyzuje data o zabezpečení z nejrůznějších zdrojů, včetně bran firewall a dalších partnerských řešení.
- Poskytuje užitečná doporučení zabezpečení k opravě problémů před tím, než je bude možné zneužít.
- Umožňuje používat zásady zabezpečení napříč hybridními cloudovými úlohami za účelem zajištění dodržování bezpečnostních standardů.

Řada těchto funkcí zabezpečení, včetně zásad zabezpečení a doporučení, je k dispozici bezplatně. Některé z pokročilejších funkcí, jako je přístup k virtuálním počítačům za běhu a podpora hybridních úloh, jsou k dispozici ve službě Security Center úrovně Standard. Přístup k virtuálním počítačům za běhu může pomoct omezit možnosti síťových útoků díky tomu, že řídí přístup k portům pro správu na virtuálních počítačích Azure.

> [!TIP]
> Služba Azure Security Center je ve výchozím nastavení povolená ve všech předplatných. Doporučujeme povolit shromažďování dat z virtuálních počítačů, aby služba Azure Security Center mohla nainstalovat svého agenta a začít shromažďovat data.

::: zone target="docs"

Pokud chcete prozkoumat Azure Security Center, přejděte na web [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Azure Security Center](https://docs.microsoft.com/azure/security-center)
- [Přístup k virtuálnímu počítači za běhu](https://docs.microsoft.com/azure/security-center/security-center-just-in-time#how-does-just-in-time-access-work)
- [Porovnání cenových úrovní Standard a Free](https://azure.microsoft.com/pricing/details/security-center)
- [Architektura přechodu na cloud: Disciplína zásad správného řízení standardních hodnot zabezpečení](../../govern/security-baseline/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Akce

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end
