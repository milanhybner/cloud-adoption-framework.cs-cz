---
title: Povolení služby správy na jednom virtuálním počítači pro vyhodnocení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Povolení služby správy na jednom virtuálním počítači pro vyhodnocení
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e9d5e17e87d79d8d1fdf7239298a973959103a37
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026513"
---
# <a name="enable-management-services-on-a-single-vm-for-evaluation"></a>Povolení služby správy na jednom virtuálním počítači pro vyhodnocení

Naučte se, jak povolit služby správy na jednom virtuálním počítači pro vyhodnocení.

> [!NOTE]
> Před připojováním virtuálních počítačů ke službě Azure Management Services vytvořte požadovaný [Log Analytics pracovní prostor a Azure Automation účet](./prerequisites.md#create-a-workspace-and-automation-account) .

Připojování jednotlivých virtuálních počítačů k Azure Server Management Services je jednoduché v Azure Portal. Portál vám umožní seznámit se s těmito službami před jejich zprovozněním pro vaše virtuální počítače. Když vyberete instanci virtuálního počítače, všechna řešení popsaná v seznamu [nástrojů a služeb pro správu](./tools-services.md) se zobrazí v nabídce **operace** nebo v nabídce **monitorování** . Můžete vybrat každé řešení a pomocí Průvodce ho připojit.

![Snímek obrazovky s nastavením virtuálního počítače v Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Související prostředky

Další informace o připojování jednotlivých virtuálních počítačů ke každému řešení najdete v těchto tématech:

- [Zprovoznění řešení Update Management, Change Tracking a inventáře z virtuálního počítače Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Zprovoznění monitorování Azure pro virtuální počítač](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Další kroky

Naučte se používat Azure Policy k připojování virtuálních počítačů Azure ve velkém měřítku.

> [!div class="nextstepaction"]
> [Konfigurace služeb správy Azure pro předplatné](./onboard-at-scale.md)
