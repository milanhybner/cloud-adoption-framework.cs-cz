---
title: Posouzení místních úloh pro migraci do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak společnost Contoso posuzuje své místní počítače pro migraci do Azure pomocí služby Azure Migrate a nástroje Data Migration Assistant.
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/30/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 021dccdbabc7d2c51b26e98b7bc6380f3a2aa8d3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70821074"
---
# <a name="assess-on-premises-workloads-for-migration-to-azure"></a>Posouzení místních úloh pro migraci do Azure

Tento článek ukazuje, jak fiktivní společnost Contoso posuzuje místní aplikaci pro migraci do Azure. V tomto ukázkovém scénáři místní aplikace SmartHotel360 společnosti Contoso aktuálně běží na VMware. Společnost Contoso posuzuje virtuální počítače aplikace pomocí služby Azure Migrate a databázi SQL Serveru aplikace pomocí nástroje Data Migration Assistant.

## <a name="overview"></a>Přehled

Společnost Contoso zvažuje migraci do Azure a potřebuje tak technické a finanční posouzení k určení, jestli jsou její místní úlohy vhodnými kandidáty pro migraci do cloudu. Konkrétně chce tým společnosti Contoso posoudit kompatibilitu počítačů a databází s migrací. Chce odhadnout kapacitu a náklady, které bude provoz prostředků společnosti Contoso v Azure vyžadovat.

Společnost Contoso začne tím, že posoudí dvě ze svých místních aplikací uvedené v následující tabulce, na kterých se lépe seznámí s příslušnými technologiemi. Společnost provede posouzení pro scénáře migrace, při kterých se změní hostitel aplikací a aplikace se refaktorují pro migraci. Další informace o změně hostitele a refaktorování najdete v [přehledu příkladů migrace](contoso-migration-overview.md).

<!-- markdownlint-disable MD033 -->

App name (Název aplikace) | Platforma | Vrstvy aplikace | Podrobnosti
--- | --- | --- | ---
SmartHotel360<br/><br/> (spravuje cestovní požadavky společnosti Contoso) | Běží na Windows s databází SQL Serveru. | Dvouvrstvá aplikace. Front-endový web ASP.NET běží na jednom virtuálním počítači (**WEBVM**) a SQL Server běží na jiném (**SQLVM**). | Virtuální počítače VMware běží na hostiteli ESXi a jejich správu zajišťuje vCenter Server.<br/><br/> Ukázkovou aplikaci si můžete stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360).
osTicket<br/><br/> (aplikace oddělení služeb společnosti Contoso) | Běží na Linuxu a Apache, MySQL a PHP (LAMP). | Dvouvrstvá aplikace. Front-endový web PHP běží na jednom virtuálním počítači (**OSTICKETWEB**) a databáze MySQL běží na jiném (**OSTICKETMYSQL**). | Aplikace služeb zákazníkům pomocí této aplikace sledují problémy pro interní zaměstnance a externí zákazníky.<br/><br/> Ukázku si můžete stáhnout z [GitHubu](https://github.com/osTicket/osTicket).

<!-- markdownlint-enable MD033 -->

## <a name="current-architecture"></a>Současná architektura

Tento diagram znázorňuje současnou místní infrastrukturu společnosti Contoso:

![Současná architektura společnosti Contoso](./media/contoso-migration-assessment/contoso-architecture.png)

- Společnost Contoso má jedno hlavní datacentrum. Toto datacentrum se nachází v New Yorku na východě USA.
- V rámci USA má společnost Contoso ještě tři další místní pobočky.
- Hlavní datacentrum je připojené k internetu přes optické připojení Metro Ethernet (500 Mb/s).
- Každá pobočka je místně připojená k internetu přes podnikové přípojky s tunely VPN IPSec, které vedou zpátky do hlavního datacentra. Díky tomuto nastavení může být celá síť společnosti Contoso trvale připojená a má optimální připojení k internetu.
- Hlavní datacentrum je plně virtualizované prostřednictvím VMware. Společnost Contoso má dva hostitele virtualizace ESXi 6.5, které spravuje vCenter Server 6.5.
- Společnost Contoso ke správě identit používá Active Directory. Společnost Contoso využívá servery DNS v interní síti.
- Řadiče domény v datacentru běží na virtuálních počítačích VMware. Řadiče domény v místních pobočkách běží na fyzických serverech.

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT ve společnosti Contoso úzce spolupracoval s obchodními partnery společnosti, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Společnost Contoso se rozšiřuje. Kvůli tomu se zvýšil tlak na místní systémy a infrastrukturu společnosti.
- **Zvýšení efektivity.** Společnost Contoso se potřebuje zbavit zbytečných postupů a zjednodušit procesy pro vývojáře i uživatele. Potřebuje IT k tomu, aby neztrácela čas ani peníze, byla rychlá a dokázala rychleji reagovat na požadavky zákazníků.
- **Zvýšení agility.** IT ve společnosti Contoso musí pohotověji reagovat na potřeby firmy. K zajištění úspěchu společnosti v globální ekonomice je nutné, aby IT dokázalo rychleji reagovat na změny na trhu. IT ve společnosti Contoso nesmí stát v cestě a nesmí se stát obchodní překážkou.
- **Škálování** Společnost Contoso se úspěšně rozšiřuje a její IT musí poskytovat systémy, které jsou schopné rozvíjet se stejným tempem.

## <a name="assessment-goals"></a>Cíle posouzení

Tým pro přechod společnosti Contoso na cloud identifikoval cíle posouzení migrace:

- Po migraci by aplikace v Azure měly mít stejné možnosti z hlediska výkonu jako současné aplikace v místním prostředí VMware společnosti Contoso. Přesun do cloudu neznamená, že je výkon aplikace méně důležitý.
- Společnost Contoso musí zjistit úroveň kompatibility svých aplikací a databází s požadavky Azure. Společnost Contoso také musí porozumět svým možnostem hostování v Azure.
- Po přesunu aplikací do cloudu by se měla minimalizovat správa databází ze strany společnosti Contoso.
- Společnost Contoso chce porozumět nejen svým možnostem migrace, ale také nákladům souvisejícím s infrastrukturou po přesunu do cloudu.

## <a name="assessment-tools"></a>Nástroje pro posouzení

Společnost Contoso k posouzení migrace použije nástroje Microsoftu. Tyto nástroje jsou v souladu s cíli společnosti a měly by jí poskytnout všechny potřebné informace.

Technologie | Popis | Náklady
--- | --- | ---
[Pomocník s migrací dat](/sql/dma/dma-overview?view=ssdt-18vs2017) | Společnost Contoso využije nástroj Data Migration Assistant k vyhodnocení a detekci problémů s kompatibilitou, které můžou ovlivnit fungování databází v Azure. Data Migration Assistant vyhodnotí paritu funkcí mezi zdroji a cíli SQL. Doporučí vylepšení z hlediska výkonu a spolehlivosti. | Nástroj Data Migration Assistant je zdarma ke stažení.
[Azure Migrate](/azure/migrate/migrate-overview) | Společnost Contoso využije službu Azure Migrate k posouzení svých virtuálních počítačů VMware. Azure Migrate posoudí vhodnost těchto počítačů k migraci. Poskytne odhad velikostí a nákladů při jejich provozu v Azure. | Od května 2018 je služba Azure Migrate bezplatná.
[Mapa služeb](/azure/operations-management-suite/operations-management-suite-service-map) | Azure Migrate využívá Service Map k zobrazení závislostí mezi počítači, které chce společnost migrovat. | Service Map je součástí protokolů služby Azure Monitor. V současné době může společnost Contoso využívat Service Map po dobu 180 dnů bez poplatků.

V tomto scénáři společnost Contoso stáhne a spustí nástroj Data Migration Assistant a provede posouzení místní databáze SQL Serveru pro svou cestovní aplikaci. Pomocí služby Azure Migrate a mapování závislostí společnost Contoso posoudí virtuální počítače aplikace před jejich migrací do Azure.

## <a name="assessment-architecture"></a>Architektura posouzení

![Architektura posouzení migrace](./media/contoso-migration-assessment/migration-assessment-architecture.png)

- Contoso je fiktivní název představující typickou podnikovou organizaci.
- Společnost Contoso má místní datacentrum (**contoso-datacenter**) a místní řadiče domény (**CONTOSODC1**, **CONTOSODC2**).
- Virtuální počítače VMware jsou umístěné na hostitelích VMware ESXi verze 6.5 (**contosohost1**, **contosohost2**).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**, spuštěný na virtuálním počítači).
- Cestovní aplikace SmartHotel360 má tyto charakteristiky:
  - Aplikace obsahuje úrovně rozdělené mezi dva virtuální počítače VMware (**WEBVM** a **SQLVM**).
  - Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com**.
  - Tyto virtuální počítače používají Windows Server 2008 R2 Datacenter SP1.
- Správu prostředí VMware zajišťuje vCenter Server (**vcenter.contoso.com**) spuštěný na virtuálním počítači.
- Aplikace oddělení služeb osTicket:
  - Aplikace obsahuje úrovně rozdělené mezi dva virtuální počítače (**OSTICKETWEB** a **OSTICKETMYSQL**).
  - Tyto virtuální počítače používají Ubuntu Linux Server 16.04-LTS.
  - Na virtuálním počítači **OSTICKETWEB** běží Apache 2 a PHP 7.0.
  - Na virtuálním počítači **OSTICKETMYSQL** běží MySQL 5.7.22.

## <a name="prerequisites"></a>Požadavky

Společnost Contoso a další uživatelé musí splňovat následující požadavky pro posouzení:

- Oprávnění vlastníka nebo přispěvatele k předplatnému Azure nebo ke skupině prostředků v předplatném Azure
- Místní instance vCenter Serveru verze 6.5, 6.0 nebo 5.5
- Účet jen pro čtení na vCenter Serveru nebo oprávnění k jeho vytvoření
- Oprávnění k vytvoření virtuálního počítače na vCenter Serveru pomocí šablony .ova
- Alespoň jeden hostitel ESXi verze 5.5 nebo novější
- Alespoň dva místní virtuální počítače VMware, na jednom z nichž běží databáze SQL Serveru.
- Oprávnění k instalaci agentů Azure Migrate na všech virtuálních počítačích
- Virtuální počítače by měly mít přímé připojení k internetu.
  - Internetový přístup můžete omezit na [požadované adresy URL](/azure/migrate/concepts-collector).
  - Pokud vaše virtuální počítače nemají připojení k internetu, je potřeba na ně nainstalovat [bránu Azure Log Analytics](/azure/azure-monitor/platform/gateway) a směrovat přes ni provoz agentů.
- Plně kvalifikovaný název domény virtuálního počítače, na kterém je spuštěná instance SQL Serveru, pro účely posouzení databáze.
- Brána Windows Firewall na virtuálním počítači s SQL Serverem by měla umožňovat externí připojení na portu TCP 1433 (výchozí nastavení). Toto nastavení umožní připojení nástroje Data Migration Assistant.

## <a name="assessment-overview"></a>Přehled posouzení

Společnost Contoso provede posouzení následujícím způsobem:

> [!div class="checklist"]
>
> - **Krok 1: Stažení a instalace nástroje Data Migration Assistant.** Společnost Contoso připraví nástroj Data Migration Assistant na posouzení místní databáze SQL Serveru.
> - **Krok 2: Posouzení databáze pomocí nástroje Data Migration Assistant.** Společnost Contoso spustí posouzení databáze a provede jeho analýzu.
> - **Krok 3: Příprava na posouzení virtuálních počítačů pomocí služby Azure Migrate.** Společnost Contoso nastaví místní účty a upraví nastavení VMware.
> - **Krok 4: Zjišťování místních virtuálních počítačů pomocí služby Azure Migrate.** Společnost Contoso vytvoří virtuální počítač kolektoru Azure Migrate. Pak společnost Contoso spustí kolektor a vyhledá virtuální počítače k posouzení.
> - **Krok 5: Příprava na analýzu závislostí pomocí služby Azure Migrate.** Společnost Contoso na virtuální počítače nainstaluje agenty Azure Migrate, aby mohla zobrazit mapování závislostí mezi virtuálními počítači.
> - **Krok 6: Posouzení virtuálních počítačů pomocí služby Azure Migrate.** Společnost Contoso zkontroluje závislosti, seskupí virtuální počítače a spustí posouzení. Jakmile bude posouzení připravené, společnost Contoso v rámci přípravy na migraci provede analýzu posouzení.

    > [!NOTE]
    > Assessments shouldn't just be limited to using tooling to discover information about your environment, you should schedule in time to speak to business owners, end users, other members within the IT department, etc in order to get a full picture of what is happening within the environment and understand things tooling cannot tell you. 

## <a name="step-1-download-and-install-data-migration-assistant"></a>Krok 1: Stažení a instalace nástroje Data Migration Assistant

1. Společnost Contoso si z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) stáhne nástroj Data Migration Assistant.
    - Nástroj Data Migration Assistant je možné nainstalovat na jakýkoli počítač, který se může připojit k instanci SQL Serveru. Společnost Contoso ho nemusí spouštět na počítači s SQL Serverem.
    - Nástroj Data Migration Assistant by se neměl spouštět na hostitelském počítači SQL Serveru.
2. Společnost Contoso spustí stažený instalační soubor (DownloadMigrationAssistant.msi) a zahájí instalaci.
3. Před dokončením průvodce na stránce **Finish** (Dokončit) společnost Contoso vybere **Launch Microsoft Data Migration Assistant** (Spustit nástroj Microsoft Data Migration Assistant).

## <a name="step-2-run-and-analyze-the-database-assessment-for-smarthotel360"></a>Krok 2: Spuštění a analýza posouzení databáze pro SmartHotel360

Teď může společnost Contoso spustit posouzení a analyzovat svou místní databázi SQL Serveru pro aplikaci SmartHotel360.

1. V nástroji Data Migration Assistant společnost Contoso vybere **New** > **Assessment** (Nový > Posouzení) a pak zadá název posouzení a projektu.
2. Jako **Source server type** (Typ zdrojového serveru) společnost Contoso vybere **SQL Server** a jako **Target server type** (Typ cílového serveru) vybere **SQL Server on Azure Virtual Machines** (SQL Server na virtuálních počítačích Azure).

    ![Data Migration Assistant – Výběr zdroje](./media/contoso-migration-assessment/dma-assessment-1.png)

    > [!NOTE]
    > V současné době nástroj Data Migration Assistant nepodporuje posouzení pro migraci na spravovanou instanci Azure SQL Database. Jako alternativní řešení společnost Contoso použije pro posouzení jako předpokládaný cíl SQL Server na virtuálním počítači Azure.

3. V části **Select target version** (Výběr cílové verze) společnost Contoso jako verzi cíle vybere SQL Server 2017. Společnost Contoso musí vybrat tuto verzi, protože tuto verzi využívá spravovaná instance SQL Database.
4. Společnost Contoso vybere sestavy, které jí pomůžou získat informace o kompatibilitě a nových funkcích:
    - **Compatibility Issues** (Problémy s kompatibilitou) uvádí změny, které můžou narušit migraci nebo které před migrací vyžadují menší úpravu. Tato sestava společnosti Contoso pomáhá udržovat si přehled o aktuálně používaných funkcích, které jsou zastaralé. Problémy jsou uspořádané podle úrovně kompatibility.
    - **New features' recommendation** (Doporučení nových funkcí) uvádí nové funkce na cílové platformě SQL Serveru, které se po migraci můžou použít pro databázi. Doporučení nových funkcí jsou uspořádaná pod nadpisy **Performance** (Výkon), **Security** (Zabezpečení) a **Storage** (Úložiště).

    ![Data Migration Assistant – Problémy s kompatibilitou a nové funkce](./media/contoso-migration-assessment/dma-assessment-2.png)

5. V části **Connect to a server** (Připojení k serveru) společnost Contoso zadá název virtuálního počítače s databází a přihlašovací údaje pro přístup k němu. Společnost Contoso vybere **Trust server certificate** (Důvěřovat certifikátu serveru), aby se zajistilo, že virtuální počítač bude mít přístup k SQL Serveru. Pak společnost Contoso vybere **Connect** (Připojit).

    ![Data Migration Assistant – Připojení k serveru](./media/contoso-migration-assessment/dma-assessment-3.png)

6. V části **Add source** (Přidání zdroje) společnost Contoso přidá databázi, kterou chce posoudit, a pak výběrem možnosti **Next** (Další) spustí posouzení.
7. Vytvoří se posouzení.

    ![Data Migration Assistant – Vytvoření posouzení](./media/contoso-migration-assessment/dma-assessment-4.png)

8. V části **Review results** (Kontrola výsledků) společnost Contoso zobrazí výsledky posouzení.

### <a name="analyze-the-database-assessment"></a>Analýza posouzení databáze

Jakmile budou k dispozici, zobrazí se výsledky. Pokud společnost Contoso nějaké chyby opraví, musí posouzení spustit znovu výběrem možnosti **Restart assessment** (Znovu spustit posouzení).

1. V sestavě **Compatibility issues** (Problémy s kompatibilitou) společnost Contoso zkontroluje případné problémy na jednotlivých úrovních kompatibility. Mapování úrovní kompatibility na verze SQL Serveru je následující:

    - 100: SQL Server 2008/Azure SQL Database
    - 110: SQL Server 2012/Azure SQL Database
    - 120: SQL Server 2014/Azure SQL Database
    - 130: SQL Server 2016/Azure SQL Database
    - 140: SQL Server 2017/Azure SQL Database

    ![Data Migration Assistant – Sestava Compatibility issues (Problémy s kompatibilitou)](./media/contoso-migration-assessment/dma-assessment-5.png)

2. V sestavě **Feature recommendations** (Doporučení funkcí) si společnost Contoso prohlédne funkce výkonu, zabezpečení a úložiště, které posouzení doporučuje po migraci. Doporučuje se celá řada funkcí, včetně OLTP v paměti, indexů columnstore, Stretch Database, Always Encrypted, dynamického maskování dat a transparentního šifrování dat.

    ![Data Migration Assistant – Sestava Feature recommendations (Doporučení funkcí)](./media/contoso-migration-assessment/dma-assessment-6.png)

    > [!NOTE]
    > Společnost Contoso by pro všechny databáze SQL Serveru měla [povolit transparentní šifrování dat](/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017). To je ještě důležitější v případě, že je databáze v cloudu, a není hostovaná v místním prostředí. Transparentní šifrování dat by se mělo povolit až po migraci. Pokud je transparentní šifrování dat již povolené, společnost Contoso musí přenést certifikát nebo asymetrický klíč do hlavní databáze cílového serveru. Informace o [přesunu databáze chráněné transparentním šifrováním dat do jiné instance SQL Serveru](/sql/relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server?view=sql-server-2017)

3. Společnost Contoso může posouzení exportovat ve formátu JSON nebo CSV.

> [!NOTE]
> V případě rozsáhlých posouzení:
>
> - Spusťte několik posouzení současně a zobrazte jejich stav na stránce **All assessments** (Všechna posouzení).
> - Konsolidujte posouzení do [databáze SQL Serveru](/sql/dma/dma-consolidatereports?view=ssdt-18vs2017).
> - Konsolidujte posouzení do [sestavy Power BI](/sql/dma/dma-powerbiassesreport?view=ssdt-18vs2017).

## <a name="step-3-prepare-for-vm-assessment-by-using-azure-migrate"></a>Krok 3: Příprava na posouzení virtuálních počítačů pomocí služby Azure Migrate

Společnost Contoso musí vytvořit účet VMware, který služba Azure Migrate může použít k automatickému zjišťování virtuálních počítačů k posouzení, ověřit, že má oprávnění k vytvoření virtuálního počítače, poznamenat si porty, které je potřeba otevřít, a nastavit úroveň nastavení statistiky.

### <a name="set-up-a-vmware-account"></a>Nastavení účtu VMware

Zjišťování virtuálních počítačů vyžaduje na vCenter Serveru účet jen pro čtení, který má následující vlastnosti:

- **Typ uživatele:** Alespoň uživatel jen pro čtení
- **Oprávnění:** Pro objekt datacentra zaškrtněte políčko **Rozšířit na podřízené objekty**. Jako **Role** vyberte **Jen pro čtení**.
- **Podrobnosti:** Uživatel je přiřazený na úrovni datacentra s přístupem ke všem objektům v datacentru.
- Pokud chcete omezit přístup, přiřaďte podřízeným objektům (hostitelé vSphere, úložiště dat, virtuální počítače a sítě) roli **Žádný přístup** s objektem **Rozšířit na podřízený objekt**.

### <a name="verify-permissions-to-create-a-vm"></a>Ověření oprávnění k vytvoření virtuálního počítače

Společnost Contoso importováním souboru ve formátu .ova zkontroluje, že má oprávnění k vytvoření virtuálního počítače. Informace o [vytvoření a přiřazení role s oprávněními](https://kb.vmware.com/s/article/1023189?other.KM_Utility.getArticleLanguage=1&r=2&other.KM_Utility.getArticleData=1&other.KM_Utility.getArticle=1&ui-comm-runtime-components-aura-components-siteforce-qb.Quarterback.validateRoute=1&other.KM_Utility.getGUser=1)

### <a name="verify-ports"></a>Ověření portů

Posouzení společnosti Contoso využívá mapování závislostí. Mapování závislostí vyžaduje, aby na virtuálních počítačích, které se budou posuzovat, byl nainstalovaný agent. Agent se na jednotlivých virtuálních počítačích musí být schopný připojit k Azure z portu TCP 443. Informace o [požadavcích na připojení](/azure/log-analytics/log-analytics-concept-hybrid)

## <a name="step-4-discover-vms"></a>Krok 4: Vyhledání virtuálních počítačů

Aby bylo možné vyhledat virtuální počítače, společnost Contoso vytvoří projekt Azure Migrate. Společnost Contoso stáhne a nastaví virtuální počítač kolektoru. Pak společnost Contoso spustí kolektor a vyhledá místní virtuální počítače.

### <a name="create-a-project"></a>Vytvoření projektu

Následujícím způsobem nastavte nový projekt Azure Migrate.

1. Na webu Azure Portal v části **Všechny služby** vyhledejte **Azure Migrate**.

2. V části **Služby** vyberte **Azure Migrate**.

3. Na stránce **Přehled** v části **Zjistit, posoudit a migrovat servery** klikněte na **Posoudit a migrovat servery**.

    ![Azure Migrate – Vytvoření projektu migrace](./media/contoso-migration-assessment/assess-migrate.png)

4. V části **Začínáme** klikněte na **Přidat nástroje**.

5. V části **Projekt migrace** vyberte své předplatné Azure a vytvořte skupinu prostředků, pokud ji ještě nemáte.

6. V části *Podrobnosti o projektu* zadejte název projektu a zeměpisnou oblast, ve které chcete projekt vytvořit. Podporované oblasti: USA, Asie, Evropa, Austrálie, Spojené království, Kanada, Indie a Japonsko.

    * Zeměpisná oblast projektu slouží pouze k ukládání metadat shromážděných z místních virtuálních počítačů.
    * Při spouštění migrace můžete vybrat jakoukoli cílovou oblast.

7. Klikněte na **Další**.

8. V části **Vybrat nástroj pro posouzení** vyberte **Azure Migrate: Server Assessment** > **Další**.

    ![Azure Migrate – Nástroj pro posouzení](./media/contoso-migration-assessment/assessment-tool.png)

9. V části **Vybrat nástroj pro migraci** vyberte **V tuto chvíli přeskočit přidání nástroje pro migraci** > **Další**.

10. V části **Kontrola a přidání nástrojů** zkontrolujte nastavení a klikněte na **Přidat nástroje**.

11. Počkejte několik minut, než se projekt Azure Migrate nasadí. Budete přesměrováni na stránku projektu. Pokud se projekt nezobrazí, můžete k němu přejít z části **Servery** na řídicím panelu služby Azure Migrate.

### <a name="download-the-collector-appliance"></a>Stažení zařízení kolektoru

1. V části **Cíle migrace** > **Servery** > **Azure Migrate: Hodnocení serverů** klikněte na **Zjistit**.

2. V části **Zjistit počítače** > **Máte počítače ve virtuální podobě?** klikněte na **Ano, s hypervisorem VMware vSphere**.

3. Pokud si chcete stáhnout soubor šablony .OVA, klikněte na **Stáhnout**.

     ![Azure Migrate – Stažení kolektoru](./media/contoso-migration-assessment/download-ovav2.png)

### <a name="verify-the-collector-appliance"></a>Ověření zařízení kolektoru

Před nasazením virtuálního počítače společnost Contoso zkontroluje, jestli je soubor OVA bezpečný:

1. Na počítači, na kterém se soubor stáhnul, společnost Contoso otevře okno příkazového řádku správce.
2. Společnost Contoso spustí následující příkaz, který pro soubor OVA vygeneruje hodnotu hash:

    ```C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]```

    **Příklad:**

    ```C:\>CertUtil -HashFile C:\AzureMigrate\AzureMigrate.ova SHA256```
3. Vygenerovaná hodnota hash by měla odpovídat hodnotám hash uvedeným v části [Ověření zabezpečení](/azure/migrate/tutorial-assess-vmware#verify-security) v kurzu [Posouzení virtuálních počítačů VMware pro migraci](/azure/migrate/tutorial-assess-vmware).

### <a name="create-the-collector-appliance"></a>Vytvoření zařízení kolektoru

Teď může společnost Contoso importovat stažený soubor do instance vCenter Serveru a zřídit virtuální počítač zařízení kolektoru:

1. V konzole vSphere Client společnost Contoso vybere **File** > **Deploy OVF Template** (Soubor > Nasadit šablonu OVF).

    ![Webový klient vSphere – Nasazení šablony OVF](./media/contoso-migration-assessment/vcenter-wizard.png)

2. V průvodci nasazením šablony OVF společnost Contoso vybere **Source** (Zdroj) a zadá umístění souboru OVA.
3. V části **Name and Location** (Název a umístění) společnost Contoso zadá zobrazovaný název virtuálního počítače kolektoru. Pak vybere umístění v inventáři, ve kterém se má virtuální počítač hostovat. Společnost Contoso zadá také hostitele nebo cluster, na kterém se bude zařízení kolektoru spouštět.
4. V části **Storage** (Úložiště) společnost Contoso zadá umístění úložiště. V části **Disk Format** (Formát disku) společnost Contoso vybere, jakým způsobem chce zřídit úložiště.
5. V části **Network Mapping** (Mapování sítě) společnost Contoso zadá síť, ve které se má virtuální počítač kolektoru připojit. Aby mohla síť odesílat metadata do Azure, potřebuje připojení k internetu.
6. Společnost Contoso zkontroluje nastavení a vybere **Power on after deployment** > **Finish** (Po nasazení vypnout > Dokončit). Po vytvoření zařízení se zobrazí zpráva potvrzující úspěšné dokončení.

### <a name="run-the-collector-to-discover-vms"></a>Spuštění kolektoru pro vyhledání virtuálních počítačů

Teď společnost Contoso spustí kolektor a vyhledá virtuální počítače. V současné době kolektor podporuje jako jazyk operačního systému a jazyk rozhraní kolektoru jen **angličtinu (Spojené státy)** .

1. V konzole vSphere Client společnost Contoso vybere **Open Console** (Otevřít konzolu). Společnost Contoso přijme licenční podmínky a zadá pro virtuální počítač kolektoru preferované heslo.
2. Na ploše společnost Contoso vybere zástupce **Microsoft Azure Appliance Configuration Manager**.

    ![Konzola vSphere Client – Zástupce kolektoru](./media/contoso-migration-assessment/collector-shortcut-v2.png)

3. Ve službě Azure Migrate Collector společnost Contoso vybere **Nastavit požadavky**. Společnost Contoso přijme licenční podmínky a přečte si informace třetích stran.
4. Kolektor zkontroluje, že má virtuální počítač připojení k internetu, synchronizaci času a spuštění služby kolektoru. (Služba kolektoru je na virtuálním počítači nainstalovaná ve výchozím nastavení.) Společnost Contoso také nainstaluje sadu VMware vSphere Virtual Disk Development Kit.

    > [!NOTE]
    > Předpokládá se, že má virtuální počítač přímý přístup k internetu bez použití proxy.

    ![Azure Migrate Collector – Ověření požadavků](./media/contoso-migration-assessment/collector-verify-prereqs-v2.png)

6. Přihlaste se ke svému účtu **Azure** a vyberte předplatné a projekt migrace, který jste vytvořili dříve. Zadejte také název **zařízení**, abyste ho rozpoznali na webu Azure Portal. 
7. V části **Zadejte podrobnosti vCenter Serveru** společnost Contoso zadá název (plně kvalifikovaný název domény) nebo IP adresu instance vCenter Serveru a přihlašovací údaje jen pro čtení, které se použijí ke zjišťování.
8. Společnost Contoso vybere rozsah zjišťování virtuálních počítačů. Kolektor může vyhledat jen virtuální počítače v rámci zadaného rozsahu. Jako rozsah je možné nastavit konkrétní složku, datacentrum nebo cluster. 

    ![Zadejte podrobnosti vCenter Serveru](./media/contoso-migration-assessment/collector-connect-vcenter.png)


8. Kolektor teď zahájí zjišťování a shromáždí informace o prostředí společnosti Contoso. 

    ![Zobrazit průběh shromažďování](./media/contoso-migration-assessment/migrate-disccovery.png)

### <a name="verify-vms-in-the-portal"></a>Kontrola virtuálních počítačů na portálu

Po dokončení shromažďování společnost Contoso zkontroluje, že se virtuální počítače zobrazí na portálu:

1. V projektu Azure Migrate společnost Contoso vybere **Servery** > **Zjištěné servery**. Společnost Contoso zkontroluje, že se zobrazí virtuální počítače, které chtěla vyhledat.

    ![Azure Migrate – Zjištěné počítače](./media/contoso-migration-assessment/discovery-complete.png)

2. Aktuálně na počítačích nejsou nainstalovaní agenti Azure Migrate. Společnost Contoso musí agenty nainstalovat, aby mohla zobrazit závislosti.

    ![Azure Migrate – Vyžaduje se instalace agenta](./media/contoso-migration-assessment/machines-no-agent.png)

## <a name="step-5-prepare-for-dependency-analysis"></a>Krok 5: Příprava na analýzu závislostí

Aby společnost Contoso mohla zobrazit závislosti mezi virtuálními počítači, které chce posoudit, stáhne a nainstaluje agenty na virtuální počítače aplikace. Společnost Contoso nainstaluje agenty na všechny virtuální počítače aplikace s Windows i Linuxem.

### <a name="take-a-snapshot"></a>Pořízení snímku

Společnost Contoso před úpravou virtuálních počítačů vytvoří jejich kopii tím, že před instalací agentů pořídí jejich snímek.

![Snímek počítače](./media/contoso-migration-assessment/snapshot-vm.png)

### <a name="download-and-install-the-vm-agents"></a>Stažení a instalace agentů virtuálního počítače

1. V části **Počítače** společnost Contoso vybere požadovaný počítač. Ve sloupci **Závislosti** společnost Contoso vybere možnost **Vyžaduje instalaci**.
2. V podokně **Zjistit počítače** společnost Contoso:
    - Stáhne agenta Microsoft Monitoring Agent (MMA) a agenta závislostí pro všechny virtuální počítače s Windows.
    - Stáhne agenta MMA a agenta závislostí pro všechny virtuální počítače s Linuxem.
3. Společnost Contoso zkopíruje ID a klíč pracovního prostoru. Společnost Contoso potřebuje klíč a ID pracovního prostoru při instalaci agenta MMA.

    ![Stažení agenta](./media/contoso-migration-assessment/download-agents.png)

### <a name="install-the-agents-on-windows-vms"></a>Instalace agentů na virtuálních počítačích s Windows

Společnost Contoso spustí instalaci na všech virtuálních počítačích.

#### <a name="install-the-mma-on-windows-vms"></a>Instalace agenta MMA na virtuálních počítačích s Windows

1. Společnost Contoso dvakrát klikne na staženého agenta.
2. V části **Cílová složka** společnost Contoso ponechá výchozí instalační složku a pak vybere **Další**.
3. V části **Možnosti instalace agenta** společnost Contoso vybere **Připojit agenta k Azure Log Analytics** > **Další**.

    ![Instalace agenta Microsoft Monitoring Agent – Možnosti instalace agenta](./media/contoso-migration-assessment/mma-install.png)

4. V části **Azure Log Analytics** společnost Contoso vloží ID a klíč pracovního prostoru, které zkopírovala z portálu.

    ![Instalace agenta Microsoft Monitoring Agent – Azure Log Analytics](./media/contoso-migration-assessment/mma-install2.png)

5. V části **Připraveno k instalaci** společnost Contoso nainstaluje agenta MMA.

#### <a name="install-the-dependency-agent-on-windows-vms"></a>Instalace agenta závislostí na virtuálních počítačích s Windows

1. Společnost Contoso dvakrát klikne na staženého agenta závislostí.
2. Společnost Contoso přijme licenční podmínky a počká na dokončení instalace.

    ![Instalace agenta závislostí – Instalace](./media/contoso-migration-assessment/dependency-agent.png)

### <a name="install-the-agents-on-linux-vms"></a>Instalace agentů na virtuálních počítačích s Linuxem

Společnost Contoso spustí instalaci na všech virtuálních počítačích.

#### <a name="install-the-mma-on-linux-vms"></a>Instalace agenta MMA na virtuálních počítačích s Linuxem

1. Společnost Contoso pomocí následujícího příkazu na všechny virtuální počítače nainstaluje knihovnu Python ctypes:

    `sudo apt-get install python-ctypeslib`
2. Společnost Contoso musí tento příkaz pro instalaci agenta MMA spustit jako uživatel root. Společnost Contoso se stane uživatelem root tak, že spustí následující příkaz a pak zadá heslo uživatele root:

    `sudo -i`
3. Společnost Contoso nainstaluje agenta MMA:
    - Společnost Contoso v rámci příkazu zadá ID a klíč pracovního prostoru.
    - Příkazy jsou určené pro 64bitovou architekturu.
    - ID a primární klíč pracovního prostoru se nacházejí v pracovním prostoru služby Log Analytics na webu Azure Portal. Stačí vybrat **Nastavení** a pak kartu **Připojené zdroje**.
    - Spuštěním následujícího příkazu stáhne agenta Log Analytics, ověří kontrolní součet a nainstaluje a nasadí agenta:

    ```console
    wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w 6b7fcaff-7efb-4356-ae06-516cacf5e25d -s k7gAMAw5Bk8pFVUTZKmk2lG4eUciswzWfYLDTxGcD8pcyc4oT8c6ZRgsMy3MmsQSHuSOcmBUsCjoRiG2x9A8Mg==
    ```

#### <a name="install-the-dependency-agent-on-linux-vms"></a>Instalace agenta závislostí na virtuálních počítačích s Linuxem

Po dokončení instalace agenta MMA společnost Contoso na virtuální počítače s Linuxem nainstaluje agenta závislostí:

1. Agent závislostí se na počítače s Linuxem instaluje skriptem prostředí se samorozbalovacím binárním souborem InstallDependencyAgent-Linux64.bin. Společnost Contoso tento soubor spustí pomocí příkazu sh nebo tak, že k samotnému souboru přidá oprávnění ke spuštění.

2. Společnost Contoso nainstaluje agenta závislostí pro Linux jako uživatel root:

    ```console
    wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin && sudo sh InstallDependencyAgent-Linux64.bin -s
    ```

## <a name="step-6-run-and-analyze-the-vm-assessment"></a>Krok 6: Spuštění a analýza posouzení virtuálních počítačů

Společnost Contoso teď může ověřit závislosti počítačů a vytvořit skupinu. Pak pro tuto skupinu spustí posouzení.

### <a name="verify-dependencies-and-create-a-group"></a>Ověření závislostí a vytvoření skupiny

1. Aby společnost Contoso zjistila, které počítače má analyzovat, vybere **Zobrazit závislosti**.

    ![Azure Migrate – Zobrazení závislostí počítačů](./media/contoso-migration-assessment/view-machine-dependencies.png)

2. Pro virtuální počítač SQLVM se na mapě závislostí zobrazí následující podrobnosti:

    - Spuštěné skupiny procesů nebo procesy s aktivními síťovými připojeními na virtuálním počítači SQLVM v zadaném časovém období (ve výchozím nastavení je to hodina).
    - Příchozí (klient) připojení přes protokol TCP ke všem závislým počítačům a odchozí (server) připojení přes protokol TCP ze všech závislých počítačů.
    - Závislé počítače s nainstalovanými agenty Azure Migrate se zobrazí v samostatných polích.
    - U počítačů bez nainstalovaných agentů se zobrazí informace o portu a IP adrese.

3. U počítačů s nainstalovaným agentem (WEBVM) společnost Contoso výběrem pole počítače zobrazí další informace. Tyto informace zahrnují plně kvalifikovaný název domény, operační systém a adresu MAC.

    ![Azure Migrate – Zobrazení závislostí skupin](./media/contoso-migration-assessment/sqlvm-dependencies.png)

4. Společnost Contoso vybere virtuální počítače, které se mají přidat do skupiny (SQLVM a WEBVM). Společnost Contoso při výběru podrží klávesu Ctrl, aby mohla vybrat více virtuálních počítačů.
5. Společnost Contoso vybere možnost **Vytvořit skupinu** a pak zadá její název (**smarthotelapp**).

    > [!NOTE]
    > Pokud chcete zobrazit podrobnější závislosti, můžete rozšířit časový rozsah. Můžete vybrat konkrétní dobu nebo počáteční a koncové datum.

### <a name="run-an-assessment"></a>Spuštění posouzení

1. V části **Skupiny** společnost Contoso otevře skupinu (**smarthotelapp**) a pak vybere možnost **Vytvořit posouzení**.

    ![Azure Migrate – Vytvoření posouzení](./media/contoso-migration-assessment/run-vm-assessment.png)

2. Společnost Contoso zobrazí posouzení výběrem možností **Správa** > **Posouzení**.

Společnost Contoso používá výchozí nastavení posouzení, ale toto [nastavení si můžete upravit](/azure/migrate/how-to-modify-assessment).

### <a name="analyze-the-vm-assessment"></a>Analýza posouzení virtuálních počítačů

Posouzení služby Azure Migrate obsahuje informace o kompatibilitě místního prostředí s Azure, navrhované správné velikosti pro virtuální počítač Azure a odhadovaných měsíčních nákladech na Azure.

![Azure Migrate – Sestava posouzení](./media/contoso-migration-assessment/assessment-overview.png)

#### <a name="review-confidence-rating"></a>Kontrola hodnocení spolehlivosti

![Azure Migrate – Zobrazení posouzení](./media/contoso-migration-assessment/assessment-display.png)

Posouzení má hodnocení spolehlivosti od 1 do 5 hvězdiček (1 hvězdička je nejnižší a 5 hvězdiček je nejvyšší).

- Hodnocení spolehlivosti se k posouzení přiřadí na základě dostupnosti datových bodů potřebných pro výpočet posouzení.
- Toto hodnocení pomáhá odhadnout spolehlivost doporučení velikostí poskytovaných službou Azure Migrate.
- Hodnocení spolehlivosti je užitečné v případě, že provádíte *určování velikosti na základě výkonu*. Azure Migrate nemusí mít dostatek datových bodů k určení velikosti na základě využití. V případě *určování stejné velikosti jako v místním prostředí* je hodnocení spolehlivosti vždy 5 hvězdiček, protože Azure Migrate má k dispozici všechny datové body, které k určení velikosti virtuálního počítače potřebuje.
- Tady je poskytnuté hodnocení spolehlivosti posouzení v závislosti na procentu dostupných datových bodů:

   Dostupnost datových bodů | Míra spolehlivosti
   --- | ---
   0 až 20 % | 1 hvězdička
   21 až 40 % | 2 hvězdičky
   41 až 60 % | 3 hvězdičky
   61 až 80 % | 4 hvězdičky
   81 až 100 % | 5 hvězdiček

#### <a name="verify-azure-readiness"></a>Ověření připravenosti pro Azure

![Azure Migrate – Posouzení připravenosti](./media/contoso-migration-assessment/azure-readiness.png)

V sestavě posouzení se zobrazí tabulka se souhrnem informací. K zobrazení velikostí určených na základě výkonu potřebuje služba Azure Migrate následující informace. Pokud tyto informace není možné shromáždit, posouzení velikostí nemusí být přesné.

- Data o využití procesoru a paměti.
- Informace o vstupně-výstupních operacích čtení a zápisu za sekundu a propustnosti pro všechny disky připojené k virtuálnímu počítači.
- Informace o síťových vstupech a výstupech pro všechny síťové adaptéry připojené k virtuálnímu počítači.

<!-- markdownlint-disable MD033 -->

Nastavení | Indikace | Podrobnosti
--- | --- | ---
**Připravenost virtuálního počítače pro Azure** | Určuje, jestli je virtuální počítač připravený k migraci. | Možné stavy:<br/><br/>– Připraveno pro Azure<br/><br/>– Připraveno s podmínkami <br/><br/>– Nepřipraveno pro Azure<br/><br/>– Připravenost neznámá<br/><br/> Pokud virtuální počítač není připravený, Azure Migrate zobrazí několik kroků pro odstranění problému.
**Velikost virtuálního počítače Azure** | Pro připravené virtuální počítače Azure Migrate nabídne doporučenou velikost virtuálního počítače Azure. | Doporučení velikosti závisí na vlastnostech posouzení:<br/><br/>– Pokud jste použili určení velikosti na základě výkonu, při určování velikosti se zohlední historie výkonu virtuálních počítačů.<br/><br/>– Pokud jste použili *určení stejné velikosti jako v místním prostředí*, určení velikosti bude založené na velikosti místního virtuálního počítače a data o využití se nepoužijí.
**Navrhovaný nástroj** | Vzhledem k tomu, že jsou na počítačích Azure spuštění agenti, Azure Migrate prozkoumá spuštěné procesy v rámci počítače. Určí, jestli je daný počítač hostitelem databáze.
**Informace o virtuálním počítači** | Tato sestava ukazuje nastavení místního virtuálního počítače, včetně informací o operačním systému, typu spouštění, discích a úložišti.

<!-- markdownlint-enable MD033 -->

#### <a name="review-monthly-cost-estimates"></a>Kontrola odhadů měsíčních nákladů

Toto zobrazení informuje o celkových nákladech na výpočetní kapacitu a úložiště, které s sebou nese provoz virtuálních počítačů v Azure. Nabízí také podrobné údaje o jednotlivých počítačích.

![Azure Migrate – Náklady na Azure](./media/contoso-migration-assessment/azure-costs.png)

- Při výpočtu odhadovaných nákladů se používají doporučené velikosti počítačů.
- Odhadované měsíční náklady na výpočetní kapacitu a úložiště jsou agregované pro všechny virtuální počítače dané skupiny.

## <a name="clean-up-after-assessment"></a>Vyčištění po posouzení

- Po dokončení posouzení si společnost Contoso ponechá zařízení Azure Migrate pro budoucí hodnocení.
- Společnost Contoso vypne virtuální počítač VMware. Společnost Contoso ho znovu použije při vyhodnocování dalších virtuálních počítačů.
- Společnost Contoso zachová projekt **ContosoMigration** v Azure. Projekt je momentálně nasazený ve skupině prostředků **ContosoFailoverRG** v oblasti Azure Východní USA.
- Součástí virtuálního počítače kolektoru je 180denní zkušební licence. Pokud tento limit vyprší, společnost Contoso bude muset kolektor znovu stáhnout a nastavit.

## <a name="conclusion"></a>Závěr

V tomto scénáři společnost Contoso pomocí nástroje Data Migration Assistant posoudila databázi své aplikace SmartHotel360. Pomocí služby Azure Migrate posoudila místní virtuální počítače. Společnost Contoso zkontrolovala posouzení, aby se ujistila, že jsou místní prostředky připravené na migraci do Azure.

## <a name="next-steps"></a>Další postup

Po posouzení této úlohy jako potenciálního kandidáta na migraci může společnost Contoso začít připravovat místní infrastrukturu a infrastrukturu Azure na migraci. Příklad toho, jak společnost Contoso provádí tyto procesy, najdete v článku o [nasazení infrastruktury Azure](contoso-migration-infrastructure.md) v části s osvědčenými postupy pro architekturu přechodu na cloud věnované migraci.
