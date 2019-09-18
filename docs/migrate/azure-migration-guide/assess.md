---
title: Vyhodnocení digitálních aktiv
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vyhodnocení digitálních aktiv
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 19c3d6861ddb4ad87255233fae1a7f535538324b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022838"
---
# <a name="assess-the-digital-estate"></a>Vyhodnocení digitálních aktiv

Při ideální migraci by každý prostředek (infrastruktura, aplikace nebo data) byl kompatibilní s cloudovou platformou a byl by připraven k migraci. Ve skutečnosti se ale všechno do cloudu migrovat nedá. Navíc ne každý prostředek je kompatibilní s cloudovými platformami. Proto než budete úlohu migrovat do cloudu, je důležité vyhodnotit nejen ji, ale také každý související prostředek (infrastrukturu, aplikace a data).

Zdroje informací v této části vám pomůžou posoudit vaše prostředí, abyste dokázali určit, jestli je pro migraci vhodné a jaké metody připadají v úvahu.

# <a name="toolstabtools"></a>[Nástroje](#tab/Tools)

K vyhodnocení prostředí můžete použít následující nástroje, abyste zjistili, jestli je migrace vhodná a jaký přístup je nejlepší. Užitečné informace o volbě správných nástrojů, které podporují migraci, najdete v [průvodci rozhodováním o migračních nástrojích pro architekturu přechodu na cloud](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Služba Azure Migrate posuzuje vhodnost místní infrastruktury, aplikací a dat k migraci do Azure. Služba posoudí vhodnost místních prostředků k migraci, nastaví velikost na základě výkonu a nabízí odhad nákladů na provoz místních prostředků v Azure. Pokud uvažujete o migracích typu „lift and shift“ nebo jste v počáteční fázi vyhodnocování migrace, je tato služba určená právě vám. Po dokončení posouzení je možné pomocí služby Azure Migrate spustit migraci.

![Přehled služby Azure Migrate](./media/assess/azuremigrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Vytvoření nového projektu migrace serveru

Pokud chcete začít s posouzením vhodnosti serveru k migraci pomocí služby Azure Migrate, postupujte následovně:

1. Vyberte **Azure Migrate**.
1. V části **Přehled** klikněte na **Posoudit a migrovat servery**.
1. Vyberte **Přidat nástroje**.
1. V části **Zjistit, posoudit a migrovat servery** klikněte na **Přidat nástroje**.
1. V části **Projekt migrace** vyberte své předplatné Azure a vytvořte skupinu prostředků, pokud ji ještě nemáte.
1. V části **Podrobnosti o projektu** zadejte název projektu a zeměpisnou oblast, ve které chcete projekt vytvořit, a klikněte na **Další**.
1. V části **Vybrat nástroj pro posouzení** vyberte **V tuto chvíli přeskočit přidání nástroje pro posouzení > Další**.
1. V části **Vybrat nástroj pro migraci** vyberte **Azure Migrate: Migrace serveru > Další**.
1. V části **Zkontrolovat a přidat nástroje** zkontrolujte nastavení a klikněte na **Přidat nástroje**.
1. Po přidání se nástroj zobrazí v části **Projekt Azure Migrate > Servery > Nástroje pro migraci**.

::: zone target="chromeless"

::: form action="Blade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="read-more"></a>Další informace

- [Přehled služby Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrace fyzických nebo virtualizovaných serverů do Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Služba Azure Migrate na webu Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

## <a name="service-map"></a>Mapa služeb

Service Map automaticky rozpozná komponenty aplikace v systémech Windows a Linux a mapuje komunikaci mezi službami. Service Map zobrazuje vaše servery tak, jak o nich přemýšlíte, tzn. jako propojené systémy, které zajišťují důležité služby. Service Map zobrazuje propojení serverů, procesů, latenci příchozích a odchozích připojení a porty v libovolné architektuře propojené protokolem TCP. Kromě instalace agenta se nevyžaduje žádná konfigurace.

Služba Azure Migrate používá službu Service Map ke zlepšení možností vytváření sestav a závislostí v celém prostředí. Veškeré podrobnosti o této integraci jsou popsány v tématu o [vizualizaci závislostí](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization). Pokud používáte službu Azure Migration, nemusíte provádět žádné další kroky, abyste nakonfigurovali službu Service Map a získali výhody, které nabízí. Následující pokyny jsou pro vaši informaci, pokud budete chtít používat Service Map k jiným účelům nebo projektům.

### <a name="enable-dependency-visualization-using-service-map"></a>Povolení vizualizace závislostí ve službě Service Map

Pokud chcete používat vizualizaci závislostí, potřebujete si stáhnout a nainstalovat agenty na každý místní počítač, který chcete analyzovat.

- Na každém počítači musí být nainstalovaný [Microsoft Monitoring Agent (MMA)](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows).
- Na každý počítač je potřeba nainstalovat [agenta závislostí](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows).
- Pokud navíc máte počítače bez připojení k internetu, musíte na ně stáhnout a nainstalovat bránu Log Analytics.

<!-- markdownlint-disable MD024 -->

### <a name="read-more"></a>Další informace

- [Používání řešení Service Map v Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate a Service Map: Vizualizace závislostí](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)


# <a name="scenarios-and-stakeholderstabscenarios"></a>[Scénáře a účastníci](#tab/Scenarios)

## <a name="scenarios"></a>Scénáře

V tomto průvodci se zaměříme na následující scénáře:

- **Starší hardware:** Migrujete, protože už nechcete být závislí na starším hardwaru, kterému se blíží konec podpory nebo životnosti.
- **Růst kapacity:** Potřebujete zvýšit kapacitu prostředků (infrastruktury, aplikací a dat), kterou vám vaše aktuální infrastruktura nemůže poskytnout.
- **Modernizace datového centra:** Potřebujete rozšířit nebo modernizovat datové centrum o cloudové technologie, aby vaše firma byla stále aktuální a konkurenceschopná.
- **Modernizace aplikací nebo služeb:** Chcete aktualizovat aplikace, protože chcete získat výhody nativních cloudových funkcí. I kdyby vaším původním záměrem byla jenom strategie migrace spočívající ve změně hostitele, je možnost vytvoření plánů na kontrolu aplikací nebo služeb a jejich potenciální modernizace běžným procesem při každé migraci.

### <a name="organizational-alignment-and-stakeholders"></a>Organizace a účastníci

Úplný seznam účastníků se u jednotlivých projektů migrace liší. Nejlépe uděláte, když budete vycházet z předpokladu, že na začátku plánování migrace neznáte všechny zúčastněné strany, protože účastníci se často objeví až v určitých fázích projektu. Před zahájením projektu migrace ale můžete určit klíčové vedoucí pracovníky z finančního oddělení, z oddělení infrastruktury IT a ze skupin aplikací, které budou zainteresovány na migraci celé organizace do cloudu.

Když vytvoříte základní tým cloudové strategie, který sestavíte z těchto klíčových vedoucích účastníků, pomůže vám to připravit organizaci na osvojení cloudu, protože tento tým povede celý proces migrace do cloudu. Tento tým bude odpovědný za pochopení cloudových technologií a migračních procesů, zajistí obchodní odůvodnění migrací a určí nejlepší hlavní řešení používaná k migraci. Dále tým pomáhá identifikovat konkrétní aplikace a firemní účastníky a spolupracuje s nimi, aby zajistil jejich úspěšnou migraci.

Další informace o přípravě organizace na migraci do cloudu najdete v článku o architektuře přechodu na cloud v [úvodním zařazení organizace](../../ready/initial-org-alignment.md).

# <a name="timelinestabtimelines"></a>[Časové osy](#tab/Timelines)

Obecně platí, že zákazníci potřebují na scénář migrace popisovaný v tomto průvodci od jednoho do šesti měsíců.

Některé skutečnosti, které je potřeba vzít v úvahu při hodnocení časové osy migrace:

- **Migrované prostředky (infrastruktura, aplikace a data):** Počet prostředků a jejich různorodost.
- **Připravenost personálu:** Jsou vaši pracovníci připraveni na správu nového prostředí nebo potřebují školení?
- **Financování:** Máte na migraci schválené prostředky a rozpočet?
- **Správa změn:** Má firma zvláštní požadavky týkající se implementace a schvalování změn?
- **Oborové předpisy:** Jste povinni dodržovat předpisy daného oboru nebo odvětví?

# <a name="cost-managementtabmanagecost"></a>[Správa nákladů:](#tab/ManageCost)

Posouzení vašeho prostředí je dokonalou příležitostí k doplnění kroku spočívajícího v analýze nákladů. Když použijete data shromážděná při posuzovacích aktivitách, měli byste být schopni analyzovat náklady a předpovědět je. Předpověď nákladů musí kromě jednorázových nákladů (například na zvýšený příchozí přenos dat) zohledňovat i náklady na spotřebované služby.

Rozhodování a realizaci během migrace ovlivňují určité okolnosti:

- **Velikost digitálních aktiv:** Porozumění velikosti digitálních aktiv přímo ovlivňuje rozhodování a prostředky potřebné k provedení migrace.
- **Účetní modely:** Přechod od modelu strukturovaných kapitálových výdajů k modelu pohyblivých provozních nákladů.

::: zone target="docs"

Následující zdroje obsahují související informace:

- [Odhad cloudových nákladů](../migration-considerations/assess/estimate.md)

::: zone-end
