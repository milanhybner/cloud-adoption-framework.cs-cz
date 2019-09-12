---
title: Ukázkové zásady konzistence prostředků – příkazy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ukázkové zásady konzistence prostředků – příkazy
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3c3cb908fb5a67f6b7d32441e82d5c8efab5b9c7
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70823999"
---
# <a name="resource-consistency-sample-policy-statements"></a>Ukázkové zásady konzistence prostředků – příkazy

Jednotlivé příkazy zásad cloudu jsou pokyny pro řešení konkrétních rizik zjištěných během procesu posouzení rizik. Tyto příkazy by měly poskytnout stručné shrnutí rizik a plánů, které je třeba řešit. Každá definice příkazu by měla obsahovat tyto informace:

- **Technické riziko:** Souhrn rizika, které tato zásada bude řešit.
- **Prohlášení o zásadách:** Jasné souhrnné vysvětlení požadavků zásad.
- **Možnosti návrhu:** Užitečná doporučení, specifikace nebo další pokyny, které mohou týmy IT a vývojáři použít při implementaci těchto zásad.

Následující ukázkové příkazy zásad řeší běžná obchodní rizika související s konzistencí prostředků. Tyto příkazy jsou příklady, na které můžete odkazovat při konceptech příkazů zásad, které řeší potřeby vaší organizace. Tyto příklady se nepovažují za podrobné a některé možnosti zásad se týkají každého identifikovaného rizika. Pracujte úzce s podnikáním a týmy IT a Identifikujte nejlepší zásady pro Vaši jedinečnou sadu rizik.

## <a name="tagging"></a>Označování

**Technické riziko:** Bez správného označování metadat přidružených k nasazeným prostředkům nemůže IT operace určovat prioritu podpory nebo optimalizace prostředků na základě požadované smlouvy SLA, důležitosti pro obchodní operace nebo provozní náklady. To může vést k chybnému přidělení prostředků IT a možným zpožděním při řešení incidentů.

**Prohlášení o zásadách:** Implementují se tyto zásady:

- Nasazené prostředky by měly být označeny následujícími hodnotami:
  - Náklady
  - Závažnost
  - SLA
  - Prostředí
- Nástroje zásad správného řízení musí ověřovat označování související s náklady, závažností, smlouvou SLA, aplikací a prostředím. Všechny hodnoty musí být zarovnané na předdefinované hodnoty, které spravuje tým zásad správného řízení.

**Možné možnosti návrhu:** V Azure jsou pro většinu typů prostředků podporovány [standardní značky metadat název-hodnota](/azure/azure-resource-manager/resource-group-using-tags) . [Azure Policy](/azure/governance/policy/overview) slouží k vymáhání určitých značek v rámci vytváření prostředků.

## <a name="ungoverned-subscriptions"></a>Neupravená předplatná

**Technické riziko:** Libovolný způsob vytváření předplatných a skupin pro správu může vést k izolovaným oddílům ve vlastnictví cloudu, které nejsou řádně předmětem zásad správného řízení.

**Prohlášení o zásadách:** Vytváření nových předplatných nebo skupin pro správu pro všechny klíčové aplikace nebo chráněná data budou vyžadovat přezkoumání od týmu zásad správného řízení cloudu. Schválené změny budou integrovány do správného přiřazení podrobného plánu.

**Možné možnosti návrhu:** Odblokujte přístup pro správu k vašim organizacím [skupiny pro správu Azure](/azure/governance/management-groups) , a to jenom na schválené členy týmu zásad správného řízení, kteří budou řídit vytváření předplatných a řízení přístupu.

## <a name="manage-updates-to-virtual-machines"></a>Správa aktualizací virtuálních počítačů

**Technické riziko:** Virtuální počítače, které nejsou aktuální s nejnovějšími aktualizacemi a opravami softwaru, jsou zranitelné při potížích se zabezpečením nebo výkonem, což může vést k výpadkům služby.

**Prohlášení o zásadách:** Nástroje řízení správného řízení musí vymáhat, aby byly na všech nasazených virtuálních počítačích povoleny automatické aktualizace. Porušení musí být přezkoumána s provozními týmy správy a opraveny v souladu se zásadami provozu. Prostředky, které se automaticky neaktualizují, musí být zahrnuté do procesů, které vlastní IT operace.

**Možné možnosti návrhu:** U hostovaných virtuálních počítačů Azure můžete zajistit konzistentní správu aktualizací pomocí [řešení Update Management v Azure Automation](/azure/automation/automation-update-management).

## <a name="deployment-compliance"></a>Dodržování předpisů při nasazení

**Technické riziko:** Skripty pro nasazení a nástroje pro automatizaci, které nejsou plně prověřené týmem zásad správného řízení cloudu, můžou mít za následek nasazení prostředků, která narušují zásady.

**Prohlášení o zásadách:** Implementují se tyto zásady:

- Nástroje pro nasazení musí schválit tým zásad správného řízení cloudu, aby se zajistilo průběžné řízení nasazených prostředků.
- Skripty nasazení musí být udržovány v centrálním úložišti přístupném týmem zásad správného řízení cloudu pro pravidelnou kontrolu a auditování.

**Možné možnosti návrhu:** Konzistentní používání plánů [Azure](/azure/governance/blueprints) ke správě automatizovaných nasazení umožňuje konzistentní nasazení prostředků Azure, které dodržují standardy a zásady správného řízení vaší organizace.

## <a name="monitoring"></a>Monitorování

**Technické riziko:** Nesprávně implementované nebo nekonzistentně instrumentované monitorování může zabránit detekci problémů se stavem úloh nebo jiným narušením dodržování zásad.

**Prohlášení o zásadách:** Implementují se tyto zásady:

- Nástroje zásad správného řízení musí ověřit, že všechny prostředky související s důležitými aplikacemi nebo chráněnými daty jsou zahrnuté do monitorování pro vyčerpání a optimalizaci prostředků.
- Nástroje správy zásad správného řízení musí ověřit, jestli jsou shromažďovány odpovídající úrovně dat protokolování pro všechny klíčové aplikace nebo chráněná data.

**Možné možnosti návrhu:** [Azure monitor](/azure/azure-monitor/overview) je výchozí služba monitorování v Azure a při nasazování prostředků se dá vymáhat konzistentní monitorování prostřednictvím [Azure modrotisky](/azure/governance/blueprints) .

## <a name="disaster-recovery"></a>Zotavení po havárii

**Technické riziko:** Selhání prostředku, odstranění nebo poškození může mít za následek přerušení důležitých aplikací a služeb a ztráty citlivých dat.

**Prohlášení o zásadách:** Všechny klíčové aplikace a chráněná data musí mít implementovaná řešení pro zálohování a obnovení, aby se minimalizoval dopad na výpadky nebo chyby systému.

**Možné možnosti návrhu:** Služba [Azure Site Recovery] poskytuje možnosti zálohování, obnovení a replikace určené k minimalizaci doby výpadku ve scénářích provozní kontinuity a zotavení po havárii (BCDR).

## <a name="next-steps"></a>Další postup

Použijte ukázky uvedené v tomto článku jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

Pokud chcete začít vyvíjet vlastní příkazy zásad související s konzistencí prostředků, Stáhněte si [šablonu konzistence prostředků](./template.md).

Pokud chcete zrychlit přijetí této disciplíny, vyberte [akčního Průvodce zásad správného řízení](../journeys/index.md) , který nejlépe zarovnává vaše prostředí. Pak upravte návrh tak, aby zahrnoval konkrétní podniková rozhodnutí o zásadách.

Sestavování rizik a tolerance, zavedení procesu řízení a komunikace s dodržováním zásad konzistence prostředků.

> [!div class="nextstepaction"]
> [Vytváření procesů dodržování zásad](./compliance-processes.md)
