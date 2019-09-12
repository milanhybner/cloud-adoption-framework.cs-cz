---
title: Hvězdicová síťová topologie
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hvězdicová síťová topologie
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 48f73d7c7f2e7f3bba8183464c786a3e0744807c
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905488"
---
# <a name="hub-and-spoke-network-topology"></a>Hvězdicová síťová topologie

*Hvězdicová architektura* je síťový model pro efektivnější správu běžné komunikace nebo požadavků na zabezpečení. Pomáhá také vyhnout se omezením předplatného Azure. Tento model řeší následující aspekty:

- **Finanční úspora a efektivita správy**. Díky centralizaci služeb, které můžou být sdílené více úlohami, například virtuálními síťovými zařízeními a servery DNS, na jednom místě, může IT minimalizovat prostředky a úsilí vynaložené na správu.
- **Překonání omezení předplatného**. Velké cloudové úlohy můžou vyžadovat použití více prostředků, než je povoleno v rámci jednoho předplatného Azure. (Viz [omezení předplatného][Limits].) Peering úloh virtuálních sítí z různých předplatných do centra může tyto limity překonat.
- **Oddělení oblastí zájmu.** Jednotlivé úlohy můžete nasazovat mezi centrální IT týmy a týmy pro úlohy.

Menší cloudové aktiva nemusí využívat výhody plynoucí z přidané struktury a možností, které tento model nabízí. Pokud však plánujete rozsáhlejší přechod na cloud, měli byste zvážit implementaci hvězdicové síťové architektury, pokud se vás týkají některé z výše uvedených aspektů.

> [!NOTE]
> Lokalita referenčních architektur Azure obsahuje ukázkové šablony, které můžete použít jako základ pro implementaci vlastních sítí s hvězdicovou topologií:
>
> - [Implementace hvězdicové síťové topologie v Azure](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementace hvězdicové síťové topologie se sdílenými službami v Azure](/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Přehled

![Příklady hvězdicové síťová topologie][1]

Jak je znázorněno v diagramu, Azure podporuje dva typy návrhu hvězdicové topologie. Podporuje komunikaci, sdílené prostředky a centralizované zásady zabezpečení („Centrum VNet“ v diagramu), nebo typ virtuální sítě WAN („Virtuální síť WAN“ v diagramu) pro rozsáhlou komunikaci mezi pobočkami a mezi pobočkami a Azure.

Centrum je centrální zóna sítě, která řídí a kontroluje příchozí nebo výchozí provoz mezi zónami: internet, místní síť a paprsky. Hvězdicová topologie poskytuje oddělení IT efektivní způsob, jak vynucovat zásady zabezpečení v centrálním umístění. Také snižuje riziko neoprávněné konfigurace a vystavení hrozbám.

Centrum často obsahuje společné komponenty služby, které využívají paprsky. Mezi běžné centrální služby patří například:

- Infrastruktura Windows Server Active Directory, která je vyžadována pro ověřování uživatelů třetích stran, kteří získávají přístup z nedůvěryhodných sítí předtím, než získají přístup k úlohám v paprsku. Včetně související služby Active Directory Federation Services (AD FS).
- Služba DNS pro překlad názvů pro úlohy v paprscích, pro přístup k prostředkům v místní síti a na internetu, pokud se nepoužívá [Azure DNS][DNS].
- Infrastruktura veřejných klíčů (PKI) pro implementaci jednotného přihlašování k úlohám.
- Řízení toku provozu TCP a UDP mezi síťovými zónami v paprscích a internetem.
- Řízení toku mezi paprsky a místní sítí.
- V případě potřeby řízení toku mezi jednotlivými paprsky.

Pomocí infrastruktury sdíleného centra, které podporuje více paprsků, můžete minimalizovat redundanci, zjednodušit správu a snížit celkové náklady.

Role jednotlivých paprsků může být hostitelem různých typů úloh. Paprsky také poskytují modulární přístup pro opakovaná nasazení stejných úloh. Příklady jsou dev and test, testování přijetím uživatelů, fázování a produkce.

Paprsky můžou také oddělit a povolit různé skupiny v rámci vaší organizace. Příkladem jsou skupiny Azure DevOps. V rámci paprsku je možné nasadit základní úlohy nebo složité vícevrstvé úlohu s řízením provozu mezi vrstvami.

## <a name="subscription-limits-and-multiple-hubs"></a>Omezení předplatného a více center

V Azure je každá komponenta bez ohledu na typ nasazená v předplatném Azure. Izolace komponent Azure v různých předplatných Azure může uspokojit požadavky různých oborů podnikání, jako je například nastavení odlišných úrovní přístupu a autorizace.

Jednoduchá implementace hvězdicové topologie může škálovat velký počet paprsků. Ale jako u každého IT systému existují i zde omezení platformy. Nasazení centra je vázáno na konkrétní předplatné Azure, pro které platí omezení a limity. (Příkladem je maximální počet peeringů virtuálních sítí. Podrobnosti naleznete v tématu [Limity, kvóty a omezení předplatného a služeb Azure][Limits].)

V případech, kdy omezení můžou být problémem, můžete architekturu dále škálovat rozšířením modelu jednoduché hvězdicové topologie na cluster sítí s hvězdicovou topologií. Pomocí peeringu virtuálních sítí, Azure ExpressRoute, virtuální sítě WAN nebo sítě S2S VPN můžete propojit více center v jedné nebo několika oblastech Azure.

![Cluster sítí s hvězdicovou topologií][2]

Zavedení více center zvyšuje náklady a nároky na správu systému. To je možné odůvodnit pouze škálovatelností, systémovými limity nebo redundancí a regionální replikací potřebnými pro výkon uživatele nebo zotavení po havárii. Ve scénářích, které vyžadují více center, by se všechna centra měla snažit nabídnout stejnou sadu služeb kvůli snadné obsluze.

## <a name="interconnection-between-spokes"></a>Propojení mezi paprsky

Je možné implementovat komplexní vícevrstvé úlohy v jednom paprsku. Konfigurace s více vrstvami můžete implementovat použitím podsítí (jedna pro každou vrstvu) ve stejné virtuální síti a filtrováním toku pomocí skupin zabezpečení sítě.

Architekt může chtít nasadit vícevrstvé úlohy napříč několika virtuálními sítěmi. Pomocí peeringu virtuálních sítí se paprsky můžou připojit k ostatním paprskům ve stejném centru nebo v jiných centrech.

Typickým příkladem tohoto scénáře je případ, kdy se servery pro zpracování aplikací nacházejí v jednom paprsku nebo virtuální síti. Databáze se nasadí v jiném paprsku nebo virtuální síti. V takovém případě je snadné propojit paprsky pomocí peeringu virtuálních sítí a vyhnout se tak přenosu přes centrum. Řešením je provést pečlivou kontrolu architektury a zabezpečení, abyste zajistili, že obejití centra neobejde důležité body zabezpečení nebo auditu, které mohou existovat pouze v centru.

![Propojení paprsků k sobě navzájem a k centru][3]

Paprsky je taky možné propojit s paprskem, který funguje jako centrum. Tento přístup vytvoří hierarchii se dvěma úrovněmi: paprsek na vyšší úrovni (úroveň 0) se změní na centrum pro paprsky nižší úrovně (úroveň 1) v hierarchii. Pro přesměrování provozu do centra se vyžadují paprsky implementace hvězdicové topologie, aby provoz mohl být směrován na místo určení v místní síti nebo veřejném internetu. Architektura se dvěma úrovněmi center přináší složité směrování, které odstraňuje výhody jednoduché hvězdicové topologie.

<!-- images -->

[0]: ./images/network-redundant-equipment.png "Příklady překrytí komponent"
[1]: ./images/network-hub-spoke-high-level.png "Příklad vysoké úrovně hvězdicové topologie"
[2]: ./images/network-hub-spokes-cluster.png "Cluster sítí s hvězdicovou topologií"
[3]: ./images/network-spoke-to-spoke.png "Propojení mezi paprsky"
[4]: ./images/network-hub-spoke-block-level-diagram.png "Diagram na úrovni bloku hvězdicové topologie"
[5]: ./images/network-users-groups-subsciptions.png "Uživatelé, skupiny, předplatná a projekty"
[6]: ./images/network-infrastructure-high-level.png "Diagram vysoké úrovně infrastruktury"
[7]: ./images/network-highlevel-perimeter-networks.png "Diagram vysoké úrovně infrastruktury"
[8]: ./images/network-vnet-peering-perimeter-neworks.png "Peering virtuálních sítí a hraniční sítě"
[9]: ./images/network-high-level-diagram-monitoring.png "Diagram vysoké úrovně pro monitorování"
[10]: ./images/network-high-level-workloads.png "Diagram vysoké úrovně pro úlohu"

<!-- links -->

[Limits]: /azure/azure-subscription-service-limits
[Roles]: /azure/role-based-access-control/built-in-roles
[VNet]: /azure/virtual-network/virtual-networks-overview
[network-security-groups]: /azure/virtual-network/virtual-networks-nsg
[DNS]: /azure/dns/dns-overview
[PrivateDNS]: /azure/dns/private-dns-overview
[VNetPeering]: /azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: /azure/virtual-network/virtual-networks-udr-overview
[RBAC]: /azure/role-based-access-control/overview
[azure-ad]: /azure/active-directory/active-directory-whatis
[VPN]: /azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: /azure/expressroute/expressroute-introduction
[ExRD]: /azure/expressroute/expressroute-erdirect-about
[vWAN]: /azure/virtual-wan/virtual-wan-about
[NVA]: /azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: /azure/firewall/overview
[SubMgmt]: /azure/architecture/cloud-adoption/appendix/azure-scaffold
[RGMgmt]: /azure/azure-resource-manager/resource-group-overview
[DMZ]: /azure/best-practices-network-security
[ALB]: /azure/load-balancer/load-balancer-overview
[PIP]: /azure/virtual-network/resource-groups-networking#public-ip-address
[AFD]: /azure/frontdoor/front-door-overview
[AppGW]: /azure/application-gateway/application-gateway-introduction
[WAF]: /azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: /azure/monitoring-and-diagnostics/
[ActLog]: /azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: /azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: /azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: /azure/operations-management-suite/operations-management-suite-overview
[NPM]: /azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: /azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: /azure/app-service/
[HDI]: /azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: /azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: /azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: /azure/traffic-manager/traffic-manager-overview
