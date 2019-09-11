---
title: Zabezpečení a správa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zabezpečení a správa
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7d742242f2639708914927aedbf45d1c59020c7d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818723"
---
# <a name="secure-and-manage"></a>Zabezpečení a správa

Po migraci prostředí do Azure je důležité zvážit zabezpečení a metody používané pro správu prostředí. Azure poskytuje mnoho funkcí a možností, které těmto potřebám ve vašem řešení odpovídají.

# <a name="azure-monitortabmonitor"></a>[Azure Monitor](#tab/monitor)

Azure Monitor maximalizuje dostupnost a výkon vašich aplikací tím, že poskytuje ucelené řešení pro shromažďování, analýzu a telemetrii z vašich cloudových a místních prostředí. Pomůže vám při zjišťování stavu vašich aplikací a proaktivně identifikuje problémy, které je ovlivňují, a prostředky, na kterých jsou závislé.

## <a name="use-and-configure-azure-monitor"></a>Použití a konfigurace služby Azure Monitor

1. Na webu Azure Portal přejděte na **Sledovat**.
2. Pro přehledy vyberte **Metriky**, **Protokoly** nebo **Service Health**.
3. Vyberte některý z relevantních přehledů.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Go to Azure Monitor" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Další informace

- [Přehled služby Azure Monitor](/azure/azure-monitor/overview)

::: zone-end

# <a name="azure-service-healthtabservicehealth"></a>[Azure Service Health](#tab/servicehealth)

Azure Service Health nabízí pokyny a podporu na míru v situacích, kdy vás ovlivňují problémy ve službách Azure. Mohou vás upozornit, pomohou vám zjistit dopad případných potíží a upozorní vás na průběh jejich řešení. Také vám pomohou připravit se na plánovanou údržbu a změny, které by mohly ovlivnit dostupnost vašich prostředků.

Azure Service Health zahrnuje:

- **Stav Azure:** Globální přehled o stavu služeb Azure
- **Stav služeb:** Přizpůsobený přehled o stavu služeb Azure
- **Stav prostředků:** Podrobnější přehled o stavu jednotlivých prostředků, které pro vás zřídily služby Azure

Kombinace těchto přehledů vám poskytne ucelený pohled na stav služby Azure na úrovni podrobností, která je pro vás důležitá.

## <a name="access-service-health"></a>Přístup ke službě Service Health

1. Na webu Azure Portal přejděte na **Sledovat**.
2. Vyberte **Service Health**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Další informace

Další informace najdete v [dokumentaci ke službě Azure Service Health](/azure/service-health).

::: zone-end

# <a name="azure-advisortabadvisor"></a>[Azure Advisor](#tab/advisor)

Azure Advisor je přizpůsobený cloudový konzultant, který pomáhá dodržovat osvědčené postupy pro optimalizaci nasazení Azure. Analyzuje telemetrii využití a konfiguraci prostředků. Na jejich základě doporučuje řešení, která pomáhají zajistit vysoký výkon, zabezpečení a dostupnost vašich prostředků, a současně hledá možnosti, jak snížit vaše celkové náklady na Azure.

## <a name="access-azure-advisor"></a>Přístup k Azure Advisoru

1. Na webu Azure Portal přejděte na **Poradce**, nebo vyhledejte prostředek.
2. Vyberte **Vysoká dostupnost**, **Zabezpečení**, **Výkon**, **Náklady**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorMenuBlade/overview]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Další informace

[Přehled](/azure/advisor/advisor-overview)

::: zone-end

# <a name="azure-security-centertabsecurity"></a>[Azure Security Center](#tab/security)

Azure Security Center je jednotný systém pro správu zabezpečení infrastruktury, který posiluje stav zabezpečení vašich datacenter a poskytuje pokročilou ochranu před hrozbami pro vaše místní nebo cloudové hybridní úlohy, ať už jsou v Azure, nebo nikoli.

## <a name="access-azure-security-center"></a>Přístup k Azure Security Center

1. Na webu Azure Portal přejděte na **Security Center**, nebo vyhledejte prostředek.
2. Vyberte **Doporučení**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/0]" submitText="Go to Security Center" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Další informace

[Přehled](/azure/security-center/security-center-intro)

::: zone-end

# <a name="azure-backuptabbackup"></a>[Azure Backup](#tab/backup)

Azure Backup je služba Azure, kterou můžete využívat k zálohování (ochraně) a obnovování vašich dat v Microsoft Cloudu. Azure Backup nahrazuje současná řešení místního nebo odlehlého zálohování spolehlivým, bezpečným a cenově konkurenceschopným cloudovým řešením.

## <a name="enable-backup-for-an-azure-vm"></a>Povolení zálohování pro virtuální počítač Azure

1. Na webu Azure Portal vyberte **Virtuální počítače** a vyberte virtuální počítač, který chcete replikovat.
1. V části **Operace** vyberte **Zálohování**.
1. Vytvořte nebo vyberte existující trezor služby Recovery Services.
1. Vyberte **Vytvořit (nebo upravit) nové zásady**.
1. Nakonfigurujte plán a dobu uchování.
1. Vyberte **OK**.
1. Vyberte **Povolit zálohování**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Přehled](/azure/backup/backup-introduction-to-azure-backup)

::: zone-end

# <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

Výše v tomto průvodci jsme diskutovali o tom, jak lze Azure Site Recovery použít jako součást provádění migrace. Po dokončení migrace ale Azure Site Recovery zároveň tvoří nezbytnou součást vaší strategie zotavení po havárii.

Služba Azure Site Recovery umožňuje replikovat virtuální počítače a úlohy hostované v primární oblasti Azure do kopie hostované v sekundární oblasti. Když ve vaší primární oblasti dojde k výpadku, můžete převzít služby při selhání do kopie v sekundární oblasti a dále přistupovat k aplikacím a službám odtud. Jakmile je výpadek v primární kopii virtuálního počítače odstraněn a počítač znovu běží, můžete do něj služby po obnovení navrátit.

## <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replikace virtuálního počítače Azure do jiné oblasti pomocí služby Site Recovery

Následující kroky popisují proces použití služby Site Recovery k replikaci virtuálního počítače Azure do jiné oblasti (Azure-to-Azure):

>
> [!TIP]
> V závislosti na vašem scénáři se konkrétní kroky můžou mírně lišit.
>

## <a name="enable-replication-for-the-azure-vm"></a>Povolení replikace virtuálního počítače Azure

1. Na webu Azure Portal vyberte **Virtuální počítače** a vyberte virtuální počítač, který chcete replikovat.
1. V části **Operace** vyberte **Zotavení po havárii**.
1. V části **Konfigurovat zotavení po havárii** > **Cílová oblast** vyberte cílovou oblast, do které chcete replikaci provést.
1. Pro účely tohoto rychlého startu přijměte výchozí nastavení.
1. Vyberte **Povolit replikaci**. Tím se spustí úloha, která povolí replikaci pro daný virtuální počítač.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

## <a name="verify-settings"></a>Ověření nastavení

Po dokončení úlohy replikace můžete zkontrolovat stav replikace, ověřit nastavení replikace a otestovat nasazení.

1. V nabídce virtuálního počítače vyberte **Zotavení po havárii**.
2. Zkontrolujte stav replikace, vytvořené body obnovení a zdrojové a cílové oblasti na mapě.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Další informace

- [Přehled Azure Site Recovery](/azure/site-recovery/site-recovery-overview)
- [Replikace virtuálního počítače Azure do jiné oblasti](/azure/site-recovery/azure-to-azure-quickstart)

::: zone-end
