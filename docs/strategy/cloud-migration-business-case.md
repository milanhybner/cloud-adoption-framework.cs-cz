---
title: Obchodní odůvodnění migrace cloudu
description: Pomocí architektury cloudového přijetí pro Azure se naučíte, jak začít vyvíjet obchodní odůvodnění pro migraci do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 28762d3540124b40bd3db4d7bd431033a1c25b5f
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337963"
---
# <a name="build-a-business-justification-for-cloud-migration"></a>Sestavení obchodního odůvodnění pro migraci do cloudu

Migrace do cloudu můžou vygenerovat včasnou návratnost investic z úsilí o transformaci cloudu (návratnost investic). Ale vývoj jasného obchodního odůvodnění s hmotnými, relevantními náklady a vrácení může být složitý proces. Tento článek vám pomůže se domnívat, jaká data potřebujete k vytvoření finančního modelu, který se zarovnává s výsledky migrace do cloudu. Nejdřív si Dispel pár mýty o migraci do cloudu, aby se vaše organizace mohla vyhnout nějakým běžným chybám.

## <a name="dispelling-cloud-migration-myths"></a>Mýty migrace do cloudu

**Mýtus: Cloud je vždycky levnější.** Často se předpokládá, že provozování Datacenter v cloudu je vždycky levnější než místní provoz. I když tento předpoklad může být obecně pravdivý, nejedná se vždy o případ. Někdy jsou cloudové provozní náklady vyšší. Tyto vyšší náklady jsou často způsobeny špatného řízení nákladů, nezarovnané systémové architektury, duplicity procesů, netypickými konfiguracemi systému nebo vyššími náklady na zaměstnance. Naštěstí můžete zmírnit mnohé z těchto problémů a vytvořit tak včasnou návratnost. Podle pokynů v tématu [sestavování obchodního odůvodnění](#build-the-business-justification) vám může pomoci detekovat a vyhnout se těmto chybovým zarovnáním. Přehláskování dalších mýty popsaných tady může také pomáhat.

**Mýtus: všechno by mělo přejít do cloudu.** Některé obchodní ovladače ve skutečnosti můžou vést k výběru hybridního řešení. Před dokončením obchodního modelu je inteligentní, aby se dokončila první naplněná kvantitativní analýza, jak je popsáno v [článcích o digitální nemovitosti](../digital-estate/5-rs-of-rationalization.md). Další informace o jednotlivých kvantitativních ovladačích, které jsou zapojeny do racionalizace, najdete v části [5 RS of racionalizace](../digital-estate/5-rs-of-rationalization.md). Buď přístup použijete k získání dat inventáře a krátké kvantitativní analýzy k identifikaci úloh nebo aplikací, které by mohly mít za následek vyšší náklady v cloudu. Tyto přístupy můžou také identifikovat závislosti nebo vzory provozu, které by vyžadovaly hybridní řešení.

**Mýtus: zrcadlení v místním prostředí vám pomůže ušetřit peníze v cloudu.** Během plánování digitálního majetku není nevyslechnuta společnost, aby zjistila nevyužitou kapacitu o více než 50% zřízeného prostředí. Pokud jsou assety zřízené v cloudu tak, aby odpovídaly aktuálnímu zřizování, nákladové úspory se těžko uvědomují. Zvažte zmenšení velikosti nasazených assetů, které se budou zarovnávat se vzorci použití namísto vzorů zřizování.

**Mýtus: Server vystavuje provozní případy migrace do cloudu.** Někdy je tento předpoklad pravdivý. U některých společností je důležité snížit průběžné kapitálové výdaje související se servery. Ale závisí na několika faktorech. Společnosti, které mají pět let na osm let cyklus aktualizace hardwaru, nejsou pravděpodobně schopné při migraci do cloudu zobrazovat rychlé návratnosti. Společnosti, které mají normalizované nebo vynucené aktualizační cykly, můžou rychle narazit ukazatel na hranice. V obou případech mohou být dalšími výdaji finanční triggery, které opravňují k migraci. Tady je několik příkladů nákladů, které se obvykle přehledají, když společnosti přebírají zobrazení nákladů jenom na serveru nebo pro virtuální počítače:

- Náklady na software pro virtualizaci, servery a middleware můžou být rozsáhlé. Poskytovatelé cloudu eliminují některé z těchto nákladů. Mezi dva příklady poskytovatele cloudu snižující náklady na virtualizaci patří [zvýhodněné hybridní využití Azure](https://azure.microsoft.com/pricing/hybrid-benefit/#services) a programy [rezervací v Azure](https://azure.microsoft.com/reservations) .
- Provozní ztráty způsobené výpadky můžou rychle překročit náklady na hardware a software. Pokud je vaše aktuální datacentrum nestabilní, pracujte s firmou a vyhodnotit dopad výpadků z hlediska nákladů na příležitosti nebo skutečných obchodních nákladů.
- Náklady na životní prostředí můžou být také významné. V případě střední řady American je doma největší investice a nejvyšší náklady rozpočtu. Totéž platí pro datová centra často. Náklady na vlastnictví, zařízení a pomůcky reprezentují spravedlivou část místních nákladů. Když se datová centra vyřadí, můžou se tato zařízení změnit na účel, nebo se vaše podnikání může z těchto nákladů potenciálně uvolnit.

**Mýtus: model s provozními náklady je lepší než model s kapitálovými náklady.** Jak je vysvětleno v článku o [fiskálních výsledcích](./business-outcomes/fiscal-outcomes.md) , může být dobrým modelem nákladů na operační systém. Ale některé obory zobrazují provozní výdaje negativně. Tady je několik příkladů, které aktivují užší integraci s účetními a obchodními jednotkami týkajícími se konverzace s provozními náklady:

- Když podnik uvidí kapitálové prostředky jako ovladač pro obchodní zhodnocení, snížení nákladů na velká písmena by mohla být negativním výsledkem. I když se nejedná o univerzální Standard, tento mínění se nejčastěji objevuje v maloobchodních, zpracovatelských a stavebních průmyslových odvětvích.
- V případě privátního jmění nebo společnosti, která žádá o kapitálový výstup, se zvyšuje provozní náklady v podobě negativního výsledku.
- Pokud se firmy zaměřuje na velmi lepší prodejní marže nebo snižuje náklady na prodané zboží, může být provozní výdaje negativním výsledkem.

U firmy je pravděpodobnější, že se provozní náklady budou lépe upřednostňovat než u velkých nákladů. Například tento přístup může být dobře přijatý společnostmi, které se snaží zlepšit peněžní toky, snižovat kapitálové investice nebo snižovat podíly na majetku.

Než zadáte obchodní odůvodnění, které se zaměřuje na převod z kapitálu na provozní náklady, pochopte, co je pro vaši firmu lepší. Monitorování účtů a nákupů často usnadňuje zarovnávání zpráv s finančními cíli.

**Mýtus: přechod na Cloud je podobný překlopení přepínače.** Migrace jsou ručně velmi náročné technické transformace. Při vývoji obchodního odůvodnění, zejména odůvodnění, která jsou citlivá na čas, vezměte v úvahu následující aspekty, které by mohly prodloužit dobu potřebnou k migraci prostředků:

- **Omezení šířky pásma:** Velikost pásma mezi aktuálním datacentrem a poskytovatelem cloudu bude během migrace řídit časové osy.
- **Testování časových OS:** Testování aplikací s firmou pro zajištění připravenosti a výkonu může být časově náročné. Zarovnávání uživatelů a testovacích procesů je velmi důležité.
- **Časové osy migrace:** Množství času a úsilí potřebného k implementaci migrace může zvýšit náklady a způsobit zpoždění. Přidělování zaměstnanců nebo smluvních partnerů může také proces zpozdit. Plán by měl pro tyto alokace počítat.

Technické a kulturní překážky mohou zpomalit přijetí v cloudu. V případě, že je čas důležitým aspektem obchodního odůvodnění, je nejlepší zmírňací vhodné plánování. Během plánování můžou dvě přístupy snížit rizika časové osy:

- Investovat čas a energii v oblasti porozumění technickým omezením přijetí. I když tlak pro rychlé přesuny může být vysoký, je důležité mít na zřeteli reálné časové osy.
- Pokud dojde k překážkám kulturního postavení nebo lidí, budou mít závažnější účinky než technická omezení. Přijetí do cloudu vytvoří změnu, která vytváří požadovanou transformaci. Lidé se někdy často změnili a můžou potřebovat další podporu pro zarovnávání s plánem. Identifikujte klíčové osoby v týmu, kteří se nemuseli měnit a zapojovat se do začátku.

Pokud chcete maximalizovat připravenost a zmírnit rizika s časovou osou, připravujte vedoucí pracovníky na základě pevně zarovnávání obchodních hodnot a obchodních výsledků. Pomůžou účastníkům pochopit změny, které se budou pocházet s transformací. Musí být jasné a nastavovat reálná očekávání od začátku. Když lidé nebo technologie zpomalí proces, bude snazší zařadit vedoucí podporu.

## <a name="build-the-business-justification"></a>Sestavení obchodního odůvodnění

Následující postup definuje přístup k vývoji obchodních odůvodnění pro migrace do cloudu. Další informace o výpočtech a finančních výrazech najdete v článku o [finančních modelech](./financial-models.md).

Na nejvyšší úrovni je vzorec pro obchodní odůvodnění jednoduchý. Ale drobné datové body, které jsou potřeba k naplnění vzorce, se dají obtížně zarovnat. Na základní úrovni se obchodní odůvodnění zaměřuje na návratnost investic (návratnost investic) spojených s navrhovanou technickou změnou. Obecný vzorec pro ni je:

![Návratnost investic se rovná (zisk z investice minus náklady na investici) dělený náklady na investici](../_images/strategy/formula-roi.png)

Tuto rovnici můžeme rozbalit a získat tak pohled na vzorce pro vstupní proměnné na pravé straně rovnice, které jsou specifické pro migraci. Zbývající části tohoto článku nabízejí několik důležitých informací, které je potřeba vzít v úvahu.

## <a name="migration-specific-initial-investment"></a>Počáteční investice specifické pro migraci

- Poskytovatelé cloudu jako Azure nabízejí kalkulačky k odhadu investic do cloudu. [Cenová Kalkulačka Azure](https://azure.microsoft.com/pricing) je jedním příkladem.
- Někteří poskytovatelé cloudu také poskytují cenové a rozdílové kalkulačky. [Kalkulačka celkové náklady na vlastnictví Azure](https://azure.com/tco) je jedním z příkladů.
- Pro přesnější cenové struktury Vezměte v úvahu [plánování digitálního majetku](../digital-estate/index.md) .
- Odhadnout náklady na migraci.
- Odhad nákladů na všechny očekávané příležitosti školení. [Microsoft Learn](https://docs.microsoft.com/learn) může být možné snížit náklady.
- V některých firmách může být potřeba zahrnout čas, který investovali stávající zaměstnanci, do počátečních nákladů. Pokyny pro finanční informace najdete v Office.
- Prodiskutujte jakékoli další náklady nebo náklady na režie s financemi k ověření.

## <a name="migration-specific-revenue-deltas"></a>Rozdíly v výnosech specifických pro migraci

Tento aspekt je často předaný vedoucímm vytvářením obchodního odůvodnění pro migraci. V některých oblastech může Cloud snížit náklady. Konečným cílem jakékoli transformace je ale poskytnout lepší výsledky v průběhu času. Vezměte v úvahu důsledky pro dlouhodobé tržby, které vám pochopí. Jaké nové technologie budou k dispozici pro vaši firmu po migraci, kterou už dnes nejde použít? Jaké projekty nebo obchodní cíle jsou v závislosti na starších technologiích blokované? Jaké programy jsou pozastavené, čekají na vysoce kapitálové výdaje na technologie?

Po zvážení příležitostí odemčených v cloudu Pracujte s firmou, abyste mohli vypočítat tržby, které by mohly přijít z těchto příležitostí.

## <a name="migration-specific-cost-deltas"></a>Cenové rozdíly specifické pro migraci

Vypočítá všechny změny nákladů, které budou pocházet z navrhované migrace. Podrobnosti o typech rozdílových nákladů najdete v článku o [finančních modelech](./financial-models.md) . Poskytovatelé cloudu často nabízejí nástroje pro výpočty s rozdílem mezi náklady. [Kalkulačka celkové náklady na vlastnictví Azure](https://azure.com/tco) je jedním z příkladů.

Další příklady nákladů, které mohou být omezeny migrací do cloudu:

- Ukončení nebo snížení datového centra (náklady na životní prostředí)
- Snížení spotřebované energie (náklady na životní prostředí)
- Ukončení racku (obnovení fyzického prostředku)
- Vyhnout se hardwarové aktualizaci (vyhýbá se nákladům)
- Vyhnout se prodloužení platnosti softwaru (snížení provozních nákladů nebo zamezení nákladů)
- Konsolidace dodavatele (snížení provozních nákladů a potenciální snížení nákladů na náklady)

## <a name="when-roi-results-are-surprising"></a>Když jsou výsledky NÁVRATNOSTi překvapivé

Pokud návratnost investic pro migraci do cloudu neodpovídá vašim očekáváním, možná budete chtít znovu navštívit společné mýty uvedené na začátku tohoto článku.

Je ale důležité si uvědomit, že úspora nákladů není vždycky možná. Některé aplikace jsou pro provoz v cloudu mnohem větší než v místním prostředí. Tyto aplikace můžou významně zkosit výsledky analýzy.

Pokud je návratnost investic nižší než 20%, berte v úvahu [plánování digitálního majetku](../digital-estate/index.md) a Zaměřte se na [racionalizaci](../digital-estate/rationalize.md)specifickou pozornost. Během kvantitativní analýzy zkontrolujte jednotlivé aplikace a najděte úlohy, které tyto výsledky zkosí. Může být vhodné odebrat tyto úlohy z plánu. Pokud jsou k dispozici data o využití, zvažte snížení velikosti virtuálních počítačů tak, aby odpovídaly využití.

Pokud je návratnost investic stále nezarovnané, obraťte se na svého obchodního zástupce Microsoftu nebo Zapojte [zkušeného partnera](https://azure.microsoft.com/migration/support).

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Vytvoření finančního modelu pro transformaci cloudu](./financial-models.md)
