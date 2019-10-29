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
ms.openlocfilehash: b2ed1b072d5226649e5248e350edfa3578978c4c
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769244"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Průvodce inovacemi Azure: Predikce a ovlivňování

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Predikce a ovlivňování

::: zone-end

Jste inovátorská společnost, a proto chcete mít přehled o datech, chování a potřebách své zákaznické základny. Rozbor těchto analytických údajů vám může usnadnit předvídání potřeb vašich zákazníků, a to ještě než si je uvědomí oni sami. Tento článek představuje několik přístupů k zajištění prediktivních řešení. V pozdější části se seznámíte s postupy pro integraci těchto předpovědí do vašeho řešení, abyste mohli ovlivňovat chování zákazníků.

Následující tabulka je navržená tak, aby vám pomohla najít nejlepší řešení na základě vašich implementačních potřeb.

|Služba  |Předdefinované modely  |Sestavení a experimentování  |Trénování a vytváření v Pythonu|Požadované dovednosti|
|---------|---------|---------|---------|---------|
|Cognitive Services|Ano|Ne|Ne|Dovednosti v oblasti rozhraní API a vývojářské dovednosti|
|Azure Machine Learning Studio|Ano|Ano|Ne|Obecné pochopení prediktivních algoritmů|
|Služba Azure Machine Learning|Ano|Ano|Ano|Odborník na datové vědy|

## <a name="azure-cognitive-servicestabcognitiveservices"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Nejrychlejší a nejjednodušší cesta k předpovědím je služba Azure Cognitive Services. Služba Cognitive Services umožňuje vytváření předpovědí na základě existujících modelů, aniž by bylo nutné nějaké další trénování. Tyto služby jsou optimální, pokud v týmu není žádný odborník na datové vědy, který by mohl prediktivní model vytrénovat. U některých služeb není žádné trénování nutné. Jiné vyžadují jenom minimální trénink.

Seznam dostupných služeb a požadované množství trénování najdete v tématu [Cognitive Services a strojové učení](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Akce

Použití rozhraní API kognitivní služby:

1. Přejděte na **Kognitivní služby**.
2. Pokud chcete najít kognitivní službu na webu Marketplace, klikněte na **Přidat+** .
3. Pokud název služby, kterou chcete použít, znáte, můžete ho zadat v textovém poli **Hledat na Marketplace**.
4. Případně si můžete zobrazit seznam kognitivních služeb, a to kliknutím na odkaz **Zobrazit více** vedle hlavičky Kognitivní služby.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Přejděte přímo na Cognitive Services na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts).

::: zone-end

## <a name="azure-machine-learning-studiotabmachinelearningstudio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Pokud existující modely v rámci kognitivních služeb neodpovídají vámi požadovaným predikcím, pak možnost, jak tyto předpovědi sestavit, aniž by to vyžadovalo hluboké znalosti v oblasti datových věd, může představovat Azure Machine Learning Studio.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akce

Pomocí služby Azure Machine Learning Studio můžete vytvořit model a experimentovat s ním:

1. Přejděte na **Azure Machine Learning Studio**.
2. Klikněte na **Vytvořit pracovní prostor Machine Learning Studio** a podle pokynů vytvořte pracovní prostor.
3. Nový pracovní prostor poskytuje rozhraní s podporou přetahování myší, které umožňuje sestavení modelu a experimentování s ním – jde o alternativu k podrobnému tréninku.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Přejděte přímo na Azure Machine Learning Studio na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces).

::: zone-end

## <a name="azure-machine-learning-servicetabmachinelearningservice"></a>[Azure Machine Learning Service](#tab/MachineLearningService)

Azure Machine Learning Service poskytuje hlubší přístup založený na kódu, který je nutný k detailnějšímu trénování podle zákaznických datových sad. Odborníci na datové vědy můžou algoritmus, který bude předpovídat potřeby zákazníků, vytvořit pomocí jazyků, jako je Python.

### <a name="action"></a>Akce

Odborník na datové vědy může pomocí Azure Machine Learning Service vytrénovat a sestavit model s použitím pokročilého jazyka, jako je Python:

1. Přejděte na **Azure Machine Learning Service**.
2. Klikněte na **Vytvořit pracovní prostory služby Machine Learning** a podle pokynů vytvořte pracovní prostor.
3. Nový pracovní prostor představuje metodu založenou na kódu, kterou můžou odborníci na datové vědy využít k vytrénování a sestavení modelů vyžadujících pokročilejší analýzy pro přesné předpovědi potřeb zákazníků.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces]" submitText="Go to Azure Machine Learning Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Přejděte přímo na Azure Machine Learning Studio na webu [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces).

::: zone-end

## <a name="influence"></a>Vliv

Všechny výše uvedené přístupy vedou k vytvoření rozhraní API, které bude zveřejňovat prediktivní model pro aplikace. V rámci svého řešení použijte libovolný z těchto přístupů k načítání dat nasbíraných u vašich zákazníků do prediktivního rozhraní API. Výsledky je pak možné integrovat do zákaznického prostředí, což navrhujeme jako další krok.

Tyto další kroky zahrnují snahu modelovat vzory chování zákazníků a ovlivnit, jak zákazník zareaguje. Vzhledem k tomu, že navrhované další kroky jsou založené na prediktivních algoritmech, budou využívat předchozí zákaznická a další dostupná data k predikci a uspokojování potřeb zákazníků, a to ještě předtím, než si je zákazník uvědomí.
