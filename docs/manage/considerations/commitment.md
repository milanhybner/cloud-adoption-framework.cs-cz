---
title: 'Obchodní závazek: cloudová správa a operace'
description: 'Obchodní závazek: cloudová správa a operace'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4827ca2aac045b105beed9c15de366311092a7f2
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807848"
---
# <a name="business-commitment-in-cloud-management"></a>Obchodní závazek ve správě cloudu

Definování _obchodních závazků_ je cvičení pro vyrovnávání priorit. Cílem je zarovnávat správnou úroveň provozní správy s přijatelnými provozními náklady. Vyhledání tohoto zůstatku vyžaduje několik datových bodů a výpočtů, které jsme si povedli v tomto článku.

![Vyvážení nákladů a odolnosti](../../_images/manage/business-commitment-scale.png)

Závazky na podnikovou stabilitu, prostřednictvím technické odolnosti nebo jiných dopadů smlouvy o úrovni služeb (SLA), představují rozhodnutí o obchodním odůvodnění. Pro většinu úloh v prostředí je základní úroveň správy cloudu dostačující. Pro ostatní je nárůst nákladů o dvojnásobek na 4x snadno odůvodněný z důvodu potenciálního dopadu na přerušování společnosti.

Předchozí články v této sérii vám pomůžou pochopit klasifikaci a dopad přerušení na různé úlohy. Tento článek vám pomůže vypočítat počet vrácených hodnot. Jak je znázorněno na předchozím obrázku, každá úroveň správy cloudu má inflexes Points, kde náklady mohou zvýšit odolnost proti chybám. Tyto body inflexe budou zobrazovat podrobné obchodní rozhodnutí a obchodní závazky.

## <a name="determine-a-proper-commitment-with-the-business"></a>Určení správného závazku pro firmu

Pro každou úlohu v portfoliu by tým cloudových operací a týmu cloudové strategie měli v souladu s úrovní správy, která je poskytována přímo týmem cloudových operací.

Když vytváříte závazek s firmou, existuje několik klíčových aspektů, které je potřeba zarovnat:

- Požadavky na provoz IT
- Zodpovědnost za správu
- Cloudové architektury
- Měkké náklady
- Návratnost investic k zamezení ztrát
- Ověření úrovně správy

V rámci vašeho rozhodovacího procesu bude zbývající část tohoto článku podrobněji popsán každé z těchto aspektů.

## <a name="it-operations-prerequisites"></a>Požadavky na provoz IT

[Příručka pro správu Azure](../azure-management-guide/index.md) popisuje nástroje pro správu, které jsou k dispozici v Azure. Než se pustíte do podnikání, měli byste určit přijatelný směrný plán správy standardní úrovně, který se má použít pro všechny spravované úlohy. Pro každou spravovanou úlohu v portfoliu IT pak vypočítá standardní náklady na správu na základě počtu jader procesoru, místa na disku a dalších proměnných souvisejících s prostředky. Také odhaduje složenou smlouvu SLA pro jednotlivé úlohy na základě architektury.

> [!TIP]
> Provozní týmy IT často používají pro počáteční složenou smlouvu SLA výchozí minimální hodnotu 99,9% doba provozu. Můžou se také rozhodnout normalizovat náklady na správu na základě průměrného zatížení, zejména pro řešení s minimálními nároky na protokolování a úložiště. Průměrné náklady na několik středně kritických úloh můžou poskytovat výchozí bod pro počáteční konverzace.

<!-- -->

> [!TIP]
> Pokud pro plánování správy cloudu používáte [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) , měla by být pole správy OPS aktualizována tak, aby odrážela tyto požadavky. Mezi tato pole patří _úroveň závazku_, _složená smlouva SLA_a _měsíční náklady_. Měsíční náklady by měly představovat náklady na přidané nástroje provozní správy měsíčně.

Operations Management směrné plány slouží jako počáteční počáteční bod, který se má ověřit v každé z následujících částí.

## <a name="management-responsibility"></a>Zodpovědnost za správu

V tradičním místním prostředí se obvykle předpokládá, že náklady na správu prostředí jsou SUNK náklady, které vlastní IT operace. V cloudu je Správa záměrné rozhodnutím s přímým dopadem na rozpočtové účely. Náklady na jednotlivé funkce správy mohou být přímo přiděleny každému zatížení, které je nasazeno do cloudu. Tento přístup umožňuje lepší kontrolu, ale vytváří požadavek na týmy cloudových operací a týmy cloudových strategií, aby se nejdřív zavázali ke Smlouvě o odpovědnosti.

Organizace také mohou zvolit, že [některé z jejich probíhajících funkcí správy pro poskytovatele služeb](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Tito poskytovatelé služeb můžou využít [Azure Lighthouse](https://azure.com/lighthouse) k zajištění přesnější kontroly nad udělením přístupu ke svým prostředkům a lepším přehledem o akcích prováděných poskytovateli služeb.

- **Delegovaná odpovědnost:** Vzhledem k tomu, že není nutné centralizovat a předpokládat provozní režii, operace IT pro mnoho organizací zvažuje nové přístupy. Jedním ze společného přístupu se říká _delegovaná odpovědnost_. V cloudovém středisku modelu vynikajících platforem můžou operace platforem a automatizace platforem poskytovat nástroje pro samoobslužné řízení, které mohou být používány provozními týmy výrobního oddělení, nezávisle na centrálním podnikovém provozu IT. Tento přístup dává obchodním stranám úplnou kontrolu nad rozpočty souvisejícími se správou. Umožňuje také týmu CCoE (Cloud Center of vynikající) zajistit, aby byla správně implementována minimální sada guardrails. V tomto modelu funguje jako zprostředkovatel a příručka, která usnadňuje rozhodování v podniku. Obchodní operace, které přihlíží ke každodenním operacím závislých úloh.

- **Centralizovaná odpovědnost:** Požadavky na dodržování předpisů, technická složitost a některé modely sdílených služeb můžou vyžadovat _centrální model IT_ . V tomto modelu se nadále vykonává odpovědnost za správu provozu. Návrh na životní prostředí, ovládací prvky pro správu a nástroje pro řízení přístupu mohou být centrálně spravovány a kontrolovány, což omezuje roli obchodních zúčastněných stran při řízení závazků. Vhledem k tomu, že jsou náklady a architektura cloudových přístupů mnohem jednodušší, je jejich centralizované, aby komunikovaly s náklady a úrovní správy pro jednotlivé úlohy.

- **Smíšený model:** Klasifikace je srdcem _smíšeného modelu_ odpovědnosti za správu. Společnosti, které jsou v průběhu transformaci z místního prostředí do cloudu, můžou během chvilky vyžadovat místní model. Společnosti, které mají přísné požadavky na dodržování předpisů nebo které závisí na dlouhodobých smlouvách se dodavateli outsourcingu IT, můžou vyžadovat centralizovaný operační model.

  Bez ohledu na jejich omezení musí dnešní firmy inovovat. V případě, že se rychlé inovace musí narazit v průběhu ústředního modelu centralizované zodpovědnosti, může to vést ke smíšenému modelu. V tomto přístupu centrální IT poskytuje centralizovaný operační model pro všechny úlohy, které jsou důležité nebo obsahují citlivé informace. Všechny ostatní klasifikace úloh se ale můžou nacházet v cloudovém prostředí, které je navržené pro delegované zodpovědnosti. Centralizovaný přístup k zodpovědnosti slouží jako obecný operační model. Společnost pak bude mít flexibilitu na základě požadované úrovně podpory a citlivosti k přijetí specializovaného operačního modelu.

První krok se zavazuje k přístupu k odpovědnosti, který potom vytvoří tyto závazky.

**Která organizace bude zodpovědná za každodenní řízení provozu této úlohy?**

## <a name="cloud-tenancy"></a>Cloudové architektury

U většiny firem je správa jednodušší, pokud jsou všechny assety umístěny v jednom tenantovi. Některé organizace ale můžou potřebovat zachovat víc tenantů. Informace o tom, proč podnik může vyžadovat víceklientské prostředí Azure, najdete v tématu [centralizace operací správy pomocí Azure Lighthouse](../centralize-operations.md).

**Bude tato úloha umístěná v jednom tenantovi Azure, společně se všemi ostatními úlohami?**

## <a name="soft-cost-factors"></a>Měkké náklady

V další části najdete popis přístupu ke srovnávacím návratům, které jsou spojeny s úrovněmi procesů a nástrojů správy. Na konci tohoto oddílu každá analyzovaná úloha měří náklady na správu vzhledem k předpokládanému dopadu na narušení podniku. Tento přístup poskytuje poměrně snadný způsob, jak pochopit, jestli je zaručená investice do rozsáhlejších přístupů ke správě.

Než začnete s čísly, je důležité se podívat na faktory měkkého nákladu. Měkké cenové faktory vyvolávají návrat, ale toto vrácení je obtížné změřit prostřednictvím přímých úspor za cenu, která by byla viditelná v rámci výkazu zisků a ztrát. Měkké náklady jsou důležité, protože mohou znamenat nutnost investovat do vyšší úrovně správy, než je fiskální – obezřetné.

Mezi příklady měkkých a nákladových faktorů patří:

- Denní využití úloh na vývěsce nebo generálního ředitele.
- Využití úlohy podle horních _x procent_ zákazníků, které vedou k většímu dopadu na výnosy jinde.
- Dopad na spokojenost zaměstnanců.

Dalším datovým bodem, který je nutný k vytvoření závazku, je seznam faktorů s měkkými náklady. Tyto faktory není v této fázi nutné zdokumentovat, ale obchodní účastníci by měli znát důležitost těchto faktorů a jejich vyloučení z následujících výpočtů.

## <a name="calculate-loss-avoidance-roi"></a>Vypočítat návratnost ztrát v případě výpadků

Při výpočtu relativního návratnosti nákladů na správu provozu by IT tým zodpovědný za cloudové operace měl provést výše zmíněné předpoklady a předpokládat minimální úroveň správy pro všechny úlohy.

Další závazek, který se má provést, je přijetí za firmy nákladů spojených s nabídkou spravovanou na základě směrného plánu.

**Souhlasí obchodní oddělení investovat v rámci základní nabídky, aby splnila minimální standardy cloudových operací?**

Pokud podnik nesouhlasí s touto úrovní správy, je nutné navrhnout řešení, které umožní podniku pokračovat, aniž by to mělo vliv na cloudové operace jiných úloh.

Pokud má firma více než úroveň Standard úrovně správy, zbývající část této části pomůže ověřit, jestli investice a související vratky (ve formě předcházení ztrátám).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Zvýšené úrovně správy: Principy návrhu a katalog služeb

Pro spravovaná řešení je možné kromě standardních hodnot správy použít několik principů návrhu a řešení šablon. Jednotlivé zásady návrhu pro spolehlivost a odolnost zvyšují provozní náklady na zatížení. Pro IT a firmy, které souhlasíte s těmito dodatečnými závazky, je důležité pochopit potenciální ztráty, které je možné vyhnout prostřednictvím této zvýšené investice.

Následující výpočty vás provedou vzorci, které vám pomůžou lépe porozumět rozdílům mezi ztrátami a vyššími investicemi do správy. Pokyny k výpočtu nákladů na zvýšenou správu najdete v tématu [Automatizace úloh](./workload.md) a [Automatizace platforem](./platform.md).

> [!TIP]
> Pokud pro plánování správy cloudu používáte [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) , aktualizujte pole správy OPS tak, aby odrážela jednotlivé konverzace. Mezi tato pole patří _úroveň závazku_, _složená smlouva SLA_a _měsíční náklady_. Měsíční náklady by měly představovat měsíční náklady na přidané nástroje provozní správy. Po aktualizaci budou pole aktualizovat vzorce návratnosti investic a každé z následujících polí.

### <a name="estimate-outage-hours-per-year"></a>Odhadnout výpadek (hodiny za rok)

Složená smlouva SLA je smlouvou na úrovni služby, která je založená na nasazení jednotlivých assetů v rámci úlohy. Toto pole _vyhodnoceno jako odhadované výpadky_ (s označením _EST. výpadek_ v sešitu). Chcete-li vypočítat odhadované výpadky v hodinách za rok bez použití sešitu, použijte následující vzorec:

> _Odhadované výpadky = (1 – složený procentní podíl &#215; smlouvy SLA) počet hodin v roce_

Sešit používá výchozí hodnotu _8 760 hodin za rok_.

### <a name="standard-loss-impact"></a>Dopad na standardní ztrátu

_Standardní dopad ztráty_ (označený jako _standardní dopad_ v sešitu) předpovídá finanční dopad jakéhokoli výpadku za předpokladu, že _odhad předpovědi výpadků_ prokáže přesnost. K výpočtu této prognózy bez použití sešitu použijte následující vzorec:

> _Standardní dopad = odhadované výpadky @ 3 devítky &#215; doby provozu – dopad na hodnotu_

Tato možnost slouží jako základ pro náklady, pokud se obchodní účastníci rozhodnou investovat do vyšší úrovně správy.

### <a name="composite-sla-impact"></a>Složený dopad na smlouvu SLA

_Složený dopad smlouvy SLA_ (s názvem _dopad na úroveň závazku_ v sešitu) poskytuje aktualizovaný daňový dopad na základě změn v rámci smlouvy SLA pro dobu provozu. Tento výpočet vám umožní porovnat plánovaný finanční dopad obou možností. Chcete-li vypočítat tento dopad prognózy bez tabulky, použijte následující vzorec:

> _Složený dopad na smlouvu SLA = &#215; odhadovaný čas výpadku – dopad na hodnotu_

Hodnota představuje potenciální ztráty, které se mají vyvarovat od změněné úrovně závazku a nové složené smlouvy SLA.

### <a name="comparison-basis"></a>Základ porovnání

_Srovnávací základ_ vyhodnocuje standardní dopad a složený dopad smlouvy SLA, aby bylo možné určit, který z nich je nejvhodnější ve sloupci vráceno.

### <a name="return-on-loss-avoidance"></a>Vyloučení při výpadku ztráty

Pokud náklady na správu zatížení překročí potenciální ztráty, nemusí být navrhovaná investice do správy cloudu neovocná. Chcete-li porovnat _vrácení se ztrátou_, přečtěte si sloupec s označením _roční návratnost investic * *_ * *. Pokud chcete tento sloupec vypočítat sami, použijte následující vzorec:

> _Nevrácení ztráty při ztrátě = (porovnání základů – (měsíční &#215; náklady 12) &#247; ) (měsíční &#215; náklady 12))_

Pokud neexistují žádné další faktory, které by bylo potřeba vzít v úvahu, může toto porovnání rychle navrhnout, jestli by měla být hlubší investice do cloudových operací, odolnosti, spolehlivosti a dalších oblastí.

## <a name="validate-the-commitment"></a>Ověřit závazek

V tomto okamžiku se v tomto procesu přijaly závazky: Centralizovaná nebo delegovaná odpovědnost, Azure tenantů a úroveň závazku. Každý závazek by se měl ověřit a zdokumentovat, aby se zajistilo, že je tým cloudových operací, tým cloudové strategie a obchodní účastníci zarovnaný k tomuto závazku spravovat úlohy.

## <a name="next-steps"></a>Další kroky

Po provedení závazků můžou odpovědné provozní týmy začít konfigurovat příslušné úlohy. Pokud chcete začít, vyhodnoťte různé přístupy k [inventarizaci a viditelnosti](./inventory.md).

> [!div class="nextstepaction"]
> [Možnosti inventarizace a viditelnosti](./inventory.md)
