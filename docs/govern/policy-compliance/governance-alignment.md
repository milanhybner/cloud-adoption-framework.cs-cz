---
title: Zarovnání Průvodce návrhem zásad správného nastavení cloudu k podnikovým zásadám
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zarovnání Průvodce návrhem zásad správného nastavení cloudu k podnikovým zásadám
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: c7be14efe6723a32808ba9bd2ba01f48292305df
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030248"
---
<!---
I've established policies. How to help developers adopt these policies?
Draft an architecture design guide.

[Aspirational statement] If you're using Azure, you can use one of ours as a starting point. The choose one of the following 6 as a starting point and mold it to fit your policies.
--->

# <a name="align-your-cloud-governance-design-guide-with-corporate-policy"></a>Zarovnání Průvodce návrhem zásad správného nastavení cloudu k podnikovým zásadám

Po [Definování zásad cloudu](./policy-definition.md) na základě [identifikovaných rizik](./business-risk.md)budete muset vygenerovat doprovodné materiály, které tyto zásady zarovnají vašim pracovníkům IT a vývojářům, na které se vztahují. Koncept Průvodce návrhem zásad správného řízení cloudu vám umožní určit konkrétní strukturální, technologické a procesní možnosti na základě příkazů zásad, které jste vygenerovali pro každý z [pěti oborů řízení](../governance-disciplines.md).

Průvodce návrhem zásad správného řízení cloudu by měl zřídit možnosti architektury a vzory návrhu pro každou základní komponentu infrastruktury cloudových nasazení, které nejlépe vyhovují vašim požadavkům na zásady. Kromě toho byste měli poskytnout nejdůležitější vysvětlení technologie, nástrojů a procesů, které budou podporovat každé z těchto rozhodnutí o návrhu.

I když se vaše prohlášení o analýze rizik a zásadách může v některých případech nezávislá do cloudové platformy, Průvodce návrhem by měl poskytnout podrobnosti o implementaci specifické pro platformu, které vaše IT a vývojářské týmy můžou použít při vytváření a nasazování cloudových úloh. Při rozhodování o návrhu a poskytování pokynů se zaměřte na architekturu, nástroje a funkce vaší zvolené platformy.

Průvodce návrhem cloudu by měl vzít v úvahu některé technické podrobnosti spojené s jednotlivými součástmi infrastruktury. nejedná se tedy o rozsáhlé technické dokumenty nebo specifikace. Zajistěte, aby vaše příručky odkazovaly na vaše příkazy zásad a jasně nastavovaná rozhodnutí o návrhu ve formátu, který usnadňuje personál pro pochopení a referenci.

<!-- markdownlint-enable MD033 -->

## <a name="using-the-actionable-governance-guides"></a>Použití pomocných průvodců zásad správného řízení

Pokud plánujete použít platformu Azure pro účely vašeho cloudu, rozhraní pro přijetí do cloudu poskytuje [akční příručky](../guides/index.md) , které ilustrují postupný přístup k modelu zásad správného řízení pro rozhraní pro přijetí cloudu. Tyto návody popisují řadu běžných scénářů přijetí, včetně obchodních rizik, požadavků na toleranci a příkazů zásad, které se přihlásily k vytvoření minimálního produktu pro řízení minimální životaschopnosti (MVP). Tyto příručky reprezentují přehled reálného prostředí pro zákazníky v rámci procesu přijetí cloudu v Azure.

Každé přijetí v cloudu má jedinečné cíle, priority a problémy, takže tyto ukázky by měly poskytnout dobrou šablonu pro převod zásad na doprovodné materiály. Vyberte nejbližší scénář pro vaši situaci jako výchozí bod a tvarovat ho tak, aby vyhovoval vašim konkrétním potřebám zásad.

## <a name="next-steps"></a>Další postup

S pokyny pro návrh můžete vytvořit procesy přihlášené k zásadám, které zajistí dodržování zásad.

> [!div class="nextstepaction"]
> [Vytváření procesů pro přistoupení k zásadám](./processes.md)
