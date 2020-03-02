---
title: Nasazení infrastruktury pro migraci
description: Přečtěte si, jak společnost Contoso nastaví infrastrukturu Azure pro migraci do Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/1/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 314cd954332907f9bf1bf63eb52ed5d88cfab121
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223137"
---
<!-- cspell:ignore CSPs domainname IPAM CIDR Untrust RRAS CONTOSODC sysvol ITIL NSGs ASGs -->

# <a name="deploy-a-migration-infrastructure"></a>Nasazení infrastruktury pro migraci

V tomto článku se dozvíte, jak fiktivní společnost Contoso připraví svoji místní infrastrukturu na migraci, v rámci příprav na migraci nastaví infrastrukturu Azure a dál provozuje svoji činnost v hybridním prostředí. Pokud se budete o tento příklad opírat při plánování migrace vlastní infrastruktury, myslete na tyto body:

- Uvedená ukázková architektura je specifická pro společnost Contoso. Když děláte důležitá rozhodnutí týkající se infrastruktury, třeba o návrhu předplatného nebo architektuře sítě, berte v úvahu obchodní požadavky, strukturu a technické požadavky své organizace.
- To, jestli potřebujete všechny prvky popsané v tomto článku, závisí na vaší strategii migrace. Pokud například vytváříte v Azure jenom nativní cloudové aplikace, budete možná potřebovat méně složitou síťovou strukturu.

## <a name="overview"></a>Přehled

Než společnost Contoso provede migraci do Azure, je zásadně důležité připravit na to infrastrukturu Azure. Obecně platí, že se společnost Contoso musí zamyslet nad těmito šesti oblastmi:

> [!div class="checklist"]
>
> - **Krok 1: předplatná Azure.** Jakou formou společnost Contoso nakoupí Azure a jak bude pracovat s platformou a službami Azure?
> - **Krok 2: hybridní identita** Jak bude po migraci spravovat a řídit přístup k místním prostředkům a prostředkům Azure? Jak společnost Contoso rozšíří nebo přesune správu identit do cloudu?
> - **Krok 3: zotavení po havárii a odolnost proti chybám.** Jak společnost Contoso zajistí odolnost svých aplikací a infrastruktury pro případ výpadků a havárií?
> - **Krok 4: vytvoření sítě.** Jak společnost Contoso navrhne síťovou infrastrukturu a vytvoří připojení mezi místním datacentrem a Azure?
> - **Krok 5: zabezpečení** Jak zabezpečí hybridní nasazení / nasazení do Azure?
> - **Krok 6: zásady správného řízení.** Jak společnost Contoso zajistí soulad nasazení s požadavky zabezpečení a zásad správného řízení?

## <a name="before-you-start"></a>Než začnete

Než se začneme zabývat infrastrukturou, možná byste si rádi přečetli pár základních informací o možnostech Azure, o kterých se v tomto článku zmiňujeme:

- K dispozici je několik možností, jak zakoupit přístup k Azure, včetně průběžných plateb, smluv Enterprise (EA), otevřených licencí od prodejců Microsoftu nebo od partnerů Microsoftu označovaných jako poskytovatelé cloudových řešení (CSP). Seznamte se s [možnostmi nákupu](https://azure.microsoft.com/pricing/purchase-options) a přečtěte si, [jak jsou uspořádaná předplatná Azure](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).
- Podívejte se na přehled [správy identit a přístupu](https://www.microsoft.com/trustcenter/security/identity) v Azure. Konkrétně se můžete seznámit s [Azure AD a rozšířením místní služby Active Directory do cloudu](https://docs.microsoft.com/azure/active-directory/identity-fundamentals). Můžete si stáhnout užitečnou elektronickou knihu o [správě identit a přístupu (IAM) v hybridním prostředí](https://azure.microsoft.com/resources/hybrid-cloud-identity).
- Azure poskytuje robustní síťovou infrastrukturu s možnostmi hybridního připojení. Podívejte se na přehled [sítí a řízení přístupu k sítím](https://docs.microsoft.com/azure/security/security-network-overview).
- Přečtěte si úvod do [zabezpečení Azure](https://docs.microsoft.com/azure/security/azure-security) a informace o vytvoření plánu [zásad správného řízení](https://docs.microsoft.com/azure/security/governance-in-azure).

## <a name="on-premises-architecture"></a>Místní architektura

Tento diagram znázorňuje aktuální místní infrastrukturu společnosti Contoso.

 ![Architektura společnosti Contoso](./media/contoso-migration-infrastructure/contoso-architecture.png)

- Společnost Contoso má jedno hlavní datacentrum v New Yorku na východě USA.
- V rámci USA má ještě tři další místní pobočky.
- Hlavní datové centrum je připojené k Internetu s vláknovým připojením k síti Ethernet (500 MB/s).
- Každá pobočka je místně připojená k internetu přes podnikové přípojky s tunely VPN IPSec, které vedou zpátky do hlavního datacentra. Díky tomu může být celá síť trvale připojená a má optimální připojení k internetu.
- Hlavní datové centrum je plně virtualizované prostřednictvím VMware. Společnost Contoso má dva hostitele virtualizace ESXi 6.5, které spravuje software vCenter Server 6.5.
- Společnost Contoso používá službu Active Directory pro správu identit a servery DNS ve vnitřní síti.
- Řadiče domény v datacentru běží na virtuálních počítačích VMware. Řadiče domény v místních pobočkách běží na fyzických serverech.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Krok 1: nákup a přihlášení k odběru Azure

Contoso se potřebuje rozhodnout, jak zakoupí Azure, jak uspořádá předplatná a jak získá licence na služby a prostředky.

### <a name="buy-azure"></a>Nákup Azure

Společnost Contoso si vybrala [smlouvu Enterprise (EA)](https://azure.microsoft.com/pricing/enterprise-agreement). Ta s sebou nese předběžný peněžní závazek vůči Azure, který dává společnosti Contoso nárok na získání skvělých výhod, včetně flexibilních možností fakturace a optimalizovaných cen.

- Společnost Contoso odhadla výši své roční útraty za Azure. Při podpisu smlouvy společnost Contoso zaplatila dopředu na celý první rok.
- Contoso musí celý závazek do jednoho roku využít, jinak jí zaplacené peníze propadnou.
- Pokud Contoso z nějakého důvodu závazek překročí a utratí víc, Microsoft jí rozdíl vyfakturuje.
- Veškeré náklady nad rámec závazku se budou účtovat podle stejných sazeb, jaké jsou uvedené ve smlouvě se společností Contoso. Za překročení závazku se neúčtují žádné pokuty.

### <a name="manage-subscriptions"></a>Správa předplatných

Po platbě za Azure musí společnost Contoso zjistit, jak spravovat předplatná Azure. Contoso má smlouvu EA, takže počet předplatných Azure, která může vytvořit, není ničím omezený.

- Registrace Azure Enterprise určuje způsob, jak bude společnost pracovat se službami Azure, a definuje základní strukturu zásad správného řízení.
- Společnost Contoso v první řadě definovala strukturu registrace Enterprise, která se označuje jako vygenerované podnikové uživatelské prostředí. Společnost Contoso použila [pokyny pro generování uživatelského rozhraní Azure Enterprise](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance) a pomůže vám pochopit a navrhovat generování uživatelského rozhraní.
- Prozatím se společnost Contoso rozhodla použít funkční přístup ke správě předplatných.
  - V rámci podniku bude mít jedno oddělení IT, které bude řídit rozpočet na Azure. Tato skupina bude jedinou skupinou s předplatnými.
  - Contoso tento model v budoucnu rozšíří, takže se do registrace Enterprise přidají další podnikové skupiny, které budou tvořit oddělení.
  - Uvnitř oddělení IT vytvořila společnost Contoso dvě předplatná, produkční a vývojářské.
  - Pokud bude Contoso v budoucnu potřebovat další předplatná, bude pro ně muset spravovat přístup, zásady a dodržování předpisů. To společnost Contoso zajistí zavedením [skupin pro správu Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview), které budou představovat další úroveň nad předplatnými.

  ![Podniková struktura](./media/contoso-migration-infrastructure/enterprise-structure.png)

### <a name="examine-licensing"></a>Zamyšlení nad licencemi

Jakmile Contoso nakonfiguruje předplatná, může začít přemýšlet od licencích Microsoftu. Strategie licencování bude záviset na zdrojích, které chce společnost Contoso migrovat do Azure, a na tom, jak jsou vybrané a nasazené virtuální počítače Azure a služby.

#### <a name="azure-hybrid-benefit"></a>Zvýhodněné hybridní využití Azure

Při nasazování virtuálních počítačů v Azure zahrnují standardní image licenci, která se bude společnosti Contoso účtovat za každou minutu využívání softwaru. Společnost Contoso je ale dlouhodobým zákazníkem Microsoftu a udržuje smlouvy EA a otevřené licence s programem SA (Software Assurance).

Zvýhodněné hybridní využití Azure poskytuje společnosti Contoso cenově výhodnou metodu migrace, umožňuje jí totiž ušetřit na virtuálních počítačích Azure a úlohách SQL Serveru díky převodu nebo opakovanému použití licencí edice Datacenter a Standard systému Windows Server, na které se vztahuje program Software Assurance. Díky tomu bude Contoso platit za virtuální počítače a SQL Server nižší sazbu za výpočetní prostředky. [Další informace](https://azure.microsoft.com/pricing/hybrid-benefit).

#### <a name="license-mobility"></a>License Mobility

Mobilita licencí v rámci programu SA poskytuje zákazníkům s multilicencemi Microsoftu, jako je společnost Contoso, flexibilitu při nasazování serverových aplikací použitelných s aktivním programem SA v Azure. Díky tomu není potřeba kupovat nové licence. Za mobilitu se neúčtují žádné poplatky a stávající licence se dají snadno nasadit v Azure. [Další informace](https://azure.microsoft.com/pricing/license-mobility).

#### <a name="reserve-instances-for-predictable-workloads"></a>Rezervované instance pro předvídatelné úlohy

Předvídatelné úlohy jsou úlohy, které musí být na spuštěných virtuálních počítačích vždy dostupné. Například obchodní aplikace, jako je třeba systém SAP ERP. K nepředvídatelným úlohám zase patří úlohy proměnlivé, třeba virtuální počítače, které se zapínají při vysoké poptávce a vypínají při nízké poptávce.

![Rezervovaná instance](./media/contoso-migration-infrastructure/reserved-instance.png)

Výměnou za používání rezervovaných instancí pro specifické instance virtuálních počítačů, které je potřeba udržovat po dlouhou dobu, získá společnost Contoso slevu a také prioritní kapacitu. Díky [rezervovaným instancím Azure](https://azure.microsoft.com/pricing/reserved-vm-instances) v kombinaci se zvýhodněným hybridním využitím Azure může společnost Contoso ušetřit až 82 % z normálních sazeb s průběžnými platbami (duben 2018).

## <a name="step-2-manage-hybrid-identity"></a>Krok 2: Správa hybridní identity

Důležitým krokem při vytváření infrastruktury Azure je udělování a řízení přístupu uživatelů k prostředkům Azure pomocí správy identit a přístupu (IAM).

- Společnost Contoso se rozhodla rozšířit svoji místní službu Active Directory do cloudu, místo aby vytvářela v Azure nový oddělený systém.
- Za tím účelem vytvoří službu Active Directory založenou na Azure.
- Společnost Contoso nemá systém Office 365, takže musí zřídit novou službu Azure AD.
- Office 365 používá službu Azure AD ke správě uživatelů. Kdyby společnost Contoso používala Office 365, už by měla tenanta Azure AD a mohla ho použít jako primární adresář.
- [Přečtěte si další informace](https://support.office.com/article/understanding-office-365-identity-and-azure-active-directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9) o Azure AD pro Office 365 a [zjistěte](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory), jak přidat předplatné do existujícího tenanta Azure AD.

### <a name="create-an-azure-ad"></a>Vytvoření Azure AD

Společnost Contoso používá edici Azure AD Free, která je součástí předplatného Azure. Správci společnosti Contoso nastaví adresář následujícím způsobem:

1. Na webu [Azure Portal](https://portal.azure.com) přejdou do části **Vytvořit prostředek** > **Identita** > **Azure Active Directory**.
2. V části **Vytvořit adresář** zadají název adresáře, počáteční název domény a oblast, ve které se má vytvořit adresář služby Azure AD.

    ![Vytvoření Azure AD](./media/contoso-migration-infrastructure/azure-ad-create.png)

    > [!NOTE]
    > Vytvořený adresář má počáteční název domény ve formátu **název_domény.onmicrosoft.com**. Tento název není možné změnit ani odstranit. Místo toho je potřeba do Azure AD přidat vlastní registrovaný název domény.

### <a name="add-the-domain-name"></a>Přidání názvu domény

Pokud chce společnost Contoso používat svůj standardní název domény, její správci ho musí přidat do Azure AD jako vlastní název domény. Tato možnost jim umožní přiřadit známá uživatelská jména. Uživatel se tak může přihlásit třeba pomocí e-mailové adresy billg@contoso.com, místo aby musel zadávat adresu billg@contosomigration.microsoft.com.

Pokud chtějí nastavit vlastní název domény, přidají ho do adresáře, přidají položku DNS a pak název ověří v Azure AD.

1. Doménu přidají v části **Vlastní názvy domén** > **Přidat vlastní doménu**.
2. Pokud chtějí v Azure použít položku DNS, musí ji zaregistrovat u svého registrátora domén.

    - V seznamu **Vlastní názvy domén** zadají údaje DNS pro požadovanou doménu. Používá se položka MX.
    - K tomu potřebují přístup k názvovému serveru. Přihlásí se k doméně Contoso.com a vytvoří nový záznam MX pro položku DNS, kterou poskytuje Azure AD, pomocí uvedených údajů.

3. Jakmile se záznamy DNS zadají do podrobného názvu domény, správci výběrem možnosti **Ověřit** zkontrolují vlastní název domény.

     ![Azure AD DNS](./media/contoso-migration-infrastructure/azure-ad-dns.png)

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Nastavení místních skupin a uživatelů a skupin a uživatelů Azure

Služba Azure AD je teď spuštěná a správci společnosti Contoso potřebují přidat zaměstnance do místních skupin Active Directory, které se budou synchronizovat s Azure Active Directory. Měli by používat názvy místních skupin odpovídající názvům skupin prostředků v Azure. To usnadní identifikaci vzájemně si odpovídajících skupin pro účely synchronizace.

#### <a name="create-resource-groups-in-azure"></a>Vytvoření skupin prostředků v Azure

Skupiny prostředků Azure slouží k seskupení prostředků Azure. Použití ID skupiny prostředků umožňuje Azure provádět operace s prostředky v dané skupině.

- Předplatné Azure může obsahovat několik skupin prostředků, ale skupina prostředků může existovat jenom v rámci jednoho předplatného.
- Kromě toho může jedna skupina prostředků obsahovat několik prostředků, ale jeden prostředek může patřit jenom do jedné skupiny prostředků.

Správci společnosti Contoso nastavili skupiny prostředků Azure tak, jak shrnuje následující tabulka.

<!-- markdownlint-disable MD033 -->

**Skupina prostředků** | **Podrobnosti**
--- | ---
**ContosoCobRG** | Tato skupina obsahuje všechny prostředky týkající se kontinuity podnikání (COB). Obsahuje trezory, které bude Contoso používat pro službu Azure Site Recovery a službu Azure Backup.<br/><br/> Bude taky zahrnovat prostředky používané k migraci, včetně služeb Azure Migrate a Azure Database Migration Service.
**ContosoDevRG** | Tato skupina obsahuje prostředky pro vývoj a testování.
**ContosoFailoverRG** | Tato skupina slouží jako cílová zóna pro prostředky, u kterých došlo k převzetí služeb při selhání.
**ContosoNetworkingRG** | Tato skupina obsahuje všechny síťové prostředky.
**ContosoRG** | Tato skupina obsahuje prostředky související s produkčními aplikacemi a databázemi.

<!-- markdownlint-disable MD026 -->

Správci vytvoří skupiny prostředků následujícím způsobem:

1. Na webu Azure Portal > **Skupiny prostředků** přidají novou skupinu.
2. Pro každou skupinu zadají název, předplatné, ke kterému má skupina patřit, a oblast.
3. Skupiny prostředků se zobrazují v seznamu **Skupiny prostředků**.

    ![Skupiny prostředků](./media/contoso-migration-infrastructure/resource-groups.png)

##### <a name="scale-resource-groups"></a>Škálování skupin prostředků

V budoucnu bude Contoso podle potřeby přidávat další skupiny prostředků. Správci například můžou definovat skupinu prostředků pro každou aplikaci nebo službu, aby je mohli spravovat a zabezpečit odděleně.

#### <a name="create-matching-security-groups-on-premises"></a>Vytvoření odpovídajících skupin zabezpečení v místním prostředí

1. V místní službě Active Directory nastavili správci společnosti Contoso skupiny zabezpečení s názvy, které odpovídají názvům skupin prostředků Azure.

    ![Skupiny zabezpečení Active Directory v místním prostředí](./media/contoso-migration-infrastructure/on-prem-ad.png)

2. Pro účely správy vytvoří správci další skupinu, která se přidá ke všem ostatním skupinám. Tato skupina bude mít oprávnění ke všem skupinám prostředků v Azure. Do této skupiny se přidá omezený počet globálních správců.

### <a name="synchronize-active-directory"></a>Synchronizace Active Directory

Společnost Contoso chce poskytnout společnou identitu pro přístup k prostředkům v místním prostředí i v cloudu. Za tím účelem integruje místní službu Active Directory se službou Azure AD. Tento model nabízí tyto výhody:

- Uživatelé a organizace můžou využívat jednu identitu pro přístup k místním aplikacím i cloudovým službám, jako je Office 365 nebo tisíce dalších webů na internetu.
- Správci můžou využít skupiny ve službě Active Directory k implementaci [řízení přístupu na základě role (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) v Azure.

V zájmu usnadnění integrace používá společnost Contoso [nástroj Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Když nástroj nainstalujete a nakonfigurujete na řadiči domény, synchronizuje identity místní služby Active Directory do Azure AD.

### <a name="download-the-tool"></a>Stažení nástroje

1. Na webu Azure Portal přejdou správci společnosti Contoso do části **Azure Active Directory** > **Azure AD Connect** a stáhnou nejnovější verzi nástroje na server, který používají k synchronizaci.

    ![Stažení Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

2. Spustí instalaci souboru **AzureADConnect.msi** s volbou **Použít expresní nastavení**. Jedná se o nejběžnější instalaci, která se dá použít pro topologii s jednou doménovou strukturou a nabízí ověřování synchronizací hodnoty hash hesla.

    ![Průvodce nástroje Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

3. V okně **Připojení ke službě Azure AD** zadají správci přihlašovací údaje pro připojení k Azure AD (ve formátu admin@contoso.com nebo admin@contoso.onmicrosoft.com).

    ![Průvodce nástroje Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

4. V části **Připojení ke službě AD DS** zadají přihlašovací údaje k místní službě Active Directory (ve formátu CONTOSO\admin nebo contoso.com\admin).

     ![Průvodce nástroje Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

5. V části **Připraveno ke konfiguraci** zvolí **Po dokončení konfigurace spusťte proces konfigurace**, aby se synchronizace hned spustila. Pak provedou instalaci.

Poznámky:

- Společnost Contoso má přímé připojení k Azure. Pokud je vaše místní služba Active Directory za proxy serverem, přečtěte si tento [článek](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-troubleshoot-connectivity).

- Po první synchronizaci se v adresáři Azure AD objeví objekty místní služby Active Directory.

    ![Místní Active Directory v Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

- V každé skupině jsou na základě svých rolí zastoupení členové týmu IT společnosti Contoso.

    ![Členové místní služby Active Directory v Azure](./media/contoso-migration-infrastructure/on-prem-ad-group-members.png)

### <a name="set-up-rbac"></a>Nastavení RBAC

[Řízení přístupu na základě role (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) v Azure umožňuje podrobnou správu přístupu. Pomocí řízení přístupu na základě role v Azure můžete uživatelům poskytnout jenom takovou úroveň přístupu, jakou potřebují ke své práci. Role RBAC přiřazujete uživatelům, skupinám a aplikacím na příslušné úrovni. Role se dají přidělovat na úrovni předplatného, skupiny prostředků nebo konkrétního prostředku.

Správci společnosti Contoso teď přiřadí role skupinám Active Directory, které synchronizovali z místního prostředí.

1. Ve skupině prostředků **ControlCobRG** zvolí **Řízení přístupu (IAM)**  > **Přidat přiřazení role**.
2. V části **Přidat přiřazení role** > **Role** > **Přispěvatel** vyberou v seznamu skupinu **ContosoCobRG**. Skupina se pak zobrazí v seznamu **Vybraní členové**.
3. Tento postup opakují se stejnými oprávněními pro ostatní skupiny prostředků (kromě **ContosoAzureAdmins**) – přidají k účtu, který odpovídá dané skupině prostředků, oprávnění přispěvatele.
4. Skupině **ContosoAzureAdmins** přiřadí roli **Vlastník**.

    ![Členové místní služby Active Directory v Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

## <a name="step-3-design-for-resiliency"></a>Krok 3: návrh pro odolnost proti chybám

### <a name="set-up-regions"></a>Nastavení oblastí

Prostředky Azure se nasazují v rámci oblastí.

- Oblasti jsou uspořádané do zeměpisných oblastí a v rámci příslušných zeměpisných hranic se dodržují požadavky na rezidenci dat, suverenitu, dodržování předpisů a zajištění odolnosti.
- Oblast se skládá ze sady datacenter. Tato datacentra jsou nasazená v rámci hranic s definovanou latencí a propojená prostřednictvím vyhrazené oblastní sítě s nízkou latencí.
- Každá oblast Azure kvůli odolnosti spárovaná s jinou oblastí.
- Přečtěte si o [oblastech Azure](https://azure.microsoft.com/global-infrastructure/regions) a zjistěte, [jak jsou oblasti spárované](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

Společnost Contoso si vybrala primární oblast USA – východ 2 (umístěnou ve Virginii) a sekundární oblast USA – střed (umístěnou v Iowě). Vedlo ji k tomu několik důvodů:

- Datacentrum společnosti Contoso se nachází v New Yorku, a tak společnost Contoso brala v úvahu latenci k nejbližšímu datacentru.
- Oblast USA – východ 2 má všechny služby a produkty, které Contoso potřebuje. Ve všech oblastech Azure nejsou dostupné stejné produkty a služby. Můžete se podívat na [produkty Azure podle oblastí](https://azure.microsoft.com/global-infrastructure/services).
- Oblast USA – střed je v Azure spárovaná s oblastí USA – východ 2.

Když společnost Contoso přemýšlí o hybridním prostředí, musí vzít v úvahu i to, jak do návrhu oblastí zabudovat strategii odolnosti a zotavení po havárii. Strategie v podstatě sahají od nasazení do jedné oblasti, které spoléhá na to, že odolnost zajistí funkce platformy Azure, jako jsou domény selhání a párování oblastí, až po plně oboustranně aktivní model, ve kterém jsou cloudové služby nasazené ve dvou oblastech a takto poskytují služby uživatelům.

Společnost Contoso se rozhodla pro střední cestu. Nasadí aplikace a prostředky v primární oblasti a v sekundární oblasti bude uchovávat úplnou kopii infrastruktury, která bude v případě úplné havárie aplikací nebo selhání oblasti fungovat jako úplná záloha.

### <a name="set-up-availability"></a>Nastavení dostupnosti

**Skupiny dostupnosti:**

Skupiny dostupnosti pomáhají chránit aplikace a data před výpadkem místního hardwaru a sítě v rámci datacentra.

- Skupiny dostupnosti distribuují virtuální počítače Azure napříč různým fyzickým hardwarem v datacentru.
- Domény selhání představují základní hardware se společným zdrojem napájení a síťovým přepínačem v rámci datacentra. Virtuální počítače v jedné skupině dostupnosti jsou distribuované napříč různými doménami selhání, aby se minimalizovaly výpadky způsobené jedním hardwarem nebo selháním sítě.
- Aktualizační domény představují základní hardwarové komponenty, u kterých je možné ve stejnou chvíli provést údržbu nebo restart. Skupiny dostupnosti taky distribuují virtuální počítače napříč několika aktualizačními doménami, aby se zajistilo, že bude vždy funkční aspoň jedna instance.

Společnost Contoso bude implementovat sady dostupnosti všude tam, kde úlohy virtuálních počítačů vyžadují vysokou dostupnost. [Další informace](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

**Zóny dostupnosti:**

Zóny dostupnosti pomáhají chránit aplikace a data proti selhání, které by zasáhlo celé datacentrum v určité oblasti.

- Každá zóna dostupnosti představuje jedinečné fyzické umístění v oblasti Azure.
- Každou zónu tvoří jedno nebo několik datacenter vybavených nezávislým napájením, chlazením a sítí.
- Ve všech povolených oblastech existují minimálně tři samostatné zóny.
- Fyzické oddělení zón v rámci oblasti chrání aplikace a data před selháním datacenter.

Contoso bude nasazovat zóny dostupnosti podle toho, jak budou aplikace vyžadovat škálovatelnost, vysokou dostupnost a odolnost. [Další informace](https://docs.microsoft.com/azure/availability-zones/az-overview).

### <a name="set-up-backup"></a>Nastavení zálohování

**Azure Backup:**

Azure Backup umožňuje zálohovat a obnovovat disky virtuálních počítačů Azure.

- Azure Backup umožňuje automatizované zálohování imagí disků virtuálních počítačů uložených ve službě Azure Storage.
- Zálohy jsou konzistentní vzhledem k aplikacím a zajišťují transakční konzistenci zálohovaných dat a spuštění aplikací po obnovení.
- Pro případ selhání místního hardwaru podporuje služba Azure Backup místně redundantní úložiště (LRS) pro replikaci více kopií zálohovaných dat v datacentru.
- V případě výpadku na úrovni oblasti služba Azure Backup podporuje také geograficky redundantní úložiště (GRS) a replikuje data záloh do sekundární spárované oblasti.
- Azure Backup šifruje přenášená data pomocí AES 256. Zálohovaná neaktivní uložená data jsou zašifrovaná pomocí [šifrování služby Storage (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).

Společnost Contoso bude u všech produkčních virtuálních počítačů používat službu Azure Backup s geograficky redundantním úložištěm, která zajistí zálohování dat úloh a možnost jejich rychlé obnovy v případě výpadku nebo jiné události. [Další informace](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup).

### <a name="set-up-disaster-recovery"></a>Nastavení zotavení po havárii

**Azure Site Recovery:**

Služba Azure Site Recovery pomáhá zajistit kontinuitu podnikových procesů tím, že zajišťuje provoz obchodních aplikací a úloh během výpadků oblastí.

- Azure Site Recovery průběžně replikuje virtuální počítače Azure z primární do sekundární oblasti a zajišťuje tak funkční kopie v obou umístěních.
- V případě výpadku v primární oblasti převezmou vaši aplikaci nebo službu instance virtuálních počítačů replikované v sekundární oblasti, čímž se možné přerušení služeb omezí na minimum.
- Jakmile se obnoví normální provoz, aplikace nebo služby se můžou vrátit na virtuální počítače v primární oblasti.

Contoso implementuje Azure Site Recovery u všech produkčních virtuálních počítačů používaných pro kritické úlohy, aby zajistila co nejmenší přerušení služeb v případě výpadku primární oblasti. [Další informace](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)

## <a name="step-4-design-a-network-infrastructure"></a>Krok 4: návrh síťové infrastruktury

Společnost Contoso má vytvořený návrh oblastí a teď se může zamyslet na strategií pro sítě. Musí při tom zohlednit, jak místní datacentrum vzájemně komunikuje s Azure a jak navrhnout síťovou infrastrukturu v Azure. Konkrétně společnost Contoso čekají tyto úkoly:

- **Naplánovat hybridní připojení k síti.** Musí se rozhodnout, jak propojit sítě mezi místním prostředím a Azure.
- **Navrhnout síťovou infrastrukturu Azure.** Musí se rozhodnout, jak nasadí sítě v příslušných oblastech. Jak budou sítě komunikovat v rámci stejné oblasti a napříč oblastmi?
- **Navrhnout a nastavit sítě Azure.** Musí nastavit sítě a podsítě Azure a rozhodnout se, co se v nich bude nacházet.

### <a name="plan-hybrid-network-connectivity"></a>Plánování hybridního připojení k síti

Společnost Contoso se rozhodovala mezi [několika architekturami](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking) hybridních sítí mezi Azure a místním datacentrem. Další informace najdete v článku [Volba řešení pro připojení místní sítě k Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations).

Připomínáme, že místní síťovou infrastrukturu společnosti Contoso v současné době tvoří datacentrum v New Yorku a místní pobočky ve východní části USA. Všechna pracoviště mají připojení k internetu na podnikové úrovni. Každá pobočka je tedy připojená k datacentru přes tunel VPN IPSec na internetu.

![Síť společnosti Contoso](./media/contoso-migration-infrastructure/contoso-networking.png)

Společnost Contoso se nakonec rozhodla implementovat hybridní připojení tímto způsobem:

1. Vytvoří nové připojení VPN typu site-to-site mezi datacentrem společnosti Contoso v New Yorku a oběma oblastmi Azure, USA – východ 2 a USA – střed.
2. Datový provoz poboček mířící do virtuálních sítí Azure bude procházet hlavním datacentrem společnosti Contoso.
3. Když někdy společnost Contoso vertikálně navýší kapacitu nasazení Azure, vytvoří mezi datacentrem a oblastmi Azure připojení ExpressRoute. Až k tomu dojde, společnost Contoso si nechá připojení VPN typu site-to-site jenom pro účely převzetí služeb při selhání.
    - [Přečtěte si další informace](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) o volbě mezi hybridním řešením se sítí VPN a se službou ExpressRoute.
    - Podívejte se na [umístění a podporu služby ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-locations-providers).

**Jenom síť VPN:**

![Contoso VPN](./media/contoso-migration-infrastructure/hybrid-vpn.png)

**VPN a ExpressRoute:**

![VPN/ExpressRoute společnosti Contoso](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

### <a name="design-the-azure-network-infrastructure"></a>Návrh síťové infrastruktury Azure

Konfigurace sítě společnosti Contoso musí zajistit, aby bylo hybridní nasazení zabezpečené a škálovatelné. Společnost Contoso tento přístup provádí dlouhodobě a navrhuje virtuální sítě (virtuální sítě) jako odolné a připravené pro podniky. [Přečtěte si další informace](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) o plánování virtuálních sítí.

K propojení těchto dvou oblastí implementuje contoso model sítě typu hub-to-hub:

- V každé oblasti bude Contoso používat model hvězdicové architektury.
- K propojení sítí a center bude společnost Contoso používat partnerské vztahy sítí v Azure.

#### <a name="network-peering"></a>Partnerské vztahy sítí

Partnerský vztah k síti Azure spojuje virtuální sítě a rozbočovače. Globální partnerský vztah umožňuje připojení mezi virtuální sítí nebo rozbočovači v různých oblastech. Místní partnerský vztah připojuje virtuální sítě ve stejné oblasti. Partnerský vztah virtuálních sítí nabízí několik výhod:

- Provoz mezi partnerskými virtuálními sítěmi je privátní.
- Provoz mezi virtuálními sítěmi probíhá na páteřní síti Microsoftu. Komunikace mezi partnerskými virtuálními sítěmi nevyžaduje veřejný internet, brány ani šifrování.
- Partnerský vztah poskytuje nízkou latenci a velkou šířku pásma při propojení prostředků v různých virtuálních sítích.

[Získejte další informace](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) o partnerských vztazích sítí.

#### <a name="hub-to-hub-across-regions"></a>Propojení oblastí typu hub-to-hub

Contoso nasadí do každé oblasti centrum. Centrem je virtuální síť v Azure, která funguje jako ústřední bod připojení k vaší místní síti. Virtuální sítě tvořící centra se vzájemně propojí přes globální partnerský vztah virtuálních sítí. Globální partnerský vztah virtuálních sítí propojuje virtuální sítě napříč oblastmi Azure.

- Centrum v každé oblasti je partnerským vztahem připojené k partnerskému centru v jiné oblasti.
- Centrum je v partnerském vztahu s každou sítí ve své oblasti a může se připojit ke všem síťovým prostředkům.

    ![Globální partnerský vztah](./media/contoso-migration-infrastructure/global-peering.png)

#### <a name="hub-and-spoke-model-within-a-region"></a>Model hvězdicové architektury v rámci oblasti

V rámci každé oblasti bude Contoso nasazovat virtuální sítě pro různé účely, které budou hvězdicově vycházet z centra oblasti. Virtuální sítě v rámci určité oblasti se připojují k centru a mezi sebou pomocí partnerského vztahu.

#### <a name="design-the-hub-network"></a>Návrh centrální sítě

Vzhledem k tomu, že si společnost Contoso zvolila model hvězdicové architektury, musí se zamyslet nad tím, jak bude směrovat provoz z místního datacentra a internetu. Společnost Contoso se rozhodla vyřešit směrování center oblastí USA – východ 2 i USA – střed tímto způsobem:

- Společnost Contoso navrhuje síť označovanou jako „reverse c“ podle cesty, kterou budou procházet pakety z příchozí do odchozí sítě.
- Síťová architektura má dvě hranice, nedůvěryhodnou front-endovou hraniční zónu a důvěryhodnou back-endovou zónu.
- V každé zóně se bude nacházet síťový adaptér brány firewall, který bude řídit přístup k důvěryhodným zónám.
- Z internetu:
  - Internetový provoz bude přicházet na veřejnou IP adresu s vyrovnáváním zatížení v hraniční síti.
  - Tento provoz se bude směrovat přes bránu firewall a bude podléhat pravidlům brány firewall.
  - Po implementaci řízení přístupu k síti se provoz přepošle na příslušné místo v důvěryhodné zóně.
  - Odchozí provoz z virtuální sítě se bude směrovat na internet přes uživatelsky definované trasy. Provoz bude muset projít bránou firewall a podrobit se kontrole podle zásad společnosti Contoso.
- Z datacentra společnosti Contoso:
  - Příchozí provoz přes síť VPN typu site-to-Site (nebo ExpressRoute) dorazí na veřejnou IP adresu služby Azure VPN Gateway.
  - Provoz se bude směrovat přes bránu firewall a bude podléhat pravidlům brány firewall.
  - Po uplatnění pravidel brány firewall se provoz přepošle do interního nástroje pro vyrovnávání zatížení (standardní SKU) v podsíti důvěryhodné interní zóny.
  - Odchozí provoz z důvěryhodné podsítě do místního datacentra prostřednictvím sítě VPN se směruje přes bránu firewall, uplatní se na něj pravidla a pak putuje přes síť VPN do připojení typu site-to-site.

### <a name="design-and-set-up-azure-networks"></a>Návrh a nastavení sítí Azure

Společnost Contoso má vytvořenou topologii sítě a směrování a teď může nastavit sítě a podsítě Azure.

- Contoso implementuje v Azure privátní síť třídy A (0.0.0.0 až 127.255.255.255). To je možné díky tomu, že místní prostředí má adresní prostor privátních adres třídy B 172.160.0/16, což dává společnosti Contoso jistotu, že se rozsahy adres nebudou překrývat.
- Společnost nasadí virtuální sítě v primární a sekundární oblasti.
- Společnost Contoso použije konvenci vytváření názvů, která zahrnuje předponu **VNET** a zkratku oblasti **EUS2** nebo **CUS**. Vzhledem k tomuto standardu budou mít centrální sítě název **VNET-HUB-EUS2** (USA – východ 2) a **VNET-HUB-CUS** (USA – střed).
- Společnost Contoso nemá [řešení IPAM](https://docs.microsoft.com/windows-server/networking/technologies/ipam/ipam-top), takže potřebuje naplánovat směrování sítě bez překladu adres (NAT).

#### <a name="virtual-networks-in-east-us-2"></a>Virtuální sítě v oblasti USA – východ 2

USA – východ 2 je primární oblast, kterou společnost Contoso použije k nasazení prostředků a služeb. V jejím rámci společnost Contoso zvolí následující uspořádání sítí:

- **Centrum:** Virtuální síť centra v Východní USA 2 je centrálním bodem primárního připojení k místnímu datovému centru.
- **Virtuální sítě:** Paprskový virtuální sítě v Východní USA 2 lze použít k izolaci úloh v případě potřeby. Kromě centrální virtuální sítě bude mít Contoso v oblasti USA – východ 2 dvě paprskové virtuální sítě:
  - **VNET-DEV-EUS2**. Tato virtuální síť poskytne týmu pro vývoj a testování plně funkční síť pro vývojářské projekty. Bude fungovat jako produkční oblast pro pilotní nasazení a při provozu se bude opírat na produkční infrastrukturu.
    - **VNET-PROD-EUS2**. V této síti se budou nacházet produkční komponenty Azure IaaS.
  - Každá virtuální síť bude mít vlastní jedinečný adresní prostor, který se nebude překrývat s ostatními. Společnost Contoso má v úmyslu nakonfigurovat směrování, které nevyžaduje překlad adres (NAT).
- **Podsítě:**
  - Každá síť bude obsahovat podsítě pro jednotlivé aplikační vrstvy.
  - Každá podsíť v produkční síti bude mít odpovídající podsíť ve virtuální síti pro vývoj.
  - Kromě toho obsahuje produkční síť podsíť pro řadiče domény.

Následující tabulka uvádí souhrn virtuálních sítí v oblasti USA – východ 2.

**Virtuální síť** | **Rozsah** | **Partnerský uzel**
--- | --- | ---
**VNET-HUB-EUS2** | 10.240.0.0/20 | VNET-HUB-CUS2, VNET-DEV-EUS2, VNET-PROD-EUS2
**VNET-DEV-EUS2** | 10.245.16.0/20 | VNET-HUB-EUS2
**VNET-PROD-EUS2** | 10.245.32.0/20 | VNET-HUB-EUS2, VNET-PROD-CUS

![Model hvězdicové architektury v primární oblasti](./media/contoso-migration-infrastructure/primary-hub-peer.png)

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Podsítě v centrální síti oblasti USA – východ 2 (VNET-HUB-EUS2)

**Podsíť/zóna** | **CIDR** | ** Použitelné IP adresy
--- | --- | ---
**IB-UntrustZone** | 10.240.0.0/24 | 251
**IB-TrustZone** | 10.240.1.0/24 | 251
**OB-UntrustZone** | 10.240.2.0/24 | 251
**OB-TrustZone** | 10.240.3.0/24 | 251
**GatewaySubnets** | 10.240.10.0/24 | 251

#### <a name="subnets-in-the-east-us-2-dev-network-vnet-dev-eus2"></a>Podsítě ve vývojářské síti oblasti USA – východ 2 (VNET-DEV-EUS2)

Virtuální síť pro vývojáře používá vývojový tým jako zónu pro pilotní nasazení do produkčního prostředí. Obsahuje tři podsítě.

**Podsíť** | **CIDR** | **Adresy** | **V podsíti**
--- | --- | --- | ---
**DEV-FE-EUS2** | 10.245.16.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
**DEV-APP-EUS2** | 10.245.20.0/22 | 1019 | Virtuální počítače aplikační vrstvy
**DEV-DB-EUS2** | 10.245.24.0/23 | 507 | Virtuální počítače databáze

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Podsítě v produkční síti oblasti USA – východ 2 (VNET-PROD-EUS2)

V produkční síti se nacházejí komponenty Azure IaaS. Každá aplikační vrstva má vlastní podsíť. Podsítě odpovídají podsítím ve vývojářské síti, navíc je tu ještě podsíť pro řadiče domény.

**Podsíť** | **CIDR** | **Adresy** | **V podsíti**
--- | --- | --- | ---
**PROD-FE-EUS2** | 10.245.32.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
**PROD-APP-EUS2** | 10.245.36.0/22 | 1019 | Virtuální počítače aplikační vrstvy
**PROD-DB-EUS2** | 10.245.40.0/23 | 507 | Virtuální počítače databáze
**PROD-DC-EUS2** | 10.245.42.0/24 | 251 | Virtuální počítače řadičů domény

![Architektura centrální sítě](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Virtuální sítě v oblasti USA – střed (sekundární oblast)

USA – střed je sekundární oblast společnosti Contoso. V jejím rámci společnost Contoso zvolí následující uspořádání sítí:

- **Centrum:** Virtuální síť rozbočovače v Východní USA 2 je centrálním bodem připojení k místnímu datovému centru a paprskový virtuální sítě v Východní USA 2 můžete použít k izolaci úloh v případě potřeby, které se spravují odděleně od ostatních paprsků.
- **Virtuální sítě:** Contoso bude mít v Střed USA dvě virtuální sítě:
  - VNET-PROD-CUS. Tato virtuální síť je produkční síť, podobně jako VNET-PROD_EUS2.
  - VNET-ASR-CUS. Tato virtuální síť bude fungovat jako místo, kde se po převzetí služeb při selhání z místního prostředí vytvářejí virtuální počítače, nebo jako umístění pro virtuální počítače Azure, u kterých došlo k převzetí služeb při selhání z primární do sekundární oblasti. Tato síť se podobá produkčním sítím, ale neobsahuje žádné řadiče domény.
  - Každá virtuální síť v oblasti bude mít vlastní adresní prostor, který se nebude překrývat s ostatními. Contoso nakonfiguruje směrování bez překladu adres (NAT).
- **Podsítě:** Podsítě budou navrženy podobným způsobem jako v Východní USA 2. Výjimkou je, že společnost Contoso nepotřebuje podsíť pro řadiče domény.

Následující tabulka uvádí souhrn virtuálních sítí v oblasti USA – střed.

**Virtuální síť** | **Rozsah** | **Partnerský uzel**
--- | --- | ---
**VNET-HUB-CUS** | 10.250.0.0/20 | VNET-HUB-EUS2, VNET-ASR-CUS, VNET-PROD-CUS
**VNET-ASR-CUS** | 10.255.16.0/20 | VNET-HUB-CUS, VNET-PROD-CUS
**VNET-PROD-CUS** | 10.255.32.0/20 | VNET-HUB-CUS, VNET-ASR-CUS, VNET-PROD-EUS2

![Model hvězdicové architektury ve spárované oblasti](./media/contoso-migration-infrastructure/paired-hub-peer.png)

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Podsítě v centrální síti oblasti USA – střed (VNET-HUB-CUS)

**Podsíť** | **CIDR** | **Použitelné IP adresy**
--- | --- | ---
**IB-UntrustZone** | 10.250.0.0/24 | 251
**IB-TrustZone** | 10.250.1.0/24 | 251
**OB-UntrustZone** | 10.250.2.0/24 | 251
**OB-TrustZone** | 10.250.3.0/24 | 251
**GatewaySubnet** | 10.250.2.0/24 | 251

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Podsítě v produkční síti oblasti USA – střed (VNET-PROD-CUS)

Paralelně s produkční sítí v primárním Východní USA 2 oblasti je produkční síť v sekundární Střed USA oblasti.

**Podsíť** | **CIDR** | **Adresy** | **V podsíti**
--- | --- | --- | ---
**PROD-FE-CUS** | 10.255.32.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
**PROD-APP-CUS** | 10.255.36.0/22 | 1019 | Virtuální počítače aplikační vrstvy
**PROD-DB-CUS** | 10.255.40.0/23 | 507 | Virtuální počítače databáze
**PROD-DC-CUS** | 10.255.42.0/24 | 251 | Virtuální počítače řadičů domény

#### <a name="subnets-in-the-central-us-failoverrecovery-network-in-central-us-vnet-asr-cus"></a>Podsítě v síti pro převzetí služeb při selhání / obnovení v oblasti USA – střed (VNET-ASR-CUS)

Síť VNET-ASR-CUS se používá pro účely převzetí služeb při selhání mezi oblastmi. K replikaci a převzetí služeb při selhání virtuálních počítačů Azure se využije služba Site Recovery. Ta funguje také jako datacentrum společnosti Contoso v síti Azure pro chráněné úlohy, které zůstávají v místním prostředí, ale pro účely zotavení po havárii přebírá jejich služby při selhání platforma Azure.

VNET-ASR-CUS je stejná základní podsíť jako produkční virtuální síť v oblasti USA – východ 2, jenom nepotřebuje podsíť pro řadiče domény.

**Podsíť** | **CIDR** | **Adresy** | **V podsíti**
--- | --- | --- | ---
**ASR-FE-CUS** | 10.255.16.0/22 | 1019 | Virtuální počítače front-endu / webové vrstvy
**ASR-APP-CUS** | 10.255.20.0/22 | 1019 | Virtuální počítače aplikační vrstvy
**ASR-DB-CUS** | 10.255.24.0/23 | 507 | Virtuální počítače databáze

![Architektura centrální sítě](./media/contoso-migration-infrastructure/azure-networks-cus.png)

#### <a name="configure-peered-connections"></a>Konfigurace partnerských připojení

Centrum v každé oblasti bude partnerským vztahem spojené s centrem v druhé oblasti a se všemi virtuálními sítěmi ve své oblasti. Díky tomu můžou centra vzájemně komunikovat a zobrazovat všechny virtuální sítě v rámci oblasti. Poznámky:

- Partnerský vztah vytváří oboustranné připojení. Jedno od iniciujícího partnerského uzlu v první virtuální síti a druhé ve druhé virtuální síti.
- V hybridním nasazení musí být provoz, který prochází mezi partnerskými uzly, viditelný z připojení VPN mezi místním datacentrem a Azure. K tomu je potřeba zvolit u partnerských připojení určitá zvláštní nastavení.

U všech připojení od paprskových virtuálních sítí přes centrum do místního datacentra musí společnost Contoso povolit přesměrování provozu a průchod bránami sítě VPN.

##### <a name="domain-controller"></a>Řadič domény

V případě řadičů domény v síti VNET-PROD-EUS2 společnost Contoso chce, aby provoz probíhal jak mezi centrem EUS2 a produkční sítí, tak přes připojení VPN do místního prostředí. K tomu je potřeba, aby správci společnosti Contoso povolili tato nastavení:

1. **Povolit přesměrovaný přenos** a **Povolit průchod bránou** u partnerského připojení. V našem příkladu by to bylo připojení ze sítě VNET-HUB-EUS2 do sítě VNET-PROD-EUS2.

    ![Partnerské vztahy](./media/contoso-migration-infrastructure/peering1.png)

2. **Povolit přesměrovaný přenos** a **Používat vzdálené brány** na druhé straně partnerského vztahu, u připojení ze sítě VNET-PROD-EUS2 do sítě VNET-HUB-EUS2.

    ![Partnerské vztahy](./media/contoso-migration-infrastructure/peering2.png)

3. V místním prostředí nastaví statickou trasu, která přesměruje místní provoz přes tunelové připojení VPN do virtuální sítě. Konfiguraci dokončí na bráně, která poskytuje tunelové připojení VPN společnosti Contoso do Azure. K tomu použijí službu RRAS.

    ![Partnerské vztahy](./media/contoso-migration-infrastructure/peering3.png)

##### <a name="production-networks"></a>Produkční sítě

Paprsková partnerská síť nevidí prostřednictvím centra paprskovou partnerskou síť v jiné oblasti.

K tomu, aby se produkční sítě společnosti Contoso z obou oblastí navzájem viděly, musejí správci společnosti Contoso vytvořit přímé partnerské připojení mezi sítěmi VNET-PROD-EUS2 a VNET-PROD-CUS.

![Partnerské vztahy](./media/contoso-migration-infrastructure/peering4.png)

### <a name="set-up-dns"></a>Nastavení DNS

Při nasazování prostředků ve virtuálních sítích si můžete vybrat z několika možností překladu názvů domén. Můžete použít překlad adres poskytovaný Azure nebo zajistit servery DNS pro překlad. To, který typ překladu názvů použijete, závisí na tom, jak spolu vaše prostředky potřebují vzájemně komunikovat. Získejte [další informace](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#azure-provided-name-resolution) o službě Azure DNS.

Správci společnosti Contoso se rozhodli, že služba Azure DNS není v hybridním prostředí dobrou volbou. Místo ní použijí místní servery DNS.

- Vzhledem k tomu, že se jedná o hybridní síť, všechny virtuální počítače v místním prostředí a v Azure musí být schopné přeložit názvy, aby správně fungovaly. To znamená, že se vlastní nastavení DNS musí použít pro všechny virtuální sítě.
- Společnost Contoso má v současnosti řadiče domény nasazené v datacentru společnosti a ve firemních pobočkách. Primární servery DNS jsou CONTOSODC1 (172.16.0.10) a CONTOSODC2 (172.16.0.1).
- Po nasazení virtuálních sítí se místní řadiče domény nastaví tak, aby v sítích fungovaly jako servery DNS.
- To je možné jenom tehdy, když se při použití vlastního DNS ve virtuální síti přidá do seznamu DNS IP adresa rekurzivního překladače Azure (například 168.63.129.16). Společnost Contoso proto nakonfiguruje nastavení serveru DNS v každé virtuální síti. Například vlastní nastavení DNS pro síť VNET-HUB-EUS2 by vypadalo takto:

    ![Vlastní DNS](./media/contoso-migration-infrastructure/custom-dns.png)

Kromě místních řadičů domény společnost Contoso implementuje čtyři další řadiče domény, aby podporovaly sítě Azure, a to dvě pro každou oblast. Contoso tedy do Azure nasadí následující prvky.

**Oblast** | **Řadič domény** | **Virtuální síť** | **Podsíť** | **IP adresa**
--- | --- | --- | --- | ---
EUS2 | CONTOSODC3 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.4
EUS2 | CONTOSODC4 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.5
CUS | CONTOSODC5 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4
CUS | CONTOSODC6 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4

Po nasazení místních řadičů domény musí Contoso aktualizovat nastavení DNS v sítích v obou oblastech a přidat do seznamu serverů DNS nové řadiče domény.

#### <a name="set-up-domain-controllers-in-azure"></a>Nastavení řadičů domény v Azure

Po aktualizaci nastavení sítě můžou správci společnosti Contoso začít vytvářet řadiče domény v Azure.

1. Na webu Azure Portal nasadí do příslušné virtuální sítě nový virtuální počítač s Windows Serverem.
2. V každém umístění vytvoří pro virtuální počítač skupiny dostupnosti. Skupiny dostupnosti mají tyto funkce:

    - Dbají na to, aby prostředky infrastruktury Azure rozdělovaly virtuální počítače do různých infrastruktur v dané oblasti Azure.
    - dávají společnosti Contoso nárok na 99,95% smlouvu SLA pro virtuální počítače v Azure. [Další informace](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets).

    ![Skupina dostupnosti](./media/contoso-migration-infrastructure/availability-group.png)

3. Po nasazení virtuálního počítače otevřou správci pro tento virtuální počítač síťové rozhraní. Nastaví privátní IP adresu na statickou a určí platnou adresu.

    ![VM NIC](./media/contoso-migration-infrastructure/vm-nic.png)

4. Teď k virtuálnímu počítači připojí nový datový disk. Tento disk obsahuje databázi služby Active Directory a sdílenou složku sysvol.
    - Velikost disku má vliv na to, jaký počet vstupně-výstupních operací (IOPS) bude podporovat.
    - Postupem času a s rozrůstáním prostředí může být potřeba velikost disku zvětšit.
    - Disk by neměl být nastavený na čtení/zápis, aby podporoval využití paměti hostitele. Databáze Active Directory tuto funkci nepodporují.

     ![Disk Active Directory](./media/contoso-migration-infrastructure/ad-disk.png)

5. Po přidání disku se správci přes vzdálenou plochu připojí k virtuálnímu počítači a otevřou Správce serveru.

6. Pak v části **Souborová služba a služba úložiště** spustí průvodce novým svazkem a zajistí, aby disk dostal v místním virtuálním počítači přiřazené písmeno F: nebo vyšší.

     ![Průvodce novým svazkem](./media/contoso-migration-infrastructure/volume-wizard.png)

7. Ve Správci serveru přidají roli **Active Directory Domain Services**. Pak nakonfigurují virtuální počítač jako řadič domény.

      ![Role serveru](./media/contoso-migration-infrastructure/server-role.png)

8. Po nakonfigurování virtuálního počítače jako řadiče domény a jeho restartování otevřou Správce DNS a nakonfigurují překladač Azure DNS jako modul pro předávání. Řadič domény tak bude moct předávat dotazy DNS, které nedokáže přeložit v Azure DNS.

    ![Modul pro předávání DNS](./media/contoso-migration-infrastructure/dns-forwarder.png)

9. Teď aktualizují vlastní nastavení DNS pro každou virtuální síť s příslušným řadičem domény pro oblast virtuální sítě. Do seznamu přidají i místní řadiče domény.

### <a name="set-up-active-directory"></a>Nastavení služby Active Directory

Služba Active Directory má z hlediska sítí zásadní význam a je potřeba ji správně nakonfigurovat. Správci společnosti Contoso vytvoří pro datacentrum společnosti a oblasti EUS2 a CUS lokality Active Directory.

1. Vytvoří dvě nové lokality (AZURE-EUS2 a AZURE-CUS) a lokalitu datacentra (ContosoDatacenter).
2. Po vytvoření lokalit vytvoří v těchto lokalitách podsítě odpovídající virtuálním sítím a datacentru.

    ![Podsítě řadiče domén](./media/contoso-migration-infrastructure/dc-subnets.png)

3. Potom vytvoří dvě propojení lokalit, která všechno vzájemně propojí. Pak by se měl provést přesun řadičů domény do příslušného umístění.

    ![Propojení řadičů domény](./media/contoso-migration-infrastructure/dc-links.png)

4. Až bude všechno nakonfigurované, vznikne hotová topologie replikace služby Active Directory.

    ![Replikace řadičů domén](./media/contoso-migration-infrastructure/ad-resolution.png)

5. Po dokončení se v místním Centru správy služby Active Directory zobrazí seznam řadičů domény a lokalit.

    ![Centrum správy služby Active Directory](./media/contoso-migration-infrastructure/ad-center.png)

## <a name="step-5-plan-for-governance"></a>Krok 5: plánování zásad správného řízení

Azure poskytuje v rámci různých služeb a platformy Azure řadu ovládacích prvků pro zásady správného řízení. Další informace najdete v tématu [Možnosti zásad správného řízení Azure](https://docs.microsoft.com/azure/security/governance-in-azure).

Během konfigurace identit a řízení přístupu už společnost Contoso začala řešit některé aspekty zásad správného řízení a zabezpečení. V podstatě existují tři oblasti, které je potřeba vzít v úvahu:

- **Zásada:** Azure Policy aplikuje a vynutila pravidla a vlivy na vaše prostředky, aby prostředky zůstaly v souladu s podnikovými požadavky a SLA.
- **Zámky:** Azure umožňuje uzamknout předplatná, skupiny prostředků a další prostředky, aby je bylo možné upravovat pouze pomocí těch, které mají oprávnění k tomu.
- **Značky:** Prostředky je možné řídit, auditovat a spravovat pomocí značek. Značky připojují k prostředkům metadata a poskytují informace o prostředcích nebo vlastnících.

### <a name="set-up-policies"></a>Nastavení zásad

Služba Azure Policy vyhodnocuje vaše prostředky a vyhledává mezi nimi ty, které nejsou v souladu s vašimi definicemi zásad. Například můžete mít zásadu, která povoluje jenom určité typy virtuálních počítačů nebo vyžaduje, aby měly prostředky určitou značku.

Zásady určují definici zásady a přiřazení zásady určuje rozsah, ve kterém se má určitá zásada použít. Rozsah může sahat od skupiny pro správu až po skupinu prostředků. [Přečtěte si](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) o vytváření a správě zásad.

Společnost Contoso chce začít jen s dvěma zásadami:

- Chce zásady zajistit, aby se prostředky mohly nasadit jenom v oblastech EUS2 a kapacitní jednotky.
- Chce omezit skladové položky virtuálních počítačů jenom na schválené skladové položky. Cílem je zajistit, aby se nepoužívaly drahé skladové jednotky virtuálních počítačů.

#### <a name="limit-resources-to-regions"></a>Omezení prostředků na oblasti

Společnost Contoso používá k omezení oblastí pro prostředky integrovanou definici **Povolené lokality**.

1. Na webu Azure Portal zvolte **Všechny služby** a vyhledejte **Zásady**.
2. Vyberte **Přiřazení** > **Přiřadit zásady**.
3. V seznamu zásad vyberte **Povolené lokality**.
4. Nastavte **Rozsah** na název předplatného Azure a v seznamu povolených lokalit vyberte obě oblasti.

    ![Povolené oblasti zásad](./media/contoso-migration-infrastructure/policy-region.png)

5. Ve výchozím nastavení je zásada nastavená na **Odepřít**, což znamená, že pokud někdo spustí v tomto předplatném nasazení mimo oblast EUS2 nebo CUS, nasazení se nezdaří. Na dalším obrázku vidíte, co se stane, když se někdo v rámci předplatného společnosti Contoso pokusí vytvořit nasazení v oblasti USA – západ.

    ![Nasazení se nezdařilo](./media/contoso-migration-infrastructure/policy-failed.png)

#### <a name="allow-specific-vm-skus"></a>Povolení určitých SKU virtuálních počítačů

Společnost Contoso pomocí integrované definice **Povolit SKU virtuálních počítačů** omezí to, jaký typ virtuálních počítačů je možné v předplatném vytvořit.

![Zásada SKU](./media/contoso-migration-infrastructure/policy-sku.png)

#### <a name="check-policy-compliance"></a>Kontrola dodržování zásad

Zásady začnou platit okamžitě a společnost Contoso může zkontrolovat, jestli jsou s nimi prostředky v souladu.

1. Na webu Azure Portal vyberte odkaz **Dodržování předpisů**.
2. Zobrazí se řídicí panel dodržování předpisů. Rozbalením nabídek zobrazíte další podrobnosti.

    ![Dodržování zásad](./media/contoso-migration-infrastructure/policy-compliance.png)

### <a name="set-up-locks"></a>Nastavení zámků

Společnost Contoso už dlouhou dobu používá ke správě svých systémů architekturu ITIL. Mezi nejdůležitější aspekty této architektury patří řízení změn a společnost Contoso chce zajistit, aby bylo řízení změn implementované i v nasazení Azure.

Společnost Contoso implementuje zámky následujícím způsobem:

- Každá komponenta produkčního prostředí nebo komponenta pro převzetí služeb při selhání se musí nacházet ve skupině prostředků, která má zámek ReadOnly. To znamená, že pokud chcete upravit nebo odstranit produkční položky, je potřeba zámek odebrat.
- Neprodukční skupiny prostředků budou mít zámky CanNotDelete. To znamená, že autorizovaní uživatelé můžou číst nebo upravovat prostředek, ale nemůžou ho odstranit.

[Přečtěte si další informace](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) o zámcích.

### <a name="set-up-tagging"></a>Nastavení značek

Pro společnost Contoso bude čím dál důležitější sledovat nově přidávané prostředky a moct je přidružit k příslušnému oddělení, zákazníkovi a prostředí.

Vedle poskytování informací o prostředcích a vlastnících umožní značky společnosti Contoso agregovat a seskupovat prostředky a získaná data používat k rozúčtování.

Společnost Contoso potřebuje mít možnost vizualizovat své prostředky Azure tak, aby to dávalo smysl z obchodního hlediska. Například podle role nebo oddělení. Upozorňujeme, že prostředky se stejnou značkou nemusí být umístěné ve stejné skupině prostředků. Společnost Contoso vytvoří jednoduchou taxonomii značek, aby všichni používali stejné značky.

**Název značky** | **Hodnota**
--- | ---
CostCenter | 12345: musí se jednat o platné nákladové středisko z SAP.
BusinessUnit | Název obchodní jednotky (ze systému SAP). Odpovídá značce CostCenter.
ApplicationTeam | E-mailový alias týmu, který je vlastníkem podpory aplikace.
CatalogName | Název aplikace nebo sdílených služeb podle katalogu služeb, který daný prostředek podporuje.
ServiceManager | E-mailový alias správce služeb ITIL pro daný prostředek.
COBPriority | Priorita nastavená firmou pro účely provozní kontinuity a zotavení po havárii. Hodnoty 1–5.
ENV | Možné hodnoty jsou DEV, STG a PROD. Představují vývojářské, přípravné a produkční prostředí.

Příklad:

 ![Značky Azure](./media/contoso-migration-infrastructure/azure-tag.png)

Po vytvoření značky se společnost Contoso vrátí a vytvoří nové definice a přiřazení zásad, aby mohla vynucovat použití požadovaných značek v rámci organizace.

## <a name="step-6-consider-security"></a>Krok 6: zvážení zabezpečení

Zabezpečení je v cloudu zcela zásadní a Azure poskytuje rozsáhlou nabídku nástrojů a možností zabezpečení. Ty vám pomůžou vytvořit zabezpečená řešení na zabezpečené platformě Azure. Další informace o zabezpečení Azure najdete v článku [Jistota v důvěryhodném cloudu](https://azure.microsoft.com/overview/trusted-cloud).

Společnost Contoso musí zohlednit několik aspektů:

- **Azure Security Center:** Azure Security Center poskytuje jednotnou správu zabezpečení a pokročilou ochranu před hrozbami napříč hybridními cloudy. Se službou Security Center můžete používat zásady zabezpečení napříč úlohami, omezit vystavení hrozbám a detekovat útoky a reagovat na ně. [Další informace](https://docs.microsoft.com/azure/security-center/security-center-intro).
- **Skupiny zabezpečení sítě (skupin zabezpečení sítě):** NSG je filtr (firewall), který obsahuje seznam pravidel zabezpečení, která při použití, povolení nebo zakázání síťového provozu pro prostředky připojené k Azure virtuální sítě. [Další informace](https://docs.microsoft.com/azure/virtual-network/security-overview).
- **Šifrování dat:** Azure Disk Encryption je funkce, která vám pomůže s šifrováním disků virtuálních počítačů s Windows a Linux IaaS. [Další informace](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest).

### <a name="work-with-the-azure-security-center"></a>Práce se službou Azure Security Center

Společnost Contoso potřebuje rychlý přehled o stavu zabezpečení svého nového hybridního cloudu, konkrétně úloh Azure. Proto se společnost Contoso rozhodla implementovat Azure Security Center. Začala při tom následujícími funkcemi:

- Centralizovaná správa zásad
- Průběžné hodnocení
- Užitečná doporučení

#### <a name="centralize-policy-management"></a>Centralizace správy zásad

Společnost Contoso dokáže díky centrální správě zásad zabezpečení v rámci celého prostředí zajistit soulad s požadavky zabezpečení. Může jednoduše a rychle implementovat zásadu, která bude platit pro všechny prostředky Azure.

![Zásady zabezpečení](./media/contoso-migration-infrastructure/security-policy.png)

#### <a name="assess-and-action"></a>Posouzení a akce

Společnost Contoso využije funkci nepřetržitého posuzování zabezpečení, která monitoruje zabezpečení počítačů, sítí, úložiště, dat a aplikací a snaží se odhalit možné problémy se zabezpečením.

- Security Center bude analyzovat stav zabezpečení výpočetních prostředků, infrastruktury a datových zdrojů společnosti Contoso a aplikací a služeb Azure.
- Nepřetržité posuzování pomáhá provoznímu týmu společnosti Contoso zjišťovat potenciální problémy se zabezpečením, jako jsou systémy s chybějícími aktualizacemi zabezpečení nebo nechráněné síťové porty.
- Konkrétně se společnost Contoso soustředí na to, aby byly chráněné všechny virtuální počítače. Za tím účelem Security Center kontroluje stav virtuálních počítačů a vydává užitečná doporučení s různými prioritami, která pomáhají napravit ohrožení zabezpečení dřív, než je někdo zneužije.

![Monitorování](./media/contoso-migration-infrastructure/monitoring.png)

### <a name="work-with-nsgs"></a>Práce se skupinami zabezpečení sítě

Společnost Contoso může pomocí skupin zabezpečení sítě omezit síťový provoz směřující do prostředků ve virtuální síti.

- Skupina zabezpečení sítě obsahuje seznam pravidel zabezpečení, která povolují nebo odepírají příchozí nebo odchozí síťový provoz v závislosti na zdrojové nebo cílové IP adrese, portu a protokolu.
- Při použití pravidel na podsíť se pravidla zabezpečení použijí na všechny prostředky v této podsíti. To se kromě síťových rozhraní týká i instancí služeb Azure nasazených v dané podsíti.
- Skupiny zabezpečení aplikace (ASG) umožňují konfigurovat zabezpečení sítě jako přirozené rozšíření struktury aplikace. Můžete seskupovat virtuální počítače a na základě těchto skupin definovat zásady zabezpečení sítě.
  - Díky skupinám zabezpečení aplikace může společnost Contoso opakovaně uplatňovat zásady zabezpečení v požadovaném měřítku, bez potřeby ruční údržby explicitních IP adres. O složitost explicitních IP adres a několika skupin pravidel se stará platforma a vy se tak můžete zaměřit na obchodní logiku.
  - Skupinu zabezpečení aplikace může společnost Contoso zadat jako zdroj a cíl v pravidlu zabezpečení. Po definování zásady zabezpečení může společnost Contoso vytvořit virtuální počítače a přiřadit jejich síťové karty k určité skupině.

Contoso bude implementovat kombinaci skupin zabezpečení sítě a skupin zabezpečení aplikace. Správa skupin zabezpečení sítě dělá společnosti Contoso starosti. Společnost se taky obává nadměrného využívání skupin zabezpečení sítě a toho, že se tím zkomplikuje práce provozního týmu. Provede to takto:

- Veškerý provoz směřující do všech podsítí a z nich (sever/jih) se bude řídit pravidlem skupin zabezpečení sítě, s výjimkou podsítí GatewaySubnets v centrálních sítích.
- Všechny brány firewall nebo řadiče domény budou chráněné jak skupinami zabezpečení sítě podsítí, tak skupinami zabezpečení sítě síťových karet.
- Skupiny zabezpečení aplikace se budou používat u všech produkčních aplikací.

Společnost Contoso vytvořila model, který znázorňuje způsob správy aplikací.

![Zabezpečení](./media/contoso-migration-infrastructure/asg.png)

Skupiny zabezpečení sítě přidružené ke skupinám zabezpečení aplikace budou mít nakonfigurované nejnižší oprávnění, aby mohly z jedné části sítě do cíle putovat jenom povolené pakety.

**Akce** | **Název** | **Zdroj** | **Cíl** | **Port**
--- | --- | --- | --- | ---
Povolit | AllowInternetToFE | VNET-HUB-EUS1/IB-TrustZone | APP1-FE 80, 443
Povolit | AllowWebToApp | APP1-FE | APP1-APP | 80, 443
Povolit | AllowAppToDB | APP1-APP | APP1-DB | 1433
Odepřít | DenyAllInbound | Vše | Vše | Vše

### <a name="encrypt-data"></a>Šifrování dat

Azure Disk Encryption taky umožňuje integraci se službou Azure Key Vault a pomáhá řídit a spravovat klíče a tajné kódy pro šifrování disků v předplatném služby Key Vault. Zajišťuje tím šifrování všech dat na discích virtuálních počítačů, která jsou uložená v neaktivním stavu ve službě Azure Storage.

- Společnost Contoso stanovila, které konkrétní virtuální počítače potřebují šifrování.
- Společnost Contoso použije šifrování na virtuální počítače s daty zákazníků, důvěrnými daty nebo osobními údaji.

## <a name="conclusion"></a>Závěr

V tomto článku společnost Contoso vytvořila infrastrukturu Azure a zásady pro předplatné Azure, hybridní identitu, zotavení po havárii, sítě, zásady správného řízení a zabezpečení.

Pro migraci do cloudu se nevyžaduje každý krok, který jste udělali. V tomto případě společnost Contoso naplánovala síťovou infrastrukturu, která by mohla zpracovávat všechny typy migrace, pokud jsou zabezpečené, odolné a škálovatelné.

V rámci této infrastruktury je contoso připravena přejít na migraci a vyzkoušet migraci.

## <a name="next-steps"></a>Další kroky

Po vytvoření infrastruktury Azure je společnost Contoso připravená začít s migrací úloh do cloudu. V části s [přehledem vzorů a příkladů migrace](./contoso-migration-overview.md#windows-server-workloads) najdete řadu scénářů, které využívají jako cíl migrace tuto ukázkovou infrastrukturu.
