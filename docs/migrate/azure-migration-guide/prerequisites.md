---
title: Požadavky na migraci do Azure
description: Pomocí architektury přechodu na cloud pro Azure se dozvíte, jak připravit migraci Azure a jaké požadavky potřebujete pro úspěšný projekt migrace.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 777b68bcd7faa613681f2d9ebbdf6cffe4accc3f
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094804"
---
::: zone target="chromeless"

# <a name="prerequisites"></a>Požadavky

::: zone-end

::: zone target="docs"

# <a name="prerequisites-for-migrating-to-azure"></a>Požadavky na migraci do Azure

::: zone-end

Prostředky v této části vám pomohou připravit vaše aktuální prostředí na migraci do Azure.

# <a name="overview"></a>[Přehled](#tab/Overview)

Mezi důvody migrace do Azure patří eliminace rizik spojených se starším hardwarem, snížení investičních nákladů, uvolnění prostoru v datovém centru a rychlá návratnost investic.

- **Eliminace staršího hardwaru.** Je možné, že jsou vaše aplikace hostované na infrastruktuře, která se blíží konci životnosti nebo podpory, ať už se jedná o místní infrastrukturu nebo poskytovatele hostingu. Migrace do cloudu představuje atraktivní řešení, protože díky možnosti migrace „beze změn“ může tým rychle vyřešit aktuální problém se životním cyklem infrastruktury a následně svou pozornost zaměřit na dlouhodobé plánování životního cyklu aplikací a jejich optimalizace v cloudu.
- **Řešení ukončení podpory softwaru.** Možná máte aplikace, které závisí na jiném softwaru nebo operačních systémech, jejichž podpora brzy skončí. S přechodem na Azure můžete pro tyto závislosti získat rozšířené možnosti podpory (případně další možnosti migrace, které minimalizují požadavky na refaktoring), aby mohly vaše aplikace fungovat i nadále. Podívejte se například na [rozšířené možnosti podpory pro Windows Server 2008 a SQL Server 2008](https://azure.microsoft.com/blog/announcing-new-options-for-sql-server-2008-and-windows-server-2008-end-of-support).
- **Snížení investičních nákladů.** Hostování vlastní serverové infrastruktury s sebou nese značné investice do hardwaru, softwaru, elektřiny a pracovní síly. Migrace do cloudového řešení tak může přinést výrazné snížení těchto nákladů. Pokud chcete, aby bylo snížení nákladů co nejefektivnější, může být potřeba návrh řešení upravit. Migrace „beze změn“ je ale dobrým prvním krokem.
- **Uvolnění prostoru v datovém centru.** Pokud chcete rozšířit kapacitu vašeho datového centra, může být vaší volbou právě Azure. Jedním z možných způsobů je použití cloudu jako rozšíření místních možností.
- **Rychlé dosažení návratnosti investic.** Dosažení návratnosti investic je díky cloudovým řešením mnohem snazší, protože s modelem cloudových plateb máte výborný přehled o využívání služeb i prostor na jeho realizaci.

Každý z výše uvedených scénářů může být vstupním bodem pro rozšíření vaší cloudové stopy za pomocí jiných metod (změna hostitele, refaktoring, změna architektury, opětovné sestavení nebo náhrada).

## <a name="migration-characteristics"></a>Vlastnosti migrace

Tento průvodce předpokládá, že ještě před zahájením migrace tvoří vaše digitální aktiva hlavně místní hostovaná infrastruktura a případně i hostované klíčové obchodní aplikace. Po úspěšné migraci mohou vaše data vypadat prakticky stejně, jako když se nacházela v místním prostředí, ale infrastruktura je hostovaná v cloudových prostředcích. Ideální datové portfolio může případně být i variací vašeho aktuálního portfolia, protože ho tvoří aspekty vaší místní infrastruktury a součásti, které se refaktorují za účelem optimalizace a využívání cloudové platformy.

Cílem tohoto postupu migrace je dosažení následujících bodů:

- Vyřešení konce životnosti staršího hardwaru
- Snížení investičních nákladů
- Návratnost investic

> [!NOTE]
> Další výhodou tohoto postupu migrace je doplňkový model softwarové podpory pro Windows 2008, Windows 2008 R2 a SQL Server 2008 a SQL Server 2008 R2. Další informace naleznete v tématu:
>
> - [Windows Server 2008 a Windows Server 2008 R2](https://www.microsoft.com/cloud-platform/windows-server-2008)
> - [SQL Server 2008 a SQL Server 2008 R2](https://www.microsoft.com/sql-server/sql-server-2008)

# <a name="understand-migration-approaches"></a>[Porozumění přístupům k migraci](#tab/Approach)

Strategie a nástroje, které použijete k migraci aplikace do Azure, budou do značné míry záviset na vašich obchodních motivacích, požadavcích na technologie, časových osách, a také na hlubokém porozumění vlastním migrovaným úlohám a prostředkům (infrastruktura, aplikace a data).

Ještě než určíte strategii migrace do cloudu, proveďte analýzu možných aplikací, abyste věděli, jak jsou kompatibilní s technologiemi hostování v cloudu. Na pomoc si můžete vzít [průvodce rozhodováním ohledně nástrojů pro migraci](../../decision-guides/migrate-decision-guide/index.md) pro architekturu přechodu na cloud.

Migrace zaměřená na technologii IaaS, při níž servery (společně s přidruženými aplikacemi a daty) změní hostitele v cloudu pomocí virtuálních počítačů, často představuje nejjednodušší způsob, jak přesunout úlohy do cloudu. Nezapomeňte ale, že správná konfigurace, zabezpečení a údržba virtuálních počítačů vyžaduje v porovnání se službami PaaS v Azure mnohem více času a odborných znalostí v oblasti IT. Pokud zvažujete službu Azure Virtual Machines, nezapomeňte vzít v úvahu náročnost průběžné údržby, kterou vyžadují opravy, aktualizace a správa vašeho prostředí virtuálních počítačů.

Při posuzování migrovaných úloh zjistěte, které aplikace mohou běžet za pomocí technologií PaaS (jako je Azure App Service) nebo orchestrátorů (například Azure Kubernetes Service) bez nutnosti provedení zásadních úprav. Právě tyto aplikace by měly být prvními kandidáty na modernizaci a cloudovou optimalizaci.

## <a name="learn-more"></a>Další informace

- [Průvodce rozhodováním ohledně nástrojů pro migraci pro architekturu přechodu na cloud](../../decision-guides/migrate-decision-guide/index.md)
- [5R racionalizace](../../digital-estate/5-rs-of-rationalization.md)

# <a name="planning-checklist"></a>[Kontrolní seznam pro plánování](#tab/Checklist)

Než začnete s migrací, je potřeba splnit některé předpoklady. Přesné podrobnosti těchto činností se liší v závislosti na migrovaném prostředí. Obecně ale platí následující kontrolní seznam:

> [!div class="checklist"]
>
> - **Identifikace zúčastněných stran:** Určete hlavní osoby, které se zúčastní migrace nebo které jsou závislé na jejím výsledku.
> - **Identifikace hlavních milníků:** Abyste mohli efektivně naplánovat časovou osu migrace, stanovte si hlavní milníky, které bude potřeba splnit.
> - **Určení strategie migrace:** Zjistěte, které z pěti zásad racionalizace využijete.
> - **Posouzení technické způsobilosti:** Ověřte si technickou připravenost a vhodnost pro migraci a určete, jakou úroveň podpory budete možná potřebovat od externích partnerů nebo podpory Azure.
> - **Plánování migrace:** Proveďte podrobné posouzení a plánování nutné k přípravě vašich prostředků (infrastruktury, aplikací a dat) i infrastruktury Azure na migraci.
> - **Otestování migrace:** Proveďte testovací migraci s omezeným rozsahem a zkontrolujte tak plán migrace.
> - **Migrace služeb:** Provedení vlastní migrace
> - **Po migraci:** Zjistěte, co je po migraci prostředí do Azure potřeba udělat.

Pokud se rozhodnete pro migraci založenou na změně hostitele, bude potřeba provést i tyto činnosti:

> [!div class="checklist"]
>
> - **Sladění se zásadami správného řízení:** Shodují se základní prvky migrace se zásadami správného řízení?
> - **Síť:** Síťová strategie by měla být sladěná s požadavky na zabezpečení IT.
> - **Identita:** Je potřeba sjednotit strategii hybridních identit, aby vyhovovala správě identit a plánu přechodu na cloud.

::: zone target="docs"

<!-- markdownlint-disable MD024 -->

## <a name="learn-more"></a>Další informace

- [5R racionalizace](../../digital-estate/5-rs-of-rationalization.md)
- [Průvodce rozhodováním ohledně nástrojů pro migraci](../../decision-guides/migrate-decision-guide/index.md)
- [Kontrolní seznam pro plánování architektury přechodu na cloud](../migration-considerations/prerequisites/planning-checklist.md)

::: zone-end
