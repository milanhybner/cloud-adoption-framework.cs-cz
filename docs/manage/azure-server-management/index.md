---
title: Přehled služeb pro správu serverů Azure
description: Tato část architektury přechodu na cloud pro Azure poskytuje normativní plán pro nasazení komplexních služeb pro správu serverů ve vašem prostředí.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c6afdfe05a9245d729b17d1d56f3c64ffa6107bd
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341670"
---
# <a name="overview-of-azure-server-management-services"></a>Přehled služeb pro správu serverů Azure

Služby správy serverů Azure poskytují konzistentní prostředí pro správu serverů ve velkém měřítku. Tyto služby pokrývají podporu operační systémy Linux i Windows. Dají se použít v produkčních, vývojových i testovacích prostředích. Služby správy serverů mohou podporovat virtuální počítače Azure IaaS, fyzické servery a virtuální počítače hostované místně nebo v jiných hostitelských prostředích.

Služby zahrnuté v sadě služeb pro správu serverů Azure ukazuje následující diagram: ![Diagram provozního modelu Azure](./media/operations-diagram.png)

Tato část architektury přechodu na cloud Microsoftu poskytuje akční a normativní plán pro nasazení komplexních služeb pro správu serverů ve vašem prostředí. Tento plán vám pomůže rychle vás na tyto služby nasměrovat a provede vás přírůstkovou sadou fází správy pro všechny velikosti prostředí.

Pro zjednodušení jsme kategorizovali tyto pokyny do tří fází:

![Tři fáze onboardingu sady služeb pro správu serverů Azure](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-server-management-services"></a>Proč využívat služby pro správu serverů Azure?

Služby pro správu serverů Azure nabízejí následující výhody:

- **Nativní pro Azure:** Služby pro správu serverů jsou nativně integrované s Azure Resource Managerem. Neustále se vylepšují, aby poskytovaly nové funkce a možnosti.
- **Windows a Linux:** Počítače s Windows a Linuxem mají stejné konzistentní prostředí pro správu.
- **Hybridní model:** Služby pro správu serverů pokrývají virtuální počítače Azure IaaS i fyzické a virtuální servery hostované místně nebo v jiných hostitelských prostředích.
- **Zabezpečení:** Microsoft věnuje značné prostředky na všechny formy zabezpečení. Tyto investice nejen chrání infrastrukturu Azure, ale také rozšiřují výsledné technologie a pomáhají chránit prostředky zákazníků bez ohledu na to, kde se nacházejí.

## <a name="next-steps"></a>Další kroky

Seznamte se s [nástroji, službami a plánováním](./prerequisites.md) souvisejícím s přijetím sady pro správu serverů Azure.

> [!div class="nextstepaction"]
> [Požadované nástroje a plánování](./prerequisites.md)
