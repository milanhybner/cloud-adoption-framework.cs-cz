---
title: Možnosti zásad správného řízení cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Popisuje tvorbu možností zásad správného řízení cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: bb40dc63fcf125548e2734cc18edf36adacb2570
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030336"
---
# <a name="cloud-governance-capabilities"></a>Možnosti zásad správného řízení cloudu

Libovolný druh změny vygeneruje nová rizika. Schopnosti zásad správného řízení cloudu zajišťují, že rizika a tolerance rizik jsou správně vyhodnoceny a spravovány. Tato schopnost zajišťuje správnou identifikaci rizik, která není možné tolerovat firmou. Lidé, kteří tuto možnost poskytují, můžou převést rizika na řízení podnikových zásad. Zásady správy se pak provádějí pomocí definovaných pravidel, která spouštějí zaměstnanci, kteří poskytují možnosti zásad správného řízení pro Cloud.

## <a name="possible-sources-for-this-capability"></a>Možné zdroje pro tuto funkci

V závislosti na požadovaných obchodních výsledcích by se měly dovednosti potřebné k poskytování úplných možností zásad správného řízení v cloudu poskytnout:

- Zásady správného řízení IT
- Podniková architektura
- IT operace
- IT infrastruktura
- Sítě
- Identita
- Virtualizace
- Provozní kontinuita a zotavení po havárii
- Vlastníci aplikace v rámci IT

Schopnost zásad správného řízení cloudu identifikuje rizika související s aktuálními a budoucími verzemi. Tato možnost se zobrazuje v úsilí vyhodnotit rizika, porozumět potenciálním dopadům a rozhodnout o toleranci rizik. V takovém případě se plány dají rychle aktualizovat, aby odrážely měnící se potřeby [cloudové možnosti pro přijetí](./cloud-adoption.md).

## <a name="key-responsibilities"></a>Klíčové zodpovědnosti

Hlavním clem jakékoli schopnosti zásad správného řízení cloudu je vyrovnávat konkurenční síly při transformaci a zmírnění rizik. Řízení cloudu navíc zajišťuje, že při [přijímání](./cloud-adoption.md) v cloudu se dozvíte o datech a klasifikaci prostředků a pokynůch k architektuře, které řídí všechny přístupy k přijetí. Tým bude také spolupracovat s cloudovým [centrem kvality](./cloud-center-of-excellence.md) , aby bylo možné používat automatizované přístupy k řízení cloudových prostředí.

Tyto úlohy obvykle provádí funkce zásad správného řízení cloudu na měsíční úrovni.

**Úlohy prvotního plánování:**

- Pochopení [obchodních rizik](../govern/policy-compliance/risk-tolerance.md) zavedených podle plánu
- Vyjádření [tolerance firmy pro riziko](../govern/policy-compliance/risk-tolerance.md)
- Podpora při vytváření MVP pro zásady [správného řízení](../govern/guides/index.md)

**Probíhající měsíční úkoly:**

- Pochopení [obchodních rizik](../govern/policy-compliance/risk-tolerance.md) zavedených během každé vydané verze
- Vyjádření [tolerance firmy pro riziko](../govern/policy-compliance/risk-tolerance.md)
- Podpora při přírůstkovém zlepšování [zásad a požadavků na dodržování předpisů](../govern/policy-compliance/index.md)

## <a name="meeting-cadence"></a>Tempo schůzky

Možnost zásad správného řízení cloudu je obvykle poskytována pracovním týmem. Časový závazek od každého člena týmu bude představovat vysoké procento denních plánů. Příspěvky nebudou omezeny na schůzky a cykly zpětné vazby.

## <a name="additional-participants"></a>Další účastníci

Níže jsou zastoupeni účastníci, kteří se často účastní aktivit zásad správného řízení cloudu:

- Vedoucí od střední správy a přímých přispěvatelů v klíčových rolích, které jsou určené k zastupování firmy, vám pomůžou vyhodnotit tolerance rizik.
- Poskytované možnosti zásad správného řízení cloudu jsou rozšířením [schopností cloudové strategie](./cloud-strategy.md). Stejně jako CIO a obchodní vedoucí se očekává, že budou zapojeny do možností strategie cloudu, očekává se, že jejich přímé sestavy budou zapojeny do aktivit zásad správného řízení cloudu.
- Podnikoví zaměstnanci, kteří jsou členy obchodní jednotky, kteří úzce pracují s vedením podnikového podnikání, by měli mít možnost rozhodovat o podnikovém a technickém riziku.
- Zaměstnanci v oblasti informačních technologií (IT) a zabezpečení informací (jsou), kteří rozumí technickým aspektům transformace cloudu, můžou obsluhovat rotující kapacitu namísto konzistentního poskytovatele možností zásad správného řízení cloudu.

## <a name="maturation-of-cloud-governance-capability"></a>Maturation možnosti zásad správného řízení cloudu

Některé velké organizace mají stávající a vyhrazené týmy, které se zaměřují na řízení IT. Tyto týmy se specializují na řízení rizik v rámci portfolia IT prostřednictvím metodologií, jako je ITIL nebo ITSM. Když tyto týmy existují, můžete rychle zrychlit následující modely splatnosti. Tým pro řízení IT ale doporučuje zkontrolovat model zásad správného řízení pro Cloud a pochopit, jak se zásad správného řízení v cloudu mírně posouvá. Mezi klíčové články patří [rozšíření firemních zásad do cloudu](../govern/corporate-policy.md) a [pět oborů řízení cloudu](../govern/governance-disciplines.md).

**Bez zásad správného řízení:** Je běžné, že se organizace přesunou do cloudu bez jasných plánů pro řízení. V souvislosti s tím, že se v souvislosti se zabezpečením, náklady, škálováním a operacemi začnou začínat konverzace o potřebě modelu zásad správného řízení a lidem personálně přidružit procesy přidružené k tomuto modelu. Spuštění těchto konverzací před tím, než se stane obavy, je vždy dobrým prvním krokem k překonání antipatternu "bez zásad správného řízení". Tato konverzace může usnadnit oddíl [definování podnikových zásad](../govern/corporate-policy.md) .

**Zakázané zásady správného řízení:** Pokud se budou týkat zabezpečení, nákladů, škálování a operací, přejdou nezodpovězené projekty a obchodní cíle a zablokují se. Nedostatek správného zásad správného řízení vygeneruje obavy, nejistotu a pochybnosti mezi zúčastněnými stranami a inženýry. Zastavte je ve svých stopách tím, že provedete akci včasnou. Dvě příručky pro zásady správného řízení definované v rámci architektury pro přijetí do cloudu vám pomůžou začít s malým nastavením zásad, které minimalizují nejistotu a vyspělé řízení přístupu v čase. Vyberte si ze [složitého podnikového Průvodce](../govern/guides/complex/index.md) nebo [standardní podniková příručka](../govern/guides/standard/index.md).

**Dobrovolné řízení:** V každém podniku je ale Brave Souls. Ty Gallant, kteří jsou ochotni přejít v týmu a pomáhat týmu, aby se dozvěděli o svých chybách. Často se jedná o způsob, jakým se spouští zásad správného řízení, zejména v menších společnostech Tyto Brave Souls včas řeší některé problémy a zadávají týmy pro přijetí cloudu do konzistentní dobře spravované sady osvědčených postupů.

Úsilí těchto jednotlivců je mnohem lepší než scénáře "bez zásad správného řízení" nebo "zásadně blokovaný". I když by jejich snaha měla být Commended, tento přístup by se neměl zaměňovat se zásadami správného řízení. Správný zásad správného řízení vyžaduje více než občasnou podporu pro zajištění konzistence, což je cílem jakéhokoli dobrého přístupu ke správě. Pokyny v [pěti oborech zásad správného řízení cloudu](../govern/governance-disciplines.md) mohou pomoci při vývoji tohoto oboru.

**Cloudové implicitní správce:** Tento moniker se stal označením pro celou řadu cloudových architektů, kteří se specializují na zásady správného řízení v rané fázi. V případě prvního spuštění postupů zásad správného řízení se výsledky projeví podobně jako u dobrovolníků týkajících se zásad správného řízení. Existuje však jeden zásadní rozdíl. Cloudový implicitní správce má na mysli plán. V této fázi zralosti stráví tým čas tím, že se bude zabývat tím, že cloudové architekti, kteří předtím získali dřív, vyčistili. Cloud implicitní správce ale zarovnává toto úsilí s dobře strukturovanými [podnikovými zásadami](../govern/corporate-policy.md). Využívají taky nástroje pro automatizaci zásad správného řízení, jako jsou ty, které jsou uvedené v [MVP MVP pro řízení](../govern/guides/complex/index.md).

Dalším zásadním rozdílem mezi cloudovým implicitní správce a dobrovolníkem zásad správného řízení je podpora vedoucího řízení. V této smlouvě jsou další hodiny nad pravidelným očekáváním z důvodu jejich získání. Cloud implicitní správce získá podporu od vedoucího ke snížení denních povinností, aby bylo zajištěno, že by bylo možné do zvýšení zásad správného řízení cloudu investovat pravidelné přidělování času.

**Strážce cloudu:** Díky postupům zásad správného řízení přesvědčit a jejich přijetí týmy přijímání v cloudu se role cloudových architektů, kteří se specializují na zásady správného řízení, mění bit, stejně jako role týmu zásad správného řízení cloudu. Obecně platí, že účinnější postupy získají pozornost pro odborníky na danou problematiku, kteří můžou přispět k posílení ochrany poskytované implementacemi zásad správného řízení.

I když je rozdíl malý, je důležité rozlišovat při sestavování jazykové verze IT zaměřené na zásady správného řízení. Cloud implicitní správce vyčistí přehledy, které udělal inovativní cloudové architekty, a tyto dvě role mají přirozené tření a protichůdné cíle. Cloudový stráž pomáhá udržet Cloud v bezpečí, takže ostatní cloudové architekty se můžou rychleji pohybovat s menším počtem obav.

Strážci cloudu začínají pokročilejším způsobem správného řízení, který urychluje nasazování platforem a usnadňuje týmům jejich potřebám v oblasti životního prostředí, takže se můžou rychleji pohybovat. Příklady těchto pokročilejších funkcí se zobrazují v přírůstkových vylepšeních MVP pro řízení MVP, jako je například [zlepšení standardních hodnot zabezpečení](../govern/guides/complex/security-baseline-improvement.md).

**Cloudové akcelerátory:** Cloudové strážce a cloudové starají přirozeně vylove skripty a automatizace, které urychlují nasazení prostředí, platforem nebo dokonce součástí různých aplikací. Dodržení a sdílení těchto skriptů kromě centralizovaných odpovědností zásad správného řízení vyvíjí pro tyto architekty v celém IT vysokou úroveň dodržování.

Specialisté na zásady správného řízení, kteří otevřou své spravované skripty, můžou rychleji poskytovat technologické projekty a vkládat zásady správného řízení do architektury úloh. Tento vliv na úlohy a podporu dobrých vzorů návrhu zvyšují akcelerátory cloudu na vyšší úroveň specialisty na zásady správného řízení.

**Globální zásady správného řízení:** Pokud organizace závisí na globálně rozptýleném IT potřebě, může to být významné odchylky v provozu a zásady správného řízení v různých geografických oblastech. Požadavky obchodní jednotky a dokonce i místní požadavky na svrchovanost dat můžou způsobit, že osvědčené postupy zásad správného řízení budou v konfliktu s požadovanými operacemi. V těchto scénářích podporuje model zásad správného řízení minimální životaschopnou konzistenci a lokalizované řízení. Článek na [více úrovních zásad správného řízení](../govern/guides/complex/multiple-layers-of-governance.md) poskytuje další přehledy o tom, jak dosáhnout této úrovně zralosti.

Každá společnost je jedinečná, a proto jejich požadavky zásad správného řízení. Vyberte si úroveň zralosti, která odpovídá vaší organizaci, a využijte rozhraní pro přijetí do cloudu, abyste mohli využít postupy, procesy a nástroje, které vám pomůžou.

## <a name="next-steps"></a>Další postup

V případě vyspělosti zásad správného řízení cloudu budou týmy k dispozici k tomu, aby měli Cloud v minulosti rychlejší tempo. Pokračující úsilí při přijímání cloudu má za následek, že bude možné v provozu IT aktivovat splatnost. Tento maturation může také vyžadovat vývoj [cloudových možností provozu](./cloud-operations.md).

> [!div class="nextstepaction"]
> [Vývoj možností cloudových operací](./cloud-operations.md)
