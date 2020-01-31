---
title: Osvědčené postupy migrace do Azure
description: Úvod k osvědčeným postupům pro migraci do Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5cc4a0cfdfe605fdd374055e782db2f0ce47c13f
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807287"
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
