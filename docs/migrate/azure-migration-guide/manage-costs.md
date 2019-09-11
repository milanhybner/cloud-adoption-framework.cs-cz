---
title: Mechanismy kontroly nákladů se zaměřením na migraci
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zjistěte, jak nastavit rozpočty a platby a jak porozumět informacím na fakturách za prostředky Azure.
author: bandersmsft
ms.author: banders
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 294a426aef047bb7acd418c19574a4fd7e0b2320
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905637"
---
# <a name="migration-focused-cost-control-mechanisms"></a>Mechanismy kontroly nákladů se zaměřením na migraci

Cloud přináší několik posunů ve způsobu, jakým pracujeme, bez ohledu na naši roli v rámci technologického týmu. Skvělým příkladem tohoto posunu jsou náklady. V minulosti se náklady na prostředky IT (infrastrukturu, aplikace a data) zabývalo jenom finanční oddělení a vedení IT. Cloud umožňuje každému členovi IT dělat kroky a přijímat rozhodnutí v zájmu lepší podpory koncového uživatele. S těmito možnostmi ale přichází také zodpovědnost brát do úvahy náklady.

V tomto článku se seznámíte s nástroji, které můžou před migrací do Azure, během ní i po ní pomáhat s rozhodováním o rozumných nákladech.

Mezi nástroje probírané v tomto článku patří:

> - Azure Migrate
> - Cenová kalkulačka Azure
> - Kalkulačka celkových nákladů na vlastnictví Azure
> - Azure Cost Management
> - Azure Advisor

Procesy popsané v tomto článku můžou vyžadovat spolupráci s manažery IT, finančním oddělením nebo vlastníky obchodních aplikací. Pokyny ke spolupráci s těmito rolemi najdete v článku o tom, jak v organizaci brát ohledy na náklady (který v rámci série o přechodu na cloud vyjde ve 3. čtvrtletí 2019).

<!-- markdownlint-disable MD024 MD025 -->

# <a name="estimate-vm-costs-prior-to-migrationtabestimatevmcosts"></a>[Odhad nákladů na virtuální počítače před migrací](#tab/EstimateVMCosts)

Před migrací jakéhokoliv prostředku (infrastruktury, aplikace nebo dat) je k dispozici možnost odhadnout náklady a upřesnit potřebnou velikost na základě pozorovaných kritérií výkonu pro dané prostředky. Odhad nákladů slouží ke dvěma účelům: umožňuje řízení nákladů a poskytuje kontrolní bod pro zajištění, že jsou aktuální rozpočty dostatečné pro nezbytné požadavky na výkon.

## <a name="cost-calculators"></a>Kalkulačky nákladů

Pro ruční výpočty nákladů jsou k dispozici dvě praktické kalkulačky, které umožňují rychle odhadnout náklady na základě architektury sady funkcí, která se má migrovat.

- [Cenová kalkulačka](https://azure.microsoft.com/pricing/calculator) Azure poskytuje odhad nákladů na základě ručně zadaných produktů Azure.
- Někdy je při rozhodování potřeba porovnat budoucí náklady na cloud a aktuální náklady na místní prostředí. Toto porovnání může poskytnout [kalkulačka celkových nákladů na vlastnictví](https://azure.microsoft.com/pricing/tco/calculator).

Tyto manuální kalkulačky nákladů je možné využít samostatně pro předpověď potenciálních výdajů a úspor. Dají se také použít společně s nástroji pro prognózování nákladů služby Azure Migrate, abyste mohli upravit očekávané náklady s ohledem na alternativní architektury nebo omezení výkonu.

## <a name="azure-migrate-calculations"></a>Výpočty v službě Azure Migrate

**Požadavky:** Zbývající část této karty předpokládá, že už jste v službě Azure Migrate zadali kolekci prostředků (infrastruktura, aplikace a data), které chcete migrovat. Pokyny k shromažďování počátečních dat poskytuje předchozí článek o posouzení. Jakmile jsou data k dispozici, můžete na jejich základě podle následujících kroků odhadovat měsíční náklady.

Azure Migrate vypočítá **odhady měsíčních nákladů** na základě dat zachycených kolektorem a mapou služeb. Odhadované náklady je možné načíst takto:

1. Na portálu přejděte do okna posouzení Azure Migrate.
1. Na stránce **Přehled** projektu vyberte **+Vytvořit posouzení**.
1. Kliknutím na **Zobrazit vše** zobrazíte vlastnosti posouzení.
1. Vytvořte skupinu a pojmenujte ji.
1. Vyberte virtuální počítače, které do ní chcete přidat.
1. Kliknutím na tlačítko **Vytvořit posouzení** vytvoříte skupinu a posouzení.
1. Po vytvoření můžete posouzení zobrazit v části Přehled > Řídicí panel.
1. V části Podrobnosti o posouzení v okně navigace vyberte **Podrobnosti nákladů**.

Výsledný odhad, jehož příklad je uvedený níže, identifikuje měsíční náklady na výpočty a úložiště, které často představují největší část nákladů na cloud.

![compute-storage-monthly-cost-estimate.png](./media/manage-costs/compute-storage-monthly-cost-estimate.png)
*Obrázek 1: Obrázek zobrazení Podrobnosti nákladů v posouzení Azure Migrate*

## <a name="additional-resources"></a>Další zdroje

- [Nastavení a kontrola posouzení pomocí Azure Migrate](/azure/migrate/tutorial-assess-vmware#set-up-an-assessment)
- Pokud potřebujete komplexnější plán správy nákladů pro větší počet prostředků (infrastruktury, aplikací a dat), podívejte se na [model zásad správného řízení architektury přechodu na cloud](../../governance/journeys/index.md). Důležité jsou zejména pokyny týkající se [disciplíny služby Cost Management](../../governance/cost-management/index.md) a [vylepšování služby Cost Management ve velkém podniku](../../governance/journeys/complex-enterprise/cost-management-evolution.md).

# <a name="estimate-and-optimize-vm-costs-during-and-after-migrationtabestimateoptimize"></a>[Odhad a optimalizace nákladů na virtuální počítače během migrace a po ní](#tab/EstimateOptimize)

Odhad nákladů před migrací poskytuje solidní cíl pro očekávání ohledně nákladů. Poskytuje také příležitosti ke zvážení, jaké jsou požadavky na výkon a náklady na jednotlivé prostředky (infrastruktura, aplikace a data), které se budou migrovat. Je to ale stále jenom odhad. Po migraci prostředku a jeho uvedení do provozu je možné provádět přesnější výpočty nákladů na základě skutečné nebo syntetizované zátěže.

## <a name="azure-advisor-cost-recommendations"></a>Doporučení k nákladům od služby Azure Advisor

Během 24 hodin od migrace prostředků (infrastruktury, aplikací a dat) do Azure začne služba Azure Advisor monitorovat výkon jednotlivých prostředků a poskytovat vám k nim zpětnou vazbu. Jedna z položek shromážděné zpětné vazby se týká rovnováhy mezi náklady a využitím.

Doporučení k nákladům pro prostředky (infrastrukturu, aplikace a data) v rámci svého aktuálního předplatného získáte takto:

1. Na portálu přejděte do okna **Azure Advisor**. Můžete to udělat tak, že v levém navigačním podokně webu Azure Portal kliknete na **Poradce**. Pokud položku Poradce v levém podokně nevidíte, vyberte **Všechny služby**. V podokně s nabídkou služeb vyberte v části **Monitorování a správa** položku **Poradce**.
1. Na řídicím panelu služby Advisor se zobrazí souhrn doporučení pro všechna vybraná předplatná. Předplatná, pro která chcete zobrazit doporučení, můžete zvolit pomocí rozevíracího seznamu filtru předplatných.
1. Pokud chcete zobrazit doporučení k nákladům, vyberte kartu Náklady.

## <a name="azure-cost-management"></a>Azure Cost Management

Služba Azure Cost Management dokáže poskytnout komplexnější pohled na vzory nákladů, včetně podrobného zobrazení nákladů a jejich trendů v průběhu času. V případě rozsáhlých nebo složitých migrací může toto zobrazení poskytnout přehledné informace potřebné k rozhodování o správě a snižování nákladů v širším měřítku.

Požadavky: Zbývající část této karty předpokládá, že jste během dokončování průvodce připraveností pro Azure dokončili nastavení služby Azure Cost Management. Další podrobnosti o konfiguraci služby Azure Cost Management najdete v tomto [článku v průvodci připraveností pro Azure](/azure/architecture/cloud-adoption/ready/azure-readiness-guide/manage-costs). Jakmile jsou data k dispozici, můžete na jejich základě podle následujících kroků odhadovat měsíční náklady.

Data analýzy nákladů služby Azure Cost Management můžete pro svá předplatná načíst takto:

1. Na portálu přejděte do okna **Správa nákladů a fakturace**. Pokud položku Správa nákladů a fakturace nevidíte v levém podokně, klikněte na **Všechny služby**. V podokně s nabídkou služeb vyberte v části **Monitorování a správa** položku **Správa nákladů a fakturace**.
1. V okně Správa nákladů a fakturace vyberte v levé navigaci možnost **Správa nákladů**. Tím můžete v otevřeném okně začít analyzovat a optimalizovat náklady na cloud.
1. V okně Správa nákladů vyberte **Analýza nákladů**.
    1. Pomocí možnosti **Obor** můžete v analýze nákladů přepnout na jiný obor.

Tato analýza vám umožní zkontrolovat celkové náklady, rozpočet (pokud je k dispozici) a kumulované náklady. Každý výpočet je možné zobrazit podle služby, podle prostředku a v průběhu času. Nejdůležitější je, že náklady je možné analyzovat pomocí značek. Správné pojmenování a označení prostředků (infrastruktury, aplikací a dat) je základním výchozím bodem všech procesů správného řízení a správy nákladů. Správné značky umožňují lepší správu nákladů a vedou k lepším výsledkům při optimalizaci výkonu a nákladů.

## <a name="additional-resources"></a>Další zdroje

- Pokud potřebujete komplexnější plán správy nákladů pro větší počet prostředků (infrastruktury, aplikací a dat), podívejte se na [model zásad správného řízení architektury přechodu na cloud](../../governance/journeys/index.md). Důležité jsou zejména pokyny týkající se [disciplíny služby Cost Management](../../governance/cost-management/index.md) a [postupného vylepšování služby Cost Management ve velkém podniku](../../governance/journeys/complex-enterprise/cost-management-evolution.md).
- Další informace o službě Azure Advisor najdete v článku o [snížení nákladů na služby pomocí Azure Advisoru](/azure/advisor/advisor-cost-recommendations).
- Další informace o službě Azure Cost Management najdete v článcích o [principech oborů a práci s nimi](/azure/cost-management/understand-work-scopes) a o [prozkoumání a analýze nákladů pomocí analýzy nákladů](/azure/cost-management/quick-acm-cost-analysis).

# <a name="tips-and-tricks-to-optimize-coststabtipstricks"></a>[Tipy a triky pro optimalizaci nákladů](#tab/TipsTricks)

Kromě nástrojů uvedených v tomto článku jsou k dispozici některé tipy a triky, které vám můžou pomoct s rychlým snížením celkových nákladů na cloud. Tady je několik obecných tipů, o kterých je dobré vědět:

## <a name="avoid-unnecessary-spending"></a>Vyhněte se zbytečnému utrácení

Do cloudu by se teoreticky mohla migrovat většina prostředků (infrastruktury, aplikací a dat) v existujícím datacentru. To ale neznamená, že to musíte udělat. Během posuzování jednotlivých sad funkcí ověřte, jestli je třeba sadu funkcí migrovat. S určením prostředků, které by se měly migrovat, může pomoct článek o [postupné (přírůstkové) racionalizaci](../../digital-estate/rationalize.md) v rámci série o přechodu na cloud.

## <a name="reduce-waste"></a>Omezte odpad

Po nasazení infrastruktury do Azure je důležité se ujistit, jestli se používá. Nejjednodušší způsob, jak okamžitě začít šetřit, je zkontrolovat vaše prostředky a odebrat ty, které se nepoužívají.

## <a name="reduce-overprovisioning"></a>Omezte nadměrné zřizování

I při nejlepším přístupu k odhadování se pravděpodobně vyskytnou nadměrně zřízené a nedostatečně využité prostředky (infrastruktura, aplikace a data). Kontrola těchto prostředků pomocí nástrojů uvedených na předchozích dvou kartách vám pomůže identifikovat potenciální možnosti pro snížení velikosti prostředků, aby lépe odpovídaly požadavkům na výkon a aby se snížily náklady.

## <a name="take-advantage-of-available-discounts"></a>Využijte dostupné slevy

Promluvte si se svým zástupcem v Microsoftu a zjistěte, jak můžete využít výhod aktuálních možností slev. Následuje několik příkladů slev, které se běžně používají ke snížení nákladů.

## <a name="azure-reservations"></a>Rezervace Azure

[Rezervace Azure](/azure/billing/billing-save-compute-costs-reservations) umožňují předplatit si jednoletou nebo tříletou výpočetní kapacitu virtuálního počítače nebo databáze SQL. Díky předplacení můžete získat slevu na využívané prostředky. Rezervace Azure můžou při jednoletém nebo tříletém závazku s platbou předem významně snížit náklady na výpočetní výkon virtuálního počítače nebo databáze SQL, a to až o 72 procent oproti průběžným platbám. Rezervace poskytují slevu z faktury a neovlivňují běhový stav virtuálních počítačů nebo databází SQL.

## <a name="use-azure-hybrid-benefit"></a>Zvýhodněné hybridní využití Azure

Pokud už máte licence na Windows Server nebo SQL Server ve svých místních nasazeních, můžete díky programu [Zvýhodněné hybridní využití Azure](https://azure.microsoft.com/pricing/hybrid-benefit) ušetřit v Azure. V případě systému Windows Server každá licence pokrývá náklady na operační systém (až na dvou virtuálních počítačích) a platíte jenom základní výpočetní náklady. Stávající licence na SQL Server můžete využít k ušetření až 55 procent nákladů u databází SQL založených na virtuálních jádrech. Mezi možnosti patří SQL Server v Azure Virtual Machines a služba SSIS (SQL Server Integration Services).

## <a name="low-priority-vms-with-batch"></a>Virtuální počítače s nízkou prioritou ve službě Batch

Pro procesy běžící na pozadí s nižší prioritou nabízí služba Batch možnost správy virtuálních počítačů pro služby na pozadí a snížení nákladů. Než ale zvolíte tuto levnější možnost, je důležité porozumět tomu, že použití [virtuálních počítačů s nízkou prioritou ve službě Batch](/azure/batch/batch-low-pri-vms) má dopad na výkon.

## <a name="additional-resources"></a>Další zdroje

Pokud potřebujete komplexnější plán správy nákladů pro větší počet prostředků (infrastruktury, aplikací a dat), podívejte se na [model zásad správného řízení architektury přechodu na cloud](../../governance/journeys/index.md). Důležité jsou zejména pokyny týkající se [disciplíny služby Cost Management](../../governance/cost-management/index.md) a [zásad správného řízení při postupném vylepšování služby Cost Management ve velkém podniku](../../governance/journeys/complex-enterprise/cost-management-evolution.md).
