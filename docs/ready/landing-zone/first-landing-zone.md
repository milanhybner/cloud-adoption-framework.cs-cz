---
title: Aspekty cílových zón Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zjistěte, jakým způsobem cílové zóny poskytují základní stavební bloky libovolného prostředí přechodu na cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 04293b0e0d30ae1eaa85f4c86c6c7d70b2cfac82
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092970"
---
# <a name="first-landing-zone"></a>První cílová zóna

Infrastruktura jako kód je přirozený přechod během většiny úsilí o přijetí do cloudu. Nasazení první zóny pro vykládku v cloudu je obvyklým výchozím bodem přesunu do prostředí založeného na kódu. Tento článek vám pomůže pochopit pojem _cílové zóny_ a rozhodnout, která cílová zóna je nejvhodnější pro vaše aktuální potřeby přijetí.

## <a name="code-first-approach-to-landing-zones"></a>Přístup z kódu na zóny pro vykládku

Následující obrázek znázorňuje celou řadu možností pro cílové zóny. Následující možnosti vám pomůžou při výběru správné cílové zóny ještě dnes. Pomáhá také vytvořit vizi pro potřeby budoucích cílových zón.

![Možnosti cílové zóny](../../_images/ready/landing-zone-options.png)

A. Začněte kódem pro vytvoření konzistentních a opakovaně se opakujících cílových zón. Pokud jste obeznámeni s refaktoringem (nebo pokud se naučíte kód a infrastruktura), začněte se základem jednoduchého kódu, jako je plán migrace cílové zóny v rozhraní pro přijetí do cloudu. Tento přístup urychluje přijetí a vytváří praktické možnosti učení. Tento typ počáteční cílové zóny ale není navržený pro citlivá data ani pro klíčové úlohy bez dalšího refaktoringu.

B. Vzhledem k tomu, že se nasazení zvýší a požadavky se podrobněji identifikují, týmy pro přijetí a platformu refaktorují cílové zóny podle toho, co se učí. Proces rozšiřování zón pro vykládku připraví prostředí pro složitější požadavky na dodržování předpisů nebo architekturu. [Rozbalením cílové zóny](../considerations/index.md) získáte rozhodovací příručky a odkazy na osvědčené postupy, které vám pomůžou s úsilím refaktoringu. Rozbalení cílové zóny může pomoci se zabezpečením, operacemi a požadavky na dodržování zásad správného řízení.

C. Některé plány přijetí do cloudu se řídí požadavky na externí dodržování předpisů. Pro snížení zátěže těchto požadavků Azure poskytuje několik ukázkových Azure modrotisky. Některé ukázky je možné přidat do prvního počátečního podrobného plánu. Další ukázky zahrnují také konkrétní implementaci, která může sloužit jako první cílová zóna.

D. Když partner poskytne průběžné spravované služby nebo se doručí na plán přijetí, obvykle poskytne vlastní cílovou zónu. Použití zóny partnerského přistání by mohlo urychlit úsilí o přijetí a zajistit konzistentní požadavky na provozní správu. Poskytněte ale další aspekty interního řízení a požadavků na zabezpečení, aby se zajistilo jejich zarovnání.

> [!NOTE]
> Předtím, než budete pokračovat s přístupem zaměřeném na kód a refaktoring, by čtenáři měli být obeznámeni s [konkurenčními prioritami za toto rozhodnutí](../../strategy/balance-competing-priorities.md#balance-during-ready). Při volbě přístupu k zóně vyzkoušení je důležité pochopit, jaký je nutný zůstatek mezi "časem přijetí" a "dlouhodobými operacemi".

## <a name="choosing-a-first-landing-zone"></a>Výběr první cílové zóny

Výběr první cílové zóny závisí na počtu proměnných. Následující mřížka zachycuje některé možnosti pro první cílové zóny, spolu s proměnnými, které mohou toto rozhodnutí řídit.

| Cílová zóna                                 | Cloudové prostředí  | Měřítko             | Čas zjišťování | Připravené na produkci | Hybridní             | Citlivá data     | Kritická poslání   | Dodržování předpisů         |
|----------------------------------------------|-------------------|-------------------|----------------|------------------|--------------------|--------------------|--------------------|--------------------|
| [Migrace CAF](./migrate-landing-zone.md)     | Novinka do cloudu      | assety < 1 000    | 1 až 5 dní    | Omezený rozsah – > | Vyžaduje se rozšíření. | Vyžaduje se rozšíření. | Vyžaduje se rozšíření. | Vyžaduje se rozšíření. |
| [CAF Terraformu](./terraform-landing-zone.md) | Různé šablony | Různé šablony | 10 až 20 týdnů | Omezený rozsah – > | Dostupné moduly  | Dostupné moduly  | Dostupné moduly  | Dostupné moduly  |

V následující tabulce jsou uvedené stejné zóny pro vykládku z mírně odlišné perspektivy, aby bylo možné seznámení s více technickými procesy rozhodování.

| Cílová zóna                                 | Rozbočovač                          | Paprsku    | Cloudový model | Technologie      |
|----------------------------------------------|------------------------------|----------|-------------|-----------------|--|--|--|
| [Migrace CAF](./migrate-landing-zone.md)     | Vyžaduje se refaktoring.            | Zahrnuto | Jenom Azure  | Azure Blueprint |
| [CAF Terraformu](./terraform-landing-zone.md) | Zahrnuto v modulu VDC       | Zahrnuto | Více cloudů  | Terraform       |

## <a name="next-steps"></a>Další kroky

Pokud si stále nejste jisti, kterou první cílovou zónu si zvolíte, doporučujeme začít s podrobným [plánem CAF migrace cílové zóny](./migrate-landing-zone.md).

> [!div class="nextstepaction"]
> [Podrobný plán CAF migrace cílové zóny](./migrate-landing-zone.md)
