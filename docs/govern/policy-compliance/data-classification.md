---
title: Co je klasifikace dat?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Co je klasifikace dat?
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d293aa5b4427b8f714175b85c6bb5197b53f107a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026681"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Co je klasifikace dat?

Klasifikace dat umožňuje určit a přiřadit hodnotu datům vaší organizace a je běžným výchozím bodem pro řízení. Proces klasifikace dat kategorizuje data podle citlivosti a dopadu na firmu, aby bylo možné identifikovat rizika. Jakmile jsou data klasifikována, je možné je spravovat způsobem, který chrání citlivá nebo důležitá data proti krádeži nebo ztrátě.

## <a name="understand-data-risks-then-manage-them"></a>Pochopení rizik dat a jejich správa

Před tím, než bude možné spravovat jakékoli riziko, je nutné ho pochopit. V případě zodpovědnosti proti porušení dat se v tomto principu zahájí klasifikace dat. Klasifikace dat je proces přidružení charakteristiky meta dat ke každému prostředku v digitální nemovitosti, který identifikuje typ dat přidružených k danému prostředku.

Společnost Microsoft navrhuje, aby všechny prostředky, které byly identifikovány jako potenciální kandidát pro migraci nebo nasazení do cloudu, měly popsány meta data pro zaznamenávání klasifikace dat, kritické pro podnikání a odpovědnost za fakturaci. Tyto tři body klasifikace můžou být delší způsob, jak pochopit a zmírnit rizika.

## <a name="microsofts-data-classification"></a>Klasifikace dat společnosti Microsoft

Následuje seznam klasifikací, které Microsoft používá. V závislosti na vašem oboru nebo stávajících požadavcích na zabezpečení mohou být standardy klasifikace dat již ve vaší organizaci existovat. Pokud žádný standardní neexistuje, pozvěte vás, abyste tuto ukázkovou klasifikaci použili k lepšímu pochopení vlastního digitálního majetku a profilu rizika.

- **Mimo firmu:** Data z vašeho osobního života, která nepatří do společnosti Microsoft.
- **Republik** Obchodní data, která jsou volně dostupná a schválená pro veřejnou spotřebu.
- **Obecné:** Obchodní data, která nejsou určena pro veřejnou cílovou skupinu.
- **Přehled** Podniková data, která by mohla způsobit poškození Microsoftu v případě, že jsou přesdílely.
- **Vysoce důvěrné:** Podniková data, která by v případě přesdílení způsobila rozsáhlá poškození Microsoftu

## <a name="tagging-data-classification-in-azure"></a>Označování klasifikace dat v Azure

Každý poskytovatel cloudu by měl nabídnout mechanismus pro zaznamenávání metadat o jakémkoli prostředku. V případě Azure představují značky prostředků navrhovaný přístup k úložišti metadat a tyto značky se dají použít k použití informací o klasifikaci dat pro nasazené prostředky. I když označení cloudových prostředků podle klasifikace není náhradou za proces klasifikace formálních dat, poskytuje cenný nástroj pro správu prostředků a používání zásad.

Další informace o označování prostředků v Azure najdete v článku o [použití značek k uspořádání prostředků Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="next-steps"></a>Další kroky

Použijte klasifikace dat v jednom z průvodců zásad správného řízení.

> [!div class="nextstepaction"]
> [Vybrat Průvodce zásad správného řízení pro akce](../guides/index.md)
