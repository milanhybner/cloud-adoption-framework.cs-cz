---
title: Osvědčené postupy pro nastavení sítě pro úlohy migrované do Azure
description: Po migraci do Azure si přečtěte o osvědčených postupech pro nastavení sítě pro migrované úlohy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 66694a9e1781f7d12d74e767b812b0831a371377
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225578"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Osvědčené postupy pro nastavení sítě pro úlohy migrované do Azure

Při plánování a navrhování migrace je jedním z nejdůležitějších kroků kromě samotné migrace navrhnutí a implementace sítě Azure. Tento článek popisuje osvědčené postupy pro sítě při migraci na implementace IaaS a PaaS v Azure.

> [!IMPORTANT]
> Uvedené osvědčené postupy a názory popsané v tomto článku jsou založené na funkcích platformy a služeb Azure, které jsou k dispozici v době vzniku tohoto článku. Funkce a možnosti se postupem času mění. Ne všechna doporučení můžou být pro vaše nasazení použitelná, takže si vyberte ty, které se vám hodí.

## <a name="design-virtual-networks"></a>Navržení virtuálních sítí

Azure poskytuje virtuální sítě:

- Prostředky Azure mezi sebou komunikují soukromě, přímo a bezpečně přes virtuální sítě.
- Ve virtuálních sítích můžete nakonfigurovat připojení koncových bodů pro virtuální počítače a služby, které vyžadují internetovou komunikaci.
- Virtuální síť je logická izolace cloudu Azure vyhrazeného pro vaše předplatné.
- V každém předplatném Azure a v každé oblasti Azure můžete implementovat několik virtuálních sítí.
- Každá virtuální síť je izolovaná od ostatních virtuálních sítí.
- Virtuální sítě můžou obsahovat privátní a veřejné IP adresy definované v [RFC 1918](https://tools.ietf.org/html/rfc1918), vyjádřené v zápisu CIDR. Veřejné IP adresy specifikované v adresním prostoru virtuální sítě nejsou přímo přístupné z internetu.
- Virtuální sítě se k sobě navzájem můžou připojit pomocí peeringu virtuálních sítí. Připojené virtuální sítě můžou být ve stejných nebo různých oblastech. Prostředky v jedné virtuální síti se můžou připojit k prostředkům v jiných virtuálních sítích.
- Azure ve výchozím nastavení směruje provoz mezi podsítěmi v rámci virtuální sítě, propojenými virtuálními sítěmi, místními sítěmi a internetem.

Při plánování topologie virtuální sítě byste měli zvážit, jak uspořádat adresní prostory IP adres, jak implementovat hvězdicovou topologii sítě, jak rozdělit virtuální sítě do podsítí, nastavit DNS a implementovat zóny dostupnosti Azure.

## <a name="best-practice-plan-ip-addressing"></a>Osvědčený postup: Naplánujte IP adresování

Když vytvoříte virtuální sítě jako součást migrace, je důležité naplánovat adresní prostor IP adres virtuální sítě.

- Pro každou virtuální síť byste měli přiřadit adresní prostor, který není větší než rozsah CIDR /16. Virtuální sítě umožňují použití 65536 IP adres a přiřazení menší předpony než /16 by způsobilo ztrátu IP adres. Je důležité IP adresami neplýtvat, i když jsou v privátních rozsazích definovaných v RFC 1918.
- Adresní prostor virtuální sítě by se neměl překrývat s rozsahy místní sítě.
- Neměl by se používat překlad adres (NAT).
- Překrývající se adresy můžou způsobit, že se sítě nemůžou připojit a směrování správně nefunguje. Pokud se sítě překrývají, budete muset změnit návrh sítě nebo použít překlad adres (NAT).

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) o virtuálních sítích Azure.
- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) nejčastější dotazy k sítím.
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
- Virtuální sítě s hvězdicovou topologií je možné implementovat v různých skupinách prostředků, a dokonce i v různých předplatných. Při peeringu virtuálních sítí v různých předplatných můžou být předplatná přidružená ke stejným nebo jiným tenantům Azure Active Directory (Azure AD). To umožňuje decentralizovanou správu každé úlohy při sdílení služeb udržovaných v centrální virtuální síti.

![Správa změn](./media/migrate-best-practices-networking/hub-spoke.png)
*Hvězdicová topologie sítě*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) o hvězdicové topologii sítě.
- Získejte síťová doporučení pro provoz virtuálních počítačů Azure s [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) a [Linuxem](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm).
- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) o peeringu virtuálních sítí.

## <a name="best-practice-design-subnets"></a>Osvědčený postup: Při navrhování podsítí

Izolace v rámci virtuální sítě se dosahuje její segmentací do jedné nebo několika podsítí a přidělením části adresního prostoru virtuální sítě každé podsíti.

- V každé virtuální síti můžete vytvořit několik podsítí.
- Azure ve výchozím nastavení směruje síťový provoz mezi všemi podsítěmi ve virtuální síti.
- Vaše rozhodnutí o podsítích vycházejí z vašich technických a organizačních požadavků.
- Podsítě se vytvářejí pomocí zápisu CIDR.
- Při rozhodování o rozsahu sítě pro podsítě je důležité si uvědomit, že Azure si zabere pět IP adres z každé podsítě, které nejde použít. Pokud třeba vytvoříte nejmenší dostupnou podsíť /29 (s osmi IP adresami), Azure si zabere pět adres, takže máte jenom tři použitelné adresy, které je možné přiřadit hostitelům v podsíti.
- Ve většině případů použijte jako nejnižší podsíť/28.

**Příklad:**

V tabulce je zobrazený příklad virtuální sítě s adresním prostorem 10.245.16.0/20 rozděleným do podsítí pro plánovanou migraci.

**Podsíť** | **CIDR** | **Adresy** | **Použití**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Virtuální počítače aplikační vrstvy
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Virtuální počítače databáze

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) o navrhování podsítí.
- [Zjistěte](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure), jak fiktivní společnost (Contoso) připravila svoji síťovou infrastrukturu pro migraci.

## <a name="best-practice-set-up-a-dns-server"></a>Osvědčený postup: nastavení serveru DNS

Když nasadíte virtuální síť, Azure ve výchozím nastavení přidá server DNS. Díky tomu můžete rychle vytvářet virtuální sítě a nasazovat prostředky. Tento server DNS ale poskytuje služby jenom prostředkům v této virtuální síti. Pokud chcete společně připojit více virtuálních sítí nebo se z virtuální sítě připojit k místnímu serveru, budete potřebovat další možnosti překladu adres IP. Můžete třeba potřebovat Active Directory k překladu názvů DNS mezi virtuálními sítěmi. Uděláte to tak, že v Azure nasadíte vlastní server DNS.

- Servery DNS ve virtuální síti můžou předávat dotazy DNS rekurzivním překladačům v Azure. To vám umožňuje překládat názvy hostitelů v rámci této virtuální sítě. Třeba řadič domény běžící v Azure může reagovat na dotazy DNS na vlastní domény a všechny ostatní dotazy předávat do Azure.
- Předávání DNS umožňuje virtuálním počítačům vidět vaše místní prostředky (prostřednictvím řadiče domény) i názvy hostitelů poskytované službou Azure (pomocí předávání). Přístup k rekurzivním překladačům v Azure je k dispozici pomocí virtuální IP adresy 168.63.129.16.
- Předávání DNS taky umožňuje překlad DNS mezi virtuálními sítěmi, takže místní počítače můžou překládat názvy hostitelů poskytovaných službou Azure.
  - Aby bylo možné přeložit název hostitele virtuálního počítače, musí se virtuální počítač serveru DNS nacházet ve stejné virtuální síti a musí být nakonfigurovaný tak, aby předával dotazy na název hostitele do Azure.
  - Vzhledem k tomu, že se přípona DNS v každé virtuální síti liší, můžete použít pravidla podmíněného předávání k odesílání dotazů DNS do správné virtuální sítě pro překlad.
- Pokud používáte vlastní servery DNS, můžete pro každou virtuální síť zadat několik serverů DNS. Můžete také zadat více serverů DNS pro každé síťové rozhraní (pro Azure Resource Manager) nebo pro každou cloudovou službu (pro klasický model nasazení).
- Servery DNS zadané pro síťové rozhraní nebo cloudovou službu mají přednost před servery DNS zadanými pro virtuální síť.
- V modelu nasazení Azure Resource Manager můžete servery DNS pro virtuální síť a síťové rozhraní zadat, ale osvědčeným postupem je použít toto nastavení jenom ve virtuální síti.

    ![DNS servery](./media/migrate-best-practices-networking/dns2.png) *servery DNS pro virtuální síť*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) o překladu názvů při použití vlastního serveru DNS.
- [Přečtěte si](../../ready/azure-best-practices/naming-and-tagging.md) o pravidlech a omezeních pro pojmenování DNS.

## <a name="best-practice-set-up-availability-zones"></a>Osvědčený postup: nastavení zóny dostupnosti

Zóny dostupnosti zvyšují vysokou dostupnost a chrání vaše aplikace a data před selháními datacenter.

- Zóny dostupnosti jsou jedinečná fyzická umístění uvnitř oblasti Azure.
- Každou zónu tvoří jedno nebo několik datacenter vybavených nezávislým napájením, chlazením a sítí.
- Kvůli odolnosti ve všech aktivovaných oblastech existují minimálně tři samostatné zóny.
- Fyzické oddělení zón dostupnosti v rámci oblasti chrání aplikace a data před selháním datacenter.
- Zónově redundantní služby replikují vaše aplikace a data napříč zónami dostupnosti, aby je chránily před kritickými prvky způsobujícími selhání. – Díky zónám dostupnosti nabízí Azure smlouvu SLA s 99,99% dobou provozu virtuálních počítačů.

    ![zóna dostupnosti](./media/migrate-best-practices-networking/availability-zone.png) *zóna dostupnosti*

- Ve své architektuře migrace můžete naplánovat a vytvořit vysokou dostupnost tím, že sdružíte výpočetní prostředky, úložiště, sítě a datové prostředky v rámci zóny a budete je replikovat do jiných zón. Služby Azure, které podporují zóny dostupnosti, spadají do dvou kategorií:
  - Oblastmi služby: přiřadit prostředek s konkrétní zónu. Třeba virtuální počítače, spravované disky, IP adresy.
  - Zónově redundantní služby: prostředku se automaticky replikuje napříč zónami. Třeba zónově redundantní úložiště, Azure SQL Database.
- Pro zajištění zonální odolnosti proti chybám můžete nasadit standardní nástroj pro vyrovnávání zatížení Azure s úlohami nebo aplikačními vrstvami s přístupem k internetu.

    Nástroj pro vyrovnávání zatížení ![](./media/migrate-best-practices-networking/load-balancer.png) *Load Balancer*

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/availability-zones/az-overview) o zónách dostupnosti.

## <a name="design-hybrid-cloud-networking"></a>Návrh hybridních cloudových sítí

Pro úspěšnou migraci je důležité připojit k Azure místní podnikové sítě. Tím se vytvoří stále aktivní připojení označované jako hybridní cloudová síť, kde se služby podnikovým uživatelům poskytují z cloudu Azure. Existují dvě možnosti, jak tento typ sítě vytvořit:

- Síť **VPN typu Site-to-site:** Vytvoříte připojení typu Site-to-site mezi kompatibilním místním zařízením VPN a bránou Azure VPN Gateway, která je nasazená ve virtuální síti. K virtuální síti může přistupovat jakýkoli autorizovaný místní prostředek. Komunikace site-to-site se odesílají prostřednictvím šifrovaného tunelu přes internet.
- **ExpressRoute Azure:** Vytvoříte připojení Azure ExpressRoute mezi vaší místní sítí a Azure prostřednictvím partnera ExpressRoute. Toto připojení je privátní a přenos neprobíhá přes internet.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) další informace o hybridních cloudových sítích.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Osvědčený postup: implementace s vysokou dostupností site-to-site VPN

K implementaci site-to-site VPN nastavíte bránu VPN v Azure.

- VPN Gateway je konkrétní typ brány virtuální sítě, která odesílá šifrovaný provoz mezi virtuální sítí Azure a místním umístěním přes veřejný Internet.
- Brána VPN může také odesílat šifrovaný provoz mezi Azure virtuální sítě přes síť Microsoftu.
- Každá virtuální síť může mít jenom jednu bránu VPN.
- K jedné bráně VPN můžete vytvořit několik připojení. Když vytvoříte několik připojení, všechny tunely VPN sdílejí dostupnou šířku pásma brány.
- Každá Azure VPN Gateway se skládá ze dvou instancí v konfiguraci aktivní-pohotovostní.
  - Při plánované údržbě nebo neplánovaném přerušení aktivní instance dojde k převzetí služeb při selhání a pohotovostní instance automaticky převezme službu a obnoví spojení site-to-site nebo VNet-to-VNet.
  - Toto přepnutí způsobí krátké přerušení.
  - Při plánované údržbě by se spojení mělo obnovit během 10 až 15 sekund.
  - U neplánovaných problémů trvá obnovení spojení déle, v nejhorším případě minutu až minutu a půl.
  - Připojení klienta VPN typu point-to-site (P2S) k bráně se odpojí a uživatelé se budou muset na klientských počítačích znovu připojit.

Při nastavování site-to-site VPN:

- Potřebujete virtuální síť, jejíž rozsah adres se nepřekrývá s místní sítí, ke které se VPN připojí.
- V síti vytvoříte podsíť brány.
- Vytvoříte bránu VPN, určíte typ brány (VPN) a jestli je brána založená na zásadách nebo na směrování. SÍŤ VPN založená na trasách je považována za větší schopnost a budoucí kontrolu.
- Vytvoříte místní síťovou bránu a nakonfigurujete místní zařízení VPN.
- Vytvoříte připojení site-to-site VPN s podporou převzetí služeb při selhání mezi bránou virtuální sítě a místním zařízením. Použití VPN založeného na směrování umožňuje aktivní-pasivní nebo aktivní-aktivní připojení k Azure. Založení na směrování také podporuje souběžná připojení site-to-site (z libovolného počítače) i point-to-site (z jednoho počítače).
- Určíte SKU brány, kterou chcete použít. To bude záviset na požadavcích na úlohy, propustnosti, funkcích a smlouvách SLA.
- Protokol BGP (Border Gateway Protocol) je volitelná funkce, kterou můžete použít s Azure ExpressRoute a branami VPN založenými na směrování k šíření místních tras BGP do vaší virtuální sítě.

![VPN](./media/migrate-best-practices-networking/vpn.png)
*Site-to-site VPN*

**Další informace:**

- [Podívejte se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) na kompatibilní místní zařízení VPN.
- [Získejte přehled](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) o branách VPN.
- [Přečtěte si](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) o připojeních VPN s vysokou dostupností.
- [Přečtěte si](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) o plánování a navrhování brány VPN.
- [Podívejte se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) na nastavení brány VPN.
- [Podívejte se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) na SKU brány.
- [Přečtěte si](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) o nastavení protokolu BGP s branami Azure VPN.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Osvědčený postup: Konfigurace brány pro VPN Gateway

Když vytvoříte bránu VPN v Azure, musíte použít speciální podsíť s názvem GatewaySubnet. Při vytváření této podsítě mějte na paměti tyto osvědčené postupy:

- Délka předpony podsítě brány může být maximálně 29 (například 10.119.255.248/29). Aktuální doporučení je použít délku předpony 27 (například 10.119.255.224/27).
- Při definování adresního prostoru podsítě brány použijte úplně poslední část adresního prostoru virtuální sítě.
- Při použití Azure GatewaySubnet nenasazujte do podsítě brány žádné virtuální počítače ani jiná zařízení jako Application Gateway.
- Nepřiřazujte této podsíti skupinu zabezpečení sítě (NSG). Způsobí to, že brána přestane fungovat.

**Další informace:**

- [Pomocí tohoto nástroje](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) můžete zjistit svůj adresní prostor IP adres.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Osvědčený postup: implementace Azure virtuální sítě WAN pro firemní pobočky

Pro více připojení VPN je Azure Virtual WAN síťová služba poskytující optimalizované a automatizované možnosti propojení jednotlivých poboček prostřednictvím Azure.

- Virtuální síť WAN umožňuje připojit a nakonfigurovat zařízení v pobočkách tak, aby komunikovala přes Azure. Můžete to udělat ručně nebo pomocí zařízení od preferovaného poskytovatele prostřednictvím partnera pro Virtual WAN.
- Využití zařízení preferovaného poskytovatele umožňuje snadné používání, připojení a správu konfigurace.
- Integrovaný řídicí panel Azure WAN nabízí okamžité přehledy pro řešení potíží, které šetří čas, a snadný způsob sledování připojení site-to-site ve velkém měřítku.

**Další informace:** 
[Přečtěte si](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) o Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Osvědčené postupy: implementace ExpressRoute pro kritická připojení

Služba Azure ExpressRoute rozšiřuje vaši místní infrastrukturu do cloudu Microsoftu tím, že vytváří privátní připojení mezi virtuálním datacentrem Azure a místními sítěmi.

- Připojení ExpressRoute můžou být prostřednictvím sítě any-to-any (IP VPN), sítě Ethernet point-to-point nebo prostřednictvím poskytovatele připojení. Neprocházejí přes veřejný internet.
- Připojení ExpressRoute nabízejí vyšší míru zabezpečení, spolehlivosti a vyšší rychlosti (až 10 Gb/s) a zároveň konzistentní latenci.
- ExpressRoute se hodí pro virtuální datacentra, protože zákazníci mohou získat výhody pravidel dodržování předpisů spojených s privátními připojeními.
- Pomocí ExpressRoute Direct se můžete připojit přímo ke směrovačům Microsoftu rychlostí 100 Gb/s pro větší potřebné šířky pásma.
- ExpressRoute používá protokol BGP pro výměnu tras mezi místními sítěmi, instancemi Azure a veřejnými adresami Microsoftu.

Nasazení připojení ExpressRoute obvykle zahrnuje angažování poskytovatel služeb ExpressRoute. Pro rychlé zprovoznění se běžně používá site-to-site VPN k navázání připojení mezi virtuálním datacentrem a místními prostředky a následná migrace na připojení ExpressRoute, když je navázané fyzické propojení s vaším poskytovatelem služeb.

**Další informace:**

- [Přečtěte si přehled](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) ExpressRoute.
- [Přečtěte si](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) o ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Osvědčený postup: optimalizace směrování ExpressRoute s komunit protokolu BGP

Pokud máte víc okruhů ExpressRoute, máte více než jednu cestu, jak se připojit k Microsoftu. V důsledku toho může dojít k neoptimálnímu směrování a přenosy dat mezi vaší sítí a Microsoftem mohou použít delší cestu. Čím delší je síťová cesta, tím větší je latence. Latence má přímý vliv na výkon aplikací a zkušenosti uživatelů.

**Příklad:**

Pojďme se podívat na příklad:

- Máte dvě pobočky v USA, jednu v Los Angeles a jednu v New Yorku.
- Vaše pobočky jsou připojené k síti WAN, což může být buď vaše páteřní síť, nebo IP VPN vašeho poskytovatele služeb.
- Máte dva okruhy ExpressRoute, jeden v oblasti USA – západ a druhý v oblasti USA – východ, které jsou také připojené k síti WAN. Zjevně máte dvě cesty, jak se připojit k síti Microsoftu.

**Problém:**

Teď si představte, že máte nasazení Azure (třeba Azure App Service) v oblastech USA – západ i USA – východ.

- Chcete, aby uživatelé v každé pobočce měli přístup k nejbližším službám Azure kvůli optimálnímu fungování.
- Proto chcete, aby uživatelé v Los Angeles byli připojení k Azure USA – západ, a uživatelé v New Yorku k Azure USA – východ.
- To funguje pro uživatele z východní pobřeží, ale ne pro ty ze západního pobřeží. V čem je problém:
  - V každém okruhu ExpressRoute inzerujeme jak předpony v Azure USA – východ (23.100.0.0/16), tak v Azure USA – západ (13.100.0.0/16).
  - Pokud se neví, která předpona je ze které oblasti, nezpracovávají se předpony odlišně.
  - Vaše síť WAN může předpokládat, že obě předpony jsou blíže k oblasti USA – východ než USA – západ, a proto směrovat uživatele z obou poboček do okruhu ExpressRoute v USA – východ. Tím poskytuje neoptimální funkčnost pro uživatele v pobočce v Los Angeles.

![VPN](./media/migrate-best-practices-networking/bgp1.png)
*Neoptimalizované připojení komunit BGP*

**Řešení:**

Abyste optimalizovali směrování pro uživatele obou poboček, musíte vědět, která předpona je z oblasti Azure USA – západ a která z Azure USA – východ. Tyto informace můžete kódovat pomocí hodnot komunity protokolu BGP.

- Každé oblasti Azure přiřadíte jedinečnou hodnotu komunity protokolu BGP. Třeba 12076:51004 pro USA – východ, 12076:51006 pro USA – západ.
- Když je teď jasné, která předpona patří ke které oblasti Azure, můžete nakonfigurovat upřednostňovaný okruh ExpressRoute.
- Vzhledem k tomu, že k výměně informací o směrování používáte protokol BGP, můžete k ovlivnění směrování použít místní preferenci protokolu BGP.
- V našem příkladu přiřadíte vyšší místní preferenci pro 13.100.0.0/16 v oblasti USA – západ než v oblasti USA – východ a obdobně vyšší místní preferenci pro 23.100.0.0/16 v oblasti USA – východ než USA – západ.
- Tato konfigurace zajišťuje, že pokud jsou k dispozici obě cesty k Microsoftu, budou se uživatelé v Los Angeles připojovat k Azure USA – západ pomocí západního okruhu a uživatelé v New Yorku se budou připojovat k Azure USA – východ pomocí východního okruhu. Směrování je optimalizované na obou stranách.

![VPN](./media/migrate-best-practices-networking/bgp2.png)
*Optimalizované připojení komunit BGP*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) o optimalizaci směrování.

## <a name="secure-vnets"></a>Zabezpečení virtuální sítě

Zodpovědnost za zabezpečení virtuálních sítí je sdílená mezi Microsoftem a vámi. Microsoft poskytuje mnoho síťových funkcí a služeb, které pomáhají zajistit zabezpečení zdrojů. K osvědčeným postupům při navrhování zabezpečení pro virtuální sítě patří implementace hraniční sítě, použití filtrování a skupin zabezpečení, zabezpečení přístupu k prostředkům a IP adresám a implementace ochrany před útoky.

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) o osvědčených postupech zabezpečení sítí.
- [Zjistěte](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security), jak navrhovat zabezpečené sítě.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Osvědčený postup: provedení Azure hraniční síti

I když Microsoft do cloudové infrastruktury výrazně investuje, musíte chránit také své cloudové služby a skupiny prostředků. Nejlepší obranu poskytuje přístup s více vrstvami zabezpečení. Významnou součástí takové strategie obrany je zřízení hraniční sítě.

- Hraniční síť chrání interní síťové prostředky před nedůvěryhodnou sítí.
- Je to vnější vrstva, která je vystavená internetu. Obecně se nachází mezi internetem a podnikovou infrastrukturou, obvykle s určitou formou ochrany na obou stranách.
- V typické topologii podnikové sítě je základní infrastruktura intenzivně zabezpečená na hraničních bodech s více vrstvami bezpečnostních zařízení. Hranice každé vrstvy se skládá ze zařízení a bodů vynucení zásad.
- Každá vrstva může zahrnovat kombinaci řešení zabezpečení sítě, která zahrnují brány firewall, prevenci přerušení služby (DoS), systémy zjišťování neoprávněných vniknutí / ochrany před neoprávněným vniknutím (ID/IPS) a zařízení VPN.
- Vynucování zásad v hraniční síti může využívat zásady brány firewall, seznamy řízení přístupu (ACL) nebo konkrétní směrování.
- Příchozí provoz z internetu se zachytí a zpracuje kombinací řešení obrany za účelem blokování útoků a škodlivého provozu a zároveň jsou umožněny legitimní požadavky na síť.
- Příchozí provoz se může směrovat přímo na prostředky v hraniční síti. Prostředek hraniční sítě pak může komunikovat s dalšími prostředky hlouběji v síti a po ověření předávat provoz do sítě.

Následující obrázek ukazuje příklad jedné hraniční sítě podsítě v podnikové síti se dvěma bezpečnostními hranicemi.

![VPN](./media/migrate-best-practices-networking/perimeter.png)
*Nasazení hraniční sítě*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o nasazení hraniční sítě mezi Azure a vaším místním datacentrem.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Osvědčený postup: provoz VNet filtrování pomocí skupin zabezpečení sítě

Skupiny zabezpečení sítě (NSG) obsahují několik příchozích a odchozích pravidel zabezpečení, která filtrují přenosy přicházející do a z prostředků. Filtrování se může provádět podle zdrojové a cílové IP adresy, portu a protokolu.

- NSG obsahují pravidla zabezpečení umožňující povolit nebo odepřít příchozí nebo odchozí síťový provoz několika typů prostředků Azure. Pro každé pravidlo můžete určit zdroj a cíl, port a protokol.
- Pravidla NSG se vyhodnocují podle priority s použitím informací o řazené kolekci pěti členů (zdroj, zdrojový port, cíl, cílový port a protokol) a určují, jestli se má provoz povolit nebo odepřít.
- Pro stávající připojení se vytvoří záznam toku. Komunikace se povoluje nebo odepírá na základě stavu připojení v záznamu toku.
- Záznam toku umožňuje, aby byla NSG stavová. Pokud třeba zadáte odchozí pravidlo zabezpečení pro všechny adresy přes port 80, není potřeba příchozí pravidlo zabezpečení pro reakci na odchozí provoz. Příchozí pravidlo zabezpečení je potřeba zadat pouze v případě, že se komunikace zahajuje externě.
- Opačně to platí také. Pokud je přes port povolený příchozí provoz, nemusíte zadávat odchozí pravidlo zabezpečení pro reakci na provoz přes tento port.
- Když odeberete pravidlo zabezpečení, které povolilo tok, stávající připojení se nepřeruší. Toky provozu se přeruší v případě zastavení připojení a toku provozu oběma směry po dobu aspoň několika minut.
- Skupin zabezpečení sítě vytvořte co nejméně, ale tolik, kolik je nezbytných.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Osvědčený postup: zabezpečení provozu north/south a východ/západ

Při zabezpečování virtuálních sítí je důležité vzít v úvahu vektory útoku.

- Použití skupin zabezpečení sítě jenom u podsítě zjednodušuje vaše prostředí, ale zabezpečuje jenom provoz do vaší podsítě. To se označuje jako provoz sever/jih.
- Provoz mezi virtuálními počítači ve stejné podsíti se označuje jako provoz východ/západ.
- Je důležité používat obě formy ochrany, aby v případě, že hacker získá přístup zvenčí, byl zastaven při pokusu o připojení počítačů umístěných ve stejné podsíti.

### <a name="use-service-tags-on-nsgs"></a>Použití značek služeb na skupiny zabezpečení sítě

Značka služby představuje skupinu předpon IP adres. Použití značky služby pomáhá minimalizovat složitost při vytváření pravidel NSG.

- Značky služeb můžete používat místo konkrétních IP adres při vytváření pravidel.
- Předpony adres spojené se značkou služby spravuje Microsoft, a pokud se adresy změní, automaticky značku služby aktualizuje.
- Nemůžete vytvořit vlastní značku služby ani určit, které IP adresy jsou ve značce zahrnuté.

Značky služby odstraňují ruční práci z přiřazování pravidla skupinám služeb Azure. Pokud třeba chcete, aby podsíť virtuální sítě obsahující webové servery měla přístup k Azure SQL Database, mohli byste vytvořit pravidlo odchozích přenosů pro port 1433 a použít značku služby **Sql**.

- Tato značka **Sql** označuje předpony adres služeb Azure SQL Database a Azure SQL Data Warehouse.
- Pokud jako hodnotu zadáte **Sql**, provoz směřující do Sql se povolí nebo zakáže.
- Pokud chcete povolit přístup k **Sql** jenom v konkrétní oblasti, můžete tuto oblast zadat. Pokud třeba chcete povolit přístup jenom ke službě Azure SQL Database v oblasti USA – východ, můžete jako značku služby zadat **Sql.EastUS**.
- Značka představuje službu, ale ne konkrétní instance služby. Značka třeba představuje službu Azure SQL Database, ale ne konkrétní databázi nebo server SQL.
- Všechny předpony adres reprezentované touto značkou jsou reprezentované také značkou **Internet**.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/security-overview) o skupinách zabezpečení sítě.
- [Podívejte se](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) na značky služby, které jsou k dispozici pro skupiny zabezpečení sítě.

## <a name="best-practice-use-application-security-groups"></a>Osvědčený postup: použití skupin zabezpečení aplikací

Skupiny zabezpečení aplikace umožňují konfigurovat zabezpečení sítě jako přirozené rozšíření struktury aplikace.

- Na základě skupin zabezpečení aplikace můžete seskupovat virtuální počítače a definovat zásady zabezpečení sítě.
- Skupiny zabezpečení aplikace umožňují opakovaně používat škálované zásady zabezpečení bez potřeby ruční údržby explicitních IP adres.
- O složitost explicitních IP adres a několika skupin pravidel se starají skupiny zabezpečení aplikace, takže se vy můžete zaměřit na obchodní logiku.

**Příklad:**

![Skupina zabezpečení aplikace](./media/migrate-best-practices-networking/asg.png)
*Skupina zabezpečení aplikace*

**Síťové rozhraní** | **Skupina zabezpečení aplikace**
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
Allow-Database-BusinessLogic | Povoluje provoz ze skupiny zabezpečení aplikace AsgLogic do skupiny zabezpečení aplikace AsgDb. Priorita pro toto pravidlo je vyšší než pravidlo Odepřít-Database-All, takže se toto pravidlo zpracuje jako první. Proto je povolen provoz ze skupiny zabezpečení aplikace AsgLogic a všechny ostatní přenosy budou zablokovány. | Priorita: 110<br/><br/> Zdroj: AsgLogic<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgDb<br/><br/> Cílový port: 1433<br/><br/> Protocol: TCP<br/><br/> Přístup: Povolit.

<!--markdownlint-enable MD033 -->

- Pravidla určující skupinu zabezpečení aplikace jako zdroj nebo cíl se použijí pouze na síťová rozhraní, která jsou členy příslušné skupiny zabezpečení aplikace. Pokud síťové rozhraní není členem žádné skupiny zabezpečení aplikace, pravidlo se pro něj nepoužije, ani když je k podsíti přiřazená skupina zabezpečení sítě.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) o skupinách zabezpečení aplikace.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Osvědčený postup: zabezpečení přístupu k PaaS pomocí koncových bodů služby virtuální sítě

Koncové body služby virtuální sítě rozšiřují privátní adresní prostor a identitu vaší virtuální sítě do služeb Azure přes přímé připojení.

- Koncové body umožňují zabezpečit důležité prostředky služeb Azure jenom do vašich virtuálních sítí. Provoz z vaší virtuální sítě do služby Azure vždy zůstává v páteřní síti Microsoft Azure.
- Privátní adresní prostor virtuální sítě se může překrývat, takže se nedá použít k jednoznačné identifikaci provozu pocházejícího z virtuální sítě.
- Po povolení koncových bodů služby ve vaší virtuální síti můžete prostředky služeb Azure zabezpečit tak, že do prostředků služby přidáte pravidlo virtuální sítě. Získáte tak lepší zabezpečení díky úplnému odebrání veřejného internetového přístupu k prostředkům a povolení provozu jenom z vaší virtuální sítě.

![Koncové body služby](./media/migrate-best-practices-networking/endpoint.png)
*Koncové body služby*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) o koncových bodech služby virtuální sítě.

## <a name="best-practice-control-public-ip-addresses"></a>Osvědčený postup: řízení veřejné IP adresy

Veřejné IP adresy v Azure je možné přidružit k virtuálním počítačům, nástrojům pro vyrovnávání zatížení, aplikačním branám a branám VPN.

- Veřejné IP adresy umožňují internetovým prostředkům příchozí komunikaci s prostředky Azure a prostředkům Azure odchozí komunikaci s internetem.
- Veřejné IP adresy se vytváří se základní nebo standardní SKU, mezi kterými je několik rozdílů. Standardní SKU se dají přiřadit k jakékoli službě, ale většinou se konfigurují na virtuálních počítačích, nástrojích pro vyrovnávání zatížení a aplikačních branách.
- Je důležité si uvědomit, že základní veřejná IP adresa nemá NSG automaticky nakonfigurovanou. Abyste mohli řídit přístup, musíte nakonfigurovat vlastní a přiřadit pravidla. IP adresy standardní SKU mají NSG a pravidla ve výchozím nastavení přiřazené.
- Virtuální počítače by se neměly konfigurovat s veřejnou IP adresou.
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
- Azure Firewall je plně integrovaný s Azure Monitorem, který zajišťuje protokolování a analýzy.
- Osvědčeným postupem při vytváření pravidel Azure Firewallu je použít k vytvoření pravidel značky plně kvalifikovaného názvu domény.
  - Značka plně kvalifikovaného názvu domény představuje skupinu plně kvalifikovaných názvů domén přidružených k dobře známým službám Microsoftu.
  - Značku plně kvalifikovaného názvu domény můžete použít k povolení požadovaného odchozího síťového provozu přes bránu firewall.
- Pokud třeba chcete ručně povolit síťový provoz webu Windows Update přes bránu firewall, museli byste vytvořit několik pravidel aplikace. Pomocí značek plně kvalifikovaného názvu domény můžete vytvořit pravidlo aplikace a zahrnout značku webu Windows Update. Při zavedení tohoto pravidla může síťový provoz do koncových bodů webu Microsoft Windows Update probíhat přes vaši bránu firewall.

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/firewall/overview) o Azure Firewallu.
- [Přečtěte si](https://docs.microsoft.com/azure/firewall/fqdn-tags) o značkách plně kvalifikovaného názvu domény.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Osvědčené postupy: nasazení firewallu webových aplikací (WAF)

Webové aplikace se čím dál častěji stávají cílem škodlivých útoků, které zneužívají běžně známé chyby zabezpečení. Patří k nim útoky prostřednictvím injektáže SQL nebo skriptování mezi weby. Předcházet takovým útokům v kódu aplikace může být náročné a může vyžadovat pečlivou údržbu, opravy a monitorování několika vrstev topologie aplikace. Centralizovaný Firewall webových aplikací značně zjednodušuje správu zabezpečení a pomáhá správcům aplikací lépe chránit před hrozbami nebo neoprávněným vniknutím. Firewall webové aplikace může na bezpečnostní hrozby reagovat rychleji díky opravení známých chyb zabezpečení v centrálním umístění místo zabezpečování jednotlivých webových aplikací. Stávající aplikační brány je možné jednoduše převést na aplikační brány doplněné webovým aplikačním firewallem.

Firewall webových aplikací (WAF) je funkce služby Azure Application Gateway.

- WAF poskytuje centralizovanou ochranu webových aplikací před běžným zneužitím a ohrožením zabezpečení.
- WAF chrání bez úprav back-endového kódu.
- Může chránit více webových aplikací současně za službou Application Gateway.
- WAF je integrovaný se službou Azure Security Center.
- Můžete přizpůsobit pravidla a skupiny pravidel WAF, aby vyhovovaly požadavkům vašich aplikací.
- Jako osvědčený postup byste měli WAF použít před každou aplikací s přístupem k webu, včetně aplikací na virtuálních počítačích Azure nebo jako Azure App Service.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/application-gateway/waf-overview) o WAF.
- [Podívejte se](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) na omezení a vyloučení WAF.

## <a name="best-practice-implement-azure-network-watcher"></a>Osvědčený postup: implementace Azure Network Watcher

Azure Network Watcher poskytuje nástroje pro monitorování prostředků a komunikací ve virtuální síti Azure. Můžete třeba sledovat komunikaci mezi virtuálním počítačem a koncovým bodem, jako je jiný virtuální počítač nebo plně kvalifikovaný název domény, zobrazit prostředky a vztahy prostředků ve virtuální síti nebo diagnostikovat problémy se síťovými přenosy.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Network Watcher umožňuje monitorovat a diagnostikovat síťové problémy bez přihlášení k virtuálním počítačům.
- Nastavením upozornění můžete aktivovat zachytávání paketů a získat přístup k informacím o výkonu v reálném čase na úrovni paketů. Když narazíte na problém, můžete ho prozkoumat podrobněji.
- Osvědčeným postupem je použít Network Watcher ke kontrole protokolů toku NSG.
  - Protokoly toku NSG v Network Watcheru umožňují zobrazit informace o příchozím a odchozím provozu IP přes NSG.
  - Protokoly toku se zapisují ve formátu JSON.
  - Protokoly toku zobrazují odchozí a příchozí toky pro jednotlivá pravidla, síťové rozhraní (NIC), na které se tok vztahuje, pětici informací o toku (zdrojová/cílová IP adresa, zdrojový/cílový port a protokol) a informace o tom, jestli byl provoz povolený nebo odepřený.

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/network-watcher) o Network Watcheru.
- [Přečtěte si další informace](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) o protokolech toku NSG.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Používání partnerských nástrojů v Azure Marketplace

U složitějších síťových topologií můžete použít bezpečnostní produkty od partnerů Microsoftu, zejména síťová virtuální zařízení (NVA).

- Síťové virtuální zařízení je virtuální počítač, který provádí síťovou funkci, jako je brána firewall, optimalizace sítě WAN nebo jiná síťové funkce.
- Síťová virtuální zařízení posilují zabezpečení a síťové funkce virtuální sítě. Můžou být nasazená pro vysoce dostupné brány firewall, prevenci vniknutí, detekci vniknutí, Firewall webových aplikací (WAF), optimalizaci sítě WAN, směrování, vyrovnávání zatížení, VPN, správu certifikátů, Active Directory a vícefaktorové ověřování.
- Síťová virtuální zařízení jsou k dispozici od mnoha dodavatelů v  [Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Osvědčený postup: implementace brány firewall a síťová virtuální zařízení v Centru sítí

V centru se hraniční síť (s přístupem k internetu) obvykle spravuje přes bránu firewall Azure, farmu bran firewall nebo Firewall webových aplikací (WAF). Podívejte se na následující porovnání.

<!--markdownlint-disable MD033 -->

**Typ brány firewall** | **Podrobnosti**
--- | ---
WAF | Webové aplikace jsou běžné a často bývají postižené ohroženími zabezpečení a potenciálními zneužitími.<br/><br/> WAF jsou navržené k detekci útoků proti webovým aplikacím (HTTP/HTTPS), a to konkrétněji než obecné brány firewall.<br/><br/> V porovnání s tradiční technologií brány firewall mají WAF sadu specifických funkcí, které chrání interní webové servery před hrozbami.
Brána Azure Firewall | Podobně jako farmy bran firewall síťových virtuálních zařízení používá Azure Firewall mechanismus společné správy a sadu pravidel zabezpečení k ochraně úloh hostovaných v paprskových sítích a k řízení přístupu k místním sítím.<br/><br/> Azure Firewall má integrovanou škálovatelnost.
Brány firewall síťových virtuálních zařízení | Podobně jako Azure Firewall mají farmy bran firewall síťových virtuálních zařízení mechanismus společné správy a sadu pravidel zabezpečení k ochraně úloh hostovaných v paprskových sítích a k řízení přístupu k místním sítím.<br/><br/> Brány firewall síťových virtuálních zařízení se dají ručně škálovat za nástrojem pro vyrovnávání zatížení.<br/><br/> I když má brána firewall síťového virtuálního zařízení méně specializovaný software než WAF, má širší obor aplikace k filtrování a kontrole libovolného typu provozu v odchozích i příchozích přenosech.<br/><br/> Pokud chcete používat síťové virtuální zařízení, najdete je v Azure Marketplace.

<!--markdownlint-enable MD033 -->

Doporučujeme používat jednu sadu Azure Firewallů (nebo síťových virtuálních zařízení) pro provoz z internetu a jinou pro provoz z místní sítě.

- Použití jenom jedné sady bran firewall pro oba typy provozu představuje bezpečnostní riziko, protože mezi těmito dvěma sadami síťových provozů neexistuje žádná bezpečnostní hranice.
- Použitím samostatných vrstev bran firewall se snižuje složitost pravidel pro kontrolu zabezpečení a vyjasňuje, která pravidla platí pro jednotlivé příchozí žádosti v síti.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o používání síťových virtuálních zařízení ve virtuální síti Azure.

## <a name="next-steps"></a>Další kroky

Projděte si další osvědčené postupy:

- [Osvědčené postupy](./migrate-best-practices-security-management.md) pro zabezpečení a správu po migraci
- [Osvědčené postupy](./migrate-best-practices-costs.md) pro správu nákladů po migraci
