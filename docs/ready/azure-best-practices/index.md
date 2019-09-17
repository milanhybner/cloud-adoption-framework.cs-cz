---
title: Osvědčené postupy pro připravenost pro Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod k osvědčeným postupům pro připravenost pro Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: f1d4423e230d2eeff524a864f163e0cb13dc065b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818263"
---
# <a name="best-practices-for-azure-readiness"></a>Osvědčené postupy pro připravenost pro Azure

Velkou část zajištění připravenosti pro cloud tvoří zajištění technických dovedností, které personál potřebuje k zahájení úsilí o přechod na cloud a k přípravě cílového prostředí migrace na aktiva a úlohy, které se budou přesouvat do cloudu. Následující témata obsahují osvědčené postupy a další pokyny, které vašemu týmu pomohou vytvořit a připravit prostředí Azure.

## <a name="azure-fundamentals"></a>Základy Azure

Následující pokyny použijte pro uspořádání a nasazení vašich aktiv v prostředí Azure:

- [Základní koncepty Azure.](../considerations/fundamental-concepts.md) Seznámíte se se základními koncepty a termíny používanými v Azure. Dozvíte se také, jak tyto koncepty vzájemně souvisejí.
- [Doporučené zásady označování a vytváření názvů.](../considerations/name-and-tag.md) Projděte si podrobná doporučení k vytváření názvů a označování prostředků. Tato doporučení podporují úsilí o přechod na podnikový cloud.
- [Škálování s využitím několika předplatných Azure.](../considerations/scaling-subscriptions.md) Seznámíte se se strategiemi pro škálování s využitím několika předplatných Azure.
- [Uspořádání prostředků s využitím skupin pro správu Azure.](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Zjistíte, jak skupiny pro správu spravují prostředky, role, zásady a nasazení napříč několika předplatnými.
- [Vytvoření konzistentního hybridního cloudu.](../../infrastructure/misc/hybrid-consistency.md) Budete mít možnost vytvořit hybridní cloudová řešení, která poskytují výhody cloudových inovací a současně si zachovávají řadu výhod správy v místním prostředí.

## <a name="networking"></a>Sítě

Následující pokyny vám umožní připravit síťovou infrastrukturu cloudu pro podporu vašich úloh.

- [Rozhodnutí o síti.](../considerations/network-decisions.md) Můžete si zvolit síťové služby, nástroje a architektury, které podporují požadavky vaší organizace na možnosti připojení, zásady správného řízení a úlohy.
- [Plánování virtuálních sítí.](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Naučíte se plánovat virtuální sítě na základě vašich požadavků na umístění, izolaci a možnosti připojení.
- [Osvědčené postupy zabezpečení sítě.](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Přečtete si osvědčené postupy pro řešení běžných problémů se zabezpečením sítě pomocí integrovaných možností Azure.
- [Hraniční sítě.](./perimeter-networks.md) Hraniční sítě, označované také jako demilitarizované zóny (DMZ), umožňují zabezpečené připojení mezi cloudovými sítěmi a vašimi místními sítěmi nebo fyzickými sítěmi datacentra, spolu s internetovým připojením.
- [Hvězdicová síťová topologie.](./hub-spoke-network-topology.md) Hvězdicová architektura je síťový model pro efektivní správu běžných požadavků na zabezpečení nebo komunikaci pro složité úlohy. Současně řeší potenciální omezení předplatných Azure.

## <a name="identity-and-access-control"></a>Identita a řízení přístupu

Následující pokyny vám při návrhu infrastruktury identit a řízení přístupu pomohou vylepšit efektivitu správy a zabezpečení vašich úloh:

- [Osvědčené postupy správy identit a zabezpečení řízení přístupu v Azure.](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Seznámíte se s osvědčenými postupy pro správu identit a řízení přístupu s využitím integrovaných funkcí Azure.
- [Osvědčené postupy pro řízení přístupu na základě role.](./roles.md) Řízení přístupu na základě role (RBAC) v Azure nabízí jemně odstupňovanou správu přístupu na základě skupin pro prostředky uspořádané podle uživatelských rolí.
- [Zabezpečení privilegovaného přístupu pro hybridní a cloudová nasazení v Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Azure Active Directory vám pomůže zajistit zabezpečení účtů správce a přístupů pro správu ve vaší organizaci, a to napříč cloudovým i místním prostředím.

## <a name="storage"></a>Storage

- [Pokyny k Azure Storage.](../considerations/storage-guidance.md) Vyberte si nejvhodnější řešení Azure Storage pro podporu vašich scénářů použití.
- [Průvodce zabezpečením Azure Storage.](https://docs.microsoft.com/azure/storage/common/storage-security-guide?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Další informace o funkcích zabezpečení ve službě Azure Storage

## <a name="databases"></a>Databáze

- [Výběr správné varianty SQL Serveru v Azure.](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Zvolíte si řešení PaaS nebo IaaS, které nejlépe vyhovuje vašim úlohám SQL Serveru.
- [Osvědčené postupy zabezpečení databází.](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Seznámíte se s osvědčenými postupy pro zabezpečení databází na platformě Azure.
- [Zvolíte si vhodné úložiště dat](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Výběr správného úložiště dat odpovídajícího konkrétním požadavkům je klíčovým rozhodnutím při návrhu řešení. U databází SQL i NoSQL existují doslova stovky možností implementace, z nichž můžete vybírat. Úložiště dat se často kategorizují podle způsobu strukturování dat a podporovaných typů operací. Tento článek popisuje některé z nejběžnějších modelů úložiště.

## <a name="cost-management"></a>Správa nákladů

- [Sledování nákladů napříč organizačními jednotkami, prostředími a projekty.](./track-costs.md) Seznámíte se s osvědčenými postupy pro vytváření vhodných mechanismů sledování nákladů.
- [Využití investice do cloudu na maximum se službou Azure Cost Management.](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Využijte možnost implementovat strategii pro správu nákladů a seznámit se s nástroji, které jsou k dispozici pro řešení problematiky nákladů.
- [Vytváření a správa rozpočtů.](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Naučíte se vytvářet a spravovat rozpočty s využitím služby Azure Cost Management.
- [Export dat nákladů.](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Naučíte se vytvářet a spravovat exportovaná data ve službě Azure Cost Management.
- [Optimalizace nákladů na základě doporučení.](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Získáte další informace o zjišťování nedostatečně využívaných prostředků a zjistíte, co dělat ke snížení nákladů, a to s využitím služeb Azure Cost Management a Azure Advisor.
- [Použití upozornění na náklady ke sledování využití a výdajů.](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Naučíte se využívat upozornění služby Cost Management k monitorování útraty a využití Azure.
