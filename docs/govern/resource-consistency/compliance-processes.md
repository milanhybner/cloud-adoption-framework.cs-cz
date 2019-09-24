---
title: Procesy dodržování předpisů v zásadách konzistence prostředků
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesy dodržování předpisů v zásadách konzistence prostředků
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fd44ae6fcdc84efd42ea3f79719475a32ead3111
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223719"
---
# <a name="resource-consistency-policy-compliance-processes"></a>Procesy dodržování předpisů v zásadách konzistence prostředků

Tento článek popisuje přístup k zásadám, které přiblíží [konzistenci prostředků, které řídí konzistenci prostředků](./index.md). Efektivní řízení dodržování konzistence prostředků cloudu začíná opakovanými ručními procesy navrženými k identifikaci provozní neefektivity, vylepšit správu nasazených prostředků a zajistit, aby klíčové úlohy měly minimální přerušení. Tyto ruční procesy jsou doplněny monitorováním, automatizací a nástroji, které vám pomůžou snížit režijní náklady na řízení a zajistit rychlejší reakci na odchylku zásad.

## <a name="planning-review-and-reporting-processes"></a>Plánování, kontrola a vytváření sestav procesů

Cloudové platformy poskytují pole nástrojů a funkcí pro správu, které můžete použít k organizování, zřizování, škálování a minimalizaci výpadků. Pomocí těchto nástrojů můžete efektivně strukturovat a provozovat nasazení v cloudu způsobem, který zajistí nápravu potenciálních rizik, a navíc také těsnou spolupráci s provozními týmy IT a podnikovými stranami.

Následuje sada ukázkových procesů, které se běžně týkají oboru konzistence prostředků. Tyto příklady použijte jako výchozí bod při plánování procesů, které vám umožní pokračovat v aktualizaci zásad konzistence prostředků na základě změny firmy a zpětné vazby od týmů pro vývoj a IT, které se provedly při zapínání pokynů.

**Prvotní posouzení rizik a plánování:** V rámci počátečního přijetí oboru konzistence prostředků Identifikujte základní obchodní rizika a tolerance týkající se provozu a správy IT. Tyto informace slouží k projednání specifických technických rizik se členy vašich IT týmů a vlastníků úloh a vytvoří základní sadu zásad konzistence prostředků, které jsou navržené k nápravě těchto rizik, a stanoví tak počáteční strategii zásad správného řízení.

**Plánování nasazení:** Před nasazením jakýchkoli assetů proveďte kontrolu a Identifikujte všechna nová provozní rizika. Stanovte požadavky na prostředky a očekávané vzory požadavků a Identifikujte potřeby škálovatelnosti a potenciální možnosti optimalizace využití. Také zajistěte, aby byly plány zálohování a obnovení zavedeny.

**Testování nasazení:** V rámci nasazení bude tým zásad správného řízení cloudu ve spolupráci s vašimi týmy cloudových operací zodpovědný za kontrolu nasazení za účelem ověření dodržování zásad konzistence prostředků.

**Roční plánování:** Na roční bázi si Projděte vysokou úroveň strategie konzistence prostředků. Prozkoumejte budoucí plány rozšíření společnosti nebo priority a aktualizujte strategie pro přijetí v cloudu, abyste mohli identifikovat potenciální zvýšení rizika nebo jiné vznikající požadavky na konzistenci prostředků. Tuto dobu Využijte také ke kontrole nejnovějších osvědčených postupů pro konzistenci prostředků v cloudu a jejich integraci do vašich zásad a kontrole procesů.

**Čtvrtletní přezkoumání a plánování:** Každý čtvrtletní základ provede přezkoumání provozních dat a sestav incidentů k identifikaci jakýchkoli změn požadovaných v zásadách konzistence prostředků. V rámci tohoto procesu zkontrolujte změny využití prostředků a výkonu a Identifikujte prostředky, které vyžadují zvýšení nebo snížení přidělení prostředků, a identifikujte všechny úlohy nebo prostředky, které jsou kandidáty na vyřazení.

Tento proces plánování je vhodný pro vyhodnocení aktuálního členství týmu zásad správného řízení cloudu pro účely znalostí, které souvisejí s novými nebo měnícími se zásadami a riziky souvisejícími s konzistencí prostředků jako s oborem. Přizvat relevantní pracovníky IT k účasti na recenzích a plánování jako na dočasné technické poradce nebo na trvalé členy týmu.

**Vzdělávání a školení:** Na bimonthly můžete nabízet cvičení a zajistit, aby pracovníci IT a vývojáři měli aktuální informace o nejnovějších požadavcích na zásady konzistence prostředků a doprovodné materiály. V rámci tohoto procesu zkontrolujte a aktualizujte jakoukoli dokumentaci nebo jiné školicí materiály, abyste se ujistili, že jsou synchronizované s nejnovějšími příkazy firemních zásad.

**Revize měsíčního auditu a vytváření sestav:** Po měsících proveďte audit všech nasazení cloudu, aby se zajistilo jejich pokračující sbližování se zásadami konzistence prostředků. Projděte si související aktivity s pracovníky IT a identifikujte všechny problémy s dodržováním předpisů, které se ještě nezpracovávají v rámci probíhajícího monitorování a procesu vynucení. Výsledkem této recenze je sestava týmu cloudové strategie a každého týmu pro přijetí cloudu, který komunikuje s celkovým výkonem a dodržováním zásad. Sestava je také uložená pro účely auditování a právní účely.

## <a name="ongoing-monitoring-processes"></a>Probíhající procesy monitorování

Určení, jestli vaše strategie správného řízení konzistence prostředků proběhne úspěšně, závisí na viditelnosti aktuálního a minulého stavu infrastruktury cloudu. Bez možnosti analyzovat relevantní metriky a data o stavu a aktivitě vašeho cloudového prostředí nemůžete identifikovat změny vašich rizik nebo zjistit porušení rizik. Probíhající procesy zásad správného řízení, které jsme probrali výše, vyžadují kvalitní data, aby bylo možné upravit zásady tak, aby optimalizoval využití prostředků cloudu a vylepšily celkový výkon úloh hostovaných v cloudu.

Ujistěte se, že vaše týmy IT implementovaly automatizované monitorovací systémy pro cloudovou infrastrukturu, které zachycují relevantní data protokolů, které potřebujete k vyhodnocení rizik. Proaktivujte tyto systémy a zajistěte tak, aby se zobrazila výzva k detekci a zmírnění potenciálního porušení zásad, a ujistěte se, že máte strategii monitorování v souladu s vašimi provozními požadavky.

## <a name="violation-triggers-and-enforcement-actions"></a>Aktivační události porušení a akce vynucení

Vzhledem k tomu, že dodržování zásad konzistence prostředků může vést ke kritickému narušení služby nebo výraznému snížení nákladů, tým zásad správného řízení cloudu by měl mít přehled o incidentech, které nedodržují předpisy. Ujistěte se, že zaměstnanci oddělení IT mají jasné cesty pro eskalaci, aby tyto problémy nastavili členům týmu zásad správného řízení, které nejlépe vyhovují, aby identifikovali a ověřili, že problémy s zásadami jsou po zjištění

Po zjištění porušení byste měli provést akce, aby se zásady znovu zarovnaly co nejdřív. Váš IT tým může automatizovat aktivační události narušení pomocí nástrojů, které jsou uvedené v [Sada nástrojů konzistence prostředků pro Azure](./toolchain.md).

Následující triggery a akce vynucení poskytují příklady, které vám pomůžou při plánování použití dat monitorování k řešení porušení zásad:

- **Zjistil se prostředek nadměrného zřízení.** Zjištěné prostředky, které používají méně než 60% kapacity procesoru nebo paměti, by měly automaticky škálovat nebo zrušit zřízení prostředků, aby se snížily náklady.
- **Byl zjištěn nezřízený prostředek.** Prostředky zjištěné při použití více než 80% kapacity procesoru nebo paměti by měly automaticky škálovat a zřizovat další prostředky, aby se zajistila další kapacita.
- **Vytváření netagovaných prostředků.** Všechny požadavky na vytvoření prostředku bez požadovaných meta značek budou automaticky odmítnuty.
- **Bylo zjištěno závažné výpadky prostředků.** Pracovníci IT jsou informováni o všech zjištěných výpadkech nepostradatelných výpadků. Pokud není výpadek okamžitě přeložitelný, zaměstnanci problém vyřeší a upozorní na vlastníky úloh a tým zásad správného řízení pro Cloud. Tým zásad správného řízení cloudu bude tento problém sledovat, dokud nebudou pokyny k vyřešení a aktualizaci, pokud je nutná revize zásad, aby nedocházelo k budoucím incidentům
- **Posun konfigurace** Prostředky, které nejsou v souladu se zavedenými směrnými plány, by měly aktivovat upozornění a automaticky je opravovat pomocí nástrojů pro správu konfigurace, jako jsou Azure Automation, Puppet, Ansible atd.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat procesy a triggery, které se rovnají aktuálnímu plánu přijetí do cloudu.

Pokyny k provádění zásad správy cloudu ve srovnání s plány přijetí najdete v článku zlepšování oborů.

> [!div class="nextstepaction"]
> [Vylepšení oboru konzistence prostředků](./discipline-improvement.md)
