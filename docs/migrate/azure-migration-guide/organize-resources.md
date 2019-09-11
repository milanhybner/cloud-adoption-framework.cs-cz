---
title: Efektivní uspořádání prostředků Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Osvědčené postupy efektivního uspořádání prostředků Azure, které usnadňují správu
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: dbfc365f874b9ad6045454c53270275a5008935d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818740"
---
# <a name="organize-your-azure-resources"></a>Uspořádání prostředků Azure

Následující funkce a osvědčené postupy použijte k zabezpečení prostředků, které jsou důležité pro váš systém. Označit prostředky, abyste je mohli sledovat podle hodnot, které dávají smysl pro vaši organizaci.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="azure-management-groups-and-hierarchytabazuremanagmentgroupsandhierarchy"></a>[skupiny pro správu Azure](#tab/AzureManagmentGroupsAndHierarchy)

Organizační struktura pro prostředky v Azure má čtyři úrovně: skupiny pro správu, předplatná, skupiny prostředků a prostředky. Následující obrázek ukazuje vztah mezi těmito úrovněmi.

![Diagram znázorňující vztahy v hierarchii správy](./media/organize-resources/scope-levels.png)

- **Skupiny pro správu:** Toto jsou kontejnery, které pomáhají spravovat přístup, zásady a dodržování předpisů pro několik předplatných. Všechna předplatná ve skupině pro správu automaticky dědí podmínky, které se na příslušnou skupinu pro správu vztahují.
- **Předplatná:** Předplatné seskupuje uživatelské účty a prostředky vytvořené těmito uživatelskými účty. Pro každé předplatné existují omezení nebo kvóty množství prostředků, které můžete vytvořit a využívat. Organizace můžou pomocí předplatných spravovat náklady a prostředky vytvořené uživateli, týmy nebo v rámci projektů.
- **Skupiny prostředků:** Skupina prostředků je logický kontejner, ve kterém se nasazují a spravují prostředky Azure, jako například webové aplikace, databáze a účty úložiště.
- **Zdroje a prostředky:** Prostředky jsou instance vytvořených služeb, jako například virtuální počítače, úložiště nebo databáze SQL.

## <a name="scope-of-management-settings"></a>Rozsah nastavení správy

Nastavení správy, jako jsou zásady a řízení přístupu na základě role, můžete používat na jakékoli úrovni správy. Vybraná úroveň určuje rozsah použití nastavení. Nižší úrovně dědí nastavení z vyšších úrovní. Když například použijete zásadu pro předplatné, tato zásada se použije také pro všechny skupiny prostředků a prostředky v tomto předplatném.

Obvykle je vhodné používat důležitá nastavení na vyšších úrovních a nastavení související s požadavky konkrétního projektu na nižších úrovních. Například můžete chtít zajistit, aby se všechny prostředky vaší organizace nasazovaly do konkrétních oblastí. Provedete to tak, že pro předplatné použijete zásadu, která udává povolená umístění. Když ostatní uživatelé ve vaší organizaci přidají nové skupiny prostředků a prostředky, automaticky se vynutí použití některého z povolených umístění. Další informace o zásadách najdete v částech tohoto průvodce věnovaných zásadám správného řízení, zabezpečení a dodržování předpisů.

Při plánování strategie dodržování předpisů doporučujeme spolupracovat s lidmi, kteří ve vaší organizaci mají na starost zabezpečení a dodržování předpisů, správu IT, podnikovou architekturu, sítě, finance a pořizování.

::: zone target="docs"

## <a name="create-a-management-level"></a>Vytvoření úrovně správy

Můžete vytvořit skupinu pro správu, další předplatná nebo skupiny prostředků.

### <a name="create-management-group"></a>Vytvoření skupiny pro správu

Vytvořte skupinu pro správu, která pomáhá spravovat přístup, zásady a dodržování předpisů pro několik předplatných.

1. Přejděte do části [Skupiny pro správu](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Vyberte **Přidat skupinu pro správu**.

### <a name="create-subscription"></a>Vytvoření odběru

Pomocí předplatných spravujte náklady a prostředky vytvořené uživateli, týmy nebo v rámci projektů.

1. Přejděte do části [Předplatná](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Vyberte **Přidat**.

### <a name="create-resource-group"></a>Vytvoření skupiny prostředků

Vytvořte skupinu prostředků sdružující prostředky, jako jsou webové aplikace, databáze a účty úložiště, které sdílejí stejný životní cyklus, oprávnění a zásady.

1. Přejděte do části [Skupiny prostředků](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Vyberte **Přidat**.
1. Vyberte **Předplatné**, ve kterém chcete skupinu prostředků vytvořit.
1. Zadejte název do pole **Skupina prostředků**.
1. Vyberte **Oblast** pro umístění skupiny prostředků.

## <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Principy správy přístupu k prostředkům v Azure](../../governance/resource-consistency/azure-resource-access.md)
- [Uspořádání prostředků s využitím skupin pro správu Azure](/azure/azure-resource-manager/management-groups-overview)
- [Omezení služeb předplatného](/azure/azure-subscription-service-limits)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Akce

**Vytvoření skupiny pro správu:**

Vytvořte skupinu pro správu, která pomáhá spravovat přístup, zásady a dodržování předpisů pro několik předplatných.

1. Přejděte do části **Skupiny pro správu**.
1. Vyberte **Přidat skupinu pro správu**.

::: form action="OpenBlade[#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade]" submitText="Go to Management groups" :::

**Vytvoření dalšího předplatného:**

Pomocí předplatných spravujte náklady a prostředky vytvořené uživateli, týmy nebo v rámci projektů.

1. Přejděte do části **Předplatná**.
1. Vyberte **Přidat**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

**Vytvoření skupiny prostředků:**

Vytvořte skupinu prostředků sdružující prostředky, jako jsou webové aplikace, databáze a účty úložiště, které sdílejí stejný životní cyklus, oprávnění a zásady.

1. Přejděte do části **Skupiny prostředků**.
1. Vyberte **Přidat**.
1. Vyberte **Předplatné**, ve kterém chcete skupinu prostředků vytvořit.
1. Zadejte název do pole **Skupina prostředků**.
1. Vyberte **Oblast** pro umístění skupiny prostředků.

::: form action="Create[#create/Microsoft.ResourceGroup]" submitText="Create a resource group" :::

::: zone-end

# <a name="naming-standardstabnamingstandards"></a>[Standardy pro vytváření názvů](#tab/NamingStandards)

Správné standardy pro vytváření názvů pomáhají identifikovat prostředky na portálu, na faktuře i ve skriptech. Asi už máte standardy pro vytváření názvů v místní infrastruktuře. Když do svého prostředí přidáte Azure, měli byste tyto standardy pro vytváření názvů rozšířit i na prostředky Azure. Standardy pro vytváření názvů zefektivňují správu prostředí na všech úrovních. Jako nástroj pro vynucování standardů pro vytváření názvů v celém prostředí Azure můžete použít službu Azure Policy.

::: zone target="docs"

Doporučujeme si projít a využít [pokyny ke vzorům a postupům](/azure/architecture/best-practices/naming-conventions).

>[!TIP]
>Nepoužívejte žádné speciální znaky (`-` nebo `_`) jako první ani poslední znak názvu. Většina ověřovacích pravidel kvůli těmto znakům selže.

::: zone-end

| Entita | Rozsah | Délka | Velikost písmen | Platné znaky | Navrhovaný vzor | Příklad |
| --- | --- | --- | --- | --- | --- | --- |
|Skupina prostředků |Předplatné |1–90 |Malá a velká písmena se nerozlišují. |Alfanumerické znaky, podtržítka, kulaté závorky, pomlčky, tečky (s výjimkou teček na konci) a znaky Unicode |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Skupina dostupnosti |Skupina prostředků |1–80 |Malá a velká písmena se nerozlišují. |Alfanumerické znaky, podtržítka a pomlčky |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Značka |Související entita |512 (název), 256 (hodnota) |Malá a velká písmena se nerozlišují. |Alfanumerické znaky |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tagstabresourcetags"></a>[Značky prostředku](#tab/ResourceTags)

Značky jsou užitečné k rychlé identifikaci prostředků a skupin prostředků. Použijte značky na prostředky Azure pro jejich logické uspořádání podle kategorií. Každá značka se skládá z názvu a hodnoty. Můžete například použít název Prostředí a hodnotu Produkční na všechny prostředky v produkčním prostředí.

Po použití značek můžete načíst všechny prostředky v předplatném s daným názvem a hodnotou značky. Značky umožňují načíst související prostředky z různých skupin prostředků, což pomáhá s uspořádáním prostředků pro účely fakturace nebo správy.

Značky můžete použít také k celé řadě dalších účelů. Mezi běžné způsoby použití patří:

- **Metadata a dokumentace:** Správci můžou snadno zobrazit podrobnosti o prostředcích, na kterých pracují, například pomocí značky ProjectOwner (Vlastník projektu).
- **Automatizace:** Můžete mít pravidelně spouštěné skripty, které můžou provádět akce na základě hodnot značek, jako je například ShutdownTime (Čas vypnutí) nebo DeprovisionDate (Datum uvolnění).
- **Fakturace:** Značky se můžou zobrazit na vaší faktuře. Pomocí nich můžete fakturu segmentovat, například pomocí značky CostCenter (Nákladové středisko) nebo BillTo (Příjemce faktury).

Každý prostředek nebo skupina prostředků může mít maximálně 15 párů název/hodnota značek. Toto omezení se však vztahuje pouze na značky použité přímo na prostředek nebo skupinu prostředků.

Další informace o používání značek najdete v [Centru architektury Azure v zásadách vytváření názvů pro prostředky Azure](../../ready/considerations/name-and-tag.md#metadata-tags).

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Použití značky prostředku

Použití značky na skupinu prostředků:

1. Přejděte do části [Skupiny prostředků](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Vyberte skupinu prostředků.
1. Vyberte **Značky**.
1. Zadejte nový název a hodnotu nebo pomocí rozevíracího seznamu vyberte existující název a hodnotu.

## <a name="learn-more"></a>Další informace

Další informace najdete v tématu [Používání značek k uspořádání prostředků Azure](/azure/azure-resource-manager/resource-group-using-tags).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Akce

**Použití značky prostředku:**

Použití značky na skupinu prostředků:

1. Přejděte do části **Skupiny prostředků**.
1. Vyberte skupinu prostředků.
1. Vyberte **Značky**.
1. Zadejte nový název a hodnotu nebo vyberte existující název a hodnotu.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups]" submitText="Go to resource groups" :::

::: zone-end
