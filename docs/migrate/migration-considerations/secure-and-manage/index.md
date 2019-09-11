---
title: Zabezpečení a správa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nástroje pro monitorování a správu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 14bd697a3332466fb97043d3420d80b1dca50679
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818127"
---
# <a name="secure-monitoring-and-management-tools"></a>Nástroje pro monitorování a správu

Po dokončení migrace by se migrované prostředky měly spravovat v rámci kontrolovaného provozu IT. Cílem tohoto článku není navrhovat odchylky od osvědčených provozních postupů. Následující text byste měli vnímat jako MVP (Minimum Viable Product) pro zabezpečení a správu migrovaných prostředků, ať už v rámci provozu IT, nebo nezávisle, jak se provoz IT přesouvá online.

## <a name="monitoring"></a>Monitorování

*Monitorování* je shromažďování a analýza dat s cílem určit výkon, stav a dostupnost podnikové úlohy a prostředků, na kterých závisí. Azure obsahuje více služeb, které v prostoru monitorování samostatně provádějí určité role nebo úlohy. Tyto služby společně poskytují komplexní řešení pro shromažďování dat, analýzy a akce na základě telemetrie z využití vašich úloh a prostředků Azure, které je podporují. Získejte přehled o stavu a výkonu aplikací, infrastruktury a dat v Azure pomocí nástrojů pro monitorování cloudu, jako jsou Azure Monitor, Log Analytics a Application Insights. Pomocí těchto nástrojů pro monitorování cloudu můžete podniknout potřebné kroky a provést integraci s řešeními pro správu služeb:

- **Základní monitorování:** Základní monitorování poskytuje nezbytné elementární monitorování prostředků Azure. Tyto služby vyžadují minimální konfiguraci a shromažďují základní telemetrii, kterou používají služby monitorování úrovně Premium.
- **Hloubkové monitorování aplikací a infrastruktury:** Služby Azure nabízejí řadu možností pro shromažďování dat monitorování a pro jejich analýzy na hlubší úrovni. Tyto služby využívají základní monitorování a běžné funkce v Azure. Nabízejí výkonné analytické nástroje pro práci se shromažďovanými daty a poskytují jedinečný přehled o vašich aplikacích a infrastruktuře.

Další informace o [Azure Monitoru](/azure/azure-monitor/overview) pro monitorování migrovaných prostředků

## <a name="security-monitoring"></a>Monitorování zabezpečení

Spolehněte se na službu Azure Security Center, která zajišťuje jednotné monitorování zabezpečení a pokročilé upozorňování na hrozby napříč hybridními cloudovými úlohami. Security Center poskytuje úplný přehled a kontrolu nad zabezpečením cloudových aplikací v Azure. Rychle detekujte hrozby, reagujte na ně a snižte svou zranitelnost vůči hrozbám povolením adaptivní ochrany před hrozbami. Integrovaný řídicí panel poskytuje okamžitý přehled o výstrahách a ohroženích zabezpečení vyžadujících pozornost. Azure Security Center pomáhá s řadou funkcí, včetně následujících:

- **Centralizované monitorování zásad:** Zajistěte dodržování předpisů společnosti nebo soulad se zákonnými požadavky na zabezpečení díky centrální správě zásad zabezpečení napříč hybridními cloudovými úlohami.
- **Nepřetržité posuzování zabezpečení:** Monitorujte zabezpečení počítačů, sítí, služeb úložiště, datových služeb a aplikací za účelem zjišťování potenciálních problémů se zabezpečením.
- **Praktická doporučení:** Napravujte ohrožení zabezpečení dříve, než je útočníci mohou zneužít. Součástí jsou praktická doporučení pro zabezpečení s určením priority.
- **Pokročilá cloudová ochrana:** Omezte hrozby díky přístupu k portům pro správu za běhu a řízení aplikací spuštěných na virtuálních počítačích jejich přidáváním na seznam povolených.
- **Upozornění a incidenty s určenou prioritou:** Zaměřte se nejprve na nejdůležitější hrozby díky upozorněním a incidentům zabezpečení s určenou prioritou.
- **Integrovaná řešení zabezpečení:** Shromažďujte, prohledávejte a analyzujte data o zabezpečení z nejrůznějších zdrojů, včetně propojených partnerských řešení.

Další informace o službě [Azure Security Center](/azure/security-center) pro zabezpečení migrovaných prostředků

## <a name="protect-assets-and-data"></a>Ochrana prostředků a dat

Azure Backup poskytuje způsob, jak chránit virtuální počítače, soubory a data. Azure Backup pomáhá s řadou funkcí, včetně následujících:

- Zálohování virtuálních počítačů
- Zálohování souborů
- Zálohování databází SQL Serveru
- Obnovení chráněných prostředků

Další informace o [Azure Backupu](/azure/backup) pro ochranu migrovaných prostředků
