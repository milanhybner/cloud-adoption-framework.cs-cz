---
title: Vyřazení zastaralých prostředků
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak řádně vyřadit vyřazené prostředky s minimálním počtem přerušení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a62ef520f948d8bea415e4a65749944b91bb16c8
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092765"
---
# <a name="decommission-retired-assets"></a>Vyřazení zastaralých prostředků

Jakmile je sada funkcí povýšená do produkčního prostředí, prostředky, ve kterých byla dřív hostovaná, už nejsou pro firemní provoz potřebné. V tomto okamžiku se starší prostředky považují za vyřazené. Vyřazené prostředky je pak možné vyřadit z provozu a snižovat provozní náklady. Vyřazení prostředku z provozu může být jednoduché – někdy stačí jen vypnout napájení a ekologicky ho zlikvidovat. Vyřazení prostředků z provozu může mít ale někdy nežádoucí důsledky. Následující průvodce vám poradí, jak správně vyřadit nepotřebné prostředky z provozu, aby firemní prostoje byly co nejkratší.

## <a name="cost-savings-realization"></a>Realizace úspor nákladů

Pokud jsou úspory nákladů primární motivace pro migraci, je vyřazení z provozu důležitým krokem. Dokud nebude prostředek vyřazený z provozu, bude nadále spotřebovávat výkon, podporu pro výpočetní prostředí a další zdroje, které zvyšují náklady. Jakmile jsou staré prostředky vyřazené z provozu, začnou se snižovat náklady organizace.

## <a name="continued-monitoring"></a>Průběžné monitorování

Po zvýšení úrovně migrované sady funkcí by se prostředky, které mají být vyřazeny, měly i nadále monitorovat, aby se ověřilo, že provoz produkčního prostředí není směrován do nesprávných prostředků.

## <a name="testing-windows-and-dependency-validation"></a>Testování systému Windows a ověřování závislostí

I přes kvalitní plánování můžou sady funkcí povýšené do produkčního prostředí stále obsahovat závislosti na prostředcích, které se považují za vyřazené. V takových případech může vypnutí vyřazeného prostředku způsobit neočekávané selhání systému. Proto je potřeba k vyřazení prostředků z provozu přistupovat se stejnou pečlivostí jako k údržbě systému. Aby bylo vyřazení prostředků z provozu jednodušší, měla by být vytvořena pravidla pro testování a výpadky provozu.

## <a name="holding-period-and-data-validation"></a>Kontrola dat a doba uchování prostředků

Často se stává, že během migrace se při procesu replikace ztratí data. Platí to především pro starší data, se kterými se pravidelně nepracuje. Jakmile vyřazený prostředek vypnete, je vhodné ho ještě chvíli ponechat jako dočasnou zálohu dat. Firmy by měly uchovat vyřazené prostředky alespoň po dobu 30 dní a zlikvidovat je až po testování dat.

## <a name="next-steps"></a>Další kroky

Po vyřazení nepotřebných prostředků z provozu je migrace dokončená. Tím vzniká dobrá příležitost pro zlepšení procesu migrace. [Retrospektiva](./retrospective.md) umožní týmu přechodu na cloud zkontrolovat uvolnění prostředků a na základě získaných informací postup vylepšit.

> [!div class="nextstepaction"]
> [Retrospektiva](./retrospective.md)
