---
title: Metriky a indikátory tolerance odchylky rizika konzistence prostředků
description: Kvantitativní stanovení tolerance obchodního rizika souvisejícího s konzistencí prostředků v rozhraní Microsoft Cloud pro přijetí v Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 71b29f1c2d87b916701767e5c74c2699cf8aa4fa
ms.sourcegitcommit: 1de39a4c3954512892f11e3d1330a04e95ce187d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/24/2020
ms.locfileid: "77567720"
---
# <a name="resource-consistency-metrics-indicators-and-risk-tolerance"></a>Metriky konzistence prostředků, indikátory a tolerance rizik

Tento článek vám pomůže kvantifikovat toleranci obchodního rizika v souvislosti s konzistencí prostředků. Definování metrik a indikátorů vám pomůže vytvořit obchodní případ pro zajištění investic do splatnosti oboru konzistence prostředků.

## <a name="metrics"></a>Metriky

Obor konzistence prostředků se zaměřuje na rizika související s provozní správou nasazení v cloudu. V rámci analýzy rizik budete chtít shromažďovat data týkající se vašich IT operací, abyste zjistili, kolik rizik čelíte, a jak důležité investice do zásad správného řízení konzistence prostředků jsou pro vaše plánovaná cloudová nasazení.

Každá organizace má různé provozní scénáře, ale následující položky znázorňují užitečné příklady metrik, které byste měli shromažďovat při vyhodnocování tolerance rizik v rámci oboru konzistence prostředků:

- **Cloudové prostředky.** Celkový počet prostředků nasazených v cloudu
- **Neoznačené prostředky.** Počet prostředků bez požadovaného účtu, obchodního dopadu nebo organizačních značek.
- **Nepoužívané prostředky.** Počet prostředků, ve kterých jsou možnosti paměti, procesoru a sítě trvale nevyužitelné.
- **Vyčerpání prostředků.** Počet prostředků, ve kterých jsou funkce paměti, procesoru nebo sítě vyčerpány zatížením.
- **Stáří prostředků.** Čas od posledního nasazení nebo změny prostředku
- **Virtuální počítače v kritickém stavu.** Počet nasazených virtuálních počítačů, u kterých se zjistí jeden nebo několik kritických problémů, které je potřeba řešit, aby se obnovily normální funkce.
- **Výstrahy podle závažnosti.** Celkový počet výstrah na nasazeném prostředku rozepsaný podle závažnosti.
- **Síťová propojení ve špatném stavu.** Počet prostředků s problémy s připojením k síti.
- **Poškozené koncové body služby.** Počet problémů s koncovými body externí sítě.
- **Incidenty stavu služby poskytovatele cloudu.** Počet výpadků nebo incidentů výkonu způsobených poskytovatelem cloudu.
- **Smlouvy o úrovni služeb.** To může zahrnovat závazky Microsoftu pro provozuschopnost a konektivitu služeb Azure, jakož i závazky, které společnost vytvořila pro externí a interní zákazníky.
- **Dostupnost služby.** Procento skutečných úloh hostovaných v cloudu, které jsou v porovnání s očekávanou dobou provozu.
- **Plánovaná doba obnovení (RTO).** Maximální přijatelná doba, po kterou může být aplikace nedostupná po incidentu.
- **Cíl bodu obnovení (RPO).** Maximální doba ztráty dat, která je přijatelná během havárie. Například pokud ukládáte data do jedné databáze, nereplikujete je do jiné databáze a provádíte zálohování každou hodinu, mohlo by dojít ke až ztrátě dat uložených za poslední hodinu.
- **Průměrná doba obnovení (MTTR).** Průměrná doba potřebná k obnovení komponenty po selhání.
- **Střední doba mezi chybami (MTBF).** Doba, po kterou může součást rozumně očekávat spouštění mezi výpadky. Tato metrika vám pomůže vypočítat, jak často bude služba nedostupná.
- **Stav zálohování** Počet záloh, které jsou aktivně synchronizovány.
- **Stav obnovení.** Počet úspěšně provedených operací obnovení.

## <a name="risk-tolerance-indicators"></a>Indikátory tolerance rizik

Cloudové platformy nabízejí základní sadu funkcí, které umožňují týmům nasazení efektivně spravovat malá nasazení bez rozsáhlých dalších plánování a procesů. V důsledku toho malé vývojové a testovací nebo experimentální první úlohy, které zahrnují relativně malé množství cloudových prostředků, reprezentují nízkou úroveň rizika a pravděpodobně nebudou potřebovat moc na cestě k zásadám konzistence formálních prostředků.

Vzhledem k nárůstu velikosti vaší cloudové složitosti je ale obtížné spravovat vaše prostředky. Díky většímu množství prostředků v cloudu se schopnost identifikovat vlastnictví prostředků a prostředků ovládacího prvku, která je zásadní pro minimalizaci rizik. Vzhledem k tomu, že se do cloudu nasazují nejdůležitější úlohy, je doba provozu služby v kritickém stavu a tolerance výpadku služby, která je potenciálních nákladů, se rychle snižuje.

V počátečních fázích přijímání v cloudu spolupracujete s vaším týmem IT a podnikovými účastníky a Identifikujte [obchodní rizika](./business-risks.md) související s konzistencí prostředků a pak určíte přijatelné standardní hodnoty pro toleranci rizik. V této části architektury pro přijetí do cloudu najdete příklady, ale podrobná rizika a směrné plány vaší společnosti nebo nasazení se můžou lišit.

Jakmile budete mít základnu, stanovte minimální srovnávací testy představující nepřijatelný nárůst zjištěných rizik. Tyto srovnávací testy fungují jako triggery, pokud potřebujete provést akci k nápravě těchto rizik. Tady je několik příkladů, jak provozní metriky, jako jsou výše popsané, můžou zvýšit investice do oboru konzistence prostředků.

- **Tagování a Trigger názvů.** Společnost s více než _x_ prostředky, které neobsahují požadované informace o označování nebo které nedodržují standardy pojmenování, by měla zvážit investování do oboru konzistence prostředků, aby se tyto standardy lépe vylepšit a zajistila konzistentní jejich použití na prostředky nasazené v cloudu.
- **Aktivační událost nadměrného zřízeného prostředku.** Pokud má společnost pravidelně více než _x%_ prostředků na základě malých objemů dostupné paměti, procesoru nebo sítě, navrhuje se investice do oboru konzistence prostředků, které vám pomůžou optimalizovat využití prostředků u těchto položek.
- **Aktivační událost podzřízeného prostředků.** Pokud má společnost více než _x%_ prostředků pravidelně vyčerpáním kapacity dostupné paměti, procesoru nebo sítě, navrhne se investice do oboru konzistence prostředků, aby se zajistilo, že tyto prostředky budou mít prostředky nezbytné k tomu, aby se předešlo přerušení služeb.
- **Aktivační událost stáří prostředku** Společnost s více než _x_ prostředky, které se _během více než měsíců_ neaktualizovala, by mohla těžit z investic do oboru konzistence prostředků, která je určená k zajištění, že aktivní prostředky jsou opravené a v pořádku, při vyřazení zastaralých nebo jinak nepoužívaných prostředků.
- **Aktivační událost smlouvy na úrovni služby.** Společnost, která nemůže splnit své smlouvy o úrovni služeb svým externím zákazníkům nebo interním partnerům, by měla investovat do disciplíny akcelerace nasazení, aby se snížil výpadek systému.
- **Aktivační události pro čas obnovení.** Pokud společnost překročí požadované prahové hodnoty pro čas obnovení po selhání systému, měl by investovat do zvýšení disciplíny akcelerace nasazení a systémů, aby se snížily nebo odstranily chyby nebo vliv jednotlivých součástí výpadku.
- **Aktivační událost stavu virtuálního počítače.** Společnost, která má více než _x%_ virtuálních počítačů, u kterých dochází k závažnému problému se stavem, by měla investovat do oboru konzistence prostředků, aby identifikovala problémy a vylepšila stabilitu virtuálních počítačů
- **Aktivační událost stavu sítě.** Společnost, která má více než _x%_ síťových podsítí nebo koncových bodů s problémy s připojením, by měla investovat do oboru konzistence prostředků k identifikaci a řešení problémů se sítí.
- **Aktivační událost pokrytí zálohování.** Společnost s _x%_ důležitých prostředků bez aktuálnosti záloh by mohla těžit z vyšší investice do oboru konzistence prostředků, aby se zajistila konzistentní strategie zálohování.
- **Aktivační událost stavu zálohování.** Společnost, která má více než _x%_ selhání operací obnovení, by měla investovat do oboru konzistence prostředků, aby identifikovala problémy se zálohováním a zajistila ochranu důležitých prostředků.

Přesné metriky a triggery, které používáte k měření tolerance rizika a úroveň investic do oboru konzistence prostředků, budou specifické pro vaši organizaci, ale výše uvedené příklady by měly sloužit jako užitečnou základnu pro diskuzi v rámci zásad správného řízení cloudu. hodnotící.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md), metriky dokumentů a indikátory tolerance, které odpovídají aktuálnímu plánu přijetí do cloudu.

Projděte si ukázkové zásady konzistence prostředků jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

> [!div class="nextstepaction"]
> [Kontrola ukázkových zásad](./policy-statements.md)
