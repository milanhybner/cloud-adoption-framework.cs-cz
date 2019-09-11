---
title: Průvodce rozhodováním ohledně softwarově definovaných sítí
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se se softwarově definovanými sítěmi jako základní službou při migraci do Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ac8d65ab897ddeac94305c9d2c365281808b36c3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817957"
---
# <a name="software-defined-networking-decision-guide"></a>Průvodce rozhodováním ohledně softwarově definovaných sítí

Softwarově definované sítě představují síťovou architekturu, která umožňuje funkce virtualizovaných sítí, které je možné centrálně spravovat, konfigurovat a upravovat prostřednictvím softwaru. Softwarově definované sítě umožňují vytvářet cloudové sítě s využitím virtualizovaných ekvivalentů fyzických směrovačů, bran firewall a dalších síťových zařízení, která se používají v místních sítích. Softwarově definované sítě jsou důležité pro vytváření zabezpečených virtuálních sítí na veřejných cloudových platformách, jako je Azure.

## <a name="networking-decision-guide"></a>Průvodce rozhodováním ohledně sítí

![Diagram možností sítí od nejjednodušších po nejsložitější, které odpovídají rychlým odkazům níže](../../_images/discovery-guides/discovery-guide-sdn.png)

Přejít na: [Jenom PaaS](paas-only.md) | [Model nativní pro cloud](cloud-native.md) | [DMZ v cloudu](cloud-dmz.md) [Hybridní model](hybrid.md) | [Model hvězdicové architektury](hub-spoke.md) | [Další informace](#learn-more)

Softwarově definované sítě poskytují několik možností s různými úrovněmi cen a složitosti. Ve výše uvedeném průvodci zjišťováním najdete odkaz, na kterém si můžete tyto možnosti rychle přizpůsobit tak, aby co nejlépe vyhovovaly konkrétním obchodním a technologických strategiím.

Inflexní bod v tomto průvodci závisí na několika klíčových rozhodnutích, která váš tým cloudové strategie učinil ještě před tím, než se začal zabývat rozhodováním o síťové architektuře. Mezi nejdůležitější patří rozhodnutí ohledně [definice digitálních aktiv](../../digital-estate/index.md) a [návrhu předplatného](../subscriptions/index.md) (která také můžou vyžadovat informace z dřívějších rozhodnutí v souvislosti s účtováním cloudu a strategií na globálním trhu).

U malých nasazení v jedné oblasti s méně než 1 000 virtuálních počítačů je menší pravděpodobnost výrazného ovlivnění tímto inflexním bodem. Naopak rozsáhlá úsilí o přechod s více než 1 000 virtuálních počítačů, několika obchodními jednotkami nebo na několika geopolitických trzích může vaše rozhodnutí ohledně softwarově definovaných sítí a tento klíčový inflexní bod ovlivnit podstatným způsobem.

## <a name="choosing-the-right-virtual-networking-architectures"></a>Výběr správných architektur virtuálních sítí

Tato část navazuje na průvodce rozhodováním a měla by vám pomoct zvolit správné architektury virtuálních sítí.

Implementovat technologie softwarově definovaných sítí a vytvářet cloudové virtuální sítě můžete mnoha způsoby. Strukturování virtuálních sítí pro vaši migraci a způsob, jakým tyto sítě budou komunikovat s vaší stávající IT infrastrukturou, bude záviset na kombinaci požadavků úloh a požadavků vašich zásad správného řízení.

Při plánování, kterou architekturu virtuálních sítí nebo kombinaci architektur byste měli zvážit při plánování migrace do cloudu, si položte následující otázky, které vám pomůžou určit, co je pro vaši organizaci nejvhodnější:

| Otázka | Jenom PaaS | Model nativní pro cloud | DMZ v cloudu | Hybridní | Hvězdicová architektura |
|-----|-----|-----|-----|-----|-----|
| Bude vaše úloha využívat pouze služby PaaS a nebude vyžadovat jiné možnosti připojení, než které poskytují tyto služby? | Ano | Ne | Ne | Ne | Ne |
| Vyžaduje vaše úloha integraci s místními aplikacemi? | Ne | Ne | Ano | Ano | Ano |
| Vytvořili jste vyspělé zásady zabezpečení a zabezpečené připojení mezi místními a cloudovými sítěmi? | Ne | Ne | Ne | Ano | Ano |
| Vyžaduje vaše úloha ověřovací služby, které nepodporují cloudové služby identit, nebo potřebujete přímý přístup k místním řadičům domény? | Ne | Ne | Ne | Ano | Ano |
| Budete potřebovat nasadit a spravovat velký počet virtuálních počítačů a úloh? | Ne | Ne | Ne | Ne | Ano |
| Budete potřebovat zajistit centrální správu a možnosti připojení k místnímu prostředí, zatímco budete delegovat kontrolu nad prostředky týmům jednotlivých úloh? | Ne | Ne | Ne | Ne | Ano |

## <a name="virtual-networking-architectures"></a>Architektury virtuálních sítí

Další informace o hlavních architekturách softwarově definovaných sítí:

- **[Jenom PaaS](paas-only.md):** Většina produktů PaaS (platforma jako služba) podporuje omezenou sadu integrovaných síťových funkcí a k zajištění podpory požadavků úloh nemusí vyžadovat explicitně softwarově definované sítě.
- **[Model nativní pro cloud](cloud-native.md):** Nativní cloudová architektura podporuje cloudové úlohy prostřednictvím virtuálních sítí využívajících výchozí softwarově definované síťové možnosti cloudové platformy a nezávislých na místních nebo jiných externích prostředcích.
- **[DMZ v cloudu](cloud-dmz.md):** Podporuje omezené možnosti připojení mezi místními a cloudovými sítěmi. Zabezpečení těchto připojení zajišťuje implementace zóny DMZ, která pečlivě kontroluje provoz mezi těmito dvěma prostředími.
- **[Hybridní model](hybrid.md):** Architektura hybridních cloudových sítí umožňuje přístup z virtuálních sítí v důvěryhodných cloudových prostředích k místním prostředkům a naopak.
- **[Hvězdicová architektura](hub-spoke.md):** Hvězdicová architektura umožňuje centrálně spravovat externí připojení a sdílené služby, izolovat jednotlivé úlohy a překonávat případná omezení předplatného.

## <a name="learn-more"></a>Další informace

Další informace o softwarově definovaných sítích v Azure najdete tady:

- [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview). Základní funkce softwarově definovaných sítí v Azure zajišťuje služba Azure Virtual Network, která funguje jako cloudová obdoba fyzických místních sítí. Virtuální sítě fungují také jak výchozí hranice izolace mezi prostředky na platformě.
- [Osvědčené postupy Azure pro zabezpečení sítě](/azure/security/azure-security-network-security-best-practices). Doporučení od týmu zabezpečení Azure ke konfiguraci virtuálních sítí za účelem minimalizace ohrožení zabezpečení.

## <a name="next-steps"></a>Další kroky

Softwarově definované sítě jsou pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)