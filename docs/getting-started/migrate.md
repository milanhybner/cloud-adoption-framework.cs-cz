---
title: Zahájení cesty migrace do cloudu v Azure
description: Získejte ucelený návod pro přechod úloh starších verzí aplikací do cloudu pomocí inovativních cloudových technologií.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 3ec14b513bc8030d2b04144465ecc0cbb48b97fc
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434794"
---
# <a name="begin-a-cloud-migration-journey-in-azure"></a>Zahájení cesty migrace do cloudu v Azure

K zahájení cesty migrace do cloudu použijte rozhraní pro přijetí Microsoft Cloud pro Azure. Tato architektura poskytuje komplexní pokyny pro přechod úloh starších verzí aplikací do cloudu pomocí inovativních cloudových technologií.

## <a name="executive-summary"></a>Shrnutí

Architektura pro přijetí do cloudu pomáhá zákazníkům provádět zjednodušenou cestu k přijetí do cloudu. Toto rozhraní obsahuje podrobné informace o cestě k přijetí cloudu, počínaje cílovým obchodním výsledkům a pak zarovnává připravenost a hodnocení cloudu s jasnými definovanými obchodními cíli. Tyto výsledky jsou dosaženy prostřednictvím definované cesty pro přijetí v cloudu. Při přijetí na základě migrace se definovaná cesta zaměřuje hlavně na migraci místních úloh do cloudu. Tato cesta někdy zahrnuje modernizaci úloh, aby se zvýšila návratnost investic z úsilí o migraci.

Tato architektura je navržená hlavně pro cloudové architekty a týmy cloudové strategie, které provedou úsilí při přijímání v cloudu. Mnoho věcí v tomto rozhraní je však relevantní pro jiné role napříč podnikem. Cloudové architekty často slouží jako zprostředkovatelé k zapojení všech relevantních rolí. Tento souhrn výkonného vedení je navržený tak, aby před tím, než usnadnil konverzace, připravil různé role.

> [!NOTE]
> Tento návod je aktuálně ve verzi Public Preview. Terminologie, přístupy a pokyny jsou v této verzi Preview důkladně testovány se zákazníky, partnery a Microsoft Teams. V takovém případě se obsah a doprovodné materiály můžou v průběhu času mírně měnit.

## <a name="motivations"></a>Motivace

Migrace do cloudu můžou popomáhat firmám, které dosáhnou svých požadovaných obchodních výsledků. Jasná komunikace motivů, obchodních faktorů a měření úspěšnosti jsou důležité základy pro rozhodování v rámci úsilí o migraci do cloudu. Následující tabulka klasifikuje podněty usnadňující tuto konverzaci. Předpokládá se, že většina společností bude mít motivaci v rámci každé klasifikace. Cílem této tabulky je Neomezovat výsledky, ale místo toho je snazší určit prioritu celkových cílů a motivace:

<!-- markdownlint-disable MD033 -->

|Kritické obchodní události | Motivace migrace | Motivace inovací |
|---------|---------|---------|
| Ukončení Datacenter<br/><br/>Fúze, akvizice nebo divestiture<br/><br/>Snížení nákladů na velká písmena<br/><br/>Konec podpory pro klíčové technologie<br/><br/>Reakce na změny dodržování předpisů v legislativě<br/><br/>Splnění nových požadavků na svrchovanost dat<br/><br/>Snížení výpadků a vylepšení stability IT|Úspora nákladů<br/><br/>Snížení pro dodavatele nebo technickou složitost<br/><br/>Optimalizace interních operací<br/><br/>Zvýšení svižnosti firmy<br/><br/>Příprava na nové technické možnosti<br/><br/>Škálování pro splnění požadavků na trh<br/><br/>Škálování pro splnění geografických nebo tržních požadavků|Příprava na nové technické možnosti<br/><br/>Sestavování nových technických možností<br/><br/>Modernizovat zabezpečení stav a ovládací prvky<br/><br/>Škálování pro splnění geografických nebo tržních požadavků<br/><br/>Zlepšení zkušeností a zapojení zákazníků<br/><br/>Transformace produktů nebo služeb<br/><br/>Přerušení trhu novými produkty nebo službami|

<!-- markdownlint-enable MD033 -->

Když je odezva na kritické obchodní události nejvyšší prioritou, je důležité zapojovat se do [cloudové implementace](#cloud-implementation) včas, často paralelně s strategií a plánováním úsilí. Provedení takového přístupu vyžaduje růst místo a ochotu pro iterativní vylepšit procesy na základě přímých lekcí, které se naučily.

Když jsou motivace migrace prioritní, [strategie a plánování](#cloud-strategy-and-planning) budou hrát důležitou roli v předstihu v tomto procesu. Je ale vysoce navržená [implementace](#cloud-implementation) prvního zatížení paralelně s plánováním, aby tým pomohla pochopit a plánovat všechny výukové křivky spojené s cloudem.

Pokud jsou motivace s nejvyšší prioritou nejvyšší prioritou, strategie a plánování budou vyžadovat další investice do začátku procesu, aby se zajistilo rovnováhu v portfoliu a provedlo se sblížení investic provedených během cloudu. Další informace o tom, jak porozumět podnětům pro inovace, najdete v tématu [pochopení cesty inovace](./innovate.md).

Připravují se všechny účastníky v rámci úsilí o migraci s vědomím motivace, která by zajistila rozhodnutí. Následující metodologie migrace popisuje, jak společnost Microsoft navrhuje zákazníky v rámci jednotné metodologie.

## <a name="migration-approach"></a>Postup migrace

Rozhraní pro přijetí do cloudu vytvoří na nejvyšší úrovni plán, který je připravený, aby bylo možné seskupit typy úsilí požadované v rámci jakéhokoli přijetí v cloudu. Tento výkonný souhrn se sestavuje na tomto toku vysoké úrovně za účelem vytvoření iterativních procesů, které můžou usnadnit optimalizaci úsilí a úsilí o modernizaci v rámci jediného přístupu napříč všemi aktivitami migrace do cloudu.

Tento přístup se skládá ze dvou metodologií nebo oblastí zaostření: strategie cloudu & plánování a implementace cloudu. [Motivace](#motivations) nebo požadovaná obchodní výsledek migrace do cloudu často určuje, kolik týmů by měl investovat do [strategie a plánování](#cloud-strategy-and-planning) a [implementace](#cloud-implementation). Tyto podněty můžou také ovlivnit rozhodování, aby se prováděly postupně nebo paralelně.

## <a name="cloud-implementation"></a>Implementace cloudu

Implementace cloudu je iterativní proces pro migraci a modernizacií digitálního majetku, který je zarovnaný k cíleným obchodním výsledkům a ovládacím prvkům pro správu změn. Během každé iterace jsou úlohy migrovány nebo moderní v souladu s strategií a plánem. Rozhodnutí týkající se IaaS, PaaS nebo hybridu jsou prováděna během fáze posuzování [metodologie migrace](../migrate/index.md) pro optimalizaci řízení a provádění. Tato rozhodnutí budou řídit nástroje používané během každé iterace fáze migrace v rámci stejné metodologie. Tento model se dá použít s minimální strategií a plánováním. Aby se ale zajistila největší obchodní návratnost, měla by IT i podnik zarovnávat jasně strategii a plán pro Průvodce aktivit implementace.

![Metodologie implementace cloudu v rozhraní pro přijetí do cloudu](../_images/migrate/methodology.png)

Zaměření na toto úsilí je migrace nebo modernizace úloh. Úloha je kolekce infrastruktury, aplikací a dat, která souhrnně podporuje běžný obchodní cíl, nebo provádění běžného obchodního procesu. Příklady úloh můžou zahrnovat například obchodní aplikace, řešení výplaty v PERSONÁLNÍm oddělení, řešení CRM, pracovní postup schvalování finančních dokumentů nebo řešení business intelligence. Úlohy mohou zahrnovat i sdílené technické prostředky, jako je datový sklad, který podporuje několik dalších řešení. V některých případech může být pracovní postup reprezentován jedním prostředkem, jako je například server, aplikace nebo datová platforma.

Migrace do cloudu se často považují za jeden projekt v širším programu, aby se zjednodušily IT operace, náklady nebo složitost. Metodologie implementace v cloudu pomáhá sjednotit technické úsilí v rámci série migrací úloh na vyšší úroveň obchodních hodnot, které jsou uvedené v cloudové strategii a plánu.

**Začínáme:** Zahajte implementaci cloudu pomocí [Průvodce migrací Azure](../migrate/azure-migration-guide/index.md) a [příručky pro instalaci Azure](../ready/azure-setup-guide/index.md), která popisuje nástroje a procesy vysoké úrovně potřebné k úspěšnému provedení implementace cloudu. Migrace prvního zatížení pomocí těchto průvodců pomůže týmu překonat počáteční výukové křivky včas v procesu plánování. Následně by se měly další informace předávat [osvědčeným postupům migrace](../migrate/azure-best-practices/index.md) a [důležitým](../migrate/migration-considerations/index.md) postupům k migraci za účelem zarovnání základních pokynů s jedinečnými omezeními, procesy, týmy týmu a cíli vaší snahy.

## <a name="cloud-strategy-and-planning"></a>Strategie a plánování cloudu

Cloudová strategie a plánování je metodologie, která se zaměřuje na zarovnání obchodních výsledků, priorit a omezení za účelem vytvoření jasné strategie a plánu migrace. Výsledný plán (nebo nevyřízené položky migrace) popisuje přístup k migraci a modernizaci v rámci portfolia IT, který může zahrnovat celá datacentra, několik úloh nebo různé kolekce infrastruktury, aplikací a dat. Řádná správa portfolia IT v rámci úsilí o implementaci v cloudu vám pomůže vyřídit požadované obchodní výsledky.

![Přehled architektury přechodu na cloud](../_images/caf-overview.png)

**Začínáme:** Zbývající část tohoto článku připravuje čtecí modul na správnou aplikaci cloudové strategie rozhraní pro přijetí do cloudu a metodologie plánování. Popisuje také další zdroje informací a odkazy, které mohou čtenářům usnadnit přístup k úsilí o implementaci cloudu.

### <a name="methodology-explained"></a>Vysvětlení metodologie

Strategii cloudu a metodologie plánování pro cloudový vývoj jsou založené na přírůstkovém přístupu k implementaci cloudu, která je v souladu s strategickými technologickými strategiemi, kulturou na základě růstu místo a strategií řízenými obchodní výsledky. Tato metodologie se skládá z následujících komponent na nejvyšší úrovni, které vedou k implementaci každé strategie.

Jak je znázorněno na obrázku výše, toto rozhraní zarovnává strategická rozhodnutí s malým počtem obsažených procesů, které fungují v iterativním modelu. Jak je popsáno v lineárním dokumentu, každý z následujících procesů se očekává do začátku paralelně s iteracemi cloudové implementace. Odkazy na jednotlivé procesy budou pomoci při definování koncového stavu a způsobů, jak se má ukončit do požadovaného koncového stavu:

- **[Plán](../strategy/index.md):** Pokud je technická implementace zarovnána s jasnými obchodními cíli, je mnohem snazší měřit a sjednotit úspěch napříč několika úsilími v oblasti implementace cloudu, bez ohledu na technické rozhodnutí.
- **[Připraveno](../ready/index.md):** Příprava podnikání, jazykové verze, lidí a prostředí pro změny vede k úspěchu v každém úsilí a zrychluje implementaci a změny projektů.
- **Přijmout:** Zajistěte správnou implementaci požadovaných změn napříč IT a obchodními procesy, abyste dosáhli obchodních výsledků.
  - **[Migrace](../migrate/index.md):** iterativní provádění [metodologie implementace v cloudu](#cloud-implementation) , která se řídí testovaným procesem vyhodnocování, migrace, optimalizace a zabezpečení & pro vytvoření opakovaného procesu pro migraci úloh.
  - Inovace  **[Innovate](../innovate/index.md):** Využijte provozní hodnoty prostřednictvím inovačních aktivit, které rozšiřují nové technické dovednosti a rozšířené obchodní možnosti.
- **[Řídit](../govern/index.md):** Zarovnejte podnikové zásady s hmotnými riziky, které jsou omezeny prostřednictvím zásad, procesů a cloudových nástrojů zásad správného řízení.
- **[Spravovat](../manage/index.md):** Rozšiřte IT operace a zajistěte, aby cloudová řešení mohla být provozována prostřednictvím bezpečných a cenově výhodnějších procesů s využitím moderních cloudových nástrojů pro operace.
- **[Uspořádání](../organize/index.md):** Zarovnejte lidi a týmy s cílem zajistit správné cloudové operace a přijetí.

V rámci této migrace se tato architektura bude používat k řešení nejednoznačnosti, správě změn a seznámení s různými funkčními týmy prostřednictvím realizace obchodních výsledků.

### <a name="common-cultural-changes-resulting-from-adherence-to-this-methodology"></a>Společné kulturní změny vyplývající z dodržování této metodiky

Snaha o dosažení požadovaných obchodních výsledků může aktivovat drobné změny v jazykové verzi, zabezpečení a do jisté míry jako jazykovou verzi firmy. Níže jsou uvedeny některé běžné kulturní změny, které se zobrazují v tomto procesu:

- Týmy IT a zabezpečení budou nejspíš přijímají nové dovednosti v podpoře úloh v cloudu.
- Provádění migrace do cloudu podporuje iterativní nebo agilní přístupy.
- Zahrnutí zásad správného řízení cloudu má také za následek inspirovat DevOps přístupy.
- Vytvoření týmu cloudové strategie může vést k užší integraci mezi firmou a vedoucími IT.
- Souhrnně tyto změny mají za následek větší firmu a flexibilitu IT.

Kulturní změna není cílem migrace do cloudu nebo architektury pro přijetí v cloudu, ale jedná se o často známý výsledek.
Kulturní změny se přímo neřídí, místo toho se v rámci těchto pokynů vloží jemných změn v jazykové verzi do navrhovaných procesů a přístupů.

### <a name="common-technical-efforts-associated-with-this-methodology"></a>Společné technické úsilí spojené s touto metodologií

Při implementaci cloudové strategie a naplánování IT týmu se zaměří na velké procento času migrace stávajících digitálních prostředků do cloudu. Během tohoto úsilí se očekávají minimální změny kódu, ale můžou se často omezit na změny konfigurace. V mnoha případech je možné pro modernizaci v rámci migrace do cloudu vytvořit silné obchodní odůvodnění.

### <a name="common-workload-examples"></a>Běžné příklady úloh

Cloudová strategie a plánování často cílí na širokou škálu úloh a aplikací. V rámci portfolia jsou obvykle migrovány běžné aplikace nebo typy úloh. Tady je několik příkladů:

- Obchodní aplikace
- Zákaznické aplikace
- Aplikace třetí strany
- Platformy pro analýzu dat
- Globálně distribuovaná řešení
- Vysoce škálovatelná řešení

### <a name="common-technologies-migrated"></a>Migrace běžných technologií

Technologie migrované do cloudu se průběžně rozšiřují jako poskytovatelé cloudu, kteří přidávají nové funkce. Následuje několik příkladů technologií, které se běžně vyskytují při migraci:

- Windows a SQL Server
- Databáze Linux a Open Source (OSS)
- Nestrukturované a NoSQL databáze
- SAP v Azure
- Analýza (datový sklad, Data Lake)

## <a name="next-steps-lifecycle-solution"></a>Další kroky: řešení životního cyklu

Rozhraní pro přijetí do cloudu je řešením životního cyklu. Je navržený tak, aby pomáhal čtenářům, kteří právě začínají svoji cestu, a také čtenářům, kteří se do migrace nacházejí hluboko. V takovém případě je obsah velmi kontextu a specifických pro cílovou skupinu. Další kroky jsou nejlépe zarovnané na proces vysoké úrovně, který čtenář chce zlepšit.

> [!div class="nextstepaction"]
> [Strategie](../strategy/index.md)
>
> [Plánování](../plan/index.md)
>
> [K](../ready/index.md)
>
> [Migrace](../migrate/index.md)
>
> [Inovace](../innovate/index.md)
>
> [Bude](../govern/index.md)
>
> [Správa](../manage/index.md)
>
> [Přehled](../organize/index.md)

<!-- test:ignoreNextStep -->
