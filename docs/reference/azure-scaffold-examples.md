---
title: Scénáře a příklady zásad správného řízení předplatného
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: V této části najdete příklady implementace zásad správného řízení předplatných Azure pro běžné scénáře.
author: rdendtler
ms.author: rodend
ms.date: 01/03/2017
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: 3cc5071ca4b57473b52e0478e59b3c6a0dd49bea
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058056"
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Příklady implementace uživatelského rozhraní Azure Enterprise

> [!NOTE]
> Prostředí Azure Enterprise vygenerovaná v rámci rozhraní Microsoft Cloud pro přijetí bylo integrováno. Obsah tohoto článku je nyní reprezentován v oddílu [připraveném](../ready/index.md) v novém rozhraní. Tento článek bude v brzké 2020 zastaralý. Pokud chcete začít používat nový proces, přečtěte si téma [připravený přehled](../ready/index.md), [Vytvoření první cílové zóny](../ready/azure-setup-guide/migration-landing-zone.md)a [informace o cílové zóně](../ready/considerations/index.md).

Tento článek popisuje příklady, jak může podnik implementovat doporučení pro [generování uživatelského rozhraní Azure Enterprise](./azure-scaffold.md). Používá fiktivní společnost s názvem contoso k ilustraci osvědčených postupů pro běžné scénáře.

## <a name="background"></a>Pozadí

Contoso je celosvětová společnost, která zákazníkům poskytuje řešení pro poskytování dodavatelských řetězců. Poskytují vše od softwaru jako model služby do zabaleného modelu nasazeného místně. Vyvíjí software po celém světě s významnými vývojovými centry v Indii, USA a Kanadě.

Část ISV společnosti je rozdělená na několik nezávislých obchodních jednotek, které spravují produkty ve významné firmě. Každá obchodní jednotka má své vlastní vývojáře, produktové manažery a architekty.

Obchodní jednotka ETS (Enterprise Technology Services) poskytuje centralizovanou funkci IT a spravuje několik datových center, kde obchodní jednotky hostují své aplikace. Společně se správou Datacenter ETS organizace poskytuje a spravuje centralizovanou spolupráci (jako je e-mail a websites) a síťové a telefonní služby. Spravují taky úlohy pro zákazníky pro menší obchodní jednotky, které nemají provozní pracovníky.

V tomto článku se používají následující osoby:

- Dave je ETS správce Azure.
- Alice je ředitelem vývoje společnosti Contoso v obchodní jednotce dodavatelského řetězce.

Contoso potřebuje vytvořit obchodní aplikaci a zákaznickou aplikaci. Rozhodla se spouštět aplikace v Azure. Dave přečte článek [zásad správného řízení předplatného](./azure-scaffold.md) a je připravený k implementaci doporučení.

## <a name="scenario-1-line-of-business-application"></a>Scénář 1: obchodní aplikace

Společnost Contoso vytváří systém správy zdrojového kódu (BitBucket), který budou používat vývojáři po celém světě. Aplikace používá infrastrukturu jako službu (IaaS) pro hostování a skládá se z webových serverů a databázového serveru. Vývojáři přistupují k serverům ve vývojových prostředích, ale nepotřebují přístup k serverům v Azure. Contoso ETS chce vlastníkovi aplikace a týmu dovolit, aby aplikaci spravoval. Aplikace je k dispozici pouze v podnikové síti společnosti Contoso. Dave musí nastavit odběr pro tuto aplikaci. Předplatné bude v budoucnu taky hostovat další software související s vývojářem.

### <a name="naming-standards-and-resource-groups"></a>Standardy pojmenování a skupiny prostředků

Dave vytvoří předplatné pro podporu vývojářských nástrojů, které jsou společné napříč všemi obchodními jednotkami. Dave musí vytvořit smysluplné názvy pro předplatné a skupiny prostředků (pro aplikaci a sítě). Vytvoří následující předplatné a skupiny prostředků:

| Položka | Name (Název) | Popis |
| --- | --- | --- |
| Předplatné |Contoso ETS DeveloperTools – výroba |Podporuje běžné vývojářské nástroje |
| Skupina prostředků |Bitbucket-prod-RG |Obsahuje aplikační webový server a databázový server. |
| Skupina prostředků |corenetworks-prod-RG |Obsahuje virtuální sítě a připojení brány mezi lokalitami. |

### <a name="role-based-access-control"></a>Řízení přístupu založené na rolích

Po vytvoření předplatného Dave chce zajistit, aby příslušné týmy a vlastníci aplikací měli přístup k jejich prostředkům. Dave rozpozná, že každý tým má jiné požadavky. Pomocí skupin synchronizovaných z místní služby Active Directory společnosti Contoso Azure Active Directory a poskytuje správnou úroveň přístupu k týmům.

Dave přiřazuje pro předplatné následující role:

| Role | Přiřazeno | Popis |
| --- | --- | --- |
| [Vlastník](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) |Spravované ID z místní služby Active Directory společnosti Contoso |Toto ID se řídí přístupem JIT (just-in-time) prostřednictvím nástroje pro správu identit společnosti Contoso a zajišťuje, aby byl přístup k vlastníkům předplatného plně auditován. |
| [Čtecí modul zabezpečení](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader) |Oddělení správy zabezpečení a rizik |Tato role umožňuje uživatelům podívat se na Azure Security Center a stav prostředků. |
| [Přispěvatel sítě](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#network-contributor) |Síťový tým |Tato role umožňuje síťovému týmu společnosti Contoso spravovat lokalitu na síť VPN a virtuální sítě. |
| *Vlastní role* |Vlastník aplikace |Dave vytvoří roli, která uděluje možnost upravovat prostředky v rámci skupiny prostředků. Další informace najdete v tématu [vlastní role v Azure RBAC](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) . |

### <a name="policies"></a>Zásady

Dave má následující požadavky na správu prostředků v rámci předplatného:

- Vzhledem k tomu, že vývojové nástroje podporují vývojáře po celém světě, nechce uživatelům zablokovat vytváření prostředků v jakékoli oblasti. Potřebuje ale informace o tom, kde jsou prostředky vytvořené.
- Má na starosti náklady. Proto chce vlastníkům aplikací zabránit v vytváření zbytečně náročných virtuálních počítačů.
- Vzhledem k tomu, že tato aplikace slouží vývojářům v mnoha obchodních jednotkách, chce označit každý prostředek pomocí obchodní jednotky a vlastníka aplikace. Pomocí těchto značek může ETS fakturovat příslušné týmy.

Pomocí [Azure Policy](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction)vytvoří následující zásady:

| Pole | Efekt | Popis |
| --- | --- | --- |
| location |ověřen |Audit vytváření prostředků v libovolné oblasti |
| type |odmítnout |Odepřít vytváření virtuálních počítačů řady G-series |
| tags |odmítnout |Vyžadovat značku vlastníka aplikace |
| tags |odmítnout |Vyžadovat značku nákladového střediska |
| tags |příloh |Připojí název značky **BusinessUnit** a hodnotu značky **ETS** všem prostředkům. |

### <a name="resource-tags"></a>Značky prostředků

Dave chápe, že musí mít konkrétní informace o fakturaci k identifikaci nákladového centra pro implementaci BitBucket. Kromě toho Dave chce znát všechny prostředky, které ETS vlastní.

Přidá následující [značky](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) do skupin prostředků a prostředků.

| Název značky | Hodnota značky |
| --- | --- |
| ApplicationOwner |Jméno osoby, která spravuje tuto aplikaci |
| CostCenter |Nákladové středisko skupiny placené za využití Azure |
| BusinessUnit |**ETS** (obchodní jednotka přidružená k předplatnému) |

### <a name="core-network"></a>Základní síť

Tým společnosti Contoso ETS Information Security and rizik Management kontroluje navrhovaný plán pro přesun aplikace do Azure. Chtějí zajistit, aby aplikace nebyla dostupná pro Internet. Dave má také vývojářské aplikace, které v budoucnu budou přesunuty do Azure. Tyto aplikace vyžadují veřejná rozhraní. Aby bylo možné tyto požadavky splnit, poskytuje interní i externí virtuální sítě a skupinu zabezpečení sítě k omezení přístupu.

Vytvoří následující prostředky:

| Typ prostředku | Name (Název) | Popis |
| --- | --- | --- |
| Virtual Network |Interní virtuální síť |Používá se s aplikací BitBucket a je připojená prostřednictvím ExpressRoute k podnikové síti společnosti Contoso. Podsíť (`bitbucket`) poskytuje aplikaci s konkrétním adresním prostorem IP adres. |
| Virtual Network |externí virtuální síť |K dispozici pro budoucí aplikace, které vyžadují veřejné koncové body |
| Skupina zabezpečení sítě |Bitbucket – NSG |Zajišťuje minimalizaci prostoru pro útok na tuto úlohu tím, že povoluje připojení pouze na portu 443 pro podsíť, ve které je aplikace umístěná (`bitbucket`). |

### <a name="resource-locks"></a>Zámky prostředků

Dave rozpozná, že připojení z podnikové sítě společnosti Contoso k interní virtuální síti musí být chráněné z jakéhokoli skriptu wayward nebo náhodného odstranění.

Vytvoří následující [Zámek prostředků](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources):

| Typ zámku | Prostředek | Popis |
| --- | --- | --- |
| **CanNotDelete** |Interní virtuální síť |Zabraňuje uživatelům odstranit virtuální síť nebo podsítě, ale nebrání přidání nových podsítí. |

### <a name="azure-automation"></a>Azure Automation

Dave nemá nic k automatizaci pro tuto aplikaci. I když vytvořil účet Azure Automation, nebude ho zpočátku používat.

### <a name="azure-security-center"></a>Centrum zabezpečení Azure

Společnost Contoso správa IT služeb potřebuje k rychlé identifikaci a manipulaci s hrozbami. Chtějí taky pochopit, jaké problémy možná existují.

Aby mohl Dave splnit tyto požadavky, umožňuje [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) a poskytuje přístup k roli čtenáře zabezpečení.

## <a name="scenario-2-customer-facing-app"></a>Scénář 2: aplikace směřující na zákazníka

Obchodní vedení v obchodní jednotce dodavatelských řetězců identifikoval různé příležitosti, aby se zvýšila produktivita se zákazníky společnosti Contoso pomocí věrnostní karty. Tým Alice musí vytvořit tuto aplikaci a rozhodne, že Azure zvýší svou schopnost uspokojit potřebu podniku. Alice spolupracuje s Dave z ETS ke konfiguraci dvou předplatných pro vývoj a provozování této aplikace.

### <a name="azure-subscriptions"></a>Předplatná Azure

Dave se do Azure Enterprise Portal a zjistí, že oddělení dodavatelských řetězců již existuje. Vzhledem k tomu, že tento projekt je prvním vývojovým projektem týmu dodavatelských řetězců v Azure, Dave rozpoznává nutnost nového účtu pro vývojového týmu Alice. Vytvoří účet "R & D" pro svůj tým a přiřadí přístup k Alici. Alice se přihlásí prostřednictvím Azure Portal a vytvoří dvě předplatná: jeden pro vývoj serverů a druhý pro uložení provozních serverů. Postupuje podle dříve vytvořených standardů pojmenování při vytváření následujících předplatných:

| Použití předplatného | Name (Název) |
| --- | --- |
| Vývoj |Contoso SupplyChain ResearchDevelopment LoyaltyCard Development |
| Výroba |Contoso SupplyChain Operations LoyaltyCard produkční prostředí |

<!-- markdownlint-disable MD024 -->

### <a name="policies"></a>Zásady

Dave a Alice projednají aplikaci a určí, že tato aplikace obsluhuje pouze zákazníky v oblasti Severní Ameriky. Alice a její tým plánuje použít Azure Application Service Environment a Azure SQL k vytvoření aplikace. Můžou být potřeba během vývoje vytvořit virtuální počítače. Alice chce zajistit, aby její vývojáři měli prostředky, které potřebují k prozkoumání a prozkoumání problémů bez navýšení ETS.

Pro **vývojové předplatné**vytvoří tyto zásady:

| Pole | Efekt | Popis |
| --- | --- | --- |
| location |ověřen |Audit vytváření prostředků v libovolné oblasti |

Neomezují typ SKU, který může uživatel vytvořit ve vývoji, a nevyžaduje značky pro žádné skupiny prostředků nebo prostředky.

Pro **produkční předplatné**vytvoří tyto zásady:

| Pole | Efekt | Popis |
| --- | --- | --- |
| location |odmítnout |Odepření vytváření jakýchkoli prostředků mimo datacentra USA |
| tags |odmítnout |Vyžadovat značku vlastníka aplikace |
| tags |odmítnout |Značka vyžadovat oddělení |
| tags |příloh |Připojit značku ke každé skupině prostředků, která označuje produkční prostředí |

Neomezují typ SKU, který uživatel může vytvořit v produkčním prostředí.

### <a name="resource-tags"></a>Značky prostředků

Dave rozumí, že musí mít konkrétní informace pro identifikaci správných obchodních skupin pro fakturaci a vlastnictví. Definuje značky prostředků pro skupiny prostředků a prostředky.

| Název značky | Hodnota značky |
| --- | --- |
| ApplicationOwner |Jméno osoby, která spravuje tuto aplikaci |
| Oddělení |Nákladové středisko skupiny placené za využití Azure |
| EnvironmentType |**Výroba** (i když předplatné zahrnuje **produkční** prostředí v názvu, včetně této značky umožňuje snadnou identifikaci při prohlížení prostředků na portálu nebo na faktuře) |

### <a name="core-networks"></a>Základní sítě

Tým společnosti Contoso ETS Information Security and rizik Management kontroluje navrhovaný plán pro přesun aplikace do Azure. Chtějí zajistit, aby byla aplikace věrnostní karty správně izolovaná a chráněná v DMZ síti. Aby bylo možné tento požadavek splnit, Dave a Alice vytvoří externí virtuální síť a skupinu zabezpečení sítě a izoluje aplikaci věrnostních karet od podnikové sítě contoso.

Pro **vývojové předplatné**vytvoří:

| Typ prostředku | Name (Název) | Popis |
| --- | --- | --- |
| Virtual Network |Interní virtuální síť |Slouží jako prostředí pro vývoj věrnostních karet společnosti Contoso a je připojené prostřednictvím ExpressRoute k podnikové síti společnosti Contoso. |

Pro **produkční předplatné**vytvoří:

| Typ prostředku | Name (Název) | Popis |
| --- | --- | --- |
| Virtual Network |externí virtuální síť |Hostuje aplikaci věrnostních karet a není přímo připojená k ExpressRoute společnosti Contoso. Kód je nabízen prostřednictvím svého systému zdrojového kódu přímo k PaaS službám. |
| Skupina zabezpečení sítě |loyaltycard – NSG |Zajišťuje minimalizaci prostoru pro útok na tuto úlohu tím, že povoluje pouze komunikaci v rámci vázané komunikace na portu TCP 443. Společnost Contoso také provádí šetření pomocí brány firewall webových aplikací pro další ochranu. |

### <a name="resource-locks"></a>Zámky prostředků

Dave a Alice se rozhodnou, že přidá zámky prostředků na některé klíčové prostředky v prostředí, aby se zabránilo nechtěnému odstranění během nabízení kódu errant.

Vytvoří následující zámek:

| Typ zámku | Prostředek | Popis |
| --- | --- | --- |
| **CanNotDelete** |externí virtuální síť |Aby uživatelé nemohli odstranit virtuální síť nebo podsítě. Zámek nebrání přidání nových podsítí. |

### <a name="azure-automation"></a>Azure Automation

Alice a její vývojový tým mají rozsáhlé Runbooky pro správu prostředí pro tuto aplikaci. Runbooky umožňují přidávání a odstraňování uzlů pro aplikaci a další DevOps úlohy.

Chcete-li použít tyto sady Runbook, povolte [automatizaci](https://docs.microsoft.com/azure/automation/automation-intro).

### <a name="azure-security-center"></a>Centrum zabezpečení Azure

Společnost Contoso správa IT služeb potřebuje k rychlé identifikaci a manipulaci s hrozbami. Chtějí taky pochopit, jaké problémy možná existují.

K splnění těchto požadavků Dave umožňuje Azure Security Center. Zajišťuje, že Azure Security Center sleduje prostředky a poskytuje přístup k týmům DevOps a zabezpečení.

## <a name="next-steps"></a>Další kroky

- Další informace o vytváření šablon Správce prostředků najdete v tématu [osvědčené postupy pro vytváření šablon Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).
