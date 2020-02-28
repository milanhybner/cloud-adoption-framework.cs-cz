---
title: Disciplína konzistence prostředků
description: Seznamte se s přístupem k vývoji disciplíny konzistence prostředků jako součásti strategie zásad správného řízení v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 93064d0c3feb8b9ee129c404e58e8d0485dcdfe5
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706961"
---
# <a name="resource-consistency-discipline-overview"></a>Disciplína konzistence prostředků

Konzistence prostředků je jednou z [pěti disciplín zásad správného řízení v cloudu](../governance-disciplines.md) v rámci [modelu zásad správného řízení architektury přechodu na cloud](../index.md). Tato disciplína se zaměřuje na způsoby vytváření zásad souvisejících s provozní správou prostředí, aplikací nebo úloh. Týmy zajišťující provoz IT často zajišťují i monitorování výkonu aplikací, úloh a prostředků. Běžně také provádějí úlohy požadované ke splnění požadavků na škálování, k nápravě porušení smlouvy SLA o výkonu a k aktivnímu předcházení porušením smlouvy SLA o výkonu prostřednictvím automatizovaných náprav. V rámci pěti disciplín zásad správného řízení v cloudu je konzistence prostředků disciplína, která zajišťuje konzistentní konfiguraci prostředků způsobem, který umožňuje jejich zjištění IT operacemi, jejich zahrnutí do řešení zotavení a možnost jejich registrace do opakovatelných provozních procesů.

> [!NOTE]
> Zásady správného řízení konzistence prostředků nenahrazují stávající IT týmy, procesy a postupy, které vaší organizaci umožňují efektivně spravovat cloudové prostředky. Primárním účelem této disciplíny je identifikovat potenciální obchodní rizika a poskytnout IT pracovníkům, kteří mají na starosti správu vašich prostředků v cloudu, pokyny ke zmírnění rizik. Při vývoji zásad a procesů správného řízení nezapomeňte do procesů plánování a kontroly zahrnout příslušné IT týmy.

Tato část architektury přechodu na cloud ukazuje, jak si v rámci strategie zásad správného řízení v cloudu osvojit disciplínu konzistence prostředků. Primární cílovou skupinou pro tyto pokyny jsou cloudoví architekti a další členové týmu zásad správného řízení v cloudu ve vaší organizaci. Na diskuzích o rozhodnutích, zásadách a procesech, které vzejdou z této disciplíny, by se však měli podílet i relevantní členové IT týmů, které mají na starosti implementaci a správu řešení konzistence prostředků ve vaší organizaci.

Pokud vaše organizace nemá interní specialisty na strategie konzistence prostředků, zvažte zapojení externích konzultantů do této disciplíny. Zvažte také využití [konzultačních služeb Microsoftu](https://www.microsoft.com/enterprise/services), služby přechodu na cloud [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) nebo jiných externích odborníků na přechod na cloud a zjistěte, jak co nejlépe uspořádat, sledovat a optimalizovat cloudové prostředky.

## <a name="policy-statements"></a>Příkazy zásad

Jako základ disciplíny konzistence prostředků slouží užitečná prohlášení o zásadách a požadavky na výslednou architekturu. Ukázky prohlášení o zásadách najdete v článku věnovaném [prohlášením o zásadách konzistence prostředků](./policy-statements.md). Tyto ukázky můžou sloužit jako výchozí bod pro zásady správného řízení vaší organizace.

> [!CAUTION]
> Ukázkové zásady vycházejí z běžných zkušeností zákazníků. Pokud chcete tyto zásady lépe sladit s konkrétními požadavky na zásady správného řízení v cloudu, provedením následujících kroků můžete vytvořit prohlášení o zásadách, která splní vaše jedinečné obchodní potřeby.

## <a name="develop-governance-policy-statements"></a>Vývoj prohlášení o zásadách správného řízení

Následujících šest kroků nabízí příklady a potenciální možnosti ke zvážení při vývoji zásad správného řízení konzistence prostředků. Jednotlivé kroky můžete použít jako výchozí body pro diskuze s vaším týmem zásad správného řízení v cloudu a ovlivněnými obchodními a IT týmy v rámci vaší organizace za účelem vytvoření požadovaných zásad a procesů správy rizik spojených s konzistencí prostředků.

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
                        <h3>Šablona konzistence prostředků</h3>
                        <p class="x-hidden-focus">Možnost stažení šablony pro dokumentaci disciplíny konzistence prostředků</p>
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
                        <p class="x-hidden-focus">Vysvětlení motivů a rizik běžně spojovaných s disciplínou konzistence prostředků</p>
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
                        <p class="x-hidden-focus">Indikátory umožňující poznat, jestli je správný čas investovat do disciplíny konzistence prostředků</p>
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
                        <p class="x-hidden-focus">Navrhované procesy pro zajištění podpory dodržování zásad v disciplíně konzistence prostředků</p>
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
                        <p class="x-hidden-focus">Služby Azure, které je možné implementovat za účelem zajištění podpory disciplíny konzistence prostředků</p>
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
