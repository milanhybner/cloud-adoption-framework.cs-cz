---
title: Zarovnání odpovědností napříč týmy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se sjednotit zodpovědnosti mezi týmy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 40ccd0c17a55a87c84d40abd749bf8e61f891e6c
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549075"
---
# <a name="align-responsibilities-across-teams"></a>Zarovnání zodpovědnosti mezi týmy

Naučte se sladit zodpovědnosti mezi týmy, a to tak, že vytvoříte matrici pro více týmů, která identifikuje *odpovědné, účetní, konzultované a podrobné* (RACI) strany. Tento článek poskytuje příkladovou matrici RACI pro organizační struktury popsané v tématu [vytváření týmových struktur](./organization-structures.md):

- [Jenom tým pro přijetí do cloudu](#cloud-adoption-team-only)
- [Osvědčený postup MVP](#best-practice-minimum-viable-product-mvp)
- [Centrální IT oddělení](#central-it)
- [Strategické zarovnání](#strategic-alignment)
- [Provozní zarovnání](#operational-alignment)
- [Cloudové centrum excelence (CCoE)](#cloud-center-of-excellence-ccoe)

Chcete-li sledovat rozhodování o organizační struktuře v průběhu času, Stáhněte a upravte [šablonu tabulky RACI](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx).

Příklady v tomto článku určují tyto RACI konstrukce:

- Jeden tým, který je pro funkci *účet* .
- Týmy, které jsou *zodpovědné* za výsledky.
- Týmy, které by měly být během plánování *projednány* .
- Týmy, které by měly být *informovány* po dokončení práce.

Poslední řádek každé tabulky (kromě prvního) obsahuje odkaz na nejvíce zarovnaný cloudovou schopnost pro další informace.

## <a name="cloud-adoption-team-only"></a>Jenom tým pro přijetí do cloudu

|  |Doručování řešení  |Obchodní zarovnání  |Správa změn  |Operace řešení  |Zásady správného řízení |Doba splatnosti platformy  |Operace platformy  |Automatizace platforem  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Tým přijetí cloudu |Odpovědné|Odpovědné|Odpovědné|Odpovědné|Odpovědné|Odpovědné|Odpovědné|Odpovědné|

## <a name="best-practice-minimum-viable-product-mvp"></a>Osvědčený postup: minimální životaschopný produkt (MVP)

|  |Doručování řešení  |Obchodní zarovnání  |Správa změn  |Operace řešení  |Zásady správného řízení |Doba splatnosti platformy  |Operace platformy  |Automatizace platforem  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Tým přijetí cloudu|Odpovědné|Odpovědné|Odpovědné|Odpovědné|Konzultované|Konzultované|Konzultované|Oznámeno|
|Tým zásad správného řízení cloudu|Konzultované|Oznámeno|Oznámeno|Oznámeno|Odpovědné|Odpovědné|Odpovědné|Odpovědné|
||||||||||
|Zarovnaná schopnost cloudu|[Přijetí do cloudu](./cloud-adoption.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudové operace](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md) -[zásad správného řízení cloudu](./cloud-governance.md)|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová automatizace](./cloud-automation.md) [CCoE](./cloud-center-of-excellence.md) -|

## <a name="central-it"></a>Centrální IT

| |Doručování řešení  |Obchodní zarovnání  |Správa změn  |Operace řešení  |Zásady správného řízení |Doba splatnosti platformy  |Operace platformy  |Automatizace platforem  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Tým přijetí cloudu  |Odpovědné|Odpovědné|Zodpovídá    |Zodpovídá|Oznámeno   |Oznámeno   |Oznámeno   |Oznámeno   |
|Tým zásad správného řízení cloudu|Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |Odpovědné|Konzultované  |Zodpovídá|Oznámeno   |
|Centrální IT           |Konzultované  |Oznámeno   |Odpovědné   |Odpovědné   |Zodpovídá  |Odpovědné|Odpovědné|Odpovědné|
||||||||||
|Zarovnaná schopnost cloudu|[Přijetí do cloudu](./cloud-adoption.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudové operace](./cloud-operations.md)|[Zásady správného řízení cloudu](./cloud-governance.md)|[Centrální IT oddělení](./central-it.md)|[Centrální IT oddělení](./central-it.md)|[Centrální IT oddělení](./central-it.md)|

## <a name="strategic-alignment"></a>Strategické zarovnání

|  |Doručování řešení  |Obchodní zarovnání  |Správa změn  |Operace řešení  |Zásady správného řízení |Doba splatnosti platformy  |Operace platformy  |Automatizace platforem  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Tým strategie cloudu  |Konzultované  |Odpovědné|Odpovědné|Konzultované  |Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |
|Tým přijetí cloudu  |Odpovědné|Konzultované  |Zodpovídá|Odpovědné|Oznámeno   |Oznámeno   |Oznámeno   |Oznámeno   |
|RACI modelu CCoE      |Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |Odpovědné|Odpovědné|Odpovědné|Odpovědné|
||||||||||
|Zarovnaná schopnost cloudu|[Přijetí do cloudu](./cloud-adoption.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudové operace](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md) -[zásad správného řízení cloudu](./cloud-governance.md)|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová automatizace](./cloud-automation.md) [CCoE](./cloud-center-of-excellence.md) -|

## <a name="operational-alignment"></a>Provozní zarovnání

|  |Doručování řešení  |Obchodní zarovnání  |Správa změn  |Operace řešení  |Zásady správného řízení |Doba splatnosti platformy  |Operace platformy  |Automatizace platforem  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Tým strategie cloudu  |Konzultované  |Odpovědné|Odpovědné|Konzultované  |Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |
|Tým přijetí cloudu  |Odpovědné|Konzultované  |Zodpovídá|Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |Oznámeno   |
|Tým cloudových operací|Konzultované  |Konzultované  |Zodpovídá|Odpovědné|Konzultované  |Oznámeno   |Odpovědné|Konzultované  |
|RACI modelu CCoE      |Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |Odpovědné|Odpovědné|Zodpovídá|Odpovědné|
||||||||||
|Zarovnaná schopnost cloudu|[Přijetí do cloudu](./cloud-adoption.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudové operace](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md) -[zásad správného řízení cloudu](./cloud-governance.md)|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová automatizace](./cloud-automation.md) [CCoE](./cloud-center-of-excellence.md) -|

## <a name="cloud-center-of-excellence-ccoe"></a>Cloudové centrum excelence (CCoE)

|  |Doručování řešení  |Obchodní zarovnání  |Správa změn  |Operace řešení  |Zásady správného řízení |Doba splatnosti platformy  |Operace platformy  |Automatizace platforem  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Tým strategie cloudu  |Konzultované  |Odpovědné|Odpovědné|Konzultované  |Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |
|Tým přijetí cloudu  |Odpovědné|Konzultované  |Zodpovídá|Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |Oznámeno   |
|Tým cloudových operací|Konzultované  |Konzultované  |Zodpovídá|Odpovědné|Konzultované  |Oznámeno   |Odpovědné|Konzultované  |
|Tým zásad správného řízení cloudu|Konzultované  |Oznámeno   |Oznámeno   |Konzultované  |Odpovědné|Konzultované  |Zodpovídá|Oznámeno   |
|Tým cloudové platformy  |Konzultované  |Oznámeno   |Oznámeno   |Konzultované  |Konzultované  |Odpovědné|Zodpovídá|Zodpovídá|
|Tým Cloud Automation|Konzultované  |Oznámeno   |Oznámeno   |Oznámeno   |Konzultované  |Zodpovídá|Zodpovídá|Odpovědné|
||||||||||
|Zarovnaná schopnost cloudu|[Přijetí do cloudu](./cloud-adoption.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudová strategie](./cloud-strategy.md)|[Cloudové operace](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md) -[zásad správného řízení cloudu](./cloud-governance.md)|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová platforma](./cloud-platform.md) [CCoE](./cloud-center-of-excellence.md) -|[Cloudová automatizace](./cloud-automation.md) [CCoE](./cloud-center-of-excellence.md) -|

## <a name="next-steps"></a>Další kroky

Chcete-li sledovat rozhodnutí o struktuře organizace v průběhu času, Stáhněte a upravte [šablonu tabulky RACI](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx). Zkopírujte a upravte nejblíže zarovnaný vzorek z matric RACI v tomto článku.

> [!div class="nextstepaction"]
> [Stáhnout šablonu tabulky RACI](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)
