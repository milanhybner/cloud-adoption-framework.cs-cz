---
title: 'Inovace cloudu: služba migrace dat'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cloudové inovace – služba migrace dat
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 7b6d9d2bb08bd4e3e34fe1cc67f4c6a006a75bb5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557398"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Shromažďování dat migrací a modernizací stávajících zdrojů dat

Společnosti mají často celou řadu existujících dat, která se dají [democratized](../considerations/data.md). Pokud zákazník hypotéza vyžaduje použití existujících dat k vytváření moderních řešení, může být prvním krokem migrace a modernizace dat pro přípravu vynálezů a inovací. V souladu se stávajícími úsilími migrace v rámci plánu přijetí do cloudu může být migrace a modernizace snazší provést v rámci [metodologie migrace](../../migrate/index.md).

## <a name="use-of-this-article"></a>Použití tohoto článku

Tento článek popisuje řadu přístupů, které jsou v souladu s procesem migrace, ale můžou být nejlépe zarovnané na standardní migraci sada nástrojů. Během procesu posuzování v rámci metodologie migrace by tým pro přijetí v cloudu vyhodnotil aktuální stav a přeje si budoucí stav assetu migrovat. Pokud je tento proces součástí snahy inovace, mohou oba týmy při přijímání v cloudu použít tento článek k rozhodování.

## <a name="primary-toolset"></a>Primární sada nástrojů

Při migraci a modernizaci dat, která se nacházejí v Prem, je nejběžnější volbou Azure Tool [služba migrace dat (DMS)](https://docs.microsoft.com/azure/dms) , která je součástí širšího [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) sada nástrojů. U stávajících SQL Server zdrojů dat mohl [Data Migration Assistant (DMA)](/sql/dma/dma-overview) poskytnout pomoc při posuzování a migraci menšího počtu datových struktur.

Aby bylo možné podporovat migrace Oracle a NoSQL, je možné [službu migrace dat (DMS)](https://docs.microsoft.com/azure/dms) použít také pro určité typy zdrojů pro cílové databáze, jako je například Oracle k PostgreSQL nebo MongoDB Cosmos DB. Pro účely migrace na Cosmos DB, HDInsight nebo možnosti virtuálního počítače založeného na IaaS je běžné, že týmy pro přijímání využívají nástroje třetích stran nebo vlastní skripty migrace.

## <a name="considerations-and-guidance"></a>Pokyny a doprovodné materiály

Pokud využíváte DMS pro migraci a modernizaci dat, je důležité pochopit aktuální platformu pro hostování dat (zdroje), verze a budoucí platformy a verze, které by nejlépe podporovaly zákaznickou hypotézu (cíl). Následující seznam uvádí zdrojové a cílové páry pro kontrolu s týmem migrace. Každá z nich zahrnuje výběr nástroje a odkaz na vodítko na základě těchto doporučení.

**Typ migrace:** Při offline migraci se spustí výpadek aplikace při spuštění migrace. V případě online migrace je doba výpadku omezená na dobu přímé migrace na konci migrace. Doporučujeme, abyste pochopili, co je to přijatelné provozní výpadky a otestovali offline migraci, abyste zjistili, jestli tento čas obnovení splňuje. Pokud ne, proveďte online migraci.

|Zdroj  |Výběr cílového umístění  |Nástroj  |Typ migrace  |Pokyny  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|DMS|Stav|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Stav|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server VP|Azure SQL Database (nebo spravovaná instance)|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure Database for MySQL|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure Database for PostgreSQL|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|MondoDB|Rozhraní API pro Azure Cosmos DB Mongo|DMS|Stav|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Rozhraní API pro Azure Cosmos DB Mongo|DMS|Online|[Kurz](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|Rozsah možností PaaS & IaaS|Třetí strana nebo Azure Migrate|Některé|[Rozhodovací strom](../considerations/data-oracle-migration.md)|
|Různé NoSQL databáze|Možnosti Cosmo DB nebo IaaS|Postupy migrace a Azure Migrate|Některé|[Rozhodovací strom](../considerations/data-no-sql-migration.md)|
