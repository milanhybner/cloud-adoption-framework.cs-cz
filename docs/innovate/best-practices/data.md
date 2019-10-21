---
title: 'Inovace v cloudu: nástroje pro demokratizujteí dat v Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nástroje pro demokratizujteí dat v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 1a4c6574ccef3f8373fe149e8756e49555cd0171
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557931"
---
# <a name="tools-to-democratize-data-in-azure"></a>Nástroje pro demokratizujteí dat v Azure

Jak je popsáno v teoretickém článku o [democratizing datech](../considerations/data.md), mnohé inovace se dají doručovat s minimálními technickými investicemi. K dispozici jsou dlouhé příklady hlavních inovací, které vyžadují trochu více než nezpracovaná data. Democratizing data o investicích se co nejvíce investují, aby vaši zákazníci mohli využívat data na svém stávajícím vědomí na velkých písmenech. Počínaje daty je rychlý způsob, jak otestovat hypotézu před rozbalením do širších, dražších digitálních vynálezů. Jak je upřesněna hypotéza a vynálezy začnou být přijaty ve velkém měřítku, níže uvedené procesy budou mít při přípravě na provozní podporu inovací k dispozici.

![Přístup k rozhraní architektury pro přijetí do cloudu pro democratizing data](../../_images/innovate/democratize-data.png)

## <a name="alignment-to-the-methodology"></a>Zarovnání na metodologii

Tento typ digitálního vynálezu se dá zrychlit prostřednictvím každé fáze následujícího procesu, která je také navýšená. Technické pokyny pro zrychlení digitálního vynálezu jsou uvedené v obsahu na levé straně. Tyto články byly seskupeny do stejných fází, aby bylo možné zarovnat doprovodné materiály k celkové metodologii:

- **Sdílet data:** První krok dat democratizing je sdílet otevřený.
- **Data upravující:** Před sdílením zajistěte, aby byla citlivá data zabezpečená, sledovaná a řízená.
- **Centralizovaná data:** V některých případech je nutné poskytnout centralizaci platformy pro sdílení dat a zásady správného řízení.
- **Shromažďovat data:** Migrace, integrace, ingestování a virtualizace můžou každá shromažďovat existující data, která se mají centrálně spravovat, řídit a sdílet.

Doporučuje se, aby týmy pro přijímání v cloudu přešly jenom do zásobníku, jak je potřeba k tomu, aby se při každé iteraci zaměřily na požadavky zákazníků nad architekturou. Prodlevy technických špiček na základě potřeb zákazníků urychlí ověřování vaší hypotézy. V takovém případě jsou všechny doprovodné materiály namapovány na čtyři procesy výše od nejvyššího dopadu zákazníků na nejvyšší technický dopad. V každé z nich se setkáte s pokyny k nejrůznějším potenciálním způsobům, které může Azure urychlit při [sestavování pomocí zákaznických soucit](../considerations/build.md).

## <a name="toolchain"></a>Sada nástrojů

V Azure se běžně využívají tyto nástroje k urychlení digitálního vynálezování v každé z výše uvedených fází: Power BI, Azure Data Catalog, Azure SQL Data Warehouse, Cosmos DB, databázích Azure pro PostgreSQL, MySQL, MariaDB, PostgreSQL, škálovatelné, Azure Data Lake, Azure Data Migration Service, Azure SQL Database (s nebo bez spravovaných instancí), Azure Data Factory, Azure Stream Analytics, služba SSIS (SQL Server Integration Services), Azure Stack, Azure SQL Stretch Database, StorSimple, Azure Files, Synchronizace souborů a PolyBase.

V rámci přístupů k vynálezu ve velkém měřítku budou aspekty každého řešení vyžadovat vylepšení a technickou splatnost. V takovém případě je pravděpodobnější, že budete potřebovat více těchto služeb. Prozatím můžete pomocí obsahu vlevo najít pokyny k nástrojům Azure relevantním pro proces potřebný k otestování hypotézy.

## <a name="get-started"></a>Začít

Obsah na levé straně obsahuje mnoho článků, které vám pomohou začít s každým z těchto nástrojů v tomto sada nástrojů.

> [!NOTE]
> Některé odkazy mohou opustit rozhraní pro přijetí cloudu, aby lépe překročily rozsah této architektury.
