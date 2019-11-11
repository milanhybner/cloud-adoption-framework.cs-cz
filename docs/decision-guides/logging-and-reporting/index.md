---
title: Průvodce rozhodováním ohledně protokolování a generování sestav
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s protokolováním, generováním sestav a monitorováním jako základními službami při migraci do Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 4328cdf3249b065bf20efd5858254ad9da1dc211
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753180"
---
# <a name="logging-and-reporting-decision-guide"></a>Průvodce rozhodováním ohledně protokolování a generování sestav

Všechny organizace potřebují mechanismy, jak informovat IT týmy o problémech s výkonem, dostupností a zabezpečením dříve, než se z nich stanou závažné problémy. Úspěšná strategie monitorování umožňuje získat přehled o výkonu jednotlivých komponent, ze kterých se skládají úlohy a síťová infrastruktura. V kontextu migrace do veřejného cloudu je k zajištění, aby vaše organizace splňovala cíle z hlediska dostupnosti, zabezpečení a dodržování zásad, důležité do stávajících systémů monitorování integrovat protokolování a generování sestav a zpřístupnit důležité události a metriky příslušným IT pracovníkům.

![Diagram možností protokolování, generování sestav a monitorování od nejjednodušších po nejsložitější, které odpovídají rychlým odkazům níže](../../_images/decision-guides/decision-guide-logging-and-reporting.png)

Přejít na: [Plánování infrastruktury monitorování](#plan-your-monitoring-infrastructure) | [Model nativní pro cloud](#cloud-native) | [Místní rozšíření](#on-premises-extension) | [Agregace pomocí brány](#gateway-aggregation) | [Hybridní monitorování (v místním prostředí)](#hybrid-monitoring-on-premises) | [Hybridní monitorování (v cloudu)](#hybrid-monitoring-cloud-based) | [Více cloudů](#multicloud) | [Další informace](#learn-more)

Inflexní bod při určování strategie cloudového protokolování a generování sestav vychází hlavně ze stávajících investic vaší organizace do provozních procesů a do určité míry i z vašich případných požadavků na podporu strategie s více cloudy.

Aktivity v cloudu je možné protokolovat a hlásit více způsoby. Dvě běžné možnosti spravovaných služeb, které vycházejí z návrhu předplatného a počtu předplatných, jsou protokolování nativní pro cloud a centrální protokolování.

## <a name="plan-your-monitoring-infrastructure"></a>Plánování infrastruktury monitorování

Při plánování nasazení je potřeba zvážit, kam se budou ukládat data protokolování, a způsob integrace cloudových služeb generování sestav a monitorování se stávajícími procesy a nástroji.

| Otázka | Model nativní pro cloud | Místní rozšíření | Hybridní monitorování | Agregace pomocí brány |
|-----|-----|-----|-----|-----|
| Máte už místní infrastrukturu monitorování? | Ne | Ano | Ano |  Ne |
| Brání vaše požadavky ukládání dat protokolů v externích umístěních úložiště? | Ne | Ano | Ne | Ne |
| Potřebujete do místních systémů integrovat monitorování cloudu? | Ne | Ne | Ano | Ne |
Potřebujete zpracovávat nebo filtrovat telemetrická data před jejich odesláním do systémů monitorování? | Ne | Ne | Ne | Ano |

### <a name="cloud-native"></a>Model nativní pro cloud

Pokud vaše organizace aktuálně nemá zavedené systémy protokolování a generování sestav nebo pokud se vaše plánované nasazení nemusí integrovat se stávajícími místními nebo jinými externími systémy monitorování, nejjednodušší je zvolit řešení SaaS nativní pro cloud, jako je [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview).

V tomto scénáři se veškerá data protokolů zaznamenávají a ukládají v cloudu, zatímco nástroje pro protokolování a generování sestav, které zpracovávají a zpřístupňují informace IT pracovníkům, poskytuje platforma Azure a služba Azure Monitor.

V menších nebo experimentálních nasazeních je pro jednotlivá předplatná nebo jednotlivé úlohy možné ad hoc implementovat vlastní řešení protokolování založená na službě Azure Monitor, která jsou centrálně uspořádaná a umožňují monitorovat data protokolů napříč všemi cloudovými aktivy.

**Předpoklady pro model nativní pro cloud:** Při použití systémů protokolování a generování sestav nativního pro cloud se předpokládá následující:

- Data protokolů z cloudových úloh nepotřebujete integrovat do stávajících místních systémů.
- Cloudové systémy generování sestav nebudete používat k monitorování místních systémů.

### <a name="on-premises-extension"></a>Místní rozšíření

Zajištění, aby aplikace a služby migrované do cloudu používaly cloudová řešení protokolování a generování sestav, jako je Azure Monitor, může vyžadovat značné úsilí spojené s opakovaným vývojem. V těchto případech zvažte možnost povolit těmto úlohám pokračovat v odesílání telemetrických dat do stávajících místních systémů.

Pro zajištění podpory tohoto přístupu je potřeba, aby vaše cloudové prostředky byly schopné komunikovat přímo s místními systémy prostřednictvím kombinace [hybridních sítí](../software-defined-network/hybrid.md) a [doménových služeb hostovaných v cloudu](../identity/index.md#cloud-hosted-domain-services). Cloudová virtuální síť pak bude fungovat jako síťové rozšíření místního prostředí. Díky tomu budou úlohy hostované v cloudu moct komunikovat přímo s místními systémy protokolování a generování sestav.

Tento přístup využívá stávající investice do nástrojů pro monitorování s minimálními úpravami aplikací nebo služeb nasazených v cloudu. Často se jedná o nejrychlejší přístup k zajištění podpory monitorování během migrace typu lift and shift. Nebudou se ale zachytávat data protokolů vygenerovaná cloudovými prostředky PaaS a SaaS a vynechají se všechny protokoly související s virtuálními počítači vygenerované samotnou cloudovou platformou, jako je například stav virtuálních počítačů. Tento model by proto měl být pouze dočasným řešením, dokud nedojde k implementaci ucelenějšího řešení hybridního monitorování.

Pouze místní prostředí &ndash; předpoklady:

- Kvůli zajištění podpory technických požadavků nebo kvůli zákonným požadavkům nebo požadavkům zásad potřebujete uchovávat data protokolů pouze v místním prostředí.
- Vaše místní systémy nepodporují řešení hybridního protokolování a generování sestav nebo agregace pomocí brány.
- Vaše cloudové aplikace můžou odesílat telemetrii přímo do vašich místních systémů protokolování nebo agentů monitorování, kteří je odesílají do místního prostředí a které je možné nasadit na virtuálních počítačích úloh.
- Vaše úlohy nejsou závislé na službách PaaS ani SaaS, které vyžadují cloudové protokolování a generování sestav.

### <a name="gateway-aggregation"></a>Agregace pomocí brány

Ve scénářích, kde je objem cloudových telemetrických dat příliš velký nebo stávající místní systémy monitorování vyžadují před zpracováním dat protokolů jejich úpravu, může být potřeba služba [agregace dat protokolů pomocí brány](https://docs.microsoft.com/azure/architecture/patterns/gateway-aggregation).

K vašemu poskytovateli cloudu se nasadí služba brány. Příslušné aplikace a služby se pak nakonfigurují tak, aby odesílaly telemetrická data do brány, a ne do výchozího systému protokolování. Brána pak může data zpracovat (agregovat, kombinovat nebo jinak formátovat) a následně je odeslat do služby monitorování pro účely ingestování a analýzy.

Pomocí brány je možné také agregovat a předběžně zpracovávat telemetrická data určená pro systémy nativní pro cloud nebo hybridní systémy.

Předpoklady pro agregaci pomocí brány:

- Očekáváte, že vaše cloudové aplikace nebo služby budou generovat velké objemy telemetrických dat.
- Před odesláním telemetrických dat do systémů monitorování je potřebujete formátovat nebo jinak optimalizovat.
- Vaše systémy monitorování mají k dispozici rozhraní API nebo jiné mechanismy pro příjem dat protokolů po jejich zpracování bránou.

### <a name="hybrid-monitoring-on-premises"></a>Hybridní monitorování (v místním prostředí)

Řešení hybridního monitorování kombinuje data protokolů z místních i cloudových prostředků a poskytuje integrovaný přehled o provozním stavu vašich digitálních aktiv.

Pokud jste už investovali do místních systémů monitorování, které by bylo obtížné nebo nákladné nahradit, možná budete potřebovat integrovat telemetrii z cloudových úloh do stávajících místních řešení pro monitorování. V místním systému hybridního monitorování místní telemetrická data i nadále využívají stávající místní systém monitorování. Cloudová telemetrická data se odesílají přímo do místního systému monitorování nebo do služby Azure Monitor, kde se pak zkompilují a v pravidelných intervalech ingestují do místního systému.

**Předpoklady pro místní hybridní monitorování:** Při použití místního systému protokolování a generování sestav pro účely hybridního monitorování se předpokládá následující:

- K monitorování cloudových úloh potřebujete používat stávající místní systémy generování sestav.
- Potřebujete udržovat vlastnictví dat protokolů v místním prostředí.
- Vaše místní systémy pro správu mají k dispozici rozhraní API nebo jiné mechanismy pro příjem dat protokolů z cloudových systémů.

> [!TIP]
> Díky iterativní povaze migrace do cloudu je pravděpodobné, že s postupným vývojem integrace cloudových prostředků a služeb mezi vaše celková digitální aktiva přejdete z rozdílného monitorování nativního pro cloud a místního monitorování na částečně hybridní přístup.

### <a name="hybrid-monitoring-cloud-based"></a>Hybridní monitorování (v cloudu)

Pokud nemáte naléhavou potřebu udržovat místní systém monitorování nebo chcete místní systémy monitorování nahradit centralizovaným cloudovým řešením, můžete také zvolit integraci místních dat protokolů se službou Azure Monitor, která bude sloužit jako centrální cloudový systém monitorování.

Podobně jako v případě přístupu zaměřeného na místní prostředí cloudové úlohy v tomto scénáři odesílají telemetrii přímo do služby Azure Monitor a místní aplikace a služby odesílají telemetrii buď přímo do služby Azure Monitor, nebo tato data agregují v místním prostředí a v pravidelných intervalech je ingestují do služby Azure Monitor. Azure Monitor pak může sloužit jako hlavní systém monitorování a generování sestav pro veškerá vaše digitální aktiva.

Předpoklady pro cloudové hybridní monitorování: Při použití cloudových systémů protokolování a generování sestav pro účely hybridního monitorování se předpokládá následující:

- Nejste závislí na stávajících místních systémech monitorování.
- Vaše úlohy nepodléhají žádným zákonným požadavkům ani požadavkům zásad na ukládání dat protokolů v místním prostředí.
- Vaše cloudové systémy monitorování mají k dispozici rozhraní API nebo jiné mechanismy pro příjem dat protokolů z místních aplikací a služeb.

### <a name="multicloud"></a>Více cloudů

Integrace funkcí protokolování a generování sestav v rámci platformy s více cloudy může být složitá. Služby nabízené různými platformami často nejsou přímo srovnatelné a liší se i funkce protokolování a telemetrie, které tyto služby nabízejí.
Zajištění podpory protokolování pro více cloudů často vyžaduje použití služeb brány, které před odesláním dat protokolů do hybridního řešení protokolování zpracují data do společného formátu.

## <a name="learn-more"></a>Další informace

Výchozí službou generování sestav a monitorování pro Azure je [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview). Tato služba poskytuje:

- Jednotnou platformu pro shromažďování telemetrie aplikací, telemetrie hostitelů (jako jsou virtuální počítače), metrik kontejnerů, metrik platformy Azure a protokolů událostí.
- Vizualizaci, dotazy, upozornění a analytické nástroje. Může poskytovat přehledy o virtuálních počítačích, hostovaných operačních systémech, virtuálních sítích a událostech aplikací úloh.
- Rozhraní [REST API](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough) umožňující integraci s externími službami a automatizaci služeb monitorování a upozorňování.
- [Integraci](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-partners) s řadou oblíbených externích dodavatelů.

## <a name="next-steps"></a>Další kroky

Protokolování a generování sestav je pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
