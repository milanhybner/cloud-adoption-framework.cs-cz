---
title: Rozhodnutí, která ovlivňují migraci
description: Důležitá rozhodnutí týkající se procesu migrace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3281f7a14c5af58e435be9e3a412fc5285da1b47
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225473"
---
<!-- cSpell:ignore migrateable -->

# <a name="decisions-that-affect-migration"></a>Rozhodnutí, která ovlivňují migraci

V průběhu migrace ovlivňuje rozhodovací a realizační činnosti několik faktorů. Tento článek vysvětluje ústřední motiv těchto rozhodnutí a zkoumá několik otázek, které přetrvávají v diskusi o principech migrace v této části dokumentace Architektura přechodu na cloud.

## <a name="business-outcomes"></a>Obchodní výsledky

Účel nebo cíl jakéhokoli úsilí o přechod na cloud může mít významný vliv na navrhovaný přístup k realizaci.

- **Migrace.** Příkladem provozních výsledků jsou naléhavé obchodní faktory, rychlost přijetí nebo úspora nákladů. Tyto výsledky jsou středobodem úsilí, které vytěžuje obchodní hodnotu z přechodné změny v IT nebo provozních modelech. Část Migrace se v Architektuře přechodu na cloud zaměřuje především na obchodní výsledky související s migrací.
- **Inovace aplikací:** Příkladem přírůstkových výsledků je zlepšení zákaznického zážitku a rostoucí podíl na trhu. Tyto výsledky vyplývají ze sady postupných změn zaměřených na potřeby a přání aktuálních zákazníků.
- **Inovace řízené daty:** Mezi příklady rušivých výsledků patří nové produkty nebo služby, zejména ty, které pocházejí z výkonu dat. Tyto výsledky jsou výsledkem experimentů a předpovědí, které používají data k rozvrácení současného stavu na trhu.

Žádná firma neusiluje jen o jeden z těchto výsledků. Bez provozu neexistují žádní zákazníci a naopak. Přechod na cloud se nijak neliší. Firmy se většinou snaží dosáhnout všech těchto výsledků, ale snaha soustředit se na všechny současně může vaše úsilí rozmělnit a zpomalit postup tam, kde by vaše firma měla největší prospěch.

Tento předpoklad neznamená, že byste si měli vybrat jeden z těchto tří cílů, ale spíše týmu cloudové strategie a týmu přechodu na cloud pomoci stanovit sadu provozních priorit, kterými se bude realizace řídit po další tři až šest měsíců. Tyto priority se stanovují určením pořadí každé z těchto tří možností od *nejvýznamnějších* po *nejméně významné*, protože souvisejí s úsilím, kterým tento tým může přispět v dalším jednom nebo dvou čtvrtletích.

### <a name="act-on-migration-outcomes"></a>Působit na výsledky migrace

Pokud provozní výsledky v seznamu mají nejvyšší prioritu, Tato část rozhraní pro přijetí do cloudu bude dobře vyhovovat vašemu týmu. V této části se předpokládá, že jako primární klíčové ukazatele výkonu (KPI) potřebujete upřednostnit rychlost a úspory nákladů. V takovém případě by model migrace pro přechod na cloud byl dobře sladěn s výsledky. Model zaměřený na migraci se silně vychází z migrace prostředků infrastruktury jako služby (IaaS) na přenesených a Shift, které umožňují vyčerpat datové centrum a snižovat náklady. V takovém modelu může dojít k modernizaci, jde ale o sekundární záměr, dokud nebude realizován primární úkol.

### <a name="act-on-application-innovations"></a>Působit na inovace aplikací

Pokud jsou vaše primární ovladače tržní podíl a prostředí pro zákazníky, může se stát, že tato část nepředstavuje nejlepší část rozhraní pro přijetí do cloudu, která vás provede úsilím vašich týmů. Inovace aplikací vyžaduje plán, který se zaměřuje na modernizaci a přechod úloh bez ohledu na podkladovou infrastrukturu. V takovém případě mohou být pokyny v této části informativní, ale nemusí představovat nejlepší přístup k základním rozhodnutím.

### <a name="act-on-data-innovations"></a>Působit na inovace dat

Pokud jsou data, experimenty, výzkum a vývoj (R & D) nebo nové produkty vaší priority následujících šest měsíců, Tato část nemusí být nejlepší součástí architektury pro přijetí v cloudu, která by provedla úsilí vašich týmů. Při úsilí souvisejícím s inovací dat byste mohli využít pokyny týkající se migrace existujícího zdroje dat. Toto úsilí by se ale mělo více zaměřit na příchozí přenos dat a integraci dalších zdrojů dat. Rozšíření těchto pokynů o předpovědi a nové zkušenosti je mnohem důležitější než migrace prostředků IaaS.

## <a name="effort"></a>Úsilí

Migrační úsilí se může značně lišit v závislosti na velikosti a složitosti zahrnutých úloh. Migrace menší úlohy obsahující několik stovek virtuálních počítačů je taktický proces, který lze implementovat pomocí automatizovaných nástrojů, jako je [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview). Naopak migrace velkého podniku s desítkami tisíc úloh vyžaduje vysoce strategický proces a může zahrnovat rozsáhlý refaktoring, opětovné sestavení a nahrazení stávajících aplikací s integrací funkcí PaaS (platforma jako služba) a SaaS (software jako služba). [Identifikace a vyvážení rozsahu](../../../strategy/balance-the-portfolio.md) plánovaných migrací je nezbytné.

Předtím, než učiníte rozhodnutí, která by mohla mít dlouhodobý vliv na aktuální program migrace, je nezbytné dojít ke shodě u následujících rozhodnutí.

### <a name="effort-type"></a>Typ úsilí

V případě jakékoli migrace významné škály (více než 250 virtuálních počítačů) se assety migrují pomocí nejrůznějších možností přechodu, které jsou popsané v pěti RS odůvodnění: opětovné *hostování*, *refaktorování*, změna *architekt*, *opětovné sestavení*a *nahrazení*.

Některé úlohy se modernizují prostřednictvím procesu *opětovného sestavení* nebo *změny architektury*, kdy vzniknou modernější aplikace s novými funkcemi a technickými možnostmi. Jiné prostředky procházejí procesem *refaktoringu*, kdy se například přesunou do kontejnerů nebo jiných modernějších hostingových a provozních metod, které nemusí nezbytně ovlivnit základ kódu daného řešení. Virtuální počítače a další prostředky, které jsou lépe navázány, přecházejí prostřednictvím procesu opětovného *hostování* a převádějí tyto prostředky z datového centra do cloudu. Některé úlohy by mohly být migrovány do cloudu, ale je třeba je *nahradit* pomocí cloudových služeb založených na službě (SaaS), které splňují stejný podnikovou potřebu&mdash;například pomocí Office 365 jako alternativu k migraci instancí Exchange serveru.

Ve většině situací dojde k tomu, že nějaká obchodní událost způsobí dočasnou migraci velkého procenta prostředků pomocí procesu *změny hostitele*, následovanou významnějším sekundárním přechodem s využitím některé z ostatních migračních strategií. Tento proces se běžně označuje jako *přechod do cloudu*.

Během tohoto procesu [odůvodnění digitálních aktiv](../../../digital-estate/calculate.md) se u jednotlivých migrovaných prostředků učiní tyto typy rozhodnutí. V tomto okamžiku je ale potřeba udělat základní předpoklad. Která z těchto pěti migračních strategií nejlépe vyhovuje obchodním cílům nebo obchodním výsledkům, kvůli kterým se migrace provádí? Toto rozhodnutí slouží jako předpoklad, kterým se bude migrace řídit.

### <a name="effort-scale"></a>Rozsah úsilí

Měřítko migrace je dalším důležitým rozhodnutím. Procesy potřebné k migraci 1 000 prostředků se liší od procesů požadovaných k přesunutí prostředků 10 000. Před zahájením migrace je důležité odpovědět na následující otázky:

- **Kolik prostředků v současnosti podporuje migraci úloh?** Prostředky se rozumí datové struktury, aplikace, virtuální počítače a nezbytná IT zařízení. Pro prvního kandidáta na migraci je doporučeno zvolit relativně malou úlohu.
- **Kolik z těchto prostředků plánujete migrovat?** Během procesu migrace je běžné určité procento prostředků ukončit z důvodu nedostatku dlouhodobé závislosti na koncových uživatelech.
- **Jaké jsou hlavní odhady škály migrovaných prostředků, které lze migrovat?** U úloh, které jsou součástí migrace, odhadněte počet podpůrných prostředků, jako jsou aplikace, virtuální počítače, zdroje dat a IT zařízení. Pokyny k identifikaci relevantních prostředků najdete v části [digitální aktiva](../../../digital-estate/index.md) Architektury přechodu na cloud.

### <a name="effort-timing"></a>Načasování

Migrace jsou často způsobeny závažnou obchodní událostí, která je citlivá na čas. Jedním z běžných faktorů je například ukončení nebo obnovení smlouvy o hostování s třetí stranou. I když existuje mnoho potenciálních obchodních událostí vyžadujících migraci, sdílí společný faktor: koncové datum. Je důležité pochopit načasování všech takových obchodních událostí, aby bylo možné správně naplánovat a ověřit činnosti a rychlost.

## <a name="recap"></a>Rekapitulace

Než budete pokračovat, zdokumentujte následující předpoklady a nasdílejte je s týmem cloudové strategie a týmem přechodu na cloud:

- Obchodní výsledky
- Role, dokumentované a vylepšené pro *vyhodnocení*, *migraci*, *optimalizaci*a *zabezpečení a správu* procesů migrace.
- Definice hotových, dokumentovaných a rafinovaných samostatně pro účely *hodnocení*, *migrace*, *optimalizace*a *zabezpečení a správy* procesů migrace.
- Typ úsilí
- Rozsah úsilí
- Načasování

## <a name="next-steps"></a>Další kroky

Po pochopení procesu mezi týmem je čas zkontrolovat technické požadavky. [Kontrolní seznam pro plánování migračního prostředí](./planning-checklist.md) pomáhá zajistit připravenost technické základny na migraci.

Jakmile se proces rozrozumí týmu, jeho čas na kontrolu technických požadavků v [kontrolní seznam pro plánování migrace] pomůže zajistit, aby byl technický základ připravený k migraci.

> [!div class="nextstepaction"]
> [Posouzení kontrolního seznamu pro plánování migrace](./planning-checklist.md)
