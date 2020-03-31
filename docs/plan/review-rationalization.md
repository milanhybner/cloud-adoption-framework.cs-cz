---
title: Kontrola racionalizačních rozhodnutí
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak zkontrolovat rozhodnutí o racionalizaci a připravit se na usnadnění konverzace s firmou.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 90a6718c028023e1bae101b35fff873dd47e4ab2
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80427962"
---
# <a name="review-rationalization-decisions"></a>Kontrola racionalizačních rozhodnutí

Při počátečních fázích a plánovacích fázích doporučujeme použít k digitálnímu majetku [přírůstkový přístup k racionalizaci](../digital-estate/rationalize.md#incremental-rationalization) . Tento přístup ale v rámci výsledných rozhodnutí vloží některé předpoklady. Doporučujeme, aby tým cloudové strategie a týmy pro přijímání v cloudu provedli tato rozhodnutí s ohledem na rozšířenou dokumentaci. Tato kontrola je také vhodnou dobou pro zapojení obchodních účastníků a vedoucího zadavatele do budoucích stavových rozhodnutí.

> [!IMPORTANT]
> K dalšímu ověření rozhodnutí o racionalizaci dojde během fáze hodnocení migrace. Toto ověření se zaměřuje na obchodní přezkoumání racionalizace pro správné zarovnání prostředků.

K ověření racionalizace rozhodnutí použijte následující otázky, které vám usnadní konverzaci s firmou. Otázky jsou seskupeny podle pravděpodobnáho zarovnání racionalizace.

## <a name="innovation-indicators"></a>Indikátory inovace

Pokud se v rámci společné recenze těchto otázek zobrazí odpověď "Ano", může být úlohou lepším kandidátem na inovace. Tato úloha by se nemohla migrovat přes model výtahu a Shift nebo modernizovat. Místo toho se obchodní logika nebo datové struktury vytvoří znovu jako nová nebo znovu navržená aplikace. Tento přístup může být náročný na práci a časově náročné. Ale u úloh, které představují významné obchodní návratnost, se investice odůvodňuje.

- Vytvoří aplikace v tomto pracovním postupu rozlišení trhu?
- Existují navrhované nebo schválené investice zaměřené na zlepšení prostředí přidružených k aplikacím v této zátěži?
- Zpřístupňují data v této úloze nové nabídky produktů nebo služeb?
- Je k dispozici navrhovaná nebo schválená investice, která má za cíl využít data spojená s touto úlohou?
- Může dojít k tomu, že se projeví rozlišení trhu nebo nové nabídky? Pokud ano, vrátí do bloku zvýšené náklady na inovace během přijetí cloudu?

Následující dvě otázky vám pomohou při zahrnutí nejdůležitějších technických scénářů do přezkoumání racionalizace. Zodpovězením možnosti "Ano" můžete identifikovat způsoby účtování nebo snížit náklady spojené s inovacemi.

- Budou se datové struktury nebo obchodní logiky měnit v průběhu přijetí cloudu?
- Je existující kanál nasazení, který se používá k nasazení této úlohy do produkčního prostředí?

Pokud odpověď na kteroukoli otázku je "Ano", tým by měl zvážit zahrnutí tohoto pracovního postupu jako kandidáta na inovace. Tým by měl označit tuto úlohu na kontrolu architektury za účelem identifikace příležitostí pro modernizaci.

## <a name="migration-indicators"></a>Indikátory migrace

Migrace je rychlejší a levnější způsob, jak si Cloud přijmout. Ale nevyužívá výhody k inovacím. Než budete investovat do inovací, odpovězte na následující otázky. Můžou vám pomůžou určit, jestli je model migrace pro úlohy víc použitelný.

- Podporuje tato aplikace stabilní zdrojový kód? Očekáváte, že zůstane v průběhu tohoto cyklu vydaných verzí v průběhu tohoto cyklu stabilní a nezměněný?
- Podporuje tato úloha provozní obchodní procesy ještě dnes? Provede to v průběhu tohoto cyklu vydávání verzí?
- Je to priorita, kterou toto úsilí při přijetí cloudu zvyšuje stabilitu a výkon této úlohy?
- Je snížení nákladů spojené s tímto zatížením cílem během tohoto úsilí?
- Snižuje se provozní složitost tohoto zatížení během tohoto úsilí?
- Jsou inovace omezené aktuální architekturou nebo procesy provozu IT?

Pokud je odpověď na kteroukoli z těchto otázek "Ano", měli byste zvážit model migrace pro tuto úlohu. Toto doporučení je pravdivé i v případě, že úlohy jsou kandidátem na inovace.

Problémy s provozní složitostí, náklady, výkonem nebo stabilitou můžou bránit obchodní návratnosti. Cloud můžete použít k rychlému tvorbě vylepšení souvisejících s těmito výzvami. Tam, kde je to možné, doporučujeme použít k první stabilizaci úlohy postup migrace. Pak můžete rozšířit možnosti pro inovace v stabilním a agilním cloudovém prostředí. Tento přístup poskytuje krátkodobé vrácení a snižuje náklady potřebné k zajištění dlouhodobé změny.

> [!IMPORTANT]
> Mezi modely migrace patří přírůstková modernizace. Použití architektury Platform as a Service (PaaS) je běžným aspektem migračních aktivit. Jsou to také drobné změny konfigurace, které používají tyto služby platformy. Hranice pro migraci je definována jako změna v obchodní logice nebo na podporu obchodních struktur. Taková změna se považuje za inovační úsilí.

## <a name="update-the-project-plan"></a>Aktualizace plánu projektu

Dovednosti potřebné pro úsilí při migraci se liší od dovedností potřebných pro úsilí v rámci inovace. Při implementaci plánu přijetí do cloudu doporučujeme, abyste přiřadili úsilí na migraci a inovace různým týmům. Každý tým má vlastní iteraci, vydanou verzi a tempem plánování. Přiřazení samostatných týmů přináší flexibilitu procesu při údržbě jednoho plánu přijetí do cloudu při monitorování účtů pro inovace a migraci.

Když spravujete plán přijetí cloudu v Azure DevOps, tato Správa se projeví změnou nadřazené pracovní položky (nebo námětu) z migrace cloudu na inovace cloudu. Tato jemná změna pomáhá zajistit, aby všichni účastníci v plánu pro přijetí do cloudu mohli rychle sledovat požadované úsilí a změny v úsilí o nápravu. Toto sledování také pomáhá zajistit správné přiřazení k příslušnému týmu přijetí cloudu.

V případě rozsáhlých složitých plánů přijetí s více různými projekty zvažte aktualizaci cesty iterace. Změna cesty k oblasti usnadňuje zobrazení úlohy pouze pro tým přiřazený k této cestě oblasti. Tato změna může usnadnit práci týmu pro přijetí cloudu tím, že snižuje počet viditelných úkolů. Přináší ale složitost pro procesy řízení projektu.

## <a name="next-steps"></a>Další kroky

[Stanovte iterace a plány vydávání](./iteration-paths.md) , abyste mohli začít plánovat práci.

> [!div class="nextstepaction"]
> [Stanovte iterace a plány vydávání](./iteration-paths.md) , abyste mohli začít plánovat práci.
