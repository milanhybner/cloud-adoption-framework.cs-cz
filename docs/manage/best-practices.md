---
title: Úvod k provozní správě
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznámení s provozní správou v rámci architektury přechodu na cloud
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 46af630c299f1fb66565cf1d55e5acf9f36d8251
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683669"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Vytvoření postupů provozní správy v cloudu

Přechod na cloud je katalyzátorem zajištění obchodních hodnot. Ale skutečné obchodní hodnoty se realizují prostřednictvím trvalého a stabilního provozu technologických aktiv nasazených do cloudu. Tato část architektury přechodu na cloud provádí čtenáře různými možnostmi přechodu na provozní správu v cloudu.

## <a name="actionable-best-practices"></a>Osvědčené postupy s praktickým využitím

Moderní řešení pro správu operací vytvářejí více cloudových zobrazení operací. Prostředky spravované prostřednictvím následujících osvědčených postupů můžou být živé v cloudu, ve stávajícím datacentru nebo i v konkurenčním poskytovateli cloudu. Tato architektura v současnosti zahrnuje dva referenční osvědčené postupy pro zajištění vyspělé provozní správy v cloudu:

- [Správa Azure serveru](./azure-server-management/index.md): integrovaný průvodce pro začlenění cloudových nativních nástrojů a služeb potřebných ke správě operací.
- [Hybridní monitorování](./monitor/index.md): mnoho zákazníků již v System Center Operations Manager provedlo značnou investici. Těmto zákazníkům tento průvodce hybridním monitorováním pomáhá porovnat nástroje pro vytváření sestav nativní pro cloud s nástroji Operations Manageru. Toto porovnání usnadňuje rozhodování, které nástroje využít pro provozní správu.

## <a name="cloud-operations"></a>Cloudový provoz

Oba tyto osvědčené postupy se vytvářejí směrem k budoucímu stavu metodologie pro Operations Management.

![Správa metodologie architektury pro přijetí do cloudu](../_images/manage/caf-manage.png)

**Zarovnání firmy:** Při správě metodologie jsou všechny úlohy klasifikované podle závažnosti a obchodní hodnoty. Tato klasifikace se dá následně měřit prostřednictvím analýz dopadu, které vypočítávají ztráty hodnoty související se snížením výkonu nebo přerušením provozu. Na základě tohoto měřitelného dopadu na výnosy mohou týmy zajišťující cloudový provoz v rámci firmy vytvořit prostředí, které vyvažuje náklady a výkon.

**Provozní obory cloudu:** Po zarovnávání firmy je mnohem snazší sledovat a sestavovat správné obory cloudových operací pro každou úlohu. Rozhodování v rámci jednotlivých disciplín se pak dá snadno převést na termíny, které jsou srozumitelné z obchodního hlediska. Díky tomuto přístupu založenému na spolupráci se zainteresované strany stávají partnery při hledání správného poměru cena/výkon.

- **Inventář a viditelnost:** Minimální Správa operací vyžaduje, aby bylo zajištěno inventarizaci prostředků a vytváření viditelnosti stavu spuštění jednotlivých assetů.
- **Provozní dodržování předpisů:** Klíčem k udržení očekávání výkonu je pravidelná Správa konfigurace, velikosti, nákladů a výkonu assetů.
- **Ochrana a obnovení:** Minimalizace provozních přerušení a urychlení obnovení každé z nich, aby se předešlo ztrátám výkonu a vlivům na výnosy. Základními aspekty této disciplíny jsou detekce a obnovení.
- **Operace platformy:** Všechna IT prostředí obsahují sadu běžně používaných platforem. Tyto platformy mohou zahrnovat úložiště dat, jako jsou SQL Server nebo HDInsight. Mezi další běžné platformy patří kontejnerová řešení, jako jsou Kubernetes nebo AKS. Zajištění vyspělosti provozu platforem se soustředí na přizpůsobení provozu na základě toho, jak jsou tyto běžné platformy nasazené, nakonfigurované a využívané jednotlivými úlohami.
- **Operace úlohy:** V nejvyšší provozní zralosti můžou cloudové provozní týmy ladit operace s úlohami, které jsou zásadní pro úspěch firmy. Pro tyto klíčové úlohy mohou dostupná data pomáhat při automatizaci nápravných akcí, nastavování velikosti nebo ochrany na základě jejich využití.

Další pokyny, jako je například [architektura pro kontrolu návrhu (kódový název: Principy návrhu cloudu)](https://docs.microsoft.com/azure/architecture/reliability) , mohou pomoci při provádění podrobných rozhodnutí o architektuře týkající se jednotlivých úloh v rámci pravidel uvedených výše.

Tato část architektury přechodu na cloud bude tato témata dále rozvíjet s cílem zajistit vyspělý cloudový provoz v rámci vaší organizace.
