---
title: Povolit úspěšnou cestu k přijetí cloudu
description: Využijte bezplatné rozhraní pro přijetí do samoobslužného cloudu a další nástroje, které vám pomůžou s rozhodováním o přijetí do cloudu, která jim umožní úspěch.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: overview
layout: LandingPage
ms.openlocfilehash: c9e33b32590cd3b73e5bc42a662abf5ef6de36da
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892238"
---
# <a name="enable-success-during-a-cloud-adoption-journey"></a>Povolit úspěch během cesty k přijetí cloudu

Rozhraní pro přijetí do cloudu je bezplatný samoobslužný nástroj, který pomáhá čtenářům prostřednictvím různých úsilí o přijetí do cloudu. Architektura pomůže zákazníkům podařit při realizaci obchodních cílů, které lze povolit pomocí Microsoft Azure. Tento obsah ale také rozpoznává, že čtenář může řešit rozsáhlé podnikové, jazykové verze nebo technické výzvy a v některých případech může vyžadovat cloudovou neneutrální pozici. Proto každá část tohoto návodu začíná prvním přístupem a pak je postupuje s neutrálními platformami, které se dají škálovat v mnoha obchodních a technických rozhodnutích.

V rámci této architektury je povolený klíčový motiv. Následující kontrolní seznam rozepisuje základní zásady pro přijetí do cloudu, které zajišťují, že je cesta k přijetí v rámci IT i firmy považována za úspěšnou:

- **Plán:** Stanovení jasných [obchodních výsledků](../strategy/business-outcomes/index.md), jasně definovaného [plánu digitální nemovitosti](../digital-estate/index.md)a dobře srozumitelného [přijímání](../migrate/migration-considerations/prerequisites/migration-backlog-review.md)nevyřízených položek.
- **Připraveno:** Zajistěte připravenost pracovníků prostřednictvím [dovedností a studijních plánů](../ready/suggested-skills.md).
- **Provoz:** Definujte spravovatelný provozní model, který bude provádět činnosti během a dlouho po přijetí.
  - **[Uspořádání](../organize/index.md):** Zarovnejte lidi a týmy s cílem zajistit správné cloudové operace a přijetí.
  - **Řídit:** Přiřaďte správné [obory zásad správného řízení](../govern/index.md) , aby se konzistentně vyrovnaly řízení nákladů, zmírnění rizik, dodržování předpisů a standardních hodnot zabezpečení v rámci veškerého přijetí cloudu.
  - **Spravovat:** Průběžná [provozní Správa](../manage/index.md) portfolia IT, aby se minimalizovala přerušení podnikových procesů a zajistila se stabilita IT portfolia.
  - **Podpora:** Zarovnejte správné [partnerství a možnosti podpory](../migrate/migration-considerations/assess/partnership-options.md).

Dalším základním motivem je zabezpečení, což je důležitý atribut kvality pro úspěšné přijetí do cloudu. Zabezpečení je integrováno v rámci této architektury, aby poskytovalo integrované pokyny k zachování důvěrnosti, integrity a záruk dostupnosti pro vaše cloudové úlohy. 

## <a name="additional-tools"></a>Další nástroje

Kromě architektury pro přijetí do cloudu Microsoft pokrývá další témata, která můžou úspěšně povolit. Tento článek popisuje několik běžných nástrojů, které můžou významně zlepšit úspěšnost nad rámec rozhraní pro přijetí do cloudu. Navázání zásad správného řízení cloudu, odolných architektur, technických dovedností a přístupu DevOps jsou důležité pro úspěch jakéhokoli úsilí o přijetí do cloudu. Umožňuje označit tuto stránku jako prostředek, aby bylo možné přenavštěvovat celou cestu k přijetí do cloudu.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsH">
<li style="display: flex; flex-direction: column;">
    <a href="../govern/guides/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Cloud Adoption Framework governance model" src="../_images/operational-transformation-govern-highres.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Zásady správného řízení cloudu</h3>
                        <p>Porozumět obchodním rizikům, namapujte tato rizika na správné zásady a procesy. Použití nástrojů zásad správného řízení cloudu a pěti disciplín zásad správného řízení cloudu minimalizuje rizika a zvyšuje pravděpodobnost úspěchu. Zásady správného řízení cloudu pomáhají řídit náklady, vytvářet konzistence, zlepšovat zabezpečení a urychlují nasazení.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/framework/resiliency/overview" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Resilient architecture" src="https://docs.microsoft.com/azure/architecture/resiliency/images/redundancy.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Spolehlivá architektura (odolnost)</h3>
                        <p>Vytváření spolehlivých aplikací v cloudu se liší od tradičního vývoje aplikací. I když jste historicky koupili úrovně redundantního hardwaru s vyšším počtem, aby se minimalizovala pravděpodobnost selhání celé aplikační platformy. V cloudu potvrzuji, že dojde k selhání. Místo snahy kompletně zabránit selháním je cílem minimalizace dopadu selhání jedné komponenty.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="../ready/suggested-skills.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Build Technical Skills" src="https://docs.microsoft.com/media/learn/Product/Learn/learningpath_graphic.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Vytváření technických dovedností</h3>
                        <p>Nejlepším nástrojem pro pomoc při přijímání v cloudu je dobře vycvičený tým. Rozbalíte dovednosti stávajících členů obchodních a technických týmů a pomůžete se zaměřit na výukové postupy.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/devops/learn/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Learn DevOps" src="https://docs.microsoft.com/azure/devops/learn/_img/learn-devops.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Přístup DevOps</h3>
                        <p>Historická transformace od Microsoftu je pevně zamístoá ve růstovém přístupu k jazykové verzi a přístup DevOps k technickému provádění. Rozhraní pro přijetí do cloudu vloží do celého rozhraní. Pokud chcete zrychlit přijetí DevOps, přečtěte si obsah výukového DevOps.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Architecture Center" src="https://docs.microsoft.com/azure/architecture/example-scenario/data/media/architecture-data-warehouse.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Azure Architecture Center</h3>
                        <p>Řešení architektury, referenční architektury, ukázkové scénáře, osvědčené postupy a vzory návrhu cloudu, které pomáhají v architektuře řešení běžících na Azure.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://azure.microsoft.com/pricing/calculator/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Pricing Calculator" src="../_images/calculator-preview.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Cenová kalkulačka funkcí Azure</h3>
                        <p>Vypočítá náklady na různé komponenty Azure potřebné k vytvoření nebo migraci zvoleného řešení.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Další kroky

V ozbrojených seznámcích s tím, že je v cloudu pro přijetí aspektů důležité, pravděpodobnost úspěchu při [migraci](./migrate.md) nebo [inovacích](./innovate.md) bude mnohem vyšší.

> [!div class="nextstepaction"]
> [Migrace](./migrate.md)
>
> [Inovace](./innovate.md)
