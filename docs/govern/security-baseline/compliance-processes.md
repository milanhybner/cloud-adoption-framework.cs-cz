---
title: Procesy dodržování předpisů zásad standardních hodnot zabezpečení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesy dodržování předpisů zásad standardních hodnot zabezpečení
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6494f64b91a0a59f235efbc21030c65fa5e7ded8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029574"
---
# <a name="security-baseline-policy-compliance-processes"></a>Procesy dodržování předpisů zásad standardních hodnot zabezpečení

Tento článek popisuje přístup k zásadám, které přistupují k zásadám, které řídí [standardní hodnoty zabezpečení](./index.md). Efektivní řízení cloudového zabezpečení začíná s opakovanými ručními procesy navrženými pro detekci ohrožení zabezpečení a stanovení zásad, které tyto bezpečnostní rizika napravují. To vyžaduje pravidelné zapojení týmu zásad správného řízení cloudu a zúčastněných podnikatelských a zúčastněných stran, aby zkontrolovali a aktualizovali zásady a zajistili dodržování zásad. Mnoho probíhajících procesů monitorování a vynucení je navíc možné automatizovat nebo doplňovat pomocí nástrojů, aby se snížila režie řízení a byla umožněna rychlejší reakce na odchylku zásad.

## <a name="planning-review-and-reporting-processes"></a>Plánování, kontrola a vytváření sestav procesů

Nejlepší nástroje pro základní zabezpečení v cloudu jsou stejně vhodné jako procesy a zásady, které podporují. Následuje sada ukázkových procesů, které se běžně podílejí na směrném plánu zabezpečení. Tyto příklady použijte jako výchozí bod při plánování procesů, které vám umožní pokračovat v aktualizaci zásad zabezpečení na základě změny firmy a zpětné vazby od týmů zabezpečení a IT, které jsou na zpracování pokynů zásad správného řízení.

**Prvotní posouzení rizik a plánování:** V rámci prvotního přijetí pravidla směrného plánu zabezpečení Identifikujte základní obchodní rizika a tolerance týkající se zabezpečení cloudu. Tyto informace slouží k projednání specifických technických rizik se členy svých týmů IT a zabezpečení a vyvine základní sadu zásad zabezpečení pro zmírnění těchto rizik, aby bylo možné vytvořit počáteční strategii zásad správného řízení.

**Plánování nasazení:** Před nasazením jakékoli úlohy nebo assetu proveďte kontrolu zabezpečení a Identifikujte všechna nová rizika a ujistěte se, že jsou splněné všechny požadavky na zásady přístupu a zabezpečení dat.

**Testování nasazení:** V rámci procesu nasazení u jakékoli úlohy nebo prostředku bude tým zásad správného řízení cloudu ve spolupráci s vašimi podnikovými bezpečnostními týmy zodpovědný za kontrolu nasazení za účelem ověření dodržování zásad zabezpečení.

**Roční plánování:** V ročních intervalech udělejte nejdůležitější kontrolu zabezpečení základní strategie. Seznamte se s budoucími podnikovými prioritami a aktualizujte strategie pro přijetí cloudu, abyste mohli identifikovat potenciální zvýšení rizika a další vznikající požadavky Tuto dobu můžete také použít ke kontrole nejnovějších osvědčených postupů zabezpečení standardních hodnot a jejich integraci do vašich zásad a kontrole procesů.

**Čtvrtletní přezkoumání a plánování:** Každý čtvrtletní základ provede přezkoumání dat auditu zabezpečení a sestav incidentů k identifikaci změn požadovaných v zásadách zabezpečení. V rámci tohoto procesu si Projděte aktuální kyberbezpečnosti na šířku, abyste proaktivně předpokládali vznikající hrozby a podle potřeby aktualizovali zásady. Po dokončení kontroly zarovnejte pokyny k návrhu s aktualizovanými Zásadami.

Tento proces plánování je také vhodný čas k vyhodnocení aktuálního členství týmu zásad správného řízení v souvislosti s novými nebo měnícími se zásadami a riziky souvisejícími se zabezpečením. Přizvat relevantní pracovníky IT k účasti na recenzích a plánování jako na dočasné technické poradce nebo na trvalé členy týmu.

**Vzdělávání a školení:** Na bimonthly jsou nabízené cvičení, které zajistí, že pracovníci IT a vývojáři budou v aktuálním stavu na nejnovější požadavky zásad zabezpečení. V rámci tohoto procesu zkontrolujte a aktualizujte veškerou dokumentaci, pokyny nebo další školicí materiály, abyste měli jistotu, že jsou synchronizované s nejnovějšími příkazy firemních zásad.

**Revize měsíčního auditu a vytváření sestav:** Po měsících proveďte audit všech nasazení cloudu a zajistěte tak jejich pokračující sbližování pomocí zásad zabezpečení. Projděte si aktivity související se zabezpečením zaměstnanců IT a identifikujte všechny problémy s dodržováním předpisů, které se ještě nezpracovávají v rámci probíhajícího monitorování a procesu vynucení. Výsledkem této recenze je sestava týmu cloudové strategie a každého týmu pro přijetí cloudu, který oznamuje celkové dodržování zásad. Sestava je také uložená pro účely auditování a právní účely.

## <a name="ongoing-monitoring-processes"></a>Probíhající procesy monitorování

Určení, jestli vaše strategie zásad správného řízení zabezpečení proběhne úspěšně, závisí na viditelnosti aktuálního a minulého stavu infrastruktury cloudu. Bez možnosti analyzovat relevantní metriky a data stavu a aktivity zabezpečení cloudových prostředků nemůžete identifikovat změny vašich rizik nebo zjistit porušení rizik. Probíhající procesy zásad správného řízení popsané výše vyžadují kvalitní data, aby bylo zajištěno, že zásady je možné upravit tak, aby lépe chránily vaši infrastrukturu před měnícími se hrozbami a požadavky

Ujistěte se, že vaše týmy zabezpečení a IT mají implementovány automatizované monitorovací systémy pro cloudovou infrastrukturu, které zachycují relevantní data protokolů, které potřebujete k vyhodnocení rizik. Proaktivně monitorujte tyto systémy, abyste se ujistili, že se vyzvat k detekci a zmírnění potenciálního porušení zásad a zajistili jsme strategii monitorování v souladu s požadavky na zabezpečení.

## <a name="violation-triggers-and-enforcement-actions"></a>Aktivační události porušení a akce vynucení

Vzhledem k tomu, že nedodržování předpisů může vést ke kritickému a bezpečnostnímu riziku a narušením služeb, tým zásad správného řízení cloudu by měl mít přehled o závažných porušeních zásad. Ujistěte se, že zaměstnanci oddělení IT mají jasné cesty k eskalaci pro oznamování problémů zabezpečení členům týmu zásad správného řízení, které nejlépe vyhovují, aby identifikovali a ověřili, že byly problémy se zásadami omezeny

Po zjištění porušení byste měli provést akce, aby se zásady znovu zarovnaly co nejdřív. Váš IT tým může automatizovat aktivační události narušení pomocí nástrojů, které jsou uvedené v části [Security Baseline sada nástrojů for Azure](./toolchain.md).

Následující triggery a akce vynucení poskytují příklady, které vám pomůžou při plánování použití dat monitorování k řešení porušení zásad:

- **Bylo zjištěno zvýšení počtu útoků.** Pokud některý z prostředků funguje o 25% v případě útoků hrubou silou nebo DDoSch útoků, prodiskutujte se s personálem zabezpečení IT a vlastníkem úloh, abyste zjistili náprav Sledujte pokyny k potížím a aktualizacím, pokud je nutná revize zásad, aby nedocházelo k budoucím incidentům.
- **Byla zjištěna neklasifikovaná data.** Veškerý zdroj dat bez vhodné klasifikace ochrany osobních údajů, zabezpečení nebo obchodní dopad bude mít odepřený externí přístup, dokud se klasifikace neuplatní vlastníkem dat a pokud se použije odpovídající úroveň ochrany dat.
- **Zjistil se problém se stavem zabezpečení.** Zakáže přístup k žádným virtuálním počítačům, které mají známý přístup nebo zjištěné chyby zabezpečení malwaru, dokud nebude možné nainstalovat příslušné opravy nebo bezpečnostní software. Aktualizujte pokyny zásad na účet pro všechny nově zjištěné hrozby.
- **Zjištěna ohrožení zabezpečení sítě.** Přístup k jakémukoli prostředku, který není výslovně povolený zásadami přístupu k síti, by měl aktivovat upozornění pro pracovníky zabezpečení IT a příslušného vlastníka úlohy. Sledujte pokyny k potížím a aktualizacím, pokud je nutná revize zásad pro zmírnění budoucích incidentů.

## <a name="next-steps"></a>Další postup

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat procesy a triggery, které se rovnají aktuálnímu plánu přijetí do cloudu.

Pokyny k provádění zásad správy cloudu ve srovnání s plány přijetí najdete v článku zlepšování oborů.

> [!div class="nextstepaction"]
> [Vylepšení oboru směrného plánu zabezpečení](./discipline-improvement.md)
