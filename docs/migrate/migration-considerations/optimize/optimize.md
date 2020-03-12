---
title: Srovnávací testování a změna velikosti cloudových prostředků
description: Naučte se, jak srovnávací testy a optimalizovat cloudové prostředky, abyste mohli najít rovnováhu mezi výkonem a náklady.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b0b49d2785de8cee4c08395f6a2893436fd0aa9e
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092785"
---
# <a name="benchmark-and-resize-cloud-assets"></a>Srovnávací testování a změna velikosti cloudových prostředků

Monitorování využití a nákladů je pro cloudové infrastruktury kriticky důležité. Organizace platí za prostředky, které v průběhu času spotřebovávají. Když využití překročí prahové hodnoty uvedené ve smlouvě, rychle se můžou začít kumulovat neočekávané poplatky za nadlimitní využití. Sestavy služby Cost Management monitorují výdaje za účelem analýzy a sledování využití cloudu, nákladů a trendů. Pomocí sestav v průběhu času můžete detekovat anomálie, které se odchylují od normálních trendů. Nedostatky cloudového nasazení se zobrazí v sestavách optimalizace. Všimněte si nedostatků v sestavách analýzy nákladů.

V tradičních místních modelech IT je získání systémů IT drahé a časově náročné. Procesy často vyžadují zdlouhavé cykly kontroly dlouhodobých výdajů a můžou dokonce vyžadovat proces ročního plánování. V takovém případě je běžné koupit víc, než je potřeba. Stejně tak je běžné, že správci IT zřídí víc prostředků v očekávání odhadovaných budoucích požadavků.

V cloudu účetní a zřizovací modely eliminují časová zpoždění, která vedou k nadměrným nákupům. Když aktivum potřebuje další prostředky, dá se vertikálně nebo horizontálně navýšit kapacitu téměř okamžitě. To znamená, že aktiva se můžou bezpečně snížit, aby se minimalizovala velikost spotřebovaných prostředků a nákladů. Během srovnávacích testů a optimalizace hledá tým přechodu na cloud rovnováhu mezi výkonem a náklady, takže zřizovaná aktiva nebudou větší a ani menší, než je nutné pro splnění produkčních požadavků.

<!-- markdownlint-disable MD026 -->

## <a name="should-assets-be-optimized-during-or-after-the-migration"></a>Měly by být aktiva optimalizovaná během migrace, nebo po ní?

Kdy by měla být aktiva optimalizovaná – během migrace, nebo po ní? Jednoduchá odpověď je *v obou případech*. Ale to není úplně přesné. Pro vysvětlení se podívejte na dva základní scénáře optimalizace velikosti prostředků:

- **Plánovaná změna velikosti.** V průběhu nasazování je často aktivum příliš velké a nedostatečně využité a měla by se změnit jeho velikost. Určení, jestli se v takovém případě velikost aktiva úspěšně změnila, vyžaduje uživatelské akceptační testování po migraci. Pokud v průběhu testování zkušení uživatelé neobjeví ztráty výkonu nebo funkčnosti, můžete z toho vyvodit, že velikost aktiva je nastavená úspěšně.
- **Optimalizace.** V případech, kdy je nutnost optimalizace nejasná, by IT týmy měly k řízení velikosti prostředků používat přístup řízený daty. Pomocí srovnávacích testů výkonu prostředků může IT tým dělat kvalifikovaná rozhodnutí týkající se nejvhodnější velikosti, služeb, škálování a architektury řešení. Můžou pak měnit velikost a testovat výkon jednotlivých teorií po migraci.

Během migrace používejte kvalifikované odhady a s určením velikosti experimentujte. Opravdová optimalizace prostředků ale vyžaduje data na základě skutečného výkonu v cloudovém prostředí. Aby mohlo dojít k opravdové optimalizaci, musí nejdřív IT tým implementovat přístupy k monitorování výkonu a využití prostředků.

## <a name="benchmark-and-optimize-with-azure-cost-management"></a>Srovnávací testování a optimalizace pomocí služby Azure Cost Management

Služba [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview), kterou licencuje Cloudyn, pobočka Microsoftu, spravuje útratu v cloudu s transparentností a přesností. Tato služba sleduje, přiděluje a optimalizuje náklady na cloud a provádí srovnávací testy.

Historická data můžou pomoct spravovat náklady díky analýze využití a nákladů v čase, aby se identifikovaly trendy, které se pak používají k předpovědi budoucích nákladů. Cost Management obsahuje také užitečné sestavy odhadovaných nákladů. Přidělování nákladů spravuje náklady díky analýze nákladů na základě zásad označování. Přidělování nákladů můžete použít také pro metody showback a chargeback. Můžete tak zobrazit využití prostředků a související náklady a ovlivnit chování spotřeby nebo spotřebu účtovat zákazníkům tenanta. Řízení přístupu pomáhá snižovat náklady tím, že zajišťuje, aby uživatelé a týmy měly přístup pouze k datům služby Cost Management, která potřebují. Upozorňování pomáhá snižovat náklady pomocí automatických upozornění na neobvyklé nebo nadměrné výdaje. Upozornění můžou také automaticky informovat ostatní účastníky na anomálie ve výdajích a rizika nadměrných výdajů. Různé sestavy podporují upozornění na základě rozpočtu a prahových hodnot nákladů.

## <a name="improve-efficiency"></a>Zlepšení efektivity

Pomocí služby Cost Management můžete určit optimální využití virtuálních počítačů, identifikovat nečinné virtuální počítače nebo odebrat nečinné virtuální počítače a nepřipojené disky. Pomocí informací v sestavách optimalizace velikosti a neefektivity můžete vytvořit plán pro zmenšení nebo odebrání nečinných virtuálních počítačů.

## <a name="next-steps"></a>Další kroky

Po otestování a optimalizaci úlohy je čas na [přípravu úlohy na povýšení](./ready.md).

> [!div class="nextstepaction"]
> [Získání migrované úlohy připravené na povýšení do produkčního prostředí](./ready.md)
