---
title: 'Migrace sálového počítače: Přepnutí z sálových počítačů do Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrujte aplikace z sálových prostředí do Azure pro systémy, které se aktuálně spouštějí na sálových počítačích.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3296a471540c921d465859d0dfd800a91996f721
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70831357"
---
# <a name="make-the-switch-from-mainframes-to-azure"></a>Přepnutí z sálových počítačů do Azure

Azure jako alternativní platforma pro spouštění tradičních sálových aplikací nabízí výpočetní výkon a úložiště v prostředí s vysokou dostupností. Získáte hodnotu a flexibilitu moderní cloudové platformy bez nákladů spojených s prostředím sálového počítače.

V této části najdete technické informace o tom, jak přepnout z sálové platformy do Azure.

![Sálové počítače a Azure](../../_images/mainframe-migration/make-the-switch.png)

## <a name="mips-vs-vcpus"></a>MIPS vs. vCPU

Neexistuje žádný vzorec univerzálního mapování, který neexistuje pro určení počtu virtuálních jednotek vCPU potřebných ke spouštění sálových úloh. Metrika milionů instrukcí za sekundu (MIPS) je ale často namapovaná na vCPU v Azure. MIPS měří celkovou výpočetní sílu sálového počítače tím, že poskytuje konstantní hodnotu počtu cyklů za sekundu pro daný počítač.

Malá organizace může vyžadovat méně než 500 MIPS, zatímco velká organizace obvykle používá více než 5 000 MIPS. Při $1 000 na jedno MIPS má velké organizace při nasazení infrastruktury 5 000-MIPS přibližně $5 000 000. Odhad ročních nákladů na typické nasazení Azure této škály je přibližně jedna z deseti nákladů na infrastrukturu MIPS. Podrobnosti najdete v části Tabulka 4 v [Demystifying sálovém počítače – do Azure. Dokument](https://azure.microsoft.com/resources/demystifying-mainframe-to-azure-migration) White paper o migraci

Přesný výpočet MIPS pro vCPU s Azure závisí na typu vCPU a na přesném zatížení, které používáte. Studie srovnávacích testů ale poskytují dobrý základ pro odhad počtu a typu vCPU, který budete potřebovat. Nedávné srovnávací testy HPE zREF poskytují tyto odhady:

- 288 MIPS na procesory založené na technologii Intel, běžící na počítačích se systémem HP provázané servery pro online úlohy (CICS).

- 170 MIPS na Intel Core pro dávkové úlohy COBOL.

Tato příručka odhadne 200 MIPS na vCPU pro online zpracování a 100 MIPS na vCPU pro dávkové zpracování.

> [!NOTE]
> Tyto odhady se mohou změnit, protože nové řady virtuálních počítačů budou v Azure dostupné.

## <a name="high-availability-and-failover"></a>Vysoká dostupnost a převzetí služeb při selhání

Sálové systémy často nabízejí pět dostupnosti devítky (99,999 procent), když se používají Sysplexy na sálovém a paralelním. Stále je potřeba naplánovat výpadky pro údržbu a počáteční načtení programu (IPLs). Skutečná dostupnost se blíží dvěma nebo třemi devítkyům, podobně jako u serverů s vysokým konečným využitím Intel.

Díky porovnání Azure nabízí smlouvy o úrovni služeb (SLA) založené na závazku, kde je výchozím nastavením více devítky dostupnosti, které jsou optimalizované pro místní nebo geografickou replikaci služeb.

Azure poskytuje další dostupnost tím, že replikuje data z více úložných zařízení, a to buď místně, nebo v jiných geografických oblastech. V případě selhání založeného na Azure mají výpočetní prostředky přístup k replikovaným datům na místní nebo regionální úrovni.

Když použijete prostředky Azure Platform as a Service (PaaS), jako je například [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) a [Azure Cosmos Database](/azure/cosmos-db/introduction), může Azure automaticky zpracovávat převzetí služeb při selhání. Pokud používáte infrastrukturu Azure jako službu (IaaS), převzetí služeb při selhání se spoléhá na konkrétní systémové funkce, jako je SQL Server třeba funkce služby Always On, instance clusteringu s podporou převzetí služeb při selhání a skupiny dostupnosti.

## <a name="scalability"></a>Škálovatelnost

Při horizontálním navýšení kapacity cloudových prostředí se většinou škálují sálové počítače. Sálové počítače můžou škálovat s využitím zařízení (CF), ale vysoké náklady na hardware a úložiště usnadňují horizontální navýšení kapacity u sálových počítačů.

CF také nabízí vysoce spárované výpočetní prostředky, zatímco funkce škálování na více instancí Azure jsou volně spojené. Cloud se dá škálovat nahoru nebo dolů, aby odpovídal přesným uživatelským specifikacím, a to s výpočetním výkonem, úložištěm a službami na vyžádání v rámci fakturačního modelu založeného na využití.

## <a name="backup-and-recovery"></a>Backup a obnovení

Zákazníci z sálových počítačů obvykle udržují weby pro zotavení po havárii nebo využívají nebo nezávislého poskytovatele sálového počítače při haváriích. Synchronizace s webem pro obnovení po havárii se obvykle provádí prostřednictvím offline kopií dat. Obě možnosti účtují vysoké náklady.

Automatizovaná geografická redundance je také k dispozici prostřednictvím spojovacího zařízení v rámci sálového počítače, a to i v případě skvělého výdaje a je obvykle vyhrazena pro klíčové systémy. Azure naopak nabízí snadno implementované a nákladově efektivní možnosti pro [zálohování](/azure/backup/backup-introduction-to-azure-backup), [obnovu](/azure/site-recovery/site-recovery-overview)a [redundanci](/azure/storage/common/storage-redundancy) na místních nebo regionálních úrovních nebo prostřednictvím geografické redundance.

## <a name="storage"></a>Storage

Část porozumění fungování sálových počítačů zahrnuje dekódování různých překrývajících se podmínek. Například centrální úložiště, skutečná paměť, reálné úložiště a hlavní úložiště obecně odkazují na úložiště připojené přímo k sálovému procesoru.

Sálový hardware obsahuje procesory a mnoho dalších zařízení, jako jsou například úložná zařízení s přímým přístupem (DASDs), magnetické páskové jednotky a několik typů uživatelských konzol. Pásky a DASDs se používají pro systémové funkce a uživatelské programy.

Mezi typy fyzického úložiště pro sálové počítače patří:

- **Centrální úložiště:** Nachází se přímo na sálovém procesoru, označované také jako procesor nebo reálné úložiště.
- **Pomocné úložiště:** Tento typ se nachází odděleně od sálového počítače, ale obsahuje úložiště v DASDs a také se označuje jako stránkovací úložiště.

Cloud nabízí řadu flexibilních, škálovatelných možností a platíte jenom za tyto možnosti, které potřebujete. [Azure Storage](/azure/storage/common/storage-introduction) nabízí rozsáhle škálovatelné úložiště objektů pro datové objekty, službu systému souborů pro Cloud, spolehlivé úložiště pro zasílání zpráv a NoSQL úložiště. U virtuálních počítačů poskytují spravované a nespravované disky Trvalé a zabezpečené úložiště na disku.

## <a name="mainframe-development-and-testing"></a>Vývoj a testování sálového počítače

Hlavním ovladačem v projektech migrace v rámci sálového počítače je měnící se tvář vývoje aplikací. Organizace chtějí, aby jejich vývojové prostředí bylo bezpečnější a reagovat na obchodní potřeby.

Sálové počítače mají typicky samostatné logické oddíly (LPARs) pro vývoj a testování, jako je třeba QA a fázování LPARs. Mezi řešení pro vývoj sálových počítačů patří kompilátory (COBOL, PL/I, assembler) a editory. Nejběžnější je ISPF (Interactive System produktivity) pro operační systém z/OS, který běží na sálovch počítačích IBM. Jiní uživatelé zahrnují nástroje ROSCOE Programming Facility (RPF) a Computer Associates Tools, jako je CA Librarian a CA-Panvalet.

Prostředí pro emulaci a kompilátory jsou dostupné na platformách x86, takže vývoj a testování můžou být obvykle mezi prvními úlohami migrace z sálového počítače do Azure. Dostupnost a širší využití [nástrojů DevOps v Azure](https://azure.microsoft.com/solutions/devops) urychluje migraci vývojových a testovacích prostředí.

Po vývoji a testování řešení v Azure a připravených k nasazení do sálového počítače budete muset zkopírovat kód do sálového počítače a zkompilovat ho tam.

## <a name="next-steps"></a>Další postup

> [!div class="nextstepaction"]
> [Migrace aplikace na sálové počítače](application-strategies.md)