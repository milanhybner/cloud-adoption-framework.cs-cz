---
title: Migrace do cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod k obsahu týkajícímu se migrace do cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1bf9497684c1043d23eec48b1ab5d5f1f12ef752
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829953"
---
# <a name="cloud-migration-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Migrace do cloudu v architektuře přechodu na cloud pro Azure od Microsoftu

Migrace do cloudu je proces přesunu stávajících digitálních prostředků na cloudovou platformu. V tomto přístupu se stávající prostředky replikují do cloudu s minimálními úpravami. Po zprovoznění aplikace nebo úlohy v cloudu se uživatelé převedou ze stávajícího řešení na cloudové řešení. Migrace do cloudu představuje jeden ze způsobů, jak efektivně zajistit rovnováhu cloudového portfolia. V krátkodobém měřítku se často jedná o nejrychlejší a nejflexibilnější přístup. Některé výhody cloudu naopak není možné tímto přístupem realizovat bez dalších budoucích úprav. Podniky a středně velcí zákazníci využívají tento přístup ke zrychlení tempa změn, k vyhnutí se plánovaným kapitálovým výdajům a ke snížení průběžných provozních nákladů.

## <a name="cloud-migration-guidance"></a>Pokyny k migraci do cloudu

Pokyny v této části architektury přechodu na cloud jsou určené ke dvěma účelům:

- Poskytnout prakticky použitelné průvodce migrací představující běžná prostředí, se kterými se zákazníci často setkávají. Každý průvodce zapouzdřuje proces a nástroje, které jsou potřeba k úspěšnému dokončení migrace do cloudu. Pokyny k návrhu jsou nutně specifické pro Azure. Všechna ostatní doporučení v těchto průvodcích je možné využít v rámci přístupu nezávislého na konkrétním cloudu nebo přístupu s více cloudy.
- Prostřednictvím podrobných pokynů k vývoji procesů, rolí a odpovědností a řízení správy změn pomoct čtenářům vytvářet přizpůsobené plány migrace do několika veřejných cloudů, které umožní splnit nejrůznější obchodní potřeby.

Tento obsah je určený pro tým přechodu na cloud. Také je relevantní pro cloudové architekty, kteří potřebují vyvinout pevný základ pro migraci do cloudu.

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Pokyny v architektuře přechodu na cloud mají vliv na obchodní aktivity, technologie a kulturu podniků. Tato část významně ovlivňuje vlastníky aplikací, pracovníky správy změn (například PMO a pracovníky agilní správy), finanční a obchodní vedoucí pracovníky a tým přechodu na cloud. Mezi těmito osobami existují různé závislosti a cloudoví architekti využívající tyto pokyny proto budou muset zvolit přístup, který je usnadní. Usnadnění pro tyto týmy může být jednorázové, ale v některých případech může vést k opakovaným interakcím s těmito dalšími osobami.

Cloudový architekt slouží jako vizionář a zprostředkovatel, který má tyto cílové skupiny dát dohromady. Obsah v této kolekci průvodců je určený k tomu, aby cloudovým architektům pomohl usnadnit správnou konverzaci se správnou cílovou skupinou, která umožní přijetí nezbytných rozhodnutí. Obchodní transformace, kterou umožňuje cloud, závisí na roli cloudového architekta, který pomáhá s přijímáním obchodních a IT rozhodnutí.

**Specializace cloudových architektů v této části:** Jednotlivé části architektury přechodu na cloud představují různé specializace nebo varianty role cloudových architektů. Tato část je určená pro cloudové architekty s odbornými znalostmi v oblasti stávajícího místního prostředí a způsobu, jakým ovlivňuje možnosti migrace.

**Rozdělení povinností:** V mnoha společnostech existuje rozdělení povinností kvůli omezení přístupu k produkčním systémům nebo segmentům podnikového prostředí. V takovém případě bude proces migrace ještě složitější. V některých případech můžou tyto role a zodpovědnosti vyžadovat několik cloudových architektů, aby pokryli celý proces migrace.

**Možnosti partnerství:** Napříč těmito procesy se budou týmy učit nové dovednosti a přístupy k technickému provádění. Rozšiřování technických dovedností mezi stávající členy týmu je během provádění jednou možností. Druhou je přijetí dalších zaměstnanců. Partnerství s třetími stranami často přináší výrazné zrychlení a snížení rizik. [Možnosti partnerství](./migration-considerations/assess/partnership-options.md) můžou při rozhodování o výběru nejlepšího partnerství pomáhat.

## <a name="next-steps"></a>Další postup

Čtenářům, kteří podle tohoto průvodce chtějí postupovat od začátku do konce, tento obsah pomůže vyvinout robustní strategii migrace do cloudu. Pokyny čtenáře provedou teorií a implementací takové strategie.

V prvním kroku se doporučuje, aby čtenáři pracovali s pomocí [průvodce migrací do Azure](./azure-migration-guide/index.md) a pochopili standardní sadu nástrojů a přístupů potřebných k migraci v běžném případu použití. Následně je možné základní pokyny rozšířit tak, aby vyhovovaly potřebám čtenářů prostřednictvím [složitých scénářů migrace](./expanded-scope/index.md), [osvědčených postupů migrace](./azure-best-practices/index.md) a [aspektech migrace](./migration-considerations/index.md).

> [!div class="nextstepaction"]
> [Průvodce migrací do Azure](./azure-migration-guide/index.md)