---
title: Rozhodnutí ovlivňující migraci
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Důležitá rozhodnutí týkající se procesu migrace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4bd04de2bd773e3fc02fbab5264ae60f275a8e7d
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564583"
---
# <a name="decisions-that-affect-migration"></a>Rozhodnutí ovlivňující migraci

V průběhu migrace ovlivňuje rozhodovací a realizační činnosti několik faktorů. Tento článek vysvětluje ústřední motiv těchto rozhodnutí a zkoumá několik otázek, které přetrvávají v diskusi o principech migrace v této části dokumentace Architektura přechodu na cloud.

## <a name="business-outcomes"></a>Obchodní výsledky

Účel nebo cíl jakéhokoli úsilí o přechod na cloud může mít významný vliv na navrhovaný přístup k realizaci.

- **Migrace.** Příkladem provozních výsledků jsou naléhavé obchodní faktory, rychlost přijetí nebo úspora nákladů. Tyto výsledky jsou středobodem úsilí, které vytěžuje obchodní hodnotu z přechodné změny v IT nebo provozních modelech. Část Migrace se v Architektuře přechodu na cloud zaměřuje především na obchodní výsledky související s migrací.
- **Inovace aplikací:** Příkladem přírůstkových výsledků je zlepšení zákaznického zážitku a rostoucí podíl na trhu. Tyto výsledky vyplývají ze sady postupných změn zaměřených na potřeby a přání aktuálních zákazníků.
- **Inovace řízené daty:** Nové produkty nebo služby, zejména ty, které využívají sílu dat, jsou příkladem rozvratných výsledků. Tyto výsledky jsou výsledkem experimentů a předpovědí, které používají data k rozvrácení současného stavu na trhu.

Žádná firma neusiluje jen o jeden z těchto výsledků. Bez provozu neexistují žádní zákazníci a naopak. Přechod na cloud se nijak neliší. Firmy se většinou snaží dosáhnout všech těchto výsledků, ale snaha soustředit se na všechny současně může vaše úsilí rozmělnit a zpomalit postup tam, kde by vaše firma měla největší prospěch.

Tento předpoklad neznamená, že byste si měli vybrat jeden z těchto tří cílů, ale spíše týmu cloudové strategie a týmu přechodu na cloud pomoci stanovit sadu provozních priorit, kterými se bude realizace řídit po další tři až šest měsíců. Tyto priority se stanovují určením pořadí každé z těchto tří možností od *nejvýznamnějších* po *nejméně významné*, protože souvisejí s úsilím, kterým tento tým může přispět v dalším jednom nebo dvou čtvrtletích.

### <a name="act-on-migration-outcomes"></a>Působit na výsledky migrace

Pokud jsou provozní výsledky na prvním místě seznamu, bude váš tým moci tuto část Architektury přechodu na cloud využít. V této části se předpokládá, že jako primární klíčové ukazatele výkonu (KPI) potřebujete upřednostnit rychlost a úspory nákladů. V takovém případě by model migrace pro přechod na cloud byl dobře sladěn s výsledky. Model zaměřený na migraci se silně vychází z migrace prostředků infrastruktury jako služby (IaaS) na přenesených a Shift, které umožňují vyčerpat datové centrum a snižovat náklady. V takovém modelu může dojít k modernizaci, jde ale o sekundární záměr, dokud nebude realizován primární úkol.

### <a name="act-on-application-innovations"></a>Působit na inovace aplikací

Pokud mezi vaše primární faktory patří podíl na trhu a zákaznický zážitek, nemusí být tato část Architektury přechodu na cloud tou nejlepší pro vedení snah vašeho týmu. Inovace aplikací vyžaduje plán, který se zaměřuje na modernizaci a přechod úloh bez ohledu na podkladovou infrastrukturu. V takovém případě mohou být pokyny v této části informativní, ale nemusí představovat nejlepší přístup k základním rozhodnutím.

### <a name="act-on-data-innovations"></a>Působit na inovace dat

Pokud jsou vaší prioritou na dalších zhruba šest měsíců data, experimenty, výzkum a vývoj nebo nové produkty, nemusí být tato část Architektury přechodu na cloud tou nejlepší pro vedení snah vašeho týmu. Při úsilí souvisejícím s inovací dat byste mohli využít pokyny týkající se migrace existujícího zdroje dat. Toto úsilí by se ale mělo více zaměřit na příchozí přenos dat a integraci dalších zdrojů dat. Rozšíření těchto pokynů o předpovědi a nové zkušenosti je mnohem důležitější než migrace prostředků IaaS.

## <a name="balance-the-portfolio"></a>Vyvážení portfolia

Tato část Architektury přechodu na cloud obsahuje teorii, která čtenářům pomůže porozumět různým přístupům k zavedení změny v rámci vyváženého portfolia. Článek o [vyvážení portfolia](../../expanded-scope/balance-the-portfolio.md) je jedním z příkladů rozšířeného rozsahu, jehož účelem je pomoci v činnostech souvisejících s touto teorií.

## <a name="effort"></a>Úsilí

Migrační úsilí se může značně lišit v závislosti na velikosti a složitosti zahrnutých úloh. Migrace menší úlohy obsahující několik stovek virtuálních počítačů je taktický proces, který lze implementovat pomocí automatizovaných nástrojů, jako je [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview). Naopak migrace velkého podniku s desítkami tisíc úloh vyžaduje vysoce strategický proces a může zahrnovat rozsáhlý refaktoring, opětovné sestavení a nahrazení stávajících aplikací s integrací funkcí PaaS (platforma jako služba) a SaaS (software jako služba). [Identifikace a vyvážení rozsahu](../../expanded-scope/balance-the-portfolio.md) plánovaných migrací je nezbytné.

Předtím, než učiníte rozhodnutí, která by mohla mít dlouhodobý vliv na aktuální program migrace, je nezbytné dojít ke shodě u následujících rozhodnutí.

### <a name="effort-type"></a>Typ úsilí

V jakékoli migraci významné škály (> 250 virtuálních počítačů) se assety migrují s využitím nejrůznějších možností přechodu, které jsou popsané v pěti RS odůvodnění: opětovné *hostování*, *refaktorování*, *rearchitekt*, *opětovné sestavení*a *nahrazení*.

Některé úlohy se modernizují prostřednictvím procesu *opětovného sestavení* nebo *změny architektury*, kdy vzniknou modernější aplikace s novými funkcemi a technickými možnostmi. Jiné prostředky procházejí procesem *refaktoringu*, kdy se například přesunou do kontejnerů nebo jiných modernějších hostingových a provozních metod, které nemusí nezbytně ovlivnit základ kódu daného řešení. Virtuální počítače a jiné prostředky, které jsou dobře zavedené, procházejí procesem *změny hostitele*, kdy se tyto prostředky přenesou z datacentra do cloudu. Některé úlohy by potenciálně bylo možné migrovat do cloudu, ale místo toho by měly být *nahrazeny* cloudovými službami typu SaaS, které splňují stejné potřeby, například pomocí Office 365 jako alternativy k migraci instancí Exchange Serveru.

Ve většině situací dojde k tomu, že nějaká obchodní událost způsobí dočasnou migraci velkého procenta prostředků pomocí procesu *změny hostitele*, následovanou významnějším sekundárním přechodem s využitím některé z ostatních migračních strategií. Tento proces se běžně označuje jako *přechod do cloudu*.

Během tohoto procesu [odůvodnění digitálních aktiv](../../../digital-estate/calculate.md) se u jednotlivých migrovaných prostředků učiní tyto typy rozhodnutí. V tomto okamžiku je ale potřeba udělat základní předpoklad. Která z těchto pěti migračních strategií nejlépe vyhovuje obchodním cílům nebo obchodním výsledkům, kvůli kterým se migrace provádí? Toto rozhodnutí slouží jako předpoklad, kterým se bude migrace řídit.

### <a name="effort-scale"></a>Rozsah úsilí

Měřítko migrace je dalším důležitým rozhodnutím. Proces potřebný k migraci 1 000 prostředků se liší od procesu potřebného k přesunutí 10 000 prostředků. Před zahájením migrace je důležité odpovědět na následující otázky:

- **Kolik prostředků v současnosti podporuje migraci úloh?** Prostředky se rozumí datové struktury, aplikace, virtuální počítače a nezbytná IT zařízení. Pro prvního kandidáta na migraci je doporučeno zvolit relativně malou úlohu.
- **Kolik z těchto prostředků plánujete migrovat?** Během procesu migrace je běžné určité procento prostředků ukončit z důvodu nedostatku dlouhodobé závislosti na koncových uživatelech.
- **Jaké jsou nejvyšší a nejnižší odhady měřítka migrovatelných prostředků?** U úloh, které jsou součástí migrace, odhadněte počet podpůrných prostředků, jako jsou aplikace, virtuální počítače, zdroje dat a IT zařízení. Pokyny k identifikaci relevantních prostředků najdete v části [digitální aktiva](../../../digital-estate/index.md) Architektury přechodu na cloud.

### <a name="effort-timing"></a>Načasování

Migrace jsou často způsobeny závažnou obchodní událostí, která je citlivá na čas. Jedním z běžných faktorů je například ukončení nebo obnovení smlouvy o hostování s třetí stranou. Ačkoli potenciálních obchodních událostí, které vyústí v migraci, existuje celá řada, mají jedno společné: koncové datum. Je důležité pochopit načasování všech takových obchodních událostí, aby bylo možné správně naplánovat a ověřit činnosti a rychlost.

## <a name="recap"></a>Rekapitulace

Než budete pokračovat, zdokumentujte následující předpoklady a nasdílejte je s týmem cloudové strategie a týmem přechodu na cloud:

- Obchodní výsledky
- Role. Bude zdokumentováno a upřesněno pro procesy migrace *Posouzení*, *Migrace*, *Optimalizace* a *Zabezpečení a správa*.
- Definice dokončení. Bude zdokumentováno a upřesněno samostatně pro procesy migrace *Posouzení*, *Migrace*, *Optimalizace* a *Zabezpečení a správa*.
- Typ úsilí
- Rozsah úsilí
- Načasování

## <a name="next-steps"></a>Další kroky

Po pochopení procesu mezi týmem je čas zkontrolovat technické požadavky. [Kontrolní seznam pro plánování migračního prostředí](./planning-checklist.md) pomáhá zajistit připravenost technické základny na migraci.

Jakmile se proces rozrozumí týmu, jeho čas na kontrolu technických požadavků v [kontrolní seznam pro plánování migrace] pomůže zajistit, aby byl technický základ připravený k migraci.

> [!div class="nextstepaction"]
> [Posouzení kontrolního seznamu pro plánování migrace](./planning-checklist.md)
