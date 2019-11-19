---
title: Nasazení cílové zóny migrace v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak cílovou zónu migrace v Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, setup
ms.openlocfilehash: 528864cab448ef2e6ead89b16ee174cc2c405401
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/18/2019
ms.locfileid: "74159570"
---
# <a name="deploy-a-migration-landing-zone"></a>Nasazení cílové zóny migrace

Termín *cílová zóna migrace* se používá k popisu prostředí, které je zřízené a připravené k hostování úloh migrovaných z místního prostředí do Azure. Zóna cílové migrace je finální doručení příručky pro instalaci Azure. Tento článek spojuje všechna témata týkající se připravenosti v tomto průvodci a používá rozhodnutí učiněná při nasazení první cílové zóny migrace.

Následující oddíly popisují cílovou zónu, která se běžně používá k vytvoření prostředí vhodného pro použití během migrace. Prostředí nebo cílová zóna popsaná v tomto článku je také zachycená v podrobném plánu Azure. Podrobný plán cílové zóny migrace architektury přechodu na cloud můžete použít k nasazení definovaného prostředí jediným kliknutím.

## <a name="purpose-of-the-blueprint"></a>Účel podrobného plánu

Podrobný plán cílové zóny migrace architektury přechodu na cloud vytváří cílovou zónu. Tato cílová zóna je úmyslně omezená. Je navržená tak, aby se vytvořil konzistentní výchozí bod, který poskytuje prostor k seznámení s infrastrukturou jako kódem. U některých aktivit migrace může být tato cílová zóna dostačující ke splnění vašich potřeb. Je také možné, že budete potřebovat něco v podrobném plánu změnit tak, aby se splnila vaše jedinečná omezení.

## <a name="blueprint-alignment"></a>Sladění podrobného plánu

Na následujícím obrázku je znázorněn podrobný plán cílové zóny migrace architektury přechodu na cloud ve vztahu ke složitosti architektury a požadavkům na dodržování předpisů.

![Sladění podrobného plánu](../../_images/ready/blueprint-overview.png)

- Písmeno A je umístěné uvnitř křivky, která označuje rozsah tohoto podrobného plánu. Tento rozsah má vyjadřovat, že tento podrobný plán pokrývá omezenou složitost architektury, ale je založený na relativně průměrných požadavcích na dodržování předpisů.
- Zákazníkům, kteří mají vysoký stupeň složitosti a přísné požadavky na dodržování předpisů, může lépe vyhovovat rozšířený podrobný plán partnera nebo jeden ze [vzorových podrobných plánů založených na standardech](https://docs.microsoft.com/azure/governance/blueprints/samples).
- Většina požadavků zákazníků spadá někam mezi tyto dva extrémy. Písmeno B představuje proces popsaný v článcích o [aspektech cílových zón](../considerations/index.md). Pro zákazníky v této oblasti můžete použít průvodce rozhodováním obsažené v těchto článcích k identifikaci uzlů, které se mají přidat do podrobného plánu cílové zóny migrace architektury přechodu na cloud. Tento přístup umožňuje přizpůsobit podrobný plán vašim potřebám.

## <a name="use-this-blueprint"></a>Použití tohoto podrobného plánu

Než použijete podrobný plán cílové zóny migrace architektury přechodu na cloud, přečtěte si následující předpoklady, rozhodnutí a pokyny k implementaci.

## <a name="assumptions"></a>Předpoklady

Při definování této počáteční cílové zóny se použily následující předpoklady nebo omezení. Pokud tyto předpoklady odpovídají vašim omezením, můžete podrobný plán použít k vytvoření první cílové zóny. Plán lze také rozšířit a vytvořit tak podrobný plán cílové zóny, který vyhovuje vašim jedinečným omezením.

- **Omezení předplatného:** Toto úsilí o přijetí neočekává překročení [limitů předplatného](https://docs.microsoft.com/azure/azure-subscription-service-limits). Dva běžné indikátory jsou překročení 25 000 virtuálních počítačů nebo 10 000 vCPU.
- **Dodržování předpisů:** V této cílové zóně nejsou potřeba žádné požadavky na dodržování předpisů od jiných výrobců.
- **Složitost architektury:** Složitost architektury nevyžaduje další produkční odběry.
- **Sdílené služby:** V Azure nejsou žádné sdílené služby, které vyžadují, aby se toto předplatné zpracovalo jako paprskový uzel v architektuře hvězdicové architektury.

Pokud se zdá, že tyto předpoklady odpovídají vašemu aktuálnímu prostředí, může být tento plán dobrým základem pro zahájení vytváření cílové zóny.

## <a name="decisions"></a>Rozhodnutí

V podrobném plánu cílové zóny jsou zastoupena následující rozhodnutí.

| Součást | Rozhodnutí | Alternativní přístupy |
|---------|---------|---------|
|Nástroje pro migraci|Nasadí se Azure Site Recovery a vytvoří se projekt Azure Migrate.|[Průvodce rozhodováním ohledně nástrojů pro migraci](../../decision-guides/migrate-decision-guide/index.md)|
|Protokolování a monitorování|Bude zřízený pracovní prostor Operational Insights a účet úložiště pro diagnostiku.|         |
|Síť|Vytvoří se virtuální síť s podsítěmi pro bránu, firewall, jumpbox a cílovou zónu.|[Rozhodnutí o síti](../considerations/networking-options.md)|
|Identita|Předpokládá se, že předplatné je už přidružené k instanci Azure Active Directory.|[Osvědčené postupy správy identit](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json)         |
|Zásady|Tento podrobný plán v současné době předpokládá, že se nemají použít žádné zásady Azure.|         |
|Návrh předplatného|Neuvedeno – Navrženo pro jedno produkční předplatné.|[Škálování předplatných](../azure-best-practices/scaling-subscriptions.md)|
|Skupiny pro správu|Neuvedeno – Navrženo pro jedno produkční předplatné.|[Škálování předplatných](../azure-best-practices/scaling-subscriptions.md)         |
|Skupiny prostředků|Neuvedeno – Navrženo pro jedno produkční předplatné.|[Škálování předplatných](../azure-best-practices/scaling-subscriptions.md)         |
|Data|Nevztahuje se|[Výběr správné možnosti SQL Server v dokumentaci k Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) a [Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Úložiště|Nevztahuje se|[Pokyny k Azure Storage](../considerations/storage-options.md)         |
|Standardy pojmenování a označování|Nevztahuje se|[Osvědčené postupy pojmenování a označování](../azure-best-practices/naming-and-tagging.md)         |
|Správa nákladů|Nevztahuje se|[Sledování nákladů](../azure-best-practices/track-costs.md)|
|Služby Compute|Nevztahuje se|[Možnosti služby Compute](../considerations/compute-options.md)|

## <a name="customize-or-deploy-a-landing-zone-from-this-blueprint"></a>Přizpůsobení nebo nasazení cílové zóny z tohoto podrobného plánu

Přečtěte si další informace a Stáhněte si referenční ukázku v tématu Migrace cílové zóny v rámcové dokumentaci k nasazení nebo přizpůsobení ze [vzorků Azure modrotisky](https://docs.microsoft.com/azure/governance/blueprints/samples).

Ukázky podrobných plánů jsou k dispozici také na portálu. Podrobnosti o tom, jak vytvořit podrobný plán, najdete v tématu [plány Azure](./govern-org-compliance.md?tabs=azureblueprints#create-a-blueprint).

Pokyny k přizpůsobení, které by se měly provést v tomto podrobném plánu nebo v výsledné cílové zóně, najdete v článcích o [aspektech cílových zón](../considerations/index.md).

## <a name="next-steps"></a>Další kroky

Po nasazení cílové zóny migrace budete připravení migrovat úlohy do Azure.
Pokyny k nástrojům a procesům, které jsou potřeba k migraci první úlohy, najdete v [Průvodci migrací do Azure](../../migrate/azure-migration-guide/index.md).

> [!div class="nextstepaction"]
> [Migrace první úlohy pomocí Průvodce migrací do Azure](../../migrate/azure-migration-guide/index.md)
