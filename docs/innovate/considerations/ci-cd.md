---
title: 'Cloud innovation: Empower adoption'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduction to Cloud innovation - Empower adoption
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 8828b79aa27083b3b3e0a0188ac9e538089c52cf
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058584"
---
# <a name="empower-adoption"></a>Posílení přechodu

The ultimate test of innovation is customer reaction to your invention. Did the hypothesis prove true? Do customers use the solution? Does it scale to meet the needs of the desired percentage of users? Most importantly, do they keep coming back? None of these questions can be asked until the minimum viable product (MVP) solution has been deployed. In this article, we'll focus on the discipline of empowering adoption.

## <a name="reducing-friction-to-adoption"></a>Reducing friction to adoption

There are a few key friction points to adoption that can be minimized through a combination of technology and processes. For readers with knowledge of continuous integration (CI) and continuous deployment (CD) or DevOps processes, the following will seem very familiar. This article intends to establish a starting point for cloud adoption teams, which will fuel innovation and feedback loops. Longer term, this starting point could foster more robust CI/CD or DevOps approaches as the products and teams mature.

As described in [Measure for customer impact](./measure.md), positive validation of any hypothesis requires iteration and determination. You'll experience far more failures than wins during any innovation cycle. To se očekává. However, when a customer need, hypothesis, and solution align at scale, the world changes quickly. This article aims to minimize [technical spikes](./build.md#reduce-complexity-and-delay-technical-spikes) that slow innovation but still make sure you keep a few solid best practices in place. Doing so will help the team design for future success while delivering on current customer needs.

## <a name="empowering-adoption-the-maturity-model"></a>Empowering adoption: the maturity model

The primary objective of the [Innovate methodology](./index.md) is to build customer partnerships and accelerate feedback loops, which will lead to market innovations. The following image and sections describe initial implementations that support this methodology.

![Empower adoption: the maturity model](../../_images/innovate/empower-adoption-maturity.png)

- [Shared solution](#shared-solution): Establish a centralized repository for all aspects of the solution.
- [Feedback loops](#feedback-loops): Make sure that feedback loops can be managed consistently through iterations.
- [Continuous integration](#continuous-integration): Regularly build and consolidate the solution.
- [Reliable testing](#reliable-testing): Validate solution quality and expected changes to ensure the reliability of your testing metrics.
- [Solution deployment](#solution-deployment): Deploy solutions so that the team can quickly share changes with customers.
- [Integrated measurement](#integrated-measurements): Add learning metrics to the feedback loop for clear analysis by the full team.

To minimize technical spikes, assume that maturity will initially be low across each of these principles. But definitely plan ahead by aligning to tools and processes that can scale as hypotheses become more fine-grained. In Azure, the [GitHub](https://guides.github.com) and [Azure DevOps](https://docs.microsoft.com/azure/devops) allow small teams to get started with little friction. These teams might grow to include thousands of developers who collaborate on scale solutions and test hundreds of customer hypotheses. The remainder of this article illustrates the plan big/start small approach to empowering adoption across each of these principles.

## <a name="shared-solution"></a>Sdílené řešení

As described in [Measure for customer impact](./measure.md), positive validation of any hypothesis requires iteration and determination. You'll experience far more failures than wins during any innovation cycle. To se očekává. However, when a customer need, hypothesis, and solution align at scale, the world changes quickly.

Při škálování inovace není k dispozici žádný hodnotný nástroj než sdílený základ kódu pro řešení. Bohužel neexistuje spolehlivý způsob, jak předpovídat tuto iteraci, nebo který MVP poskytne vítěznou kombinaci. To je důvod, proč není nikdy příliš brzy pro vytvoření sdíleného základu kódu nebo úložiště. Toto je [technický technický špička](./build.md#reduce-complexity-and-delay-technical-spikes) , který by se nikdy neměl zpozdit. Když tým projde různými řešeními MVP, sdílené úložiště umožňuje snadnou spolupráci a urychlení vývoje. Když změny řešení přetáhnete dolů metriky učení, Správa verzí vám umožní vrátit se zpět na dřívější, účinnější verzi řešení.

Nejpoužívanějším nástrojem pro správu úložišť kódu je [GitHub](https://guides.github.com), který umožňuje vytvořit úložiště se sdíleným kódem jen několika kliknutími. Kromě toho je možné pomocí funkce [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) služby Azure DevOps vytvořit úložiště [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) nebo [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="feedback-loops"></a>Smyčky zpětné vazby

Tím, že se zákazník stane součástí řešení, je klíč k sestavování zákaznických partnerství během inovačních cyklů. To je v rámci [měření dopadu na zákazníky](./measure.md)dokončeno. Vyžaduje konverzace a přímé testování u zákazníka. Vygenerujte zpětnou vazbu, která musí být spravována efektivně.

Každý bod zpětné vazby je potenciální řešení pro potřeby zákazníka. Důležitější je, že každý bit zpětné vazby od zákazníka představuje příležitost ke zlepšení partnerství. Pokud je vaše zpětná vazba k řešení MVP, Oslavte si zákazníka. I v případě, že některá zpětná vazba není nenapadnutelná, stačí jednoduše transparentní s rozhodnutím o deprioritování zpětné vazby ukazující [růst místo](./learn.md#growth-mindset) a zaměřit se na [průběžné učení](./learn.md#continuous-learning).

[Azure DevOps](https://docs.microsoft.com/azure/devops) obsahuje způsoby [, jak vyžádat, poskytnout a spravovat zpětnou vazbu](https://docs.microsoft.com/azure/devops/project/feedback). Každý z těchto nástrojů slouží k centralizaci zpětné vazby, aby tým mohl provádět akce a poskytoval následný postup ve službě transparentní smyčky zpětné vazby.

## <a name="continuous-integration"></a>Nepřetržitá integrace

Vzhledem k tomu, že se přijímají škálování a hypotéza se přiblíží k skutečným inovacím ve velkém měřítku, může být počet menších hypotéz, který se má testovat, rychlejší rychleji. Pro přesné smyčky zpětné vazby a hladké procesy přijetí je důležité, aby každá z těchto hypotéz byla integrovaná a podpora primární hypotézy na základě inovace. To znamená, že se také musíte rychle přesunout na inovace a růst, což vyžaduje více vývojářů pro testování variací základní hypotézy. Pro účely pozdějšího vývoje můžete dokonce potřebovat více týmů vývojářů, přičemž každá z nich bude sdílet řešení. Nepřetržitá integrace je prvním krokem ke správě všech přesouvaných částí.

V nepřetržité integraci jsou změny kódu často sloučeny do hlavní větve. Automatizované procesy sestavení a testování zajistí, že kód v hlavní větvi je vždy provozní kvalita. Tím je zajištěno, že vývojáři společně pracují na vývoji sdílených řešení, která poskytují přesné a spolehlivé smyčky zpětné vazby.

Azure DevOps a [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) poskytují možnosti nepřetržité integrace jenom několika kliknutími na GitHubu nebo v nejrůznějších úložištích.
Další informace o [průběžné integraci](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration)nebo další informace najdete v [praktickém testovacím prostředí](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration). K urychlení tvorby [kanálů CI/CD prostřednictvím Azure DevOps](https://azure.microsoft.com/solutions/devops)existují taky architektury řešení.

## <a name="reliable-testing"></a>Spolehlivé testování

Vady v jakémkoli řešení mohou vytvořit falešně pozitivní nebo falešně negativní výsledek. Neočekávané chyby mohou snadno vést k chybné interpretaci metrik přijetí uživateli. Můžou také vygenerovat negativní zpětnou vazbu od zákazníků, kteří nepřesně reprezentují test vaší hypotézy.

Během počátečních iterací řešení MVP se očekávají vady; Začátky můžou je dokonce najít endearing. V dřívějších verzích je testování přijetí obvykle neexistující. Jeden aspekt sestavování s soucit se ale bude týkat ověření potřeb a hypotéz. Obojí lze dokončit prostřednictvím testů jednotek na úrovni kódu a ručních testů přijetí před nasazením. Dohromady tyto prostředky poskytují spolehlivost při testování. S delší dobou byste se měli snažit automatizovat dobře definovanou řadu testů sestavení, jednotek a přijetí. Tím zajistíte spolehlivé metriky související s podrobnějším vylepšením pro hypotézu a výsledné řešení.

Funkce [Azure test Plans](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) poskytuje nástroje pro vývoj a provoz testovacích plánů během ručního nebo automatizovaného provádění testu.

## <a name="solution-deployment"></a>Nasazení řešení

Nejužitečnější aspekt, který umožňuje přijetí, je možná vaše možnost řídit vydání řešení zákazníkům. Poskytnutím samoobslužné služby nebo automatizovaného kanálu pro vydání řešení zákazníkům urychlíte smyčku zpětné vazby. Když zákazníkům umožníte rychle pracovat se změnami v řešení, budete je zvát do procesu. Tento přístup také aktivuje rychlejší testování hypotéz. tím se snižuje předpoklady a potenciální repráce.

Existuje několik metod pro nasazení řešení. Následující představuje tři nejběžnější:

- **Průběžné nasazování** je nejrozšířenější způsob, jak automaticky nasazuje změny kódu v produkčním prostředí. Pro vyspělé týmy, které testují vyspělé hypotézy, může být průběžné nasazování velmi cenné.
- V počátečních fázích vývoje může být **průběžné doručování** vhodnější. Při průběžném doručování se všechny změny kódu automaticky nasadí do prostředí podobného produkčnímu prostředí. Vývojáři, tvůrci obchodních organizací a další členové týmu mohou použít toto prostředí k ověření, že je jejich práce připravená na provoz. Tuto metodu můžete také použít k otestování předpokladů se zákazníky, aniž by to mělo vliv na obchodní aktivity.
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
