---
title: Služby a nástroje pro správu serveru Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Služby a nástroje pro správu serveru Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 854653882b8a07662da092ee4ec0006644000f56
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028379"
---
# <a name="azure-server-management-tools-and-services"></a>Služby a nástroje pro správu serveru Azure

Jak je popsáno v [přehledu](./index.md) v této části, sada Azure Server Management Services zahrnuje tyto oblasti:

- [Migrace](#migrate)
- [Zabezpečení](#secure)
- [Ochrana](#protect)
- [Monitorování](#monitor)
- [Konfigurace](#configure)
- [Bude](#govern)

Následující části stručně popisují tyto oblasti správy a poskytují odkazy na podrobný obsah hlavních služeb Azure, které je podporují.

## <a name="migrate"></a>Migrace

Služby migrace vám pomůžou migrovat vaše úlohy do Azure. Pro zajištění nejlepšího návodu se služba Azure Migrate spustí tím, že měří výkon místního serveru a vyhodnocování vhodnosti pro migraci. Až Azure Migrate dokončí posouzení, můžete k migraci místních počítačů do Azure použít [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) a [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) .

## <a name="secure"></a>Zabezpečení

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) je komplexní aplikace pro správu zabezpečení. Po připojení k Security Center můžete rychle získat posouzení stavu dodržování předpisů ve vašem prostředí. Pokyny k inzprovoznění serverů pro Azure Security Center najdete v tématu [Konfigurace služeb správy Azure pro předplatné](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Ochrana

Pro ochranu vašich dat je potřeba naplánovat zálohování, vysokou dostupnost, šifrování, autorizaci a související provozní problémy. Tato témata jsou pokrytá rozsáhle online, takže se podíváme na sestavení plánu zotavení po havárii pro podnikovou kontinuitu (BCDR). Budeme obsahovat odkazy na dokumentaci, která podrobně popisuje, jak implementovat a nasadit tento typ plánu.

Když vytváříte strategie ochrany dat, měli byste nejdřív zvážit rozdělení aplikací úloh do jejich různých vrstev, protože každá vrstva obvykle vyžaduje vlastní jedinečný plán ochrany. Další informace o navrhování aplikací tak, aby byly odolné, najdete v tématu [navrhování odolných aplikací pro Azure](https://docs.microsoft.com/azure/architecture/resiliency).

Základní ochrana dat je zálohovaná. K urychlení procesu obnovení v případě ztráty serveru byste měli zálohovat nejen data, ale také konfigurace serveru. Backup je účinný mechanismus pro zpracování náhodných odstranění dat a ransomwarem útoků. [Azure Backup](https://docs.microsoft.com/azure/backup) vám může pomáhat chránit vaše data v Azure a na místních serverech se systémem Windows nebo Linux. Podrobnosti o funkcích a průvodcích této služby najdete v [dokumentaci k Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Obnovení prostřednictvím zálohování může trvat dlouhou dobu. Obor Standard je obvykle jeden den. Pokud úloha vyžaduje kontinuitu podnikových procesů při selhání hardwaru nebo výpadku datového centra, zvažte použití replikace dat. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) poskytuje průběžnou replikaci vašich virtuálních počítačů, což je řešení, které zajišťuje neminimální ztrátu dat. Site Recovery taky podporuje několik scénářů replikace, jako je například replikace virtuálních počítačů Azure mezi dvěma oblastmi Azure, mezi místními servery a mezi místními a Azure. Další informace najdete v tématu [úplná Azure Site Recoveryová matice replikace](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

Pro data souborového serveru je [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)další službu, která se má zvážit. Tato služba umožňuje centralizovat sdílené složky ve vaší organizaci ve službě soubory Azure a současně zachovat flexibilitu, výkon a kompatibilitu místního souborového serveru. Chcete-li použít tuto službu, postupujte podle pokynů pro nasazení Azure File Sync.

## <a name="monitor"></a>Monitorování

[Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) poskytuje zobrazení různých prostředků, jako jsou aplikace, kontejnery a virtuální počítače. Shromažďuje také data z několika zdrojů.

- Azure Monitor pro virtuální počítače ([Insights](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)) poskytuje podrobné zobrazení stavu virtuálního počítače, trendů výkonu a závislostí. Služba monitoruje stav operačních systémů virtuálních počítačů Azure, virtuálních počítačů s měřítkem a počítačů ve vašem místním prostředí.
- Log Analytics ([protokoly](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)) je funkce Azure monitor. Jeho role má střed k celkovému scénáři správy Azure. Slouží jako úložiště dat pro analýzu protokolů a pro mnoho dalších služeb Azure. Nabízí bohatý dotazovací jazyk a analytický modul, který poskytuje přehled o provozu vašich aplikací a prostředků.
- [Protokol aktivit Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) je také funkcí Azure monitor. Poskytuje přehled o událostech na úrovni předplatného, ke kterým dochází v Azure.

## <a name="configure"></a>Konfigurace

Do této kategorie patří několik služeb. Můžou vám pomůžou automatizovat provozní úlohy, spravovat konfigurace serverů, měřit dodržování předpisů aktualizací, plánovat aktualizace a zjišťovat změny serverů. Tyto služby jsou jádrem podpory pokračujících operací.

- [Update Management](https://docs.microsoft.com/azure/automation/automation-update-management#viewing-update-assessments) automatizuje nasazení oprav v celém prostředí, včetně nasazení instancí operačních systémů, které běží mimo Azure. Podporuje operační systémy Windows i Linux a sleduje klíčové chyby zabezpečení a neshodující se s operačním systémem a způsobuje chybějící opravy.
- [Change Tracking a inventář](https://docs.microsoft.com/azure/automation/change-tracking) nabízí přehled o softwaru, který je spuštěný ve vašem prostředí, a obsahuje všechny změny, ke kterým došlo.
- [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) umožňuje spouštět skripty Pythonu a PowerShell nebo Runbooky pro automatizaci úloh napříč vaším prostředím. Při použití s [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)můžete své Runbooky rozmístit i na místní prostředky.
- [Konfigurace stavu Azure Automation](https://docs.microsoft.com/azure/automation/automation-dsc-overview) umožňuje doručovat konfigurace požadovaných stavů prostředí PowerShell přímo z Azure. V takovém případě DSC umožňuje monitorovat a zachovávat konfigurace operačního systému a úloh v hostovaném operačním systému.

## <a name="govern"></a>Řízení

Při přijetí a přesunu do cloudu se vytvoří nové výzvy ke správě a při přesunu z režie provozní správy na monitorování a řízení se vyžaduje jiný místo. Rozhraní pro přijetí do cloudu pro Azure začíná [zásadou správného řízení](../../govern/index.md). Vysvětluje, jak migrovat do cloudu, jak bude cesta vypadat, jako by měla být zahrnuta.

Návrh zásad správného řízení pro standardní organizace se často liší od návrhu zásad správného řízení pro komplexní podniky. Další informace o osvědčených postupech pro zásady správného řízení pro standardní organizaci najdete v tématu [standardní příručka zásad správného řízení](../../govern/guides/standard/index.md). Další informace o osvědčených postupech pro zásady správného řízení pro komplexní podnik najdete v tématu [Příručka zásad správného řízení pro komplexní podniky](../../govern/guides/complex/index.md).

## <a name="billing-information"></a>Informace o fakturaci

Další informace o cenách pro služby Azure Management Services najdete na těchto stránkách:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Služba Azure Update Management](https://azure.microsoft.com/pricing/details/automation)

- [Služby Azure Change Tracking a Inventory Services](https://azure.microsoft.com/pricing/details/automation)

- [Konfigurace požadovaného stavu](https://azure.microsoft.com/pricing/details/automation)

- [Služba Azure Automation](https://azure.microsoft.com/pricing/details/automation)

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Služba Azure File Sync](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Řešení Azure Update Management je bezplatné, ale v souvislosti s přijímáním dat se účtují malé náklady. Jako pravidlo palce je prvních 5 GB za měsíc přijímání dat za měsíc zdarma. Obecně se sleduje, že každý počítač používá přibližně 25 MB za měsíc. Takže přibližně 200 počítačů za měsíc jsou pokryty zdarma. Pro každý další server vynásobte počet dalších serverů o 25 MB za měsíc. Vynásobte to náklady na úložiště pro celkovou velikost úložiště, kterou potřebujete. [Náklady na úložiště jsou k dispozici zde](https://azure.microsoft.com/pricing/details/storage/). Každý další server by měl mít Jmenovitý dopad na náklady.
