---
title: Nastavení kontroly provozní vhodnosti
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Doprovodné materiály k provozním základům
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/20/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 04afedc133d001405c5042b309a45c9b41f3268e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026964"
---
# <a name="establish-an-operational-fitness-review"></a>Nastavení kontroly provozní vhodnosti

Jak vaše firma začne provozovat úlohy v Azure, je dalším krokem vytvoření procesu pro *kontrolu provozní způsobilosti*. Tento proces provede výčet, implementuje a iterativní kontrolu požadavků na tyto úlohy, které nejsou *funkční* . Nefunkční požadavky se vztahují k očekávanému provoznímu chování služby.

Existuje pět základních kategorií nefunkčních požadavků, které se nazývají [pilíře kvality softwaru](https://docs.microsoft.com/azure/architecture/guide/pillars):

- Škálovatelnost
- Dostupnost
- Odolnost proti chybám, včetně kontinuity podnikových a zotavení po havárii
- Správa
- Zabezpečení

Proces pro kontrolu provozní vhodnosti zajišťuje, aby vaše nejdůležitější úlohy splňovaly očekávání vaší firmy s ohledem na pilíře kvality.

Váš podnik by měl vytvořit proces pro kontrolu provozních požadavků, aby plně pochopil problémy, které vznikají při spouštění úloh v produkčním prostředí, určení způsobu nápravy těchto problémů a jejich řešení. Tento článek popisuje proces vysoké úrovně pro kontrolu provozní vhodnosti, který může vaše společnost využít k dosažení tohoto cíle.

## <a name="operational-fitness-at-microsoft"></a>Provozní způsobilost v Microsoftu

Od samého začátku je vývoj platformy Azure průběžným projektem, který provádí mnoho týmů v rámci Microsoftu. Je obtížné zajistit kvalitu a konzistenci pro projekt takové velikosti a složitosti. K vytvoření výčtu a implementaci základních nefunkčních požadavků je potřeba robustní proces.

Procesy, které Microsoft sleduje, tvoří základ pro procesy uvedené v tomto článku.

## <a name="understand-the-problem"></a>Pochopení problému

Jak jste se naučili při [zahájení práce](../getting-started/migrate.md), je prvním krokem v digitální transformaci podniku určení obchodních problémů, které je potřeba vyřešit přijetím Azure. Dalším krokem je určení vysoké úrovně řešení problému, jako je například migrace zatížení do cloudu nebo přizpůsobení stávající místní služby, která zahrnuje cloudové funkce. Nakonec je řešení navrženo a implementováno.

Během tohoto procesu je fokus často na funkcích služby: sadu funkčních požadavků, které má služba provádět. Například služba doručování produktů vyžaduje funkce pro určení zdrojového a cílového umístění produktu, sledování produktu během doručování, zákaznických oznámení a dalších.

_Nefunkční_ požadavky naproti tomu se týkají vlastností, jako je [dostupnost](https://docs.microsoft.com/azure/architecture/checklist/availability)služby, [odolnost](https://docs.microsoft.com/azure/architecture/resiliency)a [škálovatelnost](https://docs.microsoft.com/azure/architecture/checklist/scalability). Tyto vlastnosti se liší od funkčních požadavků, protože nemají přímo vliv na konečnou funkci jakékoli konkrétní funkce ve službě. Nefunkční požadavky se ale týkají výkonu a kontinuity služby.

V souvislosti se smlouvou o úrovni služeb (SLA) je možné zadat některé nefunkční požadavky. V případě kontinuity služeb může být například požadavek na dostupnost služby vyjádřen jako procento: "Dostupná 99,99% času". Jiné nefunkční požadavky se můžou obtížně definovat a můžou se změnit podle potřeby produkčních potřeb. Například služba zaměřená na spotřebitele se může stát neočekávanými nároky na propustnost po nárůstu oblíbenosti.

> [!NOTE]
> Požadavky na odolnost proti chybám jsou podrobněji popsány v [návrhu spolehlivých aplikací Azure](https://docs.microsoft.com/azure/architecture/reliability#define-requirements). Tento článek obsahuje vysvětlení konceptů, jako je cíl bodu obnovení (RPO), cíle obnovení (RTO), smlouvy SLA a dalších.

## <a name="process-for-operational-fitness-review"></a>Proces pro kontrolu provozní vhodnosti

Klíčem k udržení výkonu a kontinuitě podnikových služeb je implementace procesu pro kontrolu provozní způsobilosti.

![Přehled procesu pro kontrolu provozní vhodnosti](../_images/manage/ofr-flow.png)

Na vysoké úrovni má proces dvě fáze. Ve *fázi předpoklady*jsou požadavky navázány a namapovány na podpůrné služby. K této fázi dochází zřídka: možná jednou nebo při zavedení nových operací. Výstup fáze "předpoklady" se používá ve *fázi toku*. Fáze toku probíhá častěji: doporučujeme měsíčně.

### <a name="prerequisites-phase"></a>Fáze předpokladů

Kroky v této fázi zachytí požadavky na pravidelnou kontrolu důležitých služeb.

1. **Identifikujte důležité obchodní operace**. Identifikujte klíčové podnikové operace v podniku. Obchodní operace jsou nezávislé na všech podporovaných funkcích služby. Jinými slovy, obchodní operace představují skutečné aktivity, které musí firma provádět a které jsou podporovány sadou IT služeb.

    Termín *kritické* (nebo *důležité pro podnikání*) odráží vážný dopad na firmu, pokud je operace ovlivněná. Například online prodejce může mít obchodní operace, jako je například "povolit zákazníkovi přidat položku do nákupního košíku" nebo "zpracovat platbu platební karty." Pokud některé z těchto operací selžou, zákazník nemůže dokončit transakci a podnik nebude moci realizovat prodej.

1. **Namapujte operace na služby**. Proveďte mapování důležitých obchodních operací na služby, které je podporují. V příkladu nákupního košíku se může jednat o několik služeb: Služba pro správu zásob, služba nákupního košíku a další. Za účelem zpracování platby prostřednictvím platební karty může místní platební služba komunikovat s třetí stranou služby pro zpracování plateb.

1. **Analyzujte závislosti služby**. Většina obchodních operací vyžaduje orchestraci mezi více podpůrnými službami. Je důležité pochopit závislosti mezi službami a tokem nejdůležitějších transakcí pomocí těchto služeb.

    Zvažte také závislosti mezi místními službami a službami Azure. V příkladu nákupního košíku se služba pro správu zásob inventáře může hostovat místně a ingestovat data zadaná zaměstnanci z fyzického skladu. Může se ale stát, že se data mimo pracoviště ukládají do služby Azure, jako je například [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction)nebo databáze, jako je například [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

Výstup z těchto aktivit je sada *metrik Scorecard* pro operace služeb. Metriky jsou zařazené do kategorií podle nefunkčních kritérií, jako je dostupnost, škálovatelnost a zotavení po havárii. Metriky přehledu výkonnostních metrik vyjadřují provozní kritéria, která by služba měla splnit. Tyto metriky je možné vyjádřit na libovolné úrovni členitosti, která je vhodná pro operaci služby.

Scorecard by měl být vyjádřen jednoduchým pojmem, aby bylo usnadněno smysluplné diskuze mezi vlastníky a inženýry firmy. Metrika přehledu výkonnostních metrik pro škálovatelnost by mohla být například vyjádřena zeleně pro splnění definovaných kritérií, žlutá pro neúspěšné splnění definovaných kritérií, ale aktivně implementuje plánovanou nápravu nebo červené pro neúspěšné splnění definovaných kritérií bez plánu. nebo akce.

Je důležité zdůraznit, že tyto metriky by měly přímo odpovídat obchodním potřebám.

### <a name="service-review-phase"></a>Fáze revize služby

Fáze revize služby je základem kontroly provozní způsobilostí. Zahrnuje tyto kroky:

1. **Změřte metriky služeb**. Pomocí metriky Scorecard monitorujte služby, abyste zajistili, že služby splňují očekávání firmy. Jinými slovy je důležité monitorování služeb. Pokud nemůžete monitorovat sadu služeb s ohledem na nefunkční požadavky, zvažte, že odpovídající metriky Scorecard budou červené. V tomto případě je prvním krokem pro nápravu implementace vhodného monitorování služby. Pokud firma například očekává, že služba bude pracovat s 99,99% dostupností, ale není k dispozici žádná provozní telemetrie pro měření dostupnosti, Předpokládejme, že nesplňujete požadavek.

2. Naplánujte nápravu. Pro každou operaci služby, pro kterou metriky spadají pod přijatelnou prahovou hodnotu, určete náklady na opravaí provozu provozu na přijatelnou úroveň. Pokud jsou náklady na Oprava služby větší, než je očekávané generování příjmů služby, přejděte k části a zvažte nehmotné náklady, jako je například prostředí zákazníka. Pokud například zákazníci mají potíže s umístěním úspěšné objednávky pomocí služby, mohou místo toho zvolit konkurenci.

3. **Implementujte nápravu**. Poté, co si vlastníci a inženýrské organizace přijměte plán, implementujte ho. Ohlaste stav implementace při každé kontrole metriky scorecard.

Tento proces je iterativní a v ideálním případě vaše společnost má tým vyhrazený. Tento tým by měl pravidelně splňovat kontrolu stávajících projektů pro nápravu, vykázat základní revizi nových úloh a sledovat celkový přehled výkonnostních metrik podniku. Tým by měl také mít oprávnění k tomu, aby si nastavili nápravné týmy, pokud jsou na plánu nebo nevyhověli metrikám.

## <a name="structure-of-the-review-team"></a>Struktura přezkoumání týmu

Tým zodpovědný za kontrolu provozních způsobilostí se skládá z následujících rolí:

- **Vlastník firmy**: Poskytuje znalost firmy k identifikaci a stanovení priorit každé klíčové obchodní operace. Tato role také porovnává náklady na zmírnění dopadů na firmu a při konečném rozhodování o nápravě jednotek.

- **Generální**Poradce pro firmy: Rozděluje obchodní operace na části diskrétní a mapuje tyto části na služby a infrastrukturu, ať už místně, nebo v cloudu. Role vyžaduje důkladné znalosti technologie přidružené k jednotlivým obchodním operacím.

- **Vlastník technické**: Implementuje služby přidružené k obchodní operaci. Tito jednotlivci se můžou zúčastnit návrhu, implementace a nasazení jakýchkoli řešení pro nefunkční problémy, které jsou v rámci přezkumu zjištěny.

- **Vlastník služby**. Provozuje aplikace a služby firmy. Tito jednotlivci shromažďují data o protokolování a využití pro tyto aplikace a služby. Tato data slouží k identifikaci problémů a k ověření oprav po jejich nasazení.

## <a name="review-meeting"></a>Zkontrolovat schůzku

Doporučujeme, aby váš tým kontroloval pravidelné plnění. Tým může například plnit každý měsíc a pak na čtvrtletní bázi nahlásit stav a metriky na vyšší.

Přizpůsobte podrobnosti procesu a schůzky podle svých konkrétních potřeb. Jako výchozí bod doporučujeme použít následující úlohy:

1. Obchodní vlastník a Poradce pro firmy mají na výběr a určení nefunkčních požadavků na jednotlivé obchodní operace se vstupem od techniků a vlastníků služeb. V případě obchodních operací, které byly identifikovány dříve, je priorita přezkoumána a ověřena. Pro nové obchodní operace je přiřazena priorita v existujícím seznamu.

2. Inženýri a vlastníci služeb mapují aktuální stav obchodních operací na odpovídající místní a cloudové služby. Mapování je seznam komponent v každé službě, které se orientují jako strom závislostí. Po vygenerování seznamu a stromu závislostí se určí kritické cesty prostřednictvím stromu.

3. Vlastníci techniků a služeb si prozkoumají aktuální stav protokolování a monitorování provozu pro služby uvedené v předchozím kroku. Robustní protokolování a monitorování jsou kritické: identifikují součásti služby, které přispívají k selhání při plnění nefunkčních požadavků. Pokud není dostatek protokolování a monitorování, je nutné vytvořit a implementovat plán, aby bylo možné je umístit.

4. Metriky Scorecard jsou vytvořeny pro nové obchodní operace. Přehled výkonnostních metrik se skládá ze seznamu součástí prvků pro každou službu identifikovanou v kroku 2. Je zarovnán podle nefunkčních požadavků a zahrnuje míru, jak dobře jednotlivé komponenty splňují požadavky.

5. U komponent, které nesplňují požadavky nefungující podle potřeby, je navrženo řešení vysoké úrovně a přiřadí se mu technický vlastník. V tuto chvíli si vlastník a podnikatel firmy zřídí rozpočet na nápravnou práci na základě očekávaných výnosů obchodní operace.

6. Nakonec je revize prováděna v probíhající nápravné práci. Každá metrika přehledu výkonnostních metrik pro probíhající práci je přezkoumána podle očekávaných kritérií. Pro součásti, které splňují kritéria metriky, vlastník služby prezentuje data protokolování a monitorování a potvrzuje, že jsou splněna kritéria. Pro ty součásti, které nesplňují kritéria metriky, každý technický vlastník vysvětluje problémy, které brání splnění kritérií, a prezentuje nové návrhy pro nápravu.

## <a name="recommended-resources"></a>Doporučené materiály

- [Pilíře kvality softwaru](https://docs.microsoft.com/azure/architecture/guide/pillars).
    Tato část Průvodce architekturou aplikací Azure popisuje pět pilířů kvality softwaru: škálovatelnost, dostupnost, odolnost, Správa a zabezpečení.
- [Deset principů návrhu pro aplikace Azure](https://docs.microsoft.com/azure/architecture/guide/design-principles).
    Tato část Průvodce architekturou aplikací Azure popisuje sadu principů návrhu, aby byla vaše aplikace lépe škálovatelná, odolná a spravovatelná.
- [Navrhování odolných aplikací pro Azure](https://docs.microsoft.com/azure/architecture/resiliency).
    Tato příručka začíná definicí pojmu odolnosti a souvisejících konceptů. Pak popisuje proces pro zajištění odolnosti pomocí strukturovaného přístupu po celou dobu životnosti aplikace, od návrhu a implementace až po nasazení a provoz.
- [Vzory návrhu cloudu](https://docs.microsoft.com/azure/architecture/patterns).
    Tyto vzory návrhu jsou užitečné pro technické týmy při sestavování aplikací na pilířích kvality softwaru.
