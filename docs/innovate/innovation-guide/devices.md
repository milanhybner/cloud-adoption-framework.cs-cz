---
title: 'Průvodce inovacemi Azure: Interakce prostřednictvím zařízení'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Průvodce inovacemi Azure – Interakce prostřednictvím zařízení
author: umarmohamedusman
ms.author: umarm
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: f38c207c89cbe4d37958292c552165f39e2bd383
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769289"
---
::: zone target="docs"

# <a name="azure-innovation-guide-interact-through-devices"></a>Průvodce inovacemi Azure: Interakce prostřednictvím zařízení

::: zone-end

::: zone target="chromeless"

# <a name="interact-through-devices"></a>Interakce prostřednictvím zařízení

::: zone-end

Inovujte prostřednictvím přerušovaně připojených citlivých hraničních zařízení. Orchestrujte miliony takových zařízení, získávejte a zpracovávejte neomezené množství dat a využijte rostoucího počtu multisenzorických prostředí s více zařízeními. Pro zařízení na hranicích vaší sítě poskytuje Azure rámec pro budování působivých a efektivních obchodních řešení. Distribuované výpočetní prostředky založené na Azure kombinované s technologiemi umělé inteligence vám umožňují vytvářet všechny typy inteligentních aplikací a systémů, jaké si dokážete představit.

Zákazníci Azure využívají průběžně se rozšiřující sadu propojených zařízení a systémů, které shromažďují a analyzují data&mdash;v blízkosti vašich uživatelů, dat či obojího. Uživatelé mají k dispozici přehledy a funkce v reálném čase poskytované aplikacemi, které fungují velmi rychle a s ohledem na kontext. Přesunutím části úloh do hraničních zařízení mohou tato zařízení strávit méně času odesíláním zpráv do cloudu a rychleji reagovat na prostorové události.

> [!div class="checklist"]
>
> - Průmyslové prostředky
> - HoloLens 2
> - Azure Sphere
> - Kinect DK
> - Drony
> - Azure SQL Database Edge
> - IoT Plug and Play

<!-- markdownlint-disable MD025 -->

## <a name="global-scale-iot-servicetabiothub"></a>[Služby IoT v globálním měřítku](#tab/IoTHub)

<!-- markdownlint-enable MD025 -->

Architektonická řešení, která provádějí obousměrnou komunikaci se zařízeními IoT v miliardovém měřítku. Získejte přehled o stavu svých zařízení pomocí telemetrických dat ve směru zařízení-cloud a definujte trasy zpráv do jiných služeb Azure jednoduchou konfigurací. Pomocí zpráv z cloudu na zařízení můžete na připojená zařízení spolehlivě posílat příkazy a oznámení. Potvrzení o příjmu vám umožní sledovat doručování zpráv. Podle potřeby můžete automaticky přeposílat zprávy zařízení s ohledem na přerušované připojení.

- **Komunikační kanál s vylepšeným zabezpečením** umožňující odesílat data na zařízení IoT a přijímat je z nich.
- **Integrovaná správa zařízení** a jejich zřizování umožňující připojovat a spravovat zařízení IoT ve velkém měřítku.
- **Úplná integrace se službou Event Grid** a bezserverové výpočetní prostředí zjednodušující vývoj aplikací IoT.
- **Kompatibilita se službou Azure IoT Edge** umožňující vytvářet hybridní aplikace IoT.

::: zone target="docs"

**Přejít[ na IoT Hub](https://docs.microsoft.com/azure/iot-dps)**

**Přejít[ na službu Device Provisioning](https://docs.microsoft.com/azure/iot-dps)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Vytvoření IoT Hubu:

1. Přejděte na **IoT Hub**.
2. Klikněte na možnost pro **vytvoření IoT hubu**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FIotHubs]" submitText="Go to IoT Hub" :::

Služba IoT Hub Device Provisioning je pomocná služba pro IoT Hub, která umožňuje plně automatizované zřizování podle potřeby.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Vytvoření služby IoT Hub Device Provisioning:

1. Přejděte na **službu IoT Hub Device Provisioning**.
2. Klikněte na možnost pro **vytvoření služby Device Provisioning**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FProvisioningServices]" submitText="Go to Device Provisioning Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="azure-digital-twinstabdigitaltwins"></a>[Azure Digital Twins](#tab/DigitalTwins)

Vytvářejte opakovatelně použitelná a vysoce škálovatelná prostředí přizpůsobená prostoru, která propojují streamovaná data v digitálním a fyzickém světě. Vylepšete zapojení zákazníků pomocí komplexních modelů fyzických prostředí. Generujte grafy prostorové inteligence pro modelování vztahů a interakcí mezi lidmi, prostory a zařízeními. Využijte možnost dotazovat se na data z fyzického prostoru, a ne z mnoha různorodých senzorů.

**Objektové modely služby Azure Digital Twins:** Ontologie, která popisuje oblasti, místa, podlaží, kanceláře, zóny, konferenční místnosti a odpočinkové místnosti inteligentní budovy, nebo různé napájecí stanice, rozvodny, energetické zdroje a zákazníky energetické sítě. Lze modelovat pomocí objektových modelů služby Digital Twins a ontologií.

**Graf prostorové inteligence:** Hierarchický graf prostorů, zařízení a osob definovaných v objektovém modelu služby Digital Twins, který podporuje dědičnost, filtrování, procházení, škálovatelnost a rozšiřitelnost. Prostorový graf můžete spravovat a pracovat s ním s využitím kolekce rozhraní REST API hostovaných v Azure.

::: zone target="docs"

**Přejít[ do služby Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Vytvoření služby Azure Digital Twins:

1. V levém podokně vyberte **Vytvořit prostředek**.
2. Vyhledejte prostředek digital twins a vyberte **Digital Twins**.
3. Výběrem možnosti **Vytvořit** zahájíte proces nasazení.
4. Klikněte na tlačítko níže a zkontrolujte existující službu Digital Twins.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.IoTSpaces%2FGraph]" submitText="Go to Digital Twins" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="location-intelligencetabazuremaps"></a>[Inteligentní informace o poloze](#tab/AzureMaps)

Kromě tradičních funkcí určování polohy, jako jsou zařízení v okolí, provoz a směrování, služba Azure Maps umožňuje podnikům vytvářet řešení pomocí informací o poloze v reálném čase, které využívají špičkové technologie pro mobilitu společností **TomTom**  a **Moovit**. Snadno integrujte pokročilé funkce mobility a určování polohy do svých aplikací s využitím geoprostorových služeb.

**Data Service (verze Preview):** Nahrávejte a ukládejte geoprostorová data a používejte je v rámci prostorových operací nebo sestavování obrázků, abyste v rámci vašich aplikací snížili latenci, zvýšili produktivitu a umožnili použití nových scénářů.

**Prostorové operace:** Vylepšete vaše inteligentní informace o poloze s využitím knihovny běžných geoprostorových matematických výpočtů, včetně geofencingu, nejbližšího bodu, vzdušné vzdálenosti a rezerv.

**Geografická poloha:** Využijte možnost vyhledat zemi pro IP adresu. Podle umístění uživatele můžete přizpůsobit obsah a služby a můžete získat přehled o zeměpisném rozmístění zákazníků.

::: zone target="docs"

**Přejít[ na Azure Maps](https://docs.microsoft.com/azure/azure-maps)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Použití inteligentních informací o poloze:

1. Přejděte na **Účty Azure Maps**.
2. Klikněte na **Vytvořit účty Azure Maps**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Maps%2Faccounts]" submitText="Go to Azure Maps Account" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="spatial-experiencestabspatial"></a>[Prostorová prostředí](#tab/spatial)

Azure Spatial Anchors umožňuje vývojářům pracovat s platformami smíšené reality, vnímat prostory, navrhovat přesné body zájmu a vyvolat tyto body zájmu z podporovaných zařízení.

**Doplnění kontextu do reálného světa:** Vhodně umístěte digitální obsah a propojte ho k fyzickým bodům zájmu. Poskytnete tak uživatelům lepší přehled o jejich datech, ať už ho budou potřebovat kdykoli a kdekoli.

**Sdílení hologramů napříč zařízeními:** Poskytněte vašemu týmu a zákazníkům 3D obsah na zařízení podle jejich volby a zrychlete tak jejich rozhodování a získávání výsledků. Služba Spatial Anchors usnadňuje lidem ve stejném prostoru účast na víceuživatelských aplikacích smíšené reality.

**Poutavé prostředí:** Propojte prostorové kotvy tak, že mezi nimi vytvoříte vztahy, a vytvořte uživatelské prostředí, které může zahrnovat dva nebo více bodů zájmu, s nimiž musí uživatel interagovat, aby mohl dokončit úkol. Vaše aplikace může dát uživateli možnost umístit virtuální artefakt do reálného světa. V průmyslovém prostředí může uživatel přijímat kontextové informace o stroji tak, že na něj nasměruje kameru podporovaného zařízení.

Azure Spatial Anchors se skládá ze spravované služby a klientských sad SDK pro podporované platformy zařízení.

::: zone target="docs"

**Přejít[ na Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Použití prostorových prostředí:

1. Přejděte na **Účty Spatial Anchors**.
2. Klikněte na **Vytvořit účty Spatial Anchors**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.MixedReality%2FspatialAnchorsAccounts]" submitText="Go to Spatial Anchors Accounts" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-remote-renderingtabremoterender"></a>[Azure Remote Rendering](#tab/RemoteRender)

Vykreslujte vysoce kvalitní interaktivní 3D obsah v cloudu a streamujte ho do zařízení v reálném čase. Úlohy vykreslování se často využívají pro zvláštní efekty (VFX) v mediálním a zábavním odvětví. Vykreslování se používá i v mnoha dalších odvětvích, jako je reklama, maloobchodní prodej, ropný a plynárenský průmysl nebo výroba.

Proces vykreslování je výpočetně náročný. Často je nutné vytvořit mnoho snímků nebo obrázků a vykreslování každého z nich může trvat mnoho hodin. Vykreslování proto představuje ideální úlohu pro dávkové zpracování, které může používat Azure a Azure Batch k paralelnímu spuštění mnoha vykreslování.

::: zone target="docs"

**Přejít[ na Azure Remote Rendering](https://azure.microsoft.com/services/remote-rendering)**

**Přejít[ na vykreslování s využitím Azure](https://docs.microsoft.com/azure/batch/batch-rendering-service)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akce

Použití služby Azure Remote Rendering:

1. Přejděte na **Účty služby Batch**.
2. Klikněte na **Vytvořit účty Batch**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Batch%2FbatchAccounts]" submitText="Go to Azure Batch" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end