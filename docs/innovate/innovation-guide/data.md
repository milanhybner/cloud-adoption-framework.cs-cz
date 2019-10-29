---
title: 'Průvodce inovacemi Azure: Demokratizace dat'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se demokratizovat data pomocí Azure.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 65c1ecd1d722286fb495af3069862131629c35d1
ms.sourcegitcommit: 0d14d89b9004a65a322724342cb5086ad2c77467
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/22/2019
ms.locfileid: "72777093"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Průvodce inovacemi Azure: Demokratizace dat

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratizace dat

::: zone-end

Jedním z prvních kroků při demokratizaci dat je zlepšení zjistitelnosti dat. Katalogizace a správa sdílení dat můžou podnikům pomoct získat největší možnou hodnotu z jejich stávajících informačních prostředků. Díky katalogu dat jsou zdroje dat snadno objevitelné a srozumitelné pro uživatele, kteří tato data spravují. Služba Azure Data Catalog umožňuje správu v rámci podniku, zatímco služba Azure Data Share umožňuje správu a sdílení mimo podnik.

Služby Azure, které poskytují zpracování dat (jako jsou Azure Time Series Insights a Stream Analytics), představují další možnosti, které zákazníci a partneři úspěšně využívají k inovacím.

# <a name="catalogtabcatalog"></a>[Katalog](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Služba Azure Data Catalog řeší problémy se zjišťováním pro příjemce dat a producentům dat pomáhá s údržbou informačních prostředků. Překlenuje mezeru mezi IT a zbytkem firmy a umožňuje, aby každý mohl přispět svými poznatky. Data můžete uložit na libovolném místě a propojit je pomocí nástrojů podle své volby. Můžete také řídit, kdo může zjišťovat zaregistrované datové prostředky. Integraci do existujících nástrojů a procesů můžete zajistit pomocí otevřených rozhraní REST API.

> [!div class="checklist"]
>
> - Registrace
> - Hledání a přidávání poznámek
> - Připojení a správa

::: zone target="docs"

**Přejděte do služby [Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog).**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akce

V rámci organizace se podporuje jenom jedna instance služby Azure Data Catalog. Pokud už máte pro svou organizaci katalog vytvořený, nemůžete přidat další katalogy.

Pokud chcete vytvořit instanci služby Azure Data Catalog pro svou organizaci:

1. Přejděte do služby **Azure Data Catalog**.
2. Klikněte na tlačítko **Vytvořit**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Sdílení](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Dosažení rovnováhy mezi otevřeným sdílením dat a zachováním si kontroly nad tím, která data se sdílejí a s kým, je klíčovou podmínkou pro úspěšné inovace. Při snaze o demokratizaci dat může organizace snadno přemoci enormní objem dat, rychlost, s jakou přibývají, a jejich životní cyklus. Použití služby Azure Data Share zajišťuje, že poskytovatel si zachová kontrolu nad způsoby zpracování svých dat a může určit podmínky použití pro sdílení svých dat. Příjemce dat musí tyto podmínky přijmout, aby mohl data přijmout. Poskytovatelé dat můžou určit frekvenci, s jakou jejich příjemci dat obdrží aktualizace. Poskytovatel dat může přístup k novým aktualizacím kdykoli odvolat.

> [!div class="checklist"]
>
> - Vytvořte instanci služby Data Share.
> - Přidejte do ní datové sady.
> - Povolte pro ni plán synchronizace.
> - Přidejte do ní příjemce.

::: zone target="docs"
**Přejděte do služby [Azure Data Share](https://docs.microsoft.com/azure/data-share).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Vytvoření instance služby Azure Data Share:

1. Přejděte do služby **Azure Data Share**.
2. Klikněte na **Vytvořit instanci služby Data Share**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Share" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

Pomocí platformy [Azure Open Datasets](https://docs.microsoft.com/azure/open-datasets/overview-what-are-open-datasets) můžete vylepšit své analýzy a zahrnout do svých modelů například údaje o [svátcích](https://azure.microsoft.com/services/open-datasets/catalog/public-holidays) či [počasí](https://azure.microsoft.com/services/open-datasets/catalog/noaa-global-forecast-system) nebo [satelitní snímky](https://azure.microsoft.com/services/open-datasets/catalog/hls).

Dalšími kroky jsou [demokratizace firemních procesů](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/democratize-business-processes) a [podpora vývojářů služeb pro občany](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/empower-citizen-developers).

# <a name="insightstabinsights"></a>[Přehledy](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Téměř v reálném čase můžete zkoumat data z datových proudů nebo časových řad a modelů z vícevrstvých úložišť v měřítku IoT. Nezpracovanou telemetrii tak můžete dát do kontextu a vyvodit přehledy na základě prostředků. Možnosti inovace v oblasti práce s daty jsou prakticky nekonečné. Můžete využít bezproblémovou a kontinuální integraci s jinými datovými řešeními, zajistit analýzy původní příčiny a detekci anomálií a využít možnosti sestavení vlastních aplikací na platformě Time Series Insights.

> [!div class="checklist"]
>
> - Naplánujte si prostředí služby Time Series Insights.
> - Vizualizujte data v průzkumníku.
> - Seznamte se s principy uchovávání dat.
> - Vyvíjejte a sdílejte vlastní zobrazení.

::: zone target="docs"

**Přejděte do služby [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Vytvoření prostředí služby Azure Time Series Insights:

1. Přejděte do služby **Azure Time Series Insights**.
2. Klikněte na **Vytvořit prostředí Time Series Insights**.
3. Nasměrujte toto prostředí na zdroj událostí – službu IoT Hub nebo centrum událostí.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
