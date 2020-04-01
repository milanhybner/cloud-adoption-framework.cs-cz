---
title: Přehled platforem monitorování cloudu
description: Získejte podrobný přehled dvou monitorovacích platforem, které vám pomůžou pochopit, jak jednotlivé funkce nástroje poskytují základní monitorování.
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 088085af7dee93d0a1d69a1d6592b827c7a1c975
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527169"
---
<!-- cSpell:ignore opsman ITSM -->

# <a name="cloud-monitoring-guide-monitoring-platforms-overview"></a>Průvodce monitorováním cloudu: Přehled monitorovacích platforem

Společnost Microsoft poskytuje řadu možností monitorování ze dvou produktů: System Center Operations Manager, které byly navrženy místně a následně rozšířeny do cloudu, a Azure Monitor, které byly navrženy pro Cloud, ale mohou také monitorovat místní prostředí. OSI. Tyto dvě nabídky poskytují základní monitorovací služby, jako jsou například výstrahy, sledování doby provozu služby, monitorování stavu aplikace a infrastruktury, diagnostika a analýza.

Mnoho organizací si přechodu nejnovější postupy pro DevOps flexibilitu a cloudové inovace pro správu prostředí heterogenní. I když jsou i na jejich schopnost dělat vhodná a odpovědná rozhodnutí týkající se monitorování těchto úloh.

Tento článek obsahuje podrobný přehled našich monitorovacích platforem, které vám pomůžou pochopit, jak jednotlivé funkce nástroje poskytují základní monitorování.

## <a name="the-story-of-system-center-operations-manager"></a>Příběh System Center Operations Manager

V 2000 jsme do pole Operations Management zadali Microsoft Operations Manager (MOM) 2000. V 2007 jsme představili provedenou verzi produktu s názvem System Center Operations Manager. Přesunuli jsme se nad rámec jednoduchého monitorování Windows serveru a soustřeďte se na robustní, komplexní monitorování služeb a aplikací, včetně platforem heterogenní, síťových zařízení a dalších závislostí aplikací nebo služeb. Je to vytvořená platforma pro monitorování na podnikové úrovni pro místní prostředí ve stejné třídě jako IBM Tivoli nebo HP Operations Manager v oboru. Zvětšila se podpora monitorování výpočetních prostředků a prostředků platforem, které běží v Azure, Amazon Web Services (AWS) a dalších poskytovatelích cloudu.

## <a name="the-story-of-azure-monitor"></a>Příběh Azure Monitor

Po vydání Azure v 2010 byl k dispozici monitorování cloudových služeb s agentem Azure Diagnostics, který poskytuje způsob shromažďování diagnostických dat z prostředků Azure. Tato funkce byla považována za obecný nástroj pro monitorování, nikoli na podnikovou platformu pro monitorování.  

Application Insights bylo zavedeno k posunu se změnami v odvětví, kde došlo ke zvětšování rozšiřování cloudových, mobilních a IoT zařízení a zavedení postupů DevOps. Z monitorování výkonu aplikací v Operations Manager ke službě v Azure, kde poskytuje bohatě sledující webové aplikace napsané v různých jazycích. V 2015 byla oznámena verze Preview Application Insights pro sadu Visual Studio a později byla známa jako pouze Application Insights. Shromažďuje údaje o výkonu aplikace, požadavcích a výjimkách a trasováních.

V 2015 se služba Azure Operational Insights všeobecně zpřístupnila. Dodávala službu Analysis Services Log Analytics, která shromáždila a prohledala data z počítačů v Azure, v místním prostředí nebo v jiných cloudových prostředích a připojená k System Center Operations Manager. Byly nabídnuty sady Intelligence, které dostaly řadu předbalených konfigurací správy a monitorování, které obsahují kolekci dotazů a analytických logik, vizualizací a pravidel shromažďování dat pro takové scénáře jako audit zabezpečení, stav posouzení a správa výstrah. Později se Azure Operational Insights stal známým jako Log Analytics.  

V 2016 je verze Preview Azure Monitor oznámila na konferenci Microsoft Ignite. Poskytovala společné rozhraní pro shromažďování metrik platforem, protokoly diagnostiky prostředků a události protokolu aktivit na úrovni předplatného ze všech služeb Azure, které začali používat rozhraní. Dříve měla každá služba Azure vlastní metodu monitorování.

Na konferenci 2018 Ignite jsme oznámili, že se značka Azure Monitor rozšířila, aby zahrnovala několik různých služeb, které byly původně vyvinuty s nezávislou funkcí:

- Původní **Azure monitor**pro shromažďování metrik platforem, protokolů diagnostiky prostředků a protokolů aktivit jenom pro prostředky platformy Azure.
- **Application Insights**pro monitorování aplikací.
- **Log Analytics**, primární umístění pro shromažďování a analýzu dat protokolu.
- Nová **sjednocená služba upozorňování**, která vznesla mechanismy výstrah od každé z dalších výše zmíněných služeb.  
- **Azure Network Watcher**pro monitorování, diagnostikování a zobrazení metrik pro prostředky ve službě Azure Virtual Network.

## <a name="the-story-of-operations-management-suite-oms"></a>Scénář Operations Management Suite (OMS)

Od 2015 do dubna 2018 byla Operations Management Suite (OMS) sdružením následujících služeb správy Azure pro účely licencování:

- Application Insights
- Azure Automation
- Azure Backup
- Operational Insights (později Log Analytics)
- Site Recovery

Funkce služeb, které byly součástí OMS, se nezměnily, když byla zastavena OMS. Přerovnaná v rámci Azure Monitor.

## <a name="infrastructure-requirements"></a>Požadavky na infrastrukturu

### <a name="operations-manager"></a>Operations Manager

Operations Manager vyžaduje významnou infrastrukturu a údržbu pro podporu skupiny pro správu, což je základní funkční jednotka. Minimálně skupina pro správu se skládá z jednoho nebo více serverů pro správu, SQL Server instance, hostování provozní databáze datového skladu a sestav a agentů. Složitost návrhu skupiny pro správu závisí na několika faktorech, například na rozsahu úloh, které se mají monitorovat, a počtu zařízení nebo počítačů, které podporují úlohy. Pokud požadujete vysokou dostupnost a odolnost lokality, jak často se jedná o podnikové platformy pro monitorování, požadavky na infrastrukturu a přidružená údržba se můžou výrazně zvýšit.

![Diagram Operations Manager skupiny pro správu](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor je nabídka typu software jako služba (SaaS), takže její podpůrná infrastruktura běží v Azure a je spravovaná Microsoftem. Provádí monitorování, analýzu a diagnostiku ve velkém měřítku. Je k dispozici ve všech národních cloudech. Základní části infrastruktury (sběrače, metriky a protokoly úložiště a analýzy), které podporují Azure Monitor, jsou spravovány společností Microsoft.  

![Diagram Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Shromažďování dat

<!-- markdownlint-disable MD024 -->

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agenti

Operations Manager shromažďuje data přímo pouze z agentů, kteří jsou nainstalováni v [počítačích se systémem Windows](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent). Může přijímat data z Operations Manager SDK, ale tento přístup se obvykle používá pro partnery, kteří produkt rozšířili na vlastní aplikace, a ne pro shromažďování dat monitorování. Může shromažďovat data z jiných zdrojů, jako jsou například [počítače se systémem Linux](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) a síťová zařízení, pomocí speciálních modulů, které jsou spuštěny v agentovi systému Windows, který vzdáleně přistupuje k těmto jiným zařízením.

![Diagram agenta Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

Agent Operations Manager může shromažďovat data z několika zdrojů dat v místním počítači, například protokol událostí, vlastní protokoly a čítače výkonu. Může také spouštět skripty, které mohou shromažďovat data z místního počítače nebo z externích zdrojů. Můžete psát vlastní skripty pro shromažďování dat, která se nedají shromažďovat jiným způsobem, nebo shromažďovat data z různých vzdálených zařízení, která nemůžou jinak sledovat.

#### <a name="management-packs"></a>Sady Management Pack

Operations Manager provádí všechna monitorování pomocí pracovních postupů (pravidla, monitorování a zjišťování objektů). Tyto pracovní postupy jsou baleny společně v [Management Pack](https://docs.microsoft.com/system-center/scom/manage-overview-management-pack?view=sc-om-2019) a nasazeny do agentů. Sady Management Pack jsou k dispozici pro různé produkty a služby, které zahrnují předdefinovaná pravidla a monitory. Můžete také vytvořit vlastní Management Pack pro vlastní aplikace a vlastní scénáře.

#### <a name="monitoring-configuration"></a>Konfigurace monitorování

Sady Management Pack mohou obsahovat stovky pravidel, monitorování a pravidla zjišťování objektů. Agent spouští všechna tato nastavení monitorování ze všech použitých sad Management Pack, které jsou určeny podle pravidel zjišťování. Každá instance každého nastavení monitorování se spouští nezávisle a funguje okamžitě s daty, která shromažďuje. To je způsob, jakým Operations Manager může dosáhnout upozorňování téměř v reálném čase a aktuálního stavu monitorovaných prostředků.

Monitor může například vzorkovat čítač výkonu každých pár minut. Pokud tento čítač překročí prahovou hodnotu, okamžitě nastaví stav cílového objektu, který okamžitě aktivuje výstrahu ve skupině pro správu. Naplánované pravidlo může sledovat konkrétní událost, která se má vytvořit, a okamžitě vyvolat výstrahu, když se tato událost vytvoří v místním protokolu událostí.

Vzhledem k tomu, že jsou tato nastavení monitorování izolovaná od sebe a pracují z jednotlivých zdrojů dat, Operations Manager mají problémy korelující data mezi více zdroji. Je také obtížné reagovat na data po shromáždění. Můžete spouštět pracovní postupy, které přistupují k databázi Operations Manager, ale tento scénář není běžný a obvykle se používá pro omezený počet pracovních postupů pro zvláštní účely.

![Diagram Operations Manager skupiny pro správu](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Zdroje dat

Azure Monitor shromažďuje data z nejrůznějších zdrojů, včetně prostředků infrastruktury Azure a platforem, agentů v počítačích se systémem Windows a Linux a monitorování dat shromažďovaných ve službě Azure Storage. Libovolný klient REST může zapisovat data protokolu do Azure Monitor pomocí rozhraní API a můžete definovat vlastní metriky pro webové aplikace. Některá data metriky je možné směrovat do různých umístění v závislosti na jejich využití. Můžete například použít data pro upozorňování "rychlé použití" nebo pro dlouhodobé vyhledávání analýz trendů ve spojení s dalšími daty protokolů.

#### <a name="monitoring-solutions-and-insights"></a>Monitorování řešení a přehledů

Řešení monitorování používají platformu log v Azure Monitor k zajištění monitorování konkrétní aplikace nebo služby. Obvykle definují shromažďování dat od agentů nebo ze služeb Azure a poskytují dotazy a zobrazení protokolů k analýze těchto dat. Obvykle neposkytují pravidla upozornění, což znamená, že je nutné definovat vlastní kritéria výstrahy na základě shromážděných dat.

Přehledy, jako je například Azure Monitor pro kontejnery a Azure Monitor pro virtuální počítače, využívají platformu Azure Monitor protokoly a metriky, které poskytují přizpůsobené možnosti monitorování pro aplikaci nebo službu v Azure Portal. Kromě přizpůsobené analýzy shromážděných dat můžou poskytovat podmínky monitorování a upozorňování na stav.

#### <a name="monitoring-configuration"></a>Konfigurace monitorování

Azure Monitor odděluje shromažďování dat od akcí pořízených s těmito daty, která podporuje distribuované mikroslužby v cloudovém prostředí. Slučuje data z více zdrojů do Common data Platform a poskytuje možnosti analýzy, vizualizace a upozorňování na základě shromážděných dat.

Data shromážděná pomocí Azure Monitor se ukládají jako protokoly nebo metriky a různé funkce Azure Monitor spoléhají na obě funkce. Metriky obsahují číselné hodnoty v časových řadách, které jsou vhodné pro výstrahy téměř v reálném čase a rychlé zjišťování problémů. Protokoly obsahují text nebo číselná data a lze je dotazovat pomocí výkonného jazyka, zejména užitečného pro provádění složitých analýz.

Vzhledem k tomu, že Azure Monitor odděluje shromažďování dat z akcí proti těmto datům, nemusí být v mnoha případech možné poskytnout výstrahy téměř v reálném čase. Pro upozornění na data protokolu se dotazy spouštějí podle opakujícího se plánu definovaného v upozornění. Díky tomuto chování může Azure Monitor snadno korelovat data ze všech monitorovaných zdrojů a interaktivně analyzovat data různými způsoby. To je užitečné hlavně při provádění analýz hlavní příčiny a určení, kde k problému může dojít.

## <a name="health-monitoring"></a>Monitorování stavu

### <a name="operations-manager"></a>Operations Manager

Sady Management Pack v Operations Manager zahrnují model služby, který popisuje komponenty monitorované aplikace a jejich vztah. Monitory identifikují aktuální stav každé součásti na základě dat a skriptů v agentovi. Stavy jsou shrnuté tak, abyste mohli rychle zobrazit shrnutí stavů monitorovaných počítačů a aplikací.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor neposkytuje uživatelsky definované metody implementace modelu služby nebo monitorování, které označují aktuální stav všech součástí služby. Vzhledem k tomu, že řešení monitorování jsou založená na standardních funkcích Azure Monitor, neposkytují monitorování na úrovni stavu. Následující funkce Azure Monitor můžou být užitečné:

- **Application Insights:** Vytvoří složenou mapu webové aplikace a poskytne stav pro každou součást aplikace nebo závislost. Patří sem stav výstrah a přechod k podrobnostem pro podrobnější diagnostiku vaší aplikace.

- **Azure monitor pro virtuální počítače:** Poskytuje prostředí pro monitorování stavu pro hostované virtuální počítače Azure, podobně jako u Operations Manager, když monitoruje virtuální počítače s Windows a Linuxem. Vyhodnotí stav klíčových komponent operačního systému z perspektivy dostupnosti a výkonu a určí aktuální stav. Když zjistí, že virtuální počítač hosta má trvalé využívání prostředků, kapacitu místa na disku nebo problém související se základní funkcí operačního systému, vygeneruje výstrahu, která tento stav zaznamená do vaší pozornosti.

- **Azure monitor pro kontejnery:** Monitoruje výkon a stav služby Azure Kubernetes nebo Azure Container Instances. Z řadiče, uzly a kontejnerů, které jsou k dispozici v Kubernetes prostřednictvím rozhraní API metrik shromažďuje metriky paměti a procesoru. Shromažďuje také protokoly kontejnerů a data inventáře o kontejnerech a jejich obrázcích. Předdefinovaná kritéria stavu, která jsou založená na shromážděných datech výkonu, vám pomůžou zjistit, jestli existuje problém s kritickým prostředkem nebo kapacitou. Můžete také pochopit celkový výkon nebo výkon konkrétního typu objektu Kubernetes (pod, uzlem, kontrolérem nebo kontejnerem).

## <a name="analyze-data"></a>Analýza dat

### <a name="operations-manager"></a>Operations Manager

Operations Manager poskytuje čtyři základní způsoby, jak analyzovat data po shromáždění:

- **Průzkumník stavů:** Pomůže vám zjistit, které monitory identifikují problém se stavem, a zkontrolovat znalosti o monitorování a možných příčinách akcí, které s ním souvisejí.

- **Zobrazení:** Nabízí předdefinované vizualizace shromážděných dat, například graf dat o výkonu nebo seznam monitorovaných komponent a jejich aktuální stav. Zobrazení diagramu vizuálně prezentují model služby aplikace.

- **Sestavy:** Umožňuje shrnout historická data uložená v datovém skladu Operations Manager. Můžete přizpůsobit data, která jsou založená na zobrazeních a sestavách. Neexistuje ale žádná funkce, která umožňuje složitou nebo interaktivní analýzu shromážděných dat.

- **Operations Manager příkazové prostředí:** Rozšiřuje prostředí Windows PowerShell o další sadu rutin a může dotazovat a vizualizovat shromážděná data. To zahrnuje grafy a další vizualizace, nativně pomocí prostředí PowerShell nebo Operations Manager webové konzole založené na jazyce HTML.

### <a name="azure-monitor"></a>Azure Monitor

Pomocí výkonného analytického modulu Azure Monitor můžete interaktivně pracovat s daty protokolů a kombinovat je s dalšími daty monitorování pro účely trendů a dalších analýz dat. Zobrazení a řídicí panely umožňují vizualizovat data dotazů různými způsoby od Azure Portal a importovat je do Power BI. Mezi řešení monitorování patří dotazy a zobrazení, která prezentují data, která shromažďuje. Přehledy, jako jsou Application Insights, Azure Monitor pro virtuální počítače a Azure Monitor pro kontejnery, zahrnují přizpůsobené vizualizace pro podporu scénářů interaktivního monitorování.

## <a name="alerting"></a>Zobrazení výstrah

### <a name="operations-manager"></a>Operations Manager

Operations Manager vytváří výstrahy v reakci na předdefinované události, při splnění prahové hodnoty výkonu a při změně stavu monitorované součásti. Zahrnuje úplnou správu výstrah, což vám umožní nastavit jejich rozlišení a přiřadit je různým operátorům nebo systémovým technikům. Můžete nastavit pravidla oznámení, která určují, která upozornění budou odesílat proaktivní oznámení.

Sady Management Pack zahrnují různá předdefinovaná pravidla výstrah pro různé kritické podmínky v monitorovaných aplikacích. Tato pravidla můžete vyladit nebo vytvořit vlastní pravidla pro konkrétní požadavky vašeho prostředí.

### <a name="azure-monitor"></a>Azure Monitor

Pomocí Azure Monitor můžete vytvářet výstrahy na základě metriky překračující prahovou hodnotu nebo na základě plánovaného výsledku dotazu. I když výstrahy založené na metrikách můžou dosahovat výsledků téměř v reálném čase, plánované dotazy mají delší dobu odezvy v závislosti na rychlosti přijímání a indexování dat. Místo omezení na konkrétního agenta, výstrahy dotazování protokolu v Azure Monitor umožňují analyzovat data napříč všemi daty uloženými ve více pracovních prostorech. Tyto výstrahy také zahrnují data z konkrétní aplikace Application Insights pomocí dotazu mezi pracovními prostory.

I když monitorovací řešení můžou zahrnovat pravidla výstrah, obvykle je vytváříte na základě vašich požadavků.

## <a name="workflows"></a>Pracovní postupy

### <a name="operations-manager"></a>Operations Manager

Sady Management Pack v Operations Manager obsahují stovky individuálních pracovních postupů a určují, jaká data se mají shromažďovat a jakou akci s těmito daty mají dělat. Pravidlo může například vzorkovat čítač výkonu každých pár minut a uložit jeho výsledky k analýze. Monitorování může vzorkovat stejný čítač výkonu a porovnat jeho hodnotu s prahovou hodnotou pro zjištění stavu monitorovaného objektu. Jiné pravidlo může spustit skript, který shromáždí a analyzuje data v počítači agenta, a potom spustí výstrahu, pokud vrátí určitou hodnotu.

Pracovní postupy v Operations Manager jsou nezávisle na sobě navzájem nezávislé, což ztěžuje analýzu v několika monitorovaných objektech. Tyto scénáře monitorování musí být založené na datech po shromáždění, což je možné, ale může být obtížné a není běžné.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor odděluje shromažďování dat z akcí a analýz z těchto dat. Agenti a další zdroje dat zapisují data protokolu do Log Analyticsho pracovního prostoru a zapisují data metrik do databáze metrik bez jakékoli analýzy těchto dat nebo znalosti toho, jak by se mohla použít. Monitorování provádí výstrahy a další akce z uložených dat, což umožňuje provádět analýzu napříč daty ze všech zdrojů.

## <a name="extend-the-base-platform"></a>Rozšiřování základní platformy

### <a name="operations-manager"></a>Operations Manager

Operations Manager implementuje veškerou logiku monitorování v Management Pack, kterou buď vytvoříte sami, nebo ji získáte od nás nebo od partnera. Když nainstalujete Management Pack, automaticky zjistí komponenty aplikace nebo služby na různých agentech a nasadí vhodná pravidla a monitory. Management Pack obsahuje definice stavu, pravidla výstrah, pravidla pro shromažďování výkonu a událostí a zobrazení, která poskytují kompletní monitorování, které podporuje službu nebo aplikaci infrastruktury.

Sada Operations Manager SDK umožňuje Operations Manager integraci s monitorovacími platformami třetích stran nebo softwarem správa IT služeb (ITSM). Sada SDK je také používána některými sadami partnerských sad pro podporu monitorování síťových zařízení a poskytování vlastních prezentačních prostředí, jako je například druhý řídicí panel HTML5 nebo integrace s systém Microsoft Office Visio.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor shromažďuje metriky a protokoly z prostředků Azure, a to s nízkou konfigurací. Řešení monitorování přidávají logiku pro monitorování aplikace nebo služby, ale budou fungovat i v rámci standardních dotazů protokolu a zobrazení v monitorování. Přehledy, jako jsou Application Insights a Azure Monitor pro virtuální počítače, využívají platformu monitorování pro shromažďování a zpracování dat. Poskytují také další nástroje pro vizualizaci a analýzu dat. Data shromážděná pomocí přehledů můžete kombinovat s ostatními daty pomocí základních funkcí monitorování, jako jsou dotazy a výstrahy protokolu.

Monitorování podporuje několik metod shromažďování dat monitorování nebo správy z Azure nebo externích prostředků. Pak můžete extrahovat a přepřesměrovávat data z úložiště metriky nebo protokolů do vašich nástrojů pro ITSM nebo monitorování. Můžete také provádět úlohy správy pomocí REST API Azure Monitor.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Monitorování modelů nasazení v cloudu](./cloud-models-monitor-overview.md)
