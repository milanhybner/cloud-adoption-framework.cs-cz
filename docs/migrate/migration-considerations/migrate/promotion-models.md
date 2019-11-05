---
title: 'Propagační modely: jeden krok, připravený nebo let'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pochopení dopadu povýšení na migrační aktivity
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 690c871ab18bef96a5a1738de90a216ca5b8df90
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564623"
---
# <a name="promotion-models-single-step-staged-or-flight"></a>Propagační modely: jeden krok, připravený nebo let

O migraci úloh se často diskutuje jako o jediné aktivitě. Ve skutečnosti je to kolekce menších aktivit usnadňujících přesun digitálního aktiva do cloudu. Jednou z posledních aktivit v rámci migrace je povýšení aktiva do produkčního prostředí. Povýšení je bod, ve kterém se produkční systém mění pro koncové uživatele. Může to být často tak jednoduché jako změna síťového směrování a přesměrování koncových uživatelů na nové produkční aktivum. Povýšení je také bod, ve kterém se provoz IT nebo cloudu mění zaměření procesů provozní správy z předchozího produkčního systému na nové produkční systémy.

Existuje několik modelů povýšení. Tento článek popisuje tři nejběžněji používané při migracích do cloudu. Volba modelu povýšení mění aktivity, které se objevují v rámci procesů migrace a optimalizace. O modelu povýšení jako takovém by se mělo rozhodnout v rané fázi vydání verze.

## <a name="impact-of-promotion-model-on-migrate-and-optimize-activities"></a>Dopad modelu povýšení na aktivity migrace a optimalizace

V každém z následujících modelů povýšení vybraný nástroj pro migraci replikuje a připraví aktiva, která tvoří úlohu. Po rozfázování každý model pracuje s aktivem trochu jinak.

- **Jednokrokové povýšení.** V *jednokrokovém* modelu povýšení se proces rozfázování zdvojí jako proces povýšení. Po přípravě všech aktiv se provoz koncových uživatelů přesměruje na produkční prostředí. V takovém případě je povýšení součástí procesu migrace. Toto je nejrychlejší model migrace. Tento přístup ale ztěžuje integraci robustních testovacích nebo optimalizačních aktivit. Dále tento typ modelu předpokládá, že má migrační tým přístup k přípravnému a provoznímu prostředí, což v některých prostředích ohrožuje oddělení požadavků na povinnosti.
  > [!NOTE]
  >Obsah tohoto webu obsahuje aktivitu povýšení jako součást procesu optimalizace. V jednokrokovém modelu k povýšení dojde během procesu migrace. Při použití tohoto modelu by se role a odpovědnosti měly aktualizovat, aby tuto skutečnost odrážely.
- **S fázemi.** V modelu povýšení *s fázemi* se úloha považuje za migrovanou, když je připravená, ale ještě není povýšená. Předtím povýšením migrované úlohy podstupují řadu testů výkonu, obchodních testů a změn optimalizace. Pak se povýší v budoucím termínu ve spojitosti s plánem obchodního testování. Tento přístup zlepšuje rovnováhu mezi náklady a výkonem a zároveň usnadňuje získání obchodního ověřování.
- **Nasazení testovací verze.** Model povýšení *nasazením testovací verze* kombinuje jednokrokový model a model s fázemi. V modelu nasazením testovací verze se aktiva považují za produkční po umístění do přípravy. Po zhuštěném období automatizovaného testování se produkční provoz směruje na úlohu. Jedná se ale o podmnožinu provozu. Tento provoz slouží jako první nasazení testovací verze produkce a testování. Pokud úloha z budoucího a výkonového hlediska funguje, migruje se další provoz. Po přesunu veškerého produkčního provozu na nová aktiva se úloha považuje za plně povýšenou.

Vybraný model povýšení ovlivňuje pořadí prováděných aktivit. Má také vliv na role a zodpovědnosti v týmu přechodu na cloud. Může dokonce ovlivnit složení sprintu nebo více sprintů.

## <a name="single-step-promotion"></a>Jednokrokové povýšení

Tento model využívá nástroje pro automatizaci migrace k replikaci, přípravě a povýšení aktiv. Aktiva se replikují do obsaženého prostředí přípravy, které řídí nástroj pro migraci. Po dokončení replikace všech aktiv může nástroj spustit automatizovaný proces povýšení aktiv do vybraného předplatného v jednom kroku. Během přípravy nástroj pokračuje v replikaci aktiva a minimalizuje ztrátu dat mezi těmito dvěma prostředími. Po povýšení aktiva je spojení mezi zdrojovým systémem a replikovaným systémem přerušeno. Pokud s tímto přístupem dojde k dalším změnám v původním zdrojovém systému, tyto změny se ztratí.

**Výhody.** Mezi výhody tohoto přístupu patří:

- Tento model přináší menší změnu v cílových systémech.
- Průběžná replikace minimalizuje ztrátu dat.
- Pokud proces přípravy neproběhne úspěšně, lze ho rychle odstranit a opakovat.
- Testy replikace a opakované přípravy umožňují přírůstkový proces skriptování a testování.

**Nevýhody.** Mezi nevýhody tohoto přístupu patří:

- Aktiva připravená v sandboxu izolovaném nástroji neumožňují modely komplexního testování.
- Během replikace spotřebovává nástroj pro migraci šířku pásma v místním datovém centru. Příprava velkého objemu aktiv po delší dobu má exponenciální dopad na dostupnou šířku pásma, ubližuje procesu migrace a potenciálně ovlivňuje výkon produkčních úloh v místním prostředí.

## <a name="staged-promotion"></a>Povýšení s fázemi

V tomto modelu se pro účely omezeného testování používá přípravný sandbox spravovaný nástrojem pro migraci. Replikovaná aktiva se pak nasadí do cloudového prostředí, které slouží jako rozšířené přípravné prostředí. Migrovaná aktiva běží v cloudu, zatímco další aktiva se replikují, připravují a migrují. Když se úplné úlohy stanou dostupnými, dojde k zahájení rozsáhlejšího testování. Po migraci všech aktiv přidružených k předplatnému se předplatné a všechny hostované úlohy převýší do produkčního prostředí. V tomto scénáři se během procesu povýšení úlohy nemění. Místo toho se změny týkají spíše síťové vrstvy a vrstvy identit, směrování uživatelů do nového prostředí a odvolání přístupu týmu přechodu na cloud.

**Výhody.** Mezi výhody tohoto přístupu patří:

- Tento model poskytuje možnosti přesnějšího obchodního testování.
- Úlohy je možné studovat podrobněji, aby se lépe optimalizoval výkon a náklady na aktiva.
- Větší počet aktiv je možné replikovat v rámci podobných omezení doby a šířky pásma.

**Nevýhody.** Mezi nevýhody tohoto přístupu patří:

- Zvolený nástroj pro migraci nemůže podporovat probíhající replikaci po migraci.
- K synchronizaci datových platforem během časového rámce přípravy se vyžaduje sekundární způsob replikace dat.

## <a name="flight-promotion"></a>Povýšení nasazením testovací verze

Tento model je podobný modelu povýšení s fázemi. Existuje však jeden zásadní rozdíl. Když je předplatné připravené k povýšení, směrování koncových uživatelů probíhá ve fázích nebo v nasazeních testovací verze. U každého nasazení testovací verze se přesměrují na produkční systémy další uživatelé.

**Výhody.** Mezi výhody tohoto přístupu patří:

- Tento model snižuje rizika spojená s velkou aktivitou migrace nebo povýšení. Chyby v migrovaném řešení je možné identifikovat s menším dopadem na obchodní procesy.
- Umožňuje monitorování požadavků na výkon úloh v cloudovém prostředí po delší dobu a zvyšuje přesnost rozhodnutí o nastavení velikosti aktiv.
- Větší počet aktiv je možné replikovat v rámci podobných omezení doby a šířky pásma.

**Nevýhody.** Mezi nevýhody tohoto přístupu patří:

- Zvolený nástroj pro migraci nemůže podporovat probíhající replikaci po migraci.
- K synchronizaci datových platforem během časového rámce přípravy se vyžaduje sekundární způsob replikace dat.

## <a name="next-steps"></a>Další kroky

Po definování a přijetí modelu povýšení týmem přechodu na cloud může začít [náprava aktiv](./remediate.md).

> [!div class="nextstepaction"]
> [Náprava aktiv před migrací](./remediate.md)
