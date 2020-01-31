---
title: 'Příručka pro zásady správného řízení pro komplexní podniky: podpora mluveného komentáře'
description: Tento mluvený komentář vytváří případ použití pro zásady správného řízení během cesty k podnikovému přijetí ve složitém podnikovém cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fae1940c1cc522cd917b2b0293d60b630007537c
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805553"
---
# <a name="governance-guide-for-complex-enterprises-the-supporting-narrative"></a>Příručka pro zásady správného řízení pro komplexní podniky: podpora mluveného komentáře

Následující mluvený komentář vytváří případ použití pro zásady [správného řízení během cesty k podnikovému přijetí ve složitém podnikovém cloudu](./index.md). Před jednáním s doporučeními v průvodci je důležité pochopit předpoklady a příčiny, které se projeví v tomto mluveném komentáři. Pak můžete strategii zásad správného řízení lépe sjednotit na cestu k přijetí cloudu vaší organizace.

## <a name="back-story"></a>Příběh zpátky

Zákazníci mají lepší zkušenosti při interakci s touto společností. Aktuální prostředí způsobilo narušení trhu a vedlo se na panel, aby mohl začlenit ředitele pro digitální důstojníka (CDO). Rozhraní CDO pracuje s marketingem a prodejem k zajištění digitální transformace, která bude vylepšit prostředí. Kromě toho několik obchodních jednotek nedávno odesílalo datové odborníky na data farmy a vylepšili mnoho ručních prostředí prostřednictvím učení a předpovědi. Podporuje tato úsilí, kde může. Existují však aktivity "stínové IT", které jsou k dispozici mimo nezbytné řízení a zabezpečení.

Organizace IT také čelí vlastním výzvám. Finance plánuje průběžné snižování rozpočtu IT během následujících pěti let, což vede k potřebným útratám od tohoto roku. Naopak GDPR a další požadavky na suverenitu dat vynutí, aby investovaly do prostředků v dalších zemích k lokalizaci dat. Dvě z existujících datových center jsou pro aktualizace hardwaru zpožděny, což způsobuje další problémy se spokojeností zaměstnanců a zákazníků. Tři další datová centra při spuštění plánu s pěti roky vyžadují aktualizace hardwaru. Finanční ŘEDITELka přenáší CIO, který považuje Cloud za alternativu pro tato datacentra, aby se uvolnily kapitálové výdaje.

CIO má inovativní nápady, které by mohly pomáhat společnosti, ale její týmy jsou omezené na zdolávání požárů a řízení nákladů. V luncheon s rozhraním CDO a jedním z vedoucích organizačních jednotek se konverzace migrace do cloudu vygenerovala z partnerských vztahů CIO. Tři vedoucí se zaměřují na vzájemnou podporu pomocí cloudu, aby dosáhli svých obchodních záměrů a zahájili fáze průzkumu a plánování při přijetí cloudu.

## <a name="business-characteristics"></a>Obchodní charakteristika

Společnost má následující obchodní profil:

- Prodej a operace rozkrývají několik geografických oblastí s globálními zákazníky na více trzích.
- Společnost vzrostla prostřednictvím získání a pracuje na třech obchodních jednotkách na základě cílové zákaznické základny. Rozpočtování je složitá matice napříč obchodními jednotkami a funkcemi.
- Podniková zobrazení jsou většinou velká a nákladové středisko.

## <a name="current-state"></a>Aktuální stav

Tady je aktuální stav operací IT a cloudových operací společnosti:

- Provozuje více než 20 soukromě vlastněných Datacenter po celém světě.
- Z důvodu ekologického růstu a několika geografických oblastí existuje několik týmů IT, které mají jedinečné nároky na data a dodržování předpisů, které mají vliv na jednu organizační jednotku v konkrétní zeměpisné oblasti.
- Každé datové centrum je propojeno řadou oblastí s oddělenými pronajatými řádky a vytvoří volně propojenou globální síť WAN.
- Vstoupili do cloudu migrací všech e-mailových účtů koncových uživatelů do sady Office 365. Tato migrace byla dokončena před více než šesti měsíci. Od té doby byla do cloudu nasazená jenom několik IT prostředků.
- Primární vývojový tým služby CDO pracuje na kapacitě pro vývoj a testování, kde se seznámíte s možnostmi nativního cloudu.
- Jedna obchodní jednotka experimentuje s velkými objemy dat v cloudu. V tomto úsilí se účastní tým BI uvnitř oddělení IT.
- Stávající zásady správného řízení IT stanoví, že osobní údaje a finanční údaje o zákaznících musí být hostované na assetech vlastněných přímo společností. Tato zásada blokuje přijetí cloudu pro všechny klíčové aplikace nebo chráněná data.
- Investice do IT jsou řízeny hlavně pomocí kapitálových výdajů. Tyto investice jsou plánovány roční a často zahrnují plány pro průběžnou údržbu a také zavedené aktualizační cykly o tři až pět let v závislosti na datovém centru.
- Většina investic do technologie, která se nerovnává s ročním plánem, se řeší pomocí stínového úsilí IT. Tato snaha je obvykle spravovaná obchodními jednotkami a je financována prostřednictvím provozních nákladů obchodní jednotky.

## <a name="future-state"></a>Budoucí stav

Následující změny se odhadují v následujících několika letech:

- CIO se snaží modernizovat zásadu na osobních a finančních datech, aby podporovala budoucí cíle. K tomuto úsilí mají přehled dva členové týmu IT správy.
- CIO chce použít cloudovou migraci jako vynucenou funkci ke zvýšení konzistence a stability napříč obchodními jednotkami a geografickými oblastmi. Nicméně budoucí stav musí respektovat všechny požadavky na externí dodržování předpisů, které by vyžadovaly odchylku od standardních přístupů konkrétními IT týmy.
- Pokud brzy experimenty ve vývoji aplikací a v BI ukazují přední indikátory úspěšnosti, je třeba, aby v příštích 24 měsících vyvolaly řešení malého množství produkčního prostředí do cloudu.
- CIO a CFO přiřadili architekta a viceprezidenta infrastruktury, aby vytvořila analýzu nákladů a studii proveditelnosti. Tato snaha určí, jestli společnost může a má přesunout 5 000 prostředků do cloudu během příštích 36 měsíců. Úspěšná migrace umožní, aby CIO eliminovat dvě datová centra a snížila náklady prostřednictvím 100 milionů USD během pětiletého plánu. Pokud se tři až čtyři datacentra můžou setkat s podobnými výsledky, rozpočet se vrátí na černou, takže rozpočet CIO zajistí podporu inovativních iniciativ.
    ![místní náklady a náklady na Azure, které demonstrují vrácení $100 milionů USD za další pět let](../../../_images/govern/calculator-enterprise.png)
- Kromě těchto úspor z ceny společnost plánuje změnu správy některých investic do IT tím, že přemístí potvrzené kapitálové výdaje jako provozní náklady v rámci IT. Tato změna zajistí větší náklady, kterou může využít k urychlení dalších plánovaných úsilí.

## <a name="next-steps"></a>Další kroky

Společnost vyvinula podnikové zásady pro vytvoření obrazce implementace zásad správného řízení. Podniková zásada se řídí mnoha technickými rozhodnutími.

> [!div class="nextstepaction"]
> [Kontrola počátečních podnikových zásad](./initial-corporate-policy.md)
