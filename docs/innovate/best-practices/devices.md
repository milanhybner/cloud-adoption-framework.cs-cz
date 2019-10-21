---
title: 'Inovace v cloudu: nástroje pro interakci se zařízeními v Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nástroje pro interakci se zařízeními v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a10a0ad39db6e7683603208938a87664c7928414
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557268"
---
# <a name="tools-to-interact-with-devices-in-azure"></a>Nástroje pro interakci se zařízeními v Azure

Jak je popsáno v teoretickém článku o [interakci se zařízeními](../considerations/devices.md), zařízení používaná k interakci se zákazníkem jsou závislá na úrovni prostředí okolí potřebné k zajištění potřeby zákazníka a k přijetí. Rychlost od triggeru, která vyzývá k potřebě a schopnost vašeho řešení splnit potřeby zákazníka, je rozhodující faktor v použití opakování. Okolní prostředí vám pomůžou zrychlit dobu odezvy a vytvořit lepší prostředí pro vaše zákazníky, a to tak, že vaše řešení vloží do bezprostředního okolí zákazníků.

![Přístup k rozhraní architektury pro přijetí do cloudu pro interakci se zařízeními](../../_images/innovate/ambient-experiences.png)

## <a name="alignment-to-the-methodology"></a>Zarovnání na metodologii

Tento typ digitálního vynálezu se dá doručit prostřednictvím kterékoli z následujících úrovní okolního prostředí, a to v souladu s metodologií, jak je znázorněno výše. Technické pokyny pro zrychlení digitálního vynálezu jsou uvedené v obsahu na levé straně. Tyto články byly seskupeny do stejných úrovní okolních prostředí, aby je bylo možné zarovnat podle metodologie:

- **Mobilní prostředí:** Mobilní aplikace jsou běžně součástí okolí zákazníků. V některých scénářích může mobilní zařízení poskytnout dostatečnou úroveň interaktivity, aby bylo řešení v okolí.
- **Mixed reality:** V některých případech je nutné změnit přirozené okolí zákazníka prostřednictvím hybridní reality. Díky tomu, že zákazníci v rámci této smíšené reality můžou mít formu okolí.
- **Integrovaná realita:** S ohledem na blížící se Ambience se integrovaná řešení realit zaměřují na použití zařízení, které existuje ve fyzické realitě zákazníka a integruje řešení do přirozeného chování.
- **Upravená realita:** Pokud některé z výše uvedených řešení používají prediktivní analýzu k zajištění interakce se zákazníkem v rámci svého přirozeného okolí, řešení vytvoří nejvyšší formu prostředí.

## <a name="toolchain"></a>Sada nástrojů

V Azure se běžně využívají následující nástroje k urychlení digitálního vynálezování v každé z výše uvedených úrovní okolí řešení. Tyto nástroje byly seskupeny na základě úrovně zkušeností požadovaných k omezení složitosti v sestupných nástrojích s požadovanými prostředími.

- Mobilní prostředí: App Service, PowerApps, Microsoft Flow, Intune
- Mixed reality: Unity, prostorové kotvy Azure, HoloLens
- Integrace realit: Azure IoT Hub, Azure Sphere, Kinect DK
- Upravená realita: Cloud IoT do zařízení, digitální vlákna a HoloLens

## <a name="get-started"></a>Začít

Obsah na levé straně obsahuje mnoho článků, které vám pomohou začít s každým z těchto nástrojů v tomto sada nástrojů.

> [!NOTE]
> Některé odkazy mohou opustit rozhraní pro přijetí cloudu, aby lépe překročily rozsah této architektury.
