---
title: Vyhodnocení připravenosti úloh
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proces v rámci migrace do cloudu, který se zaměřuje na úlohy prováděné při migraci sady funkcí do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 34d9cd3252849353b0fe765db4d84f7e9f2e5ea7
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549143"
---
# <a name="evaluate-workload-readiness"></a>Vyhodnocení připravenosti úloh

Tato aktivita se zaměřuje na připravenost úlohy k migraci do cloudu. Při této aktivitě tým přechodu na cloud ověří, jestli jsou všechny prostředky spolu s přidruženými závislostmi kompatibilní se zvoleným modelem nasazení a s poskytovatelem cloudových služeb. Během tohoto procesu tým zdokumentuje všechny úkoly potřebné k [nápravě](../migrate/remediate.md) problémů s kompatibilitou.

## <a name="evaluation-assumptions"></a>Východiska vyhodnocení

Většina obsahu, který vysvětluje principy architektury přechodu na cloud, se neomezuje jenom na cloud. Proces vyhodnocení připravenosti ale musí být z větší části specifický pro každou konkrétní cloudovou platformu. Následující pokyny předpokládají, že chcete migrovat do Azure. Dále předpokládají, že k [replikačním aktivitám](../migrate/replicate.md) použijete službu Azure Migrate (říká se jí také Azure Site Recovery). Alternativní nástroje najdete v [možnostech replikace](../migrate/replicate-options.md).

Záměrem tohoto článku není zaznamenat všechny možné vyhodnocovací aktivity. Předpokládá se, že každé prostředí a obchodní výsledky diktují konkrétní požadavky. Abychom pomohli tyto požadavky rychleji vytvořit, podělíme se ve zbývající části tohoto článku o několik nejčastějších vyhodnocovacích aktivit, které se týkají hodnocení [infrastruktury](#common-infrastructure-evaluation-activities), [databáze](#common-database-evaluation-activities) a [sítě](#common-network-evaluation-activities).

## <a name="common-infrastructure-evaluation-activities"></a>Běžné aktivity při vyhodnocení infrastruktury

- Požadavky VMware: [Přečtěte si požadavky na Azure Site Recovery pro VMware](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix).
- Požadavky na technologii Hyper-V: [Přečtěte si požadavky na Azure Site Recovery pro Hyper-v](https://docs.microsoft.com/azure/site-recovery/hyper-v-azure-support-matrix).

Nezapomeňte zdokumentovat všechny rozdíly v konfiguraci hostitele, v konfiguraci replikovaných virtuálních počítačů, dále požadavky na úložiště a konfiguraci sítě.

## <a name="common-database-evaluation-activities"></a>Běžné aktivity při vyhodnocení databáze

- Zdokumentujte cíle bodu a doby obnovení u aktuálně nasazené databáze. Použijete je při [aktivitách spojených s návrhem architektury](./architect.md) a pomůžou vám při rozhodování.
- Zdokumentujte požadavky na konfiguraci vysoké dostupnosti. Pokud potřebujete pomoc pochopit požadavky SQL Serveru, podívejte se do [příručky o vysoce dostupných řešeních SQL Serveru](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).
- Vyhodnocení kompatibility PaaS. [Průvodce migrací dat Azure](https://datamigration.microsoft.com) mapuje místní databáze na kompatibilní řešení Azure PaaS, jako je [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) nebo [Azure DB](https://docs.microsoft.com/azure/sql-database) pro [MySQL](https://docs.microsoft.com/azure/mysql), [PostgreSQL](https://docs.microsoft.com/azure/postgresql)nebo [MariaDB](https://docs.microsoft.com/azure/mariadb).
- Pokud je kompatibilita PaaS možná bez nutnosti nápravy, obraťte se na tým zodpovědný za [činnosti týkající se architektury](./architect.md). Migrace PaaS jsou výrazně časově úspornější a snižují celkové náklady na vlastnictví většiny cloudových řešení.
- Pokud je kompatibilita PaaS sice možná, ale vyžaduje nápravu, obraťte se na týmy zodpovědné za [architektonické aktivity](./architect.md) a [nápravné aktivity](../migrate/remediate.md). V mnoha scénářích, které se týkají databázových řešení, můžou výhody migrací PaaS převážit delší dobu potřebnou k nápravě.
- U každé migrované databáze zdokumentujte její velikost a četnost změn.
- Pokud je to možné, zdokumentujte aplikace a další prostředky, které každou databázi volají.

> [!NOTE]
> Synchronizace prostředku klade nároky na šířku pásma při replikačních procesech. Častou chybou je opomenutí šířky pásma, která je potřeba k udržení synchronizovaných prostředků mezi replikačním bodem a vydanou verzí. Během cyklů vydávání verzí jsou to právě databáze, které spotřebovávají šířku pásma. Zvlášť problematické jsou databáze s velkými nároky na úložiště nebo s vysokým tempem změn. Před uživatelským akceptačním testováním (UAT) a vydáním verze zvažte přístup spočívající v replikaci datové struktury s řízenými aktualizacemi. V podobných scénářích může být vhodnější použít alternativy Azure Site Recovery. Podrobnější informace najdete v [průvodci migrací dat do Azure](https://datamigration.microsoft.com).

## <a name="common-network-evaluation-activities"></a>Běžné aktivity při vyhodnocení sítě

- Spočítejte si celkové úložiště pro všechny virtuální počítače, které budete při iteracích vedoucích k vydání verzí replikovat.
- Spočítejte si míru posunu nebo změny úložiště pro všechny virtuální počítače, které budete při iteracích vedoucích k vydání verzí replikovat.
- Spočítejte si požadavky na šířku pásma potřebného pro každou iteraci tím, že sečtete celkové úložiště a posun.
- Spočítejte si nevyužitou šířku pásma, která je k dispozici v aktuální síti, abyste ověřili jednotnost iterací.
- Zdokumentujte šířku pásma potřebnou k dosažení předpokládané rychlosti migrace. Pokud k zajištění potřebné šířky pásma potřebujete provést nápravu, upozorněte na to tým, který zodpovídá za [nápravnou činnost](../migrate/remediate.md).

> [!NOTE]
> Celkové úložiště má přímý vliv na požadavky na šířku pásma při úvodní replikaci. Ale posun úložiště pokračuje od okamžiku replikace až do vydání verze. To znamená, že posun má kumulativní účinek na dostupnou šířku pásma.

## <a name="next-steps"></a>Další kroky

Po vyhodnocení úplnosti systému jsou výstupy připraveny k použití při vývoji nové [cloudové architektury](./architect.md).

> [!div class="nextstepaction"]
> [Architektura úloh před migrací](./architect.md)
