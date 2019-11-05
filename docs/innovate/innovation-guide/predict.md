---
title: 'Průvodce inovacemi Azure: Predikce a ovlivňování'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se předpovídat a ovlivňovat využití Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 5bd467e6e74ff1289a7db40add87a049d2b0697e
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/29/2019
ms.locfileid: "73047621"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Průvodce inovacemi Azure: Predikce a ovlivňování

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Predikce a ovlivňování

::: zone-end

Jako inovátorská společnost máte přehled o datech, chování a potřebách své zákaznické základny. Rozbor těchto analytických údajů vám může usnadnit předvídání potřeb vašich zákazníků, a to možná ještě dříve, než si je sami uvědomí. Tento článek představuje několik přístupů k zajištění prediktivních řešení. V závěrečných částech se seznámíte s postupy pro integraci předpovědí do vašeho řešení, abyste mohli ovlivňovat chování zákazníků.

Následující tabulka vám může pomoct najít nejlepší řešení na základě vašich implementačních potřeb.

|Služba  |Předdefinované modely  |Sestavení a experimentování  |Trénování a vytváření v Pythonu|Požadované dovednosti|
|---------|---------|---------|---------|---------|
|Azure Cognitive Services|Ano|Ne|Ne|Dovednosti v oblasti rozhraní API a vývojářské dovednosti|
|Azure Machine Learning Studio|Ano|Ano|Ne|Obecné pochopení prediktivních algoritmů|
|Služba Azure Machine Learning|Ano|Ano|Ano|Odborník přes data|

## <a name="azure-cognitive-servicestabcognitiveservices"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Nejrychlejší a nejjednodušší cestu k předvídání potřeb zákazníků představují služby Azure Cognitive Services. Služba Cognitive Services umožňuje vytváření předpovědí na základě existujících modelů, aniž by bylo nutné nějaké další trénování. Tyto služby jsou optimální a efektivní, pokud v týmu není žádný odborník přes data, který by mohl prediktivní model natrénovat. U některých služeb není žádné trénování nutné. Další služby vyžadují jenom minimální trénování.

Seznam dostupných služeb a požadovaný rozsah trénování najdete v tématu [Cognitive Services a strojové učení](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Akce

Použití rozhraní API služeb Cognitive Services:

1. Na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts) přejděte do části **Cognitive Services**.
2. Vyberte **Přidat** a na webu Azure Marketplace vyhledejte rozhraní API služeb Cognitive Services.
3. Proveďte jednu z následujících akcí:
   * Pokud znáte název služby, kterou chcete použít, zadejte ho do pole **Hledat na Marketplace**.
   * Pokud chcete zobrazit seznam rozhraní API služeb Cognitive Services, vyberte odkaz **Zobrazit více** vedle nadpisu Cognitive Services.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Přejděte přímo na Cognitive Services na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts).

::: zone-end

## <a name="azure-machine-learning-studiotabmachinelearningstudio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Pokud existující modely v rámci služeb Cognitive Services neodpovídají vámi požadovaným predikcím, pak možnost, jak tyto předpovědi sestavit, aniž by to vyžadovalo hluboké znalosti v oblasti datových věd, může představovat Azure Machine Learning Studio.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Pomocí nástroje Azure Machine Learning Studio můžete následujícím způsobem vytvořit model a experimentovat s ním:

1. Na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces) přejděte do části **Azure Machine Learning Studio**.
2. Vyberte **Vytvořit pracovní prostor Machine Learning Studio** a pak podle zobrazených výzev vytvořte pracovní prostor.

   Nový pracovní prostor poskytuje rozhraní podporující přetahování, které umožňuje vytvořit model a experimentovat s ním – jde o alternativu k podrobnému tréninku.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Přejděte přímo na Azure Machine Learning Studio na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces).

::: zone-end

## <a name="azure-machine-learning-servicetabmachinelearningservice"></a>[Služba Azure Machine Learning](#tab/MachineLearningService)

Azure Machine Learning Service poskytuje hlubší přístup založený na kódu, který je nutný k podrobnějšímu trénování podle zákaznických datových sad. Odborníci přes data můžou algoritmus, který bude předpovídat potřeby zákazníků, natrénovat a vytvořit pomocí jazyka, jako je Python.

### <a name="action"></a>Akce

Odborník přes data může pomocí služby Azure Machine Learning Service natrénovat a sestavit model s použitím pokročilého jazyka, jako je Python:

1. Přejděte do služby **Azure Machine Learning Service**.
2. Vyberte **Vytvořit pracovní prostory služby Machine Learning Service** a podle zobrazených výzev vytvořte pracovní prostor.
3. Nový pracovní prostor představuje metodu založenou na kódu, kterou můžou odborníci přes data využít k trénování a sestavování modelů vyžadujících pokročilejší analýzy pro přesné předpovědi potřeb zákazníků.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces]" submitText="Go to Azure Machine Learning service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Přejděte přímo na Azure Machine Learning Studio na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces).

::: zone-end

## <a name="influence"></a>Vliv

Všechny výše uvedené přístupy vedou k vytvoření rozhraní API, které bude zveřejňovat prediktivní model pro aplikace. V rámci svého řešení použijte libovolný z těchto přístupů k načítání dat shromážděných od vašich zákazníků do prediktivního rozhraní API. Výsledky je pak možné integrovat do zákaznického prostředí, což navrhujeme jako další krok.

Tyto navrhované další kroky můžou pomoct modelovat vzory chování zákazníků a ovlivnit, jak zákazníci reagují. Vzhledem k tomu, že navrhované další kroky jsou založené na prediktivních algoritmech, využívají předchozí potřeby zákazníků a dostupná data k predikci a uspokojování budoucích potřeb zákazníků, a to často ještě předtím, než si je uvědomí sami zákazníci.
