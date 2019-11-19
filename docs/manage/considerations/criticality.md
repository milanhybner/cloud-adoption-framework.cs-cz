---
title: 'Důležitá pro podnikání: cloudová správa a operace'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Důležitá pro podnikání: cloudová správa a operace'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 219c5b402c9cdc4b6214e8a5ed38b85ba7a2e203
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160349"
---
# <a name="business-criticality-in-cloud-management"></a>Kritická obchodní náročnost v Cloud managementu

V každé firmě existuje malý počet úloh, které jsou příliš důležité k selhání. Tyto úlohy se považují za klíčové. Pokud tyto úlohy vychází z výpadků nebo snížení výkonu, může být negativní dopad na výnosy a ziskovost v celé firmě.

Na druhém konci spektra můžou některé úlohy jít v měsících v čase bez použití. Nízký výkon nebo výpadky pro tyto úlohy nejsou žádoucí, ale dopad je izolovaný a omezený.

Zásadním krokem pro zajištění vzájemného závazku ke správě cloudu je porozumění závažnosti jednotlivých úloh v portfoliu IT.
Následující diagram znázorňuje běžné zarovnání mezi rozsahem závažnosti, které je potřeba sledovat, a standardní závazky, které společnost vytvořila.

![Závažnost a zarovnání na úrovni správy](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Škálování na kritické úrovni

Prvním krokem v jakémkoli úsilí při sbližování obchodních operací je vytvořit škálu závažnosti. Následující tabulka uvádí vzorový stupnici, která se má použít jako odkaz, nebo šablona pro vytváření vlastního škálování.

| Závažnost | Obchodní zobrazení |
| --------- | --------- |
| Klíčové |  Má vliv na poslání společnosti a může to znamenat, že se v podnikových příkazech a výsledovce projeví. |
| Jednotka – kritické | Má vliv na poslání konkrétní obchodní jednotky a jejich příkazů zisku a ztráty. |
| Vysoký | Nemusí bránit služební misi, ale má vliv na procesy s vysokou důležitostí. V případě výpadků se dají měřit měřitelná ztráta. |
| Střední | Dopad na procesy je pravděpodobný. Ztráty jsou nízké nebo neměřitelné, ale jsou nejspíš poškození značky nebo nepřesné ztráty. |
| Nízký | Dopad na obchodní procesy není měřitelný. Nehrozí ani poškození značky ani nepřesné ztráty. Lokalizovaný dopad na jeden tým je pravděpodobný. |
| Nepodporované | Žádný obchodní vlastník, tým nebo proces, který je přidružený k tomuto pracovnímu zatížení, nemůže v průběhu průběžné správy úloh zdůvodnit žádnou investici. |

Je běžné, že podniky budou zahrnovat další klasifikace pro kritické účely, které jsou specifické pro jejich obor, vertikální nebo konkrétní obchodní procesy. Mezi další klasifikace patří:

- **Kritické pro dodržování předpisů:** V velmi regulovaných odvětvích můžou být některé úlohy kritické jako součást snahy zachovat požadavky na dodržování předpisů.
- **Kritické pro zabezpečení:** Některé úlohy nemusí být klíčové, ale výpadky můžou způsobit ztrátu dat nebo nezamýšlený přístup k chráněným informacím.
- **Kritické pro bezpečnost:** V případě, že je život nebo fyzická bezpečnost zaměstnanců a zákazníků ohrožena v případě výpadku, je možné klasifikovat úlohy jako kritické pro bezpečnost.

## <a name="importance-of-accurate-criticality"></a>Důležitost přesné závažnosti

V budoucnu v rámci procesu přijetí do cloudu bude tým Cloud managementu tuto klasifikaci používat k určení množství úsilí potřebného k dosažení zarovnané úrovně závažnosti. V místních prostředích se Správa provozu často kupuje a považuje se za nezbytnou obchodní režii, a to s malým nebo žádným dalším provozním nákladům. V cloudu se Správa provozu (stejně jako všechny cloudy) kupuje na základě jednotlivých assetů, jako je měsíční provozní náklady.

Vzhledem k tomu, že existují jasné a přímé náklady na správu provozu v cloudu, je důležité správně zarovnat náklady a žádoucí škály závažnosti.

## <a name="select-a-default-criticality"></a>Vyberte výchozí závažnost.

Počáteční revize každého pracovního postupu v portfoliu může být časově náročná. Aby se zajistilo, že toto úsilí neblokuje vaše širší cloudovou strategii, doporučujeme, aby vaši týmy souhlasily s výchozí závažností, která se má použít pro všechny úlohy.

V závislosti na předchozí tabulce pro kritické závažnost doporučujeme, abyste jako výchozí nepřijali *střední* důležitost. Tím umožníte týmu vaší cloudové strategie rychle identifikovat úlohy, které vyžadují vyšší úroveň závažnosti.

## <a name="use-the-template"></a>Použití šablony

Následující postup platí, pokud pro plánování správy cloudu používáte [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) .

1. Poznamenejte si měřítko závažnosti na kartě **škálování** v sešitu.
2. Aktualizujte každou úlohu v *příkladu* nebo *čistou šablonu* tak, aby odrážela výchozí závažnost ve sloupci *kritická* náročnost.
3. Firma by měla zadat správné hodnoty, aby odrážela jakékoli odchylky od výchozí závažnosti.

## <a name="next-steps"></a>Další kroky

Poté, co tým definuje kritickou obchodní náročnost, můžete [Vypočítat a zaznamenat dopad](./impact.md)na chod firmy.

> [!div class="nextstepaction"]
> [Výpočet a zaznamenání dopadu na firmu](./impact.md)
