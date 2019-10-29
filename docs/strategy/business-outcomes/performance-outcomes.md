---
title: Příklady výsledků výkonu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Příklady výsledků výkonu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: d772f7c8a2e7c76770a6496bb85acbac54debfe4
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/29/2019
ms.locfileid: "73048349"
---
# <a name="examples-of-performance-outcomes"></a>Příklady výsledků výkonu

Jak je popsáno v tématu [obchodní výsledky](./index.md), několik potenciálních obchodních výsledků může sloužit jako základ pro jakoukoli videokonverzaci v rámci transformačních cest s podnikem. Tento článek se zaměřuje na běžné obchodní opatření: výkon.

V dnešní technologické společnosti zákazníci předpokládají, že aplikace budou dobře fungovat a budou vždy k dispozici. V případě, že tato očekávání není splněna, způsobí poškození reputace, které může být nákladné a dlouhodobě trvalé.

## <a name="performance"></a>Výkon

Největší služby cloud computingu běží v celosvětové síti zabezpečených datových center, které jsou pravidelně upgradované na nejmodernější generaci rychlého a efektivního výpočetního hardwaru. To poskytuje několik výhod v rámci jednoho podnikového datového centra, například sníženou latenci sítě pro aplikace a větší úspory rozsahu.

Vyměňte svou firmu a snižte náklady pomocí energeticky hospodárné infrastruktury, která zahrnuje více než 100 vysoce zabezpečených zařízení po celém světě, které jsou propojeny jednou z největších sítí na zemi. Azure má víc globálních oblastí než jakýkoli jiný poskytovatel cloudu. To se týká škálování, které je potřeba k tomu, aby se aplikace blížily uživatelům po celém světě, zachovaly zachovávání dat a poskytovaly zákazníkům komplexní možnosti dodržování předpisů a odolnosti proti chybám.

- **Příklad 1:** Společnost služby pracovala s poskytovatelem hostingu, který hostuje více prostředků Provozní infrastruktury. Tyto systémy utrpěly časté výpadky a nízký výkon. Společnost migrovali své prostředky do Azure a využila tak výhody řízení a výkonu v cloudu. Prostoje, o kterou utrpělo, je přibližně 15 000 USD za minutu výpadku. Díky čtyř až osmi hodinám výpadku za měsíc se tato organizační transformace dá snadno zarovnat do kategorie.

- **Příklad 2:** Zákaznická investiční společnost byla v počátečních fázích úsilí o inovaci aplikací s podporou cloudu. Agilní procesy a DevOps byly dostatečně ve splatnosti, ale výkon aplikace byl nárazové. V rámci vyspělé transformace společnost zahájila program pro monitorování a automatizaci velikosti podle požadavků na použití. Společnost byla schopna eliminovat problémy s velikostí pomocí nástrojů pro správu výkonu Azure, což vede k nárůstu počtu transakcí v překvapivé 5 procent.

## <a name="reliability"></a>Spolehlivost

Cloud Computing umožňuje zálohování dat, zotavení po havárii a kontinuitu podnikových aplikací, protože data se můžou zrcadlit na několika redundantních webech v síti poskytovatele cloudu.

Jednou z těchto důležitých funkcí je zajistit, aby firemní data nebyla nikdy ztracena a aplikace zůstaly dostupné i přes havárie serveru, výpadky napájení nebo přírodní katastrofy. Vaše data můžete chránit a obnovovat tak, že je zálohujete do Azure.

Azure Backup je jednoduché řešení, které snižuje náklady na infrastrukturu a zároveň poskytuje vylepšené mechanismy zabezpečení pro ochranu vašich dat před ransomwarem. V jednom řešení můžete chránit úlohy spuštěné v Azure i v místním prostředí napříč systémy Linux, Windows, VMware a Hyper-V. Udržováním aplikací spuštěných v Azure můžete zajistit kontinuitu podnikových prostředí.

Azure Site Recovery usnadňuje testování zotavení po havárii replikací aplikací mezi oblastmi Azure. Můžete také replikovat místní virtuální počítače VMware a Hyper-V a fyzické servery do Azure, aby byly dostupné, pokud dojde k výpadku primární lokality. A v případě opětovného spuštění můžete úlohy obnovit do primární lokality.

- **Příklad:** Olejová a plynová společnost používala technologie Azure k implementaci úplného Site Recovery. Společnost se rozhodla plně využívat Cloud pro každodenní operace, ale funkce pro zotavení po havárii a kontinuitu provozu (DRBC) cloudu ještě chrání svoje datacentrum. Protože hurikán vytvořil stovky mil, jejich partnerský partner zahájil obnovování lokality do Azure. Předtím, než se doplní, všechny klíčové prostředky byly v Azure spuštěné a zabraňují případným výpadkům.

## <a name="next-steps"></a>Další kroky

Naučte se [používat šablonu výsledek podnikání](./business-outcome-template.md).

> [!div class="nextstepaction"]
> [Použití šablony výsledek podniku](./business-outcome-template.md)
