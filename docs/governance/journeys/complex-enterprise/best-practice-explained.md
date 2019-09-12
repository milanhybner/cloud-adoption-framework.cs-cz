---
title: 'Příručka zásad správného řízení pro komplexní podniky: Vysvětlení doporučených pokynů'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s doporučenými pokyny pro zásady správného řízení ve složitých podnicích.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ac099f89fe68d33ae5272e19ff97587a833c9002
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908953"
---
# <a name="governance-guide-for-complex-enterprises-prescriptive-guidance-explained"></a>Příručka zásad správného řízení pro komplexní podniky: Vysvětlení doporučených pokynů

Příručka zásad správného řízení začíná sadou počátečních [podnikových zásad](./initial-corporate-policy.md). Tyto zásady se používají k vytvoření minimálního životaschopného produktu (MVP) pro zásady správného řízení, které odráží [osvědčené postupy](./index.md).

V tomto článku probereme strategie vysoké úrovně, které jsou potřeba k vytvoření MVP pro řízení. Základem MVP v rámci zásad správného řízení je obor [akcelerace nasazení](../../deployment-acceleration/index.md) . Nástroje a vzory použité v této fázi budou umožňovat přírůstková vylepšení nutná k rozšíření zásad správného řízení v budoucnu.

## <a name="governance-mvp-initial-governance-foundation"></a>MVP pro zásady správného řízení (počáteční zásady správného řízení)

Rychlé přijetí zásad správného řízení a podnikových zásad se může dosáhnout několika jednoduchými zásadami a pomocí cloudových nástrojů zásad správného řízení. Jedná se o první ze tří oborů řízení přístupu k přístupu v jakémkoli procesu zásad správného řízení. Jednotlivé disciplíny se v tomto článku vysvětlí podrobněji.

Tento článek pojednává o strategiích vysoké úrovně za směrným plánem identity, základním hodnotám zabezpečení a akceleraci nasazení, které jsou potřeba k vytvoření MVP MVP, který bude sloužit jako základ pro všechna přijetí.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/governance/governance-mvp.png)

## <a name="implementation-process"></a>Proces implementace

Implementace MVP v rámci zásad správného řízení má závislosti na identitě, zabezpečení a síti. Až budou závislosti vyřešeny, tým zásad správného řízení pro Cloud určí několik aspektů zásad správného řízení. Rozhodnutí od týmu zásad správného řízení cloudu a od pomocných týmů budou implementována prostřednictvím jediného balíčku prostředků vynucení.

![Příklad MVP inkrementálních zásad správného řízení](../../../_images/governance/governance-mvp-implementation-flow.png)

Tuto implementaci je také možné popsat pomocí jednoduchého kontrolního seznamu:

1. Vyžádat rozhodnutí týkající se základních závislostí: Identita, síť a šifrování.
1. Určete vzor, který se použije při vynucování podnikových zásad.
1. Určete vhodné vzory zásad správného řízení pro konzistenci prostředků, označování prostředků a obory protokolování a generování sestav.
1. Implementujte nástroje zásad správného řízení zarovnané na vybraný model vynucení zásad, abyste mohli použít závislá rozhodnutí a rozhodnutí o zásadách správného řízení.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Použití vzorů definovaných zásadami správného řízení

Tým zásad správného řízení cloudu bude zodpovědný za následující rozhodnutí a implementace. Mnohé budou vyžadovat vstupy z jiných týmů, ale tým zásad správného řízení cloudu bude nejspíš vlastnit rozhodnutí i implementaci. Následující části popisují rozhodnutí učiněná v tomto případu použití a podrobnosti o každém rozhodnutí.

### <a name="subscription-design"></a>Návrh předplatného

Rozhodnutí o tom, jaký návrh předplatných se má použít, určuje, jak se předplatná Azure získají strukturovaná a jak se skupiny pro správu Azure budou používat k efektivní správě přístupu, zásad a dodržování předpisů pro toto předplatné. V tomto mluveném komentáři tým zásad správného řízení vybral vzor návrhu **[smíšeného](../../../decision-guides/subscriptions/index.md#mixed-patterns)** předplatného.

- Vzhledem k novým požadavkům na prostředky Azure by se mělo zřídit "oddělení" pro každou hlavní organizační jednotku v jednotlivých provozních zeměpisných oblastech. V rámci každého oddělení by se pro každou aplikaci Archetype vytvořit předplatné.
- Archetype aplikací je způsob seskupení aplikací s podobnými potřebami. Mezi běžné příklady patří: Aplikace s chráněnými daty, řízené aplikace (například HIPAA nebo FedRAMP), aplikace s nízkým rizikem, aplikace s místními závislostmi, SAP nebo jiné sálové aplikace v Azure nebo aplikace, které šíří místní SAP nebo sálové počítače vyrovnání. Každá organizace má jedinečné potřeby na základě klasifikace dat a typů aplikací, které podporují firmu. Mapování závislostí digitální nemovitosti může přispět k definování aplikace archetypes v organizaci.
- Společná konvence pojmenování by se měla schválit v rámci návrhu předplatného na základě výše uvedených dvou odrážek.

### <a name="resource-consistency"></a>Konzistence prostředků

Rozhodnutí o konzistenci prostředků určují nástroje, procesy a úsilí potřebné k zajištění konzistentního nasazení, konfigurace a správy prostředků Azure v rámci předplatného. V tomto mluveném komentáři byla **[Hierarchická konzistence](../../../decision-guides/resource-consistency/index.md#hierarchical-consistency)** zvolena jako vzor konzistence primárního prostředku.

- Skupiny prostředků by se měly vytvářet pro každou aplikaci. Skupiny pro správu by měly být vytvořeny pro každou aplikaci Archetype. Azure Policy by se měla použít pro všechna předplatná v přidružené skupině pro správu.
- V rámci procesu nasazení by měly být šablony konzistence prostředků pro všechny prostředky uloženy ve správě zdrojového kódu.
- Každá skupina prostředků by se měla zarovnat na konkrétní úlohu nebo aplikaci.
- Definovaná hierarchie skupiny pro správu Azure by měla představovat odpovědnost za fakturaci a vlastnictví aplikace pomocí vnořených skupin.
- Rozsáhlá implementace Azure Policy může překročit časové závazky týmu a v tomto okamžiku nesmí poskytnout mnohem větší hodnotu. Pro každou skupinu prostředků byste ale měli vytvořit a použít jednoduchou výchozí zásadu, která vynutila prvních několik příkazů zásad správného řízení cloudu. Slouží k definování implementace konkrétních požadavků zásad správného řízení. Tyto implementace je pak možné použít napříč všemi nasazenými prostředky.

### <a name="resource-tagging"></a>Označování prostředků

Rozhodnutí označování prostředků určují, jak se metadata v rámci předplatného aplikují na prostředky Azure za účelem podpory operací, správy a účetní účely. V tomto mluveném komentáři byl vzor **[monitorování účtů](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** vybraný jako výchozí model pro označování prostředků.

- Nasazené prostředky by měly být označeny hodnotami pro:
  - Oddělení/fakturační jednotka
  - Geografie
  - Klasifikace dat
  - Závažnost
  - SLA
  - Prostředí
  - Archetype aplikace
  - Aplikace
  - Vlastník aplikace
- Tyto hodnoty společně se skupinou pro správu Azure a s předplatným, které jsou přidružené k nasazenému assetu, budou řídit řízení, operacemi a bezpečnostními rozhodnutími.

### <a name="logging-and-reporting"></a>Protokolování a vytváření sestav

Rozhodnutí týkající se protokolování a vytváření sestav určují, jak jsou strukturovaná data protokolu úložiště a jak jsou strukturované nástroje pro monitorování a vytváření sestav, které udržují pracovníky IT informace o provozním stavu. V tomto mluveném komentáři je vzor **[hybridního monitorování](../../../decision-guides/log-and-report/index.md)** pro protokolování a vytváření sestav navržený, ale nevyžaduje se v tomto okamžiku žádný vývojový tým.

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
- [Vzorce protokolování a vytváření sestav](../../../decision-guides/log-and-report/index.md)
- [Vzory vynucování zásad](../../../decision-guides/policy-enforcement/index.md)
- [Vzory konzistence prostředků](../../../decision-guides/resource-consistency/index.md)
- [Vzory označování prostředků](../../../decision-guides/resource-tagging/index.md)
- [Vzory softwarově definovaných sítí](../../../decision-guides/software-defined-network/index.md)
- [Vzory návrhu předplatného](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Další kroky

Po implementaci těchto pokynů může tým pro přijetí v cloudu pokračovat se základními základními zásadami správy. Tým zásad správného řízení cloudu bude paralelně fungovat a průběžně aktualizuje podnikové zásady a obory řízení.

Oba týmy použijí indikátory tolerance k identifikaci další sady vylepšení potřebných pro pokračování v podpoře přijímání do cloudu. Dalším krokem této společnosti je přírůstkové zlepšování jejich standardních hodnot zásad správného řízení, které podporují aplikace se staršími verzemi nebo požadavky služby Multi-Factor Authentication od jiných výrobců.

> [!div class="nextstepaction"]
> [Zlepšení pravidla směrného plánu identity](./identity-baseline-evolution.md)
