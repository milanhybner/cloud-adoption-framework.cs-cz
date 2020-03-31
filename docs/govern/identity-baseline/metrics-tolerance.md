---
title: Metriky a indikátory tolerance tolerance standardních hodnot identity
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak kvantifikovat toleranci obchodního rizika související s směrným plánem identity.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5af612501dd2fb8bb73ada0e9dfcd4f3ee784e35
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433532"
---
# <a name="identity-baseline-metrics-indicators-and-risk-tolerance"></a>Metriky, ukazatele a tolerance standardních hodnot identity

Tento článek vám pomůže kvantifikovat toleranci obchodního rizika v souvislosti s směrným plánem identity. Definování metrik a indikátorů vám pomůže vytvořit obchodní případ pro investici do splatnosti oboru standardních hodnot identity.

## <a name="metrics"></a>Metriky

Směrný plán identity se zaměřuje na identifikaci, ověřování a autorizaci jednotlivců, skupin uživatelů nebo automatizovaných procesů a poskytování vhodného přístupu k prostředkům v nasazeních v cloudu. V rámci analýzy rizik budete chtít shromažďovat data související s vašimi službami identity a zjistit, kolik rizika čelíte, a jak důležité investice do zásad správného řízení identity jsou pro vaše plánovaná cloudová nasazení.

Následují příklady užitečných metrik, které byste měli shromáždit, abyste mohli vyhodnotit toleranci rizik v rámci směrného plánu identity:

- **Velikost systémů identit.** Celkový počet uživatelů, skupin nebo jiných objektů spravovaných prostřednictvím vašich systémů identit.
- **Celková velikost infrastruktury adresářových služeb.** Počet adresářových struktur, domén a klientů používaných vaší organizací.
- **Závislost na starších nebo místních mechanismech ověřování.** Počet úloh, které závisí na starších verzích nebo mechanismech třetích stran nebo ověřování Multi-Factor Authentication.
- **Rozsah adresářových služeb nasazených v cloudu.** Počet doménových struktur adresářů, domén a klientů, které jste nasadili do cloudu.
- **Servery služby Active Directory nasazené v cloudu.** Počet serverů služby Active Directory nasazených do cloudu.
- **Organizační jednotky nasazené v cloudu** Počet organizačních jednotek (OU) služby Active Directory nasazených do cloudu.
- **Rozsah federace** Počet systémů pro základní identitu, které jsou federované pro systémy vaší organizace.
- **Uživatelé se zvýšenými oprávněními.** Počet uživatelských účtů s vyšším přístupem k prostředkům nebo nástrojům pro správu.
- **Použití řízení přístupu na základě role.** Počet předplatných, skupin prostředků nebo individuálních prostředků, které nejsou spravovány prostřednictvím řízení přístupu na základě role (RBAC) prostřednictvím skupin.
- **Deklarace identity ověřování.** Počet úspěšných a neúspěšných pokusů o ověření uživatele
- **Deklarace identity autorizace.** Počet úspěšných a neúspěšných pokusů uživatelů o přístup k prostředkům.
- **Ohrožené účty.** Počet uživatelských účtů, které byly ohroženy.

## <a name="risk-tolerance-indicators"></a>Indikátory tolerance rizik

Rizika související s plánem identity jsou z velké části spojená se složitou infrastrukturou identity vaší organizace. Pokud jsou všichni uživatelé a skupiny spravováni pomocí jednoho adresáře nebo cloudového nativního poskytovatele identity s minimální integrací s jinými službami, vaše úroveň rizika bude pravděpodobně malá. Vzhledem k tím, že vaše firemní potřeby rozšiřují vaše základní systémy vaší identity, může být potřeba podporovat složitější scénáře, jako je třeba více adresářů pro podporu vaší interní organizace nebo federace s externími zprostředkovateli identity. Jelikož se tyto systémy stanou složitější, zvyšuje se riziko.

V počátečních fázích přijetí cloudu Spolupracujte se svým týmem zabezpečení IT a podnikovými stranami a Identifikujte [obchodní rizika](./business-risks.md) související s identitou a pak určíte přijatelný základ pro toleranci identity. V této části architektury pro přijetí do cloudu najdete příklady, ale podrobná rizika a směrné plány vaší společnosti nebo nasazení se můžou lišit.

Jakmile budete mít základnu, stanovte minimální srovnávací testy představující nepřijatelný nárůst zjištěných rizik. Tyto srovnávací testy fungují jako triggery, pokud potřebujete provést akci při řešení těchto rizik. Následuje několik příkladů, jak se metriky související s identitou, jako jsou výše popsané výše, můžou zvýšit investice do oboru standardních hodnot identity.

- **Aktivační událost pro číslo uživatelského účtu.** Společnost s více než _x_ uživateli, skupinami nebo jinými objekty spravovanými v systémech identit by mohla těžit z investic do směrného plánu identity, aby bylo zajištěno efektivní řízení pro velký počet účtů.
- **Místní Trigger závislosti identity** Společnost plánuje migrovat úlohy do cloudu, který vyžaduje funkce starší verze ověřování nebo Multi-Factor Authentication třetích stran by měly investovat do oboru standardních hodnot identity, aby se snížila rizika související s refaktoringem nebo dalším cloudem. nasazení infrastruktury
- **Aktivační událost složitosti adresářových služeb.** Společnost, která udržuje více než _x_ číslo of_ jednotlivých doménových struktur, domén nebo tenantů adresářů, by měla investovat do směrného plánu identity a snižovat tak rizika související se správou účtů a problémy s efektivitou související s více uživatelskými přihlašovacími údaji, které jsou v různých systémech rozdělené.
- **Aktivační událost hostovaných adresářových služeb v cloudu** Společnost hostující virtuální počítače _, které jsou_ hostovány v cloudu a které mají na těchto cloudových serverech spravovány _x organizační_ jednotky (OU), můžou těžit z investic do směrného plánu identity, aby optimalizoval integraci s místními nebo jinými externími službami identity.
- **Aktivační událost federace** Společnost implementující federaci identit se standardními systémy standardních identit _x_ (identity) může těžit z investice do směrného plánu identity, aby bylo zajištěno konzistentní zásady organizace napříč členy federace.
- **Aktivační událost zvýšeného přístupu.** Společnost s více než _x%_ uživatelů se zvýšenými oprávněními k nástrojům pro správu a prostředkům by měla zvážit investování do směrného plánu identity, aby se minimalizovalo riziko neúmyslného nadměrného přestavení přístupu uživatelům.
- **Aktivační událost RBAC** Společnost s v rámci _x%_ prostředků, které používají metody řízení přístupu na základě rolí, by měla zvážit investování do směrného plánu identity, aby identifikovala optimalizované způsoby přiřazování přístupu uživatelů k prostředkům.
- **Aktivační událost při selhání ověřování.** Společnost, kde selhání ověřování reprezentuje více než _x%_ pokusů, by měla investovat do směrného plánu identity, aby se zajistilo, že metody ověřování nejsou v rámci externích útoků a že uživatelé se mohou správně ověřit.
- **Aktivační událost při selhání autorizace** Společnost, kde jsou pokusy o přístup odmítnuty více než _x%_ času, by měly investovat do směrného plánu identity, aby se zlepšila aplikace a aktualizovala řízení přístupu a identifikovala potenciálně škodlivé pokusy o přístup.
- **Došlo k ohrožení zabezpečení triggeru účtu.** Společnost s více než 1 ohroženým účtem by měla investovat do směrného plánu identity, aby vylepšila sílu a zabezpečení ověřovacích mechanismů a vylepšila mechanismy, aby opravila rizika související s ohroženými účty.

Přesné metriky a triggery, které používáte k měření tolerance rizika a úroveň investic do směrného plánu identity, budou specifické pro vaši organizaci, ale výše uvedené příklady by měly sloužit jako užitečnou základnu pro diskuzi v rámci týmu zásad správného řízení v cloudu.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md), metriky dokumentů a indikátory tolerance, které odpovídají aktuálnímu plánu přijetí do cloudu.

Projděte si vzorové zásady pro základní identitu jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

> [!div class="nextstepaction"]
> [Kontrola ukázkových zásad](./policy-statements.md)
