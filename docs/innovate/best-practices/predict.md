---
title: 'Inovace v cloudu: nástroje k předvídání a ovlivnění v Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nástroje pro předpověď a vliv v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 9bb5f837ce3a7bb07fb108f48229f488df1b9dc7
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565789"
---
# <a name="tools-to-predict-and-influence-data-in-azure"></a>Nástroje k předvídání a ovlivnění dat v Azure

Jak je popsáno v koncepčním článku o [prediktivních a ovlivněných](../considerations/predict.md)počítačích, jsou počítače a AI mnohem lepší, než jsme viděli vzory. Pomocí cloudových analytických nástrojů můžete snadno detekovat vzory a aplikovat je na potřeby vašich zákazníků. Použití těchto nástrojů vede k předpovědií nejlepších výsledků. Když jsou tyto předpovědi integrovány zpátky do zákaznického prostředí, můžou ovlivnit vzorce chování vašich zákazníků prostřednictvím interakcí.

![Přístup k předpovídání a ovlivnění rozhraní architektury cloudového přijetí](../../_images/innovate/predict-and-influence.png)

## <a name="alignment-to-the-methodology"></a>Soulad s metodikou

Tento typ digitálního vynálezu můžete urychlit prostřednictvím každé fáze následujícího procesu. Fáze se zarovnají s metodologií, která je znázorněna na předchozím obrázku. Technické pokyny pro zrychlení digitálního vynálezu jsou uvedeny v obsahu na levé straně této stránky. Tyto články jsou seskupeny podle fáze, aby je bylo možné zarovnat podle metodologie.

V předchozím obrázku se data a přehledy zarovnají s osvědčenými postupy popsanými v článku [democratizing data](./data.md) . V případě, že odborníci na danou problematiku zjistí přehledy, které by mohly být možné opakovat, můžou tyto poznatky vymezit pomocí následujících tří kroků:

- **Vzory:** Vyhledejte a definujte vzory pro vytváření prediktivních modelů.
- **Předpovědi:** Použijte vzory pro zákaznická data pro předpověď výsledků na základě modelu a základního vzoru.
- **Interakce:** Využijte předpovědi z aplikace nebo zdroje dat, abyste mohli nařídit interakci se zákazníkem.

## <a name="toolchain"></a>Sada nástrojů

V Azure se běžně používají následující nástroje k urychlení digitálního vynálezování v každé z předchozích fází:

- Azure Machine Learning
- Azure HDInsight
- Škálování pro Hadoop R
- Azure SQL Data Warehouse

Způsob, jakým jednotlivé nástroje pomáhají s každou fází prediktivního a ovlivnění, se projeví v obsahu na levé straně této stránky.

## <a name="get-started"></a>Začínáme

Obsah na levé straně této stránky popisuje mnoho článků. Tyto články vám pomůžou začít s každým z nástrojů v tomto sada nástrojů.

> [!NOTE]
> Některé odkazy můžou opustit rozhraní pro přijetí cloudu, které vám pomůžou přesáhnout rámec tohoto rámce.
