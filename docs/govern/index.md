---
title: Zásady správného řízení v architektuře přechodu na cloud pro Azure od Microsoftu
description: Využijte architekturu přechodu na cloud pro Azure a naučte se hodnotit stávající zásady, vytvářet počáteční základ zásad správného řízení a iterativně přidávat nástroje pro zásady správného řízení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 75b2269c4db348ab6a110309490187ef44b55f6c
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706927"
---
# <a name="governance-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Zásady správného řízení v architektuře přechodu na cloud pro Azure od Microsoftu

Cloud vytváří nová paradigmata pro technologie podporujících podnikání. Tato nová paradigmata také mění způsoby, jakým se tyto technologie přijímají, spravují a řídí. Když je možné pomocí jediného řádku kódu spuštěného z bezobslužného procesu virtuálně strhnout a znovu postavit celá datacentra, musíme se znovu zamyslet nad tradičními přístupy. To platí hlavně pro zásady správného řízení.

## <a name="get-started-with-cloud-governance"></a>Začínáme se zásadami správného řízení v cloudu

Zásady správného řízení v cloudu představují iterativní proces. U organizací, které již využívají zásady pro řízení místních prostředí IT, by zásady správného řízení v cloudu měly tyto zásady doplňovat. Úroveň integrace firemních zásad mezi místním prostředím a cloudem se však bude lišit v závislosti na vyspělosti zásad správného řízení v cloudu a digitálních aktivech v cloudu. S tím, jak se v průběhu času mění cloudová aktiva, se současně mění i procesy a zásady správného řízení v cloudu. Následující cvičení vám pomůžou začít sestavovat počáteční základ zásad správného řízení.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./methodology.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Metodologie</h3>
Zajistěte základní porozumění metodologii, která v rámci architektury přechodu na cloud určuje zásady správného řízení v cloudu, a začněte promýšlet koncové řešení.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./benchmark.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Srovnávací test</h3>
Zhodnoťte aktuální a budoucí stav a vytvořte vizi pro použití této architektury.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./initial-foundation.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Základ počátečních zásad správného řízení</h3>
Začněte svou cestu zásad správného řízení s malou, snadno implementovanou sadou nástrojů zásad správného řízení. Tento počáteční základ zásad správného řízení se označuje jako minimální realizovatelný produkt (MVP – Minimum Viable Product).
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./foundation-improvements.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Vylepšení počátečních základních zásad správného řízení</h3>
Během implementace plánu přechodu na cloud postupně přidávejte kontroly zásad správného řízení umožňující reagovat na konkrétní rizika při postupu ke koncovému stavu.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="objective-of-this-content"></a>Cíle tohoto obsahu

Pokyny v této části architektury přechodu na cloud slouží dvěma účelům:

- Poskytnout zákazníkům příklady praktických průvodců zásadami správného řízení představující běžná prostředí, se kterými se často setkávají. Každý příklad zahrnuje obchodní rizika, firemní zásady pro omezení rizik a pokyny k návrhu pro implementaci technických řešení. Pokyny k návrhu jsou nutně specifické pro Azure. Veškerý další obsah v těchto průvodcích je možné využít v rámci přístupu nezávislého na konkrétním cloudu nebo přístupu s více cloudy.
- Pomáhat při vytváření přizpůsobených řešení zásad správného řízení, která splňují nejrůznější obchodní potřeby. Tyto potřeby zahrnují zásady správného řízení několika veřejných cloudů prostřednictvím podrobných pokynů k vývoji firemních zásad, procesů a nástrojů.

Tento obsah je určený pro použití týmem zásad správného řízení v cloudu. Je relevantní také pro cloudové architekty, kteří potřebují vyvinout pevný základ zásad správného řízení v cloudu.

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Obsah v architektuře přechodu na cloud má vliv na obchodní aktivity, technologie a kulturu podniků. Tato část architektury přechodu na cloud se bude ve velké míře věnovat vedoucím pracovníkům v oblasti zabezpečení IT, zásad správného řízení IT, financí a obchodu a týmům starajícím se o sítě, identity a přechod na cloud. Mezi těmito osobami existují různé závislosti a cloudoví architekti využívající tyto pokyny proto budou muset zvolit přístup, který je usnadní. Usnadnění pro tyto týmy může být jednorázové. V některých případech budou interakcím s těmito dalšími osobami pokračovat.

Cloudový architekt slouží jako vizionář a zprostředkovatel, který má tyto cílové skupiny dát dohromady. Obsah v této kolekci průvodců je určený k tomu, aby cloudovým architektům pomohl usnadnit správnou konverzaci se správnou cílovou skupinou, která umožní přijetí nezbytných rozhodnutí. Obchodní transformace, kterou umožňuje cloud, závisí na schopnosti cloudového architekta pomáhat s přijímáním obchodních a IT rozhodnutí.

**Specializace cloudových architektů v této části:** Jednotlivé části architektury přechodu na cloud představují různé specializace nebo varianty role cloudových architektů. Tato část architektury přechodu na cloud je určená pro cloudové architekty, kteří se zajímají o zmírňování nebo omezování technických rizik. Někteří poskytovatelé cloudu tyto odborníky označují jako *správce cloudu*, ale my dáváme přednost označení *strážci cloudu* nebo souhrnné označení *tým zásad správného řízení v cloudu*. V každém praktickém průvodci zásadami správného řízení najdete články, které ukazují, jak se složení a role týmu zásad správného řízení v cloudu můžou v průběhu času měnit.

## <a name="use-this-guide"></a>Použití tohoto průvodce

Pokud chcete postupovat podle tohoto průvodce od začátku do konce, tento obsah vám pomůže s vytvořením robustní strategie zásady správného řízení v cloudu paralelně s implementací cloudu. Pokyny vás provedou teorií a implementací takové strategie.

Pokud chcete bleskový kurz teorie a rychlý přístup k implementaci Azure, začněte [přehledem průvodců zásadami správného řízení](./guides/index.md). Pomocí těchto pokynů můžete začít v malém a souběžně s přechodem na cloud postupně vylepšovat své požadavky na zásady správného řízení.

## <a name="next-steps"></a>Další kroky

Zajistěte základní porozumění metodologii, která v rámci architektury přechodu na cloud určuje zásady správného řízení v cloudu.

> [!div class="nextstepaction"]
> [Seznámení s metodologií](./methodology.md)
