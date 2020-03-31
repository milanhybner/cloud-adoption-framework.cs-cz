---
title: Sestavování organizace s důrazem na náklady
description: Rozhraní pro přijetí v cloudu pro Azure použijte k získání osvědčených postupů pro sestavování organizace s důrazem na náklady.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.openlocfilehash: 714bd0d26a38a1ee3a3cb2bfc2d336d1ffd4f45c
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80428507"
---
# <a name="build-a-cost-conscious-organization"></a>Sestavení organizace s důrazem na náklady

Jak je znázorněno v [motivaci: Proč se chystáme přesunout do cloudu?](../strategy/motivations.md), existuje mnoho zvukových důvodů, které společnost potřebuje ke schválení cloudu. Když je snížení nákladů primárním ovladačem, je důležité vytvořit organizaci s důrazem na náklady.

Zajištění nákladů na vědomí není jednorázová aktivita. Stejně jako ostatní témata týkající se přijímání do cloudu je iterativní. Následující diagram popisuje tento proces a zaměřuje se na tři vzájemně závislé aktivity: *viditelnost*, *zodpovědnost*a *optimalizace*. Tyto procesy hrají na makro a mikroúrovně, které podrobně popisujeme v tomto článku.

![proces s vědomím nákladů](../_images/ready/cost-optimization-process.png)
*Obrázek 1 – osnova organizace s důrazem na náklady.*

## <a name="general-cost-conscious-processes"></a>Obecné procesy s důrazem na náklady

- **Viditelnost:** Aby organizace mohla být vědoma nákladů, je nutné, aby tyto náklady byly viditelné. Přehled v organizaci s vědomím nákladů vyžaduje konzistentní vytváření sestav pro týmy, které přijímají Cloud, finanční týmy, které spravují rozpočty a týmy pro správu, které jsou zodpovědné za náklady. Tato viditelnost se dá dosáhnout vytvořením:
  - Správný obor generování sestav.
  - Řádnou organizaci poskytující prostředky (skupiny pro správu, skupiny prostředků, předplatná).
  - Vymažte strategie označování.
  - Správné řízení přístupu (RBAC).

- **Zodpovědnost:** Zodpovědnost je důležité jako viditelnost. Zodpovědnost začíná jasnými rozpočty pro úsilí o přijetí. Rozpočty by měly být dobře zřízené, jasně sděleny a založené na reálných očekáváních. Zodpovědnost vyžaduje iterativní proces a růst místo, aby bylo možné řídit správnou úroveň zodpovědnosti.

- **Optimalizace:** Optimalizace je akce, která vytvoří snížení nákladů. Během optimalizace se upraví přidělení prostředků, aby se snížily náklady na podporu různých úloh. Tento proces vyžaduje iteraci a experimentování. Snížení nákladů snižuje výkon. Vyhledání správného zůstatku mezi náklady řízení nákladů a výkonem koncového uživatele vyžaduje vstup od více stran.

Následující části popisují role, které tým *cloudové strategie*, *tým přijetí do cloudu,* *tým zásad správného řízení*cloudu a *cloudová centra excelence* (CCoE) hrají v vývoji organizace s důrazem na náklady.

## <a name="cloud-strategy-team"></a>Tým strategie cloudu

Úsilí při sestavování nákladů na nasazení v cloudu začíná na úrovni vedoucího. Aby bylo možné dlouhodobě platit, [tým cloudové strategie](./cloud-strategy.md) by měl zahrnovat člena finančního týmu. Pokud finanční struktura obsahuje obchodní manažery, které jsou k dispozici pro náklady na řešení, měli byste je pozvat i k tomu, aby se připojili k týmu. Kromě základních aktivit, které se obvykle přiřazují týmu cloudové strategie, by měli mít všichni členové týmu cloudové strategie také zodpovědnost za:

- **Viditelnost:** Tým strategie cloudu a [tým zásad správného řízení pro Cloud](./cloud-governance.md) potřebují znát skutečné náklady na úsilí při přijetí cloudu. V rámci tohoto týmu by měl mít přístup k více oborům nákladů za účelem analýzy rozhodnutí o útratě. Pracovník obvykle potřebuje přehled o celkových nákladech v rámci všech cloudových výdajů. Ale jako aktivní členové týmu cloudové strategie by měli mít také schopnost zobrazit náklady na obchodní jednotku nebo za fakturační jednotku a ověřit showback, vrácení peněz nebo jiné [modely cloudového účetnictví](../strategy/cloud-accounting.md).

- **Zodpovědnost:** Rozpočty by měly být navázány mezi cloudovou strategií, zásadami [správného řízení cloudu](./cloud-governance.md)a týmy pro [přijetí cloudu](./cloud-adoption.md) na základě očekávaných aktivit přijetí. Pokud dojde ke odchylka od rozpočtu, tým cloudové strategie a tým zásad správného řízení cloudu musí být partnerem, aby rychle určili, co je nejlepší postup k nápravě odchylek.

- **Optimalizace:** Během optimalizace může tým cloudové strategie představovat investici a vrátit hodnotu konkrétních úloh. Pokud má úloha strategickou hodnotu nebo finanční dopad na firmu, je potřeba monitorovat úsilí v rámci optimalizace nákladů pečlivě. Pokud se nejedná o strategický dopad na organizaci a žádné podstatné náklady na špatný výkon úlohy, tým cloudové strategie může schválit optimalizaci. Aby bylo možné řídit tato rozhodnutí, tým musí být schopný zobrazit náklady na rozsah jednotlivých projektů.

## <a name="cloud-adoption-team"></a>Tým přijetí cloudu

[Tým přijetí cloudu](./cloud-adoption.md) je v centru všech aktivit přijetí. Takže se jedná o první linii obrany proti přepočítání. Tento tým má aktivní roli ve všech třech fázích pro náklady – vědomí.

- **Viditelnost**

  - **Povědomí:** Tým pro rozhodování o cloudu musí mít přehled o tom, jaké jsou cíle úsilí na úsporu nákladů. Jednoduše se dozvíte, že úsilí o přijetí cloudu pomůže snížit náklady je receptem na selhání. *Specifická* viditelnost je důležitá. Pokud je cílem například snížit náklady na vlastnictví datacentra o 3% nebo roční provozní náklady o 7%, tyto cíle uzavřete do začátku a zřetelně.
  - **Telemetrie:** Tento tým musí mít přehled o dopadu jejich rozhodnutí. Během migrace nebo inovačních aktivit mají jejich rozhodnutí přímý vliv na náklady a výkon. Tým musí vyrovnávat tyto dva konkurenční faktory. Sledování výkonu a monitorování nákladů, které je vymezeno na aktivní projekty týmu, je důležité pro zajištění potřebné viditelnosti.

- **Zodpovědnost:** Tým pro přijetí v cloudu musí vědět o všech přednastavených rozpočtech, které jsou spojené s jejich úsilím o přijetí. Pokud se skutečné náklady nerovnají s rozpočtem, je k dispozici příležitost vytvořit zodpovědnost. Zodpovědnost není rovna postihu týmu přijetí za překročení rozpočtu, protože překročení rozpočtu může vést k potřebným rozhodnutím o výkonu. Místo toho zodpovědnost znamená, že tým bude informovat o cílech a o tom, jak jejich rozhodnutí mají na tyto cíle vliv. Kromě toho odpovědnost zahrnuje poskytnutí dialogu, ve kterém tým může sdělit rozhodnutí, která vedla k přenesení. Pokud jsou tato rozhodnutí chybně zarovnaná s cíli projektu, toto úsilí poskytuje dobrou příležitost pro partnerství s týmem cloudových strategií, aby bylo možné lépe rozhodovat.

- **Optimalizace:** Toto úsilí je vyvážením, protože optimalizace prostředků může snížit výkon zátěží, které podporují. Pro úlohu se někdy předpokládá předpokládaná nebo Rozpočtovaná úspora, protože zatížení nedostatečně neprovádí s rozpočtovými prostředky. V těchto případech musí tým pro přijetí v cloudu učinit rozhodnutí a nahlásit změny týmu cloudové strategie a týmu zásad správného řízení, aby bylo možné opravit rozpočty nebo rozhodnutí o optimalizaci.

## <a name="cloud-governance-team"></a>Tým zásad správného řízení cloudu

Obecně platí, že [tým zásad správného řízení cloudu](./cloud-governance.md) zodpovídá za správu nákladů napříč celým úsilím při přijetí cloudu. Jak je uvedeno v tématu [pravidla správy nákladů](../govern/cost-management/index.md) v metodologii zásad správného řízení v rozhraní pro přijetí do cloudu, je řízení nákladů prvním z pěti oborů zásad správného řízení cloudu. Tyto články popisují řadu hlubších zodpovědností za tým zásad správného řízení cloudu.

Toto úsilí se zaměřuje na následující činnosti, které souvisejí s vývojem organizace s důrazem na náklady:

- **Viditelnost:** Tým zásad správného řízení cloudu funguje jako partner týmu cloudové strategie, který umožňuje plánovat rozpočty pro přijetí v cloudu. Tyto dva týmy také spolupracují na pravidelné kontrole skutečných výdajů. Tým zásad správného řízení cloudu zodpovídá za zajištění konzistentních, spolehlivých sestav nákladů a telemetrie výkonu.

- **Zodpovědnost:** V případě, že dojde ke odchylosti rozpočtu, tým cloudové strategie a tým zásad správného řízení cloudu musí být partnerem, aby rychle určili, co nejlepší opatření k nápravě odchylek využijete. Obecně platí, že tým zásad správného řízení cloudu bude působit na tato rozhodnutí. V některých případech se může jednat o jednoduché přeškolení pro [tým ovlivněného cloudu](./cloud-adoption.md). Tým zásad správného řízení cloudu může také pomáhat s optimalizací nasazených assetů, měnit možnosti zlevněných nebo dokonce implementovat automatizované možnosti řízení nákladů, jako je blokování nasazení neplánovaných assetů.

- **Optimalizace:** Po migraci prostředků do cloudu nebo jejich vytvoření můžete využívat monitorovací nástroje k vyhodnocení výkonu a využití těchto prostředků. Správná data monitorování a výkonu mohou identifikovat prostředky, které by měly být optimalizované. Tým zásad správného řízení cloudu zodpovídá za zajištění důsledného nasazení nástrojů monitorování a nákladového vykazování. Můžou také pomáhat týmům pro přijímání, které identifikují příležitosti pro optimalizaci na základě telemetrie výkonu a nákladů.

## <a name="cloud-center-of-excellence"></a>Vedoucí centrum cloudu

I když není typicky zodpovědná za správu nákladů, CCoE může mít významný dopad na organizace s důrazem na náklady. Mnoho základních rozhodnutí v oddělení IT má vliv na náklady ve velkém měřítku. Když CCoE svůj díl, můžou se snížit náklady na více úsilí o přijetí v rámci cloudu.

- **Viditelnost:** K CCoE týmu by měla být viditelná jakákoli skupina pro správu nebo skupina prostředků, která zahrnuje základní prostředky IT. Tým může tato data využít k tomu, aby se k optimalizaci používaly příležitosti pro farmu.

- **Zodpovědnost:** I když se obvykle nevztahují na náklady, může CCoE obsahovat vlastní účet pro vytváření opakovaných řešení, která minimalizují náklady a maximalizují výkon.

- **Optimalizace:** Vzhledem k tomu, že je CCoE k dispozici pro více nasazení, tým je ideálním umístěním pro návrhy tipů pro optimalizaci a pomáhat při přijímání týmů k lepšímu vyladění prostředků.

## <a name="next-steps"></a>Další kroky

Plnění těchto odpovědností na každé úrovni podniku pomáhá zajistit cenovou organizaci. Pokud chcete začít pracovat na těchto pokynech, přečtěte si [Úvod k organizaci připravenosti organizace](./index.md) , které vám pomůžou identifikovat správné týmové struktury.

> [!div class="nextstepaction"]
> [Identifikujte správné struktury týmu](./index.md)
