---
title: Kritická obchodní náročnost – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Kritická obchodní náročnost – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2b5901699be735bddac260c9def1a884431d8989
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557541"
---
# <a name="business-impact-in-cloud-management"></a>Dopad na firmu v Cloud managementu

Předpokládejme nejlepší, připravte se na nejhorší. V rámci správy IT je bezpečné předpokládat, že úlohy vyžadované pro podporu obchodních operací budou k dispozici a budou v závislosti na vybrané závažnosti provádět v dohodnutých omezeních. Pokud ale chcete lépe spravovat investice, je důležité pochopit dopad, který podnikání obchoduje, když dojde k výpadku nebo snížení výkonu. Tato důležitost je znázorněná v následujícím grafu, který mapuje potenciální provozní přerušení konkrétních úloh na obchodní dopad výpadků v rámci relativní hodnoty stupnice.

![Dopad na provozní přerušení](../../_images/manage/time-value-impact.png)

Chcete-li vytvořit spravedlivý základ pro porovnání dopadu na různé úlohy v rámci portfolia, je navržena metrika času a hodnoty. Metrika Time/hodnota zachycuje nepříznivý dopad výpadku úloh. Obecně platí, že tento dopad se zaznamená jako přímá ztráta výnosů nebo provozních výnosů během typického období výpadku. Přesněji řečeno, výpočet množství ztracených výnosů za jednotku času. Nejběžnější metrika času a hodnoty je "dopad na hodinu", který měří provozní ztráty za hodinu výpadku.

Existuje několik přístupů, které lze použít k výpočtu dopadu. Kteroukoli z možností v následujících částech lze využít s podobnými výsledky. Při výpočtu chráněných ztrát v rámci portfolia je důležité použít stejný přístup pro každou úlohu.

## <a name="start-with-estimates"></a>Začínáme s odhady

Aktuální operační modely mohou ztížit určení přesného dopadu. Naštěstí, několik systémů potřebuje vysoce přesný výpočet ztráty. V předchozím kroku: klasifikace závažnosti byla navržena tak, že všechny úlohy začínají výchozí hodnotou "střední závažnost". Středně kritické úlohy budou obecně dostávat standardní úroveň podpory správy s poměrně nízkým dopadem na provozní náklady. Jenom v případě, že úlohy vyžadují další prostředky provozní správy, bude potřeba mít přesný finanční dopad.

U všech standardizovaných úloh slouží dopad na firmu jako proměnná stanovení priorit při obnovování systémů během výpadku. Mimo tyto omezené situace bude mít dopad na firmu v prostředí Operations Management malé a žádné změny. 

## <a name="calculating-time"></a>Výpočet času

V závislosti na povaze zátěže se můžou ztráty vypočítávat odlišně. V případě transakčních systémů s vysokým tempem, jako je třeba obchodní platforma v reálném čase, mohou být ztráty za milisekund významné. Méně často používané systémy, jako je třeba mzda, se nemusí používat každou hodinu. Zda je četnost použití vysoká nebo nízká, je důležité při výpočtu finančního dopadu normalizovat časovou proměnnou.

## <a name="calculating-total-impact"></a>Výpočet celkového dopadu

Když se požaduje další investice do správy, je důležitější, že dopad na firmu bude přesnější. Osnova popsaných odrážek se blíží k výpočtu ztrát v pořadí nejpřesnější (od nejpřesnější po nejpřesnější):

- **Upravené ztráty:** Pokud v minulosti došlo k závažné ztrátě událostí, jako je hurikán nebo jiná přírodní katastrofa, může se při výpadku vypočítat skutečný počet ztrát. Tyto výpočty jsou založené na standardech pojišťovacího odvětví pro výpočet ztrát a řízení rizik. Použití upravených ztrát jako celkové množství ztrát v určitém časovém období může vést k velmi přesnému projekce.

- **Historické ztráty:** Pokud se místní prostředí utrpělo z historických důvodů kvůli nestabilitě infrastruktury, může být obtížnější vypočítat ztráty. Ale vzorce úprav se pořád dají využít interně. K výpočtu historických historií Porovnejte rozdíly v prodeji, hrubých výnosech a provozní náklady v průběhu tří časových rámců: před, během a po výpadku. Pokud nejsou k dispozici žádná jiná data, prozkoumání těchto rozdílů může identifikovat přesnou hodnotu ztratí.

- **Úplný výpočet ztráty:** Pokud nejsou k dispozici žádná historická data, může být odvozena hodnota srovnávací ztráty. V tomto modelu určete průměrnou hrubou tržbu za hodinu pro obchodní jednotku. Za předpokladu, že kompletní výpadek systému odpovídá 100% ztráty výnosů, je nedostatečným předpokladem při projekci investic do předcházení ztrátám. Ale dá se použít jako hrubou základnu pro porovnávání dopadů na ztráty a stanovení priorit investic.

Než začnete vytvářet předpoklady týkající se výpočtů ztrát, spolupracujte se svým finančním oddělením a určete nejlepší přístup k výpočtu potenciálních ztrát spojených s výpadkem úloh.

## <a name="calculating-workload-impact"></a>Výpočet dopadu na úlohy

Při využití historických dat pro výpočet ztrát může být k dispozici dostatek informací, které jasně určují dopad jednotlivých úloh na tyto ztráty. Toto hodnocení je tam, kde je partnerství s firmou naprosto důležité. Jakmile je celkový dopad vypočítán, musí mít tento dopad stejný atribut napříč jednotlivými úlohami. Tato distribuce dopadu by měla přijít z obchodních účastníků, kteří by měli souhlasit s relativním a kumulativním dopadem jednotlivých úloh. Tým by dál měl vyžádat zpětnou vazbu od obchodních vedoucích k ověření zarovnání. Výsledkem je, že konečný výsledek je stejný jako u emoce a odbornosti v závislosti na podstatách. Důležitost tohoto cvičení je taková, že představuje logiku a přesvědčeníi obchodních účastníků, kteří by měli mít k dispozici údaje o přidělení rozpočtu.

## <a name="using-the-template"></a>Použití šablony

Následující postup se týká čtenářů, kteří používají [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k naplánování správy cloudu.

1. Každá úloha v "příkladu" nebo "vyčistit šablonu" by měla být aktualizována firmou s hodnotou "čas/hodnota dopadu" každého zatížení. Výchozí hodnota "čas/hodnota dopadu" představuje předpokládané ztráty za hodinu přidruženou k výpadku zatížení.

## <a name="next-steps"></a>Další kroky

Po definování dopadu [lze závazky zarovnávat](./commitment.md).

> [!div class="nextstepaction"]
> [Zarovnejte závazky správy s podnikem](./commitment.md)
