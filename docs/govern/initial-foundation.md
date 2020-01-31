---
title: Navázat počáteční cloudový základ zásad správného řízení
description: Začínáme se zásadami správného řízení cloudu vytvořením počátečního základu zásad správného řízení pro Cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 290bffadc608d8ff9d593e5231242e3555732bf3
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803785"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Navázat počáteční cloudový základ zásad správného řízení

Vytváření zásad správného řízení cloudu je široké iterativní úsilí. Je náročné zamezit efektivní rovnováhu mezi rychlostí a řízením, zejména při počátečních fázích přijetí cloudu. Pokyny pro zásady správného řízení v rozhraní pro přijetí do cloudu pomáhají poskytnout tuto rovnováhu prostřednictvím agilního přístupu k přijetí.

Tento článek poskytuje dvě možnosti, jak vytvořit počáteční základ pro řízení. Jedna z možností zajišťuje, aby se omezení zásad správného řízení mohla škálovat a rozšířila, protože plán přijetí je implementovaný a požadavky jsou jasně definovány. Ve výchozím nastavení předpokládá prvotní základ izolovanou polohu a řízení. Zaměřuje se taky na organizaci prostředků, než na zásady správného řízení prostředků. Tento odlehčený počáteční bod se nazývá _minimální životaschopný produkt (MVP)_ pro řízení. Cílem MVP je snižovat překážky při stanovení počátečního stupně řízení a pak umožnit rychlé maturation řešení, aby se vyřešilo celé množství hmotných rizik.

## <a name="already-using-the-cloud-adoption-framework"></a>Už se používá architektura pro přijetí do cloudu.

Pokud jste spolu s architekturou pro přijetí v cloudu provedli následující postup, možná jste už nasadili MVP pro řízení. Doprovodné materiály k jednotlivým provozním modelům jsou základními aspekty. Je k dispozici během každé fáze životního cyklu přijetí do cloudu. V takovém případě rozhraní pro [přijetí do cloudu](../index.md) poskytuje pokyny, které vkládají zásady správného řízení do aktivit souvisejících s implementací vašeho [plánu přijetí do cloudu](../plan/index.md). Příkladem této integrace zásad správného řízení je použití plánů k nasazení jedné nebo více zón vykládku přítomných [v doprovodné dokumentaci](../ready/index.md) . Dalším příkladem jsou pokyny pro [škálování předplatných](../ready/azure-best-practices/scaling-subscriptions.md). Pokud jste postupovali s jedním z těchto doporučení, v následujících oddílech MVP jsou jenom recenze stávajících rozhodnutí o nasazení. Po rychlé kontrole přejděte k [vyspělému řešení zásad správného řízení a použijte osvědčené postupy](./foundation-improvements.md).

## <a name="establish-an-initial-governance-foundation"></a>Vytvoření počátečního základu zásad správného řízení

Níže jsou uvedeny dva různé příklady počátečních základů zásad správného řízení (označované také jako MVP MVP), pomocí kterých můžete použít pro zásady správného řízení nové nebo stávající nasazení. Vyberte si MVP, který nejlépe vyhovuje vašim obchodním potřebám, abyste mohli začít:

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./guides/standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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
    <a href="./guides/complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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

## <a name="next-steps"></a>Další kroky

Jakmile je základem zásad správného řízení, využijte vhodná doporučení pro zlepšení řešení a ochranu před riziky, která se budou uplatňovat.

> [!div class="nextstepaction"]
> [Vylepšení počátečního základu zásad správného řízení](./foundation-improvements.md)
