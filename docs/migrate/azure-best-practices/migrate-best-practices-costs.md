---
title: Úlohy s náklady a velikostí migrovány do Azure
description: Rozhraní pro přijetí v cloudu pro Azure použijte k získání osvědčených postupů pro náklady a úlohy, které se migrují do Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: dd8030c884b6c5b66c733080d26f29bb8319740e
ms.sourcegitcommit: d660484d534bc61fc60470373f3fcc885a358219
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508402"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Osvědčené postupy pro úlohy ocenění a změny velikosti migrovat do Azure

Jako je plánování a návrh pro migraci zajišťuje, zaměřuje se na náklady na dlouhodobý úspěch vaší migrace do Azure. Při migraci je nezbytné, aby všechny týmy (například finanční tým, vedení a tým vývoje aplikací) pochopili související náklady.

- Před migrací odhadování migrace náklady, Směrný plán pro měsíčně, čtvrtletně, a je zásadní pro úspěch roční cíle rozpočtu.
- Po dokončení migrace by měla optimalizovat náklady, průběžně monitorovat úlohy a plánovat budoucí využití vzorů. Migrované prostředky můžou zpočátku být jedním typem úlohy, ale postupem času se můžou změnit na jiný typ podle využití, nákladů a měnících se obchodních požadavků.

Tento článek popisuje osvědčené postupy pro výpočet nákladů a nastavování velikosti před a po migraci.

> [!IMPORTANT]
> Osvědčené postupy a názory, které jsou popsané v tomto článku jsou založeny na platformě Azure a služby funkce dostupné v době zápisu. Funkce a možnosti v průběhu času měnit. Ne všechna doporučení může být možné použít pro vaše nasazení, vyberte to, co vám vyhovuje.

## <a name="before-migration"></a>Před migrací

Předtím, než můžete svoje úlohy přesunout do cloudu, odhadněte svoje měsíční náklady spuštěných v Azure. Proaktivní správa nákladů na cloud vám pomůže dodržet váš rozpočet provozních nákladů. Jestliže rozpočet je omezené, vzít v úvahu před migrací. Vezměte v úvahu převod úlohy do Azure technologiích bez serverů, kde je to vhodné, abyste snížili náklady.

Osvědčené postupy v této části vám pomohou odhadnout náklady, zvolit správnou velikost virtuálních počítačů a úložiště, využívat výhod hybridního využití Azure, používat vyhrazené virtuální počítače a odhadnout výdaje na cloud v rámci předplatného.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Osvědčený postup: odhadnout měsíční náklady na úlohy

K předpovědi měsíčních nákladů na migrované úlohy můžete využít několik nástrojů.

- **Cenová Kalkulačka Azure:** Vyberte produkty, které chcete odhadnout, například virtuální počítače a úložiště. Vstup náklady na cenové kalkulačky, sestavit odhad.

 ![cenové kalkulačky Azure](./media/migrate-best-practices-costs/pricing.png) *cenové kalkulačky Azure*

- **Azure Migrate:** K odhadování nákladů potřebujete zkontrolovat a vyhodnotit všechny prostředky, které jsou potřebné ke spouštění vašich úloh v Azure. K získání těchto dat, vytváření inventáře majetku, včetně serverů, virtuálních počítačů, databází a úložiště. Azure Migrate můžete použít ke shromažďování těchto informací.

- Azure Migrate zjistí a vyhodnocuje vaše místní prostředí pro poskytnutí inventář.
- Azure Migrate můžete namapovat a zobrazit závislosti mezi virtuálními počítači, abyste měli ucelený přehled.
- Posouzení služby Azure Migrate obsahuje odhadované náklady.
  - Náklady na výpočetní výkon: pomocí velikost virtuálního počítače Azure, doporučuje se, když vytvoříte posouzení, migrace Azure používá rozhraní API pro fakturaci pro výpočet odhadované měsíční náklady na virtuální počítač. Odhad bere v úvahu operační systém, program software assurance, rezervované instance, virtuálního počítače doby provozu, umístění a nastavení měny. Agreguje náklady ve všech virtuálních počítačích v posouzení a vypočítá celkové měsíční náklady výpočetní prostředky.
  - Náklady na úložiště: Azure Migrate vypočítá agregováním náklady na úložiště všechny virtuální počítače ve vyhodnocení celkové měsíční náklady na úložiště. Na základě agregace měsíční náklady pro všechny disky připojené k němu můžete vypočítat měsíční náklady na úložiště pro konkrétní počítač.

    ![Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    *Hodnocení Azure Migrate*

**Další informace:**

- [Použití](https://azure.microsoft.com/pricing/calculator) cenové kalkulačky Azure
- [Přehled](https://docs.microsoft.com/azure/migrate/migrate-overview) služby Azure Migrate
- [Informace](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) o posouzení Azure Migrate
- [Další informace](https://docs.microsoft.com/azure/dms/dms-overview) o službě Azure Database Migration Service

## <a name="best-practice-right-size-vms"></a>Osvědčený postup: nastavení správné velikosti virtuálních počítačů

Při nasazování virtuálních počítačů Azure si můžete zvolit z různých možností podpory úloh. Každý typ virtuálního počítače má konkrétní funkce a různé kombinace procesoru, paměti a disky. Virtuální počítače jsou seskupeny takto:

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Obecné účely** | Vyvážený poměr procesorů k paměti. | Vhodné pro testování a vývoj, malé a střední databáze a webové servery s nízkým až středním provozem.
**Optimalizované z hlediska výpočetních prostředků** | Vysoký poměr procesorů k paměti. | Vhodné pro webové servery se středním provozem, síťová zařízení, dávkové procesy a aplikační servery.
**Paměťově optimalizované** | Vysoké paměti na-využití procesoru. | Vhodné pro relační databáze, střední a velké mezipaměti a analýzu v paměti.
**Optimalizované z hlediska úložiště** | Vysoká propustnost disku a V/V. | Vhodné pro velké objemy dat, databáze SQL a NoSQL.
**Optimalizované z hlediska GPU** | Specializované virtuální počítače. Jeden nebo více grafickými procesory. | Silná grafiky a úpravy videa.
**Vysoký výkon** | Nejrychlejší a procesorově nejvýkonnější procesoru. Virtuální počítače s volitelné vysokou propustnost síťového rozhraní (RDMA) | Kritické vysoce výkonné aplikace.

- Je důležité pochopit rozdíly v cenách tyto virtuální počítače a dlouhodobé účinky rozpočtu.
- Každý typ zahrnuje několik řad virtuálních počítačů.
- Kromě toho při výběru virtuálního počítače v rámci řady, je možné pouze škálovat virtuálního počítače navýšení nebo snížení kapacity v rámci této řady. Kapacitu virtuálního počítače DSv2\_2 můžete například navýšit na DSv2\_4, ale nemůžete ho změnit na jinou řadu, jako je Fsv2\_2.

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) o typech a určování velikosti virtuálních počítačů a mapování velikostí k typům
- [Plánování](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs) velikostí virtuálních počítačů
- [Přehled](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) ukázkového hodnocení pro fiktivní společnost Contoso

## <a name="best-practice-select-the-right-storage"></a>Osvědčený postup: vyberte správné úložiště

Ladění a udržování místního úložiště (sítě SAN nebo NAS) a sítě pro podporu, může být drahá a časově náročné. Data souborů (úložiště) je obvykle migrovat do cloudu a vyřešit provozní a správu obrovskému. Společnost Microsoft poskytuje několik možností pro přesun dat do Azure a budete muset učinit rozhodnutí o těchto možnostech. Vybrat správný typ úložiště pro data můžete uložit vaše organizace několik tisíc dolarů měsíčně. Několik důležitých informací:

- Data, která se nedají použít hodně a nejsou nepostradatelná, nemusí být umístěna na nejlevnějších úložištích.
- Naopak důležité důležitých podnikových dat se musí nacházet na vyšší úroveň možností úložiště.
- Při plánování migrace proveďte inventarizaci dat a klasifikovat podle důležitosti, abyste mohli mapovat na nejvhodnějšího úložiště. Vezměte v úvahu rozpočtu a nákladů, jakož i výkonu. Náklady by neměl být nutně faktor hlavní rozhodování. Výběr možnosti nejlevnější může zpřístupnit úloh na výkon a dostupnost rizika.

### <a name="storage-data-types"></a>Typy úložiště dat

Azure poskytuje různé typy dat úložiště.

<!--markdownlint-disable MD033 -->

**Datový typ** | **Podrobnosti** | **Použití**
--- | --- |  ---
**Objekty blob** | Optimalizovaná pro ukládání velkých objemů nestrukturovaných objektů, jako jsou textová nebo binární data<br/><br/> | Přístup k datům odkudkoli přes protokol HTTP/HTTPS. | Používá se pro scénáře datových proudů a náhodný přístup. Například k předávání obrázků a dokumentů přímo do prohlížeče, streamování Vida a zvuku a ukládání dat pro obnovení zálohování a po havárii.
**Soubory** | Spravované sdílené složky přístupné přes protokol SMB 3.0 | Použít při migraci místních sdílených složek a k poskytování více/připojení k datům souborů.
**Disky** | Založené na objekty BLOB stránky.<br/><br/> Typ (rychlost) disku: standardní (pevný disk nebo SSD) nebo Premium (SSD).<br/><br/>Správa na disku: nespravovaných (můžete spravovat nastavení disku a úložiště) nebo spravované (vyberte typ disku a Azure spravuje za vás disk). | Použijte disky úrovně Premium pro virtuální počítače. Použití spravovaných disků pro jednoduchá správa a škálování.
**Fronty** | Store a načítání velkého počtu zpráv, které jsou přístupné prostřednictvím ověřených volání (HTTP nebo HTTPS) | Připojení aplikace součástí pomocí asynchronních zpráv zařazení do fronty.
**Tabulky** | Store tabulky. | Nyní součástí rozhraní API tabulky Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Úrovně přístupu

Azure storage nabízí různé možnosti pro přístup k datům objektu blob bloku. Vyberte úroveň přístupu pomáhá zajistit, ukládání dat objektů blob bloku cenově nejvýhodnější způsobem.

<!--markdownlint-disable MD033 -->

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Horká** | Vyšší náklady než studené úložiště. Nižší poplatky za přístup než Cool.<br/><br/>Toto je výchozí úroveň. | Použijte pro data v aktivní použití, které se využívají často.
**Studená** | Nižší náklady na úložiště než horká. Vyšší poplatky za přístup než aktivní.<br/><br/> Store pro minimálně za 30 dní. | Krátkodobé na Store, data jsou k dispozici, ale jenom zřídka.
**Archiv** | Používá se pro objekty BLOB bloku jednotlivé.<br/><br/> Většina cenově výhodnější variantou při úložiště. Přístup k datům je nákladnější než horká a studená. | Používá se pro data, která se toleruje latence načtení server hodin a bude i nadále ve vrstvě nejméně 180 dnů.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy účtů úložiště

Azure poskytuje různé typy účtů úložiště a úrovně výkonu.

<!--markdownlint-disable MD033 -->

**Typ účtu** | **Podrobnosti** | **Použití**
--- | --- | ---
**Obecné účely v2 Standard** | Podporuje objekty BLOB (bloku, stránky, připojení), soubory, disky, fronty a tabulky.<br/><br/> Podporuje vrstvami přístupu Hot, Cool a Archive. ZRS se podporuje. | Používá se pro většinu scénářů a většinu typů data. Účty úložiště úrovně Standard mohou být založeny na discích HDD nebo SSD.
**Obecné účely v2 Premium** | Podporuje data objektů Blob storage (objekty BLOB stránky). Podporuje vrstvami přístupu Hot, Cool a Archive. ZRS se podporuje.<br/><br/> Uložené na SSD. | Microsoft doporučuje používat pro všechny virtuální počítače.
**Obecné účely v1** | Nepodporuje přístup vrstvení. Nepodporuje ZRS | Použijte, pokud aplikace potřebují modelu nasazení Azure classic.
**Objekt blob** | Specializovaný účet úložiště pro ukládání nestrukturovaných objektů. Poskytuje objekty BLOB bloku a doplňovacích objektů BLOB pouze (žádný soubor, fronty, tabulky nebo Disk úložiště služby). Poskytuje stejnou odolnost, dostupnost, škálovatelnost a výkon jako obecné účely v2. | v těchto účtech nejde ukládat objekty BLOB stránky a proto Nejde uložit soubory virtuálního pevného disku. Můžete nastavit na horkou nebo studenou úroveň přístupu.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Možnosti redundance služby Storage

Účty úložiště můžete použít různé typy redundance pro odolnost a vysoká dostupnost.

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Místně redundantní úložiště (LRS)** | Chrání proti místní výpadek replikací v rámci jednoho úložiště jednotky doména samostatné selhání a aktualizační doména. Udržuje několik kopií vašich dat v jednom datacentru. Poskytuje minimálně 99,999999999% (11 9) stálost objektů v průběhu daného roku. | Zvažte, pokud aplikace ukládá data, která můžou být snadno znovu vytvořena.
**Zónově redundantní úložiště (ZRS)** | Chrání znovu k výpadku datového centra pomocí replikace mezi clustery tři úložiště v jedné oblasti. Každý cluster úložiště je fyzicky oddělené a je umístěn ve své vlastní zónu dostupnosti. Poskytuje minimálně 99,9999999999% (12 9) odolnost objektů v průběhu daného roku díky uchovávání několika kopií dat v několika datacentrech nebo oblastech. | Zvažte, pokud potřebujete konzistenci, odolnost a vysokou dostupnost. Nemusí chránit před regionálním selháním, pokud je trvale ovlivněno více zón.
**Geograficky redundantní úložiště (GRS)** | Replikuje data do sekundární oblasti vzdálené stovky mil od primární chrání před výpadku celé oblasti. Poskytuje minimálně 99,99999999999999% (16 9) stálost objektů v průběhu daného roku. | Data repliky není k dispozici, pokud Microsoft nezahájí převzetí služeb při selhání do sekundární oblasti. Pokud dojde k převzetí služeb při selhání, je k dispozici oprávnění ke čtení a zápisu.
**Geograficky redundantní úložiště s přístupem pro čtení (RA-GRS)** | Podobně jako u GRS. Poskytuje minimálně 99,99999999999999% (16 9) stálost objektů v průběhu daného roku. | Poskytuje a 99,99 % dostupnosti čtení tím, že povolíte přístup pro čtení z druhé oblasti používané pro geograficky redundantní úložiště.

**Další informace:**

- [Přehled](https://azure.microsoft.com/pricing/details/storage) cen služby Azure Storage
- [Další informace](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) o službě Azure Import/Export pro migraci velkých objemů dat do objektů blob a souborů Azure
- [Srovnání](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) typů dat úložiště objektů blob, souborů a disků
- [Další informace](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o úrovních přístupu
- [Přehled](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) různých typů účtů úložiště
- Další informace o [redundanci úložiště](https://docs.microsoft.com/azure/storage/common/storage-redundancy), [LRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) a [RA-GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-to-data-in-the-secondary-region).
- [Další informace](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) o Azure Files

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Osvědčený postup: Využijte výhod hybridních výhod Azure

Z důvodu let softwaru investice do systémů, jako jsou Windows Server a SQL Server Microsoft je jedinečné pozici nabízet zákazníkům hodnotu v cloudu pomocí podstatné slevy, které nutně neposkytuje jiných poskytovatelů cloudových služeb.

Integrované portfolio typu místní nebo Azure produktu Microsoft generuje výhody konkurenceschopnost a nákladů. Pokud máte aktuálně operačního systému nebo jinými nabídkami licencování softwaru prostřednictvím programu software assurance (SA), můžete využít tyto licence s vámi do cloudu s programem Azure Hybrid Benefit.

**Další informace:**

- [Prohlídka](https://azure.microsoft.com/pricing/hybrid-benefit) kalkulačky úspor pro zvýhodněné hybridní využití
- [Další informace](https://azure.microsoft.com/pricing/hybrid-benefit) o zvýhodněném hybridním využití pro Windows Server
- [Doprovodné materiály](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) k cenám pro virtuální počítače Azure s SQL Serverem

## <a name="best-practice-use-reserved-vm-instances"></a>Osvědčený postup: použití rezervované instance virtuálních počítačů

Většina cloudových platformách jsou nastaveny jako s průběžnými platbami. Tento model představuje nevýhody, protože zatím nevíte nutně dynamické úlohy budou. Při zadávání vymazat záměry úloh můžete přispět k plánování infrastruktury.

Pomocí služby Azure Reserved VM instances, si Předplatíte jeden nebo tři roky instance virtuálního počítače.

- Zálohy poskytuje a uplatnit tak slevu na prostředky, které používáte.
- Virtuální počítač, výpočetní databáze SQL, Azure Cosmos DB nebo další náklady na prostředky může výrazně snížit až o 72 % oproti průběžným platbám.
- Rezervace poskytovat fakturační slevy a neovlivní jejich běhový stav vašich prostředků.
- Rezervované instance můžete zrušit.

![Rezervované instance](./media/migrate-best-practices-costs/reserve.png)
*Rezervované virtuální počítače Azure*

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) o rezervacích Azure
- [Nejčastější dotazy](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) k rezervovaným instancím
- [Doprovodné materiály k cenám](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) pro virtuální počítače Azure s SQL Serverem

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Osvědčený postup: útrata v cloudu agregované napříč předplatnými

Je nevyhnutelné, že nakonec budete mít více než jedno předplatné Azure. Například můžete potřebovat další předplatné k oddělení vývoje a provozu hranice, nebo můžete mít platformu, která vyžaduje samostatné předplatné pro každého klienta. Možnost agregovaných dat, vytváření sestav napříč všemi předplatnými do jedné platformy je důležité funkce.

K tomuto účelu můžete použít Azure Cost Management API. Potom po agregace dat do jednoho zdroje jako Azure SQL, můžete použít nástroje, jako je Power BI k poskytování agregovaná data. Můžete vytvořit sestavy agregované předplatného a podrobné sestavy. Například pro uživatele, kteří potřebují proaktivní přehledy o nákladové správě, můžete vytvořit konkrétní zobrazení nákladů na základě oddělení, skupiny prostředků nebo jiných informací. Není nutné jim poskytnout úplný přístup k Azure fakturačních údajů.

**Další informace:**

- [Přehled](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) rozhraní API Azure Consumption.
- [Další informace](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) o připojení k nabídce Azure Consumption Insights v Power BI Desktopu
- [Postup](https://docs.microsoft.com/azure/billing/billing-manage-access) správy přístup k fakturačním údajům pro Azure pomocí řízení přístupu na základě role (RBAC)

## <a name="after-migration"></a>Po migraci

Po úspěšné migraci úloh a pár týdnů, shromažďovat data o spotřebě budete mít jasnou představu o nákladech na prostředky.

- Jak je můžete analyzovat data, můžete začít generovat rozpočtu směrný plán pro skupiny prostředků Azure a prostředky.
- Poté jak porozumíte, kde je využita rozpočtu cloudu, můžete analyzovat jak snížit náklady a další.

Osvědčené postupy v této části zahrnují náklady na plánování rozpočtu a analýz, monitorování prostředků a provádění rozpočty skupiny prostředků a optimalizaci monitorování úložiště a virtuálních počítačů pomocí Azure Cost Management.

## <a name="best-practice-use-azure-cost-management"></a>Osvědčený postup: použití Azure Cost Management

Služba Azure Cost Management od Microsoftu vám pomůže sledovat výdaje:

- Umožňuje sledovat a řídit útraty Azure a optimalizovat využití prostředků.
- Revize, celý předplatného a všechny její prostředky a poskytuje doporučení.
- Poskytuje úplné rozhraní API, integrace externích nástrojů a finančních systémů pro vytváření sestav.
- Sleduje využití prostředků a spravovat náklady na cloud pomocí jednoho unifikovaného zobrazení.
- Obsahuje provozní a finanční informace, které vám pomůže přijímat podložená rozhodnutí.

Ve službě Cost Management můžete:

- **Vytvořit rozpočet:** Vytvořte rozpočet pro finanční zodpovědnost.
  - Můžete začlenit služby, které využíváte, nebo si předplatit jejich odběr na určité období (měsíc, čtvrtletí, rok) a v určitém rozsahu (předplatná/skupiny prostředků). Například můžete vytvořit rozpočtu předplatné Azure pro každý měsíc, čtvrtletí nebo roční období.
    - Po vytvoření rozpočtu, se zobrazí v analýze nákladů. Zobrazení vašemu rozpočtu na aktuální útratu je jedním z prvních kroků při analýze nákladů a výdajů.
  - E-mailová oznámení lze odesílat, když se dosáhne prahové hodnoty.
  - Náklady na správu dat můžete exportovat do úložiště Azure pro účely analýzy.

    ![Rozpočet ve službě Cost Management](./media/migrate-best-practices-costs/budget.png)
    *Rozpočet ve službě Azure Cost Management*

- **Proveďte analýzu nákladů:** Získejte nákladovou analýzu, která vám pomůže prozkoumat a analyzovat náklady na vaši organizaci, abyste zjistili, jak se účtují náklady, a identifikovat trendy útraty.
  - Analýza nákladů je k dispozici uživatelům EA.
  - Data analýzy nákladů můžete zobrazit pro různé rozsahy, včetně oddělení, účtu, předplatného nebo skupiny prostředků.
  - Můžete získat analýzy nákladů, který ukazuje celkové náklady pro aktuální měsíc a celkové denní náklady.

    ![Analýza ve službě Cost Management](./media/migrate-best-practices-costs/analysis.png)
    *Analýza ve službě Azure Cost Management*
- **Získat doporučení:** Získejte doporučení poradce, která vám ukáže, jak můžete optimalizovat a zlepšit efektivitu.

**Další informace:**

- [Přehled](https://docs.microsoft.com/azure/cost-management/overview) služby Azure Cost Management
- [Postup](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices) optimalizace investice do cloudu pomocí služby Azure Cost Management
- [Postup](https://docs.microsoft.com/azure/cost-management/use-reports) využití sestav služby Azure Cost Management
- [Kurz](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) optimalizace nákladů na základě doporučení
- [Přehled](https://docs.microsoft.com/rest/api/consumption/budgets) rozhraní API služby Azure Consumption

## <a name="best-practice-monitor-resource-utilization"></a>Osvědčený postup: monitorování využití prostředků

V Azure platíte za to, co používáte, a to pouze tehdy, když prostředky využíváte. Pro virtuální počítače fakturace dochází, když je přidělen virtuálnímu počítači a se vám neúčtují poplatky po zrušení přidělení virtuálního počítače. S myslete na to by měl monitorovat virtuální počítače v použití a ověřte nastavení velikosti virtuálního počítače.

- Průběžně vyhodnoťte úloh virtuálních počítačů k určení směrné plány.
- Například pokud vaše úloha je použít silně od pondělí do pátku, 8: 00 do 18: 00, ale téměř použít mimo tyto hodiny, může snížit virtuálních počítačů mimo špičky. To může znamenat, změna velikosti virtuálního počítače nebo použijete virtuálního počítače škálovací sady do virtuálních počítačů automatického škálování směrem nahoru nebo dolů.
- Některé společnosti "připomenout znovu", virtuální počítače tak, že je vložíte v kalendáři, který určuje, kdy by měla být k dispozici, a pokud nejsou potřeba.
- Kromě monitorování virtuálních počítačů, měli byste sledovat další síťové prostředky, jako je například ExpressRoute a brány virtuální sítě pro v a využití.
- Využití virtuálních počítačů můžete monitorovat pomocí nástrojů od Microsoftu, jako jsou Azure Cost Management, Azure Monitor a Azure Advisor. Nástroje třetích stran jsou také k dispozici.

**Další informace:**

- Přehled služby [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) a [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview)
- [Doporučení](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) k nákladům od služby Advisor
- [Další informace o [optimalizaci nákladů na základě doporučení](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) a [prevenci neočekávaných poplatků](https://docs.microsoft.com/azure/billing/billing-getting-started)]
- Další informace o [sadě nástrojů Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)

## <a name="best-practice-implement-resource-group-budgets"></a>Osvědčený postup: implementace rozpočty skupiny prostředků

Skupiny prostředků se často používají k reprezentaci hranice náklady. Společně se tento vzor využití pokračuje v týmu Azure pro vývoj nové a vylepšené způsoby, jak sledovat a analyzovat prostředky na různých úrovních, včetně možnosti vytvořit rozpočet na skupinu prostředků a prostředky.

- Rozpočet skupiny prostředků umožňuje sledovat náklady spojené s skupinu prostředků.
- Můžete aktivovat výstrahy a pracovat širokou škálu playbooky je dosáhli nebo Přesáhli jste rozpočtu.

**Další informace:**

- [Postup](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) správy nákladů s využitím rozpočtů Azure
- [Kurz](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json) vytváření a správy rozpočtu Azure

## <a name="best-practice-optimize-azure-monitor-retention"></a>Osvědčený postup: optimalizace uchovávání Azure Monitor

Při přesunu prostředků do Azure a povolení protokolování diagnostiky pro ně se vygeneroval velké množství dat protokolu. Tato data protokolu se obvykle odešle na účet úložiště, který je namapovaný na pracovní prostor Log Analytics.

- Čím delší dobu uchování dat protokolů, čím více dat budete mít.
- Ne všechna data protokolu se rovná a několik zdrojů informací, vygeneruje další data protokolu než jiné.
- Z důvodu dodržování předpisů a nařízení je pravděpodobné, že bude nutné zachovat data protokolu pro několik zdrojů informací, který je delší než jiné.
- Pozor, řádek by měl procházet mezi optimalizovat náklady na úložiště vašich protokolů a ponecháním dat protokolu, které potřebujete.
- Doporučujeme, abyste vaše rozhodnutí vyzkoušet a nastavení protokolování okamžitě po dokončení migrace, takže nejsou útraty peníze uchování protokolů žádný význam.

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) o monitorování využití a odhadovaných nákladů

## <a name="best-practice-optimize-storage"></a>Osvědčený postup: optimalizace úložiště

Pokud jste postupovali podle osvědčené postupy pro výběr úložiště před migrací, jsou pravděpodobně využívat některé výhody. Existují ale náklady pravděpodobně další úložiště, které můžete dál optimalizovat. V čase soubory a objekty BLOB jsou pak zastaralá. Data se možná nepoužívají už ale zákonných požadavků může znamenat, že je potřeba zachovat určitou dobu. V důsledku toho nemusí musíte uložit na vysoce výkonné úložiště, který jste použili pro původní migrace.

Identifikace a přesunutím zastaralá data do oblastí levnější úložiště můžete mít velký dopad na vaše měsíční úložiště rozpočtu a úspory nákladů. Azure poskytuje mnoho způsobů, jak vám pomohou identifikovat a poté uložit tato data zastaralá.

- Využijte výhod úrovně přístupu pro úložiště pro obecné účely v2, přesun méně důležitá data z horké úrovně do úrovně Cool a archivace.
- Pomocí StorSimple přesunout zastaralých dat podle vlastních zásad.

**Další informace:**

- [Další informace](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o úrovních přístupu
- [Přehled](https://docs.microsoft.com/azure/azure-monitor/overview) řešení StorSimple a [cen řešení StorSimple](https://azure.microsoft.com/pricing/details/storsimple)

## <a name="best-practice-automate-vm-optimization"></a>Osvědčený postup: automatické optimalizace virtuálních počítačů

Konečným cílem spuštění virtuálního počítače v cloudu je pro maximalizaci procesoru, paměti a disku, který ji používá. Pokud máte neoptimalizované virtuální počítače nebo virtuální počítače, které se často nepoužívají, je rozumné je buď vypnout, nebo vertikálně snížit jejich kapacitu pomocí škálovací sady virtuálních počítačů.

Virtuální počítač můžete optimalizovat pomocí služby Azure Automation, škálovacích sad virtuálních počítačů, automatického vypnutí a skriptovaných řešení nebo řešení od externích dodavatelů.

**Další informace:**

- [Postup](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) použití automatického vertikálního navýšení kapacity
- [Plánování](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) automatického spuštění virtuálního počítače
- [Postup](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) spuštění nebo zastavení virtuálních počítačů mimo špičku ve službě Azure Automation
- [Další informace] o [službě Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) a [sadě nástrojů Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Osvědčené postupy: používání Logic Apps a sady runbook s rozpočty rozhraní API

Azure poskytuje rozhraní REST API, který má přístup k fakturačním údajům vašeho tenanta.

- Integrace externích systémů a pracovní postupy, které jsou aktivovány metriky, které vytvoříte z dat rozhraní API můžete použít rozpočty rozhraní API.
- Do nástroje pro vaše preferované datové analýzy, si můžete vyžádat data o využití a prostředků.
- Rozhraní API využití a ceníku prostředků Azure vám pomohou přesně odhadnout a spravovat vaše náklady.
- Rozhraní API se implementují jako poskytovatele prostředků a jsou zahrnuty v rozhraní API pomocí Azure Resource Manageru.
- Rozhraní API rozpočty je možné integrovat s Azure Logic Apps a sady Runbook.

**Další informace:**

- [Další informace](https://docs.microsoft.com/rest/api/consumption/budgets) o rozhraní API pro rozpočty
- [Přehled](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) využití Azure pomocí rozhraní API pro rozpočty

## <a name="best-practice-implement-serverless-technologies"></a>Osvědčený postup: provedení technologiích bez serverů

Úlohy virtuálních počítačů se migrují často "tak jak jsou" výpadky. Často virtuálních počítačů může hostovat úlohy, které jsou k nim dochází přerušovaně, s ohledem na krátkou dobu pro spuštění, nebo můžete také mnoho hodin. Například virtuální počítače, na kterých běží naplánované úlohy, jako je například Windows úloh plánovače nebo skripty prostředí PowerShell. Pokud tyto úlohy nejsou spuštěné, jste však zajistit plynulý provoz virtuálního počítače a náklady na úložiště na disku.

Po dokončení migrace po důkladné revizi z těchto typů úloh zvažte migraci na technologiích bez serverů, jako je například úlohy Azure Functions nebo Azure Batch. Díky tomuto řešení už nemusíte spravovat a udržovat virtuální počítače, čímž ušetříte další náklady.

**Další informace:**

- Další informace o službě [Azure Functions](https://azure.microsoft.com/services/functions)
- Další informace o službě [Azure Batch](https://azure.microsoft.com/services/batch)

## <a name="next-steps"></a>Další kroky

Přečtěte si doporučené postupy:

- [Osvědčené postupy](./migrate-best-practices-security-management.md) pro zabezpečení a správu po migraci
- [Osvědčené postupy](./migrate-best-practices-networking.md) pro síťové služby po migraci
