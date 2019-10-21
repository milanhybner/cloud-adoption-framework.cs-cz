---
title: Průvodce monitorováním cloudu – strategie monitorování pro modely nasazení v cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vyberte, kdy použít Azure Monitor nebo System Center Operations Manager v Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 10/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 9fdef4d5d3d9cd39d16566221262330ef110bb3a
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548165"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Průvodce monitorováním cloudu: strategie monitorování pro modely nasazení v cloudu

Tento článek zahrnuje naši doporučenou strategii monitorování pro všechny modely nasazení v cloudu, a to na základě následujících kritérií:

- Musíte zachovat svůj závazek na Operations Manager nebo jinou platformu pro monitorování podniku, protože integrace s vašimi procesy IT, znalostmi a odbornými znalostmi nebo některými funkcemi není ještě dostupná v Azure Monitor.
- Musíte monitorovat úlohy místně i ve veřejném cloudu nebo jenom v cloudu.
- Vaše strategie migrace do cloudu zahrnuje modernizaci IT operace a přechod na naše služby a řešení Cloud monitoring.
- Je možné, že máte důležité systémy, které jsou gapped nebo fyzicky izolované, hostované v privátním cloudu nebo na fyzickém hardwaru a je třeba je monitorovat.

Naše strategie zahrnuje podporu pro monitorování infrastruktury (výpočetní prostředky, úložiště a zatížení serveru), aplikaci (koncového uživatele, výjimky a klienta) a síťové prostředky k zajištění kompletní perspektivy monitorování orientované na služby.

## <a name="azure-cloud-monitoring"></a>Monitorování cloudu Azure

Azure Monitor je služba Azure Native Platform, která poskytuje jeden zdroj pro monitorování prostředků Azure. Je navržená pro cloudová řešení, která jsou založená na Azure a která podporují obchodní funkce založené na úlohách virtuálních počítačů nebo složitých architekturách, které používají mikroslužby a další prostředky platforem. Monitoruje všechny vrstvy zásobníku počínaje službami tenanta, jako jsou Azure Active Directory Domain Services, události na úrovni předplatného a Azure Service Health. Monitoruje také prostředky infrastruktury, jako jsou virtuální počítače, úložiště a síťové prostředky, a v horní vrstvě aplikace. Monitorování každé z těchto závislostí a shromáždění správných signálů, které mohou vysílat, poskytují přehled o tom, jaké aplikace a jaká klíčová infrastruktura potřebujete.

Následující tabulka shrnuje doporučený postup pro monitorování jednotlivých vrstev zásobníku.

<!-- markdownlint-disable MD033 -->

Vrstvení | Prostředek | Rozsah | Metoda
---|---|---|----
Aplikace | Webová aplikace běžící na platformě .NET, .NET Core, Java, JavaScriptu a Node. js na virtuálním počítači Azure, App Services Azure, Service Fabric Azure, Azure Functions a Azure Cloud Services | Monitorovat živou webovou aplikaci, aby automaticky zjišťoval anomálie výkonu, identifikovala výjimky a problémy kódu a shromažďují analýzy chování uživatelů. |  Azure Monitor (Application Insights)
Prostředky Azure – PaaS | 1. Azure Database Services (například SQL nebo mySQL) | 1. Azure Database for SQL – metriky výkonu. | 1. Povolte protokolování diagnostiky, aby se streamovaná data SQL mohla zasílat do protokolů Azure Monitor.
Prostředky Azure – IaaS | 1. Azure Storage<br/> 2. Application Gateway Azure<br/> 3. skupiny zabezpečení sítě<br/> 4. Azure Traffic Manager<br/> 5. virtuální počítač<br/> 6. Služba Azure Kubernetes/Azure Container Instances | 1. kapacita, dostupnost a výkon.<br/> 2. výkon a diagnostické protokoly (aktivita, přístup, výkon a brána firewall).<br/> 3. Sledujte události při použití pravidel a čítač pravidla pro počet použití pravidla na odepřít nebo povolit.<br/> 4. monitorování dostupnosti stavu koncového bodu.<br/> 5. Sledujte kapacitu, dostupnost a výkon v operačním systému virtuálního počítače hosta. Namapujte závislosti aplikací hostované na každém virtuálním počítači, včetně viditelnosti aktivních síťových připojení mezi servery, latencí příchozího a odchozího připojení a portů v rámci libovolné architektury připojené k protokolu TCP.<br/> 6. Sledujte kapacitu, dostupnost a výkon úloh běžících na kontejnerech a instancích kontejnerů. | 1. metrika úložiště pro Blob Storage.<br/> 2. Povolte protokolování diagnostiky a nakonfigurujte streamování na Azure Monitor protokoly.<br/> 3. Povolte diagnostické protokolování skupin zabezpečení sítě a nakonfigurujete streamování na Azure Monitor protokoly.<br/> 4. Povolte diagnostické protokolování koncových bodů Traffic Manager a nakonfigurujte streamování na Azure Monitor protokoly.<br/> 5. povolení Azure Monitor pro virtuální počítače<br/> 6. povolení Azure Monitor pro kontejnery
Síť| Komunikace mezi virtuálním počítačem a jedním nebo více koncovými body (jiný virtuální počítač, plně kvalifikovaný název domény, identifikátor URI nebo adresa IPv4). | Sledujte dostupnost, latenci a změny topologie sítě, ke kterým dochází mezi virtuálním počítačem a koncovým bodem. | Network Watcher Azure
Předplatné Azure | Stav služby Azure a základní stav prostředků | <li> Akce správy prováděné u služby nebo prostředku.<br/><li> Stav služby se službou Azure je v nedostupném stavu.<br/><li> Zjistili jsme problémy se stavem prostředku Azure z hlediska služby Azure.<br/><li> Operace prováděné s Azure Autoscale indikují chybu nebo výjimku. <br/><li> Operace prováděné s Azure Policy označují, že došlo k povolené nebo odepřené akci.<br/><li> Záznam upozornění generovaných Azure Security Center. |Doručit v protokolu aktivit za účelem monitorování a upozorňování pomocí Azure Resource Manager.
Tenant Azure|Azure Active Directory || Povolte protokolování diagnostiky a nakonfigurujete streamování na Azure Monitor protokoly.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Monitorování hybridního cloudu

V mnoha organizacích se Cloud musí považovat za postupně, kde je hybridní cloudový model nejběžnější první krok na cestě. Pečlivě vyberete příslušnou podmnožinu aplikací a infrastrukturu pro zahájení migrace a zamezit tak výpadkům vaší firmy. Vzhledem k tomu, že nabízíme dvě monitorovací platformy, které podporují tento model cloudu, tvůrci rozhodnutí IT se zahodí, což je nejlepší možnost pro podporu jejich obchodních a provozních cílů. Probereme několik faktorů, které vám pomohou vyřešit nejistotu a poskytnou vám informace o tom, kterou platformu zvážit.

Mezi klíčové technické aspekty, které je potřeba vzít v úvahu, patří:

- Potřebujete shromažďovat data z prostředků Azure, které podporují úlohu, a překládat je do stávajících nástrojů pro místní nebo spravované poskytovatele služby.

- Je potřeba zachovat stávající investice do System Center Operations Manager a nakonfigurovat je pro monitorování prostředků IaaS a PaaS spuštěných v Azure. Volitelně, protože sledujete dvě prostředí s různými charakteristikami podle vašich požadavků, určíte integraci s Azure Monitor podporuje vaši strategii.

- V rámci strategie modernizace pro standardizaci a snížení nákladů a složitosti můžete potvrdit, že Azure Monitor ke sledování prostředků v Azure a ve vaší podnikové síti.

Následující tabulka shrnuje požadavky, které Azure Monitor a System Center Operations Manager podporu monitorování hybridního cloudového modelu založeného na společné sadě kritérií.

<!-- markdownlint-disable MD033 -->

|Požadavek | Azure Monitor | Operations Manager |
|:--|:---|:---|
|Požadavky na infrastrukturu | **Ne** | **Ano**<br> Vyžaduje minimálně management server a SQL Server pro hostování provozní databáze a databáze datového skladu pro sestavy. Je složitější, pokud je potřeba HA/DR, počítačů ve více lokalitách, nedůvěryhodných systémech a dalších složitých hlediscích návrhu.|
|Omezené připojení – bez internetu<br> nebo izolovaná síť | **Ne** | **Ano** |
|Omezený přístup prostřednictvím Internetu řízený připojením | **Ano** | **Ano** |
|Omezené připojení – často odpojeno | **Ano** | **Ano** |
|Konfigurovatelné monitorování stavu | **Ne** | **Ano** |
| Test dostupnosti webové aplikace (izolovaná síť) | **Ano, omezeno**<br> Azure Monitor má v této oblasti omezené podpory a vyžaduje vlastní výjimky brány firewall. | **Ano** |
| Test dostupnosti webové aplikace (globálně distribuované) | **Ne** | **Ano** |
|Monitorování úloh virtuálních počítačů | **Ano, omezeno**<br> Může shromažďovat protokoly chyb služby IIS a SQL Server, události systému Windows a čítače výkonu. Vyžaduje vytváření vlastních dotazů, upozornění a vizualizací. | **Ano**<br> Podporuje monitorování většiny úloh serveru s dostupnými sadami Management Pack. Vyžaduje buď Log Analytics agenta Windows nebo agenta Operations Manager na virtuálním počítači, a hlásí se zpátky do skupiny pro správu v podnikové síti.|
|Monitorování Azure IaaS | **Ano** | **Ano**<br> Podporuje monitorování většiny infrastruktury z podnikové sítě. Sleduje stav dostupnosti, metriky a výstrahy pro virtuální počítače Azure, SQL a úložiště prostřednictvím Azure Management Pack.|
|Monitorování Azure PaaS | **Ano** | **Ano, omezeno**<br> Na základě toho, co je podporováno v Azure Management Pack. |
|Monitorování služeb Azure | **Ano**<br> | **Ano**<br> I když v současnosti není k dispozici žádné nativní monitorování služby Azure Service Health prostřednictvím Management Pack, můžete vytvořit vlastní pracovní postupy pro dotazování na výstrahy služby Azure Service Health. Pomocí REST API Azure můžete dostávat upozornění prostřednictvím stávajících oznámení.|
|Monitorování moderní webové aplikace | **Ano** | **Ne** |
|Starší verze monitorování webových aplikací | **Ano, omezení se liší podle sady SDK**<br> Podporuje monitorování starších verzí webových aplikací .NET a Java. | **Ano, omezeno** |
|Monitorování kontejnerů služby Azure Kubernetes | **Ano** | **Ne** |
|Monitorovat kontejnery Docker/Windows | **Ano** | **Ne** |
|Sledování výkonu sítě | **Ano** | **Ano, omezeno**<br> Podporuje kontroly dostupnosti a shromažďuje základní statistiky ze síťových zařízení pomocí protokolu SNMP z podnikové sítě.|
|Interaktivní analýza dat | **Ano** | **Ne**<br> Spoléhá na SQL Server Reporting Services předem zakonzervované nebo vlastní sestavy, řešení vizualizace třetích stran nebo na vlastní Power BI implementaci. Operations Manager datový sklad má omezení škálování a výkonu. Integrujte s protokoly Azure Monitor jako alternativu pro požadavky na agregaci dat. Integraci je dosaženo konfigurací konektoru Log Analytics.|
|Komplexní diagnostika, analýza hlavní příčiny a včasné řešení potíží | **Ano** | **Ano, omezeno**<br> Podporuje ucelenou diagnostiku a řešení potíží pouze pro místní infrastrukturu a aplikace. Používá jiné součásti softwaru System Center nebo Partnerská řešení.|
|Interaktivní vizualizace (řídicí panely) | **Ano** | **Ano, omezeno**<br> Poskytuje základní řídicí panely pomocí webové konzoly HTLM5 nebo pokročilé prostředí od partnerských řešení, jako jsou čtvercová a Savision. |
|Integrace s IT/DevOps nástroji | **Ano** | **Ano, omezeno** |

<!-- markdownlint-enable MD033 -->

### <a name="collect-and-stream-monitoring-data-to-third-party-or-on-premises-tools"></a>Shromažďování a streamování dat monitorování do třetích stran nebo místních nástrojů

Abyste mohli shromažďovat metriky a protokoly z prostředků infrastruktury a platforem Azure, musíte pro tyto prostředky povolit diagnostické protokoly Azure. Kromě toho můžete pomocí virtuálních počítačů Azure shromáždit metriky a protokoly z hostovaného operačního systému tím, že povolíte rozšíření Azure Diagnostics. Pro přeposílání diagnostických dat vysílaných z prostředků Azure do místních nástrojů nebo do poskytovatele spravované služby nakonfigurujte [Event Hubs](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-stream-event-hubs) pro streamování dat.

### <a name="monitor-with-system-center-operations-manager"></a>Monitorování pomocí System Center Operations Manager

I když System Center Operations Manager původně navržený jako místní řešení pro monitorování napříč aplikacemi, úlohami a infrastrukturou běžícími ve vašem IT prostředí, vyvinul se k tomu, aby zahrnoval možnosti cloudového monitorování a integruje se s Azure, Office 365 a Amazon Web Services (AWS). Je možné monitorovat v těchto různých prostředích sady Management Pack, které jsou navržené a aktualizované tak, aby je podporovaly.  

Pro zákazníky, kteří provedli významné investice do Operations Manager k zajištění komplexního monitorování, které je úzce integrováno s jejich správa IT služeb procesy a nástroji, nebo zákazníky, kteří se do Azure seznámili, je srozumitelná otázka:

- Může Operations Manager dál doručovat hodnoty a dělat obchodní smysl?

- Pokud jsou funkce v Operations Manager vhodné pro naši organizaci IT?

- Integruje Operations Manager s Azure Monitor poskytování nákladově efektivního a komplexního monitorovacího řešení, které vyžadujeme?

Pokud jste už investovali do Operations Manager, nemusíte se soustředit na plánování migrace, abyste ho hned nahradili. Když Azure nebo jiní poskytovatelé cloudu existují jako rozšíření vaší vlastní místní sítě, Operations Manager můžou monitorovat virtuální počítače hosta a prostředky Azure, jako kdyby byly ve vaší podnikové síti. To vyžaduje spolehlivé síťové připojení mezi vaší sítí a virtuální sítí Azure, která má dostatečnou šířku pásma.

Abyste mohli monitorovat úlohy běžící v Azure, budete potřebovat:

- [Azure Management Pack](https://www.microsoft.com/download/details.aspx?id=50013) ke shromažďování metrik výkonu vysílaných službami Azure, jako jsou webové a pracovní role, Application Insights testy dostupnosti (webtests), Service Bus atd. Management Pack používá REST API Azure ke sledování dostupnosti a výkonu těchto prostředků. Některé typy služeb Azure nemají žádné metriky ani žádná předdefinovaná monitorování v Management Pack, ale pořád je můžete monitorovat pomocí vztahů definovaných v Azure Management Pack pro zjištěné služby.

- [Azure SQL Database Management Pack](https://www.microsoft.com/download/details.aspx?id=38829) k monitorování dostupnosti a výkonu databází SQL Azure a serverů Azure SQL Database pomocí dotazů Azure REST API a T-SQL k SQL Server systémových zobrazení.

- Pokud chcete monitorovat hostovaný operační systém a úlohy běžící na virtuálním počítači, například SQL Server, IIS nebo Apache Tomcat, budete muset stáhnout a naimportovat Management Pack, který podporuje aplikaci, službu a operační systém.

Znalostní báze je definována v Management Pack, který popisuje, jak monitorovat jednotlivé závislosti a součásti. Sady Management Pack pro Azure vyžadují provedení sady kroků konfigurace v Azure a Operations Manager, aby mohli začít monitorovat tyto prostředky.

V aplikační vrstvě nabízí Operations Manager základní možnosti funkce Application Performance Monitoring pro některé starší verze rozhraní .NET a Java. Pokud některé aplikace v hybridním cloudovém prostředí fungují v režimu offline nebo v izolovaném režimu, tak, aby nemohly komunikovat s veřejnou cloudovou službou, Operations Manager funkce Application Performance Monitoring (APM) může být možnost životaschopná pro určité omezené scénáře. Pro aplikace, které neběží na starších platformách, se hostují místně i v jakémkoli veřejném cloudu, který umožňuje komunikaci přes bránu firewall (buď přímo, nebo prostřednictvím proxy serveru), k Azure použijte Azure Monitor Application Insights. Tato nabídka nabízí hloubkové monitorování na úrovni kódu s prvotřídní podporou pro ASP.NET, ASP.NET Core, Java, JavaScript a Node. js.

Pro všechny webové aplikace, které lze oslovit externě, byste měli povolit typ syntetických transakcí známých jako [monitorování dostupnosti]( https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability). Je důležité zjistit, jestli vaše aplikace nebo důležitý koncový bod HTTP/HTTPS, na kterém je vaše aplikace závislá, je k dispozici a reagovat. Application Insights monitoring dostupnosti umožňuje spouštět testy z více datových center Azure a poskytnout přehled o stavu aplikace z globální perspektivy.

I když je Operations Manager schopný monitorovat prostředky hostované v Azure, je k dispozici několik výhod, které zahrnují Azure Monitor, protože jejich síly přecházejí na Operations Manager a vytváří silný základ pro podporu případné migrace. z něho. Tady si projdeme každé z nich s naším doporučením, abyste zahrnuli Azure Monitor do strategie hybridního monitorování.  

#### <a name="disadvantage-of-using-operations-manager-by-itself"></a>Nevýhody použití Operations Manager sám sebou

1. Analýza dat monitorování v Operations Manager se běžně provádí pomocí předem definovaných zobrazení definovaných v sadách Management Pack, které jsou dostupné z konzoly, ze sestav služby SQL Server Reporting Services (SSRS) nebo vlastních zobrazení vytvořených koncovým uživatelem. Provádění ad-hoc analýzy dat není možné v poli. Vytváření sestav Operations Manager je neflexibilní, datový sklad, který poskytuje dlouhodobé uchovávání dat monitorování, není škálovatelný ani výkonný a odbornost v psaní příkazů T-SQL, vývoj řešení Power BI nebo použití řešení třetích stran. vyžaduje se pro podporu požadavků pro různé osoby v organizaci IT.

2. Výstrahy v Operations Manager neposkytují podporu pro složité výrazy a zahrnují logiku korelace, která vám pomůže snížit šum výstrah a seskupit výstrahy společně s úsilím, aby se zobrazil vztah mezi nimi, který vám pomůže identifikovat hlavní příčinu chybu.

#### <a name="advantage-of-operations-manager--azure-monitor"></a>Výhody Operations Manager + Azure Monitor

1. Protokoly Azure Monitor jsou řešeními, které řeší omezení Operations Manager a připisuje Operations Manager databázi datového skladu ke shromažďování důležitých dat výkonu a protokolů. Azure Monitor zajišťuje lepší analýzy, výkon při dotazování velkého objemu dat a uchovávání dat než datový sklad Operations Manager. Dotazovací jazyk umožňuje vytvářet mnohem složitější a sofistikované dotazy s možností spouštění dotazů v různých terabajtech dat během několika sekund. Data můžete rychle transformovat do výsečových grafů, časových grafů a mnoha dalších vizualizací. Již nejste omezeni tím, že pracujete se sestavami v Operations Manager založené na SQL Server Reporting Services, vlastních dotazech SQL nebo jiných alternativních řešeních pro analýzu těchto dat.

2. Implementací řešení pro správu výstrah Azure Monitor poskytují vylepšené možnosti upozorňování. Výstrahy generované ve skupině pro správu Operations Manager lze přeslat do pracovního prostoru Azure Monitorch Log Analytics. U předplatného, které zodpovídá za předávání výstrah z Operations Manager, můžete nakonfigurovat, aby se protokoly Azure Monitor jenom na určité výstrahy. Můžete například předávat jenom výstrahy, které splňují kritéria pro dotazování na podporu správy problémů při trendech, a zkoumání hlavní příčiny selhání nebo problémů přes jedno podokno skla. Kromě toho můžete vzájemně korelovat data protokolu z Application Insights nebo jiných zdrojů a získat tak přehled, který pomáhá vylepšit uživatelské prostředí, prodloužit dobu provozu a zkrátit čas na vyřešení incidentů.

3. Monitorujte v Azure cloudovou infrastrukturu a aplikace z jednoduché nebo vícevrstvé architektury a použijte Operations Manager k monitorování místní infrastruktury. To zahrnuje jeden nebo více virtuálních počítačů, několik virtuálních počítačů umístěných do skupiny dostupnosti nebo sady škálování virtuálních počítačů nebo kontejnerové aplikace nasazené ve službě Azure Kubernetes Service (AKS) spuštěné na kontejnerech Windows Server nebo Linux.

4. Použijte řešení System Center Operations Manager Health Check k proaktivnímu vyhodnocení rizika a stavu vaší skupiny pro správu System Center Operations Manager v pravidelných intervalech. To může nahradit nebo přičíst jakékoli vlastní funkce, které jste přidali do skupiny pro správu.

5. Díky funkci map služby Azure Monitor pro virtuální počítače umožňuje monitorovat metriky standardního připojení ze síťových připojení mezi virtuálními počítači Azure a místními virtuálními počítači. Tyto metriky zahrnují dobu odezvy, požadavky za minutu, propustnost provozu a odkazy. Můžete identifikovat neúspěšná připojení, řešit potíže, provádět ověřování migrace, provádět analýzu zabezpečení a ověřovat celou architekturu služby. Map může automaticky zjišťovat součásti aplikace v systémech Windows a Linux a namapovat komunikaci mezi službami. To vám pomůže identifikovat připojení a závislosti, které jste nevědomi, naplánovat a ověřit migraci do Azure a minimalizovat spekulací během řešení incidentů.

6. Pomocí Network Performance Monitor monitorujte síťové připojení mezi:

   - Vaše podniková síť a Azure.

   - Klíčové aplikace s více vrstvami a mikroslužby.

   - Uživatelská umístění a webové aplikace (HTTP/HTTPs).

   Tato strategie nabízí viditelnost síťové vrstvy bez nutnosti SNMP. Může také existovat v mapování interaktivní topologie, topologie směrování mezi segmenty směrování tras mezi zdrojovým a cílovým koncovým bodem. Je lepší volbou než pokus o provedení stejného výsledku s monitorováním sítě v Operations Manager nebo jinými nástroji pro monitorování sítě aktuálně používanými ve vašem prostředí.

### <a name="monitor-with-azure-monitor"></a>Monitorování pomocí služby Azure Monitor

I když migrace do cloudu představuje mnoho výzev, zahrnuje také řadu příležitostí. Umožňuje vaší organizaci migrovat z jednoho nebo několika místních nástrojů pro monitorování podniku nejen na to, aby mohly snižovat kapitálové výdaje a provozní náklady, ale také přináší výhody pro cloudovou platformu monitorování, jako je Azure Monitor. v cloudovém měřítku. Projděte si požadavky na monitorování a výstrahy, konfiguraci existujících nástrojů pro monitorování, úlohy přejdoucí do cloudu a nakonfigurujte Azure Monitor po finalizaci plánu.

- Monitorujte hybridní infrastrukturu a aplikace z jednoduché nebo vícevrstvé architektury, kde se komponenty hostují mezi Azure, jiným poskytovatelem cloudu a firemní sítí. To zahrnuje jeden nebo více virtuálních počítačů, několik virtuálních počítačů umístěných do skupiny dostupnosti nebo sady škálování virtuálních počítačů nebo kontejnerové aplikace nasazené ve službě Azure Kubernetes Service (AKS) spuštěné na kontejnerech Windows Server nebo Linux.

- Povolte Azure Monitor pro virtuální počítače, Azure Monitor pro kontejnery a Application Insights k detekci a diagnostikování problémů mezi infrastrukturou a aplikacemi. Pro důkladnější analýzu a korelaci dat shromážděných z více komponent nebo závislostí, které podporují aplikaci, je nutné použít protokoly Azure Monitor.

- Vytvářejte inteligentní výstrahy, které se můžou vztahovat na základní sadu aplikací a součástí služby, které vám pomůžou snížit šum s dynamickými prahovými hodnotami pro složité signály a využívat agregace výstrah založené na algoritmech strojového učení, které vám pomůžou rychle identifikovat chybu.

- Definujte knihovnu dotazů a řídicích panelů, které budou podporovat požadavky na různé osoby v organizaci IT.

- Definování standardů a metod pro povolení monitorování v rámci hybridních i cloudových prostředků, standardních hodnot monitorování pro každý prostředek, prahových hodnot výstrah atd.  

- Nakonfigurujte řízení přístupu na základě role (RBAC), takže uživatelům a skupinám udělíte jenom množství přístupu, které potřebují k tomu, aby mohli pracovat s daty monitorování z prostředků, které zodpovídají za správu.

- Zahrnutí automatizace a samoobslužné služby, které umožní každému týmu vytvářet, aktivovat a ladit své konfigurace monitorování a upozorňování, jak potřebují.

## <a name="private-cloud-monitoring"></a>Monitorování privátního cloudu

Holistický sledování Azure Stack můžete dosáhnout pomocí System Center Operations Manager. Konkrétně můžete monitorovat úlohy spuštěné v tenantovi, na úrovni prostředků, na virtuálních počítačích a na hostování infrastruktury Azure Stack (fyzické servery a přepínače sítě). Můžete také dosáhnout holistický monitoring s kombinací [možností monitorování infrastruktury](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) , které jsou součástí Azure Stack. Tyto funkce vám pomůžou zobrazit stav a výstrahy Azure Stack oblasti a [služby Azure monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) v Azure Stack, které pro většinu služeb poskytují metriky a protokoly infrastruktury základní úrovně.

Pokud jste už investovali do Operations Manager, můžete k monitorování dostupnosti a stavu nasazení Azure Stack použít Management Pack Azure Stack. To zahrnuje oblasti, poskytovatele prostředků, aktualizace, běhy aktualizací, jednotky škálování, uzly jednotek, role infrastruktury a jejich instance (logické entity skládající se z hardwarových prostředků). K komunikaci s Azure Stack používá rozhraní REST API poskytovatele stavu a aktualizace. Pokud chcete monitorovat fyzické servery a úložná zařízení, použijte dodavatele OEM Management Pack (například poskytované Lenovo, Hewlett Packard nebo Dell). Operations Manager může nativně monitorovat síťové přepínače a shromažďovat základní statistiky pomocí protokolu SNMP. Monitorování zatížení klientů je možné u Management Pack Azure pomocí dvou základních kroků. Nakonfigurujte předplatné, které chcete monitorovat, a přidejte monitory pro toto předplatné.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Shromažďování správných dat](./data-collection.md)
