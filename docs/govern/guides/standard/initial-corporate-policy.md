---
title: 'Standardní zásady správného řízení podniku: počáteční podniková zásada'
description: Rozhraní pro přijetí v cloudu pro Azure použijte k definování počátečního umístění zásad správného řízení, rizik prvotní fáze, počátečních příkazů zásad a procesů vynuceného vynucení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 64f04fe32445f79f36fe3846f16e3296e9424130
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170932"
---
# <a name="standard-enterprise-governance-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Standardní příručka pro zásady správného řízení podniku: počáteční podniková zásada za strategii zásad správného řízení

Následující podnikové zásady definují počáteční umístění zásad správného řízení, což je výchozí bod tohoto průvodce. Tento článek definuje předem připravená rizika, počáteční příkazy zásad a prvotní procesy pro vykonání příkazů zásad.

> [!NOTE]
>Podniková zásada není technickým dokumentem, ale obsahuje mnoho technických rozhodnutí. MVP pro kontrolu zásad správného řízení, který je popsaný v [přehledu](./index.md) , je nakonec odvozený od této zásady. Před implementací MVP pro řízení by vaše organizace měla vytvořit podnikovou zásadu na základě vašich vlastních cílů a obchodních rizik.

## <a name="cloud-governance-team"></a>Tým zásad správného řízení cloudu

V tomto mluveném komentáři tým zásad správného řízení cloudu sestává ze dvou správců systémů, kteří uznávají potřebu zásad správného řízení. Během několika dalších měsíců zdědí úlohu vyčistění zásad správného řízení firemního cloudu, který jim poskytne název _cloudové starajíy_. V následných iteracích se tento název nejspíš změní.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Indikátory tolerance

Současná tolerance pro riziko je vysoká a později pro investice do zásad správného řízení cloudu je nízká. V takovém případě indikátory tolerance slouží jako systém včasného varování, který aktivuje více investic času a energie. Pokud jsou pozorovány následující indikátory, měli byste vylepšit strategii zásad správného řízení.

- **Cost management:** Škálování nasazení překračuje předem vymezené limity počtu prostředků nebo měsíčních nákladů.
- **Základní hodnoty zabezpečení:** Zahrnutí chráněných dat v definovaných plánech přijetí do cloudu.
- **Konzistence prostředků:** Zahrnutí všech klíčových aplikací v definovaných plánech přijetí do cloudu.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Další kroky

Tato podniková zásada připraví tým zásad správného řízení cloudu, aby implementovala MVP pro řízení MVP, který bude základem pro přijetí. Dalším krokem je implementace tohoto MVP.

> [!div class="nextstepaction"]
> [Vysvětlené osvědčené postupy](./prescriptive-guidance.md)
