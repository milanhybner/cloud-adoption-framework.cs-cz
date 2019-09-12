---
title: Jak řešit složitost migrace více geografických oblastí
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Jak řešit složitost migrace více geografických oblastí
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3977618981212e2c0dc4dcd95ae14bf4dc773499
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905593"
---
# <a name="multiple-geographic-regions"></a>Několik zeměpisných oblastí

Když firmy působí ve více geografických oblastech, může to představovat další úroveň složitosti v rámci migrace do cloudu. Tato složitost se projevuje ve třech primárních oblastech: distribuce prostředků, profily přístupů uživatelů a požadavky na dodržování předpisů. Než začnete řešit složitost týkající se více oblastí, je důležité pochopit, jaký je rozsah této složitosti.

## <a name="general-scope-expansion"></a>Rozšíření obecného rozsahu

Pomocí následujícího přístupu můžete posoudit potenciální výzvy a vytvořit obecný plán postupu:

- Zvažte robustnější připravenost a implementaci zásad správného řízení.
- Sepište si ovlivněné geografické oblasti. Vytvořte si seznam oblastí a zemí, na které má migrace do cloudu vliv.
- Zdokumentujte si požadavky na suverenitu dat: Mají identifikované země požadavky na dodržování předpisů, které řídí suverenitu dat?
- Zdokumentujte si uživatelskou základnu: Budou zaměstnanci, partneři nebo zákazníci v identifikované zemi ovlivněni migrací do cloudu?
- Zdokumentujte si datacentra a prostředky: Existují v identifikované zemi nějaké prostředky, které by mohly být zahrnuty do migrace?

Přizpůsobte změny v rámci procesu migrace tak, aby řešily tento úvodní soupis.

### <a name="documenting-complexity"></a>Zdokumentování složitosti

Následující tabulka vám může pomoct při dokumentování zjištěných informací z výše uvedených kroků:

|Oblast  |Country  |Místní zaměstnanci  |Místní externí uživatelé  |Místní datacentra nebo prostředky |Požadavky na suverenitu dat  |
|---------|---------|---------|---------|---------|---------|
|Severní Amerika     |USA         |Ano         |Partneři a zákazníci         |Ano         |Ne         |
|Severní Amerika     |Kanada         |Ne         |Zákazníci         |Ano         |Ano         |
|Evropa     |Německo         |Ano         |Partneři a zákazníci         |Ne – pouze síť         |Ano         |
|Asie a Tichomoří     |Jižní Korea         |Ano         |Partneři         |Ano         |Ne         |

<!-- markdownlint-disable MD026 -->

### <a name="why-is-data-sovereignty-relevant"></a>Proč je suverenita dat relevantní?

Organizace státní správy na celém světě začaly zavádět požadavky na suverenitu dat, jako je například Obecné nařízení o ochraně osobních údajů (GDPR). Požadavky na dodržování předpisů tohoto typu často vyžadují lokalizaci v konkrétní oblasti nebo dokonce v konkrétní zemi kvůli ochraně občanů. V některých případech musí být data týkající se zákazníků, zaměstnanců nebo partnerů uložená v cloudové platformě ve stejné oblasti, ve které se nachází koncový uživatel.

Řešení těchto výzev významně motivuje globálně působící společnosti k migracím do cloudu. Kvůli udržování požadavků na dodržování předpisů se některé společnosti rozhodly nasazovat duplicitní IT prostředky u poskytovatelů cloudu v rámci dané oblasti. V tabulce s příklady výše by dobrým příkladem tohoto scénáře bylo Německo. V tomto příkladu se v Německu nachází zákazníci, partneři a zaměstnanci, ale žádné existující IT prostředky. Tato společnost se může rozhodnout nasadit některé prostředky do datacentra v rámci oblasti, na kterou se vztahuje GDPR, a potenciálně může dokonce využívat německá datacentra Azure. Pochopení toho, na která data má dopad GDPR, by pomohlo týmu přechodu na cloud určit, jaký je v tomto případě nejlepší přístup při migraci.

### <a name="why-is-the-location-of-end-users-relevant"></a>Proč hraje roli místo, kde se nachází koncoví uživatelé?

Společnosti, které podporují koncové uživatele ve více zemích, vyvinuly technická řešení pro přenosy dat u koncových uživatelů. V některých případech to zahrnuje lokalizaci prostředků. V jiných scénářích se společnost může místo toho rozhodnout implementovat globální řešení prostřednictvím sítí WAN a vyřešit tak potřeby nesourodých uživatelských základen prostřednictvím síťových řešení. V obou případech může být strategie migrace ovlivněná tím, jaké profily používání tito různí koncoví uživatelé mají.

Vzhledem k tomu, že společnost podporuje zaměstnance, partnery a zákazníky v Německu, ale v této zemi nejsou v současnosti žádná datacentra, je pravděpodobné, že tato společnost implementovala nějakou formu řešení s pronajatou linkou pro směrování příslušného provozu do datacenter v jiných zemích. Toto existující směrování představuje významné riziko pro vnímaný výkon migrovaných aplikací. Vkládání dalších směrování v rámci zavedené a optimalizované globální sítě WAN může po migraci vytvořit dojem nedostatečného výkonu aplikací. Hledání a oprava těchto problémů může způsobit významné zpoždění projektu. Každý z níže popsaných procesů zahrnuje pokyny k řešení této složitosti v rámci procesů stanovení předpokladů, posouzení, migrace a optimalizace. Pochopení profilů uživatelů v každé zemi je důležité pro odpovídající správu této složitosti.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Proč hraje roli místo, kde se nachází datacentra?

Umístění existujících datacenter může mít vliv na strategii migrace. Níže jsou uvedené některé z nejběžnějších dopadů:

**Rozhodnutí týkající se architektury:** Cílová oblast nebo umístění je jedním z prvních kroků návrhu strategie migrace. To je často ovlivněno umístěním existujících prostředků. Dostupnost cloudových služeb a jednotková cena těchto služeb se navíc může v jednotlivých oblastech lišit. Pochopení současného a budoucího umístění prostředků má proto vliv na rozhodnutí týkající se architektury a může také ovlivnit odhady rozpočtu.

**Závislosti datacenter:** Na základě dat ve výše uvedené tabulce je pravděpodobné, že mezi různými datacentry po celém světě existují závislosti. V mnoha organizacích, které působí s tímto typem rozsahu, nemusí být tyto závislosti zdokumentovány nebo jim lidé nemusí dobře rozumět. Přístupy používané k vyhodnocení profilů uživatelů vám pomůžou některé z těchto závislostí identifikovat. Během procesu posuzování jsou navrhovány další kroky s cílem omezit rizika spojená s touto složitostí.

## <a name="implementing-the-general-approach"></a>Implementace obecného přístupu

Tento přístup je založený na kvantifikovatelných informacích. Z tohoto důvodu bude následující přístup využívat model založený na datech za účelem řešení složitostí globální migrace.

## <a name="suggested-prerequisites"></a>Navrhované předpoklady

Doporučujeme, aby tým přechodu na cloud začal s migrací jednoduché úlohy pomocí [průvodce migrací do Azure](../azure-migration-guide/index.md), než se bude pokoušet o globální řešení. To zajistí, že se tento tým seznámí s obecným procesem migrace do cloudu předtím, než se pokusí o složitější scénář migrace.

Pokud rozsah migrace zahrnuje více oblastí, měl by tým přechodu na cloud vyhodnotit následující aspekty připravenosti:

- Suverenita dat může vyžadovat lokalizaci některých prostředků, může však existovat mnoho prostředků, které se nemusí řídit těmito omezeními souvisejícími s dodržováním předpisů. Aktivity, jako je protokolování, generování sestav, směrování sítě, identita a další centrální IT služby, můžou mít oprávnění být hostované jako sdílené služby v rámci více předplatných nebo dokonce i více oblastí. Doporučujeme, aby tým pro přechod do cloudu vyhodnotil u těchto služeb model sdílených služeb, jak je uvedeno v [referenční architektuře hvězdicové topologie se sdílenými službami](/azure/architecture/reference-architectures/hybrid-networking/shared-services).
- Při nasazování více instancí podobných prostředí by mohl objekt pro vytváření prostředí zajistit konzistenci, zlepšit zásady správného řízení a urychlit nasazení. [Cesta k zásadám správného řízení pro velké firmy](../../governance/journeys/complex-enterprise/index.md) zavádí přístup s vytvářením objektu pro vytváření prostředí, který umožňuje škálování v rámci více oblastí.

Jakmile tým stanoví vyhovující základní přístup a je k dispozici odpovídající připravenost, je třeba zvážit několik předpokladů řízených daty:

- **Obecné zjišťování:** Vytvořte si tabulku pro [zdokumentování složitosti](#documenting-complexity), jak je uvedeno výše.
- **Proveďte analýzu profilů uživatelů v každé ovlivněné zemi:** Je důležité, abyste v počáteční fázi procesu migrace porozuměli obecnému směrování u koncových uživatelů. Změna globálních pronajatých linek a přidávání připojení, jako je ExpressRoute, do cloudového datového centra může vyžadovat zpoždění v řádu měsíců. Tuto možnost proto vyřešte v rámci procesu co nejdříve.
- **Počáteční racionalizace digitálních aktiv:** Vždy, když je do strategie migrace zavedena složitost, měla by být provedena počáteční racionalizace digitálních aktiv. Pomoc najdete v pokynech týkajících se [racionalizace digitálních aktiv](../../digital-estate/index.md).
  - **Další požadavky na digitální aktiva:** Stanovte zásady označování pro identifikaci všech úloh, které jsou ovlivněny požadavky na suverenitu dat. Požadované značky by měly začínat ve fázi racionalizace digitálních aktiv a pokračovat až do migrovaných prostředků.
- **Vyhodnocení modelu hvězdicové architektury:** Distribuované systémy často sdílí společné závislosti. Tyto závislosti lze často řešit prostřednictvím implementace modelu hvězdicové architektury. I když není takový model součástí rozsahu procesu migrace, měl by být posouzen během budoucích iterací [připravených procesů](../../ready/index.md).
- **Stanovení priorit u nevyřízených položek migrace:** Pokud je nutné dělat změny v síti kvůli podpoře nasazení úlohy podporující více oblastí do produkčního prostředí, je důležité, aby tým cloudové strategie mohl sledovat a spravovat eskalace týkající se těchto změn v síti. Tyto změny pomůže urychlit podpora na vyšší úrovni managementu. Důležitější však je, že to dává týmu pro strategii možnost měnit priority nevyřízených položek a zajistit tak, aby kvůli změnám sítě nebyly blokovány globální úlohy. Jen takové úlohy by měly mít prioritu poté, co se změny sítě dokončí.

Tyto předpoklady vám pomůžou nastavit procesy, které můžou řešit tuto složitost během realizace strategie migrace.

## <a name="assess-process-changes"></a>Posouzení změn procesu

Při řešení složitostí globálních prostředků a uživatelských základen by do posouzení jakéhokoli kandidáta na migraci mělo být přidáno několik klíčových aktivit. Každá z těchto změn pomůže vyjasnit dopad na globální uživatele a prostředky prostřednictvím přístupu řízeného daty.

### <a name="suggested-action-during-the-assess-process"></a>Navrhované akce během procesu posouzení

**Vyhodnocení závislostí mezi datacentry:** [Nástroje pro vizualizaci závislostí v Azure Migrate](/azure/migrate/concepts-dependency-visualization) vám můžou pomoct identifikovat závislosti. Použití této sady nástrojů před migrací je dobrý obecný osvědčený postup. Při řešení globální složitosti je to však nezbytný krok procesu posouzení. Prostřednictvím [seskupování závislostí](/azure/migrate/how-to-create-group-machine-dependencies) může vizualizace pomoct identifikovat IP adresy a porty všech prostředků vyžadovaných pro podporu dané úlohy.

> [!IMPORTANT]
> Dvě důležité poznámky: Zaprvé, odborník, který rozumí umísťování prostředků a schématům IP adres, musí identifikovat prostředky, které se nachází v sekundárním datovém centru. Zadruhé je důležité vyhodnotit podřízené závislosti a klienty ve vizuálu a pochopit obousměrné závislosti.

**Identifikace globálního dopadu na uživatele:** Výstupy z analýzy profilů uživatelů pro stanovení předpokladů by měly identifikovat všechny úlohy ovlivněné globálními profily uživatelů. Když je kandidát pro migraci v seznamu ovlivněných úloh, měl by se architekt připravující migraci poradit s odborníky na sítě a provoz, aby ověřil, jaká jsou očekávání týkající se směrování v síti a výkonu. Architektura by měla přinejmenším zahrnovat připojení ExpressRoute mezi nejbližším střediskem NOC (Network Operations Center) a Azure. [Referenční architektura připojení ExpressRoute](/azure/architecture/reference-architectures/hybrid-networking/expressroute) může pomoct s konfigurací nezbytného připojení.

**Návrh zohledňující dodržování předpisů:** Výstupy z analýzy profilů uživatelů pro stanovení předpokladů by měly identifikovat všechny úlohy ovlivněné požadavky na suverenitu dat. V rámci aktivit v procesu posouzení týkajících se architektury by se měl přiřazený architekt poradit s odborníky na dodržování předpisů, aby porozuměl všem požadavkům na migraci a nasazení ve více oblastech. Tyto požadavky významně ovlivní strategie návrhu. Při návrhu vám můžou pomoct referenční architektury [webových aplikací pro více oblastí](/azure/architecture/reference-architectures/app-service-web-app/multi-region) a [n-vrstvých aplikací pro více oblastí](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server).

> [!WARNING]
> Když budete používat jednu z výše uvedených referenčních architektur, může být nutné vyloučit konkrétní datové prvky z replikačních procesů kvůli zajištění požadavků na suverenitu dat. Tím se do procesu převedení přidá další krok.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Při migraci aplikace, která musí být nasazená ve více oblastech, musí tým přechodu na cloud vzít v úvahu několik důležitých aspektů. Ty zahrnují návrh trezoru Azure Site Recovery, návrh konfiguračního a procesového serveru, návrhy šířky pásma sítě a synchronizaci dat.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhované akce během procesu migrace

**Návrh trezoru Azure Site Recovery:** Azure Site Recovery je navrhovaný nástroj pro nativní cloudovou replikaci a synchronizaci digitálních prostředků do Azure. Site Recovery replikuje data o daném prostředku do trezoru Site Recovery, který je vázán na konkrétní předplatné v konkrétní oblasti a datacentru Azure. Při replikaci prostředků do druhé oblasti může být vyžadován druhý trezor Site Recovery.

**Návrh konfiguračního a procesového serveru:** Site Recovery používá místní instanci konfiguračního a procesového serveru, který je vázaný na jeden trezor Site Recovery. To znamená, že kvůli zajištění replikace může být nutné nainstalovat druhou instanci těchto serverů ve zdrojovém datacentru.

**Návrh šířky pásma sítě:** Během replikace a průběžné synchronizace se binární data přesunují po síti ze zdrojového datacentra do trezoru Site Recovery v cílovém datacentru Azure. Tento proces spotřebovává šířku pásma. Duplikování úlohy do druhé oblasti zdvojnásobí spotřebovávanou šířku pásma. Když je šířka pásma omezená nebo pokud úloha zahrnuje velký objem odchylek konfigurací nebo dat, může to kolidovat s dobou, která je vyžadovaná k dokončení migrace. Ještě důležitější je, že by to mohlo ovlivnit práci uživatelů nebo aplikací, které stále závisí na šířce pásma zdrojového datacentra.

**Synchronizace dat:** Největší využití šířky pásma je často způsobené synchronizací datové platformy. Jak je definováno v referenčních architekturách [webových aplikací pro více oblastí](/azure/architecture/reference-architectures/app-service-web-app/multi-region) a [n-vrstvých aplikací pro více oblastí](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server), synchronizace dat je často vyžadovaná kvůli udržování aplikací na stejné úrovni. Pokud je toto požadovaný provozní stav dané aplikace, může být před migrací aplikace a prostředků střední vrstvy vhodné dokončit synchronizaci mezi zdrojovou datovou platformou a všemi cloudovými platformami.
**Synchronizace dat:** Největší využití šířky pásma je často způsobené synchronizací datové platformy. Jak je definováno v referenčních architekturách [webových aplikací pro více oblastí](/azure/architecture/reference-architectures/app-service-web-app/multi-region) a [n-vrstvých aplikací pro více oblastí](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server), synchronizace dat je často vyžadovaná kvůli udržování aplikací na stejné úrovni. Pokud je toto požadovaný provozní stav dané aplikace, může být před migrací aplikace a prostředků střední vrstvy vhodné dokončit synchronizaci mezi zdrojovou datovou platformou a všemi cloudovými platformami.

**Zotavení po havárii Azure do Azure:** Pomocí alternativní možnosti můžete dále snížit složitost. Pokud časové plány a přístupy synchronizace dat vyžadují nasazení ve dvou krocích, může být [zotavení po havárii Azure do Azure](/azure/site-recovery/azure-to-azure-architecture) přijatelné řešení. V tomto scénáři je úloha nejprve migrována do prvního datacentra Azure pomocí jediného trezoru Site Recovery a návrhu konfiguračního nebo procesového serveru. Po otestování může být úloha obnovena z migrovaných prostředků do druhého datacentra Azure. Tento přístup omezuje dopad na prostředky ve zdrojovém datacentru a využívá rychlejší přenosové rychlosti a vysoké limity šířky pásma dostupné mezi datacentry Azure.

> [!NOTE]
> Tento přístup může zvýšit krátkodobé náklady na migraci, protože by to mohlo znamenat další poplatky za šířku pásma pro výchozí přenos dat.

## <a name="optimize-and-promote-process-changes"></a>Změny procesu optimalizace a převedení

Řešení globální složitosti během optimalizace a převedení by mohlo vyžadovat duplicitní úsilí v každé další oblasti. V případě, že je přijatelné jediné nasazení, může být nadále vyžadováno duplikování firemního testování a firemní plány změn.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Navrhované akce během procesu optimalizace a převedení

**Optimalizace pomocí předběžného testování:** Počáteční automatické testování může identifikovat potenciální možnosti optimalizace stejně jako při jakékoli migraci. V případě globálních úloh je důležité úlohu testovat v každé oblasti nezávisle, protože i malé změny konfigurace v síti nebo cílovém datacentru Azure můžou ovlivnit výkon.

**Firemní plány změn:** U všech složitých scénářů migrace se doporučuje vytvořit firemní plán změn, aby se zajistila jasná komunikace týkající se jakýchkoli změn firemních procesů, uživatelského prostředí a načasování úsilí potřebného k integraci těchto změn. V případě globální migrace by měl tento plán zahrnovat důležité aspekty týkající se koncových uživatelů v každé ovlivněné geografické oblasti.

**Firemní testování:** Spolu s firemním plánem změn může být v každé oblasti vyžadováno firemní testování, aby se zajistil odpovídající výkon a kompatibilita s upravenými vzory směrování v síti.

**Testování převedení:** Převedení se často provádí jako jedna aktivita, která přesměruje produkční provoz do migrovaných úloh. V případě vydávání v globálním rozsahu doporučujeme převedení provádět pomocí testovacích verzí (nebo u předem definovaných skupin uživatelů). To umožňuje týmu cloudové strategie a týmu přechodu na cloud lépe sledovat výkon a zlepšit podporu uživatelů v jednotlivých oblastech. Testovací verze převedení jsou často řízeny na úrovni sítě pomocí změn směrování konkrétních rozsahů IP adres ze zdrojových prostředků úloh na nově migrované prostředky. Po dokončení migrace určené skupiny koncových uživatelů je možné přesměrovat další skupinu.

**Optimalizace testování:** Jednou z výhod testovacích verzí převedení je to, že umožňuje podrobnější sledování a další optimalizaci nasazených prostředků. Po krátkém období používání první testovací verze jsou navržena další upřesnění migrovaných prostředků, když to umožňují provozní postupy IT.

## <a name="next-steps"></a>Další postup

Samostatnou součástí složitosti, která se často týká více oblastí, je potřeba přípravy na migraci [více datacenter](./multiple-datacenters.md). Ačkoli je to v principu podobné, řeší se u této složitosti objem prostředků k migraci při přesunování více datacenter do cloudu.

> [!div class="nextstepaction"]
> [Migrace více datacenter](./multiple-datacenters.md)
