---
title: Plánování požadavků pro služby Azure Server Management Services
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Požadované nástroje a plánování pro služby Azure Server Management.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ac4ece6c5daec788d116e67c79429572722fc618
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548242"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Fáze 1: plánování požadavků pro služby Azure Server Management Services

V této fázi se seznámíte se sadou služeb Azure Server Management Suite a naplánujete, jak nasadit prostředky potřebné k implementaci těchto řešení pro správu.

## <a name="understand-the-tools-and-services"></a>Pochopení nástrojů a služeb

Podrobné informace o oblastech správy, které se podílejí na probíhajících operacích Azure, a službách a nástrojích Azure, které vám pomůžou s podporou v těchto oblastech, najdete v tématu [nástroje a služby pro správu serveru Azure](./tools-services.md) . Splnění požadavků na správu bude zahrnovat použití několika těchto služeb dohromady. Tyto nástroje jsou v těchto pokynech často odkazovány.

Následující části popisují plánování a přípravu potřebné k používání těchto nástrojů a služeb.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Plánování Log Analytics pracovního prostoru a účtu Automation

Mnohé ze služeb, které použijete k připojení služeb Azure Management Services, vyžadují Log Analytics pracovní prostor a propojený Azure Automation účet.

[Log Analytics pracovní prostor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) je jedinečné prostředí pro ukládání dat protokolu Azure monitor. Každý pracovní prostor má své vlastní úložiště a konfiguraci dat. Zdroje dat a řešení jsou nakonfigurovány tak, aby ukládaly svá data v konkrétních pracovních prostorech. Řešení Azure Monitoring vyžadují, aby byly všechny servery připojené k pracovnímu prostoru, aby bylo možné ukládat a získávat data protokolu.

Některé služby pro správu vyžadují účet [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) . Pomocí tohoto účtu a možností Azure Automation můžete integrovat služby Azure a další veřejné systémy k nasazení, konfiguraci a správě procesů správy serveru.

Následující služby Azure Server Management vyžadují propojený pracovní prostor Log Analytics a účet Automation k fungování:

- [Update Management Azure](https://docs.microsoft.com/azure/automation/automation-update-management)
- [Change Tracking a inventář](https://docs.microsoft.com/azure/automation/change-tracking)
- [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)
- [Konfigurace požadovaného stavu](https://docs.microsoft.com/azure/virtual-machines/extensions/dsc-overview)

Druhá fáze tohoto návodu se zaměřuje na nasazení služeb a skriptů pro automatizaci. Ukazuje, jak vytvořit pracovní prostor Log Analytics a účet Automation. V těchto pokynech se dozvíte, jak pomocí Azure Policy zajistit, aby byly nové virtuální počítače připojené ke správnému pracovnímu prostoru.

Příklady zahrnuté v těchto pokynech předpokládají nasazení, které ještě nemá servery nasazené do cloudu. Další informace o principech a doporučeních, které jsou součástí plánování pracovních prostorů, najdete v tématu [Správa dat protokolu a pracovních prostorů v Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Aspekty plánování

Při přípravě pracovních prostorů a účtů, které vytvoříte pro služby správy, se podívejte na následující diskuzi o problémech:

- Geografické oblasti **Azure a dodržování legislativních předpisů**. Oblasti Azure jsou uspořádané do *geografických*oblastí. [Zeměpisná oblast Azure](https://azure.microsoft.com/global-infrastructure/geographies) zajišťuje, že se nároky na data, svrchovanost, dodržování předpisů a odolnost proti chybám uplatňují v rámci zeměpisných hranic. Pokud se vaše úlohy vztahují na svrchovanost dat nebo jiné požadavky na dodržování předpisů, musí být tento pracovní prostor a účty Automation nasazené do oblastí v rámci stejné geografické oblasti Azure jako prostředky, které podporují.
- **Počet pracovních prostorů**. Jako princip vytváření identifikátorů GUID vytvořte minimální počet pracovních prostorů vyžadovaných pro jednotlivé geografické oblasti Azure. Doporučujeme aspoň jeden pracovní prostor pro každé geografické prostředí Azure, kde se nachází vaše výpočetní prostředky nebo prostředky úložiště. Toto počáteční zarovnání pomáhá zabránit budoucím problémům při migraci dat do různých geografických oblastí.
- **Uchovávání dat a capping**. Při vytváření pracovních prostorů nebo účtů Automation možná budete muset vzít v úvahu zásady uchovávání dat nebo capping požadavky na data. Další informace o těchto principech a dalších doporučeních při plánování pracovních prostorů najdete [v tématu Správa dat protokolu a pracovních prostorů v Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).
- **Mapování oblastí** Propojení Log Analyticsho pracovního prostoru a účtu Azure Automation je podporované jenom mezi některými oblastmi Azure. Pokud je například pracovní prostor Log Analytics hostovaný v oblasti *EastUS* , musí se propojený účet Automation vytvořit v oblasti *EastUS2* , aby se mohl používat se službami pro správu. Pokud máte účet služby Automation, který byl vytvořen v jiné oblasti, nebude se moci připojit k pracovnímu prostoru v *EastUS*. Volba oblasti nasazení může významně ovlivnit požadavky na geografickou verzi Azure. V [tabulce mapování oblastí](https://docs.microsoft.com/azure/automation/how-to/region-mappings) se rozhodněte, která oblast by měla hostovat vaše pracovní prostory a účty Automation.
- **Vícedomé pracovní prostory**. Agent Log Analytics v některých scénářích podporuje více domovských stránek, ale agent při spuštění v této konfiguraci čelí několika omezením a problémům. Pokud společnost Microsoft nedoporučuje pro váš scénář používat více domovských stránek, nedoporučujeme konfigurovat více domovských stránek na agentovi Log Analytics.

## <a name="resource-placement-examples"></a>Příklady umístění prostředků

Existuje několik různých modelů pro výběr předplatného, ve kterém umístíte Log Analytics pracovní prostor a účet Automation. V krátkém případě byste měli umístit účty pracovního prostoru a Automation do předplatného, které vlastní tým, který je zodpovědný za implementaci Update Management a Change Tracking a inventáře služeb.

Následující příklady ilustrují některé způsoby, jak můžou být nasazené pracovní prostory a účty Automation.

### <a name="placement-by-geography"></a>Umístění podle geografie

V malých a středně velkých prostředích s jedním předplatným a několika stovkami prostředků, které pokrývají více geografických oblastí Azure, vytvořte jeden Log Analytics pracovní prostor a jeden Azure Automation účet v každé geografické oblasti.

Můžete vytvořit pracovní prostor a účet Azure Automation – jednu dvojici – v každé skupině prostředků a nasadit dvojici do odpovídajícího geografického umístění do virtuálních počítačů. Případně platí, že pokud vaše zásady dodržování předpisů neurčují, jaké prostředky se nacházejí v určitých oblastech, můžete vytvořit jednu dvojici, která bude spravovat všechny virtuální počítače. Doporučujeme také umístit dvojici pracovní prostor a účet služby Automation do samostatných skupin prostředků, aby bylo možné podrobnější řízení přístupu na základě role (RBAC).

Příklad v následujícím diagramu má jedno předplatné se dvěma skupinami prostředků, z nichž každý je umístěný v jiné geografické oblasti.

![Model pracovního prostoru pro malá a střední prostředí](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Umístění v rámci předplatného pro správu

V případě větších prostředí, která zahrnují více předplatných a mají centrální oddělení IT, které vlastní monitorování a dodržování předpisů, vytvořte páry pracovních prostorů a účtů Automation v předplatném správy IT. V tomto modelu prostředky virtuálních počítačů v geografickém úložišti ukládají svá data v příslušném geografickém pracovním prostoru v předplatném správy IT. Týmy aplikací, které potřebují spouštět úlohy služby Automation, ale kteří nevyžadují propojený pracovní prostor a účty Automation, můžou vytvářet samostatné účty Automation ve vlastních předplatných aplikací.

![Model pracovního prostoru pro rozsáhlá prostředí](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Decentralizované umístění

V alternativním modelu pro velká prostředí může zodpovědnost za opravy a správu nacházet s vývojem aplikací. V takovém případě byste měli umístit páry pro pracovní prostor a účty Automation v předplatných týmu aplikací vedle jejich jiných prostředků.

  ![Model účtu pracovního prostoru pro decentralizovaná prostředí](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Vytvoření pracovního prostoru a účtu Automation

Až se rozhodnete, jak nejlépe umístit a uspořádat dvojice pracovních prostorů a účtů, budete muset před zahájením procesu připojování ověřit, že jste tyto prostředky vytvořili. Příklady automatizace zahrnuté později v těchto pokynech vytvoří pro vás pár účtů v pracovním prostoru a službě Automation. Pokud ale nemáte existující dvojici v pracovním prostoru a účtu Automation, budete ji muset vytvořit, pokud chcete připojit pomocí portálu.

Pokud chcete vytvořit Log Analytics pracovní prostor pomocí Azure Portal, přečtěte si téma [Vytvoření pracovního prostoru](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). Potom vytvořte účet služby Automation pro každý pracovní prostor podle kroků v části [Vytvoření účtu Azure Automation](https://docs.microsoft.com/azure/automation/automation-quickstart-create-account).

> [!NOTE]
> Při vytváření účtu služby Automation prostřednictvím Azure Portal se výchozí chování pokusí vytvořit účty Spustit jako pro prostředky Azure Resource Manager a klasický model nasazení. Pokud ve vašem prostředí nemáte klasické virtuální počítače a nejste spolusprávcem předplatného, portál vytvoří účet Spustit jako pro Správce prostředků, ale při nasazování účtu Spustit jako pro Azure Classic se vygeneruje chyba. Pokud nechcete podporovat klasické prostředky, můžete tuto chybu ignorovat.
>
> Účty Spustit jako můžete vytvořit také pomocí [prostředí PowerShell](https://docs.microsoft.com/azure/automation/manage-runas-account#create-run-as-account-using-powershell).

## <a name="next-steps"></a>Další kroky

Naučte se, jak [vaše servery](./onboarding-overview.md) připojit ke službám pro správu Azure.

> [!div class="nextstepaction"]
> [Připojování ke službám Azure Server Management](./onboarding-overview.md)
