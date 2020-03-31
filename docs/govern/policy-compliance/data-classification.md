---
title: Co je klasifikace dat?
description: Klasifikace dat umožňuje určit a přiřadit hodnotu datům vaší organizace a poskytuje běžný výchozí bod pro řízení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 380229fd898fa36e425f4c4792de221139b64cec
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430834"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Co je klasifikace dat?

Klasifikace dat umožňuje určit a přiřadit hodnotu datům vaší organizace a poskytuje běžný výchozí bod pro řízení. Proces klasifikace dat kategorizuje data podle citlivosti a dopadu na firmu, aby bylo možné identifikovat rizika. Když jsou data klasifikována, můžete je spravovat způsobem, který chrání citlivá nebo důležitá data proti krádeži nebo ztrátě.

## <a name="understand-data-risks-then-manage-them"></a>Pochopení rizik dat a jejich správa

Před tím, než bude možné spravovat jakékoli riziko, je nutné ho pochopit. V případě zodpovědnosti proti porušení dat se v tomto principu zahájí klasifikace dat. Klasifikace dat je proces přidružení charakteristické vlastnosti metadat ke každému prostředku v digitální nemovitosti, který identifikuje typ dat přidružených k danému prostředku.

Jakýkoli Asset identifikovaný jako potenciální kandidát pro migraci nebo nasazení do cloudu by měl mít zdokumentované metadata pro záznam klasifikace dat, kritické pro podnikání a odpovědnost za fakturaci. Tyto tři body klasifikace můžou být delší způsob, jak pochopit a zmírnit rizika.

## <a name="classifications-microsoft-uses"></a>Klasifikace, které Microsoft používá

Následuje seznam klasifikací, které Microsoft používá. V závislosti na vašem oboru nebo stávajících požadavcích na zabezpečení mohou být standardy klasifikace dat již ve vaší organizaci existovat. Pokud žádný standardní neexistuje, možná budete chtít použít tuto klasifikaci vzorků k lepšímu pochopení svého vlastního digitálního majetku a profilu rizika.

- **Mimo firmu:** Data z vašeho osobního života, která nepatří společnosti Microsoft.
- **Veřejné:** Obchodní data, která jsou volně dostupná a schválená pro veřejnou spotřebu.
- **Obecné:** Obchodní data, která nejsou určena pro veřejnou cílovou skupinu.
- **Důvěrné:** Podniková data, která můžou způsobit poškození Microsoftu v případě, že jsou přesdílely.
- **Vysoce důvěrné:** Podniková data, která by v případě přesdílení způsobila rozsáhlá poškození Microsoftu

## <a name="tagging-data-classification-in-azure"></a>Označování klasifikace dat v Azure

Značky prostředků jsou dobrým přístupem k úložišti metadat a tyto značky můžete použít k použití informací o klasifikaci dat pro nasazené prostředky. I když označení cloudových prostředků podle klasifikace není náhradou za proces klasifikace formálních dat, poskytuje cenný nástroj pro správu prostředků a používání zásad. [Azure Information Protection](https://docs.microsoft.com/azure/information-protection/what-is-information-protection) je skvělé řešení, které vám usnadní klasifikaci samotných _dat_ bez ohledu na to, kde se nachází (místně, v Azure nebo někde jinde). Zvažte to jako součást celkové strategie klasifikace.

Další informace o označování prostředků v Azure najdete v tématu [použití značek k uspořádání prostředků Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="next-steps"></a>Další kroky

Použijte klasifikace dat v jednom z průvodců zásad správného řízení.

> [!div class="nextstepaction"]
> [Vybrat Průvodce zásad správného řízení pro akce](../guides/index.md)
