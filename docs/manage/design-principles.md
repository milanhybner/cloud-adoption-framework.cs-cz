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
ms.openlocfilehash: 8595dbadf5a10e19303a50f8eead1ae753612586
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683570"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Použití principů návrhu a pokročilých operací

První tři obory správy cloudu popisují směrný plán správy. Základní plán správy musí zahrnovat standardní obchodní závazek pro minimalizaci obchodních přerušení a urychlení obnovení při přerušení služby. Většina standardních hodnot správy zahrnuje oborové zaměření na údržbu inventáře a viditelnosti, "provozní dodržování" a "ochrana a obnovení".

Účelem směrného plánu správy je vytvořit konzistentní nabídku, která poskytuje minimální úroveň obchodního závazku pro všechny podporované úlohy. Tato standardní hodnota pro běžné opakované nabídky správy umožňuje týmu doručovat vysoce optimalizovanou míru provozní správy s minimální odchylkou. Tato standardní nabídka ale nemůže poskytnout dostatečně kvalitní závazek na firmu. Následující obrázek a odrážky seosnovují tři způsoby, jak jít nad rámec standardních hodnot správy.

Standardní hodnoty pro správu by měly splňovat minimální závazek, který vyžaduje 80% nejnižší zátěže v portfoliu. Základní hodnoty by se neměly použít pro klíčové úlohy. Ani by se neměl použít u běžných platforem sdílených napříč úlohami. Ty vyžadují zaměření na principy navrhování a pokročilé operace.

## <a name="advanced-operations-options"></a>Rozšířené možnosti operací

Existují tři Doporučené cesty pro zlepšení obchodních závazků nad rámec standardních hodnot správy.

![Pokročilé operace](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Rozšířená standardní hodnota správy

Jak je uvedeno v příručce pro správu Azure, rozšířená standardní hodnota správy používá cloudové nativní nástroje ke zvýšení doby provozu a snížení doby obnovení. Tato vylepšení jsou významná, ale výrazně méně, než v rámci specializace zatížení nebo platformy. Výhodou rozšířeného směrného plánu správy je poměrně významné snížení nákladů a času implementace.

## <a name="management-specialization"></a>Specializace správy

Aspekty úloh a operací platforem můžou vyžadovat změny v principech návrhu a architektury. Tyto změny můžou nějakou dobu trvat a můžou mít za následek zvýšené provozní výdaje. Aby bylo možné snížit počet úloh, které vyžadují takové investice, může vylepšený směrný plán správy zajistit dostatečné vylepšení obchodního závazku.

Pro úlohy, které opravňují vyšší investice do splnění obchodního závazku, je specializace operací klíč.

## <a name="areas-of-management-specialization"></a>Oblasti správy – specializace

Existují dvě oblasti specializace:

- **Specializace platformy:** Investovat do pokračujících operací sdílené platformy a distribuujte si investici napříč několika úlohami.
- **Specializace úloh:** Investovat do probíhajících operací konkrétního zatížení, které jsou obecně rezervované pro klíčové úlohy.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Špičkové centrum IT nebo cloudové centra (CCoE)

Rozhodnutí o specializaci platforem a specializaci úloh jsou založená na závažnosti a dopadu jednotlivých úloh. Toto rozhodnutí je ale také indikativní pro větší kulturní rozhodnutí mezi centrálními a CCoE organizačními modely IT.

Specializace úloh často aktivuje kulturní změnu. Tradiční IT a centrální IT procesy sestavují proces, který může poskytovat podporu ve velkém měřítku. Podpora škálování je více dosažitelná pro opakující se služby, které se nacházejí ve standardních hodnotách správy, rozšířených standardních hodnotách nebo dokonce operacích platforem. Specializace úloh se často nemění. Tato nedostatečná škála usnadňuje centralizované organizaci IT poskytovat potřebnou podporu bez omezení organizačního měřítka.

Cloudové centrum špičkového přístupu se dá využít i v případě, že se záměrné delegace zodpovědnosti a selektivní centralizace. Specializace úloh představuje lepší sbližování s přístupem k delegovaným zodpovědností CCoE. Následující text popisuje přirozené zarovnání rolí v CCoE. Tým cloudové platformy pomáhá vytvářet běžné platformy, které podporují více týmů pro přijímání v cloudu. Tým služby Cloud Automation rozšiřuje tyto možnosti na nasaditelné prostředky v katalogu služeb. Správa cloudu zajišťuje centrálně standardní hodnoty pro správu a pomáhá podporovat používání katalogu služeb. Ale obchodní jednotka (ve formě týmu pro přijímání obchodních DevOps nebo cloudu pro přijetí do cloudu) udržuje zodpovědnost za každodenní operace úlohy, kanálu nebo výkonu.

Když zarovnáváte oblasti správy, centrální IT a CCoE modely můžou obecně doručovat specializaci platformy s minimálními kulturními změnami. Poskytování na specializaci úloh může být pro centrální IT týmy trochu složitější.

## <a name="management-specialization-processes"></a>Procesy specializace správy

V rámci každé specializace se následující čtyři kroky doručí v rámci oboru, iterativního přístupu. Tento přístup bude vyžadovat partnerství s přijetím do cloudu, odborníky na cloudovou platformu, automatizací cloudu a odborníky na správu cloudu a vytvořit tak životaschopnou a informující smyčk

- **Vylepšit návrh systému:** Vylepšete návrh běžných systémů (platforem) nebo specifických úloh pro efektivní minimalizaci přerušení.
- **Automatizovaná náprava:** Některá vylepšení nejsou nákladově efektivní. V takových případech může být vhodnější automatizovat nápravu a snížit dopad přerušení.
- **Škálovat řešení:** Díky vylepšení systémů a automatizované nápravy je možné tyto změny škálovat v celém prostředí prostřednictvím katalogu služeb.
- **Nepřetržité zlepšování:** Ke zjištění přírůstkových vylepšení, která se dají řešit při další fázi navrhování, automatizace a škálování systému, se dají použít různé nástroje pro monitorování.

### <a name="improve-system-design"></a>Vylepšení návrhu systému

Zlepšení návrhu systému představuje nejúčinnější přístup ke zlepšení provozu jakékoli běžné platformy. Díky vylepšením návrhu systému se může zvýšit stabilita a může se snížit i jeho přerušení. Návrh jednotlivých systémů je mimo rozsah pro zobrazení prostředí, které se provádí v rámci architektury cloudového přijetí. Jako doplněk k tomuto rozhraní nabízí architektura architektury Azure osvědčené postupy pro zlepšení odolnosti a návrhu konkrétního systému. Tato vylepšení návrhu lze použít pro navrhování systémů platformy nebo konkrétního zatížení.

Architektura architektury Azure se zaměřuje na zlepšení napříč pěti pilíři návrhu systému:

- **Škálovatelnost:** Škálování běžných prostředků platformy pro zpracování zvýšené zátěže.
- **Dostupnost:** Snížení doby provozu tím, že zlepšíte potenciál v době provozu.
- **Odolnost:** Vylepšete dobu obnovení, aby se snížila doba přerušení.
- **Zabezpečení:** Chraňte aplikace a data před externími hrozbami.
- **Správa:** Provozní procesy specifické pro tyto běžné prostředky platforem.

Většina obchodních přerušení je rovna určité formě technického dluhu nebo nedostatku architektury. U stávajících nasazení se vylepšení návrhu systémů dají zobrazit jako platby na stávající Technický dluh. U nových nasazení si můžete zobrazit vylepšení návrhu systémů, protože se vyhnete technickým dluhům. Další karta, "Automatizovaná náprava", vyhledává způsoby, jak řešit Technický dluh, který nelze nebo by neměl být řešen.

Další informace o [architektuře architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) pro zlepšení návrhu systému. Jak se zlepšuje návrh systému, vraťte se do tohoto článku, abyste našli nové příležitosti pro vylepšení a škálování těchto vylepšení napříč vaším prostředím.

### <a name="automated-remediation"></a>Automatizovaná náprava

Technický dluh nelze (nebo neměli) řešit. Řešení může být příliš nákladné, aby bylo možné ho opravit. Řešení může být plánováno, ale má dlouhou dobu trvání projektu. Může to být tím, že vaše provozní přerušení nemá významný dopad na firmu nebo že obchodní Priorita se rychle obnovuje místo investic do odolnosti.

Pokud rozlišení technického dluhu není požadovanou cestou, automatizovaná náprava je často požadovaným dalším krokem. Použití Azure Automation a Azure Monitor k detekci trendů a zajištění automatizované nápravy je nejběžnějším přístupem k automatizované nápravě.

Pokyny k automatizované nápravě najdete v tomto článku o [Azure Automation a výstrahách](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Škálování řešení pomocí katalogu služeb

Základem specializace platformy a operací platforem je dobře spravovaný katalog služeb. To je způsob, jakým jsou vylepšení pro navrhování a nápravu systémů škálovaná v rámci prostředí. Tým cloudové platformy a tým Cloud Automation si můžete na nejběžnější platformy v jakémkoli prostředí vytvořit opakovaně použitelná řešení. Pokud se ale tato řešení ještě nepoužívají, cloudová správa může poskytovat jenom něco větší než nabídka standardních hodnot.

Aby bylo možné maximalizovat přijímání a minimalizaci režie údržby jakékoli optimalizované platformy, měla by být platforma přidána do katalogu služeb. Každá aplikace v katalogu se dá nasadit pro interní spotřebu prostřednictvím katalogu služeb nebo jako nabídka Marketplace pro externí zákazníky.

Pokyny k publikování do katalogu služeb najdete v článku série [publikování do katalogu služeb](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Nepřetržité zlepšování

Specializace platformy a operace platforem jsou závislé na silných smyčkách zpětné vazby mezi týmy pro přijetí, platformu, automatizaci a správu. Na základě těchto smyček zpětné vazby v datech je každému týmu možné provádět rozhodnutí. Aby operace platforem dosáhly dlouhodobých obchodních závazků, je důležité využít přehledy, které jsou specifické pro centralizovanou platformu. Vzhledem k tomu, že kontejnery a SQL Server jsou dvě nejběžnější centrálně spravované platformy, najdete v následujících článcích několik článků, které vám pomůžou začít s shromažďováním dat průběžného zlepšování.

[Výkon kontejneru](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) 
 výkon[databáze PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql) 
 výkonu[databáze IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
