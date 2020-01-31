---
title: Provozní dodržování předpisů – Správa a provoz v cloudu
description: Provozní dodržování předpisů – Správa a provoz v cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f83ec1ced367cca89349188932e608604dc3a005
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807746"
---
# <a name="operational-compliance-in-cloud-management"></a>Provozní dodržování předpisů ve správě cloudu

Provozní dodržování předpisů sestaví na disciplínách [inventarizace a viditelnosti](./inventory.md). Tato disciplína se zaměřuje na běžný postup správy cloudu a zaměřuje se na pravidelné kontroly telemetrie a úsilí o nápravu (proaktivní a reaktivní náprava). Tato disciplína je základem pro udržení rovnováhy mezi zabezpečením, zásadou správného řízení, výkonem a náklady.

## <a name="components-of-operations-compliance"></a>Součásti kompatibility operací

Udržování souladu s provozními závazky vyžaduje analýzu, automatizaci a lidskou nápravu. Účinné provozní dodržování předpisů vyžaduje konzistenci v několika kritických procesech:

- Konzistence prostředků
- Konzistence prostředí
- Konzistence konfigurace prostředků
- Aktualizovat konzistenci
- Automatizace oprav

### <a name="resource-consistency"></a>Konzistence prostředků

Nejefektivnějším krokem, který tým pro správu cloudu může vzít v úvahu k provoznímu dodržování předpisů, je vytvořit konzistenci v organizaci a označování prostředků. Když jsou prostředky konzistentně uspořádané a označené, budou se všechny ostatní provozní úlohy snadněji provádět. Podrobné pokyny týkající se konzistence prostředků najdete v tématu [fáze zásad správného řízení](../../govern/index.md) životního cyklu pro přijetí do cloudu. Konkrétně [úvodní články týkající se zásad správného řízení](../../govern/initial-foundation.md) ukazují, jak začít vyvíjet konzistenci prostředků.

### <a name="environment-consistency"></a>Konzistence prostředí

Vytváření konzistentních prostředí, neboli vykládacích zón, je dalším nejdůležitějším krokem k provoznímu dodržování předpisů. Pokud jsou zóny vykládku konzistentní a vynutily prostřednictvím automatizovaných nástrojů, je výrazně méně složitá pro diagnostiku a řešení provozních problémů. Podrobné pokyny týkající se konzistence prostředí najdete v [připravených fázích](../../ready/index.md) životního cyklu pro přijetí do cloudu. Cvičení v této fázi pomůžou vytvořit opakující se proces pro definování a vykonávání konzistentního přístupu ke kódu, který se bude zakládat za účelem vývoje cloudových prostředí.

### <a name="resource-configuration-consistency"></a>Konzistence konfigurace prostředků

Při sestavování na základě zásad správného řízení a připravenosti by měla Správa cloudu zahrnovat procesy pro průběžné monitorování a vyhodnocení požadavků na konzistenci prostředků. Jak se mění úlohy nebo se přijímají nové verze, je důležité, aby procesy správy cloudu vyhodnotily změny konfigurace, které nejsou snadno regulované prostřednictvím automatizace.

V případě zjištění nekonzistencí jsou některé z nich řešeny konzistencí v aktualizacích a jiné mohou být automaticky opraveny.

### <a name="update-consistency"></a>Aktualizovat konzistenci

Stabilita při přístupu může vést k většímu stabilnějšímu provozu. Ale v rámci procesů správy cloudu se vyžadují některé změny. Pro snížení přerušení a řízení nákladů jsou nezbytné zejména běžné opravy a změny výkonu.

Jednou z mnoha hodnot z vyspělé metodologie správy cloudu je zaměřit se na stabilizaci a kontrolu potřebného řízení.

Všechny základní hodnoty správy cloudu by měly zahrnovat způsob plánování, řízení a případného automatizace nezbytných aktualizací. Tyto aktualizace by měly obsahovat minimálně opravy, ale můžou zahrnovat i výkon, velikost a další aspekty aktualizace prostředků.

### <a name="remediation-automation"></a>Automatizace oprav

Kvůli lepšímu směrnému plánu pro správu cloudu můžou některé úlohy využívat automatizovanou nápravu. Pokud se často setkáte s problémy, které se nedají vyřešit prostřednictvím kódu nebo architektury, automatizace nápravy může přispět ke snížení zátěže správy cloudu a zvýšení spokojenosti uživatelů.

Mnohé z nich by tvrdí, že všechny problémy, které jsou dostatečně běžné pro automatizaci, by se měly vyřešit prostřednictvím rozlišení technického dluhu. Pokud je dlouhodobé rozlišení obezřetné, mělo by se jednat o výchozí možnost. Řada obchodních scénářů ale obtížně odůvodňuje velké investice do řešení technického dluhu. Pokud takové řešení není možné zdůvodnit, ale náprava je běžným a nákladným zatížením, jedná se o další nejlepší řešení automatizované nápravy.

## <a name="next-steps"></a>Další kroky

[Ochrana a obnovení](./protect.md) jsou další oblasti, které je třeba zvážit v rámci standardních hodnot správy cloudu.

> [!div class="nextstepaction"]
> [Ochrana a obnovení](./protect.md)
