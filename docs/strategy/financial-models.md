---
title: Finanční model pro migraci do cloudu
description: Seznamte se s tím, co potřebujete k vytvoření finančního modelu, který přesně představuje úplnou obchodní hodnotu cloudové transformace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: ebc85c5a76d9f53b0117567fc79de51488e9b51d
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337991"
---
# <a name="create-a-financial-model-for-cloud-transformation"></a>Vytvoření finančního modelu pro cloudovou transformaci

Vytvoření finančního modelu, který přesně představuje úplnou obchodní hodnotu jakékoli transformace v cloudu, může být složité. Finanční modely a obchodní odůvodnění se v různých organizacích velmi liší. Tento článek stanoví některé vzorce a ukazuje několik věcí, které se při vedoucím vytváření finančních modelů obvykle nevyskytují.

## <a name="return-on-investment"></a>Návratnost investic

Návratnost investic (návratnost investic) je často důležitou kritérií pro C-Suite nebo panel. Návratnost investic se používá k porovnání různých způsobů investování omezených kapitálových prostředků. Vzorec pro ni je poměrně jednoduchý. Podrobnosti, které budete potřebovat pro vytvoření každého vstupu ke vzorci, nemusí být jednoduché. Návratnost investic v podstatě představuje množství návratnosti, která je výsledkem počáteční investice. Obvykle se reprezentuje jako procento:

![Návratnost investic se rovná (zisk z investice minus náklady na investici) dělený náklady na investici](../_images/strategy/formula-roi.png)

V dalších částech provedeme data, která budete potřebovat k výpočtu počátečních investic, a zisk z investování (příjmů).

## <a name="calculate-initial-investment"></a>Vypočítat počáteční investice

Počáteční investice jsou kapitálové výdaje a provozní výdaje potřebné k dokončení transformace. Klasifikace nákladů se může lišit v závislosti na účetních modelech a preferencích CFO. Tato kategorie by ale obsahovala položky, jako jsou profesionální služby k transformaci, softwarové licence používané jenom během transformace, náklady na cloudové služby během transformace a potenciální náklady na zaměstnance placené při transformaci. .

Pokud chcete vytvořit odhad počáteční investice, přidejte tyto náklady.

## <a name="calculate-the-gain-from-investment"></a>Vypočítat zisk z investice

Výpočet zisků z investice často vyžaduje druhý vzorec, který je specifický pro obchodní výsledky a související technické změny. Výpočet výdělků je těžší než výpočet snížení nákladů.

Pokud chcete vypočítat tržby, potřebujete dvě proměnné:

![Zisk z investic se rovná rozdílům příjmů a rozdílů nákladů](../_images/strategy/formula-gain-from-investment.png)

Tyto proměnné jsou popsány v následujících částech.

## <a name="revenue-deltas"></a>Rozdíl příjmů

Rozdíl příjmů by měl být předpověď ve spolupráci se zúčastněnými podnikateli. Poté, co se podnikatelům podniku souhlasí s dopadem na výnosy, je možné ji využít ke zlepšení pozice zisku.

## <a name="cost-deltas"></a>Cenové rozdíly

Cenové rozdíly jsou množství zvýšení nebo snížení, které bude výsledkem transformace. Nezávislé proměnné mohou ovlivnit cenové rozdíly. Tržby jsou v podstatě na základě pevných nákladů, jako je snížení nákladů na kapitál, vyhýbání se nákladů, snižování provozních nákladů a snížení odpisů. Následující části popisují některé cenové rozdíly, které je třeba vzít v úvahu.

### <a name="depreciation-reduction-or-acceleration"></a>Snížení nebo zrychlení odpisování

Pokyny k odpisování můžete mluvit s týmem finančního oddělení nebo finančního oddělení. Následující informace mají sloužit jako obecný odkaz na téma o odpisování.

Když se kapitál investuje do akvizice assetu, může se tato investice použít k finančnímu nebo daňovému účelu, aby vznikly průběžné výhody za očekávanou životnost assetu. Některé společnosti vidí jako pozitivní daňovou výhodu odpisy. Ostatní se zobrazí jako potvrzené a průběžné výdaje podobné dalším opakovaným výdajům, které jsou spojené s ročním rozpočtem IT.

Promluvte si finanční kancelář, abyste zjistili, jestli je eliminace odpisů, a pokud by došlo k kladnému příspěvku na cenové rozdíly.

### <a name="physical-asset-recovery"></a>Obnovení fyzického prostředku

V některých případech je možné vyřazené prostředky prodávat jako zdroj výnosů. Tento výnos se často účtuje na snížení nákladů pro jednoduchost. Ale je to skutečně zvýšení výnosů a může být zdaněno. Promluvte si finanční kancelář, abyste pochopili životaschopnost této možnosti a zohlednili výsledný výnos.

### <a name="operational-cost-reductions"></a>Snížení provozních nákladů

Opakované výdaje potřebné k provozu firmy se často nazývají provozní výdaje. Toto je široká kategorie. Ve většině účetních modelů zahrnuje:

- Licencování softwaru.
- Výdaje na hostování.
- Elektrické platby
- Nájemné za skutečné nemovitosti.
- Výdaje na chlazení.
- Pro operace jsou vyžadovány dočasné pracovníky.
- Nájem zařízení.
- Náhradní části.
- Smlouvy o údržbě.
- Opravte služby.
- Služby pro provozní kontinuitu a zotavení po havárii (BCDR).
- Další výdaje, které nevyžadují schválení kapitálovými náklady.

Tato kategorie poskytuje jeden z nejvyšších rozdílových rozdílů. Při zvažování migrace do cloudu je doba, po kterou je tento seznam vyčerpávající, nevyužita zřídka. Položte otázky týmu CIO a finance, abyste zajistili, že se účtují všechny provozní náklady.

### <a name="cost-avoidance"></a>Vyhnout se nákladům

Pokud se očekává provozní výdaje, ale ještě nejsou ve schváleném rozpočtu, nemusí se vejít do kategorie snížení nákladů. Například pokud je třeba licence VMware a Microsoft znovu vyjednávat a platit v příštím roce, ještě nejsou plně kvalifikované náklady. Snížení předpokládaných nákladů se za běžné náklady považují za provozní náklady. V takovém případě by se však měly u nich odkazovat jako na "zamezení nákladů", dokud není dokončeno vyjednávání a schvalování rozpočtu.

### <a name="soft-cost-reductions"></a>Snížení nákladů na měkké náklady

V některých společnostech můžou být do rozdílových statistik zahrnuté i krátkodobé náklady, jako je snížení provozní složitosti nebo snížení počtu zaměstnanců pro provoz do datového centra. Ale bez měkkých nákladů nemusí být vhodné. Když zahrnete snížení nákladů na krátkodobé náklady, vložíte nedokumentované předpoklady, které snižuje náklady na hmotný úsporu nákladů. Technologie technologických projektů zřídka vede k rychlému obnovení nákladů.

### <a name="headcount-reductions"></a>Snížení počtu zaměstnanců

Časová úspora zaměstnanců často zahrnuje snížení nákladů na náklady. Když se tato časová úspora mapuje na skutečné snížení nároku na IT nebo zaměstnanců, můžou se vypočítat samostatně jako snížení počtu zaměstnanců.

To znamená, že dovednosti vyžadované v místním prostředí se obecně mapují na podobnou (nebo vyšší) sadu dovedností potřebných v cloudu. Takže lidé nejsou všeobecně po migraci do cloudu.

K výjimce dojde, když třetí strana nebo poskytovatel spravovaných služeb (MSP) poskytuje provozní kapacitu. Pokud jsou systémy IT spravovány třetí stranou, mohly by být provozní náklady nahrazeny nativním řešením cloudu nebo cloudovým nativním rozhraním MSP. V cloudu Native MSP se pravděpodobně bude pracovat efektivněji a může se snížit náklady. Pokud je to tento případ, snížení provozních nákladů patří do výpočtů s pevnými náklady.

### <a name="capital-expense-reductions-or-avoidance"></a>Snížení nebo zamezení kapitálových výdajů

Kapitálové výdaje se mírně liší od provozních nákladů. Obecně se tato kategorie řídí aktualizačními cykly nebo rozšířením Datacenter. Příkladem rozšíření Datacenter by byl nový cluster s vysokým výkonem, který bude hostovat řešení pro velké objemy dat nebo datový sklad. Tento výdaj se obecně vejde do kategorie kapitálových výdajů. Častější jsou základní aktualizační cykly. Některé společnosti mají tuhý cyklus aktualizace hardwaru, což znamená, že assety jsou vyřazené a nahrazené běžným cyklem (obvykle každých tři, pět nebo osm let). Tyto cykly se často shodují s cykly zapůjčení prostředků nebo s předpokládaným životním rozsahem zařízení. Když dojde k pokusu o aktualizační cyklus, nakreslí se kapitálové výdaje na získání nového zařízení.

Pokud je obnovovací cyklus schválen a rozpočtový, může převod cloudu přispět k eliminaci těchto nákladů. Pokud cyklus obnovení naplánujete, ale dosud neschválili, cloudová transformace by se mohla vyhnout velkým výdajům. Do rozdílové ceny budou přidány obě srážky.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o modelech [cloudového účetnictví](./cloud-accounting.md) .

> [!div class="nextstepaction"]
> [Cloudové účetnictví](./cloud-accounting.md)
