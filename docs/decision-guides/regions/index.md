---
title: Průvodce rozhodováním ohledně oblastí
description: Přečtěte si víc o oblastech cloudových platforem a faktorech a charakteristikách, které mohou ovlivnit výběry oblastí Azure.
author: doodlemania2
ms.author: dermar
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: d8545d000d817aa8d6bcaa40a67a157ca5e57669
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708491"
---
# <a name="azure-regions"></a>Oblast Azure

Azure se skládá z mnoha oblastí po celém světě. Každá z [oblastí Azure](https://azure.microsoft.com/global-infrastructure/regions) má specifickou sadu charakteristik, kvůli kterým je výběr oblasti, která se má použít, mimořádně důležitý.

1. **Dostupné služby:** Služby, které se nasazují do jednotlivých oblastí, se liší v závislosti na nejrůznějších faktorech. Pro nasazení vaší úlohy musíte vybrat oblast, která obsahuje požadovanou službu. V článku [Dostupné produkty v jednotlivých oblastech](https://azure.microsoft.com/global-infrastructure/services) najdete další informace o tom, které služby jsou v jednotlivých oblastech k dispozici.
1. **Kapacita:** Každá oblast má maximální kapacitu. Přestože tyto informace se obvykle ke koncovému uživateli nedostanou, mohou mít vliv na to, jaké typy předplatných a služeb může nasadit a za jakých okolností. Je to něco jiného než kvóty předplatného. Pokud plánujete rozsáhlou migraci datacenter do Azure, budete pravděpodobně chtít konzultovat s místním provozním týmem Azure nebo account manažerem a ujistit se, že je možné nasazovat v potřebném měřítku.
1. **Omezení:** Pro nasazení služeb v některých oblastech platí určitá omezení. Některé oblasti jsou například dostupné jenom jako cíl zálohování nebo převzetí služeb při selhání. Mezi další důležitá omezení, která je potřeba zmínit, patří [požadavky na suverenitu dat](https://azure.microsoft.com/global-infrastructure/geographies).
1. **Suverenita:** Pro konkrétní suverénní entity jsou vyhrazené konkrétní oblasti. Přestože se stále jedná o oblasti Azure, jsou tyto suverénní oblasti zcela izolované od zbytku Azure, nemusí je spravovat Microsoft a mohou být omezené jenom na konkrétní typy zákazníků. Jde o tyto suverénní oblasti:
    1. [Azure (Čína)](https://azure.microsoft.com/global-infrastructure/china)
    1. [Azure (Německo)](https://azure.microsoft.com/global-infrastructure/germany) (vyřazuje se z provozu ve prospěch standardních oblastí Azure v Německu, které nejsou suverénní)
    1. [Azure US Government](https://azure.microsoft.com/global-infrastructure/government)
    1. Poznámka: V [Austrálii](https://azure.microsoft.com/global-infrastructure/australia) jsou dvě oblasti, které spravuje Microsoft, ale poskytují se pro australskou vládu a její zákazníky a dodavatele, a proto mají obdobná klientská omezení klientů jako ostatní suverénní cloudy.

## <a name="operate-in-multiple-geographic-regions"></a>Provoz v několika geografických oblastech

Když firmy působí ve více geografických oblastech, je to sice zásadní pro zajištění odolnosti, ale přináší to další úroveň složitosti. Tyto složitosti se manifestují ve čtyřech základních podobách:

- Distribuce prostředků
- Profily přístupu uživatelů
- Požadavky na dodržování předpisů
- Regionální odolnost

Když výše uvedenou problematiku probereme blíž, začnete rozumět tomu, jak je výběr oblasti pro vaši celkovou strategii přechodu na cloud důležitý. Začněme síťovými aspekty.

## <a name="networking-considerations"></a>Aspekty sítí

Každé robustní cloudové nasazení vyžaduje dobře rozváženou síť, která bere v úvahu oblasti Azure. Po zvážení výše uvedených charakteristik pro určení, do kterých oblastí nasazovat, je potřeba nasadit síť. I když vyčerpávající diskuze na téma sítí přesahuje rozsah tohoto článku, je nutné vzít v úvahu některé okolnosti:

- Oblasti Azure se nasazují v párech. V případě závažného selhání oblasti je druhá oblast v rámci stejné geopolitické hranice* označená jako spárovaná oblast. Nasazení do spárovaných oblastí jako primární a sekundární strategie odolnosti je potřeba promyslet. \* Významnou výjimkou je Azure Brazílie, jejíž spárovanou oblastí je USA (střed) – jih. Další informace najdete v tématu [Spárované oblasti Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

  - Azure Storage podporuje [geograficky redundantní úložiště (GRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs). To znamená, že se tři kopie vašich dat ukládají v rámci primární oblasti a tři další kopie se ukládají do spárované oblasti. Párování úložiště pro GRS nejde změnit.
  - Tuto možnost spárované oblasti mohou využít služby, které se spoléhají na GRS služby Azure Storage. Je k tomu potřeba, aby vaše aplikace i síť tuto možnost podporovaly.
  - Pokud neplánujete využívat GRS k zajištění potřeb vaší místní odolnosti, doporučuje se, abyste _NEVYUŽÍVALI_ spárovanou oblast jako sekundární. V případě regionálního selhání bude při migraci na prostředky v spárované oblasti vyvíjen velký tlak. Pokud se dokážete tomuto tlaku vyhnout, můžete si zajistit vyšší rychlost během obnovování, a to obnovením do alternativní lokality.
  > [!WARNING]
  > Nepokoušejte se využít Azure GRS pro zálohování nebo obnovení virtuálních počítačů. Místo toho pro zajištění odolnosti vašich úloh IaaS využijte [Azure Backup](https://azure.microsoft.com/services/backup) a [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery) společně se [spravovanými disky Azure](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).

- Azure Backup a Azure Site Recovery spolu s návrhem vaší sítě zajišťují regionální odolnost pro potřeby zálohování dat a IaaS. Ujistěte se, že síť je optimalizovaná, aby přenosy dat zůstávaly na páteřní síti Microsoftu, a pokud je to možné, využijte [VNet Peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview). Některé větší organizace s globálními nasazeními mohou místo toho ke směrování provozu mezi oblastmi používat [ExpressRoute Premium](https://docs.microsoft.com/azure/expressroute/expressroute-introduction), což může vést k úspoře poplatků za místní výchozí přenos dat.

- Skupiny prostředků Azure jsou konstrukce specifické pro jednotlivé oblasti. Je ale obvyklé, že prostředky v rámci skupiny prostředků zasahují do více oblastí. V takovém případě je důležité vzít v úvahu, že v případě regionálního selhání v ovlivněné oblasti selžou operace řídicí roviny pro skupinu prostředků i v případě, že prostředky v jiných oblastech (v rámci této skupiny prostředků) budou i nadále fungovat. Může to mít vliv na návrh vaší sítě i skupin prostředků.

- Celá řada služeb PaaS v rámci Azure podporuje [koncové body webové služby](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) nebo [privátní propojení](https://docs.microsoft.com/azure/private-link/private-link-overview). Obě tato řešení podstatným způsobem ovlivňují síťové aspekty při úvahách o regionální odolnosti, migraci a zásadách správného řízení.

- Řada služeb PaaS se spoléhá na vlastní řešení regionální odolnosti. Například Azure SQL Database stejně jako CosmosDB umožňuje snadno replikovat do _x_ dalších oblastí. Některé služby nejsou závislé na oblastech, například Azure DNS. Když zvažujete, které služby budete během procesu přechodu využívat, je potřeba, abyste dobře rozuměli možnostem převzetí služeb při selhání a postupu obnovení, který může být pro jednotlivé služby Azure potřeba.

- Kromě podpory zotavení po havárii nasazením do více oblastí řada organizací volí nasazování v modelu aktivní-aktivní, takže žádné převzetí služeb při selhání není nutné. To přináší i další výhodu – zajištění globálního vyrovnávání zatížení a vyšší odolnost proti chybám a náhlému zvýšení výkonu sítě. Aby bylo možné tento model využít, musí vaše aplikace podporovat konfiguraci aktivní-aktivní v několika oblastech.

> [!WARNING]
> Oblasti Azure jsou vysoce dostupné konstrukce se smlouvami SLA pro služby, které v nich běží. V případě klíčových aplikací byste se ale měli vyhýbat závislosti na jedné oblasti. Vždy si naplánujte regionální selhání a vyzkoušejte si kroky pro zmírnění a obnovení.

Po zvážení síťové topologie, která bude nutná k zajištění provozu, budou potřeba další úpravy procesů a dokumentace. Pomocí následujícího přístupu můžete posoudit potenciální výzvy a vytvořit obecný plán postupu:

- Zvažte robustnější připravenost a implementaci zásad správného řízení.
- Sepište si ovlivněné geografické oblasti. Vytvořte si seznam ovlivněných oblastí a zemí.
- Zdokumentujte si požadavky na suverenitu dat. Mají identifikované země požadavky na dodržování předpisů, které řídí suverenitu dat?
- Zdokumentujte si uživatelskou základnu. Budou zaměstnanci, partneři nebo zákazníci v identifikované zemi ovlivněni migrací do cloudu?
- Zdokumentujte si datacentra a prostředky. Existují v identifikované zemi nějaké prostředky, které by mohly být zahrnuty do migrace?
- Zdokumentujte regionální dostupnost jednotek SKU a požadavky převzetí služeb při selhání.

Přizpůsobte změny v rámci procesu migrace tak, aby řešily tento úvodní soupis.

## <a name="document-complexity"></a>Složitost dokumentace

Následující tabulka vám může pomoct při dokumentování zjištěných informací z výše uvedených kroků:

| Oblast        | Země     | Místní zaměstnanci | Místní externí uživatelé   | Místní datacentra nebo prostředky | Požadavky na suverenitu dat |
|---------------|-------------|-----------------|------------------------|-----------------------------|-------------------------------|
| Severní Amerika | USA         | Ano             | Partneři a zákazníci | Ano                         | Ne                            |
| Severní Amerika | Kanada      | Ne              | Zákazníci              | Ano                         | Ano                           |
| Evropa        | Německo     | Ano             | Partneři a zákazníci | Ne – pouze síť           | Ano                           |
| Asie a Tichomoří  | Jižní Korea | Ano             | Partneři               | Ano                         | Ne                            |

<!-- markdownlint-disable MD026 -->

## <a name="data-sovereignty-relevancy"></a>Relevance suverenity dat

Organizace státní správy na celém světě začaly zavádět požadavky na suverenitu dat, jako je například Obecné nařízení o ochraně osobních údajů (GDPR). Požadavky na dodržování předpisů tohoto typu často vyžadují lokalizaci v konkrétní oblasti nebo dokonce v konkrétní zemi kvůli ochraně občanů. V některých případech musí být data týkající se zákazníků, zaměstnanců nebo partnerů uložená v cloudové platformě ve stejné oblasti, ve které se nachází koncový uživatel.

Řešení těchto výzev významně motivuje globálně působící společnosti k migracím do cloudu. Kvůli udržování požadavků na dodržování předpisů se některé společnosti rozhodly nasazovat duplicitní IT prostředky u poskytovatelů cloudu v rámci dané oblasti. Dobrým příkladem tohoto scénáře ve výše uvedené tabulce je Německo. Tento příklad zahrnuje zákazníky, partnery a zaměstnance v Německu, ale žádné existující IT prostředky. Tato společnost se může rozhodnout nasadit některé prostředky do datacentra v rámci oblasti, na kterou se vztahuje GDPR, a potenciálně může dokonce využívat německá datacentra Azure. Pochopení toho, na která data má dopad GDPR, by pomohlo týmu přechodu na cloud určit, jaký je v tomto případě nejlepší přístup při migraci.

### <a name="why-is-the-location-of-end-users-relevant"></a>Proč hraje roli místo, kde se nachází koncoví uživatelé?

Společnosti, které podporují koncové uživatele ve více zemích, vyvinuly technická řešení pro přenosy dat u koncových uživatelů. V některých případech to zahrnuje lokalizaci prostředků. V jiných scénářích se společnost může místo toho rozhodnout implementovat globální řešení prostřednictvím sítí WAN a vyřešit tak potřeby nesourodých uživatelských základen prostřednictvím síťových řešení. V obou případech může být strategie migrace ovlivněná tím, jaké profily používání tito různí koncoví uživatelé mají.

Vzhledem k tomu, že společnost podporuje zaměstnance, partnery a zákazníky v Německu, ale v této zemi nejsou v současnosti žádná datacentra, je pravděpodobné, že tato společnost implementovala nějakou formu řešení s pronajatou linkou pro směrování příslušného provozu do datacenter v jiných zemích. Toto existující směrování představuje významné riziko pro vnímaný výkon migrovaných aplikací. Vkládání dalších směrování v rámci zavedené a optimalizované globální sítě WAN může po migraci vytvořit dojem nedostatečného výkonu aplikací. Hledání a oprava těchto problémů může způsobit významné zpoždění projektu. Každý z níže popsaných procesů zahrnuje pokyny k řešení této složitosti v rámci procesů stanovení předpokladů, posouzení, migrace a optimalizace. Pochopení profilů uživatelů v každé zemi je důležité pro odpovídající správu této složitosti.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Proč hraje roli místo, kde se nachází datacentra?

Umístění existujících datacenter může mít vliv na strategii migrace. Níže jsou uvedené některé z nejběžnějších dopadů:

**Rozhodnutí týkající se architektury:** Cílová oblast je jedním z prvních kroků návrhu strategie migrace. To je často ovlivněno umístěním existujících prostředků. Dostupnost cloudových služeb a jednotková cena těchto služeb se navíc může v jednotlivých oblastech lišit. Pochopení současného a budoucího umístění prostředků má proto vliv na rozhodnutí týkající se architektury a může také ovlivnit odhady rozpočtu.

**Závislosti datacenter:** Na základě dat ve výše uvedené tabulce je pravděpodobné, že mezi různými datacentry po celém světě existují závislosti. V mnoha organizacích, které působí s tímto typem rozsahu, nemusí být tyto závislosti zdokumentovány nebo jim lidé nemusí dobře rozumět. Přístupy používané k vyhodnocení profilů uživatelů vám pomůžou některé z těchto závislostí identifikovat. Během procesu posuzování jsou navrhovány další kroky s cílem omezit rizika spojená s touto složitostí.

## <a name="implementing-the-general-approach"></a>Implementace obecného přístupu

Tento přístup je založený na kvantifikovatelných informacích. Z tohoto důvodu bude následující přístup využívat model založený na datech za účelem řešení složitostí globální migrace.

Pokud rozsah migrace zahrnuje více oblastí, měl by tým přechodu na cloud vyhodnotit následující aspekty připravenosti:

- Suverenita dat může vyžadovat lokalizaci některých prostředků, může však existovat mnoho prostředků, které se nemusí řídit těmito omezeními souvisejícími s dodržováním předpisů. Aktivity, jako je protokolování, generování sestav, směrování sítě, identita a další centrální IT služby, můžou mít oprávnění být hostované jako sdílené služby v rámci více předplatných nebo dokonce i více oblastí. Tým pro přechod do cloudu by měl pro tyto služby vyhodnotit použití modelu sdílených služeb, jak je uvedeno v [referenční architektuře hvězdicové topologie se sdílenými službami](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services).
- Při nasazování více instancí podobných prostředí by mohl objekt pro vytváření prostředí zajistit konzistenci, zlepšit zásady správného řízení a urychlit nasazení. [Průvodce zásadami správného řízení pro komplexní firmy](../../govern/guides/complex/index.md) zavádí přístup pro vytvoření prostředí, které se škáluje v rámci více oblastí.

Jakmile tým stanoví vyhovující základní přístup a je k dispozici odpovídající připravenost, je třeba zvážit několik předpokladů řízených daty:

- **Obecné zjišťování:** Vytvořte si tabulku pro [zdokumentování složitosti](#document-complexity), jak je uvedeno výše.
- **Proveďte analýzu profilů uživatelů v každé ovlivněné zemi:** Je důležité, abyste v počáteční fázi procesu migrace porozuměli obecnému směrování u koncových uživatelů. Změna globálních pronajatých linek a přidávání připojení, jako je ExpressRoute, do cloudového datového centra může vyžadovat zpoždění v řádu měsíců. Tuto možnost proto vyřešte v rámci procesu co nejdříve.
- **Počáteční racionalizace digitálních aktiv:** Vždy, když je do strategie migrace zavedena složitost, měla by být provedena počáteční racionalizace digitálních aktiv. Pomoc najdete v pokynech týkajících se [racionalizace digitálních aktiv](../../digital-estate/index.md).
  - **Další požadavky na digitální aktiva:** Stanovte zásady označování pro identifikaci všech úloh, které jsou ovlivněny požadavky na suverenitu dat. Požadované značky by měly začínat ve fázi racionalizace digitálních aktiv a pokračovat až do migrovaných prostředků.
- **Vyhodnocení modelu hvězdicové architektury:** Distribuované systémy často sdílí společné závislosti. Tyto závislosti lze často řešit prostřednictvím implementace modelu hvězdicové architektury. I když není takový model součástí rozsahu procesu migrace, měl by být posouzen během budoucích iterací [připravených procesů](../../ready/index.md).
- **Stanovení priorit u nevyřízených položek migrace:** Pokud je nutné dělat změny v síti kvůli podpoře nasazení úlohy podporující více oblastí do produkčního prostředí, je důležité, aby tým cloudové strategie mohl sledovat a spravovat eskalace týkající se těchto změn v síti. Tyto změny pomůže urychlit podpora na vyšší úrovni managementu. Důležitější však je, že to dává týmu pro strategii možnost měnit priority nevyřízených položek a zajistit tak, aby kvůli změnám sítě nebyly blokovány globální úlohy. Jen takové úlohy by měly mít prioritu poté, co se změny sítě dokončí.

Tyto předpoklady vám pomůžou nastavit procesy, které můžou řešit tuto složitost během realizace strategie migrace.

## <a name="assess-process-changes"></a>Posouzení změn procesu

Při řešení složitostí globálních prostředků a uživatelských základen by do posouzení jakéhokoli kandidáta na migraci mělo být přidáno několik klíčových aktivit. Každá z těchto změn pomůže vyjasnit dopad na globální uživatele a prostředky prostřednictvím přístupu řízeného daty.

### <a name="suggested-action-during-the-assess-process"></a>Navrhované akce během procesu posouzení

**Vyhodnocení závislostí mezi datacentry:** [Nástroje pro vizualizaci závislostí v Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) vám můžou pomoct identifikovat závislosti. Osvědčeným postupem je použití těchto nástrojů před migrací. Při řešení globální složitosti je to nezbytný krok procesu posouzení. Prostřednictvím [seskupování závislostí](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) může vizualizace pomoct identifikovat IP adresy a porty všech prostředků vyžadovaných pro podporu dané úlohy.

> [!IMPORTANT]
> Dvě důležité poznámky: Zaprvé, odborník, který rozumí umísťování prostředků a schématům IP adres, musí identifikovat prostředky, které se nachází v sekundárním datovém centru. Zadruhé je důležité vyhodnotit podřízené závislosti a klienty ve vizuálu a pochopit obousměrné závislosti.

**Identifikace globálního dopadu na uživatele:** Výstupy z analýzy profilů uživatelů pro stanovení předpokladů by měly identifikovat všechny úlohy ovlivněné globálními profily uživatelů. Když je kandidát pro migraci v seznamu ovlivněných úloh, měl by se architekt připravující migraci poradit s odborníky na sítě a provoz, aby ověřil, jaká jsou očekávání týkající se směrování v síti a výkonu. Architektura by měla přinejmenším zahrnovat připojení ExpressRoute mezi nejbližším střediskem NOC (Network Operations Center) a Azure. [Referenční architektura připojení ExpressRoute](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute) může pomoct s konfigurací nezbytného připojení.

**Návrh zohledňující dodržování předpisů:** Výstupy z analýzy profilů uživatelů pro stanovení předpokladů by měly identifikovat všechny úlohy ovlivněné požadavky na suverenitu dat. V rámci aktivit v procesu posouzení týkajících se architektury by se měl přiřazený architekt poradit s odborníky na dodržování předpisů, aby porozuměl všem požadavkům na migraci a nasazení ve více oblastech. Tyto požadavky významně ovlivní strategie návrhu. Při návrhu vám můžou pomoct referenční architektury [webových aplikací pro více oblastí](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) a [n-vrstvých aplikací pro více oblastí](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server).

> [!WARNING]
> Když budete používat jednu z výše uvedených referenčních architektur, může být nutné vyloučit konkrétní datové prvky z replikačních procesů kvůli zajištění požadavků na suverenitu dat. Tím se do procesu převedení přidá další krok.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Při migraci aplikace, která musí být nasazená ve více oblastech, musí tým přechodu na cloud vzít v úvahu několik důležitých aspektů. Ty zahrnují návrh trezoru Azure Site Recovery, návrh konfiguračního a procesového serveru, návrhy šířky pásma sítě a synchronizaci dat.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhované akce během procesu migrace

**Návrh trezoru Azure Site Recovery:** Azure Site Recovery je navrhovaný nástroj pro nativní cloudovou replikaci a synchronizaci digitálních prostředků do Azure. Site Recovery replikuje data o daném prostředku do trezoru Site Recovery, který je vázán na konkrétní předplatné v konkrétní oblasti a datacentru Azure. Při replikaci prostředků do druhé oblasti může být vyžadován druhý trezor Site Recovery.

**Návrh konfiguračního a procesového serveru:** Site Recovery používá místní instanci konfiguračního a procesového serveru, který je vázaný na jeden trezor Site Recovery. To znamená, že kvůli zajištění replikace může být nutné nainstalovat druhou instanci těchto serverů ve zdrojovém datacentru.

**Návrh šířky pásma sítě:** Během replikace a průběžné synchronizace se binární data přesunují po síti ze zdrojového datacentra do trezoru Site Recovery v cílovém datacentru Azure. Tento proces spotřebovává šířku pásma. Duplikování úlohy do druhé oblasti zdvojnásobí spotřebovávanou šířku pásma. Když je šířka pásma omezená nebo pokud úloha zahrnuje velký objem odchylek konfigurací nebo dat, může to kolidovat s dobou, která je vyžadovaná k dokončení migrace. Ještě důležitější je, že by to mohlo ovlivnit práci uživatelů nebo aplikací, které stále závisí na šířce pásma zdrojového datacentra.

**Synchronizace dat:** Největší využití šířky pásma je často způsobené synchronizací datové platformy. Jak je definováno v referenčních architekturách [webových aplikací pro více oblastí](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) a [n-vrstvých aplikací pro více oblastí](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server), synchronizace dat je často vyžadovaná kvůli udržování aplikací na stejné úrovni. Pokud je toto požadovaný provozní stav dané aplikace, může být před migrací aplikace a prostředků střední vrstvy vhodné dokončit synchronizaci mezi zdrojovou datovou platformou a všemi cloudovými platformami.
**Synchronizace dat:** Největší využití šířky pásma je často způsobené synchronizací datové platformy. Jak je definováno v referenčních architekturách [webových aplikací pro více oblastí](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) a [n-vrstvých aplikací pro více oblastí](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server), synchronizace dat je často vyžadovaná kvůli udržování aplikací na stejné úrovni. Pokud je toto požadovaný provozní stav dané aplikace, může být před migrací aplikace a prostředků střední vrstvy vhodné dokončit synchronizaci mezi zdrojovou datovou platformou a všemi cloudovými platformami.

**Zotavení po havárii Azure do Azure:** Alternativní možnost může složitost dál snížit. Pokud časové plány a přístupy synchronizace dat vyžadují nasazení ve dvou krocích, může být [zotavení po havárii Azure do Azure](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-architecture) přijatelné řešení. V tomto scénáři je úloha nejprve migrována do prvního datacentra Azure pomocí jediného trezoru Site Recovery a návrhu konfiguračního nebo procesového serveru. Po otestování může být úloha obnovena z migrovaných prostředků do druhého datacentra Azure. Tento přístup omezuje dopad na prostředky ve zdrojovém datacentru a využívá rychlejší přenosové rychlosti a vysoké limity šířky pásma dostupné mezi datacentry Azure.

> [!NOTE]
> Tento přístup může zvýšit krátkodobé náklady na migraci, protože by to mohlo znamenat další poplatky za šířku pásma pro výchozí přenos dat.

## <a name="optimize-and-promote-process-changes"></a>Změny procesu optimalizace a převedení

Řešení globální složitosti během optimalizace a převedení by mohlo vyžadovat duplicitní úsilí v každé další oblasti. V případě, že je přijatelné jediné nasazení, může být nadále vyžadováno duplikování firemního testování a firemní plány změn.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Navrhované akce během procesu optimalizace a převedení

**Optimalizace pomocí předběžného testování:** Počáteční automatické testování může identifikovat potenciální možnosti optimalizace stejně jako při jakékoli migraci. V případě globálních úloh je důležité úlohu testovat v každé oblasti nezávisle, protože i malé změny konfigurace v síti nebo cílovém datacentru Azure můžou ovlivnit výkon.

**Firemní plány změn:** U všech složitých scénářů migrace by se měl vytvořit firemní plán změn, aby se zajistila jasná komunikace týkající se jakýchkoli změn firemních procesů, uživatelského prostředí a načasování úsilí potřebného k integraci těchto změn. V případě globální migrace by měl tento plán zahrnovat důležité aspekty týkající se koncových uživatelů v každé ovlivněné geografické oblasti.

**Firemní testování:** Spolu s firemním plánem změn může být v každé oblasti vyžadováno firemní testování, aby se zajistil odpovídající výkon a kompatibilita s upravenými vzory směrování v síti.

**Testování převedení:** Převedení se často provádí jako jedna aktivita, která přesměruje produkční provoz do migrovaných úloh. V případě vydávání v globálním rozsahu by se převedení mělo provádět pomocí testovacích verzí (nebo u předem definovaných skupin uživatelů). To umožňuje týmu cloudové strategie a týmu přechodu na cloud lépe sledovat výkon a zlepšit podporu uživatelů v jednotlivých oblastech. Testovací verze převedení jsou často řízeny na úrovni sítě pomocí změn směrování konkrétních rozsahů IP adres ze zdrojových prostředků úloh na nově migrované prostředky. Po dokončení migrace určené skupiny koncových uživatelů je možné přesměrovat další skupinu.

**Optimalizace testování:** Jednou z výhod testovacích verzí převedení je to, že umožňuje podrobnější sledování a další optimalizaci nasazených prostředků. Po krátkém období používání první testovací verze jsou navržena další upřesnění migrovaných prostředků, když to umožňují provozní postupy IT.
