---
title: Vylepšený směrný plán správy v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Běžná vylepšení směrného plánu správy
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 85e289867ac69f3403d964078a7c3f3b2a6c96a7
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683700"
---
# <a name="enhanced-management-baseline-in-azure"></a>Vylepšený směrný plán správy v Azure

První tři disciplíny správy cloudu popisují směrný plán správy. Předchozí články v tomto průvodci představily minimální realizovatelný produkt pro služby správy cloudu, který se označuje jako směrný plán správy. V tomto článku si popíšeme několik běžných vylepšení tohoto směrného plánu.

Účelem směrného plánu správy je vytvořit konzistentní nabídku, která poskytuje minimální úroveň firemního závazku pro **všechny*** podporované úlohy. Tento směrný plán běžných opakovatelných nabídek správy umožňuje týmu, aby poskytoval vysoce optimalizovanou správu provozu s minimálními odchylkami. Někdy ale může být potřebný širší firemní závazek nad rámec standardní nabídky. Následující obrázek a odrážkový seznam ukazují tři možnosti rozšíření směrného plánu správy.

![Rozšíření směrného plánu správy cloudu](../../_images/manage/beyond-the-baseline.png)

- **Provoz úloh:**
  - Největší investice do provozu jednotlivých úloh.
  - Nejvyšší stupeň odolnosti.
  - Doporučuje se pro přibližně 20 % úloh, které vytvářejí největší obchodní hodnoty.
  - Obvykle je vyhrazené jenom pro nejdůležitější úlohy pro firmu.
- **Provoz platforem:**
  - Investice do provozu se rozloží mezi mnoho úloh.
  - Vylepšení odolnosti mají vliv na všechny úlohy, které využívají definovanou platformu.
  - Doporučuje se pro přibližně 20 % nejdůležitějších platforem.
  - Obvykle je vyhrazené pro úlohy střední až vysoké důležitosti.
- **Vylepšený směrný plán správy:**
  - Nejnižší relativní investice do provozu.
  - Mírně vylepšené firemní závazky pomocí dalších nástrojů a procesů pro nativní cloudové operace.

Pro provoz úloh i platforem budou potřebné změny v principech návrhu a architektury. Tyto změny můžou nějakou dobu trvat a můžou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení firemních závazků.

Následující tabulka popisuje několik běžných procesů, nástrojů a potenciálních dopadů ve vylepšených směrných plánech správy u zákazníků.

|Disciplína  |Proces  |Nástroj  |Potenciální dopad| Další informace |
|---------|---------|---------|---------|---------|
|Inventarizace a zajištění přehledu|Sledování změn služeb|Azure Resource Graph|Lepší přehled o změnách služeb Azure může pomoci dříve zjistit negativní dopady nebo rychleji zajistit nápravu.|[Přehled služby Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview)|
|Inventarizace a zajištění přehledu|Integrace správy IT služeb (ITSM)|IT Service Management Connector|Automatizované připojení ITSM může urychlit zjišťování.|[ITSM konektor pro Azure](https://docs.microsoft.com/azure/azure-monitor/platform/itsmc-overview)|
|Provozní dodržování předpisů|Automatizace operací|Azure Automation|Automatizace provozního dodržování předpisů umožňuje rychleji a přesněji reagovat na změny.|Viz níže|
|Provozní dodržování předpisů|Operace ve více cloudech|Azure Automation Hybrid Runbook Worker|Umožňuje automatizovat operace ve více cloudech.|[Přehled funkce Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)|
|Provozní dodržování předpisů|Automatizace hostů|Desired State Configuration (DSC)|Konfigurace operačních systémů hostů na základě kódu omezuje chyby a odchylky konfigurace.|[Přehled platformy DSC](/powershell/scripting/dsc/overview/overview)|
|Ochrana a zotavení|Oznámení o porušeních zabezpečení|Azure Security Center|Rozšířená ochrana zahrnuje triggery zotavení po porušeních zabezpečení.|Viz níže|

::: zone target="docs"

## <a name="azure-automation"></a>Azure Automation

::: zone-end
::: zone target="chromeless"

## <a name="azure-automationtabazureautomation"></a>[Azure Automation](#tab/AzureAutomation)

::: zone-end

Služba Azure Automation poskytuje centralizovaný systém pro správu automatizovaných kontrolních prvků. V Azure Automation je v reakci na metriky prostředí možné spustit jednoduché procesy nápravy, škálování a optimalizace. To snižuje režii související s manuální reakcí na incidenty. Nejdůležitější je, že automatizovanou nápravu je možné zajistit v téměř reálném čase, což výrazně snižuje přerušení firemních procesů. Studie nejběžnějších přerušení běžného chodu firmu bude identifikovat aktivity ve vašem prostředí, které by šlo automatizovat.

### <a name="runbooks"></a>Runbooky

Základní jednotkou kódu, který zajišťuje automatizovanou nápravu, je runbook. Runbooky obsahují instrukce pro nápravu nebo zotavení po incidentu.

Pokud chcete vytvářet nebo spravovat runbooky:

1. Přejděte do služby [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Vyberte jeden z uvedených **účtů služby Automation**.
3. V navigaci na portálu najděte oddíl **Automatizace procesu**.
4. Možnosti v tomto oddílu umožňují vytvářet nebo spravovat runbooky, plány a další funkce automatizované nápravy.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
::: zone target="docs"

## <a name="azure-security-center"></a>Azure Security Center

::: zone-end
::: zone target="chromeless"

## <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

::: zone-end

Důležitou roli ve strategii ochrany a zotavení hraje také Azure Security Center. Pomůže vám monitorovat zabezpečení počítačů, sítí, úložišť, datových služeb a aplikací. Azure Security Center poskytuje rozšířenou detekci hrozeb s využitím strojového učení a behaviorální analýzy, která pomáhá identifikovat aktivní hrozby cílené na vaše prostředky Azure. Poskytuje také ochranu před hrozbami, která blokuje malware a jiný nežádoucí kód a omezuje možnosti útoku hrubou silou a jiných síťových útoků.

Když Azure Security Center zjistí nějakou hrozbu, aktivuje výstrahu zabezpečení s kroky, které je potřeba udělat jako reakci na útok. Poskytne také zprávu s informacemi o zjištěné hrozbě.

Azure Security Center se nabízí ve dvou úrovních: Free a Standard. Funkce jako doporučení k zabezpečení jsou k dispozici na bezplatné úrovni Free. Úroveň Standard nabízí dodatečnou ochranu, jako je rozšířená detekce hrozeb a ochrana pro všechny hybridní cloudové úlohy.

::: zone target="chromeless"

### <a name="action"></a>Akce

**Vyzkoušejte úroveň Standard na prvních 30 dnů zdarma.**

Po povolení a konfiguraci zásad zabezpečení pro prostředky předplatného můžete v části **Prevence** zobrazit stav zabezpečení vašich prostředků a případné problémy. Seznam těchto problémů můžete zobrazit také na dlaždici **Doporučení**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Pokud chcete prozkoumat Azure Security Center, přejděte na web [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

### <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end