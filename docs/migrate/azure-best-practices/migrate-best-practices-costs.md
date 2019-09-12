---
title: Osvědčené postupy pro úlohy ocenění a změny velikosti migrovat do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Získejte osvědčené postupy pro určování nákladů a velikostí úloh migrovaných do Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 99255722c28b9bb6c33f78e226cb8135e7c7be17
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825988"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Osvědčené postupy pro úlohy ocenění a změny velikosti migrovat do Azure

Zaměřením se na náklady při plánování a návrhu migrace zajistíte dlouhodobý úspěch migrace do Azure. Při migraci je nezbytné, aby všechny týmy (například finanční tým, vedení a tým vývoje aplikací) pochopili související náklady.

- Klíčem k úspěchu je odhad výdajů na migraci a stanovení základních měsíčních, čtvrtletních a ročních rozpočtových cílů ještě před migrací.
- Po dokončení migrace by měla optimalizovat náklady, průběžně monitorovat úlohy a plánovat budoucí využití vzorů. Migrované prostředky můžou zpočátku být jedním typem úlohy, ale postupem času se můžou změnit na jiný typ podle využití, nákladů a měnících se obchodních požadavků.

Tento článek popisuje osvědčené postupy pro výpočet nákladů a nastavování velikosti před a po migraci.

> [!IMPORTANT]
> Osvědčené postupy a názory, které jsou popsané v tomto článku jsou založeny na platformě Azure a služby funkce dostupné v době zápisu. Funkce a možnosti v průběhu času měnit. Ne všechna doporučení může být možné použít pro vaše nasazení, vyberte to, co vám vyhovuje.

## <a name="before-migration"></a>Před migrací

Než přesunete úlohy do cloudu, proveďte odhad měsíčních nákladů na jejich provoz v Azure. Proaktivní správa nákladů na cloud vám pomůže dodržet váš rozpočet provozních nákladů. Pokud máte omezený rozpočet, vezměte to před migrací v úvahu. Tam, kde je to vhodné, zvažte převod úloh na bezserverové technologie Azure.

Osvědčené postupy v této části vám pomohou odhadnout náklady, zvolit správnou velikost virtuálních počítačů a úložiště, využívat výhod hybridního využití Azure, používat vyhrazené virtuální počítače a odhadnout výdaje na cloud v rámci předplatného.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Osvědčený postup: Odhad měsíčních nákladů na úlohy

K předpovědi měsíčních nákladů na migrované úlohy můžete využít několik nástrojů.

- **Cenová kalkulačka Azure:** Vyberete produkty, které chcete odhadnout, například virtuální počítače a úložiště. Do cenové kalkulačky zadáte vstupní náklady a vytvoříte odhad.

 ![Cenová kalkulačka Azure](./media/migrate-best-practices-costs/pricing.png) *Cenová kalkulačka Azure*

- **Azure Migrate:** Pokud chcete odhadnout náklady, musíte zkontrolovat a vzít v úvahu všechny prostředky, které budete potřebovat pro provoz úloh v Azure. Tato data získáte tak, že vytvoříte inventář prostředků, včetně serverů, virtuálních počítačů, databází a úložiště. Azure Migrate můžete použít ke shromažďování těchto informací.

- Azure Migrate zjistí a vyhodnocuje vaše místní prostředí pro poskytnutí inventář.
- Azure Migrate můžete namapovat a zobrazit závislosti mezi virtuálními počítači, abyste měli ucelený přehled.
- Hodnocení Azure Migrate obsahuje odhadované náklady.
  - Náklady na výpočetní prostředky: K výpočtu odhadu měsíčních nákladů na virtuální počítač služba Azure Migrate použije rozhraní API pro fakturaci a velikost virtuálního počítače Azure doporučenou při vytváření hodnocení. V odhadu služba zohlední operační systém, zajištění softwaru, vyhrazené instance, provozuschopnost virtuálního počítače, umístění a nastavení měny. V rámci hodnocení agreguje náklady související se všemi virtuálními počítači a vypočítá celkové měsíční náklady na výpočetní služby.
  - Náklady na úložiště: Azure Migrate v hodnocení vypočítá celkové měsíční náklady na úložiště tak, že agreguje náklady na úložiště všech virtuálního počítačů. Měsíční náklady na úložiště pro konkrétní počítač můžete vypočítat agregací měsíčních nákladů na všechny disky, které jsou k němu připojeny.

    ![Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    *Hodnocení Azure Migrate*

**Další informace:**

- [Použití](https://azure.microsoft.com/pricing/calculator) cenovou kalkulačku Azure.
- [Získejte přehled](/azure/migrate/migrate-overview) Azure Migrate.
- [Informace](/azure/migrate/concepts-assessment-calculation) o posouzení Azure Migrate
- [Další informace](/azure/dms/dms-overview) o službě Azure Database Migration Service

## <a name="best-practice-right-size-vms"></a>Osvědčený postup: Správná velikost virtuálních počítačů

Při nasazování virtuálních počítačů Azure si můžete zvolit z různých možností podpory úloh. Každý virtuální počítač má specifické funkce a různé kombinace procesoru, paměti a disků. Virtuální počítače jsou seskupeny takto:

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Obecné účely** | Vyvážený poměr procesorů k paměti. | Vhodné pro testování a vývoj, malé a střední databáze a webové servery s nízkým až středním provozem.
**Optimalizované z hlediska výpočetních prostředků** | Vysoký poměr procesorů k paměti. | Vhodné pro webové servery se středním provozem, síťová zařízení, dávkové procesy a aplikační servery.
**Paměťově optimalizované** | Vysoký poměr paměti k procesoru. | Vhodné pro relační databáze, střední a velké mezipaměti a analýzu v paměti.
**Optimalizované z hlediska úložiště** | Vysoká propustnost disku a V/V. | Vhodné pro velké objemy dat, databáze SQL a NoSQL.
**Optimalizované z hlediska GPU** | Specializované virtuální počítače. Jeden nebo více grafickými procesory. | Silná grafiky a úpravy videa.
**Vysoký výkon** | Nejrychlejší a procesorově nejvýkonnější procesoru. Virtuální počítače s volitelné vysokou propustnost síťového rozhraní (RDMA) | Kritické vysoce výkonné aplikace.

- Je důležité porozumět cenovým rozdílům mezi těmito virtuálními počítači a dlouhodobému dopadu na rozpočet.
- Každý typ zahrnuje několik řad virtuálních počítačů.
- Kromě toho, pokud vyberete virtuální počítač v rámci jedné řady, můžete jeho kapacitu vertikálně navýšit a snížit pouze v dané řadě. Například DSv2\_2 můžete vertikálně navýšit kapacitu na DSv2\_4, ale nelze změnit na jinou sérii například Fsv2\_2.

**Víc se uč:**

- [Další informace](/azure/virtual-machines/windows/sizes) o velikostech mapování na typy a velikosti a typy virtuálních počítačů.
- [Plánování](/azure/cloud-services/cloud-services-sizes-specs) velikostí virtuálních počítačů
- [Přehled](/azure/migrate/contoso-migration-assessment) ukázkového hodnocení pro fiktivní společnost Contoso

## <a name="best-practice-select-the-right-storage"></a>Osvědčený postup: Výběr správného úložiště

Ladění a údržba místního úložiště (SAN nebo NAS) a sítí, které je podporují, mohou být nákladné a časově náročné. Data souborů (úložiště) je obvykle migrovat do cloudu a vyřešit provozní a správu obrovskému. Společnost Microsoft poskytuje několik možností pro přesun dat do Azure a budete muset učinit rozhodnutí o těchto možnostech. Vybrat správný typ úložiště pro data můžete uložit vaše organizace několik tisíc dolarů měsíčně. Několik důležitých informací:

- Data, která nejsou přístupné a není důležité obchodní informace, nemusí být umístěny v úložišti nejdražší.
- Naopak důležité důležitých podnikových dat se musí nacházet na vyšší úroveň možností úložiště.
- Při plánování migrace proveďte inventarizaci dat a klasifikovat podle důležitosti, abyste mohli mapovat na nejvhodnějšího úložiště. Vezměte v úvahu rozpočtu a nákladů, jakož i výkonu. Náklady by neměl být nutně faktor hlavní rozhodování. Výběr možnosti nejlevnější může zpřístupnit úloh na výkon a dostupnost rizika.

### <a name="storage-data-types"></a>Typy úložiště dat

Azure poskytuje různé typy dat úložiště.

<!--markdownlint-disable MD033 -->

**Datový typ** | **Podrobnosti** | **Použití**
--- | --- |  ---
**Objekty blob** | Optimalizovaná pro ukládání velkých objemů nestrukturovaných objektů, jako jsou textová nebo binární data<br/><br/> | Přístup k datům odkudkoli přes protokol HTTP/HTTPS. | Používá se pro scénáře datových proudů a náhodný přístup. Například k předávání obrázků a dokumentů přímo do prohlížeče, streamování Vida a zvuku a ukládání dat pro obnovení zálohování a po havárii.
**Soubory** | Spravované sdílené složky přístupné přes protokol SMB 3.0 | Použít při migraci místních sdílených složek a k poskytování více/připojení k datům souborů.
**Disky** | Založeno na objektech blob stránky.<br/><br/> Typ disku (rychlost): Standard (HDD nebo SSD) nebo Premium (SSD).<br/><br/>Správa disků: Nespravované (spravujete nastavení disků a úložiště) nebo spravované (vyberete typ disku a Azure ho spravuje za vás). | Pro virtuální počítače se používají disky Premium. Použití spravovaných disků pro jednoduchá správa a škálování.
**fronty** | Store a načítání velkého počtu zpráv, které jsou přístupné prostřednictvím ověřených volání (HTTP nebo HTTPS) | Připojení aplikace součástí pomocí asynchronních zpráv zařazení do fronty.
**Tabulky** | Store tabulky. | Nyní součástí rozhraní API tabulky Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Úrovně přístupu

Azure storage nabízí různé možnosti pro přístup k datům objektu blob bloku. Vyberte úroveň přístupu pomáhá zajistit, ukládání dat objektů blob bloku cenově nejvýhodnější způsobem.

<!--markdownlint-disable MD033 -->

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**za běhu** | Vyšší náklady než studené úložiště. Nižší poplatky za přístup než Cool.<br/><br/>Toto je výchozí úroveň. | Použijte pro data v aktivní použití, které se využívají často.
**Cool** | Nižší náklady na úložiště než horká. Vyšší poplatky za přístup než aktivní.<br/><br/> Store pro minimálně za 30 dní. | Krátkodobé na Store, data jsou k dispozici, ale jenom zřídka.
**Archiv** | Používá se pro objekty BLOB bloku jednotlivé.<br/><br/> Většina cenově výhodnější variantou při úložiště. Přístup k datům je nákladnější než horká a studená. | Používá se pro data, která se toleruje latence načtení server hodin a bude i nadále ve vrstvě nejméně 180 dnů.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy účtů úložiště

Azure poskytuje různé typy účtů úložiště a úrovně výkonu.

<!--markdownlint-disable MD033 -->

**Typ účtu** | **Podrobnosti** | **Použití**
--- | --- | ---
**Obecné účely v2 Standard** | Podporuje objekty BLOB (bloku, stránky, připojení), soubory, disky, fronty a tabulky.<br/><br/> Podporuje vrstvami přístupu Hot, Cool a Archive. ZRS se podporuje. | Používá se pro většinu scénářů a typů dat. Účty úložiště úrovně Standard mohou být založeny na discích HDD nebo SSD.
**Obecné účely v2 Premium** | Podporuje data objektů Blob storage (objekty BLOB stránky). Podporuje vrstvami přístupu Hot, Cool a Archive. ZRS se podporuje.<br/><br/> Uložené na SSD. | Microsoft doporučuje používat pro všechny virtuální počítače.
**Účty pro obecné účely v1** | Nepodporuje přístup vrstvení. Nepodporuje ZRS | Použijte, pokud aplikace potřebují modelu nasazení Azure classic.
**Objekt blob** | Specializovaný účet úložiště pro ukládání nestrukturovaných objektů. Poskytuje objekty BLOB bloku a doplňovacích objektů BLOB pouze (žádný soubor, fronty, tabulky nebo Disk úložiště služby). Poskytuje stejnou odolnost, dostupnost, škálovatelnost a výkon jako obecné účely v2. | v těchto účtech nejde ukládat objekty BLOB stránky a proto Nejde uložit soubory virtuálního pevného disku. Můžete nastavit na horkou nebo studenou úroveň přístupu.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Možnosti redundance služby Storage

Účty úložiště můžete použít různé typy redundance pro odolnost a vysoká dostupnost.

**Typ** | **Podrobnosti** | **Použití**
--- | --- | ---
**Místně redundantní úložiště (LRS)** | Chrání před lokálním výpadkem tím, že se replikuje v rámci jedné jednotky úložiště do samostatné domény selhání a aktualizační domény. Udržuje několik kopií vašich dat v jednom datacentru. Poskytuje alespoň 99,999999999 % (11 9\'s) odolnosti objektů v průběhu daného roku. | Tuto možnost zvažte, pokud aplikace ukládá data, která lze snadno rekonstruovat.
**Zónově redundantní úložiště (ZRS)** | Chrání před výpadkem datacentra tím, že se replikuje ve třech clusterech úložiště v jedné oblasti. Jednotlivé clustery úložiště jsou fyzicky odděleny a umístění ve vlastní zóně dostupnosti. Poskytuje minimálně 99,9999999999% (12 9) odolnost objektů v průběhu daného roku díky uchovávání několika kopií dat v několika datacentrech nebo oblastech. | Tuto možnost zvažte, pokud potřebujete konzistenci, stálost a vysokou dostupnost. Nemusí chránit před regionálním selháním, pokud je trvale ovlivněno více zón.
**Geograficky redundantní úložiště (GRS)** | Chrání před výpadkem celé oblasti tím, že replikuje data do sekundární oblasti, které se nachází stovky kilometrů od primární oblasti. Poskytuje alespoň 99,99999999999999 % (16 9\'s) odolnosti objektů v průběhu daného roku. | Data repliky není k dispozici, pokud Microsoft nezahájí převzetí služeb při selhání do sekundární oblasti. Pokud dojde k převzetí služeb při selhání, je dostupný přístup pro čtení a zápis.
**Geograficky redundantní úložiště s přístupem pro čtení (RA-GRS)** | Podobné geograficky redundantnímu úložišti (GRS). Poskytuje alespoň 99,99999999999999 % (16 9\'s) odolnosti objektů v průběhu daného roku | Poskytuje a 99,99 % dostupnosti čtení tím, že povolíte přístup pro čtení z druhé oblasti používané pro geograficky redundantní úložiště.

**Víc se uč:**

- [Kontrola](https://azure.microsoft.com/pricing/details/storage) ceny za Azure Storage.
- [Další informace o](/azure/storage/common/storage-import-export-service) Azure Import/Export pro migraci velkého objemu dat v objektech BLOB Azure a soubory.
- [Porovnání](/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) objekty BLOB, soubory a disku úložiště datové typy.
- [Další informace](/azure/storage/blobs/storage-blob-storage-tiers) o úrovně přístupu.
- [Kontrola](/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) různé typy účtů úložiště.
- Další informace o [redundance úložiště](/azure/storage/common/storage-redundancy), [LRS](/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), a [Přístupem jen pro čtení](/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-geo-redundant-storage).
- [Další informace](/azure/storage/files/storage-files-introduction) o Azure Files

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Osvědčený postup: Využití výhod zvýhodněného hybridního využití Azure

Vzhledem k mnohaletým softwarovým investicím do systémů, jako jsou Windows Server a SQL Server, je Microsoft v jedinečné pozici, aby zákazníkům mohl nabídnout hodnotu v cloudu se značnými slevami, které ostatní poskytovatelé cloudu nemusí nutně poskytovat.

Integrované portfolio typu místní nebo Azure produktu Microsoft generuje výhody konkurenceschopnost a nákladů. Pokud máte aktuálně operačního systému nebo jinými nabídkami licencování softwaru prostřednictvím programu software assurance (SA), můžete využít tyto licence s vámi do cloudu s programem Azure Hybrid Benefit.

**Víc se uč:**

- [Podívejte se na](https://azure.microsoft.com/pricing/hybrid-benefit) Kalkulačka úspor Hybrid Benefit.
- [Další informace](https://azure.microsoft.com/pricing/hybrid-benefit) o Hybrid Benefit pro Windows Server.
- [Doprovodné materiály](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) k cenám pro virtuální počítače Azure s SQL Serverem

## <a name="best-practice-use-reserved-vm-instances"></a>Osvědčený postup: Použití rezervovaných instancí virtuálních počítačů

Většina cloudových platforem se nastavuje na průběžné platby. Tento model představuje nevýhody, protože zatím nevíte nutně dynamické úlohy budou. Při zadávání vymazat záměry úloh můžete přispět k plánování infrastruktury.

Pomocí služby Azure Reserved VM instances, si Předplatíte jeden nebo tři roky instance virtuálního počítače.

- Zálohy poskytuje a uplatnit tak slevu na prostředky, které používáte.
- Virtuální počítač, výpočetní databáze SQL, Azure Cosmos DB nebo další náklady na prostředky může výrazně snížit až o 72 % oproti průběžným platbám.
- Rezervace poskytovat fakturační slevy a neovlivní jejich běhový stav vašich prostředků.
- Rezervované instance můžete zrušit.

![Rezervované instance](./media/migrate-best-practices-costs/reserve.png)
*vyhrazené virtuální počítače Azure*

**Víc se uč:**

- [Další informace o](/azure/billing/billing-save-compute-costs-reservations) Azure rezervace.
- [Čtení](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) rezervované instance – nejčastější dotazy.
- [Doprovodné materiály k cenám](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) pro virtuální počítače Azure s SQL Serverem

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Osvědčený postup: Agregace výdajů na cloud napříč předplatnými

Nevyhnutelně se stane, že nakonec budete mít více než jedno předplatné Azure. Například můžete potřebovat další předplatné k oddělení vývoje a provozu hranice, nebo můžete mít platformu, která vyžaduje samostatné předplatné pro každého klienta. Možnost agregovaných dat, vytváření sestav napříč všemi předplatnými do jedné platformy je důležité funkce.

K tomuto účelu můžete použít Azure Cost Management API. Potom po agregace dat do jednoho zdroje jako Azure SQL, můžete použít nástroje, jako je Power BI k poskytování agregovaná data. Můžete vytvářet agregované sestavy předplatného a podrobné sestavy. Pro uživatele, kteří potřebují proaktivní vhled do řízení nákladů, můžete například vytvořit konkrétní zobrazení nákladů na základě oddělení, skupiny prostředků atd. Nemusíte jim udělovat úplný přístup k fakturačním datům Azure.

**Víc se uč:**

- [Získejte přehled](/azure/billing/billing-consumption-api-overview) rozhraní Azure Consumption API.
- [Další informace o](/power-bi/desktop-connect-azure-consumption-insights) připojení k Azure Consumption Insights v Power BI Desktopu.
- [Zjistěte, jak](/azure/billing/billing-manage-access) spravovat přístup k fakturačních údajů pro Azure pomocí řízení přístupu na základě role (RBAC).

## <a name="after-migration"></a>Po migraci

Po úspěšné migraci úloh a pár týdnů, shromažďovat data o spotřebě budete mít jasnou představu o nákladech na prostředky.

- Jak je můžete analyzovat data, můžete začít generovat rozpočtu směrný plán pro skupiny prostředků Azure a prostředky.
- Poté jak porozumíte, kde je využita rozpočtu cloudu, můžete analyzovat jak snížit náklady a další.

Osvědčené postupy v této části zahrnují použití služby Azure Cost Management pro vytvoření rozpočtu a analýzu nákladů, monitorování prostředků a implementaci rozpočtů skupin prostředků a optimalizaci monitorování, úložiště a virtuálních počítačů.

## <a name="best-practice-use-azure-cost-management"></a>Osvědčený postup: Použití služby Azure Cost Management

Služba Azure Cost Management od Microsoftu vám pomůže sledovat výdaje:

- Pomáhá vám sledovat a řídit výdaje na Azure a optimalizovat využití prostředků.
- Revize, celý předplatného a všechny její prostředky a poskytuje doporučení.
- Poskytuje úplné rozhraní API, integrace externích nástrojů a finančních systémů pro vytváření sestav.
- Sleduje využití prostředků a spravovat náklady na cloud pomocí jednoho unifikovaného zobrazení.
- Obsahuje provozní a finanční informace, které vám pomůže přijímat podložená rozhodnutí.

Ve službě Cost Management můžete provádět tyto akce:

- **Vytvoření rozpočtu:** Umožňuje vytvořit rozpočet pro finanční zodpovědnost.
  - Můžete začlenit služby, které využíváte, nebo si předplatit jejich odběr na určité období (měsíc, čtvrtletí, rok) a v určitém rozsahu (předplatná/skupiny prostředků). Můžete si například vytvořit rozpočet na předplatné Azure na dobu jednoho měsíce, čtvrtletí nebo rok.
    - Po vytvoření rozpočtu, se zobrazí v analýze nákladů. Zobrazení vašemu rozpočtu na aktuální útratu je jedním z prvních kroků při analýze nákladů a výdajů.
  - E-mailová oznámení lze odesílat, když se dosáhne prahové hodnoty.
  - Za účelem analýzy můžete data správy nákladů exportovat do úložiště Azure.

    ![Rozpočet ve službě Cost Management](./media/migrate-best-practices-costs/budget.png)
    *Rozpočet ve službě Azure Cost Management*

- **Analýza nákladů:** Získejte analýzu nákladů, abyste mohli prozkoumat a analyzovat firemní náklady a zjistit tak, jak náklady vznikají, a identifikovat výdajové trendy.
  - Analýza nákladů je k dispozici uživatelům se smlouvou Enterprise.
  - Data analýzy nákladů můžete zobrazit pro různé rozsahy, včetně oddělení, účtu, předplatného nebo skupiny prostředků.
  - Můžete získat analýzu nákladů, která ukazuje celkové náklady za aktuální měsíc a kumulované denní náklady.

    ![Analýza ve službě Cost Management](./media/migrate-best-practices-costs/analysis.png)
    *Analýza ve službě Azure Cost Management*
- **Získání doporučení:** Získejte doporučení Advisoru, která vám ukážou, jak můžete optimalizovat a zlepšit efektivitu.

**Další informace:**

- [Získejte přehled](/azure/cost-management/overview) služby Azure Cost Management.
- [Zjistěte, jak](/azure/cost-management/cost-mgt-best-practices) optimalizovat vaše cloudové investice ve službě Azure Cost Management.
- [Zjistěte, jak](/azure/cost-management/use-reports) pomocí sestav Azure Cost Management.
- [Získejte kurz](/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) na optimalizaci nákladů od doporučení.
- [Přehled](/rest/api/consumption/budgets) rozhraní API služby Azure Consumption

## <a name="best-practice-monitor-resource-utilization"></a>Osvědčený postup: Monitorování využití prostředků

V Azure platíte za to, co používáte, a to pouze tehdy, když prostředky využíváte. U virtuálních počítačů se poplatky účtují při jejich přidělení. Po jejich uvolnění se poplatky neúčtují. S myslete na to by měl monitorovat virtuální počítače v použití a ověřte nastavení velikosti virtuálního počítače.

- Průběžně vyhodnoťte úloh virtuálních počítačů k určení směrné plány.
- Například pokud vaše úloha je použít silně od pondělí do pátku, 8: 00 do 18: 00, ale téměř použít mimo tyto hodiny, může snížit virtuálních počítačů mimo špičky. To může znamenat, změna velikosti virtuálního počítače nebo použijete virtuálního počítače škálovací sady do virtuálních počítačů automatického škálování směrem nahoru nebo dolů.
- Některé společnosti "připomenout znovu", virtuální počítače tak, že je vložíte v kalendáři, který určuje, kdy by měla být k dispozici, a pokud nejsou potřeba.
- Kromě virtuálních počítačů byste také měli monitorovat další síťové prostředky, například ExpressRoute a brány virtuálních sítí, abyste věděli, kdy nejsou plně využity a kdy jsou přetíženy.
- Využití virtuálních počítačů můžete monitorovat pomocí nástrojů od Microsoftu, jako jsou Azure Cost Management, Azure Monitor a Azure Advisor. K dispozici máte také nástroje třetích stran.

**Víc se uč:**

- Získejte přehled o [Azure Monitor](/azure/azure-monitor/overview) a [Azure Advisoru](/azure/advisor/advisor-overview).
- [Získat](/azure/advisor/advisor-cost-recommendations) nákladů doporučení Advisoru.
- [Další informace o [optimalizaci nákladů na základě doporučení](/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) a [prevenci neočekávaných poplatků](/azure/billing/billing-getting-started)]
- Další informace o [sadě nástrojů Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)

## <a name="best-practice-implement-resource-group-budgets"></a>Osvědčený postup: Implementace rozpočtů skupin prostředků

Skupiny prostředků se často používají k vyjádření hranic nákladů. Společně se tento vzor využití pokračuje v týmu Azure pro vývoj nové a vylepšené způsoby, jak sledovat a analyzovat prostředky na různých úrovních, včetně možnosti vytvořit rozpočet na skupinu prostředků a prostředky.

- Rozpočet skupiny prostředků umožňuje sledovat náklady spojené s skupinu prostředků.
- Můžete aktivovat výstrahy a pracovat širokou škálu playbooky je dosáhli nebo Přesáhli jste rozpočtu.

**Víc se uč:**

- [Zjistěte, jak](/azure/billing/billing-cost-management-budget-scenario) Správa nákladů s rozpočty Azure.
- [Kurz](/azure/cost-management/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json) vytváření a správy rozpočtu Azure

## <a name="best-practice-optimize-azure-monitor-retention"></a>Osvědčený postup: Optimalizace uchovávání pomocí služby Azure Monitor

Po přesunu prostředků do Azure a povolení protokolování diagnostiky se generuje velké množství dat protokolu. Tato data protokolu se obvykle odešle na účet úložiště, který je namapovaný na pracovní prostor Log Analytics.

- Čím delší dobu uchování dat protokolů, čím více dat budete mít.
- Ne všechna data protokolu se rovná a několik zdrojů informací, vygeneruje další data protokolu než jiné.
- Z důvodu dodržování předpisů a nařízení je pravděpodobné, že bude nutné zachovat data protokolu pro několik zdrojů informací, který je delší než jiné.
- Pozor, řádek by měl procházet mezi optimalizovat náklady na úložiště vašich protokolů a ponecháním dat protokolu, které potřebujete.
- Doporučujeme, abyste vaše rozhodnutí vyzkoušet a nastavení protokolování okamžitě po dokončení migrace, takže nejsou útraty peníze uchování protokolů žádný význam.

**Víc se uč:**

- [Další informace](/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) o monitorování využití a odhadovaných nákladů

## <a name="best-practice-optimize-storage"></a>Osvědčený postup: Optimalizace úložiště

Pokud jste se při migraci řídili osvědčenými postupy, pravděpodobně jste získali určité výhody. Existují ale náklady pravděpodobně další úložiště, které můžete dál optimalizovat. V čase soubory a objekty BLOB jsou pak zastaralá. Data se možná nepoužívají už ale zákonných požadavků může znamenat, že je potřeba zachovat určitou dobu. V důsledku toho nemusí musíte uložit na vysoce výkonné úložiště, který jste použili pro původní migrace.

Identifikace a přesunutím zastaralá data do oblastí levnější úložiště můžete mít velký dopad na vaše měsíční úložiště rozpočtu a úspory nákladů. Azure poskytuje mnoho způsobů, jak vám pomohou identifikovat a poté uložit tato data zastaralá.

- Využijte výhod úrovně přístupu pro úložiště pro obecné účely v2, přesun méně důležitá data z horké úrovně do úrovně Cool a archivace.
- Pomocí StorSimple přesunout zastaralých dat podle vlastních zásad.

**Víc se uč:**

- [Další informace](/azure/storage/blobs/storage-blob-storage-tiers) o úrovně přístupu.
- [Přehled](/azure/azure-monitor/overview) řešení StorSimple a [cen řešení StorSimple](https://azure.microsoft.com/pricing/details/storsimple)

## <a name="best-practice-automate-vm-optimization"></a>Osvědčený postup: Automatizace optimalizace virtuálního počítače

Hlavním cílem spouštění virtuálního počítače v cloudu je maximalizace využití procesoru, paměti a disku virtuálním počítačem. Pokud máte neoptimalizované virtuální počítače nebo virtuální počítače, které se často nepoužívají, je rozumné je buď vypnout, nebo vertikálně snížit jejich kapacitu pomocí škálovací sady virtuálních počítačů.

Virtuální počítač můžete optimalizovat pomocí služby Azure Automation, škálovacích sad virtuálních počítačů, automatického vypnutí a skriptovaných řešení nebo řešení od externích dodavatelů.

**Další informace:**

- [Zjistěte, jak](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) použít vertikální automatické škálování.
- [Plán](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) automatické spuštění virtuálního počítače.
- [Zjistěte, jak](/azure/automation/automation-solution-vm-management) spuštěním a zastavením virtuálních počítačů mimo špičku ve službě Azure Automation.
- [Další informace] o [službě Azure Advisor](/azure/advisor/advisor-overview) a [sadě nástrojů Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Osvědčené postupy: Použití služby Logic Apps a runbooků s rozhraní API pro rozpočty

Azure poskytuje rozhraní REST API, které má přístup k fakturačním údajům vašeho tenanta.

- Integrace externích systémů a pracovní postupy, které jsou aktivovány metriky, které vytvoříte z dat rozhraní API můžete použít rozpočty rozhraní API.
- Do nástroje pro vaše preferované datové analýzy, si můžete vyžádat data o využití a prostředků.
- Rozhraní API využití a ceníku prostředků Azure vám pomohou přesně odhadnout a spravovat vaše náklady.
- Rozhraní API se implementují jako poskytovatele prostředků a jsou zahrnuty v rozhraní API pomocí Azure Resource Manageru.
- Rozhraní API rozpočty je možné integrovat s Azure Logic Apps a sady Runbook.

**Víc se uč:**

- [Další informace](/rest/api/consumption/budgets) o rozhraní API rozpočtů.
- [Přehled](/azure/billing/billing-usage-rate-card-overview) využití Azure pomocí rozhraní API pro rozpočty

## <a name="best-practice-implement-serverless-technologies"></a>Osvědčený postup: Implementace bezserverových technologií

Úlohy virtuálního počítače se často migrují „tak, jak jsou“, aby nedocházelo k výpadkům. Často virtuálních počítačů může hostovat úlohy, které jsou k nim dochází přerušovaně, s ohledem na krátkou dobu pro spuštění, nebo můžete také mnoho hodin. Například virtuální počítače, na kterých běží naplánované úlohy, jako je například Windows úloh plánovače nebo skripty prostředí PowerShell. Pokud tyto úlohy nejsou spuštěné, jste však zajistit plynulý provoz virtuálního počítače a náklady na úložiště na disku.

Po migraci a po důkladném přezkoumání těchto typů úloh můžete zvážit jejich migraci na bezserverové technologie, jako jsou úlohy služby Azure Functions nebo Azure Batch. Díky tomuto řešení už nemusíte spravovat a udržovat virtuální počítače, čímž ušetříte další náklady.

**Další informace:**

- Další informace o službě [Azure Functions](https://azure.microsoft.com/services/functions)
- Další informace o službě [Azure Batch](https://azure.microsoft.com/services/batch)

## <a name="next-steps"></a>Další postup

Přečtěte si doporučené postupy:

- [Osvědčené postupy](migrate-best-practices-security-management.md) pro zabezpečení a správu po migraci.
- [Osvědčené postupy](migrate-best-practices-networking.md) sítě po migraci.
