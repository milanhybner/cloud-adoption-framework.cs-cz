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
ms.openlocfilehash: b62dde42255d1a0e9f484e5bcfcd83bbff1ebf7e
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565775"
---
# <a name="engage-through-applications"></a>Zapojení aplikací

Jak je popsáno v tématu [data Demokratizujte](./data.md), jsou data novým olejem. To zahrnuje většinu inovací v rámci digitální ekonomiky. V takovém případě jsou aplikace na těchto analogických stanicích a infrastruktura nutná k získání tohoto paliva do správných rukou.

V některých případech je k dispozici pouze data pro změnu a splnění potřeb zákazníků. Častěji, ale řešení potřebná pro zákazníky vyžadují, aby aplikace procházela daty a vytvořily prostředí. Aplikace představují způsob, jakým se uživatel zavazuje. Jsou doma pro procesy potřebné k reakci na triggery zákazníků. Jsou to zákazníci, kteří poskytují data a přijímají doprovodné materiály. Tento článek shrnuje několik principů, které vám pomůžou zajistit správné řešení aplikace na základě hypotézy, která se má ověřit.

![Zapojení přes aplikace](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Sdílený kód

Týmy, které rychleji a přesně reagují na zpětnou vazbu od zákazníků, změny v trhu a příležitosti k inovacím, obvykle vedou na inovace na příslušné trhy. První princip inovativních aplikací se sestavuje v [přehledu růstu místo](./learn.md#growth-mindset): "sdílení kódu". V průběhu času se inovace vymění z kulturního zaměření. V případě trvalé inovace se vyžadují nejrůznější perspektivy a příspěvky.

Aby bylo možné začít s inovacemi, měl by vývoj všech aplikací začínat sdíleným úložištěm kódu. Nejpoužívanějším nástrojem pro správu úložišť kódu je [GitHub](https://guides.github.com), který umožňuje rychlé vytvoření sdíleného úložiště kódu. Alternativně je [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) sada nástrojů pro řízení verzí v Azure DevOps Services, které lze použít ke správě kódu. Azure Repos poskytuje dva typy správy verzí:

- [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git): Správa distribuovaných verzí
- [Správa verzí Team Foundation (TFVC)](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc): Centralizovaná správa verzí

## <a name="citizen-developers"></a>Vývojáři služeb pro občany

Profesionální vývojáři jsou důležitou součástí inovací. V případě, že hypotéza prokáže přesné škálování, je nutné, aby profesionální vývojáři mohli stabilizovat a připravit řešení pro škálování. Většina zásad, na které se odkazuje v tomto článku, vyžaduje podporu pro profesionální vývojáře. Aktuální trendy bohužel navrhují větší poptávku pro profesionální vývojáře, než je vývojář. Kromě toho může být náklady a tempo inovace méně vhodné, pokud je pro profesionální vývoj považována za nezbytná. V reakci na tyto výzvy poskytují vývojáři občanů způsob škálování úsilí při vývoji a urychlení testování hypotéz.

Použití vývojářů občanů může být životaschopné a efektivní, pokud je možné provést ověření počáteční hypotézy prostřednictvím nástrojů jako [PowerApps](https://docs.microsoft.com/powerapps/powerapps-overview) pro rozhraní aplikace, [Tvůrce AI](https://docs.microsoft.com/powerapps/use-ai-builder) pro procesy a předpovědi, [Microsoft Flow](https://docs.microsoft.com/flow) pro pracovní postupy a [výkon. BI](https://docs.microsoft.com/power-bi) pro spotřebu dat

> [!NOTE]
> Když se spoléháte na vývojáře občana k testování hypotézy, je vhodné mít k dispozici některé profesionální vývojáře, aby mohli poskytovat podporu, kontrolu a doprovodné materiály. Po ověření, že je hypotéza ve velkém měřítku, proces pro přechod aplikace do robustnějšího programovacího modelu zrychlí návratnost inovace. Díky zapojení profesionálních vývojářů v definicích procesů na začátku můžete později realizovat přechody čisticích procesů.

## <a name="intelligent-experiences"></a>Inteligentní prostředí

Inteligentní prostředí kombinují rychlost a škálování moderních webových aplikací s využitím inteligentních služeb a roboty. Každá z těchto technologií může stačit pro splnění potřeb vašich zákazníků. V případě, že se inteligentně spojí, rozšiřují spektrum potřeb, které je možné dosáhnout prostřednictvím digitálního zážitku, a současně pomůže s tím, že bude mít náklady na vývoj.

### <a name="modern-web-apps"></a>Moderní webové aplikace

Když je aplikace nebo zkušenosti nutná k uspokojení potřeb zákazníků, moderní webové aplikace mohou být nejrychlejší způsob, jak jít. Moderní webové prostředí můžou rychle vymezit interní nebo externí zákazníky a umožní rychlé opakování řešení.

### <a name="infusing-intelligence"></a>Začlenění chytrých funkcí

Strojové učení a umělá logika jsou stále k dispozici vývojářům. Rozsáhlá dostupnost běžných rozhraní API s prediktivními funkcemi umožňuje vývojářům lépe vyhovovat potřebám zákazníka prostřednictvím rozšířeného přístupu k datům a předpovědi.

Přidání inteligentních funkcí do řešení může umožňovat převod řeči na text, překlad textu, počítačové zpracování a dokonce i vizuální vyhledávání. Díky těmto rozšířeným funkcím můžou vývojáři snadněji vytvářet řešení, která využívají inteligentní prostředí k vytváření interaktivního a moderního prostředí.

### <a name="bots"></a>Roboti

Roboty poskytují prostředí, které je méně podobné jako při použití počítače a větší, jako je třeba práce s osobou, a to nejméně s inteligentním robotem. Dají se použít k posunování jednoduchých a opakujících se úloh (například vytvoření rezervace na večeři nebo shromáždění informací o profilu) na automatizované systémy, které už nemusí vyžadovat přímý zásah člověka. Uživatelé přejdou pomocí robota přes text, interaktivní karty a řeč. Interakce robota může být v rozsahu od rychlé otázky a odpovědi na propracované konverzace, která inteligentně poskytuje přístup ke službám.

Roboty je velmi podobné moderní webové aplikace: jsou živé na internetu a využívají rozhraní API k posílání a přijímání zpráv. To, co je v robotu, se velmi liší v závislosti na tom, jaký druh robota je. Moderní software bot spoléhá na nejrůznější technologie a nástroje, které vám umožní zajistit stále složitá prostředí na různých platformách. Jednoduchý robot však může pouze obdržet zprávu a vrátit ji zpět uživateli s velmi malým kódem.

Roboty můžou dělat stejné věci jako jiné typy softwaru: číst a zapisovat soubory, používat databáze a rozhraní API a zpracovávat běžné výpočetní úlohy. To znamená, že roboty jedinečný je jejich použití mechanismů všeobecně rezervovaných pro komunikaci ze lidského na člověka.

## <a name="cloud-native-solutions"></a>Nativní řešení cloudu

Nativní aplikace pro Cloud jsou postaveny od základů a jsou optimalizované pro cloudové škálování a výkon. Nativní aplikace v cloudu jsou obvykle sestavené pomocí mikroslužeb, přístupů k serveru, založeného na událostech nebo kontejnerů. Nejčastěji nativní řešení cloudu používají kombinaci architektury mikroslužeb, spravovaných služeb a průběžného doručování k zajištění spolehlivosti a rychlejšího uvedení na trh.

Řešení nativní pro Cloud umožňuje centralizovaným vývojářským týmům udržovat kontrolu nad obchodní logikou bez nutnosti monolitické, centralizovaného řešení. Tento typ řešení také vytvoří kotvu pro zajištění konzistence v rámci vstupu občanů a moderních prostředí. V konečném případě cloudová řešení poskytují akcelerátor pro inovace, který uvolňuje občany a profesionální vývojáři k bezpečnému a minimálnímu blokování.

## <a name="innovate-through-existing-solutions"></a>Inovovat prostřednictvím stávajících řešení

Mnoho zákaznických hypotéz se dá nejlépe doručovat moderní verzí stávajícího řešení. Když aktuální obchodní logika splňuje požadavky zákazníků (nebo se skutečně blíží), možná budete moct zrychlit inovace tím, že sestavíte na moderním řešení.

Do [metodologie migrace](../../migrate/index.md) v rámci architektury pro přijetí v cloudu jsou zahrnuty většina forem modernizace, včetně mírného refaktoringu aplikace. Tato metodologie provede týmy při přijímání cloudu prostřednictvím procesu migrace [digitální nemovitosti](../../digital-estate/index.md) do cloudu. [Průvodce migrací do Azure](../../migrate/azure-migration-guide/index.md) poskytuje zjednodušený přístup ke stejné metodologii, která je vhodná pro malý počet úloh nebo i pro jednu aplikaci.

Po migraci a modernizaci řešení existuje celá řada způsobů, jak se dá použít k vytvoření nových, inovativních řešení pro potřeby zákazníků. [Vývojáři občanů](#citizen-developers) můžou například testovat hypotézu nebo profesionální vývojáři můžou vytvářet [inteligentní prostředí](#intelligent-experiences) nebo [řešení nativní pro Cloud](#cloud-native-solutions).

### <a name="extend-an-existing-solution"></a>Rozšiřování existujícího řešení

Rozšíření řešení je jedna běžná forma modernizace. Tento přístup může být nejrychlejší cestou k inovacím, pokud jsou splněny následující podmínky pro zákazníka hypotézy:

- Stávající obchodní logika by měla splňovat (nebo se může jednat o schůzku), která je potřebná pro zákazníky.
- Vylepšené prostředí bude lépe vyhovovat potřebám konkrétního zákaznického kohorta.
- Obchodní logika vyžadovaná řešením pro minimální životaschopné produkty (MVP) byla centralizovaná, obvykle prostřednictvím [N-vrstvých](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), webových služeb, rozhraní API nebo návrhu [mikroslužeb](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices) . Tento přístup se skládá z balení stávajícího řešení v rámci nového prostředí hostovaného v cloudu. V Azure by toto řešení mohlo být v Azure App Services živé.

### <a name="rebuild-an-existing-solution"></a>Opětovné sestavení stávajícího řešení

Pokud aplikaci nelze snadno rozšířit, může být nutné řešení Refaktorovat. V tomto postupu se zatížení migruje do cloudu. Po migraci aplikace se její části upraví nebo duplikují jako webové služby nebo [mikroslužby](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices), které jsou nasazeny paralelně s existujícím řešením. Řešení založené na paralelních službách by se mohlo nakládat jako s rozšířeným řešením. Toto řešení jednoduše zabalí stávající řešení s novým prostředím hostovaným v cloudu. V Azure by toto řešení mohlo být v Azure App Services živé.

> [!CAUTION]
> Refaktoring nebo přeplánování řešení nebo centralizované obchodní logiky může rychle aktivovat časově náročné [technické špičky](./build.md#reduce-complexity-and-delay-technical-spikes)namísto zdroje hodnot zákazníků. Toto je riziko pro inovace, zejména v rané fázi ověřování hypotéz. V rámci navrhování řešení by měl být v rámci návrhu řešení k dispozici cesta k MVP, která nevyžaduje refaktoring stávajících řešení. Je vhodné zpozdit refaktoring, dokud se nebudete moct na škálování počáteční hypotézy ověřit.

## <a name="operating-model-innovations"></a>Inovace operačního modelu

Kromě moderních a inovativních přístupů k vytváření aplikací byly významné inovace v *operacích*aplikace. Tyto přístupy vytvářely mnoho organizačních přesunů. Jedním z nejvýraznějších z nich je [cloudové centrum vynikajícího](../../organize/cloud-center-of-excellence.md) provozního modelu. V případě plně pedagogů a vyspělých obchodních týmů máte možnost poskytovat si vlastní provozní podporu pro řešení.

Typ modelu samoobslužné správy, který najdete v cloudovém centru špičkových služeb, umožňuje užší řízení a rychlejší iterace v rámci prostředí řešení. Tyto cíle se dosahují tak, že přenáší provozní kontrolu a odpovědnost na obchodní tým.

Pokud se snažíte škálovat nebo splnit globální poptávku v existujícím řešení, může být tento přístup dostačující pro ověření zákaznických předpokladů. Po migraci řešení a mírné modernizaci může obchodní tým škálovat IT a testovat celou řadu hypotéz. Obvykle zahrnují zákazníky, kteří mají obavy o výkon, globální distribuci a jiné potřeby zákazníků, které brání IT operace.

## <a name="reduce-overhead-and-management"></a>Snížení režie a správy

V rámci řešení je údržba, což znamená pomalejší řešení. To znamená, že můžete zrychlit inovace tím, že snížíte dopad operací na dostupnou šířku pásma.

V rámci přípravy na celou řadu iterací potřebných k zajištění inovativního řešení je důležité si představit předem. Můžete například minimalizovat provozní zatížení na začátku v procesu tím, že se přihlásíte k možnostem bez serveru. V Azure můžou možnosti aplikace bez serveru zahrnovat [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) nebo [kontejnery](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql).

Paralelně poskytuje Azure možnosti pro data transakcí bez serveru, které také omezují režijní náklady. [Seznam databázových produktů](https://docs.microsoft.com/azure/#pivot=products&panel=databases) poskytuje možnosti pro hostování dat bez nutnosti celé datové platformy.

## <a name="next-steps"></a>Další kroky

V závislosti na hypotéze a řešení můžou zásady v tomto článku pomoci při navrhování aplikací, které odpovídají definicím MVP a vzdálení uživatelé. V dalším kroku najdete zásady pro zajištění [přijetí](./ci-cd.md), které nabízejí způsoby, jak aplikaci a datům poskytnout do rukou zákazníků rychleji a efektivně.

> [!div class="nextstepaction"]
> [Přijetí pravomocí](./ci-cd.md)
