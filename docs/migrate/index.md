---
title: Migrace do cloudu
description: Seznamte se s vytvářením iterativních procesů k posouzení, migraci, optimalizaci, zabezpečení a správě úloh, které chcete migrovat do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: c4ee7491fb5fbfa549dfe82c82e720f51188a25c
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312301"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Migrace do cloudu v architektuře přechodu na cloud

Všechny [plány přechodu na cloud](../plan/index.md) na podnikové úrovni budou obsahovat úlohy, které neospravedlňují významné investice při vytváření nové obchodní logiky. Tyto úlohy jde přesunout do cloudu pomocí celé řady přístupů: lift and shift, lift and optimize nebo modernizace. Za migraci se považují všechny tyto přístupy. Následující cvičení vám pomůžou vytvořit iterativní procesy k posouzení, migraci, optimalizaci, zabezpečení a správě těchto úloh.

## <a name="getting-started"></a>Začínáme

V rámci přípravy na tuto fázi životního cyklu přechodu na cloud architektura navrhuje následující cvičení:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Migrace vaší první úlohy</h3>
Využijte průvodce migrací do Azure a seznamte se s nativními nástroji Azure a s přístupem k migraci.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./expanded-scope/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Scénáře migrace</h3>
Využijte další migrační nástroje a přístupy k zajištění dalších scénářů migrace.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Osvědčené postupy</h3>
Použitím konzistentních osvědčených postupů vyřešte běžné požadavky migrace.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Vylepšení procesů</h3>
Migrace je aktivita úzce související s procesy. Při škálování úsilí o migraci využijte vylepšení těchto procesů k vyhodnocení a doladění různých aspektů migrace.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

Tato metodologie a výše uvedené kroky staví na následujících předpokladech:

- Před zahájením migrace byla identifikována a nakonfigurována nejméně jedna [cílová zóna](../ready/index.md), která byla nasazena tak, aby splňovala požadavky krátkodobého plánu přechodu na cloud.
- S migrací jsou spojené termíny jako _„lift and shift“_ nebo _změna hostitele_. Tato metodologie a výše uvedené kroky vycházejí z premisy, že žádné datové centrum (a jenom velmi málo úloh) by se nemělo migrovat čistě změnou hostitele. I když je možné u řady úloh změnit hostitele, zákazníci se častěji rozhodnou, že budou v rámci jednotlivých úloh modernizovat konkrétní prostředky. Během tohoto iterativního procesu je často předmětem diskuze zajištění rovnováhy mezi rychlostí a modernizací.

## <a name="iterative-migration-process"></a>Iterativní proces migrace

Ve své podstatě migrace do cloudu sestává ze čtyř jednoduchých fází: Posouzení, migrace, optimalizace a zabezpečení a správa. V této části architektury přechodu na cloud vás naučíme maximalizovat návratnost každé fáze procesu a dát tyto fáze do souladu s plánem přechodu na cloud. Tato fáze iterativního přístupu jsou znázorněné na následujícím obrázku:

![Model migrace architektury přechodu na cloud](../_images/migrate/methodology.png)

## <a name="create-a-balanced-cloud-portfolio"></a>Vytvoření vyrovnaného cloudového portfolia

Každé vyrovnané portfolio technologií obsahuje kombinaci prostředků v různých stavech. U některých aplikací se plánuje vyřazení z provozu a poskytuje se pro ně minimální podpora. Jiné aplikace nebo prostředky jsou podporované ve stavu údržby, ale funkce těchto řešení jsou stabilní. U novějších obchodních procesů změny podmínek na trhu pravděpodobně urychlí probíhající vylepšování nebo modernizaci funkcí. Když vzniknou nové příležitosti pro zajištění zdrojů příjmů, do prostředí se zavedou nové aplikace nebo prostředky. Vliv investic na příjmy a zisk se mění v každé fázi životního cyklu prostředku. Čím pozdější je fáze životního cyklu, tím menší je pravděpodobnost, že nová funkce nebo úsilí o modernizaci přinese výraznou návratnost investic.

Možností přechodu na cloud je hned několik, a s každou z nich je spojená podobná míra investic a jejich návratnosti. Vytvářením aplikací nativních pro cloud je možné dosáhnout výrazného snížení provozních nákladů. Po vydání aplikace nativní pro cloud je možné rychleji iterovat vývoj nových funkcí a řešení. Podobné výhody může přinést modernizace aplikací, a to díky odebrání starších omezení souvisejících s modely místního vývoje. Tyto dva modely jsou bohužel náročné na pracovní sílu a závisejí na velikosti, dovednostech a zkušenostech týmů softwarových vývojářů. Pracovní síla je často nevyvážená&mdash;lidé s potřebnými dovednostmi a talentem na modernizaci aplikací by raději vytvářeli nové aplikace. Na trhu s omezenou pracovní silou můžou rozsáhlé projekty modernizace trpět problémy souvisejícími se spokojeností a talentem zaměstnanců. Ve vyváženém portfoliu by tento přístup měl být vyhrazený pro aplikace, u kterých by došlo k výraznému vylepšení funkcí, kdyby zůstaly v místním prostředí.

## <a name="envision-an-end-state"></a>Vize koncového stavu

Efektivní cesta potřebuje cíl. Před provedením prvního kroku si udělejte hrubou představu požadovaného koncového stavu. Tato infografika popisuje výchozí bod, který se skládá ze stávajících aplikací, dat a infrastruktury a který definuje digitální aktiva. Během procesu migrace se jednotlivé prostředky převedou prostřednictvím jedné z možností na pravé straně.

## <a name="migration-implementation"></a>Implementace migrace

Tyto články popisují dvě cesty s podobným cílem &mdash; migrovat velkou část stávajících prostředků do Azure. Požadované procesy k realizaci však budou výrazně ovlivněné obchodními výsledky a aktuálním stavem. Tyto drobné odchylky mají za následek dva zcela rozdílné přístupy k dosažení podobného koncového stavu.

![Model migrace architektury přechodu na cloud](../_images/migrate/methodology.png)

Kvůli vedení inkrementálního spouštění během přechodu do koncového stavu tento model rozděluje migraci na dvě oblasti zájmu.

**Příprava migrace:** Vytvoření přibližného backlogu migrace založeného z velké části na aktuálním stavu a požadovaných výsledcích

- **Obchodní výsledky:** Klíčové obchodní cíle, které jsou podnětem k této migraci
- **Odhad digitálních aktiv:** Hrubý odhad počtu a stavu úloh, které se mají migrovat
- **Role a povinnosti:** Jasná definice struktury týmu, rozdělení povinností a požadavků na přístup
- **Požadavky na správu změn:** Tempo, procesy a dokumentace potřebné ke kontrole a schválení změn

Tyto počáteční vstupy formují backlog migrace. Výstupem backlogu migrace je podle priority seřazený seznam aplikací určených k migraci do cloudu. Tento seznam formuje provádění procesu migrace do cloudu. Postupem času se také bude rozšiřovat, aby zahrnoval většinu potřebné dokumentace ke správě změn.

**Proces migrace:** Všechny aktivity migrace do cloudu jsou součástí jednoho z následujících procesů, protože souvisí s backlogem migrace.

- **Posouzení:** Posouzení stávajícího prostředku a stanovení plánu jeho migrace
- **Migrace:** Replikace funkcí prostředku v cloudu
- **Optimalizace:** Vyvážení výkonu, nákladů, přístupu a provozní kapacity cloudového prostředku
- **Zabezpečení a správa:** Zajištění, aby byl cloudový prostředek připravený na probíhající operace

Informace shromážděné během vývoje backlogu migrace určují složitost a požadovanou úroveň úsilí v rámci procesu migrace do cloudu během jednotlivých iterací a pro každé vydání funkcí.

## <a name="transition-to-the-end-state"></a>Přechod do koncového stavu

Cílem je hladká a částečně automatizovaná migrace do cloudu. V procesu migrace se pomocí nástrojů od dodavatelů cloudu rychle replikují a připravují prostředky v cloudu. Po ověření stačí k přesměrování uživatelů na cloudové řešení jednoduchá změna sítě. Pro řadu případů použití je technologie potřebná k dosažení tohoto cíle široce dostupná. Existují ukázkové případy, které ukazují rychlost replikace 10 000 virtuálních počítačů v Azure.

Stále se však vyžaduje přístup využívající přírůstkovou migraci. Ve většině prostředí je potřeba dlouhý seznam virtuálních počítačů, které se mají migrovat, rozložit na menší jednotky práce, aby migrace mohla proběhnout úspěšně. Počet virtuálních počítačů, které je možné migrovat v určitém časovém období, ovlivňuje řada faktorů. Jedním z mála technických omezení je rychlost odchozího síťového připojení, ale většina limitů se řídí schopností firmy ověřovat a přijímat změny.

Přístup využívající přírůstkovou migraci v architektuře přechodu na cloud pomáhá vytvořit inkrementální plán, který zohledňuje a dokumentuje technická a kulturní omezení. Cílem tohoto modelu je maximalizovat rychlost migrace a zároveň minimalizovat režii pro IT i firmu. Níže jsou uvedené dva příklady provedení přírůstkové migrace na základě backlogu migrace.

## <a name="next-steps"></a>Další kroky

Začněte tím, že se seznámíte s [průvodcem migrací do Azure](./azure-migration-guide/index.md).

> [!div class="nextstepaction"]
> [Průvodce migrací do Azure](./azure-migration-guide/index.md)
