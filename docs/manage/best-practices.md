---
title: Úvod do provozní správy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pochopení provozní správy v rámci architektury pro přijetí do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 8e58aea5c0d3b77cd194f8bd8919f43143ab18a4
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979943"
---
# <a name="establish-operational-management-practices-in-the-cloud"></a>Navázat postupy provozní správy v cloudu

Přechod na cloud je katalyzátorem zajištění obchodních hodnot. Ale skutečné obchodní hodnoty se realizují prostřednictvím trvalého a stabilního provozu technologických aktiv nasazených do cloudu. Tato část rozhraní pro přijetí do cloudu vás provede různými přechody na provozní správu v cloudu.

## <a name="actionable-best-practices"></a>Osvědčené postupy s praktickým využitím

Moderní řešení pro správu operací vytvářejí více cloudových zobrazení operací. Prostředky spravované prostřednictvím následujících osvědčených postupů můžou být živé v cloudu, ve stávajícím datacentru nebo i v konkurenčním poskytovateli cloudu. V současné době rozhraní zahrnuje dva osvědčené postupy, které se týkají řízení operací v cloudu:

- [Správa Azure serveru](./azure-server-management/index.md): Příručka pro připojování k integrovaným nástrojům a službám cloudu, které jsou potřeba pro správu operací.
- [Hybridní monitorování](./monitor/index.md): mnoho zákazníků již v System Center Operations Manager provedlo značnou investici. Pro tyto zákazníky může tato příručka k hybridnímu monitorování pomáhat při porovnávání a kontrastu nativních nástrojů pro vytváření sestav v cloudu pomocí nástrojů Operations Manager. Toto porovnání usnadňuje rozhodování, které nástroje se mají použít pro provozní správu.

## <a name="cloud-operations"></a>Cloudový provoz

Oba tyto osvědčené postupy se sestavují s metodologií pro řízení provozu v rámci budoucna, jak je znázorněno v následujícím diagramu:

![Správa metodologie architektury pro přijetí do cloudu](../_images/manage/caf-manage.png)

**Obchodní zarovnání**: v metodologii Správa jsou všechny úlohy klasifikované podle závažnosti a obchodní hodnoty. Tato klasifikace se dá následně měřit prostřednictvím analýz dopadu, které vypočítávají ztráty hodnoty související se snížením výkonu nebo přerušením provozu. Na základě tohoto měřitelného dopadu na výnosy mohou týmy zajišťující cloudový provoz v rámci firmy vytvořit prostředí, které vyvažuje náklady a výkon.

**Obory cloudových operací**: po zarovnání firmy je mnohem snazší sledovat a sestavovat správné obory cloudových operací pro každou úlohu. Rozhodnutí v každé disciplíně je pak možné převést na závazky, které může snadno pochopit společnost. Díky tomuto přístupu založenému na spolupráci se zainteresované strany stávají partnery při hledání správného poměru cena/výkon.

- **Inventář a viditelnost**: minimální Správa operací vyžaduje, abyste nahlásili prostředky do inventarizace a vytvářeli přehled o stavu spuštění jednotlivých assetů.
- **Provozní dodržování předpisů**: běžná Správa konfigurace, velikosti, nákladů a výkonu assetů je klíčem k udržení očekávání výkonu.
- **Ochrana a obnovení**: minimalizace provozního přerušení a urychlení obnovení s tím, aby se zabránilo ztrátám výkonu a nepříznivým výnosům. Základními aspekty této disciplíny jsou detekce a obnovení.
- **Operace platforem**: všechna IT prostředí obsahují sadu běžně používaných platforem. Tyto platformy můžou zahrnovat úložiště dat, například SQL Server nebo Azure HDInsight. Mezi další běžné platformy patří například řešení kontejnerů, jako je Azure Kubernetes Service (AKS). Bez ohledu na platformu se v operacích s platformou zaměřuje na přizpůsobení operací na základě způsobu nasazení, konfigurace a používání běžných platforem v úlohách.
- **Provozní operace**: na nejvyšší úrovni provozní zralosti můžou týmy cloudových operací ladit operace s úlohami, které jsou zásadní pro úspěch firmy. Pro tyto úlohy s vysokou závažností může dostupná data pomoci při automatizaci nápravy, velikosti nebo ochrany úloh na základě jejich využití.

Další doprovodné materiály, jako je například [architektura pro kontrolu návrhu (název kódu: Principy návrhu cloudu)](https://docs.microsoft.com/azure/architecture/reliability), vám mohou pomoci při rozhodování o všech úlohách v rámci dříve popsaných oborů.

Tato část rozhraní pro přijetí do cloudu bude sestavená na každém z předchozích témat, která vám pomůžou povýšit vyspělé cloudové operace v rámci vaší organizace.
