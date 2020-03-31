---
title: Průvodci rozhodováním ohledně architektury
description: Tyto základní modely a vzory komponent infrastruktury cloudového nasazení využijte k podpoře vašich konkrétních scénářů nasazení v cloudu.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9a2cfb6d4280ac5d5fd6e16e330121e568ba7a71
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434894"
---
# <a name="architectural-decision-guides"></a>Průvodci rozhodováním ohledně architektury

Průvodci rozhodováním ohledně architektury v architektuře přechodu na cloud popisují vzory a modely, které vám pomůžou při vytváření pokynů k návrhu zásad správného řízení v cloudu. Každý průvodce rozhodováním se zaměřuje na jednu základní komponentu infrastruktury cloudových nasazení a uvádí vzory a modely, které mohou podporovat konkrétní scénáře cloudového nasazení.

Cesty k zásadám správného řízení vám poskytnou směrný plán, jakmile pro vaši organizaci začnete zavádět zásady správného řízení v cloudu. Pro tyto cesty však platí několik předpokladů z hlediska požadavků a priorit, které se nemusí shodovat s požadavky a prioritami vaší organizace.

Tito průvodci rozhodováním doplňují ukázkové cesty k zásadám správného řízení a poskytují alternativní vzory a modely, které vám pomůžou sladit rozhodnutí ohledně návrhu architektury z příkladu pokynů k návrhu s vašimi požadavky.

## <a name="decision-guidance-categories"></a>Kategorie pokynů k rozhodování

Každá z následujících kategorií představuje základní technologii všech cloudových nasazení. V ukázkových cestách k zásadám správného řízení se v souvislosti s těmito technologiemi přijímají rozhodnutí ohledně návrhu na základě požadavků ukázkových firem, a některá z těchto rozhodnutí nemusí odpovídat potřebám vaší organizace. Následující části popisují alternativní možnosti pro jednotlivé kategorie. Můžete si tak vybrat vzor nebo model, který nejlépe vyhovuje vašim požadavkům.

[Předplatná:](./subscriptions/index.md) Naplánujte strukturu účtu a návrh předplatného vašeho cloudového nasazení v souladu s možnostmi správy, fakturace a vlastnictví vaší organizace.

[Identita:](./identity/index.md) Integrujte cloudové služby identit s vašimi stávajícími prostředky identit a zajistěte ve svém IT prostředí podporu ověřování a řízení přístupu.

[Vynucování zásad:](./policy-enforcement/index.md) Definujte a vynucujte pro prostředky a úlohy nasazené v cloudu pravidla zásad organizace, která odpovídají vašim požadavkům na zásady správného řízení.

[Konzistence prostředků:](./resource-consistency/index.md) Zajistěte soulad nasazování a organizace vašich cloudových prostředků a vynucujte požadavky na správu a zásady.

[Označování prostředků:](./resource-tagging/index.md) Uspořádejte své cloudové prostředky a zajistěte podporu modelů fakturace, přístupů k účtování cloudu, správy a optimalizace využití prostředků a nákladů. Označování prostředků vyžaduje konzistentní a dobře uspořádané schéma pojmenování a metadat.

[Softwarově definované sítě:](./software-defined-network/index.md) Nasazujte do cloudu zabezpečené úlohy s využitím možností rychlého nasazování a úprav virtualizovaných sítí. Softwarově definované sítě podporují flexibilní úlohy, izolaci prostředků a integraci cloudových systémů se stávající IT infrastrukturou.

[Šifrování:](./encryption/index.md) Zabezpečte svá citlivá data s využitím šifrování a splňte tak požadavky vaší organizace na zabezpečení a dodržování předpisů.

[Protokolování a vytváření sestav](./logging-and-reporting/index.md) Monitorujte data protokolů generovaná cloudovými prostředky. Analýzou dat můžete získat přehledy o stavu úloh z hlediska operací, údržby, a dodržování předpisů.

## <a name="next-steps"></a>Další kroky

Zjistěte, proč předplatná a účtu slouží jako základ cloudového nasazení.

> [!div class="nextstepaction"]
> [Návrh předplatných](./subscriptions/index.md)
