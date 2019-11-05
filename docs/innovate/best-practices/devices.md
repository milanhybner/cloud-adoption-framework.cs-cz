---
title: 'Inovace v cloudu: nástroje pro interakci se zařízeními v Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nástroje pro interakci se zařízeními v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c649ef695e74dce0ae2ec21e1e0d666abc2a65e9
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565831"
---
# <a name="tools-to-interact-with-devices-in-azure"></a>Nástroje pro interakci se zařízeními v Azure

Jak je popsáno v koncepčním článku o [komunikaci se zařízeními](../considerations/devices.md), zařízení používaná k interakci se zákazníkem závisí na množství okolního prostředí potřebném k zajištění potřeby zákazníka a k přijetí. Rychlost od triggeru, která vyzve uživatele k potřebě a možnosti vašeho řešení, aby splnila požadavky na opakování použití. Okolní prostředí vám pomůžou zrychlit dobu odezvy a vytvořit lepší prostředí pro vaše zákazníky, a to vložením vašeho řešení do bezprostředního okolí zákazníků.

![Přístup k rozhraní architektury pro přijetí do cloudu pro interakci se zařízeními](../../_images/innovate/ambient-experiences.png)

## <a name="alignment-to-the-methodology"></a>Soulad s metodikou

Tento typ digitálního vynálezu se dá doručit prostřednictvím kterékoli z následujících úrovní prostředí okolí. Tyto úrovně jsou zarovnány s metodologií, jak je znázorněno na předchozím obrázku. Obsah na levé straně této stránky obsahuje technické pokyny pro zrychlení digitálního vynálezení. Tyto články jsou seskupeny podle úrovně prostředí pro vyrovnání podle metodologie.

- **Mobilní prostředí:** Mobilní aplikace jsou obvykle součástí okolí zákazníka. V některých scénářích může mobilní zařízení poskytovat dostatek interaktivity, aby bylo řešení v okolí.
- **Mixed reality:** V některých případech je nutné změnit přirozené okolí zákazníka prostřednictvím hybridní reality. Zapojení zákazníka v rámci této smíšené reality může mít formu prostředí okolí.
- **Integrovaná realita:** S ohledem na blížící se k true Ambience se integrovaná řešení realit zaměřují na použití fyzického zařízení zákazníka a integruje řešení do přirozeného chování.
- **Upravená realita:** Pokud některá z výše uvedených řešení používají prediktivní analýzu k zajištění interakce se zákazníkem v přirozeném okolí daného zákazníka, toto řešení vytváří nejvyšší formu prostředí okolí.

## <a name="toolchain"></a>Sada nástrojů

V Azure se běžně používají následující nástroje k urychlení digitálního vynálezu napříč všemi předchozími úrovněmi okolních řešení. Tyto nástroje jsou seskupené podle množství zkušeností potřebných ke snížení složitosti v serovnávání nástrojů s těmito prostředími.

- Mobilní prostředí: Azure App Service, PowerApps, Microsoft Flow, Intune
- Mixed reality: Unity, prostorové kotvy Azure, HoloLens
- Integrovaná realita: Azure IoT Hub, Azure Sphere, Azure Kinect DK
- Upravená realita: Cloud IoT do zařízení, digitální vlákna Azure a HoloLens

## <a name="get-started"></a>Začínáme

Obsah na levé straně této stránky popisuje mnoho článků. Tyto články vám pomůžou začít s každým z nástrojů v tomto sada nástrojů.

> [!NOTE]
> Některé odkazy můžou opustit rozhraní pro přijetí cloudu, které vám pomůžou přesáhnout rámec tohoto rámce.
