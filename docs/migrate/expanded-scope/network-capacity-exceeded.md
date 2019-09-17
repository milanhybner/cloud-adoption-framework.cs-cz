---
title: Překročení síťové kapacity
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Požadavky na úložiště překračují při migraci kapacitu sítě.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9b1078cbb6b7ca40b7a38ea56ae803fd61e67449
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024781"
---
# <a name="storage-requirements-exceed-network-capacity-during-a-migration-effort"></a>Požadavky na úložiště při migraci překračují kapacitu sítě

Při migraci do cloudu se prostředky replikují a synchronizují po síti mezi stávajícím datacentrem a cloudem. Není neobvyklé, že požadavky vyplývající z velikosti stávajících dat různých úloh překračují kapacitu sítě. V takových scénářích se může postup migrace výrazně zpomalit a v některých případech i úplně zastavit. Následující pokyny rozšiřují obsah [příručky k migraci do Azure](../azure-migration-guide/index.md) a nabízejí řešení, jak obejít omezení sítě.

## <a name="general-scope-expansion"></a>Obecné rozšíření rozsahu

Většina práce požadované v tomto rozšíření obsahu probíhá v rámci předběžných, vyhodnocovacích a migračních procesů.

## <a name="suggested-prerequisites"></a>Navrhované předpoklady

**Ověření rizik spojených s kapacitou sítě:** Důrazně se doporučuje [racionalizace digitálních aktiv](../../digital-estate/rationalize.md). Platí to zejména při obavách o přetížení dostupné kapacity sítě. Při racionalizaci digitálních aktiv se shromažďují podklady pro [inventarizaci digitálních prostředků](../../digital-estate/inventory.md). Tato inventarizace by měla zahrnovat požadavky na stávající úložiště digitálních aktiv. V materiálu o [replikačních rizicích: fyzická stránka replikací](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) se uvádí, že inventarizaci můžete použít k odhadu **celkové velikosti migrovaných dat**, kterou je možné porovnat s celkovou **šířkou pásma dostupnou pro migraci**. Pokud toto srovnání neodpovídá požadované **době na změnu firmy**, může vám tento článek pomoci zrychlit migraci tím, že zkrátí čas potřebný k migraci datacentra.

**Offline přenos nezávislých úložišť dat:** Na následujícím diagramu jsou příklady online a offline přenosů dat se službou Azure Data Box. Tyto postupy můžete použít k přenosu velkých objemů dat do cloudu ještě před migrací úloh. Při offline přenosu dat se zdrojová data zkopírují do služby Azure Data Box a následně se fyzicky přesunou do Microsoftu, který je přenese do účtu úložiště Azure jako soubor nebo objekt blob. Tento postup je možné použít před dalšími migračními úkoly k přesunu dat, která nejsou přímo spojena s určitou úlohou. Tímto způsobem snížíte množství dat, které je potřeba přesunout po síti, abyste mohli dokončit migraci i s omezeními sítě.

Tento přístup je možné použít k přenosu dat HDFS, záloh, archivů, souborových serverů, aplikací apod. Stávající technické pokyny vysvětlují, jak tento přístup použít k přenosu dat z [úložiště HDFS](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) nebo z disků pomocí [protokolu SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [systému souborů NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [architektury REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) nebo [služby kopírování dat](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) do Data Boxu.

Existují také [partnerská řešení třetích stran](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), která používají Azure Data Box k migraci typu „Seed and Feed“, kdy se k přesunu velkých objemů dat používají offline přenosy, ale později se v menším měřítku provádí synchronizace po síti.

![Offline a online přenos dat pomocí služby Azure Data Box](../../_images/migrate/databox.png)

## <a name="assess-process-changes"></a>Změny procesu posouzení

I když u jedné nebo více úloh požadavky na úložiště překračují kapacitu sítě, přesto můžete použít Azure Data Box k offline přenosu dat.

Microsoft se obecně přiklání k názoru, že doporučeným postupem je síťový přenos, samozřejmě pokud je síť k dispozici. Toto doporučení vychází z přenosových rychlostí. Přenos dat po síti (i při omezené šířce pásma) je většinou rychlejší než fyzické doručení stejného objemu dat s použitím offline přenosového mechanismu, jako je Data Box.

Pokud je k dispozici připojení k Azure, měli byste před použitím Data Boxu provést analýzu. Platí to hlavně tehdy, pokud máte na migraci úlohy omezený čas. Data Box se doporučuje jen tehdy, když čas na přenos potřebných dat přesahuje čas potřebný k naplnění, doručení a obnovení dat prostřednictvím Data Boxu.

### <a name="suggested-action-during-the-assess-process"></a>Doporučené akce během procesu vyhodnocení

**Analýza kapacity sítě:** Pokud požadavky na přenos dat úlohy znamenají riziko spočívající v překročení kapacity sítě, měl by tým, který se zabývá osvojením cloudu, přidat do procesu vyhodnocení další analytický úkol, který se nazývá analýza kapacity sítě. Při této analýze odhadne člen týmu, který má praktické zkušenosti s místní sítí a síťovým připojením, velikost dostupné síťové kapacity a požadovanou dobu přenosu dat. Dostupnou kapacitu pak porovná s požadavky na úložiště pro všechny prostředky migrované během aktuálního vydání verze. Pokud požadavky na úložiště přesahují dostupnou šířku pásma, měly by být prostředky, které podporují úlohu, vybrány k offline přenosu.

> [!IMPORTANT]
> V závěru analýzy bude pravděpodobně potřeba aktualizovat plán vydání verzí, aby odpovídal době potřebné k doručení, obnovení a synchronizaci prostředků přenášených offline.

**Analýza posunu:** Každý prostředek, který přenášíte offline, byste měli analyzovat z hlediska posunu úložiště a konfigurace. Posun úložiště představuje velikost změny příslušného úložiště v čase. Posun konfigurace představuje změnu konfigurace prostředku v čase. Od okamžiku zkopírování úložiště až do okamžiku předání prostředku do ostrého provozu může dojít ke ztrátě některého posunu. Pokud je potřeba tento posun u migrovaného prostředku zohlednit, je potřeba použít u místního a migrovaného prostředku některý způsob synchronizace. Tuto skutečnost je potřeba zvážit při provádění migrace.

## <a name="migrate-process-changes"></a>Změny procesu migrace

Pokud používáte offline přenosové mechanismy, nebudou [replikační procesy](../migration-considerations/migrate/replicate.md) pravděpodobně potřeba. Přesto můžou být stále potřeba [synchronizační procesy](../migration-considerations/migrate/replicate.md). Když pochopíte výsledky analýzy posunu, prováděné během procesu vyhodnocení, získáte informace o úkolech, které jsou potřeba při migraci, pokud přenos prostředku probíhá offline.

### <a name="suggested-action-during-the-migrate-process"></a>Doporučované akce během procesu migrace

**Kopírování úložiště:** Tento přístup je možné použít k přenosu dat HDFS, záloh, archivů, souborových serverů, aplikací apod. Stávající technické pokyny vysvětlují, jak tento přístup použít k přenosu dat z [úložiště HDFS](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) nebo z disků pomocí [protokolu SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [systému souborů NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [architektury REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) nebo [služby kopírování dat](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) do Data Boxu.

Existují také [partnerská řešení třetích stran](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), která používají Azure Data Box k migraci typu „Seed and Feed“, kdy se k přesunu velkého objemu dat používá offline přenos, ale později se v menším měřítku provádí synchronizace po síti.

**Odeslání zařízení:** Jakmile data zkopírujete, můžete zařízení [odeslat Microsoftu](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up). Jakmile data obdržíme a naimportujeme, budou k dispozici v účtu úložiště Azure.

**Obnovení prostředku:** [Ověřte, jestli jsou data](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) k dispozici v účtu úložiště. Ověřená data můžete používat jako objekt blob nebo v Azure Files. Pokud data představují soubor VHD/VHDX, můžete ho převést na spravované disky. Tyto spravované disky můžete použít k vytvoření instance virtuálního počítače, a vytvořit tak repliku původního místního prostředku.

**Synchronizace:** Pokud migrovaný prostředek vyžaduje synchronizaci posunu, můžete k synchronizaci souborů použít některé [externí partnerské řešení](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), dokud prostředek neobnovíte.

## <a name="optimize-and-promote-process-changes"></a>Procesní změny týkající se optimalizace a zvýšení úrovně

Činnosti týkající se optimalizace pravděpodobně nebudou touto změnou dotčeny.

## <a name="secure-and-manage-process-changes"></a>Procesní změny týkající se zabezpečení a správy

Činnosti týkající se zabezpečení a správy pravděpodobně nebudou touto změnou dotčeny.

## <a name="next-steps"></a>Další kroky

Vraťte se ke [kontrolnímu seznamu pro rozšířený rozsah](./index.md) a ověřte si, že vaše metoda migrace plně vyhovuje.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
