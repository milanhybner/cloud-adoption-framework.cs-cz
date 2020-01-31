---
title: Škálování migrace do Azure
description: Přečtěte si, jak společnost Contoso zvládá škálovanou migraci do Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 8a807bfc20289339221056b9b0798260aaddbfd8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807304"
---
# <a name="scale-a-migration-to-azure"></a>Škálování migrace do Azure

Tento článek ukazuje, jak fiktivní společnost Contoso provádí migraci do Azure ve velkém měřítku. Zvažuje, jak naplánovat a provést migraci více než 3 000 sad funkcí, 8 000 databází a 10 000 virtuálních počítačů.

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s partnery ve firmě, aby zjistil, čeho chtějí touto migrací dosáhnout:

- **Řešení obchodního růstu.** Společnost Contoso roste a to způsobuje tlak na místní systémy a infrastrukturu.
- **Zvýšení efektivity.** Společnost Contoso se potřebuje zbavit zbytečných postupů a zjednodušit procesy pro vývojáře i uživatele. Potřebuje IT k tomu, aby neztrácela čas ani peníze, byla rychlá a dokázala rychleji reagovat na požadavky zákazníků.
- **Zvýšení agility.** IT ve společnosti Contoso musí pohotověji reagovat na potřeby firmy. K zajištění úspěchu v globální ekonomice je nutné, aby IT dokázalo rychleji reagovat na změny na trhu. Nesmí stát v cestě a nesmí se stát obchodní překážkou.
- **Škálování** Společnost Contoso úspěšně roste a její tým IT musí poskytovat systémy, které jsou schopné růst stejným tempem.
- **Vylepšení nákladových modelů.** Společnost Contoso chce snížit kapitálové požadavky v oblasti rozpočtu na IT. Chce využívat možnosti škálování v cloudu a omezit potřebu nákladného hardwaru.
- **Snížení nákladů na licencování.** Společnost Contoso chce minimalizovat náklady na cloud.

## <a name="migration-goals"></a>Cíle migrace

Tým pro přechod společnosti Contoso na cloud přesně specifikoval cíle této migrace. Tyto cíle se použily k určení nejlepší metody migrace.

**Požadavky** | **Podrobnosti**
--- | ---
**Přejít na Azure rychle** | Společnost Contoso chce začít přesouvat aplikace a virtuální počítače do Azure co nejrychleji.
**Zkompilovat úplný inventář** | Společnost Contoso chce mít úplný inventář všech aplikací, databází a virtuálních počítačů v organizaci.
**Posoudit a klasifikovat aplikace** | Společnost Contoso chce plně využít výhod cloudu. Předpokládá, že všechny služby budou standardně běžet v modelu PaaS. Pokud model PaaS nebude vhodný, použije se model IaaS.
**Vyškolit a přejít na DevOps** | Společnost Contoso chce přejít na model DevOps. Poskytne školení o Azure a DevOps a podle potřeby bude reorganizovat týmy.

Po stanovení cílů a požadavků společnost Contoso zkontroluje IT zázemí a určí proces migrace.

## <a name="current-deployment"></a>Aktuální nasazení

Po naplánování a nastavení [infrastruktury Azure](./contoso-migration-infrastructure.md) a vyzkoušení různých kombinací migrace v rámci testování konceptu podle tabulky výše je společnost Contoso připravená pustit se do úplné migrace do Azure ve velkém měřítku. Tady je seznam toho, co chce společnost Contoso migrovat.

<!--markdownlint-disable MD033 -->

**Položka** | **Objem** | **Podrobnosti**
--- | --- | ---
**Úlohy** | Více než 3 000 aplikací | Aplikace běží na virtuálních počítačích.<br/><br/>  Jde o aplikace pro Windows, aplikace založené na SQL a open-source software LAMP.
**Databáze** | Přibližně 8 500 | Patří sem databáze SQL Server, MySQL a PostgreSQL.
**Virtuální počítače** | Více než 35 000 | Virtuální počítače běží na hostitelích VMware a jsou spravované pomocí serverů vCenter.

<!--markdownlint-enable MD033 -->

## <a name="migration-process"></a>Proces migrace

Po podchycení obchodních faktorů a cílů migrace se společnost Contoso rozhodne pro čtyřfázový proces migrace:

- **Fáze 1: vyhodnocení.** Prozkoumají se aktuální prostředky a zjistí se, jestli jsou vhodné pro migraci do Azure.
- **Fáze 2: migrace** Prostředky se přesunou do Azure. Způsob přesunutí aplikací a objektů do Azure bude záviset na jejich povaze a na tom, čeho se má migrací dosáhnout.
- **Fáze 3: optimalizace** Po přesunutí prostředků do Azure je společnost Contoso potřebuje vylepšit a zjednodušit, aby dosáhla maximálního výkonu a efektivity.
- **Fáze 4: zabezpečení a správa.** Teď už má společnost Contoso všechno migrované a využívá prostředky a služby Azure pro zabezpečení a správu, jejichž pomocí řídí, zabezpečuje a monitoruje své cloudové aplikace v Azure.

Tyto fáze neprobíhají v celé organizaci sériově. Každá část projektu migrace společnosti Contoso se může nacházet v jiné fázi procesu posouzení a migrace. Optimalizace, zabezpečení a správa budou probíhat neustále a dlouhodobě.

## <a name="phase-1-assess"></a>Fáze 1: posouzení

Společnost Contoso celý proces zahájí zjištěním a posouzením místních aplikací, dat a infrastruktury. Proto bude společnost Contoso postupovat takto:

- Společnost Contoso potřebuje vyhledat aplikace, zmapovat závislosti mezi nimi a rozhodnout o pořadí a prioritě migrace.
- Během posuzování vytvoří ucelený inventář aplikací a prostředků. Společně s novým inventářem bude společnost Contoso používat a aktualizovat existující databázi správy konfigurace (CMDB) a katalog služeb.
  - Databáze CMDB obsahuje technické konfigurace pro aplikace Contoso.
  - V katalogu služeb jsou zdokumentované provozní podrobnosti o aplikacích, včetně přidružených obchodních partnerů a smluv o úrovni služeb (SLA).

### <a name="discover-apps"></a>Zjištění aplikací

Společnost Contoso provozuje tisíce aplikací na celé řadě serverů. Kromě databáze CMDB a katalogu služeb potřebuje nástroje pro zjišťování a posouzení.

- Tyto nástroje musí poskytovat mechanismus, který dokáže předat data z posouzení do procesu migrace.
- Nástroje pro posouzení musí poskytovat data, která pomůžou vytvořit inteligentní inventář fyzických a virtuálních prostředků společnosti Contoso. Data by měla zahrnovat informace o profilu a metriky výkonu.
- Po dokončení zjišťování by měla společnost Contoso mít úplný inventář svých prostředků a přidružených metadat. Tento inventář se použije k definování plánu migrace.

### <a name="identify-classifications"></a>Identifikace klasifikací

Společnost Contoso identifikuje některé běžné kategorie pro klasifikaci prostředků v inventáři. Tyto klasifikace jsou pro účely migrace zásadní pro rozhodování společnosti Contoso. Seznam klasifikací pomůže nastavit priority migrace a identifikovat komplexní problémy.

**Kategorie** | **Přiřazená hodnota** | **Podrobnosti**
--- | --- | ---
Obchodní skupina | Seznam názvů obchodních skupin | Která skupina zodpovídá za položku inventáře?
Kandidát pro testování konceptu | Ano / Ne | Dá se aplikace použít pro testování konceptu nebo jako kandidát pro ranou fázi migrace do cloudu?
Technický dluh | Žádný / Nějaký / Závažný | Provozuje nebo používá daná položka inventáře nějaký produkt, platformu nebo operační systém s ukončenou podporou?
Důsledky pro bránu firewall | Ano / Ne | Komunikuje aplikace s internetem nebo externím provozem?  Integruje se s bránou firewall?
Problémy se zabezpečením | Ano / Ne | Existují známé problémy se zabezpečením aplikace?  Používá aplikace nešifrovaná data nebo zastaralé platformy?

### <a name="discover-app-dependencies"></a>Zjištění závislostí aplikací

V rámci procesu posouzení musí společnost Contoso identifikovat, kde jsou aplikace spuštěné, a zjistit závislosti a propojení mezi aplikačními servery. Společnost Contoso mapuje své prostředí v několika krocích.

1. Jako první krok zjistí, jak jsou servery a počítače namapované na jednotlivé aplikace, síťová umístění a skupiny.
2. Pomocí těchto informací může společnost Contoso jasně identifikovat aplikace, které mají málo závislostí, a jsou proto vhodné pro rychlou migraci.
3. Pomocí mapování může společnost Contoso identifikovat složitější závislosti a komunikace mezi aplikačními servery. Společnost Contoso pak může tyto servery logicky seskupit jako reprezentanty aplikací a naplánovat strategii migrace na základě těchto skupin.

Po dokončení mapování může společnost Contoso zajistit, aby se při vytváření plánu migrace identifikovaly a vzaly v úvahu všechny komponenty aplikací.

![Mapování závislostí](./media/contoso-migration-scale/dependency-map.png)

### <a name="evaluate-apps"></a>Vyhodnocení aplikací

Jako poslední krok v procesu zjišťování a posouzení může společnost Contoso vyhodnotit výsledky posouzení a mapování a naplánovat, jak migrovat jednotlivé aplikace v katalogu služeb.

K zachycení tohoto procesu vyhodnocení přidá do inventáře několik dalších klasifikací.

**Kategorie** | **Přiřazená hodnota** | **Podrobnosti**
--- | --- | ---
Obchodní skupina | Seznam názvů obchodních skupin | Která skupina zodpovídá za položku inventáře?
Kandidát pro testování konceptu | Ano / Ne | Dá se aplikace použít pro testování konceptu nebo jako kandidát pro ranou fázi migrace do cloudu?
Technický dluh | Žádný / Nějaký / Závažný | Provozuje nebo používá daná položka inventáře nějaký produkt, platformu nebo operační systém s ukončenou podporou?
Důsledky pro bránu firewall | Ano / Ne | Komunikuje aplikace s internetem nebo externím provozem?  Integruje se s bránou firewall?
Problémy se zabezpečením | Ano / Ne | Existují známé problémy se zabezpečením aplikace?  Používá aplikace nešifrovaná data nebo zastaralé platformy?
Strategie migrace | Změna hostitele / Refaktoring / Změna architektury / Nové sestavení | Jaký druh migrace je pro aplikaci potřebný? Jak se aplikace nasadí do Azure? [Další informace](./contoso-migration-overview.md#migration-patterns).
Technická složitost | 1–5 | Jak složitá je migrace? Tato hodnota by měla být definovaná týmem DevOps ve společnosti Contoso a relevantními partnery.
Obchodní důležitost | 1–5 | Jak důležitá je aplikace pro firmu? Aplikaci pro malou pracovní skupinu se například může přiřadit skóre jedna, zatímco kritické aplikaci používané v celé organizaci skóre pět. Toto skóre bude mít vliv na úroveň priority migrace.
Priorita migrace | 1/2/3 | Jaká je priorita migrace aplikace?
Riziko migrace | 1–5 | Jaká je úroveň rizika při migraci aplikace? Na této hodnotě by se měl shodnout tým DevOps ve společnosti Contoso s relevantními partnery.

### <a name="figure-out-costs"></a>Zjištění nákladů

Za účelem zjištění nákladů a potenciálních úspor při migraci do Azure může společnost Contoso využít [kalkulačku celkových nákladů na vlastnictví (TCO)](https://azure.microsoft.com/pricing/tco/calculator). Její pomocí může vypočítat a porovnat celkové náklady na Azure se srovnatelným místním nasazením.

### <a name="identify-assessment-tools"></a>Identifikace nástrojů pro posouzení

Společnost Contoso se rozhoduje, jaké nástroje se mají použít pro zjišťování, posouzení a vytvoření inventáře. Identifikuje kombinaci nástrojů a služeb Azure, nativních aplikačních nástrojů a skriptů a partnerských nástrojů. Společnost Contoso zejména zajímá, jak by šlo k posouzení ve velkém měřítku využít službu Azure Migrate.

#### <a name="azure-migrate"></a>Azure Migrate

Služba Azure Migrate pomáhá zjistit a posoudit místní virtuální počítače VMware při přípravě na migraci do Azure. Služba Azure Migrate nabízí tyto možnosti:

1. Objevování: Objevte místní virtuální počítače VMware.
    - Azure Migrate podporuje zjišťování z více serverů vCenter (sériové) a dokáže spouštět zjišťování v samostatných projektech Azure Migrate.
    - Azure Migrate provádí zjišťování prostřednictvím virtuálního počítače VMware, na kterém běží sběrná aplikace Migrate Collector. Stejná sběrná aplikace může zjišťovat virtuální počítače na různých serverech vCenter a odesílat data do různých projektů.
2. Posouzení připravenosti: Vyhodnoťte, jestli jsou místní počítače vhodné pro provoz v Azure. Posouzení zahrnuje:
    - Doporučení pro velikost: Získejte doporučení pro velikost virtuálních počítačů Azure na základě historie výkonu místních virtuálních počítačů.
    - Odhadované měsíční náklady: získáte odhadované náklady na provoz místních počítačů v Azure.
3. Identifikujte závislosti: Vizualizace závislostí místních počítačů a vytvoření optimálních skupin počítačů pro účely posouzení a migrace.

![Azure Migrate](./media/contoso-migration-scale/azure-migrate.png)

##### <a name="migrate-at-scale"></a>Migrace ve velkém měřítku

Vzhledem k rozsahu této migrace musí společnost Contoso využít službu Azure Migrate správným způsobem.

- Společnost Contoso provede pomocí služby Azure Migrate posouzení jednotlivých aplikací. Tím se zajistí, že Azure Migrate vrátí na Azure Portal aktuální data.
- Správci společnosti Contoso si přečtou informace o [nasazení služby Azure Migrate ve velkém měřítku](https://docs.microsoft.com/azure/migrate/how-to-scale-assessment).
- Společnost Contoso se seznámí s omezeními služby Azure Migrate shrnutými v následující tabulce.

**Akce** | **Omezení**
--- | ---
Vytvoření projektu Azure Migrate | 10 000 virtuálních počítačů
Zjišťování | 10 000 virtuálních počítačů
Posouzení | 10 000 virtuálních počítačů

Společnost Contoso použije Azure Migrate následujícím způsobem:

- V systému vCenter uspořádá virtuální počítače do složek. Díky tomu se bude moct snadněji zaměřit, když bude spouštět posouzení pro virtuální počítače v konkrétní složce.
- Azure Migrate využívá k posouzení závislostí mezi počítači řešení Azure Service Map. To vyžaduje, aby byly na virtuálních počítačích, které se mají posuzovat, nainstalovaní agenti.
  - Společnost Contoso využije automatizované skripty k instalaci požadovaných agentů pro Windows nebo Linux.
  - Pomocí skriptování může společnost Contoso vynutit instalaci do virtuálních počítačů v rámci složky v systému vCenter.

#### <a name="database-tools"></a>Databázové nástroje

Kromě služby Azure Migrate se společnost Contoso zaměří na použití nástrojů určených specificky pro posuzování databází. S posouzením databází SQL Serveru před migrací pomůžou nástroje, jako je [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017).

Data Migration Assistant (DMA) může společnosti Contoso pomoct zjistit, jestli jsou místní databáze kompatibilní s řadou databázových řešení Azure, jako je třeba služba Azure SQL Database, SQL Server spuštěný na virtuálním počítači Azure IaaS a spravovaná instance Azure SQL.

Kromě služby DMS má společnost Contoso několik dalších skriptů, které používá pro zjišťování a zdokumentování databází SQL Serveru. Ty jsou umístěné v úložišti GitHub.

#### <a name="partner-assessment-tools"></a>Partnerské nástroje pro posouzení

S posouzením místního prostředí před migrací do Azure může společnosti Contoso pomoct také několik dalších partnerských nástrojů. [Tady najdete další informace](https://azure.microsoft.com/migration/partners) o partnerech pro migraci do Azure.

## <a name="phase-2-migrate"></a>Fáze 2: migrace

Po dokončení posouzení potřebuje společnost Contoso identifikovat nástroje pro přesun svých aplikací, dat a infrastruktury do Azure.

### <a name="migration-strategies"></a>Strategie migrace

Existují čtyři široké strategie migrace, které může společnost Contoso vzít v úvahu.

<!--markdownlint-disable MD033 -->

**Strategie** | **Podrobnosti** | **Použití**
--- | --- | ---
**Změna hostitele** | Tato možnost se často označuje jako migrace _výtahu a posunutí_ , takže se rychle migruje stávající aplikace do Azure.<br/><br/> Aplikace se migruje tak, jak je, s výhodami cloudu a bez rizik nebo nákladů spojených se změnami kódu. | Společnost Contoso může změnu hostitele použít pro méně strategické aplikace, které nevyžadují žádné změny kódu.
**Refaktoring** | Tato strategie se také označuje jako „opětovné zabalení“ a vyžaduje minimální změny kódu nebo konfigurace aplikací. Ty jsou potřebné pro připojení aplikací k Azure PaaS a lepšímu využití možností cloudu. | Společnost Contoso může refaktorovat strategické aplikace, které si mají zachovat stejné základní funkce, ale mají se přesunout a běžet na platformě Azure, jako je Azure App Service.<br/><br/> Tato strategie vyžaduje minimální změny kódu.<br/><br/> Na druhé straně bude společnost Contoso muset udržovat platformu virtuálních počítačů, protože tu nebude spravovat společnost Microsoft.
**Změna architektury** | Při této strategii se upravuje nebo rozšiřuje základ kódu aplikace a optimalizuje se její architektura pro cloudové možnosti a škálování.<br/><br/> Aplikace se zmodernizuje na odolnou, vysoce škálovatelnou architekturu s možností nezávislého nasazení.<br/><br/> Pomocí služeb Azure je možné tento proces zrychlit, s jistotou škálovat aplikace a snadno je spravovat.
**Opětovné sestavení** | Při této strategii se aplikace znovu sestaví od základu s využitím nativních cloudových technologií.<br/><br/> Platforma Azure jako služba (PaaS) poskytuje kompletní prostředí pro vývoj a nasazení v cloudu. Eliminuje některé náklady a složité aspekty související s licencemi na software a odstraňuje potřebu základní aplikační infrastruktury, middlewaru a dalších prostředků. | Společnost Contoso může kritické aplikace přepsat od základů a využít výhody cloudových technologií, jako jsou bezserverový počítač nebo mikroslužby.<br/><br/> Společnost Contoso bude spravovat aplikace a služby, které vyvíjí, a Azure bude spravovat všechno ostatní.

<!--markdownlint-enable MD033 -->

Je také nutné vzít v úvahu data, zejména vzhledem k objemu databází, které společnost Contoso má. Výchozím přístupem společnosti Contoso je použít služby PaaS, jako je Azure SQL Database, aby bylo možné naplno využít cloudové funkce. Po přesunutí databází do služby PaaS bude společnost Contoso muset udržovat jenom data a o platformu se postará Microsoft.

### <a name="evaluate-migration-tools"></a>Vyhodnocení nástrojů pro migraci

Společnost Contoso pro migraci primárně používá několik služeb a nástrojů Azure:

- [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview): orchestruje zotavení po havárii a migruje místní virtuální počítače do Azure.
- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview): migruje místní databáze jako SQL Server, MySQL a Oracle do Azure.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery je primární služba Azure pro orchestraci zotavení po havárii a migraci v rámci Azure a z místních lokalit do Azure.

1. Služba Site Recovery umožňuje (orchestruje) replikaci z vašich místních lokalit do Azure.
2. Po nastavení a spuštění replikace můžou služby místních počítačů převzít počítače v Azure a migrace se může dokončit.

Společnost Contoso už [dokončila testování konceptu](./contoso-migration-rehost-vm.md), aby zjistila, jak může služba Site Recovery pomoct s migrací do cloudu.

##### <a name="use-site-recovery-at-scale"></a>Použití Site Recovery ve velkém měřítku

Společnost Contoso plánuje provést několik migrací výtahu a posunutí. Aby se zajistilo, že vše bude fungovat, bude služba Site Recovery provádět replikaci po dávkách obsahujících kolem 100 virtuálních počítačů. Aby to šlo dobře připravit, musí společnost Contoso provést plánování kapacity pro navrhovanou migraci pomocí služby Site Recovery.

- Společnost Contoso potřebuje shromáždit informace o svých objemech provozu. Zejména jde o toto:
  - Společnost Contoso potřebuje určit četnost změn virtuálních počítačů, které chce replikovat.
  - Musí také vzít v úvahu síťové připojení z místní lokality do Azure.
- V reakci na požadavky na kapacitu a objem musí společnost Contoso přidělit dostatečnou šířku pásma na základě denní četnosti změn dat požadovaných virtuálních počítačů, aby splnila cíl bodu obnovení (RPO).
- A musí také zjistit, kolik serverů bude potřebných ke spouštění komponent služby Site Recovery nutných pro nasazení.

###### <a name="gather-on-premises-information"></a>Shromažďování informací o místním prostředí

Společnost Contoso může pomocí [Plánovače nasazení služby Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-deployment-planner) provést tyto kroky:

- Může pomocí tohoto nástroje vzdáleně profilovat virtuální počítače, aniž by to mělo dopad na produkční prostředí. To pomáhá stanovit požadavky na šířku pásma a úložiště pro replikaci a převzetí služeb.
- Společnost Contoso může tento nástroj spustit i bez instalace jakýchkoliv komponent služby Site Recovery.
- Nástroj shromažďuje informace o kompatibilních a nekompatibilních virtuálních počítačích, discích jednotlivých virtuálních počítačů a četnosti změn dat na jednotlivých discích. Identifikuje také požadavky na šířku pásma sítě a infrastrukturu Azure potřebnou k úspěšné replikaci a převzetí služeb.
- Společnost Contoso musí plánovač spouštět na počítačích se systémem Windows Server, které splňují minimální požadavky na konfigurační server služby Site Recovery. Konfigurační server je počítač služby Site Recovery, který je potřebný k replikaci místních virtuálních počítačů VMware.

###### <a name="identify-site-recovery-requirements"></a>Identifikace požadavků na službu Site Recovery

Kromě replikovaných virtuálních počítačů vyžaduje služba Site Recovery několik komponent pro migraci počítačů VMware.

<!--markdownlint-disable MD033 -->

**Komponenta** | **Podrobnosti**
--- | ---
**Konfigurační server** | Obvykle jde o virtuální počítač VMware nastavený pomocí šablony OVF.<br/><br/> Komponenta konfiguračního serveru koordinuje komunikaci mezi místním prostředím a Azure a spravuje replikaci dat.
**Procesový server** | Obvykle se instaluje na konfigurační server.<br/><br/> Komponenta procesového serveru přijímá data replikace, optimalizuje je pomocí ukládání do mezipaměti, komprese a šifrování a odesílá je do úložiště Azure.<br/><br/> Procesový server také na virtuální počítače, které chcete replikovat, nainstaluje službu Azure Site Recovery Mobility Service a automaticky vyhledá místní virtuální počítače.<br/><br/> Škálovaná nasazení vyžadují další, samostatné procesové servery pro zpracování velkých objemů provozu replikace.
**Mobility Service** | Agent služby Mobility Service se nainstaluje na každý virtuální počítač VMware, který se bude migrovat pomocí služby Site Recovery.

<!--markdownlint-enable MD033 -->

Společnost Contoso musí zjistit, jak tyto komponenty nasadit, na základě požadavků na kapacitu.

<!--markdownlint-disable MD033 -->

**Komponenta** | **Požadavky na kapacitu**
--- | ---
**Maximální denní četnost změn** | Jeden procesový server může zpracovat denní četnost změn až do 2 TB. Vzhledem k tomu, že virtuální počítač může používat jenom jeden procesový Server, maximální denní četnost změn dat, která je podporovaná pro replikovaný virtuální počítač, je 2 TB.
**Maximální propustnost** | Standardní účet úložiště Azure může zpracovávat maximálně 20 000 požadavků za sekundu a vstupně-výstupní operace za sekundu (IOPS) replikovaného virtuálního počítače by měly být v rámci tohoto limitu. Pokud má například virtuální počítač 5 disků a každý z nich vygeneruje na virtuálním počítači 120 IOPS (o velikosti 8 kB), pak bude v rámci limitu IOPS na disk v Azure (500).<br/><br/> Potřebný počet účtů úložiště můžete zjistit tak, že celkový počet vstupně-výstupních operací zdrojových počítačů za sekundu vydělíte 20 000. Replikovaný počítač může v Azure patřit jenom do jednoho účtu úložiště.
**Konfigurační server** | Na základě předpokladu společnosti Contoso, že bude replikaci provádět po dávkách zahrnujících 100 až 200 virtuálních počítačů, a [požadavků na velikost konfiguračního serveru](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#size-recommendations-for-the-configuration-server-and-inbuilt-process-server) došla společnost Contoso k tomu, že potřebuje takovýto konfigurační server:<br/><br/> CPU: 16 vCPU (2 sokety &#215; 8 jader @ 2,5 GHz)<br/><br/> Paměť: 32 GB<br/><br/> Disk mezipaměti: 1 TB<br/><br/> Frekvence změny dat: 1 TB až 2 TB.<br/><br/> Kromě požadavků na velikost bude muset společnost Contoso zajistit také optimální umístění konfiguračního serveru ve stejné síti a segmentu LAN, jako jsou virtuální počítače, které se budou migrovat.
**Procesový server** | Contoso nasadí samostatný, vyhrazený procesový server, který dokáže replikovat 100 až 200 virtuálních počítačů:<br/><br/> CPU: 16 vCPU (2 sokety &#215; 8 jader @ 2,5 GHz)<br/><br/> Paměť: 32 GB<br/><br/> Disk mezipaměti: 1 TB<br/><br/> Frekvence změny dat: 1 TB až 2 TB.<br/><br/> Procesový server bude hodně vytížený, takže by měl být umístěný na hostiteli ESXi, který dokáže zpracovat vstupně-výstupní diskové operace, síťový provoz a výkon procesoru potřebné pro replikaci. Společnost Contoso bude pro tento účel uvažovat o vyhrazeném hostiteli.
**Sítě** | Společnost Contoso zkontrolovala aktuální infrastrukturu site-to-site VPN a rozhodla se implementovat Azure ExpressRoute. Implementace je kritická, protože se tím snižuje latence a zvyšuje šířka pásma do primární oblasti Azure, kterou je pro společnost Contoso Východní USA 2.<br/><br/> **Monitorování:** Společnost Contoso bude muset pečlivě monitorovat tok dat z procesového serveru. Pokud data způsobí přetížení šířky pásma sítě, společnost Contoso zváží [omezení šířky pásma procesového serveru](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#control-network-bandwidth).
**Úložiště Azure** | Společnost Contoso musí pro migraci identifikovat správný typ a počet cílových účtů úložiště Azure. Služba Site Recovery replikuje data virtuálních počítačů do úložiště Azure.<br/><br/> Služba Site Recovery může replikovat do účtů úložiště Standard nebo Premium (SSD).<br/><br/> Při rozhodování o úložišti musí společnost Contoso zkontrolovat [omezení úložiště](https://docs.microsoft.com/azure/virtual-machines/windows/disks-types) a musí vzít v úvahu očekávaný nárůst a zvýšené využití v průběhu času. V důsledku rychlosti a priority migrací se společnost Contoso rozhodla používat Premium SSD.<br/><br/>
Rozhodla se používat spravované disky pro všechny virtuální počítače nasazené do Azure. Požadovaný počet vstupně-výstupních operací za sekundu rozhodne, jestli se budou používat disky HDD úrovně Standard, SSD úrovně Standard nebo SSD úrovně Premium.<br/><br/>

<!--markdownlint-enable MD033 -->

#### <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service (DMS) je plně spravovaná služba, která umožňuje bezproblémovou migraci z více databázových zdrojů na datové platformy Azure s minimální dobou vyřazení z provozu.

- Služba DMS integruje funkce stávajících nástrojů a služeb. Používá nástroj Data Migration Assistant (DMA) k vygenerování hodnotících sestav, které přinášejí doporučení týkající se kompatibility databází a případných požadovaných úprav.
- DMS používá jednoduchý, samoobslužný proces migrace s inteligentním posouzením, které pomáhá vyřešit potenciální problémy před migrací.
- DMS dokáže provést škálovanou migraci do cílové databáze Azure z více zdrojů.
- DMS podporuje SQL Server od verze 2005 do verze 2017.

DMS ale není jediným nástrojem pro migraci databází od Microsoftu. Pokud chcete, podívejte se na [porovnání nástrojů a služeb](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services).

##### <a name="use-dms-at-scale"></a>Škálování pomocí DMS

Společnost Contoso bude službu DMS používat při migraci z SQL Serveru.

- Při zřizování služby DMS musí společnost Contoso správně určit její velikost a nastavit ji tak, aby měla při migraci dat optimální výkon. Společnost Contoso vybere úroveň Pro důležité obchodní informace se 4 virtuálními jádry, aby mohla služba využít více virtuálních procesorů pro paralelní a rychlejší přenos dat.

    ![Škálování služby DMS](./media/contoso-migration-scale/dms.png)

- Další škálovací taktikou společnosti Contoso je dočasné navýšení kapacity cílové instance databáze Azure SQL nebo MySQL na SKU úrovně Premium během migrace dat. Tím se minimalizuje omezování databáze, které by mohlo ovlivnit aktivity přenosu dat při použití SKU nižší úrovně.

##### <a name="use-other-tools"></a>Použití dalších nástrojů

Kromě DMS může společnost Contoso k identifikaci informací o virtuálních počítačích použít také další nástroje a služby.

- Mají skripty, které jim pomůžou s ručními migracemi. Ty jsou k dispozici v úložišti GitHub.
- K migraci se můžou použít také různé [partnerské nástroje](https://azure.microsoft.com/migration/partners).

## <a name="phase-3-optimize"></a>Fáze 3: optimalizace

Jakmile společnost Contoso přesune prostředky do Azure, potřebuje je optimalizovat v zájmu zvýšení výkonu a maximalizovat návratnost investic pomocí nástrojů pro správu nákladů. Vzhledem k tomu, že Azure je služba, která se platí podle využití, je pro společnost Contoso důležité, aby rozuměla tomu, jaký mají systémy výkon, a zajistila, aby měly správnou velikost.

### <a name="azure-cost-management"></a>Azure Cost Management

V zájmu co nejlepšího zužitkování investice do cloudu bude společnost Contoso využívat bezplatnou službu pro správu nákladů Azure Cost Management.

- Toto licencované řešení vytvořila společnost Cloudyn, která je nyní pobočkou Microsoftu. Společnosti Contoso umožní transparentně a přesně spravovat útraty v cloudu. Poskytuje nástroje pro monitorování, přidělování a snižování nákladů na cloud.
- Služba Azure Cost Management poskytuje jednoduché sestavy na řídicím panelu, které pomáhají s přidělováním, rozdělováním, analýzou a interním zúčtováním nákladů.
- Služba Cost Management pomáhá optimalizovat výdaje za cloud díky identifikaci málo využitých prostředků, které pak společnost Contoso může spravovat a upravovat.
- Přečtěte si [další informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management.

![Správa nákladů](./media/contoso-migration-scale/cost-management.png)

### <a name="native-tools"></a>Nativní nástroje

Společnost Contoso bude také používat skripty k vyhledání nepoužívaných prostředků.

- Během velkých migrací se často vyskytnou „zůstatková“ data, například virtuální pevné disky, za které se platí poplatky, ale neposkytují společnosti žádnou hodnotu. Skripty jsou k dispozici v úložišti GitHub.
- Společnost Contoso bude využívat práci, kterou provede IT oddělení Microsoftu, a zvažte implementaci sady nástrojů pro optimalizaci prostředků Azure (ARO).
- Společnost Contoso může do svého předplatného nasadit účet služby Azure Automation s předem konfigurovanými runbooky a plány, které pomůžou šetřit peníze. Po povolení nebo vytvoření plánu probíhá optimalizace prostředků Azure v předplatném automaticky, a to včetně optimalizace nových prostředků.
- To poskytuje decentralizované možnosti automatizace, které snižují náklady. K funkcím patří:
  - Automatické zastavení virtuálních počítačů Azure na základě nízkého výkonu procesoru
  - Plánování zastavení a spuštění virtuálních počítačů Azure
  - Plánování zastavení nebo spuštění virtuálních počítačů Azure ve vzestupném a sestupném pořadí pomocí značek Azure
  - Hromadné odstranění skupin prostředků na vyžádání
- Se sadou nástrojů ARO můžete začít pracovat v tomto [úložišti GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

### <a name="partner-optimization-tools"></a>Partnerské nástroje pro optimalizaci

Je také možné použít partnerské nástroje, například [Hanu](https://hanu.com/insight) a [Scalr]( https://www.scalr.com/cost-optimization).

## <a name="phase-4-secure-and-manage"></a>Fáze 4: zabezpečení a Správa

V této fázi bude společnost Contoso využívat prostředky zabezpečení a správy v Azure k řízení, zabezpečení a monitorování cloudových aplikací v Azure. Tyto prostředky pomáhají provozovat zabezpečené a dobře spravované prostředí s použitím produktů dostupných na webu Azure Portal. Společnost Contoso začne tyto služby používat během migrace a díky podpoře hybridního prostředí v Azure může řadu z nich používat i po migraci a získat konzistentní prostředí v celém hybridním cloudu.

### <a name="security"></a>Zabezpečení

Společnost Contoso bude využívat službu Azure Security Center, která zajišťuje jednotnou správu zabezpečení a pokročilou ochranu před hrozbami napříč sadami funkcí hybridního cloudu.

- Služba Security Center poskytuje úplný přehled a kontrolu nad zabezpečením cloudových aplikací v Azure.
- Společnost Contoso může rychle detekovat hrozby, reagovat na ně a snížit svou zranitelnost vůči hrozbám povolením adaptivní ochrany před hrozbami.

Přečtěte si [další informace](https://azure.microsoft.com/services/security-center) o službě Security Center.

### <a name="monitoring"></a>Sledování

Společnost Contoso potřebuje mít přehled o stavu a výkonu nově migrovaných aplikací, infrastruktury a dat, které teď má v Azure. Bude používat integrované nástroje pro monitorování cloudu Azure, jako jsou služba Azure Monitor, pracovní prostor služby Log Analytics a služba Application Insights.

- Pomocí těchto nástrojů může snadno shromáždit data z různých zdrojů a získat podrobné přehledy. Může například měřit využití procesoru, disků a paměti u virtuálních počítačů, zobrazit aplikace a síťové závislosti napříč několika virtuálními počítači nebo sledovat výkon aplikací.
- Pomocí těchto nástrojů pro monitorování cloudu může společnost Contoso podniknout potřebné kroky a provést integraci s řešeními pro služby.
- Přečtěte si [další informace](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) o monitorování Azure.

### <a name="business-continuity-and-disaster-recovery"></a>Provozní kontinuita a zotavení po havárii

Společnost Contoso bude pro svoje prostředky v Azure potřebovat strategii pro provozní kontinuitu a zotavení po havárii (BCDR).

- Azure poskytuje [integrované funkce BCDR](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications), které zajistí, aby data byla v bezpečí a aplikace nebo služby v provozu.
- Kromě využití integrovaných funkcí chce společnost Contoso zajistit, aby se mohla zotavit v případě selhání, vyhnout se nákladným výpadkům v podniku, splnit cíle v oblasti dodržování předpisů a chránit data před ransomwarem a lidskými chybami. Použijte následující postup:
  - Společnost Contoso nasadí službu Azure Backup jako nákladově efektivní řešení pro zálohování prostředků v Azure. Vzhledem k tomu, že je integrovaná, může contoso nastavit zálohování cloudu v několika jednoduchých krocích.
  - Společnost Contoso nastaví zotavení po havárii pro virtuální počítače Azure pomocí služby Azure Site Recovery. Ta bude zajišťovat replikaci, převzetí služeb při selhání a navrácení služeb po obnovení mezi zadanými oblastmi Azure. Tím se zajistí, aby aplikace běžící na virtuálních počítačích Azure zůstaly dostupné v sekundární oblasti společnosti Contoso, pokud dojde k výpadku v primární oblasti. [Další informace](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

## <a name="conclusion"></a>Závěr

V tomto článku jsme sledovali, jak společnost Contoso plánovala migraci do Azure ve velkém měřítku. Proces migrace rozdělili do čtyř fází. Začalo se posouzením a migrací a pokračovalo optimalizací, zabezpečením a správou po dokončení migrace. Většinou je důležité naplánovat projekt migrace jako celý proces, ale migrovat systémy v rámci organizace tak, že se rozdělí podle klasifikací a do dávek v počtech, které pro firmu mají smysl. Po posouzení dat a použití klasifikací jde projekt rozdělit do řady menších migrací, které mohou běžet bezpečně a rychle. Souhrn těchto menších migrací se rychle promění ve velkou a úspěšnou migraci do Azure.
