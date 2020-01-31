---
title: Ochrana a obnovení v Azure
description: Zajistěte si firemní stabilitu tím, že zkrátíte dobu nutnou k obnovení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 3e9eadbd246ba38f496d8c74b7bcd3e6ade03685
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808154"
---
# <a name="protect-and-recover-in-azure"></a>Ochrana a obnovení v Azure

_Ochrana a obnovení_ je třetí a finální disciplínou v jakémkoli směrném plánu cloudové správy.

![Směrný plán cloudové správy](../../_images/manage/management-baseline.png)

Cílem článku [Provozní dodržování předpisů](./operational-compliance.md) bylo snížit pravděpodobnost přerušení firemního provozu. Cílem aktuálního článku je zkrátit dobu trvání a dopad výpadků, kterým není možné předejít.

V této tabulce je pro jednotlivá podniková prostředí uvedeno navrhované minimum pro jakýkoli směrný plán správy.

|Proces  |Nástroj  |Účel  |
|---------|---------|---------|
|Ochrana dat|Azure Backup|Zálohujte data a virtuální počítače v cloudu.|
|Ochrana prostředí|Azure Security Center|Posilte zabezpečení a poskytujte pokročilou ochranu před hrozbami napříč vašimi hybridními úlohami.|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Pomocí Azure Backup můžete zálohovat, chránit a obnovovat svoje data v cloudu Microsoftu. Azure Backup nahrazuje současná řešení místního nebo odlehlého zálohování cloudovým řešením. Toto nové řešení je spolehlivé, bezpečné a cenově konkurenceschopné. Azure Backup vám může také pomoct ochránit a obnovovat místní prostředky prostřednictvím jednoho konzistentního řešení.

### <a name="enable-backup-for-an-azure-vm"></a>Povolení zálohování pro virtuální počítač Azure

1. Na webu Azure Portal vyberte **Virtuální počítače** a vyberte virtuální počítač, který chcete replikovat.
1. V podokně **Provoz** vyberte **Zálohovat**.
1. Vytvořte nebo vyberte existující trezor služby Azure Recovery Services.
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

Site Recovery replikuje virtuální počítače a úlohy, které jsou hostované v primární oblasti Azure. Replikují se do kopie, která je hostovaná v sekundární oblasti. Když v primární oblasti dojde k výpadku, převezme služby při selhání kopie běžící v sekundární oblasti. Tam budete mít nadále přístup k vašim aplikacím a službám. Tento proaktivní přístup k obnovení může významně zkrátit dobu nutnou pro obnovení. Pokud už prostředí pro obnovení není potřeba, může se produkční provoz vrátit do původního prostředí.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery"></a>Replikace virtuálního počítače Azure do jiné oblasti pomocí Site Recovery

Následující kroky popisují proces použití Site Recovery k replikaci Azure do Azure, což je replikace virtuálního počítače Azure do jiné oblasti:
>
> [!TIP]
> V závislosti na vašem scénáři se konkrétní kroky můžou mírně lišit.
>

### <a name="enable-replication-for-the-azure-vm"></a>Povolení replikace virtuálního počítače Azure

1. Na webu Azure Portal vyberte **Virtuální počítače** a vyberte virtuální počítač, který chcete replikovat.
1. V podokně **Provoz** vyberte **Zotavení po havárii**.
1. Vyberte **Konfigurovat zotavení po havárii** > **Cílová oblast** a zvolte cílovou oblast, do které chcete replikaci provést.
1. V tomto rychlém startu přijměte pro všechny ostatní možnosti výchozí hodnoty.
1. Vyberte **Povolení replikace**, čímž spustíte úlohu, která povolí replikaci pro daný virtuální počítač.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Ověření nastavení

Po dokončení úlohy replikace můžete zkontrolovat stav replikace, ověřit nastavení replikace a otestovat nasazení.

1. V nabídce virtuálního počítače vyberte **Zotavení po havárii**.
1. Zkontrolujte stav replikace, vytvořené body obnovení a zdrojové a cílové oblasti na mapě.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Další informace

- [Přehled Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikace virtuálního počítače Azure do jiné oblasti](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
