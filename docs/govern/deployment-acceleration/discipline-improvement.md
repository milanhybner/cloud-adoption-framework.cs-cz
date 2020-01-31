---
title: Vylepšení oboru akcelerace nasazení
description: Vylepšení oboru akcelerace nasazení
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c5f07137ac1ca8c3ddbc4717dba5622096551862
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805927"
---
# <a name="deployment-acceleration-discipline-improvement"></a>Vylepšení oboru akcelerace nasazení

Disciplína akcelerace nasazení se zaměřuje na vytvoření zásad, které zajistí, že se prostředky nasadí a nakonfigurují konzistentně a opakují a zůstávají v dodržování předpisů v celém životním cyklu. V pěti oborech zásad správného řízení cloudu zahrnuje akcelerace nasazení rozhodnutí týkající se automatizace nasazení, artefaktů nasazení zdrojového kódu, monitorování nasazených prostředků pro udržení požadovaného stavu a auditování všech dodržování předpisů. Chyba.

Tento článek popisuje některé potenciální úkoly, se kterými se může vaše společnost zapojit, aby se zlepšil vývoj a vývoj v oboru akcelerace nasazení. Tyto úlohy je možné rozdělit na plánování, sestavování, přijímání a provozní fáze implementace cloudového řešení, které se pak iterovat na to, že umožní vývoj [přírůstkového přístupu ke správě cloudu](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Čtyři fáze přijetí](../../_images/govern/adoption-phases.png)

*Obrázek 1 – fáze přijetí přírůstkového přístupu ke zásadám správného řízení cloudu.*

U každého dokumentu není možné brát v úvahu požadavky všech společností. Tento článek popisuje navrhované minimální a potenciální příklady aktivit pro každou fázi procesu maturation zásad správného řízení. Počáteční cíl těchto aktivit vám pomůže vytvořit [MVP pro zásady](../guides/index.md#an-incremental-approach-to-cloud-governance) a vytvořit rozhraní pro přírůstkové zlepšování zásad. Váš tým zásad správného řízení vašeho cloudu bude muset rozhodnout, kolik z nich investovat do těchto aktivit, aby vylepšili možnosti zásad správného řízení vaší identity.

> [!CAUTION]
> Minimální ani potenciální aktivity, které jsou uvedené v tomto článku, jsou zarovnané na konkrétní podnikové zásady nebo požadavky na dodržování předpisů třetích stran. Tento návod je navržený tak, aby usnadnil konverzace, které vedou k vyrovnání obou požadavků s modelem zásad správného řízení pro Cloud.

## <a name="planning-and-readiness"></a>Plánování a připravenost

Tato fáze předběžných postupů řízení vypořádání mostů mezi obchodními výsledky a strategiemi, které se s nimi možné. Během tohoto procesu vedoucí týmu definuje konkrétní metriky, mapuje tyto metriky na digitální nemovitosti a zahájí plánování celkové snahy o migraci.

**Minimální navrhované aktivity:**

- Vyhodnoťte možnosti [akcelerace nasazení sada nástrojů](./toolchain.md) a implementujte hybridní strategii, která je vhodná pro vaši organizaci.
- Vývoj konceptu pokynů k architektuře a distribuce pro klíčové účastníky
- Informujte a zapojte lidi a týmy, kterých se týkalo vývoje pokynů pro architekturu.
- Vývojové týmy a zaměstnanci IT pomáhají pochopit principy a strategie DevSecOps a důležitost plně automatizovaných nasazení v oboru akcelerace nasazení.

**Potenciální aktivity:**

- Definujte role a přiřazení, které budou řídit akceleraci nasazení v cloudu.

## <a name="build-and-predeployment"></a>Sestavení a přednasazení

**Minimální navrhované aktivity:**

- Pro nové cloudové aplikace zaveďte do začátku procesu vývoje plně automatizovaná nasazení. Tato investice bude zlepšit spolehlivost testovacích procesů a zajistí konzistenci napříč vývojovým, QA a produkčním prostředím.
- Uložte všechny artefakty nasazení, jako jsou šablony nasazení nebo konfigurační skripty, pomocí platformy pro správu zdrojového kódu, jako je GitHub nebo Azure DevOps.
- Ukládat všechny tajné klíče, hesla, certifikáty a připojovací řetězce v [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)
- Před implementací [akcelerace nasazení sada nástrojů](./toolchain.md)zvažte pilotní test a ujistěte se, že vaše nasazení co nejvíc zjednodušuje. Použijte zpětnou vazbu z pilotních testů během fáze předinstalace a podle potřeby opakujte.
- Vyhodnoťte logickou a fyzickou architekturu vašich aplikací a Identifikujte příležitosti pro automatizaci nasazení prostředků aplikace nebo zlepšení částí architektury pomocí dalších cloudových prostředků.
- Aktualizujte dokument s pokyny pro architekturu tak, aby zahrnoval plány nasazení a přijetí uživatelů a distribuovat do klíčových účastníků.
- Pokračujte ve vzdělávání lidí a týmů, které jsou ovlivněny pokyny pro architekturu.

**Potenciální aktivity:**

- Definujte kanál průběžné integrace a průběžného nasazování (CI/CD), abyste mohli plně spravovat vydávání aktualizací do vaší aplikace prostřednictvím vývojových, QA a produkčních prostředí.

## <a name="adopt-and-migrate"></a>Přijmout a migrovat

Migrace je přírůstkový proces, který se zaměřuje na přesun, testování a přijetí aplikací nebo úloh v existující digitální nemovitosti.

**Minimální navrhované aktivity:**

- Migrujte [akceleraci nasazení sada nástrojů](./toolchain.md) z vývoje do produkčního prostředí.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přípravě na vývojáře a IT oddělení.

**Potenciální aktivity:**

- Ověřte, zda jsou osvědčené postupy definované během fází sestavení a přednasazení správně provedeny.
- Zajistěte, aby všechny aplikace nebo úlohy odpovídaly strategii akcelerace nasazení před vydáním.

## <a name="operate-and-post-implementation"></a>Provoz a následné implementace

Po dokončení transformace musí být zásady správného řízení a provoz v provozu v rámci přirozeného životního cyklu aplikace nebo zátěže. Tato fáze řízení splatnosti se zaměřuje na aktivity, které se běžně přidávají po implementaci řešení, a cyklus transformace začíná stabilizovat.

**Minimální navrhované aktivity:**

- [Sada nástrojů akcelerace nasazení](./toolchain.md) můžete přizpůsobit na základě změn potřeb vaší organizace na změnu identity.
- Automatizujte oznámení a sestavy, které vám upozorní na potenciální problémy s konfigurací nebo nebezpečné hrozby.
- Monitorování a hlášení o využití aplikací a prostředků
- Ohlaste metriky po nasazení a distribuujte je účastníkům.
- Revidujte pokyny architektury a provedou budoucí procesy přijímání.
- Pravidelně komunikujte s a proškolujte postižené osoby a týmy, aby se zajistilo průběžné dodržování pravidel architektury.

**Potenciální aktivity:**

- Nakonfigurujte Nástroj pro monitorování a vytváření sestav konfigurace požadovaného stavu.
- Pravidelně kontrolujte nástroje pro konfiguraci a skripty, aby se zlepšily procesy a identifikovaly běžné problémy.
- Pracujte s týmy pro vývoj, provoz a zabezpečení, které vám pomůžou narušovat DevSecOps postupy a rozdělují organizace, které vedou k neefektivitám.

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte konceptu zásad správného řízení identity v cloudu, Projděte si [základní sada nástrojů identity](./toolchain.md) a Identifikujte nástroje a funkce Azure, které budete potřebovat při vývoji pravidel zásad správného řízení identity na platformě Azure.

> [!div class="nextstepaction"]
> [Sada nástrojů úrovně identity pro Azure](./toolchain.md)
