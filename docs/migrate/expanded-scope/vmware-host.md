---
title: Urychlení migrace pomocí hostitelů VMWare
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Urychlení migrace pomocí hostitelů VMWare
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b09c1dcbb36e5f630ca0ae86c95c5c874e29d60b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558204"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Urychlení migrace pomocí hostitelů VMWare

Migrace celého hostitele VMWare může přesouvat více úloh a několik prostředků v rámci jedné migrace. Následující pokyny rozšiřují rozsah [příručky migrace do Azure](../azure-migration-guide/index.md) prostřednictvím migrace hostitele VMware.

## <a name="general-scope-expansion"></a>Obecné rozšíření rozsahu

Většina tohoto úsilí požadovaná v tomto rozsahu rozšíření proběhne během procesu migrace požadavků a migrace.

## <a name="suggested-prerequisites"></a>Doporučené požadavky

Při migraci prvního hostitele VMWare do Azure je potřeba splnit několik požadavků, aby bylo možné připravit požadavky na identitu, síť a správu. Po splnění těchto požadavků by měl každý další hostitel vyžadovat, aby migrace významně nemusela být větší. Tyto požadavky se vztahují na několik klíčových snah: zabezpečení prostředí Azure, správy privátního cloudu a sítě privátního cloudu.

### <a name="secure-your-azure-environment"></a>Zabezpečení prostředí Azure

Implementujte vhodné cloudové řešení pro RBAC a připojení k síti v prostředí Azure. [Průvodce zabezpečením prostředí](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) může s touto implementací pomáhat.

### <a name="private-cloud-management"></a>Správa privátního cloudu

Pro vytvoření správy privátního cloudu jsou k dispozici dvě požadované úlohy a jedna nepovinná úloha. Pro [zvýšení oprávnění privátního cloudu](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) a [nastavení služby DNS a DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) se vyžadují osvědčené postupy.

Pokud cílem je [migrovat úlohy pomocí roztažené sítě vrstvy 2](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), bude se vyžadovat tento třetí osvědčený postup.

### <a name="private-cloud-networking"></a>Sítě privátního cloudu

Po zřízení požadavků na správu je možné vytvořit privátní cloud sítě pomocí následujících osvědčených postupů:

- [Připojení VPN k privátnímu cloudu](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Připojení k místní síti pomocí ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Připojení k virtuální síti Azure pomocí ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurace překladu názvů DNS](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrace s plánem přijetí do cloudu

Po splnění požadavků budou všichni hostitelé VMWare zahrnutí do [plánu přijetí do cloudu](../../plan/template.md). V rámci plánu přijetí do cloudu přidejte každého hostitele, který se má migrovat, jako [samostatnou úlohu](../../plan/workloads.md). V rámci každé úlohy je možné virtuální počítače, které se mají migrovat, přidat jako [prostředky](../../plan/workloads.md). Chcete-li hromadně přidávat úlohy a prostředky do plánu přijetí, přečtěte si téma [Přidání a úprava pracovních položek v aplikaci Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Změny procesu migrace

Během každé iterace tým přijetí prostřednictvím nevyřízených položek provede migraci úloh s nejvyšší prioritou. Proces se ve skutečnosti nemění pro hostitele VMWare. Pokud je další úlohou backlogu hostitel VMWare, použije se tento nástroj jenom změna.

### <a name="suggested-action-during-the-migrate-process"></a>Navrhovaná akce během procesu migrace

Následuje několik příkladů nástrojů, které je možné použít při migraci:

- [Nativní nástroje VMWare](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Úlohy můžete také migrovat pomocí převzetí služeb při selhání pro zotavení po havárii pomocí následujících nástrojů:

- [Zálohování virtuálních počítačů s úlohou](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurace privátního cloudu jako lokality pro zotavení po havárii pomocí Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurace privátního cloudu jako lokality pro obnovení po havárii pomocí VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Další kroky

Vraťte se na [kontrolní seznam pro rozšířený rozsah](./index.md) a zkontrolujte, jestli je vaše metoda migrace plně v souladu.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
