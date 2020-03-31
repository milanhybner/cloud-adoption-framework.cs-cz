---
title: Povolení služby správy serveru na virtuálním počítači
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak na jednom virtuálním počítači povolit služby pro správu Azure serveru.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 38285bfe7ebc713d186e6e952b119637161d12ce
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80426527"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Povolení služby správy serveru na jednom virtuálním počítači pro vyhodnocení

Naučte se, jak povolit služby správy serveru na jednom virtuálním počítači pro vyhodnocení.

> [!NOTE]
> Před implementací služby Azure Management Services na virtuálním počítači vytvořte požadovaný [Log Analytics pracovní prostor a Azure Automation účet](./prerequisites.md#create-a-workspace-and-automation-account) .

Je jednoduché připojit služby pro správu Azure serveru do jednotlivých virtuálních počítačů v Azure Portal. Můžete se seznámit s těmito službami před jejich zprovozněním. Když vyberete instanci virtuálního počítače, všechna řešení v seznamu [nástrojů a služeb pro správu](./tools-services.md) se zobrazí v nabídce **operace** nebo **monitorování** . Vyberte řešení a postupujte podle pokynů průvodce a připojte ho.

![Snímek obrazovky s nastavením virtuálního počítače v Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Související prostředky

Další informace o tom, jak tato řešení připojit k jednotlivým virtuálním počítačům, najdete v těchto tématech:

- [Zprovoznění řešení Update Management, Change Tracking a inventáře z virtuálního počítače Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Zprovoznění monitorování Azure pro virtuální počítače](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Další kroky

Naučte se používat Azure Policy k připojování virtuálních počítačů Azure ve velkém měřítku.

> [!div class="nextstepaction"]
> [Konfigurace služeb správy Azure pro předplatné](./onboard-at-scale.md)
