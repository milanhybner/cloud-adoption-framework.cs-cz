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
ms.openlocfilehash: 28b13b472729a8500719afbe34013daaddc9a3fc
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683352"
---
# <a name="tools-to-predict-and-influence-data-in-azure"></a>Nástroje k předvídání a ovlivnění dat v Azure

Jak je popsáno v teoretickém článku o [prediktivních a ovlivněných](../considerations/predict.md)počítačích, počítačů a umělých inteligentních příkazech je lepší, když vidíte vzory, které jsou v podstatě. Pomocí cloudových analytických nástrojů můžete vzory snadno zjistit a použít u potřeb vašich zákazníků, což vede k předpovědi nejlepšího výsledku. Pokud jsou tyto předpovědi integrovány zpátky do prostředí pro zákazníky, předpověď může ovlivnit vzorce chování vašich zákazníků prostřednictvím interakcí.

![Přístup k předpovídání a ovlivnění rozhraní architektury cloudového přijetí](../../_images/innovate/predict-and-influence.png)

## <a name="alignment-to-the-methodology"></a>Zarovnání na metodologii

Tento typ digitálního vynálezu se dá zrychlit prostřednictvím každé fáze následujícího procesu, a to v souladu s metodikou uvedenou výše. Technické pokyny pro zrychlení digitálního vynálezu jsou uvedené v obsahu na levé straně. Tyto články byly seskupeny do stejných fází, aby je bylo možné zarovnat podle metodologie:

Na výše uvedeném obrázku se data a přehledy zarovnají s osvědčenými postupy popsanými v článku [data democratizing](./data.md) . V případě, že odborníci na danou problematiku odhalují přehledy, které mohou být opakované, je možné použít následující tři kroky k vyvýšení těchto přehledů:

- **Vzory:** Vyhledejte a definujte vzory pro vytváření prediktivních modelů.
- **Předpovědi:** Použijte vzor pro zákaznická data pro předpověď výsledků na základě modelu a základního vzoru.
- **Interakce:** Využijte předpovědi z aplikace nebo zdroje dat, abyste mohli nařídit interakci se zákazníkem.

## <a name="toolchain"></a>Sada nástrojů

V Azure se běžně využívají tyto nástroje k urychlení digitálního vynálezování v každé z výše uvedených fází: Azure ML, HDInsight, Hadoop R Scaleer a Azure SQL Data Warehouse. Způsob, jakým jednotlivé nástroje pomáhají s každou fází předvídání a vlivu, se projeví v doprovodném okně obsahu vlevo.

## <a name="get-started"></a>Začít

Obsah na levé straně obsahuje mnoho článků, které vám pomohou začít s každým z těchto nástrojů v tomto sada nástrojů.

> [!NOTE]
> Některé odkazy mohou opustit rozhraní pro přijetí cloudu, aby lépe překročily rozsah této architektury.
