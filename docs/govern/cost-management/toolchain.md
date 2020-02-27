---
title: Nástroje Cost Management v Azure
description: Podívejte se, jak můžou Azure Native Tools pomoci při vyspělých zásadách a procesech, které podporují obor zásad správného řízení Cost Management.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 70014352d4b7f64f5c73a0fda96ef453f1a77176
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708780"
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
