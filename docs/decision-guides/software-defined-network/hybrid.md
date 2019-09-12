---
title: 'Softwarově definované sítě: Hybridní síť'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diskuze o tom, jak hybridní sítě umožňují vašim cloudovým virtuálním sítím připojovat se k místním prostředkům.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 94e285f59442b6632209e1cd6a76c39cfccd337b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829485"
---
# <a name="software-defined-networking-hybrid-network"></a>Softwarově definované sítě: Hybridní síť

Architektura hybridní cloudové sítě umožňuje virtuálním sítím přistupovat k místním prostředkům a službám a naopak pomocí vyhrazeného připojení WAN, jako je ExpressRoute nebo jiná metoda připojení, přímo připojit sítě.

![Hybridní síť](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/expressroute.png)

Při vytváření architektury nativní virtuální sítě v cloudu je hybridní virtuální síť při počátečním vytvoření izolovaná. Přidání připojení k místnímu prostředí uděluje přístup k místní síti i z ní, i když je nutné explicitně povolit veškerý příchozí provoz, který cílí na prostředky ve virtuální síti. Připojení můžete zabezpečit pomocí zařízení virtuální brány firewall a pravidel směrování, abyste omezili přístup, nebo můžete přesně určit, k jakým službám je možné přistupovat mezi těmito dvěma sítěmi pomocí funkcí cloudového nativního směrování nebo nasazení síťových virtuálních zařízení (síťová virtuální zařízení) do Spravujte provoz.

I když hybridní Síťová architektura podporuje připojení VPN, jsou vyhrazená připojení WAN, jako je ExpressRoute, upřednostňovaná kvůli vyššímu výkonu a zvýšenému zabezpečení.

## <a name="hybrid-assumptions"></a>Hybridní předpoklady

Nasazení hybridní virtuální sítě zahrnuje tyto předpoklady:

- Vaše týmy zabezpečení IT zarovnaly místní a cloudové zásady zabezpečení sítě, aby mohly být cloudové virtuální sítě důvěryhodné, aby komunikovaly přímo s místními systémy.
- Vaše cloudové úlohy vyžadují přístup k úložišti, aplikacím a službám hostovaným na místních nebo jiných sítích, nebo vaši uživatelé nebo aplikace v místním prostředí potřebují přístup k prostředkům hostovaným v cloudu.
- Potřebujete migrovat stávající aplikace a služby, které jsou závislé na místních prostředcích, ale nechcete prostředky vysílat na redevelopment, abyste tyto závislosti odstranili.
- Firemní zásady, požadavky na suverenitu dat nebo jiné problémy s dodržováním předpisů nebrání propojení místních sítí k prostředkům cloudu přes síť VPN nebo vyhrazené síti WAN.
- Vaše úlohy nevyžadují více předplatných, aby bylo možné vynechat omezení prostředků předplatného, nebo vaše úlohy zahrnují několik předplatných, ale nevyžadují centrální správu připojení nebo sdílených služeb používaných prostředky rozloženými napříč několik předplatných.

Týmy pro přijetí v cloudu by měly při hledání implementace hybridní virtuální síťové architektury brát v úvahu následující problémy:

- Propojení místních sítí s cloudovou sítí zvyšuje složitost vašich požadavků na zabezpečení. Obě sítě musí být zabezpečené proti externím chybám zabezpečení a neoprávněnému přístupu z obou stran hybridního prostředí.
- Škálování počtu a velikosti úloh v hybridním cloudovém prostředí může výrazně složitou složitost při směrování a správě provozu.
- Budete potřebovat vyvinout kompatibilní zásady správy a řízení přístupu, abyste zachovali konzistentní řízení v celé organizaci.

## <a name="learn-more"></a>Víc se uč

Další informace o hybridních sítích v Azure najdete v těchto tématech:

- [Referenční architektura hybridní sítě](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute). Hybridní virtuální sítě Azure používají okruh ExpressRoute nebo Azure VPN k připojení vaší virtuální sítě k existujícím assetům IT v organizaci, které nejsou hostované v Azure. Tento článek popisuje možnosti vytváření hybridní sítě v Azure.