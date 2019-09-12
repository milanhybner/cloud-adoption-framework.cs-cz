---
title: Motivace standardních hodnot identity a obchodní rizika
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Motivace standardních hodnot identity a obchodní rizika
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9c838063c77b02af4ec86187854a15d93b2998ef
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70827951"
---
# <a name="identity-baseline-motivations-and-business-risks"></a>Motivace standardních hodnot identity a obchodní rizika

Tento článek popisuje důvody, proč zákazníci obvykle přijímají pravidla směrného plánu identity v rámci strategie zásad správného řízení cloudu. Poskytuje také několik příkladů obchodních rizik, které řídí příkazy zásad.

<!-- markdownlint-disable MD026 -->

## <a name="is-identity-baseline-relevant"></a>Je základní hodnota identity relevantní?

Tradiční místní adresáře jsou navržené tak, aby podnikům umožnily přísně řídit oprávnění a zásady pro uživatele, skupiny a role v rámci svých interních sítí a datových center. To je obvykle určeno k podpoře implementace v jednom tenantovi a služeb, které platí pouze v místním prostředí.

Cloudové identity Services mají možnost rozšířit možnosti ověřování organizace a řízení přístupu na Internet. Podporují víceklientské prostředí a dají se použít ke správě uživatelů a zásad přístupu napříč cloudovým aplikacemi a nasazeními. Veřejné cloudové platformy mají určitou formu služeb cloudových nativních identit, které podporují úlohy správy a nasazení a umožňují [různé úrovně integrace](../../decision-guides/identity/index.md) s vašimi stávajícími místními řešeními identity. Všechny tyto funkce můžou mít za následek složitější zásady identity cloudu, než vaše tradiční místní řešení vyžadují.

Důležitost pravidla směrného plánu identity na nasazení v cloudu bude záviset na velikosti vašeho týmu a bude potřeba integrovat cloudové řešení identit do stávající místní služby identity. Počáteční testovací nasazení nemusí být v rámci organizace nebo správy uživatelů moc náročné, ale v případě, že vaše cloudové vlastnictví dojde k vyspělosti, budete pravděpodobně muset podporovat složitější integraci organizace a centralizovanou správu.

## <a name="business-risk"></a>Obchodní riziko

Obor směrného plánu identity se pokusí adresovat základní obchodní rizika související se službami identity a řízením přístupu. Spolupracujte s vaší firmou a Identifikujte tato rizika a sledujte, co je pro vás důležité při plánování a implementaci cloudových nasazení.

Rizika se budou lišit mezi organizací, ale v následujících případech slouží jako běžné rizika související s identitou, která můžete použít jako výchozí bod pro diskuze v rámci týmu zásad správného řízení v cloudu:

- **Neoprávněný přístup.** Citlivá data a prostředky, ke kterým můžou mít přístup neoprávnění uživatelé, můžou vést k úniku dat nebo přerušením služeb, které porušují hraniční obvodu vaší organizace a rizikové obchodní nebo zákonné závazky.
- **Neefektivita z důvodu více řešení identity** Organizace s více klienty služby identity můžou pro uživatele vyžadovat víc účtů. To může mít za následek neefektivitu pro uživatele, kteří si potřebují zapamatovat několik sad přihlašovacích údajů a pro ně při správě účtů napříč různými systémy. Pokud se přiřazení přístupu uživatele mezi řešeními identit neaktualizují, protože se mění zaměstnanci, týmy a obchodní cíle, můžou být vaše cloudové prostředky zranitelné vůči neoprávněnému přístupu nebo uživatelé nemůžou získat přístup k požadovaným prostředkům.
- **Neschopnost sdílet prostředky s externími partnery.** Problémy s přidáním externích obchodních partnerů k vašim stávajícím řešením identity můžou zabránit efektivnímu sdílení prostředků a obchodní komunikaci.
- **Místní závislosti identity.** V cloudu nemusí být k dispozici starší mechanismy ověřování nebo služba Multi-Factor Authentication jiného výrobce, aby se vyžadovalo jejich opětovné navýšení zátěže nebo další služby identit, které se mají nasadit do cloudu. Buď se může požadavek zpozdit, nebo zabránit v migraci a zvýšit náklady.

## <a name="next-steps"></a>Další postup

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat obchodní rizika, která by mohla být zavedena aktuálním plánem přijetí cloudu.

Jakmile bude navázáno porozumění reálným obchodním rizikům, je dalším krokem vytvoření dokumentu tolerance firmy pro rizika a indikátory a klíčové metriky pro monitorování této tolerance.

> [!div class="nextstepaction"]
> [Pochopení ukazatelů, metrik a tolerance rizik](./metrics-tolerance.md)
