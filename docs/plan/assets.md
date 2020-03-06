---
title: Zarovnání prostředků na úlohy s upřednostněním priorit
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak v rámci svých priorit přizpůsobit prostředky.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: c7e90c1536b2911f8301b1a97f8731139976b4f1
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78342061"
---
# <a name="align-assets-to-prioritized-workloads"></a>Zarovnání prostředků na úlohy s upřednostněním priorit

Zatížení je koncepční popis kolekce assetů: virtuální počítače, aplikace a zdroje dat. Předchozí článek, určení [priorit a definování úloh](./workloads.md), měl doprovodné materiály pro shromažďování dat, která budou definovat zatížení. Před migrací vyžaduje některé technické vstupy v tomto seznamu další ověření. Tento článek vám pomůže s ověřováním následujících vstupů:

- **Aplikace:** Vypíše všechny aplikace, které jsou součástí této úlohy.
- **Virtuální počítače a servery:** Vypíše všechny virtuální počítače nebo servery, které jsou součástí úlohy.
- **Zdroje dat:** Seznam všech zdrojů dat zahrnutých do úlohy.
- **Závislosti:** Vypíše všechny závislosti assetů, které nejsou součástí úlohy.

K dispozici je několik možností pro sestavení těchto dat. Níže jsou uvedené některé z nejběžnějších přístupů.

## <a name="alternative-inputs-migrate-modernize-innovate"></a>Alternativní vstupy: migrace, modernizovat, inovace

Cílem předchozích datových bodů je zachytit relativní technické úsilí a závislosti jako pomoc při stanovení priorit. V závislosti na požadovaném přechodu možná budete muset shromáždit alternativní datové body, které budou podporovat správné stanovení priorit.

**Migrace:** Pro účely čisté migrace existují stávající závislosti inventáře a prostředků jako poctivá míra relativní složitosti.

**Modernizovat:** Když je cílem úlohy modernizovat aplikace nebo jiné prostředky, jsou tyto datové body stále v plné míry složitosti. Může být ale vhodné přidat vstup pro příležitosti k modernizaci do dokumentace k úlohám.

Inovace **:** V případě, že se data nebo obchodní logika v průběhu snahy o přijetí do cloudu prochází změnou materiálu, považuje se za *inovační* typ transformace. Totéž platí při vytváření nových dat nebo nové obchodní logiky. U jakýchkoli scénářů inovace nejspíš migrace prostředků bude představovat nejmenší množství potřebných úsilí. V těchto scénářích by měl tým navrhnout sadu technických vstupních dat pro měření relativní složitosti.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate poskytuje sadu funkcí seskupení, které mohou zrychlit agregaci aplikací, virtuálních počítačů, zdrojů dat a závislostí. Po definování úloh se dají použít jako základ pro seskupování prostředků na základě mapování závislostí.

Dokumentace k Azure Migrate poskytuje pokyny [k seskupení počítačů na základě závislostí](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies).

## <a name="configuration-management-database"></a>Databáze správy konfigurace

Některé organizace mají dobře udržovanou databázi správy konfigurace (CMDB) v rámci svých stávajících nástrojů pro správu operací. Můžou použít CMDB nebo k poskytnutí vstupních datových bodů popsaných výše.

## <a name="next-steps"></a>Další kroky

[Projděte si rozhodnutí o racionalizaci](./review-rationalization.md) na základě zarovnání prostředků a definic úloh.

> [!div class="nextstepaction"]
> [Kontrola racionalizace rozhodnutí](./review-rationalization.md)
