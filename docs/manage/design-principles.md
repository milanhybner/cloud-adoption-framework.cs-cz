---
title: Použití principů návrhu a pokročilých operací
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Použití principů návrhu a pokročilých operací
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 8ea3610ed65ae45d924ca65ef26d249ed8343d0b
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979970"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Použití principů návrhu a pokročilých operací

První tři obory správy cloudu popisují směrný plán správy. Základní plán správy musí zahrnovat standardní obchodní závazek pro minimalizaci obchodních přerušení a urychlení obnovení při přerušení služby. Většina standardních hodnot správy zahrnuje oborové zaměření na zachování "inventáře a viditelnosti", "provozní dodržování" a "ochranu a obnovení".

Účelem směrného plánu správy je vytvořit konzistentní nabídku, která poskytuje minimální úroveň obchodního závazku pro všechny podporované úlohy. Tato standardní hodnota pro běžné a opakující se nabídky správy umožňuje týmu doručovat vysoce optimalizovanou míru provozní správy s minimální odchylkou. Tato standardní nabídka ale nemusí poskytovat dostatečný závazek k podnikání. 

Diagram v další části znázorňuje tři způsoby, jak jít nad rámec standardních hodnot správy.

Standardní hodnoty pro správu by měly splňovat minimální závazek, který vyžádala 80% z nejnižší úlohy kritické pro kritickou náročnost v portfoliu. Základní hodnoty by se neměly použít pro klíčové úlohy. Ani by se neměl použít u běžných platforem, které jsou sdíleny napříč úlohami. Tyto úlohy vyžadují zaměření na principy navrhování a pokročilé operace.

## <a name="advanced-operations-options"></a>Rozšířené možnosti operací

Existují tři Doporučené cesty pro zlepšení obchodních závazků nad rámec standardních hodnot správy, jak je znázorněno v následujícím diagramu:

![Pokročilé operace](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Rozšířená standardní hodnota správy

Jak je uvedeno v příručce pro správu Azure, rozšířená standardní hodnota správy používá nástroje Cloud-Native ke zvýšení doby provozu a snížení doby obnovení. Vylepšení jsou významná, ale méně, než v rámci specializace zatížení nebo platformy. Výhodou rozšířeného směrného plánu správy je poměrně významné snížení nákladů a času implementace.

## <a name="management-specialization"></a>Specializace správy

Aspekty úloh a operací platforem můžou vyžadovat změny v principech návrhu a architektury. Tyto změny můžou nějakou dobu trvat a můžou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení obchodního závazku.

Pro úlohy, které opravňují vyšší investice do splnění obchodního závazku, je specializace operací klíč.

## <a name="areas-of-management-specialization"></a>Oblasti správy – specializace

Existují dvě oblasti specializace:

- **Specializace platforem**: investovat do probíhajících operací sdílené platformy a distribuovat investice do různých úloh.
- **Specializace úloh**: investovat do probíhajících operací konkrétního zatížení, která je obecně rezervovaná pro klíčové úlohy.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Špičkové centrum IT nebo cloudové centra (CCoE)

Rozhodnutí o specializaci platforem a specializaci úloh jsou založená na závažnosti a dopadu jednotlivých úloh. Nicméně tato rozhodnutí jsou také indikativní pro větší kulturní rozhodnutí mezi centrálními a CCoE organizačními modely IT.

Specializace úloh často aktivuje kulturní změnu. Tradiční IT a centrální IT procesy sestavují proces, který může poskytovat podporu ve velkém měřítku. Podpora škálování je více dosažitelná pro opakující se služby, které se nacházejí ve standardních hodnotách správy, rozšířených standardních hodnotách nebo dokonce operacích platforem. Specializace úloh se často nemění. Tato nedostatečná škála usnadňuje centralizované organizaci IT poskytovat potřebnou podporu bez omezení organizačního měřítka.

Cloudové centrum špičkového přístupu se dá využít i v případě, že se záměrné delegace zodpovědnosti a selektivní centralizace. Specializace úloh představuje lepší sbližování s přístupem k delegovaným zodpovědností CCoE. 

Přirozené zarovnání rolí v CCoE je popsáno níže:
- Tým cloudové platformy pomáhá vytvářet běžné platformy, které podporují více týmů pro přijímání v cloudu. 
- Tým Cloud Automation rozšiřuje tyto platformy na nasaditelné prostředky v katalogu služeb. 
- Správa cloudu zajišťuje centrálně standardní hodnoty pro správu a pomáhá podporovat používání katalogu služeb. 
- Ale obchodní jednotka (ve formě týmu pro přijímání obchodních DevOps nebo cloudu pro přijetí do cloudu) udržuje zodpovědnost za každodenní operace úlohy, kanálu nebo výkonu.

Vzhledem k tomu, že je možné zarovnat oblasti správy, mohou centrální IT a CCoE modely obecně doručovat specializaci platformy s minimálními kulturními změnami. Poskytování na specializaci úloh může být pro centrální IT týmy trochu složitější.

## <a name="management-specialization-processes"></a>Procesy specializace správy

V rámci každé specializace se následující čtyři kroky doručí v rámci oboru, iterativního přístupu. Tento přístup vyžaduje partnerství mezi přijetím do cloudu, odborníky na cloudovou platformou, automatizací cloudu a odborníky na správu cloudu k vytvoření životaschopné a informované smyčky

- **Zlepšení návrhu systému**: Vylepšete návrh běžných systémů (platforem) nebo specifických úloh pro efektivní minimalizaci přerušení.
- **Automatizace nápravy**: některá vylepšení nejsou nákladově efektivní. V takových případech může být vhodnější automatizovat nápravu a snížit dopad přerušení.
- **Škálované řešení**: v rámci navrhování a automatizované nápravy je možné tyto změny škálovat v celém prostředí prostřednictvím katalogu služeb.
- **Průběžné vylepšování**: můžete použít různé nástroje pro monitorování k vyhledání přírůstkových vylepšení pro další předání systému, automatizace a škálování.

### <a name="improve-system-design"></a>Vylepšení návrhu systému

Zlepšení návrhu systému představuje nejúčinnější přístup ke zlepšení provozu jakékoli běžné platformy. Vylepšení návrhu systému můžou zvýšit stabilitu a snížit provozní přerušení. Návrh jednotlivých systémů je mimo rozsah pro zobrazení prostředí, které se provádí v rámci architektury cloudového přijetí. Jako doplněk k tomuto rozhraní nabízí architektura architektury Azure osvědčené postupy pro zlepšení odolnosti a návrhu konkrétního systému. Tato vylepšení návrhu můžete uplatnit na návrh systémů na platformu nebo konkrétní úlohu.

Architektura architektury Azure se zaměřuje na zlepšení napříč pěti pilíři návrhu systému:

- **Škálovatelnost**: škálování běžných prostředků platformy pro zpracování zvýšené zátěže.
- **Dostupnost**: snížení úspěšnosti v podniku tím, že se zlepší potenciální doba provozu.
- **Odolnost**proti chybám: zlepšení doby obnovení, aby se snížila doba přerušení.
- **Zabezpečení**: Ochrana aplikací a dat před externími hrozbami.
- **Správa**: provozní procesy specifické pro tyto běžné prostředky platforem.

Většina obchodních přerušení je rovna určité formě technického dluhu nebo nedostatku architektury. U stávajících nasazení se vylepšení návrhu systémů dají zobrazit jako platby na stávající Technický dluh. U nových nasazení si můžete zobrazit vylepšení návrhu systémů, protože se vyhnete technickým dluhům. V další části, "Automatizovaná náprava", se podíváme na způsoby, jak řešit Technický dluh, který nemůže nebo neměl být řešen.

Další informace o [architektuře architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars)vám pomůžou vylepšit návrh systému. Vzhledem k tomu, že se váš návrh systému zlepšuje, vraťte se do tohoto článku a najděte nové příležitosti, které vám pomůžou zlepšit a škálovat vylepšení ve vašem prostředí.

### <a name="automated-remediation"></a>Automatizovaná náprava

Technický dluh nelze nebo neměl vyřešit. Řešení může být příliš nákladné, aby bylo možné ho opravit. Může být plánováno, ale může mít dlouhou dobu trvání projektu. Provozní přerušení nemusí mít žádný významný dopad na chod firmy, jinak se obchodní Priorita může rychle zotavit místo investice do odolnosti.

Pokud rozlišení technického dluhu není požadovanou cestou, automatizovaná náprava je často požadovaným dalším krokem. Použití Azure Automation a Azure Monitor k detekci trendů a zajištění automatizované nápravy je nejběžnějším přístupem k automatizované nápravě.

Pokyny k automatizované nápravě najdete v tématu [Azure Automation a upozornění](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Škálování řešení pomocí katalogu služeb

Základem specializace platformy a operací platforem je dobře spravovaný katalog služeb. To je způsob, jakým jsou vylepšení pro navrhování a nápravu systémů škálovaná v rámci prostředí. Tým cloudové platformy a tým Cloud Automation si můžete na nejběžnější platformy v jakémkoli prostředí vytvořit opakovaně použitelná řešení. Pokud se ale tato řešení nepoužijí konzistentně, může Správa cloudu poskytovat jenom něco větší než základní nabídka.

Aby bylo možné maximalizovat přijímání a minimalizaci režie údržby jakékoli optimalizované platformy, měla by být platforma přidána do katalogu služeb. Každá aplikace v katalogu se dá nasadit pro interní spotřebu prostřednictvím katalogu služeb nebo jako nabídka Marketplace pro externí zákazníky.

Informace o publikování do katalogu služeb najdete v tématu série [publikování do katalogu služeb](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Nepřetržité zlepšování

Specializace platformy a operace platforem jsou závislé na silných smyčkách zpětné vazby mezi týmy pro přijetí, platformu, automatizaci a správu. Na základě těchto smyček zpětné vazby v datech je každému týmu možné provádět rozhodnutí. Aby operace platforem dosáhly dlouhodobých obchodních závazků, je důležité využít přehledy, které jsou specifické pro centralizovanou platformu. Vzhledem k tomu, že kontejnery a SQL Server jsou dvě nejběžnější centrálně spravované platformy, zvažte, jak začít s shromažďováním dat průběžného zlepšování, a to pomocí následujících článků: 

- [Výkon kontejneru](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Výkon databáze PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Výkon databáze IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
