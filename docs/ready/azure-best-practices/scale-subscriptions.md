---
title: Vytvoření dalších předplatných pro škálování prostředí Azure
description: Pomocí architektury cloudu pro přijetí v Azure se naučíte vyvíjet strategii pro škálování prostředí pomocí několika předplatných Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 3d879119e84bb2beebacce7a8086f2e356132bc2
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433220"
---
# <a name="create-additional-subscriptions-to-scale-your-azure-environment"></a>Vytvoření dalších předplatných pro škálování prostředí Azure

Organizace často používají několik předplatných Azure, abyste se vyhnuli omezením prostředků na základě předplatného a mohli lépe spravovat a řídit svoje prostředky Azure. Je důležité definovat strategii pro škálování vašich předplatných.

## <a name="review-fundamental-concepts"></a>Kontrola základních konceptů

Když rozšíříte prostředí Azure nad rámec [počátečních předplatných](./initial-subscriptions.md), je důležité porozumět konceptům Azure, jako jsou účty, klienti, adresáře a odběry. Další informace najdete v tématu [základní koncepty Azure](../considerations/fundamental-concepts.md).

Další požadavky mohou vyžadovat další odběry. Při rozšiřování cloudu mějte na paměti následující aspekty.

## <a name="technical-considerations"></a>Technické požadavky

**Omezení předplatného:** Předplatná mají definovaná omezení pro některé typy prostředků. Například počet virtuálních sítí v předplatném je omezený. Když se předplatné blíží těmto omezením, budete muset vytvořit další předplatné a umístit do něj další prostředky. Další informace najdete v tématu [omezení předplatného a služeb Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits#general-limits).

**Prostředky klasického modelu:** Pokud používáte Azure po dlouhou dobu, můžete mít prostředky, které byly vytvořené pomocí modelu nasazení Classic. Zásady Azure, řízení přístupu na základě rolí, seskupování prostředků a značky nelze použít pro prostředky klasického modelu. Tyto prostředky byste měli přesunout do předplatných, která obsahují jenom prostředky klasického modelu.

**Náklady:** Pro příchozí datové přenosy a výstupy mezi předplatnými může docházet k nějakým dalším poplatkům.

## <a name="business-priorities"></a>Obchodní priority

Vaše obchodní priority vám můžou vést k vytvoření dalších předplatných. Mezi tyto priority patří:

- Inovace
- Migrace
- Náklady
- Operace
- Zabezpečení
- Zásady správného řízení

Další informace o škálování vašich předplatných najdete v [Průvodci pro rozhodování o předplatném](../../decision-guides/subscriptions/index.md) v části rozhraní pro přijetí do cloudu.

## <a name="moving-resources-between-subscriptions"></a>Přesun prostředků mezi předplatnými

Při zvětšování modelu předplatného se můžete rozhodnout, že některé prostředky patří do jiných předplatných. Mezi předplatnými lze přesunout mnoho typů prostředků. K opětovnému vytváření prostředků v jiném předplatném můžete použít taky automatizovaná nasazení. Další informace najdete v tématu [Přesunutí prostředků do nové skupiny prostředků nebo předplatného](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="tips-for-creating-new-subscriptions"></a>Tipy pro vytváření nových předplatných

- Určete, kdo zodpovídá za vytváření nových předplatných.
- Rozhodněte, které typy prostředků jsou ve výchozím nastavení k dispozici v předplatném.
- Určete, jak by měla všechna standardní předplatná vypadat. Mezi požadavky patří přístup RBAC, zásady, značky a prostředky infrastruktury.
- Pokud je to možné, [programově Vytvářejte nová předplatná](https://docs.microsoft.com/azure/azure-resource-manager/management/programmatically-create-subscription) prostřednictvím instančního objektu. Aby bylo možné vytvářet odběry, musíte [objektu služby udělit oprávnění](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription) . Definujte skupinu zabezpečení, která může vyžadovat nová předplatná prostřednictvím automatizovaného pracovního postupu.
- Pokud jste zákazníkem se smlouvou Enterprise, požádejte podporu Azure, aby pro vaši organizaci zablokovala vytváření předplatných bez smlouvy Enterprise.

## <a name="next-steps"></a>Další kroky

Vytvořte hierarchii skupiny pro správu, která vám umožní [organizovat a spravovat vaše předplatná a prostředky](./organize-subscriptions.md).

> [!div class="nextstepaction"]
> [Uspořádání a Správa předplatných a prostředků](./organize-subscriptions.md)
