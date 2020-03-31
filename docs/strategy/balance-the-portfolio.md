---
title: Vyvážení portfolia
description: Objevte strategie pro vyvážení migrace, inovace a experimentování, abyste mohli využít své úsilí při migraci do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 381359391d7fc39281d49d202f66edf5691be293
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433799"
---
<!-- cSpell:ignore CSAT -->

# <a name="balance-the-portfolio"></a>Vyvážení portfolia

Přijetí do cloudu je úsilí pro správu portfolia, které cleverly zamaskováno jako technickou implementaci. Stejně jako u jakéhokoli cvičení řízení portfolia je vyrovnávání portfolia důležité. Na strategické úrovni to znamená vyvážení migrace, inovace a experimentování za účelem co nejlepšího využití cloudu. V případě, že úsilí o přijetí v cloudu je příliš daleko v jednom směru, složitost zjistí způsob, jakým se snaží přijmout. Tento článek provede čtenáře přístupy k dosažení rovnováhy v portfoliu.

## <a name="general-scope-expansion"></a>Rozšíření obecného rozsahu

Vyvážení portfolia je strategicky v podstatě. Proto je strategický také přístup v tomto článku použitý. Kvůli ukotvení strategie v rozhodnutích vycházejících z dat se v tomto článku předpokládá, že čtenář už vyhodnotil existující [digitální majetek](../digital-estate/index.md) (nebo to právě provádí). Cílem tohoto přístupu je pomoci při vyhodnocování úloh, aby se zajistilo řádné vyvážení v rámci portfolia prostřednictvím kvalitativních otázek a vylepšení portfolia.

### <a name="document-business-outcomes"></a>Dokumentace k obchodním výsledkům

Než portfolio vyrovnáváte, je důležité dokumentovat a sdílet obchodní výsledky, které řídí úsilí cloudové migrace. S dokumentováním a sdílením požadovaných obchodních výsledků vám může pomoct následující tabulka. Je důležité zmínit, že většina firem najednou usiluje o dosažení několika výsledků. Důležitost tohoto cvičení spočívá v objasnění výsledků, které jsou nejpříměji spojené se snahou o migraci do cloudu:

|Výsledek  |Měřeno podle  |Cíl  |Časový rámec  |Priorita pro tuto snahu  |
|---------|---------|---------|---------|---------|
|Snížení nákladů na IT     |Rozpočet datacenter         |Snížení o 2 mil. dolarů         |12 měsíců         |1         |
|Opuštění datacenter     |Opuštění datacenter         |2 datacentra         |6 měsíců         |2         |
|Zvýšení svižnosti firmy     |Zlepšení doby uvedení na trh  |Zkrácení doby nasazení o šest měsíců         |2 roky         |3        |
|Zlepšení zkušeností zákazníků     |Spokojenost zákazníků (CSAT)         |Zlepšení o 10 %         |12 měsíců         |4         |

> [!IMPORTANT]
> Výše uvedená tabulka je fiktivní příklad a neměla by sloužit ke stanovování priorit. V mnoha případech by se tato tabulka mohla považovat za antipattern tím, že se na základě zkušeností uživatelů umístí úspory nákladů.

Výše uvedená tabulka by mohla přesně reprezentovat priority týmu cloudové strategie a týmu přijetí cloudu. Kvůli krátkodobým omezením klade tento tým větší důraz na snížení nákladů na IT a dává větší prioritu opuštění datacenter jako způsobu, jak požadovaného snížení nákladů na IT dosáhnout. Díky zdokumentování konkurenčních priorit v této tabulce ale může tým přechodu na cloud pomoct týmu cloudové strategie s identifikováním příležitostí k lepšímu sladění implementace nadřazené strategie portfolia.

### <a name="move-fast-while-maintaining-balance"></a>Rychlé jednání při zachování rovnováhy

Pokyny týkající se [přírůstkové racionalizace digitálního majetku](../digital-estate/index.md) navrhují přístup, kdy racionalizace začíná u nevyvážené pozice. Tým cloudové strategie by měl vyhodnotit všechny úlohy z hlediska kompatibility s přístupem založeným na změně hostitele. Takový přístup se navrhuje, protože umožňuje rychlé vyhodnocení složitého digitálního majetku na základě kvantitativních dat. Vytvoření takového prvotního předpokladu umožňuje týmu přechodu na cloud, aby se rychle zapojil, čímž se zkrátí čas k dosažení obchodních výsledků. Jak je ale v uvedeném článku zmíněno, kvalitativní otázky v portfoliu zajistí potřebné vyvážení. Tento článek dokumentuje proces dosažení slíbeného vyvážení.

### <a name="importance-of-sunset-and-retire-decisions"></a>Důležitost rozhodnutí o ukončení a vyřazení

V tabulce v části [zdokumentování obchodních výsledků](#document-business-outcomes) výše chybí klíčový výsledek, který by podporoval nejdůležitější cíl snížení nákladů na IT. Když se kdekoli v seznamu obchodních výsledků nachází snížení nákladů na IT, je důležité vzít v úvahu potenciál ukončení nebo vyřazení úloh. V některých scénářích může úspora nákladů vycházet z toho, že se NEBUDOU migrovat úlohy, které si nevynucují krátkodobé investování. Někteří zákazníci hlásí úspory nákladů přesahující 20 % úspor celkových nákladů díky vyřazení nedostatečně využívaných úloh.

K vyvážení portfolia, které lépe odráží rozhodnutí o ukončení a vyřazení, se týmu cloudové strategie a týmu přechodu na cloud doporučuje, aby se v rámci procesů vyhodnocení a migrování u jednotlivých úloh ptali na tyto otázky:

- Používali koncoví uživatelé tuto úlohu v posledních šesti měsících?
- Je provoz koncových uživatelů konzistentní nebo rostoucí?
- Bude firma tuto úlohu vyžadovat za 12 měsíců?

Pokud je odpověď na kteroukoli z těchto otázek záporná, může být taková úloha kandidátem na vyřazení. Pokud vlastník aplikace potenciál k vyřazení potvrdí, může migrace takové úlohy postrádat smysl. Vede to k několika kvalifikačním otázkám:

- Je možné pro tuto úlohu stanovit plán vyřazení nebo plán ukončení?
- Dá se tato úloha vyřadit před opuštěním datacentra?

Pokud je odpověď na obě tyto otázky kladná, pak by bylo vhodné zvážit možnost, že se úloha migrovat _nebude_. Tento přístup by pomohl splnit cíle snížení nákladů a opuštění datacentra.

Pokud je odpověď na kteroukoli otázku záporná, může být vhodné vytvořit plán pro hostování úlohy, dokud ji nebude možné vyřadit. Tento plán by mohl zahrnovat přesunutí prostředků do datacentra s nižšími náklady nebo alternativního datacentra. Tím by se také dosáhlo cílů snížení nákladů a opuštění jednoho datacentra.

## <a name="adopt-process-changes"></a>Přijmout změny procesu

Vyvážení portfolia vyžaduje další kvalitativní analýzu během provádění, což vám pomůže zajistit jednoduchou racionalizaci portfolia.

Na základě dat z tabulky v části [zdokumentování obchodních výsledků](#document-business-outcomes) existuje pravděpodobné riziko, že se portfolio příliš odkloní k modelu realizace se zaměřením na migraci. Pokud byly nejvyšší prioritou zkušenosti zákazníků, bude pravděpodobnější portfolio s velkým důrazem na inovace. Ani jedno není správné nebo špatné, ale příliš velké odklonění v jednom směru má obvykle za následek snížení návratnosti, zbytečné zvýšení složitosti a prodloužení doby realizace související se snahou o přijetí cloudu.

Aby se snížila složitost, měli byste postupovat podle tradičního přístupu k racionalizaci portfolia, ale v iterativním modelu. Následující kroky popisují kvalitativní model takového přístupu:

- Tým pro cloudovou strategii udržuje backlog úloh s určenou prioritou, které se mají migrovat.
- Tým cloudové strategie a tým přechodu na cloud před dokončením každé verze pořádají schůzku k plánování verze.
- V rámci schůzky k plánování verze se týmy dohodnou na prvních 5 až 10 úlohách v backlogu úloh s určenou prioritou.
- Mimo schůzku k plánování verze klade tým pro přijetí cloudu vlastníkům aplikací a odborníkům na danou problematiku tyto otázky:
  - Dá se tato aplikace nahradit ekvivalentní platformou jako službou (PaaS)?
  - Je tato aplikace aplikací třetí strany?
  - Byl schválen rozpočet k investování do průběžného vývoje aplikace během příštích 12 měsíců?
  - Mohl by další vývoj této aplikace zlepšit zkušenosti zákazníků? Vytvořit konkurenční výhodu? Vést k dalším výnosům pro firmu?
  - Budou data v rámci této úlohy přispívat k inovacím v souvislosti s BI, Machine Learning, IoT nebo souvisejícími technologiemi?
  - Je úloha kompatibilní s moderními aplikačními platformami, jako je Azure App Service?
- Odpovědi na výše uvedené otázky a jakékoli další požadované kvalitativní analýzy by pak ovlivnily úpravy backlogu s určenou prioritou. Může jít třeba o tyto úpravy:
  - Pokud se dá úloha nahradit řešením PaaS, je možné ji z backlogu pro migraci úplně odebrat. Minimálně dodatečná opatrnost pro rozhodování mezi opětovným hostováním a nahrazením by se přidala jako úloha, dočasně se tím zkracuje priorita úlohy z nevyřízených položek migrace.
  - Pokud je úloha (nebo by měla být) vyvíjena při vývoji vývoje, může být nejlépe přizpůsobená refaktorový model opětovného sestavování. Vzhledem k tomu, že inovace a migrace vyžadují různé technické dovednosti, aplikace, které se rovnají refaktoru opětovného sestavování, by měly být spravovány pomocí nevyřízených položek pro inovace, nikoli z nevyřízených položek migrace.
  - Pokud je úloha součástí inovace podřízeného systému, může být vhodné refaktorovat datovou platformu, ale ponechat vrstvy aplikace jako kandidáta na změnu hostitele. Menší refaktoring datové platformy úlohy se dá často řešit v backlogu pro migraci nebo inovaci. Tento výsledek racionalizace může vést k podrobnějším pracovním položkám v backlogu, ale jinak žádným změnám priorit.
  - Pokud úloha není strategická, ale je kompatibilní s moderními cloudovými platformami pro hostování aplikací, může být vhodné provést v aplikaci menší refaktoring, aby se nasadila jako moderní aplikace. To může přispět k celkovým úsporám díky snížení celkových licenčních požadavků na IaaS a OS migrace do cloudu.
  - Pokud je úloha aplikací třetí strany a její data se neplánují používat v rámci inovace podřízeného systému, může být nejlepší ponechat ji v backlogu jako možnost změny hostitele.

Tyto otázky by neměly být v rozsahu kvalitativní analýzy dokončené pro každou úlohu, ale pomáhají při řešení složitosti nevyváženého portfolia.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Během migrace můžou mít aktivity vyvažování portfolia negativní dopad na rychlost migrace (rychlost, jakou se migrují prostředky). V následujících pokynech se dozvíte, proč a jak sladit práci, aby nedocházelo k přerušení snahy o migraci.

Racionalizace portfolia vyžaduje různorodé technické snahy. Pro týmy pro příjem cloudu je lákavé sladit tuto rozmanitost portfolia v rámci snah o migraci. Obchodní zúčastněné strany žádají, aby jeden tým pro přijetí cloudu řešil celý backlog pro migraci. To je jen zřídka vhodný přístup, v mnoha případech to může být kontraproduktivní.

Tyto různorodé úsilí by se měly rozdělit do dvou nebo více týmů pro přijímání v cloudu. Když jako příklad realizace použijeme model dvou týmů, je Tým 1 týmem pro migraci a Tým 2 je týmem pro inovaci. V případě větších snah se tyto týmy můžou dál rozdělit k řešení dalších přístupů, jako jsou snahy o nahrazení/PaaS nebo o menší refaktoring. Tady je popis dovedností a rolí potřebných ke změně hostitele, refaktoringu nebo menšímu refaktoringu:

Opětovné **hostování:** Opětovné hostování vyžaduje, aby členové týmu implementovali infrastruktury zaměřené na změny. Obecně se používá nástroj jako Azure Site Recovery k migraci virtuálních počítačů nebo jiných prostředků do Azure. Tato práce je vhodná pro správce datacenter nebo implementátory IT. Pro tuto práci ve velkém měřítku je dobře strukturovaný tým pro migraci do cloudu. Je to nejrychlejší přístup k migraci stávajících prostředků ve většině scénářů.

**Refaktoring:** Refaktoring vyžaduje, aby členové týmu změnili zdrojový kód, změnili architekturu aplikace nebo přijali nové cloudové služby. Obecně tato snaha využívá vývojářské nástroje jako sada Visual Studio a nástroje kanálu nasazení jako Azure DevOps k opětovnému nasazení modernizovaných aplikací do Azure. Tato práce se dobře hodí pro role vývoje aplikací nebo role vývoje kanálu DevOps. Nejlépe strukturovaný pro tuto práci je tým pro cloudové inovace. Může trvat déle, než se v tomto přístupu stávající prostředky nahradí cloudovými prostředky, aplikace ale můžou využít výhod funkcí nativních pro cloud.

**Vedlejší refaktoring:** Některé aplikace mohou být moderní s menším refaktoringem na úrovni dat nebo aplikací. Tato práce vyžaduje, aby členové týmu nasadili data do cloudových datových platforem nebo provedli drobné změny konfigurace v aplikaci. To může vyžadovat omezenou podporu pro odborníky na problematiku dat nebo vývoje aplikací. Tato práce se ale podobá práci prováděné implementátory IT při nasazování aplikací třetích stran. Tato práce je vhodná pro tým pro migraci do cloudu nebo tým pro cloudovou strategii. I když tato snaha není zdaleka tak rychlá jako migrace se změnou hostitele, zabere méně času než refaktoring.

Během migrace by se mělo úsilí rozdělit třemi způsoby uvedenými výše a v příslušné iteraci provést vhodným týmem. I když byste portfolio měli rozrůznit, zajistěte také, aby úsilí zůstalo velmi zaměřené a oddělené.

## <a name="next-steps"></a>Další kroky

Seznamte se s tím, jak může [globální rozhodnutí o trhu](./global-markets.md) ovlivnit vaši cestu transformace.

> [!div class="nextstepaction"]
> [Principy globálních trhů](./global-markets.md)
