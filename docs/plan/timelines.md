---
title: Časové osy v plánu přijetí v cloudu
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak odhadnout časové osy na základě plánu přijetí v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 885d5c46099c0e161449aeae3f9c1203a2949728
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092651"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Časové osy v plánu přijetí v cloudu

V předchozím článku v této sérii byly úlohy a úlohy přiřazené k [vydaným verzím a iteracím](./iteration-paths.md). Tato přiřazení docházejí k odhadům časové osy v tomto článku.

Struktury rozpisu práce (WBS) se běžně používají v sekvenčních nástrojích pro správu projektů. Představují způsob, jakým budou dokončeny závislé úkoly v průběhu času. Tyto struktury fungují dobře, když jsou úkoly sekvenční. Vzájemné závislosti v úlohách nalezených v rámci přijetí cloudu usnadňují správu takových struktur. Chcete-li vyplnit tuto mezeru, můžete odhadnout časové osy založené na přiřazeních cesty iterace skrytím složitosti.

## <a name="estimate-timelines"></a>Odhadnutí časových os

Pokud chcete vytvořit časovou osu, začněte s verzemi. Tyto cíle vydání vytvoří cílové datum pro jakýkoliv dopad na firmu. Iterace pomáhají při zarovnávání těchto vydání s konkrétními časovými obdobími.

Pokud časová osa vyžaduje podrobnější milníky, určete milníky pomocí přiřazení iterace. Chcete-li provést toto přiřazení, Předpokládejme, že poslední instance úkolu souvisejícího s úlohou může sloužit jako konečný milník. Týmy také běžně vysloví finální úkol jako milník.

Pro libovolnou úroveň členitosti použijte poslední den iterace jako datum každého milníku. To spojuje dokončení přijetí úlohy do konkrétního data. Můžete sledovat datum v tabulce nebo sekvenčním nástroji pro správu projektu, jako je například aplikace Microsoft Project.

## <a name="delivery-plans-in-azure-devops"></a>Plány doručování ve službě Azure DevOps

Pokud ke správě plánu přijetí do cloudu používáte Azure DevOps, zvažte použití rozšíření [Microsoft Delivery Plans](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans) . Toto rozšíření může rychle vytvořit vizuální znázornění časové osy, která je založená na přiřazeních iterace a uvolnění.
