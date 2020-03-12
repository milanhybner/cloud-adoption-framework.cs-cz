---
title: Hvězdicová síťová topologie
description: Seznamte se s topologií sítě rozbočovače a paprsků pro efektivnější správu běžných požadavků na komunikaci nebo zabezpečení.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: a2827273aa3fd28478c2615610f74f32b155a299
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092591"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs -->

# <a name="hub-and-spoke-network-topology"></a>Hvězdicová síťová topologie

*Hvězdicová architektura* je síťový model pro efektivnější správu běžné komunikace nebo požadavků na zabezpečení. Pomáhá také vyhnout se omezením předplatného Azure. Tento model řeší následující aspekty:

- **Finanční úspora a efektivita správy**. Díky centralizaci služeb, které můžou být sdílené více úlohami, například virtuálními síťovými zařízeními a servery DNS, na jednom místě, může IT minimalizovat prostředky a úsilí vynaložené na správu.
- **Překonání omezení předplatného**. Velké cloudové úlohy můžou vyžadovat použití více prostředků, než je povoleno v rámci jednoho předplatného Azure. Peering úloh virtuálních sítí z různých předplatných do centra může tyto limity překonat. Další informace najdete v tématu [omezení předplatného](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Oddělení oblastí zájmu.** Jednotlivé úlohy můžete nasazovat mezi centrální IT týmy a týmy pro úlohy.

Menší cloudové aktiva nemusí využívat výhody plynoucí z přidané struktury a možností, které tento model nabízí. Ale větší úsilí při přijetí cloudu by mělo zvážit implementaci síťové architektury hvězdicové a Paprskové sítě, pokud mají některé z výše uvedených otázek.

> [!NOTE]
> Lokalita referenčních architektur Azure obsahuje příklady šablon, které můžete použít jako základ pro implementaci vlastních sítí s rozbočovačem a paprsky:
>
> - [Implementace síťové topologie centra a paprsků v Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementace síťové topologie centra a paprsků se sdílenými službami v Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Přehled

![Příklady síťové topologie centra a paprsků][1]

Jak je znázorněno v diagramu, Azure podporuje dva typy centrálního a paprskového návrhu. Podporuje komunikaci, sdílené prostředky a centralizované zásady zabezpečení („Centrum VNet“ v diagramu), nebo typ virtuální sítě WAN („Virtuální síť WAN“ v diagramu) pro rozsáhlou komunikaci mezi pobočkami a mezi pobočkami a Azure.

Centrum je centrální zóna sítě, která řídí a kontroluje příchozí nebo výchozí provoz mezi zónami: internet, místní síť a paprsky. Topologie centra a paprsků dává vašemu oddělení IT účinný způsob, jak vynutilit zásady zabezpečení v centrálním umístění. Také snižuje riziko neoprávněné konfigurace a vystavení hrozbám.

Centrum často obsahuje společné komponenty služby, které využívají paprsky. Mezi běžné centrální služby patří například:

- Infrastruktura Windows Server Active Directory, která je vyžadována pro ověřování uživatelů třetích stran, kteří získávají přístup z nedůvěryhodných sítí předtím, než získají přístup k úlohám v paprsku. Včetně související služby Active Directory Federation Services (AD FS).
- Služba DNS pro překlad názvů pro úlohy v paprscích, pro přístup k prostředkům v místní síti a na internetu, pokud se nepoužívá [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview).
- Infrastruktura veřejných klíčů (PKI) pro implementaci jednotného přihlašování k úlohám.
- Řízení toku provozu TCP a UDP mezi síťovými zónami v paprscích a internetem.
- Řízení toku mezi paprsky a místní sítí.
- V případě potřeby řízení toku mezi jednotlivými paprsky.

Pomocí infrastruktury sdíleného centra, které podporuje více paprsků, můžete minimalizovat redundanci, zjednodušit správu a snížit celkové náklady.

Role jednotlivých paprsků může být hostitelem různých typů úloh. Paprsky také poskytují modulární přístup pro opakovaná nasazení stejných úloh. Příklady jsou dev and test, testování přijetím uživatelů, fázování a produkce.

Paprsky můžou také oddělit a povolit různé skupiny v rámci vaší organizace. Příkladem jsou skupiny Azure DevOps. V rámci paprsku je možné nasadit základní úlohy nebo složité vícevrstvé úlohu s řízením provozu mezi vrstvami.

## <a name="subscription-limits-and-multiple-hubs"></a>Omezení předplatného a více center

V Azure je každá komponenta bez ohledu na typ nasazená v předplatném Azure. Izolace komponent Azure v různých předplatných Azure může uspokojit požadavky různých oborů podnikání, jako je například nastavení odlišných úrovní přístupu a autorizace.

Jednoduchá implementace hub a paprsků se dá škálovat až na velký počet paprsků. Ale jako u každého IT systému existují i zde omezení platformy. Nasazení centra je vázáno na konkrétní předplatné Azure, pro které platí omezení a limity. Jedním z příkladů je maximální počet partnerských vztahů virtuálních sítí. Další informace najdete v tématu [Limity, kvóty a omezení předplatného a služeb Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).

V případech, kdy omezení můžou být problémem, můžete architekturu dále škálovat rozšířením modelu jednoduché hvězdicové topologie na cluster sítí s hvězdicovou topologií. Pomocí peeringu virtuálních sítí, Azure ExpressRoute, virtuální sítě WAN nebo sítě S2S VPN můžete propojit více center v jedné nebo několika oblastech Azure.

![Cluster sítí s hvězdicovou topologií][2]

Zavedení více center zvyšuje náklady a nároky na správu systému. To je možné odůvodnit pouze škálovatelností, systémovými limity nebo redundancí a regionální replikací potřebnými pro výkon uživatele nebo zotavení po havárii. Ve scénářích, které vyžadují více center, by se všechna centra měla snažit nabídnout stejnou sadu služeb kvůli snadné obsluze.

## <a name="interconnection-between-spokes"></a>Propojení mezi paprsky

Je možné implementovat komplexní vícevrstvé úlohy v jednom paprsku. Konfigurace s více vrstvami můžete implementovat použitím podsítí (jedna pro každou vrstvu) ve stejné virtuální síti a filtrováním toku pomocí skupin zabezpečení sítě.

Architekt může chtít nasadit vícevrstvé úlohy napříč několika virtuálními sítěmi. Pomocí peeringu virtuálních sítí se paprsky můžou připojit k ostatním paprskům ve stejném centru nebo v jiných centrech.

Typickým příkladem tohoto scénáře je případ, kdy se servery pro zpracování aplikací nacházejí v jednom paprsku nebo virtuální síti. Databáze se nasadí v jiném paprsku nebo virtuální síti. V takovém případě je snadné propojit paprsky pomocí peeringu virtuálních sítí a vyhnout se tak přenosu přes centrum. Řešením je provést pečlivou architekturu a kontrolu zabezpečení, abyste zajistili, že vynechání centra neobejde důležité zabezpečení nebo body auditování, které mohou existovat pouze v centru.

![Propojení paprsků k sobě navzájem a k centru][3]

Paprsky je taky možné propojit s paprskem, který funguje jako centrum. Tento přístup vytvoří hierarchii se dvěma úrovněmi: paprsek na vyšší úrovni (úroveň 0) se změní na centrum pro paprsky nižší úrovně (úroveň 1) v hierarchii. K přenosu provozu do centrálního centra se vyžadují paprsky s implementací rozbočovače a paprsku, aby se přenos mohl směrovat do svého cíle v místní síti nebo veřejné síti Internet. Architektura se dvěma úrovněmi Center přináší složité směrování, které odstraňuje výhody jednoduchého hvězdicové vztahu.

<!-- images -->

[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Příklad vysoké úrovně hvězdicové topologie"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Cluster sítí s hvězdicovou topologií"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Propojení mezi paprsky"
