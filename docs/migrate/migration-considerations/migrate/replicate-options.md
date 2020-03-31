---
title: Možnosti replikace
description: K pochopení procesu replikace a k tomu, proč potřebujete replikaci pro migraci do cloudu, použijte rozhraní pro přijetí cloudu pro Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 584ac5e962c9432e6a1824b3cbb88ff7cb24a35f
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432525"
---
# <a name="replication-options"></a>Možnosti replikace

Před každou migrací byste měli zkontrolovat, že jsou primární systémy v pořádku a budou i nadále bez problémů fungovat. Jakékoli výpadky ruší uživatele nebo zákazníky a stojí čas a peníze. Migrace nespočívá prostě jen v tom, že vypnete virtuální počítače v místním prostředí a zkopírujete je do Azure. Nástroje pro migraci musí brát v úvahu asynchronní nebo synchronní replikaci, aby se zajistilo, že aktivní systémy bude možné do Azure zkopírovat bez výpadků. Ze všeho nejdůležitější je, aby systémy zůstaly správně propojené s místními protějšky. Migrované prostředky byste možná měli otestovat v izolovaných oddílech v Azure, abyste se ujistili, že úlohy fungují podle očekávání.

Obsah v rámci architektury přijetí cloudu předpokládá, že Azure Migrate (nebo Azure Site Recovery) je nejvhodnějším nástrojem pro replikaci prostředků do cloudu. K dispozici jsou ale i další možnosti. Tento článek tyto možnosti popisuje, aby vám pomohl při rozhodování.

## <a name="azure-site-recovery-also-known-as-azure-migrate"></a>Azure Site Recovery (známý také jako Azure Migrate)

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) organizuje a spravuje zotavení po havárii pro virtuální počítače Azure, místní virtuální počítače a fyzické servery. Site Recovery můžete použít také ke správě migrace místních počítačů a jiných poskytovatelů cloudu do Azure. Replikujte místní počítače do Azure nebo virtuální počítače Azure do sekundární oblasti. Pak necháte služby virtuálního počítače převzít z primární lokality do sekundární a proces migrace dokončíte. Pomocí Azure Site Recovery můžete dosáhnout různých scénářů migrace:

- **Migrace z místního prostředí do Azure.** Migrace místních virtuálních počítačů VMware, virtuálních počítačů Hyper-V a fyzických serverů do Azure. Ta se provede tak, že dokončíte téměř stejné kroky jako při úplném zotavení po havárii. Jednoduše neprovedete převzetí počítačů při selhání zpátky z Azure do místní lokality.
- **Migrace mezi oblastmi Azure.** Migrace virtuálních počítačů Azure z jedné oblasti Azure do jiné. Po dokončení migrace nakonfigurujte zotavení po havárii pro virtuální počítače Azure tentokrát v sekundární oblasti, do které jste migrovali.
- **Migrace z jiného cloudu do Azure.** Můžete migrovat své výpočetní instance zřízené u jiných poskytovatelů cloudu na virtuální počítače Azure. Site Recovery s těmito instancemi pro účely migrace zachází jako s fyzickými servery.

![Azure Site Recovery](../../../_images/migrate/asr-replication-image.png)
*Azure Site Recovery přesouvající prostředky do Azure nebo jiných cloudů*

Potom co vyhodnotíte místní a cloudovou infrastrukturu pro migraci, Azure Site Recovery přispějete k vaší strategii migrace replikací místních počítačů. Pomocí následujících jednoduchých kroků můžete nastavit migraci místních virtuálních počítačů, fyzických serverů a instancí cloudových virtuálních počítačů do Azure:

- Ověřte požadavky.
- Připravte prostředky Azure.
- Připravte místní virtuální počítače nebo cloudové instance pro migraci.
- Nasaďte konfigurační server.
- Povolte replikace pro virtuální počítače.
- Otestujte převzetí služeb při selhání, aby bylo jisté, že všechno funguje.
- Spusťte jednorázové převzetí služeb při selhání do Azure.

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Tato služba pomáhá zjednodušit migraci do cloudu pomocí jediné komplexní služby místo řady různých nástrojů. Služba [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) je navržená jako bezproblémové a ucelené řešení pro přesun místních databází SQL Serveru do cloudu. Jedná se o plně spravovanou službu, která má umožňovat bezproblémové migrace z více zdrojů databáze na datové platformy Azure s minimální dobou vyřazení z provozu. Integruje některé funkce stávajících nástrojů a služeb a poskytuje zákazníkům komplexní řešení s vysokou dostupností.

Služba používá nástroj Data Migration Assistant k vygenerování sestav vyhodnocení poskytujících doporučení, která vás provedou nutnými změnami před provedením migrace. Provedení jakékoli požadované nápravy záleží na vás. Až budete připraveni zahájit proces migrace, Azure Database Migration Service provede všechny s tím spojené kroky. Své projekty migrace můžete v klidu spustit a dál je neřešit, protože proces využívá osvědčené postupy podle zkušeností Microsoftu.

## <a name="next-steps"></a>Další kroky

Po dokončení replikace můžou začít [přípravné aktivity](./stage.md).

> [!div class="nextstepaction"]
> [Přípravné aktivity během migrace](./stage.md)
