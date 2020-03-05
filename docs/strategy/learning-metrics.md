---
title: Sladění úsilí s metrikami učení
description: Seznamte se s postupem, jak zarovnávat úsilí s měřením a informovat o dopadu transformace na firmu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: b7a6081f37899f11716eca07b7e6a371bcefcc94
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337886"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-can-we-align-efforts-to-meaningful-learning-metrics"></a>Jak můžeme zarovnat úsilí k smysluplným výukovým metrikám?

[Přehled výsledků firmy](./business-outcomes/index.md) popisuje způsoby, jak změřit a sdělit dopad, který transformace bude mít v podnikání. Může to ale trvat i několik let, než se některé z těchto výsledků dovedou k měřitelným výsledkům. Panel a sada C-Suite jsou nespokojené se sestavami, které pro dlouhá časová období zobrazují rozdílovou hodnotu 0%.

Výukové metriky jsou průběžné a krátkodobé metriky, které se dají připravit na dlouhodobé obchodní výsledky. Tyto metriky se dobře rovnají s růstem místo a umožňují, aby se jazyková verze stala pružnější. Místo toho, abyste se vyčistili předpokládaný nedokončený pokrok směrem k dlouhodobému obchodnímu cíli, metriky výukového programu zvýrazňují počáteční indikátory úspěchu. Metriky také zvýrazňují prvotní indikátory selhání, což pravděpodobně vyprodukuje největší příležitost, abyste se mohli seznámit s plánem a upravovat ho.

Stejně jako u mnoha materiálů v této architektuře předpokládáme, že jste obeznámeni s [cestou transformace](../govern/guides/index.md) , která nejlépe odpovídá vašim požadovaným obchodním výsledkům. V tomto článku se dozvíte několik výukových metrik pro každou cestu transformace, která ilustruje koncept.

## <a name="cloud-migration"></a>Migrace do cloudu

Tato transformace se zaměřuje na náklady, složitost a efektivitu s důrazem na IT operace. Nejsnadněji měřená data na této transformaci jsou pohyb prostředků do cloudu. V tomto druhu transformace se digitální vlastnictví měří podle virtuálních počítačů (virtuálních počítačů), stojanů nebo clusterů, které tyto virtuální počítače hostují, provozní náklady na provoz Datacenter, nezbytné kapitálové výdaje na údržbu systémů a odpisy těchto prostředků v průběhu času.

Při přesunu virtuálních počítačů do cloudu dojde ke snížení závislosti na místních starších zdrojích. Náklady na údržbu prostředků se také snížily. Firmy bohužel nemůžou snížit náklady, dokud nebudou clustery zrušené a zapůjčení Datacenter vyprší. V mnoha případech je celá hodnota úsilí realizovaná až do dokončení cyklus odpisování.

Před provedením finančních příkazů vždycky zarovnejte s kanceláří nebo financemi. Týmy IT ale můžou obecně odhadnout aktuální peněžní náklady a budoucí hodnoty peněžních nákladů pro každý virtuální počítač na základě využití procesoru, paměti a využitého úložiště. Tuto hodnotu pak můžete použít u každého migrovaného virtuálního počítače, abyste mohli odhadnout okamžité úspory nákladů a budoucí peněžní hodnotu úsilí.

## <a name="application-innovation"></a>Inovace aplikací

Inovace aplikací s podporou cloudu se zaměřují hlavně na zkušenosti zákazníků a na ochotu zákazníka využívat produkty a služby poskytované společností. Zvýšení počtu změn na chování zákazníků nebo zákazníků se projeví v čase. Ale inovace aplikací je obvykle mnohem kratší než v ostatních formách transformace. Tradiční Rady je, že byste měli začít pochopit konkrétní chování, které chcete ovlivnit, a použít toto chování jako metriky učení. Například v aplikaci elektronického obchodování může být na cílovém chování celkové nákupy nebo nákupy doplňku. U video společnosti může být čas sledovat streamy videa v čase.

Výzvou se metrikami chování zákazníků je, že mohou být snadno ovlivněny vnějšími proměnnými. Je často důležité zahrnout do metriky kurzu související statistiky. Tyto související statistiky můžou zahrnovat verze tempo, chyby vyřešené pro jednotlivé verze, pokrytí kódu testů jednotek, počet zobrazení stránek, propustnost stránek, čas načítání stránky a další metriky výkonu aplikace. Každá z nich může zobrazit různé aktivity a změny základu kódu a prostředí pro zákazníky, aby bylo možné korelovat se vzory chování zákazníků vyšší úrovně.

## <a name="data-innovation"></a>Inovace dat

Změna odvětví, narušení trhů nebo transformace produktů a služeb může trvat i roky. V rámci cloudové inovace dat je experimentování klíč k měření úspěšnosti. Budou transparentní sdílením metrik předpovědi, jako je procento pravděpodobnosti, počet neúspěšných experimentů a počet vyškolených modelů. Selhání se nashromáždí rychleji než úspěch. Tyto metriky můžou být discouraging a výkonný tým musí pochopit čas a investice potřebné k tomu, aby tyto metriky správně používaly.

Na druhé straně jsou některé pozitivní indikátory často spojené s učením řízeným daty: centralizaci heterogenních datových sad, příchozí přenos dat a democratization dat. I když se tým učí o zítřejším zákazníkovi, můžou se skutečné výsledky vytvářet ještě dnes. Podpora výukových metrik může zahrnovat:

- Počet dostupných modelů
- Počet spotřebovaných zdrojů dat partnerů
- Zařízení, která vytvářejí vstupní data
- Objem příchozích dat
- Typy dat

Ještě hodnotný metrika je počet řídicích panelů vytvořených z kombinovaných zdrojů dat. Toto číslo odráží aktuální stav obchodních procesů, které jsou ovlivněny novými zdroji dat. Díky opětovnému sdílení nových zdrojů dat může vaše firma využít data pomocí nástrojů pro vytváření sestav, jako je Power BI, k tvorbě přírůstkových přehledů a změně firemních změn.

## <a name="next-steps"></a>Další kroky

Po zarovnávání výukových metrik jste připraveni začít vyhodnotit [digitální nemovitosti](../digital-estate/index.md) na základě těchto metrik. Výsledkem bude [nevyřízené položky transformace nebo nevyřízené položky migrace](../migrate/migration-considerations/prerequisites/technical-complexity.md).

> [!div class="nextstepaction"]
> [Posouzení digitální nemovitosti](../digital-estate/index.md)
