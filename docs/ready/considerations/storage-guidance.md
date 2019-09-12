---
title: Pokyny pro návrh úložiště z hlediska připravenosti pro Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pokyny pro návrh úložiště z hlediska připravenosti pro Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bdacb51aa87bd54ed3800f6b4452e446b25892aa
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819358"
---
# <a name="storage-design-decisions"></a>Rozhodnutí o návrhu úložiště

Možnosti úložiště jsou rozhodující pro podporu úloh a služeb, které jsou hostovány v cloudu. V rámci příprav připravenosti před přechodem na cloud si přečtěte tento článek, který vám pomůže plánovat a řešit vaše požadavky na úložiště.

## <a name="select-storage-tools-and-services-to-support-your-workloads"></a>Výběr nástrojů a služeb úložiště pro podporu vašich úloh

[Azure Storage](/azure/storage) je spravovaná služba platformy Azure pro poskytování cloudového úložiště. Azure Storage se skládá z několika základních služeb a podpůrných funkcí. Úložiště v Azure je vysoce dostupné, zabezpečené, odolné, škálovatelné a redundantní. Prostudujte si zde popsané scénáře a důležité informace, abyste si zvolili relevantní služby Azure a správné architektury, které odpovídají požadavkům vaší organizace na úlohy, zásady správného řízení a úložiště dat.

<!-- For each application or service you'll deploy to your landing zone environment, use the following decision tree as a starting point to help you determine your storage resources requirements:

![Azure storage decision tree](../../_images/ready/storage-decision-tree.png)
-->

### <a name="key-questions"></a>Klíčové otázky

Zodpovězení následujících otázek týkajících se vašich úloh vám pomůže při rozhodování na základě rozhodovacího stromu pro úložiště Azure:

- **Vyžadují vaše úlohy úložiště na disku pro podporu nasazení virtuálních počítačů infrastruktury jako služby (IaaS)?** [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) poskytuje funkce virtuálního disku pro virtuální počítače IaaS.
- **Potřebujete v rámci svých úloh poskytovat obrázky, dokumenty nebo jiná média ke stažení?** [Úložiště objektů blob v Azure](/azure/storage/blobs/storage-blobs-introduction) poskytuje možnost [hostování statických souborů](/azure/storage/blobs/storage-blob-static-website), které jsou pak přístupné ke stažení přes internet. Prostředky, které jsou hostované v úložišti objektů blob, můžete vytvářet jako veřejné, [nebo můžete prostředky omezit pro autorizované uživatele](/azure/storage/common/storage-auth) prostřednictvím Azure Active Directory (Azure AD), sdílených klíčů nebo sdílených přístupových podpisů.
- **Budete potřebovat umístění pro ukládání protokolů virtuálních počítačů, protokolů aplikací a analytických dat?** Úložiště objektů blob v Azure můžete použít [k ukládání dat protokolu služby Azure Monitor](/azure/storage/common/storage-analytics).
- **Budete potřebovat umístění pro zálohování, zotavení po havárii nebo archivaci dat souvisejících s úlohami?** Azure Disk Storage využívá úložiště objektů blob v Azure k poskytování [možností zálohování a zotavení po havárii](/azure/virtual-machines/windows/backup-and-disaster-recovery-for-azure-iaas-disks). Úložiště objektů blob můžete použít taky jako umístění k zálohování dalších prostředků, jako jsou [data SQL Serveru](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service?view=sql-server-2017) hostovaného v místní síti nebo na virtuálním počítači IaaS.
- **Budete potřebovat podporu úloh analýzy velkých objemů dat?** [Azure Data Lake Storage Gen 2](/azure/storage/blobs/data-lake-storage-introduction) je postavené na úložišti objektů blob v Azure. Data Lake Storage Gen 2 může podporovat funkce Data Lake pro rozsáhlá podniková data. Dokáže taky zvládnout ukládání petabajtů informací a současně udržovat stovky gigabitů propustnosti.
- **Budete potřebovat poskytovat nativní cloudové sdílené složky?** Azure má dvě primární služby, které poskytují sdílené složky hostované v cloudu: Azure NetApp Files a Azure Files. Služba [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) poskytuje vysoce výkonné sdílené složky systému souborů NFS, které jsou vhodné pro běžné podnikové úlohy, jako je SAP. Služba [Azure Files](/azure/storage/files/storage-files-introduction) poskytuje sdílené složky, které jsou přístupné přes SMB 3.0 a HTTPS.
- **Budete potřebovat podporu hybridního cloudového úložiště pro místní úlohy vysokovýkonného výpočetního prostředí (HPC)?** [Avere vFXT for Azure](/azure/avere-vfxt/avere-vfxt-overview) je řešení hybridního ukládání do mezipaměti, které můžete použít k rozšíření možností místní úložiště pomocí cloudového úložiště. Služba Avere vFXT for Azure je optimalizovaná pro úlohy HPC s vysokými nároky na čtení, které zahrnují výpočetní farmy s 1 000 až 40 000 procesorovými jádry. Avere vFXT pro Azure je možné integrovat s místním úložištěm připojeným k síti (NAS), úložištěm objektů blob v Azure nebo obojím.
- **Budete potřebovat provádět rozsáhlou archivaci a synchronizaci místních dat do cloudu?** Produkty [Azure Data Box](/azure/databox-family/) jsou navržené tak, aby vám pomohly přesunout velké objemy dat z místního prostředí do cloudu. [Azure Data box Gateway](/azure/databox-online/data-box-gateway-overview) je virtuální zařízení, které se nachází v místní síti. Data Box Gateway vám pomůže spravovat rozsáhlou migraci dat do cloudu. Pokud potřebujete data analyzovat, transformovat nebo filtrovat, než je přesunete do cloudu, můžete použít [Azure Data Box Edge](/azure/databox-online/data-box-edge-overview) – fyzické zařízení využívající výpočetní funkce Edge s podporou AI, které je nasazené do místního prostředí. Data Box Edge zrychluje zpracování a zabezpečený přenos dat do Azure.
- **Chcete rozšířit stávající místní sdílenou složku, aby používala cloudové úložiště?** [Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-deployment-guide) umožňuje používat službu Azure Files jako rozšíření sdílených složek, které jsou hostovány na místních počítačích se systémem Windows Server. Synchronizační služba transformuje Windows Server na rychlou mezipaměť sdílené složky Azure. Umožňuje místním počítačům, které přistupují ke sdílené složce, používat libovolný protokol, který je dostupný na Windows Serveru.

## <a name="common-storage-scenarios"></a>Běžné scénáře využití úložiště

Azure nabízí několik produktů a služeb pro různé možnosti úložiště. Kromě rozhodovacího stromu pro požadavky na úložiště, který je uvedený výše v tomto článku, popisuje následující tabulka řadu potenciálních scénářů úložiště a doporučené služby Azure pro řešení požadavků na scénář:

### <a name="block-storage-scenarios"></a>Scénáře blokových úložišť

<!-- markdownlint-disable MD033 -->

| **Scénář** | **Navrhované služby Azure** | **Předpoklady pro navrhované služby** |
|---|---|---|
| Mám holé servery nebo virtuální počítače (Hyper-V nebo VMware) s přímo připojeným úložištěm, na kterém běží obchodní aplikace. | [Azure Disk Storage (SSD úrovně Premium)](/azure/virtual-machines/windows/disks-types#premium-ssd) | Pro produkční služby nabízí možnost SSD úrovně Premium konzistentní nízkou latenci, která je spojená s vysokými IOPS a propustností. |
| Mám servery, které budou hostovat webové a mobilní aplikace. | [Azure Disk Storage (SSD úrovně Standard)](/azure/virtual-machines/windows/disks-types#standard-ssd) | SSD úrovně Standard nabízí dostatečnou IOPS a propustnost (s nižšími náklady než SSD úrovně Premium) pro webové a aplikační servery vázané na procesor v produkčním prostředí. |
| Mám podnikovou síť SAN nebo pole využívající paměti flash (AFA). | [Azure Disk Storage (SSD úrovně Premium nebo Ultra)](/azure/virtual-machines/windows/disks-types) <br/><br/> [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) | SSD úrovně Ultra je založené na NVMe a nabízí latenci v milisekundách s vysokými IOPS a šířkou pásma. SSD úrovně Ultra je škálovatelná až 64 TiB. Volba SSD úrovně Premium a SSD úrovně Ultra závisí na maximální latenci, IOPS a požadavcích na škálovatelnost. |
| Mám clusterované servery s vysokou dostupností (HA) (například SQL Server FCI nebo clustering s podporou převzetí služeb při selhání ve Windows Serveru). | [Azure Files (Premium)](/azure/storage/files/storage-files-planning#file-share-performance-tiers)<br/> [Azure Disk Storage (SSD úrovně Premium nebo Ultra)](/azure/virtual-machines/windows/disks-types) | Clusterované úlohy vyžadují více uzlů pro připojení stejného základního sdíleného úložiště pro převzetí služeb při selhání nebo vysokou dostupnost. Sdílené složky úrovně Premium nabízejí sdílené úložiště, které je možné připojit přes protokol SMB. Sdílené blokové úložiště je také možné nakonfigurovat na SSD úrovně Premium nebo SSD úrovně Ultra pomocí [partnerskýchřešení](https://azuremarketplace.microsoft.com/marketplace/apps/sios_datakeeper.sios-datakeeper-8?tab=Overview). |
| Mám relační databázi nebo úlohu datového skladu (například SQL Server nebo Oracle). | [Azure Disk Storage (SSD úrovně Premium nebo Ultra)](/azure/virtual-machines/windows/disks-types) | Volba mezi SSD úrovně Premium a SSD úrovně Ultra závisí na maximální latenci, IOPS a požadavcích na škálovatelnost. SSD úrovně Ultra také snižuje složitost tím, že odstraňuje nutnost konfigurace fondu úložiště pro zajištění škálovatelnosti (viz [podrobnosti](https://azure.microsoft.com/blog/mission-critical-performance-with-ultra-ssd-for-sql-server-on-azure-vm)). |
| Mám cluster NoSQL (například Cassandra nebo MongoDB). | [Azure Disk Storage (SSD úrovně Premium)](/azure/virtual-machines/windows/disks-types#premium-ssd) | Azure Disk Storage (SSD úrovně Premium) nabízí konzistentní nízkou latenci, která je spojená s vysokými IOPS a propustností. |
| Používám kontejnery s trvalými svazky. | [Azure Files (Standard nebo Premium)](/azure/storage/files/storage-files-planning) <br/><br/> [Azure Disk Storage (SSD úrovně Standard, Premium nebo Ultra)](/azure/virtual-machines/windows/disks-types) | Možnosti ovladače pro svazky File (RWX) a blokové svazky (RWO) jsou k dispozici pro službu Azure Kubernetes Service (AKS) i pro vlastní nasazení Kubernetes. Trvalé svazky mohou být namapovány na disk Azure Disk Storage nebo na spravovanou sdílenou složku Azure Files. Volba mezi úrovní Premium a Standard závisí na požadavcích na úlohy pro trvalé svazky. |
| Používám funkce Data Lake (jako je cluster Hadoop pro data HDFS). | [Azure Data Lake Storage Gen 2](/azure/storage/blobs/data-lake-storage-introduction) <br/><br/> [Azure Disk Storage (SSD úrovně Standard nebo Premium)](/azure/virtual-machines/windows/disks-types) | Funkce Data Lake Storage Gen 2 služby úložiště objektů blob v Azure poskytuje kompatibilitu HDFS na straně serveru a škálování v řádu petabajtů pro paralelní analýzy. Nabízí také vysokou dostupnost a spolehlivost. Software, jako je Cloudera, může v případě potřeby použít SSD úrovně Standard nebo Premium v hlavních nebo pracovních uzlech. |
| Mám nasazené SAP nebo SAP HANA. | [Azure Disk Storage (SSD úrovně Premium nebo Ultra)](/azure/virtual-machines/windows/disks-types) | SSD úrovně Ultra je optimalizovaná pro poskytování latence v milisekundách pro úlohy SAP úrovně 1. SSD úrovně Ultra je nyní ve verzi Preview. SSD úrovně Premium spojená s M-Series nabízí možnost obecné dostupnosti (GA). |
| Mám lokalitu pro zotavení po havárii se striktním RPO/RTO, která se synchronizuje z mých primárních serverů. | [Objekty blob stránky v Azure](/azure/storage/blobs/storage-blob-pageblob-overview) | Replikační software používá objekty blob stránky v Azure, které umožňují cenově výhodnou replikaci do Azure bez nutnosti využití výpočetníchvirtuálních počítačů, dokud neproběhne převzetí služeb při selhání. Další informace najdete v [dokumentaci k Azure Disk Storage](/azure/virtual-machines/windows/backup-and-disaster-recovery-for-azure-iaas-disks). **Poznámka:** Objekty blob stránky podporují maximálně 8 TB. |

### <a name="file-and-object-storage-scenarios"></a>Scénáře úložiště souborů a objektů

| **Scénář** | **Navrhované služby Azure** | **Předpoklady pro navrhované služby** |
|---|---|---|
| Používám souborový server Windows. | [Azure Files](/azure/storage/files/storage-files-planning) <br/><br/> [Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-planning) | Pomocí Synchronizace souborů Azure můžete ukládat zřídka používaná data v cloudových sdílených složkách Azure a současně ukládat do mezipaměti nejčastěji používané soubory v místní síti pro rychlý místní přístup. Můžete taky použít synchronizaci ve více lokalitách a udržovat soubory synchronizované mezi několika servery. Pokud máte v plánu migrovat úlohy pouze do cloudového nasazení, může být služba Azure Files dostatečná. |
| Mám podnikový NAS (například NetApp Filers nebo Dell-EMC Isilon). | [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) <br/><br/> [Azure Files (Premium)](/azure/storage/files/storage-files-planning#file-share-performance-tiers) | Pokud máte místní nasazení NetAppu, zvažte použití Azure NetApp Files pro migraci vašeho nasazení do Azure. Pokud používáte Windows Server nebo linuxový server nebo na něj budete migrovat nebo pokud potřebujete používat základní funkce sdílené složky, zvažte použití služby Azure Files. K trvalému místnímu přístupu použijte Synchronizaci souborů Azure k synchronizaci sdílených složek Azure s místními sdílenými složkami pomocí mechanismu vrstvení cloudu. |
| Mám sdílenou složku (SMB nebo NFS). | [Azure Files (Standard nebo Premium)](/azure/storage/files/storage-files-planning) <br/><br/> [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) | Volba úrovně Premium nebo Standard služby Azure Files závisí na IOPS, propustnosti a potřebě konzistence latence. Pokud máte místní nasazení NetAppu, zvažte použití Azure NetApp Files. Jestliže potřebujete migrovat seznamy řízení přístupu (ACL) a časová razítka do cloudu, může být vhodnou volbou použití Synchronizace souborů Azure, která přenese všechna tato nastavení do vašich sdílených složek Azure. |
| Mám místní úložiště objektů pro petabajty dat (například Dell-EMC ECS). | [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) |  Úložiště objektů blob v Azure poskytuje různé úrovně (prémiová, studená, horká a archivní), které vyhovují různým požadavkům na výkon úloh a cenu. |
| Mám nasazenou replikaci distribuovaného systému souborů (DFSR) nebo jiný způsob pro zpracování dat z poboček. | [Azure Files](/azure/storage/files/storage-files-planning) <br/><br/> [Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-planning) | Synchronizace souborů Azure nabízí synchronizaci ve víc lokalitách, která umožňuje synchronizaci souborů mezi více servery a nativními sdílenými složkami Azure v cloudu. Přejděte do pevného místního úložiště s využitím vrstvení cloudu. Vrstvení cloudu transformuje váš server na mezipaměť pro příslušné soubory a současně škáluje studená data ve sdílených složkách Azure. |
| Mám páskovou knihovnu (místní nebo mimo lokalitu) používanou pro zálohování nebo zotavení po havárii nebo dlouhodobé uchovávání dat. | [Úložiště objektů blob v Azure (studená nebo archivní úroveň)](/azure/storage/blobs/storage-blob-storage-tiers) | Archivní úroveň úložiště objektů blob v Azure bude mít nejnižší možné náklady, ale může trvat hodiny, než se offline data zkopírují do studené, horké nebo prémiové úrovně úložiště, aby byl umožněn přístup. Studené úrovně poskytují okamžitý přístup s nízkými náklady. |
| Mám úložiště souborů nebo objektů nakonfigurované pro příjem mých záloh. | [Úložiště objektů blob v Azure (studená nebo archivní úroveň)](/azure/storage/blobs/storage-blob-storage-tiers) <br/>[Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-planning) | Pokud chcete zálohovat data pro dlouhodobé uchovávání s nejnižšími náklady na úložiště, přesuňte data do úložiště objektů blob v Azure a používejte studené a archivní úrovně. Jestliže chcete povolit rychlé zotavení po havárii pro souborová data na serveru (v místní síti nebo virtuálním počítači Azure), synchronizujte sdílené složky s jednotlivými sdílenými složkami Azure pomocí Synchronizace souborů Azure. Pomocí snímků sdílené složky Azure můžete obnovit předchozí verze a synchronizovat je zpátky na připojené servery nebo k nim nativně přistupovat ve sdílené složce Azure. |
| Spouštím replikaci dat na lokalitu pro zotavení po havárii. | [Azure Files](/azure/storage/files/storage-files-planning) <br/><br/> [Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-planning) | Synchronizace souborů Azure odstraňuje nutnost používat server pro zotavení po havárii a ukládá soubory do nativních sdílených složek Azure, které využívají protokol SMB. Rychlé zotavení po havárii rychle znovu sestaví všechna data na místním serveru, který selhal. Můžete dokonce udržovat synchronizovaných několik serverů nebo použít vrstvení cloudu pro ukládání pouze relevantních dat v místní síti. |
| Spravuji přenos dat v situacích, kdy došlo k odpojení. | [Azure Data Box Edge nebo Azure Data Box Gateway](/azure/databox-online) | Pomocí Data Box Edge nebo Data Box Gateway můžete kopírovat data v situacích, kdy došlo k odpojení. Když je brána v režimu offline, uloží všechny soubory, které kopírujete, do mezipaměti, a pak je nahraje, až budete opět připojeni. |
| Spravuji datový kanál pro průběžný přenos dat do cloudu. | [Azure Data Box Edge nebo Azure Data Box Gateway](/azure/databox-online) | Přesouvejte data do cloudu ze systémů, ve kterých se neustále generují data, jednoduše tak, že se data zkopírují přímo do brány úložiště. V případě, že tyto systémy budou později potřebovat přístup k těmto datům, najdou je přesně tam, kam je zkopírovaly. |
| Mám špičky, ve kterých se najednou zobrazuje velké množství dat. | [Azure Data Box Edge nebo Azure Data Box Gateway](/azure/databox-online) | Spravujte velká množství dat, která se zobrazují najednou, například když se autonomní automobil vrací do garáže nebo když počítač sekvencování genů dokončí svou analýzu. V rychlé místním prostředí zkopírujte všechna tato data do Data Box Gateway a pak je nechte branou nahrát tak rychle, jak to umožňuje vaše síť.

### <a name="plan-based-on-data-workloads"></a>Plánování na základě datových úloh

| **Scénář** | **Navrhované služby Azure** | **Předpoklady pro navrhované služby** |
|---|---|---|
| Chci vyvinout novou nativní cloudovou aplikaci, která potřebuje zachovat nestrukturovaná data. | [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) | |
| Potřebuji migrovat data z místní instance NetApp do Azure. | [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) | |
| Potřebuji migrovat data z místních instancí souborového serveru Windows do Azure. | [Azure Files](/azure/storage/files/storage-files-planning) | |
| Potřebuji přesunout souborová data do cloudu, ale i nadále chci primárně přistupovat k datům z místního prostředí. | [Azure Files](/azure/storage/files/storage-files-planning) <br/><br/> [Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-planning) | |
| Potřebuji podporovat „výpočty v sekvenčním režimu“ –- úlohy NFS/SMB s vysokými nároky na čtení založené na souborech s datovými prostředky, které jsou umístěny místně, zatímco výpočet probíhá v cloudu. | [Avere vFXT for Azure](/azure/avere-vfxt/avere-vfxt-overview) | IaaS, škálování na více instancí, NFS/SMB, ukládání souborů do mezipaměti |
| Potřebuji přesunout místní aplikaci, která používá místní disk nebo iSCSI. | [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) | |
| Potřebuji migrovat kontejnerovou aplikaci, která má trvalé svazky. | [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) <br/><br/> [Azure Files](/azure/storage/files/storage-files-planning) | |
| Potřebuji přesunout sdílené složky, které nejsou ve Windows Serveru nebo NetAppu, do cloudu. | [Azure Files](/azure/storage/files/storage-files-planning) <br/><br/> [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) | Podpora protokolů, dostupnost podle oblastí, požadavky na výkon, funkce pro tvorbu snímků a klonování, citlivost na cenu |
| Potřebuji přesunout terabajty až petabajty dat z místního prostředí do Azure. | [Azure Data Box Edge](/azure/databox-online/data-box-edge-overview) | |
| Potřebuji před přenosem dat do Azure zpracovat data. | [Azure Data Box Edge](/azure/databox-online/data-box-edge-overview) | |
| Potřebuji podporu pro nepřetržitý příjem dat automatizovaným způsobem pomocí místní mezipaměti. | [Azure Data Box Gateway](/azure/databox-online/data-box-gateway-overview) | |

## <a name="learn-more-about-azure-storage-services"></a>Další informace o službách úložiště Azure

Poté, co identifikujete nástroje Azure, které nejlépe odpovídají vašim požadavkům, se s těmito službami seznamte pomocí podrobné dokumentace odkazované v následující tabulce:

| **Služba** | **Popis** |
|---|---|
| [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) | Azure Blob Storage je řešení úložiště objektů Microsoftu pro cloud. Úložiště objektů blob je optimalizované pro ukládání velkých objemů nestrukturovaných dat. Nestrukturovaná data jsou data, která nevyhovují konkrétnímu datovému modelu nebo definici, jako jsou textová nebo binární data.<br/><br/>Úložiště objektů blob je navržena pro:<ul><li>Poskytování obrázků nebo dokumentů přímo do prohlížeče</li><li>Ukládání souborů pro distribuovaný přístup</li><li>Streamování videa a zvuku</li><li>Zápis do souborů protokolů</li><li>Ukládání dat pro zálohování a obnovování, zotavení po havárii a pro archivaci</li><li>Ukládání dat, které bude analyzovat místní nebo v Azure hostovaná služba</li></ul> |
| [Azure Data Lake Storage Gen 2](/azure/storage/blobs/data-lake-storage-introduction) | Úložiště objektů blob podporuje Azure Data Lake Storage Gen2, řešení Microsoftu pro analýzy velkých objemů podnikových dat pro cloud. Azure Data Lake Storage Gen2 nabízí hierarchický systém souborů a také výhody úložiště objektů blob, včetně cenově úsporného vrstveného úložiště; vysoké dostupnosti; silné konzistence a funkcí zotavení po havárii. |
| [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) | Azure Disk Storage nabízí trvalé a vysoce výkonné blokové úložiště pro virtuální počítače Azure. Disky Azure jsou vysoce odolné, zabezpečené a nabízejí jedinou instanci SLA v oboru pro virtuální počítače, které používají SSD úrovně Premium nebo Ultra ([další informace o typech disků](/azure/virtual-machines/windows/disks-types)). Disky Azure poskytují vysokou dostupnost díky skupinám dostupnosti a zónám dostupnosti, které se namapují na domény selhání virtuálních počítačů Azure. Disky Azure se navíc spravují jako prostředky nejvyšší úrovně v Azure. Ve výchozím nastavení jsou k dispozici funkce nástroje Azure Resource Manager, jako je řízení přístupu na základě role (RBAC), zásady a označování. |
| [Služba soubory Azure](/azure/storage/files/storage-files-planning) | Služba Azure Files poskytuje plně spravované a nativní sdílené složky SMB jako službu, bez nutnosti provozovat virtuální počítač. Sdílenou složku služby Azure Files můžete připojit jako síťovou jednotku k libovolnému virtuálnímu počítači Azure nebo místnímu počítači. |
| [Synchronizace souborů Azure](/azure/storage/files/storage-sync-files-planning) | Synchronizace souborů Azure je možné použít k centralizaci sdílených složek organizace ve službě Azure Files bez ztráty flexibility, výkonu a kompatibility místního souborového serveru. Synchronizace souborů Azure transformuje Windows Server na rychlou mezipaměť sdílené složky Azure. |
| [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) | Azure NetApp Files je vysoce výkonná měřená služba úložiště souborů na podnikové úrovni. Služba Azure NetApp Files podporuje libovolný typ úloh a je ve výchozím nastavení vysoce dostupná. Prostřednictvím této služby můžete vybrat úrovně výkonu a služeb a nastavit snímky. |
| [Azure Data Box Edge](/azure/databox-online/data-box-edge-overview) | Azure Data Box Edge je místní síťové zařízení, které přesouvá data do a z Azure. Data Box Edge využívá výpočetní funkce Edge s podporou AI k předzpracování dat při nahrávání. Data Box Gateway je virtuální verze tohoto zařízení, ale se stejnými schopnostmi přenosu dat. |
| [Azure Data Box Gateway](/azure/databox-online/data-box-gateway-overview) | Azure Data Box Gateway je řešení úložiště, které vám umožňuje hladce odesílat data do Azure. Data Box Gateway je virtuální zařízení založené na virtuálním počítači zřízeném ve virtualizovaném prostředí nebo hypervisoru. Toto virtuální zařízení se nachází v místní síti a data na něj zapisujete pomocí protokolů NFS a SMB. Zařízení potom přenese data do objektů blob bloku Azure nebo objektů blob stránky Azure, případně do služby Azure Files. |
| [Avere vFXT for Azure](/azure/avere-vfxt/avere-vfxt-overview) | Avere vFXT for Azure je řešení ukládání do mezipaměti na úrovni systému souborů pro úlohy vysokovýkonného výpočetního prostředí (HPC) s velkými nároky na data. Umožňuje využít škálovatelnost cloud computingu ke zpřístupnění dat kdykoli a kdekoli jsou potřeba, a to i dat uložených na vlastním místním hardwaru. |

## <a name="data-redundancy-and-availability"></a>Redundance dat a dostupnost

Azure Storage má různé možnosti redundance, které pomáhají zajistit odolnost a vysokou dostupnost na základě zákaznických potřeb: místně redundantní úložiště (LRS), zónově redundantní úložiště (ZRS), geograficky redundantní úložiště (GRS) a geograficky redundantní úložiště jen pro čtení (RA-GRS).

Další informace o těchto možnostech a o tom, jak se rozhodnout pro nejlepší možnost redundance pro vaše případy použití, najdete v tématu o [redundanci Azure Storage](/azure/storage/common/storage-redundancy). Smlouvy o úrovni služeb (SLA) pro služby úložiště poskytují záruky, které jsou finančně zajištěny. Další informace najdete v tématech pojednávajících o [SLA pro spravované disky](https://azure.microsoft.com/support/legal/sla/managed-disks/v1_0), [SLA pro virtuální počítače](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_8) a [SLA pro účty úložiště](https://azure.microsoft.com/support/legal/sla/storage/v1_4).

Nápovědu pro plánování správného řešení pro disky Azure najdete v tématu o [zálohování a zotavení po havárii pro Azure Disk Storage](/azure/virtual-machines/windows/backup-and-disaster-recovery-for-azure-iaas-disks).

## <a name="security"></a>Zabezpečení

Aby vám pomohla chránit vaše data v cloudu, nabízí služba Azure Storage několik osvědčených postupů pro zabezpečení a šifrování neaktivních uložených dat a dat při přenosu. Můžete:

- Zabezpečit účet úložiště pomocí RBAC a Azure AD.
- Zabezpečit data při přenosu mezi aplikací a Azure pomocí šifrování na straně klienta, HTTPS nebo SMB 3.0.
- Nastavit dat, která se mají automaticky šifrovat při zápisu do Azure Storage pomocí šifrování služby Storage.
- Udělit delegovaný přístup k datovým objektům v Azure Storage pomocí sdílených přístupových podpisů.
- Pomocí analýzy sledovat metodu ověřování, kterou někdo používá při přístupu k úložiště v Azure.

Tyto funkce zabezpečení se týkají úložiště objektů blob v Azure (blok a stránka) a do službu Azure Files. Podrobné pokyny k zabezpečení úložiště najdete v [průvodci zabezpečením Azure Storage](/azure/storage/common/storage-security-guide).

[Šifrování služby Storage](/azure/storage/storage-service-encryption) poskytuje šifrování neaktivních uložených dat a chrání vaše data, aby splňovala závazky vaší organizace z hlediska zabezpečení a dodržování předpisů. Šifrování služby Storage je ve výchozím nastavení povolené pro všechny spravované disky, snímky a bitové kopie ve všech oblastech Azure. Od 10. června 10, 2017 se všechny nové spravované disky, snímky, image a nová data zapsaná na existující spravované disky automaticky šifrují v neaktivním uloženém stavu pomocí klíčů, které spravuje Microsoft. Další podrobnosti najdete na stránce s [nejčastějšími dotazy ke spravovaným diskům](/azure/virtual-machines/windows/faq-for-disks#managed-disks-and-storage-service-encryption).

Služba Azure Disk Encryption vám umožní šifrovat neaktivní uložené i přenášené spravované disky, které jsou připojené k virtuálním počítačům IaaS jako operační systém a datové disky, pomocí klíčů uložených v [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault). Ve Windows se jednotky šifrují pomocí standardní technologie šifrování [BitLocker](/windows/security/information-protection/bitlocker/bitlocker-overview). V Linuxu se disky šifrují pomocí subsystému [dm-crypt.](https://wikipedia.org/wiki/Dm-crypt) Proces šifrování je integrovaný s Azure Key Vault, abyste mohli řídit a spravovat klíče pro šifrování disků. Další informace najdete v tématu o službě [Azure Disk Encryption pro virtuální počítače IaaS se systémy Windows a Linux](/azure/security/azure-security-disk-encryption-overview).

## <a name="regional-availability"></a>Regionální dostupnost

S Azure můžete dodávat služby v měřítku, jaké potřebujete, abyste mohli oslovit zákazníky a partnery, *ať jsou kdekoli*. Stránky regionální dostupnosti pro [spravované disky](https://azure.microsoft.com/global-infrastructure/services/?products=managed-disks) a [Azure Storage](https://azure.microsoft.com/global-infrastructure/services/?products=storage) zobrazují oblasti, ve kterých jsou tyto služby k dispozici. Kontrola regionální dostupnosti služby předem vám může pomoct přijmout správné rozhodnutí pro vaše úlohy a potřeby zákazníků.

Spravované disky jsou dostupné ve všech oblastech Azure s nabídkami SSD úrovně Premium a SSD úrovně Standard. Přestože je SSD úrovně Ultra v současnosti ve verzi Public Preview, je nabízená jenom v jedné zóně dostupnosti, kterou je oblast Východní USA 2. Ověřte regionální dostupnost, pokud plánujete kritické a nejnáročnější úlohy vyžadující Ultra SSD.

Horké a studené úložiště objektů blob, Data Lake Storage Gen2 a úložiště Azure Files jsou k dispozici ve všech oblastech Azure. Archivní úložiště objektů blob, sdílené složky úrovně Premium a úložiště objektů blob bloku úrovně Premium jsou omezené na určité oblasti. Doporučujeme, abyste se podívali na stránku oblastí a zkontrolovali nejnovější stav regionální dostupnosti.

Další informace o globální infrastruktuře Azure najdete na [stránce oblastí Azure](https://azure.microsoft.com/global-infrastructure/regions). Konkrétní podrobnosti o tom, co je v jednotlivých oblastech Azure dostupné, najdete taky na stránce [produktů dostupných podle oblasti](https://azure.microsoft.com/global-infrastructure/services/?products=storage).

## <a name="data-residency-and-compliance-requirements"></a>Požadavky na rezidenci dat a dodržování předpisů

Na vaše úlohy se budou často vztahovat právní a smluvní požadavky týkající se datového úložiště. Tyto požadavky se mohou lišit v závislosti na sídle vaší organizace, jurisdikci, ve které se nacházejí fyzické prostředky, které hostují vaše uložená data, a příslušném obchodním sektoru. Mezi datové povinnosti, které je potřeba zvážit, patří klasifikace dat, umístění dat a individuální zodpovědnosti za ochranu dat v rámci sdíleného modelu odpovědnosti. Tyto požadavky jsou rozebrány v dokumentu white paper zaměřeném na [zajištění odpovídající rezidence dat a zabezpečení s využitím Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Součástí vašeho úsilí o dodržování předpisů může být kontrola nad tím, kde jsou fyzicky umístěny vaše databáze. Oblasti Azure jsou uspořádané do skupin označovaných jako zeměpisné oblasti. [Zeměpisná oblast Azure](https://azure.microsoft.com/global-infrastructure/geographies) zaručuje, že se v rámci příslušných zeměpisných a politických hranic dodržují požadavky na rezidenci dat, suverenitu, dodržování předpisů a odolnost. Pokud vaše úlohy podléhají suverenitě dat nebo jiným požadavkům na dodržování předpisů, musíte prostředky úložiště nasadit do oblastí ve vyhovující geografické oblasti Azure.