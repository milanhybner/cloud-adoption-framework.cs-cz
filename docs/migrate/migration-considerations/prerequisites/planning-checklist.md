---
title: Migrační prostředí – kontrolní seznam pro plánování
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ověřte před migrací připravenost prostředí.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8d216d65685c7e58fc622a5d7f820f0c23097fa4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833294"
---
# <a name="migration-environment-planning-checklist---validate-environmental-readiness-prior-to-migration"></a>Kontrolní seznam pro plánování migračního prostředí – ověření připravenosti prostředí před migrací

Jako počáteční krok v procesu migrace je potřeba vytvořit správné prostředí v cloudu pro příjem, hostování a podporu migrovaných prostředků. Tento článek obsahuje seznam toho, co je před migrací potřeba ověřit v aktuálním prostředí.

Následující kontrolní seznam je sladěný s pokyny v [části o připravenosti](../../../ready/index.md) v Architektuře přechodu na cloud. V této části najdete pokyny k realizaci všech následujících činností.

## <a name="effort-type-assumption"></a>Předpoklad typu úsilí

V tomto článku a kontrolním seznamu se předpokládá, že migrace do cloudu proběhne _změnou hostitele_ nebo _přechodem na cloud_.

## <a name="governance-alignment"></a>Sladění se zásadami správného řízení

Prvním a nejdůležitějším rozhodnutím ohledně jakéhokoli prostředí připraveného k migraci je volba sladění se zásadami správného řízení. Bylo při sladění zásad správného řízení se základními prvky migrace dosaženo shody? Tým přechodu na cloud by měl přinejmenším vědět, jestli je cílem této migrace jediné prostředí s omezenými zásadami správného řízení, plně řízené prostředí nebo nějaká varianta mezi tím. Další možnosti a pokyny k uvedení zásad správného řízení do souladu najdete v článku o [Sladění se zásadami správného řízení a dodržováním předpisů](../../expanded-scope/governance-or-compliance.md).

## <a name="cloud-readiness-implementation"></a>Implementace připravenosti na cloud

Bez ohledu na to, jestli se při prvotní migraci rozhodnete provést sladění s obecnější strategií zásad správného řízení cloudu, budete muset zajistit, aby bylo prostředí pro nasazení do cloudu nakonfigurované pro podporu vašich úloh.

Pokud migraci hodláte sladit se strategií zásad správného řízení cloudu hned od začátku, budete muset použít [Pět disciplín zásad správného řízení v cloudu](../../../governance/governance-disciplines.md), které vám pomohou kvalifikovaně rozhodnout o zásadách, sadách nástrojů a prosazovacích mechanismech, které sladí vaše cloudové prostředí s celkovými podnikovými požadavky. Příklady implementace tohoto modelu pomocí služeb Azure najdete v [praktických průvodcích pro návrh zásad správného řízení](../../../governance/journeys/index.md) v Architektuře přechodu na cloud.

Pokud vaše prvotní migrace není přesně sladěná s obecnější strategií zásad správného řízení cloudu, je stále potřeba se postarat o obecnější problémy organizace, přístupu a plánování infrastruktury. S těmito rozhodnutími ohledně připravenosti na cloud vám pomůže [Průvodce připraveností pro Azure](../../../ready/azure-readiness-guide/index.md).

> [!CAUTION]
> Důrazně doporučujeme, abyste vytvořili strategii zásad správného řízení pro vše, co je nad rámec prvotní migrace úloh.

Bez ohledu na úroveň sladění se zásadami správného řízení budete muset učinit rozhodnutí související s následujícími tématy.

### <a name="resource-organization"></a>Organizace prostředků

Na základě rozhodnutí o sladění zásad správného řízení by se před migrací měl stanovit postup organizace a nasazení prostředků.

### <a name="nomenclature"></a>Názvosloví

Před migrací by se měl zavést konzistentní přístup k pojmenování prostředků společně se schématy konzistentního pojmenování.

### <a name="resource-governance"></a>Zásady správného řízení prostředků

Před migrací by se mělo učinit rozhodnutí týkající se nástrojů pro řízení prostředků. Tyto nástroje nemusí být plně implementované, ale měl by být vybrán a otestován určitý směr. Doporučuje se, aby tým zásad správného řízení cloudu před migrací definoval a vyžadoval implementaci minimálního realizovatelného produktu (MVP) pro nástroje zásad správného řízení.

## <a name="network"></a>Síť

Vaše cloudové úlohy budou pro podporu koncových uživatelů a správcovského přístupu vyžadovat zřízení virtuálních sítí. Na základě rozhodnutí týkajících se organizace prostředků a zásad správného řízení prostředků byste měli vybrat přístup k síti, který bude sladěný s požadavky na zabezpečení IT. Rozhodnutí ohledně sítě by navíc měla být v souladu se všemi omezeními hybridní sítě potřebné k provozování úloh v backlogu migrace a podporovat přístup k prostředkům hostovaným místně.

## <a name="identity"></a>Identita

Služby cloudové identity jsou předpokladem pro nabízení správy identit a přístupu pro cloudové prostředky. Než budete pokračovat, slaďte svoji strategii správy identit s plány přechodu na cloud. Pokud například migrujete stávající místní prostředky, zvažte podporu hybridních identit pomocí [synchronizace adresářů](../../../decision-guides/identity/index.md), abyste během migrace a po ní používali konzistentní sadu uživatelských přihlašovacích údajů jak místně, tak v cloudovém prostředí.

## <a name="next-steps"></a>Další postup

Pokud prostředí splňuje minimální požadavky, může být považováno za schválené pro připravenost na migraci. Článek [Kulturní komplikace a správa změn](./culture-complexity.md) pomáhá sladěním rolí a zodpovědností zajistit správná očekávání během realizace plánu.

> [!div class="nextstepaction"]
> [Kulturní komplikace a správa změn](./culture-complexity.md)