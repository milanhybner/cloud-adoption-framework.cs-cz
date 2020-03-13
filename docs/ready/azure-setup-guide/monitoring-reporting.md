---
title: Monitorování a generování sestav v Azure
description: Pomocí architektury přechodu na cloud pro Azure zjistěte, jak u prostředí pro správu Azure nastavit monitorování, generování sestav a upozornění.
author: timleyden
ms.author: tileyden
ms.date: 04/09/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 1a45fda645231dcd9548c770dee0afd19b8df30c
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093535"
---
<!-- cSpell:ignore timleyden tileyden -->

# <a name="monitoring-and-reporting-in-azure"></a>Monitorování a generování sestav v Azure

Azure nabízí řadu služeb, které společně poskytují komplexní řešení pro shromažďování dat, analýzy a akce na základě telemetrie z vašich aplikací a prostředků Azure, které je podporují. Navíc jde tyto služby rozšířit na monitorování důležitých místních prostředků s cílem poskytovat prostředí hybridního monitorování.

# <a name="azure-monitor"></a>[Azure Monitor](#tab/AzureMonitor)

Azure Monitor poskytuje jedno společné centrum pro všechna data monitorování a diagnostiky v Azure. Můžete ho použít k získání přehledu o prostředcích. Pomocí Azure Monitoru můžete najít a vyřešit problémy a optimalizovat výkon. Můžete také pochopit chování zákazníků.

- **Monitorování a vizualizace metrik.** Metriky jsou číselné hodnoty dodávané prostředky Azure, které nabízejí informace o stavu vašich systémů. Grafy můžete přizpůsobit pro řídicí panely a ke generování sestav používat sešity.

- **Dotazování a analýza protokolů.** Mezi protokoly patří protokoly aktivit a diagnostické protokoly z Azure. Shromažďujte další protokoly pro vaše cloudové nebo místní prostředky z jiných řešení pro monitorování a správu. Log Analytics slouží jako centrální úložiště pro agregaci všech těchto dat. Odtud můžete spouštět dotazy, které vám pomůžou řešit potíže nebo vizualizovat data.

- **Nastavení upozornění a akcí.** Upozornění vás aktivně informují o kritických stavech. Na základě triggerů z metrik, protokolů nebo problémů se stavem služby je možné provádět opravné akce. Můžete nastavit různá oznámení a akce a odesílat data do vašich nástrojů pro správu IT služeb.

::: zone target="docs"

 Zahájení monitorování pro:

- [Aplikace](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Containers](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Virtual Machines](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Sítě](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Pokud chcete monitorovat jiné prostředky, vyhledejte další řešení na webu Azure Marketplace.

Pokud chcete prozkoumat Azure Monitor, přejděte na [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

## <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

## <a name="action"></a>Akce

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

::: zone-end

# <a name="azure-service-health"></a>[Azure Service Health](#tab/AzureServiceHealth)

Azure Service Health poskytuje přizpůsobené zobrazení stavu služeb a oblastí Azure, které využíváte. Informace o aktivních problémech se odešle do služby Service Health, aby vám pomohla porozumět dopadu na vaše prostředky. Pravidelné aktualizace vám umožní sledovat, jak se problém řeší.

Publikujeme do Service Health také události plánované údržby, takže se dozvíte o změnách, které by mohly ovlivnit dostupnost vašich prostředků. Po nastavení upozornění služby Service Health můžete být informováni o problémech služby, plánované údržbě nebo dalších změnách, které mohou mít vliv na používané služby a oblasti Azure.

Azure Service Health zahrnuje:

- **Stav Azure:** Globální přehled o stavu služeb Azure
- **Stav služeb:** Přizpůsobený přehled o stavu vašich služeb Azure
- **Stav prostředků:** Podrobnější přehled o stavu jednotlivých prostředků

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

## <a name="action"></a>Akce

Vytvoření upozornění služby Service Health:

1. Přejděte do služby **Service Health**.
2. Vyberte **Upozornění na stav**.
3. Vytvořte upozornění na stav služby.

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

Pokud chcete nastavit upozornění služby Service Health, přejděte na [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

## <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Service Health](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisor"></a>[Azure Advisor](#tab/AzureAdvisor)

Azure Advisor je bezplatný přizpůsobený cloudový konzultant, který pomáhá dodržovat a implementovat osvědčené postupy pro nasazení Azure. Analyzuje telemetrii využití a konfiguraci vašich prostředků a následně doporučí řešení, která mohou pomoci optimalizovat vaše prostředí. Doporučení se dělí do následujících kategorií:

- **Vysoká dostupnost:** Jsou určená ke zlepšení kontinuity vašich aplikací pro důležité obchodní informace. Příkladem doporučení může být přidání virtuálních počítačů do skupiny dostupnosti nebo přidání geograficky redundantních koncových bodů.
- **Zabezpečení:** Jsou určená k detekci hrozeb a ohrožení zabezpečení, která můžou vést k porušením zabezpečení. Příkladem doporučení může být použití šifrování disků nebo povolení skupin zabezpečení sítě.
- **Výkon:** Jsou určená ke zrychlení vašich aplikací. Příkladem doporučení může být zvýšení výkonu dotazů SQL vytvořením indexů nebo změna konfigurace nastavení Traffic Manageru.
- **Náklady:** Jsou určená k optimalizaci a snížení celkové útraty za Azure. Příkladem doporučení může být změna velikosti nebo vypnutí nevyužitých virtuálních počítačů nebo přepnutí na Azure Reservations kvůli snížení celkových nákladů na vlastnictví.
- **Efektivita provozu:** Jsou určená ke zlepšení možností správy a efektivity procesů a pracovních postupů. Doporučení mohou zahrnovat nastavení a vynucení pravidel Azure Policy, opravy neplatných pravidel upozornění protokolů a konfiguraci upozornění služby Azure Service Health.

Doporučení v Advisoru jsou založená na nasazených prostředcích a provedených akcích v Azure. V Advisoru můžete pravidelně kontrolovat nejnovější doporučení.

::: zone target="chromeless"

## <a name="action"></a>Akce

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Explore Azure Advisor" :::

::: zone-end

::: zone target="docs"

Pokud chcete prozkoumat Azure Advisor, přejděte na [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Expert/AdvisorBlade).

## <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci k Azure Advisoru](https://docs.microsoft.com/azure/advisor).

::: zone-end

# <a name="azure-security-center"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Důležitou roli ve strategii monitorování hraje také Azure Security Center. Pomůže vám monitorovat zabezpečení počítačů, sítí, úložišť, datových služeb a aplikací. Security Center poskytuje rozšířenou detekci hrozeb s využitím strojového učení a behaviorální analýzy, která pomáhá identifikovat aktivní hrozby cílené na vaše prostředky Azure. Poskytuje také ochranu před hrozbami, která blokuje malware a jiný nežádoucí kód a omezuje možnosti útoku hrubou silou a jiných síťových útoků.

Když Security Center zjistí nějakou hrozbu, aktivuje výstrahu zabezpečení s kroky, které je potřeba udělat jako reakci na útok. Poskytne také zprávu s informacemi o zjištěné hrozbě.

Azure Security Center se nabízí ve dvou úrovních: Free a Standard. Funkce jako doporučení k zabezpečení jsou k dispozici bezplatně. Úroveň Standard nabízí dodatečnou ochranu, jako je rozšířená detekce hrozeb a ochrana pro všechny hybridní cloudové úlohy.

::: zone target="chromeless"

## <a name="action"></a>Akce

**Vyzkoušejte úroveň Standard na prvních 30 dnů zdarma.**

Po zapnutí a nastavení zásad zabezpečení pro prostředky předplatného můžete v části **Prevence** zobrazit stav zabezpečení vašich prostředků a případné problémy. Seznam těchto problémů můžete zobrazit také na dlaždici **Doporučení**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Pokud chcete prozkoumat Azure Security Center, přejděte na web [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
