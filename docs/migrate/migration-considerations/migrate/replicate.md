---
title: Replikace a proces migrace
description: Pochopení role, kterou replikace během procesu migrace přehraje, a jak naplánovat požadavky a rizika aktivit replikace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3d1251bba8da5ec17270de38ee94ed87483c4ac6
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429328"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-role-does-replication-play-in-the-migration-process"></a>Jakou roli hraje replikace v procesu migrace?

Místní datová centra jsou naplněná fyzickými aktivy, jako jsou servery, zařízení a síťová zařízení. Každý server je ale jenom fyzickou skořápkou. Skutečná hodnota pochází z binárního obsahu spuštěného na serveru. Účelem datového centra jsou aplikace a data. To jsou primární binární soubory, který je potřeba migrovat. Tyto aplikace a úložiště dat podporují další digitální aktiva a binární zdroje, jako jsou operační systémy, síťové trasy, soubory a protokoly zabezpečení.

Replikace je tahounem úsilí o migraci. Je to proces zkopírování verze různých binárních souborů k určitému časovému okamžiku. Binární snímky se pak zkopírují na novou platformu a nasadí se na nový hardware v rámci procesu, který se označuje jako *seeding*. Při správném provedení by se kopie binárního souboru měla chovat stejně jako původní binární soubor na starém hardwaru. Tento snímek binárního souboru je ale okamžitě zastaralý a neodpovídá původnímu zdroji. Kvůli sladění nového a starého binárního souboru proces, který se označuje jako *synchronizace*, průběžně aktualizuje kopii uloženou na nové platformě. Synchronizace pokračuje až do zvýšení úrovně aktiva ve shodě s vybraným modelem povýšení. V tomto okamžiku je synchronizace přerušena.

## <a name="required-prerequisites-to-replication"></a>Vyžadované předpoklady pro replikaci

Před replikací musí být *nová platforma* a hardware připravené pro příjem binárních kopií. Článek o [požadavcích](../prerequisites/index.md) popisuje minimální požadavky na prostředí, které vám pomůžou vytvořit bezpečnou, robustní a vysoce výkonnou platformu pro příjem binárních replik.

*Zdrojové binární soubory* musí být také pro replikaci a synchronizaci připravené. Články týkající se posouzení, architektury a nápravy řeší akce nezbytné k zajištění toho, aby byl zdrojový binární soubor připravený pro replikaci a synchronizaci.

Pro spouštění a správu procesů replikace a synchronizace musí být implementována *sada nástrojů*, která slaďuje novou platformu se zdrojovými binárními soubory. Článek o [možnostech replikace](./replicate-options.md) popisuje různé nástroje, které by mohly přispět k migraci do Azure.

## <a name="replication-risks---physics-of-replication"></a>Rizika replikace – fyzika replikace

Při plánování replikace jakýchkoli binárních zdrojů do nového cíle je při plánování a provádění vhodné zvážit několik základních zákonů.

- **Rychlost světla.** Při přesunu velkého objemu dat je optické vlákno stále nejrychlejší možností. Tyto kabely bohužel můžou přesouvat data pouze dvoutřetinovou rychlostí, než je rychlost světla. To znamená, že neexistuje žádná metoda okamžité nebo neomezené replikace dat.
- **Rychlost kanálu sítě WAN.** Víc než rychlost přesunu dat je šířka pásma pro odesílání, která definuje objem dat za sekundu, který se dá přenést v existující síti WAN společnosti na cílové datové centrum.
- **Rychlost rozšíření sítě WAN.** Pokud to dovolují rozpočty, můžete do řešení sítě WAN společnosti přidat další šířku pásma. Nákup, zřízení a integrace dalších optických připojení ale může trvat týdny nebo měsíce.
- **Rychlost disků.** Pokud by se data mohla pohybovat rychleji a neexistoval žádný limit šířky pásma mezi zdrojovým binárním souborem a cílovým místem, může být fyzika stále omezením. Data je možné replikovat pouze tak rychle, jak je lze číst ze zdrojových disků. Čtení každé jedničky a nuly z každého rotujícího disku v datovém centru vyžaduje čas.
- **Rychlost lidských výpočtů.** Disky a světla jsou rychlejší než procesy lidského rozhodování. Když musí skupina lidí spolupracovat a společně rozhodovat, výsledky budou přicházet ještě pomaleji. Replikace nemůže nikdy překonat prodlevy související s lidskou inteligencí.

Každý z těchto fyzikálních zákonů vede k následujícím rizikům, která obvykle ovlivňují plány migrace:

- **Doba replikace.** Pokročilé nástroje replikace nemůžou překonat základní fyzikální principy – replikace vyžaduje čas a šířku pásma. Plány by měly obsahovat realistické časové osy, která odráží dobu potřebnou k replikaci binárních souborů. *Celková dostupná šířka pásma migrace* je velikost odchozí šířky pásma, měřená v megabitech za sekundu (Mb/s) nebo gigabitech za sekundu (Gb/s), která se nespotřebuje jinými obchodními požadavky s vyšší prioritou. *Celkové úložiště migrace* je celkové místo na disku, měřené v gigabajtech nebo terabajtech, které je potřeba k uložení snímku všech migrovaných aktiv. Počáteční odhad doby se dá vypočítat tak, že vydělíte *celkové úložiště migrace* *celkovou dostupnou šířkou pásma migrace*. Nezapomeňte na převod bitů na bajty. Přesnější výpočet doby najdete v následujícím bodu Kumulativní účinek odchylky disků.
- **Kumulativní účinek odchylky disků.** Od okamžiku replikace až po povýšení aktiva do produkčního prostředí musí zdrojové a cílové binární soubory zůstat synchronizované. *Odchylka* binárních souborů spotřebovává další šířku pásma, protože všechny změny binárního souboru se musí replikovat opakovaně. Během synchronizace musí být do výpočtu celkového úložiště migrace zahrnuté všechny odchylky binárních souborů. Čím déle bude trvat zvýšení úrovně aktiva do produkčního prostředí, tím dojde k větší kumulativní odchylce. Synchronizace více aktiv znamená větší využití šířky pásma. U každého aktiva, které se drží ve stavu synchronizace, se ztrácí další kus z celkové dostupné šířky pásma migrace.
- **Čas na obchodní změnu.** Jak je uvedeno v předchozím bodu, Kumulativní účinek odchylky disků, doba synchronizace má kumulativní negativní vliv na rychlost migrace. Pro rychlost migrace je rozhodující upřednostnění backlogu migrace a rozšířená příprava pro [plán obchodních změn](../optimize/business-change-plan.md). Nejvýznamnějším testem obchodní a technické shody během migrace je tempo povýšení. Čím rychleji jde aktivum povýšit do produkčního prostředí, tím nižší bude vliv odchylky disků na šířku pásma a tím víc šířky pásma a času se dá přidělit replikaci další úlohy.

## <a name="next-steps"></a>Další kroky

Po dokončení replikace můžou začít [přípravné aktivity](./stage.md).

> [!div class="nextstepaction"]
> [Přípravné aktivity během migrace](./stage.md)
