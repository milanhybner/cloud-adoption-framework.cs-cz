---
title: 'Virtuální datacentra: Perspektiva sítě'
description: Naučte se vytvářet virtuální datacentrum v Azure.
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: e5729e592fe0e602d24e2e37831c782fada73128
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566686"
---
# <a name="virtual-datacenters-a-network-perspective"></a>Virtuální datacentra: Perspektiva sítě

## <a name="overview"></a>Přehled

Migrace místních aplikací do Azure poskytuje organizacím výhody zabezpečené a nákladově efektivní infrastruktury, a to i v případě, že se aplikace migrují s minimálními změnami. Aby se ale zajistila možnost větší flexibility s využitím cloud computingu, podniky musí vyvíjet své architektury, aby mohli využívat možnosti Azure.

Microsoft Azure přináší služby a infrastrukturu škálovatelných a spolehlivých funkcí na podnikové úrovni. Tyto služby a infrastruktura nabízejí řadu možností hybridního připojení, aby se zákazníci mohli rozhodnout k nim přistupovat přes veřejný Internet nebo přes privátní připojení Azure ExpressRoute. Partneři Microsoftu také poskytují vylepšené funkce, které nabízejí služby zabezpečení a virtuální zařízení optimalizovaná pro spouštění v Azure.

Zákazníci si můžou zvolit přístup k těmto cloudovým službám prostřednictvím Internetu nebo pomocí Azure ExpressRoute, která poskytuje připojení k privátní síti. S Microsoft Azure platformou můžou zákazníci bezproblémově roztáhnout svoji infrastrukturu do cloudu a vytvářet vícevrstvé architektury. Partneři Microsoftu také poskytují vylepšené funkce, které nabízejí služby zabezpečení a virtuální zařízení optimalizovaná pro spouštění v Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-virtual-datacenter"></a>Co je virtuální datové centrum?

Ve svém okamžiku vzniká cloudová platforma, která je v podstatě platformou pro hostování veřejných aplikací. Podniky začaly pochopit hodnotu cloudu a začali přesunout interní obchodní aplikace do cloudu. Tyto typy aplikací dostanou dodatečné zabezpečení, spolehlivost, výkon a náklady, které vyžadují větší flexibilitu v případě doručování cloudových služeb. To paved způsob, jak nové infrastruktury a síťové služby navržené pro zajištění této flexibility, ale také nové funkce pro škálování, zotavení po havárii a další okolnosti.

Cloudová řešení byla nejprve navržena tak, aby se ve veřejném spektru hostly jedna poměrně izolovaná aplikace. Tento přístup se dobře pracoval v několika letech. Pak se tyto výhody cloudových řešení objevily a v cloudu byly hostovány víc úloh na velkém rozsahu. Řešení potíží se zabezpečením, spolehlivostí, výkonem a náklady na nasazení v jedné nebo několika oblastech se v celém životním cyklu cloudové služby stalo zásadním.

Následující diagram nasazení v cloudu ukazuje příklad bezpečnostní mezery zvýrazněný červeně. Žluté pole zobrazuje místo pro optimalizaci síťových virtuálních zařízení napříč úlohami.

![0][0]

Virtuální datacentrum představuje nutnost škálování pro podporu podnikových úloh a zároveň vyrovnává nutnost řešit problémy, které se zavedly při podpoře rozsáhlých aplikací ve veřejném cloudu.

Implementace virtuálního datového centra nereprezentuje jenom úlohy aplikací v cloudu, ale také síť, zabezpečení, správu a infrastrukturu (například DNS a adresářové služby). Vzhledem k tomu, že se více a více úloh podniku přesouvá do Azure, je důležité se zamyslet nad podpůrnou infrastrukturou a objekty, které tyto úlohy jsou umístěné v. Pečlivě se zamyslete nad tím, jak jsou prostředky strukturované, a nemusíte přitom nakládat na stovkách úloh, které se musí spravovat odděleně pomocí nezávislého toku dat, modelů zabezpečení a problémů s dodržováním předpisů.

Koncept služby Virtual datacentra je sada doporučení a osvědčených postupů pro implementaci kolekce samostatných, ale souvisejících entit se společnými podpůrnými funkcemi, funkcemi a infrastrukturou. Zobrazením úloh pomocí objektivu v rámci virtuálního datového centra můžete snížit náklady z důvodu úspory rozsahu, optimalizovaného zabezpečení prostřednictvím součásti a centralizovaného toku dat, a to spolu s jednoduššími operacemi, správou a auditem dodržování předpisů.

> [!NOTE]
> Je důležité si uvědomit, že virtuální datacentrum není **diskrétní** produktem Azure, ale kombinaci různých funkcí a možností, které splňují vaše přesné požadavky. Virtuální datacentrum představuje způsob, jak se zamyslet na vaše úlohy a využití Azure a maximalizovat vaše prostředky a schopnosti v cloudu. Jedná se o modulární přístup k vytváření IT služeb v Azure, a to s ohledem na organizační role a zodpovědnost podniku.

Implementace virtuálního datového centra může organizacím získat úlohy a aplikace do Azure v následujících situacích:

- Hostování více souvisejících úloh
- Migrujte úlohy z místního prostředí do Azure.
- Implementujte sdílené nebo centralizované požadavky na zabezpečení a přístup napříč úlohami.
- Promíchejte Azure DevOps a proveďte jejich centralizaci pro velký podnik.

Klíčem k odemknutí výhod virtuálního datacentra je centralizované hvězdicové síťové topologie s kombinací služeb a funkcí Azure:

- [Virtual Network Azure][VNet],
- [Skupiny zabezpečení sítě][network-security-groups],
- [Partnerský vztah virtuální sítě][VNetPeering],
- [Trasy definované uživatelem][user-defined-routes]a
- Identita Azure s [řízením přístupu na základě role (RBAC)][RBAC] a volitelně [Azure firewall][AzFW], [Azure DNS][DNS], [přední dveře Azure][AFD]a [Azure Virtual WAN][vWAN].

## <a name="who-should-implement-a-virtual-datacenter"></a>Kdo má implementovat virtuální datové centrum?

Každý zákazník Azure, který se rozhodl přijmout Cloud, může těžit z efektivity konfigurace sady prostředků pro běžné používání všemi aplikacemi. V závislosti na velikosti můžou i jednotlivé aplikace těžit z používání vzorů a komponent, které slouží k vytvoření implementace virtuálního datacentra.

Pokud má vaše organizace centralizované týmy nebo oddělení pro IT, sítě, zabezpečení nebo dodržování předpisů, implementace virtuálního datového centra může pomáhat vyhovět bodům zásad, oddělení povinnosti a zajišťovat jednotnost základních společných součástí a zároveň jim poskytovat týmy aplikací, které jsou vhodné pro vaše požadavky, jsou mnohem volná a ovládají.

Organizace, které hledají DevOps, mohou také využít koncepty virtuálních Datacenter k poskytování autorizovaných kapes prostředků Azure a zajistit, aby měli v rámci této skupiny celkovou kontrolu (buď předplatné, nebo skupina prostředků ve společném předplatném), ale hranice sítě a zabezpečení zůstávají v souladu s definicemi centralizovaných zásad ve virtuální síti centra a skupině prostředků.

<!-- markdownlint-enable MD026 -->

## <a name="considerations-for-implementing-a-virtual-datacenter"></a>Předpoklady pro implementaci virtuálního datového centra

Při návrhu implementace virtuálního datového centra je potřeba vzít v úvahu několik pivotových problémů:

### <a name="identity-and-directory-service"></a>Identita a adresářová služba

Služba identity a adresářové služby jsou klíčovým aspektem všech Datacenter v místním i cloudovém prostředí. Identita souvisí se všemi aspekty přístupu a autorizací ke službám v rámci implementace virtuálního datacentra. Pro zajištění toho, aby přístup k vašemu účtu a prostředkům Azure používali jenom autorizovaní uživatelé a procesy, používá Azure pro ověřování několik typů přihlašovacích údajů. Mezi ně patří hesla (pro přístup k účtu Azure), kryptografické klíče, digitální podpisy a certifikáty. [Azure Multi-Factor Authentication][multi-factor-authentication] je další úroveň zabezpečení pro přístup ke službám Azure. Multi-Factor Authentication poskytuje silné ověřování s využitím široké škály možností jednoduchého ověřování (telefonní hovor, textová zpráva nebo oznámení v mobilní aplikaci) a umožňuje zákazníkům zvolit si metodu, které dáváte přednost.

Každý velký podnik potřebuje definovat proces správy identit, který popisuje správu individuálních identit, jejich ověřování, autorizaci, rolí a oprávnění v rámci implementace virtuálního datacentra nebo napříč nimi. Cílem tohoto procesu je zvýšit zabezpečení a produktivitu při současném snížení nákladů, výpadků a opakujících se ručních úloh.

Organizace Enterprise mohou vyžadovat náročné kombinace služeb pro různé obchodní oddělení a zaměstnanci mají často různé role, pokud se účastní různých projektů. Virtuální datacentrum vyžaduje dobrou spolupráci mezi různými týmy, z nichž každá má konkrétní definice rolí, aby bylo možné spouštět systémy s dobrým dodržováním zásad správného řízení. Matice odpovědností, přístupu a práv může být složitá. Správa identit ve virtuálním datacentru je implementovaná prostřednictvím služby [Azure Active Directory (Azure AD)][azure-ad] a řízení přístupu na základě role (RBAC).

Adresářová služba je sdílená informační infrastruktura, která vyhledává, spravuje, spravuje a uspořádává každodenní položky a síťové prostředky. Tyto prostředky můžou zahrnovat svazky, složky, soubory, tiskárny, uživatele, skupiny, zařízení a další objekty. Každý prostředek v síti je považován za objekt na adresářovém serveru. Informace o prostředku jsou uloženy jako kolekce atributů přidružených k danému prostředku nebo objektu.

Všechny online obchodní služby Microsoftu využívají Azure Active Directory (Azure AD) k přihlašování a jiným potřebám identity. Azure Active Directory je komplexní, vysoce dostupné cloudové řešení pro správu identit a přístupu, které představuje kombinaci základních adresářových služeb, rozšířené správy identit a správy přístupu k aplikacím. Azure AD můžete integrovat s místní službou Active Directory a povolit tak jednotné přihlašování pro všechny cloudové a místně hostované místní aplikace. Uživatelské atributy místní služby Active Directory je možné automaticky synchronizovat do Azure AD.

Jeden globální správce není nutný k přiřazení všech oprávnění v implementaci virtuálního datacentra. Místo toho můžou mít každé konkrétní oddělení, skupinu uživatelů nebo služby v adresářové službě oprávnění potřebná ke správě vlastních prostředků v rámci implementace virtuálního datacentra. Oprávnění strukturování vyžadují vyrovnávání. Příliš mnoho oprávnění může mít vliv na efektivitu výkonu a příliš málo nebo volná oprávnění může zvýšit bezpečnostní riziko. Řízení přístupu na základě role (RBAC) Azure pomáhá vyřešit tento problém tím, že nabízí jemně odstupňovanou správu přístupu k prostředkům v implementaci virtuálního datacentra.

#### <a name="security-infrastructure"></a>Infrastruktura zabezpečení

Infrastruktura zabezpečení odkazuje na oddělení přenosů v konkrétním segmentu virtuální sítě implementace virtuálního datového centra. Tato infrastruktura určuje, jakým způsobem se v implementaci virtuálního datového centra řídí příchozí a odchozí výstup. Azure je založený na víceklientské architektuře, která zabraňuje neoprávněnému a neúmyslnému provozu mezi nasazeními pomocí izolace virtuální sítě, seznamů řízení přístupu (ACL), nástrojů pro vyrovnávání zatížení, filtrů IP a zásad toku provozu. Překlad síťových adres (NAT) odděluje interní síťový provoz z externího provozu.

Prostředky infrastruktury Azure přidělují prostředky infrastruktury klientským úlohám a spravují komunikaci s virtuálními počítači a z nich. Hypervisor Azure vynutil oddělení paměti a procesů mezi virtuálními počítači a bezpečným směrováním síťového provozu do klientů hostovaného operačního systému.

#### <a name="connectivity-to-the-cloud"></a>Připojení ke cloudu

Implementace virtuálního datového centra vyžaduje připojení k externím sítím, aby nabízela služby zákazníkům, partnerům a interním uživatelům. K tomu je potřeba, aby připojení odkazovalo nejen na Internet, ale i na místní sítě a datová centra.

Zákazníci řídí, ke kterým službám mají přístup, a jsou přístupné z veřejného Internetu pomocí [Azure firewall][AzFW] nebo jiných typů zařízení virtuální sítě (síťová virtuální zařízení), vlastních zásad směrování pomocí [uživatelem definovaných tras][user-defined-routes]a sítě. filtrování pomocí [skupin zabezpečení sítě][network-security-groups]. Doporučujeme, aby všechny internetové prostředky byly také chráněny [Azure DDoS Protection standardem][DDoS].

Podniky můžou potřebovat připojit svou implementaci virtuálních Datacenter k místním datacentrům nebo jiným prostředkům. Toto připojení mezi Azure a místními sítěmi je zásadním aspektem při navrhování efektivní architektury. Podniky mají dva různé způsoby, jak toto propojení vytvořit: přenos přes Internet nebo prostřednictvím privátních přímých připojení.

[**Síť VPN typu Site-to-site**][VPN] je propojení prostřednictvím internetu mezi místními sítěmi a implementací virtuálního datového centra vytvořená prostřednictvím zabezpečených šifrovaných připojení (tunely IPSec/IKE). Připojení mezi lokalitami Azure je flexibilní, rychlé vytvoření a nevyžaduje žádné další zásobování, protože všechna připojení se připojují přes Internet.

V případě velkého počtu připojení k síti VPN je [**Azure Virtual WAN**][vWAN] síťová služba, která poskytuje optimalizované a automatizované připojení větví k síti prostřednictvím Azure. Virtual WAN umožňuje připojit se ke konfiguraci zařízení větví ke komunikaci s Azure. Připojení a konfigurace se dá provést ručně nebo pomocí zařízení preferovaného poskytovatele prostřednictvím virtuálního partnera WAN. Použití preferovaných zařízení poskytovatele umožňuje snadné použití, zjednodušení připojení a správu konfigurace. Vestavěný řídicí panel Azure WAN nabízí okamžité přehledy pro řešení potíží, které vám ušetří mnoho času, a snadnou cestu k zobrazení projení poboček ve velkém měřítku.

[**ExpressRoute**][ExR] je služba připojení Azure, která umožňuje privátní připojení mezi implementací virtuálního datového centra a všemi místními sítěmi. Připojení ExpressRoute nevyužívají veřejný Internet a nabízejí vyšší rychlost zabezpečení, spolehlivosti a vyšší rychlosti (až 10 GB/s) spolu s konzistentní latencí. ExpressRoute je užitečné pro implementace virtuálních Datacenter, protože zákazníci ExpressRoute můžou získat výhody pravidel dodržování předpisů přidružených k soukromým připojením. Pomocí [ExpressRoute Direct][ExRD]se můžete připojit přímo ke směrovačům microsoftu na 100 GB/s pro zákazníky s většími nároky na šířku pásma.

Nasazení připojení ExpressRoute obvykle zahrnuje angažování poskytovatel služeb ExpressRoute. Pro zákazníky, kteří potřebují začít rychle, je běžné používat síť VPN typu Site-to-site k navázání připojení mezi implementací virtuálního datového centra a místními prostředky a pak migrovat na ExpressRoute připojení, když máte fyzický propojení s vaším poskytovatelem služeb je dokončené.

#### <a name="connectivity-within-the-cloud"></a>*Konektivita v cloudu*

[Virtuální sítě][VNet] a [VNet peering][VNetPeering] jsou základní síťové služby síťového připojení uvnitř implementace virtuálního datacentra. Virtuální síť garantuje přirozený rámec izolace pro virtuální datacentra a partnerský vztah virtuálních sítí umožňuje vzájemnou komunikaci mezi různými virtuální sítěy ve stejné oblasti Azure nebo i v různých oblastech. Řízení provozu uvnitř virtuální sítě a mezi virtuální sítě musí odpovídat sadě pravidel zabezpečení zadaných prostřednictvím seznamů řízení přístupu ([skupin zabezpečení sítě][network-security-groups]), [síťových virtuálních zařízení][NVA]a vlastních směrovacích tabulek ([uživatelem definovaných tras][user-defined-routes]).

## <a name="virtual-datacenter-overview"></a>Přehled virtuálního datacentra

### <a name="topology"></a>Topologie

*Hub a paprsek* je model pro návrh síťové topologie pro implementaci virtuálního datového centra.

![1][1]

Jak je znázorněno, v Azure se dá použít dva typy centrálního a paprskového návrhu. Pro komunikaci, sdílené prostředky a centralizované zásady zabezpečení (rozbočovač virtuální sítě v diagramu) nebo typ virtuální sítě WAN (virtuální síť WAN v diagramu) pro komunikaci mezi větvemi a branami mezi sítěmi a Azure.

Rozbočovač je centrální zóna sítě, která řídí a kontroluje příchozí nebo odchozí provoz mezi různými zónami: Internet, místní a paprsky. Topologie centra a paprsků poskytuje oddělení IT účinný způsob, jak vynutilit zásady zabezpečení v centrálním umístění. Také snižuje riziko neoprávněné konfigurace a vystavení hrozbám.

Centrum často obsahuje společné komponenty služeb spotřebované paprsky. Mezi běžné centrální služby patří například:

- Infrastruktura služby Windows Active Directory, která se vyžaduje pro ověřování uživatelů třetích stran, kteří mají přístup k nedůvěryhodným sítím předtím, než získají přístup k úlohám v paprsku. Včetně související služby Active Directory Federation Services (AD FS).
- Služba DNS pro překlad názvů pro úlohy v paprscích, pro přístup k prostředkům v místní síti a na internetu, pokud se nepoužívá [Azure DNS][DNS].
- Infrastruktura veřejných klíčů (PKI) pro implementaci jednotného přihlašování k úlohám.
- Řízení toku provozu TCP a UDP mezi síťovými zónami v paprscích a internetem.
- Řízení toku mezi paprsky a místní sítí.
- V případě potřeby řízení toku mezi jednotlivými paprsky.

Virtuální datové centrum snižuje celkové náklady pomocí infrastruktury sdíleného centra mezi několika paprsky.

Role jednotlivých paprsků může být hostitelem různých typů úloh. Paprsky také poskytují modulární přístup pro opakovaná nasazení stejných úloh. Mezi příklady patří vývoj a testování, uživatelské akceptační testování, předprodukce a produkce. Paprsky můžou také oddělit a povolit různé skupiny v rámci vaší organizace. Příkladem jsou skupiny Azure DevOps. V rámci paprsku je možné nasadit základní úlohy nebo složité vícevrstvé úlohu s řízením provozu mezi vrstvami.

#### <a name="subscription-limits-and-multiple-hubs"></a>Omezení předplatného a více center

V Azure je každá součást bez ohledu na typ nasazená v předplatném Azure. Izolace komponent Azure v různých předplatných Azure může vyhovovat požadavkům různých objekty LOBs s, jako je například nastavení odlišných úrovní přístupu a autorizace.

Jedna implementace virtuálního datového centra se dá škálovat až na velký počet paprsků, ale stejně jako u každého systému IT jsou k dispozici omezení platformy. Nasazení centra je svázáno s konkrétním předplatným Azure, které má omezení a omezení (například maximální počet partnerských vztahů virtuálních sítí. Podrobnosti najdete v tématu [omezení a limity předplatného a služeb Azure, kvót a omezení][limits] ). V případech, kdy omezení můžou být problémem, se může architektura lépe škálovat tím, že se model rozšíří z jednoho centra na paprsky do clusteru hub a paprsků. Více rozbočovačů v jedné nebo více oblastech Azure je možné propojit pomocí sítě VPN peering, ExpressRoute, Virtual WAN nebo site-to-Site VPN.

![2][2]

Zavedení více rozbočovačů zvyšuje náklady a intenzitu řízení systému. Dá se odůvodnit pouze pomocí škálovatelnosti, omezení systému nebo redundance a regionální replikace pro výkon koncového uživatele nebo zotavení po havárii. V případě scénářů vyžadujících více rozbočovačů by všechna centra měla usilovat, aby nabízela stejnou sadu služeb pro provozní snadné zprovoznění.

#### <a name="interconnection-between-spokes"></a>Propojení mezi paprsky

V rámci jednoho paprsku je možné implementovat složité úlohy s více vrstvami. Konfigurace s více vrstvami se dají implementovat pomocí podsítí (jeden pro každou vrstvu) ve stejné virtuální síti a filtrovat toky pomocí skupin zabezpečení sítě.

Architekt může chtít nasadit vícevrstvé úlohy napříč několika virtuálními sítěmi. S partnerským vztahem virtuální sítě se paprsky můžou připojit k ostatním paprskům ve stejném nebo jiném rozbočovači. Typickým příkladem tohoto scénáře je případ, kdy se servery pro zpracování aplikací nacházejí v jednom paprsku nebo ve virtuální síti. Databáze je nasazena v jiném paprsku nebo ve virtuální síti. V tomto případě je snadné propojit paprsky s partnerským vztahem virtuální sítě a vyhnout se tak přenosu prostřednictvím centra. Měla by se provést pečlivou architekturu a kontrolu zabezpečení, aby se zajistilo, že při obnechání centra nebude obcházet důležité body zabezpečení nebo auditování, které můžou existovat jenom v centru.

![3][3]

Paprsky je taky možné propojit s paprskem, který funguje jako centrum. Tento přístup vytvoří hierarchii se dvěma úrovněmi: paprsek na vyšší úrovni (úroveň 0) se změní na centrum pro paprsky nižší úrovně (úroveň 1) v hierarchii. K přenosu provozu do centrálního centra se vyžadují paprsky implementace virtuálního datového centra, aby se přenosy mohly směrovat do svého cíle v místní síti nebo ve veřejném internetovém prostředí. Architektura se dvěma úrovněmi centrálního centra zavádí složité směrování, které odebírá výhody jednoduchého vztahu mezi rozbočovači a paprsky.

I když Azure umožňuje komplexní topologie, je jedním ze základních principů konceptu virtuálního datového centra opakovatelnost a jednoduchost. V zájmu minimalizace úsilí správy je jednoduchý návrh hvězdicové architektury pro virtuální datové centrum, který doporučujeme.

### <a name="components"></a>Komponenty

Virtuální datové centrum se skládá ze čtyř typů základních součástí: **infrastruktura**, **hraniční sítě**, **úlohy**a **monitorování**.

Každý typ součásti se skládá z nejrůznějších funkcí a prostředků Azure. Vaše implementace virtuálního datového centra se skládá z instancí více typů komponent a několika variací stejného typu komponenty. Například můžete mít mnoho různých logicky oddělených instancí úloh, které reprezentují různé aplikace. Pomocí těchto různých typů komponent a instancí nakonec vytvoříte virtuální datové centrum.

![4][4]

Předchozí koncepční architektura virtuálního datového centra vysoké úrovně zobrazuje různé typy komponent používané v různých zónách topologie hub-paprsků. Diagram zobrazuje komponenty infrastruktury v různých částech architektury.

Obecně platí, že přístupová práva a oprávnění by měly být v souladu s dobrým zvykem na základě skupin. Díky tomu, že se skupiny rozhodnou spíše než jednotliví uživatelé, usnadňují údržbu zásad přístupu tím, že poskytují konzistentní způsob jejich správy napříč týmy a pomáhá minimalizovat chyby konfigurace. Přiřazení a odebrání uživatelů do a z příslušných skupin pomáhá udržet oprávnění určitého uživatele v aktuálním stavu.

Každá skupina rolí by měla mít pro své názvy jedinečnou předponu. Tato předpona usnadňuje identifikaci, která skupina je přidružená k jakému zatížení. Například úlohy hostující službu ověřování mohou mít skupiny s názvem **AuthServiceNetOps**, **AuthServiceSecOps**, **AuthServiceDevOps**a **AuthServiceInfraOps**. Centralizované role nebo role, které nesouvisí s konkrétní službou, můžou být s **Corp**. Příkladem je **CorpNetOps**.

Mnoho organizací používá variaci následujících skupin, které poskytují hlavní rozpis rolí:

- Centrální skupina IT, **Corp,** má vlastnická práva k řízení komponent infrastruktury. Příklady jsou sítě a zabezpečení. Skupina musí mít roli přispěvatele v předplatném, řízení centra a oprávnění přispěvatele sítě v paprskech. Velké organizace často rozdělují tyto zodpovědnosti správy mezi více týmů. Příklady jsou síťové operace **CorpNetOps** skupiny se exkluzivním soustředěním na síť a **CorpSecOps** skupiny operací zabezpečení zodpovědné za bránu firewall a zásady zabezpečení. V tomto konkrétním případě je třeba vytvořit dvě různé skupiny pro přiřazení těchto vlastních rolí.
- Skupina pro vývoj a testování **AppDevOps** má zodpovědnost za nasazení aplikací nebo úloh služeb. Tato skupina vezme roli přispěvatele virtuálních počítačů pro nasazení IaaS nebo jednu nebo více rolí přispěvatele PaaS. Prohlédněte si [předdefinované role pro prostředky Azure][Roles]. V případě potřeby může tým pro vývoj/testování potřebovat přehled o zásadách zabezpečení (skupiny zabezpečení sítě) a zásadách směrování (uživatelem definované trasy) uvnitř centra nebo konkrétního paprsku. Kromě role přispěvatele pro úlohy bude tato skupina také potřebovat roli čtečky sítě.
- Operace a skupina údržby, **CorpInfraOps** nebo **AppInfraOps,** mají zodpovědnost za správu úloh v produkčním prostředí. Tato skupina musí být přispěvatelem předplatného pro úlohy v jakémkoli produkčním předplatném. Některé organizace můžou také zhodnotit, jestli potřebují další týmovou skupinu podpory eskalace s rolí přispěvatele předplatného v produkčním prostředí a předplatným centrálního centra. Další skupina opravuje možné problémy s konfigurací v produkčním prostředí.

Virtuální datové centrum je navržené tak, aby se skupiny vytvořené pro centrální skupinu IT, která spravuje centrum, měly odpovídající skupiny na úrovni pracovního vytížení. Kromě správy jenom prostředků rozbočovače je centrální skupinou IT možné řídit pro předplatné externí přístup a oprávnění na nejvyšší úrovni. Skupiny úloh také umožňují řídit prostředky a oprávnění pro jejich virtuální síť nezávisle na centrálním IT.

Virtuální datové centrum je rozdělené na oddíly, aby bylo možné bezpečně hostovat více projektů v různých řádcích společnosti. Všechny projekty vyžadují různá izolovaná prostředí (vývoj, UAT, produkce). Oddělení předplatných Azure pro každé z těchto prostředí zajišťuje fyzickou izolaci.

![5][5]

Předchozí diagram znázorňuje vztah mezi projekty organizace, uživateli a skupinami a prostředími, ve kterých jsou nasazené komponenty Azure.

Obvykle je prostředí (nebo vrstva) systémem, ve kterém je nasazeno a spuštěno více aplikací. Velké podniky využívají vývojové prostředí (kde se provádějí změny a testují) a produkční prostředí (které používají koncoví uživatelé). Tato prostředí jsou oddělená, často s několika přípravnými prostředími mezi nimi, aby umožnila postupné nasazení (zavedení), testování a vrácení zpět, pokud dojde k problémům. Architektury nasazení se výrazně liší, ale obvykle se jedná o základní proces od vývoje (DEV) a končí v produkčním prostředí (kat).

Společná architektura pro tyto typy prostředí s více vrstvami se skládá z Azure DevOps pro vývoj a testování, UAT pro přípravu a produkční prostředí. Organizace můžou k definování přístupu a práv k těmto prostředím využít jeden nebo víc tenantů Azure AD. Předchozí diagram znázorňuje případ, kdy se používají dva různé klienty Azure AD: jeden pro Azure DevOps a UAT a druhý výhradně pro produkční prostředí.

Existence různých tenantů Azure AD vynutila oddělení mezi prostředími. Stejnou skupinu uživatelů, jako je centrální IT, se musí ověřit pomocí jiného identifikátoru URI pro přístup k jinému klientovi Azure AD, aby se změnily role nebo oprávnění k Azure DevOps nebo produkčním prostředím projektu. Existence různých ověření uživatelů pro přístup k různým prostředím zkracuje možné výpadky a další problémy způsobené lidskými chybami.

#### <a name="component-type-infrastructure"></a>Typ součásti: infrastruktura

Tento typ součásti je místo, kde se nachází většina podpůrné infrastruktury. Je to také tam, kde centralizované týmy IT, zabezpečení a dodržování předpisů tráví většinu času.

![6][6]

Komponenty infrastruktury poskytují propojení pro různé součásti implementace virtuálního datového centra a jsou k dispozici v centru i paprskech. Zodpovědnost za správu a údržbu komponent infrastruktury se obvykle přiřazuje centrálnímu týmu IT nebo Security.

Jednou z primárních úloh týmu IT infrastruktury je zaručit konzistenci schémat IP adres napříč podnikem. Privátní adresní prostor IP adres přiřazený k implementaci virtuálního datového centra musí být konzistentní a nesmí se překrývat s privátními IP adresami přiřazenými v místních sítích.

I když překlad adres (NAT) na místních hraničních směrovačích nebo v prostředích Azure se může vyhnout konfliktům IP adres, přidá komplikace k vašim komponentám infrastruktury. Jednoduchost správy je jedním z klíčových cílů virtuálního datového centra, takže použití překladu adres (NAT) ke zpracování otázek IP není doporučeným řešením.

Komponenty infrastruktury mají následující funkce:

- [**Identity a adresářové služby**][azure-ad]. Přístup ke všem typům prostředků v Azure se řídí identitou uloženou v adresářové službě. Adresářová služba ukládá nejen seznam uživatelů, ale také přístupová práva k prostředkům v konkrétním předplatném Azure. Tyto služby můžou existovat jenom pro Cloud, nebo se můžou synchronizovat s místní identitou uloženou ve službě Active Directory.
- [**Virtual Network**][VPN]. Virtuální sítě jsou jedním z hlavních součástí virtuálního datového centra a umožňují vytvořit hranici izolace provozu na platformě Azure. Virtual Network se skládá z jednoho nebo několika segmentů virtuální sítě, z nichž každá má konkrétní předponu sítě IP (podsíť). Virtual Network definuje interní nárazníkovou oblast, kde IaaS virtuální počítače a PaaS služby můžou vytvořit soukromou komunikaci. Virtuální počítače (a služby PaaS) v jedné virtuální síti nemůžou komunikovat přímo s virtuálními počítači (a PaaS službami) v jiné virtuální síti, a to i v případě, že oba virtuální sítě vytvoří stejný zákazník v rámci stejného předplatného. Izolace je kritická vlastnost, která zajišťuje, že virtuální počítače a komunikace zákazníků zůstávají privátní v rámci virtuální sítě.
- [**Trasy definované uživatelem**][user-defined-routes]. Provoz ve virtuální síti je ve výchozím nastavení směrován v závislosti na tabulce směrování systému. Uživatelem definovaná trasa je vlastní směrovací tabulka, kterou můžou správci sítě přidružit k jedné nebo více podsítím, aby přepsaly chování systémové tabulky směrování a definovali cestu komunikace v rámci virtuální sítě. Existence uživatelem definovaných tras garantuje, že odchozí přenosy z přenosu paprsků prostřednictvím konkrétních vlastních virtuálních počítačů nebo síťových virtuálních zařízení a nástrojů pro vyrovnávání zatížení jsou přítomny v centru i paprskech.
- [**Skupiny zabezpečení sítě**][network-security-groups]. Skupina zabezpečení sítě je seznam pravidel zabezpečení, která se chovají jako filtrování provozu u zdrojů IP adres, cílů IP adres, protokolů, zdrojových portů IP a cílových portů IP. Skupinu zabezpečení sítě je možné použít pro podsíť, kartu virtuální síťové karty přidruženou k virtuálnímu počítači Azure nebo obojí. Skupiny zabezpečení sítě jsou nezbytné k implementaci správného řízení toku v centru a paprskech. Úroveň zabezpečení poskytovaná skupinou zabezpečení sítě je funkce, které porty otevřete a za jaký účel. Zákazníci by měli použít další filtry pro jednotlivé virtuální počítače s bránami firewall na hostitele, jako je softwaru iptables nebo brána Windows Firewall.
- [**Služba DNS**][DNS]. Překlad názvů prostředků v virtuální sítě implementace virtuálního datacentra se zajišťuje prostřednictvím DNS. Azure poskytuje služby DNS pro účely překladu [veřejného][DNS] i [privátního][PrivateDNS] názvu. Privátní zóny poskytují překlad názvů v rámci virtuální sítě i napříč virtuálními sítěmi. Privátní zóny můžete mít nejen mezi virtuálními sítěmi ve stejné oblasti, ale i v různých oblastech a předplatných. V případě veřejného řešení Azure DNS poskytuje hostitelskou službu pro domény DNS a zajišťuje překlad názvů pomocí Microsoft Azure infrastruktury. Pokud svoje domény hostujete v Azure, můžete spravovat svoje DNS záznamy pomocí stejných přihlašovacích údajů, rozhraní API a nástrojů a za stejných fakturačních podmínek jako u ostatních služeb Azure.
- [**Předplatné**][SubMgmt] a [**Správa skupin prostředků**][RGMgmt]. Předplatné definuje přirozenou hranici pro vytváření více skupin prostředků v Azure. Prostředky v předplatném se společně seskupují do logických kontejnerů označovaných jako skupiny prostředků. Skupina prostředků představuje logickou skupinu pro uspořádání prostředků implementace virtuálního datacentra.
- [**RBAC**][RBAC]. Prostřednictvím RBAC je možné namapovat organizační roli společně s právy pro přístup ke konkrétním prostředkům Azure, což vám umožní omezit uživatele jenom na určitou podmnožinu akcí. Pomocí RBAC můžete udělit přístup přidělením příslušné role uživatelům, skupinám a aplikacím v rámci příslušného oboru. Oborem přiřazení role může být předplatné Azure, skupina prostředků nebo jeden prostředek. RBAC umožňuje dědění oprávnění. Role přiřazená v nadřazeném oboru také uděluje přístup k podřízeným objektům, které jsou v ní obsažené. Pomocí RBAC můžete oddělit povinnosti a udělit jenom množství přístupu uživatelům, kteří potřebují k provádění svých úloh. Například použijte RBAC a umožněte jednomu zaměstnanci spravovat virtuální počítače v rámci předplatného, zatímco jiný může spravovat SQL databáze v rámci stejného předplatného.
- [**VNet peering**][VNetPeering]. Základní funkcí, která se používá k vytvoření infrastruktury virtuálního datacentra, je partnerský vztah virtuálních sítí, mechanismus, který spojuje dvě virtuální sítě (virtuální sítě) ve stejné oblasti prostřednictvím sítě Azure datacentra, nebo využívá páteřní síť Azure na celém světě napříč oblastmi. .

#### <a name="component-type-perimeter-networks"></a>Typ součásti: hraniční sítě

Komponenty [hraniční sítě][DMZ] umožňují připojení k síti mezi místními nebo fyzickými sítěmi Datacenter spolu s jakýmkoli připojením k Internetu a z něj. Je to také v případě, že vaše týmy sítě a zabezpečení pravděpodobně stráví většinu času.

Příchozí pakety by měly projít přes bezpečnostní zařízení v centru před tím, než se dokončí back-endové servery na paprskech. Příklady jsou brány firewall, ID a IP adresy. Předtím, než síť opustí, by se měly směrovat pakety vázané na Internet z zatížení, a to i přes bezpečnostní zařízení v hraniční síti. Účelem tohoto toku je vynucování zásad, kontrola a auditování.

Komponenty hraniční sítě poskytují následující funkce:

- [Virtuální sítě][VNet], [trasy definované uživatelem][user-defined-routes] a [skupiny zabezpečení sítě][network-security-groups]
- [Síťová virtuální zařízení][NVA]
- [Nástroj pro vyrovnávání zatížení Azure][ALB]
- [Azure Application Gateway][AppGW] s [firewallem webových aplikací (WAF)][AppGWWAF]
- [Veřejné IP adresy][PIP]
- [Přední dvířka Azure][AFD] s [firewallem webových aplikací (WAF)][AFDWAF]
- [Azure Firewall][AzFW]

Centrální týmy IT a zabezpečení mají obvykle zodpovědnost za definici požadavků a provoz hraničních sítí.

![7][7]

Předchozí diagram znázorňuje vynucování dvou hraničních zařízení s přístupem k Internetu a místní sítí, a to v centru DMZ. V centru DMZ se hraniční síť pro Internet může škálovat až na podporu velkého počtu objekty LOBs sů, a to pomocí několika Farm firewallů webových aplikací (WAF) nebo Azure firewallů. V centru se taky v případě potřeby umožňuje připojení přes VPN nebo ExpressRoute.

[**Virtuální sítě**][VNet]. Rozbočovač je typicky sestavený ve virtuální síti s více podsítěmi, aby bylo možné hostovat různé typy služeb, které filtrují a kontrolují provoz do Internetu prostřednictvím instancí síťová virtuální zařízení, WAF a Azure Application Gateway.

[**Trasy definované uživatelem**][user-defined-routes] Pomocí uživatelem definovaných tras můžou zákazníci nasazovat brány firewall, ID/IP adresy a další virtuální zařízení a směrovat síťový provoz přes tato bezpečnostní zařízení pro vynucování zásad zabezpečení, auditování a kontrolu. Trasy definované uživatelem lze vytvořit v centru i paprskech, aby bylo zajištěno, že přenos dat probíhá přes konkrétní vlastní virtuální počítače, síťovou virtuální zařízení a nástroje pro vyrovnávání zatížení, které používá implementace virtuálního datacentra. Aby bylo zaručeno, že provoz vygenerovaný z virtuálních počítačů umístěných v přenosech paprsků do správných virtuálních zařízení, musí být v podsítích na paprske nastavená trasa definovaná uživatelem nastavením IP adresy front-endu interního nástroje pro vyrovnávání zatížení jako Další směrování. Interní nástroj pro vyrovnávání zatížení distribuuje interní provoz na virtuální zařízení (back-endový fond nástroje pro vyrovnávání zatížení).

[**Azure firewall**][AzFW] je spravovaná cloudová služba zabezpečení sítě, která chrání vaše prostředky Azure Virtual Network. Jedná se o plně stavovou bránu firewall jako službu s integrovanou vysokou dostupností a neomezenou škálovatelností cloudu. Můžete centrálně vytvářet, vynucovat a protokolovat zásady připojení k aplikacím a sítím napříč různými předplatnými a virtuálními sítěmi. Azure Firewall používá pro prostředky virtuální sítě statickou veřejnou IP adresu. Externí brány firewall díky tomu můžou identifikovat provoz pocházející z vaší virtuální sítě. Služba je plně integrovaná se službou Azure Monitor zajišťující protokolování a analýzy.

[**Síťová virtuální zařízení**][NVA]. V centru se hraniční síť s přístupem k Internetu obvykle spravuje prostřednictvím Azure Firewall instance nebo farmy bran firewall nebo brány firewall webových aplikací (WAF).

Různé obchodní aplikace běžně využívají mnoho webových aplikací. Tyto aplikace často bývají postiženy ohroženími zabezpečení a potenciálními zneužitími. Firewall webových aplikací jsou speciálním typem produktu, který slouží k detekci útoků proti webovým aplikacím, HTTP/HTTPS ve větší hloubkě než k obecné bráně firewall. V porovnání s technologií brány firewall pro WAF mají sada specifických funkcí, které chrání interní webové servery před hrozbami.

Brána firewall Azure Firewall nebo síťové virtuální zařízení používá společnou rovinu pro správu se sadou pravidel zabezpečení pro ochranu zatížení hostovaných v paprskech a řízení přístupu k místním sítím. Azure Firewall má vestavěnou škálovatelnost, zatímco brány firewall síťové virtuální zařízení se dají ručně škálovat za nástroj pro vyrovnávání zatížení. Obecně platí, že farma brány firewall má méně specializovaný software v porovnání s WAF, ale má širší obor aplikace k filtrování a kontrole libovolného typu provozu v odchozích a příchozích přenosech. Pokud se použije přístup síťové virtuální zařízení, dají se najít a nasadit z webu Azure Marketplace.

Pro provoz pocházející z Internetu použijte jednu sadu bran firewall Azure (nebo síťová virtuální zařízení) a další pro provoz pocházející z místního prostředí. Použití jenom jedné sady bran firewall pro oba typy provozu představuje bezpečnostní riziko, protože mezi těmito dvěma sadami síťových provozů neexistuje žádná bezpečnostní hranice. Použití samostatných vrstev brány firewall snižuje složitost kontroly pravidel zabezpečení a umožňuje vymazat, která pravidla odpovídají konkrétní příchozí žádosti o síť.

Pro provoz pocházející z Internetu doporučujeme použít jednu sadu instancí Azure Firewall nebo síťová virtuální zařízení. Pro provoz pocházející z místního prostředí použijte jiný. Použití jenom jedné sady bran firewall pro obojí představuje bezpečnostní riziko, protože neposkytuje bezpečnostní okruh mezi dvěma sadami síťových přenosů. Použití samostatných vrstev brány firewall snižuje složitost kontroly pravidel zabezpečení a umožňuje vymazat, která pravidla odpovídají konkrétní příchozí žádosti o síť.

[**Azure Load Balancer**][ALB] nabízí vysoce dostupnou službu vrstvy 4 (TCP, UDP), která může distribuovat příchozí provoz mezi instancemi služby definované v sadě s vyrovnáváním zatížení. Provoz odeslaný do nástroje pro vyrovnávání zatížení z front-endové koncových bodů (koncové body veřejných IP adres nebo koncových bodů privátních IP adres) se dá znovu distribuovat pomocí nebo bez překladu adres do sady fondů back-end IP adres (příklady jsou síťová virtuální zařízení nebo virtuální počítače).

Azure Load Balancer může zjistit stav různých instancí serveru i když instance nereaguje na sondu, nástroj pro vyrovnávání zatížení zastaví odesílání provozu do poškozené instance. Ve virtuálním datovém centru se externí nástroj pro vyrovnávání zatížení nasadí do centra a paprsků. V centru se nástroj pro vyrovnávání zatížení používá k efektivnímu směrování provozu do služeb v paprskech a v paprskech se ke správě provozu aplikací používají nástroje pro vyrovnávání zatížení.

[Přední dvířka Azure (AFD)][AFD] jsou vysoce dostupná a škálovatelná platforma pro akceleraci webových aplikací, globální protokol HTTP Load Balancer, ochranu aplikací a Content Delivery Network. AFD běží ve více než 100 místech na hranici globální sítě Microsoftu a umožňuje sestavovat, provozovat a škálovat dynamickou webovou aplikaci a statický obsah. AFD poskytuje vaši aplikaci s výkonem koncových uživatelů, sjednocené oblasti údržby regionálního a razítka, automatizace BCDR, sjednocené informace o klientech a uživatelích, ukládání do mezipaměti a přehledy služeb. Platforma nabízí výkon, spolehlivost a podporu SLA, certifikace dodržování předpisů a auditované postupy zabezpečení, které jsou vyvíjené, provozované a nativně podporované v Azure.

[**Application Gateway**][AppGW] Microsoft Azure Application Gateway je vyhrazené virtuální zařízení poskytující kontroler doručování aplikací (ADC) jako službu a nabízí různé možnosti vyrovnávání zatížení vrstvy 7 pro vaši aplikaci. Umožňuje optimalizovat produktivitu webové farmy tím, že v aplikační bráně převede snižování zátěže protokolu SSL náročné na procesor. Nabízí také další možnosti přesměrování vrstvy 7, jako je kruhové dotazování na distribuci příchozích přenosů, spřažení relací na základě souborů cookie, přesměrování založené na cestách URL a možnost hostování několika webů za jedinou službou Application Gateway. Firewall webových aplikací (WAF) je také součástí skladové položky WAF služby Application Gateway. Tato SKU poskytuje ochranu webových aplikací před běžnými ohroženími zabezpečení webu a zneužitím. Application Gateway je možné nakonfigurovat jako internetovou bránu nebo jen jako interní bránu, případně jako kombinaci obojího.

[**Veřejné IP adresy**][PIP]. S některými funkcemi Azure můžete přidružit koncové body služby k veřejné IP adrese, aby se k prostředkům mohl dostat z Internetu. Tento koncový bod používá překlad adres (NAT) ke směrování provozu na interní adresu a port ve virtuální síti Azure. Tato cesta je primárním způsobem, jak externí provoz předat do virtuální sítě. Veřejné IP adresy můžete nakonfigurovat, abyste zjistili, jaký provoz se předává, a jak a kde se přeloží do virtuální sítě.

[**Azure DDoS Protection Standard**][DDoS] poskytuje další funkce pro zmírnění rizik oproti [základní úrovni služeb][DDoS] , které jsou vyladěné konkrétně na prostředky Azure Virtual Network. Služba DDoS Protection Standard se snadno povoluje a nevyžaduje žádné změny aplikací. Zásady ochrany jsou vyladěny prostřednictvím vyhrazeného monitorování provozu a algoritmů strojového učení. Zásady se aplikují na veřejné IP adresy přidružené k prostředkům nasazeným ve virtuálních sítích. Příklady jsou Azure Load Balancer, Azure Application Gateway a instance služby Azure Service Fabric. Telemetrie v reálném čase jsou k dispozici prostřednictvím Azure Monitor zobrazení během útoku a historie. Ochranu aplikační vrstvy lze přidat prostřednictvím brány firewall webových aplikací Azure Application Gateway. Jsou chráněny veřejné IP adresy IPv4 Azure.

#### <a name="component-type-monitoring"></a>Typ součásti: monitorování

Monitorovací komponenty poskytují přehled a výstrahy ze všech ostatních typů součástí. Všechny týmy by měly mít přístup k monitorování pro součásti a služby, ke kterým mají přístup. Pokud máte centralizovanou desku technické podpory nebo provozní týmy, vyžadují integrovaný přístup k datům poskytovaným těmito součástmi.

Azure nabízí různé typy služeb protokolování a monitorování, které sledují chování prostředků hostovaných v Azure. Řízení a řízení úloh v Azure se nepoužívá jenom na shromažďování dat protokolů, ale také na možnosti aktivace akcí na základě konkrétních hlášených událostí.

[**Azure monitor**][Monitor]. Azure obsahuje více služeb, které v prostoru monitorování samostatně provádějí určité role nebo úlohy. Tyto služby společně poskytují komplexní řešení pro shromažďování dat, analýzy a akce na základě telemetrie z vaší aplikace a prostředků Azure, které je podporují. Můžou také provádět monitorování důležitých místních prostředků s cílem poskytovat prostředí hybridního monitorování. Důkladné seznámení s dostupnými nástroji a daty je prvním krokem při vývoji úplné strategie monitorování pro vaši aplikaci.

V Azure existují dva hlavní typy protokolů:

- [Protokol aktivit Azure][ActLog], dříve nazývaný **provozní protokoly**, nabízí přehled o operacích, které byly provedeny u prostředků v rámci předplatného Azure. Tyto protokoly nahlásí události řídicích rovin pro vaše předplatná. Každý prostředek Azure vytvoří protokoly auditu.

- [Protokoly diagnostiky Azure monitor][DiagLog] jsou protokoly generované prostředkem, který poskytuje bohatou a častou datovou činnost tohoto prostředku. Obsah těchto protokolů se liší podle typu prostředku.

![9][9]

Je důležité sledovat protokoly pro skupiny zabezpečení sítě, zejména tyto informace:

- [Protokoly událostí][nsg-log] obsahují informace o tom, jaká pravidla skupiny zabezpečení sítě se aplikují na virtuální počítače a role instancí na základě adresy Mac.
- [Protokoly čítačů][nsg-log] sledují, kolikrát bylo každé pravidlo skupin zabezpečení sítě spuštěno pro odepření nebo povolení provozu.

Všechny protokoly se můžou ukládat do účtů úložiště Azure pro účely auditu, statické analýzy nebo zálohování. Když ukládáte protokoly do účtu služby Azure Storage, zákazníci můžou pomocí různých typů platforem načítat, sestavovat, analyzovat a vizualizovat tato data a ohlásit stav a stav cloudových prostředků.

Velké podniky by již měly získat standardní architekturu pro monitorování místních systémů. Můžou tyto platformy rozsazovat a integrovat protokoly generované nasazeními v cloudu. Pomocí [Azure Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-queries)můžou organizace uchovávat všechna protokolování v cloudu. Log Analytics je implementován jako cloudová služba. Díky tomu budete moct rychle pracovat s minimálními investicemi do služeb infrastruktury. Log Analytics se taky integruje s součástmi nástroje System Center, jako je System Center Operations Manager, aby se rozšířily vaše stávající investice do správy do cloudu.

Log Analytics je služba v Azure, která pomáhá shromažďovat, korelovat, Hledat a reagovat na data protokolů a výkonu vygenerovaná operačními systémy, aplikacemi a infrastrukturou cloudových komponent. Poskytuje zákazníkům provozní přehledy v reálném čase pomocí integrovaného vyhledávání a vlastních řídicích panelů k analýze všech záznamů napříč všemi vašimi úlohami ve vaší implementaci virtuálního datacentra.

[Azure Network Watcher][NetWatch] poskytuje nástroje pro monitorování, diagnostiku a zobrazení metrik a povolení nebo zakázání protokolů pro prostředky ve službě Azure Virtual Network. Jedná se o službu mnohotvárnou, která umožňuje následující funkce a další funkce:

- Monitoruje komunikaci mezi virtuálním počítačem a koncovým bodem.
- Zobrazit prostředky ve virtuální síti a jejich vztazích.
- Diagnostikujte problémy s filtrováním síťového provozu do nebo z virtuálního počítače.
- Diagnostikujte problémy se síťovým směrováním z virtuálního počítače.
- Diagnostikujte odchozí připojení z virtuálního počítače.
- Zachytávání paketů do a z virtuálního počítače.
- Diagnostikujte problémy s bránou virtuální sítě Azure a připojením.
- Určete relativní latence mezi oblastmi Azure a poskytovateli internetových služeb.
- Zobrazení pravidel zabezpečení pro síťové rozhraní.
- Zobrazit metriky sítě.
- Analýza provozu do nebo ze skupiny zabezpečení sítě.
- Zobrazení diagnostických protokolů pro síťové prostředky.

Řešení [Network Performance Monitor][NPM] v rámci Operations Management Suite může poskytovat podrobné informace o síti od začátku do konce. Tyto informace zahrnují jediné zobrazení sítí Azure a místních sítí. Řešení má konkrétní monitorování pro ExpressRoute a veřejné služby.

#### <a name="component-type-workloads"></a>Typ součásti: úlohy

Komponenty úloh se nacházejí v místě, kde jsou umístěny vaše skutečné aplikace a služby. Také tam, kde vývojové týmy vaší aplikace tráví většinu času.

Možnosti úlohy jsou nekonečné. Níže jsou uvedené jenom některé z možných typů úloh:

**Interní obchodní aplikace:** Obchodní aplikace jsou počítačové aplikace kritické pro probíhající provoz podniku. Obchodní aplikace mají některé běžné charakteristiky:

- **Interaktivní podle povahy:** Data se zadávají a výsledky nebo sestavy se vrátí.
- **Řízená daty:** Úlohy náročné na data s častým přístupem k databázím nebo jiným úložištěm.
- **Integrováno:** Úlohy, které nabízejí integraci s jinými systémy v rámci organizace nebo mimo ni.

**Weby směřující na zákazníky (Internet nebo interní):** Většina aplikací, které komunikují s internetem, je Web Sites. Azure nabízí možnost spuštění webu na virtuálním počítači s IaaS nebo na webu [Azure Web Apps][WebApps] (PaaS). Azure Web Apps podporuje integraci s virtuální sítě, která umožňuje nasazení Web Apps v síťové zóně s paprsky. Interní weby nepotřebují vystavit veřejný internetový koncový bod, protože prostředky jsou přístupné prostřednictvím privátních adres, které se nepoužívají z privátní virtuální sítě.

**Velké objemy dat a analýza:** Pokud data potřebují škálovat až na velký svazek, nemusí se databáze správně škálovat. Technologie Hadoop nabízí systém pro paralelní spouštění distribuovaných dotazů na velkém počtu uzlů. Zákazníci mají možnost spouštět datové úlohy na virtuálních počítačích s IaaS nebo PaaS ([HDInsight][HDI]). HDInsight podporuje nasazení do virtuální sítě založené na umístění, která se dá nasadit do clusteru v paprsku virtuálního datacentra.

**Události a zasílání zpráv:** [Azure Event Hubs][EventHubs] je služba ingestování telemetrie s škálovatelným škálováním, která shromažďuje, transformuje a ukládá miliony událostí. Jako platforma pro distribuované streamování nabízí nízkou latenci a konfigurovatelné časové uchovávání, což vám umožní ingestovat obrovské objemy telemetrie do Azure a číst tato data z více aplikací. Pomocí Event Hubs může jeden datový proud podporovat kanály založené na reálném čase i v dávce.

Pomocí [Azure Service Bus][ServiceBus]můžete implementovat vysoce spolehlivou cloudovou službu pro zasílání zpráv mezi aplikacemi a službami. Nabízí asynchronní zprostředkované zasílání zpráv mezi klientem a serverem, strukturovaným zasíláním zpráv FIFO (First-in-first-out-First-Out) a funkcemi pro publikování a odběr.

![10][10]

### <a name="make-a-virtual-datacenter-highly-available-multiple-virtual-datacenters"></a>Zajištění vysoké dostupnosti virtuálního datacentra: více virtuálních Datacenter

V podstatě se tento článek zaměřuje na návrh jediného virtuálního datového centra, které popisuje základní komponenty a architekturu, které přispívají k odolnosti. Funkce Azure, jako je Azure Load Balancer, síťová virtuální zařízení, sady dostupnosti, sady škálování, spolu s dalšími mechanismy přispívají k systému, který umožňuje vytvářet v provozních službách pevné úrovně smlouvy SLA.

Vzhledem k tomu, že jedno virtuální datové centrum je obvykle implementováno v rámci jedné oblasti, může být zranitelné vůči jakémukoli významnému výpadku, který má vliv na celou oblast. Zákazníci, kteří vyžadují vysokou SLA, musí chránit služby prostřednictvím nasazení stejného projektu ve dvou (nebo více) implementacích virtuálních datacenter umístěných v různých oblastech.

Kromě otázek SLA existuje několik běžných scénářů, ve kterých je nasazení více virtuálních Datacenter vhodné:

- Regionální nebo globální přítomnost.
- Zotavení po havárii.
- Mechanismus pro přesměrování provozu mezi datovými centry.

#### <a name="regionalglobal-presence"></a>Regionální/globální přítomnost

Datacentra Azure se nacházejí v mnoha oblastech po celém světě. Při výběru více datových center Azure musí zákazníci vzít v úvahu dva související faktory: geografické vzdálenosti a latence. Aby bylo možné nabídnout nejlepší uživatelské prostředí, vyhodnoťte zeměpisnou vzdálenost mezi jednotlivými implementacemi virtuálního datového centra a vzdáleností mezi jednotlivými implementacemi virtuálního datacentra a koncovými uživateli.

Oblast, ve které jsou hostované implementace virtuálních Datacenter, musí vyhovovat zákonným požadavkům zřízeným kteroukoli právní pravomocí, na jejímž základě vaše organizace pracuje.

#### <a name="disaster-recovery"></a>Zotavení po havárii

Návrh plánu zotavení po havárii závisí na typech úloh a možnosti Synchronizovat stav úloh mezi různými implementacemi virtuálních Datacenter. V ideálním případě většina zákazníků vyžaduje rychlý mechanismus pro převzetí služeb při selhání, což může vyžadovat synchronizaci dat aplikací mezi nasazeními, které spouští více implementací virtuálních Datacenter. Při návrhu plánů zotavení po havárii je ale důležité vzít v úvahu, že většina aplikací je citlivá na latenci, kterou může tato synchronizace dat způsobovat.

Synchronizace a monitorování prezenčního signálu aplikací v různých implementacích virtuálních Datacenter vyžaduje, aby komunikovaly přes síť. Prostřednictvím následujících dvou implementací v různých oblastech lze propojit:

- Partnerský vztah virtuálních sítí – VNet peering může propojit rozbočovače napříč oblastmi.
- ExpressRoute soukromý partnerský vztah, pokud jsou rozbočovače v každé implementaci virtuálního datacentra připojené ke stejnému okruhu ExpressRoute.
- Několik okruhů ExpressRoute připojených přes vaši firemní páteřní síť a několik implementací virtuálního datového centra, které se připojují k okruhům ExpressRoute.
- Připojení VPN typu Site-to-site mezi zónou centra implementací virtuálních Datacenter v každé oblasti Azure.

Síť VNet peering nebo připojení ExpressRoute jsou obvykle upřednostňovaným typem síťového připojení z důvodu vyšší šířky pásma a konzistentních úrovní latence při přechodu přes páteřní síť Microsoftu.

Zákazníkům doporučujeme, aby při ověřování latence a šířky pásma těchto připojení mohli zákazníci spustit testy kvalifikace sítě a rozhodnout se, jestli je na základě výsledku vhodná synchronní nebo asynchronní replikace dat. Je také důležité zvážit tyto výsledky v zobrazení optimálního cíle doby obnovení (RTO).

#### <a name="disaster-recovery-diverting-traffic-from-one-region-to-another"></a>Zotavení po havárii: přesměrování provozu z jedné oblasti do druhé

Služba [Azure Traffic Manager][traffic-manager] pravidelně kontroluje stav služeb veřejných koncových bodů v různých implementacích virtuálních Datacenter a pokud tyto koncové body selžou, směruje automaticky do sekundárního virtuálního datacentra pomocí systému DNS (Domain Name System). DNS).

Protože používá DNS, Traffic Manager se dá použít jenom s veřejnými koncovými body Azure. Služba se obvykle používá k řízení nebo přesměrování provozu do virtuálních počítačů Azure a Web Apps v dobré instanci implementace virtuálního datacentra. Traffic Manager je odolný i na tváři celé oblasti Azure a může řídit distribuci provozu uživatelů pro koncové body služby v různých virtuálních datacentrech na základě několika kritérií. Například selhání služby v konkrétní implementaci virtuálního datového centra nebo výběru implementace virtuálního datového centra s nejnižší latencí sítě.

### <a name="summary"></a>Souhrn

Virtuální datacentrum je přístup k migraci datového centra, který umožňuje vytvořit škálovatelnou architekturu v Azure, která maximalizuje využití prostředků v cloudu, snižuje náklady a zjednodušuje řízení systému. Virtuální datové centrum vychází z topologie sítě rozbočovače a paprsků, která poskytuje společné sdílené služby v centru a povoluje v paprskech konkrétní aplikace a úlohy. Virtuální datové centrum také odpovídá struktuře rolí společnosti, kde různá oddělení, jako je centrální IT, DevOps a provoz a údržba, společně fungují při provádění jejich specifických rolí. Virtuální datacentrum splňuje požadavky na migraci výtahu a posunutí, ale také poskytuje mnoho výhod nasazení nativních cloudů.

## <a name="references"></a>Odkazy

Následující funkce byly popsány v tomto dokumentu. Další informace získáte pomocí odkazů.

<!-- markdownlint-disable MD033 -->

|Síťové funkce|Vyrovnávání zatížení|Připojení|
|-|-|-|
|[Virtuální sítě Azure][VNet]</br>[Skupiny zabezpečení sítě][network-security-groups]</br>[Protokoly skupin zabezpečení sítě][nsg-log]</br>[Trasy definované uživatelem][user-defined-routes]</br>[Síťová virtuální zařízení][NVA]</br>[Veřejné IP adresy][PIP]</br>[DDoS Azure][DDoS]</br>[Azure Firewall][AzFW]</br>[Azure DNS][DNS]|[Azure Front Door][AFD]</br>[Azure Load Balancer (L3)][ALB]</br>[Application Gateway (L7)][AppGW]</br>[Firewall webových aplikací] WAF</br>[Azure Traffic Manager][traffic-manager]</br></br></br></br></br> |[Partnerské vztahy virtuálních sítí][VNetPeering]</br>[Virtuální privátní síť][VPN]</br>[Virtuální síť WAN][vWAN]</br>[ExpressRoute][ExR]</br>[ExpressRoute Direct][ExRD]</br></br></br></br></br>

|Identita</br>|Monitorování</br>|Osvědčené postupy</br>|
|-|-|-|
|[Azure Active Directory][azure-ad]</br>[Multi-Factor Authentication][multi-factor-authentication]</br>[Základní ovládací prvky přístupu role][RBAC]</br>[Výchozí role Azure AD][Roles]</br></br></br> |[Network Watcher][NetWatch]</br>[Azure Monitor][Monitor]</br>[Protokoly aktivit][ActLog]</br>[Diagnostické protokoly][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br>[Sledování výkonu sítě][NPM]|[Osvědčené postupy hraniční sítě][DMZ]</br>[Správa předplatných][SubMgmt]</br>[Správa skupin prostředků][RGMgmt]</br>[Omezení předplatného Azure][limits] </br></br></br>|

|Další služby Azure|
|-|
|[Azure Web Apps][WebApps]</br>[HDInsight (Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Další kroky

- Prozkoumejte vytváření [partnerských vztahů][VNetPeering]virtuálních sítí, což je technologie pro vytváření virtuálních Datacenter a paprskových návrhů.
- Implementujte [Azure AD][azure-ad] a začněte se zkoumáním [RBAC][RBAC] .
- Vytvořte předplatné a model správy prostředků a model RBAC pro splnění struktury, požadavků a zásad vaší organizace. Nejdůležitější aktivitou je plánování. Co je to možné, naplánujte reorganizace, fúze, nové produktové řádky a další okolnosti.

<!-- images -->

[0]: ../_images/vdc/networking-redundant-equipment.png "Příklady překrytí komponent"
[1]: ../_images/vdc/networking-vdc-high-level.png "Příklad středu a paprsku v rámci implementace virtuálního datového centra na vysoké úrovni"
[2]: ../_images/vdc/networking-hub-spokes-cluster.png "Cluster sítí s hvězdicovou topologií"
[3]: ../_images/vdc/networking-spoke-to-spoke.png "Propojení mezi paprsky"
[4]: ../_images/vdc/networking-vdc-block-level-diagram.png "Diagram úrovně bloku implementace virtuálního datového centra"
[5]: ../_images/vdc/networking-users-groups-subscriptions.png "Uživatelé, skupiny, předplatná a projekty"
[6]: ../_images/vdc/networking-infrastructure-high-level.png "Diagram vysoké úrovně infrastruktury"
[7]: ../_images/vdc/networking-high-level-perimeter-networks.png "Diagram vysoké úrovně infrastruktury"
[8]: ../_images/vdc/networking-vnet-peering-perimeter-networks.png "VNet Peering a hraniční sítě"
[9]: ../_images/vdc/networking-high-level-diagram-monitoring.png "Diagram vysoké úrovně pro monitorování"
[10]: ../_images/vdc/networking-high-level-workloads.png "Diagram vysoké úrovně pro úlohu"

<!-- links -->

[limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[multi-factor-authentication]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[azure-ad]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[vWAN]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[SubMgmt]: /azure/architecture/cloud-adoption/appendix/azure-scaffold
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[AppGWWAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[NPM]: https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
