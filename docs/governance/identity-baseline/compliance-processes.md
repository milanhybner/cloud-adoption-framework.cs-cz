---
title: Procesy dodržování předpisů zásad standardních hodnot identity
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesy dodržování předpisů zásad standardních hodnot identity
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 078f2e95fcddeeca6f0bfb7dca50eb301ba36b56
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70827938"
---
# <a name="identity-baseline-policy-compliance-processes"></a>Procesy dodržování předpisů zásad standardních hodnot identity

Tento článek popisuje přístup k zásadám, které přistupují k zásadám, které řídí [standardní hodnoty identity](./index.md). Efektivní řízení identity začíná s opakovanými ručními procesy, které vedou k přijetí a revizi zásad identity. To vyžaduje pravidelné zapojení týmu zásad správného řízení cloudu a zúčastněných podnikatelských a zúčastněných stran, aby zkontrolovali a aktualizovali zásady a zajistili dodržování zásad. Mnoho probíhajících procesů monitorování a vynucení je navíc možné automatizovat nebo doplňovat pomocí nástrojů, aby se snížila režie řízení a byla umožněna rychlejší reakce na odchylku zásad.

## <a name="planning-review-and-reporting-processes"></a>Plánování, kontrola a vytváření sestav procesů

Nástroje pro správu identit nabízejí možnosti a funkce, které výrazně pomáhají při nasazení v cloudu a při řízení přístupu k uživatelům. Ale taky vyžadují, aby se na podporu cílů vaší organizace musely zamyslet i na propadlé procesy a zásady. Následuje sada ukázkových procesů, které se obvykle používají v rámci oboru standardních hodnot identity. Tyto příklady použijte jako výchozí bod při plánování procesů, které vám umožní pokračovat v aktualizaci zásad identity na základě změny firmy a zpětné vazby od IT týmů, které jsou v praxi s zapnutím pokynů zásad správného řízení.

**Prvotní posouzení rizik a plánování:** V rámci počátečního přijetí pravidla směrného plánu identity Identifikujte základní obchodní rizika a tolerance související se správou cloudových identit. Tyto informace slouží k projednání specifických technických rizik se členy vašich IT týmů zodpovědných za správu služby identity a k vývoji základní sady zásad zabezpečení pro zmírnění těchto rizik při vytváření počáteční strategie správy.

**Plánování nasazení:** Před jakýmkoli nasazením si přečtěte téma požadavky na přístup pro všechny úlohy a vytvořte strategii řízení přístupu, která zarovnává se zavedenými podnikovými zásadami identity. Pokud chcete zjistit, jestli se vyžadují aktualizace zásad, zdokumentujte případné mezery mezi požadavky a aktuálními zásadami a podle potřeby upravte zásady.

**Testování nasazení:** V rámci nasazení bude tým zásad správného cloudu ve spolupráci s týmy IT zodpovědnými za služby identity zodpovědný za kontrolu nasazení za účelem ověření dodržování zásad identity.

**Roční plánování:** Na roční bázi si Projděte vysokou úroveň strategie správy identit. Prozkoumejte plánované změny prostředí identity Services a aktualizujte strategie pro přijetí do cloudu, které identifikují potenciální zvýšení rizika nebo potřebují upravit aktuální vzory infrastruktury identit. Tuto dobu můžete také použít ke kontrole nejnovějších osvědčených postupů pro správu identit a jejich integraci do vašich zásad a kontrole procesů.

**Čtvrtletní plánování:** Každý čtvrtletní základ provede obecnou kontrolu identity a auditu řízení přístupu a naplní se týmy pro přijímání v cloudu, aby identifikovala potenciální nová rizika nebo provozní požadavky, které by vyžadovaly aktualizaci zásad identity nebo změn v řízení přístupu. strategie.

Tento proces plánování je také vhodný čas k vyhodnocení aktuálního členství týmu zásad správného řízení v souvislosti s novými nebo měnícími se zásadami a riziky týkajícími se identity. Přizvat relevantní pracovníky IT k účasti na recenzích a plánování jako na dočasné technické poradce nebo na trvalé členy týmu.

**Vzdělávání a školení:** Na bimonthly můžete nabízet cvičení a zajistit, aby pracovníci IT a vývojáři byli aktuálními požadavky na zásady identity. V rámci tohoto procesu zkontrolujte a aktualizujte veškerou dokumentaci, pokyny nebo další školicí materiály, abyste měli jistotu, že jsou synchronizované s nejnovějšími příkazy firemních zásad.

**Revize měsíčního auditu a vytváření sestav:** Po měsících proveďte audit všech nasazení cloudu, aby se zajistilo jejich pokračující sbližování se zásadami identity. Pomocí této kontroly můžete zkontrolovat přístup uživatelů proti obchodním změnám a zajistit tak, aby uživatelé měli správný přístup ke cloudovým prostředkům, a zajistili, že se strategie přístupu, jako je třeba RBAC, dodržují konzistentně. Identifikujte všechny privilegované účty a zdokumentujte jejich účel. Tento proces revize vytvoří zprávu pro tým cloudové strategie a každý tým pro přijetí v cloudu podrobně popisuje celkové dodržování zásad. Sestava je také uložená pro účely auditování a právní účely.

## <a name="ongoing-monitoring-processes"></a>Probíhající procesy monitorování

Určení, jestli vaše strategie zásad správného řízení identity proběhne úspěšně, závisí na viditelnosti aktuálního a minulého stavu systémů identity. Bez možnosti analyzovat relevantní metriky a související data nasazení cloudu nemůžete identifikovat změny vašich rizik nebo zjistit porušení rizik. Probíhající procesy zásad správného řízení popsané výše vyžadují kvalitní data, abyste měli jistotu, že zásady je možné upravit tak, aby podporovaly měnící se potřeby vaší firmy.

Ujistěte se, že vaše týmy IT implementovaly automatizované monitorovací systémy pro vaše služby identity, které zaznamenávají protokoly a informace o auditu, které potřebujete k vyhodnocení rizik. Musí být aktivní při monitorování těchto systémů, aby se zobrazila výzva k detekci a zmírnění potenciálního porušení zásad a aby se v strategii monitorování projevily změny vaší infrastruktury identity.

## <a name="violation-triggers-and-enforcement-actions"></a>Aktivační události porušení a akce vynucení

Porušení zásad identity může mít za následek neoprávněný přístup k citlivým datům a vede k závažnému narušení nejdůležitějších aplikací a služeb. Po zjištění porušení byste měli provést akce, aby se zásady znovu zarovnaly co nejdřív. Váš IT tým může automatizovat aktivační události narušení pomocí nástrojů popsaných v [Sada nástrojů podle směrného plánu identity](toolchain.md).

Následující triggery a akce vynucení poskytují příklady, které vám pomůžou při plánování použití dat monitorování k řešení porušení zásad:

- **Zjištěna podezřelá aktivita:** Přihlášení uživatelů zjištěná z IP adres anonymního proxy serveru, neznámých umístění nebo po sobě jdoucích přihlášení z možných vzdálených geografických umístění mohou označovat potenciální porušení účtu nebo pokus o škodlivý přístup. Přihlášení bude zablokováno, dokud nebude možné ověřit identitu uživatele a resetování hesla.
- **Nevrácené přihlašovací údaje uživatele:** Účty, které mají své uživatelské jméno a heslo odvrácené na Internet, budou zakázané, dokud nebude možné ověřit identitu uživatele a resetování hesla.
- **Zjištěny nedostatečné ovládací prvky přístupu:** Všechny chráněné prostředky, u kterých omezení přístupu nesplňují požadavky na zabezpečení, budou mít přístup zablokovaný, dokud se prostředek nedostane do dodržování předpisů.

## <a name="next-steps"></a>Další postup

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat procesy a triggery, které se rovnají aktuálnímu plánu přijetí do cloudu.

Pokyny k provádění zásad správy cloudu ve srovnání s plány přijetí najdete v článku zlepšování oborů.

> [!div class="nextstepaction"]
> [Vylepšení oboru směrného plánu identity](./discipline-improvement.md)
