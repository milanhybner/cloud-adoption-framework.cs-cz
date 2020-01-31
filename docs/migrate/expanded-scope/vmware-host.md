---
title: Urychlení migrace pomocí hostitelů VMware
description: Urychlení migrace pomocí hostitelů VMware
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 77d75127a497778056634f8a84a9021fa874a726
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802918"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Urychlení migrace pomocí hostitelů VMware

Migrace celého hostitele VMware může přesouvat více úloh a několik prostředků v rámci jedné migrace. Následující pokyny rozšiřují rozsah [příručky migrace do Azure](../azure-migration-guide/index.md) prostřednictvím migrace hostitele VMware. Většina úsilí požadovaná v tomto rozsahu rozšíření probíhá během navýšení požadavků a procesů migrace v rámci úsilí.

## <a name="suggested-prerequisites"></a>Doporučené požadavky

Při migraci prvního hostitele VMware do Azure musíte splnit několik požadavků na přípravu požadavků na identitu, síť a správu. Po splnění těchto požadavků by měl každý další hostitel vyžadovat, aby migrace významně nemusela být větší. Následující části obsahují další podrobnosti o požadavcích.

### <a name="secure-your-azure-environment"></a>Zabezpečení prostředí Azure

Implementujte příslušné cloudové řešení pro řízení přístupu na základě role a připojení k síti v prostředí Azure. [Průvodce zabezpečením prostředí](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) může s touto implementací pomáhat.

### <a name="private-cloud-management"></a>Správa privátního cloudu

Pro vytvoření správy privátního cloudu jsou k dispozici dvě požadované úlohy a jedna nepovinná úloha. Pro [zvýšení oprávnění privátního cloudu](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) a [nastavení služby DNS a DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) se vyžadují osvědčené postupy.

Pokud je cílem [migrovat úlohy pomocí roztažené sítě vrstvy 2](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), vyžaduje se i tento třetí osvědčený postup.

### <a name="private-cloud-networking"></a>Sítě privátního cloudu

Po navázání požadavků na správu můžete vytvořit privátní cloud sítě pomocí následujících osvědčených postupů:

- [Připojení VPN k privátnímu cloudu](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Připojení k místní síti pomocí ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Připojení k virtuální síti Azure pomocí ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurace překladu názvů DNS](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrace s plánem přijetí do cloudu

Až splníte ostatní požadavky, měli byste zahrnout každého hostitele VMware do [plánu přijetí do cloudu](../../plan/template.md). V rámci plánu přijetí do cloudu přidejte každého hostitele, který se má migrovat, jako [samostatnou úlohu](../../plan/workloads.md). V rámci každé úlohy přidejte virtuální počítače, které se mají migrovat jako [prostředky](../../plan/workloads.md). Chcete-li přidat úlohy a prostředky do plánu přijetí hromadně, přečtěte si téma [Přidání a úprava pracovních položek v aplikaci Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Změny procesu migrace

Během každé iterace tým přijetí prostřednictvím nevyřízených položek provede migraci úloh s nejvyšší prioritou. Proces se ve skutečnosti nemění pro hostitele VMware. Pokud je další úlohou backlogu hostitel VMware, použije se tento nástroj jenom změna.

V úsilí migrace můžete použít následující nástroje:

- [Nativní nástroje VMware](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Další možností je migrovat úlohy pomocí převzetí služeb při selhání pro zotavení po havárii pomocí následujících nástrojů:

- [Zálohování virtuálních počítačů s úlohou](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurace privátního cloudu jako lokality pro zotavení po havárii pomocí Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurace privátního cloudu jako lokality pro obnovení po havárii pomocí VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Další kroky

Vraťte se do kontrolního seznamu rozbaleného oboru a ujistěte se, že je vaše metoda migrace plně zarovnaná.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
