---
title: Procesy kompatibility zásad akcelerace nasazení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesy kompatibility zásad akcelerace nasazení
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c127a1c8bc8bce7608f0e146b36785fcee82dc0b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029773"
---
# <a name="deployment-acceleration-policy-compliance-processes"></a>Procesy kompatibility zásad akcelerace nasazení

Tento článek popisuje přístup k zásadám přiblížících se k zásadám, které řídí [akceleraci nasazení](./index.md). Efektivní řízení konfigurace cloudu začíná opakujícími se ručními procesy navrženými k detekci potíží a zavedení zásad, které tyto rizika napravují. Tyto procesy však můžete automatizovat a doplnit pomocí nástrojů, aby se snížila režie řízení a byla umožněna rychlejší reakce na odchylku.

## <a name="planning-review-and-reporting-processes"></a>Plánování, kontrola a vytváření sestav procesů

Nejlepší nástroje pro akceleraci nasazení v cloudu jsou stejně vhodné jako procesy a zásady, které podporují. Následuje sada ukázkových procesů běžně používaných jako součást oboru akcelerace nasazení. Tyto příklady použijte jako výchozí bod při plánování procesů, které vám umožní pokračovat v aktualizaci zásad nasazení a konfigurace na základě změny firmy a názoru vývoje a IT týmů, které jsou zodpovědné za zapnutí pokynů zásad správného řízení do kroky.

**Prvotní posouzení rizik a plánování:** V rámci počátečního přijetí oboru akcelerace nasazení Identifikujte základní obchodní rizika a tolerance týkající se nasazení vašich obchodních aplikací. Tyto informace slouží k projednání specifických technických rizik se členy provozního týmu IT a vyvine základní sadu zásad nasazení a konfigurace, které oprava tato rizika, aby se vytvořila vaše počáteční strategie zásad správného řízení.

**Plánování nasazení:** Před nasazením jakýchkoli prostředků proveďte kontrolu zabezpečení a operací a Identifikujte všechna nová rizika a ujistěte se, že jsou splněné všechny požadavky zásad související s nasazením.

**Testování nasazení:** V rámci procesu nasazení jakéhokoli prostředku zodpovídá tým zásad správného řízení cloudu ve spolupráci s vašimi týmy IT za kontrolu dodržování zásad nasazení.

**Roční plánování:** Proveďte roční kontrolu v strategii akcelerace nasazení na vysoké úrovni. Prozkoumejte budoucí podnikové priority a aktualizujte strategie pro přijetí do cloudu, abyste mohli identifikovat potenciální zvýšení rizika a další vznikající potřeby konfigurace a příležitosti. Tento čas se taky používá ke kontrole nejnovějších osvědčených postupů DevOps a jejich integraci do vašich zásad a kontrole procesů.

**Čtvrtletní přezkoumání a plánování:** Projděte si čtvrtletní přehled dat o provozním auditu a sestavy incidentů a Identifikujte případné změny, které jsou potřeba v zásadách akcelerace nasazení. V rámci tohoto postupu si přečtěte aktuální Doporučené postupy pro DevOps a DevTechOps a podle potřeby aktualizujte zásady. Po dokončení kontroly zarovnejte pokyny k návrhu aplikací a systémů pomocí aktualizovaných zásad.

Tento proces plánování je také vhodný čas k vyhodnocení aktuálního členství týmu zásad správného řízení v souvislosti s novými nebo měnícími se zásadami a riziky týkajícími se DevOps a akcelerace nasazení. Přizvat relevantní pracovníky IT k účasti na recenzích a plánování jako na dočasné technické poradce nebo na trvalé členy týmu.

**Vzdělávání a školení:** Na bimonthly můžete nabízet cvičení a zajistit, aby pracovníci IT a vývojáři byli aktuální o strategii a požadavcích na urychlení nasazení. V rámci tohoto procesu zkontrolujte a aktualizujte veškerou dokumentaci, pokyny nebo další školicí materiály, abyste měli jistotu, že jsou synchronizované s nejnovějšími příkazy firemních zásad.

**Revize měsíčního auditu a vytváření sestav:** Proveďte měsíční audit na všechna nasazení cloudu a zajistěte tak jejich pokračující sbližování pomocí zásad konfigurace. Projděte si aktivity související s nasazením pracovníky IT a identifikujte všechny problémy s dodržováním předpisů, které se ještě nezpracovávají jako součást probíhajícího monitorování a procesu vynucení. Výsledkem této recenze je sestava týmu cloudové strategie a každého týmu pro přijetí cloudu, který oznamuje celkové dodržování zásad. Sestava je také uložená pro účely auditování a právní účely.

## <a name="ongoing-monitoring-processes"></a>Probíhající procesy monitorování

Zjištění úspěšnosti strategie zásad správného řízení při nasazení závisí na viditelnosti aktuálního a minulého stavu infrastruktury cloudu. Bez možnosti analyzovat relevantní metriky a data o provozním stavu a aktivitě vašich cloudových prostředků nemůžete identifikovat změny vašich rizik ani odhalit porušení rizikových zdrojů. Probíhající procesy zásad správného řízení popsané výše vyžadují kvalitní data, aby bylo zajištěno, že je možné upravit zásady a chránit svou infrastrukturu před změnou hrozeb a rizik před nenakonfigurovanými prostředky.

Ujistěte se, že vaše provozní týmy IT implementovaly automatizované monitorovací systémy pro cloudovou infrastrukturu, které zachycují relevantní data protokolů, která potřebujete k vyhodnocení rizik. Proaktivně monitorujte tyto systémy, abyste se ujistili, že se zobrazila výzva k detekci a zmírnění potenciálního porušení zásad, a ujistěte se, že vaše strategie monitorování odpovídá potřebám nasazení a konfigurace.

## <a name="violation-triggers-and-enforcement-actions"></a>Aktivační události porušení a akce vynucení

Vzhledem k tomu, že neshoda se zásadami konfigurace může vést k důležitým rizikům při přerušení služeb, tým zásad správného řízení cloudu by měl mít přehled o závažných porušeních zásad. Ujistěte se, že zaměstnanci oddělení IT mají k dispozici jasné cesty pro eskalaci pro oznamování problémů s kompatibilitou konfigurace pro členy týmu zásad správného řízení, které nejlépe vyhovují, aby identifikovali a ověřili, že problémy s

Po zjištění porušení byste měli provést akce, aby se zásady znovu zarovnaly co nejdřív. Váš IT tým může automatizovat aktivační události narušení pomocí nástrojů, které jsou uvedené v části [akcelerace nasazení sada nástrojů pro Azure](./toolchain.md).

Následující triggery a akce vynucení poskytují příklady, které můžete použít při pojednání, jak použít data monitorování k vyřešení porušení zásad:

- **Zjištěny neočekávané změny v konfiguraci.** Pokud se konfigurace prostředku neočekávaně změní, pracujte s pracovníky IT a vlastníky úloh a Identifikujte hlavní příčinu a vytvořte plán oprav.
- **Konfigurace nových prostředků nedodržuje zásady.** Pracujte s DevOps týmy a vlastníky úloh a Projděte si zásady akcelerace nasazení během spuštění projektu, aby všichni členové pochopili relevantní požadavky zásad.
- **Selhání nasazení nebo problémy s konfigurací způsobují zpoždění v plánech projektu.** Pracujte s vývojovými týmy a vlastníky úloh a zajistěte, aby tým pochopil, jak automatizovat nasazení cloudových prostředků pro zajištění konzistence a opakovatelnosti. Plně automatizovaná nasazení by se měla vyžadovat v předstihu v&mdash;cyklu vývoje, který se snaží dosáhnout pozdě v cyklu vývoje, obvykle vede k neočekávaným problémům a prodlevám.

## <a name="next-steps"></a>Další postup

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat procesy a triggery, které se rovnají aktuálnímu plánu přijetí do cloudu.

Pokyny k provádění zásad správy cloudu ve srovnání s plány přijetí najdete v článku zlepšování oborů.

> [!div class="nextstepaction"]
> [Vylepšení oboru akcelerace nasazení](./discipline-improvement.md)
