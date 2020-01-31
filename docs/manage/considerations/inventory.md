---
title: Inventář a viditelnost – cloudová správa a provoz
description: Inventář a viditelnost – cloudová správa a provoz
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 29085f6ce1324f9f22acd0dc674c382163426233
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807763"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Inventář a viditelnost ve správě cloudu

Provozní Správa má jasné závislosti na datech. Konzistentní Správa vyžaduje porozumění obsahu spravovaného (inventarizace) a způsobu, jakým se tyto spravované úlohy a prostředky mění v čase (viditelnost). Vyjasnění přehledu o inventáři a viditelnosti vám pomůžou týmu efektivně spravovat prostředí. Všechny ostatní aktivity a procesy provozní správy sestavují na těchto dvou oblastech.

Několik klasických frází o důležitosti měření pro tento článek:

- Spravujte, co je věcí.
- Můžete spravovat jenom to, co můžete měřit.
- Pokud to nemůžete změřit, může to být nezáleží.

Obor inventarizace a viditelnosti staví na těchto Timeless frázích. Než budete moct efektivně navázat procesy provozní správy, je důležité shromáždit data a vytvořit správnou úroveň viditelnosti pro správné týmy.

## <a name="common-customer-challenges"></a>Běžné výzvy zákazníků

Pokud se nepoužívají procesy inventarizace a viditelnosti, můžou provozní týmy s využitím většího objemu přerušování, trvat delší dobu na obnovení a zvýšit množství úsilí potřebného k řešení potíží a třídění problémů. Jelikož tyto změny nepříznivě ovlivňují aplikace s vyšší prioritou a větší počet prostředků, každá z těchto metrik roste ještě rychleji.

Tyto výzvy vyplývají z malého počtu otázek, na které se dá odpovědět jenom prostřednictvím konzistentních dat nebo telemetrie:

- Jak se liší výkon aktuálního stavu ze standardní telemetrie provozního výkonu?
- Jaké prostředky způsobují provozní přerušení na úrovni zatížení?
- Které prostředky se musí opravit, aby se vracel přijatelný výkon této úlohy nebo obchodního procesu?
- Kdy se odchylka začala? Co byl Trigger?
- Které změny se provedly u základních assetů? Kým?
- Byly změny úmyslné? Úmysl?
- Jaký vliv mají změny na telemetrii výkonu?

Je obtížné, pokud není možné, odpovědět na tyto otázky bez bohatě centralizovaného zdroje pro protokoly a data telemetrie. Pokud chcete povolit správu cloudu tím, že zajistíte konzistentní konfiguraci, která je potřebná pro centralizaci dat, musí se nejdřív spustit základní služba definováním procesů. Procesy by měly zachytit, jak taková konfigurace vynutila shromažďování dat pro podporu komponent inventáře a viditelnosti v další části.

## <a name="components-of-inventory-and-visibility"></a>Komponenty inventáře a viditelnosti

Vytváření viditelnosti na jakékoli cloudové platformě vyžaduje několik klíčových součástí:

- Zodpovědnost a viditelnost
- Inventarizace
- Centrální protokolování
- Sledování změn
- Telemetrie výkonu

### <a name="responsibility-and-visibility"></a>Zodpovědnost a viditelnost

Při vytváření závazků pro jednotlivé úlohy je [zodpovědnost za správu](./commitment.md#management-responsibility) klíčovým faktorem. Delegovaná odpovědnost vytvoří nutnost delegované viditelnosti. Prvním krokem k inventarizaci a viditelnosti je zajistit, že mají odpovědné strany přístup ke správným datům. Před implementací všech cloudových nástrojů pro zajištění viditelnosti zajistěte, aby byl každý nástroj pro monitorování nakonfigurovaný se správným přístupem a rozsahem pro každý provozní tým.

### <a name="inventory"></a>Inventarizace

Pokud nikdo neví, že prostředek existuje, je obtížné ho spravovat. Než bude možné prostředek nebo úlohu spravovat, musí být v inventáři a klasifikovány. Prvním technickým krokem k dosažení stabilní operace je ověření inventáře a klasifikace tohoto inventáře.

### <a name="central-logging"></a>Centrální protokolování

Centralizované protokolování je důležité pro viditelnost, kterou si tým pro správu provozu potřebuje k dennímu dni. Všechny prostředky nasazené do cloudu by měly zaznamenávat protokoly do centrálního umístění. V Azure je toto centrální umístění v Log Analytics. Centralizované protokolování jednotek hlášení o správě změn, stavu služeb, konfiguraci a většině dalších aspektů IT operací.

Vynucování konzistentního použití centrálního protokolování je prvním krokem k navázání opakujících se operací. Vynucování je možné provést prostřednictvím podnikových zásad. Pokud je to možné, je však vhodné automatizované vynucování, aby se zajistila konzistence.

### <a name="change-tracking"></a>Sledování změn

Změna je jedna konstanta v technologickém prostředí. Pro spolehlivé operace je důležité povědomí a porozumění změnám napříč více úlohami. Jakékoli řešení pro správu cloudu by mělo zahrnovat způsob, jak pochopit, kdy a proč technickou změnu. Bez těchto datových bodů je to významně bráněno potížím s nápravou.

### <a name="performance-telemetry"></a>Telemetrie výkonu

Obchodní závazky týkající se správy cloudu jsou založené na datech. Aby bylo možné zajistit správné udržování závazků, musí tým cloudových operací nejprve porozumět telemetrie týkající se stability, výkonu a provozu úlohy a prostředků, které podporují úlohu.

Průběžným stavem a provozem sítě, DNS, operačních systémů a dalších základních aspektů prostředí jsou důležité datové body, které se počítají na celkový stav jakékoli úlohy.

## <a name="processes"></a>Procesy

V případě, že je to důležitější než u funkcí platformy pro správu cloudu, procesy správy cloudu budou realizovat provozní závazky s podnikáním. Každá metodologie správy cloudu by měla zahrnovat minimálně tyto procesy:

- **Reaktivní monitorování:** Pokud by odchylky nepříznivě ovlivnily obchodní operace, které tyto odchylky řeší? Jaké akce jsou potřeba k nápravě odchylek?
- **Proaktivní monitorování:** Pokud jsou zjištěny odchylky, ale nedošlo k ovlivnění obchodních operací, jak jsou vyřešeny tyto odchylky a kým?
- **Vytváření sestav závazků:** Jak se respektuje obchodní závazek, který komunikuje se zúčastněnými stranami společnosti?
- **Rozpočtová přezkoumání:** Jaký je proces kontroly těchto závazků proti rozpočtovaným nákladům? Jaký je proces pro úpravu nasazeného řešení nebo závazky pro vytvoření zarovnání?
- **Eskalační cesty:** Jaké cesty eskalace jsou k dispozici, když některý z předchozích procesů nevyhoví potřebám firmy?

Existuje několik dalších procesů vztahujících se k inventarizaci a viditelnosti. Předchozí seznam je navržený tak, aby se v rámci provozního týmu myslel. Zodpovězení těchto otázek vám pomůže vyvíjet některé z nezbytných procesů a také nejspíš aktivovat nové a hlubší otázky.

## <a name="responsibilities"></a>Odpovědnost

Když vyvíjíte procesy pro provozní monitorování, je stejně důležité stanovit zodpovědnost za každodenní provoz a pravidelnou podporu každého procesu.

V centrální organizaci IT by to poskytovalo provozní znalosti. V případě problémů nutných k nápravě by byl podnik v podstatě poporadním.

V cloudovém centru špičkových organizací by obchodní operace poskytovaly odbornost a zodpovědnost za správu těchto procesů. Zaměřte se na automatizaci a podporu týmů, jak provozují prostředí.

Ale jedná se o běžné zodpovědnosti. Organizace často vyžadují ke splnění obchodních závazků kombinaci zodpovědnosti.

## <a name="act-on-inventory-and-visibility"></a>Pracovat na inventáři a viditelnosti

Bez ohledu na cloudovou platformu se k zajištění většiny provozních procesů používají pět součástí inventarizace a viditelnosti. Všechna následující pravidla budou vytvořena na zachycených datech. Další články v této sérii popisují způsob fungování těchto dat a integraci dalších zdrojů dat.

### <a name="share-visibility"></a>Sdílet viditelnost

Data bez akcí vypočítávají jenom malý návrat. Správa cloudu se může rozšířit i na nástroje a procesy nativní pro Cloud. Aby bylo možné přizpůsobit širší procesy, může být nutné zvýšit úroveň správy cloudu tak, aby zahrnovala vytváření sestav, integraci správy služeb IT nebo centralizaci dat. Správa cloudu může během různých fází provozní zralosti zahrnovat jednu nebo více následujících možností.

### <a name="report"></a>Zpráva

Offline procesy a komunikace týkající se závazků obchodních účastníků často vyžadují vytváření sestav. Samoobslužné generování sestav nebo pravidelné generování sestav může být nezbytnou součástí rozšířeného směrného plánu správy.

### <a name="it-service-management-itsm-integration"></a>Integrace správy IT služeb (ITSM)

ITSM Integration je často první příklad práce na inventáři a viditelnosti. V případě, že vznikne odchylka od očekávaných vzorců výkonu, Integration ITSM pomocí výstrah z cloudové platformy spustí lístky v samostatném nástroji pro správu služby, aby mohly aktivovat nápravné aktivity. Některé provozní modely můžou vyžadovat integraci ITSM jako aspekt směrného plánu rozšířené správy.

### <a name="data-centralization"></a>Centralizované sepřenosování dat

V rámci jednoho poskytovatele cloudu může podnik vyžadovat více tenantů. V těchto scénářích je centralizaci dat požadovanou součástí rozšířené směrné plány správy, protože může poskytovat viditelnost napříč jednotlivými klienty nebo prostředími.

## <a name="next-steps"></a>Další kroky

Provozní dodržování předpisů je založeno na možnostech inventáře, a to použitím automatizace a ovládacích prvků pro správu. Podívejte se, jak se [provozní dodržování předpisů](./operational-compliance.md) mapuje na vaše procesy.

> [!div class="nextstepaction"]
> [Plán pro provozní dodržování předpisů](./operational-compliance.md)
