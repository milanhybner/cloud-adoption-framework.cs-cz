---
title: Disciplína služby Cost Management
description: Seznamte se s přístupem k vývoji disciplíny správy nákladů jako součásti strategie zásad správného řízení v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: ebb0f0899ad8ea4e5f26c43b0486c56560b4dd14
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708865"
---
# <a name="cost-management-discipline-overview"></a>Disciplína služby Cost Management

Služba Cost Management je jednou z [pěti disciplín zásad správného řízení v cloudu](../governance-disciplines.md) v rámci [modelu zásad správného řízení architektury přechodu na cloud](../index.md). Pro mnoho zákazníků jsou náklady na řízení hlavním aspektem při přechodu na cloudové technologie. Vyrovnávání požadavků na výkon, stanovení rychlosti přechodu a náklady na cloudové služby můžou znamenat velkou výzvu. Obzvlášť důležité je to během zásadních obchodních transformací, které implementují cloudové technologie. Tato část popisuje přístup k vývoji disciplíny služby Cost Management jako součásti strategie zásad správného řízení v cloudu.

> [!NOTE]
> Zásady správného řízení služby Cost Management nenahrazují existující obchodní týmy, postupy účtování ani postupy používané ve finanční správě nákladů souvisejících s IT ve vaší organizaci. Primárním účelem této disciplíny je identifikovat potenciální rizika související s cloudem a týkající se nákladů na IT a poskytnout obchodním a IT týmům, které mají na starosti nasazování a správu cloudových prostředků, pokyny ke zmírnění rizik.

Primární cílovou skupinou pro tyto pokyny jsou cloudoví architekti a další členové týmu zásad správného řízení v cloudu ve vaší organizaci. Na diskuzích o rozhodnutích, zásadách a procesech, které vzejdou z této disciplíny, by se však měli podílet i relevantní členové obchodních a IT týmů, zejména vedoucí, kteří zodpovídají za vlastnictví, správu a platby za cloudové úlohy.

## <a name="policy-statements"></a>Příkazy zásad

Jako základ disciplíny služby Cost Management slouží užitečná prohlášení o zásadách a požadavky na výslednou architekturu. Ukázky prohlášení o zásadách najdete v článku věnovaném [prohlášením o zásadách služby Cost Management](./policy-statements.md). Tyto ukázky můžou sloužit jako výchozí bod pro zásady správného řízení vaší organizace.

> [!CAUTION]
> Ukázkové zásady vycházejí z běžných zkušeností zákazníků. Pokud chcete tyto zásady lépe sladit s konkrétními požadavky na zásady správného řízení v cloudu, provedením následujících kroků můžete vytvořit prohlášení o zásadách, která splní vaše jedinečné obchodní potřeby.

## <a name="develop-governance-policy-statements"></a>Vývoj prohlášení o zásadách správného řízení

Následujících šest kroků umožňuje definovat zásady správného řízení nákladů ve vašem prostředí.

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
                        <h3>Šablona služby Cost Management</h3>
                        <p class="x-hidden-focus">Možnost stažení šablony pro dokumentaci disciplíny služby Cost Management</p>
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
                        <p class="x-hidden-focus">Vysvětlení motivů a rizik běžně spojovaných s disciplínou služby Cost Management</p>
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
                        <p class="x-hidden-focus">Indikátory umožňující poznat, jestli je správný čas investovat do disciplíny služby Cost Management</p>
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
                        <p class="x-hidden-focus">Navrhované procesy pro zajištění podpory dodržování zásad v disciplíně služby Cost Management</p>
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
                        <p class="x-hidden-focus">Služby Azure, které je možné implementovat za účelem zajištění podpory disciplíny služby Cost Management</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Další kroky

Začněte vyhodnocením obchodních rizik v konkrétním prostředí.

> [!div class="nextstepaction"]
> [Principy obchodních rizik](./business-risks.md)

<!-- markdownlint-enable MD033 -->
