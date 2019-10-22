---
title: 'Inovace v cloudu: podpora přijetí'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do cloudových inovací – zajištění přijetí
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 0c6f55ec7f82756658fc67fb9412d7d83d503b97
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683241"
---
# <a name="empower-adoption"></a>Přijetí pravomocí

Špičkový test inovace je reakce zákazníků na vynález. Prokázala se hypotéza jako true? Používají zákazníci řešení? Je potřeba se škálovat tak, aby splňovala požadavky požadovaného procenta uživatelů? Co je nejdůležitější, udělejte si zpátky? Žádná z těchto otázek se nemůže zeptat do nasazení řešení MVP. V tomto článku se zaměříme na obor, který umožňuje přijetí.

## <a name="reducing-friction-to-adoption"></a>Snížení tření k přijetí

Existuje několik klíčových příchodů, které je potřeba přijmout, aby bylo možné je minimalizovat kombinací technologií a procesů. Pro čtenáře, kteří mají zkušenosti s CI/CD nebo DevOps procesy, se podobá následující: V tomto článku se dozvíte, jak vytvořit výchozí bod pro týmy pro přijímání v cloudu, který bude poskytovat inovace na palivo a smyčky zpětné vazby. Delší období: Tento výchozí bod může růst do robustnějšího způsobu CI/CD nebo DevOpsch přístupů, jako v případě vyspělosti produktů a týmů.

Popsaný v tématu [měření dopadu zákazníků](./measure.md), pozitivní ověření jakékoli hypotézy vyžaduje iteraci a určení. Během jakýchkoli inovačních cyklů budete mít větší počet selhání než WINS. To se očekává. Pokud se ale zákaznická potřeba, hypotéza a řešení ve velkém měřítku, svět se rychle změní. Tento článek se zaměřuje na minimalizaci [technické špičky](./build.md#reduce-complexity-and-delay-technical-spikes) , která by mohla zpomalovat inovace, ale zajistěte, aby byly zavedeny některé základní osvědčené postupy Pomůže vám to navrhovat tým pro budoucí úspěch, ale doručí na základě aktuálních potřeb zákazníků.

## <a name="empowering-adoption---maturity-model"></a>Zavedení modelu splatnosti

Hlavním cílem [metodologie](./index.md) inovace je vytvořit zákaznická partnerství a urychlit smyčky zpětné vazby, což vede k inovacím na trh.
Následující obrázek a oddíly obsahu popisují počáteční implementace, které budou podporovat metodologii.

![Zajištění přijetí – model splatnosti](../../_images/innovate/empower-adoption-maturity.png)

- [Sdílené řešení](#shared-solution): Vytvořte centralizované úložiště pro všechny aspekty řešení.
- [Smyčky zpětné vazby](#feedback-loops): Ujistěte se, že smyčky zpětné vazby je možné spravovat konzistentně prostřednictvím iterací.
- [Kontinuální integrace](#continuous-integration): pravidelně Sestavujte a Konsolidujte řešení.
- [Spolehlivé testování](#reliable-testing): Ověřte kvalitu řešení a očekávané změny pro zajištění míry.
- [Nasazení řešení](#solution-deployment): nasazení řešení, které týmu umožní rychle sdílet změny se zákazníky.
- [Integrovaná měření](#integrated-measurements): přidejte metriky učení do smyčky zpětné vazby pro účely jasného seskupení úplným týmem.

Příliš minimalizace technických špiček, předpokládá se, že doba splatnosti bude zpočátku nízká v každém z těchto principů. Ale Plánujte dopředu o zarovnání k nástrojům a procesům, které se můžou škálovat, protože hypotéza je podrobněji jemně odstupňovaná. V Azure nabízí kombinace [GitHubu](https://guides.github.com) a [Azure DevOps](https://docs.microsoft.com/azure/devops) malým týmům možnost začít s malým třením. Pak se rozšiřujte na tisíce vývojářů, kteří pracují s škálováním řešení, která testují stovky zákaznických hypotéz. Zbývající část tohoto článku ilustruje plán velký, počáteční malý přístup k zajištění toho, aby se v každém z těchto principů provedlo přijímání.

## <a name="shared-solution"></a>Sdílené řešení

Popsaný v tématu [měření dopadu zákazníků](./measure.md), pozitivní ověření jakékoli hypotézy vyžaduje iteraci a určení. Během jakýchkoli inovačních cyklů budete mít větší počet selhání než WINS. To se očekává. Pokud se ale zákaznická potřeba, hypotéza a řešení ve velkém měřítku, svět se rychle změní.

Při škálování inovace není k dispozici žádný hodnotný nástroj než sdílený základ kódu pro řešení. Bohužel neexistuje žádný způsob, jak předpovídat, kterou iteraci nebo které MVP přinese na výhrou kombinaci. To je důvod, proč není nikdy příliš brzy pro vytvoření sdíleného základu kódu nebo úložiště. Toto je [technický technický špička](./build.md#reduce-complexity-and-delay-technical-spikes) , který by se nikdy neměl zpozdit. Když tým projde různými řešeními MVP, sdílené úložiště umožní snadné spolupráci a urychlení vývoje. V případě, že změny v řešení způsobují negativní dopad na metriky učení, může správa verzí umožňovat vrácení zpět k předchozí a efektivnější verzi řešení.

Nejběžnější Nástroj pro správu úložišť kódu je [GitHub](https://guides.github.com) , který umožňuje vytvoření sdíleného úložiště kódu několika kliknutími. Kromě toho je možné pomocí funkce [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) služby Azure DevOps vytvořit úložiště [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) nebo [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="feedback-loops"></a>Smyčky zpětné vazby

Klíčem k sestavování vztahů mezi zákazníky během inovačních cyklů je udělat zákazníka jako součást řešení. To se provádí na opěrce zbraní prostřednictvím [měření dopadu zákazníka](./measure.md). Přesněji, vyžaduje konverzace a přímé testování u zákazníka. Výsledkem bude zpětná vazba, která musí být spravovaná.

Každý bod zpětné vazby je potenciální řešení pro potřeby zákazníka. Důležitější je, že každý bit zpětné vazby přímo od zákazníka je příležitostí ke zlepšení partnerství. Pokud je vaše zpětná vazba k řešení MVP, Oslavte ho zákazníkovi. I v případě, že zpětná vazba není nenapadnutelná, jednoduše je transparentní s rozhodnutím o deprioritování zpětné vazby, ukazuje [růst místo](./learn.md#growth-mindset) a zaměřuje se na [průběžné učení](./learn.md#continuous-learning).

[Azure DevOps](https://docs.microsoft.com/azure/devops) obsahuje způsoby [, jak vyžádat, poskytnout a spravovat zpětnou vazbu](https://docs.microsoft.com/azure/devops/project/feedback). Každý z těchto nástrojů se může soustředit na zpětnou vazbu, aby tým mohl provádět akce a nahlásit zpětnou vazbu a poskytnout transparentní smyčku zpětné vazby.

## <a name="continuous-integration"></a>Nepřetržitá integrace

Vzhledem k tomu, že se přijímají škálování a hypotéza roste blíž k skutečným inovacím ve velkém měřítku, bude počet menších hypotéz, které se mají testovat, rychle růst. Pro přesné smyčky zpětné vazby a hladké procesy přijetí je důležité, aby každá z těchto hypotéz byla integrovaná a podpora primární hypotézy na základě inovace. Bohužel se také musíte rychle přesunout na inovace a růst, což bude vyžadovat více vývojářů, kteří testují varianty základní hypotézy. Pro pozdější vývojové úsilí může být pro každé sestavení na sdílené řešení potřeba víc týmů pro vývojáře. Nepřetržitá integrace je prvním krokem ke správě různých pohyblivých částí.

V nepřetržité integraci jsou změny kódu často sloučeny do hlavní větve. Automatizované procesy sestavení a testování zajišťují, že kód v hlavní větvi je vždy provozní kvalita. Tím je zajištěno, že vývojáři společně pracují na vývoji sdílených řešení, která poskytují přesné a spolehlivé smyčky zpětné vazby.

Azure DevOps a [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) poskytují možnosti průběžné integrace několika kliknutími, pro GitHub nebo pro celou řadu jiných úložišť.
Další informace najdete v části [průběžná integrace](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration) nebo v [praktickém testovacím prostředí](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration) . K urychlení tvorby [kanálů CI/CD s využitím Azure DevOps](https://azure.microsoft.com/solutions/devops)existují taky architektury řešení.

## <a name="reliable-testing"></a>Spolehlivé testování

Vady v jakémkoli řešení mohou vytvořit falešně pozitivní nebo falešně negativní výsledek. Neočekávané chyby mohou snadno vést k chybné interpretaci metrik přijetí uživateli. Může také vést k negativní zpětnou vazbu od zákazníků, kteří nedostatečně reprezentují test vaší hypotézy.

Během počátečních iterací řešení MVP jsou očekávané vady, kdy si je můžou endearing i první. V předčasném vydání bude testování přijetí pravděpodobně neexistující. Jednou z aspektů sestavování s soucit je ale ověření potřeby a hypotéz. Obojí lze dokončit prostřednictvím testů jednotek na úrovni kódu a ručních testů přijetí před nasazením. Dohromady tyto možnosti zajistí spolehlivost při testování. Dlouhodobě dobře definovaná řada testů sestavení, jednotek a přijetí by měla být automatizovaná, aby se zajistila spolehlivá metrika, která souvisí s přesnější úpravou zrnitosti pro hypotézu a výsledné řešení.

[Azure test Plans](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) poskytuje nástroje pro vývoj a provoz testovacích plánů během ručního nebo automatizovaného provádění testu.

## <a name="solution-deployment"></a>Nasazení řešení

Nejužitečnější aspekt oprávnění k přijetí je možná možnost řídit vydání řešení zákazníkům. Poskytnutí samoobslužné služby nebo automatizovaného kanálu pro vydání řešení zákazníkům urychluje smyčku zpětné vazby. Aby zákazníci mohli rychle komunikovat se změnami v řešení, pozve zákazníka do procesu. Umožňuje také rychlejší testy hypotéz, snižovat předpoklady a potenciální přepracování.

K nasazení řešení se používá několik přístupů, které představují tři nejběžnější přístupy:

- Nejpokročilejším přístupem, **průběžným nasazováním**, automaticky nasazuje změny kódu v produkčním prostředí. Pro vyspělé účely testování hypotézy může být průběžné nasazování velmi cenné.
- V počátečních fázích vývoje může být **průběžné doručování** vhodnější. Při průběžném doručování se všechny změny kódu automaticky nasadí do prostředí podobného produkčnímu prostředí. Vývojáři, tvůrci obchodních rozhodnutí a další členové týmu mohou použít toto prostředí k ověření, že je jejich práce připravená pro výrobu. Dá se použít i k otestování předpokladů se zákazníky, aniž by to ovlivnilo probíhající obchodní aktivity.
- **Ruční nasazení** je nejdéle pokročilý přístup k produktu Release Management. Jak název navrhuje, někdo v týmu ručně nasadí nejnovější změny kódu. Tento přístup je náchylný k chybám, nespolehlivě a považuje se za antipattern pomocí většiny sezónních technik.

Během první iterace řešení MVP je ruční nasazení běžným přístupem, a to navzdory výše uvedenému popisu. Když je řešení extrémně kapalina a zpětná vazba od zákazníka není známa, existuje významné riziko resetování celého řešení (nebo dokonce základní hypotéza). Obecné pravidlo pro ruční nasazení: žádné potvrzení od zákazníka, žádné automatizace nasazení. Investice do začátku může vést ke ztrátě času. Důležitější je, že může vytvořit závislosti v kanálu vydávání verzí, aby byl tým více odolný vůči předčasnému pivotu. Po prvních několika iteracích nebo v případě, že zpětná vazba od zákazníků navrhuje potenciální úspěch, je třeba rychle přijmout pokročilejší model nasazení.

V jakékoli fázi ověřování předpokladů poskytuje Azure DevOps a [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) možnosti průběžného doručování a průběžného nasazování pouhým několika kliknutími. Další informace o [průběžném doručování](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery) nebo práci prostřednictvím [praktického laboratorního prostředí](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment) najdete v praxi. Architektury řešení také můžou urychlit vytváření [kanálů CI/CD pomocí Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="integrated-measurements"></a>Integrovaná měření

Při [měření na dopad zákazníků](./measure.md)je důležité pochopit, jak zákazníci reagují na změny v řešení. Tato data, označovaná jako telemetrie, poskytují přehled o akcích, které při použití tohoto řešení využívají (nebo kohorta uživatele). Z těchto dat je snadné získat kvantitativní ověření hypotézy. Tyto metriky pak můžete použít k úpravě řešení a k vygenerování přesnější hypotézy. Tyto jemný změny pomůžou pořídit počáteční řešení v následných iteracích, čímž se při současném řízení opakuje i jejich opětovné přijetí.

V Azure [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) poskytuje nástroje a rozhraní pro shromažďování a kontrolu dat ze zkušeností zákazníků. Tyto poznámky a poznatky lze použít k upřesnění nevyřízených položek pomocí [Azure boards](https://docs.microsoft.com/azure/devops/boards).

## <a name="next-steps"></a>Další kroky

S porozuměním nástrojům a procesům, které jsou potřeba k tomu, abychom mohli přijmout, je čas kontrolovat pokročilejší pravidla inovace a [komunikovat se zařízeními](./devices.md). Což může přispět ke snížení bariér mezi fyzickými a digitálními prostředími, takže je vaše řešení ještě snazší.

> [!div class="nextstepaction"]
> [Interakce se zařízeními](./devices.md)
