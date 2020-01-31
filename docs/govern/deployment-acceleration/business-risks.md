---
title: Motivace a obchodní rizika, které řídí akceleraci nasazení
description: Seznamte se s principem akcelerace nasazení v rámci strategie zásad správného řízení cloudu.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c9bdb912311aac6c926402753a678b9f191594c9
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806386"
---
# <a name="deployment-acceleration-motivations-and-business-risks"></a>Motivace akcelerace a obchodní rizika pro nasazení

Tento článek popisuje důvody, proč zákazníci obvykle přijímají pravidla akcelerace při nasazení v rámci strategie zásad správného řízení cloudu. Poskytuje také několik příkladů obchodních rizik, které řídí příkazy zásad.

<!-- markdownlint-disable MD026 -->

## <a name="deployment-acceleration-relevancy"></a>Relevanci akcelerace nasazení

Místní systémy se často nasazují pomocí standardních imagí nebo instalačních skriptů. Je obvykle potřeba další konfigurace, která může zahrnovat několik kroků nebo lidské intervence. Tyto ruční procesy jsou náchylné k chybám a často způsobují "posun konfigurace", který vyžaduje časově náročné odstraňování potíží a nápravné úlohy.

Většinu prostředků Azure je možné nasadit a nakonfigurovat ručně prostřednictvím Azure Portal. Tento přístup může být dostačující pro vaše potřeby, pokud máte jen několik prostředků ke správě. Vzhledem k tomu, že se vaše cloudové prostředky rozšiřují, by se měla vaše organizace začínat integrací automatizace do procesů nasazení, aby se zajistilo, že vaše cloudové prostředky zabraňují posunu konfigurace ani jiným problémům, Přijetí přístupu DevOps nebo [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) je často nejlepším způsobem, jak spravovat nasazení během vyspělého úsilí o přijetí do cloudu.

<!-- "en-us" location is required for the URL above. -->

Robustní plán akcelerace nasazení zajišťuje, aby vaše cloudové prostředky byly nasazené, aktualizované a správně nakonfigurované a trvale a zůstaly v tomto případě. Doba splatnosti strategie akcelerace nasazení může být ve vaší [cost management strategii](../cost-management/index.md)významným faktorem. Automatizované zřizování a konfigurace vašich cloudových prostředků vám umožní horizontální navýšení nebo snížení kapacity prostředků, pokud je poptávka nízká nebo časově závislá, takže platíte jenom za prostředky, které potřebujete.

## <a name="business-risk"></a>Obchodní riziko

Obor akcelerace nasazení se pokusí vyřešit následující obchodní rizika. Při přijetí cloudu Sledujte relevanci každé z těchto možností:

- **Přerušení služby:** Nedostatečné předvídatelné opakované procesy nasazení nebo nespravované změny konfigurace systému můžou mít za následek ztrátu normálních operací a můžou vést ke ztrátě produktivity nebo ztráty podniku.
- **Náklady na přetečení:** Neočekávané změny v konfiguraci systémových prostředků mohou ztížit identifikaci hlavní příčiny problémů, což vyvolává náklady na vývoj, provoz a údržbu.
- **Neefektivita organizace:** Překážky mezi vývojem, provozem a týmy zabezpečení můžou způsobovat spoustu výzev k efektivnímu přijetí cloudových technologií a vývoji sjednoceného modelu zásad správného cloudu.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat obchodní rizika, která by mohla být zavedena aktuálním plánem přijetí cloudu.

Jakmile bude navázáno porozumění reálným obchodním rizikům, je dalším krokem vytvoření dokumentu tolerance firmy pro rizika a indikátory a klíčové metriky pro monitorování této tolerance.

> [!div class="nextstepaction"]
> [Metriky, ukazatele a tolerance rizik](./metrics-tolerance.md)
