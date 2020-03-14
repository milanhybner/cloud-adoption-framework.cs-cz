---
title: Příprava migrované aplikace pro produkční prostředí
description: Rozhraní pro přijetí v cloudu pro Azure použijte k pochopení ověření, které je součástí přípravy migrované aplikace na produkční povýšení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4b48a4ceea5d322e4a993cdba474269d73fbc7e3
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312012"
---
# <a name="prepare-a-migrated-application-for-production-promotion"></a>Příprava migrované aplikace pro produkční prostředí

Jakmile zvýšíte úroveň sady funkcí, provoz generovaný jejími uživateli směřuje do migrovaných prostředků. Sadu funkcí můžete tomuto provozu uzpůsobit ve fázi posouzení připravenosti. Níže najdete několik obchodních a technologických informací, které vám pomůžou s posouzením připravenosti.

## <a name="validate-the-business-change-plan"></a>Ověření plánu obchodních změn

Transformace probíhá ve chvíli, kdy firemní uživatelé nebo zákazníci využívají technické řešení, které zjednodušuje procesy, díky kterým se zvyšuje obchodní úspěch organizace. Fáze posouzení připravenosti představuje vhodnou příležitost pro ověření [plánu obchodních změn](./business-change-plan.md) a zajištění důkladného školení obchodních a technických týmů, kterých se změnách budou podílet. Je potřeba splnit především následující body související s technologickou stránkou plánu změn:

- Je nutné dokončit (nebo alespoň naplánovat) školení koncových uživatelů.
- Uživatelé musí mít informace o všech schválených výpadcích.
- Musí proběhnout synchronizace produkčních dat a jejich následné ověření ze strany koncových uživatelů.
- Ověřte správnost načasování zvýšení úrovně aplikace a nasazení nových technologií a zajistěte, aby koncoví uživatelé měli informace o časovém rozvrhu a změnách.

## <a name="final-technical-readiness-tests"></a>Závěrečné testy pro posouzení technické připravenosti

*Posouzení připravenosti* je poslední krok před uvolněním prostředků pro produkčního prostředí. To znamená, že představuje poslední šanci pro testování dané sady funkcí. V průběhu této fáze se doporučuje provést následující testy:

- **Test izolace sítě:** Otestujte a monitorujte síťový provoz, abyste zajistili potřebnou izolaci a nedošlo k neočekávanému narušení sítě. Také zajistěte, že veškeré směrování sítě se po dobu přímé migrace přeruší, aby nedošlo k neočekávanému provozu.
- **Testování závislostí:** Zkontrolujte, jestli proběhla migrace všech závislostí aplikace a jestli jsou tyto závislosti v migrovaném prostředku dostupné.
- **Testování provozní kontinuity a zotavení po havárii (BCDR):** Zkontrolujte, jestli existují smlouvy SLA pro zálohování a zotavení po havárii. Pokud je to možné, proveďte úplné obnovení prostředků z řešení BCDR.
- **Testování spojení s koncovými uživateli:** Zkontrolujte vzory a směrování provozu od koncových uživatelů. Zajistěte, aby síťový výkon odpovídal očekáváním.
- **Závěrečná kontrola výkonu:** Zajistěte dokončení testování výkonnosti a ověřte, jestli jsou koncoví uživatelé s výkonem spokojení. Proveďte všechny automatické testy výkonnosti.

## <a name="final-business-validation"></a>Závěrečné obchodní ověření

Jakmile zkontrolujete plán obchodních změn a posoudíte připravenost prostředí, pomocí následujících kroků můžete dokončit obchodní ověření:

- **Kontrola nákladů (plánovaných proti skutečným):** V důsledku testování se může změnit rozsah nasazení a architektura technologií. Zkontrolujte, jestli skutečná cena stále odpovídá původnímu plánu.
- **Komunikace a provedení plánu migrace:** Než proběhne migrace, informujte o ní všechny zúčastněné strany a následně proveďte potřebné kroky.

## <a name="next-steps"></a>Další kroky

Jakmile bude posouzení připravenosti hotové, je čas [povýšit úroveň sady funkcí](./promote.md).

> [!div class="nextstepaction"]
> [Co je potřeba k převedení migrovaného prostředku do produkčního prostředí?](./promote.md)
