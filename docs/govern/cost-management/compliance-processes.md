---
title: Cost Management procesy dodržování zásad
description: Rozhraní pro přijetí cloudu pro Azure použijte k získání přístupu k vytváření procesů, které podporují pravidla zásad správného řízení Cost Management.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 290f2fb23b4c79f97c6009505493c1c59ac17355
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708848"
---
# <a name="cost-management-policy-compliance-processes"></a>Cost Management procesy dodržování zásad

Tento článek popisuje přístup k vytváření procesů, které podporují pravidla zásad správného řízení [cost management](./index.md) . Efektivní řízení nákladů na Cloud začíná s opakovanými ručními procesy, které jsou navržené tak, aby podporovaly dodržování zásad. To vyžaduje pravidelné zapojení týmu zásad správného řízení cloudu a zúčastněných obchodních zúčastněných stran ke kontrole a aktualizaci zásad a zajištění dodržování zásad. Mnoho probíhajících procesů monitorování a vynucení je navíc možné automatizovat nebo doplňovat pomocí nástrojů, aby se snížila režie řízení a byla umožněna rychlejší reakce na odchylku zásad.

## <a name="planning-review-and-reporting-processes"></a>Plánování, kontrola a vytváření sestav procesů

Nejlepší Cost Management nástroje v cloudu jsou stejně vhodné jako procesy a zásady, které podporují. Následuje sada ukázkových procesů, které se běžně účastní Cost Management disciplíny. Tyto příklady použijte jako výchozí bod při plánování procesů, které vám umožní pokračovat v aktualizaci nákladových zásad na základě změny firmy a zpětné vazby z obchodních týmů, na které se vztahují doprovodné materiály pro řízení nákladů.

**Prvotní posouzení rizik a plánování:** V rámci prvotního přijetí Cost Management disciplíny Identifikujte základní obchodní rizika a tolerance související s náklady na Cloud. Tyto informace slouží k projednání rizik spojených s rozpočtem a náklady se členy vašich obchodních týmů a vyvine základní sadu zásad pro zmírnění těchto rizik za účelem vytvoření počáteční strategie zásad správného řízení.

**Plánování nasazení:** Před nasazením jakékoli assetu vytvořte prognózu rozpočtu založenou na očekávaném přidělení cloudu. Ujistěte se, že jsou informace o vlastnictví a monitorování účtů pro nasazení dokumentovány.

**Roční plánování:** Na roční bázi proveďte souhrnnou analýzu všech nasazených a nasazených prostředků. Přizpůsobte si rozpočty podle obchodních jednotek, oddělení, týmů a dalších příslušných divizí a umožněte samoobslužné přijetí. Ujistěte se, že vedoucí každé fakturační jednotky ví o rozpočtu a jak sledovat útraty.

Je to čas udělat si předplacený nebo předprodejní, aby se maximalizovala sleva. Je vhodné sjednotit roční rozpočtování s fiskálním rokem dodavatele cloudu a zajistit tak větší náklady na možnosti slevy na rok-konec.

**Čtvrtletní plánování:** Na čtvrtletním základě si Projděte rozpočty s každým vedoucím fakturační jednotky a zarovnejte prognózu a skutečnou útratu. Pokud existují změny v plánu nebo neočekávané vzory útraty, zarovnejte a znovu Přidělte rozpočet.

Tento čtvrtletní proces plánování je vhodný čas k vyhodnocení aktuálního členství týmu zásad správného řízení pro vaše znalosti v souvislosti s aktuálním nebo budoucím obchodním plánem. Přizvat příslušné vlastníky zaměstnanců a úloh k účasti na recenzích a plánování jako buď dočasné poradce nebo trvalé členy týmu.

**Vzdělávání a školení:** Na bimonthly jsou nabízené cvičení, které zajistí, aby byly firmy a zaměstnanci IT aktuální na základě nejnovějších požadavků zásad Cost Management. V rámci tohoto procesu zkontrolujte a aktualizujte veškerou dokumentaci, pokyny nebo další školicí materiály, abyste měli jistotu, že jsou synchronizované s nejnovějšími příkazy firemních zásad.

**Měsíční generování sestav:** Každý měsíc vystavte skutečnou útratu na základě předpovědi. Upozorněte vedoucí k fakturaci na případné neočekávané odchylky.

Tyto základní procesy vám pomůžou sjednotit útratu a vytvořit základ pro Cost Management disciplíny.

## <a name="processes-for-ongoing-monitoring"></a>Procesy pro průběžné monitorování

Úspěšná Cost Management strategie zásad správného řízení závisí na viditelnosti minulých, aktuálních a plánovaných budoucích výdajů souvisejících s cloudem. Bez možnosti analyzovat relevantní metriky a data o vašich stávajících nákladech nemůžete identifikovat změny vašich rizik nebo zjistit porušení rizik. Probíhající procesy zásad správného řízení popsané výše vyžadují kvalitní data, aby bylo zajištěno, že zásady je možné upravit tak, aby lépe chránily vaši infrastrukturu před měnícími se požadavky na podnik a Cloud

Ujistěte se, že vaše týmy IT implementovaly automatizované systémy pro monitorování útraty a využití cloudu pro neplánované odchylky od očekávaných nákladů. Navažte systémy vytváření sestav a upozorňování, abyste zjistili, jak vyzvat k detekci a zmírnění potenciálních porušení zásad.

## <a name="compliance-violation-triggers-and-enforcement-actions"></a>Aktivační události porušení předpisů a akce vynucení

Po zjištění narušení byste měli provést akce vynucení, aby se zásady znovu zarovnaly. Pomocí nástrojů popsaných v [cost management sada nástrojů pro Azure](./toolchain.md)můžete automatizovat aktivační události narušení.

Následují příklady aktivačních událostí:

- **Měsíční odchylky rozpočtu:** Prodiskutujte všechny odchylky v měsíčních útratách, které překračují 20% předpovědi – oproti skutečnému poměru k vedoucímu fakturační jednotky. Zaznamenejte řešení a změny v prognóze.
- **Tempo přijetí:** Jakákoli odchylka na úrovni předplatného vyšší než 20% spustí kontrolu s vedoucím fakturační jednotky. Zaznamenejte řešení a změny v prognóze.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md)můžete zdokumentovat procesy a triggery, které se rovnají aktuálnímu plánu přijetí do cloudu.

Pokyny k provádění zásad správy cloudu ve srovnání s plány přijetí najdete v článku věnovaném Cost Management zlepšování oborů.

> [!div class="nextstepaction"]
> [Vylepšení oboru Cost Management](./discipline-improvement.md)
