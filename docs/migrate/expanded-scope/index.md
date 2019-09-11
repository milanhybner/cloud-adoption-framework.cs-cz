---
title: Kontrolní seznam pro rozšířený rozsah migrace do cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Kontrolní seznam pro rozšířený rozsah migrace do cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 125c6d044fd766896971aced5bedbc515c14417f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817328"
---
# <a name="expanded-scope-for-cloud-migration"></a>Rozšířený rozsah pro migraci do cloudu

Čtenářům, kteří mají zájem o migraci do Azure změnou hostitele, která se označuje také jako migrace metodou „lift and shift“, jako výchozí bod doporučujeme [Průvodce migrací do Azure](../azure-migration-guide/index.md) v architektuře přechodu na cloud. Tento průvodce vás provede řadou požadavků, nástrojů a přístupů k migraci virtuálních počítačů do cloudu.

Tento průvodce představuje efektivní směrný plán, který vám umožní seznámit se s tímto typem migrace, ale platí pro něj několik předpokladů. Tyto předpoklady zajišťují, aby byl průvodce vhodný pro naprostou většinu čtenářů architektury přechodu na cloud díky tomu, že poskytuje zjednodušený přístup k migracím. Tato část architektury přechodu na cloud se zabývá několika rozšířenými scénáři migrace, které vám pomůžou směrovat vaše úsilí v případech, kdy tyto předpoklady neplatí.

## <a name="cloud-migration-expanded-scope-checklist"></a>Kontrolní seznam pro rozšířený rozsah migrace do cloudu

Následující kontrolní seznam popisuje běžné složité oblasti, které můžou vyžadovat rozšíření rozsahu migrace nad rámec [průvodce migrací do Azure](../azure-migration-guide/index.md).

- **Obchodní změny rozsahu:**
  - [Vyvážení portfolia](./balance-the-portfolio.md)
  - [Podpora globálních trhů](./multiple-regions.md)
  - Povědomí o nákladech během migrace *(připravujeme pro 3. čtvrtletí 2019)*
- **Změny rozsahu na základě kultury:**
  - Procesy správy a schvalování změn *(připravujeme pro 3. čtvrtletí 2019)*
  - Administrativní připravenost *(připravujeme pro 3. čtvrtletí 2019)*
  - [Připravenost dovedností](./suggested-skills.md)
  - Sladění podpory (partneři, služby a podpora) *(připravujeme pro 3. čtvrtletí 2019)*
- **Změny rozsahu na základě technické strategie:**
  - Omezení stávajících datacenter *(připravujeme pro 3. čtvrtletí 2019)*
  - Migrace ve velkém měřítku – Velkoobjemové nebo vysokorychlostní migrace *(připravujeme pro 3. čtvrtletí 2019)*
  - [Několik datacenter](./multiple-datacenters.md)
  - [Požadavky na data překračují kapacitu sítě](./network-capacity-exceeded.md)
  - Správa změn a dokumentace k řešení *(připravujeme pro 3. čtvrtletí 2019)*
  - [Strategie zásad správného řízení nebo dodržování předpisů](./governance-or-compliance.md)
- **Změny rozsahu na základě konkrétních úloh:**
  - Vytváření úloh s ohledem na odolnost *(připravujeme pro 3. čtvrtletí 2019)*
  - Přizpůsobení migrace vzorům aplikací *(připravujeme pro 3. čtvrtletí 2019)*

Pokud se některé z těchto složitostí týkají vašeho scénáře, pak v této části architektury přechodu na cloud pravděpodobně najdete potřebné pokyny pro sladění rozsahu v procesech migrace.

Každému z těchto scénářů se věnuje samostatný článek v této části architektury přechodu na cloud.

## <a name="scope-options-explained"></a>Vysvětlení možností z hlediska rozsahu

Následující seznam obsahuje stručný souhrn názvů použitých ve výše uvedeném kontrolním seznamu a pomůže vám porozumět jednotlivým scénářům rozšíření rozsahu.

### <a name="business-driven-scope-changes"></a>Obchodní změny rozsahu

- **Vyvážení portfolia přechodu na cloud:** Tým cloudové strategie se zajímá o výraznější investice do migrace (změnou hostitele stávajících úloh a aplikací s minimem úprav) nebo inovací (refaktorováním nebo opětovným sestavením těchto úloh a aplikací s využitím moderních cloudových technologií). Často je klíčem k úspěchu najít správnou rovnováhu mezi těmito dvěma prioritami. V tomto průvodci je téma vyvážení portfolia přechodu na cloud společné a řeší se v každém procesu migrace.
- **Podpora globálních trhů:** Firma působí v několika geografických oblastech s různorodými požadavky na suverenitu dat. Aby bylo možné splnit tyto požadavky, při kontrole požadavků a distribuci prostředků během migrace je potřeba vzít v úvahu další aspekty.

### <a name="culture-driven-scope-changes"></a>Změny rozsahu na základě kultury

- **Procesy správy a schvalování změn:** Pokud je kultura vaší organizace složitá, velmi roztříštěná nebo izolovaná, můžou být procesy související se správou a schvalováním změn poměrně složité. Pokyny ke zvládnutí této složitosti najdete v procesech posouzení, migrace a optimalizace.
- **Administrativní připravenost:** Správně nastavené úrovně administrativní podpory a vedení jsou klíčové pro úspěch migrace. Pokud administrativní tým není připravený se zapojit, podpory se pravděpodobně nedočkáte. Tato složitost se řeší během procesů zajištění požadavků a posouzení.
- **Připravenost dovedností:** Pokud tým přechodu na cloud nebo jiné podpůrné týmy nejsou připravené k realizaci, může to rychle vnést složitost do celého procesu migrace. Tato výzva se řeší během jednotlivých procesů migrace na samostatné stránce o připravenosti dovedností.
- **Sladění podpory (partneři, služby a možnosti podpory):** V rámci všech popisovaných procesů existují způsoby, jak můžou partneři, služby od dodavatelů cloudu a podpora od dodavatele cloudu přispět k realizaci. Podrobnější popis těchto možností najdete v částech věnovaných jednotlivým procesům na stránce o sladění podpory.

### <a name="technical-strategy-driven-scope-changes"></a>Změny rozsahu na základě technické strategie

- **Omezení stávajících datacenter:** Společnosti často volí migraci do cloudu kvůli nevyhovující kapacitě, rychlosti a stabilitě stávajícího datacentra. Stejná omezení však bohužel přidávají na složitosti procesu migrace, protože vyžadují dodatečné plánování během procesů posouzení a migrace.
- **Migrace ve velkém měřítku:** Migrace přesahující 2 000 prostředků pravděpodobně narazí na omezení vyžadující dodatečné plánování a disciplinovaný přístup k realizaci. Procesy posouzení a migrace jsou upravené s ohledem na složitost škálování.
- **Několik datacenter:** Migrace několika datacenter výrazně přidává na složitosti. Během procesů posouzení, migrace, optimalizace a správy se věnujeme dalším aspektům.
- **Správa změn a dokumentace k řešení:** Rozsáhlé inventáře cloudových aktiv, komplexní architektury řešení, dlouhodobý technický dluh a vzájemné závislosti můžou vytvořit složitost, která by se měla řešit během procesů posouzení, migrace a optimalizace.
- **Strategie zásad správného řízení nebo dodržování předpisů:** Pokud jsou pro úspěch migrace potřeba zásady správného řízení a dodržování předpisů, vyžaduje se další sladění mezi týmy zásad správného řízení v oblasti IT a týmem přechodu na cloud.

### <a name="workload-specific-scope-changes"></a>Změny rozsahu na základě konkrétních úloh

- **Vytváření úloh s ohledem na odolnost:** Běžné principy cloudového návrhu můžou pomoct připravit klíčové úlohy na vyšší odolnost. Tento článek vysvětluje vliv na proces migrace v případě, že je odolnost požadavkem úlohy. Kromě toho uvádí několik běžných principů, které by se měly zahrnout do obecné konfigurace prostředí, aby se zlepšila jeho odolnost.
- **Přizpůsobení migrace vzorům aplikací:** Vzor migrace úlohy může ovlivnit výběr cesty k migraci. Tento článek popisuje několik změn rozsahu, které by se pro různé přístupy k migraci jednotlivých úloh integrovaly do backlogu migrace na úrovni pracovní položky.

## <a name="next-steps"></a>Další kroky

Pokud hledáte řešení konkrétních požadavků nebo změn rozsahu, projděte si obsah na levé straně. Případně pokud si chcete projít tyto scénáře, můžete začít prvním vylepšením rozsahu v seznamu – [Vyvážení portfolia](./balance-the-portfolio.md).

> [!div class="nextstepaction"]
> [Vyvážení portfolia](./balance-the-portfolio.md)
