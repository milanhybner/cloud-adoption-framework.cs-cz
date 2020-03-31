---
title: Vylepšení oboru konzistence prostředků
description: Rozhraní pro přijetí cloudu pro Azure vám pomůže pochopit úkoly, které jsou nezbytné k vývoji a vyspělosti oboru konzistence prostředků v každé fázi přijetí.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dcfa6596d61233efa83bc6a1c6977a2ebe4ad510
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433486"
---
# <a name="resource-consistency-discipline-improvement"></a>Vylepšení oboru konzistence prostředků

Obor konzistence prostředků se zaměřuje na způsoby vytváření zásad souvisejících s provozní správou prostředí, aplikací nebo úloh. V rámci pěti pravidel zásad správného řízení cloudu zahrnuje konzistence prostředků monitorování výkonu aplikací, úloh a prostředků. Zahrnuje taky úkoly nutné pro splnění požadavků na škálování, napravit porušení výkonu smlouva SLA (SLA) a aktivně se vyhnout porušením SLA prostřednictvím automatizované nápravy.

Tento článek popisuje některé možné úkoly, které může vaše společnost zapojit do vývoje a vyspělosti oboru konzistence prostředků. Tyto úlohy je možné rozdělit na plánování, sestavování, přijímání a provozní fáze implementace cloudového řešení, které se pak iterovat na to, že umožní vývoj [přírůstkového přístupu ke správě cloudu](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Čtyři fáze přijetí](../../_images/govern/adoption-phases.png)

*Obrázek 1 – fáze přijetí přírůstkového přístupu ke zásadám správného řízení cloudu.*

U každého dokumentu není možné brát v úvahu požadavky všech společností. Tento článek popisuje navrhované minimální a potenciální příklady aktivit pro každou fázi procesu maturation zásad správného řízení. Počáteční cíl těchto aktivit vám pomůže vytvořit [MVP pro zásady](../guides/index.md#an-incremental-approach-to-cloud-governance) a vytvořit rozhraní pro přírůstkové zlepšování zásad. Váš tým zásad správného řízení vašeho cloudu bude muset rozhodnout, kolik investic do těchto aktivit investovat, aby se zlepšily schopnosti zásad správného řízení konzistence prostředků.

> [!CAUTION]
> Minimální ani potenciální aktivity, které jsou uvedené v tomto článku, jsou zarovnané na konkrétní podnikové zásady nebo požadavky na dodržování předpisů třetích stran. Tento návod je navržený tak, aby usnadnil konverzace, které vedou k vyrovnání obou požadavků s modelem zásad správného řízení pro Cloud.

## <a name="planning-and-readiness"></a>Plánování a připravenost

Tato fáze předběžných postupů řízení vypořádání mostů mezi obchodními výsledky a strategiemi, které se s nimi možné. Během tohoto procesu vedoucí týmu definuje konkrétní metriky, mapuje tyto metriky na digitální nemovitosti a zahájí plánování celkové snahy o migraci.

**Minimální navrhované aktivity:**

- Vyhodnoťte možnosti [Sada nástrojů konzistence prostředků](./toolchain.md) .
- Seznamte se s požadavky na licencování pro vaši cloudovou strategii.
- Vývoj konceptu pokynů k architektuře a distribuce pro klíčové účastníky
- Seznamte se s Resource managerem, který používáte k nasazení, správě a monitorování všech prostředků pro vaše řešení jako skupiny.
- Informujte a zapojte lidi a týmy, kterých se týkalo vývoje pokynů pro architekturu.
- Přidejte úlohy nasazování prostředků s upřednostněním prostředků do nevyřízených položek migrace.

**Potenciální aktivity:**

- Spolupracujte se svými podnikovými stranami a týmem vaší cloudové strategie, abyste porozuměli požadovaným přístupům ke cloudovým účetním a cenovým postupům v rámci obchodních jednotek a organizací.
- Definujte požadavky na [monitorování a vynucování zásad](./compliance-processes.md) .
- Projděte si obchodní hodnotu a náklady na výpadky a definujte zásady oprav a požadavky smlouvy SLA.
- Určete, jestli pro vaše prostředky nasadíte [jednoduchou úlohu](./governance-simple-workload.md) nebo více strategií zásad správného řízení [týmu](./governance-multiple-teams.md) .
- Určete požadavky na škálovatelnost pro plánované úlohy.

## <a name="build-and-predeployment"></a>Sestavení a přednasazení

K úspěšné migraci prostředí se vyžaduje několik technických a netechnických požadavků. Tento proces se zaměřuje na rozhodování, připravenost a základní infrastrukturu, která pokračuje v migraci.

**Minimální navrhované aktivity:**

- Implementaci [Sada nástrojů konzistence prostředků](./toolchain.md) Implementujte ve fázi předinstalace.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Implementujte úlohy nasazení prostředků ve vašich nevyřízených položkách migrace s určenou prioritou.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů

**Potenciální aktivity:**

- Rozhodněte se na [strategii návrhu předplatného](../../decision-guides/subscriptions/index.md)a vyberte vzory předplatného, které nejlépe vyhovují vašim potřebám vaší organizace a úloh.
- Využijte strategii [konzistence prostředků](../../decision-guides/resource-consistency/index.md) k vymáhání pokynů architektury v průběhu času.
- Implementujte [vytváření názvů prostředků a zaznačení standardů](../../decision-guides/resource-tagging/index.md) pro vaše prostředky tak, aby odpovídaly požadavkům vaší organizace a účetnictví.
- Chcete-li vytvořit proaktivní zásady správného řízení k určitému bodu v čase, pomocí šablon nasazení a automatizace vyjistěte, aby při nasazování zdrojů a skupin prostředků vynutila společné konfigurace a jednotnou strukturu seskupení.
- Navažte model oprávnění s minimálními oprávněními, kde uživatelé nemají ve výchozím nastavení žádná oprávnění.
- Určete, kdo ve vaší organizaci má vlastní každou úlohu a účet a kdo bude potřebovat přístup k údržbě nebo úpravě těchto prostředků. Definujte role a zodpovědnosti cloudu, které odpovídají těmto potřebám, a použijte tyto role jako základ pro řízení přístupu.
- Definujte závislosti mezi prostředky.
- Implementujte automatizované škálování prostředků, aby odpovídaly požadavkům definovaným ve fázi plánování.
- Vykonávání výkonu přístupu k měření kvality přijatých služeb.
- Zvažte nasazení [zásad](https://docs.microsoft.com/azure/governance/policy/overview) pro správu vynucování smlouvy SLA pomocí nastavení konfigurace a pravidel vytváření prostředků.

## <a name="adopt-and-migrate"></a>Přijmout a migrovat

Migrace je přírůstkový proces, který se zaměřuje na přesun, testování a přijetí aplikací nebo úloh v existující digitální nemovitosti.

**Minimální navrhované aktivity:**

- Migrujte [konzistenci prostředků sada nástrojů](./toolchain.md) z předplatného do produkčního prostředí.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů
- Migrujte všechny existující skripty nebo nástroje pro automatizované opravy, aby podporovaly definované požadavky smlouvy SLA.

**Potenciální aktivity:**

- Dokončete a otestujte data pro monitorování a vytváření sestav s vámi zvolenou místní, cloudovou bránou nebo hybridním řešením.
- Zjistěte, jestli je potřeba udělat změny v zásadách SLA nebo správy pro prostředky.
- Implementací možností dotazů můžete zlepšit úlohy operací a efektivně tak najít prostředek napříč vaší cloudovou vlastností.
- Zarovnejte prostředky s cílem změnit obchodní potřeby a požadavky zásad správného řízení.
- Ujistěte se, že vaše virtuální počítače, virtuální sítě a účty úložiště odrážejí skutečné požadavky na přístup k prostředkům během každé vydané verze a podle potřeby je upravte.
- Ověřte, že automatické škálování prostředků splňuje požadavky na přístup.
- Zkontrolujte přístup uživatelů k prostředkům, skupinám prostředků a předplatným Azure a podle potřeby upravte řízení přístupu.
- Sledujte změny v plánech přístupu k prostředkům a ověřte je u zúčastněných stran, pokud potřebujete další odhlašování.
- Aktualizujte změny v dokumentu s pokyny k architektuře, aby odrážely skutečné náklady.
- Určete, jestli vaše organizace vyžaduje pro jednotky P & LS pro firmy jasné finanční zarovnání.
- U globálních organizací implementujte požadavky na dodržování předpisů a požadavky na svrchovanost (SLA).
- Pro agregaci cloudu nasaďte řešení brány k poskytovateli cloudu.
- Pro nástroje, které neumožňují možnosti hybridního řešení nebo brány, úzce propojíme monitorování s nástrojem Operational monitoring, který zahrnuje všechna datová centra a cloudy.

## <a name="operate-and-post-implementation"></a>Provoz a následné implementace

Po dokončení transformace musí být zásady správného řízení a provoz v provozu v rámci přirozeného životního cyklu aplikace nebo zátěže. Tato fáze řízení splatnosti se zaměřuje na aktivity, které se běžně přidávají po implementaci řešení, a cyklus transformace začíná stabilizovat.

**Minimální navrhované aktivity:**

- Přizpůsobte [konzistenci prostředků sada nástrojů](./toolchain.md) na základě aktualizací potřeb vaší organizace na změnu cost management.
- Zvažte automatizaci všech oznámení a sestav, které odrážejí skutečné využití prostředků.
- Upřesněte pokyny k architekturám a provedou budoucí procesy přijímání.
- Pravidelně informovat týmy, aby se zajistilo průběžné dodržování pravidel architektury.

**Potenciální aktivity:**

- Upravte plány čtvrtletním tak, aby odrážely změny skutečných prostředků.
- Automaticky aplikujte a vynutili požadavky zásad správného řízení v budoucích nasazeních.
- Vyhodnoťte nevyužité prostředky a určete, jestli jsou v činnosti pokračovat.
- Zjistíte chybné zarovnání a anomálie mezi plánovaným a skutečným využitím prostředků.
- Pomůže týmům při přijímání cloudu a týmu cloudové strategie pochopit a řešit tyto anomálie.
- Určete, jestli je potřeba udělat změny v konzistenci prostředků pro fakturaci a SLA.
- Vyhodnoťte nástroje protokolování a monitorování, abyste zjistili, jestli je potřeba upravit místní, cloudovou bránu nebo hybridní řešení.
- V případě obchodních jednotek a geograficky distribuovaných skupin určete, jestli by vaše organizace měla zvážit použití dalších funkcí správy cloudu, jako jsou [skupiny pro správu Azure](https://docs.microsoft.com/azure/governance/management-groups) , aby lépe používaly centralizované zásady a splňovaly požadavky smlouvy SLA.

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte konceptu zásad správného řízení prostředků v cloudu, můžete přejít na Další informace o [tom, jak se v Azure spravuje přístup k prostředkům](./resource-access-management.md) v tématu Příprava pro učení, jak navrhnout model zásad správného řízení pro [jednoduchou úlohu](./governance-simple-workload.md) nebo pro [více týmů](./governance-multiple-teams.md).

> [!div class="nextstepaction"]
> Přečtěte [si o správě přístupu k prostředkům v azure](./resource-access-management.md)
> [informace o smlouvách o úrovni služeb pro Azure](https://azure.microsoft.com/support/legal/sla)
> [informace o protokolování, vytváření sestav a monitorování](../../decision-guides/logging-and-reporting/index.md) .
