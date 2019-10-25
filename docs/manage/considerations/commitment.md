---
title: Kritická obchodní náročnost – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Kritická obchodní náročnost – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7e7618163b15d17eab51571779e573dd9acb726e
ms.sourcegitcommit: 73dbedf580951f25bf4b5544b83451cb075b1fa1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/23/2019
ms.locfileid: "72805815"
---
# <a name="business-commitment-in-cloud-management"></a>Obchodní závazek ve správě cloudu

Definování obchodního závazku je cvičení pro vyrovnávání priorit. Cílem je zarovnávat správnou úroveň provozní správy s přijatelnými provozními náklady. Vyhledání tohoto zůstatku vyžaduje několik datových bodů a výpočtů, které jsou popsány v následujících částech.

![Vyvážení nákladů a odolnosti](../../_images/manage/business-commitment-scale.png)

Závazky na stabilitu podniku (prostřednictvím technické odolnosti nebo jiných dopadů na smlouvu SLA) představují rozhodnutí o obchodním odůvodnění. Pro většinu úloh v prostředí je základní úroveň správy cloudu dostačující. Pro ostatní se zvýšení nákladů na 2 &ndash;4x dá snadno zdůvodnit z důvodu potenciálního dopadu na případné přerušování. Předchozí články v této sérii pomáhají pochopit klasifikaci a dopad přerušení na různé úlohy. Tento článek vám pomůže při výpočtu vrácených chyb. Jak je uvedeno na následujícím obrázku, v každé úrovni správy cloudu jsou k dispozici inflexes Points, kde náklady mohou zvýšit odolnost proti chybám. Tyto body inflexe budou zobrazovat podrobné obchodní rozhodnutí a obchodní závazky.

## <a name="determining-a-proper-commitment-with-the-business"></a>Stanovení správného závazku pro firmu

Pro každou úlohu v portfoliu by tým cloudových operací a týmu cloudové strategie měli zarovnat na úrovni správy poskytované přímo týmem cloudových operací.

Následují klíčové aspekty, které je potřeba zarovnat při stanovování závazku s firmou:

- Požadavky na provoz IT
- Zodpovědnost za správu
- Cloudové architektury
- Měkké náklady
- Návratnost investic k zamezení ztrát
- Ověřit úroveň správy

Zbývající část tohoto článku popisuje každé z těchto kritérií, která vám pomůžou při rozhodování.

## <a name="it-operations-prerequisites"></a>Požadavky na provoz IT

[Příručka pro správu Azure](../azure-management-guide/index.md) obsahuje přehled nástrojů pro správu dostupných v Azure. Předtím, než se dokončí závazek na firmu, by mělo určit přijatelný standardní úroveň správy úrovně Standard, která se má použít pro všechny spravované úlohy. Pro každou spravovanou úlohu v portfoliu IT pak vypočítá standardní náklady na správu na základě počtu jader procesoru, místa na disku a dalších proměnných souvisejících s prostředky. Také odhaduje složenou smlouvu SLA pro jednotlivé úlohy na základě architektury.

> [!TIP]
> Provozní týmy IT často pro počáteční složenou smlouvu SLA použijí výchozí minimální dobu 99,9% dostupnost. Můžou se také rozhodnout normalizovat náklady na správu na základě průměrného zatížení, zejména pro řešení s minimálními nároky na protokolování a úložiště. Průměrné náklady na několik středně kritických úloh můžou poskytovat výchozí bod pro počáteční konverzace.

> [!TIP]
> Pro uživatele, kteří používají [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k naplánování správy cloudu, by se měla aktualizovat pole správy OPS tak, aby odrážela tyto požadavky. Mezi tato pole patří úroveň závazku, složená smlouva SLA a měsíční náklady. Měsíční náklady by měly představovat náklady na přidané nástroje provozní správy měsíčně.

Operations Management směrného plánu bude sloužit jako počáteční výchozí bod, který se má ověřit v každé z následujících sekcí.

## <a name="management-responsibility"></a>Zodpovědnost za správu

V tradičním místním prostředí se náklady na správu prostředí běžně předpokládají jako SUNK náklady vlastněné IT operacemi. V cloudu je Správa záměrné rozhodnutím s přímým dopadem na rozpočtové účely. Náklady na jednotlivé funkce správy mohou být přímo přiděleny každému zatížení, které je nasazeno do cloudu. Tento přístup umožňuje lepší kontrolu, ale vytváří požadavek na týmy cloudových operací a týmy cloudových strategií, aby se nejdřív zavázali k dohodě.

Organizace také mohou zvolit, že [některé z jejich probíhajících funkcí správy pro poskytovatele služeb](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Tito poskytovatelé služeb můžou využít [Azure Lighthouse](https://azure.com/lighthouse) a poskytnout tak větší přesnost a kontrolu nad tím, že budou poskytovat přístup ke svým prostředkům, společně s větší transparentností do akcí prováděných poskytovateli služeb.

**Delegovaná odpovědnost:** Vzhledem k tomu, že není nutné centralizovat a předpokládat provozní režii, operace IT pro mnoho organizací zvažuje nové přístupy. Jedním ze společného přístupu se říká delegovaná odpovědnost. V cloudovém středisku modelu vynikajících platforem a automatizace platforem poskytují nástroje pro samoobslužné řízení, které můžou využívat firemní týmy s provozními službami, nezávisle na centrálním týmu IT. Tento přístup poskytuje obchodním zúčastněným účastníkům úplnou kontrolu nad rozpočty souvisejícími se správou. Umožňuje také CCoE, aby bylo zajištěno, že je správně implementována minimální sada guardrails. V tomto modelu funguje jako zprostředkovatel a příručka, která usnadňuje rozhodování v podniku. Obchodní operace, které přihlíží ke každodenním operacím závislých úloh.

**Centralizovaná odpovědnost:** Požadavky na dodržování předpisů, technická složitost a některé modely sdílených služeb můžou vyžadovat centrální model IT. V tomto modelu nadále udržuje odpovědnost za správu operací. V takovém případě může být návrh prostředí, ovládací prvky pro správu a nástroj řízení přístupu centrálně spravován a kontrolován, což omezuje roli zúčastněných účastníků v rámci poskytování závazků pro správu. Díky tomu, že díky cloudovým přístupům a nákladům na architekturu získáte mnohem jednodušší centralizované oddělení IT, aby komunikovalo s náklady a úrovní správy pro jednotlivé úlohy.

**Smíšený model:** Klasifikace je srdcem smíšeného modelu pro zodpovědnost za správu. Společnosti, které jsou v průběhu transformaci z místního prostředí do cloudu, můžou během chvilky vyžadovat místní a první operační model. Jiné společnosti, které mají přísné požadavky na dodržování předpisů nebo které jsou závislé na dlouhodobých smlouvách s dodavateli IT, můžou vyžadovat centralizovaný operační model. Navzdory těmto typům omezení firmy potřebují inovovat. V případě, že se rychlé inovace musí narazit v průběhu centrálního modelu centralizované zodpovědnosti, klasifikace a smíšený model, může poskytovat rovnováhu. V tomto přístupu centrální IT poskytuje centralizovaný operační model pro všechny úlohy, které jsou důležité nebo obsahují citlivé informace. Všechny ostatní klasifikace úloh ale můžou být umístěné v cloudovém prostředí určeném pro delegované zodpovědnosti. Centralizovaný přístup k zodpovědnosti slouží jako obecný operační model. Podnikání pak má flexibilitu při využití specializovaného operačního modelu na základě požadované úrovně podpory a citlivosti.

První krok se zavazuje k přístupu k odpovědnosti, který bude tyto závazky vynést.

**Která organizace bude zodpovědná za každodenní správu provozu pro tuto úlohu?**

## <a name="cloud-tenancy"></a>Cloudové architektury

U většiny firem je správa jednodušší, pokud jsou všechny assety umístěny v jednom tenantovi. Některé organizace ale můžou potřebovat udržovat víc tenantů. Článek o [centralizaci operací správy pomocí Azure Lighthouse](../centralize-operations.md) nabízí několik příkladů, kdy podniky můžou vyžadovat víceklientské prostředí Azure.

**Bude tato úloha umístěná v jednom tenantovi Azure, společně se všemi ostatními úlohami?**

## <a name="soft-cost-factors"></a>Měkké náklady

V další části tohoto článku najdete postup srovnávacích přístupů spojených s úrovněmi procesů a nástrojů správy. Na konci této části se každou analyzovanou úlohu měří náklady na správu vzhledem k předpokládanému dopadu na narušení podniku. Tento přístup vám poskytne poměrně snadný způsob, jak pochopit, jestli je investice do rozsáhlejšího řízení přístupná.

Než začnete s čísly, je důležité se podívat na faktory měkkého nákladu. Měkké náklady vyvolávají návrat, ale toto vrácení je obtížné změřit prostřednictvím přímých úspor za cenu, která by byla viditelná v rámci výkazu zisků a ztrát. Měkké náklady jsou důležité, protože mohou znamenat nutnost investovat do vyšší úrovně správy, než je fiskální – obezřetné.

Mezi tyto faktory patří několik příkladů:

- Každodenní využití úlohy prostřednictvím senátu nebo generálního ředitele.
- Využití úlohy od nejlepších _x%_ zákazníků, kteří vedou k vyššímu dopadu na výnosy jinde.
- Dopad na spokojenost zaměstnanců.

Dalším datovým bodem, který je nutný k vytvoření závazku, je seznam faktorů s měkkými náklady. V této fázi je nemusíte zdokumentovat, ale obchodní zúčastnění by měli znát důležitost těchto faktorů a jejich vyloučení z následujících výpočtů.

## <a name="calculate-loss-avoidance-roi"></a>Vypočítat návratnost ztrát v případě výpadků

Při výpočtu relativního návratu na náklady na správu provozu by IT tým zodpovědný za cloudové operace měl dokončit výše uvedené požadavky a předpokládat minimální úroveň správy pro všechny úlohy.

Další závazek, který se má provést, je přijetí za firmy nákladů spojených s nabídkou spravovanou na základě směrného plánu.

**Souhlasí obchodní oddělení investovat v rámci základní nabídky, aby splnila minimální standardy cloudových operací?**

Pokud podnik nesouhlasí s touto úrovní správy, je nutné navrhnout řešení, které umožní podniku pokračovat, aniž by to mělo vliv na cloudové operace jiných úloh.

Pokud firma požaduje více než úroveň Standard, pak zbývající část této části pomůže ověřit, jestli investice a související návratnost (ve formě předcházení ztrátám).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Zvýšené úrovně správy: Principy návrhu a katalog služeb

Pro spravovaná řešení je k dispozici několik principů návrhu a řešení šablon, která lze použít společně se směrným plánem správy. Jednotlivé zásady návrhu pro spolehlivost a odolnost zvyšují provozní náklady na zatížení. Pro IT a firmy, které souhlasíte s těmito dodatečnými závazky, je důležité pochopit potenciální ztráty, které je možné vyhnout prostřednictvím této zvýšené investice.

Následující výpočty vám pomůžou porovnat vzorce a lépe porozumět porovnání ztrát a zvýšení investic do správy. Pokyny k výpočtu nákladů na zvýšenou správu najdete v článcích o [automatizaci úloh](./workload.md) a [automatizaci platforem](./platform.md).

> [!TIP]
> Pro uživatele, kteří používají [Sešit pro správu OPS](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) k naplánování správy cloudu, by se měla aktualizovat pole správy OPS tak, aby odrážela jednotlivé konverzace. Mezi tato pole patří úroveň závazku, složená smlouva SLA a měsíční náklady. Měsíční náklady by měly představovat náklady na přidané nástroje provozní správy měsíčně. Po aktualizaci budou tato pole aktualizovat vzorce návratnosti investic a každé z následujících polí.

### <a name="estimate-outage-hours-per-year"></a>Odhadnout výpadek (hodiny za rok)

"Složenou smlouvou SLA" je smlouva o úrovni služeb založená na nasazení jednotlivých assetů v rámci úlohy. Toto pole bude označovat "odhadovaný výpadek" (označený jako EST. Výpadek * * * v sešitu). Chcete-li vypočítat odhadované výpadky v hodinách za rok bez použití sešitu, použijte následující vzorec:

**Odhadované výpadky = (1 – složený procentní podíl smlouvy SLA)/* počet hodin v roce* *

V sešitu je použita výchozí hodnota 8 760 hodin za rok.

### <a name="standard-loss-impact"></a>Dopad na standardní ztrátu

Dopad na standardní ztráty (s názvem "standardní dopad") předpovídá finanční dopad jakéhokoli výpadku za předpokladu, že předpověď "odhadované výpadky" prokáže přesnou přesnost. K výpočtu této prognózy bez použití sešitu použijte následující vzorec:

**Standardní dopad = odhadované výpadky @ z doby provozu* /času/hodnoty dopadu* *

Tato možnost slouží jako základ pro náklady, pokud se obchodní účastníci rozhodnou investovat do vyšší úrovně správy.

### <a name="composite-sla-impact"></a>Složený dopad na smlouvu SLA

Složený dopad smlouvy SLA (s názvem "dopad na úroveň závazku" v sešitu) poskytuje aktualizovaný daňový dopad na základě změn v rámci smlouvy SLA pro dobu provozu. To vám umožní porovnat plánovaný finanční dopad obou možností. Chcete-li vypočítat tento předpokládaný dopad bez tabulky, použijte následující vzorec.

**Složený dopad na smlouvu SLA = odhadovaný výpadek* , čas/hodnota* , * dopad

Hodnota představuje potenciální ztráty, které se mají vyvarovat od změněné úrovně závazku a nové složené smlouvy SLA.

### <a name="comparison-basis"></a>Základ porovnání

Srovnávací základ vyhodnocuje standardní dopad a složený dopad smlouvy SLA, aby bylo možné určit, který z nich je nejvhodnější ve sloupci vráceno.

### <a name="return-on-loss-avoidance"></a>Vyloučení při výpadku ztráty

Pokud náklady na správu zatížení překročí potenciální ztráty, pak navrhovaná investice do správy cloudu nemusí být ovocná. Chcete-li porovnat "návratnost při ztrátě ztráty", podívejte se na sloupec označený "roční návratnost investic * * * *". Pokud chcete tento sloupec vypočítat sami, použijte tento vzorec:

**Nevracení ztrát při ztrátě = (porovnání základů – (měsíční náklady/* 12))//(měsíční náklady/* 12)) **

Pokud neexistují žádné další faktory, které by bylo potřeba vzít v úvahu, může toto porovnání rychle navrhnout, jestli by existovala hlubší investice do cloudových operací, odolnosti, spolehlivosti a dalších oblastí.

## <a name="validate-the-commitment"></a>Ověřit závazek

V tomto okamžiku se v tomto procesu přijaly závazky: Centralizovaná nebo delegovaná odpovědnost, Azure tenantů a úroveň závazku.
Každý závazek by se měl ověřit a zdokumentovat, aby se zajistilo, že je tým cloudových operací, tým cloudové strategie a obchodní účastníci zarovnaný k tomuto závazku spravovat úlohy.

## <a name="next-steps"></a>Další kroky

Po provedení závazků můžou příslušné provozní týmy začít s konfigurací pro příslušné úlohy. Pokud chcete začít, vyhodnoťte různé přístupy k [inventarizaci a viditelnosti](./inventory.md).

> [!div class="nextstepaction"]
> [Možnosti inventarizace a viditelnosti](./inventory.md)
