---
title: Průvodce rozhodováním ohledně předplatného
description: Zorientujte se ve strategiích návrhu předplatných a hierarchiích skupin pro správu pro uspořádání prostředků Azure
author: alexbuckgit
ms.author: abuck
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: e733280147a16287e92ab93334111950a2583497
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355458"
---
# <a name="subscription-decision-guide"></a>Průvodce rozhodováním ohledně předplatného

Efektivní návrh předplatného pomáhá organizacím vytvořit strukturu pro uspořádání a správu prostředků v Azure během přechodu na cloud. Tento průvodce vám pomůže rozhodnout, kdy vytvořit další předplatná a rozšířit hierarchii skupin pro správu v rámci podpory vašich obchodních priorit.

## <a name="prerequisites"></a>Požadavky

Zavádění Azure začíná vytvořením předplatného Azure, jeho přidružením k účtu a nasazením prostředků, jako jsou virtuální počítače a databáze, do tohoto předplatného. Přehled těchto pojmů najdete v článku věnovaném [základní koncepci Azure](../../ready/considerations/fundamental-concepts.md).

- [Vytvoření počátečních předplatných](../../ready/azure-best-practices/initial-subscriptions.md)
- [Vytvořte další předplatná](../../ready/azure-best-practices/scale-subscriptions.md) pro škálování vašeho prostředí Azure.
- [Uspořádejte a spravujte předplatná](../../ready/azure-best-practices/organize-subscriptions.md) pomocí skupin pro správu Azure.

## <a name="modeling-your-organization"></a>Modelování vaší organizace

Protože každá organizace je jiná, jsou skupiny pro správu Azure navržené tak, aby byly flexibilní. Modelování vašich cloudových aktiv tak, aby odráželo hierarchii vaší organizace, pomáhá definovat a aplikovat zásady na vyšších úrovních hierarchie a využívat dědičnost k zajištění toho, že se tyto zásady automaticky uplatní i pro skupiny pro správu, které jsou v hierarchii níž. Přestože se předplatná dají mezi různými skupinami pro správu přesouvat, je vhodné navrhnout takovou počáteční hierarchii skupin pro správu, která odpovídá očekávaným potřebám vaší organizace.

Před dokončením návrhu předplatného také zvažte, jak váš návrh můžou ovlivnit aspekty související s [konzistencí prostředků](../resource-consistency/index.md).

> [!NOTE]
> Smlouvy Enterprise (EA) pro Azure umožňují definovat jinou organizační hierarchii pro fakturační účely. Tato hierarchie se liší od hierarchie skupin pro správu, která se zaměřuje na zajištění modelu dědičnosti pro snadné využití vhodných zásad a řízení přístupu pro vaše prostředky.

## <a name="subscription-design-strategies"></a>Strategie návrhu předplatného

Vezměte v úvahu následující strategie návrhu předplatného, které vám umožní řešit obchodní priority.

### <a name="workload-separation-strategy"></a>Strategie oddělení úloh

Když organizace přidává do cloudu nové úlohy, může mít různé vlastnictví nebo základní rozdělení zodpovědností za následek několik předplatných v produkčních i neprodukčních skupinách pro správu. Přestože tento přístup zajišťuje základní oddělení úloh, nevyužívá významných výhod modelu dědičnosti k automatickému uplatnění zásad napříč podmnožinou předplatných.

![Strategie oddělení úloh](../../_images/ready/management-group-hierarchy-v2.png)

### <a name="application-category-strategy"></a>Strategie kategorií aplikací

Jak se cloudová stopa organizace zvětšuje, obvykle se vytvářejí další předplatná, a to kvůli zajištění podpory aplikací, které se zásadně liší z hlediska obchodní důležitosti, požadavků na dodržování předpisů, řízení přístupu nebo požadavků na ochranu dat. Na základě počátečních produkčních a neprodukčních předplatných jsou předplatná podporující tyto aplikační kategorie uspořádaná v rámci odpovídající produkční nebo neprodukční skupiny pro správu. Tato předplatná obvykle vlastní a spravuje personál starající se o centrální provoz IT.

![Strategie kategorií aplikací](../../_images/infra-subscriptions/application.png)

Každá organizace si volí jiný způsob kategorizace aplikací a předplatná často rozděluje v závislosti na konkrétních aplikacích nebo službách nebo podle archetypů aplikací. Tato kategorizace je často navržená tak, aby podporovala úlohy, u kterých se předpokládá využití většiny limitů prostředků předplatného, nebo oddělila klíčové úlohy, aby se zajistilo, že v rámci těchto limitů nebudou soupeřit s jinými úlohami. Mezi úlohy, u kterých by mohlo být odůvodnitelné použití samostatného předplatného, patří:

- Klíčové úlohy
- Aplikace, které jsou součástí „nákladů prodaného zboží“ (COGS) ve vaší společnosti. Příklad: Každá instance widgetu společnosti X obsahuje modul Azure IoT, který odesílá telemetrii. Může to vyžadovat vyhrazené předplatné pro účely účtování / zásad správného řízení v rámci COGS.
- Aplikace podléhající zákonným požadavkům, jako je HIPAA nebo FedRAMP.

### <a name="functional-strategy"></a>Funkční strategie

Funkční strategie organizuje předplatná a účty podle jejich funkcí, jako jsou finance, prodej nebo IT podpora, a to s využitím hierarchie skupin pro správu.

### <a name="business-unit-strategy"></a>Strategie obchodních jednotek

Strategie obchodních jednotek na základě hierarchie skupin pro správu seskupuje předplatná a účty podle kategorie zisků a ztrát, obchodní jednotky, oddělení, centra zisku nebo podobné obchodní struktury.

### <a name="geographic-strategy"></a>Geografická strategie

Pro organizace fungující v globálním měřítku geografická strategie na základě hierarchie skupin pro správu seskupuje předplatná a účty podle geografických oblastí.

## <a name="mixing-subscription-strategies"></a>Smíšení strategií předplatných

Hierarchie skupin pro správu mohou mít až šest úrovní. Máte tak možnost flexibilně vytvářet hierarchie, které kombinují několik těchto strategií tak, aby vyhovovaly potřebám vaší organizace. Například následující diagram znázorňuje organizační hierarchii, která kombinuje strategii obchodních jednotek s geografickou strategií.

![Strategie smíšených předplatných](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Související prostředky

- [Správa přístupu k prostředkům v Azure](../../govern/resource-consistency/resource-access-management.md)
- [Několik vrstev zásad správného řízení ve velkých firmách](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Několik geografických oblastí](../../migrate/azure-best-practices/multiple-regions.md)

## <a name="next-steps"></a>Další kroky

Návrh předplatného je pouze jedna ze základních komponent infrastruktury, která během přechodu na cloud vyžaduje rozhodování na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o dalších strategiích používaných při rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
