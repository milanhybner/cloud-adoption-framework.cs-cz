---
title: Disciplína standardních hodnot zabezpečení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Disciplína standardních hodnot zabezpečení
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: a0b0ed642e11fc3ffc81db7fd1095853a5458b1d
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565947"
---
# <a name="security-baseline-discipline-overview"></a>Disciplína standardních hodnot zabezpečení

Standardní hodnoty zabezpečení jsou jednou z [pěti disciplín zásad správného řízení v cloudu](../governance-disciplines.md) v rámci [modelu zásad správného řízení architektury přechodu na cloud](../index.md). Zabezpečení je součástí libovolného nasazení IT a cloud přináší specifické aspekty zabezpečení. Na řadu firem se vztahují zákonné požadavky, díky nimž se při zvažování cloudové transformace hlavní prioritou stává ochrana citlivých dat. Zjištění potenciálních bezpečnostních hrozeb pro vaše cloudové prostředí a nastavení procesů a procedur pro jejich řešení by mělo být prioritou pro každý tým kybernetického zabezpečení nebo zabezpečení IT. Disciplína standardních hodnot zabezpečení zajišťuje konzistentní aplikaci technických požadavků a omezení zabezpečení v cloudových prostředích tak, jak tyto požadavky vyzrávají.

> [!NOTE]
> Zásady správného řízení standardních hodnot zabezpečení nenahrazují stávající IT týmy, procesy a postupy, které vaše organizace využívá k zabezpečení prostředků nasazených do cloudu. Primárním účelem této disciplíny je identifikovat potenciální obchodní rizika související se zabezpečením a poskytnout IT pracovníkům, kteří mají na starosti infrastrukturu zabezpečení, pokyny ke zmírnění rizik. Při vývoji zásad a procesů správného řízení nezapomeňte do procesů plánování a kontroly zahrnout příslušné IT týmy.

Tento článek popisuje přístup k vývoji disciplíny standardních hodnot zabezpečení jako součásti strategie zásad správného řízení v cloudu. Primární cílovou skupinou pro tyto pokyny jsou cloudoví architekti a další členové týmu zásad správného řízení v cloudu ve vaší organizaci. Na diskuzích o rozhodnutích, zásadách a procesech, které vzejdou z této disciplíny, by se však měli podílet i relevantní členové IT týmů, zejména techničtí vedoucí, kteří zodpovídají za implementaci sítí, šifrování a správu identit.

Správná rozhodnutí ohledně zabezpečení jsou klíčem k úspěšným cloudovým nasazením a větším obchodním úspěchům. Pokud vaše organizace nemá interní specialisty na kybernetické zabezpečení, zvažte, jestli do této disciplíny nezapojit externí konzultanty. Zvažte také využití [konzultačních služeb Microsoftu](https://www.microsoft.com/enterprise/services), služby přechodu na cloud [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) nebo jiných externích odborníků na přechod na cloud při diskuzích o aspektech této disciplíny.

## <a name="policy-statements"></a>Příkazy zásad

Jako základ disciplíny standardních hodnot zabezpečení slouží praktická prohlášení o zásadách a požadavky na výslednou architekturu. Ukázky prohlášení o zásadách najdete v článku věnovaném [prohlášením o zásadách standardních hodnot zabezpečení](./policy-statements.md). Tyto ukázky můžou sloužit jako výchozí bod pro zásady správného řízení vaší organizace.

> [!CAUTION]
> Ukázkové zásady vycházejí z běžných zkušeností zákazníků. Pokud chcete tyto zásady lépe sladit s konkrétními požadavky na zásady správného řízení v cloudu, provedením následujících kroků můžete vytvořit prohlášení o zásadách, která splní vaše jedinečné obchodní potřeby.

## <a name="develop-governance-policy-statements"></a>Vývoj prohlášení o zásadách správného řízení

Následujících šest kroků nabízí příklady a potenciální možnosti ke zvážení při vývoji zásad správného řízení standardních hodnot zabezpečení. Jednotlivé kroky můžete použít jako výchozí body pro diskuze s vaším týmem zásad správného řízení v cloudu a ovlivněnými obchodními a IT týmy a týmy zabezpečení v rámci vaší organizace za účelem vytvoření požadovaných zásad a procesů správy rizik spojených se zabezpečením.

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
                        <h3>Šablona standardních hodnot zabezpečení</h3>
                        <p class="x-hidden-focus">Možnost stažení šablony pro dokumentaci disciplíny standardních hodnot zabezpečení</p>
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
                        <p class="x-hidden-focus">Vysvětlení motivů a rizik běžně spojovaných s disciplínou standardních hodnot zabezpečení</p>
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
                        <p class="x-hidden-focus">Indikátory umožňující poznat, jestli je správný čas investovat do disciplíny standardních hodnot zabezpečení</p>
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
                        <p class="x-hidden-focus">Navrhované procesy pro zajištění podpory dodržování zásad v disciplíně standardních hodnot zabezpečení</p>
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
                        <p class="x-hidden-focus">Služby Azure, které je možné implementovat za účelem zajištění podpory disciplíny standardních hodnot zabezpečení</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Další kroky

Začněte vyhodnocením obchodních rizik v konkrétním prostředí.

> [!div class="nextstepaction"]
> [Principy obchodních rizik](./business-risks.md)
