---
title: 'Průvodce monitorováním cloudu: upozorňování'
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak určit, kdy použít Azure Monitor nebo System Center Operations Manager v Microsoft Azure.
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: c6f48ae433746906d64023bd72f34c21a3163373
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79091291"
---
# <a name="cloud-monitoring-guide-alerting"></a>Průvodce monitorováním cloudu: upozorňování

V letech se organizace IT struggled, aby pomohly potírat únavu výstrah, kterou vytvořily nástroje pro monitorování nasazené v podniku. Řada systémů generuje velmi velký objem výstrah, často se považují za nevýznamné, zatímco jiné výstrahy jsou relevantní, ale jsou buď překládány nebo ignorovány. V důsledku toho struggled IT a vývojářské operace, aby splnily kvalitu na úrovni služby, kterou přislíbili interním nebo externím zákazníkům. Aby se zajistila spolehlivost, je důležité pochopit stav vaší infrastruktury a aplikací. Chcete-li minimalizovat snížení úrovně služeb a přerušení nebo snížit vliv nebo snížit počet incidentů, je nutné identifikovat příčiny rychle.

## <a name="successful-alerting-strategy"></a>Strategii úspěšného upozorňování

*Nemůžete opravit, co nevíte, že je přerušeno.*

Upozornění na to, co je důležité. Je nepřipnutý shromažďováním a měřením správných metrik a protokolů. Budete také potřebovat monitorovací nástroj schopný ukládat, agregovat, vizualizovat, analyzovat a iniciovat automatizovanou odezvu při splnění podmínek. V případě, že je jejich složení plně srozumitelné, můžete zlepšit promoci své služby a aplikace. Toto složení namapujete na detailní konfiguraci monitorování, která se má použít pro monitorovací platformu. Tato konfigurace zahrnuje předvídatelné stavy selhání (příznaky, nikoli příčinu selhání), které mají smysl na upozornění.

Vezměte v úvahu následující principy, které určují, jestli je příznakem vhodným kandidátem na výstrahy:

- **Záleží na tom?** Je problém příznaky skutečným problémem nebo problémem, který má vliv na celkový stav aplikace? Můžete třeba dbát na to, jestli je využití procesoru u prostředku vysoké? Nebo že konkrétní dotaz SQL běžící na instanci služby SQL Database na tomto prostředku spotřebovává vysoké využití procesoru v případě trvalého období? Vzhledem k tomu, že je stav využití procesoru skutečným problémem, měli byste na něj upozornit. Nemusíte ale informovat tým, protože neodkazuje na to, co způsobuje podmínku na prvním místě. Upozorňování a upozorňování na problém s využitím procesu dotazu SQL je relevantní i možné jednat.
- **Je to naléhavé?** Je problém skutečný a potřebuje naléhavou pozornost? V takovém případě by měl být příslušný tým okamžitě vyrozuměn.
- **Ovlivnili vaši zákazníci?** Jsou uživatelé služby nebo aplikace v důsledku tohoto problému ovlivněni?
- **Byly ovlivněny jiné závislé systémy?** Existují výstrahy ze závislostí, které se vzájemně souvisejí a které je možné sladit, aby se předešlo tomu, že se na stejný problém neupozorní všechny týmy?

Tyto otázky si položte při počátečním vývoji konfigurace monitorování. Otestujte a ověřte předpoklady v nevýrobním prostředí a pak je nasaďte do produkčního prostředí. Konfigurace monitorování jsou odvozeny ze známých režimů selhání, výsledků testů simulovaných selhání a zkušeností z různých členů týmu.

Po vydání konfigurace monitorování se můžete dozvědět spoustu toho, co funguje a co není. Vezměte v úvahu vysoký objem výstrah, problémy nezjištěné monitorováním, ale s upozorněním koncovými uživateli a jaké byly osvědčené akce, které se mají v rámci tohoto vyhodnocení použít. Identifikujte změny, které se implementují pro zlepšení doručování služeb, v rámci průběžného nepřetržitého procesu zlepšování monitorování. Nejedná se jenom o vyhodnocování šumu a upozornění na nepoužívané výstrahy, ale také efektivitu toho, jak úlohu sledujete. Jedná se o efektivitu zásad upozornění, procesů a celkové jazykové verze, abyste zjistili, jestli vylepšujete.

System Center Operations Manager i Azure Monitor podporují výstrahy na základě statických nebo dokonce nedynamických prahových hodnot a akcí, které jsou nad nimi nastavované. Mezi příklady patří upozornění pro e-maily, SMS a hlasová volání pro jednoduchá oznámení. Obě tyto služby také podporují integraci správa IT služeb (ITSM), automatizaci vytváření záznamů incidentů a eskalaci do správného týmu podpory nebo jakýkoli jiný systém pro správu výstrah, který používá Webhook.

Pokud je to možné, můžete k automatizaci akcí obnovení použít kteroukoli z několika služeb. Mezi ně patří System Center Orchestrator, Azure Automation, Azure Logic Apps nebo automatické škálování v případě elastických úloh. I když je oznamování odpovědných týmů nejběžnějším opatřením pro upozorňování, může být vhodné provést i automatické opravné akce. Tato automatizace může přispět k zjednodušení celého procesu správy incidentů. Automatizace těchto úloh obnovení může také snížit riziko lidské chyby.

## <a name="azure-monitor-alerting"></a>Azure Monitor upozorňování

Pokud používáte výhradně Azure Monitor, postupujte podle těchto pokynů, abyste se vybrali jako rychlost, náklady a objem úložiště.

V závislosti na používané funkci a konfiguraci můžete data monitorování ukládat do šesti úložišť:

- **Databáze Azure monitor metrik:** Databáze časových řad používaná primárně pro Azure Monitor metriky platforem, ale má také Application Insights zrcadlená data metriky. Informace, které vstupují do této databáze, mají nejrychlejší dobu upozornění.

- **Úložiště Application Insightsch protokolů:** Databáze, která ukládá většinu Application Insights telemetrie do formuláře protokolu.

- **Úložiště Azure Monitorch protokolů:** Primární úložiště pro data protokolu Azure. Další nástroje můžou do nich směrovat data a analyzovat je v Azure Monitor protokoly. Z důvodu ingestování a indexování mají dotazy protokolu výstrahy vyšší latenci. Tato latence je všeobecně 5-10 minut, ale může být za určitých podmínek vyšší.

- **Úložiště protokolů aktivit:** Používá se pro všechny události protokolu aktivit a stavu služby. Je možné použít vyhrazené upozorňování. Obsahuje události na úrovni předplatného, ke kterým dochází u objektů ve vašem předplatném, jak je vidět z vnějšku těchto objektů. Příkladem může být, když je zásada nastavená nebo je prostředek k dispozici nebo je odstraněný.

- **Azure Storage:** Úložiště pro obecné účely, které podporuje Azure Diagnostics a další nástroje pro monitorování. Je to cenová možnost pro dlouhodobé uchovávání telemetrie monitorování. U dat uložených v této službě se nepodporuje upozorňování.

- **Event Hubs:** Obecně se používá ke streamování dat do místních nebo ITSM nástrojů pro monitorování nebo pro jiné partnery.

Azure Monitor má čtyři typy výstrah, které jsou spojené s úložištěm, ve kterém jsou uložená data:

- [Výstraha metriky](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric): výstrahy na data v databázi Azure monitor metrik. K výstrahám dochází, když monitorovaná hodnota překračuje prahovou hodnotu definovanou uživatelem a potom znovu, až se vrátí do stavu "normální".

- [Výstraha na dotaz na protokol](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query): k dispozici pro výstrahy týkající se obsahu v Application Insights nebo v úložištích Azure Logs. Může také upozorňovat na závislosti na dotazech mezi jednotlivými pracovními prostory.

- [Upozornění protokolu aktivit](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log): výstrahy na položkách v úložišti protokolu aktivit, s výjimkou Service Healthch dat.

- [Výstraha Service Health](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications): speciální typ výstrahy, která se používá jenom pro Service Health problémy, které pocházejí z úložiště protokolu aktivit, jako jsou výpadky a nadcházející plánovaná údržba. Upozorňujeme, že tento typ výstrahy je nakonfigurovaný prostřednictvím [Azure Service Health](https://docs.microsoft.com/azure/service-health/service-health-overview), což je doplňková služba pro Azure monitor.

### <a name="enable-alerting-through-partner-tools"></a>Povolit upozorňování prostřednictvím partnerských nástrojů

Pokud používáte externí řešení pro upozorňování, směrování je co nejvíc v rámci služby Azure Event Hubs, což je nejrychlejší cesta mimo Azure Monitor. Budete muset zaplatit za příjem do centra událostí. Pokud se náklady nejedná o problém a rychlost, můžete Azure Storage použít jako levnější alternativu. Ujistěte se, že vaše monitorování nebo ITSM nástroje mohou číst Azure Storage k extrakci dat.

Azure Monitor zahrnují podporu pro integraci s dalšími monitorovacími platformami a ITSM software, jako je ServiceNow. Můžete použít upozorňování Azure a pořád aktivovat akce mimo Azure, jak to vyžaduje Správa incidentů nebo DevOps proces. Pokud chcete upozornit Azure Monitor a automatizovat odpověď, můžete spustit automatizované akce pomocí Azure Functions, Azure Logic Apps nebo Azure Automation na základě vašeho scénáře a požadavků.

### <a name="specialized-azure-monitoring-offerings"></a>Specializované nabídky monitorování Azure

[Řešení pro správu](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) většinou ukládají svá data v úložišti protokolů Azure. Tyto dvě výjimky jsou Azure Monitor pro virtuální počítače a Azure Monitor pro kontejnery. Následující tabulka popisuje možnosti upozorňování na základě konkrétního datového typu a místa, kde je uložený.

Řešení| Typ dat | Chování výstrahy
:---|:---|:---
Azure Monitor pro kontejnery | Vypočtená Průměrná data o výkonu z uzlů a lusky se zapisují do úložiště metrik. | Upozornění na metriku můžete vytvořit, pokud chcete být upozorňováni na základě variace měřené míry využití, agregovaně v čase.
|| Vypočtená údaje o výkonu, které používají percentily z uzlů, řadičů, kontejnerů a lusků, se zapisují do úložiště Logs. Do úložiště protokolů se zapisují také protokoly kontejnerů a informace o inventáři. | Pokud chcete být upozorňováni na základě variace měřeného využití z clusterů a kontejnerů, vytvořte výstrahy dotazování protokolu. Výstrahy dotazů na protokol se dají nakonfigurovat taky na základě počtu fází a počtu uzlů stavu.
Azure Monitor pro virtuální počítače | Kritéria stavu jsou metriky zapsané do úložiště metrik. | Výstrahy jsou generovány při změně stavu z stavu v pořádku na stav není v pořádku. Tato výstraha podporuje jenom skupiny akcí, které jsou nakonfigurované k odesílání oznámení SMS nebo e-mailem.
|| Data protokolu o namapování a data protokolu výkonu hostovaného operačního systému se zapisují do úložiště Logs. | Vytváření výstrah dotazů protokolu.

### <a name="fastest-speed-driven-by-cost"></a>Nejrychlejší rychlost řízená náklady

Latence je jedním z nepostradatelných rozhodnutí při řízení výstrah a rychlé řešení problémů, které mají vliv na vaši službu. Pokud budete během pěti minut vyžadovat upozorňování téměř v reálném čase, vyhodnoťte je jako první, pokud máte nebo můžete dostávat upozornění na telemetrii, kde je ve výchozím nastavení uložená. Obecně platí, že tato strategie je zároveň možnost nejlevnější, protože nástroj, který používáte, již do tohoto umístění odesílá svá data.

K tomuto pravidlu se říká několik důležitých poznámek pod čarou.

**Telemetrie hostovaného operačního systému** má několik cest, které se mají do systému dostat.

- Nejrychlejší způsob, jak upozornit na tato data, je importovat jako vlastní metriky. Použijte k tomu rozšíření Azure Diagnostics a pak použijte upozornění na metriku. Vlastní metriky jsou ale momentálně ve verzi Preview a jsou [dražší než jiné možnosti](https://azure.microsoft.com/pricing/details/monitor).

- Minimální náročná, ale nejpomalejší metoda je odeslání do Azure logs Kusto Storu. Spuštění agenta Log Analytics na virtuálním počítači je nejlepší způsob, jak do tohoto úložiště získat veškerou metriku a data protokolu hostovaného operačního systému.

- Můžete ho poslat do obou úložišť tak, že na stejném virtuálním počítači spustíte rozšíření i agenta. Pak můžete rychle vygenerovat výstrahu, ale také použít data hostovaného operačního systému jako součást složitějších hledání, když je zkombinujete s jinou telemetrie.

**Import dat z místního prostředí:** Pokud se snažíte dotazovat a monitorovat mezi počítači, které běží v Azure a v místním prostředí, můžete k shromažďování dat hostovaného operačního systému použít agenta Log Analytics. Pak můžete k [metrikám](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) využít funkci s názvem Logs a zjednodušit metriky do úložiště metrik. Tato metoda obchází část procesu příjmu do úložiště protokolů Azure a data jsou proto k dispozici dříve v databázi metrik.

### <a name="minimize-alerts"></a>Minimalizovat výstrahy

Pokud používáte řešení, jako je například Azure Monitor pro virtuální počítače, a najít výchozí kritéria pro stav, která monitorují přijatelné využití výkonu, nevytvářejte překrývající se metriky nebo dotazy protokolu v závislosti na stejných čítačích výkonu.

Pokud nepoužíváte Azure Monitor pro virtuální počítače, napravte si úlohy vytváření výstrah a správu oznámení tím, že prozkoumáte následující funkce:

> [!NOTE]
> Tyto funkce se vztahují jenom na výstrahy metriky, výstrahy na základě dat, která se odesílají do databáze metriky Azure Monitor. Tyto funkce se nevztahují na jiné typy výstrah. Jak už bylo zmíněno dříve, primárním cílem výstrah metriky je rychlost. Pokud se při získání výstrahy za méně než pět minut nejedná o primární obavy, můžete místo toho použít výstrahu dotazu protokolu.

- [Dynamické prahové](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds)hodnoty: dynamické prahové hodnoty prohledají aktivitu prostředku za časové období a vytvoří horní a dolní prahové hodnoty normální chování. Když je monitorovaná metrika mimo tyto prahové hodnoty, zobrazí se upozornění.

- [Výstrahy s více přihlašovacími](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts)údaji: můžete vytvořit upozornění na metriku, které používá kombinaci dvou různých vstupů ze dvou různých typů prostředků. Pokud třeba chcete vyvolat výstrahu, když je využití procesoru virtuálního počítače větší než 90%, a počet zpráv v určité frontě Azure Service Bus zaznamenání, že virtuální počítač překročí určitou hodnotu, můžete to udělat bez vytvoření dotazu protokolu. Tato funkce funguje jenom pro dva signály. Pokud máte složitější dotaz, zadáte data metriky do úložiště protokolu Azure Monitor a použijete dotaz protokolu.

- [Výstrahy](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts)s více prostředky: Azure monitor umožňuje jedno pravidlo výstrahy metriky, které se vztahuje na všechny prostředky virtuálních počítačů. Tato funkce vám může ušetřit čas, protože nemusíte vytvářet jednotlivé výstrahy pro každý virtuální počítač. Ceny za tento typ upozornění jsou stejné. Bez ohledu na to, jestli vytváříte výstrahy 50 pro monitorování využití procesoru pro virtuální počítače 50, nebo jedno upozornění, které monitoruje využití procesoru u všech virtuálních počítačů 50, náklady jsou stejné. Tyto typy výstrah můžete použít i v kombinaci s dynamickými prahovými hodnotami.

Pomocí těchto funkcí můžete ušetřit čas tím, že minimalizujete oznámení o výstrahách a správu základních výstrah.

### <a name="alerts-limitations"></a>Omezení výstrah

Nezapomeňte si uvědomit [omezení](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) počtu výstrah, které můžete vytvořit. Některá omezení (ale ne všechny) je možné zvýšit voláním podpory.

### <a name="best-query-experience"></a>Nejlepší možnosti dotazování

Pokud hledáte trendy pro všechna vaše data, je vhodné importovat všechna data do protokolů Azure, pokud už nejsou v Application Insights. Můžete vytvářet dotazy napříč oběma pracovními prostory, takže nemusíte přesouvat data mezi nimi. Do pracovního prostoru Log Analytics můžete také importovat protokol aktivit a data Service Health. Platíte za tato ingestování a ukládání, ale získáte všechna data na jednom místě pro účely analýzy a dotazování. Tento přístup vám také umožňuje vytvářet složité podmínky dotazování a upozornění.
