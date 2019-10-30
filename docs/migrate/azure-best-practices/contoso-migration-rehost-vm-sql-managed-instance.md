---
title: Změna hostitele místní aplikace migrací na virtuální počítače Azure a spravovanou instanci Azure SQL Database
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak společnost Contoso s využitím spravované instance Azure SQL Database provádí změnu hostitele místní aplikace na virtuální počítače Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 574fa1ede2d7ddeb0fe41f05c8519e9b16ba6c51
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058501"
---
# <a name="rehost-an-on-premises-app-on-an-azure-vm-and-sql-database-managed-instance"></a>Změna hostitele místní aplikace na virtuální počítač Azure a spravovanou instanci Azure SQL Database

Tento článek ukazuje, jak fiktivní společnost Contoso s využitím služby Azure Site Recovery migruje dvouúrovňovou front-endovou aplikaci Windows .NET, která běží na virtuálních počítačích VMware, na virtuální počítač Azure. Také ukazuje, jak společnost Contoso migruje databázi aplikace na spravovanou instanci Azure SQL Database.

> [!NOTE]
> Spravovaná instance Azure SQL Database je v současné době ve verzi Preview.

Aplikace SmartHotel360 použitá v tomto příkladu je k dispozici jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT ve společnosti Contoso úzce spolupracoval s obchodními partnery společnosti, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Společnost Contoso se rozšiřuje. Kvůli tomu se zvýšil tlak na místní systémy a infrastrukturu společnosti.
- **Zvýšení efektivity.** Společnost Contoso se potřebuje zbavit zbytečných postupů a zjednodušit procesy pro vývojáře i uživatele. Potřebuje IT k tomu, aby neztrácela čas ani peníze, byla rychlá a dokázala rychleji reagovat na požadavky zákazníků.
- **Zvýšení agility.** IT ve společnosti Contoso musí pohotověji reagovat na potřeby firmy. K zajištění úspěchu společnosti v globální ekonomice je nutné, aby IT dokázalo rychleji reagovat na změny na trhu. IT ve společnosti Contoso nesmí stát v cestě a nesmí se stát obchodní překážkou.
- **Škálování** Společnost Contoso se úspěšně rozšiřuje a její IT musí poskytovat systémy, které jsou schopné rozvíjet se stejným tempem.

## <a name="migration-goals"></a>Cíle migrace

Tým pro přechod společnosti Contoso na cloud identifikoval cíle této migrace. Společnost pomocí cílů migrace určí nejlepší metodu migrace.

- Po migraci by aplikace v Azure měla mít stejné možnosti z hlediska výkonu jako současná aplikace v místním prostředí VMware společnosti Contoso. Přesun do cloudu neznamená, že je výkon aplikace méně důležitý.
- Společnost Contoso nechce investovat do aplikace. Aplikace je pro firmu klíčově důležitá, ale společnost Contoso ji chce jen ve stávající podobě přesunout do cloudu.
- Po migraci aplikace by se měly minimalizovat úlohy správy databáze.
- Společnost Contoso nechce pro tuto aplikaci použít službu Azure SQL Database. Hledá proto alternativy.

## <a name="solution-design"></a>Návrh řešení

Po vytyčení cílů a požadavků společnost Contoso navrhne a zkontroluje řešení nasazení a identifikuje proces migrace včetně služeb Azure, které k migraci využije.

### <a name="current-architecture"></a>Současná architektura

- Společnost Contoso má jedno hlavní datacentrum (**contoso-datacenter**). Toto datacentrum se nachází v New Yorku na východě USA.
- V rámci USA má společnost Contoso ještě tři další místní pobočky.
- Hlavní datacentrum je připojené k internetu přes optické připojení Metro Ethernet (500 Mb/s).
- Každá pobočka je místně připojená k internetu přes podnikové přípojky s tunely VPN IPSec, které vedou zpátky do hlavního datacentra. Díky tomuto nastavení může být celá síť společnosti Contoso trvale připojená a má optimální připojení k internetu.
- Hlavní datové centrum je plně virtualizované prostřednictvím VMware. Společnost Contoso má dva hostitele virtualizace ESXi 6.5, které spravuje vCenter Server 6.5.
- Společnost Contoso ke správě identit používá Active Directory. Společnost Contoso využívá servery DNS v interní síti.
- Společnost Contoso má místní řadič domény (**contosodc1**).
- Řadiče domény běží na virtuálních počítačích VMware. Řadiče domény v místních pobočkách běží na fyzických serverech.
- Aplikace SmartHotel360 obsahuje úrovně rozdělené mezi dva virtuální počítače (**WEBVM** a **SQLVM**), které se nacházejí na hostiteli VMware ESXi verze 6.5 (**contosohost1.contoso.com**).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) provozovaný na virtuálním počítači.

![Současná architektura společnosti Contoso](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Navrhovaná architektura

V tomto scénáři chce společnost Contoso migrovat svou místní dvouúrovňovou cestovní aplikaci následujícím způsobem:

- Databázi aplikace (**SmartHotelDB**) chce migrovat na spravovanou instanci Azure SQL Database.
- Front-endový virtuální počítač **WEBVM** chce migrovat na virtuální počítač Azure.
- Po dokončení migrace se místní virtuální počítače v datacentru Contoso vyřadí z provozu.

![Architektura scénáře](media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Aspekty týkající se databáze

Při návrhu řešení společnost Contoso provedla porovnání funkcí mezi službou Azure SQL Database a spravovanou instancí SQL Serveru. Následující aspekty ji přiměly rozhodnout se pro spravovanou instanci.

- Cílem spravované instance je zajistit téměř 100% kompatibilitu s nejnovější verzí místního SQL Serveru. Microsoft doporučuje spravovanou instanci zákazníkům, kteří provozují SQL Server v místním prostředí nebo na virtuálních počítačích IaaS a chtějí migrovat své aplikace na plně spravovanou službu s minimálními změnami návrhu.
- Společnost Contoso plánuje migrovat velký počet aplikací z místního prostředí na IaaS. Řadu z nich poskytují nezávislí výrobci softwaru. Společnost Contoso si uvědomuje, že oproti použití služby SQL Database, která nemusí být podporovaná, pomůže použití spravované instance zajistit pro tyto aplikace kompatibilitu databáze.
- Společnost Contoso může jednoduše provést migraci metodou „lift and shift“ na spravovanou instanci s využitím plně automatizované služby Azure Database Migration Service. Po implementaci této služby ji společnost Contoso bude moct opakovaně používat k budoucím migracím databází.
- Spravovaná instance SQL podporuje agenta SQL Serveru, což je pro aplikaci SmartHotel360 zcela zásadní. Společnost Contoso potřebuje tuto kompatibilitu, jinak by musela změnit návrh plánů údržby, které aplikace potřebuje.
- Prostřednictvím programu Software Assurance může společnost Contoso vyměnit ve spravované instanci SQL Database stávající licence za snížené sazby, a to pomocí programu Zvýhodněné hybridní využití Azure pro SQL Server. Společnost Contoso díky tomu může ušetřit až 30 % na spravované instanci.
- Spravovaná instance SQL je plně obsažená ve virtuální síti, takže poskytuje větší izolaci a zabezpečení pro data společnosti Contoso. Společnost Contoso může získat výhody veřejného cloudu při současné izolaci prostředí od veřejného internetu.
- Spravovaná instance podporuje řadu funkcí zabezpečení, včetně funkce Always Encrypted, dynamického maskování dat, zabezpečení na úrovni řádků a detekce hrozeb.

### <a name="solution-review"></a>Revize řešení

Společnost Contoso vyhodnotí vytvořený návrh sestavením seznamu výhod a nevýhod.

<!-- markdownlint-disable MD033 -->

**Aspekty** | **Podrobnosti**
--- | ---
**Výhody** | Virtuální počítač WEBVM se přesune do Azure beze změn, takže jeho migrace bude snadná.<br/><br/> Spravovaná instance SQL podporuje technické požadavky a cíle společnosti Contoso.<br/><br/> Spravovaná instance zajistí 100% kompatibilitu se současným nasazením při přesunu společnosti z SQL Serveru 2008 R2.<br/><br/> Společnost může využít své investice do Software Assurance a využít Zvýhodněné hybridní využití Azure pro SQL Server i Windows Server.<br/><br/> Službu Azure Database Migration Service může společnost opakovaně používat k dalším budoucím migracím.<br/><br/> Spravovaná instance SQL má integrovanou odolnost proti chybám, kterou společnost Contoso nemusí konfigurovat. Tím se zajistí, že datová vrstva už nebude jediným bodem převzetí služeb při selhání.
**Nevýhody** | Na virtuálním počítači WEBVM běží Windows Server 2008 R2. Přestože Azure tento operační systém podporuje, už se nejedná o podporovanou platformu. [Další informace](https://support.microsoft.com/help/956893).<br/><br/> Když služby zajišťuje pouze virtuální počítač WEBVM, webová vrstva zůstává jediným bodem převzetí služeb při selhání.<br/><br/> Společnost Contoso bude muset dál podporovat webovou vrstvu aplikace jako virtuální počítač, místo aby ji přesunula do spravované služby jako Azure App Service.<br/><br/> V případě datové vrstvy nemusí být spravovaná instance nejlepším řešením, pokud chce společnost Contoso přizpůsobit operační systém nebo databázový server nebo pokud chce společně s SQL Serverem používat aplikace třetích stran. Tuto flexibilitu může zajistit provoz SQL Serveru na virtuálním počítači IaaS.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migrace

Společnost Contoso provede migraci webové a datové vrstvy své aplikace SmartHotel360 do Azure pomocí následujícího postupu:

1. Společnost Contoso už má zřízenou svou infrastrukturu Azure, takže jí v tomto případě stačí přidat několik konkrétních komponent Azure.
2. Datová vrstva se bude migrovat s využitím služby Azure Database Migration Service. Tato služba se připojí k místnímu virtuálnímu počítači s SQL Serverem přes připojení site-to-site VPN mezi datacentrem společnosti Contoso a Azure. Pak služba provede migraci databáze.
3. Webová vrstva se bude migrovat metodou „lift and shift“ s využitím služby Site Recovery. Tento proces zahrnuje přípravu místního prostředí VMware, nastavení a povolení replikace a migraci virtuálních počítačů prostřednictvím převzetí jejich služeb při selhání do Azure.

     ![Architektura migrace](media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Služby Azure

Služba | Popis | Náklady
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Služba Azure Database Migration Service umožňuje bezproblémovou migraci z více databázových zdrojů na datové platformy Azure s minimální dobou vyřazení z provozu. | Informace o [podporovaných oblastech](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) a [cenách služby Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration)
[Spravovaná instance Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Spravovaná instance je spravovaná databázová služba, která představuje plně spravovanou instanci SQL Serveru v cloudu Azure. Využívá stejný kód jako nejnovější verze databázového stroje SQL Serveru a nabízí nejnovější funkce, vylepšení výkonu a opravy zabezpečení. | Za používání spravované instance SQL Database v Azure se účtují poplatky podle kapacity. Další informace o [cenách spravované instance](https://azure.microsoft.com/pricing/details/sql-database/managed)
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Služba Site Recovery orchestruje a spravuje migraci a zotavení po havárii pro virtuální počítače Azure a místní virtuální počítače a fyzické servery. | Během replikace do Azure se účtují poplatky za Azure Storage. Vytvoří se virtuální počítače Azure a při převzetí služeb při selhání se za ně účtují poplatky. Další informace o [poplatcích a cenách za Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

## <a name="prerequisites"></a>Předpoklady

Společnost Contoso a další uživatelé musí v tomto scénáři splňovat následující požadavky:

<!-- markdownlint-disable MD033 -->

Požadavky | Podrobnosti
--- | ---
**Registrace spravované instance verze Preview** | Musíte mít zaregistrovanou omezenou verzi Public Preview spravované instance SQL Database. K [registraci](https://portal.azure.com#create/Microsoft.SQLManagedInstance) potřebujete předplatné Azure. Dokončení registrace může trvat několik dnů, takže se nezapomeňte zaregistrovat před tím, než začnete nasazovat tento scénář.
**Předplatné Azure** | Při vyhodnocování v prvním článku této série už byste měli mít vytvořené předplatné. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste jeho správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.<br/><br/> Pokud potřebujete podrobnější oprávnění, přečtěte si téma [Správa přístupu ke službě Site Recovery s využitím řízení přístupu na základě role](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura Azure** | Contoso nastaví svoji infrastrukturu Azure podle popisu v článku [Infrastruktura Azure pro migraci](./contoso-migration-infrastructure.md).
**Site Recovery (místní)** | Vaše místní instance vCenter Serveru by měly používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Hostitel ESXi by měl používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Na hostiteli ESXi by měl být spuštěný jeden nebo více virtuálních počítačů VMware.<br/><br/> Virtuální počítače musí splňovat [požadavky Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Podporované konfigurace [sítě](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) a [úložiště](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage)
**Database Migration Service** | Pro službu Azure Database Migration Service potřebujete [kompatibilní místní zařízení VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).<br/><br/> Místní zařízení VPN musíte mít možnost konfigurovat. Zařízení musí mít externí veřejnou IPv4 adresu. Tato adresa nesmí být umístěná za zařízením NAT.<br/><br/> Ujistěte se, že máte přístup k místní databázi SQL Serveru.<br/><br/> Brána Windows Firewall by měla mít přístup ke zdrojovému databázovému stroji. Informace o [konfiguraci brány Windows Firewall pro přístup k databázovému stroji](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access)<br/><br/> Pokud je před databázovým počítačem brána firewall, přidejte pravidla, která povolí přístup k databázi a souborům přes port SMB 445.<br/><br/> Přihlašovací údaje použité pro připojení ke zdrojové instanci SQL Serveru a cílové spravované instanci musí být členy role serveru sysadmin.<br/><br/> V místní databázi potřebujete sdílenou síťovou složku, kterou může služba Azure Database Migration Service použít k zálohování zdrojové databáze.<br/><br/> Ujistěte se, že účet služby, ve kterém je spuštěná zdrojová instance SQL Serveru, má pro tuto sdílenou síťovou složku oprávnění k zápisu.<br/><br/> Poznamenejte si uživatele Windows a jeho heslo s oprávněním Úplné řízení ke sdílené síťové složce. Služba Azure Database Migration Service zosobní tyto přihlašovací údaje uživatele za účelem nahrání záložních souborů do kontejneru služby Azure Storage.<br/><br/> V rámci instalace SQL Serveru Express se ve výchozím nastavení protokol TCP/IP nastaví jako **zakázaný**. Nezapomeňte ho povolit.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Tady je plán společnosti Contoso pro nastavení nasazení:

> [!div class="checklist"]
>
> - **Krok 1: nastavení spravované instance SQL Database.** Společnost Contoso potřebuje existující spravovanou instanci, do které se bude migrovat místní databáze SQL Serveru.
> - **Krok 2: Příprava Azure Database Migration Service.** Společnost Contoso musí zaregistrovat zprostředkovatele migrace databáze, vytvořit instanci a pak vytvořit projekt služby Azure Database Migration Service. Kromě toho musí společnost Contoso nastavit identifikátor URI sdíleného přístupového podpisu (SAS) pro službu Azure Database Migration Service. Identifikátor URI SAS poskytuje delegovaný přístup k prostředkům v účtu úložiště společnosti Contoso, aby mohla udělovat omezená oprávnění k objektům úložiště. Společnost Contoso nastaví identifikátor URI SAS, aby služba Azure Database Migration Service mohla přistupovat ke kontejneru účtu úložiště, do kterého služba nahrává záložní soubory SQL Serveru.
> - **Krok 3: Příprava Azure na Site Recovery.** Společnost Contoso musí vytvořit účet úložiště, který bude uchovávat replikovaná data pro Site Recovery. Kromě toho musí vytvořit také trezor služby Azure Recovery Services.
> - **Krok 4: Příprava místního VMware pro Site Recovery.** Společnost Contoso připraví účty pro zjišťování virtuálních počítačů a instalaci agenta, aby se po převzetí služeb při selhání bylo možné připojit k virtuálním počítačům Azure.
> - **Krok 5: replikace virtuálních počítačů** Společnost Contoso nastaví replikaci tak, že nakonfiguruje zdrojové a cílové prostředí služby Site Recovery, nastaví zásady replikace a zahájí replikaci virtuálních počítačů do služby Azure Storage.
> - **Krok 6: migrace databáze pomocí Azure Database Migration Service.** Společnost Contoso provede migraci databáze.
> - **Krok 7: migrace virtuálních počítačů pomocí Site Recovery.** Společnost Contoso spustí testovací převzetí služeb při selhání, aby se ujistila, že všechno funguje. Pak společnost Contoso provede migraci virtuálních počítačů do Azure spuštěním úplného převzetí služeb při selhání.

## <a name="step-1-prepare-a-sql-database-managed-instance"></a>Krok 1: Příprava spravované instance SQL Database

Společnost Contoso k nastavení spravované instance Azure SQL Database potřebuje podsíť, která splňuje následující požadavky:

- Podsíť musí být vyhrazená. Musí být prázdná a nesmí obsahovat žádnou jinou cloudovou službu. Podsíť nesmí být podsítí brány.
- Po vytvoření spravované instance by společnost Contoso neměla do podsítě přidávat žádné prostředky.
- K podsíti nesmí být přidružená skupina zabezpečení sítě.
- Podsíť musí mít tabulku směrování definovanou uživatelem. Jediná přiřazená trasa by měla být internetová trasa dalšího segmentu směrování 0.0.0.0/0.
- Volitelné vlastní DNS: Pokud je ve virtuální síti Azure zadaný vlastní DNS, musí se do seznamu přidat IP adresa rekurzivního překladače Azure (například 168.63.129.16). Informace o [konfiguraci vlastního serveru DNS pro spravovanou instanci](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns)
- K podsíti nesmí být přidružený žádný koncový bod služby (úložiště ani SQL). Ve virtuální síti by měly být zakázané koncové body služeb.
- Podsíť musí mít minimálně 16 IP adres. Informace o [nastavení velikosti podsítě spravované instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration)
- V hybridním prostředí společnosti Contoso se vyžaduje vlastní nastavení DNS. Společnost nakonfiguruje nastavení DNS tak, aby se používal jeden nebo několik serverů Azure DNS společnosti. Další informace o [přizpůsobení DNS](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns)

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Nastavení virtuální sítě pro spravovanou instanci

Správci společnosti Contoso nastaví virtuální síť následovně:

1. V primární oblasti Východní USA 2 vytvoří novou virtuální síť (**VNET-SQLMI-EU2**). Tato virtuální síť se přidá do skupiny prostředků **ContosoNetworkingRG**.
2. Přiřadí jí adresní prostor 10.235.0.0/24. Zajistí, aby se tento rozsah nepřekrýval s žádnou jinou sítí v rámci podniku.
3. Do této sítě přidají dvě podsítě:
    - **SQLMI-DS-EUS2** (10.235.0.0.25)
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Tato podsíť se používá k připojení adresáře ke spravované instanci.

      ![Spravovaná instance – Vytvoření virtuální sítě](media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Po nasazení virtuální sítě a podsítí následujícím způsobem vytvoří partnerské vztahy sítí:

    - Vytvoří partnerský vztah mezi sítěmi **VNET-SQLMI-EUS2** a **VNET-HUB-EUS2** (centrální virtuální síť pro oblast Východní USA 2).
    - Vytvoří partnerský vztah mezi sítěmi **VNET-SQLMI-EUS2** a **VNET-PROD-EUS2** (produkční síť).

      ![Partnerské vztahy sítí](media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Nakonfigurují vlastní nastavení DNS. DNS odkazuje nejprve na řadiče domény Azure společnosti Contoso. Azure DNS je sekundární. Umístění řadičů domény Azure společnosti Contoso je následující:

    - V podsíti **PROD-DC-EUS2** v produkční síti v oblasti Východní USA 2 (**VNET-PROD-EUS2**)
    - **CONTOSODC3** adresa: 10.245.42.4
    - **CONTOSODC4** adresa: 10.245.42.5
    - Překladač Azure DNS: 168.63.129.16

      ![Síťové servery DNS](media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Potřebujete další pomoc?**

- Přehled [spravované instance SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
- Informace o [vytvoření virtuální sítě pro spravovanou instanci SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration)
- Informace o [nastavení partnerského vztahu](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering)
- Informace o [aktualizaci nastavení DNS služby Azure Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started-dns)

### <a name="set-up-routing"></a>Nastavení směrování

Spravovaná instance je umístěná v privátní virtuální síti. Společnost Contoso potřebuje tabulku směrování, aby mohla virtuální síť komunikovat se službou pro správu Azure. Pokud virtuální síť nemůže komunikovat se službou, která ji spravuje, stane se nedostupnou.

Společnost Contoso zvažuje tyto faktory:

- Tabulka směrování obsahuje sadu pravidel (tras), která určují, jak se ve virtuální síti mají směrovat pakety odesílané ze spravované instance.
- Ke směrovací tabulce jsou přidružené podsítě, ve kterých jsou nasazené spravované instance. Všechny pakety, které opustí podsíť, se zpracovávají v závislosti na přidružené tabulce směrování.
- K podsíti může být přidružená pouze jedna tabulka směrování.
- Na vytváření tabulek směrování v Microsoft Azure se nevztahují žádné další poplatky.

 Správci společnosti Contoso při nastavování směrování postupují následovně:

1. Ve skupině prostředků **ContosoNetworkingRG** vytvoří tabulku směrování definovanou uživatelem.

    ![Tabulka směrování](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Kvůli splnění požadavků na spravovanou instanci po nasazení tabulky směrování (**MIRouteTable**) přidají trasu s předponou adresy 0.0.0.0/0. Možnost **Typ dalšího segmentu směrování** nastaví na **Internet**.

    ![Předpona tabulky směrování](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. K tabulce směrování přidruží podsíť **SQLMI-DB-EUS2** (v síti **VNET-SQLMI-EUS2**).

    ![Podsíť tabulky směrování](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Potřebujete další pomoc?**

Informace o [nastavení tras pro spravovanou instanci](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal)

### <a name="create-a-managed-instance"></a>Vytvoření Managed Instance

Teď můžou správci společnosti Contoso zřídit spravovanou instanci SQL Database:

1. Vzhledem k tomu, že spravovaná instance bude obsluhovat podnikovou aplikaci, nasadí ji v primární oblasti společnosti Východní USA 2. Spravovanou instanci přidají do skupiny prostředků **ContosoRG**.
2. Pro instanci vyberou cenovou úroveň, velikost výpočetních prostředků a úložiště. Další informace o [cenách spravované instance](https://azure.microsoft.com/pricing/details/sql-database/managed)

    ![Managed Instance](media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Po nasazení spravované instance se ve skupině prostředků **ContosoRG** zobrazí dva nové prostředky:

    - Virtuální cluster, pokud má společnost Contoso více spravovaných instancí
    - Spravovaná instance databáze SQL Serveru

      ![Managed Instance](media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Potřebujete další pomoc?**

Informace o [zřízení spravované instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal)

## <a name="step-2-prepare-the-azure-database-migration-service"></a>Krok 2: Příprava Azure Database Migration Service

Správci společnosti Contoso musí při přípravě služby Azure Database Migration Service udělat několik věcí:

- Zaregistrovat poskytovatele služby Azure Database Migration Service v Azure.
- Poskytnout službě Azure Database Migration Service přístup ke službě Azure Storage, aby do ní mohla nahrát záložní soubory sloužící k migraci databáze. Přístup ke službě Azure Storage zajistí vytvořením kontejneru úložiště objektů blob v Azure. Pro kontejner úložiště objektů blob vygenerují identifikátor URI SAS.
- Vytvořit projekt služby Azure Database Migration Service.

Pak provedou následující kroky:

1. Zaregistrují ve svém předplatném zprostředkovatele migrace databáze.
    ![Database Migration Service – Registrace](media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

2. Vytvoří kontejner úložiště objektů blob. Společnost Contoso vygeneruje identifikátor URI SAS, aby k němu měla přístup služba Azure Database Migration Service.

    ![Database Migration Service – Generování identifikátoru URI SAS](media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

3. Vytvoří instanci služby Azure Database Migration Service.

    ![Database Migration Service – Vytvoření instance](media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

4. Instanci služby Azure Database Migration Service umístí do podsítě **PROD-DC-EUS2** virtuální sítě **VNET-PROD-DC-EUS2**.
    - Služba Azure Database Migration Service je v tomto umístění, protože musí být ve virtuální síti, která má přístup k místnímu virtuálnímu počítači s SQL Serverem přes bránu VPN.
    - Virtuální síť **VNET-PROD-EUS2** je v partnerském vztahu s virtuální sítí **VNET-HUB-EUS2** a může využívat vzdálené brány. Možnost **Používat vzdálené brány** zajišťuje, aby služba Azure Database Migration Service mohla komunikovat podle potřeby.

        ![Database Migration Service – Konfigurace sítě](media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**Potřebujete další pomoc?**

- Informace o [nastavení služby Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal)
- Informace o [vytvoření a používání SAS](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2)

## <a name="step-3-prepare-azure-for-the-site-recovery-service"></a>Krok 3: Příprava Azure na službu Site Recovery

Společnost Contoso k nastavení služby Site Recovery pro migraci virtuálního počítače webové vrstvy (**WEBMV**) potřebuje několik elementů Azure:

- Virtuální síť, která bude obsahovat prostředky po převzetí služeb při selhání
- Účet úložiště, ve kterém se budou uchovávat replikovaná data
- Trezor služby Recovery Services v Azure

Správci společnosti Contoso nastaví Site Recovery následujícím způsobem:

1. Vzhledem k tomu, že je virtuální počítač webovým front-endem aplikace SmartHotel360, společnost Contoso provede převzetí služeb při selhání do své stávající produkční sítě (**VNET-PROD-EUS2**) a podsítě (**PROD-FE-EUS2**). Síť a podsíť se nacházejí v primární oblasti Východní USA 2. Společnost Contoso tuto síť nastavila při [nasazování infrastruktury Azure](./contoso-migration-infrastructure.md).
2. Vytvoří účet úložiště (**contosovmsacc20180528**). Společnost Contoso použije účet pro obecné účely. Společnost Contoso vybere úložiště úrovně Standard a replikaci do místně redundantního úložiště.

    ![Site Recovery – Vytvoření účtu úložiště](media/contoso-migration-rehost-vm-sql-managed-instance/asr-storage.png)

3. Po vytvoření sítě a účtu úložiště vytvoří trezor (**ContosoMigrationVault**). Společnost Contoso umístí trezor do skupiny prostředků **ContosoFailoverRG** v primární oblasti Východní USA 2.

    ![Recovery Services – Vytvoření trezoru](media/contoso-migration-rehost-vm-sql-managed-instance/asr-vault.png)

**Potřebujete další pomoc?**

Informace o [nastavení Azure pro Site Recovery](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure)

## <a name="step-4-prepare-on-premises-vmware-for-site-recovery"></a>Krok 4: Příprava místního VMware pro Site Recovery

Správci společnosti Contoso musí při přípravě prostředí VMware pro Site Recovery provést tyto úlohy:

- Připravit účet v instanci vCenter Serveru nebo na hostiteli vSphere ESXi. Tento účet zautomatizuje zjišťování virtuálních počítačů.
- Připravit účet, který umožní automatickou instalaci služby Mobility Service na virtuálních počítačích VMware, které chce společnost Contoso replikovat.
- Připravit místní virtuální počítače na připojení k virtuálním počítačům Azure při jejich vytvoření po převzetí služeb při selhání.

### <a name="prepare-an-account-for-automatic-discovery"></a>Příprava účtu pro automatické zjišťování

Site Recovery potřebuje přístup k serverům VMware z těchto důvodů:

- Automatické zjišťování virtuálních počítačů. Vyžaduje se minimálně účet jen pro čtení.
- Orchestrace replikace, převzetí služeb při selhání a navrácení služeb po obnovení. Společnost Contoso potřebuje účet, který může spouštět operace, jako jsou vytváření a odebírání disků a zapínání virtuálních počítačů.

Správci společnosti Contoso tento účet nastaví pomocí těchto úloh:

1. Vytvoří roli na úrovni vCenter.
2. Přiřadí této roli požadovaná oprávnění.

**Potřebujete další pomoc?**

Informace o [vytvoření a přiřazení role pro automatické zjišťování](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery)

### <a name="prepare-an-account-for-mobility-service-installation"></a>Příprava účtu pro instalaci služby Mobility Service

Na virtuálním počítači, který chce společnost Contoso replikovat, musí být nainstalovaná služba Mobility Service. Společnost Contoso v souvislosti se službou Mobility Service zvažuje tyto faktory:

- Když společnost Contoso povolí replikaci virtuálního počítače, Site Recovery může automaticky provést nabízenou instalaci této komponenty.
- U automatické nabízené instalace musí společnost Contoso připravit účet, který služba Site Recovery použije k získání přístupu k virtuálnímu počítači.
- Tento účet se určí při konfiguraci replikace v konzole Azure.
- Společnost Contoso musí mít účet domény nebo místní účet s oprávněními k instalaci na virtuální počítač.

**Potřebujete další pomoc?**

Informace o [vytvoření účtu pro nabízenou instalaci služby Mobility Service](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation)

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Příprava připojení k virtuálním počítačům Azure po převzetí služeb při selhání

Po převzetí služeb při selhání do Azure chce mít společnost Contoso možnost připojit se k replikovaným virtuálním počítačům v Azure. Aby bylo možné se připojit k replikovaným virtuálním počítačům v Azure, správci společnosti Contoso musí před migrací na místním virtuálním počítači provést několik úloh:

1. Aby byl možný přístup přes internet, před převzetím služeb při selhání povolí na místním virtuálním počítači protokol RDP. Ujistí se, že jsou přidaná pravidla TCP a UDP pro **Veřejný** profil a že v části **Brána Windows Firewall** > **Povolené aplikace** je pro všechny profily povolený protokol RDP.
2. Aby byl možný přístup přes síť site-to-site VPN společnosti Contoso, povolí na místním počítači protokol RDP. V části **Brána Windows Firewall** > **Povolené aplikace a funkce** povolí pro **doménové a privátní** sítě protokol RDP.
3. Nastaví zásadu SAN operačního systému místního virtuálního počítače na **OnlineAll**.

Před spuštěním převzetí služeb při selhání musí správci společnosti Contoso zkontrolovat také následující body:

- Při aktivaci převzetí služeb při selhání by na virtuálním počítači neměly být žádné čekající aktualizace Windows. Pokud na virtuálním počítači právě probíhají aktualizace Windows, uživatelé se k němu nemůžou přihlásit, dokud se aktualizace nedokončí.
- Po převzetí služeb při selhání by správci měli zkontrolovat **diagnostiku spuštění** a zobrazit si snímek obrazovky virtuálního počítače. Pokud nemůžou zobrazit diagnostiku spuštění, měli by zkontrolovat, že je virtuální počítač spuštěný, a pak si projít [tipy pro řešení potíží](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="step-5-replicate-the-on-premises-vms-to-azure"></a>Krok 5: replikace místních virtuálních počítačů do Azure

Před spuštěním migrace do Azure musí správci společnosti Contoso nastavit a povolit replikaci místního virtuálního počítače.

### <a name="set-a-replication-goal"></a>Určení cíle replikace

1. V trezoru pod názvem trezoru (**ContosoVMVault**) nastaví cíl replikace (**Začínáme** > **Site Recovery** > **Připravit infrastrukturu**).
2. Určí, že se počítače nacházejí v místním prostředí, že se jedná o virtuální počítače VMware a replikují se do Azure.

    ![Příprava infrastruktury – Cíl ochrany](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Potvrzení plánování nasazení

Aby mohli pokračovat, musí správci společnosti Contoso potvrdit, že dokončili plánování nasazení. Vyberou možnost **Ano, mám to hotové**. V tomto nasazení společnost Contoso migruje pouze jeden virtuální počítač, proto není potřeba nasazení plánovat.

### <a name="set-up-the-source-environment"></a>Nastavení zdrojového prostředí

Teď správci společnosti Contoso nakonfigurují zdrojové prostředí. Zdrojové prostředí nastaví tak, že si stáhnou šablonu OVF, pomocí které nasadí konfigurační server a jeho přidružené komponenty jako vysoce dostupný místní virtuální počítač VMware. Součásti na serveru zahrnují:

- Konfigurační server, který koordinuje komunikaci mezi místní infrastrukturou a Azure. Konfigurační server spravuje replikaci dat.
- Procesový server, který funguje jako replikační brána. Procesový server:
  - Přijímá data replikace.
  - Optimalizuje data replikace s využitím ukládání do mezipaměti, komprese a šifrování.
  - Odesílá data replikace do služby Azure Storage.
- Procesový server také nainstaluje službu Mobility Service na virtuální počítače, které se budou replikovat. Procesový server provádí automatické zjišťování místních virtuálních počítačů VMware.
- Po vytvoření a spuštění virtuálního počítače konfiguračního serveru společnost Contoso zaregistruje server v trezoru.

Při nastavování zdrojového prostředí správci společnosti Contoso postupují následovně:

1. Z webu Azure Portal si stáhnou šablonu OVF (v části **Připravit infrastrukturu** > **Zdroj** > **Konfigurační server**).

    ![Přidání konfiguračního serveru](./media/contoso-migration-rehost-vm-sql-managed-instance/add-cs.png)

2. Importují šablonu do VMware, aby došlo k vytvoření a nasazení virtuálního počítače.

    ![Nasazení šablony OVF](./media/contoso-migration-rehost-vm-sql-managed-instance/vcenter-wizard.png)

3. Při prvním zapnutí virtuálního počítače se spustí prostředí instalace systému Windows Server 2016. Přijmou licenční smlouvu a zadají heslo správce.
4. Po dokončení instalace se přihlásí k virtuálnímu počítači jako správce. Při prvním přihlášení se automaticky spustí nástroj pro konfiguraci služby Azure Site Recovery.
5. V nástroji pro konfiguraci služby Site Recovery zadají název použitý k registraci konfiguračního serveru v trezoru.
6. Nástroj zkontroluje připojení virtuálního počítače k Azure. Po navázání připojení vyberou **Přihlásit se** a přihlásí se k předplatnému Azure. Přihlašovací údaje musí umožňovat přístup k trezoru, ve kterém je zaregistrovaný konfigurační server.

    ![Registrace konfiguračního serveru](./media/contoso-migration-rehost-vm-sql-managed-instance/config-server-register2.png)

7. Nástroj provede několik konfiguračních úloh a pak restartuje počítač. Znovu se přihlásí k počítači. Automaticky se spustí průvodce správou konfiguračního serveru.
8. V průvodci vyberou síťovou kartu pro příjem dat přenášených při replikaci. Po dokončení konfigurace není možné toto nastavení změnit.
9. Vyberou předplatné, skupinu prostředků a trezor služby Recovery Services, ve kterém se má konfigurační server zaregistrovat.

    ![Výběr trezoru služby Recovery Services](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz1.png)

10. Stáhnou a nainstalují MySQL Server a VMware PowerCLI. Pak ověří nastavení serveru.
11. Po ověření zadají plně kvalifikovaný název domény nebo IP adresu instance vCenter Serveru nebo hostitele vSphere. Ponechají výchozí port a zadají zobrazovaný název instance vCenter Serveru v Azure.
12. Určí dříve vytvořený účet, aby služba Site Recovery mohla automaticky zjišťovat virtuální počítače VMware, které jsou k dipozici pro replikaci.
13. Zadají přihlašovací údaje, aby se po povolení replikace automaticky nainstalovala služba Mobility Service. V případě počítačů s Windows je nutné, aby na nich měl tento účet oprávnění místního správce.

    ![Konfigurace vCenter Serveru](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz2.png)

14. Po dokončení registrace na webu Azure Portal znovu ověří, jestli je ve vybraném trezoru na stránce **Zdroj** uvedený konfigurační server a server VMware. Zjišťování může trvat 15 minut nebo i více.
15. Site Recovery se připojí k serverům VMware pomocí zadaného nastavení a vyhledá virtuální počítače.

### <a name="set-up-the-target"></a>Nastavení cíle

Teď správci společnosti Contoso nakonfigurují cílové prostředí replikace:

1. V části **Připravit infrastrukturu** > **Cíl** zvolí nastavení cíle.
2. Site Recovery zkontroluje, jestli je v zadaném cílovém umístění účet úložiště a síť.

### <a name="create-a-replication-policy"></a>Vytvoření zásady replikace

Po nastavení zdroje a cíle správci společnosti Contoso vytvoří zásadu replikace a přidruží ji ke konfiguračnímu serveru:

1. V části **Připravit infrastrukturu** > **Nastavení replikace** > **Zásada replikace** >  **Vytvořit a přidružit** vytvoří zásadu **ContosoMigrationPolicy**.
2. Použijí výchozí nastavení:
    - **Prahová hodnota cíle RPO:** Výchozí hodnota je 60 minut. Tato hodnota určuje, jak často se tvoří body obnovení. Když průběžná replikace překročí tento limit, vygeneruje se upozornění.
    - **Uchování bodu obnovení:** Výchozí hodnota je 24 hodin. Tato hodnota určuje délku intervalu uchovávání dat pro jednotlivé body obnovení. Replikované virtuální počítače můžete v rámci okna uchování obnovit do libovolného časového bodu.
    - **Frekvence snímků konzistentní vzhledem k aplikacím:** Výchozí hodnota je 1 hodina. Tato hodnota určuje četnost vytváření snímků konzistentních vzhledem k aplikacím.

    ![Zásada replikace – Vytvoření](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy.png)

3. Tato zásada se automaticky přidruží ke konfiguračnímu serveru.

    ![Zásada replikace – Přidružení](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy2.png)

**Potřebujete další pomoc?**

- Podrobný popis těchto kroků najdete v článku [Nastavení zotavení po havárii pro místní virtuální počítače VMware](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- K dispozici jsou také podrobné pokyny, které vám pomůžou [nastavit zdrojové prostředí](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [nasadit konfigurační server](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) a [nakonfigurovat nastavení replikace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).

### <a name="enable-replication"></a>Povolení replikace

Teď můžou správci společnosti Contoso zahájit replikaci virtuálního počítače WEBVM.

1. V části **Replikovat aplikaci** > **Zdroj** > **Replikovat** vyberou nastavení zdroje.
2. Určí, že chtějí povolit virtuální počítače, vyberou instanci vCenter Serveru a nastaví konfigurační server.

    ![Povolení replikace – Zdroj](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication1.png)

3. Určí nastavení cíle, včetně skupiny prostředků a sítě, ve kterých se bude nacházet virtuální počítač Azure po převzetí služeb při selhání. Určí účet úložiště, do kterého se budou ukládat replikovaná data.

    ![Povolení replikace – Cíl](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication2.png)

4. Pro replikaci vyberou virtuální počítač **WEBVM**. Po povolení replikace Site Recovery na všechny virtuální počítače nainstaluje službu Mobility Service.

    ![Povolení replikace – Výběr virtuálního počítače](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication3.png)

5. Zkontrolují, jestli je vybraná správná zásada replikace, a povolí replikaci virtuálního počítače **WEBVM**. V části **Úlohy** sledují průběh replikace. Po spuštění úlohy **Dokončit ochranu** je počítač připravený k převzetí služeb při selhání.

6. Na webu Azure Portal v části **Základní údaje** můžou zobrazit stav virtuálních počítačů replikovaných do Azure:

    ![Zobrazení infrastruktury](./media/contoso-migration-rehost-vm-sql-managed-instance/essentials.png)

**Potřebujete další pomoc?**

Podrobný popis těchto kroků najdete v článku [Povolení replikace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-6-migrate-the-database"></a>Krok 6: migrace databáze

Správci společnosti Contoso musí vytvořit projekt služby Azure Database Migration Service a pak migrovat databázi.

### <a name="create-an-azure-database-migration-service-project"></a>Vytvoření projektu služby Azure Database Migration Service

1. Vytvoří projekt služby Azure Database Migration Service. Jako typ zdrojového serveru vyberou **SQL Server** a jako cíl vyberou **Spravovaná instance Azure SQL Database**.

     ![Database Migration Service – Nový projekt migrace](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

2. Otevře se průvodce migrací.

### <a name="migrate-the-database"></a>Migrace databáze

1. V průvodci migrací určí zdrojový virtuální počítač, na kterém se nachází místní databáze. Zadají přihlašovací údaje pro přístup k databázi.

    ![Database Migration Service – Podrobnosti o zdroji](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

2. Vyberou databázi, která se má migrovat (**SmartHotel.Registration**):

    ![Database Migration Service – Výběr zdrojových databází](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-sourcedb.png)

3. Jako cíl zadají název spravované instance v Azure a zadají přihlašovací údaje pro přístup.

    ![Database Migration Service – Podrobnosti o cíli](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

4. V části **Nová aktivita** > **Spustit migraci** zadají nastavení pro spuštění migrace:
    - Přihlašovací údaje ke zdroji a k cíli
    - Databáze, která se má migrovat
    - Sdílená síťová složka vytvořená na místním virtuálním počítači. Azure Database Migration Service do této sdílené složky přenese zálohy zdroje.
        - Účet služby, který spouští zdrojovou instanci SQL Serveru, musí mít oprávnění k zápisu do této sdílené složky.
        - Musí se použít cesta ke sdílené složce s plně kvalifikovaným názvem domény.
    - Identifikátor URI SAS, který službě Azure Database Migration Service umožní přistup ke kontejneru účtu úložiště, do kterého služba nahrává záložní soubory pro migraci

        ![Database Migration Service – Konfigurace nastavení migrace](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-migration-settings.png)

5. Uloží nastavení migrace a pak spustí migraci.
6. V části **Přehled** monitorují stav migrace.

    ![Database Migration Service – Monitorování](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor1.png)

7. Po dokončení migrace ověří, jestli ve spravované instanci existují cílové databáze.

    ![Database Migration Service – Ověření migrace databáze](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor2.png)

## <a name="step-7-migrate-the-vm"></a>Krok 7: migrace virtuálního počítače

Správci společnosti Contoso spustí rychlé testovací převzetí služeb při selhání a pak provedou migraci virtuálního počítače.

### <a name="run-a-test-failover"></a>Spuštění testovacího převzetí služeb při selhání

Před migrací virtuálního počítače WEBVM testovací převzetí služeb při selhání pomůže zajistit, že vše funguje podle očekávání. Správci provedou následující kroky:

1. Spustí testovací převzetí služeb při selhání k nejnovějšímu dostupnému bodu v čase (**Nejnovější zpracovaný**).
2. Vyberou možnost **Před spuštěním převzetí služeb při selhání vypnout počítač**. Když je vybraná tato možnosti, Site Recovery se před aktivací převzetí služeb při selhání pokusí vypnout zdrojový virtuální počítač. Převzetí služeb při selhání bude pokračovat i v případě, že se vypnutí nepovede.
3. Spustí se testovací převzetí služeb při selhání: a. Spustí se kontrola předpokladů, která zjistí, zda jsou splněné všechny podmínky pro migraci.
    b. Převzetí služeb při selhání tato data zpracuje, aby se mohl vytvořit virtuální počítač Azure. Pokud je vybraný nejnovější bod obnovení, vytvoří se z těchto dat nový.
    c. Pomocí dat zpracovaných v předchozím kroku se vytvoří virtuální počítač Azure.
4. Po dokončení převzetí služeb při selhání se na webu Azure Portal objeví replika virtuálního počítače Azure. Ověří, že vše funguje správně: virtuální počítač má odpovídající velikost, je připojený ke správné síti a je spuštěný.
5. Po ověření testovacího převzetí služeb při selhání vyčistí převzetí služeb při selhání a zaznamenají případné poznámky.

### <a name="migrate-the-vm"></a>Migrace virtuálního počítače

1. Po ověření toho, jestli testovací převzetí služeb při selhání funguje podle očekávání, vytvoří správci společnosti Contoso plán obnovení pro migraci a přidají do něj virtuální počítač WEBVM:

     ![Vytvoření plánu obnovení – Výběr položek](./media/contoso-migration-rehost-vm-sql-managed-instance/recovery-plan.png)

2. V rámci plánu spustí převzetí služeb při selhání a vyberou nejnovější bod obnovení. Určí, že se má Site Recovery před aktivací převzetí služeb při selhání pokusit o vypnutí místního virtuálního počítače.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-vm-sql-managed-instance/failover1.png)

3. Po převzetí služeb při selhání ověří, jestli se virtuální počítač Azure zobrazuje na webu Azure Portal podle očekávání.

   ![Podrobnosti o plánu obnovení](./media/contoso-migration-rehost-vm-sql-managed-instance/failover2.png)

4. Po ověření dokončí migraci. Tím se ukončí proces migrace, zastaví se replikace virtuálního počítače a zastaví se fakturace služby Site Recovery pro virtuální počítač.

    ![Převzetí služeb při selhání – Dokončení migrace](./media/contoso-migration-rehost-vm-sql-managed-instance/failover3.png)

### <a name="update-the-connection-string"></a>Aktualizace připojovacího řetězce

V posledním kroku tohoto procesu migrace správci společnosti Contoso aktualizují v aplikaci připojovací řetězec tak, aby odkazoval na migrovanou databázi ve spravované instanci společnosti Contoso.

1. Na webu Azure Portal najdou připojovací řetězec výběrem možnosti **Nastavení** > **Připojovací řetězce**.

    ![Připojovací řetězce](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

2. Aktualizují řetězec s použitím uživatelského jména a hesla spravované instance SQL Database.
3. Po nakonfigurování řetězce nahradí aktuální připojovací řetězec v souboru web.config aplikace.
4. Po aktualizaci a uložení souboru restartují na virtuálním počítači WEBVM službu IIS spuštěním příkazu `IISRESET /RESTART` v okně příkazového řádku.
5. Po restartování služby IIS bude aplikace používat databázi ve spravované instanci SQL Database.
6. V tuto chvíli můžou vypnout místní počítač SQLVM. Migrace je hotová.

**Potřebujete další pomoc?**

- Informace o [spuštění testovacího převzetí služeb při selhání](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure)
- Informace o [vytvoření plánu obnovení](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans)
- Informace o [převzetí služeb při selhání do Azure](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover)

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace je aplikace SmartHotel360 spuštěná na virtuálním počítači Azure a databáze SmartHotel360 je dostupná ve spravované instanci Azure SQL Database.

Teď musí společnost Contoso provést následující úlohy čištění:

- Odebrat z inventáře vCenter Serveru počítač WEBVM
- Odebrat z inventáře vCenter Serveru počítač SQLVM
- Odebrat počítače WEBVM a SQLVM z místních úloh zálohování
- Aktualizovat interní dokumentaci tak, aby obsahovala nové umístění a IP adresu virtuálního počítače WEBVM
- Odebrat z interní dokumentace virtuální počítač SQLVM. Případně může společnost Contoso dokumentaci revidovat tak, aby obsahovala informaci o odstranění virtuálního počítače SQLVM z inventáře virtuálních počítačů.
- Zkontrolovat všechny prostředky, které komunikují s vyřazenými virtuálními počítači. Aktualizovat příslušná nastavení a dokumentaci tak, aby odrážely novou konfiguraci.

## <a name="review-the-deployment"></a>Revize nasazení

Teď, když má prostředky migrované do Azure, společnost Contoso potřebuje plně zprovoznit a zabezpečit novou infrastrukturu.

### <a name="security"></a>Zabezpečení

Bezpečnostní tým společnosti Contoso zkontroluje virtuální počítače Azure a spravovanou instanci SQL Database a zjistí případné problémy se zabezpečením implementace:

- Tým zkontroluje skupiny zabezpečení sítě sloužící k řízení přístupu k virtuálnímu počítači. Skupiny zabezpečení sítě pomáhají zajistit, aby do aplikace přicházel pouze povolený provoz.
- Bezpečnostní tým společnosti Contoso také zvažuje zabezpečení dat na disku pomocí služeb Azure Disk Encryption a Azure Key Vault.
- Tým povolí detekci hrozeb ve spravované instanci. Detekce hrozeb při zjištění hrozby odešle bezpečnostnímu týmu nebo do systému oddělení služeb společnosti Contoso upozornění, že se má vytvořit lístek. Další informace o [detekci hrozeb u spravované instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-threat-detection)

     ![Zabezpečení spravované instance – Detekce hrozeb](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-security.png)

Další informace o postupech zabezpečení virtuálních počítačů najdete v tématu [Osvědčené postupy zabezpečení pro úlohy IaaS v Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>BCDR

V zájmu zajištění provozní kontinuity a zotavení po havárii (BCDR) společnost Contoso provede tyto akce:

- Zabezpečení dat: společnost Contoso zálohuje data na virtuálních počítačích pomocí služby Azure Backup. [Další informace](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Udržujte aplikace v provozu: společnost Contoso replikuje virtuální počítače aplikace v Azure do sekundární oblasti pomocí Site Recovery. [Další informace](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).
- Společnost Contoso se blíže seznamuje se správou spravované instance SQL včetně [zálohování databází](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- Společnost Contoso má stávající licenci pro virtuální počítač WEBVM. Aby mohla využít ceny programu Zvýhodněné hybridní využití Azure, společnost Contoso stávající virtuální počítač převede.
- Společnost Contoso povolí službu Azure Cost Management licencovanou společností Cloudyn, dceřinou společností Microsoftu. Cost Management je multicloudové řešení správy nákladů, které společnosti Contoso pomáhá využívat a spravovat Azure a další cloudové prostředky. Další informace o službě [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview)

## <a name="conclusion"></a>Závěr

V tomto článku společnost Contoso změnila hostitele aplikace SmartHotel360 v Azure migrací front-endového virtuálního počítače aplikace do Azure pomocí služby Site Recovery. Společnost Contoso migrovala místní databázi do spravované instance Azure SQL Database pomocí služby Azure Database Migration Service.
