---
title: Co je potřeba k převedení migrovaného prostředku do produkčního prostředí?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proces v rámci migrace do cloudu, který se zaměřuje na úkoly při migraci sad funkcí do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb025eacb7743f470b15e2714ed65a05c21034a1
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825468"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>Co je potřeba k převedení migrovaného prostředku do produkčního prostředí?

Převedení do produkčního prostředí představuje dokončení migrace sady funkcí do cloudu. Po převedení prostředku a všech jeho závislostí dojde k přesměrování provozu do produkčního prostředí. Po přesměrování provozu se stanou místní prostředky zastaralými a budou se moct vyřadit z provozu.

Proces převedení se liší v závislosti na architektuře sady funkcí. Existuje však několik konzistentních požadavků a několik běžných úkolů. Tento článek je popisuje a slouží jako jakýsi kontrolní seznam před převedením.

## <a name="prerequisite-processes"></a>Požadované procesy

Před nasazením do produkčního prostředí je třeba provést, zdokumentovat a ověřit každý z následujících procesů:

- **[Posouzení](../assess/index.md):** Posoudila se kompatibilita sady funkcí s cloudem.
- **[Návrh architektury](../assess/architect.md):** Pro strukturu sady funkcí je navržená správná architektura podle zvoleného poskytovatele cloudu.
- **[Replikace](../migrate/replicate.md):** Prostředky se replikovaly do cloudového prostředí.
- **[Přípravná instance](../migrate/stage.md):** Replikované prostředky se obnovily v přípravné instanci cloudového prostředí.
- **[Firemní testování](./business-test.md):** Sada funkcí byla plně otestovaná a ověřená firemními uživateli.
- **[Firemní plán změn](./business-change-plan.md):** Firma nasdílela plán změn, které se mají udělat v souladu s převedením do produkčního prostředí. To by mělo zahrnovat plán přijetí uživateli, změny obchodních procesů, uživatele, kteří potřebují školení, a časové osy pro různé aktivity.
- **[Připraveno](./ready.md):** Obecně řečeno je před převedením nutné provést řadu technických změn.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Osvědčené postupy, které je potřeba provést před převedením

Jako součást procesu převedení bude pravděpodobně nutné dokončit a zdokumentovat následující technické změny:

- **Doladění domén.** Některé podnikové zásady vyžadují samostatné domény pro přípravné a produkční prostředí. Zajistěte, aby všechny prostředky byly připojené ke správné doméně.
- **Směrování uživatelů.** Ověřte, že uživatelé přistupují k sadě funkcí prostřednictvím správných síťových tras. Ověřte konzistentní výkon podle očekávání.
- **Doladění identit.** Ověřte, jestli uživatelé přesměrovávaní do aplikace mají správná oprávnění v rámci domény, ve které je aplikace hostovaná.
- **Výkon.** Proveďte finální ověření výkonu sady funkcí, aby se minimalizovala překvapení.
- **Ověření provozní kontinuity a zotavení po havárii.** Ověřte, jestli máte nastavené řádné procesy zálohování a obnovení a jestli fungují podle očekávání.
- **Klasifikace dat.** Ověřte klasifikaci dat, aby se zajistila implementace správných ochran a zásad.
- **Ověření ředitelem pro zabezpečení informací.** Ujistěte se, že ředitel pro zabezpečení informací zkontroloval sadu funkcí, obchodní rizika, toleranci rizik a strategie jejich omezení.

## <a name="final-step-promote"></a>Poslední krok: Převedení

Sady funkcí budou vyžadovat různé úrovně podrobných procesů kontroly a převedení. Běžným posledním krokem při všech převedeních do produkčního prostředí ale bývá přizpůsobení nastavení sítě. Až bude všechno ostatní připravené, aktualizujte záznamy DNS nebo IP adresy, abyste mohli směrovat provoz do migrované sady funkcí.

## <a name="next-steps"></a>Další postup

Převedení sady funkcí do produkčního prostředí signalizuje dokončení migrace. Paralelně s migrací je ale potřeba [vyřadit z provozu zastaralé prostředky](./decommission.md).

> [!div class="nextstepaction"]
> [Vyřazení zastaralých prostředků](./decommission.md)
