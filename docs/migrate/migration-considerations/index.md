---
title: Model migrace architektury přechodu na cloud
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Model migrace architektury přechodu na cloud
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: acee0d171be547910a0fd7892c794400ae2ee101
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817294"
---
# <a name="cloud-adoption-framework-migration-model"></a>Model migrace architektury přechodu na cloud

Tato část architektury přechodu na cloud vysvětluje principy skryté za jejím modelem migrace. Kdykoli je to možné, v tomto obsahu se snažíme udržovat neutralitu vůči jednotlivým dodavatelům a provést vás procesy a aktivitami, které je možné využít pro migraci do jakéhokoli cloudu bez ohledu na zvoleného dodavatele.

## <a name="understand-migration-motivations"></a>Porozumění motivacím k migraci

Migrace do cloudu představuje snahu o správu portfolia chytře zamaskovanou za technickou implementaci. Během procesu migrace budete přijímat rozhodnutí nějaké prostředky přesunout, do jiných investovat a zastaralé nebo nepoužívané prostředky vyřadit z provozu. Některé prostředky se v rámci tohoto procesu optimalizují, refaktorují nebo zcela nahradí. Všechna tato rozhodnutí by měla být v souladu s vašimi motivacemi k migraci do cloudu. Ty nejúspěšnější migrace jdou ještě o krok dál a zajišťují soulad těchto rozhodnutí s požadovanými obchodními výsledky.

Předpokladem pro model migrace architektury přechodu na cloud je, aby vaše organizace dokončila proces zajištění obchodní připravenosti pro přechod na cloud. Před zahájením procesu migrace ve velkém měřítku si nezapomeňte přečíst pokyny k [plánování](../../business-strategy/index.md) a zajištění [připravenosti](../../ready/index.md) v architektuře přechodu na cloud a určete obchodní faktory nebo jiné odůvodnění migrace do cloudu a také případné požadavky na plánování nebo školení pro organizaci.

> [!NOTE]
> Přestože je obchodní plánování důležité, stejně důležité je i růstové myšlení. Souběžně s širším obchodním plánováním týmu cloudové strategie doporučujeme, aby tým přechodu na cloud zahájil migraci první úlohy, která bude sloužit jako prekurzor pro rozsáhlejší migrace. Tato počáteční migrace umožní týmu získat praktické zkušenosti s obchodními a technickými problémy spojenými s migrací.

## <a name="envision-an-end-state"></a>Vize koncového stavu

Před zahájením migrace je důležité udělat si hrubou představu požadovaného koncového stavu. Následující diagram ukazuje místní výchozí bod infrastruktury, aplikací a dat, který definuje vaše *digitální aktiva*. Během procesu migrace se tyto prostředky převedou s využitím jedné z pěti strategií migrace popsaných v tématu [5R racionalizace](../../digital-estate/5-rs-of-rationalization.md).

![Infografika možností migrace](../../_images/migration/migration-options.png)

Migrace a modernizace úloh sahají od jednoduchých migrací *změnou hostitele* (migrace metodou „lift and shift“) s využitím funkcí infrastruktury jako služby (IaaS), které nevyžadují změny kódu ani aplikací, přes *refaktorování* s minimálními změnami až po *změnu architektury*, při které se upraví a rozšíří kód a funkce aplikací tak, aby mohly využívat cloudové technologie.

V rámci strategií nativních pro cloud a zahrnujících platformu jako službu (PaaS) se místní úlohy *znovu sestaví* s využitím spravovaných služeb a nabídek platformy Azure. Úlohy, pro které existují ekvivalentní cloudové nabídky plně spravovaného softwaru jako služby (SaaS), je možné v rámci procesu migrace těmito službami zcela *nahradit*.

> [!NOTE]
> Ve verzi Public Preview architektury přechodu na cloud tato část architektury klade důraz na strategii migrace změnou hostitele. Přestože jsou jako alternativy ve vhodných případech zmíněná řešení PaaS a SaaS, migrace úloh virtuálních počítačů by se primárně měla provádět s využitím možností IaaS.
>
> Dalším přístupům se budou blíže věnovat jiné části a budoucí iterace tohoto obsahu. Základní informace o rozšíření rozsahu migrace o složitější strategie migrace najdete v článku věnovaném vyvážení portfolia.

## <a name="incremental-migration"></a>Přírůstková migrace

Model migrace architektury přechodu na cloud je založený na procesu inkrementální cloudové transformace. Předpokládá, že vaše organizace začne počáteční migrací do cloudu v omezeném rozsahu, kterou obecně označujeme jako první úlohu. S tím, jak vaše provozní týmy budou upřesňovat a zlepšovat procesy migrace, se tato činnost bude iterativně rozšiřovat o další úlohy.

Nástroje pro migraci do cloudu, jako je [Azure Site Recovery](/azure/site-recovery/site-recovery-overview), můžou migrovat celá datacentra s desítkami tisíc virtuálních počítačů. Firmy a stávající IT operace jsou však málokdy schopné toto tempo změn zvládnout. Řada organizací proto rozděluje migraci do několika iterací a v každé iteraci přesouvá jednu úlohu (nebo kolekci úloh).

Principy, na kterých stojí tento inkrementální model, vycházejí z provádění procesů a požadavků, na které odkazuje následující infografika.

![Model migrace architektury přechodu na cloud](../../_images/operational-transformation-migrate.png)

Konzistentní uplatňování těchto principů představuje konečný cíl procesů migrace do cloudu, a nemělo by se považovat za požadovaný výchozí bod. Pokyny v této části vám pomůžou definovat nejlepší procesy pro zajištění podpory potřeb vaší organizace s tím, jak se vaše migrace budou rozvíjet.

## <a name="next-steps"></a>Další kroky

Začněte se seznamovat s tímto modelem tím, že [prozkoumáte požadavky na migraci](./prerequisites/index.md).

> [!div class="nextstepaction"]
> [Požadavky na migraci](./prerequisites/index.md)