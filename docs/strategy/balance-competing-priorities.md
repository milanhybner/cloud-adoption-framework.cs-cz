---
title: Vyvážení konkurenčních priorit
description: Objevte strategie pro vyrovnávání konkurenčních priorit
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/04/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: ba70687627e81b58eb76cd69838abf1ebcdb6489
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312408"
---
# <a name="balance-competing-priorities"></a>Vyvážení konkurenčních priorit

Nastupování na cestě digitální transformace funguje jako vynucená funkce pro zúčastněné strany napříč obchodními a technologickými týmy. Cesta k úspěchu je pevně směrována v organizacích, aby bylo možné vyrovnávat konkurenční priority.

Podobně jako u jiných digitálních transformací bude při přijetí v rámci cloudu vystavení konkurenčních priorit během životního cyklu. Podobně jako u jiných forem transformace bude mít schopnost najít rovnováhu v těchto prioritách významný dopad na realizaci obchodních hodnot. Vyvážení těchto konkurenčních priorit bude vyžadovat otevřené (a někdy obtížné) konverzace mezi zúčastněnými stranami (a v časech s jednotlivými přispěvateli).

Tento článek popisuje některé z konkurenčních priorit, které se obvykle projednávají při provádění každé metodologie. Doufáme, že toto rozšířené povědomí vám pomůže lépe se připravit na tyto diskuze při vývoji strategie přijetí do cloudu.

![Přehled životního cyklu přijetí do cloudu](../_images/caf-overview.png)

V následujících částech najdete postup v rámci výše uvedeného vizuálu životního cyklu přijetí cloudu. Je ale důležité si uvědomit, že přijetí v cloudu je iterativní (nejedná se o sekvenční proces). tyto konkurenční priority se v různých bodech a v průběhu vaší cesty k vašemu cloudu vydávají (a někdy se jim projeví).

## <a name="general-theme-of-the-cloud-adoption-framework-approach"></a>Obecný motiv přístupu k rozhraní architektury pro přijetí do cloudu

Řešení monolitické a pokročilá plánování jsou postavená na sérii předpokladů, které se (nebo nemusí) prokázat jako přesné v čase. Přijetí cloudu je často nové prostředí pro podnikání a technické týmy. Stejně jako u většiny nových možností zkušeností a učení je vysoká pravděpodobnost, že tyto předpoklady budou prověřeny jako nepravdivé.

Podle osvědčených agilních principů opožděných technických rozhodnutí je pro většinu pokynů v rámci této architektury upřednostněný přístup. Tento přístup se řídí konzistentním vzorem: zřízení obecného koncového stavu, rychlé přesunutí na počáteční implementaci, testování a ověřování předpokladů, Refaktoring v předstihu za účelem vyřešení těchto předpokladů. Tento typ růstu místo maximalizuje učení a minimalizuje riziko pro obchodní hodnotu. Tento místo ale vyžaduje určitou úroveň pohodlí s nejednoznačnou.

V některých případech může být nejednoznačnost scarier (nebo více nebezpečných) než nepravdivé předpoklady. I když se tato architektura zajímá do učení a adresování nejednoznačnosti během provádění, existuje mnoho situací, které týmu vyžadují, aby se na základě analýz nebo přístupů na základě předpokladů. V následujících částech se v jednotlivých oddílech pokusí ilustrovat alespoň jeden příklad rozšířeného rozsahu, který ilustruje dobu, kdy by druhá hlubší iterace byla užitečná.

## <a name="balance-during-strategy"></a>Zůstatek během strategie

Základním cílem metodologie strategie je vyvíjet sbližování mezi zúčastněnými stranami. Po definování bude tato strategická pozice zarovnaná s chováním v každé z metod, aby bylo zajištěno, že technické rozhodnutí budou v souladu s požadovanými obchodními výsledky. Při podpoře zarovnání mezi zúčastněnými stranami se vytvoří společná konkurenční priorita: **Hloubka odůvodnění v** **čase s obchodním dopadem**.

**Konkurenční priority:**

- **Hloubka odůvodnění**: účastníci často chtějí mít rozsáhlou finanční analýzu a plný obchodní odůvodnění, aby se mohli přizpůsobit strategickému směru. Tato úroveň analýzy bohužel může vyžadovat prodloužený časový interval, který umožňuje shromažďování a analýzu dat.
- **Čas na obchodní dopad**: v opačném případě se účastníci často uchovávají za účelem poskytování obchodních výsledků v rámci definovaných časových rámců. Časově náročná analýza a posouzení můžou tyto výsledky dát do nebezpečí před tím, než bude technická práce dokonce zahájena.

**Minimální rozsah:** Hledání tohoto zůstatku vyžaduje diskuze mezi zúčastněnými stranami v brzkém průběhu procesu. Metodologie strategie navrhuje omezení rozsahu zarovnání během tohoto počátečního úsilí. V navrhovaném přístupu se účastníci zaměřují na zarovnání kolem sady základních motivů, měřitelných výsledků a vysokého obchodního odůvodnění. Doporučujeme, aby se zúčastněné strany rychle dopustily na malý počet počátečních projektů nebo pilotních projektů, které vám pomůžou vyřídit požadované příležitosti učení.

**Příklad rozšířeného oboru:** Pokud počáteční obchodní analýza indikuje vysoké riziko negativního vlivu na firmu, může se stát, že účastníci budou muset zpomalit a lépe zhodnotit hlubší analýzu během obchodní odůvodnění.

## <a name="balance-during-plan"></a>Zůstatek během plánu

Podobně jako u priorit strategie se v průběhu plánování vyžaduje vyvážit: Hloubka prvotního plánování vs. neopožděná technická rozhodnutí.

**Konkurenční priority:**

- **Hloubka prvotního plánování** v souvislosti s technickou implementací v cloudu často obsahuje velký počet předpokladů. Hlavně v případě, že tým má prodlevy, prostředí se zahodí z otvorů zjišťování nebo úlohy nemají jasně definované architektury end-stavy. Všechny tyto předpoklady jsou běžné v podrobných plánech pro přijetí do cloudu. K odebrání těchto předpokladů se vyžadují experimenty, pilotní nasazení a kvalitativní analýza.
- **Opožděná technická rozhodnutí** předpokládají, že je možné provést pozdější technické rozhodnutí, tím přesnější bude toto rozhodnutí. Následující zásady agilního plánování produktů vám pomohou zpozdit technické rozhodnutí a zajistit, aby k nim docházelo ve správný čas a měly dostatečné informace. Tento přístup ale má za následek mnohem vyšší stupeň nejednoznačnosti v počátečním plánu.

**Minimální rozsah:** V rámci spravovatelných plánů je navržený přístup k vývoji agilních produktů. Pro dosažení tohoto zůstatku vyrovnává metodologie plánu následující kroky. Využijte k inventarizaci celé digitální nemovitosti pomocí nástrojů pro automatizované zjišťování, ale použijte přírůstkovou racionalizaci k plánování až na dalších 1-3 měsíců práce. Zajistěte rychlé přesunutí správného přizpůsobení organizace. Vytvořte plán připravenosti dovedností pro přiřazený tým. K rychlému nasazení počátečních nevyřízených položek Využijte šablonu plánu přijetí do cloudu.

**Příklad rozšířeného oboru:** V některých případech může doručení plánu přijetí do cloudu reagovat na podnikovou událost, která je časově citlivá nebo má vysokou dopad. Pokud úspěch vyžaduje pohyb vysokého počtu prostředků v určitém časovém období, jsou výše uvedené kroky často následovány hlubším úsilím plánování. Klíčem k úspěchu v těchto scénářích je naplánování dostatečného plánu, aby bylo možné se vrátit a následně naplánovat na celou službu Engagement. Tento přístup omezuje pravděpodobnost plánování blokování obchodních výsledků.

## <a name="balance-during-ready"></a>Zůstatek během připravenosti

Když se týmy přijetí připravují k prvním krokům do cloudu, často jsou konkurenční priority mezi časem přijetí a dlouhodobých operací. Tým se může bojovat, aby se dobře hodí k zajištění toho, aby poskytoval úkol v rukou a byl dobře spravovaný. Tato bojovat je nezbytná v tradičních IT prostředích, kde Act z vývoje platformy vyžaduje fyzické prostředky a cykly pořízení. Pokud je však celá IT platforma definována v kódu, tradiční vývojové taktiku (jako refaktoring) snižuje nutnost jejich správné správy od začátku.

**Konkurenční priority:**

- **Dlouhodobé operace:** Zákazníci se často zablokují tím, že chtějí mít cloudové prostředí, které splňuje paritu funkcí se současnými systémy správy provozu, zásad správného řízení a zabezpečení. V rámci aktuální studie zákazníků více než 90% zákazníků potřebných k tomu, aby tuto místo mohli začít. Tento blok vloží měsíc zpoždění, které zpomaluje nebo zabrání vlivu na firmu.
- **Čas k přijetí:** Cloudové nástroje, jako jsou Azure Policy, Azure modrotisky a skupiny pro správu, umožňují snadné refaktoring napříč platformou IT. Předdefinované zóny pro vykládku navíc poskytují dogmatickým pozice, které urychlují nasazení do prostředí, které už splňuje mnoho požadavků na paritu funkcí. Společně existují příležitosti ke zrychlení času na uvedení na trh s minimálním dopadem na dlouhodobé operace.

**Minimální rozsah:** Připravená metodologie popisuje přímou cestu z rychlého přijetí na dlouhodobé operace. Tento přístup začíná základním úvodem k nástrojům, které umožňují refaktoring prostředí. Na základě těchto nástrojů a požadavků na životní prostředí se zákazníkům provede výběr předdefinovaných zón pro vykládku (každý dodaných pomocí infrastruktury jako modelů kódu). Tento kód pak může být refaktorované během přijetí do cloudu za účelem zlepšení provozu, zabezpečení a postures správy.

**Příklad rozšířeného oboru:** Pro týmy, jejichž plán přijetí volá pro střední cíl (během 24 měsíců) hostování **více než 1 000 prostředků (aplikací, infrastruktury nebo datových assetů) v cloudu**, je navrženo robustnější zobrazení zón vykládku. V těchto situacích by se při počátečních konverzacích na cílové zóně měli zvážit a spravovat metodologie. Tato hlubší úvaha však často přináší týdny nebo měsíce do plánu přijetí do cloudu. Aby se minimalizoval dopad na obchodní výsledky, měl by tým pro přijetí v cloudu, který je v cloudu, vytvořit ještě více pilotních zátěžových a centrálních řešení.

## <a name="balance-during-migrate"></a>Zůstatek během migrace

Během migrace je běžné, že týmy pro přijímání budou předpokládat, že se úlohy budou v cloudu v aktuální konfiguraci "tak," hostovat v cloudu. Tím se přímo soutěží se zobrazením s možností dopředné, aby se zajistilo jejich uspořádání, aby lépe využily cloudové možnosti. Bohužel se tyto dva vzájemně nevylučují a můžou být při správě prostřednictvím běžného procesu bezplatné.

**Konkurenční priority:**

- Opětovné **hostování:** Zákazníci často přinese migraci na _výtah a posunou_ pohyb všech prostředků do cloudu v aktuální konfiguraci stavu. Výsledkem je, že v portfoliu IT dojde k malému posunu. Tento přístup je také nejrychlejší způsob, jak vyřadit prostředky v existujícím datovém centru.
- Změna **architekta:** Modernizaci architektura jednotlivých úloh maximalizuje hodnotu cloudu napříč náklady, výkonem a operacemi. Tento přístup je však mnohem pomalejší a často vyžaduje přístup ke zdrojovému kódu jednotlivých aplikací.

**Minimální rozsah:** Během plánování prvotní fáze použijte pro plánování možnost opětovného hostování, s jasným porozuměním, že tato možnost je počátečním podnikovým předpokladem a není technickým rozhodnutím. V rámci metodologie migrace by tým přijetí mohl tento předpoklad vyvolávat pro každou migrovaná úlohu. Tato metodika se řídí kroky vyhodnocení, migrace, zvýšení úrovně pro každou úlohu nebo skupinu nebo úlohy vytvářející továrnu migrace. Během fáze hodnocení vyhodnocuje tým přijetí technické potřeby a architekturu jednotlivých úloh. Tato snaha posouzení zřídka vede k čistému přístupu a posunu, protože mnohé z komponent v architektuře jsou pro refaktoring a modernizaci obvykle vybrány.

**Příklad rozšířeného oboru:** Pro úlohy kritické nebo vysoké citlivosti, jako je například sálové a vícevrstvé aplikace mikroslužeb, může být během fáze hodnocení vyžadováno hlubší hodnocení úloh. V těchto situacích je navrženo, že zákazníci využívají kontrolu architektury Azure a architekturu architektury Azure k vylepšení požadavků na úlohy během posouzení.

## <a name="balance-during-innovate"></a>Zůstatek během inovací

Pravdivé inovace zaměřené na zákazníky vytváří společné konfliktní priority mezi nutností doručovat na plánovanou sadu funkcí a soucit vývoj zákazníků.

**Konkurenční priority:**

- Fokus funkcí: počáteční plány pro inovace na stávající digitální nemovitosti a cloudové možnosti pro zajištění sady funkcí, které splňují požadavky zákazníků. V plánu je snadné řídit technickou implementaci, což vede k tomu, že se zaměří na úsilí zaměřené na vývoj. Tento přístup často vede k dosažení dočasné spokojenosti účastníků, ale snižuje pravděpodobnost, že se inovace bude chovat, což má dopad na chování zákazníků.
- Customer soucit: počáteční plány jsou důležitou součástí vývoje na straně podnikání a měly by být zahrnuté do pravidelného generování sestav. Učení, měření a sestavování pomocí zákaznických soucit je ale přesnější mírou úspěšnosti v rámci inovace. Zaměření na funkce zákazníka nad funkcemi je pravděpodobnější pro krátkodobé i dlouhodobou spokojenost zákazníků a obchodní dopad.

**Minimální rozsah:** Metodologie inovací ukazuje, jak integrovat strategii a plány na základě konsensu obchodních hodnot. Příručka pak zavádí nástroje cloudového nativního řešení, které můžou urychlit jednotlivé obory inovací a doprovodné osvědčené postupy pro jejich implementaci. Nakonec v části vylepšení procesu se dozvíte o přístupech k sestavování zákaznických soucit a jejich plánování a strategií napříč cestou k přijetí do cloudu. Tento přístup se zaměřuje na poskytování inovace s využitím co nejmenší technologie.

**Příklad rozšířeného oboru:** V některých případech může být inovace závislá na důležitých úlohách s vysokou citlivostí. Pokud je "zákazníkem" interní uživatel, vývojové úsilí může být kritické a vysoké citlivosti v průběhu prvního opakování. V těchto scénářích se doporučuje, aby týmy přijímání využily kontrolu architektury Azure a architekturu architektury Azure k vyhodnocení pokročilého návrhu architektury včas v rámci procesu.

## <a name="balance-during-govern"></a>Zůstatek během řízení

Postup zásad správného řízení cloudu je konstantní rovnováhu mezi dvěma konkurenčními prioritami: rychlost/flexibilita a dobře řízené prostředí. Tým zásad správného řízení cloudu se zaměřuje na hodnocení a minimalizaci rizik pro podnikání prostřednictvím jednotných ovládacích prvků a minimalizace změny. Tým přijetí se zaměřuje na řízení výsledků v podniku, které vyžadují nová rizika a v podstatě vytvoří změnu.

**Konkurenční priority:**

- Dobře řízené: každý ovládací prvek, který je určený k minimalizaci rizikových bloků, je nějaký aspekt změny nebo omezení možností návrhu. Řízení je nezbytné pro dobře řízené prostředí. Nicméně pokud jsou ovládací prvky navrženy a nasazeny v izolaci, mohou být škodlivou jako rizika, která jsou určena k prevenci.
- Rychlost a flexibilita: rychlost a flexibilitu jsou základní obchodní požadavky v digitální ekonomice. Obě požadavky vyžadují možnost řídit změnu pomocí minimálních blokování na inovace nebo přijetí. Pokud je změna řízena izolací zásad správného řízení, vygeneruje nová rizika, která by mohla poškodit firmy nezamýšlenými způsoby.

**Minimální rozsah:** Metodologie správy naznačuje, že žádné zásady správného řízení ani přijetí by nikdy neměly být v izolaci. Tato metodika začíná porozuměním oborům zásad správného řízení a konverzacím o podnikovém riziku, zásadách a procesu. Tým zásad správného řízení, který je jako aktivní člen v rámci jízdy v cloudu, může implementovat minimální sadu guardrails a vyřešit tak hmotná rizika v rámci plánu přijetí v cloudu. V průběhu času může tým zásad správného řízení Refaktorovat a rozbalovat tyto guardrails, aby splnila nová rizika. Tento přístup maximalizuje učení a inovace a současně minimalizuje riziko.

**Příklad rozšířeného oboru:** Pokud je obchodní riziko vysoké, obzvláště včas v době přijetí, může tým zásad správného řízení cloudu vyžadovat urychlení rozšíření implementací zásad správného řízení. Stejné doprovodné materiály a cvičení lze použít k přidání této vyšší úrovně zásad správného řízení, ale čas může být urychlený. V některých scénářích může být během nasazování první zóny pro vykládku nutné i další stav zásad správného řízení.

## <a name="balance-during-manage"></a>Zůstatek během správy

Obchodní model IT týkající se správy provozu se neustále vyvíjí za poslední desetiletí. Vzhledem k tomu, že se údržba hardwaru od jejich základní pozice přesune dál, zobrazení v Operations managementu se také přesunulo. Vzhledem k tomu, že se zvyšuje zaměření na poskytování obchodních hodnot, jsou tyto týmy v oblasti Operations managementu v konfliktu s vyrovnáváním bez operací/nízká operace vs.

**Konkurenční priority:**

- Široká investice: investice do výpadku, rychlé obnovení a monitorování v celém prostředí je tradiční pohled na správu provozu. Tento přístup může být nákladný a v době duplikace podpůrných produktů zpřístupněných dodavatelem cloudu.
- Žádná operace/nenejnižší operace: Využijte nástroje pro operace cloudového nativního řešení, abyste minimalizovali opakované a opakované úlohy, které dříve dodali zaměstnanci na plný úvazek. Snížení těchto provozních závislostí v modelu Operations managementu uvolňují tyto zaměstnance za účelem zvýšení hodnoty. Tento přístup může vést k podpoře subpar operací.

**Minimální rozsah:** Metodologie Manage navrhuje vytváření standardních hodnot správy bez operací v cloudu. Potvrdilo se, že žádné standardní hodnoty OPS nesplňují všechny obchodní potřeby, pracují s firmou a definují závazky a lépe sbližovat investice. Rozšiřte směrný plán tak, aby splňoval běžné potřeby pro všechny úlohy. Pak můžete vývojářům platforem nebo konkrétním pracovním týmům udržovat dobře spravovaná řešení v rámci dobře spravovaného prostředí.

**Příklad rozšířeného oboru:** Ve většině prostředí má malé procento úloh, jejichž obchodní hodnota odůvodňuje hloubkové investice do provozu. V těchto scénářích může tým IT chtít využít kontrolu architektury Azure a architekturu architektury Azure a pořídit hlubší provoz.

## <a name="balance-during-organize"></a>Zůstatek během uspořádání

Konkurenční priority v rámci tohoto článku se odrážejí z jednotky, která se dodává na obchodních potřebách pro zajištění rychlosti a flexibility. Stejný Shift se zobrazuje ve změnách organizačních diagramů (nebo struktur V týmu), aby bylo možné větší podporu pro obchodní výsledky. Vzhledem k tomu, že vedoucí oddělení odráží ve strukturách týmu, jsou obvykle řešeny dvě konkurenční priority: centralizované řízení vs delegované řízení.

**Konkurenční priority:**

- Centralizované řízení: centralizované řídicí modely se zaměřují na centralizaci všech ovládacích prvků potřebných pro vymáhání tuhých zásad. V tomto modelu slouží jako Block pro inovace, rychlost a flexibilitu. Je ale schopný zajistit vyšší úroveň stability, dodržování předpisů a zabezpečení.
- Delegovaný ovládací prvek: v tomto distribuovaném provozním modelu se předpokládá, že každý tým týmu DevOps nebo obchodní aplikace poskytne svou vlastní sadu ovládacích prvků, a to na základě řešení potřebných pro zajištění obchodních cílů. V tomto modelu poskytuje guardrails k tomu, aby mohl udržet týmy na cestách, ale minimalizuje počet vynucených technických omezení, kdykoli je to možné.

**Minimální rozsah:** Většina organizací prochází přirozenou sadou vývojů v průběhu času. Metodologie uspořádání popisuje nejběžnější řady vývojů. Doporučené pokyny jsou pro týmy, které se snaží přesunout do cloudového centra struktury s cílem zajistit přístup k delegovaným řízením.

**Příklad rozšířeného oboru:** Existuje mnoho situací, které by mohly aktivovat potřebu centralizovaného řízení. Požadavky na dodržování předpisů třetích stran a dočasné bezpečnostní ozáření představují dva příklady aktivačních událostí pro centralizovaný ovládací prvek. V těchto situacích se běžně vyžaduje, abyste navázali omezující zásady a tuhé a pevné ovládací prvky. Aby bylo možné pokračovat v inovaci a přijetí, doporučujeme, aby týmy centrálního IT poskytovaly tyto ovládací prvky na základě závažnosti a citlivosti jednotlivých úloh. Poskytování prostředí s menším řízením, ale zmenšeným rozsahem nebo rizikovým profilem, umožňuje flexibilitu i v případě, že je vyžadováno řízení.
