---
title: Vyhodnocení jednotlivých úloh a zpřesnění plánů
description: Tento oddíl průvodce migrací do Azure vám pomůže vyhodnotit vaše prostředí a určit, co by se mělo migrovat a které metody migrace je vhodné zvážit.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 40e62a05101e14fcd7507011d521521e58920ffc
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225553"
---
# <a name="assess-each-workload-and-refine-plans"></a>Vyhodnocení jednotlivých úloh a zpřesnění plánů

Zdroje informací v tomto průvodci vám pomohou vyhodnotit jednotlivé úlohy, kriticky zhodnotit předpokládanou vhodnost úloh pro migraci a dokončit architektonické rozhodování o možnostech migrace.

<!-- markdownlint-disable MD025 -->

# <a name="tools"></a>[Nástroje](#tab/Tools)

Pokud jste nevyužili pokyny u výše uvedených odkazů, budete k zajištění informovaných rozhodnutí ohledně migrace pravděpodobně potřebovat data a nástroj pro posouzení. Azure Migrate je nativní nástroj pro vyhodnocení **a** migrace do Azure. Pokud jste to ještě neudělali, pomocí těchto kroků vytvořte nový projekt migrace serveru a shromážděte potřebná data.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate posuzuje vhodnost místní infrastruktury, aplikací a dat k migraci do Azure. Tato služba:

- Vyhodnotí vhodnost migrace pro prostředky v místním prostředí.
- Určí velikost na základě výkonu.
- Poskytne odhad nákladů na provoz místních aktiv v Azure.

Pokud uvažujete o migracích typu „lift and shift“ nebo jste v počáteční fázi vyhodnocování migrace, je tato služba určená právě vám. Po dokončení posouzení můžete pomocí služby Azure Migrate spustit migraci.

![Přehled služby Azure Migrate](./media/assess/azure-migrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Vytvoření nového projektu migrace serveru

Začněte s posouzením vhodnosti serveru k migraci pomocí služby Azure Migrate a postupujte následovně:

1. Vyberte **Azure Migrate**.
1. V části **Přehled** vyberte **Posoudit a migrovat servery**.
1. Vyberte **Přidat nástroje**.
1. V části **Zjistit, posoudit a migrovat servery** vyberte **Přidat nástroje**.
1. V části **Projekt migrace** vyberte předplatné Azure a potom vytvořte skupinu prostředků, pokud ji ještě nemáte.
1. V části **Podrobnosti o projektu** zadejte název projektu a zeměpisnou oblast, ve které chcete projekt vytvořit, a potom vyberte **Další**.
1. V části **Vybrat nástroj pro posouzení** vyberte **V tuto chvíli přeskočit přidání nástroje pro posouzení > Další**.
1. V části **Vybrat nástroj pro migraci** vyberte **Azure Migrate: Migrace serveru > Další**.
1. V části **Kontrola a přidání nástrojů** zkontrolujte nastavení a potom vyberte **Přidat nástroje**.
1. Po přidání se nástroj zobrazí v části **Projekt Azure Migrate > Servery > Nástroje pro migraci**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Další informace

- [Přehled služby Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrace fyzických nebo virtualizovaných serverů do Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Služba Azure Migrate na webu Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

## <a name="service-map"></a>Mapa služeb

Service Map automaticky rozpozná komponenty aplikace v systémech Windows a Linux a mapuje komunikaci mezi službami. Service Map zobrazuje vaše servery tak, jak o nich přemýšlíte, tzn. jako propojené systémy, které zajišťují důležité služby. Service Map zobrazuje propojení serverů, procesů, latenci příchozích a odchozích připojení a porty v libovolné architektuře propojené protokolem TCP. Kromě instalace agenta se nevyžaduje žádná konfigurace.

Služba Azure Migrate používá službu Service Map ke zlepšení možností vytváření sestav a závislostí v celém prostředí. Veškeré podrobnosti o této integraci najdete v tématu o [vizualizaci závislostí](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization). Pokud používáte službu Azure Migration, nemusíte provádět žádné další kroky, abyste nakonfigurovali službu Service Map a získali výhody, které nabízí. Následující pokyny jsou pro vaši informaci, pokud byste chtěli Service Map používat k jiným účelům nebo projektům.

### <a name="enable-dependency-visualization-using-service-map"></a>Povolení vizualizace závislostí ve službě Service Map

Pokud chcete používat vizualizaci závislostí, stáhněte si agenty a nainstalujte je na každý místní počítač, který chcete analyzovat.

- Na každém počítači musí být nainstalovaný [Microsoft Monitoring Agent (MMA)](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows).
- Na každý počítač je potřeba nainstalovat [agenta závislostí Microsoftu](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows).
- Pokud navíc máte počítače bez připojení k internetu, musíte na ně stáhnout a nainstalovat bránu Log Analytics.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Další informace

- [Používání řešení Service Map v Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate a Service Map: Vizualizace závislostí](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

# <a name="challenge-assumptions"></a>[Kritické zhodnocení předpokladů](#tab/Challenge-Assumptions)

Při ideální migraci by každý prostředek (infrastruktura, aplikace nebo data) byl kompatibilní s cloudovou platformou a byl by připraven k migraci nebo modernizaci. Ve skutečnosti se ale všechno do cloudu migrovat nedá. Ne každý prostředek je kompatibilní s cloudovými platformami. Proto než budete úlohu migrovat do cloudu, je důležité vyhodnotit nejen ji, ale také všechny související prostředky (infrastrukturu, aplikace a data).

[Metodika plánu architektury přechodu na cloud](../../plan/index.md) radí čtenářům, aby k posouzení migrace a jejímu naplánování využili [postupnou (přírůstkovou) racionalizaci](../../digital-estate/rationalize.md#incremental-rationalization) a [strategii Power of 10](../../digital-estate/rationalize.md#release-planning). Tyto doprovodné materiály také obsahují podrobný popis osvědčeného postupu [použití služby Azure Migrate k vyhodnocení digitálních aktiv](../../plan/contoso-migration-assessment.md).

Výše uvedené odkazy naznačují, že vytváření předpokladů je přijatelné a často se při plánování migrace podporuje. Teď ale nastává čas přejít k akci. Před zahájením migrace do cloudu je třeba pro jednotlivé úlohy tyto předpoklady kriticky posoudit.

## <a name="two-steps-of-incremental-rationalization"></a>Dva kroky postupné racionalizace

K úspěšnému zajištění [postupné racionalizace](../../digital-estate/rationalize.md#incremental-rationalization) jsou potřeba dva stejně důležité kroky. Oba tyto kroky vyžadují data a přehled o prostředí. Každý z přístupů ale respektuje množství času a podrobnosti nutné k zajištění úspěšné migrace.

- **[Plánování vydávání verzí se strategií Power of 10](../../digital-estate/rationalize.md#release-planning):** Během počáteční racionalizace a plánování vydaných verzí se při posuzování použije jenom jedno z [5R racionalizace](../../digital-estate/5-rs-of-rationalization.md). K odhadování a plánování využijte tu možnost racionalizace, která nejlépe odpovídá celkové motivaci definované v [dokumentu Strategie přechodu na cloud](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

- **Podrobné posouzení jednotlivých úloh:** Předpoklady spojené s plánováním vydávání verzí se strategií Power of 10 jsou dostatečně přijatelné pro sestavení plánu. Tyto tytéž předpoklady ale mohou způsobovat významné problémy, pokud se před migrací nevyhodnotí.

## <a name="challenge-assumptions-and-update-the-plan"></a>Kritické zhodnocení předpokladů a aktualizace plánu

Podrobně zkontrolujte data posouzení ve službě Azure Migrate nebo zvoleném nástroji pro posouzení. Tato data vám poskytnou přehled o problémech s kompatibilitou, požadavcích na nápravu, návrzích velikosti a dalších aspektech.

Před zahájením migrace využijte tato data společně se zjišťovacími konverzacemi s vlastníkem produktu, vývojovými týmy, správci a dalšími osobami k vyhodnocení proveditelnosti migrace této konkrétní úlohy. Toto zjištění využijte ke kritickému zhodnocení základních předpokladů o této úloze. Pokud zjištěné výsledky mění plán migrace nebo přechodu, odpovídajícím způsobem ho aktualizujte.

Prvním krokem při kritickém posouzení těchto předpokladů je [kontrola všech 5 R](../../digital-estate/rationalize.md).

    - Funguje předpokládaný racionalizační přístup pro tuto úlohu? Je to ten nejlepší přístup?
    - Bude mít [fyzická stránka replikace](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) vliv na migraci této úlohy?
    - Vyžaduje tato úloha před zahájením migrace nějaké [opravné aktivity](../migration-considerations/assess/evaluate.md)?

Tyto typy otázek pomáhají kriticky vyhodnotit předpoklady a vedou k nejlepší cestě pro jednotlivé úlohy.

Rozšířený seznam otázek a definovaný proces pro ověřování předpokladů najdete v [přehledu vylepšení procesu vyhodnocení](../migration-considerations/assess/index.md).

# <a name="scenarios-and-stakeholders"></a>[Scénáře a účastníci](#tab/Scenarios)

## <a name="scenarios"></a>Scénáře

Tento průvodce se zaměřuje na následující scénáře:

- **Starší hardware:** Migrujete, protože už nechcete být závislí na starším hardwaru, kterému se blíží konec podpory nebo životnosti.
- **Růst kapacity:** Chcete zvýšit kapacitu prostředků (infrastruktury, aplikací a dat), kterou vám vaše aktuální infrastruktura nemůže poskytnout.
- **Modernizace datového centra:** Chcete rozšířit nebo modernizovat datové centrum o cloudové technologie, aby vaše firma byla stále aktuální a konkurenceschopná.
- **Modernizace aplikací nebo služeb:** Chcete aktualizovat aplikace, protože chcete získat výhody nativních cloudových funkcí. I kdyby vaším původním záměrem byla jenom strategie migrace spočívající ve změně hostitele, je možnost vytvoření plánů na kontrolu aplikací nebo služeb a jejich potenciální modernizace běžným procesem při každé migraci.

### <a name="organizational-alignment-and-stakeholders"></a>Organizace a účastníci

Úplný seznam účastníků se u jednotlivých projektů migrace liší. Nejlépe uděláte, když budete vycházet z předpokladu, že na začátku plánování migrace neznáte všechny zúčastněné strany, protože účastníci se často objeví až v určitých fázích projektu. Před zahájením projektu migrace ale určete klíčové vedoucí pracovníky z finančního oddělení, z oddělení infrastruktury IT a ze skupin aplikací, kteří jsou zainteresovaní na migraci celé organizace do cloudu.

Když vytvoříte základní tým cloudové strategie, který sestavíte z těchto klíčových vedoucích účastníků, pomůže vám to připravit organizaci na osvojení cloudu, protože tento tým povede celý proces migrace do cloudu. Tento tým bude odpovědný za pochopení cloudových technologií a migračních procesů, zajistí obchodní odůvodnění migrací a určí nejlepší hlavní řešení používaná k migraci. Dále tým pomáhá identifikovat konkrétní aplikace a firemní účastníky a spolupracuje s nimi, aby zajistil jejich úspěšnou migraci.

Další informace o přípravě organizace na migraci do cloudu najdete v pokynech architektury přechodu na cloud věnovaných [počátečnímu sladění organizace](../../plan/initial-org-alignment.md).

# <a name="timelines"></a>[Časové osy](#tab/Timelines)

Obecně platí, že zákazníci potřebují na scénář migrace popisovaný v tomto průvodci od jednoho do šesti měsíců.

Při hodnocení časové osy migrace je potřeba vzít v úvahu tyto skutečnosti:

- **Migrované prostředky (infrastruktura, aplikace a data):** Počet prostředků a jejich různorodost.
- **Připravenost personálu:** Jsou vaši pracovníci připraveni na správu nového prostředí nebo potřebují školení?
- **Financování:** Máte na migraci schválené prostředky a rozpočet?
- **Správa změn:** Má firma zvláštní požadavky týkající se implementace a schvalování změn?
- **Oborové předpisy:** Jste povinni dodržovat předpisy daného oboru nebo odvětví?

# <a name="cost-management"></a>[Správa nákladů](#tab/ManageCost)

Vyhodnocení vašeho prostředí přináší skvělou příležitost pro zahrnutí kroku analýzy nákladů. Když použijete data shromážděná při posuzovacích aktivitách, měli byste být schopni analyzovat náklady a předpovědět je. Předpověď nákladů musí kromě jednorázových nákladů (například na zvýšený příchozí přenos dat) zohledňovat i náklady na spotřebované služby.

Rozhodování a realizaci během migrace ovlivňují určité okolnosti:

- **Velikost digitálních aktiv:** Porozumění velikosti digitálních aktiv přímo ovlivňuje rozhodování a prostředky potřebné k provedení migrace.
- **Účetní modely:** Přechod od modelu strukturovaných kapitálových výdajů k modelu pohyblivých provozních nákladů.

::: zone target="docs"

Následující zdroje obsahují související informace:

- [Odhad cloudových nákladů](../migration-considerations/assess/estimate.md)

::: zone-end
