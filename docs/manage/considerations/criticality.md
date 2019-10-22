---
title: Kritická obchodní náročnost – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Kritická obchodní náročnost – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 290fcf7093f128c1415bbf960d65074d12490ae1
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683650"
---
# <a name="business-criticality-in-cloud-management"></a>Kritická obchodní náročnost v Cloud managementu

V každé firmě existuje malý počet úloh, které jsou příliš důležité k selhání. Pokud tyto úlohy vykonává výpadky nebo snížení výkonu, může být nepříznivý dopad na výnosy a ziskovost napříč celou společností. Tyto úlohy se považují za klíčové.

Na druhém konci spektra můžou některé úlohy jít v měsících v čase bez použití. Nízký výkon nebo výpadky pro tyto úlohy nejsou žádoucí, ale dopad je izolovaný a omezený.

Důležitým krokem pro jednotlivé úlohy portfolia IT je první krok ke vzájemným závazkům ke správě cloudu.
Následující obrázek popisuje společné zarovnání mezi rozsahem závažnosti, které je potřeba sledovat, a standardní závazky, které firma vytvořila.

![Závažnost a zarovnání na úrovni správy](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Škálování na kritické úrovni

Prvním krokem při vyrovnávání se závažností podniku je vytvoření škálování na kritické úrovni. Níže je ukázkový rozsah, který se dá použít jako odkaz, nebo šablonu pro vytvoření vlastního měřítka.

|Závažnost  |Obchodní zobrazení  |
|---------|---------|
|Kritická poslání|Má dopad na poslání společnosti a může si všimnout, že se jedná o výkazy zisků a ztrát v podniku.|
|Kritická jednotka|Ovlivňuje misi konkrétní obchodní jednotky a příkazy zisků a ztrát obchodních jednotek.|
|Vysoký|Nemusí bránit poslání, ale má dopad na procesy s vysokou důležitostí. V případě výpadků se dají měřit měřitelná ztráta.|
|Střední|Dopad na procesy je pravděpodobný. Ztráty jsou nízké nebo neměřitelné, ale jsou nejspíš poškození značky nebo nepřesné ztráty.|
|Nízký|Dopad na obchodní procesy je neměřitelný. Neexistují ani poškození značky nebo nepřesné ztráty. Je pravděpodobná i lokalizovaný dopad na jeden tým.|
|Nepodporované|Žádný obchodní vlastník, tým nebo proces spojený s touto úlohou nesmí opravňovat k investicím do průběžné správy úloh.|

Je běžné, že podniky budou zahrnovat další klasifikace kritické pro obor, vertikální nebo konkrétní obchodní procesy. Mezi další klasifikace patří:

- **Kritické pro dodržování předpisů:** V velmi regulovaných odvětvích můžou být některé úlohy kritické jako součást snahy zachovat požadavky na dodržování předpisů.
- **Kritické pro zabezpečení:** Některé úlohy nemusí být klíčové, ale výpadky můžou způsobit ztrátu dat nebo nezamýšlený přístup k chráněným informacím.
- **Kritické pro bezpečnost:** Pokud jsou zaměstnanci a zákazníci při výpadku ohroženi fyzickou nebo fyzickou bezpečností zaměstnanců a zákazníků, může být vhodné klasifikovat úlohy jako kritické pro bezpečnost.

## <a name="importance-of-accurate-criticality"></a>Důležitost přesné závažnosti

Později v tomto procesu bude tým Cloud managementu tuto klasifikaci používat k určení množství úsilí potřebného k dosažení zarovnané úrovně závažnosti. V místních prostředích se Operations Management často koupí centrálně a považuje se za nezbytnou obchodní režii, a to s malým množstvím dalších provozních nákladů. V cloudu se Správa provozu (stejně jako všechny cloudy) kupuje na základě jednotlivých assetů, jako je měsíční provozní náklady.

Vzhledem k tomu, že existují jasné a přímé náklady na správu provozu v cloudu, je důležité správně zarovnat náklady a žádoucí škály závažnosti.

## <a name="select-a-default-criticality"></a>Vyberte výchozí závažnost.

Počáteční revize všech úloh v portfoliu může být časově náročná. Aby se zajistilo, že toto úsilí nebude zablokovat širší cloudovou strategii, doporučujeme, aby IT a firmy souhlasily s výchozí závažností, která se má použít pro všechny úlohy.

Na základě výše uvedeného měřítka se doporučuje, aby se jako výchozí použila střední důležitost. Tím umožníte, aby tým cloudové strategie rychle identifikoval úlohy, které vyžadují vyšší úroveň závažnosti.

## <a name="using-the-template"></a>Použití šablony

Následující postup se týká čtenářů, kteří používají [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k naplánování správy cloudu.

1. Měřítko závažnosti se dá zaznamenat na kartě škálování v sešitu.
2. Všechny úlohy v "příkladu" nebo "čisté šabloně" by měly být aktualizovány tak, aby odrážely výchozí závažnost ve sloupci "závažnost".
3. Správné hodnoty by měly být zadané firmou, aby odrážely případné odchylky od výchozí závažnosti.

## <a name="next-steps"></a>Další kroky

Po definování závažnosti je nutné [Vypočítat a zaznamenat dopad](./impact.md)na chod firmy.

> [!div class="nextstepaction"]
> [Výpočet a zaznamenání dopadu na firmu](./impact.md)
