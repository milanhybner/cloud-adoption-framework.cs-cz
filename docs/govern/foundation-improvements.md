---
title: Vylepšete počáteční cloudový základ zásad správného řízení
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak přírůstkově vylepšit počáteční základ zásad správného řízení pro Cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 050d9cdfd2069a4d7da2e411233f6a60f270eb10
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706604"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Vylepšete počáteční cloudový základ zásad správného řízení

V tomto článku se předpokládá, že jste navázali [počáteční základ zásad správného řízení pro Cloud](./initial-foundation.md). Vzhledem k tomu, že je váš plán přijetí do cloudu implementovaný, vychází z navrhovaných přístupů, kterými týmy chtějí daný Cloud přijmout. Vzhledem k tomu, že tato rizika nastávají na konverzacích pro plánování vydaných verzí, použijte následující mřížku k rychlému určení několika osvědčených postupů, které vám pomají v úmyslu získat před skutečnými hrozbami.

## <a name="maturity-vectors"></a>Vektory splatnosti

V některých případech je možné pro počáteční základ zásad správného řízení použít následující osvědčené postupy, které řeší riziko nebo potřebu uvedenou v následující tabulce.

> [!IMPORTANT]
> Organizace prostředků může ovlivnit, jak se tyto osvědčené postupy používají. Je důležité začít s doporučeními, která nejlépe odpovídají počátečnímu základu pro řízení cloudu, který jste implementovali v předchozím kroku.

|Riziko/potřeby | Standardní firma | Komplexní firma |
|---|---|---|
|Citlivá data v cloudu|[Vylepšení oboru](./guides/standard/security-baseline-improvement.md)|[Vylepšení oboru](./guides/complex/security-baseline-improvement.md)|
|Klíčové aplikace v cloudu|[Vylepšení oboru](./guides/standard/resource-consistency-improvement.md)|[Vylepšení oboru](./guides/complex/resource-consistency-improvement.md)|
|Správa nákladů na Cloud|[Vylepšení oboru](./guides/standard/cost-management-improvement.md)|[Vylepšení oboru](./guides/complex/cost-management-improvement.md)|
|Více cloudů|[Vylepšení oboru](./guides/standard/multicloud-improvement.md)|[Vylepšení oboru](./guides/complex/multicloud-improvement.md)|
|Komplexní a starší Správa identit|neuvedeno|[Vylepšení oboru](./guides/complex/identity-baseline-improvement.md)|
|Několik vrstev zásad správného řízení|neuvedeno|[Vylepšení oboru](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Další kroky

Kromě aplikace s doporučenými postupy lze metodologii zásad správného řízení v rozhraní pro přijetí v cloudu přizpůsobit tak, aby odpovídala jedinečným obchodním omezením. Po splnění příslušných doporučení si [vyhodnoťte firemní zásady, abyste pochopili další požadavky na přizpůsobení](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Vyhodnocení firemních zásad](./corporate-policy.md)
