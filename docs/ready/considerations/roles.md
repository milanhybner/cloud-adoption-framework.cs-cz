---
title: Doporučené řízení přístupu na základě role
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Doporučené řízení přístupu na základě role
author: rotycenh
ms.author: brblanch
ms.date: 11/28/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: BrianBlanchard
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 6aa17f3ffb16afae0b27bcccbee84ddf9ad2c5f0
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73243133"
---
# <a name="role-based-access-control"></a>Řízení přístupu založené na rolích

Přístupová práva a oprávnění založená na skupině jsou osvědčeným postupem. Práce se skupinami namísto jednotlivých uživatelů zjednodušuje správu zásad přístupu, umožňuje jednotnou správu přístupu napříč týmy a snižuje riziko chyb při konfiguraci. Přiřazení uživatelů k příslušným skupinám a jejich odebírání pomáhá udržovat aktuální oprávnění konkrétního uživatele. [Řízení přístupu na základě role (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview) v Azure nabízí jemně odstupňovanou správu přístupu pro prostředky uspořádané podle uživatelských rolí.

Přehled osvědčených postupů RBAC v rámci strategie identity a zabezpečení najdete v tématu [Osvědčené postupy správy identit a zabezpečení řízení přístupu v Azure.](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices#use-role-based-access-control)

## <a name="overview-of-role-based-access-control"></a>Přehled správy řízení přístupu na základě role

Pomocí [řízení přístupu na základě role](https://docs.microsoft.com/azure/role-based-access-control/overview) můžete v rámci svého týmu oddělit povinnosti a udělit pouze takový přístup ke konkrétním uživatelům, skupinám, instančním objektům nebo spravovaným identitám služby Azure Active Directory (Azure AD), který postačuje k provádění potřebných úloh. Místo toho, abyste komukoli udělili neomezený přístup k předplatnému nebo prostředkům Azure, můžete omezit oprávnění pro jednotlivé sady prostředků.

[Definice rolí RBAC](https://docs.microsoft.com/azure/role-based-access-control/role-definitions) obsahuje seznam operací povolených nebo zakázaných pro uživatele nebo skupiny přiřazené k této roli. [Rozsah ](https://docs.microsoft.com/azure/role-based-access-control/overview#scope) role určuje, na které prostředky se tato definovaná oprávnění vztahují. Rozsahy můžou být zadány na více úrovních: skupina pro správu, předplatné, skupina prostředků nebo prostředek. Rozsahy jsou strukturovány ve vztahu nadřazený/podřízený rozsah.

![Hierarchie rozsahu RBAC](../../_images/azure-best-practices/rbac-scope.png)

Podrobné pokyny pro přiřazení uživatelů a skupin k určitým rolím a pro přiřazení rolí k rozsahům najdete v tématu popisujícím [správu přístupu k prostředkům Azure](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) pomocí RBAC.

Při plánování strategie řízení přístupu použijte model přístupu s minimálními oprávněními, který uživatelům uděluje pouze oprávnění potřebná k provedení jejich práce. Následující diagram zobrazuje tento navrhovaný způsob používání RBAC.

![Navrhovaný vzor pro používání RBAC](../../_images/azure-best-practices/rbac-least-privilege.png)

> [!NOTE]
> Čím konkrétnější nebo podrobnější oprávnění definujete, tím je pravděpodobnější, že řízení přístupu bude složité a obtížně spravovatelné. To platí hlavně v případě, že velikost vašich cloudových aktiv roste. Vyhněte se oprávněním pro konkrétní prostředky. Místo toho [použijte skupiny pro správu](https://docs.microsoft.com/azure/governance/management-groups) k řízení přístupu na podnikové úrovni a [skupiny prostředků](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) k řízení přístupu v rámci předplatných. Vyhněte se taky konkrétním uživatelským oprávněním. Místo toho přiřaďte přístup [ke skupinám v Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups).

## <a name="using-built-in-rbac-roles"></a>Použití předdefinovaných rolí RBAC

Azure poskytuje mnoho předdefinovaných definic rolí se třemi základními rolemi pro poskytnutí přístupu:

- Role [Vlastník](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) může spravovat všechno, včetně přístupu k prostředkům.
- Role [Přispěvatel](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) může spravovat všechno, kromě přístupu k prostředkům.
- Role [Čtenář](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader) může zobrazit vše, ale nemůže provádět žádné změny.

Mimo těchto základních úrovní přístupu jsou k dispozici další předdefinované role, které poskytují podrobnější možnosti řízení přístupu ke konkrétním typům prostředků nebo funkcím Azure. Můžete například spravovat přístup k virtuálním počítačům pomocí následujících předdefinovaných rolí:

- Role [Přihlášení správce virtuálního počítače](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-administrator-login) může zobrazovat virtuální počítače na portálu a přihlásit se jako _správce_ .
- Role [Přispěvatel virtuálních počítačů](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) může spravovat virtuální počítače, ale nemůže přistupovat ani k nim, ani k virtuální síti nebo účtu úložiště, ke kterým jsou připojené.
- Role [Přihlášení uživatele virtuálního počítače](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-user-login) může zobrazovat virtuální počítače na portálu a přihlásit se jako běžný uživatel.

Další příklad použití předdefinovaných rolí ke správě přístupu k určitým funkcím najdete v informacích o řízení přístupu k funkcím pro sledování nákladů v tématu [Sledování nákladů napříč organizačními jednotkami, prostředími a projekty](../azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access).

Úplný seznam dostupných předdefinovaných rolí najdete v tématu [předdefinované role pro prostředky Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).

## <a name="using-custom-roles"></a>Používání vlastních rolí

Přestože předdefinované role v Azure podporují širokou škálu scénářů řízení přístupu, nemusí splňovat všechny potřeby vaší organizace nebo týmu. Pokud například máte jednu skupinu uživatelů odpovědných za správu virtuálních počítačů a prostředků Azure SQL Database, možná budete chtít vytvořit vlastní roli pro optimalizaci správy požadovaných řízení přístupu.

Dokumentace k RBAC v Azure obsahuje pokyny pro [vytváření vlastních rolí](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) spolu s podrobnostmi o tom, jak [fungují definice rolí](https://docs.microsoft.com/azure/role-based-access-control/role-definitions).

## <a name="separation-of-responsibilities-and-roles-for-large-organizations"></a>Oddělení odpovědností a rolí pro velké organizace

RBAC umožňuje organizacím přiřadit různé týmy k různým úlohám správy v rámci rozsáhlých cloudových aktiv. To umožňuje centrálním IT týmům řídit základní funkce přístupu a zabezpečení a zároveň poskytuje vývojářům softwaru a dalším týmům velkou kontrolu nad konkrétními úlohami nebo skupinami prostředků.

Většina cloudových prostředí může také těžit ze strategie řízení přístupu, která využívá více rolí a zdůrazňuje oddělení odpovědností mezi těmito rolemi. Tento přístup vyžaduje, aby provedení jakékoli významné změny prostředků nebo infrastruktury zahrnovalo více rolí, což zajistí, že změnu musí zkontrolovat a schválit více než jedna osoba. Toto oddělení odpovědnosti omezuje schopnost jedné osoby přistupovat k citlivým datům nebo zavést ohrožení zabezpečení bez vědomí jiných členů týmu.

Následující tabulka zobrazuje běžný vzor rozdělení IT odpovědností na samostatné vlastní role:

<!-- markdownlint-disable MD033 -->

| Skupina | Běžný název role | Odpovědnost |
| --- | --- | --- |
| Operace zabezpečení | SecOps | Poskytuje obecnou kontrolu zabezpečení.<br/><br/> Vytváří a vynucuje zásady zabezpečení, například šifrování neaktivních dat.<br/><br/> Spravuje šifrovací klíče.<br/><br/> Spravuje pravidla brány firewall. |
| Síťové operace | NetOps | Spravuje konfiguraci sítě a operace v rámci virtuálních sítí, jako jsou trasy a peering. |
| Systémové operace | SysOps | Určuje možnosti infrastruktury pro výpočetní prostředky a úložiště a spravuje prostředky, které byly nasazeny. |
| Vývoj, testování a provoz | DevOps | Vytváří a nasazuje funkce a aplikace úloh.<br/><br/> Provozuje funkce a aplikace tak, aby byly plněny smlouvy o úrovni služeb (SLA) a další standardy kvality. |

<!-- markdownlint-enable MD033 -->

Rozpis akcí a oprávnění v těchto standardních rolích je ve všech vašich aplikacích, předplatných nebo celé cloudové službě často stejný, a to i v případě, že tyto role vykonávají různí lidé na různých úrovních. Proto můžete vytvořit společnou sadu definic rolí RBAC, které se použijí v různých rozsazích ve vašem prostředí. Uživatelům a skupinám pak lze přiřadit společnou roli, ale jenom pro rozsah prostředků, skupin prostředků, předplatných nebo skupin pro správu, za jejichž správu zodpovídají.

Například v [síťové topologii rozbočovače a paprsku](../azure-best-practices/hub-spoke-network-topology.md) s více předplatnými můžete mít pro centrum a všechny úlohy na koncích společnou sadu definic rolí. Roli NetOps předplatného centra můžete přiřadit členům centrálního IT týmu organizace, kteří zodpovídají za správu sítě pro sdílené služby používané všemi úlohami. Roli NetOps předplatného paprsku úlohy potom můžete přiřadit členům tohoto konkrétního týmu úloh, což jim umožní nakonfigurovat síť v rámci tohoto předplatného tak, aby co nejlépe podporovala jejich požadavky na úlohy. Pro oba týmy se používá stejná definice rolí, ale přiřazení na základě rozsahu zajišťují, že uživatelé mají jenom takový přístup, který potřebují k provádění potřebných úloh.
