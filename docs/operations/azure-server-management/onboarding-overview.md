---
title: Připojování ke službám Azure Server Management
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Připojování ke službám Azure Server Management
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 330e297b4fb63eaa376e8b6dac0ccf77c2a16ef4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825130"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Fáze 2: Připojování služeb pro správu Azure serveru

Pokud jste obeznámeni s [nástroji](./tools-services.md) a [plánováním](./prerequisites.md) , které se týkají služby Azure Management Services, jste připraveni na druhou fázi, která poskytuje podrobné pokyny k tomu, abyste tyto služby mohli používat s prostředky Azure. Začněte tím, že tento proces připojování vyhodnocujete ještě předtím, než ho ve svém prostředí přiřadíte do značné míry.

> [!NOTE]
> Přístupy k automatizaci popsané v dalších částech tohoto návodu jsou zaměřené na nasazení, která ještě nemají servery nasazené do cloudu. Vyžadují, abyste měli v předplatném roli vlastníka, aby bylo možné vytvořit všechny požadované prostředky a zásady. Pokud už máte vytvořené prostředky pro Log Analytics pracovní prostor a účet Automation, doporučujeme při spouštění ukázkových skriptů pro automatizaci tyto prostředky předat do příslušných parametrů.

## <a name="onboarding-processes"></a>Procesy připojování

Tato část pokynů popisuje následující procesy připojování virtuálních počítačů Azure i místních serverů:

- **Povolte služby správy na jednom virtuálním počítači pro vyhodnocení pomocí portálu**. Tento postup použijte k seznámení se službami Azure Server Management.
- **Nakonfigurujte služby správy pro předplatné pomocí portálu**. Tento proces vám pomůže nakonfigurovat prostředí Azure tak, aby všechny nově zřízené virtuální počítače automaticky používaly služby pro správu. Tento postup použijte v případě, že dáváte přednost Azure Portalmu prostředí pro skripty a příkazové řádky.
- **Nakonfigurujte služby správy pro předplatné pomocí Azure Automation**. Tento proces je plně automatizovaný. Stačí vytvořit předplatné a skripty budou konfigurovat prostředí pro používání služeb správy pro všechny nově zřízené virtuální počítače. Tento postup použijte, pokud jste obeznámeni se skripty PowerShellu a Azure Resource Manager šablonami, nebo pokud se chcete dozvědět, jak je používat.

Postupy pro každý z těchto přístupů se liší.

> [!NOTE]
> Pořadí připojování kroků při použití Azure Portal se liší od automatizovaných kroků při připojování, protože portál nabízí jednodušší prostředí pro připojování.

Následující diagram znázorňuje doporučený model nasazení pro služby správy. 

![Diagram doporučeného modelu nasazení](./media/recommended-deployment.png)

> [!NOTE]
> Jak je znázorněno na předchozím diagramu, má agent Log Analytics pro místní servery jak *automatickou registraci* , tak i konfiguraci *výslovných přihlašovacích* údajů. *Automatický zápis* znamená, že když je agent Log Analytics nainstalovaný na serveru a nakonfigurovaný pro připojení k pracovnímu prostoru, budou se řešení povolená v tomto pracovním prostoru automaticky vztahovat na server. *Výslovný souhlas* znamená, že i v případě, že je agent nainstalován a připojen k pracovnímu prostoru, řešení nebude použito, pokud nebude přidáno do konfigurace oboru serveru v pracovním prostoru.

## <a name="next-steps"></a>Další postup

Naučte se, jak pomocí portálu připojit jeden virtuální počítač k vyhodnocení procesu připojování.

> [!div class="nextstepaction"]
> [Připojení jediného virtuálního počítače Azure k vyhodnocení](./onboard-single-vm.md)
