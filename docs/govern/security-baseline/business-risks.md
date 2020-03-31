---
title: Obchodní rizika standardních hodnot zabezpečení
description: Seznamte se s ukázkami typických zákaznických přijetí základu zabezpečení v rámci strategie zásad správného řízení v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 40b92c15af9ea4677d049cc76902d33e6807f139
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433629"
---
# <a name="security-baseline-motivations-and-business-risks"></a>Motivace standardních hodnot zabezpečení a obchodní rizika

Tento článek popisuje důvody, proč zákazníci obvykle přijímají pravidla standardních hodnot zabezpečení v rámci strategie zásad správného řízení cloudu. Poskytuje taky několik příkladů potenciálních obchodních rizik, která můžou řídit příkazy zásad.

<!-- markdownlint-disable MD026 -->

## <a name="security-baseline-relevancy"></a>Relevanci standardních hodnot zabezpečení

Zabezpečení je klíčovým problémem pro jakékoli IT organizace. Cloudová nasazení čelí mnoha stejným bezpečnostním rizikům jako úlohy hostované v tradičních místních datových centrech. Nicméně povaha veřejných cloudových platforem s nedostatečným přímým vlastnictvím fyzického hardwaru, který ukládá a spouští vaše zatížení, znamená, že cloudové zabezpečení vyžaduje vlastní zásady a procesy.

Jednou z primárních věcí, které nastavují zásady správného řízení zabezpečení cloudu, je snadné, které prostředky se dají vytvořit, případně přidání ohrožení zabezpečení, pokud se před nasazením nebere v úvahu zabezpečení. Flexibilita, kterou technologie jako [software definované sítě (SDN)](../../decision-guides/software-defined-network/index.md) poskytují rychlé změny síťové topologie založené na cloudu, může také snadno upravit celkové prostředí pro útok na síť v neočekávaných způsobech. Cloudové platformy také poskytují nástroje a funkce, které mohou zlepšit možnosti zabezpečení v případě, že jsou v místním prostředí vždy možné.

Velikost, kterou investujete do zásad zabezpečení a procesů, bude záviset na povaze nasazení v cloudu. Nasazení počátečních testů může vyžadovat jenom většinu základních zásad zabezpečení, zatímco klíčové úlohy budou řešit složité a rozsáhlé požadavky na zabezpečení. Všechna nasazení budou muset začít s oborem na nějaké úrovni.

Základ směrného plánu zabezpečení pokrývá podnikové zásady a ruční procesy, které můžete zavést k ochraně vašeho cloudového nasazení proti bezpečnostním rizikům.

> [!NOTE]
>I když je důležité pochopit [identitu identity](../identity-baseline/index.md) v kontextu standardních hodnot zabezpečení a jak se to týká Access Control, [pět oborů zásad správného řízení cloudu](../index.md) volá jako svůj vlastní obor [standardní](../identity-baseline/index.md) obory, oddělené od standardních hodnot zabezpečení.

## <a name="business-risk"></a>Obchodní riziko

Disciplína standardních hodnot zabezpečení se pokouší řešit základní obchodní rizika související se zabezpečením. Spolupracujte s vaší firmou a Identifikujte tato rizika a sledujte, co je pro vás důležité při plánování a implementaci cloudových nasazení.

Rizika se budou lišit mezi organizací, ale v následujícím seznamu jsou běžné bezpečnostní rizika, která můžete použít jako výchozí bod pro diskuze v rámci týmu zásad správného řízení v cloudu:

- **Porušení dat:** Neúmyslná expozice nebo ztráta citlivých dat hostovaných v cloudu může vést ke ztrátě zákazníků, smluvním problémům nebo právním důsledkům.
- **Přerušení služby:** Výpadky a další problémy s výkonem kvůli nezabezpečené infrastruktuře přerušují normální provoz a můžou způsobit ztrátu produktivity nebo ztráty podniku.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat obchodní rizika, která by mohla být zavedena aktuálním plánem přijetí cloudu.

Jakmile bude navázáno porozumění reálným obchodním rizikům, je dalším krokem vytvoření dokumentu tolerance firmy pro rizika a indikátory a klíčové metriky pro monitorování této tolerance.

> [!div class="nextstepaction"]
> [Pochopení ukazatelů, metrik a tolerance rizik](./metrics-tolerance.md)
