---
title: Nasazení základní úlohy v Azure
description: Seznamte se se základními komponentami cloudové infrastruktury a základními úlohami, jako jsou základní webové aplikace, samostatné virtuální počítače a virtuální sítě.
author: alexbuckgit
ms.author: abuck
ms.date: 12/31/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 015999a9852625abe4ad02a60ad37fc162dd4861
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425418"
---
# <a name="deploy-a-basic-workload-in-azure"></a>Nasazení základní úlohy v Azure

Termín *úlohy* je obvykle definován jako libovolná funkční jednotka, jako je například aplikace nebo služba. Pomáhá se zamyslet na zatížení s ohledem na artefakty kódu, které jsou nasazeny na server, a také na další služby, které jsou specifické pro aplikaci. Může se jednat o užitečnou definici pro místní aplikaci nebo službu, ale pro cloudové aplikace, které je potřeba rozšířit.

V cloudu úloha nezahrnuje jenom všechny artefakty, ale taky obsahuje i cloudové prostředky. Zahrnuté jsou cloudové prostředky jako součást definice z hlediska konceptu označovaného jako "infrastruktura jako kód". Jak jste se naučili, [jak Azure funguje?](../../getting-started/what-is-azure.md), jsou prostředky v Azure nasazené službou Orchestrator. Tato služba Orchestrator zpřístupňuje funkce prostřednictvím webového rozhraní API a volání webového rozhraní API můžete volat pomocí několika nástrojů, jako je PowerShell, Azure CLI a Azure Portal. To znamená, že můžete určit prostředky Azure v strojově čitelném souboru, který lze uložit spolu s artefakty kódu přidruženými k aplikaci.

To umožňuje definovat úlohu z podmínek artefaktů kódu a potřebných cloudových prostředků, takže ještě více umožníte izolaci úloh. Úlohy můžete izolovat podle způsobu uspořádání prostředků, topologie sítě nebo jiných atributů. Cílem izolace úloh je přidružit k týmu konkrétní prostředky úlohy, aby tým mohl nezávisle spravovat všechny aspekty těchto prostředků. To umožňuje více týmům sdílet služby správy prostředků v Azure, a přitom zabránit neúmyslnému odstranění nebo změně prostředků ostatních zdrojů.

Tato izolace také umožňuje další koncept, který se označuje jako DevOps. DevOps zahrnuje postupy pro vývoj softwaru, které zahrnují vývoj softwaru i jejich provoz výše, a co nejvíce využívá automatizaci. Jedním ze zásad DevOps se říká průběžná integrace a průběžné doručování (CI/CD). Průběžná integrace odkazuje na automatizované procesy sestavení, které jsou spuštěny pokaždé, když vývojář potvrdí změnu kódu. Průběžné doručování odkazuje na automatizované procesy, které nasazují tento kód do různých prostředí, jako je vývojové prostředí pro testování nebo produkční prostředí pro konečné nasazení.

## <a name="basic-workload"></a>Základní zatížení

*Základní* úloha je obvykle definovaná jako jediná webová aplikace nebo virtuální síť s virtuálním počítačem (VM).

> [!NOTE]
> Tato příručka nepokrývá vývoj aplikací. Další informace o vývoji aplikací v Azure najdete v tématu [Průvodce architekturou aplikací Azure](https://docs.microsoft.com/azure/architecture/guide).

Bez ohledu na to, jestli je zatížení webová aplikace nebo virtuální počítač, vyžaduje každé z těchto nasazení *skupinu prostředků*. Uživatel s oprávněním k vytvoření skupiny prostředků musí provést před provedením následujících kroků.

## <a name="basic-web-application-paas"></a>Základní webová aplikace (PaaS)

V případě základní webové aplikace vyberte jednu z 5 minut rychlých startů z [dokumentace k Web Apps](https://docs.microsoft.com/azure/app-service) a postupujte podle těchto kroků.

> [!NOTE]
> Někteří průvodci rychlým startem nasadí skupinu prostředků standardně. V takovém případě není nutné vytvořit skupinu prostředků explicitně. V opačném případě nasaďte webovou aplikaci do skupiny prostředků vytvořené výše.

Po nasazení jednoduché úlohy si můžete přečíst další informace o osvědčených postupech pro nasazení [základní webové aplikace](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/basic-web-app) do Azure.

## <a name="single-windows-or-linux-vm-iaas"></a>Virtuální počítač s jedním systémem Windows nebo Linux (IaaS)

Pro jednoduché úlohy, které běží na virtuálním počítači, je prvním krokem nasazení virtuální sítě. Všechny prostředky infrastruktury jako služby (IaaS) v Azure, jako jsou virtuální počítače, nástroje pro vyrovnávání zatížení a brány, vyžadují virtuální síť. Přečtěte si o [virtuálních sítích Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)a pak postupujte podle pokynů pro [nasazení Virtual Network do Azure pomocí portálu](https://docs.microsoft.com/azure/virtual-network/quick-create-portal). Když zadáte nastavení pro virtuální síť v Azure Portal, nezapomeňte zadat název skupiny prostředků vytvořené výše.

V dalším kroku se rozhodujete, jestli se má nasadit jeden virtuální počítač s Windows nebo Linuxem. Pro virtuální počítače s Windows použijte postup [nasazení virtuálního počítače s Windows do Azure s portálem](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal). Po zadání nastavení pro virtuální počítač v Azure Portal zadejte název skupiny prostředků vytvořené výše.

Až provedete kroky a nasadíte virtuální počítač, můžete získat informace o [osvědčených postupech pro spuštění virtuálního počítače s Windows v Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/single-vm). Pro virtuální počítač se systémem Linux použijte postup [nasazení virtuálního počítače se systémem Linux do Azure pomocí portálu](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal). Můžete si taky přečíst další informace o [osvědčených postupech pro spuštění virtuálního počítače se systémem Linux v Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-linux/single-vm).

## <a name="next-steps"></a>Další kroky

Postup použití základních komponent infrastruktury v cloudu Azure najdete v tématu věnovaném [rozhodovacím pokynům pro architekturu](../../decision-guides/index.md) .
