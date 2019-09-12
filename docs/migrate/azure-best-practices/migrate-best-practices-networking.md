---
title: Osvědčené postupy pro nastavení sítě pro úlohy migrované do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Po migraci do Azure si přečtěte o osvědčených postupech pro nastavení sítě pro migrované úlohy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c3d25b0a4e421b2fa8ea5e88f6385a91721713ca
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819592"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Osvědčené postupy pro nastavení sítě pro úlohy migrovat do Azure

Jako je plánování a návrh pro migraci, kromě migrace, jedním z nejdůležitějších kroků je návrh a implementaci sítí Azure. Tento článek popisuje osvědčené postupy pro sítě při migraci do implementace IaaS a PaaS v Azure.

> [!IMPORTANT]
> Osvědčené postupy a názory, které jsou popsané v tomto článku jsou založené na platformě Azure a služby funkce dostupné v době zápisu. Funkce a možnosti v průběhu času měnit. Ne všechna doporučení může být pro vaše nasazení, takže vyberte ty, které vám vyhovují.

## <a name="design-virtual-networks"></a>Návrh virtuální sítě

Azure poskytuje virtuální sítě (Vnet):

- Prostředky Azure, komunikovat soukromě, přímo a bezpečně s jinými přes virtuální sítě.
- Ve virtuálních sítích můžete nakonfigurovat koncový bod připojení pro virtuální počítače a služby, které vyžadují internetovou komunikaci.
- Virtuální sítě se o logickou izolaci cloudu Azure, který je vyhrazen pro vaše předplatné.
- Můžete implementovat více virtuálními sítěmi v rámci každého předplatného Azure a oblastí Azure.
- Každá virtuální síť je izolovaná od jiných virtuálních sítí.
- Virtuální sítě můžou obsahovat privátní a veřejné IP adresy definované v [RFC 1918](https://tools.ietf.org/html/rfc1918), vyjádřené v zápisu CIDR. Veřejné IP adresy specifikované v adresním prostoru virtuální sítě nejsou přímo přístupné z internetu.
- Virtuální sítě se k sobě navzájem můžou připojit pomocí peeringu virtuálních sítí. Připojené virtuální sítě může být v jedné nebo několika oblastech. Proto prostředky v jedné virtuální síti můžou připojit k prostředkům v jiných virtuálních sítí.
- Azure ve výchozím nastavení směruje provoz mezi podsítěmi v rámci virtuální sítě, propojenými virtuálními sítěmi, místními sítěmi a internetem.

Při plánování topologie virtuální sítě byste měli zvážit, jak uspořádat adresní prostory IP adres, jak implementovat hvězdicovou topologii sítě, jak rozdělit virtuální sítě do podsítí, nastavit DNS a implementovat zóny dostupnosti Azure.

## <a name="best-practice-plan-ip-addressing"></a>Osvědčený postup: Plánování přidělování IP adres

Když vytvoříte virtuální sítě jako součást migrace, je důležité naplánovat adresní prostor IP adres virtuální sítě.

- Byste měli přiřadit adresní prostor, který není větší než rozsah CIDR /16 pro každou virtuální síť. Virtuální sítě umožňují používání 65536 IP adresy a přiřazování předponu menší než/16 by vést ke ztrátě IP adres. Je důležité, abyste odpad IP adres, i v případě, že jsou v rozsahy privátních, které jsou definovány v dokumentu RFC 1918.
- Adresní prostor virtuální sítě se nesmí překrývat s rozsahy adres místní sítě.
- Překlad síťových adres (NAT) se nesmí používat.
- Překrývající se adresy může způsobit sítě, které nemůže být připojen a směrování, která nebude fungovat správně. Pokud sítě se překrývají, bude potřeba změnit návrh sítě, nebo použijte překlad síťových adres (NAT).

**Víc se uč:**

- [Získejte přehled](/azure/virtual-network/virtual-networks-overview) virtuálních sítí Azure.
- [Čtení](/azure/virtual-network/virtual-networks-faq) sítě – nejčastější dotazy.
- [Přečtěte si](/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) o omezeních sítí.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Osvědčený postup: Implementace hvězdicové topologie sítě

Hvězdicová topologie sítě izoluje úlohy a současně sdílí služby, jako je identita a zabezpečení.

- Centrum této topologie je virtuální síť Azure, která funguje jako centrální bod připojení.
- Paprsky jsou virtuální sítě, které se připojit k virtuální síti centra pomocí VNet peering.
- Sdílené služby jsou nasazené v centru, zatímco individuální úlohy jsou nasazené jako paprsky.

Zvažte použití těchto zdrojů:

- Implementace hvězdicové topologii v Azure centralizuje běžné služby jako připojení k místním sítím, brány firewall a izolaci mezi virtuálními sítěmi. Virtuální síť centra poskytuje centrální bod připojení k místním sítím a místo, kde můžete hostitele služby používají ve úlohami hostovanými ve virtuálních sítích paprsků.
- Hvězdicové konfigurace se obvykle používá ve velkých podnicích. Menší sítě může zvážit jednodušší návrh a Šetřete na náklady a složitost.
- Virtuální sítě paprsků slouží k izolaci úloh, pomocí každého paprsku se spravují odděleně od ostatních paprsků. Každá úloha může obsahovat několik vrstev a více podsítí, které jsou propojeny se nástroje pro vyrovnávání zatížení Azure.
- Virtuální sítě s hvězdicovou topologií je možné implementovat v různých skupinách prostředků, a dokonce i v různých předplatných. Při peeringu virtuálních sítí v různých předplatných můžou být předplatná přidružená ke stejným nebo jiným tenantům Azure Active Directory (Azure AD). To umožňuje decentralizovanou správu každé úlohy při sdílení služeb udržovaných v centrální virtuální síti.

![Správa změn](./media/migrate-best-practices-networking/hub-spoke.png)
*hvězdicové topologie*

**Víc se uč:**

- [Přečtěte si informace o](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) hvězdicové topologii.
- Získejte doporučení pro síť pro provoz Azure [Windows](/azure/architecture/reference-architectures/n-tier/windows-vm) a [Linux](/azure/architecture/reference-architectures/n-tier/linux-vm) virtuálních počítačů.
- [Přečtěte si](/azure/virtual-network/virtual-network-peering-overview) o peeringu virtuálních sítí.

## <a name="best-practice-design-subnets"></a>Osvědčený postup: Návrh podsítí

Izolace v rámci virtuální sítě se dosahuje její segmentací do jedné nebo několika podsítí a přidělením části adresního prostoru virtuální sítě každé podsíti.

- Můžete vytvořit více podsítí v rámci každé virtuální síti.
- Ve výchozím nastavení Azure směrování síťového provozu mezi všemi podsítěmi ve virtuální síti.
- Vaše podsíť rozhodnutí, která jsou založeny na technická a organizační požadavky.
- Vytvoření podsítě se používá zápis CIDR.
- Při rozhodování o rozsahu sítě pro podsítě, je důležité si uvědomit, že Azure uchovává 5 IP adres z každé podsítě, které nelze použít. Například pokud vytvoříte nejmenší dostupné podsítě minimální velikostí/29 (s osmi IP adresy), Azure si zachovají pět adres, abyste měli tři použitelné adresy, které je možné přiřadit k hostitelům v podsíti.
- Ve většině případů se doporučuje použít jako nejmenší podsíť /28.

**Příklad:**

V tabulce je zobrazený příklad virtuální sítě s adresním prostorem 10.245.16.0/20 rozděleným do podsítí pro plánovanou migraci.

**Podsíť** | **CIDR** | **Adresy** | **Použití**
--- | --- | --- | ---
DEV-FE – EUS2 | 10.245.16.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Virtuální počítače vrstvy aplikace
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Virtuální počítače databáze

**Víc se uč:**

- [Přečtěte si](/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) o navrhování podsítí.
- [Zjistěte](/azure/migrate/contoso-migration-infrastructure), jak fiktivní společnost (Contoso) připravila svoji síťovou infrastrukturu pro migraci.

## <a name="best-practice-set-up-a-dns-server"></a>Osvědčený postup: Nastavení serveru DNS

Když nasadíte virtuální síť, Azure ve výchozím nastavení přidá server DNS. To umožňuje rychle vytvořit virtuální sítě a nasazení prostředků. Tento server DNS však pouze poskytuje služby pro prostředky v této virtuální síti. Pokud chcete propojení více virtuálních sítí nebo připojení k místnímu serveru z virtuální sítě, je nutné další název možnosti řešení. Například můžete potřebovat služby Active Directory k překladu názvů DNS mezi virtuálními sítěmi. K tomuto účelu nasazení vlastní vlastní server DNS v Azure.

- Servery DNS ve virtuální síti, může předat dotazy DNS na rekurzivní překladače v Azure. To umožňuje překládat názvy hostitelů v rámci této virtuální síti. Například řadič domény spuštěný v Azure můžete odpovídat na dotazy DNS pro vlastní domény a předávat všechny ostatní dotazy k Azure.
- Předávání DNS umožňuje virtuálních počítačů určených k místním prostředkům (prostřednictvím řadič domény) a názvy hostitelů poskytuje Azure (s použitím předávání). Poskytuje přístup k rekurzivní překladače v Azure pomocí virtuální IP adresy 168.63.129.16.
- Předávání DNS také umožňuje překlad názvů DNS mezi virtuálními sítěmi a povoluje místních počítačů k překladu názvů hostitelů poskytovaný platformou Azure.
  - Přeložit název hostitele virtuálního počítače, server DNS virtuálního počítače se musí nacházet ve stejné virtuální síti a nakonfigurovat tak, aby dotazy na názvy dopředné hostitele do Azure.
  - Protože přípona DNS se liší v každé virtuální síti, můžete použít pravidla pro podmíněné předávání k odesílání dotazů DNS na správnou virtuální síť pro překlad.
- Pokud používáte vlastní servery DNS, můžete zadat víc serverů DNS pro každou virtuální síť. Můžete také zadat víc serverů DNS na síťové rozhraní (pro Azure Resource Manageru), nebo za cloudové služby (v případě modelu nasazení classic).
- Servery DNS zadaný pro síťové rozhraní nebo cloudové služby mají přednost před serverů DNS má zadaný pro virtuální síť.
- V modelu nasazení Azure Resource Manageru můžete určit servery DNS pro virtuální sítě a síťové rozhraní, ale osvědčeným postupem je použít jenom ve virtuálních sítích.

    ![Servery DNS](./media/migrate-best-practices-networking/dns2.png) *servery DNS pro virtuální síť*

**Víc se uč:**

- [Další informace o](/azure/migrate/contoso-migration-infrastructure) překlad názvů při použití vlastního serveru DNS.
- [Přečtěte si](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-subscriptions) o pravidlech a omezeních pro pojmenování DNS.

## <a name="best-practice-set-up-availability-zones"></a>Osvědčený postup: Nastavení zón dostupnosti

Zóny dostupnosti zvyšují vysokou dostupnost a chrání vaše aplikace a data před selháními datacenter.

- Zóny dostupnosti jsou jedinečná fyzická umístění v rámci oblasti Azure.
- Každá zóna se skládá z jednoho nebo více datových Center vybavených nezávislým napájením, chlazením a sítí.
- K zajištění odolnosti proti chybám, je minimálně tří samostatných zón ve všech oblastech, povolené.
- Fyzické oddělení zón dostupnosti v rámci oblasti chrání aplikace a data před selháními datových center.
- Zónově redundantní služby replikovat napříč zónami dostupnosti pro zajištění ochrany z jediné body selhání aplikace a data. --Se zónami dostupnosti Azure nabízí smlouvu SLA o 99,99 % dostupnosti virtuálního počítače.

    ![Zóna dostupnosti](./media/migrate-best-practices-networking/availability-zone.png) *zóně dostupnosti*

- Můžete naplánovat a sestavit vysokou dostupností do architektury migrace společné umístění výpočetní prostředky, úložiště, sítě a zdroje dat v rámci zóny a replikace v jiné zóně. Služby Azure, které podporují zóny dostupnosti, spadají do dvou kategorií:
  - Zónové služby: Spojíte prostředek s konkrétní zónou. Třeba virtuální počítače, spravované disky, IP adresy.
  - Zónově redundantní služby: Prostředek se automaticky replikuje mezi zónami. Třeba zónově redundantní úložiště, Azure SQL Database.
- Můžete nasadit standardní Azure zatížení vyrovnávaném pomocí úloh přístupem k Internetu nebo aplikačních vrstvách pro zónové odolné proti chybám.

    ![Nástroj pro vyrovnávání zatížení](./media/migrate-best-practices-networking/load-balancer.png) *nástroje pro vyrovnávání zatížení*

**Víc se uč:**

- [Získejte přehled](/azure/availability-zones/az-overview) zón dostupnosti.

## <a name="design-hybrid-cloud-networking"></a>Návrh hybridní cloudové sítě

Pro úspěšnou migraci je velmi důležité pro připojení k Azure v místním podnikovým sítím. Tím se vytvoří připojení vždy na označuje jako síť hybridního cloudu, kde jsou k dispozici služby Azure cloud pro podnikové uživatele. Existují dvě možnosti, jak tento typ sítě vytvořit:

- **Site-to-site VPN:** Zřídíte připojení site-to-site mezi kompatibilním místním zařízením VPN a branou Azure VPN nasazenou ve virtuální síti. K virtuální síti může přistupovat jakýkoli autorizovaný místní prostředek. Komunikace site-to-site se odesílají prostřednictvím šifrovaného tunelu přes internet.
- **Azure ExpressRoute:** Zřídíte připojení Azure ExpressRoute mezi vaší místní sítí a Azure prostřednictvím partnera ExpressRoute. Toto připojení je privátní a přenos neprobíhá přes internet.

**Víc se uč:**

- [Přečtěte si](/azure/architecture/reference-architectures/hybrid-networking/vpn) další informace o hybridních cloudových sítích.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Osvědčený postup: Implementace vysoce dostupného site-to-site VPN

K implementaci site-to-site VPN nastavíte bránu VPN v Azure.

- Brána VPN je konkrétní typ brány virtuální sítě, který slouží k posílání šifrovaného provozu mezi virtuální sítí VNet Azure a místním umístěním přes veřejný Internet.
- Bránu sítě VPN můžete použít také k posílání šifrovaného provozu mezi virtuálními sítěmi Azure po síti Microsoftu.
- Každá virtuální síť může mít pouze jednu bránu VPN.
- Můžete vytvořit několik připojení ke stejné bráně VPN. Když vytvoříte několik připojení, všechny tunely VPN sdílejí dostupnou šířku pásma.
- Každá Azure VPN Gateway se skládá ze dvou instancí v konfiguraci aktivní-pohotovostní.
  - Při plánované údržbě nebo neplánovaném přerušení aktivní instance dojde k převzetí služeb při selhání a pohotovostní instance automaticky převezme službu a obnoví spojení site-to-site nebo VNet-to-VNet.
  - Toto přepnutí způsobí krátké přerušení.
  - Při plánované údržbě by se spojení mělo obnovit během 10 až 15 sekund.
  - U neplánovaných problémů trvá obnovení spojení déle, v nejhorším případě minutu až minutu a půl.
  - Připojení klienta VPN typu point-to-site (P2S) k bráně se odpojí a uživatelé se budou muset na klientských počítačích znovu připojit.

Při nastavování site-to-site VPN:

- Potřebujete virtuální síť, jejíž rozsah adres se nepřekrývá s místní sítí, ke které se VPN připojí.
- V síti vytvoříte podsíť brány.
- Vytvoření brány VPN, zadejte typ brány (VPN) a určuje, zda je brána na základě zásad nebo založené na směrování. Síť VPN typu RouteBased se doporučuje jako více podporující a budoucnosti.
- Místní vytvoření brány místní sítě a nakonfigurujte místní zařízení VPN.
- Vytvoříte převzetí služeb při selhání připojení VPN typu site-to-site mezi bránou virtuální sítě a místním zařízením. Pomocí sítě VPN založené na trasách umožňuje aktivní pasivní nebo aktivní aktivní připojení k Azure. Založené na trasách také podporuje připojení point-to-site (z jednoho počítače) i připojení site-to-site (z libovolného počítače) současně.
- Můžete určit SKU brány, kterou chcete použít. Bude to záviset na požadavky úloh, propustnosti, funkcí a smlouvy o úrovni služeb.
- Border gateway protocol (BGP) je volitelná funkce vám pomůže s Azure ExpressRoute a VPN Gateway založená na trasách rozšířit místní trasy protokolu BGP pro vaše virtuální sítě.

![VPN](./media/migrate-best-practices-networking/vpn.png)
*Site-to-site VPN*

**Víc se uč:**

- [Kontrola](/azure/vpn-gateway/vpn-gateway-about-vpn-devices) kompatibilní s místními zařízeními VPN.
- [Získejte přehled](/azure/vpn-gateway/vpn-gateway-about-vpngateways) bran VPN.
- [Další informace o](/azure/vpn-gateway/vpn-gateway-highlyavailable) vysoce dostupných připojení VPN.
- [Další informace o](/azure/vpn-gateway/vpn-gateway-plan-design) plánování a navrhování bránu VPN.
- [Kontrola](/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) nastavení služby VPN gateway.
- [Kontrola](/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) SKU brány.
- [Přečtěte si](/azure/vpn-gateway/vpn-gateway-bgp-overview) o nastavení protokolu BGP s branami Azure VPN.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Osvědčený postup: Konfigurace brány pro brány VPN

Když vytvoříte bránu VPN v Azure, musíte použít speciální podsíť s názvem GatewaySubnet. Při vytváření této podsítě Poznámka těchto osvědčených postupů:

- Délka předpony podsítě brány může mít délku maximální předpony 29 (například 10.119.255.248/29). Aktuální doporučení je, že používáte délka předpony 27 (například 10.119.255.224/27).
- Při definování adresní prostor podsítě brány použijte poslední části adresního prostoru virtuální sítě.
- Pokud používáte Azure GatewaySubnet, nikdy neměli nasazovat všechny virtuální počítače nebo jiné zařízení, jako jsou Application Gateway do podsítě brány.
- Nepřiřazovat skupinu zabezpečení sítě (NSG) k této podsíti. To způsobí, že je brána přestane fungovat.

**Víc se uč:**

- [Pomocí tohoto nástroje](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) můžete zjistit svůj adresní prostor IP adres.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Osvědčený postup: Implementace Azure Virtual WAN pro pobočky

Pro více připojení VPN je Azure Virtual WAN síťová služba poskytující optimalizované a automatizované možnosti propojení jednotlivých poboček prostřednictvím Azure.

- Virtuální síť WAN umožňuje připojit a nakonfigurovat zařízení v pobočkách tak, aby komunikovala přes Azure. Můžete to udělat ručně nebo pomocí zařízení od preferovaného poskytovatele prostřednictvím partnera pro Virtual WAN.
- Používání preferované poskytovatele zařízení umožňuje použití, připojení a konfigurace správy.
- Azure WAN integrovaný řídicí panel poskytuje okamžitý přehled o řešení problémů, které šetří čas a poskytují snadný způsob, jak sledovat ve velkém měřítku připojení site-to-site.

**Další informace:** 
[Přečtěte si](/azure/virtual-wan/virtual-wan-about) o Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Osvědčený postup: Implementace ExpressRoute pro klíčová připojení

Služba Azure ExpressRoute rozšiřuje vaši místní infrastrukturu do cloudu Microsoftu tím, že vytváří privátní připojení mezi virtuálním datacentrem Azure a místními sítěmi.

- Připojení ExpressRoute můžou být prostřednictvím sítě any-to-any (IP VPN), sítě Ethernet point-to-point nebo prostřednictvím poskytovatele připojení. Jejich nenavazují přes veřejný internet.
- Připojení ExpressRoute nabízejí vyšší úroveň zabezpečení, spolehlivost a vyšších rychlostí (až 10 GB/s), spolu s konzistentní latence.
- ExpressRoute je užitečné pro virtuální datová centra, jak zákazníci mohou získat výhody pravidla dodržování předpisů, které jsou přidružené k připojení privátní sítě.
- S ExpressRoute Direct můžete připojit přímo k směrovače Microsoftu na 100Gbps pro potřeby větší šířku pásma.
- ExpressRoute používá protokol BGP pro výměnu tras mezi místními sítěmi, instancí Azure a veřejnými adresami Microsoftu.

Nasazení připojení ExpressRoute obvykle zahrnuje angažování poskytovatel služeb ExpressRoute. Pro rychlé zprovoznění se běžně používá site-to-site VPN k navázání připojení mezi virtuálním datacentrem a místními prostředky a následná migrace na připojení ExpressRoute, když je navázané fyzické propojení s vaším poskytovatelem služeb.

**Další informace:**

- [Přečtěte si přehled](/azure/expressroute/expressroute-introduction) ExpressRoute.
- [Přečtěte si](/azure/expressroute/expressroute-erdirect-about) o ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Osvědčený postup: Optimalizace směrování ExpressRoute s využitím komunit BGP

Pokud máte víc okruhů ExpressRoute, máte více než jednu cestu, jak se připojit k Microsoftu. V důsledku toho může dojít k neoptimálnímu směrování a přenosy dat mezi vaší sítí a Microsoftem mohou použít delší cestu. Čím delší je síťová cesta, tím větší je latence. Latence má přímý vliv na výkon aplikací a zkušenosti uživatelů.

**Příklad:**

Pojďme se podívat na příklad:

- Máte dvě pobočky v USA, jednu v Los Angeles a jednu v New Yorku.
- Vaše pobočky jsou připojené v síti WAN, což může být vlastní páteřní sítě nebo VPN IP poskytovatele služeb.
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

Abyste optimalizovali směrování pro uživatele obou poboček, musíte vědět, která předpona je z oblasti Azure USA – západ a která z Azure USA – východ. Tyto informace můžete kódovat s použitím hodnoty komunity protokolu BGP.

- Každé oblasti Azure přiřadíte jedinečnou hodnotu komunity protokolu BGP. Třeba 12076:51004 pro USA – východ, 12076:51006 pro USA – západ.
- Když je teď jasné, která předpona patří ke které oblasti Azure, můžete nakonfigurovat upřednostňovaný okruh ExpressRoute.
- Vzhledem k tomu, že k výměně informací o směrování používáte protokol BGP, můžete k ovlivnění směrování použít místní preferenci protokolu BGP.
- V našem příkladu přiřadíte vyšší místní preferenci pro 13.100.0.0/16 v oblasti USA – západ než v oblasti USA – východ a obdobně vyšší místní preferenci pro 23.100.0.0/16 v oblasti USA – východ než USA – západ.
- Tato konfigurace zajišťuje, že při cesty společnosti Microsoft jsou k dispozici, uživatelé v Los Angeles se připojí k Azure USA – západ – západ okruh pomocí i uživatelé New Yorku k Azure USA – východ připojit pomocí – východ okruh. Směrování je optimalizované na obou stranách.

![VPN](./media/migrate-best-practices-networking/bgp2.png)
*komunit protokolu BGP optimalizované připojení*

**Další informace:**

- [Přečtěte si](/azure/expressroute/expressroute-optimize-routing) o optimalizaci směrování.

## <a name="securing-vnets"></a>Zabezpečení virtuálních sítí

Zodpovědnost za zabezpečení virtuálních sítí je sdílená mezi Microsoftem a vámi. Microsoft poskytuje mnoho síťových funkcí a služeb, které pomáhají zajistit zabezpečení zdrojů. K osvědčeným postupům při navrhování zabezpečení pro virtuální sítě patří implementace hraniční sítě, použití filtrování a skupin zabezpečení, zabezpečení přístupu k prostředkům a IP adresám a implementace ochrany před útoky.

**Další informace:**

- [Získejte přehled](/azure/security/azure-security-network-security-best-practices) osvědčených postupů pro zabezpečení sítě.
- [Zjistěte](/azure/virtual-network/virtual-network-vnet-plan-design-arm#security), jak navrhovat zabezpečené sítě.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Osvědčený postup: Implementace hraniční sítě Azure

I když Microsoft do cloudové infrastruktury výrazně investuje, musíte chránit také své cloudové služby a skupiny prostředků. S více vrstvami přístup k zabezpečení poskytuje nejlepší ochranu. Vložení do hraniční sítě v místě je důležitou součástí strategie je, že ochranu.

- Hraniční síť chrání prostředkům v interní síti z nedůvěryhodné sítě.
- Je nejkrajnější vrstvy, který je přístupný z Internetu. Obecně nachází se mezi Internetem a podnikovou infrastrukturou, obvykle s určitou formu ochrany na obou stranách.
- V typické podnikové síťové topologie základní infrastruktury silně přidá na perimetry, s víc vrstvami zabezpečení zařízení. Hranice každou vrstvu se skládá ze zařízení a body vynucení zásad.
- Každá vrstva může obsahovat kombinaci řešení zabezpečení sítě, které zahrnují brány firewall, ochrany před únikem informací s cílem odepření služby (DoS), systémů ochrany zjišťování/vniknutí neoprávněného vniknutí (IDS/IPS) a zařízení VPN.
- Vynucení zásad v hraniční síti můžete použít zásady brány firewall, seznamy řízení přístupu (ACL) nebo konkrétní směrování.
- Protože doručena příchozí provoz z Internetu, má zachytit a zpracovat kombinaci řešení ochrany před mobilními útoky bloku a škodlivého provozu, dovolující oprávněné požadavky na síť.
- Příchozí provoz směrovat přímo k prostředkům v hraniční síti. Prostředek hraniční sítě může komunikovat s jiným prostředkům hlouběji v síti, přesun vpřed provoz do sítě po ověření.

Následující obrázek znázorňuje příklad hraniční síti jedinou podsítí v podnikové síti, s dvěma hranice zabezpečení.

![VPN](./media/migrate-best-practices-networking/perimeter.png)
*nasazení hraniční sítě*

**Víc se uč:**

- [Přečtěte si](/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o nasazení hraniční sítě mezi Azure a vaším místním datacentrem.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Osvědčený postup: Filtrování provozu virtuálních sítí pomocí skupin zabezpečení sítě

Skupiny zabezpečení sítě (NSG) obsahují několik příchozích a odchozích pravidel zabezpečení, která filtrují přenosy přicházející do a z prostředků. Filtrování může být ve zdrojové a cílové IP adresy, portu a protokolu.

- Skupiny zabezpečení sítě obsahují pravidla zabezpečení, které povolit nebo odepřít příchozí síťové přenosy do (nebo odchozí síťový provoz ze) několik typů prostředků Azure. Pro každé pravidlo můžete určit zdroj a cíl, port a protokol.
- Pravidla skupiny zabezpečení sítě jsou vyhodnocovány podle priority, pomocí informací o pěti řazené kolekce členů (zdroj, zdrojový port, cíl, cílový port a protokol) která povolí nebo zakážou provoz.
- Pro stávající připojení se vytvoří záznam toku. Komunikace se povoluje nebo odepírá na základě stavu připojení v záznamu toku.
- Záznam flow umožňuje stavové existenci NSG. Například pokud chcete zadat odchozí pravidlo zabezpečení na jakoukoli adresu přes port 80, není nutné příchozí pravidlo zabezpečení pro reakci na odchozí provoz. Příchozí pravidlo zabezpečení je potřeba zadat pouze v případě, že se komunikace zahajuje externě.
- Opačně to platí také. Pokud je povolený příchozí provoz přes port, není nutné zadat odchozí pravidlo zabezpečení pro reakci na provoz přes port.
- Existující připojení nepřerušily při odebrání pravidla zabezpečení, který povolen tok. Přenosové toky jsou přerušen, připojení se zastaví a žádný provoz se přenášejí v obou směrech po dobu aspoň pár minut.
- Skupin zabezpečení sítě vytvořte co nejméně, ale tolik, kolik je nezbytných.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Osvědčený postup: Zabezpečení provozu sever/jih a východ/západ

Při zabezpečování virtuálních sítí je důležité vzít v úvahu vektory útoku.

- Použití pouze skupiny Nsg podsítě se prostředí zjednoduší, ale pouze zabezpečuje provoz do podsítě. To se označuje jako north/south provoz.
- Provoz mezi virtuálními počítači ve stejné podsíti se označuje jako provoz východ/západ.
- Je důležité používat obě formy ochrany, aby v případě, že hacker získá přístup zvenčí, byl zastaven při pokusu o připojení počítačů umístěných ve stejné podsíti.

### <a name="use-service-tags-on-nsgs"></a>Použití značek služeb na skupiny zabezpečení sítě

Značka služby představuje skupinu předpon IP adres. Použití značku služby pomáhá minimalizovat složitost vytváření pravidla skupiny zabezpečení sítě.

- Značky služeb můžete používat místo konkrétních IP adres při vytváření pravidel.
- Společnost Microsoft spravuje předpony adres, které jsou přidružené k značku služby a automaticky značku služby aktualizuje při změně adres.
- Nelze vytvořit vlastní značku služby ani určit, které IP adresy jsou ve značce zahrnuté.

Značky služeb vyžadují ruční práce z pravidla přiřazení do skupin služby Azure. Například pokud chcete povolit virtuální síť podsíť obsahující webové servery pro přístup ke službě Azure SQL Database, můžete vytvořit pravidlo odchozí port 1433 a použít **Sql** značka služby.

- To **Sql** značka označuje předpony adres služeb Azure SQL Database a Azure SQL Data Warehouse.
- Pokud zadáte **Sql** jako hodnotu, provoz je povolený nebo zakázaný jazyka SQL.
- Pokud chcete povolit přístup k **Sql** v konkrétní oblasti, můžete zadat tuto oblast. Například pokud chcete povolit přístup pouze ke službě Azure SQL Database v oblasti východní USA, můžete zadat **Sql.EastUS** jako značku služby.
- Značka představuje službu, ale ne konkrétní instance služby. Značka například představuje službu Azure SQL Database, ale nepředstavuje konkrétní SQL database nebo serveru.
- Všechny předpony adres reprezentované touto značkou jsou reprezentované také značkou **Internet**.

**Víc se uč:**

- [Přečtěte si informace o](/azure/virtual-network/security-overview) skupin zabezpečení sítě.
- [Podívejte se](/azure/virtual-network/security-overview#service-tags) na značky služby, které jsou k dispozici pro skupiny zabezpečení sítě.

## <a name="best-practice-use-application-security-groups"></a>Osvědčený postup: Použití skupin zabezpečení aplikace

Skupiny zabezpečení aplikace umožňují konfigurovat zabezpečení sítě jako přirozené rozšíření struktury aplikace.

- Můžete seskupit virtuální počítače a definovat zásady zabezpečení sítě na základě skupin zabezpečení aplikací.
- Skupiny zabezpečení aplikací umožňují snadno opakovaně používat zásady zabezpečení ve velkém měřítku bez potřeby ruční údržby explicitních IP adres.
- O složitost explicitních IP adres a několika skupin pravidel se starají skupiny zabezpečení aplikace, takže se vy můžete zaměřit na obchodní logiku.

**Příklad:**

![Skupina zabezpečení aplikace](./media/migrate-best-practices-networking/asg.png)
*Skupina zabezpečení aplikace*

**Síťové rozhraní** | **Skupiny zabezpečení aplikací**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- V našem příkladu každé síťové rozhraní patří do pouze jednu skupinu zabezpečení aplikace, ale ve skutečnosti rozhraní patří do více skupin, v souladu s omezení v Azure.
- Žádný ze síťových rozhraní nemá přidruženou skupinu NSG. NSG1 je přidružená k obě podsítě a obsahuje následující pravidla.

<!--markdownlint-disable MD033 -->

**Název pravidla** | **Účel** | **Podrobnosti**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Povolte přenosy z Internetu k webovým serverům. Výchozí pravidlo zabezpečení DenyAllInbound odepírá příchozí provoz z internetu, takže pro skupiny zabezpečení aplikace AsgLogic a AsgDb není potřeba žádné další pravidlo. | Priorita: 100<br/><br/> Zdroj: internet<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgWeb<br/><br/> Cílový port: 80<br/><br/> Protokol: TCP<br/><br/> Přístup: Povolit.
Deny-Database-All | Výchozí pravidlo zabezpečení AllowVNetInBound povoluje veškerou komunikaci mezi prostředky ve stejné virtuální síti, takže toto pravidlo je potřeba k odepření provozu ze všech prostředků. | Priorita: 120<br/><br/> Zdroj: *<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgDb<br/><br/> Cílový port: 1433<br/><br/> Protokol: Vše<br/><br/> Přístup: Odepřít.
Allow-Database-BusinessLogic | Povoluje provoz ze skupiny zabezpečení aplikace AsgLogic do skupiny zabezpečení aplikace AsgDb. Priorita pro toto pravidlo je vyšší než pro pravidlo Deny-Database-All a zpracovává se před ním, takže se povolí provoz ze skupiny zabezpečení aplikace AsgLogic a veškerý ostatní provoz se zablokuje. | Priorita: 110<br/><br/> Zdroj: AsgLogic<br/><br/> Zdrojový port: *<br/><br/> Cíl: AsgDb<br/><br/> Cílový port: 1433<br/><br/> Protokol: TCP<br/><br/> Přístup: Povolit.

<!--markdownlint-enable MD033 -->

- Pravidla určující skupinu zabezpečení aplikace jako zdroj nebo cíl se použijí pouze na síťová rozhraní, která jsou členy příslušné skupiny zabezpečení aplikace. Pokud síťové rozhraní není členem žádné skupiny zabezpečení aplikace, pravidlo se pro něj nepoužije, ani když je k podsíti přiřazená skupina zabezpečení sítě.

**Víc se uč:**

- [Přečtěte si](/azure/virtual-network/security-overview#application-security-groups) o skupinách zabezpečení aplikace.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Osvědčený postup: Zabezpečení přístupu k PaaS pomocí koncových bodů služby virtuální sítě

Koncové body služby virtuální sítě rozšiřují privátní adresní prostor a identitu vaší virtuální sítě do služeb Azure přes přímé připojení.

- Koncové body umožňují zabezpečit důležité prostředky služeb Azure pro vaše virtuální sítě pouze. Provoz z vaší virtuální sítě do služby Azure vždy zůstává v páteřní síti Microsoft Azure.
- Privátní adresní prostor virtuální sítě můžou se překrývat a proto jej nelze použít k jednoznačné identifikaci přenos dat pocházejících z jedné virtuální sítě.
- Jakmile se ve vaší virtuální síti povolené koncové body služby, můžete svázat prostředky služeb Azure tak, že přidáte pravidlo virtuální sítě k prostředkům služby. To poskytuje lepší zabezpečení díky úplnému odebrání veřejného internetového přístupu k prostředkům a povolení provozu pouze z vaší virtuální sítě.

![Koncové body služby](./media/migrate-best-practices-networking/endpoint.png)
*koncové body služby*

**Víc se uč:**

- [Přečtěte si](/azure/virtual-network/virtual-network-service-endpoints-overview) o koncových bodech služby virtuální sítě.

## <a name="best-practice-control-public-ip-addresses"></a>Osvědčený postup: Řízení veřejných IP adres

Veřejné IP adresy v Azure je možné přidružit k virtuálním počítačům, nástrojům pro vyrovnávání zatížení, aplikačním branám a branám VPN.

- Veřejné IP adresy umožňují internetovým prostředkům příchozí komunikaci s prostředky Azure a prostředkům Azure odchozí komunikaci s internetem.
- Veřejné IP adresy se vytváří se základní nebo standardní SKU, mezi kterými je několik rozdílů. Standardní SKU se dají přiřadit k jakékoli službě, ale většinou se konfigurují na virtuálních počítačích, nástrojích pro vyrovnávání zatížení a aplikačních branách.
- Je důležité si uvědomit, že základní veřejnou IP adresu nemusí automaticky nakonfiguruje skupiny NSG. Budete muset nakonfigurovat vlastní a přiřadit pravidla pro řízení přístupu. Standardní SKU IP adres máte skupinu zabezpečení sítě a pravidel přiřazené ve výchozím nastavení.
- Jako osvědčený postup by neměl být virtuální počítače nakonfigurované s použitím veřejné IP adresy.
  - Pokud potřebujete otevřít port, mělo by být pouze pro webové služby, jako je port 80 nebo 443.
  - Porty standardní vzdálené správy, jako jsou SSH (22) a protokolu RDP (3389) je třeba nastavit na odepřít, spolu s všech ostatních portech pomocí skupin zabezpečení sítě.
- Je doporučeno umístit virtuální počítače s bránou Azure load balancer nebo aplikace. V případě potřeby přístup k portům pro vzdálenou správu můžete použít v čase přístup k virtuálním počítačům v Azure Security Center.

**Víc se uč:**

- [Další informace o](/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses) veřejné IP adresy v Azure.
- [Přečtěte si další informace](/azure/security-center/security-center-just-in-time) o přístupu k virtuálnímu počítači podle potřeby v Azure Security Center.

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Využití funkcí zabezpečení Azure pro sítě

Azure má funkce zabezpečení platformy, které se snadno používají a poskytují bohatou škálu opatření proti běžným síťovým útokům. Patří k nim Azure Firewall, firewall webových aplikací a Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Osvědčený postup: Nasazení Azure Firewallu

Azure Firewall je spravovaná cloudová služba síťového zabezpečení, která chrání vaše prostředky ve virtuálních sítích. Jde o plně stavovou spravovanou bránu firewall s integrovanou vysokou dostupností a neomezenou cloudovou škálovatelností.

![Koncové body služby](./media/migrate-best-practices-networking/firewall.png)
*Azure Firewall*

- Azure Firewall může centrálně vytvářet, vynucovat a protokolovat zásady připojení k aplikacím a sítím napříč různými předplatnými a virtuálními sítěmi.
- Brána Azure Firewall používá statickou veřejnou IP adresu pro prostředky virtuální sítě a díky tomu umožňuje venkovním bránám firewall identifikovat provoz pocházející z vaší virtuální sítě.
- Brány Firewall na Azure je plně integrované s Azure Monitor pro protokolování a analýza.
- Jako osvědčený postup při vytváření pravidel brány Firewall na Azure vytvořte pravidla pomocí značek plně kvalifikovaný název domény.
  - Značku plně kvalifikovaný název domény představuje skupinu plně kvalifikované názvy domén, které jsou spojené s dobře známými službami Microsoftu.
  - Použít značku plně kvalifikovaný název domény Pokud chcete povolit požadované odchozí síťové přenosy přes bránu firewall.
- Například pokud chcete ručně povolit aktualizace Windows síťové přenosy přes bránu firewall, je třeba vytvořit víc pravidel aplikace. Pomocí značek plně kvalifikovaný název domény, vytvoření pravidla pro aplikace a zahrnují značku aktualizace Windows. S tímto pravidlem na místě síťového provozu do koncových bodů služby Microsoft Windows Update probíhá přes bránu firewall.

**Víc se uč:**

- [Získejte přehled](/azure/firewall/overview) ze Brána Firewall služby Azure.
- [Přečtěte si](/azure/firewall/fqdn-tags) o značkách plně kvalifikovaného názvu domény.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Osvědčený postup: Nasazení Firewallu webových aplikací (WAF)

Webové aplikace se čím dál častěji stávají cílem škodlivých útoků, které zneužívají běžně známé chyby zabezpečení. Zneužití patří útoky prostřednictvím injektáže SQL a útoky skriptování napříč weby. Předcházet takovým útokům v kódu aplikace může být náročné a může vyžadovat pečlivou údržbu, opravy a monitorování několika vrstev topologie aplikace. Centralizovaný firewall webových aplikací pomáhá dělat mnohem jednodušší správu zabezpečení a pomáhá správcům aplikace pomáhalo chránit před hrozbami neoprávněného vniknutí. Firewall webových aplikací může reagovat na ohrožení zabezpečení, rychlejší, protože opravuje známé chyby zabezpečení v centrálním umístění, namísto zabezpečování jednotlivých webových aplikací. Stávající aplikační brány je možné jednoduše převést na aplikační brány doplněné webovým aplikačním firewallem.

Firewall webových aplikací (WAF) je funkce služby Azure Application Gateway.

- WAF poskytuje centralizovanou ochranu webových aplikací před běžným zneužitím a ohrožením zabezpečení.
- WAF chrání bez úprav back-endového kódu.
- Může chránit více webových aplikací současně za službou Application Gateway.
- WAF je integrovaný se službou Azure Security Center.
- Můžete přizpůsobit pravidla firewallu webových aplikací a skupin pravidel tak, aby vyhovoval vašim požadavkům aplikace.
- Jako osvědčený postup byste měli použít WAF v popředí u žádné aplikace s přístupem k web, včetně aplikací na virtuálních počítačích Azure nebo služby Azure App Service.

**Víc se uč:**

- [Další informace o](/azure/application-gateway/waf-overview) WAF.
- [Podívejte se](/azure/application-gateway/application-gateway-waf-configuration) na omezení a vyloučení WAF.

## <a name="best-practice-implement-azure-network-watcher"></a>Osvědčený postup: Implementace Azure Network Watcheru

Azure Network Watcher poskytuje nástroje pro monitorování prostředků a komunikací ve virtuální síti Azure. Můžete například monitorovat komunikace mezi virtuálním Počítačem a koncový bod jako jiný virtuální počítač nebo plně kvalifikovaný název domény, zobrazení zdroje a vztahy prostředků ve virtuální síti, nebo diagnostikovat problémy se sítí provoz.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Pomocí služby Network Watcher můžete monitorovat a diagnostikovat problémy se sítí bez nutnosti přihlášení do virtuálních počítačů.
- Můžete nastavením upozornění můžete aktivovat zachytávání paketů a získat přístup k informacím o výkonu v reálném čase na úrovni paketů. Když narazíte na problém, můžete ho prozkoumat podrobněji.
- Osvědčeným postupem je použít Network Watcher ke kontrole protokolů toku NSG.
  - Protokoly toku NSG v Network Watcheru umožňují zobrazit informace o příchozím a odchozím provozu IP přes NSG.
  - Protokoly toku se zapisují ve formátu JSON.
  - Protokoly toku zobrazují odchozí a příchozí toky pro jednotlivá pravidla, síťové rozhraní (NIC), na které se tok vztahuje, pětici informací o toku (zdrojová/cílová IP adresa, zdrojový/cílový port a protokol) a informace o tom, jestli byl provoz povolený nebo odepřený.

**Víc se uč:**

- [Získejte přehled](/azure/network-watcher) služby Network Watcher.
- [Další informace](/azure/network-watcher/network-watcher-nsg-flow-logging-overview) protokoly toků NSG.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Použití nástrojů partnerů na webu Azure Marketplace

Pro složitější topologií sítě můžete použít produkty zabezpečení od partnerů Microsoftu, v konkrétní síťová virtuální zařízení (Nva).

- Síťové virtuální zařízení je virtuální počítač, který provádí síťovou funkci, jako je například Brána firewall, optimalizace sítě WAN nebo jiná síťová funkce.
- Síťová virtuální zařízení posilují zabezpečení a síťové funkce virtuální sítě. Můžou být nasazená pro vysoce dostupné brány firewall, prevenci vniknutí, detekci vniknutí, Firewall webových aplikací (WAF), optimalizaci sítě WAN, směrování, vyrovnávání zatížení, VPN, správu certifikátů, Active Directory a vícefaktorové ověřování.
- Síťová virtuální zařízení jsou k dispozici od mnoha dodavatelů v  [Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Osvědčený postup: Implementace bran firewall a síťových virtuálních zařízení v sítích s centrem

V centru se hraniční síť (s přístupem k internetu) obvykle spravuje přes bránu firewall Azure, farmu bran firewall nebo Firewall webových aplikací (WAF). Podívejte se na následující porovnání.

<!--markdownlint-disable MD033 -->

**Typ brány firewall** | **Podrobnosti**
--- | ---
WAF | Webové aplikace jsou běžné a často bývají postižené ohroženími zabezpečení a potenciálními zneužitími.<br/><br/> WAF jsou navržené k detekci útoků proti webovým aplikacím (HTTP/HTTPS), a to konkrétněji než obecné brány firewall.<br/><br/> V porovnání s tradiční technologií brány firewall mají WAF sadu specifických funkcí, které chrání interní webové servery před hrozbami.
Brána Azure Firewall | Podobně jako farmy bran firewall síťových virtuálních zařízení používá Azure Firewall mechanismus společné správy a sadu pravidel zabezpečení k ochraně úloh hostovaných v paprskových sítích a k řízení přístupu k místním sítím.<br/><br/> Azure Firewall má integrovanou škálovatelnost.
Brány firewall síťových virtuálních zařízení | Například síťové virtuální zařízení brány Firewall Azure farmy brány firewall mají společného mechanismu správy a sadu pravidel zabezpečení k ochraně úloh hostovaných v sítích paprsků a pro řízení přístupu k místním sítím.<br/><br/> Síťové virtuální zařízení brány firewall můžete ručně škálovat za nástrojem pro vyrovnávání zatížení.<br/><br/> Když síťové virtuální zařízení brány firewall má menší speciální software než brány WAF, má širší rozsah aplikace můžete filtrovat a kontrolovat libovolného typu v příchozího a odchozího provozu.<br/><br/> Pokud chcete používat síťové virtuální zařízení, najdete je na webu Azure Marketplace.

<!--markdownlint-enable MD033 -->

Doporučujeme používat jednu sadu Azure brány firewall (nebo síťová virtuální zařízení) pro přenosy z Internetu, a jinou pro přenosy pocházející místní.

- Použití jenom jedné sady brány firewall pro obě představuje bezpečnostní riziko, protože nabízí neexistuje žádná bezpečnostní hranice mezi těmito dvěma sadami síťových přenosů.
- Pomocí vrstev samostatnou bránu firewall snižuje složitost pravidel pro kontrolu zabezpečení a je jasné, která pravidla platí pro které příchozí žádosti v síti.

**Víc se uč:**

- [Další informace o](/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) pomocí síťových virtuálních zařízení ve virtuální síti Azure.

## <a name="next-steps"></a>Další postup

Přečtěte si doporučené postupy:

- [Osvědčené postupy](migrate-best-practices-security-management.md) pro zabezpečení a správu po migraci.
- [Osvědčené postupy](migrate-best-practices-costs.md) cost Management po migraci.
