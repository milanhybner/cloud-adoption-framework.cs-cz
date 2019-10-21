---
title: Operace platforem – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Operace platforem – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: aab6dbe2ff8b1037a86317d00d717b4b22052c59
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558048"
---
# <a name="platform-operations-in-cloud-management"></a>Operace s platformou ve správě cloudu

Správa cloudu pokrývá [inventář a viditelnost](./inventory.md), [provozní dodržování předpisů](./operational-compliance.md)a [ochrana a obnovení](./protect.md) může poskytovat dostatečnou úroveň správy cloudu pro většinu úloh v portfoliu IT. To však není dostatečně málo, aby bylo možné podporovat celé portfolio. Tento článek sestaví na nejběžnějším dalším kroku správy cloudu, operací portfolia.

Rychlá studie prostředků v portfoliu IT bude zvýrazňovat vzory napříč podporovanými úlohami. V rámci těchto úloh bude existovat řada běžných platforem. V závislosti na minulých technických rozhodnutích v rámci společnosti se tyto platformy můžou výrazně lišit. U některých organizací bude existovat těžká závislost na SQL serveru, Oracle nebo jiných open source datových platformách. V jiných organizacích může být commonalities rootem na hostujících platformách pro virtuální počítače nebo kontejnery. Jiné můžou mít i jiné společné závislosti na aplikacích nebo systémech pro plánování podnikových zdrojů (ERP), jako je například SAP, Oracle nebo jiné.

Porozumění těmto commonalities umožňuje, aby se tým Cloud managementu specializoval na vyšší úroveň podpory pro tyto platformy.

## <a name="establish-a-service-catalog"></a>Zřízení katalogu služeb

Cílem operací s platformou je vytvořit spolehlivé a opakující se řešení, které může tým pro přijetí cloudu využít k tomu, aby poskytoval platformu, která poskytuje vyšší úroveň obchodního závazku. Tento závazek by mohl snížit pravděpodobnost nebo četnost výpadků, což zlepšuje spolehlivost. Závazek by taky mohl snížit množství ztráty dat nebo času na obnovení, a to v případě selhání systému. Tento závazek často zahrnuje průběžné a centralizované operace pro podporu platformy.

Jelikož tým pro správu cloudu vytváří vyšší úrovně provozní správy a specializace související s konkrétními platformami, přidají se tyto platformy do rostoucího katalogu služeb. Katalog služeb poskytuje samoobslužné nasazení platforem v konkrétní konfiguraci, které dodržuje průběžné operace platforem. Během konverzace o obchodním zarovnání můžou týmy pro správu cloudu a cloudové strategie navrhovat řešení služby Service Catalog jako způsob, jak podniku zlepšit závazky spolehlivosti, provozu a obnovení v řízeném, opakujícím se procesu.

V případě referenčních informací v některých organizacích se jako "schválený seznam" odkazuje na katalog služby rané fáze. Hlavním rozdílem je to, že katalog služeb přináší průběžné provozní závazky z cloudového centra excelence. "Schválený seznam" je podobný v tom, že poskytuje předem schválený seznam řešení, které může tým používat v cloudu, ale obvykle není k dispozici žádný provozní přínos spojený s aplikacemi "schválený seznam". Podobně jako v diskusi mezi centrálním IT a CCoE je rozdíl jedna z priorit. Katalog služeb předpokládá dobrý záměr, ale poskytuje provozní, vládnutí a bezpečnostní guardrailsy, které urychlují inovace. "Schválený seznam" brání inovaci, dokud nebudete moci předat operace, dodržování předpisů a brány zabezpečení pro řešení. Obě jsou životaschopná řešení, ale vyžadují společnost, aby v rámci inovace nebo dodržování předpisů investovala do malého počtu rozhodnutí.

### <a name="building-the-service-catalog"></a>Sestavení katalogu služeb

Správa cloudu se nedoporučuje úspěšně při doručování katalogu služeb v silu. Řádný vývoj katalogu vyžaduje partnerství v rámci centrálního IT nebo cloudového centra excelence (CCoE). Tento přístup má největší úspěšnost, když organizace IT dosáhne CCoE úrovně zralosti, ale může být implementována dřív.

Při sestavování katalogu služeb v rámci modelu CCoE vytvoří tým cloudové platformy požadovanou stavovou platformu. Služby řízení cloudu a týmy cloudového zabezpečení ověřují zásady správného řízení a dodržování předpisů v rámci nasazení. Tým pro správu cloudu zavádí pro tuto platformu průběžné operace. Tým Cloud Automation balí platformu pro škálovatelné a opakované nasazení.

Po zabalení může tým pro správu cloudu přidat balíček do rostoucího katalogu služeb. Odtud může tým přijetí cloudu využít tento balíček nebo jiné v katalogu během nasazování. Jakmile řešení přejde do produkčního prostředí, získá další výhody vylepšené provozní správy a potenciální snížené výpadky v podniku.

> [!NOTE]
> Vytváření katalogu služeb vyžaduje skvělou námahu a dobu od více týmů. Použití katalogu služeb nebo seznamu povolených operací jako mechanismu uzavírání bude mít za chvíli pomalé inovace. Když je inovace prioritou, katalogy služeb by se měly vyvíjet paralelně s dalšími úsilími o přijetí.

## <a name="defining-your-own-platform-operations"></a>Definování vlastních operací platformy

Nástroje a procesy pro správu můžou zlepšit operace platforem. To ale často není dostatečné, aby bylo možné dosáhnout požadovaného stavu stability a spolehlivosti. Pravdivé operace platforem vyžadují zaměření na pilíře kvality architektury. Pokud platforma odůvodňuje hlubší investici v rámci provozu, je třeba zvážit následující pět sloupků, než se platforma bude součástí jakéhokoli katalogu služeb:

1. Škálovatelnost: schopnost systému zvládnout zvýšené zatížení.
2. Dostupnost: poměr doby, po kterou je systém funkční a funguje.
3. Odolnost: schopnost systému obnovit selhání a nadále fungovat.
4. Správa: provozní procesy, které udržují systém běžící v produkčním prostředí.
5. Zabezpečení: Ochrana aplikací a dat před hrozbami.

[Architektura architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) poskytuje přístup k vyhodnocení konkrétních úloh pro přistoupení k těmto pilířům ve snaze zlepšit celkové operace. Tyto pilíře lze použít pro operace platforem i pro operace s úlohou.

## <a name="getting-started-with-specific-platforms"></a>Začínáme s konkrétními platformami

V typických zákaznících Azure se jedná o běžné platformy, které můžou snadno zdůvodnit investici do operací platforem. Týmy pro správu cloudu mají při vytváření požadavků na operace s platformou nebo úplného katalogu služeb začít s těmito postupy.

### <a name="paas-data-operations"></a>PaaS datové operace

Data jsou často první platformou, která zaručuje investice do operací s platformou. Když jsou data hostována v prostředí PaaS (Platform as a Service), účastníci podniku mají v úmyslu požádat o nižší cíl bodu obnovení, aby se minimalizovala ztráta dat. V závislosti na povaze aplikace si taky můžou vyžádat snížení RTO. V obou případech může architektura podporující datová řešení založená na PaaS snadno přizpůsobit určité zvýšené úrovni podpory správy.

Ve většině scénářů jsou náklady na zlepšení závazků za správu snadno odůvodněné, a to i u aplikací, které nejsou klíčové. Tato vylepšení operací s platformou je tak běžné, že mnoho týmů pro správu cloudových řešení se lépe zobrazuje jako rozšířené standardní hodnoty, a to na rozdíl od toho, že se považuje za nepravdivé provozní operace.

### <a name="iaas-data-operations"></a>IaaS datové operace

Když jsou data hostována v tradičním řešení infrastruktury jako služba (IaaS), snaha zvýšit RTO a RPO může být výrazně vyšší. Nicméně přání obchodních zúčastněných stran dosáhnout lepších závazků správy je zřídka ovlivněno PaaS vs. IaaS rozhodnutí. Pokud vše, porozumění základním rozdílům v architektuře, může vyzvat firmu, aby požádal o řešení PaaS nebo závazky, které odpovídají čemu k dispozici v řešeních PaaS. Modernizace všech IaaS datových platforem by se měla považovat za první krok do operací platforem.

V případě, že modernizace není možnost, týmy pro správu cloudu budou běžně upřednostňovat datové platformy založené na IaaS jako první požadovaná služba v katalogu služeb. Díky tomu, že podnik nabízí možnost volby mezi samostatnými datovými servery a clusterovanými, vysoce dostupnými datovými řešeními, je snazší zjednodušit konverzaci obchodních závazků. Základní porozumění provozním vylepšením a zvýšeným nákladům zahodí firmu, aby zajistila nejlepší rozhodnutí pro obchodní procesy a podpůrné úlohy.

### <a name="other-common-platform-operations"></a>Další běžné operace platformy

Kromě datových platforem se jako hostitelé virtuálních počítačů běžně jedná o společnou platformu pro vylepšení provozu. Nejčastěji týmy cloudových platforem a cloudu pro správu cloudu budou investovat do vylepšení hostitelů VMWare nebo řešení kontejnerů, aby se zlepšila stabilita a spolehlivost hostitelů, které podporují virtuální počítače, které jsou v nich napájené. Správné operace na jednom hostiteli nebo kontejneru můžou zlepšit RPO/RTO několika úloh. Tento přístup vytvoří vylepšené obchodní závazky, ale distribuuje investici. Vylepšené závazky a snížené náklady zjednodušují vylepšení správy cloudu a operací platforem.

## <a name="next-steps"></a>Další kroky

V paralelním prostředí s vylepšeními operací s platformou se týmy pro správu cloudu taky zaměřují na vylepšení [operací s úlohou](./workload.md) v horních 20% nebo méně produkčních úlohách.

> [!div class="nextstepaction"]
> [Vylepšení operací s úlohou](./workload.md)
