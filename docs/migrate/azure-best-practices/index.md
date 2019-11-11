---
title: Osvědčené postupy migrace do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod k osvědčeným postupům pro migraci do Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1519adff06d600b9829c9b7ff3ca82a0aa5a0160
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753375"
---
# <a name="azure-migration-best-practices"></a>Osvědčené postupy migrace do Azure

Azure poskytuje několik nástrojů v Azure jako pomoc ke zvládnutí procesu migrace. Tento oddíl architektury přechodu na cloud slouží jako pomoc čtenářům implementovat tyto nástroje v souladu s osvědčenými postupy pro migraci. Tyto osvědčené postupy odpovídají jednomu z procesů v rámci modelu migrace architektury přechodu na cloud znázorněné na obrázku níže.

Rozbalte jakýkoli proces v obsahu na levé straně a zobrazíte osvědčené postupy, které jsou obvykle nutné v průběhu tohoto procesu.

![Model migrace architektury přechodu na cloud](../../_images/operational-transformation-migrate.png)

> [!NOTE]
> Plánování digitálních aktiv a posouzení prostředků představují dvě různé úrovně plánování a hodnocení migrace:
>
> - **Plánování digitálních aktiv:** Během plánování plánujete nebo racionalizujete digitální aktiva, abyste vytvořili celkový backlog migrace. Tento plán je ale založený na některých předpokladech a podrobnostech, které je potřeba ověřit dřív, než je možné úlohu migrovat.
> - **Posouzení prostředků:** Jednotlivé prostředky úlohy posuzujete před migrací úlohy, abyste vyhodnotili kompatibilitu s cloudem a pochopili omezení architektury a velikosti. Tento proces ověří počáteční předpoklady a poskytne podrobné informace potřebné k migraci jednotlivého prostředku.
