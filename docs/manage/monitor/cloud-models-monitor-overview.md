---
title: Průvodce monitorováním cloudu – strategie monitorování pro modely nasazení v cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vyberte, kdy použít Azure Monitor nebo System Center Operations Manager v Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: badf03f3616de8e6612221282aa24996f0b6e8f8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221124"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Průvodce monitorováním cloudu: Strategie monitorování pro modely nasazení v cloudu

Tento článek zahrnuje naši doporučenou strategii monitorování pro všechny modely nasazení v cloudu, a to na základě následujících kritérií:

- Budete potřebovat pokračující závazek na Operations Manager nebo jinou podnikovou platformu pro monitorování. Důvodem je integrace s vašimi procesy IT, znalostmi a odbornými znalostmi nebo vzhledem k tomu, že některé funkce nejsou v Azure Monitor ještě k dispozici.
- Musíte monitorovat úlohy místně i ve veřejném cloudu nebo jenom v cloudu.
- Vaše strategie migrace do cloudu zahrnuje modernizaci IT operace a přechod na naše služby a řešení Cloud monitoring.
- Je možné, že máte důležité systémy, které jsou gapped nebo fyzicky izolované, hostované v privátním cloudu nebo na fyzickém hardwaru a je třeba je monitorovat.

Naše strategie zahrnuje podporu pro monitorování infrastruktury (výpočetní prostředky, úložiště a zatížení serveru), aplikaci (koncového uživatele, výjimky a klienta) a síťové prostředky k zajištění kompletní perspektivy monitorování orientované na služby.

## <a name="azure-cloud-monitoring"></a>Monitorování cloudu Azure

Azure Monitor je služba platformy, která poskytuje jeden zdroj pro monitorování prostředků Azure. Je navržená pro cloudová řešení, která jsou založená na Azure a která podporují obchodní funkce založené na úlohách virtuálních počítačů nebo složitých architekturách, které používají mikroslužby a další prostředky platforem. Monitoruje všechny vrstvy zásobníku počínaje službami tenanta, jako jsou Azure Active Directory Domain Services, události na úrovni předplatného a Azure Service Health. Monitoruje také prostředky infrastruktury, jako jsou virtuální počítače, úložiště a síťové prostředky, a v horní vrstvě aplikace. Monitorování každé z těchto závislostí a shromáždění správných signálů, které mohou vysílat, poskytují přehled o tom, jaké aplikace a jaká klíčová infrastruktura potřebujete.

Následující tabulka shrnuje doporučený postup pro monitorování jednotlivých vrstev zásobníku.

<!-- markdownlint-disable MD033 -->

Vrstva | Resource | Scope | Metoda
---|---|---|----
Aplikace | Webová aplikace běžící na platformě .NET, .NET Core, Java, JavaScriptu a Node. js na virtuálním počítači Azure, App Services Azure, Service Fabric Azure, Azure Functions a Azure Cloud Services | Monitorujte živou webovou aplikaci, aby automaticky zjišťoval anomálie v oblasti výkonu, identifikovala výjimky a problémy kódu a shromáždila telemetrii použitelnosti. |  Application Insights
Containers | Služba Azure Kubernetes/Azure Container Instances | Sledujte kapacitu, dostupnost a výkon úloh běžících na kontejnerech a instancích kontejnerů. | Azure Monitor pro kontejnery
Hostovaný operační systém | Operační systém Linux a Windows VM | Sledujte kapacitu, dostupnost a výkon. Mapování závislostí hostovaných na každém virtuálním počítači, včetně viditelnosti aktivních síťových připojení mezi servery, latencí příchozího a odchozího připojení a portů v rámci libovolné architektury připojené k protokolu TCP. | Azure Monitor pro virtuální počítače
Prostředky Azure – PaaS | Azure Database Services (například SQL nebo mySQL) | Metriky výkonu Azure Database for SQL. | Povolí protokolování diagnostiky pro streamování dat SQL pro Azure Monitor protokolů.
Prostředky Azure – IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. Azure Key Vault<br/> 4. Skupiny zabezpečení sítě<br/> 5. Azure Traffic Manager | 1. Kapacita, dostupnost a výkon.<br/> 2. Protokoly výkonu a diagnostiky (aktivita, přístup, výkon a brána firewall).<br/> 3. Sledujte, jak a kdy jsou k vašim trezorům klíčů přistupované a kým.<br/> 4. Sledujte události při použití pravidel a čítač pravidla, kolikrát se pravidlo použije pro zamítnutí nebo povolení.<br/>5. Monitoruje dostupnost stavu koncového bodu. | 1. Metriky úložiště pro úložiště objektů BLOB.<br/> 2. Povolte protokolování diagnostiky a nakonfigurujte streamování na protokoly Azure Monitor.<br/> 3. Povolte protokolování diagnostiky, nakonfigurujte streamování do Azure Monitor protokolů a povolte [řešení Azure Key Vault Analytics](https://docs.microsoft.com/azure/azure-monitor/insights/azure-key-vault). <br/> 4. Povolte diagnostické protokolování skupin zabezpečení sítě a nakonfigurujete streamování na protokoly Azure Monitor.<br/> 5. Povolte protokolování diagnostiky koncových bodů Traffic Manager a nakonfigurujte streamování na Azure Monitor protokoly.
Síť| Komunikace mezi virtuálním počítačem a jedním nebo více koncovými body (jiný virtuální počítač, plně kvalifikovaný název domény, identifikátor URI nebo adresa IPv4). | Sledujte dostupnost, latenci a změny topologie sítě, ke kterým dochází mezi virtuálním počítačem a koncovým bodem. | Azure Network Watcher
Předplatné Azure | Stav služby Azure a základní stav prostředků | <li> Akce správy prováděné u služby nebo prostředku.<br/><li> Stav služby se službou Azure je v nedostupném stavu.<br/><li> Zjistili jsme problémy se stavem prostředku Azure z hlediska služby Azure.<br/><li> Operace prováděné s Azure Autoscale indikují chybu nebo výjimku. <br/><li> Operace prováděné s Azure Policy označují, že došlo k povolené nebo odepřené akci.<br/><li> Záznam upozornění generovaných Azure Security Center. |Doručit v protokolu aktivit za účelem monitorování a upozorňování pomocí Azure Resource Manager.
Tenant Azure|Azure Active Directory || Povolte protokolování diagnostiky a nakonfigurujete streamování na Azure Monitor protokoly.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Monitorování hybridního cloudu

V tuto chvíli probíhá vývoj, aby bylo možné doručovat komplexní sadu doporučení, která řeší váš zájem o tento cloudový model a která bude brzy k dispozici.  

## <a name="private-cloud-monitoring"></a>Monitorování privátního cloudu

Holistický sledování Azure Stack můžete dosáhnout pomocí System Center Operations Manager. Konkrétně můžete monitorovat úlohy spuštěné v tenantovi, na úrovni prostředků, na virtuálních počítačích a na hostování infrastruktury Azure Stack (fyzické servery a přepínače sítě). Můžete také dosáhnout holistický monitoring s kombinací [možností monitorování infrastruktury](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) , které jsou součástí Azure Stack. Tyto funkce vám pomůžou zobrazit stav a výstrahy Azure Stack oblasti a [služby Azure monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) v Azure Stack, které pro většinu služeb poskytují metriky a protokoly infrastruktury základní úrovně.

Pokud jste už investovali do Operations Manager, můžete k monitorování dostupnosti a stavu nasazení Azure Stack použít Management Pack Azure Stack. To zahrnuje oblasti, poskytovatele prostředků, aktualizace, běhy aktualizací, jednotky škálování, uzly jednotek, role infrastruktury a jejich instance (logické entity skládající se z hardwarových prostředků). K komunikaci s Azure Stack používá rozhraní REST API poskytovatele stavu a aktualizace. Pokud chcete monitorovat fyzické servery a úložná zařízení, použijte dodavatele OEM Management Pack (například poskytované Lenovo, Hewlett Packard nebo Dell). Operations Manager může nativně monitorovat síťové přepínače a shromažďovat základní statistiky pomocí protokolu SNMP. Monitorování zatížení klientů je možné u Management Pack Azure pomocí dvou základních kroků. Nakonfigurujte předplatné, které chcete monitorovat, a přidejte monitory pro toto předplatné.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Shromažďování správných dat](./data-collection.md)
