---
title: Co je účtování cloudu?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vysvětlení konceptu monitorování účtů cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 62eea92ae85faa396cc36e062735ab2ed182b012
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905744"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-accounting"></a>Co je účtování cloudu?

Cloud mění způsob, jakým IT účty vychází, jak je popsáno v [tématu vytváření finančních modelů pro cloudovou transformaci](financial-models.md). Různé modely účtů IT jsou pro podporu mnohem jednodušší, protože Cloud přiděluje náklady. Proto je důležité pochopit, jak se má účet pro cloudovou cenu začínat, než začnete s cestou k transformaci cloudu. Tento článek popisuje nejběžnější modely cloudového účetnictví.

## <a name="traditional-it-accounting-cost-center-model"></a>Tradiční IT účetnictví (model nákladového centra)

To je často přesné, aby se mu mohla považovat nákladové středisko. V tradičním modelu IT Accounting konsoliduje kupní sílu pro všechny prostředky IT. Jak jsme odkazovali na článek o [finančních modelech](financial-models.md) , může tato konsolidace napájení zahrnovat licence na software, opakované poplatky za licencování CRM, nákup stolních počítačů a další velké náklady.

Pokud to slouží jako nákladové středisko, vnímaná hodnota je z velké části zobrazená v rámci objektivu řízení zásobování. V tomto vnímání je obtížné, aby Rada nebo jiní pracovníci pochopili skutečnou hodnotu, kterou poskytuje. Náklady na nákup mají za následek, že se jejich zobrazení převažuje na základě většího množství jiné hodnoty přidané organizací. V tomto zobrazení se dozvíte, proč se často používá zodpovědnost za COO nebo oddělení. JEHO vnímání je omezené a může být krátké.

## <a name="central-it-accounting-profit-center-model"></a>Centrální účetní oddělení (model ziskového centra)

Pro účely překonání podrobného cenového centra si některé ředitelé informačních technologiíy vybírají pro centrální IT model účetnictví. V tomto typu modelu se chová jako konkurenční obchodní jednotka a partnerský podnik k výrobním jednotkám produkujícím výnosy. V některých případech může být tento model zcela logický. Některé organizace například mají profesionální oddělení IT Services, které generuje datový proud příjmů. Modely centrálních IT často negenerují významné tržby, takže je obtížné model zdůvodnit.

Bez ohledu na model příjmů jsou modely centrálního účetnictví IT jedinečné, protože se jedná o náklady na jednotkové účty. V tradičním IT modelu zaznamenává tým IT náklady a tyto náklady vyplatí ze sdílených prostředků, jako jsou operace a údržba (O & M) nebo vyhrazený zisk a ztráta (P & L) účtu.

V centrálním modelu IT tým vyznačuje služby poskytované k tomu, aby se zohlednila režie, Správa a další odhadované náklady. Pak účtuje konkurenční obchodní jednotky pro označené služby. V tomto modelu se očekává, že CIO spravuje P & L spojené s prodejem těchto služeb. To může vytvořit ploché IT náklady a kolize mezi ústředním IT a obchodními jednotkami, zejména v případě, že potřebuje snížit náklady nebo nesouhlasí s dohodnutým SLA. V době, kdy došlo ke změně technologie nebo trhu, by jakákoli nová technologie způsobila narušení centrálního vývoje P & L, což ztěžuje transformaci.

## <a name="chargeback"></a>Vratka

Jedním z běžných prvních kroků při změně reputace v podobě nákladového centra je implementace vrácení peněz modelu monitorování účtů. Tento model je zvlášť společný v menších podnicích nebo vysoce efektivních organizacích IT. V modelu vrácení peněz se všechny náklady na IT spojené s konkrétní obchodní jednotkou považují za provozní náklady v rozpočtu této obchodní jednotky. Tento postup snižuje celkové vlivy na něj, což umožňuje, aby se obchodní hodnoty zobrazovaly zřetelně.

V rámci starší verze místního modelu je vrácení peněz obtížné si uvědomit, protože stále musí přenášet velké náklady a odpisy. Pokračující převod z kapitálu na provozní náklady související s využitím je obtížné účetní cvičení. Tato obtíže je hlavním důvodem pro vytváření tradičních modelů IT a modelu centrálního účetnictví IT. Pokud chcete efektivně doručovat vrácení peněz model, je model provozních nákladů cloudového nákladového účetnictví skoro vyžadován.

Ale neměli byste tento model implementovat bez zvážení dopadu. Tady je několik důsledků, které jsou jedinečné pro vrácení peněz model:

- Vrácení peněz vede k obrovskému snížení celkového rozpočtu na IT. V případě organizací v oblasti IT, které jsou neefektivní nebo vyžadují rozsáhlé složité technické dovednosti v provozu nebo údržbě, může tento model tyto výdaje vystavit bezproblémový způsob.
- Ztráta řízení je běžná. V vysoce politických prostředích může vrácení peněz mít za následek ztrátu řízení a zaměstnanců, kteří se znovu přidělují podniku. To může způsobit významné neefektivity a snížit schopnost konzistentně splňovat požadavky SLA nebo projektu.
- Problémy se účetnictvím sdílených služeb je další běžná služba. Pokud se organizace rozrostla prostřednictvím získání a má v důsledku technického dluhu, je možné, že je potřeba udržovat vysoké procento sdílených služeb, aby všechny systémy byly efektivně spolupracovaly.

Cloudové transformace zahrnují řešení těchto a dalších následků přidružených k vrácení peněz modelu. Každé z těchto řešení však zahrnuje implementaci a provozní výdaje. CIO a ředitel by se před zvážením měli pečlivě zvážit pro odborníky a nevýhody modelu vrácení peněz.

## <a name="showback-or-awareness-back"></a>Showback nebo povědomí – zpátky

U větších podniků je model showback nebo se zpětným přechodem bezpečnější první krok v přechodu z nákladového střediska do centra hodnot. Tento model nemá vliv na finanční účetnictví. V podstatě & LS každé organizace se nemění. Největší posun je v místo a povědomí. V showback nebo v modelu zpětného zvyšování povědomí spravuje centralizovaný a konsolidovanou kupní sílu jako agenta pro firmu. V sestavách zpět na firmu si atributy přesměrují všechny přímé náklady na příslušnou organizační jednotku, což snižuje zjištěné rozpočty přímo využívané IT. Také plánuje rozpočty založené na potřebách přidružených obchodních jednotek, což jim umožňuje přesněji přihlédnout k nákladům spojeným s čistě IT iniciativami.

Tento model poskytuje rovnováhu mezi skutečným modelem vrácení peněz a různými tradičními modely IT oddělení.

## <a name="impact-of-cloud-accounting-models"></a>Dopad modelů monitorování účtů cloudu

Možnost výběru účetních modelů je zásadní pro návrh systému. Volba modelu monitorování účtů může ovlivnit strategie předplatného, standardy pojmenování, standardy označování a návrh zásad a podrobných plánů.

Po práci s firmou pro rozhodování o modelu cloudového účetnictví a [globálních trzích](global-markets.md)máte dostatek informací pro [vývoj platformy Azure Foundation](../ready/index.md).

> [!div class="nextstepaction"]
> [Vývoj pro Azure Foundation](../ready/index.md)
