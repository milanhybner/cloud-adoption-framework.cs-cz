---
title: Několik datových center
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Několik datových center
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e58dd50417ec6377774f07ee613a5fc69f74f0ea
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833567"
---
# <a name="multiple-datacenters"></a>Několik datových center

Rozsah migrace často zahrnuje i převedení několika datových center. Následující pokyny rozšíří rozsah [Průvodce migrací do Azure](../azure-migration-guide/index.md), aby pokrýval i víc datových center.

## <a name="general-scope-expansion"></a>Obecné rozšíření rozsahu

Většina činností požadovaných v tomto rozšíření rozsahu proběhne během procesů řešení požadavků, vyhodnocení a optimalizace migrace.

## <a name="suggested-prerequisites"></a>Navrhované předpoklady

Před zahájením migrace byste měli v rámci nástroje pro správu projektů vytvořit náměty, které budou představovat jednotlivá migrovaná datová centra. Je pak důležité porozumět obchodním výsledkům a motivacím, které tuto migraci ospravedlňují. Tyto motivace lze použít k určení priorit seznamu námětů (nebo datových center). Pokud je například migrace hnaná snahou opustit datová centra před tím, než bude potřeba prodloužit nájem, jednotlivé náměty budou mít priority na základě data vypršení nájmu.

V rámci každého námětu budou úlohy, které se mají vyhodnocovat a migrovat, spravované jako funkce. Každé aktivum v rámci této úlohy se bude spravovat jako uživatelský scénář. Práce, která je nutná k vyhodnocení, migraci, optimalizaci, povýšení, zabezpečení a správě každého aktiva, bude reprezentovaná úkolem pro každé aktivum.

Sprinty nebo iterace se pak skládají z řady úkolů potřebných k migraci aktiv a uživatelských scénářů, potvrzených týmem přechodu na cloud. Vydání se pak skládají z jedné nebo několika úloh nebo funkcí, které mají být povýšeny do produkčního prostředí.

## <a name="assess-process-changes"></a>Změny procesu vyhodnocení

Největší změna procesu vyhodnocení při rozšiřování rozsahu na pokrytí více datových center se týká přesného záznamu a stanovení priorit úloh a závislostí mezi datovými centry.

### <a name="suggested-action-during-the-assess-process"></a>Navrhovaná akce během procesu vyhodnocení

**Vyhodnocení závislostí mezi datacentry:** [Nástroje pro vizualizaci závislostí v Azure Migrate](/azure/migrate/concepts-dependency-visualization) vám můžou pomoct identifikovat závislosti. Použití této sady nástrojů před migrací je dobrý obecný osvědčený postup. Při řešení globální složitosti je to však nezbytný krok procesu posouzení. Prostřednictvím [seskupování závislostí](/azure/migrate/how-to-create-group-machine-dependencies) může vizualizace pomoct identifikovat IP adresy a porty všech prostředků vyžadovaných pro podporu dané úlohy.

> [!IMPORTANT]
> Dvě důležité poznámky: Zaprvé odborník, který rozumí umísťování aktiv a schématům IP adres, musí identifikovat aktiva, která se nachází v sekundárním datovém centru. Zadruhé je důležité vyhodnotit podřízené závislosti a klienty ve vizuálu a pochopit obousměrné závislosti.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Migrace několika datových center je podobná konsolidaci datových center. Po migraci se cloud stane jediným datovým centrem pro víc aktiv. Nejpravděpodobnějším rozšířením rozsahu během procesu migrace je ověření a sladění IP adres.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhovaná akce během procesu migrace

Dál jsou uvedené aktivity, které silně ovlivňují úspěšnost migrace do cloudu:

- **Vyhodnocení konfliktů sítě:** Při konsolidaci datových center k jednomu poskytovateli cloudu je pravděpodobné, že se vytvoří síťové konflikty, konflikty DNS nebo jiné. Během migrace je důležité testovat konflikty, aby nedocházelo k přerušením funkce produkčních systémů hostovaných v cloudu.
- **Aktualizace směrovacích tabulek:** Při konsolidaci sítí nebo datových center jsou často potřeba úpravy směrovacích tabulek.

## <a name="optimize-and-promote-process-changes"></a>Změny procesu optimalizace a povýšení

Během optimalizace může být nutné provést další testování.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Navrhovaná akce během procesu optimalizace a povýšení

Před povýšením je důležité zajistit během tohoto rozšiřování rozsahu další úrovně testování. Během testování je důležité otestovat směrování nebo jiné síťové konflikty. Dále je důležité izolovat nasazenou aplikaci a znovu otestovat, že byly všechny závislosti migrovány do cloudu. V tomto případě izolace znamená oddělení nasazeného prostředí od produkčních sítí. Při tom je možné zachytit přehlédnutá aktiva, která se pořád spouští místně.

## <a name="secure-and-manage-process-changes"></a>Změny procesu zabezpečení a správy

Toto rozšíření rozsahu by nemělo procesy zabezpečení a správy měnit.

## <a name="next-steps"></a>Další postup

Vraťte se na [kontrolní seznam pro rozšířený rozsah](./index.md) a zkontrolujte, jestli je vaše metoda migrace plně v souladu.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
