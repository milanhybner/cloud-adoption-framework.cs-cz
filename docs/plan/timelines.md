---
title: Časové osy v plánu přijetí v cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Časové osy v plánu přijetí v cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 4e095dd90711f201935e88ea5f2712e881a8574b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828731"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Časové osy v plánu přijetí v cloudu

V předchozím článku v této sérii byly úlohy a úlohy přiřazené k vydaným [verzím a iteracím](./iteration-paths.md). Tato přiřazení docházejí k odhadům časové osy v tomto článku.

Struktury rozpisu práce (WBS) se běžně používají v sekvenčních nástrojích pro správu projektů. Představují způsob, jakým se v časovém intervalu dokončí závislé úlohy. Tyto struktury fungují dobře, když jsou úkoly sekvenční. Vzájemné závislosti v úlohách nalezených v rámci přijetí cloudu usnadňují správu takových struktur. Chcete-li vyplnit tuto mezeru, můžete odhadnout časové osy založené na přiřazeních cesty iterace skrytím složitosti.

## <a name="estimate-timelines"></a>Odhadnout časové osy

Pokud chcete vytvořit časovou osu, začněte s verzemi. Tyto cíle vydání vytvoří cílové datum pro jakýkoliv dopad na firmu. Iterace pomáhají při zarovnávání těchto vydání s konkrétními časovými obdobími.

Pokud časová osa vyžaduje podrobnější milníky, určete milníky pomocí přiřazení iterace. Chcete-li provést toto přiřazení, Předpokládejme, že poslední instance úkolu souvisejícího s úlohou může sloužit jako konečný milník. Týmy také běžně vysloví finální úkol jako milník.

Pro libovolnou úroveň členitosti použijte poslední den iterace jako datum každého milníku. To spojuje dokončení přijetí úlohy do konkrétního data. Můžete sledovat datum v tabulce nebo sekvenčním nástroji pro správu projektu, jako je například aplikace Microsoft Project.

## <a name="delivery-plans-in-azure-devops"></a>Plány doručování ve službě Azure DevOps

Pokud ke správě plánu přijetí do cloudu používáte Azure DevOps, zvažte použití rozšíření [Microsoft Delivery Plans](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans) . Toto rozšíření může rychle vytvořit vizuální znázornění časové osy, která je založená na přiřazeních iterace a uvolnění.
