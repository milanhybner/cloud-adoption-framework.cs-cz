---
title: Změna hostitele místní linuxové aplikace na virtuální počítače Azure
description: Přečtěte si, jak Contoso mění hostitele místní linuxové aplikaci tím, že migruje do virtuálních počítačů Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: b629cc932b54b7ef7c633cefc847ac3263477674
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807338"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms"></a>Změna hostitele místní linuxové aplikace na virtuální počítače Azure

V tomto článku se dozvíte, jak fiktivní společnost Contoso mění hostitele dvouvrstvé linuxové aplikace Apache MySQL PHP (LAMP) s využitím virtuálních počítačů Azure IaaS.

Aplikace technické podpory osTicket používaná v tomto příkladu je poskytována jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s obchodními partnery, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Contoso roste, čímž vzniká tlak na místní systémy a infrastrukturu.
- **Omezení rizik.** Aplikace technické podpory je pro společnost Contoso velmi důležitá. Contoso ji chce přesunout do Azure s nulovým rizikem.
- **Rozšíření.** Společnost Contoso teď nechce aplikaci měnit. Stačí jí zajistit, aby byla aplikace stabilní.

## <a name="migration-goals"></a>Cíle migrace

Cloudový tým Contoso vytyčil cíle pro tuto migraci, aby bylo možné určit nejlepší způsob migrace:

- Po dokončení migrace by aplikace v Azure měla mít stejné možnosti z hlediska výkonu, jaké má dnes v místním prostředí VMware. Aplikace bude v cloudu nadále stejně důležitá, jako je dnes v místním prostředí.
- Společnost Contoso nechce investovat do této aplikace. Aplikace je pro firmu důležitá, ale Contoso ji zatím chce jen ve stávající podobě bezpečně přesunout do cloudu.
- Contoso nechce měnit provozní model aplikace. Contoso bude chtít pracovat s aplikací v cloudu stejným způsobem jako dosud.
- Contoso nechce měnit žádné funkce aplikace. Změní se jenom umístění aplikace.
- Po dokončení několika migrací aplikací pro Windows se společnost Contoso chce dozvědět, jak v Azure využívat infrastrukturu založenou na platformě Linux.

## <a name="solution-design"></a>Návrh řešení

Po dokončení podrobné specifikace cílů a požadavků Contoso navrhne a zkontroluje řešení nasazení a určí proces migrace, včetně služeb Azure, které se k migraci využijí.

### <a name="current-app"></a>Aktuální aplikace

- Aplikace OSTicket obsahuje úrovně rozdělené mezi dva virtuální počítače (**OSTICKETWEB** a **OSTICKETMYSQL**).
- Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com** (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) spuštěný na virtuálním počítači.
- Společnost Contoso má místní datacentrum (**contoso-datacenter**) s místním řadičem domény (**contosodc1**).

### <a name="proposed-architecture"></a>Navrhovaná architektura

- Vzhledem k tomu, že se jedná o produkční úlohu, budou se virtuální počítače v Azure nacházet v produkční skupině prostředků **ContosoRG**.
- Virtuální počítače se migrují do primární oblasti (Východní USA 2) a umístí se do produkční sítě (VNET-PROD-EUS2):
  - Webový virtuální počítač bude umístěný ve front-endové podsíti (PROD-FE-EUS2).
  - Virtuální počítač databáze se bude nacházet v databázové podsíti (PROD-DB-EUS2).
- Po dokončení migrace budou místní virtuální počítače v datacentru společnosti Contoso vyřazeny z provozu.

![Architektura scénáře](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Revize řešení

Společnost Contoso vyhodnotí vytvořený návrh sestavením seznamu výhod a nevýhod.

<!-- markdownlint-disable MD033 -->

**Aspekty** | **Podrobnosti**
--- | ---
**Výhody** | Oba virtuální počítače aplikace se přesunou do Azure beze změn, takže bude migrace snadná.<br/><br/> Vzhledem k tomu, že společnost Contoso používá pro virtuální počítače s aplikacemi přístup typu výtah a Shift, nejsou pro databázi aplikací potřeba žádné speciální nástroje pro konfiguraci a migraci.<br/><br/> Contoso bude mít virtuální počítače aplikace v Azure stále plně pod kontrolou. <br/><br/> Virtuální počítače aplikace používají Ubuntu 16.04-TLS, což je schválená distribuce systému Linux. [Další informace](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros).
**Nevýhody** | Webová a datová vrstva aplikace zůstanou jediným bodem převzetí služeb při selhání. <br/><br/> Contoso bude muset dále podporovat aplikaci jako virtuální počítače Azure, místo aby ji přesunula do spravované služby jako Azure App Service a Azure Database for MySQL.<br/><br/> Společnost Contoso si je vědoma, že při migraci virtuálních počítačů typu výtah a Shift nevyužívá plně výhodu funkcí poskytovaných službou [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) (integrovaná vysoká dostupnost, předvídatelný výkon, jednoduché škálování, automatické zálohování a integrované zabezpečení).

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migrace

Společnost Contoso provede migraci následujícím způsobem:

- Společnost Contoso nejprve připraví a nastaví komponenty Azure pro migraci serverů Azure Migrate a připraví místní infrastrukturu VMware.
- Společnost Contoso už má připravenou [infrastrukturu Azure](./contoso-migration-infrastructure.md), takže jí stačí pouze přidat a nakonfigurovat replikaci virtuálních počítačů pomocí nástroje pro migraci serverů Azure Migrate.
- Až bude všechno připravené, může Contoso začít replikovat virtuální počítače.
- Až se rozběhne replikace, Contoso provede migraci virtuálních počítačů tak, že Azure převezme jejich služby při selhání.

![Proces migrace](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[Migrace serverů Azure Migrate](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm) | Tato služba orchestruje a spravuje migraci místních aplikací a úloh a instancí virtuálních počítačů AWS a GCP. | Během replikace do Azure se účtují poplatky za Azure Storage. Vytvoří se virtuální počítače Azure a při převzetí služeb při selhání se za ně účtují poplatky. [Získejte další informace](https://azure.microsoft.com/pricing/details/azure-migrate) o poplatcích a cenách.

## <a name="prerequisites"></a>Požadavky

Tady je seznam toho, co Contoso k realizaci tohoto scénáře potřebuje.

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Společnost Contoso vytvořila předplatná v dřívějším článku v této sérii. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.<br/><br/> Pokud potřebujete podrobnější oprávnění, přečtěte si [tento článek](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura Azure** |  [Přečtěte si](./contoso-migration-infrastructure.md) o tom, jak společnost Contoso nastavila infrastrukturu Azure.<br/><br/> Další informace o konkrétních [požadavcích](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) na migraci serverů Azure Migrate
**Místní servery** | Místní servery vCenter by měly používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Hostitel ESXi by měl používat verzi 5.5, 6.0 nebo 6.5.<br/><br/> Na hostiteli ESXi by měl být spuštěný jeden nebo více virtuálních počítačů VMware.
**Místní virtuální počítače** | [Projděte si počítače s Linuxem](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), které mají schválený provoz v Azure.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Contoso dokončí migraci tímto způsobem:

> [!div class="checklist"]
>
> - **Krok 1: Příprava migrace serveru Azure na Azure Migrate.** Do svého projektu Azure Migrate přidá nástroj pro migraci serverů.
> - **Krok 2: Příprava místní služby VMware na migraci serveru Azure Migrate.** Připraví účty pro zjišťování virtuálních počítačů a připraví se na připojení k virtuálním počítačům Azure po převzetí služeb při selhání.
> - **Krok 3: replikace virtuálních počítačů** Nastaví replikaci a začnou replikovat virtuální počítače do Azure Storage.
> - **Krok 4: migrujte virtuální počítače pomocí migrace serveru Azure Migrate.** Provedou testovací převzetí služeb při selhání, aby zkontrolovali, jestli všechno funguje, a pak spustí úplné převzetí služeb při selhání, během kterého proběhne migrace virtuálních počítačů do Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Krok 1: Příprava Azure na nástroj pro migraci serveru Azure Migrate

Contoso potřebuje k migraci virtuálních počítačů do Azure tyto komponenty Azure:

- Virtuální síť, ve které se budou nacházet virtuální počítače Azure vytvořené během převzetí služeb při selhání
- Zřízený nástroj pro migraci serverů Azure Migrate

Komponenty se vytvoří takto:

1. **Nastavit síť:** Společnost Contoso již nastavila síť, která může být pro Azure Migrate migrace serveru při [nasazení infrastruktury Azure](./contoso-migration-infrastructure.md) .

    - Aplikace SmartHotel360 je produkční aplikace a virtuální počítače se migrují do produkční sítě Azure (VNET-PROD-EUS2) v primární oblasti Východní USA 2.
    - Oba virtuální počítače se umístí do skupiny prostředků ContosoRG, která se používá pro produkční prostředky.
    - Virtuální počítač front-endu aplikace (WEBVM) se migruje do front-endové podsítě (PROD-FE-EUS2) v produkční síti.
    - Virtuální počítač databáze aplikace (SQLVM) se migruje do databázové podsítě (PROD-DB-EUS2) v produkční síti.

2. **Zřízení nástroje pro migraci Azure Migrate serveru:** Když se zařadí síť a účet úložiště, společnost Contoso teď vytvoří trezor Recovery Services (ContosoMigrationVault) a umístí ho do skupiny prostředků ContosoFailoverRG v primární Východní USA 2 oblasti.

    ![Nástroj pro migraci serverů Azure Migrate](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**Potřebujete další pomoc?**

[Informace](https://docs.microsoft.com/azure/migrate) o nastavení nástroje pro migraci serverů Azure Migrate

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Příprava připojení k virtuálním počítačům Azure po převzetí služeb při selhání

Po převzetí služeb při selhání do Azure chce mít společnost Contoso možnost připojit se k replikovaným virtuálním počítačům v Azure. K tomu je potřeba, aby správci společnosti Contoso udělali několik věcí:

- Pokud chtějí přistupovat k virtuálním počítačům Azure přes internet, před zahájením migrace na místním linuxovém virtuálním počítači povolí SSH. Ubuntu to můžete provést pomocí následujícího příkazu: **sudo apt-get SSH Install-y**.
- Po zahájení migrace (převzetí služeb při selhání) můžou zkontrolovat **diagnostiku spuštění** a zobrazit si snímek obrazovky virtuálního počítače.
- Pokud to nefunguje, musí zkontrolovat, jestli je virtuální počítač spuštěný, a projít si tyto [tipy pro řešení potíží](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) o přípravě virtuálních počítačů na migraci

## <a name="step-3-replicate-the-on-premises-vms"></a>Krok 3: replikace místních virtuálních počítačů

Než budou moct správci společnosti Contoso spustit migraci do Azure, musejí nastavit a povolit replikaci.

Po dokončení zjišťování můžete zahájit replikaci virtuálních počítačů VMware do Azure.

1. V Azure Migrate Project > **servery** **Azure Migrate: Migrace serveru**klikněte na **replikovat**.

    ![Replikace virtuálních počítačů](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. V části **Replikovat** > **Nastavení zdroje** > **Máte počítače ve virtuální podobě?** vyberte **Ano, s VMware vSphere**.

3. V části **Místní zařízení** vyberte název zařízení Azure Migrate, které jste nastavili, a klikněte na **OK**.

    ![Nastavení zdroje](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. V části **Virtuální počítače** vyberte počítače, které chcete replikovat.
    - Pokud jste pro virtuální počítače spustili posouzení, můžete použít doporučenou velikost a typ disku (Premium nebo Standard) z výsledků posouzení. Pokud to chcete provést, v části **Importovat nastavení migrace z posouzení Azure Migrate?** vyberte možnost **Ano**.
    - Pokud jste neprovedli posouzení nebo pokud nechcete použít nastavení posouzení, vyberte možnost **Ne**.
    - Pokud jste se rozhodli použít posouzení, vyberte skupinu virtuálních počítačů a název posouzení.

    ![Výběr posouzení](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. V části **Virtuální počítače** vyhledejte požadované virtuální počítače a zkontrolujte všechny virtuální počítače, které chcete migrovat. Pak klikněte na **Další: nastavení cíle**.

6. V části **Nastavení cíle** vyberte předplatné a cílovou oblast migrace a zadejte skupinu prostředků, ve které se po migraci budou nacházet virtuální počítače Azure. V části **Virtuální síť** vyberte virtuální síť a podsíť Azure, ke kterým se po migraci připojí virtuální počítače Azure.

7. V **zvýhodněné hybridní využití Azure**vyberte následující:

    - Vyberte **Ne**, pokud nechcete využít Zvýhodněné hybridní využití Azure. Pak klikněte na tlačítko **Další**.
    - Vyberte **Ano**, pokud máte počítače s Windows Serverem s aktivním Software Assurance nebo předplatným Windows Serveru a u migrovaných počítačů chcete využít tuto výhodu. Pak klikněte na tlačítko **Další**.

8. V části **Výpočetní prostředky** zkontrolujte název, velikost, typ disku s operačním systémem a skupinu dostupnosti virtuálního počítače. Virtuální počítače musí splňovat [požadavky Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements).

    - **Velikost virtuálního počítače:** Pokud používáte doporučení pro vyhodnocení, bude rozevírací seznam velikost virtuálního počítače obsahovat doporučenou velikost. Jinak Azure Migrate vybere velikost na základě nejbližší shody v předplatném Azure. Případně můžete velikost vybrat ručně v části **Velikost virtuálního počítače Azure**.
    - **Disk s operačním systémem:** Zadejte operační systém (spouštěcí) disk pro virtuální počítač. Disk s operačním systémem je disk, který obsahuje spouštěcí zavaděč a instalační program operačního systému.
    - **Skupina dostupnosti:** Pokud má být virtuální počítač v sadě dostupnosti Azure po migraci, zadejte sadu. Skupina musí být v cílové skupině prostředků, kterou pro migraci zadáte.

9. V části **Disky** zadejte, jestli se mají disky virtuálních počítačů replikovat do Azure, a vyberte typ disků (disky SSD nebo HDD úrovně Standard nebo spravované disky úrovně Premium) v Azure. Pak klikněte na tlačítko **Další**.
    - Disky můžete z replikace vyloučit.
    - Pokud disky vyloučíte, po migraci nebudou na virtuálním počítači Azure.

10. V části **Kontrola a zahájení replikace** zkontrolujte nastavení a kliknutím na **Replikovat** spusťte počáteční replikaci serverů.

> [!NOTE]
> Před zahájením replikace můžete nastavení replikace kdykoli aktualizovat v části **Správa** > **Replikace počítačů**. Po spuštění replikace není možné nastavení změnit.

## <a name="step-4-migrate-the-vms"></a>Krok 4: migrace virtuálních počítačů

Správci společnosti Contoso spustí rychlé testování převzetí služeb při selhání a potom provedou úplné převzetí služeb při selhání, při kterém proběhne migrace virtuálních počítačů.

### <a name="run-a-test-failover"></a>Spuštění testovacího převzetí služeb při selhání

1. V ** > ** **cíle migrace** > **Azure Migrate: Migrace serveru**klikněte na **test migrovaných serverů**.

     ![Test migrovaných serverů](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Klikněte pravým tlačítkem na virtuální počítač, který chcete otestovat, a klikněte na **Testovací migrace**.

    ![Testovací migrace](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. V části **Testovací migrace** vyberte virtuální síť Azure, ve které se po migraci bude nacházet virtuální počítač Azure. Doporučujeme použít nevýrobní síť VNet.
4. Spustí se úloha **Testovací migrace**. Tuto úlohu můžete monitorovat pomocí oznámení portálu.
5. Po dokončení migrace si můžete migrovaný virtuální počítač Azure prohlédnout na webu Azure Portal v části **Virtuální počítače**. Název počítače má příponu **-Test**.
6. Po dokončení testu v části **Replikace počítačů** klikněte pravým tlačítkem na virtuální počítač Azure a klikněte na **Vyčistit testovací migraci**.

    ![Vyčištění migrace](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrace virtuálních počítačů

Teď správci společnosti Contoso provedou úplné převzetí služeb při selhání, a tím dokončí migraci.

1. V Azure Migrate Project > **servery** > **Azure Migrate: Migrace serveru**klikněte na **replikovat servery**.

    ![Replikace serverů](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. V části **Replikace počítačů** klikněte pravým tlačítkem na virtuální počítač a vyberte **Migrovat**.
3. V části **Migrovat** > **Vypnout virtuální počítače a provést naplánovanou migraci bez ztráty dat** vyberte **Ano** > **OK**.
    - Azure Migrate ve výchozím nastavení vypne místní virtuální počítač a spustí replikaci na vyžádání, při které se synchronizují všechny změny virtuálního počítače, ke kterým došlo od poslední replikace. Tím se zajistí, že nedojde ke ztrátě dat.
    - Pokud virtuální počítač nechcete vypnout, vyberte **Ne**.
4. Pro virtuální počítač se spustí úloha migrace. Tuto úlohu můžete sledovat pomocí oznámení Azure.
5. Po dokončení úlohy můžete virtuální počítač zobrazit a spravovat na stránce **Virtuální počítače**.

### <a name="connect-the-vm-to-the-database"></a>Připojení virtuálního počítače k databázi

V posledním kroku tohoto procesu migrace správci společnosti Contoso aktualizují v aplikaci připojovací řetězec tak, aby odkazoval na databázi aplikace spuštěnou na virtuálním počítači **OSTICKETMYSQL**.

1. S využitím Putty nebo jiného klienta SSH vytvoří připojení SSH k virtuálnímu počítači **OSTICKETWEB**. Virtuální počítač je privátní, takže se připojují pomocí privátní IP adresy.

    ![Připojení k databázi](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Připojení k databázi](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. Musí se ujistit, že virtuální počítač **OSTICKETWEB** může komunikovat s virtuálním počítačem **OSTICKETMYSQL**. V současné době je tato konfigurace pevně zakódovaná s místní IP adresou 172.16.0.43.

    **Před aktualizací:**

    ![Aktualizace IP adresy](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Po aktualizaci:**

    ![Aktualizace IP adresy](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. Restartují službu pomocí **systemctl restart apache2**.

    ![Restartování](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Nakonec aktualizují záznamy DNS pro **OSTICKETWEB** a **OSTICKETMYSQL**, a to na jednom z řadičů domény Contoso.

    ![Aktualizace DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Aktualizace DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Potřebujete další pomoc?**

- [Informace](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) o spuštění testovacího převzetí služeb při selhání
- [Informace](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) o migraci virtuálních počítačů do Azure

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace teď běží vrstvy aplikace osTicket na virtuálních počítačích Azure.

Společnost Contoso teď musí provést vyčištění následujícím způsobem:

- Odebrat místní virtuální počítače z inventáře vCenter
- Odebrat místní virtuální počítače z místních zálohovacích úloh
- Aktualizovat interní dokumentaci tak, aby zobrazovala nová umístění a IP adresy pro OSTICKETWEB a OSTICKETMYSQL
- Zkontrolovat všechny prostředky, které s virtuálními počítači spolupracují, a aktualizovat veškeré související nastavení nebo dokumentaci tak, aby odrážely novou konfiguraci
- Společnost Contoso využila službu Azure Migrate s mapováním závislostí k posouzení virtuálních počítačů z hlediska migrace. Správci by měli odebrat Microsoft Monitoring Agent a pro tento účel nainstalovanou aplikaci Microsoft Dependency agent, z virtuálního počítače.

## <a name="review-the-deployment"></a>Kontrola nasazení

Aplikace je teď spuštěná a společnost Contoso ji potřebuje v nové infrastruktuře plně zprovoznit a zabezpečit.

### <a name="security"></a>Zabezpečení

Tým zabezpečení společnosti Contoso kontroluje virtuální počítače OSTICKETWEB a OSTICKETMYSQL a zjišťuje případné problémy se zabezpečením.

- V rámci řízení přístupu tým kontroluje skupiny zabezpečení sítě pro virtuální počítače. Skupiny zabezpečení sítě zajišťují, aby se k aplikaci dostal jen povolený provoz.
- Tým také zvažuje zabezpečení dat na discích virtuálních počítačů pomocí služeb Disk Encryption a Azure Key Vault.

Další informace najdete v tématu [osvědčené postupy zabezpečení pro úlohy IaaS v Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>BCDR

V zájmu zajištění provozní kontinuity a zotavení po havárii společnost Contoso provede tyto akce:

- **Zajištění bezpečnosti dat:** Společnost Contoso zálohuje data na virtuálních počítačích pomocí služby Azure Backup. [Další informace](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- **Zajištění nepřetržitého provozu aplikací:** Společnost Contoso replikuje virtuální počítače aplikace v Azure do sekundární oblasti pomocí Site Recovery. [Další informace](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- Po nasazení prostředků společnost Contoso přiřadí značky Azure, které definovala během nasazení [infrastruktury Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- Společnost Contoso nemá žádné problémy s licencováním na serverech Ubuntu.
- Společnost Contoso povolí službu Azure Cost Management licencovanou společností Cloudyn, dceřinou společností Microsoftu. Jedná se o multicloudové řešení správy nákladů, které pomáhá využívat a spravovat Azure a další cloudové prostředky. Přečtěte si [další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management.
