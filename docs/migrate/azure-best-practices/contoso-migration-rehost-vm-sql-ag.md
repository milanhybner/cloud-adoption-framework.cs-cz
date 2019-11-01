---
title: Opětovné hostování aplikace migrací do virtuálních počítačů Azure a skupin dostupnosti Always On SQL Server
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak společnost Contoso mění hostitele místní aplikace tím, že ji migruje na virtuální počítače Azure a skupiny dostupnosti AlwaysOn pro SQL Server.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 3f80454b864ae89f15a3be6d736192545683a0ed
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239281"
---
# <a name="rehost-an-on-premises-app-on-azure-vms-and-sql-server-always-on-availability-groups"></a>Opětovné hostování místní aplikace na virtuálních počítačích Azure a skupin dostupnosti Always On SQL Server

Tento článek ukazuje, jak fiktivní společnost Contoso v rámci migrace do Azure mění hostitele dvouúrovňové aplikace Windows .NET, která běží na virtuálních počítačích VMware. Společnost Contoso provede migraci front-endového virtuálního počítače aplikace na virtuální počítač Azure a databázi aplikace na virtuální počítač Azure s SQL Serverem v clusteru s podporou převzetí služeb při selhání Windows Serveru a se skupinami dostupnosti AlwaysOn pro SQL Server.

Aplikace SmartHotel360 použitá v tomto příkladu je k dispozici jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s partnery ve firmě, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Společnost Contoso roste, čímž vzniká tlak na místní systémy a infrastrukturu.
- **Zvýšení efektivity.** Společnost Contoso se potřebuje zbavit zbytečných postupů a zjednodušit procesy pro vývojáře i uživatele. Potřebuje IT k tomu, aby neztrácela čas ani peníze, byla rychlá a dokázala rychleji reagovat na požadavky zákazníků.
- **Zvýšení agility.** IT ve společnosti Contoso musí pohotověji reagovat na potřeby firmy. K zajištění úspěchu v globální ekonomice je nutné, aby IT dokázalo rychleji reagovat na změny na trhu. IT nesmí stát v cestě a nesmí se stát obchodní překážkou.
- **Škálování** Contoso se úspěšně rozšiřuje a IT musí poskytovat systémy, které jsou schopné rozvíjet se stejným tempem.

## <a name="migration-goals"></a>Cíle migrace

Tým pro přechod společnosti Contoso na cloud přesně specifikoval cíle této migrace. Tyto cíle se použily k určení nejlepší metody migrace:

- Po migraci by měla mít aplikace v Azure stejné možnosti výkonu jako v současnosti v prostředí VMware. Aplikace bude v cloudu nadále stejně důležitá, jako je dnes v místním prostředí.
- Společnost Contoso nechce investovat do této aplikace. Aplikace je pro firmu důležitá, ale Contoso ji zatím chce jen ve stávající podobě bezpečně přesunout do cloudu.
- U místní databáze aplikace docházelo k problémům s dostupností. Společnost Contoso by ji chtěla nasadit do Azure jako vysoce dostupný cluster s možnostmi převzetí služeb při selhání.
- Společnost Contoso chcete upgradovat z aktuální platformy SQL Server 2008 R2 na SQL Server 2017.
- Společnost Contoso nechce pro tuto aplikaci použít službu Azure SQL Database a proto hledá alternativy.

## <a name="solution-design"></a>Návrh řešení

Po vytyčení cílů a požadavků společnost Contoso navrhne a zkontroluje řešení nasazení a identifikuje proces migrace včetně služeb Azure, které k migraci využije.

### <a name="current-architecture"></a>Současná architektura

- Aplikace obsahuje úrovně rozdělené mezi dva virtuální počítače (WEBVM a SQLVM).
- Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com** (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) provozovaný na virtuálním počítači.
- Společnost Contoso má místní datacentrum (contoso-datacenter) s místním řadičem domény (**contosodc1**).

### <a name="proposed-architecture"></a>Navrhovaná architektura

V tomto scénáři:

- Společnost Contoso provede migraci front-endového virtuálního počítače WEBVM aplikace na virtuální počítač Azure IaaS.
  - Front-endový virtuální počítač v Azure se nasadí do skupiny prostředků ContosoRG (která se používá pro produkční prostředky).
  - Bude se nacházet v produkční síti Azure (VNET-PROD-EUS2) v primární oblasti Východní USA 2.
- Databáze aplikace se bude migrovat na virtuální počítač Azure s SQL Serverem.
  - Bude se nacházet v databázové síti Azure společnosti Contoso (PROD-DB-EUS2) v primární oblasti Východní USA 2.
  - Bude umístěný v clusteru s podporou převzetí služeb při selhání Windows Serveru se dvěma uzly, který využívá skupiny dostupnosti AlwaysOn pro SQL Server.
  - Tyto dva uzly virtuálních počítačů s SQL Serverem v clusteru se v Azure nasadí do skupiny prostředků ContosoRG.
  - Uzly virtuálních počítačů se budou nacházet v produkční síti Azure (VNET-PROD-EUS2) v primární oblasti Východní USA 2.
  - Na virtuálních počítačích bude Windows Server 2016 s SQL Serverem 2017 Enterprise. Společnost Contoso na tento operační systém nemá licence, takže použije image z Azure Marketplace, která jí příslušnou licenci zajistí za poplatek v rámci její smlouvy Azure EA.
  - Kromě jedinečných názvů bude nastavení obou virtuálních počítačů stejné.
- Společnost Contoso nasadí interní nástroj pro vyrovnávání zatížení, který bude naslouchat provozu v clusteru a směrovat ho na příslušné uzly clusteru.
  - Interní nástroj pro vyrovnávání zatížení se nasadí do skupiny prostředku ContosoNetworkingRG (která se používá pro síťové prostředky).
- Po dokončení migrace se místní virtuální počítače v datacentru Contoso vyřadí z provozu.

![Architektura scénáře](media/contoso-migration-rehost-vm-sql-ag/architecture.png)

### <a name="database-considerations"></a>Aspekty týkající se databáze

Při návrhu řešení společnost Contoso provedla porovnání funkcí mezi Azure SQL Database a SQL Serverem. Následující aspekty ji přiměly rozhodnout se pro virtuální počítač Azure IaaS s SQL Serverem:

- Použití virtuálního počítače Azure s SQL Serverem se jeví jako optimální řešení, pokud bude Contoso chtít přizpůsobit operační systém nebo databázový server nebo pokud bude chtít do stejného virtuálního počítače umístit i aplikace třetích stran a spouštět je.
- Společnost Contoso může službu Azure SQL Database snadno vyhodnotit a migrovat na ni s využitím nástroje Data Migration Assistant.

### <a name="solution-review"></a>Revize řešení

Společnost Contoso vyhodnotí vytvořený návrh tím, že sestaví seznam pro a proti.

<!-- markdownlint-disable MD033 -->

**Aspekty** | **Podrobnosti**
--- | ---
**Výhody** | Virtuální počítač WEBVM se přesune do Azure beze změn, takže jeho migrace bude snadná.<br/><br/> Vrstva SQL Serveru poběží na SQL Serveru 2017 a Windows Serveru 2016. Tím se aktuální operační systém Windows Server 2008 R2 vyřadí z provozu. SQL Server 2017 navíc podporuje technické požadavky a cíle společnosti Contoso. IT při přesunu z SQL Serveru 2008 R2 poskytuje 100% kompatibilitu.<br/><br/> Společnost Contoso může využít své investice do Software Assurance pomocí programu Zvýhodněné hybridní využití Azure.<br/><br/> Nasazení SQL Serveru s vysokou dostupností v Azure zajišťuje odolnost proti chybám, takže datová vrstva aplikace už není jediným bodem převzetí služeb při selhání.
**Nevýhody** | Na virtuálním počítači WEBVM běží Windows Server 2008 R2. Azure podporuje tento operační systém pro konkrétní role (červenec 2018). [Další informace](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).<br/><br/> Webová vrstva aplikace zůstane jediným bodem převzetí služeb při selhání.<br/><br/> Společnost Contoso bude muset dál podporovat webovou vrstvu jako virtuální počítač Azure, místo aby ji přesunula do spravované služby jako Azure App Service.<br/><br/> V případě zvoleného řešení bude společnost Contoso muset dál spravovat dva virtuální počítače s SQL Serverem, a nebude moct přejít na spravovanou platformu, jako je spravovaná instance Azure SQL Database. Díky Software Assurance by společnost Contoso navíc mohla vyměnit své stávající licence za nižší sazby za spravovanou instanci Azure SQL Database.

<!-- markdownlint-enable MD033 -->

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[Pomocník s migrací dat](/sql/dma/dma-overview?view=ssdt-18vs2017) | DMA se spouští místně z místního počítače s SQL Serverem a migruje databáze přes síť site-to-site VPN do Azure. | Nástroj DMA je zdarma ke stažení.
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Site Recovery orchestruje a spravuje migraci a zotavení po havárii pro virtuální počítače Azure a místní virtuální počítače a fyzické servery. | Během replikace do Azure se účtují poplatky za Azure Storage. Vytvoří se virtuální počítače Azure a při převzetí služeb při selhání se za ně účtují poplatky. [Další informace](https://azure.microsoft.com/pricing/details/site-recovery) o poplatcích a cenách

## <a name="migration-process"></a>Proces migrace

Správci společnosti Contoso provedou migraci virtuálních počítačů aplikace do Azure.

- Pomocí Site Recovery provedou migraci front-endového virtuálního počítače na virtuální počítač Azure:
  - Jako první krok připraví a nastaví komponenty Azure a připraví místní infrastrukturu VMware.
  - Až bude všechno připravené, můžou začít replikovat virtuální počítač.
  - Až se rozběhne replikace, provedou migraci virtuálního počítače tak, že Azure převezme jeho služby při selhání.
- Pomocí nástroje Data Migration Assistant (DMA) provedou migraci databáze do clusteru SQL Serveru v Azure.
  - Jako první krok budou muset zřídit virtuální počítače s SQL Serverem v Azure, nastavit cluster a interní nástroj pro vyrovnávání zatížení a nakonfigurovat skupiny dostupnosti AlwaysOn.
  - Jakmile to bude hotové, můžou migrovat databázi.
- Po dokončení migrace pro databázi povolí ochranu AlwaysOn.

![Proces migrace](media/contoso-migration-rehost-vm-sql-ag/migration-process.png)

## <a name="prerequisites"></a>Předpoklady

Tady je seznam toho, co společnost Contoso musí udělat k realizaci tohoto scénáře.

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Společnost Contoso již vytvořila předplatné v dřívějším článku této série. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.<br/><br/> Pokud potřebujete podrobnější oprávnění, přečtěte si [tento článek](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura Azure** | [Přečtěte si víc](./contoso-migration-infrastructure.md) o tom, jak společnost Contoso nastavuje infrastrukturu Azure.<br/><br/> Přečtěte si další informace o konkrétních požadavcích na [síť](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) a [úložiště](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage) pro Site Recovery.
**Site Recovery (místní)** | Místní servery vCenter by měly používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Hostitel ESXi by měl používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Na hostiteli ESXi by měl být spuštěný jeden nebo více virtuálních počítačů VMware.<br/><br/> Virtuální počítače musí splňovat [požadavky Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Podporované konfigurace [sítě](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) a [úložiště](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage)<br/><br/> Virtuální počítače, které chcete replikovat, musí splňovat [požadavky Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Contoso provede migraci takto:

> [!div class="checklist"]
>
> - **Krok 1: Příprava clusteru** Vytvoření clusteru pro nasazení dvou uzlů virtuálních počítačů s SQL Serverem v Azure.
> - **Krok 2: nasaďte a nastavte cluster.** Příprava clusteru Azure s SQL Serverem. Do tohoto existujícího clusteru se migrují databáze.
> - **Krok 3: nasaďte Nástroj pro vyrovnávání zatížení.** Nasazení nástroje pro vyrovnávání zatížení provozu na uzlech SQL Serveru.
> - **Krok 4: Příprava Azure na Site Recovery.** Vytvoření účtu úložiště Azure, ve kterém se budou uchovávat replikovaná data, a trezoru služby Recovery Services.
> - **Krok 5: Příprava místního VMware pro Site Recovery.** Příprava účtů pro zjišťování virtuálních počítačů a instalaci agenta. Příprava místních virtuálních počítačů, aby se uživatelé po migraci mohli připojit k virtuálním počítačům Azure.
> - **Krok 6: replikace virtuálních počítačů** Povolení replikace virtuálních počítačů do Azure.
> - **Krok 7: Nainstalujte DMA.** Stažení a instalace nástroje Data Migration Assistant.
> - **Krok 8: migrace databáze pomocí DMA.** Migrace databáze do Azure.
> - **Krok 9: Ochrana databáze.** Vytvoření skupiny dostupnosti AlwaysOn pro cluster.
> - **Krok 10: migrujte virtuální počítač webové aplikace.** Otestujete převzetí služeb při selhání, abyste měli jistotu, že všechno funguje, jak má. Následné spuštění úplného převzetí služeb při selhání do Azure.

## <a name="step-1-prepare-a-sql-server-always-on-availability-group-cluster"></a>Krok 1: Příprava clusteru skupiny dostupnosti Always On SQL Server

Správci společnosti Contoso nastaví cluster následujícím způsobem:

1. Na webu Azure Marketplace vyberou image Windows Serveru 2016 s SQL Serverem 2017 Enterprise a vytvoří dva virtuální počítače s SQL Serverem.

    ![Skladová položka virtuálního počítače SQL](media/contoso-migration-rehost-vm-sql-ag/sql-vm-sku.png)

2. V **průvodci vytvořením virtuálního počítače** > **Základy** nakonfigurují:

    - Názvy virtuálních počítačů: **SQLAOG1** a **SQLAOG2**.
    - Vzhledem k tomu, že jsou počítače klíčové pro chod firmy, jako typ disku virtuálního počítače povolí SSD.
    - Zadají přihlašovací údaje počítačů.
    - Nasadí virtuální počítače v primární oblasti Východní USA 2 ve skupině prostředků ContosoRG.

3. V části **Velikost** začnou se skladovou položkou D2s_V3 pro oba virtuální počítače. Později budou podle potřeby škálovat.
4. V **Nastavení** provedou následující:

    - Vzhledem k tomu, že tyto virtuální počítače představují klíčové databáze aplikace, používají spravované disky.
    - Umístí počítače do produkční sítě primární oblasti Východní USA 2 (**VNET-PROD-EUS2**) do podsítě databáze (**PROD-DB-EUS2**).
    - Vytvoří novou skupinu dostupnosti: **SQLAOGAVSET**se dvěma doménami selhání a pěti aktualizačními doménami.

      ![Virtuální počítač SQL](media/contoso-migration-rehost-vm-sql-ag/sql-vm-settings.png)

5. V **Nastavení SQL Serveru** omezí připojení SQL k virtuální síti (privátní) na výchozí port 1433. K ověření použijí stejné přihlašovací údaje jako v místním prostředí (**contosoadmin**).

    ![Virtuální počítač SQL](media/contoso-migration-rehost-vm-sql-ag/sql-vm-db.png)

**Potřebujete další pomoc?**

- [Pomoc](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#1-configure-basic-settings) se zřizováním virtuálního počítače s SQL Serverem
- [Informace](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-prereq#create-sql-server-vms) o konfiguraci virtuálních počítačů pro různé skladové položky SQL Serveru

## <a name="step-2-deploy-and-set-up-the-cluster"></a>Krok 2: nasazení a nastavení clusteru

Správci společnosti Contoso nastaví cluster následujícím způsobem:

1. Nastaví účet úložiště Azure, který bude fungovat jako disk s kopií cloudu.
2. Přidají virtuální počítače s SQL Serverem do domény Active Directory v místním datacentru společnosti Contoso.
3. Vytvoří cluster v Azure.
4. Nakonfigurují disk s kopií cloudu.
5. Nakonec povolí skupiny dostupnosti AlwaysOn pro SQL.

### <a name="set-up-a-storage-account-as-cloud-witness"></a>Nastavení účtu úložiště jako disku s kopií cloudu

Aby společnost Contoso mohla nastavit disk s kopií cloudu, potřebuje účet Azure Storage, který bude obsahovat soubor objektu blob sloužící k arbitráži clusteru. Stejný účet úložiště je možné použít k nastavení disku s kopií cloudu pro více clusterů.

Správci společnosti Contoso vytvoří účet úložiště následujícím způsobem:

1. Zadají rozpoznatelný název účtu (**contosocloudwitness**).
2. Nasadí účet pro obecné účely s úložištěm LRS.
3. Tento účet umístí do třetí oblasti: Středojižní USA. Umístí ho mimo primární a sekundární oblast, aby zůstal dostupný v případě selhání oblasti.
4. Umístí ho do skupiny prostředků **ContosoInfraRG**, která obsahuje prostředky infrastruktury.

    ![Disk s kopií cloudu](media/contoso-migration-rehost-vm-sql-ag/witness-storage.png)

5. Při vytvoření účtu úložiště se pro něj vygenerují primární a sekundární přístupový klíč. K vytvoření disku s kopií cloudu potřebují primární přístupový klíč. Klíč se zobrazí pod názvem účtu úložiště v části **Přístupové klíče**.

    ![Přístupový klíč](media/contoso-migration-rehost-vm-sql-ag/access-key.png)

### <a name="add-sql-server-vms-to-contoso-domain"></a>Přidání virtuálních počítačů s SQL Serverem do domény Contoso

1. Společnost Contoso přidá virtuální počítače SQLAOG1 a SQLAOG2 do domény contoso.com.
2. Pak na obou virtuálních počítačích nainstalují funkce a nástroje clusteru s podporou převzetí služeb při selhání Windows.

### <a name="set-up-the-cluster"></a>Nastavení clusteru

Před nastavením clusteru správci společnosti Contoso pořídí snímek disku s operačním systémem obou počítačů.

![Snímek](media/contoso-migration-rehost-vm-sql-ag/snapshot.png)

1. Potom spustí skript, který sestavili pro vytvoření clusteru s podporou převzetí služeb při selhání Windows.

    ![Vytvoření clusteru](media/contoso-migration-rehost-vm-sql-ag/create-cluster1.png)

2. Po vytvoření clusteru ověří, že se virtuální počítače zobrazí jako uzly clusteru.

     ![Vytvoření clusteru](media/contoso-migration-rehost-vm-sql-ag/create-cluster2.png)

### <a name="configure-the-cloud-witness"></a>Konfigurace disku s kopií cloudu

1. Správci společnosti Contoso nakonfigurují disk s kopií cloudu pomocí **průvodce konfigurací kvóra** v doplňku Správce clusteru s podporou převzetí služeb při selhání.
2. V průvodci zvolí, že chtějí vytvořit disk s kopií cloudu s využitím účtu úložiště.
3. Po nakonfigurování se disk s kopií cloudu zobrazí v doplňku Správce clusteru s podporou převzetí služeb při selhání.

    ![Disk s kopií cloudu](media/contoso-migration-rehost-vm-sql-ag/cloud-witness.png)

### <a name="enable-sql-server-always-on-availability-groups"></a>Povolení skupin dostupnosti AlwaysOn pro SQL Server

Správci společnosti Contoso teď můžou povolit skupiny dostupnosti AlwaysOn:

1. V SQL Server Configuration Manageru povolí **Skupiny dostupnosti AlwaysOn** pro službu **SQL Server (MSSQLSERVER)** .

    ![Povolení skupin dostupnosti AlwaysOn](media/contoso-migration-rehost-vm-sql-ag/enable-alwayson.png)

2. Restartují službu, aby se změny projevily.

Když jsou skupiny dostupnosti AlwaysOn povolené, společnost Contoso může nastavit skupinu dostupnosti AlwaysOn, která bude chránit databázi SmartHotel360.

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness) o disku s kopií cloudu a nastavení účtu úložiště pro něj
- [Pokyny](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial) k nastavení clusteru a vytvoření skupiny dostupnosti

## <a name="step-3-deploy-the-azure-load-balancer"></a>Krok 3: nasazení Azure Load Balancer

Správci společnosti Contoso teď chtějí nasadit interní nástroj pro vyrovnávání zatížení, který se bude nacházet před uzly clusteru. Nástroj pro vyrovnávání zatížení naslouchá provozu a směruje ho do příslušných uzlů.

![Vyrovnávání zatížení](media/contoso-migration-rehost-vm-sql-ag/architecture-lb.png)

Nástroj pro vyrovnávání zatížení vytvoří následujícím způsobem:

1. V Azure Portal > **sítě**  > **Load Balancer**nastavili nový interní nástroj pro vyrovnávání zatížení: **interního nástroje-prod-DB-EUS2-SQLAOG**.
2. Umístí nástroj pro vyrovnávání zatížení do produkční sítě **VNET-PROD-EUS2** do podsítě databáze **PROD-DB-EUS2**.
3. Přiřadí jí statickou IP adresu: 10.245.40.100.
4. Jako síťový prvek umístí nástroj pro vyrovnávání zatížení do skupiny síťových prostředků **ContosoNetworkingRG**.

    ![Vyrovnávání zatížení](media/contoso-migration-rehost-vm-sql-ag/lb-create.png)

Po nasazení interního nástroje pro vyrovnávání zatížení ho musí nastavit. Vytvoří back-endový fond adres, nastaví sondu stavu a nakonfigurují pravidlo vyrovnávání zatížení.

### <a name="add-a-back-end-pool"></a>Přidání back-endového fondu

Aby bylo možné distribuovat provoz do virtuálních počítačů v clusteru, správci společnosti Contoso nastaví back-endový fond adres, který obsahuje IP adresy síťových karet virtuálních počítačů, které budou přijímat síťový provoz z nástroje pro vyrovnávání zatížení.

1. V nastavení nástroje pro vyrovnávání zatížení na portálu contoso přidejte fond back-end: **interního nástroje-prod-DB-EUS-SQLAOG-BEPOOL**.
2. Fond přidruží ke skupině dostupnosti SQLAOGAVSET. Do fondu se přidají virtuální počítače v sadě (**SQLAOG1** a **SQLAOG2**).

    ![Back-endový fond](media/contoso-migration-rehost-vm-sql-ag/backend-pool.png)

### <a name="create-a-health-probe"></a>Vytvoření sondy stavu

Správci společnosti Contoso vytvoří sondu stavu, aby nástroj pro vyrovnávání zatížení mohl monitorovat stav aplikace. Sonda dynamicky přidává virtuální počítače do oběhu nástroje pro vyrovnávání zatížení nebo je z něj odebírá na základě jejich reakce na kontroly stavu.

Sondu vytvoří následujícím způsobem:

1. V nastavení nástroje pro vyrovnávání zatížení na portálu contoso vytvoří sondu stavu: **SQLAlwaysOnEndPointProbe**.
2. Sondu nastaví tak, aby monitorovala virtuální počítače na portu TCP 59999.
3. Nastaví interval 5 sekund mezi sondami a prahovou hodnotou 2. V případě selhání dvou sond se virtuální počítač bude považovat za poškozený.

    ![Sonda](media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

### <a name="configure-the-load-balancer-to-receive-traffic"></a>Konfigurace nástroje pro vyrovnávání zatížení pro příjem provozu

Teď správci společnosti Contoso nastaví pravidlo nástroje pro vyrovnávání zatížení, které bude definovat způsob distribuce provozu do virtuálních počítačů.

- Front-endová IP adresa zpracovává příchozí provoz.
- Back-endový fond IP adres přijímá provoz.

Pravidlo vytvoří následujícím způsobem:

1. V nastavení nástroje pro vyrovnávání zatížení na portálu přidávají nové pravidlo vyrovnávání zatížení: **SQLAlwaysOnEndPointListener**.
2. Nastaví front-endový naslouchací proces tak, aby přijímal příchozí provoz z klienta SQL na portu TCP 1433.
3. Určí back-endový fond, do kterého se provoz bude směrovat, a port, na kterém budou virtuální počítače naslouchat provozu.
4. Povolí plovoucí IP adresu (přímá odpověď ze serveru). Toto se vždy vyžaduje u skupin dostupnosti AlwaysOn pro SQL.

    ![Sonda](media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

**Potřebujete další pomoc?**

- [Přehled](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) nástroje Azure Load Balancer
- [Informace](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal) o vytvoření nástroje pro vyrovnávání zatížení

## <a name="step-4-prepare-azure-for-the-site-recovery-service"></a>Krok 4: Příprava Azure na službu Site Recovery

Contoso potřebuje k nasazení Site Recovery tyto komponenty Azure:

- Virtuální síť, ve které se budou nacházet virtuální počítače vytvořené během převzetí služeb při selhání
- Účet Azure Storage, ve kterém se budou uchovávat replikovaná data
- Trezor služby Recovery Services v Azure

Správci společnosti Contoso je nastaví následujícím způsobem:

1. Společnost Contoso už vytvořila síť nebo podsíť, kterou může použít pro Site Recovery, když [nasazovala infrastrukturu Azure](./contoso-migration-rehost-vm-sql-ag.md).

    - Aplikace SmartHotel360 je produkční aplikace a virtuální počítač WEBVM se bude migrovat do produkční sítě Azure (VNET-PROD-EUS2) v primární oblasti Východní USA 2.
    - Virtuální počítač WEBVM se umístí do skupiny prostředků ContosoRG, která se používá pro produkční prostředky, a do produkční podsítě (PROD-FE-EUS2).

2. Správci společnosti Contoso vytvoří účet úložiště Azure (contosovmsacc20180528) v primární oblasti.

    - Společnost používá účet pro obecné účely se standardním úložištěm a replikaci LRS.
    - Účet musí být ve stejné oblasti jako trezor.

      ![Úložiště služby Site Recovery](media/contoso-migration-rehost-vm-sql-ag/asr-storage.png)

3. Když je připravená síť a účet úložiště, vytvoří trezor služby Recovery Services (**ContosoMigrationVault**) a umístí ho do skupiny prostředků **ContosoFailoverRG** v primární oblasti Východní USA 2.

    ![Trezor služby Recovery Services](media/contoso-migration-rehost-vm-sql-ag/asr-vault.png)

**Potřebujete další pomoc?**

[Přečtěte si](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure) o nastavení Azure pro Site Recovery.

## <a name="step-5-prepare-on-premises-vmware-for-site-recovery"></a>Krok 5: Příprava místního VMware pro Site Recovery

V místním prostředí správci společnosti Contoso připraví tyto položky:

- Účet na serveru vCenter nebo hostiteli vSphere ESXi pro automatizaci zjišťování virtuálních počítačů
- Účet, který umožní automatickou instalaci služby Mobility na virtuálních počítačích VMware, které chtějí replikovat
- Nastavení místních virtuálních počítačů, aby se společnost Contoso mohla po převzetí služeb při selhání připojit k replikovanému virtuálnímu počítači Azure

### <a name="prepare-an-account-for-automatic-discovery"></a>Příprava účtu pro automatické zjišťování

Site Recovery potřebuje přístup k serverům VMware z těchto důvodů:

- Automatické zjišťování virtuálních počítačů.
- Orchestrace replikace, převzetí služeb při selhání a navrácení služeb po obnovení.
- Vyžaduje se alespoň účet jen pro čtení. Potřebujete účet, který může spouštět operace, jako jsou vytváření a odebírání disků a zapínání virtuálních počítačů.

Správci společnosti Contoso nastaví účet následujícím způsobem:

1. Vytvoří roli na úrovni vCenter.
2. Potom této roli přiřadí požadovaná oprávnění.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Příprava účtu pro instalaci služby Mobility

Na každý virtuální počítač je potřeba nainstalovat službu Mobility.

- Když je povolená replikace virtuálního počítače, Site Recovery může automaticky provést nabízenou instalaci této komponenty.
- U nabízené instalace potřebujete účet, který služba Site Recovery může použít k získání přístupu k virtuálnímu počítači. Tento účet zadáte při nastavování replikace v konzole Azure.
- Může se jednat do doménový nebo místní účet s oprávněními k instalaci na virtuální počítač.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Příprava připojení k virtuálním počítačům Azure po převzetí služeb při selhání

Po převzetí služeb při selhání chce společnost Contoso mít možnost se připojit k virtuálním počítačům Azure. K tomu musí správci společnosti Contoso provést před migrací tyto kroky:

1. Přístup přes internet zajistí takto:

   - Před převzetím služeb při selhání povolí na místním virtuálním počítači protokol RDP.
   - Zajistí přidání pravidel protokolu TCP a UDP pro profil **Public**.
   - Zkontrolují, jestli je v části **Brána Windows Firewall** > **Povolené aplikace** pro všechny profily povolený protokol RDP.

2. Přístup přes síť site-to-site VPN zajistí takto:

   - Povolí na místním počítači protokol RDP.
   - V části **Brána Windows Firewall** -> **Povolené aplikace a funkce** povolí pro **doménové a privátní** sítě protokol RDP.
   - Nastaví zásadu SAN operačního systému místního virtuálního počítače na **OnlineAll**.

Kromě toho musejí při spuštění převzetí služeb při selhání zkontrolovat tyto body:

- Při aktivaci převzetí služeb při selhání by na virtuálním počítači neměly být žádné čekající aktualizace Windows. V opačném případě se uživatelé nebudou moct k virtuálnímu počítači přihlásit, dokud se aktualizace nedokončí.
- Po převzetí služeb při selhání můžou zkontrolovat **diagnostiku spuštění** a zobrazit si snímek obrazovky virtuálního počítače. Pokud to nefunguje, měli by zkontrolovat, jestli je virtuální počítač spuštěný, a projít si tyto [tipy pro řešení potíží](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) o vytváření a přiřazování rolí pro automatické zjišťování
- [Informace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) o vytvoření účtu pro nabízenou instalaci služby Mobility Service

## <a name="step-6-replicate-the-on-premises-vms-to-azure-with-site-recovery"></a>Krok 6: replikace místních virtuálních počítačů do Azure pomocí Site Recovery

Než budou moct správci společnosti Contoso spustit migraci do Azure, musejí nastavit a povolit replikaci.

### <a name="set-a-replication-goal"></a>Určení cíle replikace

1. V trezoru pod názvem trezoru (ContosoVMVault) vyberou cíl replikace (**Začínáme** > **Site Recovery** > **Připravit infrastrukturu**).
2. Určí, že se jejich počítače nacházejí v místním prostředí, běží na VMware a replikují se do Azure.

    ![Cíl replikace](./media/contoso-migration-rehost-vm-sql-ag/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Potvrzení plánování nasazení

Dále musí potvrdit, že provedli plánování nasazení, výběrem možnosti **Ano, mám to hotové**. V tomto scénáři společnost Contoso migruje pouze virtuální počítač a plánování nasazení nepotřebuje.

### <a name="set-up-the-source-environment"></a>Nastavení zdrojového prostředí

Správci společnosti Contoso musejí nakonfigurovat zdrojové prostředí. K tomu si musí stáhnout šablonu OVF a pomocí ní nasadit konfigurační server Site Recovery jako místní virtuální počítač VMware s vysokou dostupností. Po nastavení a spuštění zaregistrují konfigurační server v trezoru.

Konfigurační server spustí několik komponent:

- Komponenta konfiguračního serveru, která koordinuje komunikaci mezi místním prostředím a Azure a spravuje replikaci dat.
- Procesový server, který funguje jako replikační brána. Přijímá data replikace, optimalizuje je pomocí ukládání do mezipaměti, komprese a šifrování a odesílá je do úložiště Azure.
- Procesový server také na všechny virtuální počítače, které chcete replikovat, nainstaluje službu mobility a automaticky vyhledá místní virtuální počítače VMware.

Správci společnosti Contoso provedou tyto kroky následujícím způsobem:

1. V trezoru si stáhnou šablonu OVF z části **Připravit infrastrukturu** > **Zdroj** > **Konfigurační server**.

    ![Stažení souboru OVF](./media/contoso-migration-rehost-vm-sql-ag/add-cs.png)

2. Importují šablonu do VMware, aby došlo k vytvoření a nasazení virtuálního počítače.

    ![Šablona OVF](./media/contoso-migration-rehost-vm-sql-ag/vcenter-wizard.png)

3. Při prvním zapnutí virtuálního počítače se spustí prostředí instalace systému Windows Server 2016. Přijmou licenční smlouvu a zadají heslo správce.
4. Po dokončení instalace se přihlásí k virtuálnímu počítači jako správce. Při prvním přihlášení se automaticky spustí nástroj pro konfiguraci služby Azure Site Recovery.
5. V nástroji zadají název, který se má použít pro registraci konfiguračního serveru v trezoru.
6. Nástroj zkontroluje, jestli se virtuální počítač může připojit k Azure. Po navázání připojení se správci přihlásí k předplatnému Azure. Přihlašovací údaje musí zajišťovat přístup k trezoru, do kterého chcete konfigurační server zaregistrovat.

    ![Registrace konfiguračního serveru](./media/contoso-migration-rehost-vm-sql-ag/config-server-register2.png)

7. Nástroj provede několik úloh konfigurace a pak restartuje počítač.
8. Znovu se přihlásí k počítači a automaticky se spustí průvodce správou konfiguračního serveru.
9. V průvodci vyberou síťovou kartu pro příjem dat přenášených při replikaci. Po dokončení konfigurace není možné toto nastavení změnit.
10. Vyberou předplatné, skupinu prostředků a trezor, ve kterém se má konfigurační server zaregistrovat.
        ![Trezor](./media/contoso-migration-rehost-vm-sql-ag/cswiz1.png)

11. Potom stáhnou a nainstalují MySQL Server a VMware PowerCLI.
12. Po ověření zadají plně kvalifikovaný název domény nebo IP adresu serveru vCenter nebo hostitele vSphere. Ponechají výchozí port a zadají popisný název serveru vCenter.
13. Zadají účet, který vytvořili pro automatické zjišťování, a přihlašovací údaje, které slouží k automatické instalaci Mobility Service. V případě virtuálních počítačů s Windows je nutné, aby na nich měl tento účet oprávnění místního správce.

    ![vCenter](./media/contoso-migration-rehost-vm-sql-ag/cswiz2.png)

14. Po dokončení registrace zkontrolují na webu Azure Portal, jestli je ve vybraném trezoru na stránce **Zdroj** uvedený konfigurační server a server VMware. Zjišťování může trvat 15 minut nebo i více.
15. Potom se služba Site Recovery připojí k serverům VMware pomocí zadaného nastavení a vyhledá virtuální počítače.

### <a name="set-up-the-target"></a>Nastavení cíle

Teď správci společnosti Contoso určí nastavení cíle replikace.

1. V části **Připravit infrastrukturu** > **Cíl** zvolí nastavení cíle.
2. Site Recovery zkontroluje, jestli je v zadaném cílovém umístění účet úložiště Azure a síť.

### <a name="create-a-replication-policy"></a>Vytvoření zásady replikace

Teď můžou správci společnosti Contoso vytvořit zásadu replikace.

1. V části **Připravit infrastrukturu** > **Nastavení replikace** > **Zásady replikace** >  **Vytvořit a přidružit** vytvoří zásadu **ContosoMigrationPolicy**.
2. Použijí výchozí nastavení:
    - **Prahová hodnota cíle RPO:** Výchozí hodnota je 60 minut. Tato hodnota určuje, jak často se tvoří body obnovení. Když průběžná replikace překročí tento limit, vygeneruje se upozornění.
    - **Uchování bodu obnovení:** Výchozí hodnota je 24 hodin. Tato hodnota určuje délku intervalu uchovávání dat pro jednotlivé body obnovení. Replikované virtuální počítače můžete v rámci okna uchování obnovit do libovolného časového bodu.
    - **Frekvence snímků konzistentní vzhledem k aplikacím:** Výchozí hodnota je jedna hodina. Tato hodnota určuje četnost vytváření snímků konzistentních vzhledem k aplikacím.

        ![Vytvoření zásady replikace](./media/contoso-migration-rehost-vm-sql-ag/replication-policy.png)

3. Tato zásada se automaticky přidruží ke konfiguračnímu serveru.

    ![Přidružení zásady replikace](./media/contoso-migration-rehost-vm-sql-ag/replication-policy2.png)

### <a name="enable-replication"></a>Povolení replikace

Teď můžou správci společnosti Contoso zahájit replikaci virtuálního počítače WEBVM.

1. V části **Replikovat aplikaci** > **Zdroj** >  **+Replikovat** vyberou nastavení zdroje.
2. Určí, že chtějí povolit virtuální počítače, zvolí server vCenter a konfigurační server.

    ![Povolení replikace](./media/contoso-migration-rehost-vm-sql-ag/enable-replication1.png)

3. Teď určí nastavení cíle, včetně skupiny prostředků, virtuální sítě a účtu úložiště, ve kterém se budou uchovávat replikovaná data.

     ![Povolení replikace](./media/contoso-migration-rehost-vm-sql-ag/enable-replication2.png)

4. Pro replikaci vyberou počítač WEBVM, zkontrolují zásadu replikace a povolí replikaci. Po povolení replikace Site Recovery na virtuální počítač nainstaluje službu Mobility Service.

    ![Povolení replikace](./media/contoso-migration-rehost-vm-sql-ag/enable-replication3.png)

5. V části **Úlohy** sledují průběh replikace. Po spuštění úlohy **Dokončit ochranu** je počítač připravený k převzetí služeb při selhání.
6. Na webu Azure Portal v části **Základní údaje** se zobrazuje struktura virtuálních počítačů replikovaných do Azure.

    ![Zobrazení infrastruktury](./media/contoso-migration-rehost-vm-sql-ag/essentials.png)

**Potřebujete další pomoc?**

- Podrobný popis všech těchto kroků najdete v článku [Nastavení zotavení po havárii pro místní virtuální počítače VMware](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- K dispozici jsou také podrobné pokyny, které vám pomůžou [nastavit zdrojové prostředí](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [nasadit konfigurační server](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) a [nakonfigurovat nastavení replikace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).
- Můžete si přečíst další informace o [povolení replikace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-7-install-the-data-migration-assistant-dma"></a>Krok 7: instalace Data Migration Assistant (DMA)

Správci společnosti Contoso budou pomocí DMA migrovat databázi SmartHotel360 na virtuální počítač Azure **SQLAOG1**. DMA nastaví následujícím způsobem:

1. Tento nástroj si stáhnou z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) do místního virtuálního počítače s SQL Serverem (**SQLVM**).
2. Na tomto virtuálním počítači spustí instalační program (DownloadMigrationAssistant.msi).
3. Před dokončením průvodce na stránce **Finish** (Dokončit) vyberou **Launch Microsoft Data Migration Assistant** (Spustit nástroj Microsoft Data Migration Assistant).

## <a name="step-8-migrate-the-database-with-dma"></a>Krok 8: migrace databáze pomocí DMA

1. V DMA spustí novou migraci **SmartHotel**.
2. Jako **Target server type** (Typ cílového serveru) vyberou **SQL Server on Azure Virtual Machines** (SQL Server na virtuálních počítačích Azure).

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-1.png)

3. V podrobnostech o migraci doplní **SQLVM** jako zdrojový server a **SQLAOG1** jako cíl. Zadají přihlašovací údaje k oběma počítačům.

     ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-2.png)

4. Vytvoří místní sdílenou složku pro databázi a informace o konfiguraci. Účet služby SQL na virtuálních počítačích SQLVM a SQLAOG1 musí k této složce mít přístup k zápisu.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-3.png)

5. Společnost Contoso zvolí přihlašovací jména, která se mají migrovat, a spustí migraci. Po jejím dokončení se v DMA zobrazí úspěšně provedená migrace.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-4.png)

6. Ověří, že databáze běží na virtuálním počítači **SQLAOG1**.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-5.png)

DMA se připojí k místnímu virtuálnímu počítači s SQL Serverem přes připojení site-to-site VPN mezi datacentrem společnosti Contoso a Azure a pak provede migraci databáze.

## <a name="step-9-protect-the-database-with-always-on"></a>Krok 9: Ochrana databáze pomocí nástroje Always On

Když teď databáze aplikace běží na virtuálním počítači **SQLAOG1**, můžou ji správci společnosti Contoso zabezpečit s využitím skupin dostupnosti AlwaysOn. Pomocí aplikace SQL Server Management Studio nakonfigurují skupiny dostupnosti AlwaysOn a pak s využitím clusteringu Windows přiřadí naslouchací proces.

### <a name="create-an-always-on-availability-group"></a>Vytvoření skupiny dostupnosti AlwaysOn

1. V aplikaci SQL Server Management Studio kliknutím pravým tlačítkem na **Vysoká dostupnost AlwaysOn** spustí **průvodce vytvořením nové skupiny dostupnosti**.
2. V části **Určení možností** zadají název skupiny dostupnosti **SHAOG**. V části **Výběr databází** vyberou databázi SmartHotel360.

    ![Skupina dostupnosti Always On](media/contoso-migration-rehost-vm-sql-ag/aog-1.png)

3. V části **Určit repliky** přidají dva uzly SQL jako repliky dostupnosti a nakonfigurují je tak, aby zajišťovaly automatické převzetí při selhání se synchronním potvrzováním.

     ![Skupina dostupnosti Always On](media/contoso-migration-rehost-vm-sql-ag/aog-2.png)

4. Nakonfigurují naslouchací proces pro příslušnou skupinu (**SHAOG**) a port. IP adresa interního nástroje pro vyrovnávání zatížení se přidá jako statická IP adresa (10.245.40.100).

    ![Skupina dostupnosti Always On](media/contoso-migration-rehost-vm-sql-ag/aog-3.png)

5. V části **Vybrat synchronizaci dat** povolí automatické předvyplňování. S využitím této možnosti SQL Server automaticky vytvoří sekundární repliky všech databází ve skupině, aby je společnost Contoso nemusela ručně zálohovat a obnovovat. Po ověření se vytvoří skupina dostupnosti.

    ![Skupina dostupnosti Always On](media/contoso-migration-rehost-vm-sql-ag/aog-4.png)

6. Společnost Contoso při vytváření skupiny narazila na problém. Nepoužívají integrované zabezpečení systému Windows pro Active Directory, a proto musí přihlášení SQL udělit oprávnění k vytvoření rolí clusteru s podporou převzetí služeb při selhání Windows.

    ![Skupina dostupnosti Always On](media/contoso-migration-rehost-vm-sql-ag/aog-5.png)

7. Po vytvoření se skupina společnosti Contoso zobrazí v aplikaci SQL Server Management Studio.

### <a name="configure-a-listener-on-the-cluster"></a>Konfigurace naslouchacího procesu v clusteru

Jako poslední krok při nastavování nasazení SQL správci společnosti Contoso nakonfigurují interní nástroj pro vyrovnávání zatížení jako naslouchací proces v clusteru a přepnou ho do režimu online. Použijí k tomu skript.

![Naslouchací proces clusteru](media/contoso-migration-rehost-vm-sql-ag/cluster-listener.png)

### <a name="verify-the-configuration"></a>Ověření konfigurace

Vše je nastavené a společnost Contoso teď má v Azure funkční skupinu dostupnosti, která využívá migrovanou databázi. Správci to ověří tím, že se v aplikaci SQL Server Management Studio připojí k internímu nástroji pro vyrovnávání zatížení.

![Připojení k internímu nástroji pro vyrovnávání zatížení](media/contoso-migration-rehost-vm-sql-ag/ilb-connect.png)

**Potřebujete další pomoc?**

- Informace o vytvoření [skupiny dostupnosti](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#create-the-availability-group) a [naslouchacího procesu](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#configure-listener)
- Ruční [nastavení clusteru pro používání IP adresy nástroje pro vyrovnávání zatížení](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#configure-the-cluster-to-use-the-load-balancer-ip-address)
- [Další informace](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2) o vytvoření a používání SAS

## <a name="step-10-migrate-the-vm-with-site-recovery"></a>Krok 10: migrace virtuálního počítače pomocí Site Recovery

Správci společnosti Contoso spustí rychlé testovací převzetí služeb při selhání a pak provedou migraci virtuálního počítače.

### <a name="run-a-test-failover"></a>Spuštění testovacího převzetí služeb při selhání

Spuštění testovacího převzetí služeb při selhání slouží k ověření toho, jestli před migrací všechno funguje podle očekávání.

1. Spustí testovací převzetí služeb při selhání k nejnovějšímu dostupnému bodu v čase (**Nejnovější zpracovaný**).
2. Vyberou **Před spuštěním převzetí služeb při selhání vypnout počítač**, takže se Site Recovery pokusí před aktivací převzetí služeb při selhání vypnout zdrojový virtuální počítač. Převzetí služeb při selhání bude pokračovat i v případě, že se vypnutí nepovede.
3. Spustí se testovací převzetí služeb při selhání:

    - Spustí se kontrola předpokladů, která zjistí, jestli jsou splněné všechny podmínky pro migraci.
    - Převzetí služeb při selhání tato data zpracuje, aby se mohl vytvořit virtuální počítač Azure. Pokud jste vybrali nejnovější bod obnovení, vytvoří se z těchto dat nový.
    - Pomocí dat zpracovaných v předchozím kroku se vytvoří virtuální počítač Azure.

4. Po dokončení převzetí služeb při selhání se na portálu Azure Portal objeví replika virtuálního počítače Azure. Zkontrolují, že virtuální počítač má odpovídající velikost, je připojený ke správné síti a běží.
5. Po ověření vyčistí převzetí služeb při selhání a zaznamenají a uloží případné poznámky.

### <a name="run-a-failover"></a>Spuštění převzetí služeb při selhání

1. Po ověření toho, jestli testovací převzetí služeb při selhání funguje podle očekávání, vytvoří správci společnosti Contoso plán obnovení pro migraci a přidají do něj virtuální počítač WEBVM.

     ![Plán obnovení](./media/contoso-migration-rehost-vm-sql-ag/recovery-plan.png)

2. V rámci plánu spustí převzetí služeb při selhání. Zvolí nejnovější bod obnovení a určí, že se má Site Recovery před aktivací převzetí služeb při selhání pokusit o vypnutí místního virtuálního počítače.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-vm-sql-ag/failover1.png)

3. Po převzetí služeb při selhání ověří, jestli se virtuální počítač Azure zobrazuje na webu Azure Portal podle očekávání.

    ![Plán obnovení](./media/contoso-migration-rehost-vm-sql-ag/failover2.png)

4. Po ověření virtuálního počítače v Azure dokončí migraci. Tím se ukončí proces migrace, zastaví se replikace virtuálního počítače a zastaví se fakturace služby Site Recovery pro virtuální počítač.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-vm-sql-ag/failover3.png)

### <a name="update-the-connection-string"></a>Aktualizace připojovacího řetězce

V posledním kroku tohoto procesu migrace správci společnosti Contoso aktualizují v aplikaci připojovací řetězec tak, aby odkazoval na migrovanou databázi v naslouchacím procesu SHAOG. Tato konfigurace se změní na virtuálním počítači WEBVM, který teď běží v Azure. Tato konfigurace se nachází v souboru web.config aplikace ASP.

1. Vyhledejte soubor na adrese C:\inetpub\SmartHotelWeb\web.config. Změňte název serveru tak, aby odrážel plně kvalifikovaný název domény AOG: shaog.contoso.com.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-vm-sql-ag/failover4.png)

2. Po aktualizaci a uložení souboru restartují na virtuálním počítači WEBVM službu IIS. Provedou to spuštěním příkazu IISRESET /RESTART na příkazovém řádku.
3. Po restartování služby IIS teď aplikace používá databázi běžící na spravované instanci SQL.

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) o spuštění testovacího převzetí služeb při selhání
- [Informace](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans) o vytvoření plánu obnovení
- [Informace](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) o převzetí služeb při selhání do Azure

### <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace je aplikace SmartHotel360 spuštěná na virtuálním počítači Azure a databáze SmartHotel360 se nachází v clusteru Azure SQL.

Společnost Contoso teď potřebuje provést tyto kroky čištění:

- Odebrat místní virtuální počítače z inventáře vCenter
- Odebrat virtuální počítače z úloh místního zálohování
- Aktualizovat interní dokumentaci tak, aby obsahovala nová umístění a IP adresy virtuálních počítačů
- Zkontrolovat všechny prostředky, které s vyřazenými virtuálními počítači spolupracují, a aktualizovat veškeré související nastavení nebo dokumentaci tak, aby odrážely novou konfiguraci
- Přidat dva nové virtuální počítače (SQLAOG1 a SQLAOG2) do produkčních monitorovacích systémů.

### <a name="review-the-deployment"></a>Revize nasazení

Teď, když má prostředky migrované do Azure, společnost Contoso potřebuje plně zprovoznit a zabezpečit novou infrastrukturu.

### <a name="security"></a>Zabezpečení

Bezpečnostní tým společnosti Contoso zkontroluje virtuální počítače Azure WEBVM, SQLAOG1 a SQLAOG2 a určí případné problémy se zabezpečením.

- V rámci řízení přístupu tým zkontroluje skupiny zabezpečení sítě pro virtuální počítač. Skupiny zabezpečení sítě zajišťují, aby se k aplikaci dostal jen povolený provoz.
- Tým zváží zabezpečení dat na disku pomocí služeb Azure Disk Encryption a Key Vault.
- Tým by měl vyhodnotit transparentní šifrování dat a pak ho povolit v databázi SmartHotel360 běžící v nové skupině dostupnosti SQL. [Další informace](/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017).

Další informace najdete v tématu [osvědčené postupy zabezpečení pro úlohy IaaS v Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="bcdr"></a>BCDR

V zájmu zajištění provozní kontinuity a zotavení po havárii (BCDR) společnost Contoso provede tyto akce:

- Společnost Contoso zálohuje data na virtuální počítače s WEBVM, SQLAOG1 a SQLAOG2 pomocí služby Azure Backup, aby se zajistila bezpečnost dat. [Další informace](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Společnost Contoso se také naučí, jak pomocí služby Azure Storage zálohovat SQL Server přímo do úložiště objektů blob. [Další informace](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-use-storage-sql-server-backup-restore).
- Aby se aplikace udržovaly v provozu, společnost Contoso replikuje virtuální počítače aplikace v Azure do sekundární oblasti pomocí Site Recovery. [Další informace](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

1. Společnost Contoso má stávající licence pro virtuální počítač WEBVM a bude využívat Zvýhodněné hybridní využití Azure. Společnost Contoso převede stávající virtuální počítače Azure, aby mohla tyto ceny využít.
2. Contoso povolí službu Azure Cost Management licencovanou Cloudynem, dceřinou společností Microsoftu. Jedná se o multicloudové řešení správy nákladů, které pomáhá využívat a spravovat Azure a další cloudové prostředky. [Další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management

## <a name="conclusion"></a>Závěr

V tomto článku společnost Contoso změnila hostitele aplikace SmartHotel360 v Azure migrací front-endového virtuálního počítače aplikace do Azure pomocí služby Site Recovery. Společnost Contoso migrovala databázi aplikace do clusteru SQL Serveru zřízeného v Azure a zabezpečila ho ve skupině dostupnosti AlwaysOn pro SQL Server.
