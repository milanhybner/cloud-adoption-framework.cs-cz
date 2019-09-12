---
title: První projekt přijetí do cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si o implementaci prvního projektu pro přijetí do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 6f3e1ad47b329e39addd9fff087568e4124f8859
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825078"
---
<!-- markdownlint-disable MD026 -->

# <a name="first-cloud-adoption-project"></a>První projekt přijetí do cloudu

Existuje výuková křivka a časový závazek spojený s plánováním přijetí cloudu. I u zkušených týmů trvalo plánování trvat delší dobu: čas k zarovnávání zúčastněných stran, čas potřebný ke shromažďování a analýze dat, čas potřebný k ověření dlouhodobých rozhodnutí a čas potřebný k zarovnávání osob, procesů a technologií. V rámci maximální produktivity při přijímání je plánování zaměřené na souběžné přijetí, vylepšení při každém vydání a při každé migraci zatížení do cloudu. Je důležité pochopit rozdíl mezi plánem přijetí do cloudu a strategií přijetí cloudu. Potřebujete dobře definovanou strategii, která usnadňuje implementaci plánu přijetí do cloudu a pomůže vám s ním.

Rozhraní pro přijetí do cloudu pro Azure popisuje procesy pro přijetí do cloudu a provoz úloh hostovaných v cloudu. Každý proces v rámci definice strategie, plánování, připravenosti, přijetí a provozních fází vyžaduje mírné rozšiřování technických, obchodních a provozních dovedností. Některé z těchto dovedností můžou pocházet z řízeného učení. Mnohé z nich se ale nejúčinnějším způsobem získávají prostřednictvím praktických zkušeností.

Spuštění prvního procesu přijetí paralelně s vývojem plánu přináší některé výhody:

- Vytvoření nárůstu místo pro podporu učení a průzkumu
- Poskytněte týmu příležitost pro vývoj nezbytných dovedností.
- Vytváření situací, které připomáhají novým přístupům k spolupráci
- Identifikujte mezery mezi dovednostmi a potenciálními partnerskými požadavky
- Poskytněte do plánu hmotné vstupy.

## <a name="first-project-criteria"></a>První kritérium projektu

Váš první projekt přijetí by měl být v [](./motivations-why-are-we-moving-to-the-cloud.md) souladu s vašimi motivací pro přijetí do cloudu. Kdykoli je to možné, váš první projekt by měl také Ukázat pokrok směrem k definovanému [obchodnímu výsledku](./business-outcomes/how-to-use-the-business-outcome-template.md).

## <a name="first-project-expectations"></a>Očekávání prvního projektu

Projekt prvního přijetí vašeho týmu může mít za následek produkční nasazení nějakého druhu. Nejedná se ale vždy o případ. Stanovte správné očekávání na začátku. Tady je několik moudrých očekávání k nastavení:

- Tento projekt je zdrojem učení.
- Tento projekt může mít za následek nasazení v produkčním prostředí, ale bude to pravděpodobně vyžadovat další úsilí.
- Výstupem tohoto projektu je sada jasných požadavků, které poskytují řešení pro dlouhodobé produkční prostředí.

## <a name="first-project-examples"></a>Příklady prvního projektu

Pro podporu výše uvedených kritérií poskytuje tento seznam příklad prvního projektu pro každou kategorii motivace:

- **Kritické obchodní události:** Když je kritická obchodní událost primární motivace, implementace nástroje jako [Azure Site Recovery](../migrate/azure-migration-guide/migrate.md?tabs=Tools#azure-site-recovery) může být dobrým prvním projektem. Během migrace můžete pomocí tohoto nástroje rychle migrovat assety Datacenter. Ale během prvního projektu ho můžete použít čistě jako nástroj pro zotavení po havárii, což snižuje závislosti na prostředcích pro obnovení po havárii v rámci datového centra.

- **Motivace migrace:** Když je migrace primární motivací, je vhodné začít s migrací nekritického zatížení. Průvodce migrací na [Azure](../ready/azure-readiness-guide/index.md) a příručka k [migraci Azure](../migrate/azure-migration-guide/index.md) vám poskytnou pokyny k migraci prvního zatížení.

- **Podněty pro inovace:** Když je inovace primární motivace, vytvoření cíleného vývojového a testovacího prostředí může být skvělým prvním projektem.

Mezi další příklady projektů pro první přijetí patří:

- **Zotavení po havárii a Kontinuita podnikových aplikací (DRBC):** Nad rámec Azure Site Recovery můžete implementovat několik strategií DRBC jako první projekt.
- **Neprovozním** Nasaďte nevýrobní instanci úlohy.
- **Zálohovat** Studené úložiště může dát do prostředků datového centra datový kmen. Přesun těchto dat do cloudu je plný rychlý Win.
- **Konec podpory (EOS):** Migrace assetů, které dosáhly konce podpory, je další rychlý soubor, který vytváří technické dovednosti. Mohlo by také docházet k tomu, že se vyhnete nákladným smlouvám podpory nebo nákladům na licencování.
- **Rozhraní virtuálních klientských počítačů (VDI):** Vytváření virtuálních ploch pro vzdálené zaměstnance může poskytovat rychlý Win. V některých případech může tento první projekt přijetí také snížit závislost na nákladných privátních sítích, a to ve prospěch komoditních veřejných připojení k Internetu.
- **Vývoj a testování:** Z místních prostředí můžete odebrat vývoj a testování, abyste vývojářům poskytovali řízení, flexibilitu a kapacitu samoobslužných služeb.
- **Jednoduché aplikace (méně než pět):** Modernizovat a migrujte jednoduchou aplikaci, abyste rychle získali vývojářské a provozní prostředí.
- **Výkonnostní Labs:** Pokud potřebujete vysoce škálovatelný výkon v nastavení testovacího prostředí, využijte Cloud k rychlému a nákladově efektivnímu zajišťování těchto cvičení po krátkou dobu.
- **Datová platforma:** Vytvoření Data Lake s škálovatelným výpočetním prostředím pro analýzy, vytváření sestav nebo úlohy strojového učení.

## <a name="next-steps"></a>Další kroky

Po zahájení prvního projektu pro přijetí do cloudu může tým cloudové strategie změnit svůj pozornost na dlouhodobý [plán přijímání](../plan/index.md)do cloudu.

> [!div class="nextstepaction"]
> [Sestavení plánu přijetí cloudu](../plan/index.md)
