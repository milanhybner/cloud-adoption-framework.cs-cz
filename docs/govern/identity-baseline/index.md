---
title: Disciplína standardních hodnot identit
description: Vysvětlení standardních hodnot identit ve vztahu k zásadám správného řízení v cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 1ac3041abc6e4721366f8270ce37d6bf6885b140
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806182"
---
# <a name="identity-baseline-discipline-overview"></a>Disciplína standardních hodnot identit

Standardní hodnoty identit jsou jednou z [pěti disciplín zásad správného řízení v cloudu](../governance-disciplines.md) v rámci [modelu zásad správného řízení architektury přechodu na cloud](../index.md). Identita je stále více považována za primární ochranný prvek pro zabezpečení cloudu, což představuje posun od tradičního zaměření na zabezpečení sítě. Služby identit poskytují základní mechanismy podporující řízení přístupu a organizaci v rámci IT prostředí a disciplína standardních hodnot identit doplňuje [disciplínu standardních hodnot zabezpečení](../security-baseline/index.md) konzistentním aplikováním požadavků na ověřování a autorizaci v rámci snahy o přechod na cloud.

> [!NOTE]
> Zásady správného řízení standardních hodnot identit nenahrazují stávající IT týmy, procesy a postupy, které vaší organizaci umožňují spravovat a zabezpečovat služby identit. Primárním účelem této disciplíny je identifikovat potenciální obchodní rizika souvisejících s identitami a poskytnout IT pracovníkům, kteří mají na starosti implementaci, údržbu a provoz vaší infrastruktury pro správu identit, pokyny ke zmírnění rizik. Při vývoji zásad a procesů správného řízení nezapomeňte do procesů plánování a kontroly zahrnout příslušné IT týmy.

Tato část architektury přechodu na cloud popisuje přístup k vývoji disciplíny standardních hodnot identit jako součásti vaší strategie zásad správného řízení v cloudu. Primární cílovou skupinou pro tyto pokyny jsou cloudoví architekti a další členové týmu zásad správného řízení v cloudu ve vaší organizaci. Na diskuzích o rozhodnutích, zásadách a procesech, které vzejdou z této disciplíny, by se však měli podílet i relevantní členové IT týmů, které mají na starosti implementaci a správu řešení správy identit ve vaší organizaci.

Pokud vaše organizace nemá interní specialisty na standardní hodnoty identit a zabezpečení, zvažte zapojení externích konzultantů do této disciplíny. Při diskuzích o aspektech této disciplíny zvažte také využití [konzultačních služeb Microsoftu](https://www.microsoft.com/enterprise/services), služby přechodu na cloud [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) nebo jiných externích partnerů pro přechod na cloud.

## <a name="policy-statements"></a>Příkazy zásad

Jako základ disciplíny standardních hodnot identit slouží užitečná prohlášení o zásadách a požadavky na výslednou architekturu. Ukázky prohlášení o zásadách najdete v článku věnovaném [prohlášením o zásadách standardních hodnot identit](./policy-statements.md). Tyto ukázky můžou sloužit jako výchozí bod pro zásady správného řízení vaší organizace.

> [!CAUTION]
> Ukázkové zásady vycházejí z běžných zkušeností zákazníků. Pokud chcete tyto zásady lépe sladit s konkrétními požadavky na zásady správného řízení v cloudu, provedením následujících kroků můžete vytvořit prohlášení o zásadách, která splní vaše jedinečné obchodní potřeby.

## <a name="develop-governance-policy-statements"></a>Vývoj prohlášení o zásadách správného řízení

Následujících šest kroků nabízí příklady a potenciální možnosti ke zvážení při vývoji zásad správného řízení standardních hodnot identit. Jednotlivé kroky můžete použít jako výchozí body pro diskuze s vaším týmem zásad správného řízení v cloudu a ovlivněnými obchodními a IT týmy v rámci vaší organizace za účelem vytvoření požadovaných zásad a procesů správy rizik spojených s identitami.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Šablona standardních hodnot identit</h3>
                        <p class="x-hidden-focus">Možnost stažení šablony pro dokumentaci disciplíny standardních hodnot identit</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li><li style="display: flex; flex-direction: column;">
    <a href="./business-risks.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Obchodní rizika</h3>
                        <p class="x-hidden-focus">Vysvětlení motivů a rizik běžně spojovaných s disciplínou standardních hodnot identit</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./metrics-tolerance.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indikátory a metriky</h3>
                        <p class="x-hidden-focus">Indikátory umožňující poznat, jestli je správný čas investovat do disciplíny standardních hodnot identit</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./compliance-processes.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Procesy dodržování zásad</h3>
                        <p class="x-hidden-focus">Navrhované procesy pro zajištění podpory dodržování zásad v disciplíně standardních hodnot identit</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./discipline-improvement.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Vyspělost</h3>
                        <p class="x-hidden-focus">Sladění vyspělosti správy cloudu s fázemi přechodu na cloud</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./toolchain.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Sada nástrojů</h3>
                        <p class="x-hidden-focus">Služby Azure, které je možné implementovat za účelem zajištění podpory disciplíny standardních hodnot identit</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Další kroky

Začněte vyhodnocením [obchodních rizik](./business-risks.md) v konkrétním prostředí.

> [!div class="nextstepaction"]
> [Principy obchodních rizik](./business-risks.md)
