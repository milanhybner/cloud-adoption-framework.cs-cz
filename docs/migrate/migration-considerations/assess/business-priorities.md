---
title: Obchodní priority během procesu transformace
description: Pomocí architektury cloudového přijetí pro Azure se naučíte udržovat obchodní zarovnání během dlouhodobě transformačního procesu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: df41ee9dfe94d0279f8a0c29982e8aff2dd83782
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312046"
---
# <a name="business-priorities-maintaining-alignment"></a>Obchodní priority: zachování zarovnání

*Transformace* se často definuje jako dramatická nebo spontánní změna. Na úrovni správní rady může změna vypadat jako dramatická transformace. Pro ty, kteří se procesem změny zabývají v organizaci, je ale pojem transformace poněkud zavádějící. Na této úrovni se transformace popisuje spíše jako série vhodně realizovaných přechodů od jednoho stavu k jinému.

Množství času potřebné k odůvodnění nebo přechodu úlohy se bude lišit v závislosti na technické složitosti. I když lze tento proces rychle aplikovat na jednu úlohu nebo skupinu aplikací, prosazení významných změn mezi uživatelskou základnou chce svůj čas. Rozšíření změn skrze různé úrovně existujících obchodních procesů trvá déle. Pokud se od transformace očekává, že změní vzorce chování uživatelů, mohou se významné výsledky projevit později.

Trh ale bohužel nečeká, až firma přechod dokončí. Vzorce chování uživatelů se mění samy, a to často neočekávaně. Vnímání firmy a jejích produktů na trhu může být ovlivněno sociálními médii nebo pozicí konkurence. Rychlé a neočekávané změny na trhu vyžadují, aby firmy byly pohotové a rychle reagovaly.

Schopnost realizovat procesy a technické přechody vyžaduje konzistentní a stabilní úsilí. Reakce na podmínky trhu vyžaduje rychlá rozhodnutí a hbité akce. To si navzájem odporuje, takže se snadno může stát, že priority nejsou v souladu. Tento článek popisuje přístupy pro zachování souladu během migrace.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-business-and-technical-priorities-stay-aligned-during-a-migration"></a>Jak mohou obchodní a technické priority zůstat během migrace v souladu?

Tým přechodu na cloud a tým zásad správného řízení cloudu se zaměřují na realizaci aktuální iterace a aktuální verze. Iterace zajišťují stabilní přírůstky technických prací a zabraňují tak nákladným náhlým změnám, které by jinak zpomalily prostup migrace. Verze zajišťují, aby technické úsilí a energie zůstaly zaměřené na obchodní cíle migrace úloh. Projekt migrace může vyžadovat spoustu verzí za dlouhé období. Do jeho dokončení se pravděpodobně výrazně změní podmínky na trhu.

Tým cloudové strategie se souběžně soustředí na realizaci plánu obchodních změn a přípravu na příští verzi. Tým cloudové strategie obecně sleduje alespoň jednu verzi dopředu a monitoruje měnící se podmínky na trhu a odpovídajícím způsobem upravuje backlog migrace. Toto zaměření na řízení transformace a úpravy plánu vytváří přirozené oblasti, ve kterých probíhají technické práce. Když se změní obchodní priority, je jejich převzetí jen jednu verzi pozadu, což zajišťuje technickou a obchodní agilitu.

## <a name="business-alignment-questions"></a>Otázky k obchodní rovnováze

Následující otázky mohou týmu cloudové strategie pomoci zformovat a stanovit prioritu backlogu migrace tak, aby bylo transformační úsilí v souladu s aktuálními obchodními potřebami.

- Identifikoval tým přechodu na cloud seznam úloh připravených k migraci?
- Vybral tým přechodu na cloud z tohoto seznamu úloh jednoho kandidáta na počáteční migraci?
- Mají tým přechodu na cloud a tým zásad správného řízení cloudu všechna nezbytná data týkající se úloh a cloudového prostředí, aby uspěly?
- Má kandidátská úloha nejvýznamnější dopad na firmu v příští verzi?
- Jsou některé jiné úlohy lepšími kandidáty pro migraci?

## <a name="tangible-actions"></a>Konkrétní akce

Během realizace plánu obchodních změn monitoruje tým cloudové strategie pozitivní a negativní výsledky. Pokud z těchto pozorování vyplyne technická změna, doplní se úpravy ve formě pracovních položek do backlogu verze a upřednostní se v příští iteraci.

Při změně na trhu spolupracuje tým cloudové strategie s firmou, aby porozuměl tomu, jak na tyto změny nejlépe reagovat. Pokud tato reakce vyžaduje změnu v prioritách migrace, upraví se backlog migrace. Úlohy, které měly dříve nižší prioritu, se tak přesunou nahoru.

## <a name="next-steps"></a>Další kroky

Díky správně sladěným obchodním prioritám může tým přechodu na cloud bez obav začít [vyhodnocovat úlohy](./evaluate.md) pro vývoj architektury a plánů migrace.

> [!div class="nextstepaction"]
> [Vyhodnocení úloh](./evaluate.md)
