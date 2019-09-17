---
title: Průvodce rozhodováním ohledně předplatného
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s předplatnými cloudové platformy jako základní službou při migraci do Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 06/07/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 209de4c03474a956edf629c9c24f6b29f492284b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023636"
---
# <a name="subscription-decision-guide"></a>Průvodce rozhodováním ohledně předplatného

Efektivní návrh předplatného pomáhá organizacím vytvořit strukturu pro uspořádání prostředků v Azure během přechodu na cloud.

Každý prostředek v Azure, jako je třeba virtuální počítač nebo databáze, je přidružený k předplatnému. Zavádění Azure začíná vytvořením předplatného Azure, jeho přidružením k účtu a nasazením prostředků do tohoto předplatného. Přehled těchto pojmů najdete v článku věnovaném [základní koncepci Azure](../../ready/considerations/fundamental-concepts.md).

Jak se vaše digitální aktiva v Azure budou rozšiřovat, budete pro splnění vašich požadavků pravděpodobně muset vytvořit další předplatná. Azure umožňuje definovat hierarchii skupin pro správu sloužící k uspořádání předplatných a snadno propojovat zásady s odpovídajícími prostředky. Další informace najdete v tématu věnovaném [škálování s využitím několika předplatných Azure](../../ready/considerations/scaling-subscriptions.md).

Tady je několik základních příkladů využití skupin pro správu k oddělení různých úloh:

- **Produkční prostředí v porovnání s neprodukčním prostředím:** Některé podniky vytvářejí skupiny pro správu za účelem oddělení svých produkčních a neprodukčních předplatných. Skupiny pro správu těmto uživatelům umožňují snadnější správu rolí a zásad. Například v neprodukčním předplatném můžou mít vývojáři povolený přístup **přispěvatele**, ale v produkčním prostředí můžou mít pouze přístup **čtenáře**.
- **Interní služby v porovnání s externími službami:** Podobně jako v případě produkčních a neprodukčních úloh podniky pro interní služby a externí služby určené pro zákazníky často mají různé požadavky, zásady a role.

Tento průvodce rozhodováním pomáhá porovnat různé přístupy k uspořádání hierarchie skupin pro správu.

## <a name="subscription-design-patterns"></a>Způsoby návrhu předplatného

Protože každá organizace je jiná, jsou skupiny pro správu Azure navržené tak, aby byly flexibilní. Modelování vašich cloudových aktiv tak, aby odráželo hierarchii vaší organizace, pomáhá definovat a aplikovat zásady na vyšších úrovních hierarchie a využívat dědičnost k zajištění toho, že se tyto zásady automaticky uplatní i pro skupiny pro správu, které jsou v hierarchii níž. Přestože se předplatná dají mezi různými skupinami pro správu přesouvat, je vhodné navrhnout takovou počáteční hierarchii skupin pro správu, která odpovídá očekávaným potřebám vaší organizace.

Před dokončením návrhu předplatného také zvažte, jak váš návrh můžou ovlivnit aspekty související s [konzistencí prostředků](../resource-consistency/index.md).

> [!NOTE]
> Smlouvy Enterprise (EA) pro Azure umožňují definovat jinou organizační hierarchii pro fakturační účely. Tato hierarchie se liší od hierarchie skupin pro správu, která se zaměřuje na zajištění modelu dědičnosti pro snadné využití vhodných zásad a řízení přístupu pro vaše prostředky.

Následující modely předplatného odrážejí postupné zvyšování propracovanosti návrhu předplatného. Po nich následuje několik pokročilejších hierarchií, které by vaší organizaci mohly vyhovovat:

### <a name="single-subscription"></a>Jedno předplatné

Jedno předplatné na účet může být dostačující pro organizace, které potřebují nasadit malé množství prostředků hostovaných v cloudu. Jedná se o první model předplatného, který implementujete v začátcích přechodu na cloud a který umožňuje méně rozsáhlá experimentální nebo testovací nasazení za účelem prozkoumání jeho možností.

### <a name="production-and-nonproduction-pattern"></a>Model produkčního a neprodukčního prostředí

Jakmile jste připravení nasadit úlohu do produkčního prostředí, měli byste přidat další předplatné. Pomůže vám udržet vaše produkční data a další aktiva mimo prostředí pro vývoj a testování. Můžete také snadno využít dvě různé sady zásad napříč prostředky ve dvou předplatných.

![Model produkčních a neprodukčních předplatných](../../_images/ready/basic-subscription-model.png)

### <a name="workload-separation-pattern"></a>Model oddělení úloh

Když organizace přidává do cloudu nové úlohy, může mít různé vlastnictví nebo základní rozdělení zodpovědností za následek několik předplatných v produkčních i neprodukčních skupinách pro správu. Přestože tento přístup zajišťuje základní oddělení úloh, nevyužívá významných výhod modelu dědičnosti k automatickému uplatnění zásad napříč podmnožinou předplatných.

![Model oddělení úloh](../../_images/ready/management-group-hierarchy.png)

### <a name="application-category-pattern"></a>Model kategorií aplikací

Jak se cloudová stopa organizace zvětšuje, obvykle se vytvářejí další předplatná, a to kvůli zajištění podpory aplikací, které se zásadně liší z hlediska obchodní důležitosti, požadavků na dodržování předpisů, řízení přístupu nebo požadavků na ochranu dat. Na základě modelu produkčních a neprodukčních předplatných jsou předplatná podporující tyto aplikační kategorie uspořádaná v rámci odpovídající produkční nebo neprodukční skupiny pro správu. Tato předplatná obvykle vlastní a spravuje personál starající se o centrální provoz IT.

![Model kategorií aplikací](../../_images/infra-subscriptions/application.png)

Každá organizace si volí jiný způsob kategorizace aplikací a předplatná často rozděluje v závislosti na konkrétních aplikacích nebo službách nebo podle archetypů aplikací. Tato kategorizace je často navržená tak, aby podporovala úlohy, u kterých se předpokládá využití většiny limitů prostředků předplatného, nebo oddělila klíčové úlohy, aby se zajistilo, že v rámci těchto limitů nebudou soupeřit s jinými úlohami. Mezi úlohy, u kterých by v rámci tohoto modelu mohlo být odůvodnitelné použití samostatného předplatného, patří:

- Klíčové úlohy
- Aplikace s chráněnými daty
- Experimentální aplikace
- Aplikace podléhající zákonným požadavkům (jako je HIPAA nebo FedRAMP)
- Dávkové úlohy
- Úlohy s velkým objemem dat, jako je Hadoop
- Kontejnerizované úlohy využívající orchestrátory nasazení, jako je Kubernetes
- Analytické úlohy

### <a name="functional-pattern"></a>Funkční model

Funkční model na základě hierarchie skupin pro správu organizuje předplatná a účty podle jejich funkcí, jako jsou finance, prodej nebo IT podpora, a to s využitím hierarchie skupin pro správu.

### <a name="business-unit-pattern"></a>Model obchodních jednotek

Model obchodních jednotek na základě hierarchie skupin pro správu seskupuje předplatná a účty podle kategorie zisků a ztrát, obchodní jednotky, oddělení, centra zisku nebo podobné obchodní struktury.

### <a name="geographic-pattern"></a>Geografický model

Pro organizace fungující v globálním měřítku geografický model na základě hierarchie skupin pro správu seskupuje předplatná a účty podle geografických oblastí.

## <a name="mixed-patterns"></a>Smíšené modely

Hierarchie skupin pro správu mohou mít až šest úrovní. Máte tak možnost flexibilně vytvářet hierarchie, které kombinují několik těchto modelů tak, aby vyhovovaly potřebám vaší organizace. Například následující diagram znázorňuje organizační hierarchii, která kombinuje model obchodních jednotek s geografickým modelem.

![Model smíšených předplatných](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Související prostředky

- [Správa přístupu k prostředkům v Azure](../../govern/resource-consistency/resource-access-management.md)
- [Několik vrstev zásad správného řízení ve velkých firmách](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Několik geografických oblastí](../../migrate/expanded-scope/multiple-regions.md)

## <a name="next-steps"></a>Další kroky

Návrh předplatného je pouze jedna ze základních komponent infrastruktury, která během přechodu na cloud vyžaduje rozhodování na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
