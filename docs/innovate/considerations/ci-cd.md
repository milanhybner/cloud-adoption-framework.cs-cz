---
title: Zajištění přijetí pomocí digitální vynález
description: Použijte model splatnosti metodologie inovace, abyste snížili tření, které zpomaluje přijetí, a přitom zachováváme osvědčené postupy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c29eedc234d3795ce0bad76b324e7049dfe15633
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433339"
---
<!-- cSpell:ignore deprioritize -->

# <a name="empower-adoption"></a>Posílení přechodu

Špičkový test inovace je reakce zákazníků na vynález. Prokázala se hypotéza jako true? Používají zákazníci řešení? Je potřeba se škálovat tak, aby splňovala požadavky požadovaného procenta uživatelů? Co je nejdůležitější, udělejte si zpátky? Žádná z těchto otázek se nemůže zeptat, dokud nebude nasazené řešení pro minimální životaschopné produkty (MVP). V tomto článku se zaměříme na obor, který umožňuje přijetí.

## <a name="reduce-friction-that-affects-adoption"></a>Snížení tření, které má vliv na přijetí

Existuje několik klíčových příchodů, které je potřeba přijmout, aby bylo možné je minimalizovat kombinací technologií a procesů. Pro čtenáře s poznatky o kontinuální integraci (CI) a procesu průběžného nasazování (CD) nebo DevOps se seznámíte s tímto. Tento článek zavádí výchozí bod pro týmy přijímání v cloudu, které se zajímá z smyček a zpětné vazby. V budoucnu by tento výchozí bod mohl podporovat robustnější přístup k CI/CD nebo DevOpsům, jako jsou produkty a týmy zralé.

Jak je popsáno v tématu [měření dopadu zákazníka](./measure.md), pozitivní ověření jakékoli hypotézy vyžaduje iteraci a určení. Během jakýchkoli inovačních cyklů dojde k většímu počtu chyb než WINS. To se očekává. Pokud ale zákazník potřebuje, hypotéza a řešení ve velkém měřítku, svět se rychle změní. V tomto článku se zaměřujeme na minimalizaci [technických špiček](./build.md#reduce-complexity-and-delay-technical-spikes) , které se pomalými inovacemi, ale pořád se ujistěte, že zachováte několik pevných osvědčených postupů. V takovém případě vám pomůže návrh týmu pro budoucí úspěch při dodávání aktuálních zákaznických potřeb.

## <a name="empowering-adoption-the-maturity-model"></a>Zajištění přijetí: model splatnosti

Hlavním cílem [metodologie](./index.md) inovace je vytvořit zákaznická partnerství a urychlit smyčky zpětné vazby, což vede k inovacím na trh. Následující obrázek a oddíly popisují počáteční implementace, které podporují tuto metodologii.

![Přijetí pravomocí: model splatnosti](../../_images/innovate/empower-adoption-maturity.png)

- [Sdílené řešení](#shared-solution): Vytvořte centralizované úložiště pro všechny aspekty řešení.
- [Smyčky zpětné vazby](#feedback-loops): Ujistěte se, že smyčky zpětné vazby je možné spravovat konzistentně prostřednictvím iterací.
- [Kontinuální integrace](#continuous-integration): pravidelně Sestavujte a Konsolidujte řešení.
- [Spolehlivé testování](#reliable-testing): Ověřte kvalitu řešení a očekávané změny, abyste zajistili spolehlivost vašich testovacích metrik.
- [Nasazení řešení](#solution-deployment): nasaďte řešení, aby tým mohl rychle sdílet změny se zákazníky.
- [Integrovaná měření](#integrated-measurements): přidejte metriky učení do smyčky zpětné vazby pro účely jasného seskupení úplným týmem.

Aby se minimalizovaly technické špičky, Přepokládejme, že v každé z těchto principů bude tato splatnost v prvním stavu nízká. Ale bez omezení plánu Naplánujte na nástroje a procesy, které se můžou škálovat, protože hypotéza se bude podrobněji jemně rozrovnávat. V Azure můžou [GitHub](https://guides.github.com) a [Azure DevOps](https://docs.microsoft.com/azure/devops) začít pracovat malým týmem s malým třením. Tyto týmy se můžou rozrůstat, aby zahrnovaly tisíce vývojářů, kteří spolupracují na řešeních škálování a testují stovky zákaznických hypotéz. Zbývající část tohoto článku ukazuje, jak velký/počáteční malý přístup k zajištění toho, aby se v každém z těchto principů probíralo přijetí.

## <a name="shared-solution"></a>Sdílené řešení

Jak je popsáno v tématu [měření dopadu zákazníka](./measure.md), pozitivní ověření jakékoli hypotézy vyžaduje iteraci a určení. Během jakýchkoli inovačních cyklů dojde k většímu počtu chyb než WINS. To se očekává. Pokud ale zákazník potřebuje, hypotéza a řešení ve velkém měřítku, svět se rychle změní.

Při škálování inovace není pro řešení k dispozici žádný hodnotný nástroj, než je základem sdíleného kódu. Bohužel neexistuje spolehlivý způsob, jak předpovídat tuto iteraci, nebo který MVP poskytne vítěznou kombinaci. To je důvod, proč není nikdy příliš brzy k navázání sdíleného základního kódu nebo úložiště. Toto je [technický technický špička](./build.md#reduce-complexity-and-delay-technical-spikes) , který by se nikdy neměl zpozdit. Když tým projde různými řešeními MVP, sdílené úložiště umožňuje snadnou spolupráci a urychlení vývoje. Když změny řešení přetáhnete dolů metriky učení, Správa verzí vám umožní vrátit se zpět na dřívější, účinnější verzi řešení.

Nejpoužívanějším nástrojem pro správu úložišť kódu je [GitHub](https://guides.github.com), který umožňuje vytvořit úložiště se sdíleným kódem v několika krocích. Kromě toho je možné pomocí funkce [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) služby Azure DevOps vytvořit úložiště [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) nebo [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="feedback-loops"></a>Smyčky zpětné vazby

Tím, že se zákazník stane součástí řešení, je klíč k sestavování zákaznických partnerství během inovačních cyklů. To je v rámci [měření dopadu na zákazníky](./measure.md)dokončeno. Vyžaduje konverzace a přímé testování u zákazníka. Vygenerujte zpětnou vazbu, která musí být spravována efektivně.

Každý bod zpětné vazby je potenciální řešení pro potřeby zákazníka. Důležitější je, že každý bit zpětné vazby od zákazníka představuje příležitost ke zlepšení partnerství. Pokud je vaše zpětná vazba k řešení MVP, Oslavte si zákazníka. I v případě, že některá zpětná vazba není nenapadnutelná, stačí jednoduše transparentní s rozhodnutím o deprioritování zpětné vazby ukazující [růst místo](./learn.md#growth-mindset) a zaměřit se na [průběžné učení](./learn.md#continuous-learning).

[Azure DevOps](https://docs.microsoft.com/azure/devops) obsahuje způsoby [, jak vyžádat, poskytnout a spravovat zpětnou vazbu](https://docs.microsoft.com/azure/devops/project/feedback). Každý z těchto nástrojů slouží k centralizaci zpětné vazby, aby tým mohl provádět akce a poskytoval následný postup ve službě transparentní smyčky zpětné vazby.

## <a name="continuous-integration"></a>Kontinuální integrace

Vzhledem k tomu, že se přijímají škálování a hypotéza se přiblíží k skutečným inovacím ve velkém měřítku, může být počet menších hypotéz, který se má testovat, rychlejší rychleji. Pro přesné smyčky zpětné vazby a hladké procesy přijetí je důležité, aby každá z těchto hypotéz byla integrovaná a podpora primární hypotézy na základě inovace. To znamená, že se také musíte rychle přesunout na inovace a růst, což vyžaduje více vývojářů pro testování variací základní hypotézy. Pro účely pozdějšího vývoje můžete dokonce potřebovat více týmů vývojářů, přičemž každá z nich bude sdílet řešení. Nepřetržitá integrace je prvním krokem ke správě všech přesouvaných částí.

V nepřetržité integraci jsou změny kódu často sloučeny do hlavní větve. Automatizované procesy sestavení a testování zajistí, že kód v hlavní větvi je vždy provozní kvalita. Tím je zajištěno, že vývojáři společně pracují na vývoji sdílených řešení, která poskytují přesné a spolehlivé smyčky zpětné vazby.

Azure DevOps a [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) poskytují možnosti průběžné integrace jenom s několika kroky na GitHubu nebo v nejrůznějších úložištích.
Další informace o [průběžné integraci](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration)nebo další informace najdete v [praktickém testovacím prostředí](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration). K urychlení tvorby [kanálů CI/CD prostřednictvím Azure DevOps](https://azure.microsoft.com/solutions/devops)existují taky architektury řešení.

## <a name="reliable-testing"></a>Spolehlivé testování

Vady v jakémkoli řešení mohou vytvořit falešně pozitivní nebo falešně negativní výsledek. Neočekávané chyby mohou snadno vést k chybné interpretaci metrik přijetí uživateli. Můžou také vygenerovat negativní zpětnou vazbu od zákazníků, kteří nepřesně reprezentují test vaší hypotézy.

Během počátečních iterací řešení MVP se očekávají vady; Začátky můžou je dokonce najít endearing. V dřívějších verzích je testování přijetí obvykle neexistující. Jeden aspekt sestavování s soucit se ale bude týkat ověření potřeb a hypotéz. Obojí lze dokončit prostřednictvím testů jednotek na úrovni kódu a ručních testů přijetí před nasazením. Dohromady tyto prostředky poskytují spolehlivost při testování. Měli byste usilovat o automatizaci dobře definované řady testů sestavení, jednotek a přijetí. Tím zajistíte spolehlivé metriky související s podrobnějším vylepšením pro hypotézu a výsledné řešení.

Funkce [Azure test Plans](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) poskytuje nástroje pro vývoj a provoz testovacích plánů během ručního nebo automatizovaného provádění testu.

## <a name="solution-deployment"></a>Nasazení řešení

Nejužitečnější aspekt, který umožňuje přijetí, je možná vaše možnost řídit vydání řešení zákazníkům. Poskytnutím samoobslužné služby nebo automatizovaného kanálu pro vydání řešení zákazníkům urychlíte smyčku zpětné vazby. Když zákazníkům umožníte rychle pracovat se změnami v řešení, budete je zvát do procesu. Tento přístup také aktivuje rychlejší testování hypotéz. tím se snižuje předpoklady a potenciální repráce.

Existuje několik metod pro nasazení řešení. Následující představuje tři nejběžnější:

- **Průběžné nasazování** je nejrozšířenější způsob, jak automaticky nasazuje změny kódu v produkčním prostředí. Pro vyspělé týmy, které testují vyspělé hypotézy, může být průběžné nasazování velmi cenné.
- V počátečních fázích vývoje může být **průběžné doručování** vhodnější. Při průběžném doručování se všechny změny kódu automaticky nasadí do prostředí podobného produkčnímu prostředí. Vývojáři, tvůrci obchodních organizací a další členové týmu mohou použít toto prostředí k ověření, že je jejich práce připravená na provoz. Tuto metodu můžete také použít k otestování předpokladů se zákazníky, aniž by to ovlivnilo probíhající obchodní aktivity.
- **Ruční nasazení** je nejméně důmyslný přístup k produktu Release Management. Jak název navrhuje, někdo v týmu ručně nasadí nejnovější změny kódu. Tento přístup je náchylný k chybám, nespolehlivě a považuje se za antipattern pomocí většiny sezónních technik.

Během první iterace řešení MVP je běžné nasazení společné bez ohledu na předchozí posouzení. Když je řešení extrémně kapalina a zpětná vazba od zákazníka není známa, existuje významné riziko pro resetování celého řešení (nebo dokonce i základní hypotézy). Tady je obecné pravidlo pro ruční nasazení: žádné potvrzení od zákazníka, žádné automatizace nasazení.

Investice do začátku může vést ke ztrátě času. Důležitější je, že může vytvořit závislosti v kanálu vydávání verzí, aby byl tým více odolný vůči počátečnímu pivotu. Po prvních několika iteracích nebo v případě, že zpětná vazba od zákazníků navrhuje potenciální úspěch, je třeba rychle přijmout pokročilejší model nasazení.

V jakékoli fázi ověřování předpokladů poskytuje Azure DevOps a [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) možnosti průběžného doručování a průběžného nasazování. Přečtěte si další informace o [průběžném doručování](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery)nebo si Projděte [praktická cvičení](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment). Architektura řešení také umožňuje urychlit vytváření [kanálů CI/CD prostřednictvím Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="integrated-measurements"></a>Integrovaná měření

Když [měříte na dopad zákazníků](./measure.md), je důležité pochopit, jak zákazníci reagují na změny v řešení. Tato data, označovaná jako *telemetrie*, poskytují přehled o akcích, které uživatel (nebo kohorta uživatelé) přijal při práci s řešením. Z těchto dat je snadné získat kvantitativní ověření hypotézy. Tyto metriky pak můžete použít k úpravě řešení a k vygenerování přesnější hypotézy. Tyto jemný změny pomůžou pořídit počáteční řešení v následných iteracích, čímž se při současném řízení opakuje i jejich opětovné přijetí.

V Azure [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) poskytuje nástroje a rozhraní pro shromažďování a kontrolu dat ze zkušeností zákazníků. Tyto poznámky a přehledy můžete použít k upřesnění nevyřízených položek pomocí [Azure boards](https://docs.microsoft.com/azure/devops/boards).

## <a name="next-steps"></a>Další kroky

Jakmile se seznámíte s nástroji a procesy potřebnými k tomu, abyste si je mohli přijmout, je čas kontrolovat pokročilejší pravidla inovace: [interakce se zařízeními](./devices.md). Tato disciplína může přispět ke snížení bariér mezi fyzickým a digitálním prostředím, takže je vaše řešení ještě snazší.

> [!div class="nextstepaction"]
> [Interakce se zařízeními](./devices.md)
