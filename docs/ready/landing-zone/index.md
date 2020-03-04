---
title: Co je cílová zóna
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zjistěte, jakým způsobem cílové zóny poskytují základní stavební bloky libovolného prostředí přechodu na cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6db16b50115f2ba145dd4980dc5d57867f438de7
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228355"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-a-landing-zone"></a>Co je cílová zóna?

Infrastruktura jako kód představuje přirozený přechod během většiny snah o přechod na cloud. Nasazení prvních cílových zón v cloudu je obvyklým výchozím bodem pro přechod k vytváření prostředí založených na kódu. Tento článek vám pomůže pochopit pojem _cílová zóna_ a další související termíny.

## <a name="landing-zone-definition"></a>Definice cílové zóny

Cílové zóny jsou základní stavební bloky libovolného prostředí přechodu na cloud. Termín _cílová zóna_ označuje logickou konstrukci, která zachycuje všechno, co je potřeba splnit pro zajištění požadovaného přechodu na cloud.

**Rozsah:** Plně funkční cílová zóna bere v úvahu všechny prostředky platforem, které jsou potřeba k podpoře potřeb přechodu příslušného zákazníka.

**Refaktoring:** Plně funkční cílová zóna je finálním produktem všech iterací metodiky připravenosti architektury přechodu na cloud. V průběhu každé iterace se základ kódu, který definuje příslušnou cílovou zónu, refaktoruje nebo rozšíří. Po dokončení refaktoringu je možné cílovou zónu upravit nebo znovu nasadit, aby se zajistily nové požadavky přechodu na cloud.

**Cíl:** Cílem cílových zón je vytvořit společnou sadu konzistentních implementací platforem. Zavedením těchto konzistentních implementací se zajistí, že aplikace budou mít při nasazení přístup k požadovaným komponentám. Každá iterace cílové zóny musí být následně navržena a nasazena v souladu s požadavky plánu přechodu na cloud a strategií návrhu předplatného.

**Základní účel:** Základním účelem cílové zóny je zajistit, aby při přesunu aplikace do Azure už k byla dispozici požadovaná „vnitřní kabeláž“.

## <a name="landing-zone-usage"></a>Využití cílové zóny

Cílové zóny nemusí nutně rozlišovat mezi přechodem na IaaS nebo PaaS. Cílové zóny ale plní konkrétní účel, kterým je podpora plánu přechodu realizací strategie předplatného. Podpora plánu přechodu může vyžadovat několik cílových zón a kombinaci požadovaných komponent.

Účel a rozsah celkového plánu přechodu na cloud definuje, jaká „vnitřní kabeláž“ je potřeba. Výchozí rozsah cílové zóny se pravděpodobně rozšíří o požadavky zásad správného řízen, dodržování předpisů, zabezpečení a provozní správy. Během počátečních fází přechodu mohou cílové zóny zahrnovat méně „vnitřní kabeláže“, a to v důsledku definovaných požadavků a přijatelných rizik.  Pokud existuje několik cílových zón, je velmi běžné, že každá cílová zóna bude závislá na centrech, která poskytují požadované ovládací prvky prostřednictvím modelu sdílených služeb.

## <a name="related-terms"></a>Související termíny

- **Sdílené služby:** Úlohy často mají sdílené závislosti, které používá řada různých úloh. Přístup zaměřený na sdílené služby přesouvá řadu těchto společných závislostí do jedné logické konstrukce.

- **Model hvězdicové architektury:** Jednou z implementací přístupu zaměřeného na sdílené služby je model hvězdicové architektury. V tomto modelu je centrum jedinou logickou konstrukcí pro hostování všech sdílených služeb. Cílové zóny potom na základě společných závislostí působí jako paprsky vycházející z tohoto centra.

- **Nezávislá cílová zóna:** Některé přístupy k cílovým zónám konkrétně nevyžadují vyhrazené centrum. Setkáte se s tím nejčastěji v případě, kdy se všechna produkční aktiva (aplikace, data a virtuální počítače) v rámci plánu přechodu na cloud dají bezpečně hostovat, spravovat a řídit v jednom prostředí.

## <a name="next-steps"></a>Další kroky

Pokud chcete začít používat cílové zóny, [vyberte si vaši první cílovou zónu](./first-landing-zone.md)zóny.

> [!div class="nextstepaction"]
> [Volba první cílové zóny](./first-landing-zone.md)
