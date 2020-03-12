---
title: Osvědčené postupy migrace do Azure
description: Využijte architekturu přechodu na cloud pro Azure k seznámení s tím, jak implementovat nástroje nezbytné pro sladění s osvědčenými postupy pro migraci do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 90ec573d59c88187081fd640d9eb769977b787cf
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79091426"
---
# <a name="best-practices-for-cloud-migration"></a>Osvědčené postupy pro migraci do cloudu

Pokud vás zajímá migrace do Azure, doporučeným výchozím bodem v rámci architektury přechodu na cloud je [průvodce migrací do Azure](../azure-migration-guide/index.md). Tento průvodce vás provede řadou nástrojů a základních přístupů k migraci virtuálních počítačů do cloudu. Tato část architektury přechodu na cloud se zaměřuje na celou řadu osvědčených postupů, které jdou nad rámec základních nástrojů nativních pro cloud.

## <a name="cloud-migration-best-practice-checklist"></a>Kontrolní seznam osvědčených postupů pro migraci do cloudu

Následující kontrolní seznam popisuje běžné složité situace, které mohou vyžadovat rozšíření rozsahu migrace nad rámec [průvodce migrací do Azure](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>Rozšíření rozsahu řízené obchodními procesy

- **[Podpora globálních trhů:](./multiple-regions.md)** Firma působí v několika geografických oblastech s různorodými požadavky na suverenitu dat. Aby bylo možné splnit tyto požadavky, při kontrole požadavků a distribuci prostředků během migrace je potřeba vzít v úvahu další aspekty.

### <a name="technology-driven-scope-expansion"></a>Rozšíření rozsahu řízené technologiemi

- **[Migrace VMware:](./vmware-host.md)** Migrace hostitelů VMware dokáže celkový proces migrace zrychlit. Každý migrovaný hostitel VMware může do cloudu pomocí přístupu „lift and shift“ přesunout několik úloh. Po dokončení migrace mohou tyto virtuální počítače a úlohy zůstat ve VMware nebo se migrovat na moderní cloudové možnosti.
- **[Migrace SQL Serveru:](./sql-migration.md)** Migrace SQL Serverů dokáže celkový proces migrace zrychlit. Každý migrovaný SQL Server může přesunout několik databází a služeb a potenciálně tak zrychlit několik úloh.
- **[Několik datacenter:](./multiple-datacenters.md)** Migrace několika datacenter výrazně přidává na složitosti. Během procesů posouzení, migrace, optimalizace a správy se v rámci přípravy na složitější prostředí probírají další aspekty.
- **[Požadavky na data překračující kapacitu sítě:](./network-capacity-exceeded.md)** Společnosti často volí migraci do cloudu kvůli nevyhovující kapacitě, rychlosti a stabilitě stávajícího datacentra. Stejná omezení však bohužel přidávají na složitosti procesu migrace, protože vyžadují dodatečné plánování během procesů posouzení a migrace.
- **[Strategie pro zásady správného řízení nebo dodržování předpisů:](./governance-or-compliance.md)** Pokud jsou pro úspěch migrace potřeba zásady správného řízení a dodržování předpisů, vyžaduje se další sladění mezi týmy zásad správného řízení v oblasti IT a týmem přechodu na cloud.

Pokud se některé z těchto složitostí týkají vašeho scénáře, pak v této části architektury přechodu na cloud pravděpodobně najdete potřebné pokyny pro sladění rozsahu v procesech migrace.

Každému z těchto scénářů se věnuje samostatný článek v této části architektury přechodu na cloud.

## <a name="next-steps"></a>Další kroky

Pokud hledáte řešení konkrétních požadavků nebo změn rozsahu, projděte si obsah na levé straně. Případně pokud si chcete projít tyto scénáře, můžete začít prvním vylepšením rozsahu v seznamu – [Podpora globálních trhů](./multiple-regions.md).

> [!div class="nextstepaction"]
> [Podpora globálních trhů](./multiple-regions.md)
