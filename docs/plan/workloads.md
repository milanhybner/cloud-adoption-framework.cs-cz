---
title: Určení priorit a definování úloh pro plán přijetí do cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Určení priorit a definování úloh pro plán přijetí do cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: d77a17af60c8ed4540b2c40ddf8d75a4e4f6f306
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833736"
---
# <a name="prioritize-and-define-workloads-for-a-cloud-adoption-plan"></a>Určení priorit a definování úloh pro plán přijetí do cloudu

Stanovení jasných a napadnutelných priorit je jedním z tajných kódů, aby bylo možné provést úspěšné přijetí do cloudu. Přirozeným pokušení je investovat čas do definování všech úloh, které by mohly být ovlivněné při přijetí cloudu. Ale to je counterproductive, zejména v rané fázi procesu přijetí.

Místo toho doporučujeme, aby se váš tým zaměřil na důkladné stanovení priorit a nadokumentování prvních 10 úloh. Po zahájení nasazení plánu přijetí může tým udržovat seznam dalších 10 úloh s nejvyšší prioritou. Tento přístup poskytuje dostatek informací pro plánování následujících několika iterací.

Omezení plánu na 10 úloh podporuje flexibilitu a zarovnání priorit při změně obchodních kritérií. Díky tomuto přístupu se taky snaží tým pro přijetí cloudu seznámit s odhadem a Upřesnit odhady. Nejdůležitějším způsobem je odebrání rozsáhlého plánování jako bariéra pro efektivní obchodní změnu.

## <a name="what-is-a-workload"></a>Co je zatížení?

V souvislosti s přijetím cloudu je zatížení kolekce prostředků IT (servery, virtuální počítače, aplikace, data nebo zařízení), které společně podporují definovaný proces. Úlohy mohou podporovat více než jeden proces. Úlohy můžou záviset i na dalších sdílených prostředcích a větších platformách. Pracovní vytížení ale by mělo mít definované hranice týkající se závislých prostředků a procesů, které závisí na zatížení. Úlohy je často možné vizuálně vymezit monitorováním síťového provozu mezi prostředky IT.

## <a name="prerequisites"></a>Požadavky

Strategické vstupy z kontrolního seznamu požadavků umožňují mnohem jednodušší provádění následujících úloh. Nápovědu k shromažďování dat popsaných v tomto článku najdete v [kontrolním seznamu požadovaných součástí](./prerequisites.md).

## <a name="initial-workload-prioritization"></a>Stanovení priorit počátečních úloh

Během postupu přírůstkového [racionalizace](../digital-estate/rationalize.md)by váš tým měl souhlasit s "výkonem 10" přístupu, který se skládá z 10 úloh priority. Tyto úlohy slouží jako počáteční hranice pro plánování přijetí.

Pokud se rozhodnete, že nepotřebujete racionalizaci digitální nemovitosti, doporučujeme, aby týmy pro přijetí v cloudu a tým cloudových strategií souhlasili se seznamem 10 aplikací, které budou sloužit jako prvotní zaměření migrace. Doporučujeme, aby tyto 10 úloh obsahovaly kombinaci jednoduchých úloh (méně než 10 prostředků v samostatném nasazení) a složitější úlohy. U těchto 10 úloh se spustí proces stanovení priorit úloh.

> [!NOTE]
> Mocnina 10 slouží jako počáteční hranice pro plánování a zaměřuje se na energii a investice do prvotní analýzy. Při analýze a definování úloh ale nejspíš dojde ke změnám v seznamu úloh priorit.

## <a name="add-workloads-to-your-cloud-adoption-plan"></a>Přidání úloh do plánu přijetí do cloudu

V předchozím článku [plán přijetí do cloudu a Azure DevOps](./template.md)jste v Azure DevOps vytvořili plán pro přijetí do cloudu.

Nyní můžete reprezentovat úlohy ve sílu 10 seznamu v plánu přijetí v cloudu. Nejjednodušší způsob, jak to provést, je hromadné úpravy v Microsoft Excelu. Informace o přípravě pracovní stanice pro hromadnou úpravu najdete v tématu [hromadné přidání nebo úprava pracovních položek pomocí aplikace Excel](/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Krok 5 v tomto článku vám ukáže, jak vybrat **Vstupní seznam**. Místo toho vyberte **seznam dotazů**. Pak v rozevíracím seznamu **Vybrat dotaz** vyberte dotaz **šablony úlohy** . Tento dotaz načte všechny úsilí související s migrací jedné úlohy do tabulky.

Po načtení pracovních položek pro šablonu úlohy proveďte následující kroky a začněte přidávat nové úlohy:

1. Zkopírujte všechny položky, které mají značku **šablony úlohy** , ve sloupci úplně vpravo.
2. Vložte zkopírované řádky pod poslední položku řádku v tabulce.
3. Změňte buňku s nadpisem nové funkce ze **šablony úlohy** na název vaší nové úlohy.
4. Do sloupce značek pro všechny řádky pod novou funkcí vložte buňku název nové úlohy. Buďte opatrní, abyste neměnili značky nebo názvy řádků, které se týkají skutečné funkce **šablony úlohy** . Tyto pracovní položky budete potřebovat při přidávání další úlohy do plánu přijetí do cloudu.
5. Pokud chcete publikovat list, přejděte ke kroku 8 v pokynech k hromadnému úpravám. Tento krok vytvoří všechny pracovní položky potřebné k migraci vašich úloh.

Opakujte kroky 1 až 5 pro všechny úlohy ve vysílacích 10 seznamů.

## <a name="define-workloads"></a>Definování úloh

Po definování počátečních priorit a přidání úloh do plánu je možné každou úlohu definovat pomocí hlubší kvalitativní analýzy. Před zahrnutím všech úloh do plánu přijetí do cloudu zkuste pro každou úlohu poskytnout následující datové body.

### <a name="business-inputs"></a>Obchodní vstupy

| Datový bod | Popis | Vstup |
|---|---|---|
| Název úlohy | Jaká je tato úloha volána? |         |
| Popis úlohy | Co toto zatížení dělá v jedné větě? |         |
| Motivace pro přijetí | Které z motivů pro přijetí do cloudu ovlivňují tuto úlohu? |         |
| Primární sponzor | Z těchto zúčastněných stran, kdo je primárním sponzorem požadujícím předchozí podněty? |         |
| Obchodní jednotka | Jakou obchodní jednotku zodpovídá za náklady na tuto úlohu? |         |
| Obchodní procesy | Které obchodní procesy ovlivní změny úlohy? |         |
| Obchodní týmy | Které obchodní týmy ovlivní změny? |         |
| Obchodní účastníci | Existují nějaké vedoucí pracovníky, jejichž podnikání ovlivní změny? |         |
| Obchodní výsledky | Jak bude firmy změřit úspěch tohoto úsilí? |         |
| Metriky | Jaké metriky se budou používat ke sledování úspěchu? |         |
| Dodržování předpisů | Existují pro tuto úlohu nějaké požadavky na dodržování předpisů třetích stran? |         |
| Vlastníci aplikace | Kdo má za to, jaký má obchodní dopad na jakékoli aplikace přidružené k tomuto zatížení? |         |
| Doba zablokování podniku | Existují nějaké časy, během kterých podnik nepovoluje změnu? |         |
| Zeměpisné oblasti | Jsou všechny geografické oblasti ovlivněné touto úlohou? |         |

### <a name="technical-inputs"></a>Technické vstupy

| Datový bod | Popis | Vstup |
|---|---|---|
| Přístup k přijetí | Je to přijetí kandidáta na migraci nebo inovace? |         |
| Vedoucí operace aplikace | Seznam stran zodpovědných za výkon a dostupnost této úlohy. |         |
| Smlouvy SLA | Vypíše všechny smlouvy o úrovni služeb (požadavky RTO/RPO). |         |
| Závažnost | Vypíše závažnost aktuální aplikace. |         |
| Klasifikace dat | Vypíše klasifikaci citlivosti dat. |         |
| Provozní geografické oblasti | Seznamte se s případnými geografickými oblastmi, ve kterých je zatížení nebo by mělo být hostováno. |         |
| Aplikace | Zadejte počáteční seznam nebo počet všech aplikací, které jsou součástí této úlohy. |         |
| virtuálních počítačů | Zadejte počáteční seznam nebo počet všech virtuálních počítačů nebo serverů, které jsou součástí úlohy. |         |
| Zdroje dat | Zadejte počáteční seznam nebo počet všech zdrojů dat zahrnutých do úlohy. |         |
| Závislosti | Vypíše všechny závislosti assetů, které nejsou součástí úlohy. |         |
| Geografické oblasti provozu uživatelů | Seznamte se s geografickými oblastmi, které mají významnou kolekci uživatelských přenosů. |         |

## <a name="confirm-priorities"></a>Potvrďte priority

Na základě sestavených dat by tým cloudové strategie a tým pro přijetí v cloudu měli splnit k přehodnocení priorit. Při objasnění obchodních datových bodů se můžou zobrazit výzvy změny v prioritách. Technické složitosti nebo závislosti můžou způsobit změny týkající se přidělování zaměstnanců, časových os nebo sekvencování technického úsilí.

Po kontrole by měly být oba týmy pohodlné s potvrzením výsledných priorit. Tato sada dokumentovaných, ověřených a potvrzených priorit je nevyřízené položky pro přijetí do cloudu s určenou prioritou.

## <a name="next-steps"></a>Další postup

Pro všechny úlohy v nevyřízených položkách pro přijetí do cloudu, je teď tým připravený na [Zarovnání prostředků](./assets.md).

> [!div class="nextstepaction"]
> [Zarovnání prostředků pro úlohy s upřednostněním priorit](./assets.md)
