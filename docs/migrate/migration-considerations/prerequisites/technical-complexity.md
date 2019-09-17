---
title: 'Příprava na technicky složité prostředí: Agilní správa změn'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Příprava na technicky složité prostředí – agilní správa změn
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ba799c8634fc6eeda70507ae85464506103e44ff
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025374"
---
# <a name="prepare-for-technical-complexity-agile-change-management"></a>Příprava na technicky složité prostředí: Agilní správa změn

Pokud je možné zrušit a znovu vytvořit celé datové centrum pomocí jednoho řádku kódu, tradiční postupy nedokážou s těmi moderními držet krok. Pokyny obsažené v dokumentu Architektura přechodu na cloud vycházejí z metod, jako je řízení IT služeb (ITSM), rámec TOGAF (The Open Group Architecture Framework) a další. Aby byla po provedení obchodních změn zajištěná agilita a rychlost odezvy, tato architektura pracuje s danými postupy tak, aby byly v souladu s agilními metodologiemi a přístupy modelu DevOps.

Při přechodu na agilní model, který zdůrazňuje flexibilitu a iteraci, se k technické složitosti a správě změn přistupuje jinak než v případě tradičního vodopádového modelu, který se zaměřuje na lineární řadu jednotlivých kroků migrace. Tento článek popisuje špičkový přístup ke správě změn v rámci provádění migrace založené na agilních metodách. Po jeho přečtení byste měli mít obecnou představu o úrovních správy změn a o dokumentaci, která se týká inkrementální migrace. Informace, které tady najdete, slouží spolu s doplňujícím školením jako výchozí bod pro výběr a implementaci agilních postupů. Účelem tohoto článku je připravit cloudové architekty na diskuzi s projektovými manažery, aby mohli vysvětlit obecný koncept správy změn, který je součástí tohoto přístupu.

## <a name="addressing-technical-complexity"></a>Řešení technické složitosti

Při změně jakéhokoli technického systému vnáší složitost a vzájemná závislost do projektových plánů prvek rizika. Migrace do cloudu není výjimkou. Když se tisíce &mdash;nebo desítky tisíc&mdash; prostředků přesouvají do cloudu, riziko se ještě zvyšuje. Detekce a mapování všech závislostí napříč rozsáhlým digitálním prostředím by trvalo roky. S takto dlouhým analytickým cyklem by se nespokojila snad žádná firma. Aby se vyrovnala potřeba analýzy a modernizace podnikové architektury, dokument Architektura přechodu na cloud se v oblasti správy produktových backlogů zaměřuje na model INVEST. Následující části shrnují tento typ modelu.

## <a name="invest-in-workloads"></a>Model INVEST a sady funkcí

Dokument Architektura přechodu na cloud často pracuje s pojmem _sada funkcí_. Sada funkcí představuje jednotku aplikačních funkcí, kterou je možné migrovat do cloudu. Může to být jedna aplikace, vrstva aplikace, nebo kolekce aplikací. Tato definice je flexibilní a v různých fázích migrace se může měnit. Architektura přechodu na cloud často pro definici sady aplikací používá pojem _INVEST_.

INVEST představuje v řadě agilních metodologií běžný akronym pro zápis uživatelských scénářů nebo položek produktových backlogů. Obě tyto položky jsou výstupem nástrojů pro agilní řízení projektů. Měrnou jednotkou výstupu migrace je migrovaná sada funkcí. Architektura pro přechod do cloudu pracuje s akronymem INVEST trochu volněji a vytváří na jeho základě koncept pro definici sad funkcí:

- **Independent (Nezávislost):** Sada funkcí by neměla mít žádné nepřístupné závislosti. Aby bylo možné sadu funkcí považovat za migrovanou, všechny závislosti by měly být přístupné a měly by být součástí procesu migrace.
- **Negotiable (Možnost změn):** Když se provede další zjišťování, definice sady funkcí se změní. Architekti, kteří plánují migraci, můžou měnit faktory týkající se závislostí. Mezi body, které můžou podléhat změnám, patří předběžné uvolnění funkcí do produkčního prostředí, zpřístupnění funkcí prostřednictvím hybridní sítě nebo balíčkování všech závislostí do jednoho uvolnění prostředků.
- **Valuable (Hodnota):** Hodnota se v sadě funkcí měří podle schopnosti zajistit uživatelům přístup k produkčnímu prostředí.
- **Estimable (Možnost odhadu):** Mělo by být možné předem odhadnout počet všech závislostí, prostředků, dobu trvání migrace, výkonnost cloudu a náklady na něj a tento odhad by měl být vytvořen dřív, než začne samotná migrace.
- **Small (Malý počet):** Cílem je zabalit sady funkcí do jednoho sprintu. Ne vždy je to ale možné. Místo toho se doporučuje plánovat sprinty a uvolnění prostředků tak, aby se co nejvíce zkrátil čas potřebný k přesunu sady funkcí do produkčního prostředí.
- **Testable (Možnost testování):** Vždy by měl být definovaný způsob, jak otestovat a ověřit dokončení migrace jednotlivých sad funkcí.

Smyslem tohoto akronymu není jeho přísné dodržování. Měl by sloužit jako návod pro definování pojmu _sada funkcí_.

## <a name="migration-backlog-aligning-business-priorities-and-timing"></a>Backlog migrace: Sladění obchodních priorit a načasování

Backlog migrace umožňuje sledovat portfolio vašich nejdůležitějších sad funkcí, které jsou určené pro migraci. Před zahájením migrace by tým cloudové strategie a tým přechodu na cloud měly provést kontrolu aktuálního [stavu digitálního prostředí](../../../digital-estate/index.md) a shodnout se na seznamu prioritních sad funkcí, které se budou migrovat. Tento seznam bude sloužit jako výchozí backlog migrace.

Sady funkcí obsažené v backlogu migrace nebudou na začátku pravděpodobně splňovat kritéria INVEST popsaná v předchozí části. Budou představovat logické seskupení prostředků z počátečního inventáře a bude se od nich odvíjet budoucí práce. Jako zástupné symboly nemusí být technicky přesné, ale budou sloužit jako základ pro koordinaci postupu s firmou.

![Vztah mezi backlogy migrace, uvolněných prostředků a iterace v průběhu procesu migrace](../../../_images/migrate/backlog-relationships.png)

*Backlogy migrace, uvolněných prostředků a iterace zaznamenávají během procesů migrace různé úrovně činností.*

V případě všech backlogů migrace by se tým zodpovědný za správu změn měl snažit získat pro všechny sady funkcí, které jsou součástí plánu, následující informace. Tato data by měla být k dispozici alespoň pro všechny sady funkcí, které jsou v procesu migrace prioritní pro následující dva nebo tři případy uvolnění prostředků.

### <a name="migration-backlog-data-points"></a>Informace v backlogu migrace

- **Obchodní dopad:** Je důležité rozumět dopadu, jaký bude mít na firmu případné nesplnění časového plánu nebo používání omezených funkcí v době, kdy budou prostředky zablokované.
- **Relativní obchodní priority:** Seznam sad funkcí seřazený podle obchodních priorit.
- **Vlastník firmy:** Zdokumentujte, kdo zodpovídá za obchodní rozhodnutí související s konkrétní sadou funkcí.
- **Technický vlastník:** Zdokumentujte, kdo zodpovídá za technická rozhodnutí související s touto sadou funkcí.
- **Předpokládaný časový plán:** Doba, na kterou se plánuje dokončení migrace.
- **Blokování sady funkcí:** Časové rámce, ve kterých by nemělo být možné sadu funkcí změnit.
- **Název sady funkcí**
- **Počáteční inventář:** Všechny prostředky potřebné k tomu, aby sada funkcí pracovala správně, včetně například virtuálních počítačů, IT zařízení, dat, aplikací a kanálů nasazení. Tyto informace budou pravděpodobně nepřesné.

## <a name="release-backlog-aligning-business-change-and-technical-coordination"></a>Backlog vydání prostředků: Sladění obchodních změn a koordinace technických aspektů

V kontextu migrace představuje _uvolnění prostředků_ nasazení jedné nebo několika sad funkcí do produkčního prostředí. Uvolnění prostředků obvykle zahrnuje několik iterací nebo technických kroků. Z pohledu obchodních změn ale představuje jednu iteraci. Jakmile bude určený počet sad funkcí připravený pro nasazení v produkčním prostředí, dojde k uvolnění prostředků. Rozhodnutí vytvořit balíček uvolněných prostředků se přijme, pokud migrované sady funkcí mají dostatečnou obchodní hodnotu, která zdůvodní provedení změn v podnikovém prostředí. Uvolnění prostředků probíhá v souladu s [plánem obchodních změn](../optimize/business-change-plan.md) a po dokončení [firemního testování](../optimize/business-test.md). Tým cloudové strategie zodpovídá za plánování a dohled nad uvolněním požadovaných podnikových prostředků.

*Backlog uvolnění prostředků* představuje plán budoucího stavu, který definuje nadcházející uvolnění prostředků. Backlog uvolnění prostředků je hlavní spojnicí mezi správou obchodních změn (*backlog migrace*) a správou technických změn (*backlog sprintu*). Backlog uvolnění prostředků tvoří seznam sad funkcí z backlogu migrace, které splňují konkrétní podmnožinu požadavků na výsledné obchodní změny. Definování a předložení backlogu uvolnění prostředků týmu přechodu na cloud je základem hlubší analýzy a plánování migrace. Jakmile tým přechodu na cloud ověří technické údaje související s uvolněním prostředků, může v souladu s aktuálními daty toto uvolnění potvrdit a vytvořit jeho časový plán.

V závislosti na stupni analýzy, který je potřeba pro potvrzení uvolnění prostředků, by tým cloudové strategie měl mít vytvořený průběžný seznam následujících dvou až čtyř balíčků s uvolněnými prostředky. Před definováním a potvrzením uvolnění prostředků by se tým měl také pokusit ověřit co největší část následujících informací. Pokud je tým cloudové strategie disciplinovaný a dokáže si udržet přehled o následujících čtyřech balíčcích uvolnění prostředků, výrazně se tím zvýší konzistence i přesnost odhadovaných časových rozvrhů těchto uvolnění.

### <a name="release-backlog-data-points"></a>Informace v backlogu uvolnění prostředků

Tým cloudové strategie a tým přechodu na cloud by měly spolupracovat a ke všem sadám funkcí v backlogu uvolnění prostředků přidat následující informace:

- **Upřesněný inventář.** Ověření požadovaných prostředků, u kterých proběhne migrace. Ověření často probíhá pomocí protokolu nebo monitorování dat na úrovni hostitele, sítě nebo operačního systému. Cílem je důkladně se seznámit se závislostmi jednotlivých prostředků na síti a hardwaru při standardním zatížení.
- **Vzorce používání.** Pomáhají porozumět tomu, jak koncoví uživatelé pracují s danými prostředky. Součástí těchto vzorců je často analýza geografického rozmístění koncových uživatelů, síťových tras, pravidelných špiček v provozu, denních a hodinových špiček a složení koncových uživatelů (poměr interních a externích).
- **Očekávaný výkon.** Analýza dostupných dat z protokolu, která se na zaměřuje na propustnost, počet zobrazení stránek, síťové trasy a další údaje o výkonu potřebné pro replikaci prostředí pro koncové uživatele.
- **Závislosti:** Analýza síťového provozu a vzorců pro práci s aplikacemi, která identifikuje všechny doplňující závislosti sady funkcí, které by měly být zohledněny při posuzování připravenosti prostředí. Mezi uvolněné prostředky nezahrnujte sadu funkcí, dokud nebudete moct splnit některé z následujících kritérií:
  - Všechny závislé sady funkcí prošly migrací.
  - Byly implementovány konfigurace sítě a zabezpečení, které dané sadě funkcí umožňují mít přístup ke všem závislostem tak, aby byly splněny stávající požadavky na výkon.
- **Požadovaný postup migrace.** Na úrovni backlogu migrace představují kroky vedoucí k plánované migraci jen předpoklad, který slouží pro účely analýzy. Pokud firma přijme rozhodnutí opustit stávající datové centrum, v backlogu migrace se všechny kroky migrace považují za scénář změny hostování. Pomocí backlogu uvolněných prostředků by tým cloudové strategie měl spolu s týmem přechodu na cloud vyhodnotit dlouhodobou hodnotu dalších funkcí, modernizace a nepřetržitých investic do vývoje a rozhodnout o tom, jestli zvolit modernější postup.
- **Kritéria firemního testování.** Jakmile se do backlogu migrace přidá sada funkcí, příslušné týmy by se měly dohodnout na kritériích testování. V některých případech mohou být kritéria testování omezena na test výkonnosti s definovanou skupinou Power Users. Pro statistické ověřování se ale vyžaduje automatizovaný test výkonnosti, který by se neměl vynechat. Stávající instance aplikace často nemá žádné funkce pro automatizované testování. Pokud se tento předpoklad potvrdí, cloudoví architekti obvykle spolupracují se skupinou Power Users, aby pomocí základního zátěžového testu stávajícího řešení vytvořili srovnávací test, který se použije během migrace.

### <a name="release-backlog-cadence"></a>Backlog uvolněných prostředků a tempo jejich uvolňování

Pokud je migrace dobře připravená, prostředky se uvolňují pravidelným tempem. Rychlost práce týmu přechodu na cloud se často ustálí a prostředky se pak uvolňují po každých dvou až čtyřech iteracích (přibližně jednou za měsíc až dva). Tento proces by se ale neměl zrychlovat na úkor kvality práce. Nastavení umělého tempa uvolňování prostředků může negativně ovlivnit schopnost týmu přechodu na cloud dosahovat konzistentních výsledků.

Aby se stabilizoval dopad na podnik, tým cloudové strategie by měl ve spolupráci s firmou nastavit proces měsíčního uvolňování prostředků a pravidelně s ní komunikovat. Také by měl zajistit, aby si zákazník uvědomoval, že může trvat několik měsíců, než se nastaví pravidelné tempo uvolňování prostředků.

## <a name="sprint-or-iteration-backlog-aligning-technical-change-and-effort"></a>Backlog sprintu nebo iterace: Sladění plánu a realizace technických změn

*Sprint* neboli *iterace* představuje konzistentní, časově vázanou jednotku práce. V procesu migrace se často měří ve dvoutýdenních přírůstcích. Vyskytují se ale i případy týdenních nebo čtyřtýdenních iterací. Vytvoření časově vázaných iterací vynutí pravidelné intervaly pro dokončení dílčích úloh a umožní častěji upravovat plány na základě nově zjištěných informací. Pro každý sprint jsou obvykle v backlogu migrace definované úlohy týkající se posouzení, migrace a optimalizace sad funkcí. Tyto jednotky práce by se měly sledovat a spravovat ve stejném nástroji pro řízení projektů jako backlog migrace a uvolnění prostředků. Tento postup zajistí konzistenci napříč všemi úrovněmi správy změn.

*Backlog sprintu* neboli *backlog iterace* se skládá z technických úloh, které se mají provést v jednom sprintu nebo iteraci v rámci migrace jednotlivých prostředků. Tyto úlohy by měly vycházet ze seznamu sad funkcí, u kterých probíhá migrace. Pokud pro řízení projektů používáte nástroje, jako je například Azure DevOps (dřív Visual Studio Online), pracovní položky ve sprintu jsou podřízené položkám v produktovém backlogu v backlogu uvolnění prostředků a námětům v backlogu migrace. Vztahy nadřazených a podřízených položek zajišťují lepší přehled na všech úrovních správy změn.

Tým přechodu na cloud bude v rámci každého sprintu nebo iterace usilovat o splnění plánovaného množství technických úloh, které budou směřovat k migraci stanovené sady funkcí. Toto je konečný výsledek strategie správy změn. Jakmile bude práce hotová, tým může její úspěšné dokončení otestovat tak, že ověří, jestli je sada funkcí převedená do cloudu připravená pro nasazení v produkčním prostředí.

### <a name="large-or-complex-sprint-structures"></a>Sprinty s rozsáhlou nebo složitou strukturou

V případě migrace malého rozsahu, na které pracuje jeden samostatný tým, může jeden sprint zahrnovat všechny čtyři fáze migrace jedné sady funkcí (*posouzení*, *migraci*, *optimalizaci*, *zabezpečení a správu*). Častěji se ale stává, že tyto procesy jsou rozdělené do samostatných pracovních položek v různých sprintech a spolupracuje na nich několik týmů. V závislosti na typu změn, jejich rozsahu a jednotlivých rolích můžou mít tyto sprinty různou podobu.

- **Tovární přístup k migraci:** Migrace velkého rozsahu někdy vyžaduje přístup, který se v praxi podobá továrně. V tomto modelu se různé týmy věnují konkrétnímu procesu migrace (nebo podmnožině procesů). Po jeho dokončení se výstup sprintu jednoho týmu importuje do backlogu pro další tým. Toto je efektivní postup pro migrace velkého rozsahu typu změny hostitele, které zahrnují mnoho sad funkcí a týkají se tisíců virtuálních počítačů, které musí projít posouzením, návrhem architektury, odstraněním problémů a migrací. Podmínkou tohoto přístupu je ale nové homogenní prostředí s optimalizovanými procesy pro správu a schvalování změn.
- **Migrace ve vlnách:** Dalším postupem, který se osvědčil u migrací velkého rozsahu, je model vln. V tomto případě není rozdělení práce tak jasné. Týmy se podílí na provádění migrace jednotlivých sad funkcí. Povaha jednotlivých sprintů se ale mění. V jednom sprintu může určitý tým provést posouzení a vytvořit návrh architektury. V jiném sprintu může stejný tým provést samotnou migraci. V následujícím sprintu se může soustředit na optimalizaci a uvolnění prostředků. Tento přístup umožňuje, aby si hlavní tým udržel přehled o sadách funkcí a všech procesech, kterými procházejí. Vzhledem k rozmanitosti odborných dovedností a změnám kontextu se může stát, že tým bude pracovat pomaleji a migrace bude trvat déle. Další významné prostoje můžou být způsobené překážkami, které se objeví během schvalovacích procesů. Při použití tohoto modelu je důležité, aby backlog uvolnění prostředků obsahoval možnosti, díky kterým bude práce postupovat i v době prostojů. Také je důležité, aby členové týmu zvládali různé role a byli vybavení dovednostmi potřebnými pro zpracování jednotlivých sprintů.

### <a name="sprint-backlog-data-points"></a>Informace v backlogu sprintu

Výsledek sprintu zachycuje a dokumentuje změny provedené v sadě funkcí, takže uzavírá smyčku správy změn. Po dokončení tohoto postupu je třeba zdokumentovat minimálně následující informace: Během provádění sprintu by tato dokumentace měla být dokončena společně s technickými pracovními položkami.

- **Nasazené prostředky:** Všechny prostředky nasazené do cloudu, které hostují zatížení.
- **Nápravné akce:** Jakékoli změny prostředků, které se mají připravit na migraci do cloudu.
- **Konfigurace:** Vybraná konfigurace všech nasazených prostředků, včetně všech odkazů na konfigurační skripty.
- **Model nasazení:** Postup, který se použil pro nasazení prostředku do cloudu, včetně odkazů na jakékoli skripty nebo nástroje pro nasazení.
- **Architektura:** Dokumentace k architektuře nasazené do cloudu.
- **Metriky výkonu:** Výstup automatizovaného testování nebo podnikového testování prováděného za účelem ověření výkonu v době nasazení.
- **Jedinečné požadavky nebo konfigurace:** Jakékoli jedinečné aspekty nasazení, konfigurace nebo technických požadavků, které jsou nezbytné pro zpracování zatížení.
- **Schválení pro provoz:** Vlastník aplikace a pracovníci IT oddělení zodpovědní za správu sady funkcí po jejím nasazení s konečnou platností odsouhlasí, že je připravená na provoz.
- **Schválení architektury:** Vlastník sady funkcí a tým přechodu na cloud potvrdí všechny změny architektury, které jsou potřebné pro hostování jednotlivých prostředků.

## <a name="next-steps"></a>Další kroky

Po nastavení modelů pro správu změn je třeba vyřešit poslední požadavek, kterým je [kontrola backlogu migrace](./migration-backlog-review.md).

> [!div class="nextstepaction"]
> [Kontrola backlogu migrace](./migration-backlog-review.md)
