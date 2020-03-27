---
title: 'Standardní zásady správného řízení podniku: vysvětlení osvědčených postupů'
description: Rozhraní pro přijetí v cloudu pro Azure umožňuje vytvořit minimální životaschopný produkt (MVP) pro zásady správného řízení, které odráží osvědčené postupy pro standard Enterprise.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1d0c6d30e7bba864fb52b14fb82e1e88231e9a3c
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80357039"
---
# <a name="standard-enterprise-governance-guide-best-practices-explained"></a>Standardní příručka pro zásady správného řízení podniku: vysvětlené osvědčené postupy

Příručka zásad správného řízení začíná sadou počátečních [podnikových zásad](./initial-corporate-policy.md). Tyto zásady se používají ke zřízení MVP pro řízení správného řízení, který odráží [osvědčené postupy](./index.md).

V tomto článku probereme strategie vysoké úrovně, které jsou potřeba k vytvoření MVP pro řízení. Základem MVP v rámci zásad správného řízení je obor [akcelerace nasazení](../../deployment-acceleration/index.md) . Nástroje a vzory použité v této fázi budou umožňovat přírůstková vylepšení nutná k rozšíření zásad správného řízení v budoucnu.

## <a name="governance-mvp-initial-governance-foundation"></a>MVP pro zásady správného řízení (počáteční zásady správného řízení)

Rychlé přijetí zásad správného řízení a podnikových zásad se může dosáhnout několika jednoduchými zásadami a pomocí cloudových nástrojů zásad správného řízení. Toto jsou první tři disciplíny pro přístup k jakémukoli procesu zásad správného řízení. Jednotlivé disciplíny budou popsány dále v tomto článku.

Tento článek pojednává o strategiích vysoké úrovně za směrným plánem identity, základním hodnotám zabezpečení a akceleraci nasazení, které jsou potřeba k vytvoření MVP MVP, který bude sloužit jako základ pro všechna přijetí.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Proces implementace

Implementace MVP v rámci zásad správného řízení má závislosti na identitě, zabezpečení a síti. Až budou závislosti vyřešeny, tým zásad správného řízení pro Cloud určí několik aspektů zásad správného řízení. Rozhodnutí od týmu zásad správného řízení cloudu a od pomocných týmů budou implementována prostřednictvím jediného balíčku prostředků vynucení.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-mvp-implementation-flow.png)

Tuto implementaci je také možné popsat pomocí jednoduchého kontrolního seznamu:

1. Vyžádá si rozhodnutí týkající se základních závislostí: identita, sítě, monitorování a šifrování.
2. Určete vzor, který se použije při vynucování podnikových zásad.
3. Určete vhodné vzory zásad správného řízení pro konzistenci prostředků, označování prostředků a obory protokolování a generování sestav.
4. Implementujte nástroje zásad správného řízení zarovnané na vybraný model vynucení zásad, abyste mohli použít závislá rozhodnutí a rozhodnutí o zásadách správného řízení.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Použití vzorů definovaných zásadami správného řízení

Tým zásad správného řízení cloudu zodpovídá za následující rozhodnutí a implementace. Řada vyžaduje vstupy z jiných týmů, ale tým zásad správného řízení cloudu může vlastnit jak rozhodnutí, tak i implementaci. Následující části popisují rozhodnutí učiněná v tomto případu použití a podrobnosti o každém rozhodnutí.

### <a name="subscription-design"></a>Návrh předplatného

Rozhodnutí o tom, jaký návrh předplatných se má použít, určuje, jak se předplatná Azure získají strukturovaná a jak se skupiny pro správu Azure budou používat k efektivní správě přístupu, zásad a dodržování předpisů pro toto předplatné. V tomto mluveném komentáři tým zásad správného řízení navázal předplatné pro produkční a nevýrobní úlohy, které jsou v [produkčním prostředí a](../../../ready/azure-best-practices/initial-subscriptions.md) neproduktivní.

- Oddělení se pravděpodobně nevyžadují při aktuálním výběru. Očekává se, že nasazení budou omezená v rámci jedné fakturační jednotky. Ve fázi přijetí se nemusí ani stát smlouvou Enterprise k centralizaci fakturace. Je možné, že tato úroveň přijetí je spravovaná jedním předplatným Azure s průběžnými platbami.
- Bez ohledu na používání portálu EA nebo existence smlouvy Enterprise by se model předplatného měl ještě definovat a souhlasit s tím, aby se minimalizovala Správa přeslyšela nad rámec pouhého fakturace.
- Společná konvence pojmenování by se měla schválit jako součást návrhu předplatného, a to na základě předchozích dvou bodů.

### <a name="resource-consistency"></a>Konzistence prostředků

Rozhodnutí o konzistenci prostředků určují nástroje, procesy a úsilí potřebné k zajištění konzistentního nasazení, konfigurace a správy prostředků Azure v rámci předplatného. V tomto mluveném komentáři je **[konzistence nasazení](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** zvolena jako vzor konzistence primárního prostředku.

- Skupiny prostředků se vytvářejí pro aplikace využívající přístup k životnímu cyklu. Všechny položky, které se vytvářejí, udržují a vyřazené dohromady, by měly být umístěné v jedné skupině prostředků. Další informace o skupinách prostředků najdete [tady](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy by se měla použít pro všechna předplatná z přidružené skupiny pro správu.
- V rámci procesu nasazení by měly být šablony konzistence prostředků Azure pro skupinu prostředků uložené ve správě zdrojového kódu.
- Každá skupina prostředků je přidružená ke konkrétnímu pracovnímu vytížení nebo aplikaci na základě výše popsaného přístupu k životnímu cyklu.
- Skupiny pro správu Azure umožňují aktualizovat návrhy zásad správného řízení, protože podniková zásada je vyspělá.
- Rozsáhlá implementace Azure Policy může překročit časové závazky týmu a v tuto chvíli nemusí poskytovat skvělou hodnotu. Pro každou skupinu pro správu byste ale měli vytvořit a použít jednoduchou výchozí zásadu, která vynutila malý počet aktuálních příkazů zásad správného řízení cloudu. Tyto zásady definují implementaci konkrétních požadavků zásad správného řízení. Tyto implementace je pak možné použít napříč všemi nasazenými prostředky.

>[!IMPORTANT]
>Všechny prostředky ve skupině prostředků už nesdílejí stejný životní cyklus, měli byste je přesunout do jiné skupiny prostředků. Mezi příklady patří běžné databáze a síťové komponenty. I když můžou vycházet z vyvíjené aplikace, můžou sloužit i jiným účelům, a proto by měly existovat i v jiných skupinách prostředků.

### <a name="resource-tagging"></a>Označování prostředků

Rozhodnutí označování prostředků určují, jak se metadata v rámci předplatného aplikují na prostředky Azure za účelem podpory operací, správy a účetní účely. V tomto mluveném komentáři byl vzor **[klasifikace](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** zvolen jako výchozí model pro označování prostředků.

- Nasazené prostředky by měly být označeny:
  - Klasifikace dat
  - Závažnost
  - SLA
  - Prostředí
- Tyto čtyři hodnoty budou řídit řízení, provoz a rozhodnutí o zabezpečení.
- Pokud je tato příručka zásad správného řízení implementovaná pro obchodní jednotku nebo tým v rámci většího podniku, měla by označení obsahovat také metadata fakturační jednotky.

### <a name="logging-and-reporting"></a>Protokolování a vytváření sestav

Rozhodnutí týkající se protokolování a vytváření sestav určují, jak jsou strukturovaná data protokolu úložiště a jak jsou strukturované nástroje pro monitorování a vytváření sestav, které udržují pracovníky IT informace o provozním stavu. V tomto mluveném komentáři navrhneme [model nativního cloudu](../../../decision-guides/logging-and-reporting/index.md#cloud-native)* * pro protokolování a vytváření sestav.

## <a name="incremental-improvement-of-governance-processes"></a>Přírůstkové zlepšování procesů zásad správného řízení

Jako změny zásad správného řízení se některé příkazy zásad nedají nebo nemají řídit automatizovanými nástroji. Další zásady budou mít za následek úsilí bezpečnostního týmu IT a místního týmu správy identit v průběhu času. Aby bylo možné spravovat nová rizika při jejich vzniku, bude tým zásad správného řízení pro Cloud dohlížet na následující procesy.

**Akcelerace přijetí:** Tým zásad správného řízení cloudu kontroluje skripty pro nasazení napříč několika týmy. Uchovávají sadu skriptů, které slouží jako šablony nasazení. Tyto šablony používá týmy pro přijetí v cloudu a DevOps pro rychlejší definování nasazení. Každý z těchto skriptů obsahuje nezbytné požadavky pro vymáhání sady zásad správného řízení bez dalšího úsilí od techniků při přijímání cloudu. Jako curators těchto skriptů může tým zásad správného řízení cloudu rychleji implementovat změny zásad. V důsledku obřízení skriptu se tým zásad správného řízení cloudu zobrazuje jako zdroj akcelerace přijetí. Tím se vytvoří konzistence mezi nasazeními bez striktního vynucení dodržování.

**Školení pro inženýry:** Tým zásad správného řízení cloudu nabízí bimonthly školicích cvičení a vytvořil dvě videa pro inženýry. Tyto materiály umožňují technikům rychle zjistit jazykovou verzi zásad správného řízení a to, jak se probíhají během nasazení. Tým přidává školicí materiály, které ukazují rozdíl mezi nasazeními v produkčním prostředí a neprodukčním prostředí, aby technici pochopili, jak budou nové zásady ovlivněny přijetí. Tím se vytvoří konzistence mezi nasazeními bez striktního vynucení dodržování.

**Plánování nasazení:** Před nasazením jakýchkoli prostředků, které obsahují chráněná data, tým zásad správného řízení pro Cloud zkontroluje skripty nasazení, aby ověřili zarovnání zásad správného řízení. Stávající týmy s dřív schváleným nasazením budou auditovány pomocí programových nástrojů.

**Měsíční audit a vytváření sestav:** Každý měsíc tým zásad správného řízení cloudu spustí audit všech nasazení cloudu, aby ověřil pokračování v sestavování zásad. Když se zjistí odchylky, budou se zdokumentovat a sdílet s týmy pro přijetí v cloudu. Pokud vynucení nehrozí při výpadku nebo úniku dat, zásady se automaticky vynucuje. Na konci auditu zkompiluje tým zásad správného řízení Cloud zprávu pro tým cloudové strategie a každý tým pro přijetí cloudu, aby komunikoval celkové dodržování zásad. Sestava je také uložená pro účely auditování a právní účely.

**Kontrola čtvrtletních zásad:** V každém čtvrtletí si tým zásad správného řízení cloudu a tým cloudových strategií zkontroluje výsledky auditu a navrhne změny firemních zásad. Mnohé z těchto návrhů jsou výsledkem průběžných vylepšení a pozorování vzorců používání. Schválené změny zásad jsou integrovány do nástrojů zásad správného řízení během dalších cyklů auditu.

## <a name="alternative-patterns"></a>Alternativní vzory

Pokud se některý ze vzorů vybraných v této příručce zásad správného řízení Nezarovnává s požadavky čtenáře, jsou k dispozici alternativy ke každému vzoru:

- [Vzory šifrování](../../../decision-guides/encryption/index.md)
- [Vzory identity](../../../decision-guides/identity/index.md)
- [Vzorce protokolování a vytváření sestav](../../../decision-guides/logging-and-reporting/index.md)
- [Vzory vynucování zásad](../../../decision-guides/policy-enforcement/index.md)
- [Vzory konzistence prostředků](../../../decision-guides/resource-consistency/index.md)
- [Vzory označování prostředků](../../../decision-guides/resource-tagging/index.md)
- [Vzory softwarově definovaných sítí](../../../decision-guides/software-defined-network/index.md)
- [Vzory návrhu předplatného](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Další kroky

Po implementaci této příručky se každý tým pro přijetí v cloudu může obrátit na zásady správného řízení zvuku. Ve stejnou chvíli tým zásad správného řízení pro Cloud bude fungovat tak, aby průběžně aktualizoval podnikové zásady a obory řízení.

Dva týmy použijí indikátory tolerance k identifikaci další sady vylepšení potřebných pro pokračování v podpoře přijetí do cloudu. Pro fiktivní společnost v tomto průvodci je dalším krokem zlepšení standardních hodnot zabezpečení pro podporu přesunu chráněných dat do cloudu.

> [!div class="nextstepaction"]
> [Zlepšení pravidla směrného plánu zabezpečení](./security-baseline-improvement.md)
