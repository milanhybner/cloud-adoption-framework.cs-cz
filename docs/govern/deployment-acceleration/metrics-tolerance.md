---
title: Metriky akcelerace nasazení, indikátory a tolerance rizik
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Metriky akcelerace nasazení, indikátory a tolerance rizik
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d7a7965acb7b1ace74983c7d0e1e65c3d47b2cc5
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220706"
---
# <a name="deployment-acceleration-metrics-indicators-and-risk-tolerance"></a>Metriky akcelerace nasazení, indikátory a tolerance rizik

Tento článek vám pomůže kvantifikovat toleranci obchodního rizika v souvislosti s akcelerací nasazení. Definování metrik a indikátorů vám pomůže vytvořit obchodní případ, který zajistí investici do splatnosti oboru akcelerace nasazení.

## <a name="metrics"></a>Metriky

Obor akcelerace nasazení se zaměřuje na rizika související s tím, jak se konfigurují, nasazují, aktualizují a udržují cloudové prostředky. Následující informace jsou užitečné při přijímání tohoto pravidla zásad správného řízení cloudu:

- **Selhání nasazení:** Procento nasazení, která selžou nebo způsobují nesprávně nakonfigurované prostředky.
- **Čas do nasazení:** Množství času potřebného k nasazení aktualizací do stávajícího systému.
- **Prostředky nesplňující předpisy:** Počet nebo procentuální podíl prostředků, které nedodržují definované zásady.

## <a name="risk-tolerance-indicators"></a>Indikátory tolerance rizik

Rizika související s akcelerací nasazení jsou převážně v podstatě týkající se počtu a složitosti cloudových systémů nasazených pro váš podnik. Vzhledem k růstu vaší cloudové služby se zvýší počet nasazených systémů a frekvence aktualizace prostředků cloudu. Závislosti mezi prostředky zvyšují důležitost zajištění správné konfigurace prostředků a navrhování systémů pro odolnost v případě, že jeden nebo více prostředků dochází k neočekávanému výpadku.

<!-- "en-us" location is required for the URL below. -->

Tradiční firemní IT oddělení často vypracovali operace, zabezpečení a vývojové týmy, které často nespolupracují dobře nebo jsou dokonce Adversarial nebo nepřátelně navzájem. V brzké době se tyto výzvy uznávají a integrují klíčové účastníky z každého týmu, které vám pomůžou zajistit flexibilitu v průběhu vašeho cloudového přijetí a přitom zůstat zabezpečený a dobře řízený. Proto by se jedna měla zvážit přijetí DevOps nebo [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) organizační kultury na začátku v cestě k přijetí vašeho cloudu. 

Spolupracujte se svým DevSecOps týmem a obchodními stranami a Identifikujte [obchodní rizika](./business-risks.md) související s konfigurací a pak určíte přijatelné standardní hodnoty pro odolnost proti riziku konfigurace. V této části doprovodné materiály k rozhraní pro přijetí do cloudu najdete příklady, ale podrobná rizika a směrné plány vaší společnosti nebo nasazení se nejspíš budou lišit.

Jakmile budete mít základnu, stanovte minimální srovnávací testy představující nepřijatelný nárůst zjištěných rizik. Tyto srovnávací testy fungují jako triggery, pokud potřebujete provést akci k nápravě těchto rizik. Následuje několik příkladů, jak se metriky související se konfigurací, jako jsou výše popsané výše, můžou zvýšit investice do oboru akcelerace nasazení.

- **Aktivační události posunu konfigurace:** Společnost, u které dochází k neočekávaným změnám v konfiguraci klíčových systémových komponent nebo selhání při nasazení nebo aktualizacích systémů, by měla investovat do oboru akcelerace nasazení, aby identifikovala hlavní příčiny a kroky pro nápravu.
- **Aktivační události mimo dodržování předpisů:** Pokud počet prostředků nesplňujících požadavky překročí stanovenou prahovou hodnotu (buď jako celkový počet prostředků, nebo procento z celkového počtu prostředků), společnost by měla investovat do vylepšení oboru akcelerace nasazení, aby se zajistilo, že se každý prostředek Konfigurace zůstává v souladu s životním cyklem daného prostředku.
- **Aktivační události plánu projektu:** Pokud čas nasadit prostředky společnosti a aplikace často překračuje prahovou hodnotu definovat, společnost by měla investovat do procesů zrychlení nasazení, aby zavedla nebo vylepšila automatizované nasazení za účelem zajištění konzistence a předvídatelnosti. Doba nasazení měřená ve dnech nebo dokonce i v týdnech obvykle indikuje strategii akcelerace nasazení, která je v podoptimálním prostředí.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md), metriky dokumentů a indikátory tolerance, které odpovídají aktuálnímu plánu přijetí do cloudu.

Projděte si ukázkové zásady akcelerace nasazení jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

> [!div class="nextstepaction"]
> [Kontrola ukázkových zásad](./policy-statements.md)
