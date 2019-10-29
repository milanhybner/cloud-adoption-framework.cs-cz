---
title: Ochrana a obnovení v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zajistěte si firemní stabilitu tím, že zkrátíte dobu nutnou k obnovení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: a79164435772f571849d0a836f43b53ce3bca087
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557002"
---
# <a name="protect-and-recover-in-azure"></a>Ochrana a obnovení v Azure

Ochrana a obnovení je třetí a finální disciplínou v jakémkoli směrném plánu cloudové správy.

![Směrný plán cloudové správy](../../_images/manage/management-baseline.png)

Cílem posledního článku, Provozní dodržování předpisů, bylo snížit pravděpodobnost přerušení firemního provozu. Cílem tohoto článku, Ochrana a obnovení, je zkrátit dobu trvání a dopad výpadků, kterým není možné předejít.

V následující tabulce je uvedeno navrhované minimum pro všechny směrné plány správy v jakémkoli podnikovém prostředí.

|Proces  |Nástroj  |Účel  |
|---------|---------|---------|
|Ochrana dat|Azure Backup|Zálohování dat a virtuálních počítačů v cloudu|
|Ochrana prostředí|Azure Security Center|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Azure Backup je služba Azure, kterou můžete využívat k zálohování (ochraně) a obnovování vašich dat v Microsoft Cloudu. Azure Backup nahrazuje současná řešení místního nebo odlehlého zálohování spolehlivým, bezpečným a cenově konkurenceschopným cloudovým řešením. Je možné ji také použít k ochraně a obnovování místních prostředků prostřednictvím jednoho konzistentního řešení.

### <a name="enable-backup-for-an-azure-vm"></a>Povolení zálohování pro virtuální počítač Azure

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

[Přehled](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery je zásadní součástí strategie zotavení po havárii.

Služba Azure Site Recovery umožňuje replikovat virtuální počítače a úlohy hostované v primární oblasti Azure do kopie hostované v sekundární oblasti. Když ve vaší primární oblasti dojde k výpadku, můžete převzít služby při selhání do kopie v sekundární oblasti a dále přistupovat k aplikacím a službám odtud. Tento proaktivní přístup k obnovení může významně zkrátit dobu nutnou pro obnovení. Pokud už prostředí pro obnovení nepotřebujete, může se produkční provoz vrátit do původního prostředí.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replikace virtuálního počítače Azure do jiné oblasti pomocí služby Site Recovery

Následující kroky popisují proces použití služby Site Recovery k replikaci virtuálního počítače Azure do jiné oblasti (Azure-to-Azure):

>
> [!TIP]
> V závislosti na vašem scénáři se konkrétní kroky můžou mírně lišit.
>

### <a name="enable-replication-for-the-azure-vm"></a>Povolení replikace virtuálního počítače Azure

1. Na webu Azure Portal vyberte **Virtuální počítače** a vyberte virtuální počítač, který chcete replikovat.
1. V části **Operace** vyberte **Zotavení po havárii**.
1. V části **Konfigurovat zotavení po havárii** > **Cílová oblast** vyberte cílovou oblast, do které chcete replikaci provést.
1. Pro účely tohoto rychlého startu přijměte výchozí nastavení.
1. Vyberte **Povolení replikace**, čímž spustíte úlohu, která povolí replikaci pro daný virtuální počítač.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Ověření nastavení

Po dokončení úlohy replikace můžete zkontrolovat stav replikace, ověřit nastavení replikace a otestovat nasazení.

1. V nabídce virtuálního počítače vyberte **Zotavení po havárii**.
2. Zkontrolujte stav replikace, vytvořené body obnovení a zdrojové a cílové oblasti na mapě.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Další informace

- [Přehled Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikace virtuálního počítače Azure do jiné oblasti](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
