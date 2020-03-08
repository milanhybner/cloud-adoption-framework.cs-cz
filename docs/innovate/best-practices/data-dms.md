---
title: Inovační nástroje pro migraci dat
description: Přečtěte si o Azure Database Migration Service a dalších nástrojích, které migrují a modernizovatí data pro přípravu na vynálezy a inovace cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 1f6d7545814f51f79a45b619f73dab857ac582d3
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/07/2020
ms.locfileid: "78891985"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Shromažďování dat migrací a modernizací stávajících zdrojů dat

Společnosti mají často různé druhy stávajících dat, která můžou [Demokratizujte](../considerations/data.md). Když zákazník hypotéza vyžaduje použití existujících dat k vytváření moderních řešení, může být prvním krokem migrace a modernizace dat pro přípravu na vynálezy a inovace. V souladu se stávajícími úsilími migrace v rámci plánu přijetí do cloudu můžete snadněji provádět migraci a modernizaci v rámci [metodologie migrace](../../migrate/index.md).

## <a name="use-of-this-article"></a>Použití tohoto článku

Tento článek popisuje řadu přístupů, které jsou v souladu s procesem migrace. Tyto přístupy můžete nejlépe zarovnat na standardní sada nástrojů migrace.

Během procesu posuzování v rámci metodologie migrace vyhodnocuje tým přijetí do cloudu aktuální stav a požadovaný budoucí stav migrovaného assetu. Pokud je tento proces součástí snahy inovace, mohou oba týmy při přijímání v cloudu využít tento článek k tomu, aby tyto hodnocení pomohli.

## <a name="primary-toolset"></a>Primární sada nástrojů

Když migrujete a modernizovatte místní data, je [Azure Database Migration Service](https://docs.microsoft.com/azure/dms)nejběžnějším nástrojem Azure. Tato služba je součástí širší [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) sada nástrojů. U stávajících SQL Server zdrojů dat vám [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview) může posuzovat a migrovat malý počet datových struktur.

Aby bylo možné podporovat migrace Oracle a NoSQL, můžete také použít [Database Migration Service](https://docs.microsoft.com/azure/dms) pro určité typy databází typu zdroj-cíl. Mezi příklady patří Oracle to PostgreSQL a MongoDB to Cosmos DB. Týmy pro přijímání často využívají partnerské nástroje nebo vlastní skripty k migraci na Azure Cosmos DB, Azure HDInsight nebo možnosti virtuálních počítačů na základě infrastruktury jako služby (IaaS).

## <a name="considerations-and-guidance"></a>Pokyny a doprovodné materiály

Když použijete Azure Database Migration Service pro migraci a modernizaci dat, je důležité pochopit:

- Aktuální platforma pro hostování zdroje dat.
- Aktuální verze
- Budoucí platforma a verze, které nejlépe podporují zákaznickou hypotézu nebo cíl.

V následující tabulce jsou uvedeny zdrojové a cílové páry pro kontrolu s týmem migrace. Každý pár obsahuje možnost výběru nástroje a odkaz na související vodítko.

### <a name="migration-type"></a>Typ migrace

V případě offline migrace dojde při spuštění migrace k výpadku aplikace. V případě online migrace je doba výpadku omezená na dobu přímé migrace na konci migrace.

Doporučujeme, abyste se rozhodli, že máte přijatelné provozní výpadky a otestujete offline migraci. Provedete to tak, abyste zkontrolovali, jestli doba obnovení vyhovuje přijatelnému výpadku. Pokud není čas obnovení přijatelný, proveďte online migraci.

|Zdroj  |Cíl  |Nástroj  |Typ migrace  |Doprovodné materiály  |
|---------|---------|---------|---------|---------|
|Server SQL|Azure SQL Database|Database Migration Service|Offline|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|Server SQL|Azure SQL Database|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|Server SQL|Spravovaná instance Azure SQL Database|Database Migration Service|Offline|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|Server SQL|Spravovaná instance Azure SQL Database|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server VP|Azure SQL Database nebo Azure SQL Database spravované instance|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure Database for MySQL|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure Database for PostgreSQL|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|MongoDB|Rozhraní API pro Azure Cosmos DB Mongo|Database Migration Service|Offline|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Rozhraní API pro Azure Cosmos DB Mongo|Database Migration Service|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
