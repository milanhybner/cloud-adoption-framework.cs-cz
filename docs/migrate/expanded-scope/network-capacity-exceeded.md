---
title: Překročení síťové kapacity
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Požadavky na data přesahují kapacitu sítě během migrace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 402628da8fb5af7526c33d6c4900298eb42bced5
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753494"
---
# <a name="data-requirements-exceed-network-capacity-during-a-migration-effort"></a>Požadavky na data přesahují kapacitu sítě během migrace.

Při migraci do cloudu se prostředky replikují a synchronizují po síti mezi stávajícím datacentrem a cloudem. Není neobvyklé, že požadavky vyplývající z velikosti stávajících dat různých úloh překračují kapacitu sítě. V takových scénářích se může postup migrace výrazně zpomalit a v některých případech i úplně zastavit. Následující pokyny rozšiřují obsah [příručky k migraci do Azure](../azure-migration-guide/index.md) a nabízejí řešení, jak obejít omezení sítě.

## <a name="general-scope-expansion"></a>Obecné rozšíření rozsahu

Většina práce požadované v tomto rozšíření obsahu probíhá v rámci předběžných, vyhodnocovacích a migračních procesů.

## <a name="suggested-prerequisites"></a>Doporučené požadavky

**Ověření rizik kapacity sítě:** [racionalizace digitální nemovitosti](../../digital-estate/rationalize.md) je vysoce doporučená požadovaná součást, zejména v případě, že existují obavy o přetěžování dostupné kapacity sítě. Při racionalizaci digitálních aktiv se shromažďují podklady pro [inventarizaci digitálních prostředků](../../digital-estate/inventory.md). Tato inventarizace by měla zahrnovat požadavky na stávající úložiště digitálních aktiv. Jak je uvedeno v [části rizika replikace: fyzika replikace](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication), kterou lze použít k odhadu **celkové velikosti migračních dat**, která může být porovnána s celkovou **dostupnou šířkou pásma migrace**. Pokud toto srovnání neodpovídá požadované **době na změnu firmy**, může vám tento článek pomoci zrychlit migraci tím, že zkrátí čas potřebný k migraci datacentra.

**Offline přenos nezávislých úložišť dat:** Obrázek v následujícím diagramu je příkladem přenosů dat online i offline s Azure Data Box. Tyto postupy můžete použít k přenosu velkých objemů dat do cloudu ještě před migrací úloh. Při offline přenosu dat se zdrojová data zkopírují do služby Azure Data Box a následně se fyzicky přesunou do Microsoftu, který je přenese do účtu úložiště Azure jako soubor nebo objekt blob. Tento postup je možné použít před dalšími migračními úkoly k přesunu dat, která nejsou přímo spojena s určitou úlohou. Tímto způsobem snížíte množství dat, které je potřeba přesunout po síti, abyste mohli dokončit migraci i s omezeními sítě.

Tento přístup je možné použít k přenosu dat HDFS, záloh, archivů, souborových serverů, aplikací apod. Stávající technické pokyny vysvětlují, jak tento přístup použít k přenosu dat z [úložiště HDFS](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) nebo z disků pomocí [protokolu SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [systému souborů NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [architektury REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) nebo [služby kopírování dat](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) do Data Boxu.

Existují také [partnerská řešení třetích stran](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), která používají Azure Data Box k migraci typu „Seed and Feed“, kdy se k přesunu velkých objemů dat používají offline přenosy, ale později se v menším měřítku provádí synchronizace po síti.

![Offline a online přenos dat pomocí služby Azure Data Box](../../_images/migrate/databox.png)

## <a name="assess-process-changes"></a>Vyhodnocení změn procesu

I když u jedné nebo více úloh požadavky na úložiště překračují kapacitu sítě, přesto můžete použít Azure Data Box k offline přenosu dat.

Síťový přenos je doporučený přístup, pokud síť není k dispozici. Rychlost přenosu dat v síti, i když je šířka pásma omezená, je obvykle rychlejší než fyzicky dodávat stejný objem dat pomocí mechanismu přenosu offline, například Data Box.

Pokud je k dispozici připojení k Azure, měli byste před použitím Data Boxu provést analýzu. Platí to hlavně tehdy, pokud máte na migraci úlohy omezený čas. Data Box se doporučuje jen tehdy, když čas na přenos potřebných dat přesahuje čas potřebný k naplnění, doručení a obnovení dat prostřednictvím Data Boxu.

### <a name="suggested-action-during-the-assess-process"></a>Navrhovaná akce během procesu vyhodnocení

**Analýza kapacity sítě:** Pokud jsou požadavky na přenos dat související s úlohou ohroženy překročením kapacity sítě, tým pro přijetí do cloudu přidá další úlohu analýzy do procesu vyhodnocení s názvem Analýza kapacity sítě. Při této analýze odhadne člen týmu, který má praktické zkušenosti s místní sítí a síťovým připojením, velikost dostupné síťové kapacity a požadovanou dobu přenosu dat. Dostupnou kapacitu pak porovná s požadavky na úložiště pro všechny prostředky migrované během aktuálního vydání verze. Pokud požadavky na úložiště přesahují dostupnou šířku pásma, měly by být prostředky, které podporují úlohu, vybrány k offline přenosu.

> [!IMPORTANT]
> V závěru analýzy bude pravděpodobně potřeba aktualizovat plán vydání verzí, aby odpovídal době potřebné k doručení, obnovení a synchronizaci prostředků přenášených offline.

**Analýza posunu:** Každý prostředek, který se má převést do režimu offline, by se měl analyzovat za úložiště a posun konfigurace. Posun úložiště představuje velikost změny příslušného úložiště v čase. Posun konfigurace představuje změnu konfigurace prostředku v čase. Od okamžiku zkopírování úložiště až do okamžiku předání prostředku do ostrého provozu může dojít ke ztrátě některého posunu. Pokud je potřeba tento posun u migrovaného prostředku zohlednit, je potřeba použít u místního a migrovaného prostředku některý způsob synchronizace. Tuto skutečnost je potřeba zvážit při provádění migrace.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Pokud používáte offline přenosové mechanismy, nebudou [replikační procesy](../migration-considerations/migrate/replicate.md) pravděpodobně potřeba. Přesto můžou být stále potřeba [synchronizační procesy](../migration-considerations/migrate/replicate.md). Když pochopíte výsledky analýzy posunu, prováděné během procesu vyhodnocení, získáte informace o úkolech, které jsou potřeba při migraci, pokud přenos prostředku probíhá offline.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhovaná akce během procesu migrace

**Kopírování úložiště:** Tento přístup se dá použít k přenosu dat HDFS, zálohování, archivů, souborových serverů, aplikací atd... Stávající technické pokyny vysvětlují, jak tento přístup použít k přenosu dat z [úložiště HDFS](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) nebo z disků pomocí [protokolu SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [systému souborů NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [architektury REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) nebo [služby kopírování dat](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) do Data Boxu.

Existují také [partnerská řešení třetích stran](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), která používají Azure Data Box k migraci typu „Seed and Feed“, kdy se k přesunu velkého objemu dat používá offline přenos, ale později se v menším měřítku provádí synchronizace po síti.

Dodejte **zařízení:** Po zkopírování dat je možné zařízení odeslat [společnosti Microsoft](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up). Jakmile data obdržíme a naimportujeme, budou k dispozici v účtu úložiště Azure.

**Obnovení assetu:** [Ověřte, že jsou data](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) dostupná v účtu úložiště. Ověřená data můžete používat jako objekt blob nebo v Azure Files. Pokud data představují soubor VHD/VHDX, můžete ho převést na spravované disky. Tyto spravované disky můžete použít k vytvoření instance virtuálního počítače, a vytvořit tak repliku původního místního prostředku.

**Synchronizace:** Pokud je synchronizace posunu požadavkem na migrovaných assetů, můžete k synchronizaci souborů použít jedno z [partnerských řešení jiných výrobců](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) , než se Asset obnoví.

## <a name="optimize-and-promote-process-changes"></a>Optimalizace a propagace změn procesů

Činnosti týkající se optimalizace pravděpodobně nebudou touto změnou dotčeny.

## <a name="secure-and-manage-process-changes"></a>Změny procesu zabezpečení a správy

Činnosti týkající se zabezpečení a správy pravděpodobně nebudou touto změnou dotčeny.

## <a name="next-steps"></a>Další kroky

Vraťte se ke [kontrolnímu seznamu pro rozšířený rozsah](./index.md) a ověřte si, že vaše metoda migrace plně vyhovuje.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
