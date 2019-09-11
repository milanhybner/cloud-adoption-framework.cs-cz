---
title: Úvod k provozní správě
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznámení s provozní správou v rámci architektury přechodu na cloud
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: manage
ms.openlocfilehash: ed8afc403f217475cb69d4f0bf6742fe64443ae3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818433"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Vytvoření postupů provozní správy v cloudu

Přechod na cloud je katalyzátorem zajištění obchodních hodnot. Ale skutečné obchodní hodnoty se realizují prostřednictvím trvalého a stabilního provozu technologických aktiv nasazených do cloudu. Tato část architektury přechodu na cloud provádí čtenáře různými možnostmi přechodu na provozní správu v cloudu.

## <a name="actionable-best-practices"></a>Osvědčené postupy s praktickým využitím

Moderní řešení provozní správy vytvářejí multicloudové zobrazení provozu. Aktiva spravovaná prostřednictvím následujících osvědčených postupů se mohou nacházet v cloudu, v už existujícím datacentru nebo dokonce u konkurenčního poskytovatele cloudu. Tato architektura v současnosti zahrnuje dva referenční osvědčené postupy pro zajištění vyspělé provozní správy v cloudu:

* [Správa serverů v Azure:](./azure-server-management/index.md) Průvodce onboardingem pro začlenění služeb a nástrojů nativních pro cloud, které jsou pro provozní správu potřeba.
* [Hybridní monitorování:](./monitor/index.md) Celá řada zákazníků už značně investovala do System Center Operations Manageru. Těmto zákazníkům tento průvodce hybridním monitorováním pomáhá porovnat nástroje pro vytváření sestav nativní pro cloud s nástroji Operations Manageru. Toto porovnání usnadňuje rozhodování, které nástroje využít pro provozní správu.

## <a name="cloud-operations"></a>Cloudový provoz

Oba tyto osvědčené postupy se zaměřují na budoucí metodologie pro provozní správu.

![Metodologie Manage architektury přechodu na cloud (CAF)](../_images/operate/caf-manage.png)

**Obchodní rovnováha:** V rámci metodologie Manage se všechny úlohy klasifikují z hlediska závažnosti a obchodní hodnoty. Tato klasifikace se dá následně měřit prostřednictvím analýz dopadu, které vypočítávají ztráty hodnoty související se snížením výkonu nebo přerušením provozu. Na základě tohoto měřitelného dopadu na výnosy mohou týmy zajišťující cloudový provoz v rámci firmy vytvořit prostředí, které vyvažuje náklady a výkon.

**Disciplíny cloudového provozu:** Jakmile je zajištěná obchodní rovnováha, je mnohem jednodušší sledovat odpovídající disciplíny cloudového provozu pro každou úlohu a vytvářet na jejich základě sestavy. Rozhodování v rámci jednotlivých disciplín se pak dá snadno převést na termíny, které jsou srozumitelné z obchodního hlediska. Díky tomuto přístupu založenému na spolupráci se zainteresované strany stávají partnery při hledání správného poměru cena/výkon.

* Inventarizace a zajištění přehledu: Provozní správa vyžaduje přinejmenším možnost inventarizace aktiv a zajištění přehledu o stavu jejich spuštění.
* Provozní dodržování předpisů: Klíčem k zajištění provozních očekávání je pravidelná správa konfigurace, rozsahu, nákladů a výkonu jednotlivých aktiv.
* Ochrana a zotavení: Minimalizace provozních přerušení a zrychlené obnovení pomáhá zmírnit snížení výkonu a jeho dopad na náklady. Základními aspekty této disciplíny jsou detekce a obnovení.
* Provoz platforem: Všechna prostředí IT obsahují sadu běžně využívaných platforem. Tyto platformy mohou zahrnovat úložiště dat, jako jsou SQL Server nebo HDInsight. Mezi další běžné platformy patří kontejnerová řešení, jako jsou Kubernetes nebo AKS. Zajištění vyspělosti provozu platforem se soustředí na přizpůsobení provozu na základě toho, jak jsou tyto běžné platformy nasazené, nakonfigurované a využívané jednotlivými úlohami.
* Provoz úloh: Na nejvyšší úrovni provozní vyspělosti mohou týmy zajišťující cloudový provoz ladit provoz pro úlohy, které jsou pro úspěch firmy zásadní. Pro tyto klíčové úlohy mohou dostupná data pomáhat při automatizaci nápravných akcí, nastavování velikosti nebo ochrany na základě jejich využití.

Při dalším podrobnějším architektonickém rozhodování ohledně jednotlivých úloh vám v rámci výše uvedených disciplín mohou pomoci další průvodci, například [Architektura pro kontrolu návrhu (kódový název: Principy návrhu v cloudu)](/azure/architecture/reliability).

Tato část architektury přechodu na cloud bude tato témata dále rozvíjet s cílem zajistit vyspělý cloudový provoz v rámci vaší organizace.
