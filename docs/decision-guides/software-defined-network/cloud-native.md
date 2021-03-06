---
title: 'Softwarově definované sítě: Cloud – nativní'
description: Rozhraní pro přijetí v cloudu pro Azure použijte k získání informací o virtuálních sítích nativních pro Cloud, které jsou potřeba pro nasazení virtuálních počítačů do cloudu.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ffcec60ce604cd4698daa78065223c52d1136c51
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80431289"
---
# <a name="software-defined-networking-cloud-native"></a>Softwarově definované sítě: Cloud – nativní

Virtuální síť nativní pro Cloud se vyžaduje při nasazení prostředků IaaS, jako jsou virtuální počítače, na cloudovou platformu. Přístup k virtuálním sítím z externích zdrojů, podobně jako na webu, je nutné explicitně zřídit. Tyto typy virtuálních sítí podporují vytváření podsítí, pravidla směrování a virtuální brány firewall a zařízení pro správu provozu.

Virtuální síť cloudového nativního prostředí nemá žádné závislosti na místních nebo jiných necloudových prostředcích vaší organizace, aby podporovala úlohy hostované v cloudu. Všechny požadované prostředky se zřídí buď ve virtuální síti, nebo pomocí spravovaných PaaS nabídek.

## <a name="cloud-native-assumptions"></a>Předpoklady cloudu – nativní

Nasazení cloudové nativní virtuální sítě předpokládá následující:

- Úlohy, které nasadíte do virtuální sítě, nemají žádné závislosti na aplikacích nebo službách, které jsou přístupné jenom v rámci vaší místní sítě. Neposkytují přístup k koncovým bodům přes veřejný Internet, nepoužívané aplikace a služby hostované interně, ale prostředky hostované na cloudové platformě nejsou použitelné.
- Správa identit a řízení přístupu vašich úloh závisí na službách identity Cloud Platform nebo serverech IaaS hostovaných ve vašem cloudovém prostředí. Nebudete se muset přímo připojovat ke službám identit hostovaným místně nebo jinými externími umístěními.
- Vaše služby identity nemusejí podporovat jednotné přihlašování (SSO) s místními adresáři.

Virtuální sítě nativní pro Cloud nemají žádné externí závislosti. To usnadňuje nasazení a konfiguraci. v důsledku toho je tato architektura často nejlepší volbou pro experimenty nebo jiná menší samostatná nebo rychlé iterace nasazení.

Další problémy, které by týmy při přijímání cloudu měly zvážit při projednávání cloudové nativní architektury virtuálních sítí, zahrnují:

- Stávající úlohy navržené pro běh v místním datovém centru můžou potřebovat rozsáhlou úpravu, která bude využívat cloudové funkce, jako jsou služby úložiště nebo ověřování.
- Cloudové nativní sítě se spravují výhradně prostřednictvím nástrojů pro správu cloudových platforem, a proto můžou v rámci svých stávajících standardů IT vést ke správě a zásadám, jako je čas.

## <a name="next-steps"></a>Další kroky

Další informace o virtuálních sítích nativních pro Cloud v Azure najdete v těchto tématech:

- [Azure Virtual Network: průvodci postupy](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm). Nově vytvořené virtuální sítě Azure jsou ve výchozím nastavení cloudově nativní. Pomocí těchto průvodců můžete naplánovat návrh a nasazení virtuálních sítí.
- [Omezení předplatného: sítě](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=/azure/virtual-network/toc.json#networking-limits). Každá virtuální síť a připojené prostředky existují v rámci jednoho předplatného. Tyto prostředky jsou vázané na omezení předplatného.
