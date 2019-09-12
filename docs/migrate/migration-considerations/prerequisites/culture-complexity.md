---
title: 'Příprava na kulturní komplikace: sladění rolí a zodpovědností'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Připravte se na kulturní komplikace – slaďte role a zodpovědnosti.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 011d00038ea29c60601945441f21b14b8865f80d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833346"
---
# <a name="prepare-for-cultural-complexity-aligning-roles-and-responsibilities"></a>Příprava na kulturní komplikace: sladění rolí a zodpovědností

Pochopení kultury potřebné k provozování existujících datacenter je důležité pro úspěch každé migrace. V některých organizacích připadá správa datacenter na centralizovaný provozní tým IT. V těchto centralizovaných týmech bývají role a zodpovědnosti v rámci týmu dobře definované a chápané. U větších podniků, zejména u těch, které jsou vázané požadavky na dodržování předpisů třetích stran, bývá tato kultura odlišná a komplikovaná. Kulturní komplikace mohou vést k překážkám, které je obtížné pochopit a jejichž překonání je časově náročné.

V obou případech je vhodné investovat do dokumentování rolí a zodpovědností, které se vyžadují k dokončení migrace. Tento článek popisuje některé role a zodpovědnosti používané při migraci datacenter, a slouží jako šablona pro dokumentaci, která do realizace vnese jasno.

## <a name="business-functions"></a>Obchodní funkce

Při jakékoli migraci existuje několik klíčových funkcí, které by pokud možno měla realizovat firma. IT oddělení je často schopné následující úkoly provést. Zapojení členů firmy ale může pomoci eliminovat bariéry později v procesu přechodu na cloud. Zajišťuje také vzájemné investice klíčových účastníků během procesu migrace.

| Proces | Aktivita | Popis |
|---------|---------|---------|
| Posouzení | Obchodní cíle | Definujte požadované obchodní výsledky migračního úsilí. |
| Posouzení | Priority | Zajistěte soulad s měnícími se obchodními prioritami a podmínkami na trhu. |
| Posouzení | Zdůvodnění | Ověřte předpoklady, které stojí za změnou obchodních zdůvodnění. |
| Posoudit | Riziko | Pomozte týmu přechodu na cloud pochopit dopad reálných obchodních rizik. |
| Posoudit | Schválení | Zkontrolujte a schvalte obchodní dopad navrhovaných změn architektury. |
| Optimalizace | Plán změn | Definujte ve firmě plán realizace změn včetně období nízké aktivity a zablokování změn. |
| Optimalizace | Testování | Vyberte zkušené uživatele, kteří jsou schopni ověřit výkon a funkčnost. |
| Zabezpečení a správa | Dopad přerušení | Pomozte týmu přechodu na cloud vyčíslit vliv na přerušení firemních procesů. |
| Zabezpečení a správa | Ověření smlouvy o úrovni služeb (SLA) | Pomozte týmu přechodu na cloud při definování smluv o úrovni služeb a přijatelných tolerancí pro výpadky. |

V konečném důsledku je za každou z těchto činností zodpovědný tým přechodu na cloud. Stanovení zodpovědností a pravidelných schůzek s firmou kvůli provádění těchto činností v určeném tempu však může zlepšit angažovanost účastníků a soudržnost s firmou.

## <a name="common-roles-and-responsibilities"></a>Obecné role a zodpovědnosti

Každý proces v rámci diskuse o principech migrace Architektury přechodu na cloud obsahuje článek popisující konkrétní činnosti pro sladění rolí a zodpovědností. Kvůli jasným kompetencím během realizace by ke každé činnosti měla být přiřazena zodpovědná strana spolu s případnými pomocnými stranami potřebnými pro podporu těchto činností. Následující seznam ale obsahuje řadu obecných rolí a zodpovědností, které mají větší vliv na realizaci migrace. Tyto role by se měly identifikovat na začátku migrace.

> [!NOTE]
> V následující tabulce by zodpovědná strana mohla zahájit sladění rolí. Kvůli efektivní realizaci by se tento sloupec měl přizpůsobit stávajícím procesům. V ideálním případě by jako zodpovědná strana měla být jmenována jedna osoba.

| Proces | Aktivita | Popis | Zodpovědná strana |
|---------|---------|---------|---------|
| Požadavek | Digitální aktiva | Na základě obchodních výsledků slaďte existující inventář se základními předpoklady. | Tým cloudové strategie |
| Požadavek | Backlog migrace | Určete prioritu posloupnosti úloh, které se mají migrovat. | Tým cloudové strategie |
| Posoudit | Architektura | Rozebráním prvotních předpokladů definujte cílovou architekturu na základě metrik využití. | Tým přechodu na cloud |
| Posoudit | Schválení | Schvalte navrhovanou architekturu. | Tým cloudové strategie |
| Migrace | Přístup k replikaci | Zpřístupněním existujících místních hostitelů a prostředků zřiďte procesy replikace. | Tým přechodu na cloud |
| Optimalizace | Připraven | Před povýšením ověřte, že systém splňuje požadavky na výkon a náklady. | Tým přechodu na cloud |
| Optimalizace | Povýšení | Oprávnění k povýšení úlohy do produkce a přesměrování produkčního provozu. | Tým přechodu na cloud |
| Zabezpečení a správa | Přechod provozu | Před provozními operacemi zdokumentujte produkční systémy. | Tým přechodu na cloud |

> [!CAUTION]
> Tyto činnosti, oprávnění a autorizace silně ovlivňují zodpovědnou stranu, která musí mít přímý přístup k produkčním systémům ve stávajícím prostředí nebo prostředky zabezpečeného přístupu prostřednictvím jiných odpovědných aktérů. Určení této zodpovědné strany přímo ovlivňuje strategii povýšení během procesů migrace a optimalizace.

## <a name="next-steps"></a>Další postup

Jakmile je tým všeobecně seznámen s rolemi a zodpovědnostmi, je čas začít připravovat technické podrobnosti migrace. Znalost [technické složitosti a správy změn](./technical-complexity.md) může pomoci připravit tým přechodu na cloud na technické záludnosti migrace tím, že bude postupovat v souladu s procesem správy postupných změn.

> [!div class="nextstepaction"]
> [Technická složitost a správa změn](./technical-complexity.md)