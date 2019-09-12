---
title: Nasazení plánu přijetí do cloudu do Azure DevOps
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nasazení šablony pro plán přijetí do cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 91c1433f300efc3950cb54852a00b5020a992e8f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833723"
---
# <a name="cloud-adoption-plan-and-azure-devops"></a>Plán přijetí do cloudu a Azure DevOps

Azure DevOps je sada cloudových nástrojů pro zákazníky Azure, kteří spravují iterativní projekty. Zahrnuje také nástroje pro správu kanálů nasazení a další důležité aspekty DevOps. 

V tomto článku se dozvíte, jak rychle nasadit nevyřízené položky do Azure DevOps pomocí šablony plánu přijetí v cloudu. Tato šablona zarovnává úsilí o přijetí cloudu do standardizovaného procesu na základě pokynů v rozhraní pro přijetí do cloudu.

## <a name="create-your-cloud-adoption-plan"></a>Vytvoření plánu přijetí do cloudu

Pokud chcete nasadit plán pro přijetí do cloudu, otevřete [generátor ukázek Azure DevOps](https://aka.ms/adopt/plan/generator). Tento nástroj nasadí šablonu do vašeho tenanta Azure DevOps. Použití nástroje vyžaduje následující kroky:

1. Ověřte, jestli je **vybrané pole šablony** nastavené na **plán přijetí**do cloudu. Pokud tomu tak není, vyberte možnost **Zvolit šablonu** a zvolte správnou šablonu.
2. Z rozevíracího seznamu **Vybrat organizaci** vyberte svoji organizaci Azure DevOps.
3. Zadejte název nového projektu. Plán přijetí do cloudu bude mít tento název při nasazení do vašeho tenanta Azure DevOps.
4. Vyberte **vytvořit projekt** pro vytvoření nového projektu ve vašem tenantovi na základě šablony plánu. Indikátor průběhu zobrazuje pokrok v nasazení projektu.
5. Po dokončení nasazení vyberte možnost **Přejít do projektu** a zobrazí se nový projekt.

Po vytvoření projektu pokračujte v této sérii článků, abyste viděli, jak můžete upravit šablonu, aby se narovnala vašemu plánu přijetí do cloudu.

Další podporu a pokyny k tomuto nástroji naleznete v tématu [Azure DevOps Services demo Generator](https://docs.microsoft.com/azure/devops/demo-gen/?toc=%2Fazure%2Fdevops%2Fdemo-gen%2Ftoc.json&bc=%2Fazure%2Fdevops%2Fdemo-gen%2Fbreadcrumb%2Ftoc.json&view=azure-devops).

## <a name="bulk-edit-the-cloud-adoption-plan"></a>Hromadná úprava plánu přijetí cloudu

Po nasazení projektu plánu můžete k jeho úpravě použít aplikaci Microsoft Excel. Je mnohem snazší vytvořit nové úlohy nebo prostředky v plánu pomocí aplikace Excel, než pomocí prostředí Azure DevOps Browser.

Informace o přípravě pracovní stanice pro hromadnou úpravu najdete v tématu [hromadné přidání nebo úprava pracovních položek pomocí aplikace Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="use-the-cloud-adoption-plan"></a>Použití plánu přijetí do cloudu

Plán přijetí do cloudu organizuje aktivity podle typu aktivity:

- **Náměty**: *Námětu* představuje celkovou fázi životního cyklu pro přijetí do cloudu.
- **Funkce**: Funkce se používají k organizování konkrétních cílů v jednotlivých fázích. Například migrace konkrétního zatížení bude jedna funkce.
- **Uživatelské scénáře**: Skupina uživatelských scénářů pracuje na logických kolekcích aktivit na základě konkrétního cíle.
- **Úkoly**: Úkoly představují skutečnou práci, která má být provedena.

V každé vrstvě jsou aktivity seřazeny na základě závislostí. Aktivity jsou propojeny s články v rozhraní pro přijetí do cloudu, které umožňují objasnit cíl nebo úkol.

V zobrazení nevyřízených položek **náměty** se nachází jasné zobrazení plánu přijetí do cloudu. Nápovědu ke změně zobrazení nevyřízených položek **náměty** najdete v článku o [Zobrazení nevyřízených položek](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops#view-a-backlog-or-portfolio-backlog). Z tohoto zobrazení je snadné naplánovat a spravovat práci potřebnou k dokončení aktuální fáze životního cyklu přijetí.

> [!NOTE]
> Aktuální stav plánu přijetí do cloudu se zaměřuje na značné úsilí při migraci. Úkoly týkající se zásad správného řízení, inovací nebo operací se musí naplnit ručně.

## <a name="align-the-cloud-adoption-plan"></a>Zarovnání plánu přijetí do cloudu

Stránky s přehledem pro fáze strategie a plánování životního cyklu přijetí v cloudu – každá odkazuje na [strategii rozhraní pro přijetí do cloudu a na šablonu plánování](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Tato šablona uspořádá rozhodnutí a datové body, které budou zarovnávat šablonu pro plán přijetí cloudu s vašimi konkrétními plány pro přijetí. Pokud jste to ještě neudělali, možná budete chtít dokončit cvičení týkající se [strategie](../business-strategy/index.md) a [plánování](../plan/index.md) před zarovnáním nového projektu.

Následující články podporují zarovnání plánu přijetí do cloudu:

- [Úlohy](./workloads.md): Zarovnejte funkce v rámci Migrace do cloudu námětu a zachyťte každou úlohu, kterou chcete migrovat nebo moderním. Přidejte a upravte tyto funkce, abyste mohli zachytit úsilí k migraci prvních 10 úloh.
- [Prostředky](./assets.md): Jednotlivé prostředky (virtuální počítače, aplikace nebo data) jsou reprezentovány uživatelskými příběhy v rámci jednotlivých úloh. Přidejte a upravte tyto uživatelské scénáře tak, aby byly v souladu s vaší digitální nemovitosti.
- [Racionalizace](./review-rationalization.md): Při definování jednotlivých úloh je možné vyvolávat počáteční předpoklady pro tuto úlohu. To může mít za následek změny úkolů v rámci jednotlivých assetů.
- [Vytvořit plány vydání](./iteration-paths.md): Cesty iterace vytvářejí plány vydání tak, že zarovnají úsilí s různými verzemi a iteracemi.
- [Navázat časové osy](./timelines.md): Definováním počátečního a koncového data pro každou iteraci vytvoříte časovou osu pro správu celkového projektu.

Tyto pět článků vám pomůžou s každou úlohou zarovnání potřebnou k zahájení správy snahy o přijetí. Další krok vám pomůže začít s cvičením na základě zarovnání.

## <a name="next-steps"></a>Další postup

Začněte zarovnávat projekt plánu definováním [a určením priorit úloh](./workloads.md).

> [!div class="nextstepaction"]
> [Definování a stanovení priorit úloh](./workloads.md)
