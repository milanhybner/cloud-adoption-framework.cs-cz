---
title: Několik datových center
description: Několik datových center
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1a9e9082e4ceca7b83a4491c49e0932a3caaa9d7
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429661"
---
# <a name="multiple-datacenters"></a>Několik datových center

Rozsah migrace často zahrnuje i převedení několika datových center. Následující pokyny rozšíří rozsah [Průvodce migrací do Azure](../azure-migration-guide/index.md), aby pokrýval i víc datových center.

## <a name="general-scope-expansion"></a>Rozšíření obecného rozsahu

Většina činností požadovaných v tomto rozšíření rozsahu proběhne během procesů řešení požadavků, vyhodnocení a optimalizace migrace.

## <a name="suggested-prerequisites"></a>Navrhované předpoklady

Před zahájením migrace byste měli v rámci nástroje pro správu projektů vytvořit náměty, které budou představovat jednotlivá migrovaná datová centra. Je pak důležité porozumět obchodním výsledkům a motivacím, které tuto migraci ospravedlňují. Tyto motivace lze použít k určení priorit seznamu námětů (nebo datových center). Pokud je například migrace hnaná snahou opustit datová centra před tím, než bude potřeba prodloužit nájem, jednotlivé náměty budou mít priority na základě data vypršení nájmu.

V rámci každého námětu budou úlohy, které se mají vyhodnocovat a migrovat, spravované jako funkce. Každé aktivum v rámci této úlohy se bude spravovat jako uživatelský scénář. Práce, která je nutná k vyhodnocení, migraci, optimalizaci, povýšení, zabezpečení a správě každého aktiva, bude reprezentovaná úkolem pro každé aktivum.

Sprinty nebo iterace se pak skládají z řady úkolů potřebných k migraci aktiv a uživatelských scénářů, potvrzených týmem přechodu na cloud. Vydání se pak skládají z jedné nebo několika úloh nebo funkcí, které mají být povýšeny do produkčního prostředí.

## <a name="assess-process-changes"></a>Posouzení změn procesu

Největší změna procesu vyhodnocení při rozšiřování rozsahu na pokrytí více datových center se týká přesného záznamu a stanovení priorit úloh a závislostí mezi datovými centry.

### <a name="suggested-action-during-the-assess-process"></a>Navrhovaná akce během procesu posouzení

**Vyhodnotit závislosti mezi datovými centru:** [Nástroje pro vizualizaci závislostí v Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) můžou přispět ke kotvícím závislostem. Použití této sady nástrojů před migrací je dobrý obecný osvědčený postup. Při řešení globální složitosti je to však nezbytný krok procesu posouzení. Prostřednictvím [seskupování závislostí](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) může vizualizace pomoct identifikovat IP adresy a porty všech prostředků vyžadovaných pro podporu dané úlohy.

> [!IMPORTANT]
> Dvě důležité poznámky: Nejdřív je k identifikaci prostředků, které se nacházejí v sekundárním datacentru, nutný odborník na danou problematiku s porozuměním umístění prostředků a schématy IP adres. Zadruhé je důležité vyhodnotit podřízené závislosti a klienty ve vizuálu a pochopit obousměrné závislosti.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Migrace několika datových center je podobná konsolidaci datových center. Po migraci se cloud stane jediným datovým centrem pro víc aktiv. Nejpravděpodobnějším rozšířením rozsahu během procesu migrace je ověření a sladění IP adres.

### <a name="suggested-action-during-the-migrate-process"></a>Doporučované akce během procesu migrace

Dál jsou uvedené aktivity, které silně ovlivňují úspěšnost migrace do cloudu:

- **Vyhodnotit konflikty sítě:** Při konsolidaci datových center do jednoho poskytovatele cloudu je pravděpodobné, že se vytvoří síť, DNS nebo jiné konflikty. Během migrace je důležité testovat konflikty, aby nedocházelo k přerušením funkce produkčních systémů hostovaných v cloudu.
- **Aktualizovat směrovací tabulky:** Při konsolidaci sítí nebo datových center se často vyžadují úpravy směrovacích tabulek.

## <a name="optimize-and-promote-process-changes"></a>Optimalizace a propagace změn procesů

Během optimalizace může být nutné provést další testování.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Navrhované akce během procesu optimalizace a převedení

Před povýšením je důležité zajistit během tohoto rozšiřování rozsahu další úrovně testování. Během testování je důležité otestovat směrování nebo jiné síťové konflikty. Dále je důležité izolovat nasazenou aplikaci a znovu otestovat, že byly všechny závislosti migrovány do cloudu. V tomto případě izolace znamená oddělení nasazeného prostředí od produkčních sítí. Při tom je možné zachytit přehlédnutá aktiva, která se pořád spouští místně.

## <a name="secure-and-manage-process-changes"></a>Zabezpečení a správa změn procesů

Toto rozšíření rozsahu by nemělo procesy zabezpečení a správy měnit.

## <a name="next-steps"></a>Další kroky

Vraťte se na [kontrolní seznam pro rozšířený rozsah](./index.md) a zkontrolujte, jestli je vaše metoda migrace plně v souladu.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
