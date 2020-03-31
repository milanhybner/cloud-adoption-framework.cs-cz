---
title: Provedení kontroly zásad cloudu
description: Naučte se, jak modernizovat stávající podnikové zásady IT, aby poskytovaly odpovídající úroveň řízení rizik pro cloudové prostředky.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3027b2195363499a2f3b383b8bb4f0eaf3b64da8
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430888"
---
<!-- markdownlint-disable MD026 -->

# <a name="conduct-a-cloud-policy-review"></a>Provedení kontroly zásad cloudu

Kontrola zásad cloudu je prvním krokem ke [správě splatnosti](../index.md) v cloudu. Cílem tohoto procesu je modernizovat stávající podnikové zásady IT. Po dokončení aktualizované zásady poskytují odpovídající úroveň řízení rizik pro cloudové prostředky. Tento článek popisuje proces kontroly zásad cloudu a jeho důležitost.

## <a name="why-perform-a-cloud-policy-review"></a>Proč provést kontrolu zásad cloudu?

Většina společností ji spravuje prostřednictvím provádění procesů, které se týkají zásad řízení. V malých firmách se tyto zásady můžou neoficiální a procesy budou volně definovány. Jelikož se podniky rozrůstou na velké podniky, zásady a procesy jsou v úmyslu jasně zdokumentováné a konzistentně spuštěné.

Vzhledem k tomu, že společnosti uzavřely podnikové zásady IT, mají závislosti na minulých technických rozhodnutích tendenci Seep se na řízení zásad. Například běžné informace o procesech zotavení po havárii zahrnují zásady, které zajišťují zálohování na pásku mimo lokalitu. Toto zahrnutí předpokládá závislost na jednom typu technologie (zálohy na pásce), které už nemusí být relevantní.

Cloudové transformace vytvářejí přirozený bod inflexe pro přehodnocování starších rozhodnutí o zásadách v minulosti. Technické možnosti a výchozí procesy se výrazně mění v cloudu, stejně jako tato zděděná rizika. Pomocí předchozího příkladu zásady zálohování na pásku vzniklé rizikem jediného bodu selhání tím, že zachovají data na jednom místě a podnik potřebuje minimalizovat rizikový profil tím, že toto riziko sníží. V nasazení v cloudu existuje několik možností, které dodávají stejné zmírnění rizik, a to s mnohem kratšími cíli pro dobu obnovení (RTO). Příklad:

- Řešení nativní pro Cloud by mohlo umožňovat geografickou replikaci Azure SQL Database.
- Hybridní řešení může použít Azure Site Recovery k replikaci úloh IaaS do Azure.

Při provádění transformace cloudu se často řídí mnoho nástrojů, služeb a procesů, které jsou k dispozici pro týmy pro přijetí v cloudu. Pokud jsou tyto zásady založené na starších technologiích, mohou bránit úsilí týmu o změnu. V nejhorším případě jsou důležité zásady zcela ignorovat z týmu migrace, aby bylo možné alternativní řešení. Ani to není přijatelný výsledek.

## <a name="the-cloud-policy-review-process"></a>Proces kontroly zásad cloudu

Kontroly zásad cloudu zarovnají stávající zásady správného řízení IT a zabezpečení IT s [pěti disciplínami zásad správného řízení cloudu](../index.md): [cost management](../cost-management/index.md), [směrného plánu zabezpečení](../security-baseline/index.md), [standardních hodnot identity](../identity-baseline/index.md), [konzistenci prostředků](../resource-consistency/index.md)a [akcelerace nasazení](../deployment-acceleration/index.md).

U každého z těchto oborů se v procesu kontroly postupuje takto:

1. Projděte si stávající místní zásady týkající se konkrétního oboru a vyhledejte dva klíčové datové body: starší závislosti a zjištěná obchodní rizika.
2. Vyhodnotit jednotlivá obchodní rizika tak, že požádáme o jednoduchou otázku: obchodní riziko ještě existuje v cloudovém modelu? "
3. Pokud riziko ještě existuje, přepište zásadu tím, že zadáte nezbytné omezení pro obchodování, nikoli technické řešení.
4. Projděte si aktualizované zásady s týmy pro přijetí cloudu, které vám pomohou porozumět potenciálním technickým řešením pro požadované zmírnění.

## <a name="example-of-a-policy-review-for-a-legacy-policy"></a>Příklad kontroly zásad pro starší zásady

Pokud chcete zadat příklad procesu, zkuste znovu použít zásady zálohování na pásku v předchozí části:

- Podnikové zásady připravují zálohy na pásku mimo provoz všech produkčních systémů. V této zásadě vidíte dva datové body, které vás zajímají:
  - Starší závislost na řešení zálohování na pásku
  - Předpokládané obchodní riziko spojené s úložištěm záloh ve stejném fyzickém umístění jako produkční vybavení.
- Je riziko stále k dispozici? Ano. I v cloudu závisí závislost na jednom zařízení k vytvoření rizika. Existuje nižší pravděpodobnost, že by toto riziko mělo vliv na firmu, než se nacházelo v místním řešení, ale riziko ještě existuje.
- Přepište zásadu. V případě havárie v rámci datového centra musí existovat způsob obnovení produkčních systémů do 24 hodin výpadku v jiném datovém centru a v různých geografických umístěních.
  - Je také důležité vzít v úvahu, že časová osa uvedená v předchozím požadavku mohla být nastavena technickými omezeními, která již nejsou v cloudu k dispozici. Před pouhým použitím starší verze RTO/RPO se ujistěte, že rozumíte technickým omezením a možnostem cloudu.
- Projděte si týmy pro přijetí cloudu. V závislosti na implementovaném řešení existuje několik způsobů, jak řídit tyto zásady konzistence prostředků.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o zahrnutí klasifikace dat v strategii zásad správného řízení cloudu.

> [!div class="nextstepaction"]
> [Klasifikace dat](./data-classification.md)
