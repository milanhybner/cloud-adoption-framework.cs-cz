---
title: Služby a nástroje pro správu serveru Azure
description: Služby a nástroje pro správu serveru Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: df6851ff628c0abcb38ee9139fcf24f31e2117cf
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223288"
---
# <a name="azure-server-management-tools-and-services"></a>Služby a nástroje pro správu serveru Azure

Jak je popsáno v [přehledu](./index.md) tohoto návodu, sada Azure Server Management Services pokrývá tyto oblasti:

- Migrace
- Zabezpečení
- Ochrana
- Monitorování
- Konfigurace
- Řízení

Následující části stručně popisují tyto oblasti správy a poskytují odkazy na podrobný obsah hlavních služeb Azure, které je podporují.

## <a name="migrate"></a>Migrace

Služby migrace vám pomůžou migrovat vaše úlohy do Azure. Pro zajištění nejlepšího návodu se služba Azure Migrate spustí tím, že měří výkon místního serveru a vyhodnocování vhodnosti pro migraci. Až Azure Migrate dokončí posouzení, můžete k migraci místních počítačů do Azure použít [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) a [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) .

## <a name="secure"></a>Zabezpečení

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) je komplexní aplikace pro správu zabezpečení. Po připojení k Security Center můžete rychle získat posouzení stavu dodržování předpisů ve vašem prostředí. Pokyny k inzprovoznění serverů pro Azure Security Center najdete v tématu [Konfigurace služeb správy Azure pro předplatné](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Ochrana

Pro ochranu vašich dat je potřeba naplánovat zálohování, vysokou dostupnost, šifrování, autorizaci a související provozní problémy. Tato témata jsou pokrytá rozsáhle online, takže se můžete soustředit na vytvoření plánu provozní kontinuity a zotavení po havárii (BCDR). Budeme obsahovat odkazy na dokumentaci, která podrobně popisuje, jak implementovat a nasadit tento typ plánu.

Při sestavování strategií ochrany dat zvažte nejprve rozdělení aplikací úloh do jejich různých vrstev. Tento přístup pomáhá, protože každá vrstva obvykle vyžaduje svůj vlastní jedinečný plán ochrany. Další informace o navrhování aplikací tak, aby byly odolné, najdete v tématu [navrhování odolných aplikací pro Azure](https://docs.microsoft.com/azure/architecture/resiliency).

Základní ochrana dat je zálohovaná. Pokud chcete urychlit proces obnovení, pokud dojde ke ztrátě serverů, zálohujte nejen data, ale také konfigurace serveru. Backup je účinný mechanismus pro zpracování náhodných odstranění dat a ransomwarem útoků. [Azure Backup](https://docs.microsoft.com/azure/backup) vám může pomáhat chránit vaše data v Azure a na místních serverech se systémem Windows nebo Linux. Podrobnosti o tom, co zálohování může dělat a návody najdete v [dokumentaci k Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Obnovení prostřednictvím zálohování může trvat dlouhou dobu. Obor Standard je obvykle jeden den. Pokud úloha vyžaduje kontinuitu podnikových procesů při selhání hardwaru nebo výpadku datového centra, zvažte použití replikace dat. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) poskytuje průběžnou replikaci vašich virtuálních počítačů, což je řešení, které zajišťuje neminimální ztrátu dat. Site Recovery také podporuje několik scénářů replikace, jako je například replikace:

- Virtuálních počítačů Azure mezi dvěma oblastmi Azure.
- Mezi místními servery.
- Mezi místními servery a Azure.

Další informace najdete v tématu [úplná Azure Site Recoveryová matice replikace](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

Pro data souborového serveru je [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)další službu, která se má zvážit. Tato služba vám pomůže centralizovat sdílené složky ve vaší organizaci ve službě soubory Azure a současně zachovává flexibilitu, výkon a kompatibilitu místního souborového serveru. Chcete-li použít tuto službu, postupujte podle pokynů pro nasazení Azure File Sync.

## <a name="monitor"></a>Monitorování

[Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) poskytuje zobrazení různých prostředků, jako jsou aplikace, kontejnery a virtuální počítače. Shromažďuje také data z několika zdrojů:

- Azure Monitor pro virtuální počítače ([Insights](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)) poskytuje podrobné zobrazení stavu virtuálního počítače, trendů výkonu a závislostí. Služba monitoruje stav operačních systémů virtuálních počítačů Azure, virtuálních počítačů s měřítkem a počítačů ve vašem místním prostředí.
- Log Analytics ([protokoly](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)) je funkce Azure monitor. Jeho role má střed k celkovému scénáři správy Azure. Slouží jako úložiště dat pro analýzu protokolů a pro mnoho dalších služeb Azure. Nabízí bohatý dotazovací jazyk a analytický modul, který poskytuje přehled o provozu vašich aplikací a prostředků.
- [Protokol aktivit Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) je také funkcí Azure monitor. Poskytuje přehled o událostech na úrovni předplatného, ke kterým dochází v Azure.

## <a name="configure"></a>Konfigurace

Do této kategorie patří několik služeb. Můžou vám:

- Automatizujte provozní úlohy.
- Spravujte konfigurace serveru.
- Měření shody aktualizací
- Naplánujte aktualizace.
- Detekuje změny serverů.

Tyto služby jsou nezbytné pro podporu pokračujících operací:

- [Update Management](https://docs.microsoft.com/azure/automation/automation-update-management#view-update-assessments) automatizuje nasazení oprav v celém prostředí, včetně nasazení instancí operačního systému spuštěných mimo Azure. Podporuje operační systémy Windows i Linux a sleduje klíčové chyby zabezpečení operačního systému a neshodu v důsledku chybějících oprav.
- [Change Tracking a inventář](https://docs.microsoft.com/azure/automation/change-tracking) nabízí přehled o softwaru, který je spuštěný ve vašem prostředí, a zvýrazní všechny změny, ke kterým došlo.
- [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) umožňuje spouštět skripty Pythonu a PowerShellu a runbooky pro automatizaci úloh ve vašem prostředí. Pokud používáte automatizaci s [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker), můžete své Runbooky také rozmístit na místní prostředky.
- [Konfigurace stavu Azure Automation](https://docs.microsoft.com/azure/automation/automation-dsc-overview) umožňuje doručovat konfigurace požadovaných stavů prostředí PowerShell přímo z Azure. DSC taky umožňuje monitorovat a uchovávat konfigurace hostovaných operačních systémů a úloh.

## <a name="govern"></a>Řízení

Při přijetí a přesunu do cloudu se vytvoří nové výzvy ke správě. Při přesunu z režie provozní správy do monitorování a zásad správného řízení vyžaduje jiný místo. Rozhraní pro přijetí do cloudu pro Azure začíná [zásadou správného řízení](../../govern/index.md). V tomto rozhraní je vysvětleno, jak migrovat do cloudu, jak bude cesta vypadat a kdo má být součástí.

Návrh zásad správného řízení pro standardní organizace se často liší od návrhu zásad správného řízení pro komplexní podniky. Další informace o osvědčených postupech pro zásady správného řízení pro standardní organizaci najdete v tématu [standardní příručka pro zásady správného řízení podniku](../../govern/guides/standard/index.md). Další informace o osvědčených postupech pro zásady správného řízení pro komplexní podnik najdete v [příručce pro zásady správného řízení pro komplexní podniky](../../govern/guides/complex/index.md).

## <a name="billing-information"></a>Informace o fakturaci

Další informace o cenách pro služby Azure Management Services najdete na těchto stránkách:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Azure Automation](https://azure.microsoft.com/pricing/details/automation), včetně:
  - Desired State Configuration
  - Služba Azure Update Management
  - Služby Azure Change Tracking a Inventory Services

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Služba Azure File Sync](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Řešení Azure Update Management je bezplatné, ale v souvislosti s přijímáním dat se účtují malé náklady. Jako pravidlo palec je prvních 5 gigabajtů (GB) za měsíc přijímání dat zdarma. Obecně se sleduje, že každý počítač používá přibližně 25 MB za měsíc. To znamená, že přibližně 200 počítačů za měsíc se zaplatí zdarma. U více serverů vynásobte počet dalších serverů o 25 MB za měsíc. Potom výsledek vynásobte cenou za úložiště pro další úložiště, které potřebujete. Informace o cenách najdete v tématu [Azure Storage Overview (přehled](https://azure.microsoft.com/pricing/details/storage)). Každý další server má obvykle nominální dopad na náklady.
