---
title: Průvodce rozhodováním ohledně pojmenování a označování prostředků
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s organizací a označováním prostředků jako základní službou při migraci do Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 77fe8ba38b2ebf79ddceeb9fe2df940e8e333cc6
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73238855"
---
# <a name="resource-naming-and-tagging-decision-guide"></a>Průvodce rozhodováním ohledně pojmenování a označování prostředků

Pokud nemáte jednoduchá nasazení, organizace cloudových prostředků je jedním z nejdůležitějších úkolů IT týmů. Organizace prostředků slouží primárně ke třem účelům:

- **Správa prostředků:** Vaše IT týmy potřebují mít možnost rychle vyhledat prostředky související s konkrétními úlohami, prostředími a skupinami vlastnictví nebo jiné důležité informace. Organizace prostředků je klíčové při přiřazování rolí v organizaci a přístupových oprávnění ke správě prostředků.
- **Automatizace:** Kromě usnadnění správy prostředků IT týmům vám vhodné organizační schéma umožní využívat automatizaci v rámci vytváření prostředků, monitorování provozu a vytváření procesů DevOps.
- **Účetnictví:** Aby mohly IT týmy informovat obchodní skupiny o spotřebě cloudových prostředků, musí nejprve zjistit, které úlohy a týmy využívají které prostředky. Aby bylo možné zajistit podporu přístupů, jako je účtování vratek a metody showback, cloudové prostředky musí být uspořádané tak, aby bylo zřejmé jejich vlastnictví a využití.

## <a name="tagging-decision-guide"></a>Průvodce rozhodováním ohledně označování

![Diagram možností označování od nejjednodušších po nejsložitější, které odpovídají rychlým odkazům níže](../../_images/decision-guides/decision-guide-resource-tagging.png)

Přejít na: [Základní zásady vytváření názvů](#baseline-naming-conventions) | [Vzory označování prostředků](#resource-tagging-patterns) | [Další informace](#learn-more)

Váš přístup k označování může být jednoduchý nebo složitý a může klást důraz na cokoli od podpory IT týmů spravujících cloudové úlohu až po integraci informací souvisejících se všemi aspekty obchodní činnosti.

Pokud se zaměříte na označování sladěné s IT, jako je označování na základě úloh, funkcí nebo prostředí, zjednodušíte tím složité monitorování prostředků a výrazně usnadníte rozhodování ohledně správy založené na provozních požadavcích.

Schémata označování, mezi která patří zaměření sladěné s obchodní činností, jako je účetnictví, obchodní vlastnictví nebo důležitost pro firmu, můžou vyžadovat větší časové investice do vytvoření standardů označování odrážejících obchodní zájmy a udržování těchto standardů v průběhu času. Výsledkem tohoto procesu je však systém označování, který poskytuje lepší možnosti zahrnutí nákladů na IT prostředky a jejich hodnoty do celkové obchodní činnosti. Toto přidružení obchodní hodnoty prostředku k jeho provozním nákladům je prvním krokem ke změně vnímání nákladového střediska IT v rámci širší organizace.

## <a name="baseline-naming-conventions"></a>Základní zásady vytváření názvů

Standardizované zásady vytváření názvů představují výchozí bod při organizaci prostředků hostovaných v cloudu. Vhodně strukturovaný systém vytváření názvů vám umožní rychle identifikovat prostředky pro účely správy i účetnictví. Pokud v jiných částech organizace již existují zásady vytváření názvů pro IT, zvažte, jestli by se jim měly vaše zásady vytváření názvů v cloudu přizpůsobit, nebo jestli byste měli zavést nové cloudové standardy.

Mějte také na paměti, že různé typy prostředků Azure mají rozdílné [požadavky na pojmenování](../../ready/azure-best-practices/naming-and-tagging.md). Vaše zásady vytváření názvů musí s těmito požadavky na pojmenování být kompatibilní.

## <a name="resource-tagging-patterns"></a>Vzory označování prostředků

Pro účely sofistikovanější organizace, než můžou poskytovat konzistentní zásady vytváření názvů, cloudové platformy podporují možnost označovat prostředky.

*Značky* jsou elementy metadat připojené k prostředkům. Značky se skládají z párů řetězců klíč-hodnota. Je jen na vás, jaké hodnoty v těchto párech použijete. Používání konzistentní sady globálních značek v rámci komplexních zásad pojmenování a označování je ale důležitou součástí celkových zásad správného řízení.

Během procesu plánování si položte následující otázky, které vám pomůžou určit, jaký druh informací vaše značky prostředku musí podporovat:

- Je potřeba, aby se vaše zásady pojmenování a označování integrovaly se stávajícími zásadami pojmenování a organizace ve vaší společnosti?
- Budete implementovat účetní systém pracující s vratkami a metodou showback? Budete potřebovat přidružovat prostředky k účetním informacím o odděleních, obchodních skupinách a týmech na podrobnější úrovni, než umožňuje prostý rozpis na úrovni předplatného?
- Musí být z označení zřejmé podrobnosti, jako jsou požadavky prostředku na dodržování právních předpisů? A co podrobnosti o provozu, jako jsou požadavky na dostupnost, plány oprav nebo požadavky na zabezpečení?
- Jaké značky budou podle centrálních zásad IT vyžadovat všechny prostředky? Jaké značky budou volitelné? Můžou jednotlivé týmy implementovat vlastní schémata označování?

Následující běžné vzory označování uvádějí příklady možného použití označování k organizaci cloudových prostředků. Tyto vzory se vzájemně nevylučují a je možné je používat souběžně. Získáte tak více možností organizace prostředků podle potřeb vaší společnosti.

<!-- markdownlint-disable MD033 -->

| Typ značky | Příklady | Popis |
|-----|-----|-----|
| Funkční            | app = catalogsearch1 <br/>tier = web <br/>webserver = apache<br/>env = prod <br/>env = staging <br/>env = dev                 | Kategorizuje prostředky v závislosti na jejich účelu v rámci úlohy, prostředí, ve kterém jsou nasazené, nebo jiných podrobnostech o jejich funkci nebo provozu.                                 |
| Classification        | confidentiality=private<br/>sla = 24hours                                 | Klasifikuje prostředek podle toho, k čemu slouží a jaké zásady pro něj platí.                               |
| Účetnictví            | department = finance <br/>project = catalogsearch <br/>region = northamerica | Umožňuje přidružení prostředku s konkrétními skupinami v rámci organizace pro účely fakturace. |
| Partnerství           | owner = jsmith <br/>contactalias = catsearchowners<br/>stakeholders = user1;user2;user3<br/>                       | Poskytuje informace o lidech (mimo IT), se kterými prostředek souvisí nebo které ovlivňuje.                      |
| Účel               | businessprocess=support<br/>businessimpact=moderate<br/>revenueimpact=high   | Zajistí sladění prostředků s obchodními funkcemi za účelem lepší podpory investičního rozhodování.  |

<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Další informace

Další informace o vytváření názvů a označování v Azure najdete tady:

- [Zásady vytváření názvů pro prostředky Azure](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). V těchto pokynech najdete doporučené zásady vytváření názvů pro prostředky Azure.
- [Používání značek k uspořádání prostředků Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags?toc=/azure/billing/TOC.json). Značky v Azure můžete používat na úrovni skupin prostředků i jednotlivých prostředků. Ve všech účetních sestavách založených na použitých značkách tak můžete využít flexibilní možnosti nastavení úrovně podrobností.

## <a name="next-steps"></a>Další kroky

Označování prostředků je pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
