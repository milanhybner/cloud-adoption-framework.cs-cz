---
title: Požadavky na migraci
description: Seznamte se s požadavky, které vám pomohou připravit se na migraci do cloudu a vyhnout se běžným důvodům pro její selhání.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb7d0c8b0ee6ebd328ffd4807199e0b0e2620d35
ms.sourcegitcommit: 238e7a06b56950cebdcc8f75924849fc995e6ff2
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173323"
---
# <a name="prerequisites-for-migration"></a>Požadavky na migraci

Před zahájením jakékoli migrace musí vaše _prostředí_ cíle migrace být připravené na přicházející změny. V tomto případě prostředí označuje technické základy v cloudu. Prostředí také znamená obchodní prostředí a způsob myšlení podporující migraci. Podobně prostředí zahrnuje kulturu týmů, které provádějí změny, a těch, kteří obdrží výsledky. Nedostatečná příprava na tyto změny je nejčastějším důvodem selhání migrace. Tato série článků vás provede navrhovanými požadavky na přípravu prostředí.

## <a name="objective"></a>Cíl

Zajištění obchodní, kulturní a technické připravenosti před zahájením iterativního plánu migrace

## <a name="review-business-drivers"></a>Kontrola obchodních faktorů

Před zahájením jakékoli migrace do cloudu si přečtěte pokyny k [plánování](../../../strategy/index.md) a zajištění [připravenosti](../../../ready/index.md) v architektuře přechodu na cloud a ujistěte se, že je vaše organizace připravená na procesy přechodu na cloud a migrace. Konkrétně si projděte obchodní požadavky a očekávané výsledky, které jsou důvodem k migraci:

- [Začínáme: Migrace](../../../getting-started/migrate.md)
- [Proč přecházíme na cloud?](../../../strategy/motivations.md)

## <a name="definition-of-done"></a>Definice *dokončení*

Požadavky jsou dokončené po splnění následujících podmínek:

- **Obchodní připravenost:** Tým cloudové strategie definoval a určil prioritu backlogu migrace nejvyšší úrovně, který představuje část digitálních aktiv, která se má migrovat v dalších dvou nebo třech verzích. Tým cloudové strategie se shodl s týmem přechodu na cloud na počáteční strategii pro zvládnutí této změny.
- **Kulturní připravenost:** Tým přechodu na cloud, tým cloudové strategie a ovlivnění uživatelé se shodli na svých rolích, povinnostech a očekáváních týkajících se úloh, které se mají migrovat v dalších dvou nebo třech verzích.
- **Technická připravenost:** Cílová zóna (neboli přidělený prostor pro hostování v cloudu) pro migrované prostředky splňuje minimální požadavky na hostování první migrované úlohy.

> [!CAUTION]
> Příprava je klíčem k úspěšné migraci. Přehnaná příprava však může vést k *analytické paralýze*, kdy příliš mnoho času věnovaného plánování může výrazně zpozdit migraci. Procesy a požadavky definované v této části vám mají pomoct s rozhodováním, ale nenechte se jimi omezovat ve smysluplném pokroku.
>
> Pro počáteční migraci zvolte poměrně jednoduchou úlohu. Při plánování a implementaci této první migrace využijte procesy popsané v této části. První příklad migrace členům vašeho týmu rychle předvede principy cloudu a přiměje je seznámit se s fungováním cloudu. S tím, jak bude váš tým získávat zkušenosti, můžete tyto poznatky využít při rozsáhlejších a složitějších migracích.

## <a name="accountability-during-prerequisites"></a>Odpovědnost během přípravy

Za připravenost během fáze přípravy nesou odpovědnost dva týmy:

- **Tým cloudové strategie:** Tento tým odpovídá za identifikaci a určení priority prvních dvou nebo tří úloh, které budou sloužit jako kandidáti na migraci.
- **Tým přechodu na cloud:** Tento tým odpovídá za ověření připravenosti technického prostředí a proveditelnosti migrace navržených úloh.

Za splnění každé ze tří definic dokončení uvedených v předchozí části by v obou týmech měl nést odpovědnost jeden člen.

## <a name="responsibilities-during-prerequisites"></a>Povinnosti během přípravy

Kromě odpovědnosti na nejvyšší úrovni existují akce, za které musí nést přímou odpovědnost určitý jednotlivec nebo skupina. Následuje několik takových povinností, které tyto aktivity ovlivňují:

- **Stanovení obchodních priorit:** Přijetí obchodních rozhodnutí týkajících se úloh, které se mají migrovat, a obecných časových omezení. Další informace najdete v tématu [Motivace firem k migraci do cloudu](../../../strategy/motivations.md).
- **Připravenost na správu změn:** Stanovení a komunikace plánu sledování technických změn během migrace.
- **Sladění s podnikovými uživateli:** Stanovení plánu přípravy komunity podnikových uživatelů na provedení migrace.
- **Inventura a analýza digitálních aktiv:** Spuštění nástrojů potřebných k inventuře a analýze digitálních aktiv. Další informace najdete v popisu [digitálních aktiv](../../../digital-estate/index.md) v architektuře přechodu na cloud.
- **Připravenost na cloud:** Posouzení cílového prostředí pro nasazení, aby se zajistilo, že splňuje požadavky prvních několika kandidátských úloh. Další informace najdete v [průvodci nastavením Azure](../../../ready/azure-setup-guide/index.md).

S těmito povinnostmi vám pomůžou zbývající články v této sérii.

## <a name="next-steps"></a>Další kroky

Když máte obecný přehled o požadavcích, jste připraveni přijmout první požadovaná [raná rozhodnutí ohledně migrace](./decisions.md).

> [!div class="nextstepaction"]
> [Raná rozhodnutí ohledně migrace](./decisions.md)
