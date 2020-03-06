---
title: Principy návrhu a pokročilé operace
description: Naučte se používat principy návrhu a rozšířené možnosti k vytvoření nabídky, která poskytuje minimální úroveň obchodního závazku pro všechny podporované úlohy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a5861b23e5cc408957f922472dd6ee863c7c13fa
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341041"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Použití principů návrhu a pokročilých operací

První tři disciplíny správy cloudu popisují směrný plán správy. Základní plán správy musí zahrnovat standardní obchodní závazek pro minimalizaci obchodních přerušení a urychlení obnovení při přerušení služby. Většina standardních hodnot správy zahrnuje oborové zaměření na zachování "inventáře a viditelnosti", "provozní dodržování" a "ochranu a obnovení".

Účelem směrného plánu správy je vytvořit konzistentní nabídku, která poskytuje minimální úroveň obchodního závazku pro všechny podporované úlohy. Tato standardní hodnota pro běžné a opakující se nabídky správy umožňuje týmu doručovat vysoce optimalizovanou míru provozní správy s minimální odchylkou. Tato standardní nabídka ale nemusí poskytovat dostatečný závazek k podnikání.

Diagram v další části znázorňuje tři způsoby, jak jít nad rámec standardních hodnot správy.

Standardní hodnoty pro správu by měly splňovat minimální závazek, který vyžádala 80% z nejnižší úlohy kritické pro kritickou náročnost v portfoliu. Základní hodnoty by se neměly použít pro klíčové úlohy. Ani by se neměl použít u běžných platforem, které jsou sdíleny napříč úlohami. Tyto úlohy vyžadují zaměření na principy navrhování a pokročilé operace.

## <a name="advanced-operations-options"></a>Rozšířené možnosti operací

Existují tři Doporučené cesty pro zlepšení obchodních závazků nad rámec standardních hodnot správy, jak je znázorněno v následujícím diagramu:

![Pokročilé operace](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Rozšířená standardní hodnota správy

Jak je uvedeno v příručce pro správu Azure, rozšířená standardní hodnota správy používá nástroje Cloud-Native ke zvýšení doby provozu a snížení doby obnovení. Vylepšení jsou významná, ale méně, než v rámci specializace zatížení nebo platformy. Výhodou rozšířeného směrného plánu správy je poměrně významné snížení nákladů a času implementace.

## <a name="management-specialization"></a>Specializace správy

Aspekty úloh a operací platforem můžou vyžadovat změny v principech návrhu a architektury. Tyto změny můžou nějakou dobu trvat a můžou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení firemních závazků.

Pro úlohy, které opravňují vyšší investice do splnění obchodního závazku, je specializace operací klíč.

## <a name="areas-of-management-specialization"></a>Oblasti správy – specializace

Existují dvě oblasti specializace:

- **Specializace platformy:** Investovat do pokračujících operací sdílené platformy a distribuujte si investici napříč několika úlohami.
- **Specializace úloh:** Investovat do probíhajících operací konkrétního zatížení, která je obecně rezervovaná pro klíčové úlohy.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Špičkové centrum IT nebo cloudové centra (CCoE)

Rozhodnutí o specializaci platforem a specializaci úloh jsou založená na závažnosti a dopadu jednotlivých úloh. Nicméně tato rozhodnutí jsou také indikativní pro větší kulturní rozhodnutí mezi centrálními a CCoE organizačními modely IT.

Specializace podle úloh často podněcuje kulturní změnu. Tradiční IT a centrální IT procesy sestavují proces, který může poskytovat podporu ve velkém měřítku. Podpora škálování je více dosažitelná pro opakující se služby, které se nacházejí ve standardních hodnotách správy, rozšířených standardních hodnotách nebo dokonce operacích platforem. Specializace úloh se často nemění. Tato nedostatečná škála usnadňuje centralizované organizaci IT poskytovat potřebnou podporu bez omezení organizačního měřítka.

Cloudové centrum špičkového přístupu se dá využít i v případě, že záměrné delegace zodpovědnosti a selektivní centralizaci. Specializace úloh představuje lepší sbližování s přístupem k delegovaným zodpovědností CCoE.

Přirozené zarovnání rolí v CCoE je popsáno níže:

- Tým cloudové platformy pomáhá vytvářet běžné platformy, které podporují více týmů pro přijímání v cloudu.
- Tým Cloud Automation rozšiřuje tyto platformy na nasaditelné prostředky v katalogu služeb.
- Správa cloudu zajišťuje centrálně standardní hodnoty pro správu a pomáhá podporovat používání katalogu služeb.
- Ale obchodní jednotka (ve formě týmu pro přijímání obchodních DevOps nebo cloudu pro přijetí do cloudu) udržuje zodpovědnost za každodenní operace úlohy, kanálu nebo výkonu.

Vzhledem k tomu, že je možné zarovnat oblasti správy, mohou centrální IT a CCoE modely obecně doručovat specializaci platformy s minimálními kulturními změnami. Poskytování na specializaci úloh může být pro centrální IT týmy trochu složitější.

## <a name="management-specialization-processes"></a>Procesy specializace správy

V rámci každé specializace se následující čtyři kroky doručí v rámci oboru, iterativního přístupu. Tento přístup vyžaduje partnerství mezi přijetím do cloudu, odborníky na cloudovou platformou, automatizací cloudu a odborníky na správu cloudu k vytvoření životaschopné a informované smyčky

- **Vylepšit návrh systému:** Vylepšete návrh běžných systémů (platforem) nebo specifických úloh pro efektivní minimalizaci přerušení.
- **Automatizovaná náprava:** Některá vylepšení nejsou nákladově efektivní. V takových případech může být vhodnější automatizovat nápravu a snížit dopad přerušení.
- **Škálovat řešení:** Díky vylepšení systémů a automatizované nápravy můžete škálovat tyto změny v celém prostředí prostřednictvím katalogu služeb.
- **Nepřetržité zlepšování:** Můžete použít různé nástroje pro monitorování ke zjištění přírůstkových vylepšení, která se mají řešit při dalším průchodu návrhu, automatizace a škálování systému.

### <a name="improve-system-design"></a>Vylepšení návrhu systémů

Vylepšení návrhu systémů představuje nejúčinnější přístup k vylepšení provozu jakékoliv běžné platformy. Vylepšení návrhu systému můžou zvýšit stabilitu a snížit provozní přerušení. Návrh jednotlivých systémů je mimo rozsah pohledu na prostředí, který prezentujeme v rámci této řady článků o přechodu na cloud. Jako doplněk k těmto článkům nabízí rozhraní architektury Azure osvědčené postupy pro zlepšení odolnosti a návrhu specifického systému. Tato vylepšení návrhu můžete uplatnit na návrh systémů na platformu nebo konkrétní úlohu.

Rozhraní architektury Azure se zaměřuje na vylepšení pěti pilířů návrhu systémů:

- **Škálovatelnost:** Škálování běžných prostředků platformy pro zpracování zvýšené zátěže.
- **Dostupnost:** Snížení doby provozu tím, že zlepšíte potenciál v době provozu.
- **Odolnost:** Zlepšení doby obnovení pro snížení doby trvání přerušení.
- **Zabezpečení:** Ochrana aplikací a dat před externími hrozbami.
- **Správa:** Provozní procesy specifické pro tyto běžné prostředky platforem.

Většina přerušení běžného chodu firmy vyplývá z určité formy technického dluhu nebo nedostatku v architektuře. U stávajících nasazení se vylepšení návrhu systémů dají vnímat jako splátky technického dluhu. U nových nasazení můžete na vylepšení návrhu systémů nahlížet jako na možnost, jak technickému dluhu předejít. V další části, "Automatizovaná náprava", se podíváme na způsoby, jak řešit Technický dluh, který nemůže nebo neměl být řešen.

Další informace o [architektuře architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars)vám pomůžou vylepšit návrh systému. Vzhledem k tomu, že se váš návrh systému zlepšuje, vraťte se do tohoto článku a najděte nové příležitosti, které vám pomůžou zlepšit a škálovat vylepšení ve vašem prostředí.

### <a name="automated-remediation"></a>Automatizovaná náprava

Technický dluh nelze nebo neměl vyřešit. Řešení by například mohlo být příliš nákladné. Může být plánováno, ale může mít dlouhou dobu trvání projektu. Provozní přerušení nemusí mít žádný významný dopad na chod firmy, jinak se obchodní Priorita může rychle zotavit místo investice do odolnosti.

Pokud vyřešení technického dluhu není požadovaným postupem, je obvykle dalším požadovaným krokem automatizovaná náprava. Ta se obvykle zajišťuje pomocí služeb Azure Automation a Azure Monitor, které detekují trendy a poskytují automatizovanou nápravu.

Další rady k automatizované nápravě najdete v tématu věnovaném [upozorněním a službě Azure Automation](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Škálování řešení pomocí katalogu služeb

Základním kamenem specializace podle platformy a provozu platforem je dobře spravovaný katalog služeb. Jeho prostřednictvím se vylepšení návrhu systémů a nápravy škálují do celého prostředí. Týmy pro cloudové platformy a automatizaci cloudu společně vytvářejí opakovatelná řešení pro nejběžnější platformy v jakémkoliv prostředí. Pokud se ale tato řešení nepoužijí konzistentně, může Správa cloudu poskytovat jenom něco větší než základní nabídka.

Aby bylo možné maximalizovat přijímání a minimalizaci režie údržby jakékoli optimalizované platformy, měla by být platforma přidána do katalogu služeb. Každou aplikaci v katalogu služeb je možné nasadit pro interní použití prostřednictvím katalogu nebo nabídnout externím uživatelům přes Marketplace.

Informace o publikování do katalogu služeb najdete v tématu série [publikování do katalogu služeb](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Průběžné vylepšování

Specializace podle platformy i provoz platforem jsou silně závislé na smyčkách zpětné vazby mezi týmy přechodu, platforem, automatizace a správy. Zhmotnění těchto smyček zpětné vazby v datech umožňuje každému týmu přijímat moudrá rozhodnutí. Aby operace platforem dosáhly dlouhodobých obchodních závazků, je důležité využít přehledy, které jsou specifické pro centralizovanou platformu. Vzhledem k tomu, že kontejnery a SQL Server jsou dvě nejběžnější centrálně spravované platformy, zvažte, jak začít s shromažďováním dat průběžného zlepšování, a to pomocí následujících článků:

- [Výkon kontejnerů](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Výkon databází PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Výkon databází IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
