---
title: Kontrola možností sítě
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak identifikovat možnosti sítě, které vaše cílová zóna potřebuje k podpoře úloh Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 71c3a135a89d3ff09cf8511ca619c47db21e1ac9
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093150"
---
<!-- cSpell:ignore paas NVAs VPNs -->

# <a name="review-your-network-options"></a>Kontrola možností sítě

Návrh a implementace síťových funkcí Azure představuje důležitou součást vašeho úsilí o přechod na cloud. Budete muset přijmout taková rozhodnutí o návrhu sítě, aby správně podporovala úlohy a služby, které budou hostovány v cloudu. Síťové produkty a služby Azure podporují širokou škálu síťových funkcí. To, jak strukturujete tyto služby a zvolené síťové architektury, závisí na požadavcích vaší organizace na úlohy, zásady správného řízení a připojení.

## <a name="identify-workload-networking-requirements"></a>Identifikace požadavků na síťové úlohy

V rámci vyhodnocení a přípravy cílového prostředí musíte identifikovat všechny síťové funkce, která bude vaše cílové prostředí muset podporovat. Součástí tohoto procesu je posouzení všech aplikací a služeb, ze kterých jsou tvořeny vaše úlohy, a určení požadavků na řízení síťového připojení. Po zjištění a zdokumentování těchto požadavků můžete pro cílové prostředí vytvořit zásady, které na základě potřeb vašich úloh určují, jaké síťové prostředky a konfigurace jsou povolené.

Pro každou aplikaci nebo službu, kterou nasadíte do cílového prostředí, použijte jako výchozí bod následující rozhodovací strom, který vám pomůže určit síťové nástroje a služby, které byste měli použít:

![Rozhodovací strom síťových služeb Azure](../../_images/ready/network-decision-tree.png)

### <a name="key-questions"></a>Klíčové otázky

Zodpovězení následujících otázek týkajících se vašich úloh vám pomůže při rozhodování na základě rozhodovacího stromu síťových služeb Azure:

- **Budou vaše úlohy vyžadovat virtuální síť?** Typy prostředků spravované platformy jako služby (PaaS) používají základní síťové funkce platformy, u kterých není nutné vždy používat virtuální síť. Pokud vaše úlohy nevyžadují pokročilé síťové funkce a nepotřebujete nasazovat prostředky infrastruktury jako služby (IaaS), můžou výchozí [nativní síťové funkce poskytované prostředky PaaS](../../decision-guides/software-defined-network/paas-only.md) vyhovovat vašim nárokům na možnosti připojení úloh a správu provozu.
- **Budou vaše úlohy vyžadovat připojení mezi virtuálními sítěmi a vaším místním datovým centrem?** Azure poskytuje dvě řešení pro vytváření hybridních síťových možností: Azure VPN Gateway a Azure ExpressRoute. [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) připojuje vaše místní sítě k Azure prostřednictvím sítě site-to-site VPN, podobně jako když vytvoříte a použijete připojení ke vzdálené pobočce. VPN Gateway má maximální šířku pásma 1,25 GB/s. [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) nabízí vyšší spolehlivost a nižší latenci díky privátnímu připojení mezi Azure a vaší místní infrastrukturou. Šířka pásma pro ExpressRoute se pohybuje v rozsahu od 50 MB/s do 100 GB/s.
- **Budete muset kontrolovat a auditovat odchozí provoz pomocí místních síťových zařízení?** U nativních cloudových úloh můžete ke kontrole a auditování provozu směřujícího do nebo přicházejícího z veřejného internetu použít [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview) nebo [síťová virtuální zařízení (NVA)](https://azure.microsoft.com/solutions/network-appliances) třetích stran hostovaná v cloudu. Mnoho podnikových zásad zabezpečení IT však vyžaduje, aby odchozí provoz směřující na internet procházel centrálně spravovanými zařízeními v místním prostředí organizace. Tyto scénáře podporuje [vynucené tunelové připojení](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview). Některé spravované služby však toto řešení nepodporují. Služby a funkce jako [App Service Environment v Azure App Service](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-key-concepts), [Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/intro-kubernetes), [spravované instance v Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index), [Azure Databricks](https://docs.microsoft.com/azure/azure-databricks/what-is-azure-databricks) a [Azure HDInsight](https://docs.microsoft.com/azure/hdinsight) tuto konfiguraci podporují, pokud je služba nebo funkce nasazena ve virtuální síti.
- **Budete muset připojovat více virtuálních sítí?** K připojení více instancí [virtuálních sítí Azure](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) můžete použít [peering virtuálních sítí](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Peering může podporovat připojení mezi předplatnými a oblastmi. V případě scénářů, kde poskytujete služby, které jsou sdíleny ve více předplatných, nebo potřebujete spravovat velký počet peeringů sítí, zvažte použití [hvězdicové síťové architektury](../../decision-guides/software-defined-network/hub-spoke.md) nebo služby [Azure Virtual WAN ](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about). Peering virtuálních sítí poskytuje konektivitu jenom mezi dvěma partnerskými sítěmi. Ve výchozím nastavení neposkytuje přenositelnou konektivitu mezi několika peeringy.
- **Budou vaše úlohy přístupné přes internet?** Azure poskytuje služby, které jsou navržené tak, aby vám pomohly spravovat a zabezpečit externí přístup k vašim aplikacím a službám:
  - [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview)
  - [Síťová zařízení](https://azure.microsoft.com/solutions/network-appliances)
  - [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
  - [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway)
  - [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)
- **Budete muset podporovat vlastní správu DNS?** [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) je hostitelská služba pro domény DNS. Azure DNS poskytuje překlad názvů pomocí infrastruktury Azure. Pokud vaše úlohy vyžadují překlad názvů, který přesahuje funkce poskytované Azure DNS, možná budete muset nasadit další řešení. Pokud vaše úlohy vyžadují i službu Active Directory, zvažte použití [Azure Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/overview) k rozšíření možností Azure DNS. Pokud vyžadujete další funkce, můžete také [nasadit vlastní virtuální počítače IaaS](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances), které podporují vaše požadavky.

## <a name="common-networking-scenarios"></a>Běžné scénáře sítě

Síť Azure se skládá z několika produktů a služeb, které poskytují různé síťové funkce. V rámci návrhu sítě můžete porovnat své požadavky na úlohy se scénáři práce v síti v následující tabulce a identifikovat nástroje nebo služby Azure, které můžete použít k poskytování požadovaných síťových funkcí:

<!-- markdownlint-disable MD033 -->

| **Scénář** | **Síťový produkt nebo služba** |
| --- | --- |
| Potřebuji síťovou infrastrukturu pokrývající všechny potřeby připojení, od virtuálních počítačů až po příchozí připojení k síti VPN. | [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network) |
| Potřebuji vyrovnávat příchozí a odchozí připojení a požadavky na mé aplikace nebo služby. | [Nástroj pro vyrovnávání zatížení Azure](https://docs.microsoft.com/azure/load-balancer) |
| Potřebuji optimalizovat doručování ze serverových farem aplikací při současném zvýšení zabezpečení aplikací pomocí firewallu webových aplikací. | [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway) <br/>[Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |
| Potřebuji bezpečně přes internet přistupovat k virtuálním sítím Azure prostřednictvím vysoce výkonných bran VPN. | [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway) |
| Vyžaduji ultrarychlé odezvy DNS a ultravysokou dostupnost pro všechny mé doménové potřeby. | [Azure DNS](https://docs.microsoft.com/azure/dns) |
| Potřebuji zrychlit doručování širokopásmového obsahu zákazníkům po celém světě – od aplikací a uloženého obsahu po streamování videa. | [Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn) |
| Potřebuji chránit mé aplikace Azure před útoky DDoS. | [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) |
| Potřebuji optimálně distribuovat provoz do služeb napříč globálními oblastmi Azure při zajištění vysoké dostupnosti a rychlosti odezvy. | [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)<br/>[Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |
| Potřebuji přidat možnost připojení privátní sítě pro zajištění přístupu ke cloudovým službám Microsoftu z mých podnikových sítí, jako kdyby byly místní a nacházely se v mém vlastním datacentru. | [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute) |
| Chci monitorovat a diagnostikovat podmínky na úrovni síťového scénáře. | [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher) |
| Potřebuji nativní možnosti brány firewall s integrovanou vysokou dostupností, neomezenou škálovatelností cloudu a nulovou údržbou. | [Azure Firewall](https://docs.microsoft.com/azure/firewall) |
| Potřebuji bezpečně propojit obchodní kanceláře, maloobchodní prodejny a weby. | [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan) |
| Potřebuji škálovatelný bod s rozšířeným zabezpečením pro globální doručování webových aplikací založených na mikroslužbách. | [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |

<!-- markdownlint-enable MD033 -->

## <a name="choose-a-networking-architecture"></a>Volba síťové architektury

Poté, co identifikujete síťové služby Azure, které potřebujete pro podporu vašich úloh, musíte taky navrhnout architekturu, která tyto služby spojí, aby poskytovala cloudovou síťovou infrastrukturu pro vaše cílové prostředí. Podrobnosti o některých nejběžnějších vzorech síťové architektury používaných v Azure najdete v [Průvodci rozhodováním ohledně softwarově definovaných sítí](../../decision-guides/software-defined-network/index.md) pro architekturu přechodu na cloud.

V následující tabulce najdete přehled hlavních scénářů, které tyto vzory podporují:

| **Scénář**                                                                                                                                                                                                                                                                                                                        | **Doporučená síťová architektura**                                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Všechny úlohy hostované v Azure nasazené do vaší cílové zóny budou zcela PaaS, nevyžadují virtuální síť a nejsou součástí širšího úsilí o přijetí cloudu, které zahrnuje prostředky IaaS.                                                                                                                        | [Jenom PaaS](../../decision-guides/software-defined-network/paas-only.md)            |
| Vaše úlohy hostované v Azure nasadí prostředky založené na IaaS, jako jsou virtuální počítače, nebo jinak vyžadují virtuální síť, ale nevyžadují připojení k vašemu místnímu prostředí.                                                                                                                                          | [Model nativní pro cloud](../../decision-guides/software-defined-network/cloud-native.md)      |
| Vaše úlohy hostované v Azure vyžadují omezený přístup k místním prostředkům, cloudová připojení je ale nutné považovat za nedůvěryhodná.                                                                                                                                                                                           | [DMZ v cloudu](../../decision-guides/software-defined-network/cloud-dmz.md)            |
| Vaše úlohy hostované v Azure vyžadují omezený přístup k místním prostředkům a máte v úmyslu implementovat vyspělé zásady zabezpečení a zabezpečené propojení mezi cloudem a místním prostředím.                                                                                                                         | [Hybridní model](../../decision-guides/software-defined-network/hybrid.md)                  |
| Potřebujete nasadit a spravovat velký počet virtuálních počítačů a úloh, potenciálně překračující [omezení předplatného Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits), potřebujete sdílet služby napříč předplatnými nebo potřebujete více segmentovanou strukturu pro oddělení rolí, aplikací nebo oprávnění. | [Hvězdicová architektura](../../decision-guides/software-defined-network/hub-spoke.md)        |
| Máte mnoho poboček, které je třeba propojit navzájem a s Azure.                                                                                                                                                                                                                                                       | [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) |

### <a name="azure-virtual-datacenter"></a>Virtuální datové centrum Azure

Pokud vaše podniková IT skupina spravuje velká cloudová prostředí, pak kromě použití jednoho z těchto vzorů architektury zvažte při navrhování cloudové infrastruktury založené na Azure také použití [virtuálního datového centra Azure](../../reference/vdc.md). Virtuální datové centrum Azure poskytuje kombinovaný přístup k vytváření sítí, zabezpečení, správě a infrastruktuře, pokud vaše organizace splňuje následující kritéria:

- Váš podnik musí splňovat požadavky dodržování legislativních předpisů, které vyžadují centralizované monitorování a audit.
- Vaše cloudová aktiva se budou skládat z více než 10 000 virtuálních počítačů IaaS nebo ekvivalentního objemu služeb PaaS.
- V rámci podpory vývojářských a provozních týmů potřebujete zajistit možnosti agilního nasazení úloh a současně zajistit dodržování společných zásad, předpisů a centrální kontroly IT nad základními službami.
- Váš obor závisí na komplexní platformě, která vyžaduje hluboké znalosti domén (například finančnictví, petrochemický průmysl nebo výroba).
- Vaše stávající zásady správného řízení IT vyžadují přesnější shodu s existujícími funkcemi, a to i v rané fázi přechodu na cloud.

## <a name="follow-azure-networking-best-practices"></a>Dodržování osvědčených postupů pro sítě Azure

V rámci procesu návrhu sítě si prostudujte tyto články:

- [Plánování virtuálních sítí.](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Naučte se plánovat virtuální sítě na základě vašich požadavků na umístění, izolaci a připojení.
- [Osvědčené postupy Azure pro zabezpečení sítě](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Seznamte se s osvědčenými postupy Azure, které vám pomůžou zlepšit zabezpečení sítě.
- [Osvědčené postupy pro sítě při migraci úloh do Azure](https://docs.microsoft.com/azure/migrate/migrate-best-practices-networking?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Získejte další informace, jak implementovat sítě Azure pro podporu úloh založených na IaaS a PaaS.
