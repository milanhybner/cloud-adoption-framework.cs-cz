---
title: Změna hostitele linuxové aplikace technické podpory na Azure a Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak Contoso mění hostitele místní linuxové aplikaci tím, že ji migruje do virtuálních počítačů Azure a Azure Database for MySQL.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3e39452782f1966e0efe2742264d26a60062d78b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547326"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms-and-azure-database-for-mysql"></a>Změna hostitele místní linuxové aplikace na virtuální počítače Azure a Azure Database for MySQL

V tomto článku se dozvíte, jak fiktivní firma Contoso mění hostitele dvouvrstvé linuxové aplikace Apache/MySQL/PHP (LAMP) tím, že ji migruje z místního prostředí do Azure s využitím virtuálních počítačů Azure a Azure Database for MySQL.

Aplikace technické podpory osTicket používaná v tomto příkladu se poskytuje jako open source. Pokud ji chcete použít pro vlastní testování, můžete si ji stáhnout z [GitHubu](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s obchodními partnery, aby zjistil, čeho chtějí dosáhnout:

- **Řešení obchodního růstu.** Contoso roste, čímž vzniká tlak na místní systémy a infrastrukturu.
- **Omezení rizik.** Aplikace oddělení služeb je pro firmu velmi důležitá. Contoso ji chce přesunout do Azure s nulovým rizikem.
- **Rozšíření.** Společnost Contoso teď nechce aplikaci měnit. Stačí, aby tato aplikace dál zůstala stabilní.

## <a name="migration-goals"></a>Cíle migrace

Cloudový tým Contoso vytyčil cíle pro tuto migraci, aby bylo možné určit nejlepší způsob migrace:

- Po dokončení migrace by aplikace v Azure měla mít stejné možnosti z hlediska výkonu, jaké má dnes v místním prostředí VMware. Aplikace bude v cloudu nadále stejně důležitá, jako je dnes v místním prostředí.
- Společnost Contoso nechce investovat do této aplikace. Aplikace je pro firmu důležitá, ale Contoso ji zatím chce jen ve stávající podobě bezpečně přesunout do cloudu.
- Po dokončení několika migrací aplikací pro Windows se společnost Contoso chce dozvědět, jak v Azure využívat infrastrukturu založenou na platformě Linux.
- Po přesunu aplikace do cloudu chce Contoso minimalizovat úlohy správce databáze.

## <a name="proposed-architecture"></a>Navrhovaná architektura

V tomto scénáři:

- Aplikace obsahuje úrovně rozdělené mezi dva virtuální počítače (`OSTICKETWEB` a `OSTICKETMYSQL`).
- Virtuální počítače jsou umístěné na hostiteli VMware ESXi `contosohost1.contoso.com` (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (`vcenter.contoso.com`) spuštěný na virtuálním počítači.
- Contoso má místní datacentrum (`contoso-datacenter`) s místním řadičem domény (`contosodc1`).
- Webová vrstva aplikace pro `OSTICKETWEB` se bude migrovat do virtuálního počítače Azure IaaS.
- Databáze aplikace se bude migrovat do služby Azure Database for MySQL PaaS.
- Vzhledem k tomu, že Contoso migruje produkční úlohu, budou prostředky Azure umístěné ve skupině produkčních prostředků `ContosoRG`.
- Prostředky se budou replikovat do primární oblasti (Východní USA 2) a umístí se do produkční sítě (`VNET-PROD-EUS2`):
  - Webový virtuální počítač bude umístěný ve front-endové podsíti (`PROD-FE-EUS2`).
  - Instance databáze bude umístěná v podsíti databáze (`PROD-DB-EUS2`).
- Databáze aplikace se bude do služby Azure Database for MySQL migrovat pomocí nástrojů MySQL.
- Po dokončení migrace se místní virtuální počítače v datacentru Contoso vyřadí z provozu.

![Architektura scénáře](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Proces migrace

Contoso dokončí proces migrace následujícím způsobem:

Migrace webového virtuálního počítače:

1. Jako první krok Contoso nastaví místní infrastrukturu a infrastrukturu Azure potřebnou k nasazení Site Recovery.
2. Po přípravě Azure a místních komponent Contoso nastaví a povolí replikaci pro webový virtuální počítač.
3. Až se rozběhne replikace, Contoso provede migraci virtuálního počítače tak, že Azure převezme jejich služby při selhání.

Postup při migraci databáze:

1. Společnost Contoso zřídí instanci MySQL v Azure.
2. Contoso nastaví MySQL Workbench a zazálohuje databázi místně.
3. Potom obnoví databázi z místní zálohy do Azure.

![Proces migrace](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Služba orchestruje a spravuje migraci a zotavení po havárii pro virtuální počítače Azure a místní virtuální počítače a fyzické servery. | Během replikace do Azure se účtují poplatky za Azure Storage. Vytvoří se virtuální počítače Azure a při převzetí služeb při selhání se za ně účtují poplatky. [Další informace](https://azure.microsoft.com/pricing/details/site-recovery) o poplatcích a cenách
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Tato databáze je založená na opensourcovém stroji MySQL Server. Poskytuje plně spravovanou podnikovou komunitní databázi MySQL jako službu pro vývoj a nasazení aplikací.

## <a name="prerequisites"></a>Předpoklady

Tady je seznam toho, co Contoso k realizaci tohoto scénáře potřebuje.

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Společnost Contoso vytvořila předplatná v jednom z předchozích článků. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.<br/><br/> Pokud potřebujete podrobnější oprávnění, přečtěte si [tento článek](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura Azure** | Společnost Contoso nastaví infrastrukturu Azure podle popisu v článku [Infrastruktura Azure pro migraci](./contoso-migration-infrastructure.md).<br/><br/> Přečtěte si další informace o konkrétních požadavcích na [síť](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) a [úložiště](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage) pro Site Recovery.
**Místní servery** | Místní servery vCenter by měly používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Hostitel ESXi by měl používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Na hostiteli ESXi by měl být spuštěný jeden nebo více virtuálních počítačů VMware.
**Místní virtuální počítače** | [Projděte si požadavky na linuxové virtuální počítače](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#replicated-machines), u kterých se podporuje migrace s využitím Site Recovery.<br/><br/> Ověřte podporované [linuxové souborové a úložné systémy](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#linux-file-systemsguest-storage).<br/><br/> Virtuální počítače musí splňovat [požadavky Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Správci Contoso provedou migraci tímto způsobem:

> [!div class="checklist"]
>
> - **Krok 1: Příprava Azure na Site Recovery.** Vytvoří účet úložiště Azure, ve kterém se budou uchovávat replikovaná data, a vytvoří trezor služby Recovery Services.
> - **Krok 2: Příprava místního VMware pro Site Recovery.** Připraví účty pro zjišťování virtuálních počítačů a instalaci agenta a připraví se na připojení virtuálních počítačů Azure po převzetí služeb při selhání.
> - **Krok 3: zřízení databáze.** V Azure zřídí instanci Azure Database for MySQL.
> - **Krok 4: replikace virtuálních počítačů** Nakonfigurují zdrojové a cílové prostředí služby Site Recovery, nastaví zásady replikace a zahájí replikaci virtuálních počítačů do služby Azure Storage.
> - **Krok 5: migrace databáze.** Nastaví migraci s využitím nástrojů MySQL.
> - **Krok 6: migrace virtuálních počítačů pomocí Site Recovery.** Nakonec provedou testovací převzetí služeb při selhání, aby zkontrolovali, jestli všechno funguje, a pak spustí úplné převzetí služeb při selhání, během kterého proběhne migrace virtuálních počítačů do Azure.

## <a name="step-1-prepare-azure-for-the-site-recovery-service"></a>Krok 1: Příprava Azure na službu Site Recovery

Pro Site Recovery Contoso potřebuje několik komponent Azure:

- Virtuální síť, která bude obsahovat prostředky po převzetí služeb při selhání. Společnost Contoso už tuto virtuální síť vytvořila během [nasazení infrastruktury Azure](./contoso-migration-infrastructure.md).
- Nový účet úložiště Azure, ve kterém se budou uchovávat replikovaná data.
- Trezor služby Recovery Services v Azure

Správci společnosti Contoso vytvoří účet úložiště a trezor následujícím způsobem:

1. Vytvoří účet úložiště (**contosovmsacc20180528**) v oblasti Východní USA 2.

    - Účet úložiště musí být ve stejné oblasti jako trezor služby Recovery Services.
    - Použijí účet pro obecné účely se standardním úložištěm a replikaci LRS.

    ![Úložiště služby Site Recovery](./media/contoso-migration-rehost-linux-vm-mysql/asr-storage.png)

2. Společnost Contoso má připravenou síť a účet úložiště a teď vytvoří trezor (ContosoMigrationVault) a umístí ho do skupiny prostředků **ContosoFailoverRG** v primární oblasti Východní USA 2.

    ![Trezor služby Recovery Services](./media/contoso-migration-rehost-linux-vm-mysql/asr-vault.png)

**Potřebujete další pomoc?**

[Přečtěte si](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure) o nastavení Azure pro Site Recovery.

## <a name="step-2-prepare-on-premises-vmware-for-site-recovery"></a>Krok 2: Příprava místního VMware pro Site Recovery

Správci společnosti Contoso připraví místní infrastrukturu VMware následujícím způsobem:

- Na serveru vCenter vytvoří účet pro automatizaci zjišťování virtuálních počítačů.
- Vytvoří účet, který umožní automatickou instalaci služby Mobility na virtuálních počítačích VMware, které se budou replikovat.
- Připraví místní virtuální počítače, aby se daly připojit k virtuálním počítačům Azure vytvořeným po dokončení migrace.

### <a name="prepare-an-account-for-automatic-discovery"></a>Příprava účtu pro automatické zjišťování

Site Recovery potřebuje přístup k serverům VMware z těchto důvodů:

- Automatické zjišťování virtuálních počítačů. Vyžaduje se alespoň účet jen pro čtení.
- Orchestrace replikace, převzetí služeb při selhání a navrácení služeb po obnovení. Potřebujete účet, který může spouštět operace, jako jsou vytváření a odebírání disků a zapínání virtuálních počítačů.

Správci společnosti Contoso nastaví účet následujícím způsobem:

1. Vytvoří roli na úrovni vCenter.
2. Potom této roli přiřadí požadovaná oprávnění.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Příprava účtu pro instalaci služby Mobility

Na každém virtuálním počítači, na který chce Contoso replikovat, musí být nainstalovaná služba Mobility.

- Když povolíte replikaci virtuálních počítačů, Site Recovery může automaticky provést nabízenou instalaci této komponenty.
- Pro automatickou instalaci Site Recovery potřebuje účet s oprávněními pro přístup k virtuálnímu počítači.
- Podrobnosti účtu se zadávají během nastavení replikace.
- Účet může být doménový nebo místní, pokud má oprávnění k instalaci.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Příprava připojení k virtuálním počítačům Azure po převzetí služeb při selhání

Po převzetí služeb při selhání do Azure chce společnost Contoso mít možnost se připojit k virtuálním počítačům Azure. Proto musí správci Contoso provést tyto kroky:

- Pokud chtějí mít přístup přes internet, před zahájením migrace na místním linuxovém virtuálním počítači povolí SSH. Ubuntu to můžete provést pomocí následujícího příkazu: **sudo apt-get SSH Install-y**.
- Po převzetí služeb při selhání by měli zkontrolovat **diagnostiku spuštění** a zobrazit si snímek obrazovky virtuálního počítače.
- Pokud to nefunguje, musí zkontrolovat, jestli je virtuální počítač spuštěný, a projít si tyto [tipy pro řešení potíží](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) o vytváření a přiřazování rolí pro automatické zjišťování
- [Informace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) o vytvoření účtu pro nabízenou instalaci služby Mobility Service

## <a name="step-3-provision-azure-database-for-mysql"></a>Krok 3: zřízení Azure Database for MySQL

Správci Contoso zřídí v primární oblasti Východní USA 2 instanci databáze MySQL.

1. Na webu Azure Portal vytvoří prostředek Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

2. Přidají k databázi Azure název **contosoosticket**. Přidají tuto databázi do produkční skupiny prostředků **ContosoRG** a zadají pro ni přihlašovací údaje.
3. Místní databáze MySQL je verze 5.7, takže tuto verzi vyberou pro zajištění kompatibility. Použijí výchozí velikosti, které odpovídají jejich požadavkům na databázi.

     ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

4. Jako **Možnosti redundance zálohy** vyberou **Geograficky redundantní**. Tato možnost jim v případě výpadku umožňuje obnovit databázi v sekundární oblasti Střední USA. Tuto možnost mohou nakonfigurovat jenom při zřizování databáze.

     ![Redundance](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

5. U sítě **VNET-PROD-EUS2** v části **Koncové body služby** přidají koncový bod služby (podsíť databáze) pro službu SQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

6. Po přidání podsítě vytvoří pravidlo virtuální sítě, které umožňuje přístup z podsítě databáze v produkční síti.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-4-replicate-the-on-premises-vms"></a>Krok 4: replikace místních virtuálních počítačů

Než budou moct správci společnosti Contoso migrovat webový virtuální počítač do Azure, musí nastavit a povolit replikaci.

### <a name="set-a-protection-goal"></a>Nastavení cíle ochrany

1. V trezoru pod názvem trezoru (ContosoVMVault) nastaví cíl replikace (**Začínáme** > **Site Recovery** > **Připravit infrastrukturu**).
2. Určí, že se počítače nacházejí v místním prostředí, že se jedná o virtuální počítače VMware a že chtějí replikovat do Azure.

    ![Cíl replikace](./media/contoso-migration-rehost-linux-vm-mysql/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Potvrzení plánování nasazení

Dále potvrdí, že provedli plánování nasazení, a to výběrem možnosti **Ano, mám to hotové**. V tomto scénáři provádí Contoso migraci jen jednoho virtuálního počítače a plánování nasazení nepotřebuje.

### <a name="set-up-the-source-environment"></a>Nastavení zdrojového prostředí

Správci společnosti Contoso teď nakonfigurují zdrojové prostředí. Pomocí šablony OVF nasadí konfigurační server Site Recovery jako místní virtuální počítač VMware s vysokou dostupností. Po nastavení a spuštění zaregistrují konfigurační server v trezoru.

Konfigurační server spustí několik komponent:

- Komponenta konfiguračního serveru, která koordinuje komunikaci mezi místním prostředím a Azure a spravuje replikaci dat.
- Procesový server, který funguje jako replikační brána. Přijímá data replikace, optimalizuje je pomocí ukládání do mezipaměti, komprese a šifrování a odesílá je do úložiště Azure.
- Procesový server také na všechny virtuální počítače, které chcete replikovat, nainstaluje službu mobility a automaticky vyhledá místní virtuální počítače VMware.

Správci společnosti Contoso přitom postupují takto:

1. Stáhnou si šablonu OVF z části **Připravit infrastrukturu** > **Zdroj** > **Konfigurační server**.

    ![Stažení souboru OVF](./media/contoso-migration-rehost-linux-vm-mysql/add-cs.png)

2. Tuto šablonu naimportují do VMware, aby došlo k vytvoření virtuálního počítače, a tento virtuální počítač nasadí.

    ![Šablona OVF](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-wizard.png)

3. Při prvním zapnutí virtuálního počítače se spustí prostředí instalace systému Windows Server 2016. Přijmou licenční smlouvu a zadají heslo správce.
4. Po dokončení instalace se přihlásí k virtuálnímu počítači jako správce. Při prvním přihlášení se automaticky spustí nástroj pro konfiguraci služby Azure Site Recovery.
5. V nástroji zadají název, který se má použít pro registraci konfiguračního serveru v trezoru.
6. Nástroj zkontroluje, jestli se virtuální počítač může připojit k Azure.
7. Po navázání připojení se správci přihlásí k předplatnému Azure. Přihlašovací údaje musí umožňovat přístup k trezoru, do kterého chtějí konfigurační server zaregistrovat.

    ![Registrace konfiguračního serveru](./media/contoso-migration-rehost-linux-vm-mysql/config-server-register2.png)

8. Nástroj provede několik úloh konfigurace a pak restartuje počítač.
9. Znovu se přihlásí k počítači a automaticky se spustí průvodce správou konfiguračního serveru.
10. V průvodci vyberou síťovou kartu pro příjem dat přenášených při replikaci. Po dokončení konfigurace není možné toto nastavení změnit.
11. Vyberou předplatné, skupinu prostředků a trezor, ve kterém se má konfigurační server zaregistrovat.

    ![Trezor](./media/contoso-migration-rehost-linux-vm-mysql/cswiz1.png)

12. Potom stáhnou a nainstalují MySQL Server a VMware PowerCLI.
13. Po ověření zadají plně kvalifikovaný název domény nebo IP adresu serveru vCenter nebo hostitele vSphere. Ponechají výchozí port a zadají popisný název serveru vCenter.
14. Zadají účet, který vytvořili pro automatické zjišťování, a přihlašovací údaje, které Site Recovery použije k automatické instalaci služby Mobility Service.

    ![vCenter](./media/contoso-migration-rehost-linux-vm-mysql/cswiz2.png)

15. Po dokončení registrace zkontrolují na webu Azure Portal, jestli je ve vybraném trezoru na stránce **Zdroj** uvedený konfigurační server a server VMware. Zjišťování může trvat 15 minut nebo i více.
16. Když je všechno připravené, Site Recovery se připojí k serverům VMware a vyhledá virtuální počítače.

### <a name="set-up-the-target"></a>Nastavení cíle

Teď správci společnosti Contoso určí nastavení cíle replikace.

1. V části **Připravit infrastrukturu** > **Cíl** zvolí nastavení cíle.
2. Site Recovery zkontroluje, jestli je v zadaném cílovém umístění účet úložiště Azure a síť.

### <a name="create-a-replication-policy"></a>Vytvoření zásady replikace

Když jsou zdroj i cíl nastavené, jsou správci společnosti Contoso připravení vytvořit zásadu replikace.

1. V části **Připravit infrastrukturu** > **Nastavení replikace** > **Zásady replikace** >  **Vytvořit a přidružit** vytvoří zásadu **ContosoMigrationPolicy**.

2. Použijí výchozí nastavení:
    - **Prahová hodnota cíle RPO:** Výchozí hodnota je 60 minut. Tato hodnota určuje, jak často se tvoří body obnovení. Když průběžná replikace překročí tento limit, vygeneruje se upozornění.
    - **Uchování bodu obnovení:** Výchozí hodnota je 24 hodin. Tato hodnota určuje délku intervalu uchovávání dat pro jednotlivé body obnovení. Replikované virtuální počítače můžete v rámci okna uchování obnovit do libovolného časového bodu.
    - **Frekvence snímků konzistentní vzhledem k aplikacím:** Výchozí hodnota je jedna hodina. Tato hodnota určuje četnost vytváření snímků konzistentních vzhledem k aplikacím.

        ![Vytvoření zásady replikace](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy.png)

3. Tato zásada se automaticky přidruží ke konfiguračnímu serveru.

    ![Přidružení zásady replikace](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy2.png)

**Potřebujete další pomoc?**

- Podrobný popis všech těchto kroků najdete v článku [Nastavení zotavení po havárii pro místní virtuální počítače VMware](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- K dispozici jsou také podrobné pokyny, které vám pomůžou [nastavit zdrojové prostředí](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [nasadit konfigurační server](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) a [nakonfigurovat nastavení replikace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).
- [Další informace](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux) o hostovaném agentovi Azure pro Linux

### <a name="enable-replication-for-the-web-vm"></a>Povolení replikace pro webový virtuální počítač

Teď můžou správci společnosti Contoso zahájit replikaci virtuálního počítače **OSTICKETWEB**.

1. V části **Replikovat aplikaci** > **Zdroj** >  **+Replikovat** vyberou nastavení zdroje.
2. Určí, že chtějí povolit virtuální počítače a vyberou nastavení zdroje, včetně vCenter Serveru, a konfigurační server.

    ![Povolení replikace](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication-source.png)

3. Teď určí nastavení cíle. Patří mezi ně skupina prostředků a síť, ve kterých bude virtuální počítač Azure umístěný po převzetí služeb při selhání, a účet úložiště, do kterého se budou ukládat replikovaná data.

     ![Povolení replikace](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication2.png)

4. Pro replikaci vyberou **OSTICKETWEB**.

    ![Povolení replikace](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication3.png)

5. Ve vlastnostech virtuálního počítače vyberou účet, který se má použít k automatické instalaci služby Mobility Service na virtuálním počítači.

     ![Služba Mobility](./media/contoso-migration-rehost-linux-vm-mysql/linux-mobility.png)

6. V části **Nastavení replikace** > **Konfigurace nastavení replikace** zkontrolují, jestli je použitá správná zásada replikace, a vyberou **Povolit replikaci**. Služba Mobility se nainstaluje automaticky.
7. V části **Úlohy** sledují průběh replikace. Po spuštění úlohy **Dokončit ochranu** je počítač připravený k převzetí služeb při selhání.

**Potřebujete další pomoc?**

Podrobný popis všech těchto kroků najdete v článku [Povolení replikace](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-5-migrate-the-database"></a>Krok 5: migrace databáze

Správci Contoso migrují databázi pomocí zálohování a obnovení s využitím nástrojů MySQL. Nainstalují MySQL Workbench, zálohují databázi z počítače OSTICKETMYSQL a pak ji obnoví na server Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Instalace aplikace MySQL Workbench

1. Zkontrolují [předpoklady a stáhnou MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Nainstalují MySQL Workbench pro Windows podle [pokynů k instalaci](https://dev.mysql.com/doc/workbench/en/wb-installing.html).
3. V nástroji MySQL Workbench vytvoří připojení MySQL k počítači OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

4. Exportují databázi jako **osticket** do místního samostatného souboru.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

5. Po dokončení místního zálohování databáze vytvoří připojení k instanci Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

6. Teď mohou ze samostatného souboru naimportovat (obnovit) databázi do této instance Azure Database for MySQL. Pro instanci se vytvoří nové schéma (osticket).

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

## <a name="step-6-migrate-the-vms-with-site-recovery"></a>Krok 6: migrace virtuálních počítačů pomocí Site Recovery

Správci společnosti Contoso spustí rychlé testování převzetí služeb při selhání a potom migrují virtuální počítače.

### <a name="run-a-test-failover"></a>Spuštění testovacího převzetí služeb při selhání

Spuštění testovacího převzetí služeb při selhání pomáhá ověřit, jestli před migrací všechno funguje podle očekávání.

1. Spustí testovací převzetí služeb při selhání k nejnovějšímu dostupnému bodu v čase (**Nejnovější zpracovaný**).
2. Vyberou **Před spuštěním převzetí služeb při selhání vypnout počítač**, takže se Site Recovery pokusí před aktivací převzetí služeb při selhání vypnout zdrojový virtuální počítač. Převzetí služeb při selhání bude pokračovat i v případě, že se vypnutí nepovede.
3. Spustí se testovací převzetí služeb při selhání:

    - Spustí se kontrola předpokladů, která zjistí, jestli jsou splněné všechny podmínky pro migraci.
    - Převzetí služeb při selhání tato data zpracuje, aby se mohl vytvořit virtuální počítač Azure. Pokud jste vybrali nejnovější bod obnovení, vytvoří se z těchto dat nový.
    - Pomocí dat zpracovaných v předchozím kroku se vytvoří virtuální počítač Azure.

4. Po dokončení převzetí služeb při selhání se na portálu Azure Portal objeví replika virtuálního počítače Azure. Zkontrolují, že virtuální počítač má odpovídající velikost, je připojený ke správné síti a běží.
5. Po ověření vyčistí převzetí služeb při selhání a zaznamenají a uloží případné poznámky.

### <a name="migrate-the-vm"></a>Migrace virtuálního počítače

Pro migraci virtuálního počítače vytvoří správci společnosti Contoso plán obnovení, který zahrnuje virtuální počítač, a provedou převzetí služeb při selhání plánu do Azure.

1. Vytvoří plán a přidají do něj **OSTICKETWEB**.

    ![Plán obnovení](./media/contoso-migration-rehost-linux-vm-mysql/recovery-plan.png)

2. V rámci plánu spustí převzetí služeb při selhání. Zvolí nejnovější bod obnovení a určí, že se má Site Recovery před aktivací převzetí služeb při selhání pokusit o vypnutí místního virtuálního počítače. Průběh převzetí služeb při selhání můžou sledovat na stránce **Úlohy**.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-linux-vm-mysql/failover1.png)

3. Během převzetí služeb při selhání vCenter Server vydá příkazy k zastavení dvou virtuálních počítačů spuštěných na hostiteli ESXi.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-failover.png)

4. Po převzetí služeb při selhání ověří, jestli se virtuální počítač Azure zobrazuje na webu Azure Portal podle očekávání.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-linux-vm-mysql/failover2.png)

5. Po kontrole virtuálního počítače dokončí migraci. Tím se zastaví replikace tohoto virtuálního počítače a zastaví se pro něj i fakturace služby Site Recovery.

    ![Převzetí služeb při selhání](./media/contoso-migration-rehost-linux-vm-mysql/failover3.png)

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) o spuštění testovacího převzetí služeb při selhání
- [Informace](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans) o vytvoření plánu obnovení
- [Informace](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) o převzetí služeb při selhání do Azure

### <a name="connect-the-vm-to-the-database"></a>Připojení virtuálního počítače k databázi

V posledním kroku tohoto procesu migrace správci společnosti Contoso aktualizují připojovací řetězec aplikace tak, aby odkazoval na Azure Database for MySQL.

1. S využitím Putty nebo jiného klienta SSH vytvoří připojení SSH k virtuálnímu počítači OSTICKETWEB VM. Virtuální počítač je privátní, takže se připojují pomocí privátní IP adresy.

    ![Připojení k databázi](./media/contoso-migration-rehost-linux-vm-mysql/db-connect.png)

    ![Připojení k databázi](./media/contoso-migration-rehost-linux-vm-mysql/db-connect2.png)

2. Aktualizují nastavení tak, aby virtuální počítač **OSTICKETWEB**mohl komunikovat s databází **OSTICKETMYSQL**. V současné době je tato konfigurace pevně zakódovaná s místní IP adresou 172.16.0.43.

    **Před aktualizací:**

    ![Aktualizace IP adresy](./media/contoso-migration-rehost-linux-vm-mysql/update-ip1.png)

    **Po aktualizaci:**

    ![Aktualizace IP adresy](./media/contoso-migration-rehost-linux-vm-mysql/update-ip2.png)

    ![Aktualizace IP adresy](./media/contoso-migration-rehost-linux-vm-mysql/update-ip3.png)

3. Restartují službu pomocí **systemctl restart apache2**.

    ![Restartování](./media/contoso-migration-rehost-linux-vm-mysql/restart.png)

4. Nakonec aktualizují záznamy DNS pro **OSTICKETWEB**, a to na jenom z řadičů domény Contoso.

    ![Aktualizace DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace běží vrstvy aplikace osTicket na virtuálních počítačích Azure.

Teď Contoso musí provést tyto akce:

- Odebrat virtuální počítače VMware z inventáře vCenter.
- Odebrat místní virtuální počítače z místních zálohovacích úloh
- Aktualizovat interní dokumentaci o nová umístění a IP adresy.
- Zkontrolovat všechny prostředky, které spolupracují s místními virtuálními počítači, a aktualizovat všechna související nastavení nebo dokumentaci tak, aby odrážely novou konfiguraci.
- Společnost Contoso využila službu Azure Migrate s mapováním závislostí k posouzení virtuálního počítače **OSTICKETWEB** z hlediska migrace. Nyní by měli odebrat agenty (Microsoft Monitoring Agent a agenta Microsoft Dependency Agent), které jsou pro tento účel nainstalovány, z virtuálního počítače.

## <a name="review-the-deployment"></a>Revize nasazení

Aplikace je teď spuštěná a firma Contoso ji teď potřebuje v nové infrastruktuře plně zprovoznit a zabezpečit.

### <a name="security"></a>Zabezpečení

Tým zabezpečení Contoso kontroluje virtuální počítač a data aplikaci a zjišťuje případné problémy se zabezpečením.

- V rámci řízení přístupu pro tento virtuální počítač kontrolují skupiny zabezpečení sítě. Skupiny zabezpečení sítě zajišťují, aby se k aplikaci dostal jen povolený provoz.
- Zvažují také zabezpečení dat na discích virtuálních počítačů pomocí služeb Disk Encryption a Azure Key Vault.
- Komunikace mezi virtuálním počítačem a instancí databáze není nakonfigurovaná pro SSL. Touto konfigurací bude potřeba zajistit, aby provoz databáze nebylo možné prolomit.

[Přečtěte si víc](https://docs.microsoft.com/azure/security/azure-security-best-practices-vms) o postupech zabezpečení pro virtuální počítače.

### <a name="bcdr"></a>BCDR

V zájmu zajištění provozní kontinuity a zotavení po havárii společnost Contoso provede tyto akce:

- **Zajištění bezpečnosti dat:** Společnost Contoso zazálohuje data na virtuálním počítači aplikace pomocí služby Azure Backup. [Další informace](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nepotřebují konfigurovat zálohování databáze. Azure Database for MySQL automaticky vytváří a ukládá zálohy serveru. U databáze se používá geografická redundance, takže je odolná a připravená k produkci.
- **Zajištění nepřetržitého provozu aplikací:** Společnost Contoso replikuje virtuální počítače aplikace v Azure do sekundární oblasti pomocí Site Recovery. [Další informace](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- Po nasazení prostředků společnost Contoso přiřadí značky Azure, a to v souladu s rozhodnutími, které udělala během nasazení [infrastruktury Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- U serverů Ubuntu nejsou žádné licenční problémy.
- Contoso povolí službu Azure Cost Management licencovanou Cloudynem, dceřinou společností Microsoftu. Jedná se o multicloudové řešení správy nákladů, které pomáhá využívat a spravovat Azure a další cloudové prostředky. [Další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management
