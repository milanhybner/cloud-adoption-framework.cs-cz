---
title: Racionalizace cloudu
description: Projděte si možnosti, které jsou k dispozici pro rationalizingi digitální nemovitosti.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/16/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 1a74487a77388e6260c177096d9563dbe6646cf2
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806556"
---
# <a name="cloud-rationalization"></a>Racionalizace cloudu

Racionalizace cloudu je proces vyhodnocení prostředků k určení nejlepšího způsobu, jak migrovat nebo modernizovat jednotlivé assety v cloudu. Další informace o procesu racionalizace najdete v tématu [co je to Digital nemovitosti?](./index.md).

## <a name="rationalization-context"></a>Kontext racionalizace

"Pět RS of racionalizace" uvedená v tomto článku jsou skvělým způsobem, jak popsat potenciální budoucí stav pro všechny úlohy, které se považují za cloudový kandidát. Tento proces označování by však měl být před pokusem o racionalizovat prostředí přepnut do správného kontextu. Zkontrolujte následující mýty a poskytněte tak tento kontext:

- **Mýtus: je snadné učinit rozhodnutí o racionalizaci v předstihu v průběhu procesu.** Přesná racionalizace vyžaduje důkladnou znalost úlohy a přidružených prostředků (aplikace, virtuální počítače a data). Co je nejdůležitější, přesné rozhodnutí o racionalizaci trvá v čase. Doporučujeme použít [přírůstkový proces racionalizace](./rationalize.md#incremental-rationalization).

- **Mýtus: přijetí do cloudu musí čekat na racionalizaci všech úloh.** Rationalizing celé IT Portfolio nebo dokonce jedno datové centrum může zpozdit realizaci obchodních hodnot podle měsíců nebo i roků. Pokud je to možné, měli byste se vyhnout plné racionalizaci. Místo toho využijte [sílu 10 přístupů k vydání plánování](./rationalize.md#release-planning) , abyste se mohli rozhodnout o dalších 10 úlohách, které se plánované pro přijetí do cloudu.

- **Mýtus: obchodní odůvodnění musí počkat na racionalizaci všech úloh.** Chcete-li vyvinout obchodní odůvodnění úsilí při přijetí do cloudu, udělejte na úrovni portfolia několik základních předpokladů. Pokud jsou motivace zarovnané na inovace, předpokládají se rearchitektura. V případě, že motivace je zarovnána k migraci, je nutné předpokládat opětovné hostování. Tyto předpoklady můžou urychlit proces obchodního odůvodnění. Předpoklady a jejich rozpočty jsou provedené během fáze hodnocení u cyklů přijetí jednotlivých úloh.

Teď si Projděte následující pět RS k racionalizaci, abyste se seznámili s dlouhodobým procesem. Při vývoji plánu přijetí do cloudu vyberte možnost, která nejlépe odpovídá vašim motivům, obchodním výsledkům a aktuálnímu stavu. Cílem v racionalizaci v digitální nemovitosti je nastavit směrný plán, aby se racionalizovat všechny úlohy.

## <a name="the-five-rs-of-rationalization"></a>Pět RS racionalizace

Pět RS of racionalizace, které jsou zde uvedeny, popisují nejběžnější možnosti pro racionalizaci.

## <a name="rehost"></a>Změna hostitele

I když se označuje jako migrace _výtahu a posunutí_ , přenáší úsilí o opětovné hostování aktuální stavový prostředek vybranému poskytovateli cloudu s minimální změnou na celkovou architekturu.

Mezi běžné ovladače můžou patřit:

- Snížení nákladů na kapitál
- Uvolnění prostoru Datacenter
- Dosažení rychlé návratnosti investic do cloudu

Kvantitativní analytické faktory:

- Velikost virtuálního počítače (CPU, paměť, úložiště)
- Závislosti (síťový provoz)
- Kompatibilita prostředků

Kvalitativní faktory analýzy:

- Tolerance pro změnu
- Obchodní priority
- Kritické obchodní události
- Závislosti procesů

## <a name="refactor"></a>Refaktoring

Možnosti platformy jako služby (PaaS) můžou snižovat provozní náklady spojené s mnoha aplikacemi. Je vhodné trochu Refaktorovat aplikaci, aby odpovídala modelu založenému na PaaS.

Refaktoring také odkazuje na proces vývoje aplikací kódu refaktoringu, který umožňuje aplikaci doručovat nové obchodní příležitosti.

Mezi běžné ovladače můžou patřit:

- Rychlejší a kratší aktualizace
- Přenositelnost kódu
- Vyšší efektivita cloudu (prostředky, rychlost, náklady, spravované operace)

Kvantitativní analytické faktory:

- Velikost assetu aplikace (CPU, paměť, úložiště)
- Závislosti (síťový provoz)
- Přenos uživatelů (zobrazení stránky, čas na stránce, doba načítání)
- Vývojová platforma (jazyky, datové platformy, služby střední vrstvy)
- Databáze (procesor, paměť, úložiště, verze)

Kvalitativní faktory analýzy:

- Pokračující obchodní investice
- Možnosti a časové osy shlukování
- Závislosti obchodních procesů

## <a name="rearchitect"></a>Změna architektury

Některé aplikace pro prodlení nejsou kompatibilní se zprostředkovateli cloudu z důvodu rozhodování o architektuře, které byly provedeny při vytvoření aplikace. V těchto případech může být před transformací aplikace nutné znovu provést její navržení.

V ostatních případech aplikace, které jsou kompatibilní s cloudem, ale ne pro cloudové nativní, můžou vytvořit cenovou efektivitu a provozní efektivitu tím, že se řešení rearchitektí do nativní cloudové aplikace.

Mezi běžné ovladače můžou patřit:

- Škálování a flexibilita aplikace
- Snadnější přijímání nových možností cloudu
- Kombinace technologických zásobníků

Kvantitativní analytické faktory:

- Velikost assetu aplikace (CPU, paměť, úložiště)
- Závislosti (síťový provoz)
- Přenos uživatelů (zobrazení stránky, čas na stránce, doba načítání)
- Vývojová platforma (jazyky, datové platformy, služby střední úrovně)
- Databáze (procesor, paměť, úložiště, verze)

Kvalitativní faktory analýzy:

- Rostoucí investice do podniku
- Provozní náklady
- Potenciální smyčky zpětné vazby a DevOps investice.

## <a name="rebuild"></a>Opětovné sestavení

V některých scénářích je rozdíl mezi tím, že je nutné provést převzetí aplikace, může být příliš velký, aby se do ní dalo zabývat další investice. To platí zejména pro aplikace, které dříve splnily potřeby firmy, ale nyní jsou nepodporované nebo špatně zarovnané s aktuálními obchodními procesy. V tomto případě je vytvořen nový základ kódu pro zarovnávání s přístupem [nativním pro Cloud](https://azure.microsoft.com/overview/cloudnative) .

Mezi běžné ovladače můžou patřit:

- Zrychlení inovací
- Rychlejší sestavování aplikací
- Snížení provozních nákladů

Kvantitativní analytické faktory:

- Velikost assetu aplikace (CPU, paměť, úložiště)
- Závislosti (síťový provoz)
- Přenos uživatelů (zobrazení stránky, čas na stránce, doba načítání)
- Vývojová platforma (jazyky, datové platformy, služby střední úrovně)
- Databáze (procesor, paměť, úložiště, verze)

Kvalitativní faktory analýzy:

- Odmítnutí spokojenosti koncových uživatelů
- Obchodní procesy omezené funkcí
- Potenciální zisky s náklady, zkušenostmi nebo výnosy

## <a name="replace"></a>Nahradit

Řešení jsou obvykle implementovaná pomocí nejlepší technologie a přístupu, který je k dispozici v čase. Někdy aplikace SaaS (software jako služba) můžou poskytovat všechny nezbytné funkce pro hostovanou aplikaci. V těchto scénářích je možné naplánovat budoucí nahrazení úloh. Tato úloha je efektivně odebrána z úsilí transformace.

Mezi běžné ovladače můžou patřit:

- Standardizace v oboru osvědčených postupů
- Urychlení přijetí přístupů řízených podnikovým procesem
- Přerozdělení investic do vývoje do aplikací, které vytvářejí konkurenční oddělení nebo výhody

Kvantitativní analytické faktory:

- Celkové snížení provozních nákladů
- Velikost virtuálního počítače (CPU, paměť, úložiště)
- Závislosti (síťový provoz)
- Prostředky k vyřazení
- Databáze (procesor, paměť, úložiště, verze)

Kvalitativní faktory analýzy:

- Analýza cenových výhod aktuální architektury oproti SaaS řešení
- Mapy obchodních procesů
- Schémata dat
- Vlastní nebo automatizované procesy

## <a name="next-steps"></a>Další kroky

Souhrnně můžete použít tyto pět RS k racionalizaci v digitální nemovitosti, které vám pomůžou při rozhodování o budoucím stavu jednotlivých aplikací.

> [!div class="nextstepaction"]
> [Co je to digitální majetek?](./index.md)
