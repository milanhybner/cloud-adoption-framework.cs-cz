---
title: Úroveň správy napříč obory pro správu cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úroveň správy napříč obory pro správu cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 0517816bd01221da8f5b4d97cc40dd39f4599b5e
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557567"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Úroveň správy napříč obory pro správu cloudu

Klíčem ke správné správě v jakémkoli prostředí je konzistence a opakující se procesy. K dispozici jsou nekonečné možnosti pro věci, které je možné provést v Azure. Podobně existují dlouhé přístupy ke správě cloudu. Aby se zajistila konzistence a opakovatelnost, je důležité tyto možnosti zúžit na konzistentní sadu procesů a nástrojů pro správu, které se budou nabízet pro úlohy hostované v cloudu.

## <a name="suggested-management-levels"></a>Navrhované úrovně správy

Vzhledem k tomu, že úlohy v portfoliu IT nejsou všechny stejné, není pravděpodobné, že pro každou úlohu bude stačit jedna úroveň správy. Aby bylo možné podporovat různé úlohy a různé obchodní závazky, je doporučeno, aby tým operací cloudu nebo provozního provozu platformy navázal několik úrovní správy operací.

![Správa úrovní správy a zralosti v rámci architektury pro přijetí v cloudu](../../_images/manage/cloud-management-maturity.png)

Následující úrovně správy (kromě výše uvedeného obrázku) jsou několika navrhovanými úrovněmi, které slouží jako výchozí bod:

- **Standardní hodnoty správy**: základní (neboli standardní) Správa cloudu (neboli standardní hodnota správy) je definovaná sada nástrojů, procesů a konzistentní ceny, které budou sloužit jako základ pro veškerou správu cloudu v Azure. Pokud chcete vytvořit směrný plán správy cloudu, přečtěte si tabulku v následující části a určete, které nástroje se budou do vaší firmy zahrnout do základní nabídky.
- **Rozšířené základní hodnoty**: řada úloh může vyžadovat vylepšení standardních hodnot, které nejsou nutně specifické pro jednu platformu nebo úlohu. I když tato vylepšení nejsou nákladově efektivní pro každou úlohu, měly by existovat běžné procesy, nástroje a řešení pro všechny úlohy, které můžou nákladně zdůvodnit dodatečnou podporu.
- **Specializace platformy**: v jakémkoli prostředí existují běžné platformy, které jsou používány více různými úlohami. Toto obecné společné architektury se nemění, když firmy přijímají Cloud. Specializace platformy je zvýšená úroveň správy, která využívá odbornosti dat a architektury, aby poskytovaly vyšší úroveň provozní správy. Příklady specializace platforem zahrnují funkce správy, které jsou specifické pro SQL Server, kontejnery, služby Active Directory nebo jiné služby, které je možné lépe spravovat prostřednictvím konzistentních, opakujících se procesů, nástrojů a architektur.
- **Specializace úloh**: u pracovních procesů, které jsou skutečně důležité, může dojít k výraznému snížení nákladů na správu této úlohy. Specializace úloh využívá telemetrii úloh k určení dalších přístupů ke každodenní správě. Stejná data často označují vylepšení automatizace, nasazení a návrhu, která by vedla k větší stabilitě, spolehlivosti a odolnosti nad rámec toho, co je možné jenom s provozní správou.
- **Nepodporované**: je stejně důležité, aby komunikovaly s běžnými procesy správy, které nebudou dodány v oborech správy cloudu pro jakékoli zatížení klasifikované jako nepodporované nebo nepostradatelné.

Zbývající články v této sérii vysvětlují počet procesů, které se běžně v rámci každého z těchto pravidel vyskytují.
V rámci paralelní [příručky Azure Management](../azure-management-guide/index.md) demonstruje nástroje, které můžou podporovat jednotlivé procesy. Pokud potřebujete pomoc s vytvářením standardních hodnot správy, začněte s průvodcem pro správu Azure. Po vytvoření směrného plánu Tato řada článků a doprovodné osvědčené postupy mohou pomoci tuto základnu rozšířit a definovat další úrovně podpory správy.

## <a name="cloud-management-disciplines"></a>Obory pro správu cloudu

Každá z navrhovaných úrovní správy se může volat v různých oborech pro správu cloudu. Mapování je ale navržené tak, aby bylo snazší najít navrhované procesy a nástroje pro zajištění vhodné úrovně správy cloudu.

Ve většině případů se výše uvedená úroveň správy na úrovni standardně skládá z procesů a nástrojů z následujících oborů. V každém případě se zvýrazní několik procesů a nástrojů, které ukazují "rozšířené funkce standardních hodnot".

- **Inventář a viditelnost**: minimální standardní hodnoty pro správu by měly zahrnovat způsob inventarizace assetů a vytváření viditelnosti stavu spuštění jednotlivých assetů.
- **Provozní dodržování předpisů:** Běžnou správou konfigurace, velikosti, nákladů a výkonu assetů je klíč pro udržení očekávání výkonu a standardních hodnot správy.
- **Ochrana a obnovení:** Minimalizace provozních přerušení a urychlení obnovení každé z nich, aby se předešlo ztrátám výkonu a vlivům na výnosy. Zjišťování a obnovení jsou zásadními aspekty tohoto oboru v rámci všech standardních hodnot správy.

Úroveň specializace platformy, kterou Správa přebírá z procesů a nástrojů zarovnaných k provozním oborům platformy.
Podobně platí, že úroveň specializace úlohy správy se vyžádá z procesů a nástrojů zarovnaných k provozním oborům úloh.
  
## <a name="next-steps"></a>Další kroky

Dalším krokem k definování jednotlivých úrovní správy cloudu je porozumění [inventarizaci a viditelnosti](./inventory.md).

> [!div class="nextstepaction"]
> [Možnosti inventarizace a viditelnosti](./inventory.md)
