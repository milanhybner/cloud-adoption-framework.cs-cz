---
title: Vylepšení oboru Cost Management
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vylepšení oboru Cost Management
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1b59121bc0679475079dc1a7b5d3770cc87d7523
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753083"
---
# <a name="cost-management-discipline-improvement"></a>Vylepšení oboru Cost Management

Cost Management disciplína se snaží řešit základní obchodní rizika související s výdaji při hostování cloudových úloh. V pěti oborech zásad správného řízení cloudu se Cost Management v rámci řízení nákladů a využití cloudových prostředků s cílem vytvořit a udržovat plánovaný nákladový cyklus.

Tento článek popisuje možné úkoly, které vaše společnost provádí při vývoji a rozvinutí Cost Managementch oborů. Tyto úlohy je možné rozdělit na plánování, sestavování, přijímání a provozní fáze implementace cloudového řešení, které se pak iterovat na to, že umožní vývoj [přírůstkového přístupu ke správě cloudu](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Čtyři fáze přijetí](../../_images/govern/adoption-phases.png)

*Obrázek 1 – fáze přijetí přírůstkového přístupu ke zásadám správného řízení cloudu.*

Žádný dokument nemůže mít žádný z těchto požadavků na požadavky všech společností. Tento článek popisuje navrhované minimální a potenciální příklady aktivit pro každou fázi procesu maturation zásad správného řízení. Počáteční cíl těchto aktivit vám pomůže vytvořit [MVP pro zásady](../guides/index.md#an-incremental-approach-to-cloud-governance) a vytvořit rozhraní pro přírůstkové zlepšování zásad. Váš tým zásad správného řízení vašeho cloudu bude muset rozhodnout, kolik investic do těchto aktivit investovat, aby se zlepšily možnosti zásad správného řízení Cost Management.

> [!CAUTION]
> Minimální ani potenciální aktivity, které jsou uvedené v tomto článku, jsou zarovnané na konkrétní podnikové zásady nebo požadavky na dodržování předpisů třetích stran. Tento návod je navržený tak, aby usnadnil konverzace, které vedou k vyrovnání obou požadavků s modelem zásad správného řízení pro Cloud.

## <a name="planning-and-readiness"></a>Plánování a připravenost

Tato fáze předběžných postupů řízení vypořádání mostů mezi obchodními výsledky a strategiemi, které se s nimi možné. Během tohoto procesu vedoucí týmu definuje konkrétní metriky, mapuje tyto metriky na digitální nemovitosti a zahájí plánování celkové snahy o migraci.

**Minimální navrhované aktivity:**

- Vyhodnoťte možnosti [cost management sada nástrojů](./toolchain.md) .
- Vývoj konceptu pokynů k architektuře a distribuce pro klíčové účastníky
- Informujte a zapojte lidi a týmy, kterých se týkalo vývoje pokynů pro architekturu.

**Potenciální aktivity:**

- Zajistěte, aby rozpočtová rozhodnutí podporovala obchodní odůvodnění pro vaši cloudovou strategii.
- Ověřte metriky učení, které použijete k hlášení úspěšného přidělení finančních prostředků.
- Seznamte se s požadovaným modelem cloudového účetnictví, který má vliv na to, jak by měly být poplatky za Cloud
- Seznamte se s plánem digitální nemovitosti a ověřte přesné očekávané náklady.
- Vyhodnoťte možnosti nákupu, abyste zjistili, jestli je lepší "průběžné platby", nebo abyste mohli předplatit zakoupením smlouva Enterprise.
- Zarovnejte obchodní cíle s plánovanými rozpočty a podle potřeby upravte rozpočtové plány.
- Vývoj cílů a mechanizmu generování sestav rozpočtu pro informování technických a obchodních účastníků na konci každého nákladového cyklu.

## <a name="build-and-predeployment"></a>Sestavení a přednasazení

K úspěšné migraci prostředí je nutné provést několik technických a netechnických požadavků. Tento proces se zaměřuje na rozhodování, připravenost a základní infrastrukturu, která pokračuje v migraci.

**Minimální navrhované aktivity:**

- Implementujte své [cost management sada nástrojů](./toolchain.md) , a to tak, že zavedete do fáze předinstalace.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů
- Určete, jestli vaše požadavky na nákup odpovídají vašim rozpočtům a cílům.

**Potenciální aktivity:**

- Narovnejte své rozpočtové plány pomocí [strategie předplatného](../../decision-guides/subscriptions/index.md) , která definuje váš model základního vlastnictví.
- Využijte [strategii konzistence prostředků](../../decision-guides/resource-consistency/index.md) k prosazování pravidel architektury a nákladů v průběhu času.
- Zjistěte, jestli jakékoli anomálie s náklady ovlivňují vaše plány přijetí a migrace.

## <a name="adopt-and-migrate"></a>Přijmout a migrovat

Migrace je přírůstkový proces, který se zaměřuje na přesun, testování a přijetí aplikací nebo úloh v existující digitální nemovitosti.

**Minimální navrhované aktivity:**

- Migrujte [cost management sada nástrojů](./toolchain.md) před nasazením do produkčního prostředí.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů

**Potenciální aktivity:**

- Implementujte model monitorování účtů cloudu.
- Ujistěte se, že vaše rozpočty odráží skutečnou útratu během každé vydané verze, a podle potřeby je upravte.
- Sledujte změny v rozpočtových plánech a ověřte je u zúčastněných stran, pokud potřebujete další odhlašování.
- Aktualizujte změny v dokumentu s pokyny k architektuře, aby odrážely skutečné náklady.

## <a name="operate-and-post-implementation"></a>Provoz a následné implementace

Po dokončení transformace musí být zásady správného řízení a provoz v provozu v rámci přirozeného životního cyklu aplikace nebo zátěže. Tato fáze řízení splatnosti se zaměřuje na aktivity, které se běžně přidávají po implementaci řešení, a cyklus transformace začíná stabilizovat.

**Minimální navrhované aktivity:**

- Přizpůsobte [cost management sada nástrojů](./toolchain.md) na základě změn v potřebách správy nákladů vaší organizace.
- Zvažte automatizaci všech oznámení a sestav, které odrážejí skutečnou útratu.
- Upřesněte pokyny k architekturám a provedou budoucí procesy přijímání.
- Pravidelně informujte s ovlivněnými týmy, aby se zajistilo průběžné dodržování pravidel architektury.

**Potenciální aktivity:**

- Spusťte čtvrtletní cloudovou recenzi za účelem sdělování hodnoty poskytované obchodním a souvisejícím nákladům.
- Upravte plány čtvrtletním tak, aby odrážely změny skutečné útraty.
- Určete finanční zarovnání pro předplatné P & LS pro Business Unit.
- Analyzujte hodnoty účastníků a metody vykazování nákladů měsíčně.
- Opravte nepoužívané prostředky a určete, jestli se budou dál zařazovat.
- Odhalte chybné zarovnání a anomálie mezi plánem a skutečnou útratou.
- Pomáhat týmům při přijímání cloudu a týmu cloudové strategie s porozuměním a řešením těchto anomálií.

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte konceptu zásad správného řízení identity v cloudu, Projděte [cost management sada nástrojů](./toolchain.md) a Identifikujte nástroje a funkce Azure, které budete potřebovat při vývoji cost management pravidla řízení na platformě Azure.

> [!div class="nextstepaction"]
> [Cost Management sada nástrojů pro Azure](./toolchain.md)
