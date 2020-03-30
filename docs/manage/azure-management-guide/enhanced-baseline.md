---
title: Vylepšený směrný plán správy v Azure
description: Využijte architekturu přechodu na cloud pro Azure k pochopení běžných vylepšení směrného plánu správy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 223d6bf040987b7266d284d9175b588d08806c9f
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356517"
---
<!-- cSpell:ignore ITSMC -->

# <a name="enhanced-management-baseline-in-azure"></a>Vylepšený směrný plán správy v Azure

První tři disciplíny správy cloudu popisují směrný plán správy. Předchozí články v tomto průvodci představily minimální realizovatelný produkt pro služby správy cloudu, který se označuje jako směrný plán správy. V tomto článku si popíšeme několik běžných vylepšení tohoto směrného plánu.

Účelem směrného plánu správy je vytvořit konzistentní nabídku, která poskytuje minimální úroveň firemního závazku pro *všechny* podporované úlohy. Tento směrný plán běžných opakovatelných nabídek správy umožňuje týmu, aby poskytoval vysoce optimalizovanou správu provozu s minimálními odchylkami.

Někdy ale může být potřebný širší firemní závazek nad rámec standardní nabídky. Následující obrázek a seznam ukazují tři možnosti rozšíření směrného plánu správy.

![Rozšíření směrného plánu správy cloudu](../../_images/manage/beyond-the-baseline.png)

- **Provoz úloh:**
  - Největší investice do provozu jednotlivých úloh.
  - Nejvyšší stupeň odolnosti.
  - Doporučuje se pro přibližně 20 % úloh, které vytvářejí největší obchodní hodnoty.
  - Obvykle je vyhrazené jenom pro nejdůležitější úlohy pro firmu.
- **Provoz platforem:**
  - Investice do provozu se rozloží mezi mnoho úloh.
  - Vylepšení odolnosti mají vliv na všechny úlohy, které využívají definovanou platformu.
  - Doporučují se pro přibližně 20 % platforem, které jsou nejdůležitější.
  - Obvykle je vyhrazené pro úlohy střední až vysoké důležitosti.
- **Vylepšený směrný plán správy:**
  - Nejnižší relativní investice do provozu.
  - Mírně vylepšené firemní závazky pomocí dalších nástrojů a procesů pro nativní cloudové operace.

Pro provoz úloh i platforem budou potřebné změny v principech návrhu a architektury. Tyto změny mohou nějakou dobu trvat a mohou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení firemních závazků.

Tato tabulka ukazuje několik běžných procesů, nástrojů a potenciálních dopadů ve vylepšených směrných plánech správy u zákazníků.

| Disciplína  | Proces  | Nástroj | Potenciální dopad | Další informace |
|---|---|---|---|---|
|Inventarizace a zajištění přehledu|Sledování změn služeb|Azure Resource Graph|Lepší přehled o změnách služeb Azure napomáhá dřívějšímu zjištění negativních dopadů a rychlejšímu zajištění nápravy.|[Přehled služby Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview)|
|Inventarizace a zajištění přehledu|Integrace správy IT služeb (ITSM)|IT Service Management Connector|Automatizované připojení ITSM může urychlit zjišťování.|[ITSM konektor (ITSMC)](https://docs.microsoft.com/azure/azure-monitor/platform/itsmc-overview)|
|Provozní dodržování předpisů|Automatizace operací|Azure Automation|Automatizace provozního dodržování předpisů umožňuje rychleji a přesněji reagovat na změny.|Projděte si následující oddíly:|
|Provozní dodržování předpisů|Operace ve více cloudech|Azure Automation Hybrid Runbook Worker|Umožňuje automatizovat operace ve více cloudech.|[Přehled funkce Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)|
|Provozní dodržování předpisů|Automatizace hostů| Konfigurace požadovaného stavu (DSC)|Konfigurace operačních systémů hostů na základě kódu omezuje chyby a odchylky konfigurace.|[Přehled platformy DSC](https://docs.microsoft.com/powershell/scripting/dsc/overview/overview)|
|Ochrana a zotavení|Oznámení o porušeních zabezpečení|Azure Security Center|Rozšířená ochrana zahrnuje triggery zotavení po porušeních zabezpečení.|Projděte si následující oddíly:|

::: zone target="docs"

## <a name="azure-automation"></a>Azure Automation

::: zone-end
::: zone target="chromeless"

## <a name="azure-automation"></a>[Azure Automation](#tab/AzureAutomation)

::: zone-end

Služba Azure Automation poskytuje centralizovaný systém pro správu automatizovaných kontrolních prvků. Ve službě Azure Automation je v reakci na metriky prostředí možné spustit jednoduché procesy nápravy, škálování a optimalizace. Tyto procesy snižují režii související s manuálním zpracováním incidentů.

Nejdůležitější je, že automatizovanou nápravu je možné zajistit v téměř reálném čase, což výrazně snižuje přerušení firemních procesů. Studie nejběžnějších přerušení běžného chodu firmu identifikuje aktivity ve vašem prostředí, které by šlo automatizovat.

### <a name="runbooks"></a>Runbooky

Základní jednotkou kódu pro zajištění automatizované nápravy je runbook. Runbooky obsahují instrukce pro nápravu nebo zotavení po incidentu.

Pokud chcete vytvářet nebo spravovat runbooky:

1. Přejděte do služby [Azure Automation](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Vyberte **Účty služby Automation** a zvolte jeden z uvedených účtů.
1. Přejděte na **Automatizaci procesů**.
1. Uvedené možnosti umožňují vytvářet nebo spravovat runbooky, plány a další funkce automatizované nápravy.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
::: zone target="docs"

## <a name="azure-security-center"></a>Azure Security Center

::: zone-end
::: zone target="chromeless"

## <a name="azure-security-center"></a>[Azure Security Center](#tab/AzureSecurityCenter)

::: zone-end

Důležitou roli ve strategii ochrany a zotavení hraje také Azure Security Center. Pomůže vám monitorovat zabezpečení počítačů, sítí, úložišť, datových služeb a aplikací.

Azure Security Center poskytuje rozšířenou detekci hrozeb s využitím strojového učení a behaviorální analýzy, která pomáhá identifikovat aktivní hrozby cílené na vaše prostředky Azure. Poskytuje také ochranu před hrozbami, která blokuje malware a jiný nežádoucí kód a omezuje možnosti útoku hrubou silou a jiných síťových útoků.

Když Azure Security Center zjistí nějakou hrozbu, aktivuje výstrahu zabezpečení s kroky, které je potřeba v rámci reakce na tento útok udělat. Poskytne také zprávu s informacemi o zjištěné hrozbě.

Azure Security Center se nabízí ve dvou úrovních: Free a Standard. Funkce jako doporučení k zabezpečení jsou k dispozici na bezplatné úrovni Free. Úroveň Standard nabízí dodatečnou ochranu, jako je rozšířená detekce hrozeb a ochrana pro všechny hybridní cloudové úlohy.

::: zone target="chromeless"

### <a name="action"></a>Akce

#### <a name="try-standard-tier-for-free-for-your-first-30-days"></a>Vyzkoušejte úroveň Standard na prvních 30 dnů zdarma

Po povolení a konfiguraci zásad zabezpečení pro prostředky předplatného můžete v podokně **Prevence** zobrazit stav zabezpečení vašich prostředků a případné problémy. Seznam těchto problémů můžete zobrazit také na dlaždici **Doporučení**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Pokud chcete prozkoumat Azure Security Center, přejděte na web [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

### <a name="learn-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
