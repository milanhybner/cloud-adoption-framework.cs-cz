---
title: Zprovoznění služeb pro správu Azure serveru
description: Zprovoznění služby správy serveru Azure pomocí informací pro virtuální počítače Azure a místní servery.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f83678c1a2b3387155b9fa908c54e81670daf8ae
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80426508"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Fáze 2: zprovoznění služeb správy serveru Azure

Až budete obeznámeni s [nástroji](./tools-services.md) a [plánováním](./prerequisites.md) , které se týkají služby Azure Management Services, jste připraveni na druhou fázi. Fáze 2 poskytuje podrobné pokyny pro připojování těchto služeb k prostředkům Azure. Začněte tím, že tento proces připojování vyhodnocujete ještě předtím, než ho ve svém prostředí přiřadíte do značné míry.

> [!NOTE]
> Přístupy k automatizaci popsané v dalších částech tohoto návodu jsou určeny pro nasazení, která ještě nemají servery nasazené do cloudu. Vyžadují, abyste měli v předplatném roli vlastníka, aby bylo možné vytvořit všechny požadované prostředky a zásady. Pokud jste již vytvořili Log Analytics pracovní prostory a účty Automation, doporučujeme při spuštění ukázkových skriptů pro automatizaci tyto prostředky předat do příslušných parametrů.

## <a name="onboarding-processes"></a>Procesy připojování

Tato část pokynů popisuje následující procesy připojování virtuálních počítačů Azure i místních serverů:

- **Povolte služby správy na jednom virtuálním počítači pro vyhodnocení pomocí portálu**. Tento postup použijte k seznámení se službami Azure Server Management.
- **Nakonfigurujte služby správy pro předplatné pomocí portálu**. Tento proces vám pomůže nakonfigurovat prostředí Azure tak, aby všechny nově zřízené virtuální počítače automaticky používaly služby pro správu. Tento postup použijte v případě, že dáváte přednost Azure Portalmu prostředí pro skripty a příkazové řádky.
- **Nakonfigurujte služby správy pro předplatné pomocí Azure Automation**. Tento proces je plně automatizovaný. Stačí vytvořit předplatné a skripty budou nakonfigurovat prostředí tak, aby používalo služby pro správu pro všechny nově zřízené virtuální počítače. Tento postup použijte, pokud jste obeznámeni se skripty PowerShellu a Azure Resource Manager šablonami, nebo pokud se chcete dozvědět, jak je používat.

Postupy pro každý z těchto přístupů se liší.

> [!NOTE]
> Při použití Azure Portal se posloupnost kroků připojování liší od automatizovaných kroků připojování. Portál nabízí jednodušší prostředí pro připojování.

Následující diagram znázorňuje doporučený model nasazení pro služby správy:

![Diagram doporučeného modelu nasazení](./media/recommended-deployment.png)

Jak je znázorněno na předchozím diagramu, má agent Log Analytics pro místní servery jak *automatickou registraci* , tak i konfiguraci *výslovných přihlašovacích* údajů:

- **Automatický zápis:** Když je agent Log Analytics nainstalovaný na serveru a nakonfigurovaný tak, aby se připojil k pracovnímu prostoru, řešení, která jsou v tomto pracovním prostoru povolená, se automaticky aplikují na server.
- **Výslovný souhlas:** I když je agent nainstalovaný a připojený k pracovnímu prostoru, řešení se nepoužije, pokud se nepřidá do konfigurace oboru serveru v pracovním prostoru.

## <a name="next-steps"></a>Další kroky

Naučte se, jak pomocí portálu připojit jeden virtuální počítač k vyhodnocení procesu připojování.

> [!div class="nextstepaction"]
> [Připojení jediného virtuálního počítače Azure k vyhodnocení](./onboard-single-vm.md)
