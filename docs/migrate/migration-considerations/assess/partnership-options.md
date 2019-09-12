---
title: Vysvětlení možností partnerství a podpory
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Popisuje možnosti a přístupy k podpoře úsilí migrace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b19353ebe22faf089ff56b5ee84289928a8eaca7
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905632"
---
# <a name="understand-partnership-options"></a>Vysvětlení možností partnerství

Při migraci tým přechodu na cloud provádí skutečnou migraci úloh do cloudu. Na rozdíl od úkolů spolupráce a řešení problémů při definování [digitálních aktiv](../../../digital-estate/index.md) nebo při vytváření základní cloudové infrastruktury má migrace tendenci stát se řadou opakujících se prováděných úkolů. Kromě aspektů opakování existují pravděpodobně akce testování a optimalizace, které vyžaduje důkladné znalosti zvoleného poskytovatele cloudu. Opakující se povaha tohoto procesu může být někdy nejlépe zvládnutá partnerem, což snižuje nároky na stálé zaměstnance. Kromě toho se mohou partneři lépe vyrovnat s potřebou hlubokých technických vědomostí, když se při provádění opakujících se procesů vyskytnou anomálie.

Partneři mají tendenci úzce spolupracovat s jedním dodavatelem cloudu nebo s malým počtem dodavatelů cloudu. Abychom lépe ilustrovali možnosti spolupráce, ve zbývající část tohoto článku se předpokládá, že vybraným poskytovatelem cloudu je Microsoft Azure.

Během plánování, sestavování nebo migrace má společnost obecně čtyři možnosti partnerství:

- **Samoobslužné s asistencí.** Stávající technický tým provádí migraci s pomocí od Microsoftu.
- **FastTrack for Azure.** K urychlení migrace použijte program Microsoft FastTrack for Azure.
- **Partner řešení.** K urychlení migrace se spojíte s partnery řešení Azure nebo partnery pro cloudová řešení (CSP).
- **Podporované samoobslužné.** Provádění je dokončeno stávajícími technickými pracovníky s podporou Microsoftu.

## <a name="guided-self-service"></a>Samoobslužné s asistencí

Pokud organizace plánuje migraci do Azure vlastními silami, vždy je tu Microsoft, aby na této cestě pomohl. Abychom usnadnili migraci do Azure, Microsoft a jeho partneři vyvinuli rozsáhlou sadu architektur, průvodců, nástrojů a služeb, které snižují riziko a urychlují migraci virtuálních počítačů, aplikací a databází. Tyto nástroje a služby podporují širokou škálu operačních systémů, programovacích jazyků, architektur a databází.

- **Nástroje posouzení a migrace.** Azure poskytuje rozsáhlou řadu nástrojů, které se používají v různých fázích vaší transformaci na cloud, včetně posouzení vaší stávající infrastruktury. Další informace najdete v části Posouzení v dále uvedené kapitole Migrace.
- **[Architektura přechodu na cloud od Microsoftu](../../index.md).** Tato architektura představuje strukturovaný přístup k přechodu a migraci do cloudu. Je založený na postupech osvědčených u mnoha zákaznických iniciativ podporovaných Microsoftem a organizuje se jako posloupnost kroků, od architektury a návrhu až po implementaci. U každého kroku vám podpůrné doprovodné materiály pomůžou s návrhem architektury vlastní aplikace.
- **[Vzory návrhu v cloudu](/azure/architecture/patterns).** Azure poskytuje některé užitečné vzory cloudového návrhu pro sestavování spolehlivých, škálovatelných a zabezpečených úloh v cloudu. Každý vzor popisuje problém, ke kterému se vztahuje, důležité informace týkající se použití tohoto vzoru a příklad s využitím Azure. Většina vzorů zahrnuje ukázky nebo fragmenty kódu, které ukazují, jak tento vzor implementovat v Azure. Jsou ale relevantní pro libovolný distribuovaný systém bez ohledu na to, jestli je hostovaný v Azure nebo na jiných cloudových platformách.
- **[Základy práce s cloudy](/azure/architecture/guide).** Základy vám pomůžou naučit se základní přístupy k implementaci základních konceptů. Tato příručka pomáhá technikům zvážit řešení, která přesahují jednu službu Azure.
- **[Ukázkové scénáře](/azure/architecture/example-scenario).** Příručka obsahuje odkazy na implementace reálného zákazníka, přehled nástrojů, přístupů a procesů, které minulí zákazníci použili k dosažení konkrétních obchodních cílů.
- **[Referenční architektury](/azure/architecture/reference-architectures).** Referenční architektury jsou uspořádané podle scénáře a související architektury jsou seskupené dohromady. Každá architektura zahrnuje doporučené postupy a také důležité informace o škálovatelnosti, dostupnosti, možnostech správy a zabezpečení. Většina zahrnuje také nasaditelné řešení.

## <a name="fasttrack-for-azure"></a>FastTrack for Azure

Program [FastTrack for Azure](https://azure.microsoft.com/roadmap/fasttrack-for-azure) poskytuje přímou asistenci odborníků na Azure a ve spolupráci s partnery pomáhá zákazníkům rychle a bez obav sestavovat řešení Azure. FastTrack přináší osvědčené postupy a nástroje z reálných zákaznických prostředí a pomáhá zákazníkům od instalace, konfigurace a vývoje po produkci řešení Azure, jako například:

- Migrace datacenter
- Windows Server v Azure
- Linux v Azure
- SAP v Azure
- Provozní kontinuita a zotavení po havárii (BCDR)
- Vysokovýkonné výpočetní prostředí*
- Aplikace nativní pro cloud
- DevOps
- Modernizace aplikací
- Analýzy v cloudovém měřítku**
- Inteligentní aplikace
- Inteligentní agenti**
- Modernizace dat v Azure
- Zabezpečení a správa
- Globálně distribuovaná data
- IoT***

*Omezená verze Preview ve Spojených státech, Kanadě, Spojeném království a Západní Evropě

**Omezená verze Preview ve Spojeném království a Západní Evropě

***K dispozici v druhé polovině roku 2019

Během typického zapojení do programu FastTrack for Azure pomáhá Microsoft definovat obchodní vizi, aby plánování a vývoj řešení Azure bylo úspěšné. Tým posuzuje potřeby architektury a poskytuje pokyny, principy návrhu, nástroje a prostředky, které vám pomůžou při sestavování, nasazování a správě řešení Azure. Tým na vyžádání poskytuje kvalifikované partnery pro služby nasazení a pravidelně kontroluje, aby se zajistilo, že nasazení probíhá podle plánu, a pomohly se odstranit překážky.

Toto jsou hlavní fáze typického zapojení do programu FastTrack for Azure:

- **Zjišťování:** Identifikace klíčových účastníků, pochopení cílů nebo vize pro problémy, pro které se hledá řešení, a vyhodnocení požadavků na architekturu.
- **Podpora řešení:** Seznámení s principy návrhu pro vytváření aplikací, kontrola architektury aplikací a řešení a získání pokynů a nástrojů pro zajištění testování konceptu a zavedení do produkčního prostředí.
- **Nepřetržité partnerství:** Technici a programoví manažeři Azure občas provádějí kontrolu, aby se zajistilo, že nasazení probíhá podle plánu, a pomohly se odstranit překážky.

## <a name="microsoft-services-offerings-aligned-to-cloud-adoption-framework-approaches"></a>Nabídky služeb Microsoftu odpovídající přístupům k architektuře přechodu na cloud

![Přístup k architektuře přechodu na cloud služeb Microsoftu](../../../_images/mcs-program-approach.jpg)

**Posouzení:** Služby Microsoftu využívají [jednotný přístup založený na datech a nástrojích](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf), který se skládá z architektonických seminářů, informací o Azure v reálném čase, modelů hrozeb zabezpečení a identity a různých nástrojů, které poskytují přehled o výzvách, rizicích, doporučeních a problémech s existujícím prostředím Azure, přičemž klíčovým výstupem je [plán modernizace na vysoké úrovni](https://download.microsoft.com/download/F/7/2/F72FAD7E-8BBD-4E04-8C7B-9AC4FE04A150/Cloud_Adoption_Discovery_and_Roadmap_Datasheet.pdf).

**Přechod:** Prostřednictvím [Azure Cloud Foundation](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) služeb Microsoftu můžete vytvářet základní návrhy Azure, vzory a architekturu zásad správného řízení tím, že své požadavky namapujete na nejvhodnější referenční architekturu a naplánujete, navrhnete a nasadíte infrastrukturu, správu, zabezpečení a identity potřebné pro úlohy.

**Migrace/optimalizace:** [Řešení modernizace cloudu](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) služeb Microsoftu nabízí komplexní přístup pro přesun aplikací a infrastruktury do Azure a jejich následnou optimalizaci a modernizaci, podpořenou zjednodušenou migrací.

**Inovace:** [Řešení Cloud Center of vynikající verze společnosti Microsoft (CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) nabízí DevOps výukovým Engagement a používá zásady DevOps v kombinaci s předm nativním cloudovým řízením služeb a bezpečnostními prvky zabezpečení, které vám pomůžou při firemních inovacích. Zvyšte flexibilitu a omezte čas na hodnotu v rámci zabezpečené, předvídatelné a flexibilní funkce pro poskytování služeb a provozu.

## <a name="azure-support"></a>Podpora Azure

Pokud máte dotazy nebo potřebujete pomoc, [vytvořte žádost o podporu](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest). Pokud vaše žádost o podporu vyžaduje podrobné technické pokyny, přejděte na [Plány podpory Azure](https://azure.microsoft.com/support/plans), abyste vybrali nejlepší plán pro vaše potřeby.

## <a name="azure-solutions-partner"></a>Partner pro řešení Azure

Certifikovaní poskytovatelé řešení Microsoftu se specializují na poskytování aktuálních zákaznických řešení založených na technologii Microsoftu po celém světě. Optimalizujte firemní cloud s pomocí od zkušeného partnera.

Získejte pomoc od partnerů s předem připravenými nebo vlastními řešeními Azure a partnerů, kteří vám můžou pomoct s nasazením a správou těchto řešení:

- **[Najděte partnera pro cloudová řešení](https://www.microsoft.com/solution-providers/home).** Certifikovaný partner CSP může pomoct plně využít výhod cloudu vyhodnocením obchodních cílů pro přechod na cloud, určením správného cloudového řešení, které vyhovuje obchodním potřebám a pomůže větší agilitě a efektivitě podnikání.
- **[Najděte partnera pro spravované služby](https://www.microsoft.com/solution-providers/search?cacheId=16a3b49b-fef2-449d-bdf0-628008114cca).** Partner pro spravované služby Azure (MSP) vás při přesunu podnikání do Azure pomůže provést všemi aspekty přechodu na cloud. Cloudoví partneři MSP ukáží zákazníkům všechny výhody, které přechod na cloud poskytuje, od konzultací po správu migrace a provozu. Fungují také jako jednotné místo pro obecnou podporu, zřizování a fakturaci, a to vše s flexibilním obchodním modelem průběžných plateb (PAYG).

## <a name="next-steps"></a>Další kroky

Po výběru partnera a strategie podpory je možné aktualizovat [backlogy vydání a iterace](./release-iteration-backlog.md) tak, aby odrážely plánované úsilí a přiřazení.

> [!div class="nextstepaction"]
> [Správa změn pomocí backlogů vydání a iterace](./release-iteration-backlog.md)
