---
title: Provoz úloh ve správě cloudu
description: Seznamte se s přístupem k investicím do pokračujících operací těchto úloh s vysokou prioritou, abyste vylepšili lepší obchodní závazky.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 43399d4d84d824f03a7fb19da493223f3baea717
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341245"
---
# <a name="workload-operations-in-cloud-management"></a>Provoz úloh ve správě cloudu

Některé úlohy jsou zásadní pro úspěch firmy. Pro tyto úlohy není standardní hodnota správy dostačující pro splnění požadovaných obchodních závazků ke správě cloudu. Operace s platformou nemusí být pro splnění obchodních závazků ještě dostačující. Tato vysoce důležitá podmnožina úloh vyžaduje specializovaný fokus na způsob fungování úlohy a způsobu jejich podpor.

V důsledku toho může investice do operací zatížení vést k lepšímu výkonu, snížení rizika při přerušení provozu a rychlejšímu obnovení, když dojde k selhání systému. Tento článek popisuje přístup k investicím do pokračujících operací těchto úloh s vysokou prioritou za účelem vylepšení obchodních závazků.

## <a name="when-to-invest-in-workload-operations"></a>Kdy investovat do provozu úloh

_Princip Paretova_ (označovaný také jako _pravidlo 80/20_) uvádí, že 80 procento efektů vede od 20% příčin. Když se portfolia IT můžou v průběhu času rozrůstat organicky, toto pravidlo je často znázorněné na revizi portfolia IT. V závislosti na vlivu, který vyžaduje investici, může být příčina odlišná, ale obecná zásada má hodnotu true:

- 80 procent systémových selhání by vedlo k tomu, že je výsledkem 20 procent běžných chyb nebo chyb.
- 80 procentuální hodnota z firmy představuje 20% úloh v portfoliu.
- 80 procent úsilí o migraci do cloudu je z 20 procent přesouvaných úloh.
- 80 procent úsilí správy cloudu bude podporovat 20% incidentů služby nebo lístků s problémy.
- 80 procent z nepracovního dopadu z výpadku bude pocházet z 20% systémů, které by se při výpadku ovlivnily.

Operace úlohy by se měly použít jenom v případě, že je strategie pro přijetí do cloudu, obchodní výsledky a provozní metrika velmi srozumitelná. Jedná se o paradigma posun z klasického zobrazení. Tradičně předpokládá, že všechny úlohy mají stejný stupeň podpory a vyžadují podobnou úroveň priority.

Předtím, než investovaly do operací s hlubokým zatížením, by IT a firmy měly pochopit obchodní odůvodnění a očekávání většího investování do správy cloudu.

## <a name="start-with-the-data"></a>Začněte s daty

Provozní operace začínají hlubokou znalostí výkonu úloh a požadavků na podporu. Než tým investuje do provozu, musí mít rozsáhlá data o závislostech úloh, výkonu aplikace, diagnostikě databáze, telemetrie virtuálních počítačů a historii incidentů.

Tato data se týkají přehledů, které řídí rozhodování o provozu úloh.

## <a name="continued-observation"></a>Pokračování v pozorování

Počáteční data a průběžná telemetrie můžou přispět k formulování a testování teorie výkonu úloh. Ale probíhající operace úloh jsou zachovány v nepřetržitém a rozšířeném sledování výkonu úloh, s důrazem na výkon aplikací a dat.

### <a name="test-the-automation"></a>Testování automatizace

Na úrovni aplikace jsou první požadavky na úlohy zatížení investice do hloubkového testování. Pro všechny aplikace, které jsou podporovány prostřednictvím operací zatížení, by měl být vytvořen testovací plán, který bude pravidelně proveden pro zajištění funkčního a škálovatelného testování napříč aplikacemi.

Pravidelná telemetrie testů může poskytovat okamžité ověření různých hypotéz o provozu úlohy. Vylepšení provozních a architektonických vzorů se dá spouštět a testovat. Výsledné rozdíly poskytují nejasnou analýzu dopadu, aby bylo možné pokračovat v investicích.

### <a name="understand-releases"></a>Pochopení verzí

Jasné porozumění cyklům vydávání verzí a kanálům pro vydávání verzí je důležitým prvkem operací s úlohami.

Porozumění cyklům se může připravit na potenciální přerušení a umožní týmu proaktivně řešit všechny verze, které by mohly způsobit nepříznivý vliv na operace. Díky tomuto porozumění můžou tým pro správu cloudu spolupracovat s týmy přijímání a průběžně zlepšovat kvalitu produktu a řešit všechny chyby, které by mohly ovlivnit stabilitu.

Důležitější je, že porozumění kanálům vydání může významně zlepšit cíl bodu obnovení (RPO) úlohy. V mnoha scénářích je nejrychlejší a nejpřesnější cesta k obnovení aplikace kanál verze. Pro aplikační vrstvy, které se mění pouze v případě, že dojde k nové verzi, může být vhodnější investovat do optimalizace kanálu, než při obnovení aplikace z tradičních záložních procesů.

I když kanál nasazení může být nejrychlejší cestou k obnovení, může to být také nejrychlejší cesta k nápravě. Pokud má aplikace rychlý, efektivní a spolehlivý kanál pro vydávání verzí, tým pro správu cloudu má možnost automatizovat nasazení na nového hostitele jako formu automatizované nápravy.

K dispozici může být mnoho dalších rychlejších a efektivnějších mechanismů pro nápravu a obnovení. Pokud však použití existujícího kanálu může splňovat obchodní závazky a využít stávající investice do DevOps, může být existující kanál životaschopnou alternativou.

### <a name="clearly-communicate-changes-to-the-workload"></a>Jasně informovat o změnách zatížení

Změna na jakékoli zatížení je mezi největšími riziky při provozu úloh. Pro všechny úlohy na úrovni operací správy cloudu, které tým pro správu cloudu musí úzce zarovnávat s týmy pro přijetí cloudu a pochopit, jaké změny přicházejí v jednotlivých vydaných verzích. Tato investice v proaktivním porozumění budou mít přímý a kladný dopad na provozní stabilitu.

## <a name="improve-outcomes"></a>Zlepšení výsledků

Investice do dat a komunikace v rámci úlohy budou poskytovat návrhy na vylepšení probíhajících operací v jedné ze tří oblastí:

- Řešení technického dluhu
- Automatizovaná náprava
- Vylepšený návrh systému

### <a name="technical-debt-resolution"></a>Řešení technického dluhu

Nejlepší provozní plány úloh stále vyžadují nápravu. Vzhledem k tomu, že váš tým pro správu cloudu usiluje o připojení k porozumění vývoji a vydávání verzí, by měl tým podobně pravidelně sdílet požadavky na nápravu, aby se zajistilo, že technický dluh a chyby jsou nepřetržitou prioritou pro vývojové týmy.

### <a name="automated-remediation"></a>Automatizovaná náprava

Když použijete princip Paretova, můžeme říct, že 80 procent negativního dopadu na firmu je pravděpodobný z 20% incidentů služeb. V případě, že se tyto incidenty nedají řešit v normálním vývojovém cyklu, investice do automatizace nápravy můžou významně snižovat provozní přerušení.

### <a name="improved-system-design"></a>Vylepšený návrh systému

V případě řešení technického dluhu a automatizované nápravy jsou systémové chyby běžnou příčinou většiny výpadků systému. Můžete mít největší dopad na celkové operace úloh, a to díky několika principům návrhu:

- **Škálovatelnost:** Schopnost systému zpracovávat zvýšené zatížení.
- **Dostupnost:** Procento času, po který je systém funkční a funguje.
- **Odolnost:** Schopnost systému obnovit selhání a nadále fungovat.
- **Správa:** Provozní procesy, které udržují systém běžící v produkčním prostředí.
- **Zabezpečení:** Ochrana aplikací a dat před hrozbami.

V rámci vylepšení celkových operací poskytuje [Architektura architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) přístup k vyhodnocení konkrétních úloh pro dodržování těchto pilířů. Pilíře lze použít pro operace platforem i pro operace s úlohou.

## <a name="next-steps"></a>Další kroky

S úplným porozuměním metodologii v rámci architektury pro přijetí do cloudu teď jste si vyrozuměli implementaci principů správy cloudu. Pokyny k provedení této metodologie v rámci provozního prostředí najdete v tématu [Správa cloudu v rozhraní pro přijetí do cloudu v rámci](../index.md) životního cyklu přijetí.

> [!div class="nextstepaction"]
> [Použít tuto metodologii](../index.md)
