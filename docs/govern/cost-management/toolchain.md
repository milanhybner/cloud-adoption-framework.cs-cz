---
title: Nástroje Cost Management v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nástroje Cost Management v Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 230e36d1ca59c208109eedbbdf7466f6373f4b00
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028951"
---
# <a name="cost-management-tools-in-azure"></a>Nástroje Cost Management v Azure

[Cost management](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na způsoby vytváření plánů útraty cloudu, přidělování cloudových rozpočtů, monitorování a vynucování cloudových rozpočtů, zjišťování nákladných anomálií a úpravy plánu zásad správného řízení pro Cloud, pokud je skutečná útrata chybně zarovnaná.

Následuje seznam nativních nástrojů Azure, které mohou pomoci při vyspělosti zásad a procesů, které podporují tento obor řízení.

| Tool | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Balíček obsahu EA pro Azure](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Smlouva Enterprise požadováno?     | Ne         | Ne         | Ano         | Ne         |
|Řízení rozpočtu     | Ne         | Ano         | Ne         | Ano         |
|Monitorování útraty na jednom prostředku    | Ano         | Ano         | Ano         | Ne         |
|Monitorování útraty napříč několika prostředky    | Ne         | Ano        | Ano         | Ne         |
|Řízení útraty na jednom prostředku     | Ano – ruční změna velikosti         | Ano         | Ne         | Ano         |
|Vymáhání útraty napříč několika prostředky    | Ne         | Ano         | Ne         | Ano         |
|Vynutilit metadata monitorování účtů u prostředků    | Ne         | Ne         | Ne         | Ano         |
|Monitorování a detekce trendů     | Ano – omezení         | Ano        | Ano         | Ne         |
|Detekovat anomálie útraty     | Ne         | Ano        | Ano         | Ne        |
|Socialize odchylky     | Ne        | Ano        | Ano        | Ne        |
