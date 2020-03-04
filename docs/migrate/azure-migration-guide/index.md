---
title: Úvod k průvodci migrací do Azure
description: Podrobné pokyny vám pomůžou efektivně migrovat služby vaší organizace do Azure.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 4d2bb420609bb703a1f32b0912eb9c17ccabe4e9
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225506"
---
# <a name="azure-migration-guide-before-you-start"></a>Průvodce migrací do Azure: Než začnete

[Metodika migrace architektury přechodu na cloud](../index.md) provede čtenáře iterativním procesem migrace jedné úlohy nebo malé kolekce úloh. V každé iteraci se procházejí procesy vyhodnocení, migrace, optimalizace a zvýšení úrovně, aby se zaručilo, že úlohy jsou připravené pro splnění produkčních požadavků. Tento proces nezávislý na cloudu může řídit migraci na libovolného poskytovatele cloudu.

Tento průvodce ukazuje zjednodušenou verzi tohoto procesu při migraci z místního prostředí do **Azure**.

::: zone target="docs"

> [!TIP]
> Pokud chcete interaktivní prostředí, zobrazte tuto příručku na webu Azure Portal. Na webu Azure Portal přejděte do [Centra rychlého startu Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade), vyberte **Migrace prostředí do Azure** a potom postupujte podle podrobných pokynů.

::: zone-end

## <a name="migration-tools"></a>[Nástroje pro migraci](#tab/MigrationTools)

Tento průvodce ukazuje navrhovaný způsob pro vaši první migraci do Azure, protože vás seznámí s metodikou a nástroji nativními pro cloud, které se při migraci do Azure běžně používají. Tyto nástroje jsou uvedené na následujících stránkách:

> [!div class="checklist"]
>
> - **Vyhodnocení technické vhodnosti jednotlivých úloh:** Ověření technické připravenosti a vhodnosti k migraci
> - **Migrace služeb:** Provedení vlastní migrace replikací místních prostředků do Azure.
> - **Správa nákladů a fakturace:** Seznámení s nástroji pro kontrolu nákladů v Azure.
> - **Optimalizace a zvýšení úrovně:** Optimalizace pro zajištění rovnováhy mezi výkonem a náklady před přesunem úlohy do produkčního prostředí.
> - **Získání pomoci:** Získání pomoci a podpory v průběhu migrace nebo aktivit po migraci

Předpokládá se, že cílová zóna je už nasazená, a to v souladu s osvědčenými postupy uvedenými v [metodice připravenosti architektury přechodu na cloud](../../ready/index.md).

## <a name="when-to-use-this-guide"></a>[Kdy použít tohoto průvodce](#tab/WhenToUseThisGuide)

Nástroje popsané v tomto průvodci podporují širokou škálu scénářů migrace, ale tento průvodce se zaměřuje pouze na situace omezeného rozsahu s _minimální složitostí_. Pokud chcete zjistit, jestli je tento průvodce migrací vhodný pro váš projekt, zvažte, jestli pro vaši situaci platí následující podmínky:

- Úlohy pro počáteční migraci nejsou klíčové a neobsahují citlivá data.
- Migrujete homogenní prostředí.
- K dokončení migrace je potřeba spolupráce pouze několika obchodních jednotek.
- Nemáte v plánu celou migraci automatizovat.
- Migrujete malý počet serverů.
- Mapování závislostí komponent, které se mají migrovat, je snadno definovatelné.
- Ve vašem odvětví platí minimální zákonné požadavky týkající se této migrace.

Pokud některé z těchto podmínek pro vaši situaci neplatí, měli byste zvážit použití [rozšířeného průvodce](../expanded-scope/index.md). Při provádění migrací, které vyžadují rozšířeného průvodce, také doporučujeme požádat o pomoc některého z týmů nebo partnerů Microsoftu. Zákazníci, kteří se spojí s Microsoftem nebo certifikovanými partnery, dosahují v těchto scénářích lepších výsledků. Další informace o tom, jak požádat o pomoc, najdete v tomto průvodci.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Další informace naleznete v tématu:

- [Rozšířený průvodce](../expanded-scope/index.md)

::: zone-end
