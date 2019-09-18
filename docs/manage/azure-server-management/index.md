---
title: Přehled služeb pro správu serverů Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do služeb pro správu serverů Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4d1ada9d47e54f4b0d3828ce93b2d55f3eda8a34
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025712"
---
# <a name="overview-of-azure-server-management-services"></a>Přehled služeb pro správu serverů Azure

Služby pro správu serverů Azure poskytují zákazníkům konzistentní prostředí pro správu jejich serverů ve velkém měřítku. Tyto služby zahrnují operační systémy Linux a Windows a můžete je použít v produkčním, vývojovém i testovacím prostředí. Navíc můžou podporovat virtuální počítače Azure IaaS, fyzické servery a virtuální počítače hostované místně nebo v jiných hostitelských prostředích. 

Služby zahrnuté v sadě služeb pro správu serverů Azure jsou uvedené na následujícím diagramu. 

![Diagram provozního modelu Azure](./media/operations-diagram.png)

Pokyny v této části architektury přechodu na cloud Microsoftu poskytují akční a normativní plán pro nasazení komplexních služeb pro správu serverů ve vašem prostředí. Cílem tohoto plánu je pomoct vám rychle vás na tyto služby nasměrovat a provést vás přírůstkovou sadou fází správy pro všechny velikosti prostředí.

Pro zjednodušení jsme kategorizovali tyto pokyny do tří fází:

![Tři fáze onboardingu sady služeb pro správu serverů Azure](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-management-services"></a>Proč používat služby pro správu Azure?

Služby pro správu Azure nabízí následující výhody:

- **Nativní pro Azure.** Služby pro správu jsou nativně integrované s Azure Resource Managerem. Neustále se vylepšují, aby poskytovaly nové funkce a možnosti.
- **Windows a Linux.** Počítače s Windows a Linuxem mají stejné konzistentní prostředí pro správu.
- **Hybridní.** Služby pro správu pokrývají virtuální počítače Azure IaaS i fyzické a virtuální servery hostované místně nebo v jiných hostitelských prostředích.
- **Zabezpečení.** Microsoft věnuje značné prostředky na všechny formy zabezpečení. Tyto investice nejen chrání infrastrukturu cloudu Azure, ale také rozšiřují výsledné technologie a pomáhají chránit prostředky zákazníků bez ohledu na to, kde se nacházejí.

## <a name="next-steps"></a>Další kroky

Seznamte se s [nástroji, službami a plánováním](./prerequisites.md) souvisejícím s přijetím sady pro správu serverů Azure.

> [!div class="nextstepaction"]
> [Požadované nástroje a plánování](./prerequisites.md)
