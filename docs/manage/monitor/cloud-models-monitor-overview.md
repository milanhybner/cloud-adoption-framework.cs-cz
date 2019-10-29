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
ms.openlocfilehash: 6e02cffdbd76932e3066ed68501856aef2669b02
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979897"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Průvodce monitorováním cloudu: strategie monitorování pro modely nasazení v cloudu

Tento článek zahrnuje naši doporučenou strategii monitorování pro všechny modely nasazení v cloudu, a to na základě následujících kritérií:

- Je potřeba zachovat svůj závazek na Operations Manager nebo jinou platformu pro monitorování podniku, protože je integrovaná s vašimi procesy IT, znalostmi a odbornými znalostmi a některé funkce nejsou ještě dostupné v Azure Monitor.
- Potřebujete monitorovat úlohy místně i ve veřejném cloudu nebo jenom v cloudu.
- Vaše strategie migrace do cloudu zahrnuje modernizaci IT operace a přechod na naše služby a řešení Cloud monitoring.
- Je možné, že máte důležité systémy, které jsou gapped nebo fyzicky izolované, hostované v privátním cloudu nebo na fyzickém hardwaru. A systémy musí být monitorovány.

Naše strategie zahrnuje podporu monitorování infrastruktury (výpočetní služby, úložiště a zatížení serveru), aplikace (koncového uživatele, výjimky a klienta) a síťových prostředků. Nabízí kompletní perspektivu monitorování orientované na služby.

## <a name="azure-cloud-monitoring"></a>Monitorování cloudu Azure

Azure Monitor je služba Azure Native Platform, která poskytuje jeden zdroj pro monitorování prostředků Azure. Je navržená pro cloudová řešení, která:
* Jsou postavené na Azure.
* Podporují obchodní funkce založené na úlohách virtuálních počítačů nebo složitých architekturách, které používají mikroslužby a další prostředky platforem.

Monitoruje všechny vrstvy zásobníku počínaje klientskými službami, jako jsou Azure Active Directory Domain Services, události na úrovni předplatného a Azure Service Health. 

Monitoruje také prostředky infrastruktury, jako jsou virtuální počítače, úložiště a síťové prostředky. V horní vrstvě monitoruje vaši aplikaci. 

Monitorováním každé z těchto závislostí a shromažďováním správných signálů, které mohou vysílat, získáte přehled o tom, jaké aplikace a jaká klíčová infrastruktura potřebujete.

Náš doporučený postup pro monitorování jednotlivých vrstev zásobníku je shrnutý v následující tabulce:

<!-- markdownlint-disable MD033 -->

Vrstvení | Prostředek | Rozsah | Metoda
---|---|---|----
Aplikace | Webová aplikace, která běží na platformě .NET, .NET Core, Java, JavaScriptu a Node. js na virtuálním počítači Azure, Azure App Services, Azure Service Fabric, Azure Functions a Azure Cloud Services. | Monitorovat živou webovou aplikaci, aby automaticky zjišťoval anomálie výkonu, identifikovala výjimky a problémy kódu a shromažďují analýzy chování uživatelů. |  Azure Monitor (Application Insights).
Prostředky Azure – platforma jako služba (PaaS) | Služby Azure Database (například SQL nebo MySQL). | Metriky výkonu Azure Database for SQL. | Povolí protokolování diagnostiky pro streamování dat SQL pro Azure Monitor protokolů.
Prostředky Azure – infrastruktura jako služba (IaaS) | 1. Azure Storage<br/> 2. Application Gateway Azure<br/> 3. skupiny zabezpečení sítě<br/> 4. Azure Traffic Manager<br/> 5. Virtual Machines Azure<br/> 6. Služba Azure Kubernetes/Azure Container Instances | 1. kapacita, dostupnost a výkon.<br/> 2. protokoly výkonu a diagnostiky (aktivita, přístup, výkon a brána firewall).<br/> 3. Sledujte události při použití pravidel a čítač pravidla pro počet použití pravidla na odepřít nebo povolit.<br/> 4. monitorování dostupnosti stavu koncového bodu.<br/> 5. Sledujte kapacitu, dostupnost a výkon v operačním systému hostovaného virtuálního počítače (OS). Namapujte závislosti aplikací hostované na každém virtuálním počítači, včetně viditelnosti aktivních síťových připojení mezi servery, latencí příchozího a odchozího připojení a portů v rámci libovolné architektury připojené k protokolu TCP.<br/> 6. Sledujte kapacitu, dostupnost a výkon úloh běžících na kontejnerech a instancích kontejnerů. | 1. metrika úložiště pro Blob Storage.<br/> 2. Povolte protokolování diagnostiky a nakonfigurujte streamování na Azure Monitor protokoly.<br/> 3. Povolte diagnostické protokolování skupin zabezpečení sítě a nakonfigurujete streamování na Azure Monitor protokoly.<br/> 4. Povolte protokolování diagnostiky koncových bodů Traffic Manager a nakonfigurujte streamování na Azure Monitor protokoly.<br/> 5. Povolte Azure Monitor pro virtuální počítače.<br/> 6. Povolte Azure Monitor pro kontejnery.
Síť | Komunikace mezi virtuálním počítačem a jedním nebo více koncovými body (jiný virtuální počítač, plně kvalifikovaný název domény, identifikátor URI nebo adresa IPv4). | Sledujte dostupnost, latenci a změny topologie sítě, ke kterým dochází mezi virtuálním počítačem a koncovým bodem. | Network Watcher Azure.
Předplatné Azure | Stav služby Azure a základní stav prostředků. | <li> Akce správy prováděné u služby nebo prostředku.<br/><li> Stav služby se službou Azure je v nedostupném stavu.<br/><li> Zjistili jsme problémy se stavem prostředku Azure z hlediska služby Azure.<br/><li> Operace prováděné s Azure Autoscale indikují chybu nebo výjimku. <br/><li> Operace prováděné s Azure Policy označují, že došlo k povolené nebo odepřené akci.<br/><li> Záznam upozornění generovaných Azure Security Center. | Doručit v protokolu aktivit za účelem monitorování a upozorňování pomocí Azure Resource Manager.
Tenant Azure | Azure Active Directory || Povolte protokolování diagnostiky a nakonfigurujete streamování na Azure Monitor protokoly.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Monitorování hybridního cloudu

Pro mnoho organizací se musí přejít do cloudu postupně, kde je hybridní cloudový model nejběžnějším prvním krokem v cestě. Pečlivě vyberete vhodnou podmnožinu aplikací a infrastruktury pro zahájení migrace, zatímco se vyhnete přerušení vaší firmy. Vzhledem k tomu, že nabízíme dvě monitorovací platformy, které podporují tento model cloudu, tvůrci rozhodnutí IT můžou být nejistí, jaké jsou nejlepší možnosti pro podporu jejich obchodních a provozních cílů. 

V této části řešíme nejistotu tím, že provedeme několik faktorů a nabídneme porozumění platformě, kterou je potřeba vzít v úvahu.

Mějte na paměti následující klíčové technické aspekty:

- Potřebujete shromažďovat data z prostředků Azure, které podporují úlohu, a překládat je do stávajících nástrojů pro místní nebo spravované poskytovatele služby.

- Je potřeba zachovat stávající investice do System Center Operations Manager a nakonfigurovat je pro monitorování prostředků IaaS a PaaS, které běží v Azure. V případě, že v závislosti na vašich požadavcích sledujete dvě prostředí s různými charakteristikami, musíte určit, jak integrace s Azure Monitor podporuje vaši strategii.

- Jako součást strategie pro modernizaci, která se má sjednotit na jeden nástroj pro snížení nákladů a složitosti, je potřeba potvrdit Azure Monitor pro monitorování prostředků v Azure a ve vaší podnikové síti.

Následující tabulka shrnuje požadavky, které Azure Monitor a System Center Operations Manager podporu monitorování hybridního cloudového modelu založeného na společné sadě kritérií.

<!-- markdownlint-disable MD033 -->

|Požadavek | Azure Monitor | Operations Manager |
|:--|:---|:---|
|Požadavky na infrastrukturu | Ne | Ano<br> Vyžaduje minimálně management server a SQL Server pro hostování provozní databáze a databáze datového skladu pro sestavy. Složitost se zvyšuje, když potřebujete vysokou dostupnost a zotavení po havárii a že jsou počítače ve více lokalitách, nedůvěryhodných systémech a dalších komplexních hlediscích návrhu.|
|Omezené připojení – bez internetu<br> nebo izolovaná síť | Ne | Ano |
|Omezený přístup prostřednictvím Internetu řízený připojením | Ano | Ano |
|Omezené připojení – často odpojeno | Ano | Ano |
|Konfigurovatelné monitorování stavu | Ne | Ano |
| Test dostupnosti webové aplikace (izolovaná síť) | Ano, omezeno<br> Azure Monitor má v této oblasti omezené podpory a vyžaduje vlastní výjimky brány firewall. | Ano |
| Test dostupnosti webové aplikace (globálně distribuované) | Ne | Ano |
|Monitorování úloh virtuálních počítačů | Ano, omezeno<br> Může shromažďovat protokoly chyb služby IIS a SQL Server, události systému Windows a čítače výkonu. Vyžaduje vytváření vlastních dotazů, upozornění a vizualizací. | Ano<br> Podporuje monitorování většiny úloh serveru s dostupnými sadami Management Pack. Vyžaduje buď Log Analytics agenta Windows nebo agenta Operations Manager na virtuálním počítači, a hlásí se zpátky do skupiny pro správu v podnikové síti.|
|Monitorování Azure IaaS | Ano | Ano<br> Podporuje monitorování většiny infrastruktury z podnikové sítě. Sleduje stav dostupnosti, metriky a výstrahy pro virtuální počítače Azure, SQL a úložiště prostřednictvím Azure Management Pack.|
|Monitorování Azure PaaS | Ano | Ano, omezeno<br> Na základě toho, co je podporováno v Azure Management Pack. |
|Monitorování služeb Azure | Ano<br> | Ano<br> I když v současnosti není k dispozici žádné nativní monitorování služby Azure Service Health prostřednictvím Management Pack, můžete vytvořit vlastní pracovní postupy pro dotazování na výstrahy služby Azure Service Health. Pomocí REST API Azure můžete dostávat upozornění prostřednictvím stávajících oznámení.|
|Monitorování moderní webové aplikace | Ano | Ne |
|Starší verze monitorování webových aplikací | Ano, omezeno, se liší podle sady SDK<br> Podporuje monitorování starších verzí webových aplikací .NET a Java. | Ano, omezeno |
|Monitorování kontejnerů služby Azure Kubernetes | Ano | Ne |
|Monitorovat kontejnery Docker/Windows | Ano | Ne |
|Sledování výkonu sítě | Ano | Ano, omezeno<br> Podporuje kontroly dostupnosti a shromažďuje základní statistiky ze síťových zařízení pomocí protokolu SNMP (Simple Network Management Protocol) od podnikové sítě.|
|Interaktivní analýza dat | Ano | Ne<br> Spoléhá na SQL Server Reporting Services předem zakonzervované nebo vlastní sestavy, řešení vizualizace třetích stran nebo na vlastní Power BI implementaci. Operations Manager datový sklad má omezení škálování a výkonu. Integrujte s protokoly Azure Monitor jako alternativu pro požadavky na agregaci dat. Integraci můžete dosáhnout konfigurací konektoru Log Analytics.|
|Komplexní diagnostika, analýza hlavní příčiny a včasné řešení potíží | Ano | Ano, omezeno<br> Podporuje ucelenou diagnostiku a řešení potíží pouze pro místní infrastrukturu a aplikace. Používá jiné součásti softwaru System Center nebo Partnerská řešení.|
|Interaktivní vizualizace (řídicí panely) | Ano | Ano, omezeno<br> Poskytuje základní řídicí panely s webovou konzolou HTML5 nebo pokročilé prostředí z partnerských řešení, jako jsou například čtvercová a Savision. |
|Integrace s IT nebo DevOps nástroji | Ano | Ano, omezeno |

<!-- markdownlint-enable MD033 -->

### <a name="collect-and-stream-monitoring-data-to-third-party-or-on-premises-tools"></a>Shromažďování a streamování dat monitorování do třetích stran nebo místních nástrojů

Abyste mohli shromažďovat metriky a protokoly z prostředků infrastruktury a platforem Azure, musíte pro tyto prostředky povolit protokoly Azure Diagnostics. Kromě toho můžete pomocí virtuálních počítačů Azure shromáždit metriky a protokoly z hostovaného operačního systému tím, že povolíte rozšíření Azure Diagnostics. Pokud chcete data diagnostiky vysílaná z vašich prostředků Azure přesměrovat na vaše místní nástroje nebo poskytovatele spravované služby, nakonfigurujte [Event Hubs](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-stream-event-hubs) pro streamování dat.

### <a name="monitor-with-system-center-operations-manager"></a>Monitorování pomocí System Center Operations Manager

I když byl System Center Operations Manager původně navržený jako místní řešení pro monitorování napříč aplikacemi, úlohami a infrastrukturou, které běží ve vašem IT prostředí, vyvinula se tak, aby zahrnovala možnosti cloudového monitorování. Integruje se s Azure, Office 365 a Amazon Web Services (AWS). Dá se monitorovat napříč různými prostředími pomocí sad Management Pack, které jsou navržené a aktualizované pro jejich podporu.  

Pro zákazníky, kteří provedli významné investice do Operations Manager k zajištění komplexního monitorování, které je pevně integrovaná s jejich správa IT služeb procesy a nástroji nebo pro zákazníky, kteří jsou v Azure noví, je lepší položit následující postup: otázky

- Může Operations Manager nadále doručovat hodnoty a dělat obchodní smysl?
- Je vhodné, aby se funkce v Operations Manager správně vešly na naši IT organizaci?
- Integruje Operations Manager s Azure Monitor poskytování nákladově efektivního a komplexního monitorovacího řešení, které vyžadujeme?

Pokud jste už investovali do Operations Manager, nemusíte se soustředit na plánování migrace, abyste ho hned nahradili. S Azure nebo jinými poskytovateli cloudu, kteří existují jako rozšíření vaší vlastní místní sítě, Operations Manager můžou monitorovat virtuální počítače hosta a prostředky Azure, jako kdyby byly ve vaší podnikové síti. Tento přístup vyžaduje spolehlivé síťové připojení mezi vaší sítí a virtuální sítí Azure, která má dostatečnou šířku pásma.

K monitorování úloh, které běží v Azure, potřebujete:

- [Sada Management Pack pro Azure](https://www.microsoft.com/download/details.aspx?id=50013). Shromažďuje metriky výkonu vydávané službami Azure, jako jsou webové a pracovní role, Application Insights testy dostupnosti (webové testy), Azure Service Bus atd. Management Pack používá REST API Azure ke sledování dostupnosti a výkonu těchto prostředků. Některé typy služeb Azure nemají žádné metriky nebo předem definované monitory v sadě Management Pack, ale můžete je i nadále monitorovat prostřednictvím vztahů definovaných v sadě Management Pack pro zjištěné služby.

- [Sada Management Pack pro Azure SQL Database](https://www.microsoft.com/download/details.aspx?id=38829) pro monitorování dostupnosti a výkonu databází SQL Azure a serverů Azure SQL Database s využitím dotazů Azure REST API a T-SQL k SQL Server systémových zobrazení.

- Chcete-li monitorovat hostovaný operační systém a úlohy, které jsou spuštěny na virtuálním počítači, například SQL Server, IIS nebo Apache Tomcat, je třeba stáhnout a naimportovat Management Pack, který podporuje aplikaci, službu a operační systém.

Znalostní báze je definována v Management Pack, který popisuje, jak monitorovat jednotlivé závislosti a součásti. Sady Management Pack pro Azure vyžadují provedení sady konfiguračních kroků v Azure a Operations Manager před tím, než bude možné začít monitorovat tyto prostředky.

V aplikační vrstvě nabízí Operations Manager základní možnosti funkce Application Performance Monitoring pro některé starší verze rozhraní .NET a Java. Pokud některé aplikace v hybridním cloudovém prostředí fungují v režimu offline nebo v izolovaném režimu, tak, aby nemohly komunikovat s veřejnou cloudovou službou, Operations Manager funkce Application Performance Monitoring (APM) může být možnost životaschopná pro určité omezené scénáře. Pro aplikace, které neběží na starších platformách, ale jsou hostované místně i v jakémkoli veřejném cloudu, který umožňuje komunikaci přes bránu firewall (přímo nebo prostřednictvím proxy serveru) do Azure, použijte Azure Monitor Application Insights. Tato služba nabízí hloubkové monitorování na úrovni kódu s špičkovou podporou pro ASP.NET, ASP.NET Core, Java, JavaScript a Node. js.

Pro všechny webové aplikace, které lze oslovit externě, byste měli povolit typ syntetické transakce označované jako [monitorování dostupnosti]( https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability). Je důležité zjistit, jestli vaše aplikace nebo důležitý koncový bod HTTP/HTTPS, na kterém je vaše aplikace závislá, je k dispozici a reagovat. Díky monitorování dostupnosti Application Insights můžete spouštět testy z více datových center Azure a poskytnout přehled o stavu aplikace z globální perspektivy.

I když je Operations Manager schopný monitorovat prostředky, které jsou hostované v Azure, existuje několik výhod, jak zahrnout Azure Monitor, protože jeho síly přecházejí omezení v Operations Manager a můžou vytvořit silnou základnu pro Podpora případné migrace. Tady si projdeme každou z těchto silných a slabých stránek s naším doporučením, jak zahrnout Azure Monitor do strategie hybridního monitorování.  

#### <a name="disadvantages-of-using-operations-manager-by-itself"></a>Nevýhody použití Operations Manager sám sebou

- Analýza dat monitorování v Operations Manager se běžně provádí pomocí předem definovaných zobrazení, která jsou definovaná v sadách Management Pack, které máte přístup z konzoly, ze sestav služby SQL Server Reporting Services (SSRS) nebo vlastních zobrazení, která koncoví uživatelé vytvořili. Provádění ad-hoc analýz dat není možné v poli. Vytváření sestav Operations Manager je neflexibilní. Datový sklad, který poskytuje dlouhodobé uchovávání dat monitorování, není škálovatelný ani nefunguje správně. A odbornosti při psaní příkazů T-SQL, vývoj řešení Power BI nebo použití řešení třetích stran, je nutná k podpoře požadavků různých osoby v organizaci IT.

- Výstrahy v Operations Manager nepodporují složité výrazy nebo zahrnují logiku korelace. Aby se zabránilo snížení šumu, jsou výstrahy seskupené tak, aby zobrazovaly vztahy mezi nimi a identifikovaly jejich příčiny.

#### <a name="advantages-of-using-operations-manager-with-azure-monitor"></a>Výhody použití Operations Manager s Azure Monitor

- Azure Monitor je způsob, jak obejít omezení Operations Manager. Doplňuje Operations Manager databázi datového skladu shromažďováním důležitých dat o výkonu a protokolu. Azure Monitor zajišťuje lepší analýzu, výkon (při dotazování velkého objemu dat) a uchovávání dat než datový sklad Operations Manager. 

  Pomocí dotazovacího jazyka Azure Monitor můžete vytvářet mnohem složitější a sofistikované dotazy. Dotazy můžete spouštět v různých terabajtech dat během několika sekund. Data můžete rychle transformovat do výsečových grafů, časových grafů a mnoha dalších vizualizací. Pokud chcete tato data analyzovat, nebudete už omezeni tím, že pracujete se Operations Managermi sestavami, které jsou založené na SQL Server Reporting Services, vlastních dotazech SQL a dalších řešeních.

- Nasazením řešení pro správu výstrah Azure Monitor můžete zajistit vylepšené prostředí pro upozorňování. Výstrahy, které jsou generovány ve skupině pro správu Operations Manager, lze přeslat do pracovního prostoru Azure Monitorch Log Analytics. U předplatného, které zodpovídá za předávání výstrah z Operations Manager, můžete nakonfigurovat, aby se protokoly Azure Monitor předávaly jenom určitým výstrahám. Můžete například předávat jenom výstrahy, které splňují kritéria pro dotazování na podporu správy problémů při trendech, a zkoumání hlavní příčiny selhání nebo problémů přes jedno podokno skla. Kromě toho můžete vzájemně korelovat data protokolu z Application Insights nebo jiných zdrojů a získat tak přehled, který pomáhá vylepšit uživatelské prostředí, prodloužit dobu provozu a zkrátit čas na vyřešení incidentů.

- V Azure můžete monitorovat infrastrukturu a aplikace v cloudu, a to z jednoduché nebo vícevrstvé architektury v Azure. pomocí Operations Manager můžete monitorovat místní infrastrukturu. Toto monitorování zahrnuje jeden nebo více virtuálních počítačů, několik virtuálních počítačů umístěných do skupiny dostupnosti nebo sady škálování virtuálních počítačů nebo kontejnerové aplikace nasazené do služby Azure Kubernetes Service (AKS), která běží na kontejnerech Windows Server nebo Linux.

- Řešení System Center Operations Manager Health Check můžete použít k proaktivnímu vyhodnocení rizik a stavu skupiny pro správu System Center Operations Manager v pravidelných intervalech. Toto řešení může nahradit nebo doplnit jakékoli vlastní funkce, které jste přidali do skupiny pro správu.

- Pomocí funkce map Azure Monitor pro virtuální počítače můžete monitorovat metriky standardního připojení ze síťových připojení mezi virtuálními počítači Azure a místními virtuálními počítači. Tyto metriky zahrnují dobu odezvy, požadavky za minutu, propustnost provozu a odkazy. Můžete identifikovat neúspěšná připojení, řešit potíže, provádět ověřování migrace, provádět analýzu zabezpečení a ověřovat celou architekturu služby. Map může automaticky zjišťovat součásti aplikace v systémech Windows a Linux a namapovat komunikaci mezi službami. Tato automatizace vám pomůže identifikovat připojení a závislosti, které jste nevědomi, naplánovat a ověřit migraci do Azure a minimalizovat spekulací během řešení incidentů.

- Pomocí Network Performance Monitor můžete monitorovat síťové připojení mezi:

   - Vaše podniková síť a Azure.
   - Klíčové vysoce vícevrstvé aplikace a mikroslužby.
   - Uživatelská umístění a webové aplikace (HTTP/HTTPS).

   Tato strategie nabízí viditelnost síťové vrstvy bez nutnosti SNMP. Může také existovat v mapování interaktivní topologie, topologie směrování mezi segmenty směrování tras mezi zdrojovým a cílovým koncovým bodem. Je lepší volbou než pokus o provedení stejného výsledku s monitorováním sítě v Operations Manager nebo s dalšími nástroji pro monitorování sítě aktuálně používanými ve vašem prostředí.

### <a name="monitor-with-azure-monitor"></a>Monitorování pomocí služby Azure Monitor

I když migrace do cloudu představuje mnoho výzev, zahrnuje také řadu příležitostí. Umožňuje vaší organizaci migrovat z jednoho nebo několika místních nástrojů pro monitorování podniku nejen na to, aby mohly snižovat kapitálové výdaje a provozní náklady, ale také využil výhody výhod, které cloudová monitorovací platforma jako Azure Monitor může poskytovat škálování v cloudu. Projděte si požadavky na monitorování a výstrahy, konfiguraci existujících nástrojů pro monitorování a převeďte úlohy do cloudu. Po dokončení plánu nakonfigurujte Azure Monitor.

- Monitorujte hybridní infrastrukturu a aplikace z jednoduché nebo vícevrstvé architektury, kde se komponenty hostují mezi Azure, jinými poskytovateli cloudu a firemní sítí. Komponenty mohou zahrnovat jeden nebo více virtuálních počítačů, několik virtuálních počítačů umístěných ve skupině dostupnosti nebo sadě virtuálních počítačů nebo kontejnerové aplikace nasazené do služby Azure Kubernetes Service (AKS) spuštěné v kontejnerech systému Windows Server nebo Linux.

- Povolte Azure Monitor pro virtuální počítače, Azure Monitor pro kontejnery a Application Insights k detekci a diagnostikování problémů mezi infrastrukturou a aplikacemi. Pro důkladnější analýzu a korelaci dat shromážděných z více komponent nebo závislostí, které podporují aplikaci, je nutné použít protokoly Azure Monitor.

- Vytvářejte inteligentní výstrahy, které se můžou vztahovat na základní sadu aplikací a součástí služby, které vám pomůžou snížit šum s dynamickými prahovými hodnotami pro složité signály a využívat agregace výstrah založené na algoritmech strojového učení, které vám pomůžou rychle identifikovat chybu.

- Definujte knihovnu dotazů a řídicích panelů, které budou podporovat požadavky různých osoby v organizaci IT.

- Definujte standardy a metody pro povolení monitorování v rámci hybridních a cloudových prostředků, standardní hodnoty monitorování pro každý prostředek, prahové hodnoty výstrah a tak dále.  

- Nakonfigurujte řízení přístupu na základě role (RBAC), abyste uživatelům a skupinám udělili jenom množství přístupu, které potřebují k monitorování dat z prostředků, které zodpovídají za správu.

- Zahrnutí automatizace a samoobslužné služby, které umožní každému týmu vytvářet, aktivovat a ladit konfigurace monitorování a upozorňování podle potřeby.

## <a name="private-cloud-monitoring"></a>Monitorování privátního cloudu

Holistický sledování Azure Stack můžete dosáhnout pomocí System Center Operations Manager. Konkrétně můžete monitorovat úlohy spuštěné v tenantovi, na úrovni prostředků, na virtuálních počítačích a na hostování infrastruktury Azure Stack (fyzické servery a přepínače sítě). 

Můžete také dosáhnout holistický monitoring s kombinací [možností monitorování infrastruktury](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) , které jsou součástí Azure Stack. Tyto funkce vám pomůžou zobrazit stav a výstrahy Azure Stack oblasti a [služby Azure monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) v Azure Stack, které pro většinu služeb poskytují metriky a protokoly infrastruktury základní úrovně.

Pokud jste už investovali do Operations Manager, můžete k monitorování dostupnosti a stavu nasazení Azure Stack použít Management Pack Azure Stack. To zahrnuje oblasti, poskytovatele prostředků, aktualizace, běhy aktualizací, jednotky škálování, uzly jednotek, role infrastruktury a jejich instance (logické entity skládající se z hardwarových prostředků). K komunikaci s Azure Stack používá rozhraní REST API poskytovatele stavu a aktualizace. Pokud chcete monitorovat fyzické servery a úložná zařízení, použijte dodavatele OEM Management Pack (například poskytované Lenovo, Hewlett Packard nebo Dell). Operations Manager může nativně monitorovat síťové přepínače a shromažďovat základní statistiky pomocí protokolu SNMP. Monitorování zatížení klientů je možné u Management Pack Azure pomocí dvou základních kroků. Nakonfigurujte předplatné, které chcete monitorovat, a přidejte monitory pro toto předplatné.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Shromáždění správných dat](./data-collection.md)
