---
title: Průvodce monitorováním cloudu – upozorňování
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vyberte, kdy použít Azure Monitor nebo System Center Operations Manager v Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 554bfdaf0a21fac50cafe9c510c4fd83c6702b81
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221379"
---
# <a name="cloud-monitoring-guide-alerting"></a>Průvodce monitorováním cloudu: Zobrazení výstrah

Pro roky si IT organizace struggled, aby pomohly bojovat proti únavě výstrahám vytvořeným nástroji pro monitorování nasazenými v podniku. Řada systémů generuje velmi velký objem výstrah, často se považují za nevýznamné, zatímco ostatní jsou relevantní, ale jsou buď předané, nebo ignorované. V důsledku toho struggled IT a vývojářské operace, aby splnily kvalitu na úrovni služby, kterou přislíbili interním nebo externím zákazníkům. Je důležité pochopit stav vaší infrastruktury a aplikací, aby se zajistila spolehlivost. Je potřeba identifikovat příčiny rychle, minimalizovat snížení úrovně služeb a přerušení nebo snížit dopad nebo snížit počet incidentů.

## <a name="successful-alerting-strategy"></a>Strategii úspěšného upozorňování

*Nemůžete opravit, co nevíte, že je přerušeno.*

Upozornění na to, co je důležité. Je nepřipnutý shromažďováním a měřením správných metrik a protokolů. Budete také potřebovat monitorovací nástroj schopný ukládat, agregovat, vizualizovat, analyzovat a iniciovat automatizovanou odezvu při splnění podmínek. Zlepšení pozorovatele služeb a aplikací je možné provést pouze v případě, že plně rozumíte jejímu složení. Toto složení namapujete na detailní konfiguraci monitorování, která se má použít pro monitorovací platformu. To zahrnuje předvídatelné stavy selhání (příznaky, které nejsou příčinou selhání), které mají smysl na upozornění.

Vezměte v úvahu následující principy, které určují, jestli je příznakem vhodným kandidátem na výstrahy:

- **Záleží na tom?** Je problém příznaky skutečným problémem nebo problémem, který má vliv na celkový stav aplikace? Máte třeba na starosti, jestli je využití procesoru v prostředku vysoké? Nebo že konkrétní dotaz SQL běžící na instanci služby SQL Database na tomto prostředku spotřebovává vysoké využití procesoru v případě trvalého období? Vzhledem k tomu, že je stav využití procesoru skutečným problémem, měli byste na něj upozornit. Nemusíte ale informovat tým, protože neodkazuje na to, co způsobuje podmínku na prvním místě. Upozorňování a upozorňování na problém s využitím procesu dotazu SQL je relevantní i možné jednat.
- **Je to naléhavé?** Je problém skutečný a potřebuje naléhavou pozornost? V takovém případě by měl zodpovědný tým okamžitě sdělit.
- **Ovlivnili vaši zákazníci?** Jsou uživatelé služby nebo aplikace v důsledku tohoto problému ovlivněni?
- **Byly ovlivněny jiné závislé systémy?** Existují výstrahy ze závislostí, které se vzájemně souvisejí a které je možné sladit, aby se předešlo tomu, že se na stejný problém neupozorní všechny týmy?

Tyto otázky si položte při počátečním vývoji konfigurace monitorování. Otestujte a ověřte předpoklady v nevýrobním prostředí a pak je nasaďte do produkčního prostředí. Konfigurace monitorování jsou odvozeny ze známých režimů selhání, výsledků testů simulovaných selhání a zkušeností z různých členů týmu.

Po vydání konfigurace monitorování se můžete dozvědět spoustu toho, co funguje a co není. Vezměte v úvahu vysoký objem výstrah, problémy nezjištěné monitorováním, ale s upozorněním koncovými uživateli a jaké byly osvědčené akce, které se mají v rámci tohoto vyhodnocení použít. Identifikujte změny, které se implementují pro zlepšení doručování služeb, v rámci průběžného nepřetržitého procesu zlepšování monitorování. Nejedná se jenom o vyhodnocování šumu a upozornění na nepoužívané výstrahy, ale také efektivitu toho, jak úlohu sledujete. Jedná se o efektivitu zásad, procesů a celkové jazykové verze, abyste zjistili, jestli vylepšujete.

System Center Operations Manager i Azure Monitor podporují výstrahy na základě statických nebo dokonce nedynamických prahových hodnot a akcí, které jsou nad nimi nastavované. Mezi příklady patří upozornění pro e-maily, SMS a hlasová volání pro jednoduchá oznámení. Obě tyto služby také podporují integraci ITSM, automatizaci vytváření záznamů incidentů a eskalaci do správného týmu podpory nebo jakéhokoli jiného systému pro správu výstrah pomocí Webhooku.

Pokud je to možné, můžete k automatizaci akcí obnovení použít kteroukoli z několika služeb. Mezi ně patří System Center Orchestrator, Azure Automation, Azure Logic Apps nebo automatické škálování v případě elastických úloh. I když je oznamování odpovědným týmům nejběžnějším opatřením pro upozorňování, může být vhodné provést i automatické opravné akce. To může usnadnit zjednodušení celého procesu správy incidentů. Automatizace těchto úloh obnovení může také snížit riziko lidské chyby.

## <a name="azure-monitor-alerting"></a>Azure Monitor upozorňování

Pokud používáte výhradně Azure Monitor, platí následující doprovodné materiály. Při zvažování rychlosti, nákladů a objemu úložiště v Azure Monitor postupujte podle těchto pokynů.

Existují šest úložišť, která ukládají data monitorování v závislosti na používané funkci a konfiguraci.

- **Databáze metrik Azure Monitor.** Databáze časových řad používaná primárně pro Azure Monitor metriky platforem, ale má také Application Insights zrcadlená data metriky. Informace, které vstupují do této databáze, mají nejrychlejší dobu upozornění.

- **Úložiště protokolů Application Insights.** Databáze, která ukládá většinu Application Insights telemetrie do formuláře protokolu.

- **Úložiště protokolů Azure Monitor.** Primární úložiště pro data protokolu Azure. Další nástroje můžou do nich směrovat data a analyzovat je v Azure Monitor protokoly. Dotazy na výstrahy protokolu mají vyšší latenci kvůli ingestování a indexování. Tato latence je všeobecně 5-10 minut, ale může být za určitých podmínek vyšší.

- **Úložiště protokolu aktivit.** Používá se pro všechny události protokolu aktivit a stavu služby. Je možné použít vyhrazené upozorňování. Obsahuje události na úrovni předplatného, ke kterým dochází u objektů ve vašem předplatném, jak je vidět z vnějšku těchto objektů. Například když je zásada nastavená nebo je prostředek k dispozici nebo je odstraněný.

- **Azure Storage.** Úložiště pro obecné účely, které podporuje Azure Diagnostics a další nástroje pro monitorování. Je to cenová možnost pro dlouhodobé uchovávání telemetrie monitorování. U dat uložených v této službě se nepodporuje upozorňování.

- **Event Hubs.** Obecně se používá ke streamování dat do místních nebo ITSM nástrojů pro monitorování nebo pro jiné partnery.

Existují čtyři typy výstrah v Azure Monitor, které jsou spojené s úložištěm, ve kterém jsou uložená data.

- [Výstraha metriky](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric). Výstrahy na data v databázi Azure Monitorch metrik. K výstrahám dochází, když monitorovaná hodnota překračuje prahovou hodnotu definovanou uživatelem a potom znovu, až se vrátí do stavu "normální".

- [Výstraha dotazu protokolu](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query). K dispozici pro výstrahy týkající se obsahu v Application Insights nebo v úložištích protokolů Azure. Může také upozorňovat na závislosti na dotazech mezi jednotlivými pracovními prostory.

- [Výstraha protokolu aktivit](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log). Výstrahy na položky v úložišti protokolu aktivit s výjimkou Service Healthch dat.

- [Výstraha Service Health](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications?toc=%2fazure%2fservice-health%2ftoc.json). Speciální typ výstrahy, a to jenom pro Service Health problémů přicházejících z úložiště protokolu aktivit.

### <a name="alerting-through-partner-tools"></a>Upozorňování prostřednictvím partnerských nástrojů

Pokud používáte externí řešení pro upozorňování, pak můžete směrovat co nejvíc jako prostřednictvím Azure Event Hubs, protože to je nejrychlejší cesta z Azure Monitor. Budete muset zaplatit za příjem do centra událostí. Pokud jsou náklady problém a rychlost, můžete Azure Storage použít jako levnější alternativu. Ujistěte se, že vaše monitorování nebo ITSM nástroje mohou číst Azure Storage k extrakci dat.

Azure Monitor zahrnují podporu pro integraci s dalšími monitorovacími platformami a ITSM software, jako je ServiceNow. Můžete použít upozorňování Azure a pořád aktivovat akce mimo Azure, jak to vyžaduje Správa incidentů nebo DevOps proces. Pokud chcete upozornit Azure Monitor a automatizovat odpověď, můžete spustit automatizované akce pomocí Azure Functions, Azure Logic Apps nebo Azure Automation na základě vašeho scénáře a požadavků.

### <a name="specialized-azure-monitoring-offerings"></a>Specializované nabídky monitorování Azure

[Řešení pro správu](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) většinou ukládají svá data v úložišti protokolů Azure. Tyto dvě výjimky jsou Azure Monitor pro virtuální počítače a Azure Monitor pro kontejnery. Následující tabulka popisuje možnosti upozorňování na základě konkrétního datového typu a místa, kde je uložený.

Řešení| Datový typ | Chování výstrahy
:---|:---|:---
Azure Monitor pro kontejnery | Vypočtená Průměrná data o výkonu z uzlů a lusky se zapisují do úložiště metrik. | Upozornění na metriku můžete vytvořit, pokud chcete být upozorňováni na základě variace měřeného výkonu využití agregovaného v časovém intervalu.
|| Vypočtená údaje o výkonu, které používají percentily z uzlů, řadičů, kontejnerů a lusků, se zapisují do úložiště Logs. Do úložiště protokolů se zapisují také protokoly kontejnerů a informace o inventáři. | Pokud chcete být upozorňováni na základě variace měřeného využití z clusterů a kontejnerů, vytvořte výstrahy dotazování protokolu. Výstrahy dotazů na protokol se dají nakonfigurovat taky na základě počtu fází a počtu uzlů stavu.
Azure Monitor pro virtuální počítače | Kritéria stavu jsou metriky zapsané do úložiště metrik. | Výstrahy jsou generovány při změně stavu z stavu v pořádku do stavu není v pořádku. Podporuje jenom skupiny akcí nakonfigurované pro odesílání oznámení SMS nebo e-mailem.
|| Data protokolu o namapování a data protokolů výkonu hostovaného operačního systému se zapisují do úložiště Logs. | Vytváření výstrah dotazů protokolu.

### <a name="fastest-speed-driven-by-cost"></a>Nejrychlejší rychlost řízená náklady

Latence je jedním z nejdůležitějších rozhodnutí při řízení výstrah a rychlé řešení problémů, které mají vliv na vaši službu. Pokud budete během pěti minut vyžadovat upozorňování téměř v reálném čase, vyhodnoťte je jako první, pokud máte nebo můžete získat výstrahy na telemetrii, kde je ve výchozím nastavení uložený. Obecně platí, že tato strategie je zároveň možnost nejlevnější, protože nástroj, který používáte, již do tohoto umístění odesílá svá data.

K tomuto pravidlu se říká několik důležitých poznámek pod čarou.

**Telemetrie hostovaného operačního systému** má několik cest, které se mají do systému dostat.

- Nejrychlejší způsob, jak upozornit na tato data, je importovat jako vlastní metriky. Použijte k tomu rozšíření Azure Diagnostics a pak použijte upozornění na metriku. Vlastní metriky jsou ale momentálně ve verzi Preview a jsou [dražší než jiné možnosti](https://azure.microsoft.com/pricing/details/monitor).

- Nejlevnější, ale nejpomalejší metodou je odeslat je do úložiště Azure logs Kusto. Spuštění agenta Log Analytics na virtuálním počítači je nejlepší způsob, jak do tohoto úložiště získat veškerou metriku a data protokolu hostovaného operačního systému.

- Do obou úložišť můžete posílat tak, že na stejném virtuálním počítači spustíte rozšíření i agenta. Pak můžete rychle vygenerovat výstrahu, ale také použít data hostovaného operačního systému jako součást složitějších hledání v kombinaci s jinou telemetrie.

**Import dat z místního prostředí.** Pokud se snažíte dotazovat a monitorovat mezi počítači, které běží v Azure a v místním prostředí, můžete k shromažďování dat hostovaného operačního systému použít agenta Log Analytics. Pak můžete k metrikám využít funkci s názvem [logs](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) a zjednodušit tyto metriky do úložiště metrik. Tato metoda obchází část procesu příjmu do úložiště protokolů Azure a proto je v databázi metrik k dispozici dříve.

### <a name="minimize-alerts"></a>Minimalizovat výstrahy

Pokud použijete řešení jako Azure Monitor pro virtuální počítače a vyhledáte výchozí kritéria stavu, která monitorují přijatelné nároky na výkon, nevytvářejte v závislosti na stejných čítačích výkonu překrývající se výstrahy nebo dotazování protokolu metriky.

Pokud nepoužíváte Azure Monitor pro virtuální počítače, prozkoumejte následující funkce, které vám usnadní vytváření výstrah a správu oznámení.  

> [!NOTE]
> Tyto funkce se vztahují jenom na výstrahy metriky. To znamená, že výstrahy na základě dat odesílaných do databáze metrik Azure Monitor. Nevztahují se na další typy výstrah. Jak už bylo zmíněno dříve, primárním cílem výstrah metriky je rychlost. Pokud se při získání výstrahy za méně než 5 minut nejedná o primární obavy, můžete místo toho použít výstrahu dotazu protokolu.

- [Dynamické prahové hodnoty](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds). Dynamické prahové hodnoty prohledají aktivitu prostředku za časové období a vytvoří horní a dolní prahové hodnoty normální chování. Když je monitorovaná metrika mimo tyto prahové hodnoty, zobrazí se upozornění.

- [Nepodepsané výstrahy](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts). Můžete vytvořit upozornění metriky, které používá kombinaci dvou různých vstupů ze dvou různých typů prostředků. Pokud třeba chcete vyvolat výstrahu, když je procesor virtuálního počítače větší než 90%, a počet zpráv v určité frontě Azure Service Bus zaznamenání, že virtuální počítač překročí určitou hodnotu, můžete to udělat bez vytvoření dotazu protokolu. To funguje jenom pro dva signály. Pokud máte složitější dotaz, zadáte data metriky do úložiště protokolu Azure Monitor a použijete dotaz protokolu.

- [Výstrahy](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts)s více prostředky Azure Monitor umožňuje jedno pravidlo výstrahy metriky, které se vztahuje na všechny prostředky virtuálních počítačů. Tato funkce vám může ušetřit čas, protože nemusíte vytvářet jednotlivé výstrahy pro každý virtuální počítač. Ceny za tento typ upozornění jsou stejné. Pokud jste vytvořili 50 upozornění pro monitorování využití procesoru pro virtuální počítače 50 nebo 1 výstrahu, která monitoruje využití procesoru u všech virtuálních počítačů 50, náklady budou stejné. Tyto typy výstrah můžete použít i v kombinaci s dynamickými prahovými hodnotami.

Pomocí těchto funkcí můžete ušetřit čas tím, že minimalizujete oznámení o výstrahách a správu základních výstrah.

### <a name="alerts-limitations"></a>Omezení výstrah

Nezapomeňte si poznamenat [omezení](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) počtu výstrah, která je možné vytvořit. Některá omezení (ale ne všechny) je možné zvýšit voláním podpory.

### <a name="best-query-experience"></a>Nejlepší možnosti dotazování

Pokud hledáte trendy pro všechna vaše data, je vhodné importovat všechna data do protokolů Azure, pokud už nejsou v Application Insights. Můžete vytvářet dotazy napříč oběma pracovními prostory, takže nemusíte přesouvat data mezi nimi. Do pracovního prostoru Log Analytics můžete také importovat protokol aktivit a data Service Health. Platíte za tato ingestování a ukládání, ale získáte všechna data na jednom místě pro účely analýzy a dotazování. Díky tomu máte možnost vytvářet na nich složité podmínky dotazování a upozornění.
