---
title: Optimalizace a transformace
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Optimalizace a transformace
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: c44bcd45783ee6ea61bbbe33b6b76ce7034eca2c
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818893"
---
# <a name="optimize-and-transform"></a>Optimalizace a transformace

Další fází po migraci vašich služeb do Azure je kontrola řešení a hledání možností jeho optimalizace. To může zahrnovat kontrolu návrhu řešení, nastavení správné velikosti služeb a analýzu nákladů.

Tato fáze také nabízí příležitost k optimalizaci prostředí a případně k jeho transformaci. Například jste mohli provést migraci, která spočívala ve změně hostitele. Teď, když máte služby spuštěné v Azure, můžete překontrolovat konfiguraci řešení nebo konfiguraci používaných služeb, případně provést refaktoring, abyste modernizovali nebo zvýšili funkčnost svého řešení.

# <a name="right-size-assetstaboptimize"></a>[Správná velikost prostředků](#tab/optimize)

Všem službám Azure, které nabízejí nákladový model založený na využití, můžete změnit velikost. Můžete k tomu použít Azure Portal, CLI nebo PowerShell. Prvním krokem při nastavování správné velikosti služby je kontrola metrik využití. Přístup k těmto metrikám nabízí služba Azure Monitor. Pro analyzovanou službu pravděpodobně budete muset nakonfigurovat kolekci metrik a pak nějakou dobu počkat, až se na základě způsobu používání úloh shromáždí vypovídající data.

1. Přejděte na **Sledovat**.
1. Vyberte **Metriky** a nakonfigurujte graf, aby zobrazoval metriky analyzované služby.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/metrics]" submitText="Go to Monitor" :::

::: zone-end

Níže jsou nejčastější služby, které umožňují změnu velikosti.

## <a name="resize-a-virtual-machine"></a>Změna velikosti virtuálního počítače

Azure Migrate provádí v rámci předběžné vyhodnocovací fáze analýzu správné velikosti služby. Pokud k migraci virtuálních počítačů použijete tento nástroj, bude jejich velikost pravděpodobně založena na vašich předběžných požadavcích před migrací.

Pokud jste k vytvoření nebo migraci virtuálních počítačů použili jiný způsob nebo pokud chcete požadavky na migrované virtuální počítače upravit, bude pravděpodobně potřeba velikost virtuálních počítačů zpřesnit.

1. Přejděte na **Virtuální počítače**.
1. Ze seznamu vyberte požadovaný virtuální počítač.
1. Vyberte **Velikost** a ze seznamu vyberte požadovanou novou velikost. K vyhledání potřebné velikosti možná budete muset upravit filtry.
1. Vyberte **Změnit velikost**.

Pokud měníte velikost virtuálních počítačů za provozu, může dojít k přerušení služby. Proto se pokuste nastavit správnou velikost virtuálních počítačů, než je nasadíte do ostrého provozu.


::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

- [Správa rezervací prostředků Azure](/azure/billing/billing-manage-reserved-vm-instance)
- [Změna velikosti virtuálního počítače s Windows](/azure/virtual-machines/windows/resize-vm)
- [Změna velikosti virtuálního počítače s Linuxem pomocí Azure CLI](/azure/virtual-machines/linux/change-vm-size)

Partneři můžou kontrolovat použití v Partnerském centru.

- [Nastavení velikosti virtuálního počítače Microsoft Azure, která maximálně využívá rezervaci](/partner-center/azure-usage)

::: zone-end

## <a name="resize-a-storage-account"></a>Změna velikosti účtu úložiště

1. Přejděte na **Účty úložiště**.
1. Vyberte požadovaný účet úložiště.
1. Vyberte **Konfigurovat** a upravte vlastnosti účtu úložiště podle svých požadavků.
1. Vyberte **Uložit**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2FStorageAccounts]" submitText="Go to Storage Accounts" :::

::: zone-end

## <a name="resize-a-sql-database"></a>Změna velikosti Databáze SQL

1. Přejděte na **Databáze SQL** nebo na **SQL Servery** a vyberte server.
1. Vyberte požadovanou databázi.
1. Vyberte **Konfigurovat** a pak vyberte novou požadovanou úroveň služby.
1. Vyberte **Použít**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Sql%2Fservers%2Fdatabases]" submitText="Go to SQL Databases" :::

::: zone-end

# <a name="cost-managementtabmanagecost"></a>[Správa nákladů](#tab/ManageCost)

Průběžná analýza a kontrola nákladů je důležitá. Umožní vám podle potřeby měnit velikost prostředků, abyste vyvážili náklady a používané úlohy.

Služba Azure Cost Management spolupracuje s Azure Advisorem a nabízí doporučení, která se týkají optimalizace nákladů. Azure Advisor provádí optimalizaci a zvyšuje efektivitu tím, že identifikuje nečinné a nevyužité prostředky.

1. Vyberte **Správa nákladů a fakturace**.
1. Vyberte **Doporučení poradce** a kartu **Náklady**.
1. Ke kontrole možných výhod použijte **Dopad** a **Možné úspory za rok**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" :::

::: zone-end

K získání doporučení ohledně možné úspory nákladů také můžete použít **Poradce** a vybrat kartu **Náklady**.

> [!TIP]
> Pokud služby nemusí být nepřetržitě dostupné (například Azure Virtual Machines nebo Azure SQL Data Warehouse), můžete implementovat řešení, které řídí náklady tím, že službu podle potřeby spustí, zastaví nebo pozastaví.
>

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

- [Kurz: Optimalizace nákladů na základě doporučení](/azure/cost-management/tutorial-acm-opt-recommendations)
- [Jak zabránit neočekávaným poplatkům v rámci fakturace Azure a správy nákladů](/azure/billing/billing-getting-started)
- [Prozkoumání a analýza nákladů pomocí služby Analýzy nákladů](/azure/cost-management/quick-acm-cost-analysis)

::: zone-end