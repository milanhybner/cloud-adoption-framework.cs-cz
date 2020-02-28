---
title: Průvodci zásadami správného řízení v cloudu
description: Projděte si průvodce zásadami správného řízení v cloudu, které ilustrují osvědčené postupy pro inkrementální přístup k jakémukoli scénáři zásad správného řízení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 51f24653998ab3cd4cf7fd043b487e4d7c1ccc5b
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709222"
---
# <a name="cloud-governance-guides"></a>Průvodci zásadami správného řízení v cloudu

Praktičtí průvodci zásadami správného řízení v této části ukazují inkrementální přístup modelu zásad správného řízení architektury přechodu na cloud (CAF), který vychází z dříve popsané [metodologie zásad správného řízení](../methodology.md). Můžete si vytvořit agilní přístup k zásadám správného řízení v cloudu, který se bude rozšiřovat tak, aby splňoval požadavky libovolného scénáře zásad správného řízení v cloudu.

## <a name="review-and-adopt-cloud-governance-best-practices"></a>Kontrola a aplikace osvědčených postupů zásad správného řízení v cloudu

Pokud chcete zahájit cestu přechodu na cloud, vyberte si jednoho z následujících průvodců zásadami správného řízení. Každý průvodce uvádí řadu osvědčených postupů, a to na základě zkušeností několika fiktivních zákazníků. Čtenáři, kteří s inkrementálním přístupem modelu zásad správného řízení architektury přechodu na cloud teprve začínají, by si měli přečíst následující obecný úvod do teorie zásad správného řízení, a teprve potom aplikovat některou sadu osvědčených postupů.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Standardní průvodce zásadami správného řízení</h3>
                        <p>Průvodce pro většinu organizací vycházející z doporučeného modelu dvou předplatných, který je navržený pro nasazení v několika oblastech, ale nepokrývá veřejné a suverénní cloudy a cloudy pro státní správu</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Průvodce zásadami správného řízení pro komplexní firmy</h3>
                        <p>Průvodce pro firmy, které spravuje několik nezávislých obchodních jednotek IT nebo které využívají veřejné a suverénní cloudy a cloudy pro státní správu</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="an-incremental-approach-to-cloud-governance"></a>Inkrementální přístup k zásadám správného řízení v cloudu

## <a name="choose-a-governance-guide"></a>Volba průvodce zásadami správného řízení

Tito průvodci předvádějí, jak implementovat MVP zásad správného řízení. Dál ukazují, jak tým zásad správného řízení v cloudu může pracovat v předstihu před týmy přechodu na cloud a stát se partnerem pro zrychlení tohoto úsilí. Model zásad správného řízení architektury přechodu na cloud prostřednictvím následných vylepšení a rozvoje řídí aplikaci zásad správného řízení od základů.

Pokud chcete zahájit cestu k zásadám správného řízení v cloudu, zvolte si jednu ze dvou možností uvedených níž. Tyto možnosti jsou založené na syntéze zkušeností zákazníků. Jejich názvy jsou pro zjednodušení odvozené od složitosti firem. Rozhodování čtenáře ale může být složitější. Rozdíly mezi těmito dvěma možnostmi popisují následující tabulky.

> [!WARNING]
> Situace může vyžadovat robustnější výchozí bod zásad správného řízení. V takových případech zvažte přístup [Virtuální datové centrum Azure](#azure-virtual-datacenter), který je stručně popsaný [níž](#azure-virtual-datacenter). Tento přístup se během úsilí o přechod na podnikové úrovni navrhuje běžně, zejména v případech s více než 10 000 prostředky. Je to také faktická volba pro komplexní scénáře zásad správného řízení, kdy se vyžaduje zajištění dodržování předpisů třetích stran ve velkém objemu, hluboké znalosti domén nebo parita s vyspělými zásadami správného řízení IT a požadavky dodržování předpisů.

<!-- markdownlint-disable MD028 -->

> [!NOTE]
> Je nepravděpodobné, že by některý z průvodců kompletně odpovídal vaší situaci. Vyberte si nejpodobnější z nich a použijte ho jako výchozí bod. V rámci průvodce získáte další informace, které vám pomohou přizpůsobit vaše rozhodnutí tak, aby odpovídala konkrétním kritériím.

### <a name="business-characteristics"></a>Obchodní charakteristika

| Charakteristika | Standardní organizace | Komplexní firma |
|---|---|---|
| Geografická oblast (země nebo geopolitická oblast) | Zákazníci nebo zaměstnanci sídlí převážně v jedné geografické oblasti. | Zákazníci nebo zaměstnanci sídlí v několika geografických oblastech nebo vyžadují suverénní cloudy. |
| Dotčené obchodní jednotky | Obchodní jednotky, které sdílejí společnou infrastrukturu IT | Několik obchodních jednotek, které nesdílejí společnou infrastrukturu IT |
| Rozpočet pro IT | Jeden rozpočet | Rozpočet přidělený napříč obchodními jednotkami a měnami |
| Investice do IT | Investiční náklady se plánují pro jednotlivé roky a zpravidla zahrnují jenom základní údržbu. | Investiční náklady se plánují pro jednotlivé roky a zpravidla zahrnují údržbu a cyklus obnovení během tří až pěti let. |

### <a name="current-state-before-adopting-cloud-governance"></a>Aktuální stav před přijetím zásad správného řízení v cloudu

| Stav | Standardní firma | Komplexní firma |
|---|---|---|
| Datové centrum nebo poskytovatelé hostingových služeb třetích stran | Méně než pět datových center | Více než pět datových center |
| Sítě | Bez sítě WAN nebo 1 až 2 poskytovatelé WAN | Složitá síť nebo globální síť WAN |
| Identita | Jedna doménová struktura, jedna doména. | Komplexní, několik doménových struktur, několik domén. |

### <a name="desired-future-state-after-incremental-improvement-of-cloud-governance"></a>Požadovaný budoucí stav po postupné vylepšování zásad správného řízení cloudu

| Stav | Standardní organizace | Komplexní firma |
|---|---|---|
| Správa nákladů – účtování cloudu | Model showback. Fakturace je centralizovaná prostřednictvím IT. | Model chargeback. Fakturace se dá distribuovat prostřednictvím zajišťování IT. |
| Standardní hodnoty zabezpečení – chráněná data | IP adresy a finanční data společnosti. Omezená zákaznická data. Bez požadavků na dodržování předpisů třetích stran. | Více kolekcí finančních a osobních dat zákazníků. Může být potřeba brát v úvahu dodržování předpisů třetích stran. |

## <a name="azure-virtual-datacenter"></a>Virtuální datové centrum Azure

Virtuální datové centrum Azure je přístup, který umožňuje využít možnosti cloudové platformy Azure na maximum a současně respektovat požadavky firmy na zásady správného řízení a zabezpečení.

V porovnání s tradičními místními prostředími Azure umožňuje týmům vývoje úloh a jejich investorům, aby využívali výhod vyšší flexibility nasazení, kterou cloudové platformy nabízejí. Současně s tím, jak se úsilí o přechod na cloud rozšiřuje a začíná zahrnovat klíčová data a úlohy, může ale tato flexibilita představovat konflikt s firemními požadavky na zabezpečení a dodržování zásad, které nastavily týmy IT. To platní zejména pro velké společnosti, které už mají propracované požadavky vyplývající ze zákonů a předpisů.

Cílem virtuálního datového centra Azure je vyřešit tyto aspekty v dřívějších fázích přechodu na cloud, a to poskytnutím modelů, referenčních architektur, ukázkových artefaktů automatizace a pokynů, které pomohou zajistit rovnováhu mezi požadavky zásad správného řízení vývojářů a IT v rámci celého procesu přechodu na cloud. Základem tohoto přístupu je samotná koncepce virtuálního datového centra: implementace izolovaných hranic kolem cloudové infrastruktury využitím kontrolních mechanismů zabezpečení a přístupu, síťových zásad a monitorování dodržování předpisů.

Na virtuální datové centrum můžete nahlížet jako na váš vlastní izolovaný cloud na platformě Azure, který integruje procesy správy, požadavky vyplývající ze zákonů a předpisů a procesy zabezpečení vyžadované vašimi zásadami správného řízení. V rámci této virtuální hranice virtuální datové centrum Azure nabízí ukázkové modely pro nasazování úloh se současným zajištěním konzistentního dodržování předpisů a poskytuje základní pokyny k implementaci oddělení rolí a odpovědností v cloudu.

### <a name="azure-virtual-datacenter-assumptions"></a>Předpoklady pro virtuální datové centrum Azure

Přestože z modelů a doporučení, které virtuální datové centrum Azure poskytuje, mohou těžit i menší týmy, tento přístup je určený pro podniková oddělení IT spravující rozsáhlá cloudová prostředí. To, aby vaše organizace při návrhu cloudové infrastruktury založené na Azure uvážila konzultaci pokynů pro virtuální datové centrum Azure, se doporučuje v případě, že splňuje následující kritéria:

- Vaše firma musí splňovat požadavky dodržování legislativních předpisů, které vyžadují možnosti centralizovaného monitorování a auditu.
- Musíte zajišťovat dodržování společných zásad, předpisů a centrálních možností kontroly IT nad základními službami.
- Vaše odvětví závisí na komplexní platformě, která ke svému řízení vyžaduje komplexní ovládací prvky a hluboké znalosti daného oboru. Nejběžnější je to ve velkých podnicích v rámci finančnictví, ropného a plynárenského průmyslu a výroby.
- Vaše stávající zásady správného řízení IT vyžadují přesnější shodu s existujícími funkcemi, a to i v rané fázi přechodu na cloud.

Další informace najdete na webu Architektura přechodu na cloud v části [Virtuální datové centrum Azure](../../reference/vdc.md).

## <a name="next-steps"></a>Další kroky

Zvolte jednoho z těchto průvodců:

> [!div class="nextstepaction"]
> [Průvodce zásadami správného řízení pro standardní firmy](./standard/index.md)
>
> [Průvodce zásadami správného řízení pro komplexní firmy](./complex/index.md)
