---
title: Ustanovení procesů dodržování zásad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Navažte procesy, aby se zajistilo dodržování podnikových zásad.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: eff80cb530141a64f706d046bb9f76319f03e3c1
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030247"
---
<!-- markdownlint-disable MD026 -->

# <a name="establish-policy-adherence-processes"></a>Ustanovení procesů dodržování zásad

<!---
I've defined policies, I've provided an architecture guide. Now how do I monitor adherence to policy? If there is a violation, how do I enforce the policy?
--->

Po vytvoření příkazů cloudových zásad a návrh Průvodce návrhem budete muset vytvořit strategii pro zajištění, že nasazení v cloudu zůstane v souladu se svými požadavky na zásady. Tato strategie bude potřebovat, abyste zahrnovali probíhající kontrolu a komunikační procesy vašeho týmu zásad správného řízení pro Cloud, stanovili kritéria pro případy, kdy porušení zásad vyžadují akci a definovali požadavky na automatizované monitorování a systémy dodržování předpisů, které budou Odhalte porušení a triggery nápravy.

Příklady toho, jak se proces dodržování zásad vejde do plánu zásad správného řízení, najdete v oddílech podnikových zásad v [průvodcích](../guides/index.md) s podporou akcí.

## <a name="prioritize-policy-adherence-processes"></a>Určení priorit procesů pro dodržování zásad

Kolik investic do vývojových procesů je potřeba k podpoře cílů zásad? V závislosti na velikosti a zralosti nasazení v cloudu se může velmi výrazně lišit úsilí potřebné k navázání procesů, které podporují dodržování předpisů a náklady spojené s tímto úsilím.

Pro malá nasazení skládající se z prostředků vývoje a testování můžou být požadavky na zásady jednoduché a vyžadují několik vyhrazených prostředků k adresování. Na druhé straně je možné, že nasazení cloudu s vysokou prioritou a s vysokými nároky na výkon může vyžadovat tým pracovníků, rozsáhlých interních procesů a vlastní nástroje pro monitorování, aby podporovaly cíle zásad.

Jako první krok při definování strategie dodržování zásad se vyhodnotí, jak procesy popsané níže můžou podporovat vaše požadavky na zásady. Určete, kolik úsilí stojí v těchto procesech, a pak tyto informace využijte k navázání reálných plánů rozpočtu a zaměstnanců pro splnění těchto potřeb.

## <a name="establish-cloud-governance-team-processes"></a>Vytvoření týmových procesů zásad správného řízení pro Cloud

Před definováním triggerů pro nápravu dodržování zásad je potřeba vytvořit celkové procesy, které bude váš tým používat, a způsob, jakým budou informace sdílet a překládat mezi pracovníky IT a týmem zásad správného řízení pro Cloud.

### <a name="assign-cloud-governance-team-members"></a>Přiřazení členů týmu zásad správného řízení pro Cloud

Váš tým zásad správného řízení vašeho cloudu bude poskytovat průběžné pokyny k dodržování předpisů a zpracovávat problémy související se zásadami, které se objeví při nasazení a provozování vašich cloudových prostředků. Při sestavování tohoto týmu pozvat pracovníky z vaší organizace, kteří mají zkušenosti v oblastech, které jsou pokryté příkazy definovaných zásad a zjištěnými riziky.

U počátečních nasazení testů to může být omezeno na několik správců systému zodpovědných za vytvoření základů zásad správného řízení. V případě vyspělosti procesů zásad správného řízení si pravidelně prostudujte členství v týmu orientačního cloudu, abyste mohli správně řešit nová potenciální rizika a požadavky zásad. Identifikujte členy IT a obchodních pracovníků se souvisejícími zkušenostmi nebo zájmy v konkrétních oblastech zásad správného řízení a zahrňte je do týmů na trvalém nebo ad hoc bázi, jak potřebujete.

### <a name="reviews-and-policy-iteration"></a>Recenze a iterace zásad

Po nasazení dalších prostředků a úloh bude tým zásad správného řízení cloudu potřebovat zajistit, aby nové úlohy nebo prostředky splňovaly požadavky zásad. Vyhodnoťte nové požadavky z vývojových týmů úloh, abyste zajistili, že jejich plánovaná nasazení budou v souladu s vašimi vodítky návrhu, a aktualizujte zásady tak, aby tyto požadavky podporovaly.

Naplánujte vyhodnocení nových potenciálních rizik a příkazů zásad aktualizace a vodítek návrhu podle potřeby. Pracujte s pracovníky IT a týmy úloh a průběžně vyhodnoťte nové funkce a služby Azure. Také můžete naplánovat pravidelné revize každé z pěti oborů zásad správného řízení, abyste zajistili aktuálnost a dodržování zásad.

### <a name="education"></a>Vzdělávání

Dodržování zásad vyžaduje, aby pracovníci IT a vývojáři pochopili požadavky zásad, které mají vliv na jejich oblasti zodpovědnosti. Naplánujte vyhradit prostředky pro dokumentaci rozhodnutí a požadavky a informujte všechny příslušné týmy na návrhových průvodcích, které podporují vaše požadavky na zásady.

Jako změny zásad, pravidelná aktualizace dokumentace a školicí materiály a zajištění, aby úsilí o vzdělávání komunikovalo s aktualizovanými požadavky a pokyny pro příslušné IT pracovníky.

### <a name="establish-escalation-paths"></a>Vytvoření cest eskalace

Pokud prostředek nedodržuje předpisy, kdo obdrží oznámení? Pokud pracovníci IT zjistí problém s dodržováním zásad, na koho se obrátit? Ujistěte se, že je jasně definovaný proces eskalace týmu zásad správného řízení cloudu. Zajistěte, aby byly tyto komunikační kanály aktualizované, aby odrážely změny zaměstnanců a organizace.

## <a name="violation-triggers-and-actions"></a>Aktivační události a akce porušení

Po definování týmu zásad správného řízení pro Cloud a jeho procesů je nutné explicitně definovat, co se má vyhodnotit jako porušení dodržování předpisů, které aktivuje akce a jaké by měly být tyto akce.

### <a name="define-triggers"></a>Definovat triggery

U každého příkazu zásad Zkontrolujte požadavky a určete, co znamená porušení zásad. Vygenerujte triggery pomocí informací, které jste už vytvořili v rámci procesu definice zásad.

- **Tolerance rizika:** Na základě metrik a rizikových ukazatelů, které jste vytvořili jako součást [analýzy tolerance rizik](./risk-tolerance.md), vytvořte aktivační události porušení.
- **Definované požadavky zásad:** Příkazy zásad můžou poskytovat smlouvy o úrovni služeb (SLA), provozní kontinuitu a zotavení po havárii (BCDR) nebo požadavky na výkon, které by se měly používat jako základ pro triggery dodržování předpisů.

### <a name="define-actions"></a>Definovat akce

Každé triggery porušení by měla mít odpovídající akci. Aktivované akce by měly vždy upozorňovat na příslušné zaměstnance IT nebo členy týmu zásad správného řízení, když dojde k porušení. Toto oznámení může vést k ruční revizi problému s dodržováním předpisů nebo úvodní předdefinovaného procesu nápravy v závislosti na typu a závažnosti zjištěného narušení.

Některé příklady aktivačních událostí a akcí porušení:

| Obor zásad správného řízení cloudu | Ukázka triggeru | Ukázková akce |
|-----------------------------|----------------|---------------|
| Cost Management | Útrata v měsíčním cloudu je větší než 20% vyšší, než se očekávalo. | Upozorněte vedoucího fakturační jednotky, který začne kontrolovat využití prostředků. |
| Standardní hodnoty zabezpečení | Zjišťuje podezřelou aktivitu přihlášení uživatele. | Upozorněte tým zabezpečení IT a zakažte podezřelý uživatelský účet. |
| Konzistence prostředků | Využití CPU pro úlohu je větší než 90%. | Upozorněte tým oddělení IT a nahorizontální navýšení kapacity pro zpracování zatížení. |

## <a name="monitoring-and-compliance-automation"></a>Automatizace monitorování a dodržování předpisů

Po definování aktivačních událostí a akcí narušení dodržování předpisů můžete začít s plánováním, jak nejlépe využít nástroje protokolování a vytváření sestav, a další funkce cloudové platformy, které vám pomůžou automatizovat strategii monitorování a dodržování zásad.

Pokyny k výběru nejlepšího vzoru monitorování pro vaše nasazení najdete v tématu [Průvodce pro protokolování a](../../decision-guides/logging-and-reporting/index.md) nastavování v cloudu.

## <a name="next-steps"></a>Další postup

Přečtěte si další informace o dodržování legislativních předpisů v cloudu.

> [!div class="nextstepaction"]
> [Dodržování předpisů](./regulatory-compliance.md)
