---
title: Průvodce monitorováním cloudu – přehled platforem monitorování
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vyberte, kdy použít Azure Monitor nebo System Center Operations Manager v Microsoft Azure
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 33d9647a0804859a611d45e130c753cab89a6ef6
ms.sourcegitcommit: b94e9be9e43214d954ff8a7b6fdf96b84cbac55a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2019
ms.locfileid: "70863638"
---
# <a name="cloud-monitoring-guide-overview-of-our-monitoring-platforms"></a>Průvodce monitorováním cloudu: Přehled našich monitorovacích platforem

Společnost Microsoft poskytuje řadu možností monitorování ze dvou produktů: System Center Operations Manager, která byla navržená místně a pak se rozšířila do cloudu a Azure Monitor, která byla navržena pro Cloud, ale může také monitorovat místní systémy. Tyto dvě nabídky poskytují základní monitorovací služby, jako jsou například výstrahy, sledování doby provozu služby, monitorování stavu aplikace a infrastruktury, diagnostika a analýza.

Mnoho organizací si přechodu nejnovější postupy pro DevOps flexibilitu a cloudové inovace pro správu prostředí heterogenní. I když jsou ještě obavy o jejich schopnost dělat vhodná a odpovědná rozhodnutí týkající se monitorování těchto úloh.

Tento článek poskytuje podrobný přehled našich monitorovacích platforem, které vám pomůžou pochopit, jak poskytují základní monitorovací funkce.

## <a name="story-of-system-center-operations-manager"></a>Příběh System Center Operations Manager

V 2000 jsme do pole Operations Management zadali Microsoft Operations Manager (MOM) 2000. V 2007 jsme zavedli novou inženýrskou verzi produktu s názvem System Center Operations Manager. Přesunuli jsme se nad rámec jednoduchého monitorování Windows serveru a soustřeďte se na robustní, komplexní monitorování služeb a aplikací, včetně platforem heterogenní, síťových zařízení a dalších závislostí aplikací nebo služeb. Je to vytvořená platforma pro monitorování na podnikové úrovni pro místní prostředí ve stejné třídě jako IBM Tivoli nebo HP Operations Manager v oboru. Zvětšila se podpora monitorování výpočetních prostředků a prostředků platforem, které běží v Azure, Amazon Web Services (AWS) a dalších poskytovatelích cloudu.

## <a name="story-of-azure-monitor"></a>Příběh Azure Monitor

Po vydání Azure v 2010 byl k dispozici monitorování cloudových služeb s agentem Azure Diagnostics, který poskytuje způsob shromažďování diagnostických dat z prostředků Azure. Tato funkce byla považována za obecný nástroj pro monitorování, nikoli na podnikovou platformu pro monitorování.  

Application Insights bylo zavedeno k posunu se změnami v odvětví, kde bylo rostoucí šíření cloudových, mobilních a IoT zařízení a zavedení postupů DevOps. Z monitorování výkonu aplikací v Operations Manager ke službě v Azure, kde poskytuje bohatě sledující webové aplikace napsané v různých jazycích. V 2015 byla oznámena verze Preview Application Insights pro sadu Visual Studio a později byla známa jako Application Insights. Shromažďuje podrobnosti o výkonu aplikace, požadavcích a výjimkách a trasováních.

V 2015 se služba Azure Operational Insights všeobecně zpřístupnila. Dodávala službu Analysis Services Log Analytics, která shromáždila a prohledala data z počítačů v Azure, v Prem nebo v jiných cloudových prostředích a připojená k System Center Operations Manager. Byly nabídnuty sady Intelligence, které dodávaly různé konfigurace pro správu a monitorování, které obsahují kolekci dotazů a analytické logiky, vizualizace a pravidla shromažďování dat pro takové scénáře jako audit zabezpečení, stav posouzení a správa výstrah.  Novější verze Azure Operational Insights se staly známými jako Log Analytics.  

V 2016 byl ve verzi Preview Azure Monitor oznámena Ignite. Poskytovala společné rozhraní pro shromažďování metrik platforem, protokoly diagnostiky prostředků a události protokolu aktivit na úrovni předplatného ze všech služeb Azure, které začali používat rozhraní. Dříve měla každá služba Azure vlastní metodu monitorování.

Na konferenci Microsoft Ignite v 2018 jsme oznámili, že Azure Monitor značka rozbalená tak, aby zahrnovala několik různých služeb, které byly původně vyvinuty s nezávislou funkcí:

- Původní funkce **Azure monitor** shromažďování metrik platforem, protokolů diagnostiky prostředků a protokolů aktivit jenom pro prostředky platformy Azure.
- **Application Insights** pro monitorování aplikací.
- **Log Analytics** jako primární umístění pro shromažďování a analýzu dat protokolu.
- Nová **sjednocená služba upozorňování** , která spojuje mechanismy výstrah od každé z dalších výše zmíněných služeb.  
- **Azure Network Watcher** k monitorování, diagnostice a zobrazování metrik pro prostředky ve službě Azure Virtual Network.

## <a name="the-story-of-operations-management-suite-oms"></a>Scénář Operations Management Suite (OMS)

Od 2015 do dubna 2018 byla Operations Management Suite (OMS) sdružením následujících služeb správy Azure pro účely licencování:

- Application Insights
- Azure Automation
- Azure Backup
- Operational Insights (později Log Analytics znovu značka)
- Site Recovery

Funkce služeb, které byly součástí OMS, se nezměnily, když OMS byla zastavena, byly v rámci Azure Monitor znovu zarovnány.

## <a name="infrastructure-requirements"></a>Požadavky na infrastrukturu

### <a name="operations-manager"></a>Operations Manager

Operations Manager vyžaduje významnou infrastrukturu a údržbu pro podporu skupiny pro správu, což je základní funkční jednotka. Minimálně skupina pro správu se skládá z jednoho nebo více serverů pro správu, SQL Server, hostování provozní databáze datového skladu a sestav a agentů. Složitost návrhu skupiny pro správu závisí na několika faktorech, jako je například rozsah úloh, které se mají monitorovat, a kolik zařízení nebo počítačů podporují úlohy. Pokud požadujete vysokou dostupnost a odolnost lokality, jak často se jedná o podnikové platformy pro monitorování, požadavky na infrastrukturu a přidružená údržba se můžou výrazně zvýšit.

![Diagram Operations Manager skupiny pro správu](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor je služba SaaS, kde veškerá infrastruktura, která ji podporuje, běží v Azure a spravuje ji Microsoft. Je navržená tak, aby prováděla monitorování, analýzu a diagnostiku ve velkém měřítku a je dostupná ve všech národních cloudech. Základní části infrastruktury (sběrače, metriky a úložiště protokolů a analýza), které jsou nezbytné pro podporu Azure Monitor, jsou spravovány společností Microsoft.  

![Diagram Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Shromažďování dat

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agenti

Operations Manager pouze shromažďuje data přímo z agentů nainstalovaných v [počítačích se systémem Windows](https://docs.microsoft.com//system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent). Může přijímat data z Operations Manager SDK, ale obvykle se používá pro partnery, kteří rozšiřují produkt s vlastními aplikacemi, a ne pro shromažďování dat monitorování. Může shromažďovat data z jiných zdrojů, jako jsou například [počítače se systémem Linux](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) a síťová zařízení, pomocí speciálních modulů, které jsou spouštěny v agentovi Windows vzdáleně přístup k těmto ostatním zařízením.

![Diagram agenta Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

Agent Operations Manager může shromažďovat data z několika zdrojů dat v místním počítači, například protokol událostí, vlastní protokoly a čítače výkonu. Může také spouštět skripty, které mohou shromažďovat data z místního počítače nebo z externích zdrojů. Můžete psát vlastní skripty pro shromažďování dat, která nelze shromažďovat jiným způsobem, nebo z nejrůznějších vzdálených zařízení, která nelze jinak monitorovat.

#### <a name="management-packs"></a>Sady Management Pack

Operations Manager provádí všechna monitorování pomocí pracovních postupů (pravidla, monitorování a zjišťování objektů). Tyto jsou zabaleny dohromady do [Management Pack](https://docs.microsoft.com/system-center/scom/manage-overview-management-pack?view=sc-om-2019)a nasazeny do agentů. Sady Management Pack jsou k dispozici pro různé produkty a služby, které obsahují předdefinovaná pravidla a monitory. Můžete také vytvořit vlastní Management Pack pro vlastní aplikace a vlastní scénáře.

#### <a name="monitoring-configuration"></a>Konfigurace monitorování

Sady Management Pack mohou obsahovat stovky pravidel, monitorování a pravidla zjišťování objektů. Agent spouští všechna tato nastavení monitorování ze všech použitých sad Management Pack, které jsou určeny podle pravidel zjišťování. Každá instance každého nastavení monitorování se spouští nezávisle a funguje okamžitě s daty, která shromažďuje. To je způsob, jakým Operations Manager může dosáhnout upozorňování téměř v reálném čase a aktuálního stavu monitorovaných prostředků.

Monitor může například vzorkovat čítač výkonu každých pár minut. Pokud tento čítač překročí prahovou hodnotu, okamžitě nastaví stav cílového objektu, který okamžitě aktivuje výstrahu ve skupině pro správu. Naplánované pravidlo může být sledováno pro konkrétní událost, která má být vytvořena, a okamžitě vyvolat výstrahu, pokud je tato událost vytvořena v místním protokolu událostí.

Vzhledem k tomu, že jsou tato nastavení monitorování izolovaná od sebe a pracují z jednotlivých zdrojů dat, Operations Manager mají problémy korelující data mezi více zdroji. Je také obtížné reagovat na data po shromáždění. Můžete spouštět pracovní postupy, které přistupují k databázi Operations Manager, ale tento scénář není běžný a obvykle se používá pro omezený počet pracovních postupů pro zvláštní účely.

![Diagram Operations Manager skupiny pro správu](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Zdroje dat

Azure Monitor shromažďuje data z nejrůznějších zdrojů, včetně prostředků infrastruktury Azure a platforem, agentů v počítačích se systémem Windows a Linux a monitorování dat shromažďovaných ve službě Azure Storage. Libovolný klient REST může zapisovat data protokolu do Azure Monitor pomocí rozhraní API a můžete definovat vlastní metriky pro webové aplikace. Některá data metriky je možné směrovat do různých umístění v závislosti na jejich využití. Můžete například použít data pro rychlé upozorňování nebo pro dlouhodobé analýzy trendů ve spojení s dalšími daty protokolů.

#### <a name="monitoring-solutions-and-insights"></a>Monitorování řešení a přehledů

Řešení monitorování používají platformu log v Azure Monitor k zajištění monitorování konkrétní aplikace nebo služby. Obvykle definují shromažďování dat od agentů nebo ze služeb Azure a poskytují dotazy a zobrazení protokolů k analýze těchto dat. Obvykle neposkytují pravidla výstrah, což znamená, že musíte definovat vlastní kritéria upozornění na základě shromážděných dat.

Přehledy, jako je například Azure Monitor pro kontejnery a Azure Monitor pro virtuální počítače, využívají platformu Azure Monitor protokoly a metriky, které poskytují přizpůsobené možnosti monitorování pro aplikaci nebo službu v Azure Portal. Kromě přizpůsobené analýzy shromážděných dat můžou poskytovat podmínky monitorování a upozorňování na stav.

#### <a name="monitoring-configuration"></a>Konfigurace monitorování

Azure Monitor odděluje shromažďování dat od akcí pořízených s těmito daty, která podporuje distribuované mikroslužby v cloudovém prostředí. Slučuje data z více zdrojů do Common data Platform a poskytuje možnosti analýzy, vizualizace a upozorňování na základě shromážděných dat.

Všechna data shromážděná pomocí Azure Monitor jsou uložená jako protokoly nebo metriky a různé funkce monitorování spoléhají na jednu z nich. Metriky obsahují číselné hodnoty v časových řadách, které jsou vhodné pro výstrahy téměř v reálném čase a rychlé zjišťování problémů. Protokoly obsahují text nebo číselná data a podporují ho výkonný dotazovací jazyk, který je vhodný zejména pro provádění složitých analýz.

Vzhledem k tomu, že monitorování odděluje shromažďování dat od akcí proti těmto datům, nemusí být schopné v mnoha případech poskytovat výstrahy téměř v reálném čase. Pro upozornění na data protokolu se dotazy spouštějí podle opakujícího se plánu definovaného v upozornění. Díky tomuto chování může Azure Monitor snadno korelovat data ze všech monitorovaných zdrojů a interaktivně analyzovat data různými způsoby. To je užitečné hlavně při provádění analýz hlavní příčiny a určení, kde k problému může dojít.

## <a name="health-monitoring"></a>Monitorování stavu

### <a name="operations-manager"></a>Operations Manager

Sady Management Pack v Operations Manager zahrnují model služby, který popisuje komponenty monitorované aplikace a jejich vztah. Monitory identifikují aktuální stav každé součásti na základě dat a skriptů v agentovi. Stavy jsou shrnuté tak, abyste se rychle zobrazovaly souhrnnému stavu monitorovaných počítačů a aplikací.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor neposkytuje uživatelsky definované metody implementace modelu služby nebo monitorování, které označují aktuální stav všech součástí služby. Vzhledem k tomu, že řešení monitorování jsou založená na standardních funkcích Azure Monitor, neposkytují monitorování na úrovni stavu. Následující funkce Azure Monitor můžou být užitečné:

- **Application Insights** vytvoří složenou mapu vaší webové aplikace a poskytne stav pro každou součást aplikace nebo závislost. Patří sem stav výstrah a přechod k podrobnostem pro podrobnější diagnostiku vaší aplikace.

- **Azure monitor pro virtuální počítače** poskytuje prostředí pro monitorování stavu pro hostované virtuální počítače Azure, podobně jako Operations Manager při monitorování virtuálních počítačů se systémem Windows a Linux. Vyhodnotí stav klíčových komponent operačního systému z perspektivy dostupnosti a výkonu a určí aktuální stav. Když zjistí, že virtuální počítač hosta má trvalé využívání prostředků, kapacitu místa na disku nebo problém související s funkcí základního operačního systému, vygeneruje výstrahu, která tento stav zaznamená do vaší pozornosti.

- **Azure monitor pro kontejnery** monitorují výkon a stav služeb Azure Kubernetes nebo Azure Container Instances. Z řadiče, uzly a kontejnerů, které jsou k dispozici v Kubernetes prostřednictvím rozhraní API metrik shromažďuje metriky paměti a procesoru. Také shromažďuje protokoly kontejnerů a data inventáře o kontejnerech a jejich obrázcích. Předem definovaná kritéria stavu na základě shromážděných údajů o výkonu vám pomůžou zjistit, jestli došlo k potížím s kritickým prostředkem nebo kapacitou. Můžete také pochopit celkový výkon nebo výkon konkrétního typu objektu Kubernetes (pod, uzlem, kontrolérem nebo kontejnerem).

## <a name="analyzing-data"></a>Analýza dat

### <a name="operations-manager"></a>Operations Manager

Operations Manager poskytuje čtyři základní způsoby, jak analyzovat data po shromáždění.

- Pomocí **Průzkumník stavů**zjistíte, které monitory identifikují problém se stavem, a přečtěte si informace o monitorování a možných příčinách pro akce, které s ním souvisejí.

- **Zobrazení** jsou předdefinované vizualizace shromážděných dat, jako je například graf dat o výkonu nebo seznam monitorovaných komponent a jejich aktuální stav. Zobrazení diagramu vizuálně prezentují model služby aplikace.

- **Sestavy** umožňují shrnout historická data uložená v datovém skladu Operations Manager. Můžete přizpůsobit data, která jsou založená na zobrazeních a sestavách. Neexistuje ale žádná funkce, která umožňuje složitou nebo interaktivní analýzu shromážděných dat.

- **Operations Manager příkazové prostředí**, které rozšiřuje prostředí Windows PowerShell o další sadu rutin, může dotazovat a vizualizovat shromážděná data. To zahrnuje grafy a další vizualizace, nativně pomocí prostředí PowerShell nebo Operations Manager webové konzole založené na jazyce HTML.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor má výkonný analytický modul, který umožňuje interaktivně pracovat s daty protokolů a kombinovat je s dalšími daty monitorování pro vývoj a další analýzu dat. Zobrazení a řídicí panely umožňují vizualizovat data dotazů různými způsoby z Azure Portal a importovat je do Power BI. Mezi řešení monitorování patří dotazy a zobrazení, která prezentují data, která shromažďuje. Přehledy, jako jsou Application Insights, Azure Monitor pro virtuální počítače a Azure Monitor pro kontejnery, zahrnují přizpůsobené vizualizace pro podporu scénářů interaktivního monitorování.

## <a name="alerting"></a>Zobrazení výstrah

### <a name="operations-manager"></a>Operations Manager

Operations Manager vytváří výstrahy v reakci na předdefinované události, při splnění prahové hodnoty výkonu a při změně stavu monitorované součásti. Zahrnuje úplnou správu výstrah, což vám umožní nastavit jejich rozlišení a přiřadit je různým operátorům nebo systémovým technikům. Můžete nastavit pravidla oznámení, která určují, která upozornění budou odesílat proaktivní oznámení.

Sady Management Pack zahrnují různá předdefinovaná pravidla výstrah pro různé kritické podmínky v monitorovaných aplikacích. Tato pravidla můžete vyladit nebo vytvořit vlastní pravidla pro konkrétní požadavky vašeho prostředí.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor umožňuje vytvářet výstrahy na základě metriky překračující prahovou hodnotu nebo na základě plánovaného výsledku dotazu. Výstrahy založené na metrikách můžou dosáhnout téměř reálných výsledků, zatímco plánované dotazy mají delší dobu odezvy v závislosti na rychlosti příjmu dat a indexování. Místo omezení na konkrétního agenta, výstrahy dotazování protokolu v Azure Monitor umožňují analyzovat data napříč všemi daty uloženými ve více pracovních prostorech. Tyto výstrahy také zahrnují data z konkrétní aplikace Application Insights pomocí dotazu mezi pracovními prostory.

I když monitorovací řešení můžou zahrnovat pravidla výstrah, obvykle je vytvoříte na základě vašich požadavků.

## <a name="workflows"></a>Workflows

### <a name="operations-manager"></a>Operations Manager

Sady Management Pack v Operations Manager obsahují stovky individuálních pracovních postupů a určují, jaká data se mají shromažďovat a jakou akci mají s těmito daty pracovat. Pravidlo může například vzorkovat čítač výkonu každých pár minut a uložit jeho výsledky k analýze. Monitorování může vzorkovat stejný čítač výkonu a porovnat jeho hodnotu s prahovou hodnotou, aby bylo možné zjistit stav monitorovaného objektu. Jiné pravidlo může spustit skript pro shromáždění a analýzu dat v počítači agenta a vyvolat výstrahu, pokud vrátí určitou hodnotu.

Pracovní postupy v Operations Manager jsou vzájemně nezávislé, takže analýza napříč více monitorovanými objekty je obtížná. Tyto scénáře monitorování musí být založené na datech po shromáždění, což je možné, ale může být obtížné a není běžné.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor odděluje shromažďování dat z akcí a analýz z těchto dat. Agenti a další zdroje dat zapisují data protokolu do pracovního prostoru Log Analytics a data metriky do databáze metriky bez jakékoli analýzy těchto dat nebo znalosti toho, jak je možné je použít. Monitorování provádí výstrahy a další akce z uložených dat, což umožňuje provádět analýzu napříč daty ze všech zdrojů.

## <a name="extending-base-platform"></a>Rozšiřování základní platformy

### <a name="operations-manager"></a>Operations Manager

Operations Manager implementuje veškerou logiku monitorování v Management Pack, kterou buď vytvoříte sami, nebo ji získáte od nás nebo od partnera. Když nainstalujete Management Pack, automaticky zjistí komponenty aplikace nebo služby na různých agentech a nasadí vhodná pravidla a monitory. Management Pack obsahuje definice stavu, pravidla výstrah, pravidla výkonu a shromažďování událostí a zobrazení, aby bylo možné zajistit kompletní monitorování, které podporuje službu infrastruktury nebo aplikaci.

Sada Operations Manager SDK umožňuje Operations Manager integraci s monitorovacími platformami třetích stran nebo ITSM softwarem. Sada SDK je také používána některými sadami partnerských sad pro podporu monitorování síťových zařízení a přináší vlastní prezentační prostředí, jako je například druhý řídicí panel HTML5 nebo integrace s systém Microsoft Office Visio.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor shromažďuje metriky a protokoly z prostředků Azure, a to s nízkou konfigurací. Řešení monitorování přidávají logiku pro monitorování aplikace nebo služby, ale stále pracují v rámci standardních dotazů protokolů a zobrazení v monitorování. Přehledy, jako jsou Application Insights a Azure Monitor pro virtuální počítače, využívají platformu monitorování pro shromažďování a zpracování dat a také poskytují další nástroje pro vizualizaci a analýzu dat. Data shromážděná pomocí přehledů můžete kombinovat s ostatními daty pomocí základních funkcí monitorování, jako jsou dotazy a výstrahy protokolu.

Monitorování podporuje několik metod shromažďování dat monitorování nebo správy z Azure nebo externích prostředků. Pak můžete extrahovat a přepřesměrovávat data z úložiště metriky nebo protokolů do nástrojů pro ITSM nebo monitorování nebo provádět úlohy správy pomocí REST API Azure Monitor.

## <a name="next-steps"></a>Další postup

> [!div class="nextstepaction"]
> [Monitorování modelů nasazení v cloudu](./cloud-models-monitor-overview.md)
