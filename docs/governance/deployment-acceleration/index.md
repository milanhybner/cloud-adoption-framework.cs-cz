---
title: Disciplína zrychlení nasazení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vysvětlení zrychlení nasazení v souvislosti se zásadami správného řízení v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 5ae0769fd40bc88673adc031b5b1aa5c7d93d4d8
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816920"
---
# <a name="deployment-acceleration-discipline-overview"></a>Disciplína zrychlení nasazení

Zrychlení nasazení je jednou z [pěti disciplín zásad správného řízení v cloudu](../governance-disciplines.md) v rámci [modelu zásad správného řízení architektury přechodu na cloud](../index.md). Tato disciplína se zaměřuje na způsoby vytváření zásad správného řízení konfigurace nebo nasazení prostředků. V rámci pěti disciplín zásad správného řízení v cloudu disciplína zrychlení nasazení zahrnuje nasazení, sladění konfigurace a opětovnou použitelnost skriptů. Může se to provádět ručními aktivitami nebo pomocí plně automatizovaných aktivit DevOps. V obou případech zůstávají zásady z velké části stejné. Během vývoje této disciplíny může tým zásad správného řízení v cloudu fungovat jako partner ve strategiích DevOps a nasazení a zrychlit nasazení a odstranit překážky přechodu na cloud díky opakovanému používání prostředků.

Tento článek vysvětluje proces zrychlení nasazení, kterým společnost prochází při plánování, vytváření, zavádění a zajišťování provozu jednotlivých fází implementace cloudového řešení. V jednom dokumentu není možné se věnovat všem požadavkům všech podniků. Jednotlivé části tohoto článku proto popisují navrhované minimální a potenciální aktivity. Cílem těchto aktivit je pomoct vám vytvořit [MVP zásad](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy), ale vytvoříte architekturu pro vylepšení [inkrementálních zásad](../policy-compliance/index.md#incremental-policy-growth). Tým zásad správného řízení v cloudu by měl určit, kolik času se má investovat do těchto aktivit s cílem zlepšit pozici z hlediska zrychlení nasazení.

> [!NOTE]
> Disciplína zrychlení nasazení nenahrazuje stávající IT týmy, procesy a postupy, které vaší organizaci umožňují efektivně vyvíjet a konfigurovat cloudové prostředky. Primárním účelem této disciplíny je identifikovat potenciální obchodní rizika a poskytnout IT pracovníkům, kteří mají na starosti správu vašich prostředků v cloudu, pokyny ke zmírnění rizik. Při vývoji zásad a procesů správného řízení nezapomeňte do procesů plánování a kontroly zahrnout příslušné IT týmy.

Primární cílovou skupinou pro tyto pokyny jsou cloudoví architekti a další členové týmu zásad správného řízení v cloudu ve vaší organizaci. Na diskuzích o rozhodnutích, zásadách a procesech, které vzejdou z této disciplíny, by se však měli podílet i relevantní členové obchodních a IT týmů, zejména vedoucí, kteří zodpovídají za nasazování a konfiguraci cloudových úloh.

## <a name="policy-statements"></a>Příkazy zásad

Jako základ disciplíny zrychlení nasazení slouží užitečná prohlášení o zásadách a požadavky na výslednou architekturu. Ukázky prohlášení o zásadách najdete v článku věnovaném [prohlášením o zásadách zrychlení nasazení](./policy-statements.md). Tyto ukázky můžou sloužit jako výchozí bod pro zásady správného řízení vaší organizace.

> [!CAUTION]
> Ukázkové zásady vycházejí z běžných zkušeností zákazníků. Pokud chcete tyto zásady lépe sladit s konkrétními požadavky na zásady správného řízení v cloudu, provedením následujících kroků můžete vytvořit prohlášení o zásadách, která splní vaše jedinečné obchodní potřeby.

## <a name="developing-deployment-acceleration-governance-policy-statements"></a>Vývoj prohlášení o zásadách správného řízení zrychlení nasazení

Následujících šest kroků vám pomůže definovat zásady správného řízení nasazování a konfigurace prostředků ve vašem cloudovém prostředí.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/governance/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Šablona zrychlení nasazení</h3>
                        <p class="x-hidden-focus">Možnost stažení šablony pro dokumentaci disciplíny zrychlení nasazení</p>
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
                            <img src="../../_images/governance/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Obchodní rizika</h3>
                        <p class="x-hidden-focus">Vysvětlení motivů a rizik běžně spojovaných s disciplínou zrychlení nasazení</p>
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
                            <img src="../../_images/governance/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indikátory a metriky</h3>
                        <p class="x-hidden-focus">Indikátory umožňující poznat, jestli je správný čas investovat do disciplíny služby zrychlení nasazení</p>
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
                            <img src="../../_images/governance/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Procesy dodržování zásad</h3>
                        <p class="x-hidden-focus">Navrhované procesy pro zajištění podpory dodržování zásad v disciplíně zrychlení nasazení</p>
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
                            <img src="../../_images/governance/process-maturity.png" class="x-hidden-focus"/>
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
                            <img src="../../_images/governance/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Sada nástrojů</h3>
                        <p class="x-hidden-focus">Služby Azure, které je možné implementovat za účelem zajištění podpory disciplíny zrychlení nasazení</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Další kroky

Začněte vyhodnocením [obchodních rizik](./business-risks.md) v konkrétním prostředí.

> [!div class="nextstepaction"]
> [Principy obchodních rizik](./business-risks.md)

<!-- markdownlint-enable MD033 -->
