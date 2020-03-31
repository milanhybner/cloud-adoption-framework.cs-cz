---
title: Osvědčené postupy pro připravenost pro Azure
description: Seznamte se s osvědčenými postupy a dalšími pokyny, které vašemu týmu pomohou vytvořit a připravit prostředí Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 9d14209da7c18a2ba8279977e3c860a3dd1d0589
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433960"
---
# <a name="best-practices-for-azure-readiness"></a>Osvědčené postupy pro připravenost pro Azure

Připravenost pro cloud vyžaduje zajištění technických dovedností, které personál potřebuje k zahájení úsilí o přechod na cloud a k přípravě cílového prostředí migrace na aktiva a úlohy, které se budou přesouvat do cloudu. Přečtěte si tyto osvědčené postupy a další pokyny, které vašemu týmu pomohou připravit prostředí Azure.

## <a name="azure-fundamentals"></a>Základy Azure

Uspořádejte a nasaďte vaše aktiva v prostředí Azure.

- [Základní koncepty Azure.](../considerations/fundamental-concepts.md) Seznamte se s klíčovými pojmy a koncepcemi Azure a jejich vzájemnými souvislostmi.
- [Vytvoření počátečních předplatných](./initial-subscriptions.md) Vytvořte počáteční sadu předplatných Azure pro zahájení přechodu na cloud.
- [Škálování prostředí Azure pomocí několika předplatných](../azure-best-practices/scale-subscriptions.md). Seznamte se s důvody a strategiemi pro vytváření dalších předplatných pro škálování prostředí Azure.
- [Uspořádání prostředků s využitím skupin pro správu Azure.](../azure-best-practices/organize-subscriptions.md) Zjistíte, jak skupiny pro správu spravují prostředky, role, zásady a nasazení napříč několika předplatnými.
- [Využijte doporučené konvence pro tvorbu názvů a značek](../azure-best-practices/naming-and-tagging.md). Projděte si podrobná doporučení k vytváření názvů a označování prostředků. Tato doporučení podporují úsilí o přechod na podnikový cloud.
- [Vytvoření konzistentního hybridního cloudu.](../considerations/hybrid-consistency.md) Budete mít možnost vytvořit hybridní cloudová řešení, která poskytují výhody cloudových inovací a současně si zachovávají řadu výhod správy v místním prostředí.

## <a name="networking"></a>Sítě

Připravte síťovou infrastrukturu cloudu pro podporu vašich úloh.

- [Rozhodnutí o síti.](../considerations/networking-options.md) Můžete si zvolit síťové služby, nástroje a architektury, které podporují požadavky vaší organizace na možnosti připojení, zásady správného řízení a úlohy.
- [Plánování virtuálních sítí.](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Naplánujte virtuální sítě na základě vašich požadavků na umístění, izolaci a možnosti připojení.
- [Osvědčené postupy zabezpečení sítě.](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Přečtete si osvědčené postupy pro řešení běžných problémů se zabezpečením sítě pomocí integrovaných možností Azure.
- [Hraniční sítě.](./perimeter-networks.md) Umožněte zabezpečené připojení mezi cloudovými sítěmi a vašimi místními sítěmi nebo fyzickými sítěmi datacentra, spolu s internetovým připojením.
- [Hvězdicová síťová topologie.](./hub-spoke-network-topology.md) Efektivně spravujte běžné komunikační a bezpečnostní požadavky pro složité úlohy a vyřešte potenciální omezení předplatných Azure.

## <a name="identity-and-access-control"></a>Identita a řízení přístupu

Navrhněte infrastrukturu identit a řízení přístupu tak, abyste vylepšili efektivitu správy a zabezpečení vašich úloh.

- [Osvědčené postupy správy identit a zabezpečení řízení přístupu v Azure.](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Seznámíte se s osvědčenými postupy pro správu identit a řízení přístupu s využitím integrovaných funkcí Azure.
- [Osvědčené postupy pro řízení přístupu na základě role.](../considerations/roles.md) Zajistěte jemně odstupňovanou správu přístupu na základě skupin pro prostředky uspořádané podle uživatelských rolí.
- [Zabezpečení privilegovaného přístupu pro hybridní a cloudová nasazení v Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Zajistěte zabezpečení přístupů pro správu a privilegovaných účtů ve vaší organizaci, a to napříč cloudovým i místním prostředím.

## <a name="storage"></a>Storage

- [Pokyny k Azure Storage.](../considerations/storage-options.md) Vyberte si nejvhodnější řešení Azure Storage pro podporu vašich scénářů použití.
- [Průvodce zabezpečením Azure Storage.](https://docs.microsoft.com/azure/storage/blobs/security-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Další informace o funkcích zabezpečení ve službě Azure Storage

## <a name="databases"></a>Databáze

- [Výběr správné varianty SQL Serveru v Azure.](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Zvolíte si řešení PaaS nebo IaaS, které nejlépe vyhovuje vašim úlohám SQL Serveru.
- [Osvědčené postupy zabezpečení databází.](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Seznámíte se s osvědčenými postupy pro zabezpečení databází na platformě Azure.
- [Zvolíte si vhodné úložiště dat](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Vyberte nejvhodnější úložiště dat pro splnění vašich požadavků. V rámci databází SQL a NoSQL jsou k dispozici stovky možností implementace. Úložiště dat se často kategorizují podle způsobu strukturování dat a podporovaných typů operací. Tento článek popisuje několik běžných modelů úložiště.

## <a name="cost-management"></a>Správa nákladů

- [Sledování nákladů napříč organizačními jednotkami, prostředími a projekty.](./track-costs.md) Seznámíte se s osvědčenými postupy pro vytváření vhodných mechanismů sledování nákladů.
- [Využití investice do cloudu na maximum se službou Azure Cost Management.](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Využijte možnost implementovat strategii pro správu nákladů a seznámit se s nástroji, které jsou k dispozici pro řešení problematiky nákladů.
- [Vytváření a správa rozpočtů.](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Naučíte se vytvářet a spravovat rozpočty s využitím služby Azure Cost Management.
- [Export dat nákladů.](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Naučíte se exportovat informace o nákladech pomocí Azure Cost Managementu.
- [Optimalizace nákladů na základě doporučení.](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Získáte další informace o zjišťování nedostatečně využívaných prostředků a snižování nákladů, a to s využitím služeb Azure Cost Management a Azure Advisor.
- [Použití upozornění na náklady ke sledování využití a výdajů.](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Naučíte se využívat upozornění služby Cost Management k monitorování útraty a využití Azure.
