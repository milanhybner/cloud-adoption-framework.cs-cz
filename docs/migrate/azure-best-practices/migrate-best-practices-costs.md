---
title: Osvědčené postupy pro určování nákladů a velikostí úloh migrovaných do Azure
description: Získejte osvědčené postupy pro určování nákladů a velikostí úloh migrovaných do Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0616b2721a903be369192a47fcd888247fd6cad6
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222622"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Osvědčené postupy pro určování nákladů a velikostí úloh migrovaných do Azure

Zaměřením se na náklady při plánování a návrhu migrace zajistíte dlouhodobý úspěch migrace do Azure. Při migraci je nezbytné, aby všechny týmy (například finanční tým, vedení a tým vývoje aplikací) pochopili související náklady.

- Klíčem k úspěchu je odhad výdajů na migraci a stanovení základních měsíčních, čtvrtletních a ročních rozpočtových cílů ještě před migrací.
- Po migraci byste měli optimalizovat náklady, průběžně sledovat úlohy a plánovat budoucí způsoby využití. Migrované prostředky můžou zpočátku být jedním typem úlohy, ale postupem času se můžou změnit na jiný typ podle využití, nákladů a měnících se obchodních požadavků.

Tento článek popisuje osvědčené postupy pro kalkulaci nákladů a stanovení velikosti před migrací a po ní.

> [!IMPORTANT]
> Uvedené osvědčené postupy a názory popsané v tomto článku jsou založené na funkcích platformy a služeb Azure, které jsou k dispozici v době vzniku tohoto článku. Funkce a možnosti se postupem času mění. Některá doporučení nemusí být pro vaše nasazení použitelná, takže si vyberte ty, které se vám hodí.

## <a name="before-migration"></a>Před migrací

Než přesunete úlohy do cloudu, proveďte odhad měsíčních nákladů na jejich provoz v Azure. Proaktivní správa nákladů na cloud vám pomůže dodržet váš rozpočet provozních nákladů. Pokud máte omezený rozpočet, vezměte to před migrací v úvahu. Tam, kde je to vhodné, zvažte převod úloh na bezserverové technologie Azure.

Osvědčené postupy v této části vám pomohou odhadnout náklady, zvolit správnou velikost virtuálních počítačů a úložiště, využívat výhod hybridního využití Azure, používat vyhrazené virtuální počítače a odhadnout výdaje na cloud v rámci předplatného.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Osvědčený postup: odhadnout měsíční náklady na úlohy

K předpovědi měsíčních nákladů na migrované úlohy můžete využít několik nástrojů.

- **Cenová Kalkulačka Azure:** Vyberte produkty, které chcete odhadnout, například virtuální počítače a úložiště. Do cenové kalkulačky zadáte vstupní náklady a vytvoříte odhad.

 ![cenové kalkulačky Azure](./media/migrate-best-practices-costs/pricing.png) *cenové kalkulačky Azure*

- **Azure Migrate:** K odhadování nákladů potřebujete zkontrolovat a vyhodnotit všechny prostředky, které jsou potřebné ke spouštění vašich úloh v Azure. Tato data získáte tak, že vytvoříte inventář prostředků, včetně serverů, virtuálních počítačů, databází a úložiště. Ke shromáždění těchto informací můžete použít službu Azure Migrate.

- Azure Migrate zjistí a vyhodnotí místní prostředí a poskytne inventář.
- Azure Migrate umí zmapovat a zobrazovat závislosti mezi virtuálními počítači, takže získáte úplný obrázek.
- Hodnocení Azure Migrate obsahuje odhadované náklady.
  - Náklady na výpočetní výkon: pomocí velikost virtuálního počítače Azure, doporučuje se, když vytvoříte posouzení, migrace Azure používá rozhraní API pro fakturaci pro výpočet odhadované měsíční náklady na virtuální počítač. V odhadu služba zohlední operační systém, zajištění softwaru, vyhrazené instance, provozuschopnost virtuálního počítače, umístění a nastavení měny. V rámci hodnocení agreguje náklady související se všemi virtuálními počítači a vypočítá celkové měsíční náklady na výpočetní služby.
  - Náklady na úložiště: Azure Migrate vypočítá agregováním náklady na úložiště všechny virtuální počítače ve vyhodnocení celkové měsíční náklady na úložiště. Měsíční náklady na úložiště pro konkrétní počítač můžete vypočítat agregací měsíčních nákladů na všechny disky, které jsou k němu připojeny.

    ![Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    *Hodnocení Azure Migrate*

**Další informace:**

- [Použití](https://azure.microsoft.com/pricing/calculator) cenové kalkulačky Azure
- [Přehled](https://docs.microsoft.com/azure/migrate/migrate-overview) služby Azure Migrate
- [Informace](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) o posouzení Azure Migrate
- [Další informace](https://docs.microsoft.com/azure/dms/dms-overview) o službě Azure Database Migration Service

## <a name="best-practice-right-size-vms"></a>Osvědčený postup: nastavení správné velikosti virtuálních počítačů

Při nasazování virtuálních počítačů Azure si můžete zvolit z různých možností podpory úloh. Každý virtuální počítač má specifické funkce a různé kombinace procesoru, paměti a disků. Virtuální počítače jsou seskupeny takto:

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Obecné účely** | Vyvážený poměr procesorů k paměti. | Vhodné pro testování a vývoj, malé a střední databáze a webové servery s nízkým až středním provozem.
**Optimalizované z hlediska výpočetních prostředků** | Vysoký poměr procesorů k paměti. | Vhodné pro webové servery se středním provozem, síťová zařízení, dávkové procesy a aplikační servery.
**Paměťově optimalizované** | Vysoký poměr paměti k procesoru. | Vhodné pro relační databáze, střední a velké mezipaměti a analýzu v paměti.
**Optimalizované z hlediska úložiště** | Vysoká propustnost disku a V/V. | Vhodné pro databáze NoSQL, SQL a velké objemy dat.
**Optimalizované z hlediska GPU** | Specializované virtuální počítače. Jeden nebo více GPU. | Velké úpravy grafiky a videí.
**Vysoký výkon** | Nejrychlejší a nejvýkonnější procesor. Virtuální počítače s volitelnými síťovými rozhraními s vysokou propustností (RDMA). | Důležité aplikace s vysokým výkonem.

- Je důležité porozumět cenovým rozdílům mezi těmito virtuálními počítači a dlouhodobému dopadu na rozpočet.
- Každý typ zahrnuje několik řad virtuálních počítačů.
- Kromě toho, pokud vyberete virtuální počítač v rámci jedné řady, můžete jeho kapacitu vertikálně navýšit a snížit pouze v dané řadě. Kapacitu virtuálního počítače DSv2\_2 můžete například navýšit na DSv2\_4, ale nemůžete ho změnit na jinou řadu, jako je Fsv2\_2.

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) o typech a určování velikosti virtuálních počítačů a mapování velikostí k typům
- [Plánování](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs) velikostí virtuálních počítačů
- [Přehled](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) ukázkového hodnocení pro fiktivní společnost Contoso

## <a name="best-practice-select-the-right-storage"></a>Osvědčený postup: vyberte správné úložiště

Ladění a údržba místního úložiště (SAN nebo NAS) a sítí, které je podporují, mohou být nákladné a časově náročné. Data ze souboru (úložiště) se běžně migrují do cloudu za účelem zmírnění problémů souvisejících s provozem a správou. Microsoft nabízí několik možností pro přesun dat do Azure a je třeba o nich rozhodnout. Výběr správného typu úložiště dat může každý měsíc vaší organizaci ušetřit několik tisíc dolarů. Několik důležitých informací:

- Data, která se nedají použít hodně a nejsou nepostradatelná, nemusí být umístěna na nejlevnějších úložištích.
- Pro důležitá podniková data byste naopak měli zvolit úložiště vyšší úrovně.
- Při plánování migrace proveďte inventarizaci dat a klasifikujte je podle důležitosti, abyste je mohli namapovat na nejvhodnější úložiště. Vezměte v úvahu rozpočet a náklady, ale i výkon. Náklady nemusí nutně být hlavním rozhodujícím faktorem. Při výběru nejlacinější možnosti byste mohli úlohy vystavit problémům s výkonem a dostupností.

### <a name="storage-data-types"></a>Typy dat úložiště

Azure poskytuje různé typy dat úložiště

<!--markdownlint-disable MD033 -->

**Datový typ** | **Podrobnosti** | **Použití**
--- | --- |  ---
**Objekty blob** | Optimalizováno pro ukládání velkých objemů nestrukturovaných dat objektů, jako jsou textová nebo binární data.<br/><br/> | Přístup k datům odkudkoli přes protokol HTTP/HTTPS. | Používá se pro scénáře streamování a náhodného přístupu. Slouží například pro zobrazování obrázků a dokumentů přímo v prohlížeči, streamování videa a zvuku a pro ukládání dat za účelem zálohování a zotavení po havárii.
**Soubory** | Spravované sdílené složky přístupné přes SMB 3.0. | Používá se při migraci místních sdílených složek a k poskytování vícenásobného přístupu nebo připojení k datům souborů.
**Disky** | Založeno na objektech blob stránky.<br/><br/> Typ (rychlost) disku: standardní (pevný disk nebo SSD) nebo Premium (SSD).<br/><br/>Správa na disku: nespravovaných (můžete spravovat nastavení disku a úložiště) nebo spravované (vyberte typ disku a Azure spravuje za vás disk). | Pro virtuální počítače se používají disky Premium. Pro jednoduchou správu a změnu velikosti se používají spravované disky.
**Fronty** | Ukládání a načítání velkého počtu zpráv přístupných přes ověřená volání (HTTP nebo HTTPS). | Připojení komponent aplikací pomocí zařazování asynchronních zpráv do fronty.
**Tabulky** | Ukládání tabulek. | Nyní součástí rozhraní API tabulky Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Úrovně přístupu

Úložiště Azure poskytuje různé možnosti pro přístup k datům objektu blob bloku. Výběr správné úrovně přístupu vám pomůže zajistit, že data objektu blob bloku ukládáte cenově nejefektivnějším způsobem.

<!--markdownlint-disable MD033 -->

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Horká** | Vyšší náklady na úložiště než poskytuje studená úroveň přístupu. Nižší poplatky za přístup než poskytuje studená úroveň přístupu.<br/><br/>Jedná se o výchozí úroveň. | Používá se pro aktivní data, která se často používají.
**Studená** | Nižší náklady na úložiště než poskytuje horká úroveň přístupu. Vyšší poplatky za přístup než poskytuje horká úroveň přístupu.<br/><br/> Uložení po dobu minimálně 30 dnů. | Krátkodobé ukládání, data jsou dostupná, ale často se nepoužívají.
**Archiv** | Slouží pro jednotlivé objekty blob bloku.<br/><br/> Cenově nejefektivnější možnost úložiště. Přístup k datům je dražší než v případě horké a studené úrovně přístupu. | Určeno pro data, u kterých se toleruje latence načtení několik hodin a která zůstanou v archivní vrstvě nejméně 180 dnů.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy účtů úložiště

Azure poskytuje různé typy účtů úložiště a úrovní výkonu.

<!--markdownlint-disable MD033 -->

**Typ účtu** | **Podrobnosti** | **Použití**
--- | --- | ---
**Obecné účely v2 Standard** | Podporuje objekty blob (bloku, stránky, doplňovací objekty blob), soubory, disky, fronty a tabulky.<br/><br/> Podporuje horkou, studenou a archivní úroveň přístupu. Podporuje se zónově redundantní úložiště. | Používá se pro většinu scénářů a typů dat. Účty úložiště úrovně Standard mohou být založeny na discích HDD nebo SSD.
**Obecné účely v2 Premium** | Podporuje data úložiště objektů blob (objekty blob stránky). Podporuje horkou, studenou a archivní úroveň přístupu. Podporuje se zónově redundantní úložiště.<br/><br/> Data se ukládají na disku SSD. | Tuto možnost Microsoft doporučuje pro všechny virtuální počítače.
**Obecné účely v1** | Použití různých úrovní přístupu se nepodporuje. Nepodporuje se zónově redundantní úložiště. | Používá se v případě, že aplikace vyžadují model nasazení Azure Classic.
**Objekt blob** | Specializovaný účet úložiště pro ukládání nestrukturovaných objektů. Poskytuje pouze objekty blob bloku a doplňovací objekty blob (nikoli služby úložiště File, Queue, Table nebo Disk). Poskytuje stejnou stálost, dostupnost, škálovatelnost a výkon jako Obecné účely v2. | V těchto účtech nejde ukládat objekty blob stránky, a proto nemůžete ukládat soubory VHD. Úroveň přístupu můžete nastavit na horkou nebo studenou.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Možnosti redundance služby Storage

Účty úložiště mohou používat různé typy redundance za účelem zachování odolnosti a vysoké dostupnosti.

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Místně redundantní úložiště (LRS)** | Chrání před lokálním výpadkem tím, že se replikuje v rámci jedné jednotky úložiště do samostatné domény selhání a aktualizační domény. Uchovává více kopií dat v jednom datacentru. Poskytuje minimálně 99,999999999% (11 9) stálost objektů v průběhu daného roku. | Tuto možnost zvažte, pokud aplikace ukládá data, která lze snadno rekonstruovat.
**Zónově redundantní úložiště (ZRS)** | Chrání před výpadkem datacentra tím, že se replikuje ve třech clusterech úložiště v jedné oblasti. Jednotlivé clustery úložiště jsou fyzicky odděleny a umístění ve vlastní zóně dostupnosti. Poskytuje minimálně 99,9999999999% (12 9) odolnost objektů v průběhu daného roku díky uchovávání několika kopií dat v několika datacentrech nebo oblastech. | Tuto možnost zvažte, pokud potřebujete konzistenci, stálost a vysokou dostupnost. Nemusí chránit před regionálním selháním, pokud je trvale ovlivněno více zón.
**Geograficky redundantní úložiště (GRS)** | Chrání před výpadkem celé oblasti tím, že replikuje data do sekundární oblasti, které se nachází stovky kilometrů od primární oblasti. Poskytuje minimálně 99,99999999999999% (16 9) stálost objektů v průběhu daného roku. | Data repliky nemusí být k dispozici, pokud Microsoft nezahájí převzetí služeb při selhání a přechod na sekundární oblast. Pokud dojde k převzetí služeb při selhání, je dostupný přístup pro čtení a zápis.
**Geograficky redundantní úložiště s přístupem pro čtení (RA-GRS)** | Podobné geograficky redundantnímu úložišti (GRS). Poskytuje minimálně 99,99999999999999% (16 9) stálost objektů v průběhu daného roku. | Poskytuje 99,9% dostupnost pro čtení tím, že povolí přístup ke čtení ze sekundární oblasti použité pro GRS.

**Další informace:**

- [Přehled](https://azure.microsoft.com/pricing/details/storage) cen služby Azure Storage
- [Další informace](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) o službě Azure Import/Export pro migraci velkých objemů dat do objektů blob a souborů Azure
- [Srovnání](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) typů dat úložiště objektů blob, souborů a disků
- [Další informace](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o úrovních přístupu
- [Přehled](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) různých typů účtů úložiště
- Další informace o [redundanci úložiště](https://docs.microsoft.com/azure/storage/common/storage-redundancy), [LRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) a [RA-GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-to-data-in-the-secondary-region).
- [Další informace](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) o Azure Files

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Osvědčený postup: Využijte výhod hybridních výhod Azure

Vzhledem k mnohaletým softwarovým investicím do systémů, jako jsou Windows Server a SQL Server, je Microsoft v jedinečné pozici, aby zákazníkům mohl nabídnout hodnotu v cloudu se značnými slevami, které ostatní poskytovatelé cloudu nemusí nutně poskytovat.

Portfolio integrovaných místní produktů a produktů Azure od Microsoftu přináší konkurenční a cenové výhody. Pokud v současné době máte operační systém nebo jiný software licencovaný prostřednictvím Software Assurance (SA), díky zvýhodněnému hybridnímu využití Azure si můžete tyto licence přenést i do cloudu.

**Další informace:**

- [Prohlídka](https://azure.microsoft.com/pricing/hybrid-benefit) kalkulačky úspor pro zvýhodněné hybridní využití
- [Další informace](https://azure.microsoft.com/pricing/hybrid-benefit) o zvýhodněném hybridním využití pro Windows Server
- [Doprovodné materiály](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) k cenám pro virtuální počítače Azure s SQL Serverem

## <a name="best-practice-use-reserved-vm-instances"></a>Osvědčený postup: použití rezervované instance virtuálních počítačů

Většina cloudových platforem se nastavuje na průběžné platby. Tento model ale má nevýhody, protože nemusíte nutně vědět, jak dynamické úlohy budou. Stanovením jasných záměrů úlohy přispějete k plánování infrastruktury.

Při použití služby Azure Reserved VM Instances si předplatíte instanci virtuálního počítače na jeden nebo tři roky.

- Při platbě předem získáte slevu na používané prostředky.
- Můžete výrazně snížit náklady na virtuální počítač, výpočetní prostředky SQL Database, Azure Cosmos DB a další prostředky, a to až o 72 % oproti průběžným platbám.
- Rezervace poskytují slevu z faktury a neovlivňují běhový stav prostředků.
- Rezervované instance můžete zrušit.

![Rezervované instance](./media/migrate-best-practices-costs/reserve.png)
*Rezervované virtuální počítače Azure*

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) o rezervacích Azure
- [Nejčastější dotazy](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) k rezervovaným instancím
- [Doprovodné materiály k cenám](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) pro virtuální počítače Azure s SQL Serverem

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Osvědčený postup: útrata v cloudu agregované napříč předplatnými

Nevyhnutelně se stane, že nakonec budete mít více než jedno předplatné Azure. Můžete například potřebovat další předplatné, abyste oddělili vývoj a produkci, nebo můžete mít platformu, která vyžaduje samostatné předplatné pro každého klienta. Možnost agregace generování sestav dat napříč všemi předplatnými na jednu platformu je neocenitelnou funkcí.

K tomu můžete využít rozhraní API Azure Cost Management. Po agregaci dat do jednoho zdroje, například Azure SQL, můžete pomocí nástrojů, jako je Power BI, zobrazit agregovaná data. Můžete vytvářet agregované sestavy předplatného a podrobné sestavy. Například pro uživatele, kteří potřebují proaktivní přehledy o nákladové správě, můžete vytvořit konkrétní zobrazení nákladů na základě oddělení, skupiny prostředků atd. Nemusíte jim poskytnout úplný přístup k fakturačním datům Azure.

**Další informace:**

- [Přehled](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) rozhraní API Azure Consumption.
- [Další informace](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) o připojení k nabídce Azure Consumption Insights v Power BI Desktopu
- [Postup](https://docs.microsoft.com/azure/billing/billing-manage-access) správy přístup k fakturačním údajům pro Azure pomocí řízení přístupu na základě role (RBAC)

## <a name="after-migration"></a>Po migraci

Po úspěšné migraci úloh a několikatýdenním shromažďování dat o spotřebě budete mít jasnou představu o nákladech na prostředky.

- Při analýze dat můžete začít vytvářet základní rozpočet pro skupiny prostředků a prostředky Azure.
- Poté, jakmile zjistíte, kde dochází k vyčerpávání rozpočtu na cloud, můžete analyzovat, jak dále snížit své náklady.

Osvědčené postupy v této části zahrnují použití služby Azure Cost Management pro vytvoření rozpočtu a analýzu nákladů, monitorování prostředků a implementaci rozpočtů skupin prostředků a optimalizaci monitorování, úložiště a virtuálních počítačů.

## <a name="best-practice-use-azure-cost-management"></a>Osvědčený postup: použití Azure Cost Management

Služba Azure Cost Management od Microsoftu vám pomůže sledovat výdaje:

- Pomáhá vám sledovat a řídit výdaje na Azure a optimalizovat využití prostředků.
- Kontroluje celé předplatné a všechny jeho prostředky a poskytuje doporučení.
- Poskytuje úplné rozhraní API pro integraci externích nástrojů a finančních systémů pro vytváření sestav.
- Sleduje využití prostředků a správu nákladů na cloud pomocí jednoho sjednoceného zobrazení.
- Poskytuje podrobné provozní a finanční přehledy, které vám pomohou činit informovaná rozhodnutí.

Ve službě Cost Management můžete provádět tyto akce:

- **Vytvořit rozpočet:** Vytvořte rozpočet pro finanční zodpovědnost.
  - Můžete začlenit služby, které využíváte, nebo si předplatit jejich odběr na určité období (měsíc, čtvrtletí, rok) a v určitém rozsahu (předplatná/skupiny prostředků). Můžete si například vytvořit rozpočet na předplatné Azure na dobu jednoho měsíce, čtvrtletí nebo rok.
    - Vytvořený rozpočet se zobrazí v analýze nákladů. Zobrazení rozpočtu oproti aktuálním výdajům je prvním krokem, který je nutné udělat při analýze nákladů a výdajů.
  - Při dosažení rozpočtového prahu si můžete nechat e-mailem poslat oznámení.
  - Za účelem analýzy můžete data správy nákladů exportovat do úložiště Azure.

    ![Rozpočet ve službě Cost Management](./media/migrate-best-practices-costs/budget.png)
    *Rozpočet ve službě Azure Cost Management*

- **Proveďte analýzu nákladů:** Získejte nákladovou analýzu, která vám pomůže prozkoumat a analyzovat náklady na vaši organizaci, abyste zjistili, jak se účtují náklady, a identifikovat trendy útraty.
  - Analýza nákladů je k dispozici uživatelům se smlouvou Enterprise.
  - Data analýzy nákladů můžete zobrazit pro různé rozsahy, včetně oddělení, účtu, předplatného nebo skupiny prostředků.
  - Můžete získat analýzu nákladů, která ukazuje celkové náklady za aktuální měsíc a kumulované denní náklady.

    ![Analýza ve službě Cost Management](./media/migrate-best-practices-costs/analysis.png)
    *Analýza ve službě Azure Cost Management*
- **Získat doporučení:** Získejte doporučení poradce, která vám ukáže, jak můžete optimalizovat a zlepšit efektivitu.

**Další informace:**

- [Přehled](https://docs.microsoft.com/azure/cost-management/overview) služby Azure Cost Management
- [Postup](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices) optimalizace investice do cloudu pomocí služby Azure Cost Management
- [Postup](https://docs.microsoft.com/azure/cost-management/use-reports) využití sestav služby Azure Cost Management
- [Kurz](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) optimalizace nákladů na základě doporučení
- [Přehled](https://docs.microsoft.com/rest/api/consumption/budgets) rozhraní API služby Azure Consumption

## <a name="best-practice-monitor-resource-utilization"></a>Osvědčený postup: monitorování využití prostředků

V Azure platíte za to, co používáte, a to pouze tehdy, když prostředky využíváte. U virtuálních počítačů se poplatky účtují při jejich přidělení. Po jejich uvolnění se poplatky neúčtují. S ohledem na to byste měli sledovat používané virtuální počítače a kontrolovat jejich velikost.

- Průběžně vyhodnocujte úlohy virtuálního počítače, abyste stanovili standardní hodnoty.
- Pokud se například úloha intenzivně využívá od pondělí do pátku v době od 8 do 18 hodin, ale mimo tuto dobu jen velmi málo, můžete mimo špičku virtuální počítač downgradovat. To znamená, že změníte velikosti virtuálních počítačů, nebo pomocí škálovací sady virtuálních počítačů automaticky vertikálně navýšíte nebo snížíte kapacitu virtuálních počítačů.
- Některé společnosti virtuální počítače „uspí“ tak, že v kalendáři nastaví, kdy by měly být k dispozici a kdy nejsou potřeba.
- Kromě virtuálních počítačů byste také měli monitorovat další síťové prostředky, například ExpressRoute a brány virtuálních sítí, abyste věděli, kdy nejsou plně využity a kdy jsou přetíženy.
- Využití virtuálních počítačů můžete monitorovat pomocí nástrojů od Microsoftu, jako jsou Azure Cost Management, Azure Monitor a Azure Advisor. K dispozici máte také nástroje třetích stran.

**Další informace:**

- Přehled služby [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) a [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview)
- [Doporučení](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) k nákladům od služby Advisor
- [Další informace o [optimalizaci nákladů na základě doporučení](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) a [prevenci neočekávaných poplatků](https://docs.microsoft.com/azure/billing/billing-getting-started)]
- Další informace o [sadě nástrojů Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)

## <a name="best-practice-implement-resource-group-budgets"></a>Osvědčený postup: implementace rozpočty skupiny prostředků

Skupiny prostředků se často používají k vyjádření hranic nákladů. Spolu s tímto vzorem používání tým Azure pokračuje ve vývoji nových a vylepšených způsobů sledování a analýzy výdajů na prostředky na různých úrovních, včetně schopnosti vytvářet rozpočty skupin prostředků a prostředků.

- Rozpočet skupiny prostředků vám usnadňuje sledování nákladů přidružených ke skupině prostředků.
- Při dosažení rozpočtu nebo jeho překročení můžete aktivovat upozornění a spouštět nejrůznější playbooky.

**Další informace:**

- [Postup](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) správy nákladů s využitím rozpočtů Azure
- [Kurz](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json) vytváření a správy rozpočtu Azure

## <a name="best-practice-optimize-azure-monitor-retention"></a>Osvědčený postup: optimalizace uchovávání Azure Monitor

Po přesunu prostředků do Azure a povolení protokolování diagnostiky se generuje velké množství dat protokolu. Tato data protokolu se obvykle posílají do účtu úložiště, který je namapován k pracovnímu prostoru Log Analytics.

- Čím delší je doba uchovávání dat protokolu, tím více dat budete mít.
- Všechna data protokolu nejsou stejná a některé prostředky vygenerují více dat protokolu než jiné.
- Vzhledem k předpisům a nutnosti jejich dodržování je pravděpodobné, že budete muset u některých prostředků uchovávat data protokolu déle než u jiných.
- Při optimalizaci nákladů na úložiště protokolů a uchovávání dat protokolu byste měli postupovat opatrně.
- Doporučujeme vyhodnotit a nastavit protokolování ihned po dokončení migrace, abyste zbytečně neutráceli peníze za uchovávání nedůležitých protokolů.

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) o monitorování využití a odhadovaných nákladů

## <a name="best-practice-optimize-storage"></a>Osvědčený postup: optimalizace úložiště

Pokud jste se při migraci řídili osvědčenými postupy, pravděpodobně jste získali určité výhody. Pravděpodobně však existují další náklady na úložiště, které si zaslouží optimalizaci. Postupem času objekty blob a soubory zastarají. Data již možná nikdo nebude používat, ale v souladu se zákonnými požadavky je možná budete muset po určitou dobu uchovávat. Proto je nebude třeba ukládat v úložišti s vysokým výkonem, které jste použili pro původní migraci.

Identifikace a přesun zastaralých dat do levnějších úložných prostorů může mít obrovský dopad na váš měsíční rozpočet na úložiště a na úsporu nákladů. Azure poskytuje řadu způsobů, které vám pomohou identifikovat tato zastaralá data a následně je uložit.

- Využijte výhod úrovní přístupu pro úložiště v2 pro obecné účely, které umožňuje přesunout méně důležitá data z horké úrovně přístupu na studenou a archivní úroveň přístupu.
- StorSimple vám pomůže přesunout zastaralá data na základě přizpůsobených zásad.

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o úrovních přístupu
- [Přehled](https://docs.microsoft.com/azure/azure-monitor/overview) řešení StorSimple a [cen řešení StorSimple](https://azure.microsoft.com/pricing/details/storsimple)

## <a name="best-practice-automate-vm-optimization"></a>Osvědčený postup: automatické optimalizace virtuálních počítačů

Hlavním cílem spouštění virtuálního počítače v cloudu je maximalizace využití procesoru, paměti a disku virtuálním počítačem. Pokud máte neoptimalizované virtuální počítače nebo virtuální počítače, které se často nepoužívají, je rozumné je buď vypnout, nebo vertikálně snížit jejich kapacitu pomocí škálovací sady virtuálních počítačů.

Virtuální počítač můžete optimalizovat pomocí služby Azure Automation, škálovacích sad virtuálních počítačů, automatického vypnutí a skriptovaných řešení nebo řešení od externích dodavatelů.

**Další informace:**

- [Postup](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) použití automatického vertikálního navýšení kapacity
- [Plánování](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) automatického spuštění virtuálního počítače
- [Postup](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) spuštění nebo zastavení virtuálních počítačů mimo špičku ve službě Azure Automation
- [Další informace] o [službě Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) a [sadě nástrojů Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Osvědčené postupy: používání Logic Apps a sady runbook s rozpočty rozhraní API

Azure poskytuje rozhraní REST API, které má přístup k fakturačním údajům vašeho tenanta.

- Pomocí rozhraní API pro rozpočty můžete integrovat externí systémy a pracovní postupy, které se aktivují na základě metrik vytvořených z dat rozhraní API.
- Můžete předat data o využití a prostředcích do preferovaného nástroje pro datové analýzy.
- Rozhraní API využití a ceníku prostředků Azure vám pomohou přesně odhadnout a spravovat vaše náklady.
- Tato rozhraní API se implementují jako poskytovatel prostředků a jsou součástí rozhraní API, která zveřejňuje Azure Resource Manager.
- Rozhraní API pro rozpočty lze integrovat se službou Azure Logic Apps a runbooky.

**Další informace:**

- [Další informace](https://docs.microsoft.com/rest/api/consumption/budgets) o rozhraní API pro rozpočty
- [Přehled](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) využití Azure pomocí rozhraní API pro rozpočty

## <a name="best-practice-implement-serverless-technologies"></a>Osvědčený postup: provedení technologiích bez serverů

Úlohy virtuálního počítače se často migrují „tak, jak jsou“, aby nedocházelo k výpadkům. Virtuální počítače často mohou hostovat úlohy, které jsou přerušované, trvají jen velmi krátce nebo naopak mnoho hodin. Virtuální počítače například mohou spouštět naplánované úlohy, jako jsou skripty služby Plánovač úloh systému Windows nebo powershellové skripty. I když tyto úlohy neběží, stále vám vznikají náklady na virtuální počítač a diskové úložiště.

Po migraci a po důkladném přezkoumání těchto typů úloh můžete zvážit jejich migraci na bezserverové technologie, jako jsou úlohy služby Azure Functions nebo Azure Batch. Díky tomuto řešení už nemusíte spravovat a udržovat virtuální počítače, čímž ušetříte další náklady.

**Další informace:**

- Další informace o službě [Azure Functions](https://azure.microsoft.com/services/functions)
- Další informace o službě [Azure Batch](https://azure.microsoft.com/services/batch)

## <a name="next-steps"></a>Další kroky

Projděte si další osvědčené postupy:

- [Osvědčené postupy](./migrate-best-practices-security-management.md) pro zabezpečení a správu po migraci
- [Osvědčené postupy](./migrate-best-practices-networking.md) pro síťové služby po migraci
