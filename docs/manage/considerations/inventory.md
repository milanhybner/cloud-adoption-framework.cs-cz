---
title: Inventář a viditelnost – cloudová správa a provoz
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Inventář a viditelnost – cloudová správa a provoz
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: fe46ec035bb732ec82931358c7e79b41b4f18bd5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558061"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Inventář a viditelnost ve správě cloudu

Provozní Správa má jasné závislosti na datech. Konzistentní Správa vyžaduje jasné informace o tom, co je spravované (inventarizace) a jak se tyto spravované úlohy a prostředky mění v čase (viditelnost). Díky přehlednějšímu využití inventáře a viditelnosti tým umožňuje týmu efektivně spravovat prostředí. Všechny ostatní aktivity a procesy provozní správy sestavují na těchto dvou oblastech Insights.

Několik klasických frází, které jsou důležité pro měření, jsou tímto článkem popsány v tomto článku: Správa důležitých věcí. Můžete spravovat jenom to, co můžete měřit. Pokud to nemůžete změřit, může to být nezáleží. Obor inventarizace a viditelnosti staví na těchto Timeless frázích. Před zřízením procesů provozní správy je důležité shromáždit data a vytvořit správnou úroveň viditelnosti pro správné týmy.

## <a name="common-customer-challenges"></a>Běžné výzvy zákazníků

V případě, že se procesy inventáře a viditelnosti nepoužívají konzistentně, provozní týmy pro provoz nevyužívají vyšší objemy obchodních přerušení, delší dobu k obnovení a větší úsilí potřebné k řešení problémů a jejich třídění. Jak změny mají vliv na aplikace s vyšší prioritou a větší počet prostředků, každá z těchto metrik roste ještě rychleji.

Tyto výzvy vyplývají z malého počtu otázek, které mohou být zodpovězeny pouze prostřednictvím konzistentních dat nebo telemetrie:

- Jak se liší výkon aktuálního stavu ze standardní telemetrie provozního výkonu?
- Jaké prostředky způsobují provozní přerušení na úrovni zatížení?
- Které prostředky se musí opravit, aby se vracel přijatelný výkon této úlohy nebo obchodního procesu?
- Kdy se odchylka začala? Co byl Trigger?
- Které změny se provedly u základních assetů? Kým?
- Byly změny úmyslné? Úmysl?
- Jak změny ovlivnily výkon telemetrie?

Je obtížné, pokud není možné odpovědět na tyto otázky bez bohatě centralizovaného zdroje pro protokoly a data telemetrie. Aby bylo možné povolit správu cloudu, musí základní služba nejdřív začít s definicí procesů, aby se zajistila konzistentní konfigurace potřebná pro centralizaci dat. Tyto procesy by měly zachytit způsob, jakým bude konfigurace vyhovět shromažďování dat pro podporu komponent inventáře a viditelnosti v další části.

## <a name="components-of-inventory-and-visibility"></a>Komponenty inventáře a viditelnosti

Vytváření viditelnosti na jakékoli cloudové platformě vyžaduje několik klíčových součástí:

1. Zodpovědnost a viditelnost
2. Inventarizace
3. Centrální protokolování
4. Sledování změn
5. Telemetrie výkonu

### <a name="responsibility-and-visibility"></a>Zodpovědnost a viditelnost

Při stanovování závazků pro jednotlivé úlohy je [zodpovědnost za správu](./commitment.md#management-responsibility) klíčovým faktorem. Delegovaná odpovědnost vytvoří nutnost delegované viditelnosti. Prvním krokem k inventarizaci a viditelnosti je zajistit, aby zodpovědné strany měly přístup ke správným datům. Před implementací všech nástrojů nativního pro Cloud pro zajištění viditelnosti si zajistěte, aby byl každý nástroj pro monitorování nakonfigurovaný se správným přístupem a rozsahem pro každý provozní tým.

### <a name="inventory"></a>Inventarizace

Pokud nikdo neví, že Asset existuje, je velmi obtížné ho spravovat. Než bude možné prostředek nebo úlohu spravovat, musí být v inventáři a klasifikovány. Prvním technickým krokem k dosažení stabilní operace je ověření inventáře a klasifikace tohoto inventáře.

### <a name="central-logging"></a>Centrální protokolování

Centralizované protokolování je důležité pro viditelnost, kterou vyžadují týmy pro správu provozu. Všechny prostředky nasazené do cloudu by měly zaznamenávat protokoly do centrálního umístění. V Azure je toto centrální umístění v Log Analytics. Centralizované protokolování jednotek hlásí týkajících se správy změn, stavu služeb, konfigurace a většiny dalších aspektů IT operací.

Vynucení konzistentního použití centrálního protokolování je prvním krokem k konzistentnímu opakování operací. Vynucování je možné provést prostřednictvím podnikových zásad. Nicméně, pokud je možné vynucení zajistit konzistenci.

### <a name="change-tracking"></a>Sledování změn

Změna je jedna konstanta v technologickém prostředí. Pro spolehlivé operace je důležité povědomí a porozumění změnám napříč více úlohami. Jakékoli řešení pro správu cloudu by mělo zahrnovat způsob, jak pochopit, kdy a proč technickou změnu. Bez těchto datových bodů je to významně bráněno potížím s nápravou.

### <a name="performance-telemetry"></a>Telemetrie výkonu

Obchodní závazky týkající se správy cloudu jsou založené na datech. Aby bylo možné zajistit správné udržování závazků, musí tým cloudových operací nejprve porozumět telemetrie týkající se stability, výkonu a provozu úlohy a prostředků, které podporují úlohu.

Dobrými datovými body, které se počítají do celkového stavu jakékoli úlohy, jsou průběžné stavy a provoz sítě, DNS, operačních systémů a dalších základních aspektů prostředí.

## <a name="processes"></a>Procesy

Je možné, že procesy správy cloudu budou v rámci podnikových procesů realizovat závazky, které jsou důležitější než funkce platformy pro správu cloudu. Každá metodologie správy cloudu by měla obsahovat minimálně tyto procesy:

- Reaktivní monitorování: Pokud odchylky ovlivňují obchodní operace, které tyto odchylky řeší? Jaké akce jsou potřeba k nápravě odchylek.
- Proaktivní monitorování: Pokud se zjistí odchylky, ale provozní operace na ně neovlivní, jak jsou vyřešené odchylky a podle koho?
- Vytváření sestav o závazcích: jak se přikládáte na potvrzené podnikání sdělené obchodním stranám?
- Rozpočtová přezkoumání: Jaký je proces kontroly těchto závazků proti rozpočtovaným nákladům? Jaký je proces pro úpravu nasazeného řešení nebo závazky pro vytvoření zarovnání?
- Eskalační cesty: Jaké cesty eskalace jsou k dispozici, když některý z výše uvedených procesů nevyhovuje potřebám firmy?

Existuje několik dalších procesů souvisejících s inventářem a viditelností. Seznam výše je navržený tak, aby se mohl rozmyslet mezi provozním týmem. Po zodpovězení těchto otázek se budou vyvíjet některé z nezbytných procesů. Bude nejspíš aktivovat i nové hlubší otázky.

## <a name="responsibilities"></a>Odpovědnost

Při vývoji procesů pro provozní monitorování je stejně důležité, abyste určili zodpovědnost za každodenní provoz a pravidelnou podporu každého procesu.

V centrální organizaci IT by to poskytovalo provozní znalosti. V případě problémů Oprava by byl podnik v podstatě poporadním.
V cloudovém centru špičkových organizací by obchodní operace poskytovaly odbornost a zodpovědnost za správu těchto procesů. Zaměřte se na automatizaci a podporu týmů, jak provozují prostředí.

Jsou to ale běžné zodpovědnosti. Organizace často vyžadují ke splnění obchodních závazků kombinaci zodpovědnosti.

## <a name="acting-on-inventory-and-visibility"></a>Práce na inventáři a viditelnosti

Bez ohledu na cloudovou platformu se k zajištění většiny provozních procesů používají pět součástí inventarizace a viditelnosti. Všechna následující pravidla budou vytvořena pro sebraná data. Následující články v této sérii budou mít přehled o způsobech, kterými se tato data budou chovat, a integraci dalších zdrojů dat.

### <a name="sharing-visibility"></a>Sdílení viditelnosti

Data bez akcí vypočítávají jenom malý návrat. Správa cloudu se může rozšířit i na nástroje a procesy nativní pro Cloud. Aby bylo možné přizpůsobit širší procesy, může být nutné zvýšit úroveň správy cloudu tak, aby zahrnovala vytváření sestav, integraci správy služeb IT nebo centralizaci dat. Správa cloudu může během různých fází provozní zralosti zahrnovat jednu nebo více následujících možností.

### <a name="reporting"></a>Generování sestav

Offline procesy a komunikace týkající se závazků obchodních účastníků často vyžadují vytváření sestav. Samoobslužné generování sestav nebo pravidelné generování sestav může být nezbytnou součástí rozšířeného směrného plánu správy.

### <a name="it-service-management-itsm-integration"></a>Integrace správy služeb IT (ITSM)

ITSM Integration je často první příklad práce na inventáři a viditelnosti. V případě, že vznikne odchylka od očekávaných vzorců výkonu, bude integrace ITSM používat výstrahy z cloudové platformy, aby aktivovala lístky v samostatném nástroji pro správu služby, aby mohly aktivovat opravné aktivity. Některé provozní modely můžou vyžadovat integraci ITSM jako aspekt směrného plánu rozšířené správy.

### <a name="data-centralization"></a>Centralizované sepřenosování dat

Existuje celá řada důvodů, proč podnik může vyžadovat více tenantů v rámci jednoho poskytovatele cloudu. V těchto scénářích je centralizaci dat požadovanou součástí rozšířeného směrného plánu správy, aby poskytovala přehled napříč jednotlivými klienty nebo prostředími.

## <a name="next-steps"></a>Další kroky

Provozní dodržování předpisů je založeno na možnostech inventáře, a to použitím automatizace a ovládacích prvků pro správu. Podívejte se, jak se [provozní dodržování předpisů](./operational-compliance.md) mapuje na vaše procesy.

> [!div class="nextstepaction"]
> [Plán pro provozní dodržování předpisů](./operational-compliance.md)
