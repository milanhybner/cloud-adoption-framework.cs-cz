---
title: Schválení změn architektury před migrací
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pochopení významu schvalování před migrací
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: cdc6abe2be94bb0d91047d4d64a0774bac6a8e0e
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549224"
---
# <a name="approve-architecture-changes-before-migration"></a>Schválení změn architektury před migrací

Během procesu posuzování migrace prochází každá úloha vyhodnocením, návrhem architektury a odhadem, aby pro ni bylo možné připravit plán budoucího stavu. Některé úlohy můžou být migrovány do cloudu bez změny architektury. Pokud zachováte místní konfiguraci a architekturu, snížíte tím riziko a zjednodušíte postup migrace. Bohužel každá aplikace nepoběží v cloudu beze změn architektury. Pokud potřebujete změnit architekturu, pomůže vám tento článek změnu klasifikovat a najdete v něm také pokyny, jak správně schvalovat aktivity.

## <a name="business-impact-and-approval"></a>Obchodní dopad a schválení

Při migraci se některé věci pravděpodobně změní takovým způsobem, který ovlivní firmu. I když se změnou někdy nelze vyhnout, překvapením v důsledku nezveřejňovaného nebo nedokumentované změny by měly být. Aby bylo možné udržovat podporu účastníků v průběhu migrace, je důležité se vyhnout překvapením. Překvapení vlastníci aplikací nebo firemní účastníci můžou zpomalit nebo úplně zastavit vaši snahu o zavedení cloudu.

Před migrací je důležité připravit firemního vlastníka pracovního procesu pro všechny změny, které by mohly mít vliv na obchodní procesy, jako jsou například změny:

- Smlouvy o úrovni služeb.
- Přístupové vzorce nebo požadavky na zabezpečení, které ovlivňují koncového uživatele.
- Postupy uchovávání dat.
- Výkon základní aplikace.

I když můžete úlohu migrovat s minimálními změnami nebo i bez nich, může mít tento proces dopad na firmu. Replikační postupy můžou zpomalit výkon provozních systémů. Změny prostředí při přípravě na migraci můžou omezit výkon při směrování nebo můžou omezit výkon sítě. Aktivity spojené s replikací, fázováním nebo zvýšením úrovně můžou mít i další dopady.

Pravidelné schvalování minimalizuje nebo úplně eliminuje překvapení způsobená změnami a minimalizuje nebo eliminuje také dopady sníženého výkonu. Tým přechodu na cloud by měl na konci procesu posouzení, ale ještě před zahájením migrace iniciovat proces schválení změn.

## <a name="existing-culture"></a>Stávající kultura

Týmy IT pravděpodobně mají mechanismy na řízení změn, které se týkají místních prostředků. Tyto mechanismy se většinou řídí tradičními procesy změnového řízení založenými na standardu ITIL (Information Technology Infrastructure Library). U mnoha podnikových migrací se těchto procesů účastní poradní rada pro změny (CAB), která zodpovídá za kontrolu, dokumentaci a schválení všech změnových požadavků, které se týkají IT.

V radě CAB jsou většinou odborníci z více týmů IT a firemních týmů, kteří můžou nabídnout různé úhly pohledu a mají podrobný přehled o všech změnách týkajících se IT. Proces schvalování radou CAB představuje ověřený způsob, jak snížit riziko a minimalizovat obchodní dopad změn, které ovlivňují stabilitu úloh v důsledku operací řízených IT.

## <a name="technical-approval"></a>Technické schválení

K nejčastějším důvodům neúspěšné migrace do cloudu patří nepřipravenost organizace na schvalování technických změn. Kvůli řadě technických schválení se zastaví více projektů než kvůli nedostatkům cloudové platformy. Připravenost organizace na schvalování technických změn je důležitým předpokladem úspěšné migrace. Následující osvědčené postupy zajistí, aby byla organizace připravena na schvalování technických záležitostí.

### <a name="itil-change-advisory-board-challenges"></a>Problémy poradní rady pro změny (CAB) týkající se standardu ITIL

Každý přístup ke změnovému řízení má vlastní sadu kontrolních a schvalovacích procesů. Migrace je řada nepřetržitých změn, která se na začátku vyznačuje vysokým stupněm nejednoznačnosti a jasnějších obrysů nabývá až během realizace. Proto se k řízení migrace nejlépe hodí přístup založený na agilním změnovém řízení, kdy je vlastníkem produktu tým cloudové strategie.

Ale rozsah a frekvence změn při migraci do cloudu přesně neodpovídá povaze procesů ITIL. Požadavek týkající se schvalování radou CAB může ohrozit úspěch migrace, protože může migrační úsilí zpomalit nebo i zastavit. Navíc v úvodních fázích je migrace nejednoznačná a zkušeností s danou problematikou je spíše méně. U několika prvních migrací nebo vydaných verzí se tým přechodu na cloud často spíše učí. Proto může být pro tým obtížné, aby dokázal poskytnout takový typ dat, jaký potřebuje rada CAB ke schválení.

Následující osvědčené postupy pomůžou radě CAB zachovat si při migraci určitý manévrovací prostor, aniž by představovala nepříjemnou překážku.

### <a name="standardize-change"></a>Standardizace změn

Tým přechodu na cloud možná nechce u každé úlohy migrované do cloudu podrobně zvažovat rozhodnutí týkající se architektury. A naopak zase může chtít použít migraci do cloudu jako katalyzátor opětovného uskutečnění starších rozhodnutí o architektuře. Pokud organizace migrují několik set virtuálních počítačů nebo několik desítek úloh, dají se oba přístupy správně uřídit. Ale při migraci datacentra, které čítá 1000 nebo více prostředků, se oba uvedené přístupy považují za vysoce riskantní, nevhodný postup, který výrazně snižuje pravděpodobnost úspěchu. Modernizace, refaktoring a vytvoření nové architektury vyžadují u každé aplikace různé sady dovedností a zcela jiné druhy změn. Tyto úkoly ve velké míře závisejí na lidském úsilí. Každá z těchto závislostí představuje pro migraci riziko.

Článek o [racionalizaci digitálních aktiv](../../../digital-estate/rationalize.md) vysvětluje základní předpoklady racionalizace digitálních aktiv a jejich dopad na flexibilitu a úsporu času. Standardizace změn přináší také další výhodu. Pokud zvolíte výchozí racionalizační přístup, kterým se migrace řídí, může rada CAB nebo vlastník produktu kontrolovat a schvalovat použití jedné změny na dlouhý seznam úloh. Tím se omezí technické schvalování každé úlohy jenom na ty, jejichž kompatibilita s cloudem vyžaduje výrazné změny architektury.

### <a name="clarify-expectations-and-roles-of-approvers"></a>Vyjasnění očekávání a rolí schvalovatelů

Před posouzením první úlohy musí tým cloudové strategie zdokumentovat očekávání všech účastníků, kteří změnu schvalují, a tlumočit je ostatním. Tato jednoduchá aktivita pomůže týmu přechodu na cloud předejít nákladným zpožděním, když bude plně vytížený.

### <a name="seek-approval-early"></a>Včasné schvalování

Pokud to jde, je potřeba technické změny rozpoznat a zdokumentovat během procesu posuzování. Bez ohledu na schvalovací proces musí tým přechodu na cloud angažovat schvalovatele co nejdříve. Čím dříve může schvalování změny začít, tím menší pravděpodobnost je, že schvalovací proces zablokuje aktivity při migraci.

## <a name="next-steps"></a>Další kroky

Tyto osvědčené postupy mají usnadnit integraci správného schvalování do vaší migrace, abyste riskovali co nejméně. Jakmile tým přechodu na cloud schválí změny úloh, je připraven na [migraci úloh](../migrate/index.md).

> [!div class="nextstepaction"]
> [Migrace úloh](../migrate/index.md)
