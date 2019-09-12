---
title: 'Softwarově definované sítě: Model nativní pro cloud'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diskuze o virtuálních síťových službách, které jsou nativní pro Cloud
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 1c30e57761b12d00617296fb3f9d5a87b8b6cce7
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828328"
---
# <a name="software-defined-networking-cloud-native"></a>Softwarově definované sítě: Model nativní pro cloud

Virtuální síť nativní pro Cloud je nutná při nasazení prostředků IaaS, jako jsou virtuální počítače, na cloudovou platformu. Přístup k virtuálním sítím z externích zdrojů, podobně jako na webu, je nutné explicitně zřídit. Tyto typy virtuálních sítí podporují vytváření podsítí, pravidla směrování a virtuální brány firewall a zařízení pro správu provozu.

Cloudová virtuální síť nemá žádné závislosti na místních nebo jiných necloudových prostředcích vaší organizace pro podporu úloh hostovaných v cloudu. Všechny požadované prostředky se zřídí buď ve virtuální síti, nebo pomocí spravovaných PaaS nabídek.

## <a name="cloud-native-assumptions"></a>Předpoklady cloudu – nativní

Nasazení cloudové nativní virtuální sítě předpokládá následující:

- Úlohy, které nasadíte do virtuální sítě, nemají žádné závislosti na aplikacích nebo službách, které jsou přístupné jenom v rámci vaší místní sítě. Neposkytují přístup k koncovým bodům přes veřejný Internet, nepoužívané aplikace a služby hostované interně, ale prostředky hostované na cloudové platformě nejsou použitelné.
- Správa identit a řízení přístupu vašich úloh závisí na službách identity Cloud Platform nebo serverech IaaS hostovaných ve vašem cloudovém prostředí. Nebudete se muset přímo připojovat ke službám identit hostovaným místně nebo jinými externími umístěními.
- Vaše služby identity nemusejí podporovat jednotné přihlašování (SSO) s místními adresáři.

Virtuální sítě nativní pro Cloud nemají žádné externí závislosti. To usnadňuje nasazení a konfiguraci. v důsledku toho je tato architektura často nejlepší volbou pro experimenty nebo jiná menší samostatná nebo rychlé iterace nasazení.

Další problémy, které by týmy při přijímání cloudu měly zvážit při projednávání cloudové nativní architektury virtuálních sítí, zahrnují:

- Stávající úlohy navržené pro běh v místním datovém centru můžou potřebovat rozsáhlou úpravu, která bude využívat cloudové funkce, jako jsou služby úložiště nebo ověřování.
- Cloudové nativní sítě se spravují výhradně prostřednictvím nástrojů pro správu cloudových platforem, a proto můžou v rámci svých stávajících standardů IT vést ke správě a zásadám, jako je čas.

## <a name="next-steps"></a>Další postup

Další informace o virtuálních sítích nativních pro Cloud v Azure najdete v těchto tématech:

- [Azure Virtual Network: Návody](/azure/virtual-network/virtual-network-vnet-plan-design-arm). Nově vytvořené virtuální sítě Azure jsou ve výchozím nastavení cloudově nativní. Pomocí těchto průvodců můžete naplánovat návrh a nasazení virtuálních sítí.
- [Omezení předplatného: Sítě](/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits). Jedna virtuální síť a připojené prostředky můžou existovat jenom v rámci jednoho předplatného, které jsou svázané s omezeními předplatného.