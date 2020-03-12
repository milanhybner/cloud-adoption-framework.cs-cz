---
title: Sítě perimetru
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak efektivně nastavit Azure pro vaši organizaci.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: cbf77bad65753d219e3a0a53f300aee3690b001d
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093237"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs WAFs -->

# <a name="perimeter-networks"></a>Sítě perimetru

[Hraniční sítě][perimeter-network] umožňují zabezpečené připojení mezi cloudovými sítěmi a vašimi místními sítěmi nebo fyzickými sítěmi datacentra, spolu s internetovým připojením. Označují se také jako demilitarizované zóny (zóny DMZ).

Aby hraniční sítě byly účinné, musí příchozí pakety projít přes bezpečnostní zařízení hostovaná v zabezpečených podsítích předtím, než jsou odeslány na back-endové servery. Jako příklady je možné uvést brány firewall, systémy zjišťování neoprávněných vniknutí (IDS) a systémy ochrany před neoprávněnými vniknutími (IPS). Předtím, než síť opustí, by bezpečnostními zařízeními v hraniční síti měly projít také internetové pakety z úloh. Účelem tohoto toku je vynucování zásad, kontrola a auditování.

Hraniční sítě využívají následující funkce a služby Azure:

- [Virtuální sítě][virtual-networks], [trasy definované uživatelem][user-defined-routes] a [skupiny zabezpečení sítě][network-security-groups]
- [Síťová virtuální zařízení (síťová virtuální zařízení)][NVA]
- [Nástroj pro vyrovnávání zatížení Azure][ALB]
- [Azure Application Gateway][AppGW] a [Firewall webových aplikací (WAF)][AppGWWAF]
- [Veřejné IP adresy][PIP]
- [Azure Front Door Service][AFD] s [firewallem webových aplikací][AFDWAF]
- [Azure Firewall][AzFW]

> [!NOTE]
> Referenční architektury Azure poskytují ukázkové šablony, které můžete použít k implementaci vlastních hraničních sítí:
>
> - [Implementace hraniční sítě mezi Azure a vaším místním datovým centrem](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid)
> - [Implementace DMZ mezi Azure a internetem](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Za definování požadavků pro provoz hraničních sítí obvykle zodpovídají centrální tým IT a tým zabezpečení.

![Příklad síťové topologie centra a paprsků](../../_images/azure-best-practices/network-high-level-perimeter-networks.png)

Výše uvedený diagram znázorňuje ukázkovou [síťovou topologii rozbočovače a paprsku](./hub-spoke-network-topology.md) , která implementuje vynucování dvou hraničních zařízení s přístupem k Internetu a místní sítí. Obě hranice se nacházejí v centru DMZ. V centru DMZ se hraniční síť pro přístup k internetu může škálovat, aby podporovala řadu obchodních aplikací. Ke škálování slouží několik farem WAF a instancí Azure Firewall, které pomáhají chránit paprskové virtuální sítě. Podle potřeby centrum taky umožňuje připojení prostřednictvím sítě VPN nebo Azure ExpressRoute.

## <a name="virtual-networks"></a>Virtuální sítě

Hraniční sítě se obvykle vytvářejí pomocí [virtuální sítě][virtual-networks] s několika podsítěmi hostujícími různé typy služeb, které filtrují a kontrolují internetový provoz přes síťová virtuální zařízení, firewally webových aplikací a instance Azure Application Gateway.

## <a name="user-defined-routes"></a>Trasy definované uživatelem

Pomocí [uživatelem definovaných tras][user-defined-routes] můžou zákazníci nasazovat brány firewall, systémy IDS/IPS a další virtuální zařízení. Zákazníci pak můžou směrovat síťový provoz přes tato bezpečnostní zařízení a vynucovat tak zásady zabezpečení hranic a provádět auditování a kontrolu. Uživatelem definované trasy můžou být vytvořeny, aby bylo zaručeno, že provoz prochází určenými vlastními virtuálními počítači, firewally webových aplikací a nástroji pro vyrovnávání zatížení.

V příkladu sítě typu centrum a paprsky zaručujete, že provoz generovaný virtuálními počítači, které se nacházejí v paprskech, projde správnými virtuálními zařízeními v centru, vyžaduje trasu definovanou uživatelem, která je definovaná v podsítích paprsku. Tato trasa nastaví front-end IP adresu interního nástroje pro vyrovnávání zatížení jako další segment směrování. Interní nástroj pro vyrovnávání zatížení distribuuje interní provoz na virtuální zařízení (back-endový fond nástroje pro vyrovnávání zatížení).

## <a name="azure-firewall"></a>Azure Firewall

[Azure Firewall][AzFW] je spravovaná cloudová služba, která chrání vaše prostředky ve virtuálních sítích Azure. Jde o plně stavovou spravovanou bránu firewall s integrovanou vysokou dostupností a neomezenou cloudovou škálovatelností. Můžete centrálně vytvářet, vynucovat a protokolovat zásady připojení k aplikacím a sítím napříč různými předplatnými a virtuálními sítěmi.

Azure Firewall používá pro prostředky virtuální sítě statickou veřejnou IP adresu. Externí brány firewall díky tomu můžou identifikovat provoz pocházející z vaší virtuální sítě. Tato služba spolupracuje se službou Azure Monitor zajišťující protokolování a analýzy.

## <a name="network-virtual-appliances"></a>Síťová virtuální zařízení

Hraniční sítě s přístupem k internetu se obvykle spravují prostřednictvím instance služby Azure Firewall, farmy bran firewall nebo [firewally webových aplikací][AFDWAF].

Různé obchodní aplikace běžně využívají mnoho webových aplikací. Tyto aplikace často bývají postiženy ohroženími zabezpečení a potenciálními zneužitími. Firewall webových aplikací detekuje útoky proti webovým aplikacím (HTTP/HTTPS) více do hloubky než obecné brány firewall. V porovnání s tradiční technologií brány firewall mají firewally webových aplikací sadu specifických funkcí, které chrání interní webové servery před hrozbami.

Instalace služby Azure Firewall a brána firewall [síťového virtuálního zařízení][NVA] používají společnou rovinu správy se sadou pravidel zabezpečení, která pomáhají chránit úlohy hostované v paprscích a řídit přístup k místním sítím. Azure Firewall má vestavěnou škálovatelnost, zatímco brány firewall síťových virtuálních zařízení se dají ručně škálovat za nástrojem pro vyrovnávání zatížení.

Farma bran firewall obvykle má v porovnání s WAF méně specializovaný software, má však širší obor aplikací k filtrování a kontrole libovolného typu provozu v odchozích i příchozích přenosech. Pokud používáte síťová virtuální zařízení, můžete najít a nasadit software z Azure Marketplace.

Pro přenosy, které pocházejí z internetu, použijte jednu sadu instancí Azure Firewall (nebo síťová virtuální zařízení) a jinou sadu pro provoz pocházející z místních sítí. Použití jenom jedné sady bran firewall pro oba typy přenosů představuje bezpečnostní riziko, protože mezi těmito dvěma sadami síťových přenosů neexistuje žádná bezpečnostní hranice. Použitím samostatných vrstev bran firewall se snižuje složitost pravidel pro kontrolu zabezpečení a zlepšuje se přehled o tom, která pravidla platí pro jednotlivé příchozí žádosti v síti.

## <a name="azure-load-balancer"></a>Nástroj pro vyrovnávání zatížení Azure

[Azure Load Balancer][ALB] nabízí službu s vysokou dostupností vrstvy 4 (TCP/UDP), která může distribuovat příchozí provoz mezi instancemi služby definovanými v sadě pro vyrovnávání zatížení. Provoz odeslaný do nástroje pro vyrovnávání zatížení z front-endových koncových bodů (koncových bodů veřejných IP adres nebo koncových bodů privátních IP adres) se dá předistribuovat s překladem adresy do fondu back-endových IP adres (například síťová virtuální zařízení nebo virtuální počítače) nebo bez něj.

Azure Load Balancer může také zkoumat stav různých instancí serveru. Pokud instance na test stavu nereaguje, nástroj pro vyrovnávání zatížení zastaví odesílání provozu na instanci serveru, která není v pořádku.

Jako příklad použití síťové topologie centra a paprsků můžete nasadit externí nástroj pro vyrovnávání zatížení do středu i paprsků. Nástroj pro vyrovnávání zatížení v centru efektivně směruje provoz do služeb v paprscích. Nástroje pro vyrovnávání zatížení v paprscích spravují provoz aplikací.

## <a name="azure-front-door-service"></a>Azure Front Door Service

Služba [Azure Front Door Service][AFD] je vysoce dostupná a škálovatelná platforma Microsoftu pro zrychlení webových aplikací a globální nástroj pro vyrovnávání zatížení HTTPS. Službu Azure Front Door Service můžete použít k sestavení, provozování a škálování dynamické webové aplikace a statického obsahu. Běží na více než 100 umístěních na okraji globální sítě Microsoftu.

Služba Azure Front Door Service zajišťuje pro vaši aplikaci jednotnou automatizaci údržby razítek v různých oblastech, automatizaci BCDR, jednotné informace o klientech a uživatelích, ukládání do mezipaměti a přehledy služeb. Tato platforma nabízí výkon, spolehlivost a podporu SLA. Nabízí také certifikaci dodržování předpisů a auditovatelné postupy zabezpečení, které jsou vyvíjeny, provozovány a nativně podporovány v Azure.

## <a name="application-gateway"></a>Application Gateway

[Azure Application Gateway][AppGW] je vyhrazené virtuální zařízení poskytující spravovaný kontroler doručování aplikací (ADC) jako službu. Vaší aplikaci nabízí různé možnosti vyrovnávání zatížení vrstvy 7.

Application Gateway umožňuje optimalizovat produktivitu webové farmy tím, že se ukončování protokolu SSL, které je náročné na CPU, přesměruje na aplikační bránu. Nabízí také další možnosti přesměrování vrstvy 7, jako je kruhové dotazování na distribuci příchozích přenosů, spřažení relací na základě souborů cookie, přesměrování založené na cestách URL a možnost hostování několika webů za jedinou službou Application Gateway.

WAF SKU služby Application Gateway zahrnuje bránu firewall webových aplikací. Tato SKU poskytuje ochranu webových aplikací před běžnými ohroženími zabezpečení webu a zneužitím. Application Gateway můžete nakonfigurovat jako internetovou bránu nebo jen jako interní bránu, případně jako kombinaci obojího.

## <a name="public-ips"></a>Veřejné IP adresy

Pomocí některých funkcí Azure můžete přidružit koncové body služby k [veřejné IP][PIP] adrese, aby byl váš prostředek přístupný z internetu. Tento koncový bod používá překlad adres (NAT) ke směrování provozu na interní adresu a port ve virtuální síti Azure. Tato cesta je primárním způsobem, jak externí provoz předat do virtuální sítě. Konfigurace veřejné IP adresy vám umožní zjistit, jaký provoz se předává, a jak a kde se převede do virtuální sítě.

## <a name="azure-ddos-protection-standard"></a>Azure DDoS Protection Standard

Služba [Azure DDoS Protection Standard][DDoS] poskytuje další funkce pro zmírnění rizik oproti vrstvě [Basic][DDoS] této služby, které jsou vyladěny konkrétně pro prostředky virtuální sítě Azure. Služba DDoS Protection Standard se snadno povoluje a nevyžaduje žádné změny aplikací.

Zásady ochrany můžete ladit prostřednictvím vyhrazeného monitorování provozu a algoritmů strojového učení. Zásady se aplikují na veřejné IP adresy přidružené k prostředkům nasazeným ve virtuálních sítích. Příklady jsou Azure Load Balancer, Azure Application Gateway a instance služby Azure Service Fabric.

Prostřednictvím zobrazení Azure Monitor je k dispozici telemetrie v reálném čase, a to jak během útoku, tak pro historické účely. Pomocí firewallu webových aplikací v Azure Application Gateway můžete přidat ochranu na úrovni aplikací. Jsou chráněny veřejné IP adresy IPv4 Azure.

<!-- links -->

[virtual-networks]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[perimeter-network]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[AppGWWAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
