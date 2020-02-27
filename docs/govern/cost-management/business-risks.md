---
title: Cost Management obchodních rizik
description: Seznamte se s ukázkami typických zákaznických přijetí Cost Management disciplíny v rámci strategie zásad správného řízení cloudu. 
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 544c425e94e9fa2cc4a687608f0dece80b3e9251
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707879"
---
# <a name="cost-management-motivations-and-business-risks"></a>Cost Management motivace a obchodních rizik

Tento článek popisuje důvody, proč zákazníci obvykle přijímají Cost Management disciplíny v rámci strategie zásad správného řízení cloudu. Poskytuje také několik příkladů obchodních rizik, které řídí příkazy zásad.

<!-- markdownlint-disable MD026 -->

## <a name="is-cost-management-relevant"></a>Je Cost Management relevantní?

V souvislosti se správou nákladů se při přijetí do cloudu vytvoří paradigmatový posun. Správa nákladů v tradičním místním světě je založená na aktualizačních cyklech, akvizicích Datacenter, obnoveních hostitelů a potížích s údržbou. Každý z těchto nákladů můžete vypovědět, naplánovat a zpřesnit s ročními rozpočty investičních výdajů.

V případě cloudových řešení mnoho organizací má za následek i další reaktivní přístup k Cost Management. V mnoha případech si firmy předkupují nebo potvrzují použití, což je nastavené množství cloudových služeb. Tento model předpokládá, že maximalizuje slevy na základě toho, kolik obchodních plánů na útratě s konkrétním dodavatelem cloudu vytváří vnímání proaktivního a plánovaného nákladového cyklu. Nicméně tato vnímání se stane realitou pouze v případě, že podnik také implementuje vyspělé Cost Management disciplíny.

Cloud nabízí funkce samoobslužné služby, které byly dřív nevyslechnuty v tradičních místních datových centrech. Tyto nové funkce umožňují firmám pružnější, méně omezující a další otevřené, aby bylo možné přijímat nové technologie. Nevýhodou samoobslužné služby je však, že koncoví uživatelé mohou nevědomě překročit přidělené rozpočty. Naopak stejné uživatele mohou mít změnu v plánech a neočekávaně nevyužívají množství předpokládaných cloudových služeb. Potenciál Shift v obou směrech opravňuje k investicím v Cost Managementm oboru v rámci týmu zásad správného řízení.

## <a name="business-risk"></a>Obchodní riziko

Cost Management disciplína se snaží řešit základní obchodní rizika související s výdaji při hostování cloudových úloh. Spolupracujte s vaší firmou a Identifikujte tato rizika a sledujte, co je pro vás důležité při plánování a implementaci cloudových nasazení.

Rizika se budou lišit mezi organizací, ale v následujících případech jsou k disdílným rizikům souvisejícím s náklady, které můžete použít jako výchozí bod pro diskuze v rámci týmu zásad správného řízení v cloudu:

- **Řízení rozpočtu:** Neřízení rozpočtu může vést k nadměrné útratě s dodavatelem cloudu.
- **Ztráta využití:** Předprodejní nebo předplacení, která se nepoužívá, může způsobit ztrátu investic.
- **Anomálie útraty:** Neočekávané špičky v obou směrech mohou být indikátory nesprávného použití.
- **Přebytek zajištěných prostředků:** Při nasazení prostředků v konfiguraci, která překračuje potřeby aplikace nebo virtuálního počítače, můžou vytvořit odpad.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat obchodní rizika, která by mohla být zavedena aktuálním plánem přijetí cloudu.

Po objasnění principu reálných obchodních rizik je dalším krokem dokument tolerance firmy pro rizika a indikátory a klíčové metriky pro monitorování této tolerance.

> [!div class="nextstepaction"]
> [Pochopení ukazatelů, metrik a tolerance rizik](./metrics-tolerance.md)
