---
title: Provozní dodržování předpisů – Správa a provoz v cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Provozní dodržování předpisů – Správa a provoz v cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: bb6e4584da87d992f85b6ce90e21081c9c19d7c3
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682547"
---
# <a name="operational-compliance-in-cloud-management"></a>Provozní dodržování předpisů ve správě cloudu

Provozní dodržování předpisů sestaví na principu [inventarizace a viditelnosti](./inventory.md)jako první napadnutelný krok správy cloudu. Tato disciplína se zaměřuje na pravidelné kontroly telemetrie a úsilí o nápravu (proaktivní a reaktivní náprava). Tato disciplína je základem pro udržení rovnováhy mezi zabezpečením, zásadou správného řízení, výkonem a náklady.

## <a name="components-of-operations-compliance"></a>Součásti kompatibility operací

Zachování dodržování předpisů pro provozní závazky vyžaduje analýzu, automatizaci a lidskou nápravu. Účinné provozní dodržování předpisů vyžaduje konzistenci v několika kritických procesech:

1. Konzistence prostředků
2. Konzistence prostředí
3. Konzistence konfigurace prostředků
4. Aktualizovat konzistenci
5. Automatizace oprav

### <a name="resource-consistency"></a>Konzistence prostředků

Nejúčinnější krok, který tým pro správu cloudu může využít k zajištění konzistence v organizaci a označování prostředků. Když jsou prostředky konzistentně uspořádané a označené, budou se všechny ostatní provozní úlohy snadněji provádět. Podrobné pokyny týkající se konzistence prostředků najdete v tématu [fáze zásad správného řízení](../../govern/index.md) životního cyklu pro přijetí do cloudu. Konkrétně [základní články zásad správného řízení](../../govern/initial-foundation.md) ukazují příklady způsobů, jak začít vyvíjet konzistenci prostředků.

### <a name="environment-consistency"></a>Konzistence prostředí

Konzistentní prostředí, neboli cílové zóny, je nejdůležitějším krokem k provoznímu dodržování předpisů. Pokud jsou zóny vykládku konzistentní a vynutily prostřednictvím automatizovaných nástrojů, je výrazně méně složitá pro diagnostiku a řešení provozních problémů. Podrobné pokyny týkající se konzistence prostředí najdete v [připravených fázích](../../ready/index.md) životního cyklu pro přijetí do cloudu. Cvičení v této fázi stanovují opakující se proces pro definování a vykonávání konzistentního přístupu ke kódu, který je první pro vývoj cloudových prostředí.

### <a name="resource-configuration-consistency"></a>Konzistence konfigurace prostředků

V rámci přístupů na zásady správného řízení a připravenosti by Správa cloudu měla zahrnovat procesy pro průběžné monitorování a vyhodnocení požadavků na konzistenci prostředků. Jak se mění úlohy nebo se přijímají nové verze, je důležité, aby procesy správy cloudu vyhodnotily změny konfigurace, které nejsou snadno regulované prostřednictvím automatizovaných prostředků.

Pokud jsou zjištěny nekonzistence, některé jsou řešeny konzistencí v aktualizacích a jiné mohou být automaticky opraveny.

### <a name="update-consistency"></a>Aktualizovat konzistenci

Stabilita může vést k stabilním operacím. V rámci procesů správy cloudu se ale vyžadují některé změny. Pro snížení přerušení a řízení nákladů jsou nezbytné zejména běžné opravy a změny výkonu.

Jednou z mnoha hodnot z vyspělé metodiky správy cloudu je stabilizace a řízení nezbytné změny.

Všechny základní hodnoty správy cloudu by měly zahrnovat způsob plánování, řízení a případného automatizace nezbytných aktualizací. Tyto aktualizace by měly obsahovat minimálně opravy, ale můžou zahrnovat i výkon, velikost a další aspekty aktualizace prostředků.

### <a name="remediation-automation"></a>Automatizace oprav

Kvůli lepšímu směrnému plánu pro správu cloudu můžou některé úlohy využívat automatizovanou nápravu. Pokud se v úloze často setkáte s problémy, které se nedají vyřešit prostřednictvím změny kódu nebo architektury, automatizace nápravy může snížit zatížení cloudového řízení a zvýšit spokojenost uživatelů.

Mnohé z nich by tvrdí, že všechny problémy, které jsou pro automatizaci dostatečně časté, by se měly vyřešit prostřednictvím rozlišení technického dluhu. Pokud je dlouhodobé rozlišení obezřetné, mělo by se jednat o výchozí možnost. Existuje však několik obchodních scénářů, které usnadňují zakládání velkých investic do řešení technického dluhu. Pokud se rozlišení technického dluhu nedá zdůvodnit, ale náprava je běžným a nákladným zatížením, jedná se o další nejlepší řešení.

## <a name="next-steps"></a>Další kroky

[Ochrana a obnovení](./protect.md) jsou další oblasti, které je třeba zvážit v rámci standardních hodnot správy cloudu.

> [!div class="nextstepaction"]
> [Ochrana a obnovení](./protect.md)
