---
title: Průvodce připravenostmi na cloudový zabezpečení ředitelka zabezpečení informací
description: Přečtěte si, jak připravit hlavní kancelář pro zabezpečení informací (ředitelka zabezpečení informací) pro transformaci a přírůstkové řízení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: b30cac2fb4ba372c7fd11f8528ecac4c0f3e84c3
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433057"
---
<!-- cSpell:ignore CISO -->

# <a name="ciso-cloud-readiness-guide"></a>Průvodce připravenostmi na Cloud ředitelka zabezpečení informací

Pokyny společnosti Microsoft, jako je rozhraní pro přijetí v cloudu, nejsou umístěny k určení nebo vodítkí jedinečného omezení zabezpečení tisíců podniků, které tato dokumentace podporuje. Při přechodu do cloudu se v cloudových technologiích supplanted role ředitele Information Security důstojníka nebo hlavní kancelář zabezpečení informací (ředitelka zabezpečení informací). V rozporu s ředitelka zabezpečení informací a kanceláří ředitelka zabezpečení informací se stane víc engrained a integrovaných. Tato příručka předpokládá, že čtenář je obeznámený s ředitelka zabezpečení informací procesy a snaží se modernizovat tyto procesy, aby umožnil transformaci cloudu.

Přijetí do cloudu umožňuje službám, které se často nepovažovaly za tradiční IT prostředí. Samoobslužná nebo automatizovaná nasazení se běžně spouštějí při vývoji aplikací nebo jiných IT týmech, která nejsou tradičně zarovnaná do produkčního nasazení. V některých organizacích mají obchodní prvky podobně možnosti samoobslužné služby. To může aktivovat nové požadavky na zabezpečení, které se nevyžadovaly v místním světě. Centralizované zabezpečení je náročnější, ale zabezpečení se často stává sdílenou odpovědností napříč podnikovou a IT kulturou. Tento článek může přispět k ředitelka zabezpečení informací přípravě na tento přístup a zapojit se do přírůstkového řízení.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-a-ciso-prepare-for-the-cloud"></a>Jak se CISO může připravit na cloud?

Stejně jako většina zásad, zabezpečení a zásady správného řízení v rámci organizace se obvykle rozšiřují na organické. Dojde-li k incidentům zabezpečení, zásady pro uživatele informují o tom, že by se snížila pravděpodobnost výskytu opakování. V přirozeném případě tento přístup vytvoří zásady dispozici determinističtější a technické závislosti. Cesty k transformaci cloudu vytvářejí jedinečnou příležitost pro modernizovat a resetování zásad. Při přípravě na cestu transformace může ředitelka zabezpečení informací vytvořit okamžitou a měřitelnou hodnotu, která slouží jako primární účastník v rámci [Revize zásad](./cloud-policy-review.md).

V takovém případě má role ředitelka zabezpečení informací vytvořit bezpečný rovnováhu mezi omezeními stávající zásady nebo dodržování předpisů a vylepšeným stav zabezpečení poskytovatelů cloudu. Měření tohoto pokroku může trvat mnoho forem, často se měří v počtu zásad zabezpečení, které se dají bezpečně přesměrovat na poskytovatele cloudu.

**Přenos rizik zabezpečení:** Jako služby se přesunou na modely hostování IaaS (infrastruktura jako služba), předpokládá podnik méně přímé riziko týkající se zřizování hardwaru. Riziko se neodebere, místo toho se převede na dodavatele cloudu. Pokud má dodavatel cloudu přístup k zřizování hardwaru, zajišťují stejnou úroveň zmírnění rizik, a to v zabezpečeném opakovaném procesu, ale riziko spuštění hardwarového zřizování se z oblasti IT oddělení zodpovědnosti a přenosu do cloudu odebere. zprostředkovatele. Tím se sníží celkové riziko zabezpečení, které podnik nese za správu, i když riziko samotného by mělo být stále sledováno a přezkoumáváno.

Když řešení přesunou dále "sestavou", aby zahrnovala modely PaaS (Platform as a Service) nebo software jako služba (SaaS), je možné vyhnout se nebo přenášet další rizika. Když se riziko bezpečně přesune do poskytovatele cloudu, náklady na spuštění, monitorování a vynucování zásad zabezpečení nebo jiných zásad dodržování předpisů se taky můžou bezpečně snížit.

**Místo růstu:** Změna se může Scary na obchodní i technické implementátory. Když ředitelka zabezpečení informací vede k růstu místo Shift v organizaci, zjistili jsme, že tyto přirozené obavyy se zvýšily o zvýšení zájmu na bezpečnost a dodržování zásad. Přístup k [revizi zásad](./cloud-policy-review.md), transformační cestě nebo jednoduchým kontrolám implementace s růstovým místo umožňuje týmu, aby se rychle přesunuly, ale ne náklady na spravedlivý a spravovatelný profil rizika.

## <a name="resources-for-the-chief-information-security-officer"></a>Prostředky pro vedoucího zabezpečení informací

Poznatky o cloudu jsou zásadní pro přístup k [revizi zásad](./cloud-policy-review.md) s růst místo. Následující zdroje vám pomohou ředitelka zabezpečení informací lépe pochopit stav zabezpečení platformy Microsoft Azure.

Prostředky platformy zabezpečení:

- [Životní cyklus vývoje zabezpečení, interní audity](https://www.microsoft.com/sdl)
- [Povinné školení zabezpečení, kontroly na pozadí](https://downloads.cloudsecurityalliance.org/star/self-assessment/StandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx)
- [Testování průniku, zjišťování neoprávněných vniknutí, DDoS, audity a protokolování](https://www.microsoft.com/trustcenter/Security/AuditingAndLogging)
- Špičkové [datové centrum](https://www.microsoft.com/cloud-platform/global-datacenters), fyzické zabezpečení, zabezpečení [sítě](https://docs.microsoft.com/azure/security/security-network-overview)
- [Microsoft Azure odpověď zabezpečení v cloudu (PDF)](https://aka.ms/SecurityResponsePaper)

Ochrana osobních údajů a ovládací prvky:

- [Správa dat ve všech časových intervalech](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data)
- [Řízení na umístění dat](https://www.microsoft.com/trustcenter/Privacy/Where-your-data-is-located)
- [Poskytnutí přístupu k datům podle vašich podmínek](https://www.microsoft.com/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)
- [Reakce na vynucování zákonů](https://www.microsoft.com/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data)
- [Přísné standardy ochrany osobních údajů](https://www.microsoft.com/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards)

Dodržování

- [Centrum zabezpečení Microsoftu](https://www.microsoft.com/trustcenter/default.aspx)
- [Centrum běžných ovládacích prvků](https://www.microsoft.com/trustcenter/Common-Controls-Hub)
- [Cloud Services kontrolní seznam pro náležité opatrnosti](https://www.microsoft.com/trustcenter/Compliance/Due-Diligence-Checklist)
- [Dodržování předpisů podle služeb, umístění a odvětví](https://www.microsoft.com/trustcenter/Compliance/default.aspx)

Transparentnosti

- [Jak Microsoft zabezpečuje zákaznická data ve službách Azure](https://www.microsoft.com/trustcenter/Transparency/default.aspx)
- [Jak Microsoft spravuje umístění dat ve službách Azure](https://azuredatacentermap.azurewebsites.net)
- [Kdo v Microsoftu má přístup k vašim datům za podmínek](https://www.microsoft.com/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)
- [Jak Microsoft zabezpečuje zákaznická data ve službách Azure](https://www.microsoft.com/trustcenter/Transparency/default.aspx)
- [Kontrola certifikace pro služby Azure, centrum průhledností](https://www.microsoft.com/trustcenter/Compliance/default.aspx)

## <a name="next-steps"></a>Další kroky

Prvním krokem k provedení akce v jakékoli strategii zásad správného řízení je [Kontrola zásad](./cloud-policy-review.md). [Zásady a dodržování předpisů](./index.md) by mohly být užitečným průvodcem během kontroly zásad.

> [!div class="nextstepaction"]
> [Příprava na revizi zásad](./cloud-policy-review.md)
