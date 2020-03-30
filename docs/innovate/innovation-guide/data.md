---
title: 'Inovace Azure: Demokratizace dat'
description: Seznamte se se službami Azure Data Catalog, Azure Data Share a dalšími nástroji, které vylepšují vyhledatelnost dat a jejich pochopení.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0c3a584277d708a0dcef8fcf019ed76589a3fd16
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356653"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Průvodce inovacemi Azure: Demokratizace dat

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratizace dat

::: zone-end

Jedním z prvních kroků při demokratizaci dat je zlepšení zjistitelnosti dat. Katalogizace a správa sdílení dat můžou podnikům pomoct získat největší možnou hodnotu z jejich stávajících informačních prostředků. Díky katalogu dat jsou zdroje dat snadno vyhledatelné a srozumitelné pro uživatele, kteří tato data spravují. Azure Data Catalog umožňuje správu v rámci podniku, zatímco služba Azure Data Share umožňuje správu a sdílení mimo podnik.

Služby Azure, které poskytují zpracování dat,jako jsou Azure Time Series Insights a Stream Analytics, představují další možnosti, které zákazníci a partneři úspěšně využívají k inovacím.

# <a name="catalog"></a>[Katalog](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Azure Data Catalog řeší problémy se zjišťováním pro příjemce dat a producentům dat pomáhá s údržbou informačních prostředků. Překlenuje propast mezi IT a zbytkem firmy a umožňuje, aby každý mohl přispět svými poznatky. Svá data můžete ukládat, kdekoli chcete, a připojovat se k nim pomocí libovolných nástrojů. Pomocí služby Azure Data Catalog můžete řídit, kdo může zjišťovat zaregistrované datové prostředky. S využitím otevřených rozhraní REST API ji můžete integrovat do stávajících nástrojů a procesů.

> [!div class="checklist"]
>
> - Zaregistrovat
> - Hledání a přidávání poznámek
> - Připojení a správa

::: zone target="docs"

**Přejít do [dokumentace ke službě Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akce

V rámci organizace můžete používat pouze jeden katalog dat Azure. Pokud už máte pro svou organizaci katalog dat vytvořený, nemůžete přidat další katalogy.

Vytvoření katalogu dat Azure pro vaši organizaci:

1. Přejděte do služby **Azure Data Catalog**.
2. Vyberte **Vytvořit**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2FCatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="share"></a>[Sdílení](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Dosažení rovnováhy mezi otevřeným sdílením dat a vykonáváním kontroly nad tím, která data se sdílejí a s kým, je klíčovou podmínkou pro úspěšné inovace. Při snaze o demokratizaci dat může organizace snadno přemoct enormní objem dat, rychlost, s jakou přibývají, a jejich životní cyklus. Azure Data Share zajišťuje, že poskytovatelé můžou řídit způsob zpracování svých dat určením podmínek použití pro své sdílené datové složky. Příjemce dat musí tyto podmínky přijmout, aby mohl data přijmout. Poskytovatelé dat můžou určit frekvenci, s jakou jejich příjemci dat obdrží aktualizace. Poskytovatel dat může přístup k novým aktualizacím kdykoli odvolat.

> [!div class="checklist"]
>
> - Vytvořte instanci služby Data Share.
> - Přidejte do ní datové sady.
> - Povolte pro ni plán synchronizace.
> - Přidejte do ní příjemce.

::: zone target="docs"
**Přejít do [dokumentace ke službě Azure Data Share](https://docs.microsoft.com/azure/data-share)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Vytvoření sdílené datové složky:

1. Přejděte do služby **Azure Data Share**.
2. Vyberte **Vytvořit sdílenou datovou složku**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2FAccounts]" submitText="Go to Azure Data Shares" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="insights"></a>[Přehledy](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Možnosti inovace v oblasti práce s daty, které nabízí služba Azure Time Series Insights, jsou neomezené. Umožňuje téměř v reálném čase zkoumat data z datových proudů a poskytuje vícevrstvé úložiště pro data časových řad v měřítku IoT. Poskytuje také modely pro zasazování nezpracované telemetrie do kontextu a vyvozování přehledů na základě prostředků. Na platformě Time Series Insights můžete využít bezproblémovou a kontinuální integraci s dalšími datovými řešeními, zajistit analýzy původní příčiny a detekci anomálií a využít možnosti sestavování vlastních aplikací.

> [!div class="checklist"]
>
> - Naplánujte si prostředí služby Time Series Insights.
> - Vizualizujte data v průzkumníku.
> - Seznamte se s principy uchovávání dat.
> - Vyvíjejte a sdílejte vlastní zobrazení.

::: zone target="docs"

**Přejít na [přehled služby Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akce

Vytvoření prostředí služby Azure Time Series Insights:

1. Přejděte do části **Prostředí služby Azure Time Series Insights**.
2. Vyberte **Vytvořit prostředí služby Time Series Insights**.
3. Nasměrujte toto prostředí na zdroj událostí – službu Azure IoT Hub nebo Event Hubs.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2FEnvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
