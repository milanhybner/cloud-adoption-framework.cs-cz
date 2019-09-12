---
title: 'Migrace sálového počítače: Mýty a fakta'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrujte aplikace z sálových prostředí do Azure, osvědčené, vysoce dostupné a škálovatelné infrastruktury pro systémy, které se aktuálně spouštějí na sálových počítačích.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7a3e1c7cd0003191838f08569b18de4626745745
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70830993"
---
# <a name="mainframe-myths-and-facts"></a>Mýty sálového počítače a fakta

Sálové počítače jsou výrazně v historii výpočetního prostředí a zůstávají životaschopné pro vysoce specifické úlohy. Nejvíc souhlasíte s tím, že sálové počítače jsou prověřené platformy s dlouhodobě zavedenými provozními postupy, které zajistí jejich spolehlivé a robustní prostředí. Software se spouští na základě využití, měřeno v milionech instrukcí za sekundu (MIPS) a pro vratek jsou k dispozici rozsáhlé sestavy o využití.

Spolehlivost, dostupnost a výpočetní výkon sálových počítačů se vychází z téměř mythicalch poměrů. Abyste vyhodnotili úlohy pro sálové počítače, které jsou pro Azure nejvhodnější, je nejdříve potřeba odlišit mýty od reality.

## <a name="myth-mainframes-never-go-down-and-have-a-minimum-of-five-9s-of-availability"></a>Mýtus Sálové počítače se nikdy neprovozují a mají minimálně pět devítky dostupnosti.

Sálový hardware a operační systémy se zobrazují jako spolehlivé a stabilní. Je ale možné, že výpadky musí být naplánované pro údržbu a restartování (označované jako počáteční načtení programu nebo IPLs). Při zvážení těchto úloh se řešení sálového počítače často blíží dvěma nebo třem devítky dostupnosti, což je ekvivalentem vysoce špičkových serverů se systémem Intel.

Sálové počítače také zůstávají jako zranitelné vůči haváriím jako jakékoli jiné servery a vyžadují, aby tyto typy selhání byly ošetřeny systémy nepřerušitelného zdroje napájení (UPS).

## <a name="myth-mainframes-have-limitless-scalability"></a>Mýtus Sálové počítače mají neomezenou škálovatelnost.

Škálovatelnost sálového počítače závisí na kapacitě svého systémového softwaru, jako je třeba systém pro řízení informací o zákaznících (CICS), a na kapacitu nových instancí sálových strojů a úložišť. Některé velké společnosti, které používají sálové počítače, si přizpůsobily jejich CICS k výkonu a v ostatních případech vypěstují schopnost největších dostupných sálových počítačů.

## <a name="myth-intel-based-servers-are-not-as-powerful-as-mainframes"></a>Mýtus Servery založené na technologii Intel nejsou tak výkonné jako sálové počítače.

Nové základní-husté systémy založené na procesorech Intel mají tolik výpočetní kapacity jako sálové počítače.

## <a name="myth-the-cloud-cant-accommodate-mission-critical-applications-for-large-companies-such-as-financial-institutions"></a>Mýtus Cloud nemůže pojmout klíčové aplikace pro velké společnosti, jako jsou finanční instituce.

I když se může jednat o některé izolované instance, u kterých cloudová řešení jsou krátká, je obvykle to proto, že se algoritmy aplikace nedají distribuovat. Tyto příklady jsou výjimky, nikoli pravidlo.

## <a name="summary"></a>Souhrn

Díky porovnání nabízí Azure alternativní platformu, která dokáže poskytovat ekvivalentní funkce a funkce sálového počítače, a to s mnohem nižšími náklady. Navíc platí, že celkové náklady na vlastnictví cloudového modelu založeného na předplatném, které jsou na základě využití založené na předplatném, je mnohem levnější než u sálových počítačů.

## <a name="next-steps"></a>Další postup

> [!div class="nextstepaction"]
> [Přepnutí z sálových počítačů do Azure](migration-strategies.md)
