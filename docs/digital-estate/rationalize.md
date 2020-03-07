---
title: Racionalizace digitálních aktiv
description: Používejte racionalizaci cloudu k vyhodnocení vašich digitálních prostředků a určení nejlepšího přístupu k hostování v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 14f96dde6558588c092a181aa2b7a2e57220cf5f
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337413"
---
# <a name="rationalize-the-digital-estate"></a>Racionalizace digitálních aktiv

Racionalizace cloudu je proces vyhodnocení prostředků k určení nejlepšího přístupu k hostování v cloudu. Po určení [přístupu](./approach.md) a agregovaného [inventáře](./inventory.md)může začít racionalizace v cloudu. Racionalizace cloudu popisuje nejběžnější možnosti racionalizace.

## <a name="traditional-view-of-rationalization"></a>Tradiční pohled na racionalizaci

Je snadné pochopit racionalizaci, když vizualizujete tradiční proces racionalizace jako složitý rozhodovací strom. Každý Asset v digitální nemovitosti se dodává prostřednictvím procesu, který má za následek jednu z pěti odpovědí (pět RS). Pro malé Estates tento proces funguje dobře. Pro větší Estates je neefektivní a může vést k významným zpožděním. Podívejme se na proces, kde zjistíte, proč. Pak budeme docházet k efektivnějšímu modelu.

**Inventář:** Úplný soupis prostředků, včetně aplikací, softwaru, hardwaru, operačních systémů a metrik výkonu systému, je nutný k dokončení úplné racionalizace s využitím tradičních modelů.

**Kvantitativní analýza:** Ve stromové struktuře se kvantitativní otázky řídí první vrstvou rozhodnutí. Mezi běžné otázky patří následující: je prostředek používaný ještě dnes? Pokud ano, je optimalizovaná a velikost správně? Jaké závislosti existují mezi prostředky? Tyto otázky jsou zásadní pro klasifikaci inventáře.

**Kvalitativní analýza:** Další sada rozhodnutí vyžaduje lidské poznatky ve formě kvalitativní analýzy. Nejčastější dotazy, které jsou zde uvedeny, jsou často jedinečné pro řešení a mohou být zodpovězeny pouze obchodními stranami a skupinami Power Users. Tato rozhodnutí obvykle odloží proces a výrazně zpomalují věci. Tato analýza obvykle spotřebovává 40 až 80 hodin FTE na aplikaci.

Pokyny k vytvoření seznamu kvalitativních otázek analýzy najdete v tématu [přístupy k plánování digitálních nemovitostí](./approach.md).

**Rozhodnutí o racionalizaci:** V případě praktického týmu racionalizace jsou kvalitativní a kvantitativní data vytvořena jasná rozhodnutí. Týmy s vysokým stupněm racionalizace by bohužel byly náročné na to, aby se mohli zajímat nebo přebírat v měsících.

## <a name="rationalization-at-enterprise-scale"></a>Racionalizace v podnikovém měřítku

Pokud je toto úsilí časově náročné a těžké pro digitální vlastnictví 50-VM, Představte si úsilí, které je potřeba k tomu, aby probírala obchodní transformaci v prostředí s tisíci virtuálních počítačů a stovkami aplikací. Požadovaná lidská námaha může snadno překročit 1 500 hodin FTE a devět měsíců plánování.

I když je úplná racionalizace koncovým stavem a skvělým směrem k přesunu v nástroji, nezpůsobí se tím vysoká návratnost investic (návratnost investic) vzhledem k požadovanému času a energie.

Pokud je racionalizace zásadní pro finanční rozhodnutí, je vhodné zvážit organizaci profesionálních služeb, které se specializují na racionalizaci cloudu, a urychlit tak proces. I pak plná racionalizace může být nákladný a časově náročné úsilí, které zpozdí transformaci nebo obchodní výsledky.

Zbývající část tohoto článku popisuje alternativní přístup, označovaný jako přírůstkové racionalizace.

## <a name="incremental-rationalization"></a>Přírůstkové racionalizace

Kompletní racionalizace rozsáhlého digitálního majetku je náchylná k riziku a může způsobit zpoždění z důvodu jeho složitosti. Předpokladem pro přírůstkový přístup je to, že opožděná rozhodnutí rozdělují zatížení podniku, aby se snížilo riziko překážek. V průběhu času tento přístup vytvoří organické modely pro vývoj procesů a zkušeností potřebných k efektivnějšímu rozhodování o rozhodnutích racionalizace.

### <a name="inventory-reduce-discovery-data-points"></a>Inventář: omezení datových bodů zjišťování

Několik organizací investuje čas, energii a náklady na zajištění přesného digitálního majetku v reálném čase. Ztráty, krádeže, aktualizační cykly a registrace zaměstnanců často opravňují k podrobnému sledování prostředků zařízení koncových uživatelů. Technologie NÁVRATNOSTi správného inventáře serverů a aplikací v tradičním místním datacentru je ale často nízká. Většina organizací IT má další problémy, které je potřeba řešit, než sledování využívání dlouhodobých assetů v datovém centru.

V cloudové transformaci se přímo korelují s provozními náklady. Pro správné plánování se vyžadují přesné údaje inventáře. Současné možnosti kontroly životního prostředí můžou zpozdit rozhodování na základě týdnů nebo měsíců. Pár štychů může zrychlit shromažďování dat.

Kontrola založená na agentech je nejčastěji citovaná prodleva. Robustní data potřebná pro tradiční racionalizaci je často možné shromažďovat pouze s agentem spuštěným na jednotlivých prostředcích. Tato závislost na agentech často zpomaluje průběh, protože může vyžadovat zpětnou vazbu od funkcí zabezpečení, operací a správy.

V přírůstkovém procesu racionalizace může být pro počáteční zjišťování použito řešení bez agentů k urychlení prvotních rozhodnutí. V závislosti na úrovni složitosti prostředí se může stále vyžadovat řešení založené na agentech. Dá se ale odebrat z kritické cesty na změnu firmy.

### <a name="quantitative-analysis-streamline-decisions"></a>Kvantitativní analýza: zjednodušení rozhodnutí

Bez ohledu na přístup ke zjišťování inventáře může kvantitativní analýza řídit počáteční rozhodnutí a předpoklady. To platí zejména při pokusu o identifikaci první úlohy nebo v případě, že cílem racionalizace je srovnání nákladů na vysoké úrovni. V přírůstkovém procesu racionalizace tým cloudové strategie a týmy přijímání v cloudu omezují [pět RS účelnosti](./5-rs-of-rationalization.md) na dvě Stručná rozhodnutí a uplatňují tyto kvantitativní faktory. Tím se zjednoduší analýza a sníží se množství počátečních dat, která je potřeba ke změně jednotky.

Pokud se například organizace nachází v průběhu migrace IaaS do cloudu, můžete předpokládat, že většina úloh bude buď vyřazena, nebo bude znovu hostovat.

### <a name="qualitative-analysis-temporary-assumptions"></a>Kvalitativní analýza: dočasné předpoklady

Omezením počtu potenciálních výsledků je snazší získat počáteční rozhodnutí o budoucím stavu assetu. Když omezíte možnosti, snížíte tím také počet otázek, které v této úvodní fázi požádaly o firmu.

Například pokud jsou možnosti omezeny na opětovné hostování nebo vyřazení z provozu, musí podnik při počátečním racionalizaci odpovědět pouze na jednu otázku, což znamená, zda Asset vyřadit.

"Analýza naznačuje, že tento Asset aktivně nepoužívá žádní uživatelé. Je to přesné nebo podíváme se na něco? " Tato binární otázka je obvykle mnohem jednodušší spustit pomocí kvalitativní analýzy.

Díky tomuto zjednodušenému přístupu vznikne směrný plán, finanční plány, strategie a směr. V novějších aktivitách každý Asset prochází další racionalizací a kvalitativní analýzou pro vyhodnocení dalších možností. Všechny předpoklady, které uděláte v této počáteční racionalizaci, se testují před

## <a name="challenge-assumptions"></a>Předpoklady pro výzvu

Výsledek předchozí části je hrubá racionalizace, která je úplným předpokladem. Dále je čas na to, abyste si vyzpochybnili některé z těchto předpokladů.

### <a name="retire-assets"></a>Vyřazení prostředků

V tradičním místním prostředí je hostování malých, nepoužívaných prostředků zřídka významným dopadem na roční náklady. S několika výjimkami musí být úsilí, které je potřeba k analýze a vyřazení skutečného prostředku, převážene za cenu z vyřazení a vyřazení těchto prostředků.

Když ale přejdete na model monitorování účtů cloudu, vyřazení prostředků může způsobit výrazné úspory za roční provozní náklady a úsilí na migraci vpřed.

Po dokončení kvantitativní analýzy není pro organizace neobvyklá vyřazení 20% nebo více jeho digitálního majetku. Před provedením akce doporučujeme provést další kvalitativní analýzu. Po potvrzení se tyto prostředky vyřazením z provozu budou moci vydávat první návratnost Victory migrace do cloudu. Často se jedná o jeden z největších faktorů úspory nákladů. Proto by tým cloudové strategie měl dohlížet na ověřování a vyřazení prostředků paralelně s provedením [metodologie migrace](../migrate/index.md), aby se dosáhlo předčasného finančního úspěchu.

### <a name="program-adjustments"></a>Úpravy programu

Společnost se zřídka zachází jenom na jednu cestu transformace. Volba mezi snížením nákladů, nárůstem trhu a novými datovými proudy je zřídka binární rozhodnutí. V takovém případě doporučujeme, aby tým cloudové strategie spolupracoval s ním k identifikaci prostředků v úsilí paralelní transformace, které jsou mimo rozsah primární cesty transformace.

V příkladu migrace IaaS uvedeném v tomto článku:

- Požádejte tým DevOps, aby identifikoval prostředky, které už jsou součástí automatizace nasazení, a odeberte tyto prostředky z základního plánu migrace.

- Položte si data a týmy R & D, abyste identifikovali prostředky, které vycházejí z nových datových proudů příjmů, a odebrat je z základního plánu migrace.

Tuto aplikaci můžete rychle provést a vytvořit tak jejich kvalitativní analýzu do několika nevyřízených položek migrace.

Je možné, že stále budete muset vzít v úvahu některé prostředky, jako je opětovné hostování prostředků. Po počáteční migraci můžete postupovat v pozdějším racionalizaci.

## <a name="select-the-first-workload"></a>Vyberte první úlohu.

Implementace prvního pracovního vytížení je klíč k testování a učení. Je první příležitostí k předvedení a sestavení růstové místoy.

### <a name="business-criteria"></a>Obchodní kritéria

Aby se zajistila transparentnost firmy, identifikujte zatížení, které je podporováno členem organizační jednotky týmu cloudové strategie. Nejlépe si vyberte, ve kterém má tým svěřenou a silnou motivaci, která se má přesunout do cloudu.

### <a name="technical-criteria"></a>Technická kritéria

Vyberte úlohu, která má minimální závislosti a kterou lze přesunout jako malou skupinu prostředků. Doporučujeme vybrat úlohu s definovanou testovací cestou, aby bylo ověřování snazší.

První zatížení je často nasazeno v experimentálním prostředí bez provozní kapacity nebo kapacity zásad správného řízení. Je důležité vybrat úlohu, která nekomunikuje s zabezpečenými daty.

### <a name="qualitative-analysis"></a>Kvalitativní analýza

Týmy pro přijetí do cloudu a tým cloudové strategie můžou spolupracovat na analýze těchto malých úloh. Tato spolupráce vytvoří kontrolované možnosti pro vytváření a testování kvalitativních kritérií analýzy. Menší populace vytvoří příležitost k prošetření ovlivněných uživatelů a k provedení podrobné kvalitativní analýzy za týden nebo méně. Pro běžné kvalitativní analytické faktory se podívejte na konkrétní cíl racionalizace v [5 RS of racionalizace](./5-rs-of-rationalization.md).

### <a name="migration"></a>Migrace

Paralelně s pokračující racionalizací může tým pro přijetí cloudu začít migrovat malé úlohy a rozšířit tak učení v následujících klíčových oblastech:

- Posílit dovednosti s platformou poskytovatele cloudu.
- Definujte základní služby (a standardy Azure) potřebné k tomu, aby odpovídaly dlouhodobému záměru.
- Lépe pochopíte, jak může operace později v transformaci vyžadovat změnu.
- Seznamte se s případnými podnikovými riziky a tolerancemi firmy pro tato rizika.
- Vytvořte směrný plán nebo minimální životaschopný produkt (MVP) pro řízení na základě tolerance rizika firmy.

## <a name="release-planning"></a>Plánování vydání

I když tým pro přijetí cloudu provádí migraci nebo implementaci první úlohy, může tým cloudové strategie začít upřednostňovat zbývající aplikace a úlohy.

### <a name="power-of-10"></a>Výkon 10

Tradiční přístup k racionalizaci pokusům o splnění všech předvídatelných potřeb. Naštěstí platí, že plán pro každou aplikaci není často nutný ke spuštění cesty transformace. V přírůstkovém modelu výkon 10 poskytuje dobrý výchozí bod. V tomto modelu tým strategie cloudu vybere prvních 10 aplikací, které se mají migrovat. Tyto deset úloh by měly obsahovat kombinaci jednoduchých a složitých úloh.

### <a name="build-the-first-backlogs"></a>Sestavte první nevyřízené položky.

Týmy pro přijetí do cloudu a tým cloudové strategie můžou spolupracovat na kvalitativní analýze prvních 10 úloh. Toto úsilí vytvoří nové nevyřízené položky s určenou prioritou a první nevyřízené položky s určenou prioritou. Tato metoda umožňuje týmům iterovat v přístupu a poskytuje dostatek času pro vytvoření vhodného procesu pro kvalitativní analýzu.

### <a name="mature-the-process"></a>Vyspělý proces

Jakmile dva týmy souhlasí s kritérii kvalitativní analýzy, může se vyhodnocení v rámci každé iterace stát úkolem. Dosažení konsensu na kritéria hodnocení obvykle vyžaduje dvě až tři verze.

Po přesunu posouzení do procesu přírůstkového provádění migrace může tým pro přijetí do cloudu v rámci posuzování a architektury iterovat rychleji. V této fázi je také abstraktní tým cloudové strategie, který zkracuje dobu vyčerpání. To také umožňuje týmu cloudové strategie zaměřit se na aplikace, které ještě nejsou v určité vydané verzi, což zajistí těsné sblížení se měnícími se podmínkami na trhu.

Ne všechny aplikace s určenou prioritou budou připravené k migraci. Řazení se pravděpodobně změní, protože tým má hlubší kvalitativní analýzu a zjišťuje obchodní události a závislosti, které mohou vyzvat k přehodnocení nevyřízených položek. Některé verze můžou seskupit dohromady malý počet úloh. Jiné můžou obsahovat jenom jednu úlohu.

Tým pro přijetí cloudu může spouštět iterace, které nepřinesou úplnou migraci zatížení. Čím menší je zatížení a čím méně závislostí, tím pravděpodobnější je, že úloha bude vyhovovat jednomu sprintu nebo iteraci. Z tohoto důvodu doporučujeme, aby několik prvních aplikací v nevyřízených položkách Release bylo malé a obsahovalo několik externích závislostí.

## <a name="end-state"></a>Koncový stav

V průběhu času bude kombinace týmu pro přijetí cloudu a týmu cloudové strategie dokončit plnou racionalizaci inventáře. Tento přírůstkový přístup ale umožňuje týmům průběžně urychlit proces racionalizace. Pomáhá také cestám pro transformaci, která dřív přinese velké obchodní výsledky, a to bez tolika úsilí před analýzou.

V některých případech může být finanční model příliš těsný, aby bylo rozhodnutí bez dodatečné racionalizace. V takových případech možná budete potřebovat obecnější přístup k racionalizaci.

## <a name="next-steps"></a>Další kroky

Výstupem úsilí racionalizace je nevyřízené položky pro všechny prostředky, které jsou ovlivněny zvolenou transformací. Tyto nevyřízené položky teď můžou sloužit jako základ pro nákladové modely cloudových služeb.

> [!div class="nextstepaction"]
> [Zarovnávání nákladových modelů s digitální nemovitosti](./calculate.md)
