---
title: Ukázkové příkazy zásad standardních hodnot zabezpečení
description: Tyto ukázkové příkazy zásad standardních hodnot zabezpečení vám pomůžou v konceptech příkazů zásad, které řeší potřeby vaší organizace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 34135a7bb0a6fb97895bde3b002426f37c0f53fd
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425948"
---
# <a name="security-baseline-sample-policy-statements"></a>Ukázkové příkazy zásad standardních hodnot zabezpečení

Jednotlivé příkazy zásad cloudu jsou pokyny pro řešení konkrétních rizik zjištěných během procesu posouzení rizik. Tyto příkazy by měly poskytnout stručné shrnutí rizik a plánů, které je třeba řešit. Každá definice příkazu by měla obsahovat tyto informace:

- **Technické riziko:** Souhrn rizika, které tato zásada bude řešit.
- **Prohlášení o zásadách:** Jasné souhrnné vysvětlení požadavků zásad.
- **Technické možnosti:** Užitečná doporučení, specifikace nebo další pokyny, které mohou týmy IT a vývojáři použít při implementaci těchto zásad.

Následující vzorové příkazy zásad řeší běžná obchodní rizika související se zabezpečením. Tyto příkazy jsou příklady, na které můžete odkazovat při konceptech příkazů zásad, které řeší potřeby vaší organizace. Tyto příklady se nepovažují za podrobné a některé možnosti zásad se týkají každého identifikovaného rizika. Pracujte úzce se společnostmi, zabezpečením a týmy IT a Identifikujte nejlepší zásady pro Vaši jedinečnou sadu rizik.

## <a name="asset-classification"></a>Klasifikace prostředků

**Technické riziko:** Prostředky, které nejsou správně identifikované jako kritické nebo které obsahují citlivá data, nemusí přijímat dostatečné ochrany, což vede k potenciálním únikům dat nebo výpadkům v podniku.

**Prohlášení o zásadách:** Všechny nasazené prostředky musí být rozdělené do kategorií podle závažnosti a klasifikace dat. Klasifikace musí být přezkoumány týmem zásad správného řízení cloudu a vlastníkem aplikace před nasazením do cloudu.

**Potenciální možnost návrhu:** Stanovte [standardy označování prostředků](../../decision-guides/resource-tagging/index.md) a zajistěte, aby je zaměstnanci oddělení IT konzistentně použili u všech nasazených prostředků pomocí [značek prostředků Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="data-encryption"></a>Šifrování dat

**Technické riziko:** Existuje riziko, že chráněná data se během úložiště zveřejňují.

**Prohlášení o zásadách:** Všechna chráněná data musí být v klidovém stavu zašifrovaná.

**Potenciální možnost návrhu:** V článku [Přehled šifrování Azure](https://docs.microsoft.com/azure/security/security-azure-encryption-overview) najdete diskuzi o tom, jak se na platformě Azure provádějí šifrování na základě dat. Také je potřeba vzít v úvahu další ovládací prvky, jako je například šifrování dat a kontrola nad tím, jak lze změnit nastavení účtu úložiště.

## <a name="network-isolation"></a>Izolace sítě

**Technické riziko:** Připojení mezi sítěmi a podsítěmi v rámci sítí přináší potenciální ohrožení zabezpečení, které může vést k úniku dat nebo přerušení služeb důležitých pro klíčové služby.

**Prohlášení o zásadách:** Podsítě sítě obsahující chráněná data musí být izolované od všech ostatních podsítí. Síťový provoz mezi podsítěmi chráněných dat je třeba pravidelně auditovat.

**Potenciální možnost návrhu:** V Azure se izolace sítě a podsítě spravují prostřednictvím [Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

## <a name="secure-external-access"></a>Zabezpečený externí přístup

**Technické riziko:** Povolení přístupu k úlohám z veřejného Internetu představuje riziko vniknutí v důsledku neoprávněného vystavení dat nebo narušení podniku.

**Prohlášení o zásadách:** K žádné podsíti obsahující chráněná data se dá přímo získat přímý pøístup přes veřejné Internet nebo přes datová centra. Přístup k těmto podsítím musí být směrován prostřednictvím zprostředkujících podsítí. Veškerý přístup k těmto podsítím se musí nacházet prostřednictvím řešení brány firewall schopnýho provádět funkce kontroly a blokování paketů.

**Potenciální možnost návrhu:** V Azure Zabezpečte veřejné koncové body nasazením [DMZ mezi veřejným internetem a vaší cloudovou sítí](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Zvažte nasazení, konfiguraci a automatizaci [Azure firewall](https://docs.microsoft.com/azure/firewall).

## <a name="ddos-protection"></a>Ochrana před útoky DDoS

**Technické riziko:** K distribuovaným útokům DOS (Denial of Service) může dojít v případě výpadku.

**Prohlášení o zásadách:** Nasaďte automatizované mechanismy pro zmírnění DDoS do všech veřejně přístupných koncových bodů sítě. Žádný veřejný web, na který se IaaS, by neměl být vystavený pro Internet bez DDoS.

**Potenciální možnost návrhu:** [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) Standard můžete použít k minimalizaci výpadků způsobených útoky DDoS.

## <a name="secure-on-premises-connectivity"></a>Zabezpečené místní připojení

**Technické riziko:** Nešifrovaný provoz mezi vaší cloudovou sítí a místním prostředím přes veřejný Internet je zranitelný vůči zachytávání a představuje riziko úniku dat.

**Prohlášení o zásadách:** Všechna připojení mezi místními a cloudovou sítí musí probíhat buď prostřednictvím zabezpečeného šifrovaného připojení VPN nebo vyhrazeného privátního propojení WAN.

**Potenciální možnost návrhu:** V Azure použijte ExpressRoute nebo Azure VPN k vytvoření privátního připojení mezi místními a cloudovou sítí.

## <a name="network-monitoring-and-enforcement"></a>Monitorování a vynucování sítě

**Technické riziko:** Změny konfigurace sítě mohou vést k novým chybám zabezpečení a rizikům při expozici dat.

**Prohlášení o zásadách:** Nástroje zásad správného řízení musí auditovat a vymáhat požadavky na konfiguraci sítě definované týmem standardních hodnot zabezpečení.

**Potenciální možnost návrhu:** V Azure se síťová aktivita dá monitorovat pomocí [azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)a [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-network-recommendations) může pomoci identifikovat slabá místa zabezpečení. Azure Policy umožňuje omezit síťové prostředky a zásady konfigurace prostředků v závislosti na omezeních definovaných týmem zabezpečení.

## <a name="security-review"></a>Kontrola zabezpečení

**Technické riziko:** V průběhu času vzroste nové bezpečnostní hrozby a typy útoků a zvyšuje riziko vystavení nebo přerušení vašich cloudových prostředků.

**Prohlášení o zásadách:** Díky trendům a potenciálním útokům, které by mohly mít vliv na nasazení v cloudu, je třeba pravidelně kontrolovat bezpečnostní tým, aby poskytoval aktualizace nástroje pro základní hodnoty zabezpečení používané v cloudu.

**Potenciální možnost návrhu:** Navažte běžnou schůzku kontroly zabezpečení, která zahrnuje relevantní členy týmu IT a zásad správného řízení. Projděte si stávající data a metriky zabezpečení a zaveďte mezery v aktuálních zásadách a nástrojích pro základní hodnoty zabezpečení a aktualizujte zásady tak, aby opravily všechna nová rizika. Využijte [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) a [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) k získání užitečných přehledů o nově vznikajících hrozbách, které jsou specifické pro vaše nasazení.

## <a name="next-steps"></a>Další kroky

Použijte ukázky uvedené v tomto článku jako výchozí bod pro vývoj zásad, které řeší konkrétní bezpečnostní rizika, která odpovídají vašim plánům pro přijetí v cloudu.

Pokud chcete začít vyvíjet vlastní příkazy zásad týkající se standardních hodnot zabezpečení, Stáhněte si [šablonu standardních hodnot zabezpečení](./template.md).

Pokud chcete zrychlit přijetí této disciplíny, vyberte [akčního Průvodce zásad správného řízení](../guides/index.md) , který nejlépe zarovnává vaše prostředí. Pak upravte návrh tak, aby zahrnoval konkrétní podniková rozhodnutí o zásadách.

Sestavování rizik a tolerance, zavedení procesu řízení a komunikace s dodržováním zásad standardních hodnot zabezpečení.

> [!div class="nextstepaction"]
> [Vytváření procesů dodržování zásad](./compliance-processes.md)
