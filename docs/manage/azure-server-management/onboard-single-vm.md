---
title: Povolení služby správy serveru na jednom virtuálním počítači pro vyhodnocení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Povolení služby správy serveru na jednom virtuálním počítači pro vyhodnocení
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7ee8cab09fc5ad875240a10d7fe6f632d91432c9
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73751656"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Povolení služby správy serveru na jednom virtuálním počítači pro vyhodnocení

Naučte se, jak povolit služby správy serveru na jednom virtuálním počítači pro vyhodnocení.

> [!NOTE]
> Před implementací služby Azure Management Services na virtuálním počítači vytvořte požadovaný [Log Analytics pracovní prostor a Azure Automation účet](./prerequisites.md#create-a-workspace-and-automation-account) .

Je jednoduché připojit služby pro správu Azure serveru do jednotlivých virtuálních počítačů v Azure Portal. Můžete se seznámit s těmito službami před jejich zprovozněním. Když vyberete instanci virtuálního počítače, všechna řešení v seznamu [nástrojů a služeb pro správu](./tools-services.md) se zobrazí v nabídce **operace** nebo **monitorování** . Vyberte řešení a postupujte podle pokynů průvodce a připojte ho.

![Snímek obrazovky s nastavením virtuálního počítače v Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Související materiály

Další informace o tom, jak tato řešení připojit k jednotlivým virtuálním počítačům, najdete v těchto tématech:

- [Zprovoznění řešení Update Management, Change Tracking a inventáře z virtuálního počítače Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Zprovoznění monitorování Azure pro virtuální počítače](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Další kroky

Naučte se používat Azure Policy k připojování virtuálních počítačů Azure ve velkém měřítku.

> [!div class="nextstepaction"]
> [Konfigurace služeb správy Azure pro předplatné](./onboard-at-scale.md)
