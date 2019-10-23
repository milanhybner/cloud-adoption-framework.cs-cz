---
title: Kontrolní seznam pro rozšířený rozsah migrace do cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Kontrolní seznam pro rozšířený rozsah migrace do cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ee164f75b4f3748fce027d0c6c98db5200dcdd71
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548501"
---
# <a name="expanded-scope-for-cloud-migration"></a>Rozšířený rozsah pro migraci do cloudu

Čtenářům, kteří mají zájem o migraci do Azure změnou hostitele, která se označuje také jako migrace metodou „lift and shift“, jako výchozí bod doporučujeme [Průvodce migrací do Azure](../azure-migration-guide/index.md) v architektuře přechodu na cloud. Tento průvodce vás provede řadou požadavků, nástrojů a přístupů k migraci virtuálních počítačů do cloudu.

Tento průvodce představuje efektivní směrný plán, který vám umožní seznámit se s tímto typem migrace, ale platí pro něj několik předpokladů. Tyto předpoklady zajišťují, že tento průvodce je vhodný pro řadu čtenářů architektury přechodu na cloud, protože poskytuje zjednodušený přístup k migracím. Tato část architektury přechodu na cloud se zabývá několika rozšířenými scénáři migrace, které vám pomůžou směrovat vaše úsilí v případech, kdy tyto předpoklady neplatí.

## <a name="cloud-migration-expanded-scope-checklist"></a>Kontrolní seznam pro rozšířený rozsah migrace do cloudu

Následující kontrolní seznam popisuje běžné složité oblasti, které můžou vyžadovat rozšíření rozsahu migrace nad rámec [průvodce migrací do Azure](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>Rozšíření rozsahu řízené obchodními procesy

- **[Vyvážení portfolia:](./balance-the-portfolio.md)** Tým cloudové strategie se zajímá o výraznější investice do migrace (změnou hostitele stávajících úloh a aplikací s minimem úprav) nebo inovací (refaktorováním nebo opětovným sestavením těchto úloh a aplikací s využitím moderních cloudových technologií). Často je klíčem k úspěchu najít správnou rovnováhu mezi těmito dvěma prioritami. V tomto průvodci je téma vyvážení portfolia přechodu na cloud společné a řeší se v každém procesu migrace.
- **[Podpora globálních trhů:](../../decision-guides/regions/index.md)** Firma působí v několika geografických oblastech s různorodými požadavky na suverenitu dat. Aby bylo možné splnit tyto požadavky, při kontrole požadavků a distribuci prostředků během migrace je potřeba vzít v úvahu další aspekty.

### <a name="technology-driven-scope-expansion"></a>Rozšíření rozsahu řízené technologiemi

- **[Migrace VMWare:](./vmware-host.md)** Migrace hostitelů VMWare dokáže celkový proces migrace zrychlit. Každý migrovaný hostitel VMWare může do cloudu pomocí přístupu „lift and shift“ přesunout několik úloh. Po dokončení migrace mohou tyto virtuální počítače a úlohy zůstat ve VMWare nebo se migrovat na moderní cloudové možnosti.
- **[Migrace SQL Serveru:](./sql-migration.md)** Migrace SQL Serverů dokáže celkový proces migrace zrychlit. Každý migrovaný SQL Server může přesunout několik databází a služeb a potenciálně tak zrychlit několik úloh.
- **[Několik datacenter:](./multiple-datacenters.md)** Migrace několika datacenter výrazně přidává na složitosti. Během procesů posouzení, migrace, optimalizace a správy se v rámci přípravy na složitější prostředí probírají další aspekty.
- **[Požadavky na data překračující kapacitu sítě:](./network-capacity-exceeded.md)** Společnosti často volí migraci do cloudu kvůli nevyhovující kapacitě, rychlosti a stabilitě stávajícího datacentra. Stejná omezení však bohužel přidávají na složitosti procesu migrace, protože vyžadují dodatečné plánování během procesů posouzení a migrace.
- **[Strategie pro zásady správného řízení nebo dodržování předpisů:](./governance-or-compliance.md)** Pokud jsou pro úspěch migrace potřeba zásady správného řízení a dodržování předpisů, vyžaduje se další sladění mezi týmy zásad správného řízení v oblasti IT a týmem přechodu na cloud.

Pokud se některé z těchto složitostí týkají vašeho scénáře, pak v této části architektury přechodu na cloud pravděpodobně najdete potřebné pokyny pro sladění rozsahu v procesech migrace.

Každému z těchto scénářů se věnuje samostatný článek v této části architektury přechodu na cloud.

## <a name="next-steps"></a>Další kroky

Pokud hledáte řešení konkrétních požadavků nebo změn rozsahu, projděte si obsah na levé straně. Případně pokud si chcete projít tyto scénáře, můžete začít prvním vylepšením rozsahu v seznamu – [Vyvážení portfolia](./balance-the-portfolio.md).

> [!div class="nextstepaction"]
> [Vyvážení portfolia](./balance-the-portfolio.md)
