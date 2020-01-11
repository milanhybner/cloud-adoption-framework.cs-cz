---
title: Refaktoring nasazení sady Team Foundation Server do sady Azure DevOps Services v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak Contoso refaktoruje svoje místní nasazení TFS tím, že je migruje do sady Azure DevOps Services v Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 48ceb3581f72f6fed72360ecf4e30596b4d2eb72
ms.sourcegitcommit: 390b374dc7af4c4b85ef9fcb381c7c1bc6076ac7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/10/2020
ms.locfileid: "75868104"
---
# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Refaktoring nasazení sady Team Foundation Server do sady Azure DevOps Services

Tento článek popisuje, jak fiktivní společnost Contoso refaktoruje svoje místní nasazení sady Team Foundation Server (TFS) tím, že je migruje do sady Azure DevOps Services v Azure. Posledních pět let vývojový tým společnosti Contoso používá sadu TFS pro týmovou spolupráci a správu zdrojového kódu. Nyní chtějí přejít na cloudové řešení, které jim umožní vývoj a testování a také správu zdrojového kódu. Při přechodu na model Azure DevOps a při vývoji nových aplikací nativních pro cloud sehraje roli sada Azure DevOps Services.

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s obchodními partnery na identifikaci budoucích cílů. Partneři se příliš nestarají o vývojářské nástroje a technologie, ale vypíchli tyto body:

- **Software:** Bez ohledu na základní firmu jsou nyní všechny společnosti softwarové společnosti, včetně společnosti Contoso. Vedení podniku se zajímá o to, jak mohou informační technologie pomoci při vedení společnosti s využitím nových pracovních postupů pro uživatele a jak z nich mohou těžit zákazníci.
- **Efektivita:** Contoso potřebuje zjednodušit proces a odebrat zbytečné postupy pro vývojáře a uživatele. To společnosti umožní efektivněji plnit požadavky zákazníků. Firma potřebuje zrychlit informační technologie bez utrácení peněz a času.
- **Flexibilita:** Společnost Contoso musí reagovat na obchodní potřeby a reagovat rychleji než na webu Marketplace a umožnit tak úspěch v globálním hospodářství. Informační technologie nesmí firmu nijak brzdit.

## <a name="migration-goals"></a>Cíle migrace

Tým společnosti Contoso pro přechod na cloud přesně specifikoval cíle této migrace na Azure DevOps Services:

- Tým potřebuje nástroj pro migraci dat do cloudu. Bude potřeba několika ručních procesů.
- Je třeba migrovat data a historie pracovních položek za poslední rok.
- Nechtějí nastavovat nová uživatelská jména a hesla. Musí být zachována všechna aktuální přiřazení systému.
- Kontrolu zdrojového kódu chtějí přesunout z technologie Správa verzí Team Foundation (TFVC) do Gitu.
- Do Gitu se provede přímá migrace, která naimportuje pouze nejnovější verzi zdrojového kódu. Migrace proběhne během odstávky, kdy se veškerá práce pozastaví, protože se přesune základ kódu. Chápou, že po přesunu bude k dispozici pouze historie aktuální hlavní větve.
- Tato změna jim dělá starosti a chtějí ji před úplným přesunem otestovat. Přístup k TFS chtějí zachovat i po přechodu na Azure DevOps Services.
- Mají několik kolekcí a chtějí začít s jednou, která obsahuje pouze několik projektů, aby lépe porozuměli celému procesu.
- Chápou, že kolekce TFS mají vztah s jednotlivými organizacemi sady Azure DevOps Services, a proto budou mít více adres URL. To ale odpovídá jejich aktuálnímu modelu oddělení kódu a projektů.

## <a name="proposed-architecture"></a>Navrhovaná architektura

- Společnosti Contoso přesune svoje projekty TFS do cloudu a nadále už nebude hostovat svoje projekty ani správu zdrojového kódu místně.
- Sada TFS se bude migrovat do Azure DevOps Services.
- V současné době má společnost Contoso jednu kolekci TFS s názvem `ContosoDev`, která se bude migrovat do organizace sady Azure DevOps Services s názvem `contosodevmigration.visualstudio.com`.
- Do Azure DevOps Services se budou migrovat projekty, pracovní položky, chyby a iterace z loňského roku.
- Společnost Contoso využije službu Azure Active Directory, kterou nastavila při [nasazení infrastruktury Azure](./contoso-migration-infrastructure.md) na začátku plánování migrace.

![Architektura scénáře](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Proces migrace

Contoso dokončí proces migrace následujícím způsobem:

1. Je třeba provést rozsáhlou přípravu. Contoso nejprve musí upgradovat implementaci sady TFS na podporovanou úroveň. Contoso v současné době používá TFS 2017 Update 3, ale pro použití migrace databáze je nutné spustit podporovanou verzi 2018 s nejnovějšími aktualizacemi.
2. Po upgradu Contoso spustí nástroj pro migraci TFS a ověří kolekci.
3. Contoso vytvoří sadu přípravných souborů a za účelem otestování provede zkušební migraci.
4. Potom spustí další migraci. Tentokrát se bude jednat o úplnou migraci, která zahrnuje pracovní položky, chyby, sprinty a kód.
5. Po migraci Contoso přesune kód z TFVC do Gitu.

![Proces migrace](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Požadavky

Zde zjistíte, co Contoso potřebuje k realizaci tohoto scénáře.

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Společnost Contoso vytvořila předplatná v dřívějším článku v této sérii. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.<br/><br/> Pokud potřebujete podrobnější oprávnění, přečtěte si [tento článek](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura Azure** | Společnost Contoso nastaví svoji infrastrukturu Azure podle popisu v článku [Infrastruktura Azure pro migraci](./contoso-migration-infrastructure.md).
**Místní server TFS** | Je třeba, aby místní server používal TFS 2018 Upgrade 2, nebo aby byl v rámci tohoto procesu upgradován.

## <a name="scenario-steps"></a>Kroky scénáře

Contoso dokončí migraci tímto způsobem:

> [!div class="checklist"]
>
> - **Krok 1: vytvoření účtu služby Azure Storage.** Tento účet úložiště se použije při procesu migrace.
> - **Krok 2: upgrade TFS.** Contoso upgraduje nasazení na TFS 2018 Upgrade 2.
> - **Krok 3: ověření kolekce.** Při přípravě na migraci společnost Contoso ověří kolekci TFS.
> - **Krok 4: Sestavte soubor přípravy.** Contoso vytvoří migrační soubory pomocí nástroje pro migraci TFS.

## <a name="step-1-create-a-storage-account"></a>Krok 1: Vytvoření účtu úložiště

1. Správce společnosti Contoso vytvoří na webu Azure Portal účet úložiště (**contosodevmigration**).
2. Tento účet umístí do sekundární oblasti, kterou společnost používá pro převzetí služeb při selhání – USA – střed. Použije účet Standard pro obecné účely s místně redundantním úložištěm.

    ![Účet úložiště](./media/contoso-migration-tfs-vsts/storage1.png)

**Potřebujete další pomoc?**

- [Seznámení se službou Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction)
- [Vytvoření účtu úložiště](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)

## <a name="step-2-upgrade-tfs"></a>Krok 2: upgrade TFS

Správce společnosti Contoso upgraduje server TFS na TFS 2018 Update 2. Než začne:

- Stáhnou [TFS 2018 Update 2](https://visualstudio.microsoft.com/downloads).
- Ověří [požadavky na hardware](https://docs.microsoft.com/azure/devops/server/requirements) a pročte si [poznámky k verzi](https://docs.microsoft.com/visualstudio/releasenotes/tfs2018-relnotes) a [možná úskalí upgradu](https://docs.microsoft.com/azure/devops/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).

Upgrade provede takto:

1. Nejprve zazálohuje server TFS, který běží na virtuálním počítači VMware, a pořídí stínovou kopii VMwaru.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png)

2. Po spuštění instalačního programu TFS vybere umístění instalace. Instalační program potřebuje mít přístup k internetu.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png)

3. Po dokončení instalace se spustí Průvodce konfigurací serveru.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png)

4. Po ověření Průvodce dokončí upgrade.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png)

5. Správce ověří instalaci TFS tak, že zkontroluje projekty, pracovní položky a kód.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Některé upgrady TFS musí po dokončení upgradu spustit Průvodce konfigurací funkcí. [Další informace](https://docs.microsoft.com/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).

**Potřebujete další pomoc?**

Přečtěte si další informace o [upgradu TFS](https://docs.microsoft.com/azure/devops/server/upgrade/get-started).

## <a name="step-3-validate-the-tfs-collection"></a>Krok 3: ověření kolekce TFS

Správce společnosti Contoso spustí u databáze kolekce ContosoDev nástroj pro migraci TFS, aby ji před migrací ověřil.

1. Stáhne a rozzipuje [nástroj pro migraci TFS](https://www.microsoft.com/download/details.aspx?id=54274). Musí stáhnout verzi pro aktualizaci TFS, která je spuštěná. Verzi je možné zkontrolovat v konzole pro správu.

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. Spustí nástroj a zadáním adresy URL kolekce projektu provede ověření:

        `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

3. Nástroj zobrazí chybu.

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

4. Vyhledá soubory protokolu, které se nachází ve složce `Logs` těsně před umístěním nástroje. Pro každé hlavní ověření se vygeneruje soubor protokolu. Hlavní informace jsou uloženy v souboru `TfsMigration.log`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

5. Vyhledá tuto položku, která se vztahuje k identitě.

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

6. Na příkazovém řádku spustí `TfsMigrator validate /help` a zjistí, zda se k ověření identit vyžaduje příkaz `/tenantDomainName`.

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

7. Znovu spustí příkaz pro ověření a zahrne tuto hodnotu spolu s názvem Azure AD: `TfsMigrator validate /collection: http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

8. Zobrazí se obrazovka přihlášení k Azure AD. Správce zadá přihlašovací údaje uživatele s rolí globálního správce.

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

9. Ověření projde a nástroj ho potvrdí.

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-create-the-migration-files"></a>Krok 4: vytvoření souborů migrace

Po dokončení ověří může správce společnosti Contoso pomocí nástroje pro migraci TFS vytvořit migrační soubory.

1. V nástroji spustí přípravný krok.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Připravit](./media/contoso-migration-tfs-vsts/prep1.png)

    Příprava provádí následující:
    - V kolekci vyhledá seznam všech uživatelů a naplní protokol mapování identit (**IdentityMapLog.csv**).
    - Připraví připojení ke službě Azure Active Directory a vyhledá shodu pro jednotlivé identity.
    - Společnost Contoso už nasadila službu Azure AD a synchronizovala ji pomocí služby Azure AD Connect, proto by funkce přípravy měla být schopná najít odpovídající identity a označit je jako aktivní.

2. Zobrazí se obrazovka přihlášení k Azure AD. Správce zadá přihlašovací údaje globálního správce.

    ![Připravit](./media/contoso-migration-tfs-vsts/prep2.png)

3. Příprava se dokončí a nástroj zobrazí hlášení, že soubory importu se úspěšně vygenerovaly.

    ![Připravit](./media/contoso-migration-tfs-vsts/prep3.png)

4. Správce uvidí, že v nové složce se vytvořil soubor IdentityMapLog.csv a soubor import.json.

    ![Připravit](./media/contoso-migration-tfs-vsts/prep4.png)

5. Soubor import.json poskytuje nastavení importu. Obsahuje informace, jako jsou požadovaný název organizace a informace o účtu úložiště. Většina polí je už automaticky vyplněna. Některá pole vyžadují zadání ze strany uživatele. Správce společnosti Contoso otevře soubor a přidá název organizace sady Azure DevOps Services, která se má vytvořit: **contosodevmigration**. Pokud použije tento název, adresa URL sady Azure DevOps Services bude **contosodevmigration.visualstudio.com**.

    ![Připravit](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > Organizaci je třeba vytvořit před migrací. Po dokončení migrace ji můžete změnit.

6. Správce zkontroluje soubor protokolu mapování identit. Ten obsahuje účty, které se během importu přenesou do Azure DevOps Services.

    - Aktivní identity jsou identity, které se po importu změní na uživatele v sadě Azure DevOps Services.
    - Po migraci budou tyto identity v sadě Azure DevOps Services licencovány a zobrazí se jako uživatelé v organizaci.
    - V souboru jsou tyto identity označeny ve sloupci **Expected Import Status** (Očekávaný stav importu) jako **aktivní**.

    ![Připravit](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Krok 5: migrace na Azure DevOps Services

Když je příprava hotová, může se správce společnosti Contoso soustředit na migraci. Po spuštění migrace přepne správu verzí z TFVC na Git.

Než začne, správce spolu s vývojovým týmem naplánuje odstávku, aby mohl kolekci převést do režimu offline pro migraci. Postup migrace je následující:

1. **Odpojení kolekce.** Když je kolekce připojena a online, data identit pro kolekce jsou umístěny v konfigurační databázi serveru TFS. Při odpojení kolekce od serveru TFS se kopie těchto dat identit zabalí spolu s kolekcí pro přenos. Bez těchto dat nelze část importu související s identitami provést. Doporučujeme, abyste kolekci nechali odpojenou, dokud se import nedokončí, protože neexistuje způsob importu změn, k nimž dojde při importu.
2. **Vygenerování zálohy.** Dalším krokem migrace je vygenerování zálohy, kterou lze naimportovat do Azure DevOps Services. DACPAC, neboli balíčky komponent aplikací na datové vrstvě, je funkce SQL Serveru, která umožňuje zabalit změny databáze do jednoho souboru a nasadit je na jiné instance SQL. Změny lze obnovit přímo do sady Azure DevOps Services, a proto se tato funkce používá jako metoda balení pro přesun dat kolekce do cloudu. K vygenerování balíčku DACPAC společnost Contoso použije nástroj SqlPackage.exe. Tento nástroj je součástí nástrojů SQL Server Data Tools.
3. **Nahrání do úložiště.** Vytvořený balíček DACPAC správce nahraje do služby Azure Storage. Po nahrání správce získá sdílený přístupový podpis (SAS), který nástroji pro migraci TFS umožní přístup k úložišti.
4. **Vyplnění importu.** Potom správce společnosti Contoso vyplní v souboru importu chybějící pole, včetně nastavení DACPAC. Pro začátek uvede, že chce provést **zkušební** import, aby mohl před úplnou migraci zkontrolovat, zda vše správně funguje.
5. **Zkušební import.** Zkušební importy pomáhají otestovat migraci kolekce. Zkušební importy mají omezenou životnost a před spuštěním produkční migrace se odstraní. Po nastavené době se automaticky odstraní. Informace o tom, kdy se zkušební import odstraní, jsou uvedeny v e-mailu o úspěchu, který dostanete po dokončení importu. Údaje si poznamenejte a zařiďte se podle toho.
6. **Provedení produkční migrace.** Po dokončení zkušební migrace správce společnosti Contoso provede konečnou migraci tak, že aktualizuje soubor **import.json** a spustí import znovu.

### <a name="detach-the-collection"></a>Odpojení kolekce

Před začátkem správce společnosti Contoso pořídí místní zálohu SQL Serveru a stínovou kopii VMwaru serveru TFS, než odpojí kolekci.

1. V konzole pro správu TFS vybere kolekci, kterou chce odpojit (**ContosoDev**).

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate1.png)

2. V části **Obecné** vybere **Detach Collection** (Odpojit kolekci).

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate2.png)

3. V průvodci odpojením kolekce týmových projektů > **Servicing Message** (Servisní zpráva) zadá zprávu pro uživatele, kteří by se chtěli připojit k projektům v kolekci.

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate3.png)

4. V části **Detach Progress** (Průběh odpojení) může sledovat průběh a po dokončení procesu vybere **Další**.

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate4.png)

5. Po dokončení kontrol vybere v části **Kontroly připravenosti** možnost **Odpojit**.

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate5.png)

6. Proces dokončí výběrem možnosti **Zavřít**.

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate6.png)

7. V konzole pro správu TFS už se už kolekce nezobrazuje.

    ![Migrace](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Vygenerování balíčku DACPAC

Správce společnosti Contoso vytvoří zálohu (balíček DACPAC) pro import do Azure DevOps Services.

- DACPAC se vytvoří pomocí nástroje SqlPackage.exe v nástrojích SQL Server Data Tools. S nástroji SQL Server Data Tools se nainstaluje více verzí nástroje SqlPackage.exe, které se nacházejí ve složkách s názvy, jako jsou 120, 130 a 140. Pro přípravu balíčku DACPAC je důležité použít správnou verzi nástroje.
- Importy TFS 2018 vyžadují použití nástroje SqlPackage.exe ze složky 140 nebo vyšší. V případě CONTOSOTFS je tento soubor umístěný ve složce C:\Program Files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140.

Správce společnosti Contoso vygeneruje balíček DACPAC takto:

1. Otevře příkazový řádek a přejde do umístění SQLPackage.exe. Pomocí následujícího příkazu vygeneruje balíček DACPAC:

    ``` console
    SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory
    ```

    ![Backup](./media/contoso-migration-tfs-vsts/backup1.png)

2. Po spuštění příkazu se zobrazí následující zpráva.

    ![Backup](./media/contoso-migration-tfs-vsts/backup2.png)

3. Správce ověří vlastnosti souboru DACPAC.

    ![Backup](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a>Aktualizace souboru do úložiště

Vytvořený balíček DACPAC správce společnosti Contoso nahraje do služby Azure Storage.

1. Stáhne a následně nainstaluje [Průzkumník služby Azure Storage](https://azure.microsoft.com/features/storage-explorer).

    ![Nahrávání](./media/contoso-migration-tfs-vsts/backup5.png)

2. Správce se připojí k předplatnému a vyhledá účet úložiště vytvořený pro migraci (**contosodevmigration**). Vytvoří nový kontejner objektů blob **azuredevopsmigration**.

    ![Nahrávání](./media/contoso-migration-tfs-vsts/backup6.png)

3. Zadá soubor DACPAC, který se má nahrát jako objekt blob bloku.

    ![Nahrávání](./media/contoso-migration-tfs-vsts/backup7.png)

4. Po nahrání souboru vybere název souboru > **Generovat SAS**. Rozbalí kontejnery objektů blob v účtu úložiště, vybere kontejner se soubory importu a vybere **Získat sdílený přístupový podpis**.

    ![Nahrávání](./media/contoso-migration-tfs-vsts/backup8.png)

5. Přijme výchozí hodnoty a vybere **Vytvořit**. Tento podpis umožní přístup po dobu 24 hodin.

    ![Nahrávání](./media/contoso-migration-tfs-vsts/backup9.png)

6. Správce zkopíruje adresu URL sdíleného přístupového podpisu, aby ho mohl použít nástroj pro migraci TFS.

    ![Nahrávání](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> Migrace musí proběhnout v povoleném časovém intervalu, nebo vyprší platnost oprávnění.
> Klíč SAS negenerujte na webu Azure Portal. Klíče vygenerované tímto způsobem platí pouze pro účet a s importem nebudou fungovat.

### <a name="fill-in-the-import-settings"></a>Vyplnění nastavení importu

Správce společnosti Contoso už dříve částečně vyplnil soubor specifikace importu (import.json). Nyní musí přidat zbývající nastavení.

Otevře soubor import.json a vyplní následující pole:

- **Umístění:** Umístění klíče SAS, který byl vygenerován výše.
- **DACPAC:** Nastavte název souboru DACPAC, který jste nahráli do účtu úložiště. Nezapomeňte zahrnout příponu .dacpac.
- **ImportType:** Nastavte na DryRun nyní.

![Nastavení importu](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="do-a-dry-run-migration"></a>Provedení zkušební migrace

Správce společnosti Contoso spustí zkušební migraci, aby ověřil, že vše funguje podle očekávání.

1. Otevře příkazový řádek a přejde do umístění TfsMigration (`C:\TFSMigrator`).
2. Nejprve ověří soubor importu. Chce mít jistotu, že je soubor správně zformátován a že funguje klíč SAS.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

3. Ověření vrátí chybu, že klíč SAS potřebuje delší platnost.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test1.png)

4. Pomocí Průzkumníku služby Azure Storage Explorer vytvoří nový klíč SAS s dobou platnosti nastavenou na sedm dní.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test2.png)

5. Aktualizuje soubor `import.json` a znovu spustí ověření. Tentokrát se proces dokončí úspěšně.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test3.png)

6. Spustí zkušební běh:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

7. Zobrazí se zpráva s potvrzením migrace. Poznamenejte si dobu, po kterou se po migraci zachovají připravená data.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test4.png)

8. Zobrazí se přihlášení k Azure AD. Správce zadá přihlašovací údaje správce společnosti Contoso.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test5.png)

9. Zobrazí se zpráva s informacemi o importu.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test6.png)

10. Přibližně po 15 minutách správce přejde na adresu URL a uvidí následující informace:

     ![Zkušební běh](./media/contoso-migration-tfs-vsts/test7.png)

11. Po dokončení migrace se vedoucí vývoje společnosti Contoso přihlásí k Azure DevOps Services a zkontroluje, zda zkušební běh proběhl správně. Po ověření Azure DevOps Services potřebuje několik podrobností k potvrzení organizace.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test8.png)

12. V Azure DevOps Services uvidí vedoucí vývoje projekty, které byly migrovány do Azure DevOps Services. Najde tam také upozornění, že organizace bude za 15 dnů odstraněna.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test9.png)

13. Vedoucí vývoje otevře jeden z projektů a otevře **Pracovní položky** > **Přiřazeno mně**. Zobrazí se migrovaná data pracovní položky spolu s identitou.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test10.png)

14. Vedoucí vývoje také zkontroluje ostatní projekty a kód, aby měl jistotu, že se migroval i zdrojový kód a historie.

    ![Zkušební běh](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Spuštění produkční migrace

Po dokončení zkušebního běhu správce společnosti Contoso přejde k produkční migraci. Odstraní zkušební běh, aktualizuje nastavení importu a znovu spustí import.

1. Na portálu Azure DevOps Services odstraní zkušební organizaci.
2. Aktualizuje soubor import.json a nastaví **ImportType** na **ProductionRun**.

    ![Výroba](./media/contoso-migration-tfs-vsts/full1.png)

3. Spustí migraci stejným způsobem jako v případě zkušebního běhu: `TfsMigrator import /importFile:C:\TFSMigrator\import.json`.
4. Zobrazí se potvrzení migrace a upozornění, že data mohou být uložena v zabezpečeném umístění jako přípravná oblast po dobu maximálně sedmi dnů.

    ![Výroba](./media/contoso-migration-tfs-vsts/full2.png)

5. Na přihlašovací obrazovce Azure AD správce zadá přihlašovací údaje správce společnosti Contoso.

    ![Výroba](./media/contoso-migration-tfs-vsts/full3.png)

6. Zobrazí se zpráva s informacemi o importu.

    ![Výroba](./media/contoso-migration-tfs-vsts/full4.png)

7. Přibližně po 15 minutách správce přejde na adresu URL a uvidí následující informace:

    ![Výroba](./media/contoso-migration-tfs-vsts/full5.png)

8. Po dokončení migrace se vedoucí vývoje společnosti Contoso přihlásí k Azure DevOps Services a zkontroluje, zda migrace proběhla správně. Po přihlášení správce uvidí, že projekty byly migrovány.

    ![Výroba](./media/contoso-migration-tfs-vsts/full6.png)

9. Vedoucí vývoje otevře jeden z projektů a otevře **Pracovní položky** > **Přiřazeno mně**. Zobrazí se migrovaná data pracovní položky spolu s identitou.

    ![Výroba](./media/contoso-migration-tfs-vsts/full7.png)

10. Vedoucí vývoje zkontroluje ostatní data pracovních položek.

    ![Výroba](./media/contoso-migration-tfs-vsts/full8.png)

11. Vedoucí vývoje také zkontroluje ostatní projekty a kód, aby měl jistotu, že se migroval i zdrojový kód a historie.

    ![Výroba](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Přesunutí správy zdrojového kódu z TFVC do GITu

Po dokončení migrace chce společnost Contoso přesunout správu zdrojového kódu z TFVC do Gitu. Společnost potřebuje importovat zdrojový kód, který má momentálně ve své organizaci Azure DevOps Services, jako úložiště Git ve stejné organizaci.

1. Na portálu Azure DevOps Services správce otevře jedno z úložišť TFVC ( **$/PolicyConnect**) a zkontroluje ho.

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. Potom vybere rozevírací nabídku **Zdroj** > **Import**.

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. V části **Typ zdroje** vybere **TFVC** a zadá cestu k úložišti. Společnost se rozhodla, že historii migrovat nechce.

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > Kvůli rozdílům ve způsobu, jakým TFVC a Git ukládají informace o správě verzí, jsme společnosti Contoso doporučili, aby nemigrovala historii. Tento přístup Microsoft zaujal při migraci systému Windows a dalších produktů z centralizované správy verzí do Gitu.

4. Po importu správce zkontroluje kód.

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. Stejný postup zopakuje u druhého úložiště ( **$/SmartHotelContainer**).

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. Po kontrole zdroje vedoucí vývoje odsouhlasí, že migrace do Azure DevOps Services je hotová. Azure DevOps Services se nyní stává zdrojem veškerého vývoje v rámci týmů zapojených do migrace.

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)

**Potřebujete další pomoc?**

[Další informace](https://docs.microsoft.com/azure/devops/repos/git/import-from-TFVC?view=vsts) o importu z TFVC

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace společnost Contoso musí provést toto:

- Přečíst si článek o tom, co je třeba provést [po importu](https://docs.microsoft.com/azure/devops/articles/migration-post-import?view=vsts). Tento článek obsahuje informace o dalších aktivitách importu.
- Odstranit úložiště TFVC, nebo je umístit do režimu jen pro čtení. Základy kódu se nesmí používat, ale lze do nich nahlížet kvůli historii.

## <a name="post-migration-training"></a>Školení po migraci

Příslušným členům týmu bude muset společnost Contoso poskytnout školení k Azure DevOps Services a Gitu.
