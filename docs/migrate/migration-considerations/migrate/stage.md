---
title: Pracovní aktivity během migrace
description: K pochopení přípravných aktivit a přidružených dodávek potřebných během migrace použijte rozhraní pro přijetí cloudu pro Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: f6d45943ac8545083ce8d31215488b433a3ad00b
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432458"
---
# <a name="understand-staging-activities-during-a-migration"></a>Pochopení přípravných aktivit během migrace

Jak je popsáno v článku o modelech povýšení, *příprava* je bod, ve kterém byly prostředky migrovány do cloudu. Zatím ale nejsou připravené k povýšení do produkčního prostředí. To je často posledním krokem během procesu migrace. Po přípravě je úloha spravovaná týmem provozu IT nebo provozu cloudu, aby byla připravená k využití v produkčním prostředí.

## <a name="deliverables"></a>Výstupy

Připravené prostředky nemusí být připravené k použití v produkčním prostředí. Existuje několik kontrol připravenosti na produkční prostředí, které by se měly dokončit před tím, než se tato fáze považuje za dokončenou. Následuje seznam výstupů často spojených s dokončením přípravy prostředků.

- **Automatizované testy.** Všechny automatizované testy, které jsou k dispozici pro ověření výkonu úloh, by se měly spustit před uzavřením procesu přípravy. Jakmile prostředek opustí fázi přípravy, synchronizace s původním zdrojovým systémem se ukončí. V takovém případě je těžší znovu nasadit replikované prostředky poté, co proběhla příprava prostředků na optimalizaci.
- **Dokumentace k migraci.** Většina nástrojů pro migraci může generovat automatizovanou sestavu migrovaných prostředků. Před uzavřením aktivity přípravy by se měly pro přehlednost zdokumentovat všechny migrované prostředky.
- **Dokumentace ke konfiguraci.** Všechny změny provedené u prostředku (během nápravy, replikace nebo přípravy), by se měly zdokumentovat kvůli provozní připravenosti.
- **Dokumentace backlogu.** Backlog migrace by se měl aktualizovat tak, aby odrážel připravené úlohy a prostředky.

## <a name="next-steps"></a>Další kroky

Po otestování a zdokumentování připravených prostředků můžete přejít k [aktivitám optimalizace](../optimize/index.md).

> [!div class="nextstepaction"]
> [Optimalizace migrovaných úloh](../optimize/index.md)
