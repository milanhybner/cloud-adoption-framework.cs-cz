---
title: Operace platforem – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Operace platforem – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 6a2cf644a7c046dfb62f6049c2eae6b283e6552b
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565076"
---
# <a name="platform-operations-in-cloud-management"></a>Operace s platformou ve správě cloudu

Základní plán správy cloudu, který pokrývá [inventář a viditelnost](./inventory.md), [provozní dodržování předpisů](./operational-compliance.md)a [ochrana a obnovení](./protect.md) , může poskytovat dostatečnou úroveň správy cloudu pro většinu úloh v portfoliu IT. Nicméně tento směrný plán je pro podporu celého portfolia dostatečně málo. Tento článek sestaví na nejběžnějším dalším kroku správy cloudu, operací portfolia.

Rychlá studie prostředků v portfoliu IT zvýrazňuje vzory napříč úlohami, které jsou podporované. V rámci těchto úloh bude existovat řada běžných platforem. V závislosti na minulých technických rozhodnutích v rámci společnosti se tyto platformy můžou výrazně lišit.

U některých organizací dojde k těžké závislosti na SQL Server, Oracle nebo jiných open source datových platformách. V jiných organizacích může být commonalities rootem na hostujících platformách pro virtuální počítače (VM) nebo kontejnery. Další mohou mít i jiné společné závislosti na aplikacích nebo systémech pro plánování podnikových zdrojů (ERP), jako jsou například SAP, Oracle nebo jiné.

Díky porozumění těmto commonalities se tým pro správu cloudu může specializovat na vyšší úroveň podpory pro tyto platformy s určenou prioritou.

## <a name="establish-a-service-catalog"></a>Zřízení katalogu služeb

Cílem operací platforem je vytvořit spolehlivá a opakující se řešení, která tým pro přijetí do cloudu může použít k zajištění platformy, která poskytuje vyšší úroveň obchodního závazku. Tento závazek by mohl snížit pravděpodobnost nebo četnost výpadků, což zvyšuje spolehlivost. V případě selhání systému může závazek také snížit množství ztráty dat nebo času na obnovení. Takový závazek často zahrnuje průběžné a centralizované operace pro podporu platformy.

Jelikož tým pro správu cloudu vytváří vyšší úrovně provozní správy a specializace související s konkrétními platformami, přidají se tyto platformy do rostoucího katalogu služeb. Katalog služeb poskytuje samoobslužné nasazení platforem v konkrétní konfiguraci, které dodržuje průběžné operace platforem. Během konverzace o obchodním vyrovnání můžou týmy pro správu cloudu a cloudové strategie navrhovat řešení služby Service Catalog jako způsob, jak podniku zlepšit závazky spolehlivosti, provozu a obnovení v řízeném, opakujícím se procesu.

V případě referenčních informací některé organizace odkazují na předběžnou fázi katalogu služeb jako _seznam schválených_. Hlavním rozdílem je to, že katalog služeb přináší průběžné provozní závazky z cloudového centra excelence (CCoE). Seznam schválených je podobný v tom, že poskytuje předschválený seznam řešení, které může tým používat v cloudu. Obvykle ale není k dispozici žádný provozní přínos spojený s aplikacemi na seznamu schválených aplikací.

Podobně jako v diskusi mezi centrálním IT a CCoE je rozdíl jedna z priorit. Katalog služeb předpokládá dobrý záměr, ale poskytuje provozní, vládnutí a bezpečnostní guardrailsy, které urychlují inovace. Schválený seznam brání inovaci, dokud nebudete moci předat operace, dodržování předpisů a brány zabezpečení pro řešení. Obě řešení jsou životaschopná, ale vyžadují společnost, aby v rámci inovace nebo dodržování předpisů investovala do malého počtu rozhodnutí.

### <a name="build-the-service-catalog"></a>Sestavení katalogu služeb

Správa cloudu se nedoporučuje úspěšně při doručování katalogu služeb v silu. Řádný vývoj katalogu vyžaduje partnerství v rámci ústředního IT nebo CCoE. Tento přístup má největší úspěšnost, když organizace IT dosáhne CCoE úrovně zralosti, ale může být implementována dřív.

Při sestavování katalogu služeb v rámci modelu CCoE tým cloudové platformy vytvoří platformu požadovaného stavu. Služby řízení cloudu a týmy cloudového zabezpečení ověřují zásady správného řízení a dodržování předpisů v rámci nasazení. Tým pro správu cloudu zavádí pro tuto platformu průběžné operace. A tým Cloud Automation zabalí platformu pro škálovatelné a opakované nasazení.

Po zabalení platformy ho tým pro správu cloudu může přidat do rostoucího katalogu služeb. Odtud může tým přijetí cloudu použít balíček nebo jiné v katalogu během nasazování. Až řešení přejde do produkčního prostředí, bude mít za následek další výhody vylepšené provozní správy a potenciálně omezené fungování v podniku.

> [!NOTE]
> Vytváření katalogu služeb vyžaduje skvělou námahu a dobu od více týmů. Použití katalogu služeb nebo seznamu schválených jako mechanismus uzavírání bude mít za chvíli pomalé inovace. Když je inovace prioritou, katalogy služeb by se měly vyvíjet paralelně s dalšími úsilími o přijetí.

## <a name="define-your-own-platform-operations"></a>Definování vlastních operací platformy

I když nástroje pro správu a procesy mohou pomoci vylepšit operace s platformou, což často není dostatečné pro dosažení požadovaných stavů stability a spolehlivosti. Pravdivé operace platforem vyžadují zaměření na pilíře kvality architektury. Pokud platforma odůvodňuje hlubší investici v rámci provozu, je třeba zvážit následující pět sloupků, než se platforma bude součástí jakéhokoli katalogu služeb:

- **Škálovatelnost:** Schopnost systému zpracovávat zvýšené zatížení.
- **Dostupnost:** Procento času, po který je systém funkční a funguje.
- **Odolnost:** Schopnost systému obnovit selhání a nadále fungovat.
- **Správa:** Provozní procesy, které udržují systém běžící v produkčním prostředí.
- **Zabezpečení:** Ochrana aplikací a dat před hrozbami.

[Architektura architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) poskytuje přístup k vyhodnocení konkrétních úloh pro přistoupení k těmto pilířům ve snaze zlepšit celkové operace. Tyto pilíře lze použít pro operace platforem i pro operace s úlohou.

## <a name="get-started-with-specific-platforms"></a>Začínáme s konkrétními platformami

Platformy popsané v dalších oddílech jsou společné pro typické zákazníky Azure a můžou snadno zdůvodnit investici do operací platforem. Týmy pro správu cloudu mají při sestavování požadavků na operace s platformou nebo úplného katalogu služeb začít s nimi.

### <a name="paas-data-operations"></a>PaaS datové operace

Data jsou často první platformou, která zaručuje investice do operací s platformou. Když jsou data hostována v prostředí PaaS (Platform as a Service), účastníci obchodních stran mají v úmyslu vyžádat si pro minimalizaci ztráty dat snížený cíl bodu obnovení (RPO). V závislosti na povaze aplikace si taky můžou vyžádat snížení cíle doby obnovení (RTO). V obou případech může architektura, která podporuje datová řešení založená na PaaS, snadno přizpůsobit určitou zvýšenou úroveň podpory správy.

Ve většině scénářů jsou náklady na zlepšení závazků za správu snadno odůvodněné, a to i u aplikací, které nejsou klíčové. Tato vylepšení operací s platformou je tak běžné, že mnoho týmů pro správu cloudu se lépe zobrazuje jako rozšířené standardní hodnoty, nikoli jako zlepšení provozu na platformě.

### <a name="iaas-data-operations"></a>IaaS datové operace

Když jsou data hostována v tradičním řešení infrastruktury jako služba (IaaS), snaha o vylepšení RPO a RTO může být výrazně vyšší. Nicméně přání obchodních zúčastněných stran dosáhnout lepších závazků pro správu je zřídka ovlivněno PaaS a rozhodnutím IaaS. Pokud je to vše, může se při porozumění základních rozdílů v architektuře vyzvat firma, aby požádal o řešení PaaS nebo závazky, které odpovídají dostupnosti v řešeních PaaS. Modernizace všech IaaS datových platforem by se měla považovat za první krok do operací platforem.

V případě, že modernizace není možnost, týmy pro správu cloudu běžně v katalogu služeb přednostně IaaS datové platformy založené na jako první požadovaná služba. Díky tomu, že podnik nabízí možnost volby mezi samostatnými datovými servery a clusterovanými, vysoce dostupnými datovými řešeními, je snazší zjednodušit konverzaci obchodních závazků. Základní porozumění provozním vylepšením a zvýšeným nákladům si zajistěte, aby firma zajistila nejlepší rozhodnutí pro obchodní procesy a podpůrné úlohy.

### <a name="other-common-platform-operations"></a>Další běžné operace platformy

Kromě datových platforem se jako hostitelé virtuálních počítačů běžně jedná o společnou platformu pro vylepšení provozu. Nejčastější týmy cloudových platforem a cloudových řešení investují do vylepšení hostitelů VMware nebo řešení kontejnerů. Tyto investice můžou zlepšit stabilitu a spolehlivost hostitelů, které podporují virtuální počítače, které jsou zase napájené z úloh. Správné operace na jednom hostiteli nebo kontejneru můžou zlepšit RPO nebo RTO několika úloh. Tento přístup vytvoří vylepšené obchodní závazky, ale distribuuje investici. Vylepšené závazky a snížené náklady jsou zkombinovány, aby byly mnohem snazší s vylepšením v oblasti správy cloudu a operací platforem.

## <a name="next-steps"></a>Další kroky

V paralelním prostředí s vylepšeními operací s platformou se týmy pro správu cloudu zaměřují také na vylepšení [operací s úlohou](./workload.md) v horních 20 procentech nebo méně produkčních úlohách.

> [!div class="nextstepaction"]
> [Vylepšení operací s úlohou](./workload.md)
