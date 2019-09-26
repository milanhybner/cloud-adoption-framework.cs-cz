---
title: Úvod do provozní správy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznámení s provozní správou v rámci architektury přechodu na cloud
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: manage
ms.openlocfilehash: 96f87583f50783fa0c6a8c947aa8b34ae440fc95
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221436"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Vytvoření postupů provozní správy v cloudu

Přechod na cloud je katalyzátorem zajištění obchodních hodnot. Ale skutečné obchodní hodnoty se realizují prostřednictvím trvalého a stabilního provozu technologických aktiv nasazených do cloudu. Tato část architektury přechodu na cloud provádí čtenáře různými možnostmi přechodu na provozní správu v cloudu.

## <a name="actionable-best-practices"></a>Osvědčené postupy s praktickým využitím

Moderní řešení provozní správy poskytují multicloudové zobrazení provozu. Aktiva spravovaná prostřednictvím následujících doporučených postupů se mohou nacházet v cloudu, v už existujícím datacentru nebo dokonce u konkurenčního poskytovatele cloudu. Tato architektura v současnosti zahrnuje dva referenční doporučené postupy pro zajištění vyspělé provozní správy v cloudu:

- [Správa serverů v Azure:](./azure-server-management/index.md) Tento průvodce onboardingem slouží pro začlenění služeb a nástrojů nativních pro cloud, které jsou pro provozní správu potřeba.
- [Hybridní monitorování:](./monitor/index.md) Celá řada zákazníků už značně investovala do System Center Operations Manageru. Těmto zákazníkům tento průvodce hybridním monitorováním pomáhá porovnat nástroje pro vytváření sestav nativní pro cloud s nástroji Operations Manageru. Toto porovnání usnadňuje rozhodování, které nástroje využít pro provozní správu.

## <a name="cloud-operations"></a>Cloudový provoz

Oba tyto osvědčené postupy se zaměřují na budoucí metodologie pro provozní správu.

![Metodologie Manage architektury přechodu na cloud (CAF)](../_images/manage/caf-manage.png)

**Obchodní rovnováha:** V rámci metodologie Manage se všechny úlohy klasifikují z hlediska závažnosti a obchodní hodnoty. Tato klasifikace se dá následně měřit prostřednictvím analýz dopadu, které vypočítávají ztráty hodnoty související se snížením výkonu nebo přerušením provozu. Na základě tohoto měřitelného dopadu na výnosy mohou týmy zajišťující cloudový provoz v rámci firmy vytvořit prostředí, které vyvažuje náklady a výkon.

**Disciplíny cloudového provozu:** Jakmile je zajištěná obchodní rovnováha, je mnohem jednodušší sledovat odpovídající disciplíny cloudového provozu pro každou úlohu a vytvářet na jejich základě sestavy. Rozhodování v rámci jednotlivých disciplín pak může vést k závazkům, které jsou dobře srozumitelné z obchodního hlediska. Díky tomuto přístupu založenému na spolupráci se zainteresované strany stávají partnery při hledání správného poměru cena/výkon.

- **Inventarizace a zajištění přehledu:** Provozní správa vyžaduje přinejmenším možnost inventarizace aktiv a zajištění přehledu o stavu jejich spuštění.
- **Provozní dodržování předpisů:** Klíčem k zajištění provozních očekávání je pravidelná správa konfigurace, rozsahu, nákladů a výkonu jednotlivých aktiv.
- **Ochrana a zotavení:** Minimalizace provozních přerušení a zrychlené obnovení pomáhá zmírnit snížení výkonu a jeho dopad na náklady. Základními aspekty této disciplíny jsou detekce a obnovení.
- **Provoz platforem:** Všechna prostředí IT obsahují sadu běžně využívaných platforem. Tyto platformy mohou zahrnovat úložiště dat, jako jsou SQL Server nebo HDInsight. Mezi další běžné platformy patří kontejnerová řešení jako Kubernetes nebo AKS. Zajištění vyspělosti provozu platforem se soustředí na přizpůsobení provozu na základě toho, jak jsou tyto běžné platformy nasazené, nakonfigurované a využívané jednotlivými úlohami.
- **Provoz úloh:** Na nejvyšší úrovni provozní vyspělosti mohou týmy zajišťující cloudový provoz ladit provoz pro úlohy, které jsou pro obchodní úspěch zásadní. Pro tyto klíčové úlohy mohou dostupná data pomáhat při automatizaci nápravných akcí, nastavování velikosti nebo ochrany na základě jejich využití.

Při dalším podrobnějším architektonickém rozhodování ohledně jednotlivých úloh vám v rámci výše uvedených disciplín mohou pomoci další průvodci, například [Architektura pro kontrolu návrhu (kódový název: Principy návrhu v cloudu)](https://docs.microsoft.com/azure/architecture/reliability).

Tato část architektury přechodu na cloud bude tato témata dále rozvíjet s cílem zajistit vyspělý cloudový provoz v rámci vaší organizace.
