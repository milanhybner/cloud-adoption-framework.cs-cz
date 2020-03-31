---
title: Dopad na firmu v Cloud managementu
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak určit a pochopit dopad, který může mít výpadky nebo snížení výkonu ve vaší firmě.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 3e7c74a1d2afa880a0bdec5215b2237e8261ec79
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80426365"
---
# <a name="business-impact-in-cloud-management"></a>Dopad na firmu v Cloud managementu

Předpokládejme nejlepší, připravte se na nejhorší. V rámci správy IT je bezpečné předpokládat, že úlohy vyžadované pro podporu obchodních operací budou k dispozici a budou na základě vybrané závažnosti provádět v rámci sjednaných omezení. Pokud ale chcete lépe spravovat investice, je důležité pochopit dopad na firmu, když dojde k výpadku nebo snížení výkonu. Tato důležitost je znázorněná v následujícím grafu, který namapuje potenciální provozní přerušení konkrétních úloh na provozní dopad výpadků v rámci relativní škály hodnot.

![Dopad na provozní přerušení](../../_images/manage/time-value-impact.png)

Pokud chcete vytvořit spravedlivý základ pro srovnání dopadu na různé úlohy v rámci portfolia, navrhne se metrika času a hodnoty. Metrika Time/hodnota zachycuje nepříznivý dopad výpadku úloh. Obecně platí, že tento dopad se zaznamená jako přímá ztráta výnosů nebo provozních výnosů během typického období výpadku. Přesněji řečeno, vypočítá množství ztracených výnosů za jednotku času. Nejběžnější metrika času/hodnoty má *dopad na hodinu*, což měří provozní ztráty za hodinu výpadku.

K výpočtu dopadu lze použít několik přístupů. K dosažení podobných výsledků můžete použít kteroukoli z možností v následujících částech. Při výpočtu chráněných ztrát v rámci portfolia je důležité použít stejný přístup pro každou úlohu.

## <a name="start-with-estimates"></a>Začínáme s odhady

Aktuální operační modely mohou ztížit určení přesného dopadu. Naštěstí, několik systémů potřebuje vysoce přesný výpočet ztráty. V předchozím kroku zařadíme *kritickou náročnost*a doporučujeme, abyste spustili všechny úlohy s výchozí *střední důležitostí*. Středně kritické úlohy obecně získávají standardní úroveň podpory správy s poměrně nízkým dopadem na provozní náklady. Jenom v případě, že úlohy vyžadují další prostředky provozní správy, budete potřebovat přesný finanční dopad.

U všech standardizovaných úloh slouží dopad na firmu při obnovování systémů během výpadku jako proměnná stanovení priorit. Mimo tyto omezené situace má dopad na firmu malou změnu v prostředí Operations Management.

## <a name="calculate-time"></a>Vypočítat čas

V závislosti na povaze úlohy můžete vypočítat ztráty odlišně. V případě transakčních systémů s vysokým tempem, jako je třeba obchodní platforma v reálném čase, mohou být ztráty za milisekund významné. Méně často používané systémy, jako je třeba mzda, se nemusí používat každou hodinu. Bez ohledu na to, jestli je frekvence využití vysoká nebo nízká, je důležité při výpočtu finančního dopadu normalizovat časovou proměnnou.

## <a name="calculate-total-impact"></a>Vypočítat celkový dopad

Pokud chcete zvážit další investice do správy, je důležitější, že bude mít přesnější dopad na firmu. Následující tři přístupy k výpočtu ztrát jsou seřazené z nejpřesnější a nejpřesnější:

- **Upravené ztráty:** Pokud vaše firma v minulosti narazila na závažnou ztrátu, jako je hurikán nebo jiná přírodní katastrofa, mohl by při výpadku vypočítat skutečné ztráty. Tyto výpočty jsou založené na standardech pojišťovacího odvětví pro výpočet ztrát a řízení rizik. Použití upravených ztrát jako celkové množství ztrát v určitém časovém období může vést k velmi přesnému projekce.

- **Historické ztráty:** Pokud se vaše místní prostředí utrpělo historicky z výpadků infrastruktury, což vede k nestabilitě infrastruktury, může být obtížnější vypočítat ztráty. Ale stále můžete použít vzorce seřizovacího rozhraní používané interně. Pro výpočet historických ztrát Porovnejte rozdíly v prodeji, hrubých výnosech a provozní náklady v průběhu tří časových rámců: před, během a po výpadku. Prozkoumáním těchto rozdílů můžete identifikovat přesné ztráty, pokud nejsou k dispozici žádná jiná data.

- **Úplný výpočet ztráty:** Pokud nejsou k dispozici žádná historická data, můžete odvodit hodnotu srovnávací ztráty. V tomto modelu určíte průměrně hrubý výnos za hodinu pro obchodní jednotku. Když procházíte investicím, nemusíte předpokládat, že kompletní výpadek systému odpovídá 100% ztrátám výnosů. Tento předpoklad ale můžete použít jako hrubou základnu pro porovnání dopadů na ztráty a stanovení priorit investic.

Než provedete určité předpoklady týkající se potenciálních ztrát, které jsou spojené s výpadky úloh, je vhodné pracovat s vaším finančním oddělením a určit nejlepší přístup k takovým výpočtům.

## <a name="calculate-workload-impact"></a>Vypočítat dopad úloh

Při výpočtu ztrát pomocí historických dat je možné, že budete mít k dispozici dostatek informací, abyste mohli jasně určit příspěvek jednotlivých úloh k těmto ztrátám. Provádění tohoto vyhodnocení je v případě, že partnerství v rámci podniku je naprosto důležité. Po výpočtu celkového dopadu musí být tento dopad na jednotlivé úlohy rozdělený. Tato distribuce dopadu by měla přijít z obchodních účastníků, kteří by měli souhlasit s relativním a kumulativním dopadem jednotlivých úloh. Z tohoto důvodu by váš tým měl vyžádat zpětnou vazbu od vedoucích firmy, aby ověřil zarovnání. Tato zpětná vazba je často stejná jako v části emoce a odborníci na danou problematiku. Je důležité, aby toto cvičení představovalo logiku a přesvědčeníi obchodních účastníků, kteří by měli mít k dispozici informace o přidělení rozpočtu.

## <a name="use-the-template"></a>Použití šablony

Pokud používáte [sešit Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k plánování správy cloudu, zvažte následující:

- Každá z nich by měla aktualizovat každou úlohu v *příkladu* nebo *čistou šablonu* s *vlivem na čas a hodnotu* jednotlivých úloh. Ve výchozím nastavení má *dopad na čas a hodnotu* za hodinu, která je přidružena k výpadku zatížení.

## <a name="next-steps"></a>Další kroky

Po definování dopadu firmy můžete [závazky zarovnávat](./commitment.md).

> [!div class="nextstepaction"]
> [Zarovnejte závazky správy s podnikem](./commitment.md)
