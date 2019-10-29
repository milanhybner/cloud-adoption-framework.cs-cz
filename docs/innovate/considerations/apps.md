---
title: 'Inovace v cloudu: zapojení aplikací'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do cloudových inovací – zapojení do aplikací
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3db2349e3c1da7c80f3089ea187a3de72d006d1f
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683301"
---
# <a name="engage-through-applications"></a>Zapojení aplikací

Jak je popsáno v článku o [democratizing datech](./data.md), jsou data novým olejem. To zahrnuje většinu inovací v rámci digitální ekonomiky. V takovém případě jsou aplikace na této analogové infrastruktuře a infrastruktura nutná k získání tohoto paliva do správných rukou.

V některých případech jsou data dostačující pro změnu a splnění potřeb zákazníků. Častěji řešení potřebnou pro zákazníky bude vyžadovat, aby aplikace napracovaly s daty a vytvořily prostředí. Aplikace představují způsob, jakým se uživatel zavazuje. Jsou doma pro procesy potřebné k reakci na triggery zákazníků. Jsou to zákazníci, kteří poskytují informace a přijímají doprovodné materiály. Tento článek popisuje několik principů, které vám pomůžou při zarovnávání správného řešení aplikace na základě hypotézy, která se má ověřit.

![Zapojení přes aplikace](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Sdílený kód

Tým, který může rychleji a přesně reagovat na zpětnou vazbu od zákazníků, změny v trhu a příležitosti k inovacím, povede na jejich příslušné trhy. První princip inovativních aplikací je popsaný v tématu [růst místo – přehled](./learn.md#growth-mindset)"sdílení kódu". Inovace v průběhu času můžou pocházet jenom z kulturního zaměření. V případě trvalé inovace se budou vyžadovat nejrůznější perspektivy a příspěvky.

Aby bylo možné začít s inovacemi, měl by vývoj všech aplikací začínat sdíleným úložištěm kódu. Nejběžnějším nástrojem pro správu úložišť kódu je [GitHub](https://guides.github.com/), který umožňuje vytvoření sdíleného úložiště kódu několika kliknutími. Alternativně lze funkci [Azure Repos](/azure/devops/repos/get-started/what-is-repos?view=azure-devops) služby Azure DevOps použít k vytvoření úložiště [Git](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) nebo [Team Foundation](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="citizen-developers"></a>Vývojáři občanů

Profesionální vývojáři jsou důležitou součástí inovací. V případě, že hypotéza prokáže přesné škálování, je nutné, aby profesionální vývojáři mohli stabilizovat a připravit řešení pro škálování. Většina zásad, na které se odkazuje v tomto článku, bude vyžadovat podporu od profesionálních vývojářů. Aktuální trendy si bohužel navrhují, že pro profesionální vývojáře existuje více otevřených vývojářů, a pak vývojáři. Dále platí, že náklady a tempo inovace můžou být méně vhodné, když se vyžadují potřeby profesionálního vývoje. Vývojáři občanů poskytují způsob, jak škálovat vývojové úsilí a urychlit testování hypotéz.

Vývojáři občanů můžou být v případě, že je možné ověřit počáteční hypotézu pomocí nástrojů jako [PowerApps](https://docs.microsoft.com/powerapps/powerapps-overview) pro rozhraní aplikace, [Tvůrce AI](/powerapps/use-ai-builder) pro procesy a předpovědi, [Microsoft Flow](https://docs.microsoft.com/flow) pro pracovní postupy nebo [Power BI](https://docs.microsoft.com/power-bi) pro data nároky.

> [!NOTE]
> Při využití vývojářů občana k testování hypotézy doporučujeme, aby profesionální vývojáři poskytovali podporu, kontrolu a doprovodné materiály. Jakmile se ve velkém měřítku vrátí hypotéza, proces převodu aplikace do robustnějšího programovacího modelu zrychluje jejich inovace. V případě profesionálních vývojářů v definicích prvotního procesu může dojít k pozdějšímu čištění přechodů.

## <a name="intelligent-experiences"></a>Inteligentní prostředí

Inteligentní prostředí kombinují rychlost a škálování moderních webových aplikací s využitím nástrojů pro rozpoznávání služeb a roboty. Každá z nich může být dostačující pro splnění potřeb vašich zákazníků. Kombinování spektra potřeb, které je možné splnit prostřednictvím digitálního prostředí, se rozbalí, ale investice do vývoje můžou být i nadále obsažené.

### <a name="modern-web-apps"></a>Moderní webové aplikace

Když je aplikace nebo zkušenosti nutná k uspokojení potřeb zákazníků, moderní webové aplikace mohou být nejrychlejší způsob, jak tyto požadavky splnit. Moderní webové prostředí můžou rychle vymezit interní nebo externí zákazníky a umožní rychlé opakování řešení.

### <a name="infusing-intelligence"></a>Nematoucí inteligentní funkce

Strojové učení a umělá inteligentní funkce jsou pro vývojáře stále více dostupné. Rozsáhlá dostupnost běžných rozhraní API s prediktivními funkcemi umožňuje vývojářům lépe vyhovovat potřebám zákazníka prostřednictvím rozšířeného přístupu k datům a předpovědi.

Přidání inteligentních funkcí do řešení může umožňovat převod řeči na text, překlad textu, počítačové zpracování a dokonce i vizuální vyhledávání. Díky těmto rozšířeným funkcím můžou vývojáři snadněji vytvářet řešení, která využívají inteligentní prostředí k vytváření interaktivního a moderního prostředí.

### <a name="bots"></a>Roboti

Roboty poskytují prostředí, které je méně podobné jako při použití počítače a větší, jako je třeba práce s osobou nebo aspoň inteligentním robotem. Dají se použít k posunování jednoduchých a opakujících se úloh, jako je třeba rezervace na večeři nebo shromažďování informací o profilu, na automatizované systémy, které už nemusí vyžadovat přímý zásah člověka. Uživatelé můžou s robotem přemluvit pomocí textu, interaktivních karet a řeči. Interakce robota může být rychlá otázka a odpověď, nebo se může jednat o propracované konverzaci, která inteligentně poskytuje přístup ke službám.

Roboty jsou velmi podobné moderní webové aplikace, které jsou na internetu a využívají rozhraní API k posílání a přijímání zpráv. To, co je v robotu, se velmi liší v závislosti na tom, jaký druh robota je. Moderní software bot spoléhá na nejrůznější technologie a nástroje, které vám umožní zajistit stále složitá prostředí pro širokou škálu platforem. Jednoduchý robot však může pouze obdržet zprávu a vrátit ji zpět uživateli s velmi malým kódem.

Roboty můžou dělat stejné věci i jiné typy softwaru, které můžou číst a zapisovat soubory, používat databáze a rozhraní API a provádět běžné výpočetní úkoly. To znamená, že roboty jedinečný je jejich použití mechanismů všeobecně rezervovaných pro komunikaci ze lidského na člověka.

## <a name="cloud-native-solutions"></a>Nativní řešení cloudu

Nativní aplikace v cloudu jsou postaveny od základů. Nativní cloudové aplikace jsou optimalizované pro cloudové škálování a výkon. Nativní aplikace v cloudu jsou obvykle sestavené pomocí mikroslužeb, přístupů k serveru, založeného na událostech nebo kontejnerů. Nejčastěji nativní řešení cloudu využívají kombinaci architektury mikroslužeb, spravovaných služeb a průběžného doručování k zajištění spolehlivosti a rychlejšího uvedení na trh.

Řešení nativní pro Cloud umožňuje centralizovaným vývojářským týmům udržovat kontrolu nad obchodní logikou bez nutnosti monolitické centralizovaného řešení. Tento typ řešení také vytvoří kotvu k zajištění konzistence mezi vývojáři občanů a moderními prostředími. A konečně cloudová řešení poskytují akcelerátor pro inovace, který uvolňuje občany a profesionální vývojáři, aby mohli bezpečně inovovat a s minimálními blokováními.

## <a name="innovate-through-existing-solutions"></a>Inovovat prostřednictvím stávajících řešení

Mnoho zákaznických hypotéz se dá nejlépe doručovat moderní verzí stávajícího řešení. Když aktuální obchodní logika splňuje požadavky zákazníků (nebo se skutečně blíží), možná budete moct zrychlit inovace tím, že sestavíte na moderním řešení.

Do [metodologie migrace](../../migrate/index.md) v rámci architektury pro přijetí v cloudu jsou zahrnuty většina forem modernizace, včetně mírného refaktoringu aplikace. Tato metodologie provede týmy pro přijímání cloudu prostřednictvím procesů pro migraci [digitální nemovitosti](../../digital-estate/index.md) do cloudu. [Průvodce migrací do Azure](../../migrate/azure-migration-guide/index.md) poskytuje zjednodušený přístup ke stejné metodologii, která je vhodná pro malý počet úloh nebo i pro jednu aplikaci.

Po migraci a modernizaci existuje celá řada způsobů, jak řešení využít při vytváření nových inovativních řešení potřebných pro zákazníky. [Vývojáři občanů](#citizen-developers) by například mohli otestovat hypotéza nebo profesionální vývojáři, kteří můžou vytvářet [inteligentní prostředí](#intelligent-experiences) nebo [nativní řešení cloudu](#cloud-native-solutions).

### <a name="extend-an-existing-solution"></a>Rozšiřování existujícího řešení

Rozšíření řešení je jedna běžná forma modernizace. Tento přístup může být nejrychlejší cestou k inovacím, pokud jsou splněny následující podmínky pro zákazníka hypotézy:

- Stávající obchodní logika by měla splňovat (nebo se může jednat o schůzku), která je potřebná pro zákazníky.
- Vylepšené prostředí bude lépe vyhovovat potřebám konkrétního zákaznického kohorta.
- Obchodní logika požadovaná řešením MVP byla centralizovaná, obvykle prostřednictvím [N-vrstvých](/azure/architecture/guide/architecture-styles/n-tier), webových služeb, rozhraní API nebo návrhu [mikroslužeb](/azure/architecture/guide/architecture-styles/microservices) . Tento přístup se skládá z balení stávajícího řešení s novým prostředím hostovaným v cloudu. V Azure by toto řešení mohlo být v Azure App Services živé.

### <a name="rebuild-an-existing-solution"></a>Opětovné sestavení stávajícího řešení

Pokud aplikaci nelze snadno rozšířit, může být nutné řešení Refaktorovat. V tomto postupu se zatížení migruje do cloudu. Po migraci se části aplikace upraví nebo duplikují jako webové služby nebo [mikroslužby](/azure/architecture/guide/architecture-styles/microservices), které jsou nasazeny paralelně s existujícím řešením. Řešení založené na paralelních službách by se mohlo nakládat jako s rozšířeným řešením. Toto řešení jednoduše zabalí stávající řešení s novým prostředím hostovaným v cloudu. V Azure by toto řešení mohlo být v Azure App Services živé.

> [!CAUTION]
> Refaktoring nebo přeplánování řešení nebo centralizace obchodní logiky může rychle vzniknout časově náročné [technické špičky](./build.md#reduce-complexity-and-delay-technical-spikes), a to na rozdíl od zdroje hodnot zákazníků. Toto je riziko pro inovace, zejména v rané fázi ověřování hypotéz. V rámci navrhování řešení by měl být v rámci návrhu řešení k dispozici cesta k MVP, která nevyžaduje refaktoring stávajících řešení. Je vhodné zpozdit refaktoring, dokud se nebudete moct na škálování počáteční hypotézy ověřit.

## <a name="operating-model-innovations"></a>Inovace operačního modelu

Kromě moderních inovačních postupů při vytváření aplikací byly k dispozici inovace týkající se provozu aplikací. Přístupy vytvářely mnoho organizačních přesunů. Jedním z nejvýraznějších z nich je přesun do [cloudového centra špičkových](../../organize/cloud-center-of-excellence.md) provozních modelů. V případě plně pedagogů a vyspělých obchodních týmů máte možnost poskytovat si vlastní provozní podporu pro řešení.

Typ modelu provozní správy samoobslužné služby, který se nachází v cloudovém centru, umožňuje užší řízení a rychlejší iterace v rámci prostředí řešení. To se provádí tak, že se přenáší provozní řízení a odpovědnost na obchodní tým.

V případě, že cílem je škálovat nebo splnit globální poptávku pro existující řešení, může být tento přístup dostačující k ověření zákaznických předpokladů. Po migraci a mírném modernizaci může mít obchodní tým možnost škálovat řešení a otestovat celou řadu hypotéz týkajících se zákazníka kohorty, kteří mají obavy o výkon, globální distribuci nebo jiné požadavky zákazníků, které mu brání. Operations.

## <a name="reduce-overhead-and-management"></a>Snížení režie a správy

V rámci řešení je údržba, což znamená pomalejší řešení. Zrychlete inovace tím, že omezíte operace dopadu na dostupnou rychlost.

V rámci přípravy na celou řadu iterací, které jsou potřeba k zajištění inovativního řešení, je důležité si představit předem. Přihlaste možnosti bez serveru a minimalizujte provozní zátěže na začátku procesu.

V Azure můžou možnosti aplikace bez serveru zahrnovat [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) nebo [kontejnery](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql).

Paralelně poskytuje Azure možnosti pro data transakcí bez serveru, které také omezují režijní náklady. [Seznam databázových produktů](https://docs.microsoft.com/azure/#pivot=products&panel=databases) poskytuje možnosti pro hostování dat bez nutnosti celé datové platformy.

## <a name="next-steps"></a>Další kroky

V závislosti na hypotéze a řešení můžou zásady v tomto článku pomoci při navrhování aplikací, které odpovídají definicím MVP a vzdálení uživatelé. V dalším kroku se dozvíte, jakým způsobem je možné [přijmout](./ci-cd.md)informace, které projednávají způsoby, jak rychle získat aplikaci a data do rukou zákazníků rychleji.

> [!div class="nextstepaction"]
> [Přijetí pravomocí](./ci-cd.md)