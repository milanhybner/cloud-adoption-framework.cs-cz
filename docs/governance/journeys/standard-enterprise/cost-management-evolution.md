---
title: 'Standardní podniková příručka: Zlepšení Cost Management disciplíny'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Standardní podniková příručka: Zlepšení Cost Management disciplíny'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 078d484becaf62cd07ec124d818891c8a52b8dbc
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908797"
---
# <a name="standard-enterprise-guide-improve-the-cost-management-discipline"></a>Standardní podniková příručka: Zlepšení Cost Management disciplíny

Tento článek popisuje mluvený komentář přidáním řízení nákladů do MVP pro kontrolu zásad správného řízení.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Přijetí dosáhlo nad ukazatelem tolerance nákladů, který je definovaný v MVP pro kontrolu zásad správného řízení. To je dobré, protože odpovídá migraci z datacentra "DR". Zvýšení útraty nyní odůvodňuje investování času z týmu zásad správného řízení cloudu.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

V předchozí fázi tohoto mluveného komentáře bylo vyřazení 100% datacentra DR. Vývoj aplikací a týmy BI byly připravené na provozní provoz.

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- Tým migrace začal migrovat virtuální počítače z provozního centra.
- Vývojové týmy pro aplikace aktivně přenáší produkční aplikace do cloudu prostřednictvím kanálů CI/CD. Tyto aplikace se můžou reaktivním škálováním požadavků uživatelů.
- Tým business intelligence v rámci něho dodal několik nástrojů prediktivní analýzy v cloudu. Objemy dat agregovaných v cloudu se i nadále rozšiřují.
- Veškerý tento nárůst podporuje potvrzené obchodní výsledky. Náklady však začaly Mushroom. Předpokládané rozpočty rostou rychleji, než se očekávalo. Finanční ředitel potřebuje vylepšené přístupy ke správě nákladů.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Monitorování nákladů a vytváření sestav je třeba přidat do cloudového řešení. Stále slouží jako nákladově clearingová dům. To znamená, že platba za cloudové služby bude i nadále pocházet z nákupu IT. Vytváření sestav by ale mělo spojovat s přímými provozními náklady na funkce, které spotřebovávají náklady na Cloud. Tento model se označuje jako model cloudového účetnictví "Zobrazit zpátky".

Změny aktuálního a budoucího stavu zveřejňují nová rizika, která budou vyžadovat nové příkazy zásad.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Řízení rozpočtu:** Existuje riziko, že funkce samoobslužné služby budou mít za následek nadměrné a neočekávané náklady na novou platformu. Procesy zásad správného řízení pro monitorování nákladů a zmírnění probíhajících nákladů na zpracování musí být zavedeny, aby se zajistilo pokračující sblížení s plánovaným rozpočtem.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

- Skutečné náklady mohou překročit plán.
- Obchodní podmínky se změní. V takovém případě budou existovat případy, kdy obchodní funkce potřebuje spotřebovat více cloudových služeb, než se očekávalo, což vede k nepravidelnosti útraty. Existuje riziko, že tato dodatečná útrata bude považována za nadlimitní využití, a to na rozdíl od nezbytného nastavení plánu.
- Systémy by mohly být nadměrné zřízení, což vede k překročení útraty.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky.

- Všechny náklady na Cloud by měly být sledovány týmem zásad správného plánu každý týden. Vykazování odchylek mezi náklady na Cloud a plánem se sdílí s vedením IT a finančními službami měsíčně. Všechny náklady na Cloud a plán aktualizací by se měly kontrolovat s využitím IT a finančních prostředků měsíčně.
- Všechny náklady musí být přiděleny obchodní funkci pro účely zodpovědnosti.
- Cloudové prostředky by se měly průběžně monitorovat podle možností optimalizace.
- Nástroje pro řízení cloudu musí omezit možnosti změny velikosti Assetu na schválený seznam konfigurací. Nástroj musí zajistit, aby všechny prostředky byly zjistitelné a sledované řešením pro monitorování nákladů.
- Během plánování nasazení by se měly zdokumentovat všechny požadované cloudové prostředky spojené s hostováním produkčních úloh. Tato dokumentace vám pomůže Upřesnit rozpočty a připravit další automatizaci, aby nedocházelo k používání dražších možností. Během tohoto procesu by se mělo předávat různým nástrojům diskontování nabízeným poskytovatelem cloudu, jako jsou rezervované instance nebo snížení nákladů na licence.
- Všichni vlastníci aplikací se budou muset zúčastnit školení o postupech pro optimalizaci úloh, aby lépe ovládají náklady na Cloud.

## <a name="incremental-improvement-of-the-best-practices"></a>Přírůstkové zlepšení osvědčených postupů

V této části článku se změní návrh MVP zásad správného řízení tak, aby zahrnoval nové zásady Azure a implementaci Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

1. Implementujte Azure Cost Management.
    1. Navažte správný rozsah přístupu, který se zarovnává se vzorem předplatného a oborem konzistence prostředků. Za předpokladu, že se přizpůsobuje přizpůsobení MVP MVP definovaného v předchozích článcích, vyžaduje přístup k **oboru účtu registrace** pro tým zásad správného řízení cloudu, který běží na vytváření sestav vysoké úrovně. Další týmy mimo řízení přístupu můžou vyžadovat přístup k **oboru skupiny prostředků** .
    1. Vytvořte rozpočet v Azure Cost Management.
    1. Projděte si úvodní doporučení a vyjednání s nimi. Pro podporu vytváření sestav můžete mít opakovaný proces.
    1. Nakonfigurujte a spusťte vytváření sestav Azure Cost Management, jak počáteční, tak i opakovaný.
2. Aktualizovat Azure Policy
    1. Chcete-li identifikovat jakoukoli odchylku, proveďte auditování hodnot označování, skupiny pro správu, předplatného a skupiny prostředků.
    1. Vytvořte možnosti velikosti SKU pro omezení nasazení na SKU uvedené v dokumentaci plánování nasazení.

## <a name="conclusion"></a>Závěr

Přidání těchto procesů a změn do procesu MVP pro řízení systému vám pomůže napravit mnoho rizik spojených se správou nákladů. Dohromady vytvářejí viditelnost, zodpovědnost a optimalizaci potřebné k řízení nákladů.

## <a name="next-steps"></a>Další postup

V případě, že se přijetí do cloudu pokračuje a přináší další obchodní hodnotu, rizika a potřeby zásad správného řízení cloudu se změní také. Pro fiktivní společnost v tomto průvodci je dalším krokem použití této investice do zásad správného řízení pro správu více cloudů.

> [!div class="nextstepaction"]
> [Vývoj pro více cloudů](./multicloud-evolution.md)
