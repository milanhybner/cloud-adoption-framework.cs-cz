---
title: Připravenost na dovednosti pro monitorování cloudu
description: Připravenost na dovednosti pro monitorování cloudu
author: BrianBlanchard
ms.author: magoedte
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2cfa4ec997dc211ad50eafcb723c58d934c45d10
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527028"
---
<!-- cSpell:ignore kusto ITIL -->

# <a name="skills-readiness-for-cloud-monitoring"></a>Připravenost na dovednosti pro monitorování cloudu

Během fáze plánování cesty migrace je cílem vyvinout plány potřebné k implementaci příručky. Plány musí také zahrnovat způsob, jakým budete pracovat s těmito úlohami před jejich přechodem nebo uvolněním do produkčního prostředí, a ne následně. Obchodní účastníci očekávají cenné služby a očekávají je bez přerušení. Zaměstnanci oddělení IT si uvědomuje, že potřebují vědět nové dovednosti a přizpůsobovat jim, aby mohli efektivně využívat integrované služby Azure pro efektivní monitorování prostředků v Azure a hybridních prostředích.

Rozvoj potřebných dovedností lze urychlit pomocí následujících studijních programů:

- Úvod k [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) popisuje základní koncepty správy a nasazování prostředků Azure. Pracovníci IT, kteří spravují monitorování v rámci podniku, by měli pochopit rozsahy správy, řízení přístupu na základě role (RBAC) pomocí nástroje. Azure Resource Manager šablony a správu prostředků pomocí Azure CLI a Azure PowerShell.

- Naučte se zabezpečit prostředky pomocí zásad, řízení přístupu na základě rolí a dalších služeb Azure díky zobrazení [implementace zabezpečení správy prostředků v Azure](https://docs.microsoft.com//learn/paths/implement-resource-mgmt-security).

- Úvod do [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) vám pomůže zjistit, jak můžete pomocí Azure Policy vytvářet, přiřazovat a spravovat zásady. Azure Policy můžou nasazovat a konfigurovat agenty Azure Monitor, povolit monitorování pomocí Azure Monitor pro virtuální počítače a Azure Security Center, nasazovat nastavení diagnostiky, auditovat nastavení konfigurace hostů a další.

- Seznámení s [rozhraním příkazového řádku Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest) (CLI), které je naše prostředí příkazového řádku pro více platforem pro správu prostředků Azure. Přečtěte si také téma Úvod do [Azure PowerShell](https://docs.microsoft.com/powershell/azure/?view=azps-3.6.1). LinkedIn nabízí jako součást [nástrojů pro správu Azure](https://www.linkedin.com/learning/learning-azure-management-tools)na nejvyšší úrovni výukového kurzu, relace zahrnující rozhraní příkazového řádku Azure a programovací jazyky prostředí PowerShell:

  - [Použijte rozhraní příkazového řádku Azure](https://www.linkedin.com/learning/learning-azure-management-tools/use-the-azure-cli).
  - [Začínáme s Azure PowerShell](https://www.linkedin.com/learning/learning-azure-management-tools/understand-azure-powershell)

- Naučte se vytvářet [dotazy protokolu v Azure monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries).  Dotazovací jazyk Kusto je primárním prostředkem pro psaní dotazů protokolu Azure Monitor k prozkoumávání a analýze dat protokolů mezi shromažďovanými daty z Azure a závislostmi aplikací hybridních prostředků, včetně živé aplikace.

- Seznamte se s tím, jak [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) pomáhají Zobrazit dostupnost a výkon svých aplikací a služeb z jednoho místa. Pluralsight nabízí následující kurzy, které vám pomůžou:

  - [Microsoft Azure sledování a Správa IaaS](https://www.pluralsight.com/courses/azure-iaas-monitoring-management-getting-started) vám pomůže naučit se používat Azure monitor k provádění základních monitorování úloh běžících na IaaS.

  - [Sledování Microsoft Azure prostředků a úlohách](https://www.pluralsight.com/courses/microsoft-azure-resources-workloads-monitoring) pomáhá naučit se používat nástroje pro monitorování Microsoft Azure k monitorování prostředků sítě Azure (stejně jako Prem).

  - [Microsoft Azure inženýr DevOps: optimalizovat mechanismy pro zpětnou vazbu](https://www.pluralsight.com/courses/microsoft-azure-optimize-feedback-mechanisms) vám pomůžou připravit se na použití Azure monitor, včetně Application Insights a Log Analytics k monitorování a optimalizaci vašich webových aplikací.

  - [Microsoft Azure PlayBook monitoring Database](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) vám pomůže naučit se implementovat a používat monitorování Azure SQL Database, Azure SQL Data Warehouse a Azure Cosmos DB.

- Pomocí [ARC Azure pro servery](https://docs.microsoft.com/azure/azure-arc/servers/overview)se dozvíte, jak můžete spravovat počítače s Windows a Linux hostovanými mimo Azure podobně jako při správě nativních virtuálních počítačů Azure.

## <a name="deeper-skills-exploration"></a>Nabytí hlubších znalostí

Kromě těchto prvotních materiálů pro rozvoj dovedností je k dispozici celá řada dalších možností vzdělávání.

### <a name="typical-mappings-of-cloud-it-roles"></a>Typická přiřazení IT rolí v cloudu

Microsoft a partneři nabízejí řadu možností pro všechny cílové skupiny, které umožňují rozvinout dovednosti v oblasti služeb Azure:

- [Microsoft IT pro kariéry Center](https://www.microsoft.com/itpro): slouží jako bezplatný online prostředek, který vám pomůže namapovat cestu k kariéry cloudu. Zjistěte, co oboroví specialisté navrhují pro vaši roli v cloudu a jaké dovednosti potřebujete. Studujte podle studijního plánu svým vlastním tempem a získejte dovednosti, které potřebujete nejvíce.

Využijte [certifikačních školení a zkoušky pro Microsoft Azure]( https://www.microsoft.com/learning/azure-certification.aspx) a získejte pro svoje znalosti oficiální potvrzení.

## <a name="azure-devops-and-project-management"></a>Správa projektů a Azure DevOps

Hybridní cloudové prostředí je přerušuje pomocí nedefinovaných rolí, odpovědností a aktivit. Organizace se musí přesunout na moderní postupy pro správu služeb, včetně agilních a DevOpsch metodologií, aby lépe vyhovovaly vašim požadavkům na transformaci a optimalizaci pro dnešní firmy, a to díky jednoduššímu a efektivnímu způsobu.

V rámci migrace na platformu monitorování cloudu, kterou IT tým zodpovídá za správu monitorování v podniku, musí zahrnovat agilní školení a účast v DevOps aktivitách. To zahrnuje i sledování *vývoje* v DevOps, a to díky tomu, že pobírají požadavky a zajišťují uspořádané agilní požadavky, aby bylo možné doručovat minimální řešení pro monitorování, která jsou v souladu s podnikovými požadavky. Aby Správa zdrojového kódu spravovala balíčky řešení iterativního monitorování a všechny další související materiály, připojte svůj Azure DevOps Server projekt k úložišti serveru GitHub Enterprise. To poskytuje propojení mezi potvrzeními GitHubu a žádostmi o přijetí změn pracovních položek. GitHub Enterprise můžete použít pro vývoj v rámci podpory nepřetržitého monitorování a nasazení a při použití Azure Boards k plánování a sledování práce.

Pokud se chcete dozvědět víc, přečtěte si následující informace:

- [Začínáme s Azure DevOps](https://docs.microsoft.com/learn/modules/get-started-with-devops).

- [Další informace o DevOps Dojo – White pás Foundation](https://docs.microsoft.com/learn/paths/devops-dojo-white-belt-foundation)

- [Vývoj postupů DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)

- [Automatizace nasazení pomocí Azure DevOps](https://docs.microsoft.com/learn/paths/automate-deployments-azure-devops)

## <a name="other-considerations"></a>Další požadavky

Zákazníci se často bojovat ke správě, údržbě a poskytování předpokládaných firem (a organizacím IT) pro služby, které se účtují v rámci poskytování. Monitorování se považuje za jádro správy infrastruktury a firmy a zaměřuje se na měření kvality služeb a zkušeností zákazníků.  Aby bylo možné dosáhnout těchto cílů, rozložte základy pomocí ITSM ve spojení s DevOps, což vám pomůže týmu monitorování, jak spravovat, dodávat a podporovat monitorovací službu. Přijetím ITSM Framework umožňuje týmu monitorování fungovat jako poskytovatel a získat jeho rozpoznávání jako důvěryhodný obchodní aktivátor, a to tak, že bude sjednotit strategické cíle a potřeby organizace.

Přečtěte si následující informace, abyste pochopili aktualizace pro nejoblíbenější ITSM Framework [ITIL v4 a Cloud Computing White Paper](https://www.axelos.com/case-studies-and-white-papers/itil-4-and-the-cloud), které se zaměřují na připojení stávajících pokynů k ITIL s osvědčenými postupy z DevOps, agilního a štíhlého. Zvažte také [referenční architekturu IT4IT](https://www.opengroup.org/it4it) , která poskytuje alternativní podrobný plán na jejich transformaci pomocí architektury procesu nezávislá.

## <a name="learn-more"></a>Další informace

Pokud chcete zjistit další způsoby učení, Projděte si [katalog Microsoft Learn](https://docs.microsoft.com/learn/browse). Pomocí filtru role můžete v rámci své role zarovnat studijních cest.
