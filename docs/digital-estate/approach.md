---
title: Přístupy k plánování digitálních aktiv
description: Přečtěte si o různých metodách pro plánování digitálních nemovitostí.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 453ac12e8c86aed46675c710395101ff3a121195
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806539"
---
# <a name="approaches-to-digital-estate-planning"></a>Přístupy k plánování digitálních aktiv

Plánování digitálních nemovitostí může v závislosti na požadovaných výsledcích a velikosti stávající nemovitosti trvat několik forem. Existují různé přístupy, které můžete provést. Je důležité, abyste nastavili očekávání týkající se přístupu v počátečních cyklech plánování. Nejasné očekávání často vedou k prodlevám souvisejícím s dalšími cvičeními shromažďování inventáře. Tento článek popisuje tři přístupy k analýze.

## <a name="workload-driven-approach"></a>Přístup řízený úlohou

Přístup k vyhodnocování shora dolů vyhodnocuje aspekty zabezpečení. Zabezpečení zahrnuje kategorizaci dat (vysoký, střední nebo nízký dopad na firmu), požadavky na dodržování předpisů, svrchovanost a bezpečnostní riziko. Tento přístup vyhodnocuje složitost architektury na vysoké úrovni. Vyhodnocuje aspekty, jako je ověřování, datová struktura, požadavky na latenci, závislosti a očekávané životního cyklu aplikace.

Přístup shora dolů také měří provozní požadavky aplikace, jako jsou úrovně služeb, integrace, časová období údržby, monitorování a přehled. Až se všechny tyto aspekty analyzují a berou v úvahu, výsledný výsledek odráží relativní obtížnost migrace této aplikace na každou cloudovou platformu: IaaS, PaaS a SaaS.

Kromě toho posouzení shora dolů vyhodnocuje finanční přínosy aplikace, jako je provozní efektivita, celkové náklady na vlastnictví, návratnost investic a další vhodné finanční metriky. Posouzení také prověřuje sezónnost aplikace (například v případě špičky poptávky v roce) a celkové zátěžové zátěže.

Také se podíváme na typy uživatelů, které podporuje (příležitostné/občasně přihlášené), a na požadovanou škálovatelnost a pružnost. Nakonec se posouzení uzavře kontrolou provozní kontinuity a požadavky na odolnost a také závislosti pro spuštění aplikace, pokud by došlo k přerušení služby.

> [!TIP]
> Tento přístup vyžaduje rozhovory a neoficiální zpětnou vazbu od obchodních a technických zúčastněných stran. Dostupnost klíčových jednotlivců je největší riziko pro časování. Neoficiální povaha datových zdrojů usnadňuje vytváření přesného odhadu nákladů nebo časování. Naplánujte předem plány a ověřte všechna shromážděná data.

## <a name="asset-driven-approach"></a>Přístup řízený Assetem

Přístup řízený prostředky poskytuje plán založený na assetech, které podporují migraci aplikace. V tomto přístupu vyžádáte statistická data o využití z databáze správy konfigurace (CMDB) nebo jiných nástrojů pro vyhodnocení infrastruktury.

Tento přístup obvykle předpokládá IaaS model nasazení jako základní hodnotu. V tomto procesu analýza vyhodnocuje atributy jednotlivých assetů: paměť, počet procesorů (jádra procesoru), prostor úložiště operačního systému, datové jednotky, síťové karty, protokoly IPv6, služba Vyrovnávání zatížení sítě, clustering, verze operačního systému, verze databáze (v případě potřeby), podporované domény a součásti nebo softwarové balíčky třetích stran mimo jiné. Prostředky, které v tomto přístupu zaznamenáte, se pak zarovnají s úlohami nebo aplikacemi pro účely mapování seskupení a závislostí.

> [!TIP]
> Tento přístup vyžaduje bohatou zdroj statistických údajů o využití. Čas potřebný ke kontrole inventáře a shromažďování dat představuje největší riziko pro časování. Zdroje dat nízké úrovně můžou přijít o závislosti mezi prostředky nebo aplikacemi. Naplánujte aspoň jeden měsíc na kontrolu inventáře. Před nasazením ověřte závislosti.

## <a name="incremental-approach"></a>Přírůstkový přístup

Důrazně doporučujeme přírůstkový přístup, protože provedeme pro mnoho procesů v rámci architektury pro přijetí do cloudu. V případě plánování digitální nemovitosti, které odpovídá multiphase procesu:

- **Analýza počátečních nákladů:** Pokud je vyžadováno finanční ověření, začněte s přístupem řízeným prostředkem, který je popsán dříve, a získat počáteční výpočet nákladů pro celou digitální nemovitosti bez racionalizace. Tím se vytvoří srovnávací test scénářů v nejhorším případě.

- **Plánování migrace:** Po sestavení týmu cloudové strategie Sestavte počáteční backlog migrace pomocí pracovního postupu založeného na úlohách, který je založený na jejich kolektivních znalostech a omezených rozhovorech účastníků. Tento postup rychle sestaví zjednodušené vyhodnocení úloh, které podporuje spolupráci.

- **Plánování vydání:** V každé vydané verzi se nevyřízené položky migrace vyřadí a přesměrují do priorit, aby se zaměřily na relevantní dopad na firmu. Během tohoto procesu se jako vydaných verzí vyberou další pět až deset úloh. V tomto okamžiku tým strategie cloudu investuje čas na dokončení podrobného přístupu řízeného úlohami. Toto posouzení bude odloženo až do chvíle, kdy bude vydaná verze lépe respektovat čas zúčastněných stran. Také zpozdí investici do úplné analýzy, dokud se společnost nezačne zobrazovat výsledky z dřívějšího úsilí.

- **Analýza spuštění:** Před migrací, modernizaci nebo replikací libovolného assetu ho posuďte individuálně i v rámci kolektivního vydání. V tuto chvíli je možné zkontrolovat data z počátečního přístupu na základě prostředků, aby se zajistila správná velikost a provozní omezení.

> [!TIP]
> Tento přírůstkový přístup umožňuje jednodušší plánování a urychlení výsledků. Je důležité, aby všechny zúčastněné strany pochopily přístup k opožděnému rozhodování. Je stejně důležité, aby byly předpoklady v jednotlivých fázích zdokumentovány, aby nedošlo ke ztrátě podrobností.

## <a name="next-steps"></a>Další kroky

Po výběru přístupu se může inventář shromažďovat.

> [!div class="nextstepaction"]
> [Shromáždění dat inventáře](./inventory.md)
