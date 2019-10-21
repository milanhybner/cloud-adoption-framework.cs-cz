---
title: 'Inovace v cloudu: sestavení pomocí zákaznických soucit'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se sestavovat pomocí zákaznických soucit.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5faaaf5b4c6b4c766c47dc6331723bed31e02d8e
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557203"
---
# <a name="build-with-customer-empathy"></a>Sestavování pomocí zákaznických soucit

"Nezbytnost je matka vynálezu." Tato proverb zachycuje indelibility lidského destilátu a náš přirozený disk k zásobám. Jak je vysvětleno v Oxford anglickém slovníku, "Pokud je potřeba něco v naléhavém případě, budete muset najít způsob, jak ho napravit nebo dosáhnout." Pár by tyto univerzální pravdivosti vynálezu zamítli. Jak je popsáno v tématu [metodologie](./index.md)inovací, inovace vyžaduje rovnováhu **vynálezu** a **přijetí**.

V případě analogie se inovace procházejí z více než rozšířené rodiny. *Customer soucit je hrdým nadřazených inovací.* Vytvoření řešení, které řídí inovace, vyžaduje legitimní zákazníky &mdash;one, který zákazníkům udržuje zpátky k řešení kritických zákaznických problémů. Tato řešení jsou založená na tom, co zákazník potřebuje, a ne na tom, co chce nebo Whims. Abychom vyhledali pravdivé potřeby zákazníků, začneme s soucit &mdash;a hlubokou znalostí o zkušenostech zákazníka. Jedná se o podvyvíjenou dovednost pro mnoho inženýrů, správců produktů a dokonce i vedoucích firmy. Mezi nejrůznějšími interakcemi a rychlým tempem role architekta cloudu se už nejspíš začaly vyvíjet tyto dovednosti.

Proč je soucit tak důležité? Od první verze minimálního životaschopného produktu (MVP) až po obecnou dostupnost řešení na úrovni trhu vám zákaznická soucit pomůže pochopit a sdílet zkušenosti zákazníka. Tento soucit nám pomáhá naučit se sestavovat lepší řešení. Důležitější je, že se nám lépe hodí pro řešení **zásob** , která budou podporovat **přijetí**. V digitální ekonomice můžou uživatelé, kteří se nejčastěji empathize s potřebou zákazníků, vytvořit jasnější budoucnost, která předefinuje a navede na trh.

## <a name="how-to-build-with-empathy"></a>Postup při sestavování pomocí soucit

Plánování je vnitřně cvičení při definování předpokladů. Tím více předpokládáme, že další předpoklady se budou přepočítat do základu skvělého nápadu. Obecně řečeno, předpokládá se, že předpoklady soucit &mdash;in jiných slov, "co bych chtěl, kdyby byla na této pozici?" Počínaje fází sestavení minimalizuje čas, který mohou předpoklady Invade řešení. Také urychluje smyčku zpětné vazby se skutečnými zákazníky a aktivuje předchozí příležitosti pro učení a zostření soucit.

> [!CAUTION]
> Správné definování toho, co se má sestavit, může být obtížné a vyžaduje určitý postup. Pokud sestavíte příliš rychle, může se stát, že nebudou odpovídat potřebám zákazníků. Pokud strávíte příliš dlouhou dobu od počátečního zákaznického potřeb a zákaznických požadavků, může se stát, že trh bude vyhovovat potřebě, než budete mít možnost sestavit cokoli. V obou případech může být příležitost k učení významně zpožděná nebo omezená. Někdy mohou být data dokonce poškozena.

Nejvíce inovativní řešení v historii se začala intuitivním přesvědčením. Tato střeva přichází z stávajících zkušeností a pozorování sami. Začneme s buildem, protože umožňuje rychlou zkoušku tohoto Intuition. Odtud můžeme pochopit hlubší porozumění a soucitější stupně. V každé iteraci nebo vydání řešení vychází zůstatek z vytváření odborníků MVP, který předvádí zákaznickou soucit.

Pro účely tohoto vyrovnávání Act se v následujících dvou částech projednávají koncepty vytváření pomocí soucit a definování MVP.

### <a name="define-a-customer-focused-hypothesis"></a>Definování zaměření na zákazníka – hypotéza

Sestavování pomocí soucit znamená vytvoření řešení na základě definované hypotézy, které ilustrují konkrétní potřeby zákazníka. Následující kroky vám pomůžou formulovat hypotézu, která vede k sestavování pomocí soucit.

1. Při sestavování pomocí soucit je zákazník vždycky aktivní. To může trvat mnoho tvarů. Můžete odkazovat na Archetype zákazníka, konkrétního uživatele nebo dokonce na fotografii zákazníka v průběhu problému, který chcete vyřešit. Zákazníci můžou mít taky interní (zaměstnanci nebo partneři) nebo externí (spotřebitelé nebo obchodní zákazníci). Tato definice zákazníka je první předpoklad, který se má testovat &mdash;can pomůžete tomuto konkrétnímu zákazníkovi?
2. Druhým je porozumění prostředí pro zákazníky. Sestavování pomocí soucit znamená, že zkušenost zákazníka je relatable a jejich výzvy jsou srozumitelné. Toto je další hypotéza, která se má testovat &mdash;can pomůžeme tomuto konkrétnímu zákazníkovi s touto spravovatelnou výzvou?
3. Třetí je definování jednoduchého řešení pro jednu výzvu. V souvislosti s odbornými znalostmi pro lidi, procesy a odborníky na konkrétní technologie vede k potenciálnímu řešení. Toto je kompletní hypotéza, která se má testovat &mdash;can pomůžeme tomuto konkrétnímu zákazníkovi s touto spravovatelnou výzvou pomocí navrženého řešení?
4. Posledním krokem při sestavování pomocí soucit je příkaz Value. Jakou dlouhodobou hodnotu máte k dispozici pro tyto zákazníky? Tato odpověď vytvoří kompletní &mdash;how předpokladů, že se zákazníci budou moci zlepšit pomocí navrženého řešení a vyřešit tuto spravovatelnou výzvu?

Tento poslední krok je vrcholem soucity řízené hypotézy. Definuje cílovou skupinu, problém, řešení a metriku, podle které se má zlepšit, a to vše, co je na zákazníkovi. Během fází měření a učení by se měla testovat každá hypotéza. Změny v rámci zákazníka, prohlášení o problému nebo řešení se předpokládá, že tým vyvíjí větší soucit jako adresovatelné zákaznické základny.

> [!CAUTION]
> Cílem je _sestavování_ pomocí zákaznických soucit, nikoli _plánování_ pomocí zákaznických soucit. Můžete se snadno zablokovat v nekonečných cyklech plánování a vylepšit si, abyste našli dokonalý soucitý výraz zákazníka. Než začnete s pokusy o vývoj takového příkazu, přečtěte si následující dvě části týkající se definování a sestavení MVP.

Jakmile je možné vyhodnotit základní předpoklady, budou se později iterace soustředit na testovací testy, a to v dalších testech soucit testů. Jakmile soucit sestavíte, otestujete a ověříte, můžeme začít pochopit, jak adresovatelné trhy se škáluje. To se dá udělat prostřednictvím rozšíření standardního vzorce hypotézy uvedeného výše. Na základě dostupných dat odhadujte velikost celkového trhu (jinými slovy, kolik potenciálních zákazníků). Odtud odhadujte procento z celkového trhu, který se podobá výzvě, a může být zajímat toto řešení, pokud by mohlo vyřešit výzvu. Toto je váš adresovatelný trh. Další hypotéza, která se má testovat, je: jak se má zlepšit _×%_ z životního života zákazníků pomocí navrženého řešení k řešení této spravovatelné výzvy? Malým vzorkováním zákazníků se odhalí úvodní indikátory, které mají za důsledek procentní dopad na zákazníky.

### <a name="define-a-solution-to-test-the-hypothesis"></a>Definovat řešení pro otestování hypotézy

Při každé iteraci smyčky sestavení-měření – učení se pokus o sestavení pomocí soucit definuje s minimálním životaschopným produktem.

Minimální životaschopný produkt (MVP) je nejmenší jednotkou úsilí (vynález, inženýr, vývoj aplikací nebo architektura dat), aby se vytvořilo dostatečné řešení pro učení _se zákazníkem_. Cílem každého MVP je otestovat některé nebo všechny předchozí hypotézy a získat zpětnou vazbu od zákazníka přímo. Výstup není atraktivní aplikace se všemi funkcemi potřebnými ke změně vašeho odvětví. Požadovaný výstup každé iterace je výuková příležitost &mdash;a možnost hlubšího testování hypotézy.

Běžný způsob, jak zajistit, aby byl produkt minimální, timeboxing vytváření řešení. Ujistěte se, že vývojový tým má za následek, že řešení lze vytvořit v jedné iteraci, aby bylo možné rychlé testování. Chcete-li lépe pochopit použití rychlosti, iterací a vydání k definování minimálních prostředků, přečtěte si téma [plánování rychlosti, iterace, verze a cesty iterace](../../plan/iteration-paths.md).

### <a name="reduce-complexity-and-delay-technical-spikes"></a>Snížení složitosti a zpoždění technických špiček

[Pravidla inovace](./invention.md) zjištěná v rámci [metodologie](./index.md) inovací popisují funkčnost, která je často nutná k zajištění vyspělých inovací nebo řešení MVP připravené pro škálování. Tyto disciplíny použijte jako dlouhodobou příručku pro zahrnutí funkcí. Stejně tak je používejte jako průvodce postupovat opatrněji při počátečním testování hodnot zákazníků a soucit ve vašem řešení.

Funkce a různé disciplíny inovací se nedají vytvářet v jediné iteraci. Řešení MVP často trvá několik vydání, aby zahrnovalo složitost více oborů. V závislosti na investicích do vývoje může více paralelních týmů pracovat v různých oborech k otestování více hypotéz. I když je u těchto týmů vhodné zachovat strukturální sblížení, není vhodné se pokusit složitá integrovaná řešení, dokud nelze ověřit hodnotu hypotézy.

Složitost se nejlépe detekuje v četnosti nebo objemu **technických špiček**. Technické špičky jsou úsilím vytvořit technická řešení, která se zákazníkům nedají snadno testovat. Pokud je hodnota zákazníka a zákaznická soucit netestovaná, technické špičky představují riziko pro inovace a měly by být minimalizovány, pokud je to možné. Pro typy vyspělých testovaných řešení zjištěných při migraci můžou být technické špičky běžné v rámci přijetí. Jejich testování je však zpožděné při inovacích, a pokud je to možné, měli byste je odložit.

Přístup k zjednodušení vystavit útokům je navržený pro všechny definice MVP. Zjednodušení vystavit útokům je odebrání cokoli, co nepřidává do vaší schopnosti ověřit hypotézu. Chcete-li minimalizovat složitost, snižte integraci a funkce, které nejsou nutné k otestování hypotéz.

### <a name="build-a-minimum-viable-product-mvp"></a>Sestavte minimální životaschopný produkt (MVP).

V každé iteraci může řešení MVP trvat mnoho různých tvarů. Běžný požadavek je pouze v případě, že výstup umožňuje měření a testování hypotézy. Tento jednoduchý požadavek iniciuje vědecký proces a umožňuje týmu sestavovat pomocí soucit. K tomu, aby se tento zákazník nejprve zaměřil, měl by počáteční MVP spoléhat jenom na jeden z [oborů inovace](./invention.md).

V některých případech nejrychlejší cesta k inovacím dočasně vyloučí tyto disciplíny, dokud tým pro přijetí cloudu nejistí, že hypotéza je přesně ověřena. Tato příručka může přijít z technologické společnosti, jako je Microsoft, na neintuitivní. Cílem tohoto prohlášení je zdůraznit, že zákazník potřebuje a ne konkrétní technologické rozhodnutí, by měl být nejvyšší prioritou v řešení MVP.

Řešení MVP se běžně skládá z jednoduché webové aplikace nebo řešení dat s minimálními funkcemi a omezeným polským. Pro organizace, které mají odborné zkušenosti s profesionálním vývojem, se jedná často o nejrychlejší cestu k učení a iteraci. Následuje několik dalších přístupů, které tým může využít k sestavení MVP:

- Prediktivní algoritmus, který je chybný 99% času, ale znázorňuje konkrétní požadované výsledky.
- Zařízení IoT, které nekomunikuje bezpečně v produkčním měřítku, ale může ukázat hodnotu téměř dat v reálném čase v rámci procesu.
- Aplikace vytvořená vývojářem občana k testování hypotézy nebo splnění potřeb menšího rozsahu.
- Ruční proces, který znovu vytvoří výhody aplikace, aby následoval.
- Drátový model nebo video, které jsou dostatečně podrobné, aby zákazník mohl pracovat.

Vývoj MVP by neměl vyžadovat obrovské množství investic do vývoje. V takovém případě by měly být investice omezeny co nejvíce, aby se minimalizoval počet testovaných hypotéz najednou. V každé iteraci a každé vydané verzi se řešení záměrně vylepšuje směrem k řešení připravenému ke škálování, které představuje několik oborů inovace.

### <a name="accelerate-mvp-development"></a>Urychlení vývoje MVP

Doba uvedení na trh je zásadní pro úspěch jakékoli inovace. Rychlejší verze vedou k rychlejšímu učení. Rychlejší učení s produkty, které se dají rychleji škálovat V některých případech může tento proces zpomalit tradiční vývojové cykly aplikací. Častěji jsou inovace omezené pomocí dostupných zkušeností. Rozpočty, počty a dostupnost zaměstnanců můžou vytvářet omezení počtu nových inovací, které tým může zpracovat.

Omezení zaměstnanců a přání k sestavování pomocí soucit vytvořili rychle rostoucí trend pro vývojáře občanů. Tito vývojáři omezují rizika a poskytují škálování v rámci organizace odborného vývoje v organizaci. Vývojáři občana mají v potaz odborníky v oblasti zkušeností zákazníků, ale nejsou školením jako technici. Tito jednotlivci využívají nástroje pro vytváření prototypů nebo světlejší vývojové nástroje pro vývoj, které můžou být nelibě neseno profesionálními vývojáři. Toto nové množství vývojářů zarovnaných organizací vytváří řešení MVP a teorie testování. V případě, že je správně zarovnaná, může tento proces vytvořit produkční řešení, která by mohla poskytovat hodnotu, ale Nepředávat účinný, dostatečně škálovatelný předpoklad. Můžou se také použít jako ověření prototypu před zahájením škálování úsilí.

V rámci jakékoli inovačního plánu se doporučuje, aby týmy pro přijetí v cloudu rozrůzní své portfolio, aby zahrnovali občanská úsilí pro vývojáře. Díky škálování úsilí při vývoji může být více hypotéz vytvořeno a testováno sníženou investicí. Když se ověří hypotéza a identifikuje se adresovatelné trhy, profesionální vývojáři můžou toto řešení posílit a škálovat pomocí moderních vývojářských nástrojů.

### <a name="final-build-gate-customer-pain"></a>Konečná brána sestavení: bolesti zákazníka

Pokud je zákazník soucit silný, je třeba snadno identifikovat problém s jasným problémem. Bolest zákazníka by měla být zřejmá. Během sestavování tým přijetí do cloudu sestaví řešení pro testování hypotézy na základě bodového bodu zákazníka. Pokud je hypotéza, která je dobře definovaná, ale nejedná se o problém, řešení není skutečně založené na zákaznických soucit. V tomto scénáři sestavení není správným výchozím bodem. Místo toho investovat do budování soucit a učení od skutečných zákazníků. Nejlepším přístupem k sestavování soucit a ověřování bolesti je jednoduché: naslouchat zákazníkům. Investovat čas do plnění a sledování zákazníků, dokud nebudete schopni identifikovat nějaký problém, ke kterému dochází často. Po pochopení bodového bodu může tento přístup otestovat řešení hypotetické, aby bylo možné tento problém řešit.

## <a name="when-not-to-apply-this-approach"></a>Kdy nepoužívat tento přístup

Existuje mnoho právních požadavků, dodržování předpisů a odvětví, které by mohly vyžadovat alternativní přístup. Pokud veřejné verze vývojového řešení vytvářejí riziko pro patentové časování, ochranu duševních vlastností, nevracení zákaznických dat nebo porušení požadavků na dodržování předpisů, pak tento přístup nemusí být vhodný. V případě pozorovaných rizik, která by taková existence existovala, se poraďte s právním poradcem před tím, než si vyžádáte jakýkoli postup

## <a name="references"></a>Odkazy

Některé z konceptů v tomto článku se sestavují v tématech popsaných v tématu  _[štíhlé spuštění](http://theleanstartup.com/book)(Eric Internet Explorer, koruna Business, 2011)_ .

## <a name="next-steps"></a>Další kroky

Po vytvoření řešení MVP se dá měřit hodnota soucit a hodnota škálování. Přečtěte si, jak [změřit dopad na zákazníky](./measure.md).

> [!div class="nextstepaction"]
> [Měření dopadu zákazníka](./measure.md)
