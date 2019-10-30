---
title: Průvodce rozhodováním ohledně nástrojů pro migraci
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Průvodce rozhodováním ohledně nástrojů pro migraci
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.openlocfilehash: cdfa8ffe64ac7af6d545f9706f8f0652a4d583c4
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/29/2019
ms.locfileid: "73047723"
---
# <a name="migration-tools-decision-guide"></a>Průvodce rozhodováním ohledně nástrojů pro migraci

Strategie a nástroje, které použijete k migraci aplikace do Azure, budou do značné míry záviset na vašich obchodních motivacích, technologických strategiích, časových osách a také na hlubokém porozumění vlastním migrovaným úlohám a prostředkům (infrastruktura, aplikace a data). Následující rozhodovací strom slouží jako základní vodítko při výběru nejlepších nástrojů k použití v závislosti na rozhodnutích ohledně migrace. Považujte tento rozhodovací strom za výchozí bod.

Výběr migrace s využitím technologií PaaS (platforma jako služba) nebo IaaS (infrastruktura jako služba) vychází z rovnováhy mezi náklady, časovými nároky, stávajícím technickým dluhem a dlouhodobou návratností. Model IaaS často představuje nejrychlejší cestu ke cloudu, protože vyžaduje nejméně změn úloh. Model PaaS může vyžadovat úpravy datových struktur nebo zdrojového kódu, ale dosahuje výrazné dlouhodobé návratnosti v podobě nižších provozních nákladů a větší technické flexibility. V následujícím diagramu termín _modernizace_ odráží rozhodnutí během migrace modernizovat prostředek a modernizovaný prostředek migrovat na platformu PaaS.

![Příklad rozhodovacího stromu pro výběr nástrojů pro migraci.](../../_images/migrate/migration-tools-decision-tree.png)

## <a name="key-questions"></a>Klíčové otázky

Zodpovězení následujících otázek vám pomůže při rozhodování na základě výše uvedeného stromu.

- **Ukázala by se modernizace aplikační platformy během migrace jako moudrá investice času, energie a rozpočtu?** Technologie PaaS, jako jsou služby Azure App Service nebo Azure Functions, můžou zvýšit flexibilitu nasazení a snížit jeho složitost tím, že spravují virtuální počítače pro hostování aplikací. Aby však aplikace mohly využívat tyto funkce nativní pro cloud, můžou vyžadovat refaktorování, což může celou migraci výrazně prodloužit a prodražit. Pokud se vaše aplikace může s minimálními úpravami migrovat na technologie PaaS, pravděpodobně se jedné o vhodného kandidáta na modernizaci. Kdyby to vyžadovalo rozsáhlé refaktorování, může být lepší volbou migrace s využitím virtuálních počítačů založených na modelu IaaS.
- **Ukázala by se modernizace datové platformy během migrace jako moudrá investice času, energie a rozpočtu?** Stejně jako v případě migrace aplikací nabízejí varianty spravovaného úložiště Azure PaaS, jako jsou služby Azure SQL Database, Cosmos DB a Azure Storage, výrazné výhody v oblasti správy a flexibility, ale migrace těchto služeb může vyžadovat refaktorování stávajících dat a aplikací využívajících tato data. Datové platformy často vyžadují výrazně méně refaktorování než aplikační platformy. Proto se datová platforma velmi často modernizuje i přesto, že aplikační platforma zůstane stejná. Pokud se vaše data můžou s minimálními změnami migrovat do spravované datové služby, jsou vhodnými kandidáty na modernizaci. Data, jejichž refaktorování kvůli možnosti využít tyto služby PaaS by bylo časově nebo finančně náročné, může být lepší migrovat s využitím virtuálních počítačů založených na modelu IaaS, aby lépe vyhovovala stávajícím možnostem hostování.
- **Běží vaše aplikace v současné době na vyhrazených virtuálních počítačích nebo sdílí hosting s jinými aplikacemi?** Aplikace běžící na vyhrazených virtuálních počítačích je snadnější migrovat na varianty hostingu PaaS než aplikace běžící na sdílených serverech.
- **Překročí migrace vašich dat šířku pásma vaší sítě?** Kapacita sítě mezi místními zdroji dat a Azure může představovat kritický bod migrace dat. Pokud data, která potřebujete přenést, čelí omezením šířky pásma, která brání efektivní nebo včasné migraci, pravděpodobně budete muset prozkoumat alternativní mechanismy přenosu nebo mechanismy offline přenosu. [Článek o replikaci migrace](../../migrate/migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) v architektuře přechodu na cloud popisuje, jakým způsobem můžou omezení replikace ovlivnit migraci. V rámci posuzování migrace se spojte se svými IT týmy a ověřte, že šířka pásma místní sítě nebo sítě WAN dokáže zvládnout vaše požadavky na migraci. Projděte si také [rozšířený scénář migrace pro případ, kdy požadavky na úložiště během migrace překračují kapacitu sítě](../../migrate/expanded-scope/network-capacity-exceeded.md#suggested-prerequisites).
- **Využívá vaše aplikace stávající kanál DevOps?** Azure Pipelines je v řadě případů možné snadno refaktorovat a umožnit nasazení aplikací do cloudových hostitelských prostředí.
- **Mají vaše data složité požadavky na úložiště?** Produkční aplikace většinou vyžadují úložiště dat, které je vysoce dostupné a nabízí funkci AlwaysOn a podobné funkce pro zajištění dostupnosti a kontinuity služeb. Všechny varianty spravované databáze založené na modelu Azure PaaS, jako jsou služby Azure SQL Database, Azure Database for MySQL nebo Azure Cosmos DB, nabízejí smlouvy o úrovni služeb zajišťující 99,99% dostupnost. Naopak SQL Server založený na modelu IaaS na virtuálních počítačích Azure nabízí smlouvy o úrovni služeb zajišťující 99,95% dostupnost pro jednu instanci. Pokud vaše data není možné modernizovat pro varianty úložiště PaaS, zajištění vyšší dostupnosti IaaS bude zahrnovat složitější scénáře ukládání dat, například provoz clusterů SQL Serveru s technologií AlwaysOn a průběžnou synchronizaci dat mezi jednotlivými instancemi. To může zahrnovat výrazné náklady na hostování a údržbu. Proto je při zvažování možností migrace dat důležité najít rovnováhu mezi požadavky na dostupnost, obtížností modernizace a celkovým vlivem na rozpočet.

## <a name="innovation-and-migration"></a>Inovace a migrace

V souladu s důrazem, který architektura přechodu na cloud klade na [přírůstkovou migraci](../../migrate/index.md#migration-implementation), prvotní rozhodnutí ohledně strategie migrace a nástrojů nevylučuje možnost budoucích inovací a aktualizace aplikací tak, aby mohly využít příležitosti, které jim nabízí platforma Azure. Přestože se počáteční migrace může zaměřovat primárně na změnu hostitele s využitím přístupu IaaS, měli byste si naplánovat pravidelné kontroly vašeho portfolia aplikací hostovaných v cloudu, abyste mohli prozkoumat příležitosti k optimalizaci.

## <a name="learn-more"></a>Další informace

- **[Základy práce s cloudy: Přehled možností výpočetního prostředí Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview).** Tento článek obsahuje informace o funkcích ve variantách výpočetního prostředí Azure IaaS a PaaS.
- **[Základy práce s cloudy: Volba správného úložiště dat](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview).** Tento článek popisuje dostupné možnosti úložiště PaaS na platformě Azure.
- **[Migrace s rozšířeným rozsahem: Požadavky na úložiště při migraci překračují kapacitu sítě](../../migrate/expanded-scope/network-capacity-exceeded.md).** Tento článek popisuje alternativní mechanismy migrace dat pro scénáře, kdy migraci dat brání dostupná šířka pásma sítě.
- **[SQL Database: Výběr správné varianty SQL Serveru v Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#business-motivations-for-choosing-databases-managed-instances-or-sql-virtual-machines).** Tento článek obsahuje popis možností a obchodních odůvodnění pro rozhodnutí hostovat úlohy SQL Serveru v prostředí hostované infrastruktury (IaaS) nebo hostované služby (PaaS).
