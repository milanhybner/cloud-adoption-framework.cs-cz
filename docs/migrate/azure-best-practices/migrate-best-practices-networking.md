---
title: Osvědčené postupy pro nastavení sítě pro úlohy migrované do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Po migraci do Azure, získejte doporučené postupy pro nastavení sítě pro přenášená zatížení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a7f119dcfd2b7cdfc71b8a4c6f913448cd98e763
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753613"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Osvědčené postupy pro nastavení sítě pro úlohy migrované do Azure

Jako je plánování a návrh pro migraci, kromě migrace, jedním z nejdůležitějších kroků je návrh a implementaci sítí Azure. Tento článek popisuje osvědčené postupy pro sítě při migraci na implementace IaaS a PaaS v Azure.

> [!IMPORTANT]
> Uvedené osvědčené postupy a názory popsané v tomto článku jsou založené na funkcích platformy a služeb Azure, které jsou k dispozici v době vzniku tohoto článku. Funkce a možnosti se postupem času mění. Ne všechna doporučení můžou být pro vaše nasazení použitelná, takže si vyberte ty, které se vám hodí.

## <a name="design-virtual-networks"></a>Navržení virtuálních sítí

Azure poskytuje virtuální sítě:

- Prostředky Azure mezi sebou komunikují soukromě, přímo a bezpečně přes virtuální sítě.
- Ve virtuálních sítích můžete nakonfigurovat připojení koncových bodů pro virtuální počítače a služby, které vyžadují internetovou komunikaci.
- Virtuální sítě se o logickou izolaci cloudu Azure, který je vyhrazen pro vaše předplatné.
- V každém předplatném Azure a v každé oblasti Azure můžete implementovat několik virtuálních sítí.
- Každá virtuální síť je izolovaná od ostatních virtuálních sítí.
- Virtuální sítě může obsahovat privátní a veřejné IP adresy definované v [RFC 1918](https://tools.ietf.org/html/rfc1918), vyjádřené v zápisu CIDR. Veřejné IP adresy specifikované v adresním prostoru virtuální sítě nejsou přímo přístupné z internetu.
- Virtuální sítě se k sobě navzájem můžou připojit pomocí peeringu virtuálních sítí. Připojené virtuální sítě může být v jedné nebo několika oblastech. Prostředky v jedné virtuální síti se můžou připojit k prostředkům v jiných virtuálních sítích.
- Ve výchozím nastavení směruje Azure provoz mezi podsítěmi v rámci virtuální sítě, připojené virtuální sítě, místními sítěmi a Internetem.

Při plánování topologie virtuální sítě byste měli zvážit, jak uspořádat adresní prostory IP adres, jak implementovat hvězdicovou topologii sítě, jak rozdělit virtuální sítě do podsítí, nastavit DNS a implementovat zóny dostupnosti Azure.

## <a name="best-practice-plan-ip-addressing"></a>Osvědčený postup: Naplánujte IP adresování

Když vytvoříte virtuální sítě jako součást migrace, je důležité naplánovat adresní prostor IP adres virtuální sítě.

- Pro každou virtuální síť byste měli přiřadit adresní prostor, který není větší než rozsah CIDR /16. Virtuální sítě umožňují použití 65536 IP adres a přiřazení menší předpony než /16 by způsobilo ztrátu IP adres. Je důležité IP adresami neplýtvat, i když jsou v privátních rozsazích definovaných v RFC 1918.
- Adresní prostor virtuální sítě by se neměl překrývat s rozsahy místní sítě.
- Neměl by se používat překlad adres (NAT).
- Překrývající se adresy může způsobit sítě, které nemůže být připojen a směrování, která nebude fungovat správně. Pokud se sítě překrývají, budete muset změnit návrh sítě nebo použít překlad adres (NAT).

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) virtuálních sítí Azure.
- [Čtení](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) sítě – nejčastější dotazy.
- [Přečtěte si](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) o omezeních sítí.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Osvědčený postup: implementace topologie sítě rozbočovače a paprsků

Hvězdicová topologie sítě izoluje úlohy a současně sdílí služby, jako je identita a zabezpečení.

- Centrum této topologie je virtuální síť Azure, která funguje jako centrální bod připojení.
- Paprsky hvězdicové topologie jsou virtuální sítě, které se připojují k centrální virtuální síti pomocí peeringu virtuálních sítí.
- Sdílené služby jsou nasazené v centru, zatímco individuální úlohy jsou nasazené jako paprsky.

Zvažte použití těchto zdrojů:

- Implementace hvězdicové topologie sítě v Azure centralizuje běžné služby, jako jsou připojení k místním sítím, brány firewall a izolace mezi virtuálními sítěmi. Centrální virtuální síť poskytuje centrální bod připojení k místním sítím a místo pro hostování služeb využívaných úlohami, které jsou hostované v paprskových virtuálních sítích.
- Hvězdicovou konfiguraci obvykle používají větší podniky. Menší sítě můžou zvážit jednodušší formu, aby se nepotýkaly s takovými náklady a složitostí.
- Paprskové virtuální sítě se dají použít k izolování úloh, kdy se každý paprsek spravuje odděleně od ostatních paprsků. Každá úloha může obsahovat několik vrstev a několik podsítí připojených pomocí nástrojů pro vyrovnávání zatížení Azure.
- Střed a paprsek virtuální sítě se dá implementovat v různých skupinách prostředků a dokonce i v různých předplatných. Při peeringu virtuálních sítí v různých předplatných můžou být předplatná přidružená ke stejným nebo jiným tenantům Azure Active Directory (Azure AD). To umožňuje decentralizovanou správu každé úlohy při sdílení služeb udržovaných v centrální síti.

![Správa změn](./media/migrate-best-practices-networking/hub-spoke.png)
*Hvězdicová topologie sítě*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) o hvězdicové topologii sítě.
- Získejte doporučení pro síť pro provoz Azure [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) a [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm) virtuálních počítačů.
- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) o peeringu virtuálních sítí.

## <a name="best-practice-design-subnets"></a>Osvědčený postup: Při navrhování podsítí

Izolace v rámci virtuální sítě se dosahuje její segmentací do jedné nebo několika podsítí a přidělením části adresního prostoru virtuální sítě každé podsíti.

- V každé virtuální síti můžete vytvořit několik podsítí.
- Azure ve výchozím nastavení směruje síťový provoz mezi všemi podsítěmi ve virtuální síti.
- Vaše rozhodnutí o podsítích vycházejí z vašich technických a organizačních požadavků.
- Vytvoření podsítě se používá zápis CIDR.
- Při rozhodování o rozsahu sítě pro podsítě, je důležité si uvědomit, že Azure uchovává 5 IP adres z každé podsítě, které nelze použít. Pokud třeba vytvoříte nejmenší dostupnou podsíť /29 (s osmi IP adresami), Azure si zabere pět adres, takže máte jenom tři použitelné adresy, které je možné přiřadit hostitelům v podsíti.
- Ve většině případů použijte jako nejnižší podsíť/28.

**Příklad:**

Tabulka ukazuje příklad virtuální sítě s adresním prostorem 10.245.16.0/20 segmentovat do podsítí pro plánované migrace.

**Podsíť** | **CIDR** | **Adresy** | **Použití**
--- | --- | --- | ---
DEV-FE – EUS2 | 10.245.16.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Virtuální počítače vrstvy aplikace
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Virtuální počítače databáze

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) o navrhování podsítí.
- [Zjistěte](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure), jak fiktivní společnost (Contoso) připravila svoji síťovou infrastrukturu pro migraci.

## <a name="best-practice-set-up-a-dns-server"></a>Osvědčený postup: nastavení serveru DNS

Když nasadíte virtuální síť, Azure ve výchozím nastavení přidá server DNS. Díky tomu můžete rychle vytvářet virtuální sítě a nasazovat prostředky. Tento server DNS ale poskytuje služby jenom prostředkům v této virtuální síti. Pokud chcete propojení více virtuálních sítí nebo připojení k místnímu serveru z virtuální sítě, je nutné další název možnosti řešení. Například můžete potřebovat služby Active Directory k překladu názvů DNS mezi virtuálními sítěmi. Uděláte to tak, že v Azure nasadíte vlastní server DNS.

- Servery DNS ve virtuální síti, může předat dotazy DNS na rekurzivní překladače v Azure. To umožňuje překládat názvy hostitelů v rámci této virtuální síti. Třeba řadič domény běžící v Azure může reagovat na dotazy DNS na vlastní domény a všechny ostatní dotazy předávat do Azure.
- Předávání DNS umožňuje virtuálním počítačům vidět vaše místní prostředky (prostřednictvím řadiče domény) i názvy hostitelů poskytované službou Azure (pomocí předávání). Přístup k rekurzivním překladačům v Azure je k dispozici pomocí virtuální IP adresy 168.63.129.16.
- Předávání DNS taky umožňuje překlad DNS mezi virtuálními sítěmi, takže místní počítače můžou překládat názvy hostitelů poskytovaných službou Azure.
  - Přeložit název hostitele virtuálního počítače, server DNS virtuálního počítače se musí nacházet ve stejné virtuální síti a nakonfigurovat tak, aby dotazy na názvy dopředné hostitele do Azure.
  - Protože přípona DNS se liší v každé virtuální síti, můžete použít pravidla pro podmíněné předávání k odesílání dotazů DNS na správnou virtuální síť pro překlad.
- Pokud používáte vlastní servery DNS, můžete pro každou virtuální síť zadat několik serverů DNS. Můžete také zadat více serverů DNS pro každé síťové rozhraní (pro Azure Resource Manager) nebo pro každou cloudovou službu (pro klasický model nasazení).
- Servery DNS zadaný pro síťové rozhraní nebo cloudové služby mají přednost před serverů DNS má zadaný pro virtuální síť.
- V modelu nasazení Azure Resource Manager můžete servery DNS pro virtuální síť a síťové rozhraní zadat, ale osvědčeným postupem je použít toto nastavení jenom ve virtuální síti.

    ![Servery DNS](./media/migrate-best-practices-networking/dns2.png) *Servery DNS pro virtuální síť*

**Další informace:**

- [Další informace o](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) překlad názvů při použití vlastního serveru DNS.
- [Přečtěte si](../../ready/azure-best-practices/naming-and-tagging.md) o pravidlech a omezeních pro pojmenování DNS.

## <a name="best-practice-set-up-availability-zones"></a>Osvědčený postup: nastavení zóny dostupnosti

Zóny dostupnosti zvýšit vysokou dostupnost pro ochranu aplikací a dat z datacenter selhání.

- Zóny dostupnosti jsou jedinečná fyzická umístění uvnitř oblasti Azure.
- Každá zóna se skládá z jednoho nebo více datových Center vybavených nezávislým napájením, chlazením a sítí.
- Kvůli odolnosti ve všech aktivovaných oblastech existují minimálně tři samostatné zóny.
- Fyzické oddělení zón dostupnosti v rámci oblasti chrání aplikace a data před selháním datacenter.
- Zónově redundantní služby replikovat napříč zónami dostupnosti pro zajištění ochrany z jediné body selhání aplikace a data. --Se zónami dostupnosti Azure nabízí smlouvu SLA o 99,99 % dostupnosti virtuálního počítače.

    ![Zóna dostupnosti](./media/migrate-best-practices-networking/availability-zone.png) *zóně dostupnosti*

- Ve své architektuře migrace můžete naplánovat a vytvořit vysokou dostupnost tím, že sdružíte výpočetní prostředky, úložiště, sítě a datové prostředky v rámci zóny a budete je replikovat do jiných zón. Služby Azure, které podporují zóny dostupnosti se dělí do dvou kategorií:
  - Oblastmi služby: přiřadit prostředek s konkrétní zónu. Pro příklad virtuálních počítačů spravované disky, IP adresy).
  - Zónově redundantní služby: prostředku se automaticky replikuje napříč zónami. Třeba zónově redundantní úložiště, Azure SQL Database.
- Můžete nasadit standardní Azure zatížení vyrovnávaném pomocí úloh přístupem k Internetu nebo aplikačních vrstvách pro zónové odolné proti chybám.

    ![Nástroj pro vyrovnávání zatížení](./media/migrate-best-practices-networking/load-balancer.png) *Nástroj pro vyrovnávání zatížení*

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/availability-zones/az-overview) o zónách dostupnosti.

## <a name="design-hybrid-cloud-networking"></a>Návrh hybridních cloudových sítí

Pro úspěšnou migraci je důležité připojit k Azure místní podnikové sítě. Tím se vytvoří připojení vždy na označuje jako síť hybridního cloudu, kde jsou k dispozici služby Azure cloud pro podnikové uživatele. Existují dvě možnosti pro vytvoření tohoto typu sítě:

- **Síť Site-to-site VPN:** navázat připojení site-to-site mezi kompatibilní místní zařízení VPN a službou Azure VPN gateway, který je nasazený ve virtuální síti. Žádné oprávnění místních prostředků můžete přístup k virtuálním sítím. Komunikace Site-to-site se odesílá prostřednictvím šifrovaného tunelu přes internet.
- **Azure ExpressRoute:** navázat připojení k Azure ExpressRoute mezi místní sítí a Azure prostřednictvím partnera ExpressRoute. Toto připojení je privátní a přenos neprobíhá přes internet.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) další informace o hybridních cloudových sítích.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Osvědčený postup: implementace s vysokou dostupností site-to-site VPN

K implementaci site-to-site VPN nastavíte bránu VPN v Azure.

- VPN Gateway je konkrétní typ brány virtuální sítě, která odesílá šifrovaný provoz mezi virtuální sítí Azure a místním umístěním přes veřejný Internet.
- Brána VPN může také odesílat šifrovaný provoz mezi Azure virtuální sítě přes síť Microsoftu.
- Každá virtuální síť může mít jenom jednu bránu VPN.
- K jedné bráně VPN můžete vytvořit několik připojení. Když vytvoříte několik připojení, všechny tunely VPN sdílejí dostupnou šířku pásma.
- Každá Azure VPN Gateway se skládá ze dvou instancí v konfiguraci aktivní-pohotovostní.
  - Při plánované údržbě nebo neplánovaném přerušení aktivní instance dojde k převzetí služeb při selhání a pohotovostní instance automaticky převezme službu a obnoví spojení site-to-site nebo VNet-to-VNet.
  - Toto přepnutí způsobí krátké přerušení.
  - Při plánované údržbě by se spojení mělo obnovit během 10 až 15 sekund.
  - U neplánovaných problémů trvá obnovení spojení déle, v nejhorším případě minutu až minutu a půl.
  - Připojení klienta VPN typu point-to-site (P2S) k bráně se odpojí a uživatelé se budou muset na klientských počítačích znovu připojit.

Při nastavování site-to-site VPN, postupujte takto:

- Potřebujete virtuální síť, jejíž rozsah adres se nepřekrývá s místní sítí, ke které se VPN připojí.
- V síti vytvoříte podsíť brány.
- Vytvoření brány VPN, zadejte typ brány (VPN) a určuje, zda je brána na základě zásad nebo založené na směrování. SÍŤ VPN založená na trasách je považována za větší schopnost a budoucí kontrolu.
- Vytvoříte místní síťovou bránu a nakonfigurujete místní zařízení VPN.
- Vytvoříte připojení site-to-site VPN s podporou převzetí služeb při selhání mezi bránou virtuální sítě a místním zařízením. Použití VPN založeného na směrování umožňuje aktivní-pasivní nebo aktivní-aktivní připojení k Azure. Založené na trasách také podporuje připojení point-to-site (z jednoho počítače) i připojení site-to-site (z libovolného počítače) současně.
- Můžete určit SKU brány, kterou chcete použít. To bude záviset na požadavcích na úlohy, propustnosti, funkcích a smlouvách SLA.
- Protokol BGP (Border Gateway Protocol) je volitelná funkce, kterou můžete použít s Azure ExpressRoute a branami VPN založenými na směrování k šíření místních tras BGP do vaší virtuální sítě.

![VPN](./media/migrate-best-practices-networking/vpn.png)
*Site-to-site VPN*

**Další informace:**

- [Podívejte se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) na kompatibilní místní zařízení VPN.
- [Získejte přehled](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) o branách VPN.
- [Přečtěte si](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) o připojeních VPN s vysokou dostupností.
- [Další informace o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) plánování a navrhování bránu VPN.
- [Podívejte se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) na nastavení brány VPN.
- [Podívejte se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) na SKU brány.
- [Přečtěte si](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) o nastavení protokolu BGP s branami Azure VPN.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Osvědčený postup: Konfigurace brány pro VPN Gateway

Při vytváření brány VPN gateway v Azure, musíte použít speciální podsíť s názvem GatewaySubnet. Při vytváření této podsítě mějte na paměti tyto osvědčené postupy:

- Délka předpony podsítě brány může mít délku maximální předpony 29 (například 10.119.255.248/29). Aktuální doporučení je, že používáte délka předpony 27 (například 10.119.255.224/27).
- Při definování adresního prostoru podsítě brány použijte úplně poslední část adresního prostoru virtuální sítě.
- Pokud používáte Azure GatewaySubnet, nikdy neměli nasazovat všechny virtuální počítače nebo jiné zařízení, jako jsou Application Gateway do podsítě brány.
- Nepřiřazovat skupinu zabezpečení sítě (NSG) k této podsíti. Způsobí to, že brána přestane fungovat.

**Další informace:**

- [Pomocí tohoto nástroje](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) můžete zjistit svůj adresní prostor IP adres.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Osvědčený postup: implementace Azure virtuální sítě WAN pro firemní pobočky

Pro více připojení k síti VPN Azure virtuální síť WAN je síťové služby, která poskytuje optimalizované a automatizované větve do větve připojením prostřednictvím Azure.

- Virtuální síť WAN umožňuje připojit a nakonfigurovat zařízení v pobočkách tak, aby komunikovala přes Azure. Můžete to udělat ručně nebo pomocí zařízení od preferovaného poskytovatele prostřednictvím partnera pro Virtual WAN.
- Využití zařízení preferovaného poskytovatele umožňuje snadné používání, připojení a správu konfigurace.
- Integrovaný řídicí panel Azure WAN nabízí okamžité přehledy pro řešení potíží, které šetří čas, a snadný způsob sledování připojení site-to-site ve velkém měřítku.

**Další informace:** 
[Další informace o](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) Azure virtuální sítě WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Osvědčené postupy: implementace ExpressRoute pro kritická připojení

Služba Azure ExpressRoute rozšiřuje vaši místní infrastrukturu do cloudu Microsoftu tím, že vytváří privátní připojení mezi virtuálním datacentrem Azure a místními sítěmi.

- Připojení ExpressRoute můžou být prostřednictvím sítě any-to-any (IP VPN), sítě Ethernet point-to-point nebo prostřednictvím poskytovatele připojení. Neprocházejí přes veřejný internet.
- Připojení ExpressRoute nabízejí vyšší úroveň zabezpečení, spolehlivost a vyšších rychlostí (až 10 GB/s), spolu s konzistentní latence.
- ExpressRoute se hodí pro virtuální datacentra, protože zákazníci mohou získat výhody pravidel dodržování předpisů spojených s privátními připojeními.
- S ExpressRoute Direct můžete připojit přímo k směrovače Microsoftu na 100Gbps pro potřeby větší šířku pásma.
- ExpressRoute používá protokol BGP pro výměnu tras mezi místními sítěmi, instancí Azure a veřejnými adresami Microsoftu.

Nasazení připojení ExpressRoute obvykle zahrnuje zapojení poskytovatele služeb ExpressRoute. Pro rychlé zprovoznění se běžně používá site-to-site VPN k navázání připojení mezi virtuálním datacentrem a místními prostředky a následná migrace na připojení ExpressRoute, když je navázané fyzické propojení s vaším poskytovatelem služeb.

**Další informace:**

- [Přečtěte si přehled](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) ExpressRoute.
- [Přečtěte si](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) o ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Osvědčený postup: optimalizace směrování ExpressRoute s komunit protokolu BGP

Pokud máte víc okruhů ExpressRoute, máte více než jednu cestu, jak se připojit k Microsoftu. V důsledku toho může dojít k neoptimálnímu směrování a přenosy dat mezi vaší sítí a Microsoftem mohou použít delší cestu. Čím delší je síťová cesta, tím větší je latence. Latence má přímý vliv na výkon aplikací a zkušenosti uživatelů.

**Příklad:**

Pojďme se podívat na příklad:

- Máte dvě pobočky v USA, jednu v Los Angeles a jednu v New Yorku.
- Vaše pobočky jsou připojené v síti WAN, což může být vlastní páteřní sítě nebo VPN IP poskytovatele služeb.
- Máte dva okruhy ExpressRoute, jeden v oblasti USA – západ a druhý v oblasti USA – východ, které jsou také připojené k síti WAN. Zjevně máte dvě cesty, jak se připojit k síti Microsoftu.

**Problém:**

Teď si představte, že máte nasazení Azure (třeba Azure App Service) v oblastech USA – západ i USA – východ.

- Chcete, aby uživatelé v každé pobočce měli přístup k nejbližším službám Azure kvůli optimálnímu fungování.
- Proto budete chtít připojit uživatele z Los Angeles k Azure USA – západ a uživatele z New Yorku k Azure USA – východ.
- To funguje pro uživatele z východní pobřeží, ale ne pro ty ze západního pobřeží. V čem je problém:
  - V každém okruhu ExpressRoute inzerujeme jak předpony v Azure USA – východ (23.100.0.0/16), tak v Azure USA – západ (13.100.0.0/16).
  - Pokud se neví, která předpona je ze které oblasti, nezpracovávají se předpony odlišně.
  - Vaše síť WAN může předpokládat, že obě předpony jsou blíže k oblasti USA – východ než USA – západ, a proto směrovat uživatele z obou poboček do okruhu ExpressRoute v USA – východ. Tím poskytuje neoptimální funkčnost pro uživatele v pobočce v Los Angeles.

![VPN](./media/migrate-best-practices-networking/bgp1.png)
*komunit protokolu BGP neoptimalizované připojení*

**Řešení:**

Abyste optimalizovali směrování pro uživatele obou poboček, musíte vědět, která předpona je z oblasti Azure USA – západ a která z Azure USA – východ. Tyto informace můžete kódovat pomocí hodnot komunity protokolu BGP.

- Každé oblasti Azure přiřadíte jedinečnou hodnotu komunity protokolu BGP. Třeba 12076:51004 pro USA – východ, 12076:51006 pro USA – západ.
- Teď, když je jasné předpony, které patří do které oblasti Azure, můžete nakonfigurovat upřednostňované okruh ExpressRoute.
- Vzhledem k tomu, že k výměně informací o směrování používáte protokol BGP, můžete k ovlivnění směrování použít místní preferenci protokolu BGP.
- V našem příkladu přiřaďte vyšší hodnotu local preference pro 13.100.0.0/16 v oblasti USA – západ než v oblasti USA – východ a obdobně vyšší hodnotu local preference pro 23.100.0.0/16 v oblasti USA – východ než USA – západ.
- Tato konfigurace zajišťuje, že při cesty společnosti Microsoft jsou k dispozici, uživatelé v Los Angeles se připojí k Azure USA – západ – západ okruh pomocí i uživatelé New Yorku k Azure USA – východ připojit pomocí – východ okruh. Směrování je optimalizované na obou stranách.

![VPN](./media/migrate-best-practices-networking/bgp2.png)
*komunit protokolu BGP optimalizované připojení*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) o optimalizaci směrování.

## <a name="secure-vnets"></a>Zabezpečení virtuální sítě

Zodpovědnost za zabezpečení virtuálních sítí je sdílená mezi Microsoftem a vámi. Microsoft poskytuje mnoho síťových funkcí a služeb, které pomáhají zajistit zabezpečení zdrojů. K osvědčeným postupům při navrhování zabezpečení pro virtuální sítě patří implementace hraniční sítě, použití filtrování a skupin zabezpečení, zabezpečení přístupu k prostředkům a IP adresám a implementace ochrany před útoky.

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) osvědčených postupů pro zabezpečení sítě.
- [Zjistěte](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security), jak navrhovat zabezpečené sítě.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Osvědčený postup: provedení Azure hraniční síti

I když Microsoft do cloudové infrastruktury výrazně investuje, musíte chránit také své cloudové služby a skupiny prostředků. S více vrstvami přístup k zabezpečení poskytuje nejlepší ochranu. Významnou součástí takové strategie obrany je zřízení hraniční sítě.

- Hraniční síť chrání prostředkům v interní síti z nedůvěryhodné sítě.
- Je to vnější vrstva, která je vystavená internetu. Obecně se nachází mezi internetem a podnikovou infrastrukturou, obvykle s určitou formou ochrany na obou stranách.
- V typické podnikové síťové topologie základní infrastruktury silně přidá na perimetry, s víc vrstvami zabezpečení zařízení. Hranice každé vrstvy se skládá ze zařízení a bodů vynucení zásad.
- Každá vrstva může obsahovat kombinaci řešení zabezpečení sítě, které zahrnují brány firewall, ochrany před únikem informací s cílem odepření služby (DoS), systémů ochrany zjišťování/vniknutí neoprávněného vniknutí (IDS/IPS) a zařízení VPN.
- Vynucení zásad v hraniční síti můžete použít zásady brány firewall, seznamy řízení přístupu (ACL) nebo konkrétní směrování.
- Příchozí provoz z internetu se zachytí a zpracuje kombinací řešení obrany za účelem blokování útoků a škodlivého provozu a zároveň jsou umožněny legitimní požadavky na síť.
- Příchozí provoz se může směrovat přímo na prostředky v hraniční síti. Prostředek hraniční sítě může komunikovat s jiným prostředkům hlouběji v síti, přesun vpřed provoz do sítě po ověření.

Následující obrázek znázorňuje příklad hraniční síti jedinou podsítí v podnikové síti, s dvěma hranice zabezpečení.

![VPN](./media/migrate-best-practices-networking/perimeter.png)
*Nasazení hraniční sítě*

**Další informace:**

- [Další informace o](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) nasazení hraniční sítě mezi Azure a místním datacentrem.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Osvědčený postup: provoz VNet filtrování pomocí skupin zabezpečení sítě

Skupiny zabezpečení sítě (NSG) obsahují několik příchozích a odchozích pravidel zabezpečení, která filtrují přenosy přicházející do a z prostředků. Filtrování může být ve zdrojové a cílové IP adresy, portu a protokolu.

- Skupiny zabezpečení sítě obsahují pravidla zabezpečení, které povolit nebo odepřít příchozí síťové přenosy do (nebo odchozí síťový provoz ze) několik typů prostředků Azure. Pro každé pravidlo můžete určit zdroj a cíl, port a protokol.
- Pravidla NSG se vyhodnocují podle priority s použitím informací o řazené kolekci pěti členů (zdroj, zdrojový port, cíl, cílový port a protokol) a určují, jestli se má provoz povolit nebo odepřít.
- Pro stávající připojení se vytvoří záznam toku. Komunikace se povoluje nebo odepírá na základě stavu připojení v záznamu toku.
- Záznam flow umožňuje stavové existenci NSG. Pokud třeba zadáte odchozí pravidlo zabezpečení pro všechny adresy přes port 80, není potřeba příchozí pravidlo zabezpečení pro reakci na odchozí provoz. Příchozí pravidlo zabezpečení je potřeba zadat pouze v případě, že se komunikace zahajuje externě.
- Opačně to platí také. Pokud je povolený příchozí provoz přes port, není nutné zadat odchozí pravidlo zabezpečení pro reakci na provoz přes port.
- Existující připojení nepřerušily při odebrání pravidla zabezpečení, který povolen tok. Toky provozu se přeruší v případě zastavení připojení a toku provozu oběma směry po dobu aspoň několika minut.
- Při vytváření skupin zabezpečení sítě, vytvořte jako málo nejdříve ale tolik, které jsou nezbytné.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Osvědčený postup: zabezpečení provozu north/south a východ/západ

Při zabezpečování virtuálních sítí je důležité vzít v úvahu vektory útoku.

- Použití skupin zabezpečení sítě jenom u podsítě zjednodušuje vaše prostředí, ale zabezpečuje jenom provoz do vaší podsítě. To se označuje jako provoz sever/jih.
- Provoz mezi virtuálními počítači ve stejné podsíti se označuje jako provoz typu east/west.
- Je důležité používat obě formy ochrany, aby v případě, že hacker získá přístup zvenčí, byl zastaven při pokusu o připojení počítačů umístěných ve stejné podsíti.

### <a name="use-service-tags-on-nsgs"></a>Použití značek služeb na skupiny zabezpečení sítě

Značka služby představuje skupinu předpon IP adres. Použití značku služby pomáhá minimalizovat složitost vytváření pravidla skupiny zabezpečení sítě.

- Značky služeb můžete používat místo konkrétních IP adres při vytváření pravidel.
- Předpony adres spojené se značkou služby spravuje Microsoft, a pokud se adresy změní, automaticky značku služby aktualizuje.
- Nelze vytvořit vlastní značku služby ani určit, které IP adresy jsou ve značce zahrnuté.

Značky služby odstraňují ruční práci z přiřazování pravidla skupinám služeb Azure. Například pokud chcete povolit virtuální síť podsíť obsahující webové servery pro přístup ke službě Azure SQL Database, můžete vytvořit pravidlo odchozí port 1433 a použít **Sql** značka služby.

- Tato značka **Sql** označuje předpony adres služeb Azure SQL Database a Azure SQL Data Warehouse.
- Pokud jako hodnotu zadáte **Sql**, provoz směřující do Sql se povolí nebo zakáže.
- Pokud chcete povolit přístup k **Sql** jenom v konkrétní oblasti, můžete tuto oblast zadat. Pokud třeba chcete povolit přístup jenom ke službě Azure SQL Database v oblasti USA – východ, můžete jako značku služby zadat **Sql.EastUS**.
- Značka představuje službu, ale ne konkrétní instance služby. Značka třeba představuje službu Azure SQL Database, ale ne konkrétní databázi nebo server SQL.
- Všechny předpony adres reprezentované touto značkou jsou reprezentované také značkou **Internet**.

**Další informace:**

- [Přečtěte si informace o](https://docs.microsoft.com/azure/virtual-network/security-overview) skupin zabezpečení sítě.
- [Podívejte se](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) na značky služby, které jsou k dispozici pro skupiny zabezpečení sítě.

## <a name="best-practice-use-application-security-groups"></a>Osvědčený postup: použití skupin zabezpečení aplikací

Skupiny zabezpečení aplikací umožňují konfigurovat zabezpečení sítě jako přirozené rozšíření struktury aplikace.

- Na základě skupin zabezpečení aplikace můžete seskupovat virtuální počítače a definovat zásady zabezpečení sítě.
- Skupiny zabezpečení aplikace umožňují opakovaně používat škálované zásady zabezpečení bez potřeby ruční údržby explicitních IP adres.
- Skupiny zabezpečení aplikace zpracovávat složitost explicitních IP adres nebo více sad pravidel, tak budete moct soustředit na obchodní logiku.

**Příklad:**

![Skupina zabezpečení aplikace](./media/migrate-best-practices-networking/asg.png)
*Skupina zabezpečení aplikace*

**Síťové rozhraní** | **Skupiny zabezpečení aplikací**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- V našem příkladu každé síťové rozhraní patří jenom do jedné skupiny zabezpečení aplikace, ale ve skutečnosti může rozhraní patřit do více skupin v souladu s omezeními Azure.
- Žádné ze síťových rozhraní nemá přidruženou skupinu zabezpečení sítě (NSG). Skupina NSG1 je přidružená k oběma podsítím a obsahuje následující pravidla:

<!--markdownlint-disable MD033 -->

**Název pravidla** | **Účel** | **Podrobnosti**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Povoluje provoz z internetu na webové servery. Výchozí pravidlo zabezpečení DenyAllInbound odepírá příchozí provoz z internetu, takže pro skupiny zabezpečení aplikace AsgLogic a AsgDb není potřeba žádné další pravidlo. | Priorita: 100<br/><br/> Zdroj: internet<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgWeb<br/><br/> Cílový port: 80<br/><br/> Protocol: TCP<br/><br/> Přístup: Povolit.
Deny-Database-All | Výchozí pravidlo zabezpečení AllowVNetInBound povoluje veškerou komunikaci mezi prostředky ve stejné virtuální síti, takže toto pravidlo je potřeba k odepření provozu ze všech prostředků. | Priorita: 120<br/><br/> Zdroj: *<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgDb<br/><br/> Cílový port: 1433<br/><br/> Protokol: všechny<br/><br/> Přístup: odepřít.
Allow-Database-BusinessLogic | Povoluje provoz ze skupiny zabezpečení aplikace AsgLogic do skupiny zabezpečení aplikace AsgDb. Priorita pro toto pravidlo je vyšší než pro pravidlo Deny-Database-All a zpracovává se před ním, takže se povolí provoz ze skupiny zabezpečení aplikace AsgLogic a veškerý ostatní provoz se zablokuje. | Priorita: 110<br/><br/> Zdroj: AsgLogic<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgDb<br/><br/> Cílový port: 1433<br/><br/> Protocol: TCP<br/><br/> Přístup: Povolit.

<!--markdownlint-enable MD033 -->

- Pravidla určující skupinu zabezpečení aplikace jako zdroj nebo cíl se použijí pouze na síťová rozhraní, která jsou členy příslušné skupiny zabezpečení aplikace. Pokud síťové rozhraní není členem žádné skupiny zabezpečení aplikace, pravidlo se pro něj nepoužije, ani když je k podsíti přiřazená skupina zabezpečení sítě.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) o skupinách zabezpečení aplikace.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Osvědčený postup: zabezpečení přístupu k PaaS pomocí koncových bodů služby virtuální sítě

Koncové body služby virtuální sítě rozšiřují privátní adresní prostor virtuální sítě a identitu do služeb Azure přes přímé připojení.

- Koncové body umožňují zabezpečit důležité prostředky služeb Azure jenom do vašich virtuálních sítí. Provoz z vaší virtuální sítě do služby Azure vždy zůstává v páteřní síti Microsoft Azure.
- Privátní adresní prostor virtuální sítě můžou se překrývat a proto jej nelze použít k jednoznačné identifikaci přenos dat pocházejících z jedné virtuální sítě.
- Po povolení koncových bodů služby ve vaší virtuální síti můžete prostředky služeb Azure zabezpečit tak, že do prostředků služby přidáte pravidlo virtuální sítě. To poskytuje lepší zabezpečení díky úplnému odebrání veřejného internetového přístupu k prostředkům a povolení provozu pouze z vaší virtuální sítě.

![Koncové body služby](./media/migrate-best-practices-networking/endpoint.png)
*Koncové body služby*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) o koncových bodech služby virtuální sítě.

## <a name="best-practice-control-public-ip-addresses"></a>Osvědčený postup: řízení veřejné IP adresy

Veřejné IP adresy v Azure je možné přidružit k virtuálním počítačům, nástrojům pro vyrovnávání zatížení, aplikačním branám a branám VPN.

- Veřejné IP adresy umožňují internetovým prostředkům příchozí k prostředkům Azure komunikovat a prostředkům Azure komunikovat odchozí k Internetu.
- Veřejné IP adresy se vytváří se základní nebo standardní SKU, mezi kterými je několik rozdílů. Standardní SKU se dají přiřadit k jakékoli službě, ale většinou se konfigurují na virtuálních počítačích, nástrojích pro vyrovnávání zatížení a aplikačních branách.
- Je důležité si uvědomit, že základní veřejnou IP adresu nemusí automaticky nakonfiguruje skupiny NSG. Abyste mohli řídit přístup, musíte nakonfigurovat vlastní a přiřadit pravidla. Standardní SKU IP adres máte skupinu zabezpečení sítě a pravidel přiřazené ve výchozím nastavení.
- Jako osvědčený postup by neměl být virtuální počítače nakonfigurované s použitím veřejné IP adresy.
  - Pokud potřebujete otevřený port, měl by být jenom pro webové služby, jako je port 80 nebo 443.
  - Standardní porty vzdálené správy jako SSH (22) a RDP (3389), by měly být pomocí skupin zabezpečení sítě nastavené na odepření, stejně jako všechny ostatní porty.
- Lepším postupem je umístit virtuální počítače za nástroj pro vyrovnávání zatížení Azure nebo aplikační bránu. Pokud je pak potřeba přístup k portům pro vzdálenou správu, můžete v Azure Security Center použít přístup k virtuálnímu počítači podle potřeby.

**Další informace:**

- [Veřejné IP adresy v Azure](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses)
- [Správa přístupu k virtuálnímu počítači pomocí za běhu](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Využití funkcí zabezpečení Azure pro sítě

Azure má funkce zabezpečení platformy, které se snadno používají a poskytují bohatou škálu opatření proti běžným síťovým útokům. Patří k nim Azure Firewall, firewall webových aplikací a Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Osvědčený postup: nasazení Azure Firewall

Azure Firewall je spravovaná cloudová služba síťového zabezpečení, která chrání vaše prostředky ve virtuálních sítích. Jde o plně stavovou spravovanou bránu firewall s integrovanou vysokou dostupností a neomezenou cloudovou škálovatelností.

![Koncové body služby](./media/migrate-best-practices-networking/firewall.png)
*Azure Firewall*

- Azure Firewall může centrálně vytvářet, vynucovat a protokolovat zásady připojení k aplikacím a sítím napříč různými předplatnými a virtuálními sítěmi.
- Brána Azure Firewall používá statickou veřejnou IP adresu pro prostředky virtuální sítě a díky tomu umožňuje venkovním bránám firewall identifikovat provoz pocházející z vaší virtuální sítě.
- Brány Firewall na Azure je plně integrované s Azure Monitor pro protokolování a analýza.
- Jako osvědčený postup při vytváření pravidel brány Firewall na Azure vytvořte pravidla pomocí značek plně kvalifikovaný název domény.
  - Značku plně kvalifikovaný název domény představuje skupinu plně kvalifikované názvy domén, které jsou spojené s dobře známými službami Microsoftu.
  - Značku plně kvalifikovaného názvu domény můžete použít k povolení požadovaného odchozího síťového provozu přes bránu firewall.
- Například pokud chcete ručně povolit aktualizace Windows síťové přenosy přes bránu firewall, je třeba vytvořit víc pravidel aplikace. Pomocí značek plně kvalifikovaného názvu domény můžete vytvořit pravidlo aplikace a zahrnout značku webu Windows Update. S tímto pravidlem na místě síťového provozu do koncových bodů služby Microsoft Windows Update probíhá přes bránu firewall.

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/firewall/overview) ze Brána Firewall služby Azure.
- [Další informace o](https://docs.microsoft.com/azure/firewall/fqdn-tags) značky plně kvalifikovaný název domény.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Osvědčené postupy: nasazení firewallu webových aplikací (WAF)

Webové aplikace se čím dál častěji stávají cílem škodlivých útoků, které zneužívají běžně známé chyby zabezpečení. Zneužití patří útoky prostřednictvím injektáže SQL a útoky skriptování napříč weby. Předcházet takovým útokům v kódu aplikace může být náročné a může vyžadovat pečlivou údržbu, opravy a monitorování několika vrstev topologie aplikace. Centralizovaný Firewall webových aplikací značně zjednodušuje správu zabezpečení a pomáhá správcům aplikací lépe chránit před hrozbami nebo neoprávněným vniknutím. Firewall webové aplikace může na bezpečnostní hrozby reagovat rychleji díky opravení známých chyb zabezpečení v centrálním umístění místo zabezpečování jednotlivých webových aplikací. Stávající aplikační brány je možné jednoduše převést na aplikační brány doplněné webovým aplikačním firewallem.

Firewall webových aplikací (WAF) je funkce služby Azure Application Gateway.

- WAF poskytuje centralizovanou ochranu webových aplikací, z běžných zneužitím a ohrožením zabezpečení.
- WAF chrání bez úprav back-endového kódu.
- Může chránit více webových aplikací současně za službou Application Gateway.
- WAF je integrovaný se službou Azure Security Center.
- Můžete přizpůsobit pravidla a skupiny pravidel WAF, aby vyhovovaly požadavkům vašich aplikací.
- Jako osvědčený postup byste měli použít WAF v popředí u žádné aplikace s přístupem k web, včetně aplikací na virtuálních počítačích Azure nebo služby Azure App Service.

**Další informace:**

- [Další informace o](https://docs.microsoft.com/azure/application-gateway/waf-overview) WAF.
- [Podívejte se](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) na omezení a vyloučení WAF.

## <a name="best-practice-implement-azure-network-watcher"></a>Osvědčený postup: implementace Azure Network Watcher

Azure Network Watcher nabízí nástroje pro monitorování prostředků a komunikace ve virtuální síti Azure. Můžete třeba sledovat komunikaci mezi virtuálním počítačem a koncovým bodem, jako je jiný virtuální počítač nebo plně kvalifikovaný název domény, zobrazit prostředky a vztahy prostředků ve virtuální síti nebo diagnostikovat problémy se síťovými přenosy.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Network Watcher umožňuje monitorovat a diagnostikovat síťové problémy bez přihlášení k virtuálním počítačům.
- Nastavením upozornění můžete aktivovat zachytávání paketů a získat přístup k informacím o výkonu v reálném čase na úrovni paketů. Když narazíte na problém, můžete ho prozkoumat podrobněji.
- Osvědčeným postupem je použít Network Watcher ke kontrole protokolů toku NSG.
  - Protokoly toku NSG v Network Watcheru umožňují zobrazit informace o příchozím a odchozím provozu IP přes NSG.
  - Protokoly toku se zapisují ve formátu JSON.
  - Protokoly toku zobrazují odchozí a příchozí toky pro jednotlivá pravidla, síťové rozhraní (NIC), na které se tok vztahuje, pětici informací o toku (zdrojová/cílová IP adresa, zdrojový/cílový port a protokol) a informace o tom, jestli byl provoz povolený nebo odepřený.

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/network-watcher) služby Network Watcher.
- [Další informace](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) protokoly toků NSG.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Použití nástrojů partnerů na webu Azure Marketplace

Pro složitější topologií sítě můžete použít produkty zabezpečení od partnerů Microsoftu, v konkrétní síťová virtuální zařízení (Nva).

- Síťové virtuální zařízení je virtuální počítač, který provádí síťovou funkci, jako je brána firewall, optimalizace sítě WAN nebo jiná síťové funkce.
- Síťová virtuální zařízení posilují zabezpečení a síťové funkce virtuální sítě. Můžou být nasazená pro vysoce dostupné brány firewall, prevenci vniknutí, detekci vniknutí, Firewall webových aplikací (WAF), optimalizaci sítě WAN, směrování, vyrovnávání zatížení, VPN, správu certifikátů, Active Directory a vícefaktorové ověřování.
- Síťové virtuální zařízení je k dispozici mnoho dodavatelů v [Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Osvědčený postup: implementace brány firewall a síťová virtuální zařízení v Centru sítí

V centru se hraniční síť (s přístupem k internetu) obvykle spravuje přes bránu firewall Azure, farmu bran firewall nebo Firewall webových aplikací (WAF). Podívejte se na následující porovnání.

<!--markdownlint-disable MD033 -->

**Typ brány firewall** | **Podrobnosti**
--- | ---
WAF | Webové aplikace jsou běžné a často bývají postižené ohroženími zabezpečení a potenciálními zneužitími.<br/><br/> Řešení Waf jsou navržené k detekování útoků, které webové aplikace (HTTP/HTTPS), přesněji než obecné brány firewall.<br/><br/> V porovnání s tradiční technologií brány firewall mají WAF sadu specifických funkcí, které chrání interní webové servery před hrozbami.
Brána Azure Firewall | Podobně jako farmy bran firewall síťových virtuálních zařízení používá Azure Firewall mechanismus společné správy a sadu pravidel zabezpečení k ochraně úloh hostovaných v paprskových sítích a k řízení přístupu k místním sítím.<br/><br/> Azure Firewall má integrovanou škálovatelnost.
Brány firewall síťových virtuálních zařízení | Podobně jako Azure Firewall mají farmy bran firewall síťových virtuálních zařízení mechanismus společné správy a sadu pravidel zabezpečení k ochraně úloh hostovaných v paprskových sítích a k řízení přístupu k místním sítím.<br/><br/> Brány firewall síťových virtuálních zařízení se dají ručně škálovat za nástrojem pro vyrovnávání zatížení.<br/><br/> Když síťové virtuální zařízení brány firewall má menší speciální software než brány WAF, má širší rozsah aplikace můžete filtrovat a kontrolovat libovolného typu v příchozího a odchozího provozu.<br/><br/> Pokud chcete používat síťové virtuální zařízení, najdete je v Azure Marketplace.

<!--markdownlint-enable MD033 -->

Doporučujeme používat jednu sadu Azure Firewallů (nebo síťových virtuálních zařízení) pro provoz z internetu a jinou pro provoz z místní sítě.

- Použití jenom jedné sady brány firewall pro obě představuje bezpečnostní riziko, protože nabízí neexistuje žádná bezpečnostní hranice mezi těmito dvěma sadami síťových přenosů.
- Použitím samostatných vrstev bran firewall se snižuje složitost pravidel pro kontrolu zabezpečení a vyjasňuje, která pravidla platí pro jednotlivé příchozí žádosti v síti.

**Další informace:**

- [Další informace o](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) pomocí síťových virtuálních zařízení ve virtuální síti Azure.

## <a name="next-steps"></a>Další kroky

Projděte si další osvědčené postupy:

- [Osvědčené postupy](./migrate-best-practices-security-management.md) pro zabezpečení a správu po migraci
- [Osvědčené postupy](./migrate-best-practices-costs.md) cost Management po migraci.
