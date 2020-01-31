---
title: Nástroje Cost Management v Azure
description: Nástroje Cost Management v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e35530fbf3a858c000cb78c0c076d7d56d5fbd86
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806403"
---
# <a name="cost-management-tools-in-azure"></a>Nástroje Cost Management v Azure

[Cost management](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na způsoby vytváření plánů útraty cloudu, přidělování cloudových rozpočtů, monitorování a vynucování cloudových rozpočtů, zjišťování nákladných anomálií a úpravy plánu zásad správného řízení pro Cloud, pokud je skutečná útrata chybně zarovnaná.

Následuje seznam nativních nástrojů Azure, které mohou pomoci při vyspělosti zásad a procesů, které podporují tento obor řízení.

| Nástroj | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Balíček obsahu EA pro Azure](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Smlouva Enterprise požadováno?     | Ne         | Ne         | Ano         | Ne         |
|Řízení rozpočtu     | Ne         | Ano         | Ne         | Ano         |
|Monitorování útraty na jednom prostředku    | Ano         | Ano         | Ano         | Ne         |
|Monitorování útraty napříč několika prostředky    | Ne         | Ano        | Ano         | Ne         |
|Řízení útraty na jednom prostředku     | Ano – ruční změna velikosti         | Ano         | Ne         | Ano         |
|Vymáhání útraty napříč několika prostředky    | Ne         | Ano         | Ne         | Ano         |
|Vynutilit metadata monitorování účtů u prostředků    | Ne         | Ne         | Ne         | Ano         |
|Monitorování a detekce trendů     | Ano          | Ano        | Ano         | Ne         |
|Detekovat anomálie útraty     | Ne         | Ano        | Ano         | Ne        |
|Socialize odchylky     | Ne        | Ano        | Ano        | Ne        |
