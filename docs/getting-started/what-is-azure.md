---
title: Jak funguje Azure?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vysvětlení interního fungování Azure
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 6aabf9545aa6774b63d3dbd201373273c3f8f1ab
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829147"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>Jak funguje Azure?

Azure je veřejná cloudová platforma Microsoftu. Azure nabízí rozsáhlou kolekci služeb, včetně platforem jako služby (PaaS), infrastruktury jako služby (IaaS) a funkcí spravované databázové služby. Ale co přesně je Azure a jak to funguje?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ixGo]

Azure, podobně jako jiné cloudové platformy, spoléhá na technologii, která se označuje jako **virtualizace**. Většina počítačového hardwaru může být emulovaná v softwaru, protože většina hardwaru počítače je jednoduše sadou instrukcí trvale nebo částečně nakódovaných v silikonu. Pomocí vrstvy emulace, která mapuje pokyny pro software k hardwarovým pokynům, virtualizovaný hardware může být spuštěný v softwaru, jako by šlo o skutečný hardware.

Cloud je v podstatě sada fyzických serverů v jednom nebo několika datových centrech, které provádějí virtualizovaného hardwaru jménem zákazníků. Jak Cloud vytváří, spouští, zastavuje a odstraňuje miliony instancí virtualizovaného hardwaru pro miliony zákazníků současně?

Abychom to porozuměli, Podívejme se na architekturu hardwaru v datacentru. V každém datovém centru je kolekce serverů, které se nacházejí v rackech serveru. Každý stojan serveru obsahuje mnoho serverů a také síťový **přepínač, který** poskytuje síťové připojení a jednotku pro distribuci napájení (PDU) poskytující napájení. Stojany se někdy seskupují dohromady ve větších jednotkách známých jako **clustery**.

V rámci každého stojanu nebo clusteru je většina serverů určena ke spouštění těchto virtualizovaných hardwarových instancí jménem uživatele. Některé servery ale spouštějí software pro správu cloudu, který se označuje jako kontroler prostředků infrastruktury. **Kontroler prostředků infrastruktury** je distribuovaná aplikace s mnoha zodpovědnostmi. Přiděluje služby, monitoruje stav serveru a služby, které jsou v něm spuštěné, a při selhání zaceleuje servery.

Každá instance kontroleru prostředků infrastruktury je připojená k jiné sadě serverů, na kterých je spuštěný software orchestrace cloudu, obvykle označovaný jako **front-end**. Front-end hostuje webové služby, rozhraní RESTful API a interní databáze Azure používané pro všechny funkce, které Cloud provádí.

Například front-end hostuje služby, které zpracovávají žádosti zákazníků o přidělení prostředků Azure, jako jsou [virtuální počítače](/azure/virtual-machines), a služby, jako je [Cosmos DB](/azure/cosmos-db/introduction). Za prvé, front-end ověří uživatele a ověří, jestli má uživatel oprávnění přidělit požadované prostředky. V takovém případě front-end zkontroluje databázi, aby vyhledala serverovou skříň s dostatečnou kapacitou, a pak řadiči prostředků infrastruktury na daném stojanu přidělí prostředky.

Proto je Azure velkou kolekcí serverů a síťových hardwarových zařízení, na kterých je spuštěná složitá sada distribuovaných aplikací pro orchestraci konfigurace a provozu virtualizovaného hardwaru a softwaru na těchto serverech. Je to orchestrace, která zajišťuje, že Azure&mdash;už nebude zodpovědný za údržbu a upgrade hardwaru, protože Azure to vše udělá na pozadí.

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte interním Azure, se dozvíte o řízení prostředků cloudu.

> [!div class="nextstepaction"]
> [Další informace o správě prostředků](../governance/resource-consistency/what-is-governance.md)

<!-- links -->

[docs-add-users-to-aad]: /azure/active-directory/add-users-azure-active-directory?toc=/azure/architecture/cloud-adoption-guide/toc.json
