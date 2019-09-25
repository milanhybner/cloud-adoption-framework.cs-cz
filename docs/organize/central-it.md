---
title: Centrální možnosti IT
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si o tvorbě centrálních funkcí IT.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 54e08a42a64d06005620b450b1458288316df74e
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224014"
---
# <a name="central-it-capabilities"></a>Centrální možnosti IT

Vzhledem k škálováním při přijetí do cloudu nemusí být možnost zásad správného řízení cloudu dostatečná, aby bylo možné řídit úsilí při přijímání. Když je přijetí postupný, týmy mají za následek ekologicky vyvíjet dovednosti a procesy potřebné k tomu, aby byly v průběhu času připravené pro Cloud.

Pokud však tým pro přijetí v rámci jednoho cloudu využívá Cloud k dosažení vysokého obchodního výsledku, postupné přijetí je v některých případech jen zřídka. Úspěch následuje po úspěšném provedení. To platí také pro přijetí v cloudu, ale k tomu dochází v cloudovém měřítku. Když se přijetí do cloudu v poměrně krátké době rozšíří z jednoho týmu na několik týmů, je potřeba další podpora od stávajících zaměstnanců IT. Nicméně zaměstnanci nemusí mít školení a zkušenosti potřebné k podpoře cloudu s využitím nativních nástrojů IT pro Cloud. Tím se často řídí vytváření centrálního IT týmu, který řídí Cloud.

> [!CAUTION]
> I když se jedná o běžný krok v rámci splatnosti, může představovat vysoké riziko pro přijetí a potenciálně blokovat inovace a úsilí při migraci, pokud není spravováno efektivně. V části rizika níže najdete informace o tom, jak zmírnit riziko centralizovaného řešení v rámci kulturního antipatternu.

## <a name="possible-sources-for-central-it-expertise"></a>Možné zdroje pro střední odbornost IT

Dovednosti potřebné k poskytování centralizovaných funkcí IT můžou poskytnout:

- Stávající centrální tým IT
- Podnikové architekty
- IT operace
- Zásady správného řízení IT
- IT infrastruktura
- Sítě
- Identita
- Virtualizace
- Provozní kontinuita a zotavení po havárii
- Vlastníci aplikace v rámci IT

> [!WARNING]
> Centrální IT oddělení by mělo být použito v cloudu, pokud je stávající místní doručování založené na modelu centrálního IT. Pokud je aktuální místní model založený na delegovaném řízení, zvažte přístup k cloudovým centrům (CCoE), abyste mohli lépe kompatibilní alternativy.

## <a name="key-responsibilities"></a>Klíčové zodpovědnosti

Přizpůsobte stávající IT postupy, aby bylo zajištěno, že úsilí o přijetí bude mít za následek dobře řízená a dobře spravovaná prostředí v cloudu.

Následující úkoly jsou obvykle spouštěny pravidelně:

### <a name="strategic-tasks"></a>Strategické úkoly

- Zrevidujte
  - [obchodní výsledky](../strategy/business-outcomes/index.md)
  - [finanční modely](../strategy/financial-models.md)
  - [motivace pro přijetí do cloudu](../strategy/motivations.md)
  - [obchodní rizika](../govern/policy-compliance/risk-tolerance.md)
  - [racionalizace digitální nemovitosti](../digital-estate/index.md)
- Umožňuje monitorovat plány a průběh přijetí v rámci nevyřízených [položek migrace](../migrate/migration-considerations/assess/release-iteration-backlog.md)s určenou prioritou.
- Identifikujte a určete prioritu změn platformy, které jsou potřeba pro podporu nevyřízených položek migrace.
- Působit jako zprostředkující nebo převodní vrstva mezi potřebou pro přijetí do cloudu a stávajícími týmy IT.
- Využijte stávající IT týmy, abyste urychlili možnosti platformy a umožnili jejich přijetí.

### <a name="technical-tasks"></a>Technické úkoly

- Sestavujte a udržujte cloudovou platformu pro podporu řešení.
- Definujte a implementujte architekturu platformy.
- Provoz a správa cloudové platformy
- Trvale Vylepšete platformu.
- Udržujte si nové inovace na cloudové platformě.
- Doručovat nové cloudové možnosti pro podporu vytváření obchodních hodnot.
- Navrhněte řešení samoobslužných služeb.
- Zajistěte, aby řešení splňovala stávající požadavky zásad správného řízení a dodržování předpisů.
- Vytvořte a ověřte nasazení architektury platformy.
- Přečtěte si plány vydání pro zdroje nových požadavků na platformu.

## <a name="meeting-cadence"></a>Tempo schůzky

Centrální IT oddělení obvykle pochází z pracovního týmu. Očekává, že účastníci potvrdili spoustu každodenních plánů, aby bylo možné přidružení úsilí. Příspěvky nejsou omezeny na schůzky a cykly zpětné vazby.

## <a name="central-it-risks"></a>Střední rizika IT

Každá z možností cloudu a fází organizace splatnosti má předponu slova "Cloud". Jedinou výjimkou je střední. Ústřední IT oddělení se přestalo, když se všechny prostředky IT můžou nacházet v několika lokalitách, které spravuje malý počet týmů, a řídí se jednou platformou pro správu provozu. Globální obchodní postupy a digitální hospodářství mají značně omezené instance těchto centrálně spravovaných prostředí.

V moderních zobrazeních jsou prostředky globálně distribuované. Odpovědnosti jsou delegovány. Služba Operations Management je poskytována kombinací interních zaměstnanců, poskytovatelů spravovaných služeb a poskytovatelů cloudu. V digitální ekonomice se postupy správy IT převádějí do modelu samoobslužné služby a delegovaného řízení s jasným guardrails pro vymáhání zásad správného řízení. Centrální IT oddělení IT může být hodnotným přispěvatelem při přijímání do cloudu, protože se stane zprostředkovatelem cloudu a partnerem pro inovace a flexibilitu firmy.

Centrální IT oddělení IT jako funkce je dobře na úrovni, aby bylo možné brát v úvahu cennou znalost a postupy ze stávajících místních modelů a uplatňovat postupy na doručování do cloudu. Tento proces však bude vyžadovat změnu. Nové procesy, nové dovednosti a nové nástroje se vyžadují pro podporu přijímání do cloudu ve velkém měřítku. Když se centrální IT přizpůsobí, stane se důležitým partnerem při přijímání v cloudu. Pokud se ale hlavní IT aplikace nepřizpůsobí cloudu nebo se pokusí použít Cloud jako katalyzátor pro důkladné kontroly, centrální IT služby se rychle přestanou blokovat na přijetí, inovace a migraci.

Míry tohoto rizika představují rychlost a flexibilitu. Cloud zjednodušuje rychlé přijímání nových technologií. Když se nové možnosti cloudu dají nasadit během několika minut, ale centrální recenze IT do procesu nasazení přidají týdny nebo měsíce, pak se tyto centralizované procesy stanou významnou překážkou pro úspěch firmy. Po zjištění tohoto indikátoru zvažte alternativní strategie pro doručení IT.

### <a name="exceptions"></a>Výjimky

Řada oborů vyžaduje pevné dodržování předpisů třetí strany. Některé požadavky na dodržování předpisů stále vyžadují centralizovaný ovládací prvek IT. Doručení těchto měr dodržování předpisů může přidat čas do procesů nasazení, zejména pro nové technologie, které se v podstatě nepoužívaly. V těchto scénářích očekáváte zpoždění při nasazení v počátečních fázích přijetí. Podobné situace existují pro společnosti, které se týkají citlivých zákaznických dat, ale nemusí se řídit požadavkem na dodržování předpisů třetí strany.

### <a name="operating-within-the-exceptions"></a>Fungování v rámci výjimek

Když se vyžadují centralizované procesy IT a tyto procesy vytvoří vhodné kontrolní body při přijímání nových technologií, můžou se tyto kontrolní body pro inovace pořád řešit rychle. Požadavky zásad správného řízení a dodržování předpisů jsou navržené tak, aby chránily citlivé věci a nechránily všechno. Cloud poskytuje jednoduché mechanismy pro získání a nasazení izolovaných prostředků a současně zachovává správné guardrails.

Vyspělý centrální tým IT udržuje nezbytná ochrana, ale vyjednává postupy, které stále umožňují inovaci. Demonstrace této úrovně splatnosti závisí na správné klasifikaci a izolaci prostředků.

### <a name="example-narrative-of-operating-within-exceptions-to-empower-adoption"></a>Příklad mluveného komentáře v rámci výjimek pro zajištění přijetí

Tento příklad ilustruje postup, který vychází z vyspělého centrálního IT týmu k tomu, aby bylo možné ho přijmout.

Contoso, LLC přijalo centrální IT model pro podporu cloudových prostředků firmy. Pro dodávání tohoto modelu implementovaly těsné ovládací prvky pro různé sdílené služby, například připojení k síti příchozího přenosu dat. Tím se snižuje riziko úniku jejich cloudového prostředí a poskytlo se jediné zařízení se systémem "break-sklo", které zablokuje veškerý provoz v případě porušení. Zásady standardních hodnot zabezpečení mají stav, že všechny příchozí přenosy musí pocházet ze sdíleného zařízení spravovaného centrálním IT týmem.

Jeden z svých týmů pro přijetí v cloudu teď ale vyžaduje prostředí s vyhrazeným a speciálně nakonfigurovaným připojením k síti příchozího přenosu dat, které využívá konkrétní cloudovou technologii. Nezralý centrální IT tým by jednoduše odmítl žádost a určila prioritu svých stávajících procesů během potřeb pro přijetí. Centrální tým IT společnosti Contoso je jiný. V tomto dilematem rychle identifikovali jednoduché řešení se čtyřmi částmi: Klasifikace, vyjednávání, izolace a automatizace.

**Mazal** Vzhledem k tomu, že tým pro přijetí cloudu byl v počátečních fázích vytváření nového řešení a neobsahuje žádná citlivá data ani důležité požadavky na technickou podporu, prostředky v prostředí byly klasifikovány jako nízké riziko a nekritické. Efektivní klasifikace je znaménkem zralosti v centrálním IT oddělení. Klasifikace všech prostředků a prostředí umožňuje vymazat zásady.

**Jedna** Samotná klasifikace není dostatečná. Sdílené služby byly implementovány tak, aby konzistentně fungovaly citlivé a klíčové prostředky. Změna pravidel by způsobila ohrožení zásad správného řízení a dodržování předpisů, které jsou navržené pro prostředky, které vyžadují vyšší ochranu. K přijetí nemůže dojít na náklady na stabilitu, zabezpečení nebo řízení. To vedlo k vyjednávání s týmem přijetí k zodpovězení konkrétních otázek. Mohl DevOps tým pro toto prostředí poskytnout správu operací? Bude toto řešení vyžadovat přímý přístup k jiným interním prostředkům? Pokud tým pro přijetí v cloudu vyhovuje těmto kompromisům, může být přenos příchozích dat možný.

**Oddělení** Vzhledem k tomu, že podnik může poskytovat svou vlastní správu probíhajících operací a vzhledem k tomu, že řešení nespoléhá na přímý provoz do jiných interních prostředků, může být uzavřené v novém předplatném. Toto předplatné je také přidáno do samostatného uzlu nové hierarchie skupiny pro správu.

**Automatizace:** Dalším znaménkem splatnosti v tomto týmu jsou zásady automatizace. Tým používá Azure Policy pro automatizaci vynucování zásad. Používají také plány Azure k automatizaci nasazení běžných komponent platforem a vynutily dodržování definovaných standardních hodnot identity. U tohoto předplatného a dalších uživatelů v nové skupině pro správu se zásady a šablony mírně liší. Zásady blokující šířku pásma příchozího přenosu dat byly zrušeny. Nahradily se požadavky na směrování provozu prostřednictvím předplatného sdílených služeb, jako je jakýkoli příchozí přenos dat, pro zajištění izolace provozu. Vzhledem k tomu, že nástroje pro správu místních operací nemůžou získat přístup k tomuto předplatnému, už agenti pro tento nástroj nemusejí být. Všechny ostatní zásady správného řízení guardrails vyžadované jinými předplatnými v hierarchii skupin pro správu se pořád vynutily, což zajišťuje dostatečné guardrails.

Vyspělý tvůrčí přístup týmu centrálního IT společnosti Contoso nabízí řešení, které neohrožuje zásady správného řízení nebo dodržování předpisů, ale přesto bylo podporováno jejich přijetí. Tento přístup ke službě Broker spíše než vlastnící cloudový nativní přístup k centralizovanému je prvním krokem k vytvoření skutečné cloudové centra excelence (CCoE). Přijetí tohoto přístupu k rychlému vytváření stávajících zásad umožní centralizovanou kontrolu v případě potřeby a guardrails zásad správného řízení, pokud je přijatelná větší flexibilita. Vyrovnávání těchto dvou hledisek snižuje rizika spojená s centrálním IT v cloudu.

## <a name="next-steps"></a>Další kroky

V rámci centrálního IT v cloudu je v dalším kroku k diskrokování obvykle volného spojení [cloudových operací](./cloud-operations.md). Dostupnost nástrojů pro správu operací v cloudu a nižší provozní náklady na PaaS řešení často vede k obchodním týmům (nebo speciálně DevOps týmům v rámci podniku) za předpokladu, že se jedná o zodpovědnost za cloudové operace.

> [!div class="nextstepaction"]
> [Schopnost cloudových operací](./cloud-operations.md)
