---
title: Efektivní uspořádání prostředků Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Osvědčené postupy efektivního uspořádání prostředků Azure, které usnadňují správu
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 79102a3664f055489da37fc3de0ec7156c1272ef
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239829"
---
# <a name="organize-your-azure-resources"></a>Uspořádání prostředků Azure

Uspořádání cloudových prostředků je důležité pro zabezpečení, správu a sledování nákladů souvisejících s vašimi úlohami. K uspořádání prostředků můžete použít hierarchie pro správu v rámci platformy Azure, implementovat správné konvence pojmenování a opatřit prostředky značkami.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="azure-management-groups-and-hierarchytabazuremanagmentgroupsandhierarchy"></a>[skupiny pro správu Azure](#tab/AzureManagmentGroupsAndHierarchy)

Azure poskytuje čtyři úrovně rozsahu správy: skupiny pro správu, předplatná, skupiny prostředků a prostředky. Následující obrázek ukazuje vztah mezi těmito úrovněmi.

   ![Diagram znázorňující vztahy v hierarchii správy](./media/organize-resources/scope-levels.png)

- **Skupiny pro správu:** Tyto skupiny jsou kontejnery, které pomáhají při správě přístupu, zásad a dodržování předpisů pro několik předplatných. Všechna předplatná ve skupině pro správu automaticky dědí podmínky, které se na příslušnou skupinu pro správu vztahují.
- **Předplatná:** Předplatné seskupuje uživatelské účty a prostředky, které byly vytvořeny těmito uživatelskými účty. Každé předplatné má limity nebo kvóty pro množství prostředků, které můžete vytvořit a využívat. Organizace můžou pomocí předplatných spravovat náklady a prostředky vytvořené uživateli, týmy nebo v rámci projektů.
- **Skupiny prostředků:** Skupina prostředků je logický kontejner, ve kterém se nasazují a spravují prostředky Azure, jako například webové aplikace, databáze a účty úložiště.
- **Zdroje a prostředky:** Prostředky jsou instance vytvořených služeb, jako například virtuální počítače, úložiště nebo databáze SQL.

## <a name="scope-of-management-settings"></a>Rozsah nastavení správy

Nastavení správy, jako jsou zásady a řízení přístupu na základě role, můžete používat na jakékoli úrovni správy. Vybraná úroveň určuje rozsah použití nastavení. Nižší úrovně dědí nastavení z vyšších úrovní. Když například použijete zásadu pro předplatné, tato zásada se použije také pro všechny skupiny prostředků a prostředky v tomto předplatném.

Obvykle je vhodné používat důležitá nastavení na vyšších úrovních a nastavení související s požadavky konkrétního projektu na nižších úrovních. Například můžete chtít zajistit, aby se všechny prostředky vaší organizace nasazovaly do konkrétních oblastí. Provedete to tak, že pro předplatné použijete zásadu, která udává povolená umístění. Když ostatní uživatelé ve vaší organizaci přidají nové skupiny prostředků a prostředky, automaticky se vynutí použití některého z povolených umístění. Další informace o zásadách najdete v částech tohoto průvodce věnovaných zásadám správného řízení, zabezpečení a dodržování předpisů.

Pokud máte jen několik předplatných, je poměrně snadné je spravovat nezávisle. Se zvyšováním počtu používaných předplatných zvažte vytvoření hierarchie skupin pro správu, která zjednodušuje správu předplatných a prostředků. Další informace o správě více předplatných najdete v článku o [škálování s využitím několika předplatných Azure](../azure-best-practices/scaling-subscriptions.md).

Při plánování strategie dodržování předpisů spolupracujte s lidmi, kteří ve vaší organizaci mají na starost zabezpečení a dodržování předpisů, správu IT, podnikovou architekturu, sítě, finance a pořizování.

::: zone target="docs"

## <a name="create-a-management-level"></a>Vytvoření úrovně správy

Můžete vytvořit skupinu pro správu, další předplatná nebo skupiny prostředků.

### <a name="create-a-management-group"></a>Vytvoření skupiny pro správu

Vytvořte skupinu pro správu, která pomáhá spravovat přístup, zásady a dodržování předpisů pro několik předplatných.

1. Přejděte do části [Skupiny pro správu](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Vyberte **Přidat skupinu pro správu**.

### <a name="create-a-subscription"></a>Vytvoření odběru

Pomocí předplatných spravujte náklady a prostředky vytvořené uživateli, týmy nebo v rámci projektů.

1. Přejděte do části [Předplatná](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Vyberte **Přidat**.

### <a name="create-a-resource-group"></a>Vytvoření skupiny prostředků

Vytvořte skupinu prostředků sdružující prostředky, jako jsou webové aplikace, databáze a účty úložiště, které sdílejí stejný životní cyklus, oprávnění a zásady.

1. Přejděte do části [Skupiny prostředků](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Vyberte **Přidat**.
1. Vyberte **Předplatné**, ve kterém chcete skupinu prostředků vytvořit.
1. Zadejte název do pole **Skupina prostředků**.
1. Vyberte **Oblast** pro umístění skupiny prostředků.

## <a name="learn-more"></a>Další informace

Další informace naleznete v tématu:

- [Základy Azure](../considerations/fundamental-concepts.md)
- [Škálování s využitím několika předplatných Azure](../azure-best-practices/scaling-subscriptions.md)
- [Principy správy přístupu k prostředkům v Azure](../../govern/resource-consistency/resource-access-management.md)
- [Uspořádání prostředků s využitím skupin pro správu Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview)
- [Omezení služeb předplatného](https://docs.microsoft.com/azure/azure-subscription-service-limits)

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

Správný standard pro vytváření názvů pomáhá identifikovat prostředky na portálu Azure, na faktuře a ve skriptech. Ve strategii pro vytváření názvů byste jako součásti názvů měli používat firemní a provozní údaje:

- Firemní údaje by v této strategii měly zajistit, aby názvy prostředků obsahovaly informace organizace, které jsou potřeba k identifikaci týmů. Použijte prostředek společně s vlastníky, kteří zodpovídají za náklady na prostředky.

- Provozní údaje by měly zajistit, aby názvy obsahovaly informace, které potřebuje tým IT. Použijte údaje identifikující úlohy, aplikace, prostředí, důležitost a další informace, které jsou užitečné pro správu prostředků.

Různé typy prostředků mohou mít různé délkové limity a povolené znaky, z nichž mnohé jsou uvedené v [článku s osvědčenými postupy pro pojmenování v Azure](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). Další informace a doporučení zaměřená konkrétně na podporu přechodu do cloudu najdete v [pokynech k pojmenování a označování](../azure-best-practices/naming-and-tagging.md) v článku Architektura přechodu na cloud.

Následující tabulka obsahuje vzory vytváření názvů pro několik ukázkových typů prostředků Azure.

::: zone target="docs"

>[!TIP]
>Nepoužívejte žádné speciální znaky (`-` nebo `_`) jako první ani poslední znak názvu. Většina ověřovacích pravidel kvůli těmto znakům selže.

::: zone-end

| Entita | Rozsah | Délka | Velikost písmen | Platné znaky | Navrhovaný vzor | Příklad |
| --- | --- | --- | --- | --- | --- | --- |
|Skupina prostředků |Předplatné |1–90 |Malá a velká písmena se nerozlišují. |Alfanumerické znaky, podtržítka, kulaté závorky, pomlčky, tečky (s výjimkou teček na konci) a znaky Unicode |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Skupina dostupnosti |Skupina prostředků |1–80 |Malá a velká písmena se nerozlišují. |Alfanumerické znaky, podtržítka a pomlčky |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Značka |Související entita |512 (název), 256 (hodnota) |Malá a velká písmena se nerozlišují. |Alfanumerické znaky |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tagstabresourcetags"></a>[Značky prostředku](#tab/ResourceTags)

Značky jsou užitečné k rychlé identifikaci prostředků a skupin prostředků. Použijte značky na prostředky Azure pro jejich logické uspořádání podle kategorií. Každá značka se skládá z názvu a hodnoty. Můžete například použít název Prostředí a hodnotu Produkční na všechny prostředky v produkčním prostředí. Značky by měly obsahovat kontext týkající se úlohy nebo aplikace přiřazené k prostředku, provozních požadavků a informací o vlastnictví.

Po použití značek můžete načíst všechny prostředky v předplatném s daným názvem a hodnotou značky. Při uspořádání prostředků kvůli fakturaci nebo správě vám značky mohou pomoci najít související prostředky z různých skupin prostředků.

Značky můžete použít také k celé řadě dalších účelů. Mezi běžné způsoby použití patří:

- **Metadata a dokumentace:** Správci mohou snadno zobrazit podrobnosti o prostředcích, na kterých pracují, například pomocí značky „VlastníkProjektu“.
- **Automatizace:** Možná máte pravidelně spouštěné skripty, které provádějí akce na základě hodnoty značky, jako je „ČasVypnutí“ nebo „DatumZrušeníZřízení“.
- **Fakturace:** Značky se můžou zobrazit na vaší faktuře. S jejich pomocí můžete fakturu segmentovat například pomocí značek „NákladovéStředisko“ nebo „PříjemceFaktury“.

Každý prostředek nebo skupina prostředků může mít maximálně 50 dvojic název/hodnota značky. Toto omezení se vztahuje jen na značky použité přímo u prostředku nebo skupiny prostředků.

Další doporučení a příklady značek najdete v [pokynech k označování](../azure-best-practices/naming-and-tagging.md) v Architektuře přechodu na cloud.

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Použití značky prostředku

Použití značky na skupinu prostředků:

1. Přejděte do části [Skupiny prostředků](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Vyberte skupinu prostředků.
1. Vyberte **Přiřadit značky**.
1. Zadejte nový název a hodnotu nebo pomocí rozevíracího seznamu vyberte existující název a hodnotu.

## <a name="learn-more"></a>Další informace

Další informace najdete v tématu [Používání značek k uspořádání prostředků Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

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
