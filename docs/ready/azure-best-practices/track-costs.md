---
title: Sledování nákladů napříč organizačními jednotkami, prostředími a projekty
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Sledování nákladů napříč organizačními jednotkami, prostředími a projekty
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 67313af2166fbd8dab0f66abb8c6477079a049ad
ms.sourcegitcommit: 945198179ec215fb264e6270369d561cb146d548
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2019
ms.locfileid: "71967758"
---
# <a name="track-costs-across-business-units-environments-or-projects"></a>Sledování nákladů napříč organizačními jednotkami, prostředími a projekty

[Budování nákladově orientované organizace](../../organize/cost-conscious-organization.md) vyžaduje viditelnost a správně definovaný přístup (nebo rozsah) k datům souvisejícím s náklady. Tento článek o osvědčených postupech popisuje rozhodnutí a implementační přístupy k vytváření mechanismů sledování.

![Osnova procesu s ohledem na náklady](../../_images/ready/cost-optimization-process.png)

## <a name="establish-a-well-managed-environment-hierarchy"></a>Vytvoření hierarchie dobře spravovaného prostředí

Řízení nákladů, podobně jako zásady správného řízení a jiné konstrukce správy, závisí na dobře spravovaném prostředí. Vytvoření takového prostředí (zejména složitého) vyžaduje konzistentní procesy v klasifikaci a organizaci všech prostředků.

Prostředky zahrnují všechny virtuální počítače, zdroje dat a aplikace nasazené do cloudu. Azure poskytuje několik mechanismů pro klasifikaci a organizování prostředků. V tématu o [škálování s více předplatnými Azure](../considerations/scaling-subscriptions.md) naleznete podrobné informace o možnostech organizace prostředků na základě více kritérií za účelem vytvoření dobře spravovaného prostředí. Tento článek se zaměřuje na použití základních konceptů Azure k zajištění viditelnosti nákladů na cloud.

### <a name="classification"></a>Klasifikace

*Označování*  je snadný způsob klasifikace prostředků. Označení přidruží metadata k prostředku. Tato metadata lze použít ke klasifikaci prostředků na základě různých datových bodů. Při používání značek ke klasifikaci prostředků v rámci řízení nákladů, společnosti často potřebují následující značky: organizační jednotka, oddělení, fakturační kód, zeměpisná oblast, prostředí, projekt a úloha nebo „kategorizace aplikací“. Azure Cost Management může tyto značky použít k vytváření různých zobrazení dat o nákladech.

Označování je primární způsob, jak porozumět datům v jakémkoli vykazování nákladů. Jedná se o základní součást všech dobře spravovaných prostředí. Je to také první krok při vytváření řádných zásad správného řízení jakéhokoli prostředí.

Prvním krokem při přesném sledování informací o nákladech napříč organizačními jednotkami, prostředími a projekty je definování standardu označování. Druhým krokem je zajištění konzistentního uplatňování tohoto standardu označování. Následující články vám mohou pomoci provést každý z těchto kroků:

- [Vytvoření standardů pojmenování a označování](../considerations/naming-and-tagging.md)
- [Vytvoření MVP pro zásady správného řízení pro vynucování standardů označování](../../govern/guides/complex/index.md)

### <a name="resource-organization"></a>Organizace prostředků

Existují různé přístupy k uspořádání prostředků. Tato část popisuje osvědčené postupy založené na potřebách velké firmy s nákladovými strukturami rozloženými napříč organizačními jednotkami, zeměpisnými oblastmi a organizacemi IT. Podobný osvědčený postup pro menší, méně složitou organizaci je dostupný v [základní příručce Enterprise zásad správného řízení podniku](../../govern/guides/standard/index.md).

Pro velký podnik vytvoří následující model pro skupiny pro správu, předplatná a skupiny prostředků hierarchii, která umožní každému týmu mít správnou úroveň viditelnosti k plnění svých povinností. Pokud podnik potřebuje kontrolu nákladů, aby se zabránilo překročení rozpočtu, může na předplatná v této struktuře použít nástroje správného řízení, jako Azure Blueprints nebo Azure Policy, a rychle tak blokovat budoucí chyby v nákladech.

![Diagram organizace prostředků pro velký podnik](../../_images/govern/large-enterprise-resource-organization.png)

V předchozím diagramu obsahuje kořen hierarchie skupiny pro správu uzel pro každou organizační jednotku. V tomto příkladu potřebuje nadnárodní společnost přehled o regionálních organizačních jednotkách, takže vytvoří uzel pro zeměpisnou oblast v rámci každé organizační jednotky v hierarchii.

V rámci každé zeměpisného oblasti je k dispozici samostatný uzel pro provozní a neprovozní prostředí, který izoluje řízení nákladů, přístupu a zásad správného řízení. Společnost využívá předplatná k další izolaci produkčních prostředí s různou mírou vlivu na provozní výkonnost, aby mohla provádět efektivnější operace a moudré investice do provozu. Společnost také používá skupiny prostředků k zachytávání nasaditelných jednotek funkce, označovaných jako aplikace.

Diagram zobrazuje osvědčené postupy, ale nezahrnuje tyto možnosti:

- Mnoho společností působí v jediné geopolitické oblasti. Tento přístup snižuje potřebu diverzifikace správních disciplín nebo údajů o nákladech na základě místních požadavků na suverenitu dat. V těchto případech je uzel pro zeměpisnou oblast zbytečný.
- Některé společnosti dávají přednost dalšímu oddělení prostředí pro vývoj, testování a kontrolu kvality do samostatných předplatných.
- Když společnost integruje tým CCoE, můžou předplatná sdílených služeb v jednotlivých uzlech zeměpisných oblastí snížit počet duplicitních prostředků.
- Při méně rozsáhlém přechodu na cloud může být použita mnohem menší hierarchie správy. Běžně je vidět jeden kořenový uzel pro firemní IT s jedinou úrovní podřízených uzlů v hierarchii pro různá prostředí. Nejedná se o porušení osvědčených postupů pro dobře spravované prostředí. Je však obtížnější použít přístupový model s minimálními právy pro řízení nákladů a další důležité funkce.

Zbývající část tohoto článku předpokládá použití osvědčeného postupu popsaného v předchozím diagramu. Následující články vám můžou pomoct aplikovat přístup k organizaci prostředků, který nejlépe vyhovuje vaší společnosti:

- [Škálování s využitím několika předplatných Azure](../considerations/scaling-subscriptions.md)
- [Nasazení MVP pro zásady správného řízení k řízení standardů dobře spravovaného prostředí](../../govern/guides/complex/index.md)

## <a name="provide-the-right-level-of-cost-access"></a>Poskytnutí správné úrovně přístupu k nákladům

Správa nákladů je týmová aktivita. Část připravenosti organizace v architektuře přechodu na cloud definuje malý počet základních týmů a popisuje, jak tyto týmy podporují přechod na cloud. Tento článek vysvětluje definice týmů a definuje rozsah a role, které mají být přiřazeny členům každého týmu, kvůli zajištění správné úrovně viditelnosti dat správy nákladů.

- *Role* definují, co může uživatel provádět s různými prostředky.
- *Rozsah* definuje, se kterými prostředky (uživatel, skupina, instanční objekt nebo spravovaná identita) uživatel může tyto akce provádět.

Obecně doporučujeme použít při přidělování osob k různým rolím a rozsahům model s minimálním oprávněním.

### <a name="roles"></a>Role

Azure Cost Management podporuje následující předdefinované role pro každý rozsah:

- [Vlastník](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner). Může zobrazit náklady a spravovat vše včetně konfigurace nákladů.
- [Přispěvatel](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Může zobrazit náklady a spravovat vše včetně konfigurace nákladů, ale bez řízení přístupu.
- [Čtenář](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader). Může zobrazit vše, včetně údajů o nákladech a konfigurace, ale nemůže provádět žádné změny.
- [Přispěvatel služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor). Může zobrazit náklady a spravovat jejich konfiguraci.
- [Čtenář služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) Může zobrazit data a konfiguraci nákladů.

Obecně se doporučuje členům všech týmů přiřadit roli Přispěvatel služby Cost Management. Tato role uděluje přístup k vytváření a správě rozpočtů a exportů za účelem efektivnějšího monitorování a vykazování nákladů. Pro členy [týmu cloudové strategie](../../organize/cloud-strategy.md) byste však měli nastavit jen roli Čtenář služby Cost Management. a to proto, že v rámci nástroje Azure Cost Management nejsou zapojeni do stanovování rozpočtů.

### <a name="scope"></a>Scope

Následující nastavení rozsahu a rolí vytvoří požadovanou viditelnost pro správu nákladů. Tento osvědčený postup může vyžadovat menší změny v souladu s rozhodnutím o organizaci prostředků.

- [Tým přechodu na cloud](../../organize/cloud-adoption.md). Zodpovědnost za probíhající optimalizační změny vyžaduje přístup Přispěvatel služby Cost Management na úrovni skupiny prostředků.

  - **Pracovní prostředí**. Tým pro přechod na cloud by již měl mít alespoň přístup [Přispěvatel](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) ke všem ovlivněným skupinám prostředků, nebo alespoň ke skupinám souvisejícím s vývojem a testováním nebo probíhajícími aktivitami nasazení. Není vyžadováno žádné další nastavení rozsahu.
  - **Provozní prostředí**. Po zřízení správného oddělení odpovědnosti tým přechodu na cloud pravděpodobně nebude mít nadále přístup ke skupinám prostředků souvisejících s jeho projekty. Skupiny prostředků, které podporují provozní instance svých úloh, budou potřebovat další rozsah, aby tento tým viděl dopad svých rozhodnutí na provozní náklady. Nastavení rozsahu [Přispěvatel služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) pro skupiny provozních prostředků pro tento tým umožní týmu sledovat náklady a nastavovat rozpočty na základě využití a průběžných investic do podporovaných úloh.

- [Tým cloudové strategie](../../organize/cloud-strategy.md). Zodpovědnost za sledování nákladů napříč více projekty a organizačními jednotkami vyžaduje přístup Čtenář služby Cost Management na kořenové úrovni hierarchie skupiny pro správu.

  - Přiřaďte tomuto týmu přístup [Čtenář služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) ve skupině pro správu. Tím zajistíte nepřetržitou viditelnost všech nasazení přidružených k předplatným, která se řídí hierarchií této skupiny správy.

- [Tým zásad správného řízení cloudu](../../organize/cloud-governance.md). Odpovědnost za správu nákladů, sladění rozpočtu a vykazování v rámci všech činností přechodu na cloud vyžaduje přístup Přispěvatel služby Cost Management na kořenové úrovni hierarchie skupiny pro správu.

  - V dobře spravovaném prostředí má tým zásad správného řízení cloudu pravděpodobně ještě vyšší úroveň přístupu, takže další přiřazení rozsahu [Přispěvatel pro Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) není nutné.

- [CCoE](../../organize/cloud-center-of-excellence.md). Zodpovědnost za správu nákladů souvisejících se sdílenými službami vyžaduje přístup Přispěvatel služby Cost Management na úrovni předplatného. Kromě toho může tento tým vyžadovat přístup Přispěvatel služby Cost Management ke skupinám prostředků nebo předplatným, které obsahují prostředky nasazené automatizacemi CCoE, aby porozuměli tomu, jak tyto automatizace ovlivňují náklady.

  - **Sdílené služby**. Když je zapojen tým CCoE, osvědčeným postupem je, že prostředky spravované CCoE jsou podporovány z předplatného centralizované sdílené služby v rámci hvězdicové topologie sítě. V tomto scénáři má CCoE k tomuto předplatnému pravděpodobně přístup přispěvatele nebo vlastníka, takže další přiřazení rozsahu [Přispěvatel služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) není nutné.
  - **Automatizace a řízení CCoE**. Tým CCoE obvykle poskytuje ovládací skripty a skripty pro automatizované nasazení týmům přechodu na cloud. Úkolem CCoE je porozumět tomu, jak tyto akcelerátory ovlivňují náklady. Aby tento přehled získal, tým potřebuje přístup [Přispěvatel služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) k jakýmkoli skupinám prostředků nebo předplatným, které tyto akcelerátory spouští.

- **Tým cloudových operací**. Zodpovědnost za správu průběžných nákladů v provozních prostředích vyžaduje přístup Přispěvatel služby Cost Management ke všem provozním předplatným.

  - Obecné doporučení přináší provozní a nevýrobní prostředky do samostatných předplatných, která se řídí uzly hierarchie skupiny pro správu, která je přidružená k produkčním prostředím. V dobře spravovaném prostředí již členové provozního týmu pravděpodobně mají oprávnění vlastníka nebo přispěvatele k provozním předplatným, takže role [Přispěvatel služby Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) není nutná.

## <a name="additional-cost-management-resources"></a>Další prostředky pro správu nákladů

Azure Cost Management je dobře zdokumentovaný nástroj pro stanovení rozpočtů a získání přehledu o nákladech na cloud pro Azure nebo AWS. Poté co vytvoříte přístup k hierarchii dobře spravovaného prostředí, vám následující články pomohou tento nástroj použít ke sledování a řízení nákladů.

### <a name="get-started-with-azure-cost-management"></a>Začínáme s Azure Cost Management

Další informace o tom, jak začít s pracovat nástrojem Azure Cost Management, najdete v tématu pojednávajícím o [optimalizaci investic do cloudu pomocí Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json).

### <a name="use-azure-cost-management"></a>Práce s nástrojem Azure Cost Management

- [Vytváření a správa rozpočtů](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets)
- [Export dat o nákladech](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data)
- [Optimalizace nákladů na základě doporučení](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations)
- [Použití upozornění na náklady ke sledování využití a výdajů](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending)

### <a name="use-azure-cost-management-to-govern-aws-costs"></a>Použití Azure Cost Management k řízení nákladů AWS

- [Integrace sestavy nákladů a využití služby AWS](https://docs.microsoft.com/azure/cost-management/aws-integration-set-up-configure)
- [Správa nákladů AWS](https://docs.microsoft.com/azure/cost-management/aws-integration-manage)

### <a name="establish-access-roles-and-scope"></a>Vytvoření přístupu, rolí a rozsahu

- [Principy rozsahu správy nákladů](https://docs.microsoft.com/azure/cost-management/understand-work-scopes)
- [Nastavení rozsahu pro skupinu prostředků](https://docs.microsoft.com/azure/role-based-access-control/quickstart-assign-role-user-portal)
