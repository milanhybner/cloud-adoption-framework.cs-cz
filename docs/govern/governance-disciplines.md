---
title: Pět disciplín zásad správného řízení v cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s pěti disciplínami zásad správného řízení cloudu v architektuře pro přijetí v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: e162dd4aad284d7de430a2483ccda04b99e21dd3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027711"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Pět disciplín zásad správného řízení v cloudu

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsI">
    <li style="display: flex; flex-direction: column;">
        <div class="cardSize">
            <div class="cardPadding" style="padding-bottom:10px;">
                <div class="card" style="padding-bottom:10px;">
                    <div class="cardText" style="padding-left:0px;">
Jakékoli změny obchodních procesů nebo technologických platforem přináší riziko. Týmu zásad správného řízení cloudu, jejichž členové se někdy označují jako cloudová starají, jsou tato rizika spojená s omezením těchto rizik a zajištěním minimálního přerušení pro úsilí na přijetí nebo inovaci.<br/><br/>Model zásad správného řízení v cloudu vás provede jednotlivými rozhodnutími (bez ohledu na zvolenou cloudovou platformu), a to zaměřením na <a href="./corporate-policy.md">vývoj podnikových zásad</a> a <a href="#disciplines-of-cloud-governance">pět oborů řízení cloudu</a>. <a href="./guides/index.md">Akční vodítko</a> , které je možné využít k tomu, ukazují tento model pomocí služeb Azure. Seznamte se s disciplínami modelu zásad správného řízení v rámci cloudu.
                    </div>
                </div>
            </div>
        </div>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="../_images/operational-transformation-govern-highres.png" style="display: flex; flex-direction: column; flex: 1 0 auto;">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardText" style="padding-left:0px;">
    <img src="../_images/operational-transformation-govern-highres.png" alt="Diagram of the Cloud Adoption Framework governance model: Corporate policy and governance disciplines">
    <br>
    <i>Obrázek 1: diagram podnikových zásad a pět oborů řízení cloudu.</i>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="disciplines-of-cloud-governance"></a>Pravidla zásad správného řízení cloudu

U jakékoli cloudové platformy existují běžné disciplíny zásad správného řízení, které vám pomůžou s informování zásad a zarovnávání sady nástrojů. Tyto disciplíny se seznámí s rozhodováním o správné úrovni automatizace a vynucování podnikových zásad napříč cloudovou platformou.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsA">
<li style="display: flex; flex-direction: column;">
    <a href="./cost-management/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/cost-management.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Cost Management</h3>
                        <p>Náklady jsou zásadním problémem pro uživatele cloudu. Vývoj zásad pro řízení nákladů pro všechny cloudové platformy.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./security-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/security-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Standardní hodnoty zabezpečení</h3>
                        <p>Zabezpečení je složité téma, které je jedinečné pro jednotlivé společnosti. Jakmile se naváže požadavky na zabezpečení, zásady zásad správného řízení cloudu a vynucení tyto požadavky použijí napříč konfigurací sítě, dat a prostředků.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./identity-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/identity-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Standardní hodnoty identit</h3>
                        <p>Nekonzistence v aplikaci požadavků na identitu můžou zvýšit riziko narušení. V rámci směrného plánu identity se zaměřujeme na to, aby se identita konzistentně používala při jejich úsilí.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./resource-consistency/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/resource-consistency.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Konzistence prostředků</h3>
                        <p>Cloudové operace závisí na konzistentní konfiguraci prostředků. Prostřednictvím nástrojů pro správu zásad správného řízení se prostředky dají konzistentně konfigurovat pro správu rizik spojených s připojováním, unášeným, zjistitelným a obnovením.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./deployment-acceleration/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/deployment-acceleration.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Zrychlení nasazení</h3>
                        <p>Centralizace, standardizace a konzistence v přístupech k nasazení a konfiguraci zlepšují postupy zásad správného řízení. Pokud poskytujete cloudové nástroje pro zásady správného řízení, vytvoří cloudový faktor, který dokáže zrychlit aktivity nasazení.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->
