---
title: Vylepšení oboru směrného plánu zabezpečení
description: Vylepšení oboru směrného plánu zabezpečení
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 316a848e0f9f3f90a2f7badde3166733dce4a4c0
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808902"
---
# <a name="security-baseline-discipline-improvement"></a>Vylepšení oboru směrného plánu zabezpečení

Základ směrného plánu zabezpečení se zaměřuje na způsoby vytváření zásad, které chrání síť, prostředky a nejdůležitější data, která se budou nacházet v řešení poskytovatele cloudu. V pěti oborech zásad správného řízení cloudu zahrnuje standardní hodnoty zabezpečení klasifikaci digitálních nemovitostí a dat. Zahrnuje taky dokumentaci rizik, obchodní tolerance a strategie zmírňování, které souvisejí s bezpečností dat, prostředků a sítě. Z technického hlediska to zahrnuje také zapojení do rozhodnutí týkajících se [šifrování](../../decision-guides/encryption/index.md), [požadavků na síť](../../decision-guides/software-defined-network/index.md), [strategií hybridních identit](../../decision-guides/identity/index.md)a [procesů](./compliance-processes.md) používaných k vývoji zásad standardních hodnot zabezpečení cloudu.

Tento článek popisuje některé možné úkoly, které může vaše společnost zapojit do vývoje a vyspělosti směrného plánu zabezpečení. Tyto úlohy je možné rozdělit na plánování, sestavování, přijímání a provozní fáze implementace cloudového řešení, které se pak iterovat na to, že umožní vývoj [přírůstkového přístupu ke správě cloudu](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Čtyři fáze přijetí](../../_images/govern/adoption-phases.png)

*Obrázek 1 – fáze přijetí přírůstkového přístupu ke zásadám správného řízení cloudu.*

U každého dokumentu není možné brát v úvahu požadavky všech společností. Tento článek popisuje navrhované minimální a potenciální příklady aktivit pro každou fázi procesu maturation zásad správného řízení. Počáteční cíl těchto aktivit vám pomůže vytvořit [MVP pro zásady](../guides/index.md#an-incremental-approach-to-cloud-governance) a vytvořit rozhraní pro přírůstkové zlepšování zásad. Váš tým zásad správného řízení vašeho cloudu bude muset rozhodnout, kolik z nich investovat do těchto aktivit, aby vylepšilo možnosti zásad správného řízení zabezpečení.

> [!CAUTION]
> Minimální ani potenciální aktivity, které jsou uvedené v tomto článku, jsou zarovnané na konkrétní podnikové zásady nebo požadavky na dodržování předpisů třetích stran. Tento návod je navržený tak, aby usnadnil konverzace, které vedou k vyrovnání obou požadavků s modelem zásad správného řízení pro Cloud.

## <a name="planning-and-readiness"></a>Plánování a připravenost

Tato fáze předběžných postupů řízení vypořádání mostů mezi obchodními výsledky a strategiemi, které se s nimi možné. Během tohoto procesu vedoucí týmu definuje konkrétní metriky, mapuje tyto metriky na digitální nemovitosti a zahájí plánování celkové snahy o migraci.

**Minimální navrhované aktivity:**

- Vyhodnoťte možnosti [Sada nástrojů standardních hodnot zabezpečení](./toolchain.md) .
- Vývoj konceptu pokynů k architektuře a distribuce pro klíčové účastníky
- Informujte a zapojte lidi a týmy, kterých se týkalo vývoje pokynů pro architekturu.
- Přidejte úkoly zabezpečení podle priorit do nevyřízených položek migrace.

**Potenciální aktivity:**

- Definujte schéma klasifikace dat.
- V rámci procesu plánování digitálních věcí můžete vystavit aktuální prostředky IT, které řídí vaše obchodní procesy a podpůrné operace.
- [Proveďte revizi zásad](../../govern/policy-compliance/cloud-policy-review.md) a zahajte proces modernizaci stávajících podnikových zásad zabezpečení IT a DEFINUJTE zásady MVP, které řeší známá rizika.
- Projděte si pokyny pro zabezpečení cloudové platformy. Pro Azure najdete je na [platformě Microsoft Service Trust](https://www.microsoft.com/trustcenter/stp/default.aspx).
- Určete, jestli vaše zásada standardních hodnot zabezpečení zahrnuje [životní cyklus vývoje zabezpečení](https://www.microsoft.com/securityengineering/sdl).
- Vyhodnotit podniková rizika pro síť, data a prostředky v závislosti na dalších až třech verzích a posoudit u těchto rizik toleranci vaší organizace.
- Seznamte se s hlavními [trendy Microsoftu v sestavě kyberbezpečnosti](https://www.microsoft.com/security/operations/security-intelligence-report) , abyste získali přehled o aktuálním zabezpečení na úrovni.
- Zvažte vývoj [DevOps role zabezpečení](https://www.microsoft.com/en-us/securityengineering/devsecops) ve vaší organizaci.

<!-- "en-us" location is required for the URL above. -->

## <a name="build-and-predeployment"></a>Sestavení a přednasazení

K úspěšné migraci prostředí se vyžaduje několik technických a netechnických požadavků. Tento proces se zaměřuje na rozhodování, připravenost a základní infrastrukturu, která pokračuje v migraci.

**Minimální navrhované aktivity:**

- Implementujte [Sada nástrojů standardních hodnot zabezpečení](./toolchain.md) , a to tak, že zavedete do fáze předinstalace.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Implementujte úlohy zabezpečení ve vašich nevyřízených položkách migrace s určenou prioritou.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů

**Potenciální aktivity:**

- Určete strategii [šifrování](../../decision-guides/encryption/index.md) vaší organizace pro data hostovaná v cloudu.
- Vyhodnoťte strategii [identity](../../decision-guides/identity/index.md) nasazení v cloudu. Určete, jak bude vaše cloudové řešení identity fungovat, nebo se bude integrovat s místními zprostředkovateli identity.
- Určete zásady ohraničení sítě pro návrh [SDN (Software Defined Networking)](../../decision-guides/software-defined-network/index.md) , aby se zajistila bezpečnost virtualizovaných síťových možností.
- Vyhodnoťte zásady [přístupu pro nejnižší oprávnění](https://docs.microsoft.com/azure/active-directory/users-groups-roles/roles-delegate-by-task) vaší organizace a použijte role založené na úlohách k poskytnutí přístupu ke konkrétním prostředkům.
- Použijte mechanismy zabezpečení a monitorování pro všechny cloudové služby a virtuální počítače.
- Automatizace [zásad zabezpečení](../../decision-guides/policy-enforcement/index.md) , pokud je to možné.
- Zkontrolujte zásady standardních hodnot zabezpečení a určete, jestli potřebujete upravit plány podle pokynů pro osvědčené postupy, jako jsou ty, které jsou uvedené v [životním cyklu vývoje zabezpečení](https://www.microsoft.com/securityengineering/sdl).

## <a name="adopt-and-migrate"></a>Přijmout a migrovat

Migrace je přírůstkový proces, který se zaměřuje na přesun, testování a přijetí aplikací nebo úloh v existující digitální nemovitosti.

**Minimální navrhované aktivity:**

- Migrujte [základní sada nástrojů zabezpečení](./toolchain.md) z předplatného do produkčního prostředí.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů

**Potenciální aktivity:**

- Projděte si nejnovější informace o základní úrovni zabezpečení a hrozbách a Identifikujte nová obchodní rizika.
- Vyměřte toleranci vaší organizace za účelem zpracování nových rizik zabezpečení, která mohou nastat.
- Identifikujte odchylky ze zásad a vynuťte opravy.
- Upravte zabezpečení a automatizaci řízení přístupu, abyste zajistili maximální dodržování zásad.
- Ověřte, zda jsou osvědčené postupy definované během fází sestavení a přednasazení správně provedeny.
- Zkontrolujte zásady přístupu k vašim minimálním oprávněním a upravte řízení přístupu, aby se maximalizovala bezpečnost.
- Otestujte základní sada nástrojů zabezpečení pro vaše úlohy a identifikujte a vyřešte případné chyby zabezpečení.

## <a name="operate-and-post-implementation"></a>Provoz a následné implementace

Po dokončení transformace musí být zásady správného řízení a provoz v provozu v rámci přirozeného životního cyklu aplikace nebo zátěže. Tato fáze řízení splatnosti se zaměřuje na aktivity, které se běžně přidávají po implementaci řešení, a cyklus transformace začíná stabilizovat.

**Minimální navrhované aktivity:**

- Ověřte a upřesněte [základní sada nástrojů zabezpečení](./toolchain.md).
- Přizpůsobte oznámení a sestavy, abyste zobrazili výstrahy na potenciální problémy se zabezpečením.
- Upřesněte pokyny k architektuře a provedou budoucí procesy přijímání.
- Pravidelně komunikujte a informujte dotčené týmy, aby se zajistilo průběžné dodržování pravidel architektury.

**Potenciální aktivity:**

- Seznamte se se vzorci a chováním vašich úloh a konfigurací nástrojů pro monitorování a vytváření sestav, které vám umožní identifikovat a upozorňovat na jakékoli neobvyklé aktivity, přístup nebo využití prostředků.
- Průběžně aktualizujte zásady monitorování a vytváření sestav, aby bylo možné zjistit nejnovější ohrožení zabezpečení, zneužití a útoky.
- Měli byste mít zavedeny postupy pro rychlé zastavení neoprávněného přístupu a zakázání prostředků, které by mohl útočník ohrozit.
- Pravidelně Projděte nejnovější osvědčené postupy zabezpečení a použijte doporučení pro vaše zásady zabezpečení, automatizaci a možnosti monitorování, pokud je to možné.

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte konceptu zásad správného řízení cloudového zabezpečení, přejděte na Další informace o [zásadách zabezpečení a osvědčených postupů, které Microsoft poskytuje](./azure-security-guidance.md) pro Azure.

> [!div class="nextstepaction"]
> [Přečtěte si informace o zásadách zabezpečení pro azure](./azure-security-guidance.md)
> [Úvod do zabezpečení Azure](https://docs.microsoft.com/azure/security/azure-security)
> [o protokolování, generování sestav a monitorování](../../decision-guides/logging-and-reporting/index.md) .
