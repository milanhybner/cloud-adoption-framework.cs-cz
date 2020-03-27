---
title: Co je nového
description: Seznamte se s aktualizacemi rozhraní pro přijetí Microsoft Cloud pro Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: a3e316d49acaaee00d5ecd10efac9aa15c2dbd49
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353672"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework"></a>Co je nového v rozhraní pro přijetí Microsoft Cloud

## <a name="fulfilling-the-vision"></a>Naplnění této vize

Tato architektura přešla do fáze obecné dostupnosti (GA). Tuto ambiciózní architekturu ale dál aktivně vytváříme ve spolupráci se zákazníky, partnery a interními týmy. V rámci podpory partnerství se obsah vydává, jakmile je k dispozici. Tyto veřejné verze umožňují testování, ověřování a postupné vylepšování těchto pokynů.

V následující poznámkách k verzi jsou zaznamenány významné změny.

## <a name="migration-update-03022020"></a>Aktualizace migrace: 03/02/2020

Tato verze reaguje na zpětnou vazbu týkající se kontinuity přístupu k migraci prostřednictvím několika metod, včetně strategie, plánu, připravenosti a migrace. Cílem této verze bylo usnadnit čtenářům pochopení průběžných vylepšení plánování a přijetí, protože zákazníci pokračují v migraci. Byly provedeny následující změny pro splnění duchu této verze:

### <a name="new-articles"></a>Nové články

- [Vyvážení konkurenčních priorit](../strategy/balance-competing-priorities.md): popisuje rovnováhu mezi prioritami, ke kterým dochází v každé metodologii pro informování zákaznických strategií.
- [Klasifikace během vyhodnocování procesů](../migrate/migration-considerations/assess/classify.md): popisuje důležitost klasifikace každého assetu a zatížení před migrací.

### <a name="restructure-landing-zone-process"></a>Proces restrukturování cílové zóny

První zóna pro vykládku se vyžádala z Průvodce připravenosti, aby sloužila jako vlastní oddíl. Tento přístup nám umožňuje rozšířit koncepci konceptů a možností cílové zóny. To také vedlo k vytvoření několika nových článků:

- [Co je cílová zóna?](../ready/landing-zone/index.md)definuje termín cílové zóny.
- [První cílová zóna](../ready/landing-zone/first-landing-zone.md): rozbalí porovnání různých zón vykládku.
- [Migrace cílové zóny](../ready/landing-zone/migrate-landing-zone.md): přesunuli jsme předchozí článek podrobného podrobného povýšení zóny, aby se rozvedla definice CAF podrobného plánu od výběru první cílové zóny, která umožňuje další možnosti cílové zóny.
- Článek o [cílové zóně terraformu](../ready/landing-zone/terraform-landing-zone.md) : přesunuli jsme se z oddílu "rozšířeného rozsahu" připravené metodologie na novou "cílovou zónu" v části připravená metodologie, aby se terraformu první občan třídy v konverzaci k cílové zóně.
- Seskupí požadavky na cílové zóny v obsahu v části základní požadavky na cílovou zónu.
- Doporučené postupy zabezpečení z metodologie migrace do nové cílové zóny: Vylepšete zabezpečení cílové zóny (citlivá data) k vystavení čtenářům výše v životním cyklu.

### <a name="refinements-to-the-azure-migration-guide"></a>Vylepšení Průvodce migrací Azure

Vzory provozu uživatelů naznačují, že tato část obsahu je pravděpodobnější, že ji implementují implementátori a architekti během první migrace. Aby bylo možné lépe podporovat tuto cílovou skupinu, zaměřuje se na vylepšení Průvodce migrací, aby lépe odpovídal původnímu záměru vystavení čtenářů nástrojům použitým během první migrace.

- [Přehled](../migrate/azure-migration-guide/index.md): jasný popis průvodce s omezeným počtem kroků.
- [Vyhodnocení](../migrate/azure-migration-guide/assess.md): lepší představu o tom, že posouzení v této fázi se zaměřuje na posouzení technického přizpůsobení konkrétního zatížení a souvisejících prostředků. Přidání nenáročného oddílu předpoklady k předvedení toho, kdo tato úroveň posouzení funguje s postupem přírůstkového vyhodnocování, který je první uveden v metodologii plánování.
- [Migrace](../migrate/azure-migration-guide/migrate.md): v reakci na zpětnou vazbu na konferencích vrstvy 1 byl do možností nástroje třetích stran přidán odkaz na UnifyCloud.
- [Testování, optimalizace a propagace](../migrate/azure-migration-guide/optimize-and-transform.md): zarovnání názvu tohoto článku k ostatním návrhům na zlepšení procesu.

### <a name="refinements-to-migration-process-improvements"></a>Vylepšení procesů migrace

- [Přehled vyhodnocení](../migrate/migration-considerations/assess/index.md): lepší představu o tom, že posouzení v této fázi se zaměřuje na posouzení technického přizpůsobení konkrétního zatížení a souvisejících prostředků.
- [Kontrolní seznam pro plánování](../migrate/migration-considerations/prerequisites/planning-checklist.md): objasnění důležitosti operací zarovnání v průběhu plánování pro účely migrace zajistíte správnou správu úloh po migraci.

### <a name="placement-of-related-articles"></a>Umístění souvisejících článků

Všechny níže uvedené seznamy článků byly přesunuty. Provoz se přesměruje na nové místo.

- Článek o [osvědčených postupech pro posouzení](../plan/contoso-migration-assessment.md) : přesunuli jsme se z oddílu "osvědčené postupy" migrace metodologie do nového oddílu "osvědčených postupů" metodologie plánování. Tento přesun zpřístupňuje čtenářům postup vyhodnocení místních prostředí dříve v životním cyklu.
- Vyvážení článku o [portfoliu](../strategy/balance-the-portfolio.md) : přesunuli jsme se z oddílu "Rozšířený rozsah" metody migrace na metodologii strategie. Toto přesunutí zpřístupňuje čtenářům tento myšlenkový proces dříve v životním cyklu.

### <a name="alignment-of-the-changes"></a>Zarovnání změn

- [Připravený přehled](../ready/index.md): aktualizujte čtyři kroky v přehledu připraveno, aby odrážely proces objemnějšího.
- [Přehled migrace](../migrate/index.md): aktualizujte kroky v přehledu migrace tak, aby odrážely proces objemnějšího.
- [Migrace metodologie obrázek](../migrate/index.md): aktualizace obrazu metodologie, aby odrážel změny
- [Přehled grafiky](../index.md): aktualizace grafického přehledu, aby odrážely změny
