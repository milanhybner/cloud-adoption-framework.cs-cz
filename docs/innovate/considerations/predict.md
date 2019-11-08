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
ms.openlocfilehash: bcb01ada3589b733fe97de2689352ab414ef469b
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752980"
---
# <a name="predict-and-influence"></a>Predikce a ovlivňování

V digitálním hospodářství jsou dvě třídy aplikací: *historické* a *prediktivní*. Mnoho zákaznických potřeb je možné splnit výhradně pomocí historických dat, včetně téměř dat v reálném čase. Většina řešení se zaměřuje hlavně na agregaci dat v daném okamžiku. Pak tato data zpracovávají a sdílejí je zpátky zákazníkovi ve formě digitálního nebo okolního prostředí.

Protože prediktivní modelování bude cenově výhodnější a snadno dostupné, zákazníci si můžou přesměrovat prostředí, které vede k lepším rozhodováním a akcím. Tato poptávka ale vždy nenavrhuje prediktivní řešení. Ve většině případů může historický pohled poskytnout dostatečné množství dat, aby si zákazník mohl učinit rozhodnutí sami.

Zákazníci si bohužel často myopic zobrazení, které vede k rozhodnutím na základě jejich bezprostředního okolí a oblasti vlivu. Vzhledem k možnostem a rozhodnutím roste počet a dopad, takže zobrazení myopic nemusí sloužit potřebám zákazníka. Ve stejnou dobu, protože předpoklad je ve velkém měřítku, společnost poskytující řešení uvidí v tisících nebo milionech rozhodnutí o zákaznících. Tento přístup ve velkém obrazu umožňuje zobrazit široké vzory a dopady těchto vzorů. Prediktivní funkce je moudrá investice, pokud je potřeba pochopit tyto vzory, aby bylo možné učinit rozhodnutí, která zákazníkům nejlépe obsluhují.

## <a name="examples-of-predictions-and-influence"></a>Příklady předpovědi a vlivu

Nejrůznější aplikace a okolní prostředí využívají data k zajištění předpovědi:

- **Elektronické obchodování:** Na základě toho, co si koupili jiní uživatelé, nabízí web elektronického obchodování produkty, které se dají přidat do košíku.
- **Upravená realita:** IoT nabízí pokročilejší instance prediktivních funkcí. Například zařízení na řádku sestavení zjistí nárůst teploty počítače. Způsob, jak reagovat, určuje cloudový model prediktivního škálování. Na základě této předpovědi jiné zařízení zpomaluje čáru sestavení, dokud se počítač nedokáže vychladnout.
- **Zákaznické produkty:** Mobilní telefony, chytré domy, dokonce i vaše auto, které používají prediktivní možnosti, které využívají k návrhu chování uživatelů na základě faktorů, jako je umístění nebo denní doba. V případě, že předpověď a počáteční hypotéza jsou zarovnány, předpovědi vede k akci. V rámci velmi vyspělé fáze může toto zarovnání zajistit, aby produkty, jako je například samočinná hnací auto, mohly být realitou.

## <a name="develop-predictive-capabilities"></a>Vývoj prediktivních funkcí

Řešení, která konzistentně poskytují přesné prediktivní funkce, mají obvykle pět základních charakteristik: *data*, *přehledy*, *vzory*, *předpovědi*a *interakce*. Každý aspekt je nutný k vývoji prediktivních schopností. Stejně jako všechny skvělé inovace vyžaduje vývoj prediktivních funkcí [závazek na iteraci](./index.md#commitment-to-iteration). V každé iteraci je možné vymezit jednu nebo více následujících vlastností, které ověří stále složitou hypotézu zákazníka.

![Kroky k prediktivním funkcím](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Pokud zákazníková hypotéza vyvinutá v [buildu s využitím Customer soucit](./build.md) zahrnuje prediktivní možnosti, může to znamenat i tyto principy. Prediktivní funkce ale vyžadují významnou investici času a energie. Pokud jsou pro prediktivní funkce [technické špičky](./build.md#reduce-complexity-and-delay-technical-spikes)na rozdíl od zdroje reálné hodnoty zákazníka, doporučujeme, abyste zpozdili předpovědi, dokud se neověří hypotéza zákazníka ve velkém měřítku.

## <a name="data"></a>Data

Data jsou nejvíce prvky výše zmíněných vlastností. Každé z oborů pro vývoj digitálních vynálezů generuje data. Tato data samozřejmě přispívají k vývoji předpovědi. Další informace o tom, jak získat data do prediktivního řešení, najdete v tématu [Democratizing data](./data.md) a [interakce se zařízeními](./devices.md).

K disřadě zdrojů dat lze využít k zajištění prediktivních funkcí:

## <a name="insights"></a>Poznatky

Odborníci na danou problematiku využívají data týkající se potřeb zákazníků a chování při vývoji základních obchodních přehledů z studie nezpracovaných dat. Tyto přehledy můžou určit výskyty požadovaného chování zákazníka (nebo případně nežádoucí výsledky). Během iterací na předpovědi můžou tyto přehledy pomoci při identifikaci potenciálních relací, které by mohly nakonec vygenerovat pozitivní výsledky. Pokyny k povolení odborníků na danou problematiku pro vývoj přehledů najdete v tématu [Democratizing data](./data.md).

## <a name="patterns"></a>Vzory

Lidé se vždycky pokusili detekovat vzory ve velkých objemech dat. Počítače byly navrženy pro tento účel. Machine Learning zrychluje toto zjišťování tak, že detekuje přesně takové vzory, dovednosti, které zahrnují model strojového učení. Tyto vzory se pak aplikují prostřednictvím algoritmů strojového učení k předpovědi výsledků při zadání nové sady dat do algoritmů.

S využitím přehledů jako výchozího bodu vyvíjí strojové učení a aplikuje prediktivní modely na velká písmena na vzorcích dat. Díky více iteracím školení, testování a přijetí můžou tyto modely a algoritmy přesně předpovídat budoucí výsledky.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) je cloudová služba v Azure pro vytváření a školení modelů na základě vašich dat. Tento nástroj zahrnuje také [pracovní postup pro urychlení vývoje algoritmů strojového učení](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Tento pracovní postup lze použít k vývoji algoritmů prostřednictvím vizuálního rozhraní nebo Pythonu.

V případě robustnějších modelů strojového učení poskytuje [Služba ml služby ve službě Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) platformu strojového učení založenou na Apache Hadoopch clusterech. Tento přístup umožňuje podrobnější kontrolu nad základními clustery, úložištěm a výpočetními uzly. Azure HDInsight taky nabízí pokročilejší integraci prostřednictvím nástrojů, jako je například nástroj pro škálování a Spark, k vytváření předpovědi založeného na integrovaných a ingestných datech, a to i při práci s daty z datového proudu. [Řešení předpovědi zpoždění letu](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) ukazuje každou z těchto pokročilých funkcí, pokud se používá k předpovědi zpoždění letu na základě povětrnostních podmínek. Řešení HDInsight také umožňuje podnikovým ovládacím prvkům, jako jsou zabezpečení dat, přístup k síti a monitorování výkonu, zprovoznění vzory.

## <a name="predictions"></a>Predikce

Když je vzor sestavený a vycvičený, můžete ho použít prostřednictvím rozhraní API, které může předpovědi při doručování digitálního prostředí. Většina těchto rozhraní API je postavená z dobře vycvičeného modelu na základě vzoru ve vašich datech. Čím víc zákazníků nasadí každodenní úlohy do cloudu, předpovědi rozhraní API používaná poskytovateli cloudu vede k rychlejšímu přijetí.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) je příkladem PREDIKTIVNÍHO rozhraní API sestaveného dodavatelem cloudu. Tato služba zahrnuje prediktivní rozhraní API pro moderování obsahu, detekci anomálií a návrhy na přizpůsobení obsahu. Tato rozhraní API jsou připravená k použití a jsou založená na známých vzorech obsahu, které Microsoft použil k učení modelů. Každé z těchto rozhraní API vytváří předpovědi na základě dat, která zadáváte do rozhraní API.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning) umožňuje nasadit uživatelsky vytvořené algoritmy, které můžete vytvořit a naučit se výhradně na svých vlastních datech. Přečtěte si další informace o nasazení předpovědi pomocí [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

[Nastavení clusterů HDInsight popisuje procesy pro vystavení](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) předpovědi vyvinutých pro služby ml ve službě Azure HDInsight.

## <a name="interactions"></a>Interakce

Po zpřístupnění předpovědi prostřednictvím rozhraní API ji můžete použít k ovlivnění chování zákazníků. Tento vliv má formu interakcí. Interakce s algoritmem strojového učení se odehrává v rámci vašich jiných digitálních nebo okolních prostředí. Jelikož se data shromažďují prostřednictvím aplikace nebo zkušeností, běží prostřednictvím algoritmů strojového učení. Když algoritmus předpovídá výsledek, může být předpověď zpětně sdílena se zákazníkem prostřednictvím stávajícího prostředí.

Přečtěte si další informace o tom, jak vytvořit okolní prostředí prostřednictvím [upraveného řešení realit](./devices.md#adjusted-reality).

## <a name="next-steps"></a>Další kroky

Seznámili jste se s [obory vynálezu](./invention.md) a [metodologií](./index.md)inovace, teď jste připraveni zjistit, jak [sestavovat pomocí zákaznických soucit](./build.md).

> [!div class="nextstepaction"]
> [Sestavení pomocí soucit](./build.md)
