---
title: Zabezpečení, monitorování a správa prostředků
description: Nástroje pro monitorování a správu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5e0267c5b15e01b9f53e76ba2bc16f95381f81aa
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801269"
---
# <a name="secure-monitoring-and-management-tools"></a>Nástroje pro monitorování a správu

Po dokončení migrace by se migrované prostředky měly spravovat v rámci kontrolovaného provozu IT. Tento článek nepředstavuje odchylku od osvědčených provozních postupů. Následující text byste měli vnímat jako MVP (Minimum Viable Product) pro zabezpečení a správu migrovaných prostředků, ať už v rámci provozu IT, nebo nezávisle, jak se provoz IT přesouvá online.

## <a name="monitoring"></a>Monitorování

*Monitorování* je shromažďování a analýza dat s cílem určit výkon, stav a dostupnost podnikové úlohy a prostředků, na kterých závisí. Azure obsahuje více služeb, které v prostoru monitorování samostatně provádějí určité role nebo úlohy. Tyto služby společně poskytují komplexní řešení pro shromažďování dat, analýzy a akce na základě telemetrie z využití vašich úloh a prostředků Azure, které je podporují. Získejte přehled o stavu a výkonu aplikací, infrastruktury a dat v Azure pomocí nástrojů pro monitorování cloudu, jako jsou Azure Monitor, Log Analytics a Application Insights. Pomocí těchto nástrojů pro monitorování cloudu můžete podniknout potřebné kroky a provést integraci s řešeními pro správu služeb:

- **Základní monitorování:** Základní monitorování poskytuje nezbytné elementární monitorování prostředků Azure. Tyto služby vyžadují minimální konfiguraci a shromažďují základní telemetrii, kterou používají služby monitorování úrovně Premium.
- **Hloubkové monitorování aplikací a infrastruktury:** Služby Azure nabízejí řadu možností pro shromažďování dat monitorování a pro jejich analýzy na hlubší úrovni. Tyto služby využívají základní monitorování a běžné funkce v Azure. Nabízejí výkonné analytické nástroje pro práci se shromažďovanými daty a poskytují jedinečný přehled o vašich aplikacích a infrastruktuře.

Další informace o [Azure Monitoru](https://docs.microsoft.com/azure/azure-monitor/overview) pro monitorování migrovaných prostředků

## <a name="security-monitoring"></a>Monitorování zabezpečení

Spolehněte se na službu Azure Security Center, která zajišťuje jednotné monitorování zabezpečení a pokročilé upozorňování na hrozby napříč hybridními cloudovými úlohami. Security Center poskytuje úplný přehled a kontrolu nad zabezpečením cloudových aplikací v Azure. Rychle detekujte hrozby, reagujte na ně a snižte svou zranitelnost vůči hrozbám povolením adaptivní ochrany před hrozbami. Integrovaný řídicí panel poskytuje okamžitý přehled o výstrahách a ohroženích zabezpečení vyžadujících pozornost. Azure Security Center pomáhá s řadou funkcí, včetně následujících:

- **Centralizované monitorování zásad:** Zajistěte dodržování předpisů společnosti nebo soulad se zákonnými požadavky na zabezpečení díky centrální správě zásad zabezpečení napříč hybridními cloudovými úlohami.
- **Nepřetržité posuzování zabezpečení:** Monitorujte zabezpečení počítačů, sítí, služeb úložiště, datových služeb a aplikací za účelem zjišťování potenciálních problémů se zabezpečením.
- **Praktická doporučení:** Napravujte ohrožení zabezpečení dříve, než je útočníci mohou zneužít. Součástí jsou praktická doporučení pro zabezpečení s určením priority.
- **Pokročilá cloudová ochrana:** Omezte hrozby díky přístupu k portům pro správu za běhu a řízení aplikací spuštěných na virtuálních počítačích jejich přidáváním na seznam povolených.
- **Upozornění a incidenty s určenou prioritou:** Zaměřte se nejprve na nejdůležitější hrozby díky upozorněním a incidentům zabezpečení s určenou prioritou.
- **Integrovaná řešení zabezpečení:** Shromažďujte, prohledávejte a analyzujte data o zabezpečení z nejrůznějších zdrojů, včetně propojených partnerských řešení.

Další informace o službě [Azure Security Center](https://docs.microsoft.com/azure/security-center) pro zabezpečení migrovaných prostředků

## <a name="service-health-monitoring"></a>Monitorování stavu služby

Azure Service Health nabízí upozornění a pokyny na míru v situacích, kdy vás ovlivňují problémy se službami Azure. Mohou vás upozornit, pomohou vám zjistit dopad případných potíží a upozorní vás na jejich vyřešení. Také vám pomohou připravit se na plánovanou údržbu a změny, které by mohly ovlivnit dostupnost vašich prostředků.

- **Řídicí panel pro sledování stavu služby:** Projděte si celkový stav služeb a oblastí Azure s podrobnými informacemi o stávajících problémech se službami, chystané plánované údržbě a převodech služeb.
- **Upozornění týkající se stavu služby:** Nakonfigurujte si upozornění, která budou vás a vaše týmy informovat v případě potíží se službou, jako je výpadek nebo chystaná plánovaná údržba.
- **Historie stavu služby:** Projděte si předchozí problémy se službou a stáhněte si oficiální souhrny a sestavy od Microsoftu.

Přečtěte si víc o službě [Azure Service Health](https://docs.microsoft.com/azure/service-health) a zajistěte si informovanost o stavu vašich migrovaných prostředků.

## <a name="protect-assets-and-data"></a>Ochrana prostředků a dat

Azure Backup poskytuje způsob, jak chránit virtuální počítače, soubory a data. Azure Backup pomáhá s řadou funkcí, včetně následujících:

- Zálohování virtuálních počítačů
- Zálohování souborů
- Zálohování databází SQL Serveru
- Obnovení chráněných prostředků

Další informace o [Azure Backupu](https://docs.microsoft.com/azure/backup) pro ochranu migrovaných prostředků

## <a name="optimize-resources"></a>Optimalizace prostředků

Azure Advisor je průvodce s individuálními doporučeními pro osvědčené postupy Azure. Analyzuje vaše konfigurace a telemetrii využití a nabízí doporučení, která vám pomohou optimalizovat prostředky Azure a zajistit vysokou dostupnost, zabezpečení a výkon a efektivitu nákladů. Vložené akce Advisoru vám pomohou rychle a snadno zpracovat doporučení a optimalizovat vaše nasazení.

- **Osvědčené postupy Azure:** Optimalizujte migrované prostředky z hlediska vysoké dostupnosti, zabezpečení,výkonu a nákladů.
- **Podrobné pokyny:** Využijte možnost efektivního zpracování doporučení prostřednictvím rychlých odkazů s pokyny.
- **Upozornění na nová doporučení:** Zajistěte si přehled o nových doporučeních, jako jsou další příležitosti k nastavení správné velikosti virtuálních počítačů a úspoře nákladů.

Přečtěte si další informace o použití [Azure Advisoru ](https://docs.microsoft.com/azure/advisor/advisor-overview) při optimalizaci migrovaných prostředků.

## <a name="suggested-skills"></a>Navrhované dovednosti

Microsoft Learn je nový přístup ke studiu. Připravenosti na nové dovednosti a úkoly, které souvisejí s přechodem do cloudu, není snadné dosáhnout. Microsoft Learn poskytuje efektivnější přístup k praktické výuce, který vám umožní dosáhnout vašich cílů rychleji. Získávejte body, nové úrovně a dovednosti!

Tady je příklad přizpůsobeného studijního programu na Microsoft Learn, který je v souladu s částí architektury přechodu na cloud věnovanou zabezpečení a správě: 

[Zabezpečení cloudových dat:](https://docs.microsoft.com/learn/paths/secure-your-cloud-data/) Platforma Azure byla navržená tak, aby zajišťovala bezpečí a dodržování předpisů. Zjistěte, jak využít integrované služby k bezpečnému ukládání dat aplikací, abyste měli jistotu, že k nim budou mít přístup jenom autorizovaní klienti a služby.
