---
title: Plánování pro služby Azure Server Management Services
description: Přečtěte si o nástrojích a připravte se na prostředky potřebné ke správě služby Azure Server Management Services.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 97d4b52b50f943dfd0e146e84d4e5fc5a1d97711
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094644"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Fáze 1: plánování požadavků pro služby Azure Server Management Services

V této fázi se seznámíte se sadou služeb Azure Server Management Suite a naplánujete, jak nasadit prostředky potřebné k implementaci těchto řešení pro správu.

## <a name="understand-the-tools-and-services"></a>Pochopení nástrojů a služeb

Podrobné informace o těchto nástrojích najdete v článku [nástroje a služby pro správu serveru Azure](./tools-services.md) :

- Oblasti správy, které se podílejí na probíhajících operacích Azure.
- Služby a nástroje Azure, které vám pomůžou v těchto oblastech podporovat.

K splnění požadavků na správu budete používat několik těchto služeb dohromady. Tyto nástroje jsou v těchto pokynech často odkazovány.

Následující části popisují plánování a přípravu potřebné k používání těchto nástrojů a služeb.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Plánování Log Analytics pracovního prostoru a účtu Automation

Mnohé ze služeb, které použijete k připojení služeb Azure Management Services, vyžadují Log Analytics pracovní prostor a propojený Azure Automation účet.

[Pracovní prostor Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) představuje jedinečné prostředí pro ukládání dat protokolů platformy Azure Monitor. Každé pracovní prostředí má vlastní úložiště dat a konfiguraci. Zdroje dat a řešení jsou nakonfigurovány tak, aby ukládaly svoje data do konkrétních pracovních prostorů. Řešení Azure pro monitorování vyžadují připojení všech serverů k pracovním prostorům, aby mohla data ukládat a přistupovat k nim.

Některé služby pro správu vyžadují účet [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) . Tento účet a funkce Azure Automation slouží k integraci služeb Azure a dalších veřejných systémů pro nasazení, konfiguraci a správu procesů správy serveru.

Následující služba pro správu serveru Azure vyžaduje propojený pracovní prostor Log Analytics a účet Automation:

- [Update Management Azure](https://docs.microsoft.com/azure/automation/automation-update-management)
- [Change Tracking a inventář](https://docs.microsoft.com/azure/automation/change-tracking)
- [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)
- [Konfigurace požadovaného stavu](https://docs.microsoft.com/azure/virtual-machines/extensions/dsc-overview)

Druhá fáze tohoto návodu se zaměřuje na nasazení služeb a skriptů pro automatizaci. Ukazuje, jak vytvořit pracovní prostor Log Analytics a účet Automation. V těchto pokynech se dozvíte, jak pomocí Azure Policy zajistit, aby byly nové virtuální počítače připojené ke správnému pracovnímu prostoru.

Příklady v těchto pokynech předpokládají nasazení, které ještě nemá servery nasazené do cloudu. Další informace o principech a doporučeních, které jsou součástí plánování pracovních prostorů, najdete v tématu [Správa dat protokolu a pracovních prostorů v Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Aspekty plánování

Při přípravě pracovních prostorů a účtů potřebných ke zprovoznění služeb správy Vezměte v úvahu následující problémy:

- Geografické oblasti **Azure a dodržování předpisů:** Oblasti Azure jsou uspořádané do *geografických*oblastí. [Zeměpisná oblast Azure](https://azure.microsoft.com/global-infrastructure/geographies) zajišťuje, že se nároky na data, svrchovanost, dodržování předpisů a odolnost proti chybám uplatňují v rámci zeměpisných hranic. Pokud se vaše úlohy vztahují na svrchovanost nebo jiné požadavky na dodržování předpisů, musí být pracovní prostor a účty Automation nasazené do oblastí v rámci stejné geografické oblasti Azure jako prostředky, které podporují.
- **Počet pracovních prostorů:** Jako princip vytváření identifikátorů GUID vytvořte minimální počet pracovních prostorů vyžadovaných pro jednotlivé geografické oblasti Azure. Doporučujeme aspoň jeden pracovní prostor pro každé geografické prostředí Azure, kde se nachází vaše výpočetní prostředky nebo prostředky úložiště. Toto počáteční zarovnání pomáhá zabránit budoucím problémům v legislativě při migraci dat do různých geografických oblastí.
- **Uchovávání dat a capping:** Při vytváření pracovních prostorů nebo účtů Automation možná budete muset vzít v úvahu zásady uchovávání dat nebo capping požadavky na data. Další informace o těchto zásadách a další informace o plánování pracovních prostorů najdete v tématu [Správa dat protokolu a pracovních prostorů v Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).
- **Mapování oblastí:** Propojení Log Analyticsho pracovního prostoru a účtu Azure Automation se podporuje jenom mezi některými oblastmi Azure. Pokud je například pracovní prostor Log Analytics hostovaný v oblasti *EastUS* , musí se v oblasti *EastUS2* vytvořit propojený účet Automation, který se má používat se službami pro správu. Pokud máte účet Automation, který byl vytvořen v jiné oblasti, nemůže se připojit k pracovnímu prostoru v *EastUS*. Volba oblasti nasazení může významně ovlivnit požadavky na geografickou verzi Azure. V [tabulce mapování oblastí](https://docs.microsoft.com/azure/automation/how-to/region-mappings) se rozhodněte, která oblast by měla hostovat vaše pracovní prostory a účty Automation.
- **Vícedomé pracovní prostory:** Agent Azure Log Analytics v některých scénářích podporuje více domovských stránek, ale agent při spuštění v této konfiguraci čelí několika omezením a problémům. Pokud to Microsoft nedoporučuje pro konkrétní scénář, nedoporučujeme konfigurovat více domovských stránek na agentovi Log Analytics.

## <a name="resource-placement-examples"></a>Příklady umístění prostředků

Existuje několik různých modelů pro výběr předplatného, ve kterém umístíte Log Analytics pracovní prostor a účet Automation. V krátkých případech umístěte pracovní prostor a účty Automation do předplatného, které vlastní tým, který je zodpovědný za implementaci služby Update Management a služby Change Tracking a inventarizace.

Následují příklady některých způsobů nasazení pracovních prostorů a účtů Automation.

### <a name="placement-by-geography"></a>Umístění podle geografie

Malá a střední prostředí mají jedno předplatné a několik stovky prostředků, které jsou rozloženy na více geografických oblastí Azure. V těchto prostředích můžete vytvořit jeden Log Analytics pracovní prostor a jeden Azure Automation účet v každé geografické oblasti.

V každé skupině prostředků můžete vytvořit pracovní prostor a účet Azure Automation jako jednu dvojici. Pak pár nasaďte do odpovídajícího geografického umístění do virtuálních počítačů.

Případně, pokud vaše zásady dodržování předpisů neurčují, jaké prostředky se nacházejí v určitých oblastech, můžete vytvořit jednu dvojici, která bude spravovat všechny virtuální počítače. Doporučujeme také umístit dvojici pracovní prostor a účet Automation do samostatných skupin prostředků a poskytnout tak podrobnější řízení přístupu na základě role (RBAC).

Příklad v následujícím diagramu má jedno předplatné se dvěma skupinami prostředků, z nichž každý je umístěný v jiném geografickém umístění:

![Model pracovního prostoru pro malá a střední prostředí](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Umístění v rámci předplatného pro správu

Větší prostředí zahrnují více předplatných a mají centrální IT oddělení, které vlastní monitorování a dodržování předpisů. V těchto prostředích vytvořte páry pracovních prostorů a účtů Automation v předplatném správy IT. V tomto modelu jsou prostředky virtuálních počítačů v geografickém úložišti jejich data v příslušném geografickém pracovním prostoru v předplatném správy IT. Pokud je potřeba, aby týmy aplikace spouštěly úlohy automatizace, ale nevyžadují propojený pracovní prostor a účty Automation, můžou vytvářet samostatné účty Automation ve vlastních předplatných aplikací.

![Model pracovního prostoru pro rozsáhlá prostředí](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Decentralizované umístění

V alternativním modelu pro rozsáhlá prostředí může být vývojový tým aplikací zodpovědný za opravy a správu. V takovém případě umístěte do předplatného týmu aplikací dvojice účtů pracovního prostoru a účtu Automation společně s jejich jinými prostředky.

  ![Model účtu pracovního prostoru pro decentralizovaná prostředí](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Vytvoření pracovního prostoru a účtu Automation

Po zvolení nejlepšího způsobu, jak umístit a uspořádat dvojice pracovních prostorů a účtů, se ujistěte, že jste vytvořili tyto prostředky před zahájením procesu připojování. Příklady automatizace dále v těchto pokynech vytvoří pro vás pár účtů v pracovním prostoru a Automation. Pokud se ale chcete připojit pomocí Azure Portal a nemáte existující dvojici v pracovním prostoru a účtu Automation, budete ho muset vytvořit.

Chcete-li vytvořit pracovní prostor Log Analytics pomocí Azure Portal, přečtěte si téma [Vytvoření pracovního prostoru](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). Potom vytvořte účet služby Automation pro každý pracovní prostor podle kroků v části [Vytvoření účtu Azure Automation](https://docs.microsoft.com/azure/automation/automation-quickstart-create-account).

> [!NOTE]
> Když vytvoříte účet Automation pomocí Azure Portal, portál se ve výchozím nastavení pokusí vytvořit účty Spustit jako pro prostředky Azure Resource Manager a model nasazení Classic. Pokud nemáte klasické virtuální počítače ve vašem prostředí a nejste spolusprávcem předplatného, portál vytvoří účet Spustit jako pro Správce prostředků, ale při nasazení účtu Spustit jako pro Classic vygeneruje chybu. Pokud nechcete podporovat klasické prostředky, můžete tuto chybu ignorovat.
>
> Účty Spustit jako můžete vytvořit také pomocí [prostředí PowerShell](https://docs.microsoft.com/azure/automation/manage-runas-account#creating-a-run-as-account-using-powershell).

## <a name="next-steps"></a>Další kroky

Naučte se, jak [vaše servery](./onboarding-overview.md) připojit ke službám Azure Server Management.

> [!div class="nextstepaction"]
> [Připojování ke službám Azure Server Management](./onboarding-overview.md)
