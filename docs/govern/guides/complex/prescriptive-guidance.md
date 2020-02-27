---
title: 'Komplexní řízení podniku: vysvětlené osvědčené postupy'
description: Rozhraní pro přijetí v cloudu pro Azure umožňuje vytvořit minimální životaschopný produkt (MVP) pro zásady správného řízení, které odráží osvědčené postupy pro komplexní firmu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 74f81e139e7eacc7445321592eab4027a40a8c56
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709205"
---
# <a name="governance-guide-for-complex-enterprises-best-practices-explained"></a>Příručka zásad správného řízení pro komplexní podniky: vysvětlení osvědčených postupů

Příručka zásad správného řízení začíná sadou počátečních [podnikových zásad](./initial-corporate-policy.md). Tyto zásady se používají k vytvoření minimálního životaschopného produktu (MVP) pro zásady správného řízení, které odráží [osvědčené postupy](./index.md).

V tomto článku probereme strategie vysoké úrovně, které jsou potřeba k vytvoření MVP pro řízení. Základem MVP v rámci zásad správného řízení je obor [akcelerace nasazení](../../deployment-acceleration/index.md) . Nástroje a vzory použité v této fázi budou umožňovat přírůstková vylepšení nutná k rozšíření zásad správného řízení v budoucnu.

## <a name="governance-mvp-initial-governance-foundation"></a>MVP pro zásady správného řízení (počáteční zásady správného řízení)

Rychlé přijetí zásad správného řízení a podnikových zásad se může dosáhnout několika jednoduchými zásadami a pomocí cloudových nástrojů zásad správného řízení. Jedná se o první ze tří oborů řízení přístupu k přístupu v jakémkoli procesu zásad správného řízení. Jednotlivé disciplíny se v tomto článku vysvětlí podrobněji.

Tento článek pojednává o strategiích vysoké úrovně za směrným plánem identity, základním hodnotám zabezpečení a akceleraci nasazení, které jsou potřeba k vytvoření MVP MVP, který bude sloužit jako základ pro všechna přijetí.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Proces implementace

Implementace MVP v rámci zásad správného řízení má závislosti na identitě, zabezpečení a síti. Až budou závislosti vyřešeny, tým zásad správného řízení pro Cloud určí několik aspektů zásad správného řízení. Rozhodnutí od týmu zásad správného řízení cloudu a od pomocných týmů budou implementována prostřednictvím jediného balíčku prostředků vynucení.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/govern/governance-mvp-implementation-flow.png)

Tuto implementaci je také možné popsat pomocí jednoduchého kontrolního seznamu:

1. Vyžádá si rozhodnutí týkající se základních závislostí: identita, síť a šifrování.
1. Určete vzor, který se použije při vynucování podnikových zásad.
1. Určete vhodné vzory zásad správného řízení pro konzistenci prostředků, označování prostředků a obory protokolování a generování sestav.
1. Implementujte nástroje zásad správného řízení zarovnané na vybraný model vynucení zásad, abyste mohli použít závislá rozhodnutí a rozhodnutí o zásadách správného řízení.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Použití vzorů definovaných zásadami správného řízení

Tým zásad správného řízení cloudu bude zodpovědný za následující rozhodnutí a implementace. Mnohé budou vyžadovat vstupy z jiných týmů, ale tým zásad správného řízení cloudu bude nejspíš vlastnit rozhodnutí i implementaci. Následující části popisují rozhodnutí učiněná v tomto případu použití a podrobnosti o každém rozhodnutí.

### <a name="subscription-design"></a>Návrh předplatného

Rozhodnutí o tom, jaký návrh předplatných se má použít, určuje, jak se předplatná Azure získají strukturovaná a jak se skupiny pro správu Azure budou používat k efektivní správě přístupu, zásad a dodržování předpisů pro toto předplatné. V tomto mluveném komentáři tým zásad správného řízení vybral vzor návrhu **[smíšeného](../../../decision-guides/subscriptions/index.md#mixed-patterns)** předplatného.

- Vzhledem k novým požadavkům na prostředky Azure by se mělo zřídit "oddělení" pro každou hlavní organizační jednotku v jednotlivých provozních zeměpisných oblastech. V rámci každého oddělení by se pro každou aplikaci Archetype vytvořit předplatné.
- Archetype aplikací je způsob seskupení aplikací s podobnými potřebami. Mezi běžné příklady patří: aplikace s chráněnými daty, řízené aplikace (například HIPAA nebo FedRAMP), aplikace s nízkým rizikem, aplikace s místními závislostmi, SAP nebo jiné sálové aplikace v Azure nebo aplikace, které rozšiřuje místní aplikace SAP nebo sálové. Každá organizace má jedinečné potřeby na základě klasifikace dat a typů aplikací, které podporují firmu. Mapování závislostí digitální nemovitosti může přispět k definování aplikace archetypes v organizaci.
- Společná konvence pojmenování by se měla schválit v rámci návrhu předplatného na základě výše uvedených dvou odrážek.

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

Rozhodnutí označování prostředků určují, jak se metadata v rámci předplatného aplikují na prostředky Azure za účelem podpory operací, správy a účetní účely. V tomto mluveném komentáři byl vzor **[monitorování účtů](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** vybraný jako výchozí model pro označování prostředků.

- Nasazené prostředky by měly být označeny hodnotami pro:
  - Oddělení/fakturační jednotka
  - Geografické
  - Klasifikace dat
  - Závažnost
  - SLA
  - Prostředí
  - Archetype aplikace
  - Aplikace
  - Vlastník aplikace
- Tyto hodnoty společně se skupinou pro správu Azure a s předplatným, které jsou přidružené k nasazenému assetu, budou řídit řízení, operacemi a bezpečnostními rozhodnutími.

### <a name="logging-and-reporting"></a>Protokolování a vytváření sestav

Rozhodnutí týkající se protokolování a vytváření sestav určují, jak jsou strukturovaná data protokolu úložiště a jak jsou strukturované nástroje pro monitorování a vytváření sestav, které udržují pracovníky IT informace o provozním stavu. V tomto mluveném komentáři je vzor **[hybridního monitorování](../../../decision-guides/logging-and-reporting/index.md)** pro protokolování a vytváření sestav navržený, ale nevyžaduje se v tomto okamžiku žádný vývojový tým.

- V současné době nejsou nastaveny žádné požadavky zásad správného řízení týkající se konkrétních datových bodů, které se mají shromáždit pro účely protokolování nebo generování sestav. Tato funkce je specifická pro tento fiktivní mluvený komentář a měla by být považována za antipattern. Standardy protokolování by měly být určovány a vynutily co nejrychleji.
- Další analýza se vyžaduje před vydáním jakýchkoli chráněných dat nebo úloh, které jsou důležité pro kritické úlohy.
- Předtím, než podporuje chráněná data nebo úlohy kritické, musí mít existující místní řešení pro monitorování provozu udělený přístup k pracovnímu prostoru, který se používá k protokolování. Aplikace se vyžadují pro splnění požadavků na zabezpečení a protokolování spojených s používáním tohoto tenanta, pokud je aplikace podporovaná s definovanou smlouvou SLA.

## <a name="incremental-of-governance-processes"></a>Přírůstkové procesy zásad správného řízení

Některé příkazy zásad nelze nebo by neměly být ovládány pomocí automatizovaných nástrojů. Další zásady budou vyžadovat pravidelné úsilí od zabezpečení IT a místních týmů standardních identit. Tým zásad správného řízení cloudu bude muset dohlížet na následující procesy, aby implementovaly posledních osm příkazů zásad:

**Změny firemních zásad:** Tým zásad správného řízení cloudu provede změny v návrhu MVP zásad správného řízení, aby tyto nové zásady přijaly. Hodnota MVP pro řízení správného řízení je taková, že umožní automatické vynucení nových zásad.

**Akcelerace přijetí:** Tým zásad správného řízení cloudu kontroluje skripty pro nasazení napříč několika týmy. Udržovaly sadu skriptů, které slouží jako šablony nasazení. Tyto šablony můžou týmy pro přijetí cloudu a DevOps týmy použít k rychlejšímu definování nasazení. Každý skript obsahuje požadavky na vynucování zásad správného řízení a další úsilí od techniků na přijetí cloudu není potřeba. Curators těchto skriptů může provádět změny zásad rychleji. Navíc se zobrazují jako akcelerátory přijetí. Tím se zajistí konzistentní nasazení bez striktního vynucování dodržování.

**Školení pro inženýry:** Tým zásad správného řízení cloudu nabízí bimonthly školicích cvičení a vytvořil dvě videa pro inženýry. Oba prostředky pracovníkům umožňují rychle zrychlit používání jazykové verze zásad správného řízení a postup nasazení. Tým přidává školicí materiály, které ukazují rozdíl mezi nasazeními v produkčním prostředí a neprodukčním prostředí, které pomáhá technikům pochopit, jak nové zásady ovlivňují přijetí. Tím se zajistí konzistentní nasazení bez striktního vynucování dodržování.

**Plánování nasazení:** Před nasazením jakýchkoli prostředků, které obsahují chráněná data, bude tým zásad správného řízení pro Cloud zodpovědný za kontrolu skriptů nasazení za účelem ověření přizpůsobení zásad správného řízení. Stávající týmy s dřív schváleným nasazením budou auditovány pomocí programových nástrojů.

**Měsíční audit a vytváření sestav:** Každý měsíc tým zásad správného řízení cloudu spustí audit všech nasazení cloudu, aby ověřil pokračování v sestavování zásad. Když se zjistí odchylky, budou se zdokumentovat a sdílet s týmy pro přijetí v cloudu. Pokud vynucení nehrozí při výpadku nebo úniku dat, zásady se automaticky vynucuje. Na konci auditu zkompiluje tým zásad správného řízení Cloud zprávu pro tým cloudové strategie a každý tým pro přijetí cloudu, aby komunikoval celkové dodržování zásad. Sestava je také uložená pro účely auditování a právní účely.

**Kontrola čtvrtletních zásad:** Každé čtvrtletí, tým zásad správného řízení cloudu a tým cloudových strategií ke kontrole výsledků auditu a navrhování změn podnikových zásad. Mnohé z těchto návrhů jsou výsledkem průběžných vylepšení a pozorování vzorců používání. Schválené změny zásad jsou integrovány do nástrojů zásad správného řízení během dalších cyklů auditu.

## <a name="alternative-patterns"></a>Alternativní vzory

Pokud se některý ze vzorů zvolených v této příručce zásad správného řízení Nezarovnává s požadavky čtenáře, jsou k dispozici alternativy ke každému vzoru:

- [Vzory šifrování](../../../decision-guides/encryption/index.md)
- [Vzory identity](../../../decision-guides/identity/index.md)
- [Vzorce protokolování a vytváření sestav](../../../decision-guides/logging-and-reporting/index.md)
- [Vzory vynucování zásad](../../../decision-guides/policy-enforcement/index.md)
- [Vzory konzistence prostředků](../../../decision-guides/resource-consistency/index.md)
- [Vzory označování prostředků](../../../decision-guides/resource-tagging/index.md)
- [Vzory softwarově definovaných sítí](../../../decision-guides/software-defined-network/index.md)
- [Vzory návrhu předplatného](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Další kroky

Po implementaci těchto pokynů může tým pro přijetí v cloudu pokračovat se základními základními zásadami správy. Ve stejnou chvíli tým zásad správného řízení pro Cloud bude fungovat tak, aby průběžně aktualizoval podnikové zásady a obory řízení.

Oba týmy použijí indikátory tolerance k identifikaci další sady vylepšení potřebných pro pokračování v podpoře přijímání do cloudu. Dalším krokem této společnosti je přírůstkové zlepšování jejich standardních hodnot zásad správného řízení, které podporují aplikace se staršími verzemi nebo požadavky služby Multi-Factor Authentication od jiných výrobců.

> [!div class="nextstepaction"]
> [Zlepšení pravidla směrného plánu identity](./identity-baseline-improvement.md)
