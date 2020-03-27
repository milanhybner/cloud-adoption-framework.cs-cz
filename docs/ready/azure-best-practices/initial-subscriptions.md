---
title: Vytvoření počátečních předplatných Azure
description: Zahajte přijetí Azure vytvořením počátečních předplatných.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 4e2a538c91328e7153f7f5ed37d07b8dbbeb4ea0
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359826"
---
# <a name="create-your-initial-azure-subscriptions"></a>Vytvoření počátečních předplatných Azure

Začněte s přijetím Azure vytvořením počáteční sady předplatných. Seznamte se s předplatnými, která byste měli začít v závislosti na vašich původních požadavcích.

## <a name="your-first-two-subscriptions"></a>Vaše první dvě předplatná

Začněte vytvořením dvou předplatných:

- Vytvořte jedno předplatné Azure, které bude obsahovat vaše produkční úlohy.
- Druhé předplatné slouží jako nevýrobní prostředí (vývoj/testování) s využitím [nabídky Azure pro vývoj/testování](https://azure.microsoft.com/pricing/dev-test) s nižšími cenami.

![Počáteční model předplatného, který zobrazuje klíče vedle polí označených jako produkce a neproduktivní](../../_images/ready/initial-subscription-model.png)

Tento přístup má mnoho výhod:

- Použití samostatných předplatných pro vaše produkční a nevýrobní prostředí vytváří hranici, která usnadňuje a bezpečněji správu prostředků.
- Azure má specifické nabídky pro vývoj a testování pro úlohy, které neposkytují produkty. Tyto nabídky poskytují zvýhodněné sazby za služby Azure a licencování softwaru.
- Vaše produkční a nevýrobní prostředí budou pravděpodobně mít různé sady zásad Azure. Použití samostatných předplatných umožňuje jednoduché použití jednotlivých zásad na úrovni předplatného.
- V rámci předplatného pro účely testování můžete u svých předplatných využít určité typy prostředků Azure. Poskytovatele prostředků můžete povolit v neprodukčním předplatném, aniž byste je měli k dispozici ve svém provozním prostředí.
- Předplatná pro vývoj/testování můžete použít jako izolovaná prostředí sandboxu. Tyto izolované prostory umožňují správcům a vývojářům rychle sestavovat a odtrhnout celé sady prostředků Azure. Tato izolace může také pomoct se záležitostmi ohledně ochrany dat a zabezpečení.
- Přijatelné prahové hodnoty nákladů, které definujete, se pravděpodobně liší v předplatných pro vývoj a testování.

## <a name="sandbox-subscriptions"></a>Předplatná izolovaného prostoru

Pokud máte cíle inovace v rámci strategie přijetí do cloudu, zvažte vytvoření jednoho nebo více předplatných izolovaného prostoru (sandbox). Zásady zabezpečení můžete použít k udržení těchto testovacích předplatných, které jsou izolované od produkčního a nevýrobního prostředí. Uživatelé můžou v těchto izolovaných prostředích snadno experimentovat s funkcemi Azure. K vytvoření těchto předplatných použijte nabídku pro vývoj/testování Azure.

![Model prvotního předplatného, který zobrazuje klíče vedle polí označených jako produkční, neproduktivní a Sandboxy](../../_images/ready/initial-subscription-model-with-sandboxes.png)

## <a name="shared-services-subscription"></a>Předplatné sdílených služeb

Pokud plánujete hostovat **více než 1 000 virtuálních počítačů nebo výpočetních instancí v cloudu do 24 měsíců**, vytvořte další předplatné Azure pro hostování sdílených služeb. To vás připraví na podporu podnikové architektury end.

![Počáteční model předplatného, který zobrazuje klíče vedle polí označených jako produkce a sdílené služby](../../_images/ready/initial-subscription-model-with-shared-services.png)

## <a name="next-steps"></a>Další kroky

Přečtěte si důvody, proč byste mohli chtít [vytvořit další předplatná Azure](./scale-subscriptions.md) , aby splňovala vaše požadavky.

> [!div class="nextstepaction"]
> [Vytvoření dalších předplatných pro škálování prostředí Azure](./scale-subscriptions.md)
