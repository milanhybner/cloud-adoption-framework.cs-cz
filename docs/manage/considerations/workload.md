---
title: Provoz úloh – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Provoz úloh – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5f250362e93a81c6bb38ef11e8659484ef023182
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683737"
---
# <a name="workload-operations-in-cloud-management"></a>Provoz úloh ve správě cloudu

Některé úlohy jsou zásadní pro úspěch firmy. Pro tyto úlohy není standardní hodnota správy dostačující pro splnění požadovaných obchodních závazků ke správě cloudu. Operace platformy nemusí být ještě dostačující pro splnění obchodních závazků. Tato vysoce důležitá podmnožina úloh vyžaduje specializovaný fokus na způsob fungování úlohy a způsobu jejich podpor.

V důsledku toho může investice do operací zatížení vést k lepšímu výkonu, snížení rizika při přerušení provozu a rychlejšímu obnovení, když dojde k selhání systému. Tento článek vás provede přístupem k investicím do pokračujících operací těchto úloh s vysokou prioritou za účelem vylepšení obchodních závazků.

## <a name="when-to-invest-in-workload-operations"></a>Kdy investovat do provozu úloh

Princip Paretova (označovaný také jako pravidlo 80/20) uvádí, že 80% účinků přichází z 20% příčin. Když se portfolia IT můžou v průběhu času rozrůstat organicky, toto pravidlo se běžně zobrazuje na revizi portfolia IT. V závislosti na tom, jaký vliv vychází z investování, může být příčina odlišná, ale obecná zásada má hodnotu true:

- 80% systémových selhání by vedlo k tomu, že výsledkem je 20% běžných chyb nebo chyb.
- 80% obchodní hodnoty je v portfoliu pocházet z 20% úloh.
- 80% úsilí, které se má migrovat do cloudu, pochází z 20% přesouvaných úloh.
- 80% úsilí správy cloudu bude podporovat 20% incidentů služby nebo lístky pro řešení problémů.
- 80% dopadu na firmu z výpadku bude pocházet z 20% systémů, které mají vliv na výpadek.

Operace úlohy by se měly použít jenom v případě, že je strategie pro přijetí do cloudu, obchodní výsledky a provozní metrika velmi srozumitelná. Jedná se o paradigma posun z klasického zobrazení. Tradičně předpokládá, že všechny úlohy mají stejný stupeň podpory a vyžadují podobnou úroveň priority.

Před investicí do operací s hlubokým zatížením by IT i firmy měly pochopit obchodní odůvodnění a očekávání většího investování do správy cloudu.

## <a name="start-with-the-data"></a>Začněte s daty

Provozní operace začínají hlubokou znalostí výkonu úloh a požadavků na podporu. Než bude tým investovat do provozu, musí mít k dispozici bohatou datovou úlohu týkající se závislostí úloh, výkonu aplikace, diagnostiky databáze, telemetrie virtuálních počítačů a historie incidentů.

Tato data se týkají přehledů, které řídí rozhodování o provozu úloh.

## <a name="continued-observation"></a>Pokračování v pozorování

Počáteční data a průběžná telemetrie můžou přispět k formulování a testování teorie týkajících se výkonu úlohy. Ale probíhající operace úloh jsou zachovány v nepřetržitém a rozšířeném sledování výkonu úloh, s důrazem na výkon aplikací a dat.

### <a name="testing-automation"></a>Testování automatizace

Na úrovni aplikace jsou první požadavky na úlohy zatížení investice do hloubkového testování. Pro všechny aplikace, které jsou podporovány prostřednictvím operací s úlohou, by měl být vytvořen testovací plán, který bude pravidelně proveden pro zajištění funkčního a škálovatelného testování napříč aplikacemi.

Pravidelná telemetrie testů poskytne okamžité ověření různé hypotézy týkající se provozu úlohy. Vylepšení provozních a architektonických vzorů může být spuštěno a testováno, rozdíly v těchto výsledcích poskytují nejasnou analýzu dopadu, aby bylo možné pokračovat v investicích.

### <a name="understand-releases"></a>Pochopení verzí

Jasné porozumění cyklům vydávání verzí a kanálům vydávání je důležitým prvkem operací s úlohami.

Porozumění cyklům se může připravit na potenciální přerušení a umožní týmu proaktivně řešit všechny vydané verze, které by mohly způsobit nepříznivý vliv na operace. Díky tomuto porozumění můžou tým pro správu cloudu spolupracovat s týmy přijímání a průběžně zlepšovat kvalitu produktu a řešit chyby, které by mohly mít dopad na stabilitu.

Důležitější je, že porozumění kanálům vydaným verzím může významně zlepšit RTO úlohy. V mnoha scénářích je nejrychlejší a nejpřesnější cesta k obnovení aplikace, což je kanál vydání. U aplikačních vrstev, které se změní jenom v případě, že dojde k nové verzi, může být vhodnější investovat do optimalizace kanálu, než je obnovení aplikace z tradičních procesů zálohování.

I když kanál nasazení může být nejrychlejší cestou k obnovení, může to být také nejrychlejší cesta k nápravě. Pokud má aplikace rychlý, efektivní a spolehlivý kanál pro vydávání verzí, tým pro správu cloudu má možnost automatizovat nasazení na nového hostitele jako formu automatizované nápravy.

Může existovat spousta dalších rychlejších a efektivnějších mechanismů pro nápravu a obnovení. Pokud však použití existujícího kanálu může splňovat obchodní závazky a velká písmena na stávajících DevOpsch investicích, může to být životaschopná alternativa.

### <a name="clearly-communicate-changes-to-the-workload"></a>Jasně informovat o změnách zatížení

Změna na jakékoli zatížení je mezi největšími riziky při provozu úloh. Pro všechny úlohy na úrovni operací správy cloudu musí být tým pro správu cloudu úzce zarovnaný s týmy pro přijetí cloudu, aby pochopili změny přicházející z jednotlivých verzí. Tato investice v proaktivním porozumění bude mít přímý dopad na provozní stabilitu.

## <a name="improve-outcomes"></a>Zlepšení výsledků

Průběžné operace se obecně zdokonalují jedním ze dvou způsobů. Investice do dat a komunikace v rámci úlohy budou poskytovat návrhy na vylepšení jedné ze dvou cest: automatizovaná oprava nebo vylepšený návrh systému.

### <a name="technical-debt-resolution"></a>Řešení technického dluhu

Nejlepší provozní plány úloh budou stále vyžadovat nápravu. Vzhledem k tomu, že tým pro správu cloudu usiluje o připojení k pochopení vývoje a vydání, stejně tak by tým měl pravidelně sdílet požadavky na nápravu, aby se zajistilo, že technický dluh a chyby jsou nepřetržitou prioritou pro vývojové týmy.

### <a name="automate-remediation"></a>Automatizace odstraňování problémů

Použití principu Paretův, 80% negativního dopadu na chod firmy, který je nejspíš z 20% incidentů služeb. V případě, že se tyto incidenty nedají řešit v normálním vývojovém cyklu, investice do automatizace nápravy můžou významně snižovat provozní přerušení.

### <a name="improved-system-design"></a>Vylepšený návrh systému

V obou případech (rozlišení technického dluhu nebo automatizovaná náprava) jsou systémové chyby běžnou příčinou většiny výpadků systému. Dodržování několika principů návrhu může mít největší dopad na celkové operace úloh.

1. Škálovatelnost: schopnost systému zvládnout zvýšené zatížení.
2. Dostupnost: poměr doby, po kterou je systém funkční a funguje.
3. Odolnost: schopnost systému obnovit selhání a nadále fungovat.
4. Správa: provozní procesy, které udržují systém běžící v produkčním prostředí.
5. Zabezpečení: Ochrana aplikací a dat před hrozbami.

[Architektura architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) poskytuje přístup k vyhodnocení konkrétních úloh pro přistoupení k těmto pilířům ve snaze zlepšit celkové operace. Tyto pilíře lze použít pro operace platforem i pro operace s úlohou.

## <a name="next-steps"></a>Další kroky

S úplným porozuměním metodologii v rámci architektury pro přijetí do cloudu teď jste si vyrozuměli implementaci principů správy cloudu. Pokyny k provedení této metodologie v rámci vašeho provozního prostředí najdete na [úvodní stránce pro fázi správy](../index.md) životního cyklu přijetí.

> [!div class="nextstepaction"]
> [Použít tuto metodologii](../index.md)
