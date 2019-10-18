---
title: Průvodce rozhodováním ohledně konzistence prostředků
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s konzistencí prostředků při plánování migrace do Azure.
author: doodlemania2
ms.author: dermar
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: c32bbb180bc7b78a74681dc4a2554fd449bb21dc
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547880"
---
# <a name="resource-consistency-decision-guide"></a>Průvodce rozhodováním ohledně konzistence prostředků

[Návrh předplatného](../subscriptions/index.md) Azure definuje způsob uspořádání cloudových prostředků ve vztahu ke struktuře, postupům účtování a požadavkům úloh vaší organizace. Kromě této úrovně struktury vyžaduje řešení požadavků zásad správného řízení vaší organizace napříč cloudovými aktivit také možnost konzistentně organizovat, nasazovat a spravovat prostředky v rámci předplatného.

![Diagram možností konzistence prostředků od nejjednodušších po nejsložitější, které odpovídají rychlým odkazům níže](../../_images/decision-guides/decision-guide-resource-consistency.png)

Přejít na: [Základní seskupování](#basic-grouping) | [Konzistence nasazení](#deployment-consistency) | [Konzistence zásad](#policy-consistency) | [Hierarchická konzistence](#hierarchical-consistency) | [Automatizovaná konzistence](#automated-consistency)

Rozhodnutí ohledně úrovně požadavků na konzistenci prostředků cloudových aktiv se řídí primárně těmito faktory: velikost digitálních aktiv po migraci, obchodní požadavky nebo požadavky na prostředí, které zcela nezapadají do stávajících přístupů návrhu předplatných nebo potřeba vynucování zásad správného řízení v průběhu času po nasazení prostředků.

S tím, jak se bude zvyšovat význam těchto faktorů, budou čím dál důležitější také výhody vyplývající ze zajištění konzistentního nasazování, seskupování a správy cloudových prostředků. K dosažení pokročilejších úrovní konzistence prostředků pro splnění rostoucích požadavků je potřeba vynaložit větší úsilí na automatizaci, nástroje a vynucování konzistence, což má za následek delší dobu strávenou správou a sledováním změn.

## <a name="basic-grouping"></a>Základní seskupování

[Skupiny prostředků](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) v Azure představují základní mechanismus pro organizaci prostředků umožňující logické seskupování prostředků v rámci předplatného.

Skupiny prostředků fungují jako kontejnery prostředků se společným životním cyklem A sdílenými omezeními správy, jako jsou požadavky na zásady nebo řízení přístupu na základě role (RBAC). Skupiny prostředků není možné vnořovat a prostředky můžou patřit pouze do jedné skupiny prostředků. Všechny akce řídicí roviny se provádějí se všemi prostředky ve skupině prostředků. Například při odstranění skupiny prostředků se také odstraní všechny prostředky v dané skupině. Pro správu skupin prostředků je vhodné zvážit následující otázky:

1. Vyvíjí se obsah skupin prostředků společně?
1. Je obsah skupiny prostředků spravovaný, aktualizovaný a monitorovaný najednou, a to stejnými lidmi nebo týmy?
1. Vyřazuje se obsah skupin prostředků z provozu společně?

Pokud jste na libovolnou z výš uvedených otázek odpověděli _NE_, příslušný prostředek by měl být umístěný jinde, v jiné skupině prostředků.

> [!IMPORTANT]
> Skupina prostředků jsou také specifické pro jednotlivé oblasti. Pro prostředky je ale běžné, že jsou v různých oblastech v rámci stejné skupiny prostředků, protože se spravují dohromady, jak je popsáno výš. Další informace o výběru oblastí najdete [tady](../regions/index.md).

## <a name="deployment-consistency"></a>Konzistence nasazení

Platforma Azure využívá základní mechanismus seskupování prostředků a poskytuje systém umožňující nasazovat prostředky do cloudového prostředí pomocí šablon. Pomocí šablon můžete vytvářet konzistentní zásady organizace a vytváření názvů při nasazování úloh a vynucovat aspekty vašeho návrhu nasazování a správy prostředků.

[Šablony Azure Resource Manageru](https://docs.microsoft.com/azure/azure-resource-manager/template-deployment-overview) umožňují opakovaně nasazovat prostředky v konzistentním stavu s využitím předem stanovené konfigurace a struktury skupin prostředků. Šablony Resource Manageru pomáhají definovat sadu standardů, které představují základ vašich nasazení.

Například můžete mít standardní šablonu pro nasazení úlohy webového serveru, která obsahuje dva virtuální počítače jako webové servery v kombinaci s nástrojem pro vyrovnávání zatížení pro distribuci provozu mezi těmito servery. Tuto šablonu pak můžete opakovaně používat k vytvoření sady virtuálních počítačů a nástroje pro vyrovnávání zatížení s identickou strukturou, kdykoli se bude tento typ úlohy vyžadovat, a bude vám stačit jenom změnit příslušný název nasazení a IP adresu.

Tyto šablony můžete také nasazovat programově a integrovat s vašimi systémy CI/CD.

## <a name="policy-consistency"></a>Konzistence zásad

Aby se zajistilo, že se při vytvoření prostředků použijí zásady správného řízení, část návrhu seskupování prostředků zahrnuje použití společné konfigurace při nasazování prostředků.

Kombinace skupin prostředků a standardizovaných šablon Resource Manageru umožňuje vynucování standardů z hlediska požadovaných nastavení v nasazeních a pravidel [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview), která se mají použít pro jednotlivé skupiny prostředků nebo prostředky.

Například můžete mít požadavek, aby se všechny virtuální počítače nasazené v rámci předplatného připojovaly ke společné podsíti spravované centrálním IT týmem. Pokud chcete pro úlohu vytvořit samostatnou skupinu prostředků a do ní nasazovat požadované virtuální počítače, můžete vytvořit standardní šablonu pro nasazování virtuálních počítačů úloh. Tato skupina prostředků bude obsahovat pravidlo zásad, které povolí připojení ke sdílené podsíti pouze síťovým rozhraním v této skupině prostředků.

Podrobnější popis vynucování zásad v rámci cloudového nasazení najdete v tématu [Vynucování zásad](../policy-enforcement/index.md).

## <a name="hierarchical-consistency"></a>Hierarchická konzistence

Skupiny prostředků umožňují v rámci organizace zajistit podporu dalších úrovní hierarchie předplatného, a to díky uplatňování řízení přístupu a pravidel Azure Policy na úrovni skupiny prostředků. S rostoucí velikostí vašich cloudových aktiv však možná bude potřeba zajistit podporu složitějších požadavků na zásady správného řízení mezi předplatnými. Toho je možné dosáhnout s využitím hierarchie smlouvy Azure Enterprise (podnik/oddělení/účet/předplatné).

[Skupiny pro správu Azure](https://docs.microsoft.com/azure/governance/management-groups) umožňují uspořádání předplatných do sofistikovanějších organizačních struktur, a to seskupením předplatných v jiné hierarchii, než je hierarchie vaší smlouvy Enterprise. Tato alternativní hierarchie umožňuje používat mechanismy řízení přístupu a vynucování zásad pro různá předplatná a prostředky, které obsahují. Pomocí hierarchií skupin pro správu je možné sladit předplatná cloudových aktiv s provozními nebo obchodními požadavky zásad správného řízení. Další informace najdete v [Průvodci rozhodováním ohledně předplatného](../subscriptions/index.md).

## <a name="automated-consistency"></a>Automatizovaná konzistence

U rozsáhlých cloudových nasazení jsou globální zásady správného řízení čím dál důležitější a zároveň složitější. Při nasazování prostředků je důležité automaticky používat a vynucovat požadavky zásad správného řízení. Stejně důležité je, aby aktualizované požadavky splňovala také stávající nasazení.

Služba [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) umožňuje organizacím zajistit podporu globálních zásad správného řízení rozsáhlých cloudových aktiv v Azure. Podrobné plány přesahují možnosti, které poskytují standardní šablony Azure Resource Manageru, a vytvářejí kompletní orchestrace nasazení schopné nasazovat prostředky a uplatňovat pravidla zásad. Podrobné plány podporují správu verzí, možnost aktualizovat všechna předplatná, ve kterých se použil podrobný plán, a možnost uzamknout nasazená předplatná, aby se zabránilo neoprávněnému vytváření a úpravám prostředků.

Tyto balíčky pro nasazení umožňují vývojovým a IT týmům rychle nasazovat nové úlohy a síťové prostředky, které vyhovují měnícím se požadavkům zásad organizace. Podrobné plány je také možné integrovat do kanálů CI/CD a zajistit tak v nasazeních používání revidovaných standardů zásad správného řízení ihned po jejich aktualizaci.

## <a name="next-steps"></a>Další kroky

Konzistence prostředků je pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
