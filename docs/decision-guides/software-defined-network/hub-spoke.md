---
title: 'Softwarově definované sítě: střed a paprskový'
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak centrum a Paprskové sítě organizují síťovou infrastrukturu do několika propojených virtuálních sítí.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9bcdc7168fccc24eba8c3a6a55668c976556590d
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433158"
---
# <a name="software-defined-networking-hub-and-spoke"></a>Softwarově definované sítě: střed a paprskový

Model sítě hub a paprsková síť uspořádá vaši cloudovou síťovou infrastrukturu založenou na Azure do několika propojených virtuálních sítí. Tento model vám umožní efektivněji spravovat společné komunikační nebo bezpečnostní požadavky a řešit potenciální omezení předplatného.

V _modelu hvězdicové lokality je výchozím_ centrem virtuální síť, která funguje jako centrální umístění pro správu externího připojení a hostitelských služeb používaných více úlohami. _Paprsky_ jsou virtuální sítě, které hostují úlohy a připojují se k centrálnímu centru prostřednictvím [partnerského vztahu virtuálních sítí](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

Veškerý provoz procházející nebo z sítí paprsků úloh je směrován přes síť centra, kde se dá směrovat, kontrolovat nebo jinak spravovat centrálně spravovaná pravidla nebo procesy IT.

Tento model se zaměřuje na každý z následujících otázek:

- **Úspora nákladů a efektivita správy.** Centralizované služby, které mohou být sdíleny více úlohami, jako jsou síťová virtuální zařízení (síťová virtuální zařízení) a servery DNS, v jednom umístění umožňují IT minimalizovat redundantní prostředky a procesy správy napříč více úlohami.
- **Překonání omezení předplatného.** Velké cloudové úlohy můžou vyžadovat využívání více prostředků, než je povolené v rámci jednoho předplatného Azure (viz [omezení předplatného](https://docs.microsoft.com/azure/azure-subscription-service-limits)). Peering úloh virtuálních sítí z různých předplatných do centra může tyto limity překonat.
- **Oddělení obav.** Možnost nasazovat jednotlivé úlohy mezi týmy centrálního IT a týmy úloh.

Následující diagram znázorňuje příklad architektury centra a paprsků, včetně centrálního spravovaného hybridního připojení.

![Architektura sítě centra a paprsků](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

Architektura centra a paprsků se často používá společně s architekturou hybridní sítě a poskytuje centrálně spravované připojení k místnímu prostředí, které je sdílené mezi několika úlohami. V tomto scénáři se veškerý provoz mezi úlohami a místními průchody provádí přes centrum, kde se dá spravovat a zabezpečit.

## <a name="hub-and-spoke-assumptions"></a>Předpoklady centra a paprsků

Implementace virtuální síťové architektury hub a paprsek předpokládá následující:

- Vaše cloudová nasazení budou zahrnovat úlohy hostované v různých pracovních prostředích, jako je vývoj, testování a produkce, které všechny spoléhají na sadu běžných služeb, jako jsou DNS nebo adresářové služby.
- Vaše úlohy nepotřebují vzájemně komunikovat, ale mají společné požadavky na externí komunikaci a sdílené služby.
- Vaše úlohy vyžadují více prostředků, než kolik jich bylo v rámci jednoho předplatného Azure k dispozici.
- Je potřeba poskytnout týmům pro úlohy delegovaná práva pro správu nad svými vlastními prostředky a přitom zachovat centrální kontrolu zabezpečení pro externí připojení.

## <a name="global-hub-and-spoke"></a>Globální střed a paprskový

Architektury hub a paprsků se běžně implementují s virtuálními sítěmi nasazenými do stejné oblasti Azure, aby se minimalizovala latence mezi sítěmi. Velké organizace s globálním dosahem ale můžou potřebovat nasazovat úlohy napříč několika oblastmi za účelem dostupnosti, zotavení po havárii nebo zákonných požadavků. Model hvězdicové lokality může využívat [partnerský vztah globálních virtuálních sítí](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) Azure pro rozšiřování centralizované správy a sdílených služeb napříč oblastmi a podpora úloh distribuovaných po celém světě.

## <a name="learn-more"></a>Další informace

Příklady, jak implementovat sítě rozbočovače a paprsků v Azure, najdete v následujících příkladech v lokalitě referenčních architektur Azure:

- [Implementace síťové topologie centra a paprsků v Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
- [Implementace síťové topologie centra a paprsků se sdílenými službami v Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
