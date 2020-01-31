---
title: 'Příručka zásad správného řízení pro komplexní podniky: počáteční podniková zásada za strategii zásad správného řízení'
description: 'Příručka zásad správného řízení pro komplexní podniky: počáteční podniková zásada za strategii zásad správného řízení'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2949c89b5cafd472af98245a37cae43e69c634a4
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806301"
---
# <a name="governance-guide-for-complex-enterprises-initial-corporate-policy-behind-the-governance-strategy"></a>Příručka zásad správného řízení pro komplexní podniky: počáteční podniková zásada za strategii zásad správného řízení

Následující podnikové zásady definují počáteční umístění zásad správného řízení, což je výchozí bod tohoto průvodce. Tento článek definuje předem připravená rizika, počáteční příkazy zásad a prvotní procesy pro vykonání příkazů zásad.

> [!NOTE]
>Podniková zásada není technickým dokumentem, ale obsahuje mnoho technických rozhodnutí. MVP pro kontrolu zásad správného řízení, který je popsaný v [přehledu](./index.md) , je nakonec odvozený od této zásady. Před implementací MVP pro řízení by vaše organizace měla vytvořit podnikovou zásadu na základě vašich vlastních cílů a obchodních rizik.

## <a name="cloud-governance-team"></a>Tým zásad správného řízení cloudu

CIO nedávno držela schůzku se svým týmem zásad správného IT, aby porozuměla historii osobních údajů a zásad kritických zásad a zkontrolovala účinek změny těchto zásad. CIO také probrala Celkový potenciál cloudu pro IT a společnost.

Po schůzce se dva členové týmu pro řízení IT požádali o oprávnění k výzkumu a podpoře úsilí v oblasti plánování cloudu. UZNÁVAJÍCE nutnost zásad správného řízení a možnost omezit její stínové vlastnictví, což je ředitel zásad správného řízení IT, který tento nápad podporuje. V takovém případě se jednalo o cloudový tým zásad správného řízení. Během několika dalších měsíců zdědí z perspektivy zásad správného řízení vyčištění mnoha chyb provedených během průzkumu v cloudu. Tím získají moniker _Cloud starají_. V pozdějších iteracích Tato příručka ukazuje, jak se jejich role v průběhu času mění.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Indikátory tolerance

Aktuální tolerance rizika je vysoká a později pro investice do zásad správného řízení cloudu je nízká. V takovém případě indikátory tolerance slouží jako systém včasného varování, který aktivuje investici času a energie. Pokud jsou pozorovány následující indikátory, bylo by vhodné předem navýšit strategii zásad správného řízení.

- **Cost management:** Škálování nasazení překračuje 1 000 prostředků do cloudu nebo měsíční útrata překračuje $10 000 USD za měsíc.
- **Směrné plány identity:** Zahrnutí aplikací se staršími požadavky na službu Multi-Factor Authentication nebo třetích stran.
- **Základní hodnoty zabezpečení:** Zahrnutí chráněných dat v definovaných plánech přijetí do cloudu.
- **Konzistence prostředků:** Zahrnutí všech klíčových aplikací v definovaných plánech přijetí do cloudu.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Další kroky

Tato podniková zásada připraví tým zásad správného řízení cloudu, aby implementovala MVP pro řízení MVP, který bude základem pro přijetí. Dalším krokem je implementace tohoto MVP.

> [!div class="nextstepaction"]
> [Vysvětlené osvědčené postupy](./prescriptive-guidance.md)
