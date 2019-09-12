---
title: Provedení kontroly zásad cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak provádět kontrolu zásad cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ec3cc2eda1cd3c67b2d5e8c2f7dc04a8867622aa
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70826937"
---
<!-- markdownlint-disable MD026 -->

# <a name="conduct-a-cloud-policy-review"></a>Provedení kontroly zásad cloudu

Kontrola zásad cloudu je prvním krokem ke [správě splatnosti](../index.md) v cloudu. Cílem tohoto procesu je modernizovat stávající podnikové zásady IT. Po dokončení aktualizované zásady poskytují odpovídající úroveň řízení rizik pro cloudové prostředky. Tento článek popisuje proces kontroly zásad cloudu a jeho důležitost.

## <a name="why-perform-a-cloud-policy-review"></a>Proč provést kontrolu zásad cloudu?

Většina společností ji spravuje prostřednictvím provádění procesů, které se týkají zásad řízení. V malých firmách se tyto zásady můžou neoficiální a procesy budou volně definovány. Jelikož se podniky rozrůstou na velké podniky, zásady a procesy jsou v úmyslu jasně zdokumentováné a konzistentně spuštěné.

Vzhledem k tomu, že společnosti uzavřely podnikové zásady IT, mají závislosti na minulých technických rozhodnutích tendenci Seep se na řízení zásad. Například běžné informace o procesech zotavení po havárii zahrnují zásady, které zajišťují zálohování na pásku mimo lokalitu. Toto zahrnutí předpokládá závislost na jednom typu technologie (zálohy na pásce), které už nemusí být relevantní.

Cloudové transformace vytvářejí přirozený bod inflexe pro přehodnocování starších rozhodnutí o zásadách v minulosti. Technické možnosti a výchozí procesy se výrazně mění v cloudu, stejně jako tato zděděná rizika. Pomocí předchozího příkladu zásady zálohování na pásku vzniklé rizikem jediného bodu selhání tím, že zachovají data na jednom místě a podnik potřebuje minimalizovat rizikový profil tím, že toto riziko sníží. V nasazení v cloudu existuje několik možností, které dodávají stejné zmírnění rizik, a to s mnohem kratšími cíli pro dobu obnovení (RTO). Příklad:

- Řešení nativní pro Cloud by mohlo umožňovat geografickou replikaci Azure SQL Database.
- Hybridní řešení může použít Azure Site Recovery k replikaci úloh IaaS do několika datových center.

Při provádění transformace cloudu se často řídí mnoho nástrojů, služeb a procesů, které jsou k dispozici pro týmy pro přijetí v cloudu. Pokud jsou tyto zásady založené na starších technologiích, mohou bránit úsilí týmu o změnu. V nejhorším případě jsou důležité zásady zcela ignorovat z týmu migrace, aby bylo možné alternativní řešení. Ani to není přijatelný výsledek.

## <a name="the-cloud-policy-review-process"></a>Proces kontroly zásad cloudu

Recenze zásad cloudu zarovnají stávající zásady správného řízení IT a zabezpečení IT s [pěti disciplínami zásad správného řízení cloudu](../index.md): [Cost management](../cost-management/index.md), [směrného plánu zabezpečení](../security-baseline/index.md), [směrného plánu identity](../identity-baseline/index.md), [konzistenci prostředků](../resource-consistency/index.md)a [akceleraci nasazení](../deployment-acceleration/index.md).

U každého z těchto oborů se v procesu kontroly postupuje takto:

1. Projděte si stávající místní zásady týkající se konkrétního oboru a vyhledejte dva klíčové datové body: starší závislosti a zjištěná obchodní rizika.
2. Vyhodnoťte každé z obchodních rizik tak, že požádáme o jednoduchou otázku: "Podniková rizika stále existují v cloudovém modelu?"
3. Pokud riziko ještě existuje, přepište zásadu tím, že zdokumentujte nezbytné zmírnění, nikoli technické řešení.
4. Projděte si aktualizované zásady s týmy pro přijetí cloudu, které vám pomohou pochopit možná řešení požadovaných rizik.

## <a name="example-of-a-policy-review-for-a-legacy-policy"></a>Příklad kontroly zásad pro starší zásady

Pokud chcete zadat příklad procesu, zkuste znovu použít zásady zálohování na pásku v předchozí části:

- Podnikové zásady připravují zálohy na pásku mimo provoz všech produkčních systémů. V této zásadě vidíte dva datové body, které vás zajímají:
  - Starší závislost na řešení zálohování na pásku
  - Předpokládané obchodní riziko spojené s úložištěm záloh ve stejném fyzickém umístění jako produkční vybavení.
- Je riziko stále k dispozici? Ano. I v cloudu závisí závislost na jednom zařízení k vytvoření rizika. Existuje nižší pravděpodobnost, že by toto riziko mělo vliv na firmu, než se nacházelo v místním řešení, ale riziko ještě existuje.
- Přepište zásadu. V případě havárie v rámci datového centra musí existovat způsob obnovení produkčních systémů do 24 hodin výpadku v jiném datovém centru a v různých geografických umístěních.
- Projděte si týmy pro přijetí cloudu. V závislosti na implementovaném řešení existuje několik způsobů, jak řídit tyto zásady konzistence prostředků.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o zahrnutí klasifikace dat v strategii zásad správného řízení cloudu.

> [!div class="nextstepaction"]
> [Klasifikace dat](./what-is-data-classification.md)
