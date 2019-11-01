---
title: 'Inovace v cloudu: předpověď a vliv'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do cloudových inovací – předpověď a vliv
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 83165e21882b4979d0fb3b104fa4f2c12aed326c
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239464"
---
# <a name="predict-and-influence"></a>Predikce a ovlivňování

V digitálním hospodářství jsou dvě třídy aplikací: historické a prediktivní. Mnoho zákaznických potřeb je možné splnit výhradně pomocí historických dat, včetně dat téměř v reálném čase. Většina řešení se zaměřuje primárně na agregaci dat, a to v okamžiku. Pak tato data zpracovávají a sdílejí je zpátky zákazníkovi ve formě digitálního nebo okolního prostředí.

Protože prediktivní modelování se bude cenově výhodnější a snadno dostupné, nabízí zákazníkům možnost dopředné prostředí, které vede k lepším rozhodnutím a akcím. Nicméně tato poptávka nemusí vždy vést k prediktivnímu řešení. Ve většině scénářů může historický pohled poskytnout dostatečné množství dat, aby zákazník mohl učinit rozhodnutí sám o sobě.

Zákazníci bohužel mají myopic zobrazení, které vede k rozhodnutím na základě jejich bezprostředního okolí a oblasti vlivu. V důsledku možností a rozhodování o růstu čísel a dopadu nemusí myopic zobrazení vést ke splnění potřeb zákazníka. Ve stejnou dobu, protože předpoklad je ve velkém měřítku, společnost poskytující řešení uvidí v tisících nebo milionech rozhodnutí o zákaznících. Je možné vidět vzory a dopady těchto vzorů. Prediktivní funkce je moudrá investice, pokud je potřeba pochopit tyto vzory, aby bylo možné učinit rozhodnutí, která vyhovují potřebám zákazníků.

## <a name="examples-of-predictions-and-influence"></a>Příklady předpovědi a vlivu

Použití dat k zajištění předpovědi lze zobrazit v různých aplikacích a okolí.

- **elektronického obchodování:** Navrhované položky jsou příklad předpovědi. Na základě toho, co si jiní koupili dohromady, může web navrhnout produkty, které mohou být přidávány do košíku.
- **Upravená realita:** IoT nabízí další příklady předběžných. Jedno zařízení na řádku sestavení zjistí nárůst teploty počítačů. Způsob, jak reagovat, určuje cloudový model prediktivního škálování. Na základě této předpovědi má jiné zařízení pokyn zpomalit čáru sestavení, dokud se počítač nedokáže vychladnout.
- **Zákaznické produkty:** Mobilní telefony, chytré domy, dokonce i vaše auto obsahují určitou stupeň prediktivních funkcí, které navrhují aktivity na základě faktorů, jako je umístění nebo denní doba. V případě, že předpověď a počáteční hypotéza jsou zarovnány, mají tyto předpovědi vliv na vaše chování. Když se obě stanou hodně vyspělé, předpovědi vede k akci, jako je například autohnací auto.

## <a name="developing-predictive-capabilities"></a>Vývoj prediktivních funkcí

Řešení, která konzistentně poskytují přesné prediktivní funkce, mají obvykle pět základních charakteristik: data, přehledy, vzory, předpovědi a interakce. Každý je vyžadován pro vývoj prediktivních schopností. Stejně jako všechny skvělé inovace bude vývoj prediktivních funkcí vyžadovat [závazek k iteraci](./index.md#commitment-to-iteration). V každé iteraci by bylo možné provést jednu nebo více následujících vlastností a ověřit stále složitou hypotézu zákazníka.

![Kroky k prediktivním funkcím](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Pokud zákazníková hypotéza vyvinutá v článku [Build with Customer soucit](./build.md) zahrnuje prediktivní možnosti, může se tento článek použít. Ale prediktivní funkce vyžadují významnou investici času a energie. Pokud jsou v případě prediktivních schopností [technické špičky](./build.md#reduce-complexity-and-delay-technical-spikes)na rozdíl od zdroje dosažitelné hodnoty zákazníků, navrhne se zpoždění předpovědi až do doby, kdy se u zákazníka hypotézy ověřuje škálování.

## <a name="data"></a>Data

Nejjednodušší z výše uvedených charakteristik je data. Všechny předchozí obory pro vývoj digitálních vynálezů budou generovat data. Tato data můžou přispět ke vývojům předpovědi. Další informace o tom, jak získat data do prediktivního řešení, najdete v článcích o [democratizing datech](./data.md) nebo při [komunikaci se zařízeními](./devices.md).

K disřadě zdrojů dat lze použít k zajištění prediktivních funkcí:

## <a name="insights"></a>Poznatky

Odborníci na danou problematiku využívají data týkající se potřeb zákazníků a chování při vývoji základních obchodních přehledů z studie nezpracovaných dat. Tyto přehledy můžou určit výskyty požadovaného chování zákazníka (nebo alternativní nežádoucí výsledky). Během iterací na předpovědi můžou tyto přehledy pomoci při identifikaci potenciálních korelačních, což by mohlo mít nepříznivý vliv na pozitivní výsledky. Pokyny k tomu, aby odborníci na danou problematiku mohli vyvíjet přehledy, najdete v článku o [democratizing datech](./data.md).

## <a name="patterns"></a>Vzory

Člověkem, který je v podstatě bojovat s detekcí vzorů napříč velkými objemy dat. Počítače byly navrženy pro tento účel. Machine Learning zrychluje tento účel prostřednictvím detekce vzorů napříč velkým množstvím dat, označovaných jako model strojového učení. Tyto vzory se pak použijí prostřednictvím algoritmů strojového učení, abyste předpovídat, co se stane při zadání nové sady datových bodů do algoritmů.

Použití přehledů jako výchozího bodu, strojového učení vlaků a používání prediktivních modelů na data pro použití ve vzorcích dat. Pomocí několika iterací školení, testování a přijetí tyto modely a algoritmy můžou přesně předpovídat budoucí výsledky.

[Služba Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) je nativní cloudový nástroj v Azure pro vytváření a školení modelů na základě vašich dat. Tento nástroj zahrnuje také [pracovní postup pro urychlení vývoje algoritmů strojového učení](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Tento pracovní postup lze použít k vývoji algoritmů pomocí vizuálního rozhraní nebo Pythonu.

V případě robustnějších modelů strojového učení poskytuje [Služba ml služby ve službě Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) platformu strojového učení založenou na Apache Hadoopch clusterech. Tento přístup umožňuje podrobnější kontrolu nad základními clustery, úložištěm a výpočetními uzly. Využití Azure HDInsight taky nabízí větší integraci prostřednictvím nástrojů, jako je například nástroj pro škálování a Spark, k vytvoření předpovědi založeného na integrovaných a ingestných datech, a to i v případě práce s daty z datového proudu. [Řešení předpovědi zpoždění letu](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) předvádí každou z těchto pokročilých možností a předpovídá zpoždění letů na základě povětrnostních podmínek. Řešení HDInsight také umožňuje podnikovým ovládacím prvkům, jako jsou zabezpečení dat, přístup k síti a monitorování výkonu, zprovoznění vzory.

## <a name="predictions"></a>Predikce

Jakmile je vzor sestavený a vycvičený, dá se použít pomocí rozhraní API, které může předpovědi při doručování digitálního prostředí. Většina těchto rozhraní API je postavená z dobře vycvičeného modelu na základě vzoru v rámci vašich dat. I když ale více zákazníků nasazuje běžné úlohy do cloudu, poskytovatelé cloudu můžou poskytnout společná rozhraní API pro rychlejší přijímání předpovědi.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) je příkladem prediktivního sestavení API od dodavatele cloudu. Tato služba zahrnuje prediktivní rozhraní API pro moderování obsahu, detekci anomálií nebo návrhy na přizpůsobení obsahu. Tato rozhraní API jsou připravená k použití v závislosti na běžných vzorech obsahu, které Microsoft použil k proškolování modelů. Každé z těchto rozhraní API předpovědi na základě dat, která zadáváte do rozhraní API.

[Služba Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning) umožňuje nasazení uživatelsky sestavených algoritmů, které můžete vytvořit a naučit se výhradně na základě vašich vlastních dat. Další informace o nasazení předpovědi pomocí Azure Machine Learning najdete [tady](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

Článek o [Nastavení clusterů HDInsight popisuje procesy pro vystavení](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) předpovědi vyvinutých pro služby ml ve službě Azure HDInsight.

## <a name="interactions"></a>Interakce

Jakmile je předpověď zpřístupněna prostřednictvím rozhraní API, předpovědi lze použít k ovlivnění chování zákazníků. Takový vliv přichází do formy interakcí. Interakce s algoritmem strojového učení se odehrává v rámci vašich jiných digitálních nebo okolních prostředí. Při shromažďování dat prostřednictvím aplikace nebo zkušeností se data spouštějí prostřednictvím algoritmů strojového učení. Když algoritmus předpovídá výsledek, může být předpověď zpětně sdílena se zákazníkem prostřednictvím stávajícího prostředí.

Přečtěte si další informace o interakcích v rámci [upraveného řešení realit](./devices.md#adjusted-reality), kde najdete další podrobnosti o vytváření interakce v prostředí okolí.

## <a name="next-steps"></a>Další kroky

Na základě znalostí získaných v souvislosti s [disciplínami vynálezy](./invention.md) v rámci [metodologie inovací](./index.md) víte, že máte k dispozici technické nástroje vyžadované k [sestavování pomocí soucit](./build.md).

> [!div class="nextstepaction"]
> [Sestavení pomocí soucit](./build.md)
