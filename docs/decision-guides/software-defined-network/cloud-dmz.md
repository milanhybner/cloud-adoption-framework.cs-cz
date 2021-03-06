---
title: 'Softwarově definované sítě: Cloud DMZ'
description: Přečtěte si o architektuře Cloud DMZ Network, která umožňuje omezený přístup mezi místními a cloudovou sítí pomocí sítě VPN.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 63d882aefab6488b05e7f0aec506c2e371d9464e
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80431307"
---
# <a name="software-defined-networking-cloud-dmz"></a>Softwarově definované sítě: Cloud DMZ

Architektura sítě Cloud DMZ umožňuje omezený přístup mezi místními i cloudovou sítí, a to pomocí virtuální privátní sítě (VPN) pro připojení sítí. I když se model DMZ běžně používá v případě, že chcete zabezpečit externí přístup k síti, architektura cloudových DMZ, kterou popisuje tady, je určená konkrétně k zabezpečení přístupu k místní síti z cloudových prostředků a naopak.

![Zabezpečení hybridní síťové architektury](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/images/dmz-private.png)

Tato architektura je navržená tak, aby podporovala scénáře, ve kterých vaše organizace chce zahájit integraci cloudových úloh s místními úlohami, ale nemusí mít plně prozatímované zásady zabezpečení cloudu nebo nezískaly zabezpečené vyhrazené připojení WAN mezi Tato dvě prostředí. V důsledku toho by se měly cloudové sítě zacházet jako demilitarizovaná zóna, aby byly místní služby zabezpečené.

DMZ nasadí síťová virtuální zařízení (síťová virtuální zařízení), aby implementovala funkce zabezpečení, jako jsou brány firewall a kontrola paketů. Přenos mezi místními a cloudovou aplikací nebo službami musí projít DMZ, kde se dá auditovat. Připojení k síti VPN a pravidla určující, jaký provoz je povolený prostřednictvím sítě DMZ, jsou čistě řízeny bezpečnostními týmy IT.

## <a name="cloud-dmz-assumptions"></a>Předpoklady cloudu DMZ

Nasazení cloudového DMZ zahrnuje tyto předpoklady:

- Vaše týmy zabezpečení neodpovídaly plně místním a cloudovým požadavkům na zabezpečení a zásadám.
- Vaše cloudové úlohy vyžadují přístup k omezené podmnožině služeb hostovaných na místních nebo jiných sítích, nebo uživatelé nebo aplikace v místním prostředí potřebují omezený přístup k prostředkům hostovaným v cloudu.
- Implementace připojení VPN mezi místními sítěmi a poskytovatelem cloudu nebrání podnikovým zásadám, zákonovým požadavkům ani problémům s technickými problémy s kompatibilitou.
- Vaše úlohy nevyžadují více předplatných, aby bylo možné obejít omezení prostředků předplatného, nebo zahrnuje několik předplatných, ale nevyžaduje centrální správu připojení nebo sdílených služeb používaných prostředky rozloženými mezi více odběru.

Při hledání implementace virtuální síťové architektury cloudové DMZ by týmy pro přijetí v cloudu měly brát v úvahu následující problémy:

- Propojení místních sítí s cloudovou sítí zvyšuje složitost vašich požadavků na zabezpečení. I když jsou připojení mezi cloudovou sítí a místním prostředím zabezpečená, je stále potřeba zajistit zabezpečení cloudových prostředků. Všechny veřejné IP adresy vytvořené pro přístup ke cloudovým úlohám musí být správně zabezpečené pomocí [veřejné DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) nebo [Azure firewall](https://docs.microsoft.com/azure/firewall).
- Architektura cloudu DMZ se běžně používá jako krokování, zatímco připojení je dál zabezpečené a zarovnává se bezpečnostní zásady mezi místními a cloudovou sítí a umožňuje širší přijetí hybridní síťové architektury s plnou škálou. Může se ale vztahovat i na izolovaná nasazení s konkrétními požadavky na zabezpečení, identitu a připojení, které DMZ přístup ke cloudu.

## <a name="learn-more"></a>Další informace

Další informace o implementaci cloudového DMZu v Azure najdete v tématech:

- [Implementujte DMZ mezi Azure a vaším](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid)místním datovým centrem. Tento článek popisuje, jak implementovat zabezpečenou hybridní síťovou architekturu v Azure.
