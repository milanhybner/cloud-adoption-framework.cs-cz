---
title: Jak funguje Azure?
description: Seznamte se se základy interní struktury a fungování cloudové platformy Azure a virtualizace cloudu.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 39373c0f2c4c7d96613fd10d5734a2826b6f1933
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892060"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>Jak funguje Azure?

Azure je veřejná cloudová platforma Microsoftu. Azure nabízí rozsáhlou kolekci služeb, včetně platforem jako služby (PaaS), infrastruktury jako služby (IaaS) a funkcí spravované databázové služby. Ale co přesně je Azure a jak to funguje?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ixGo]

Azure, podobně jako jiné cloudové platformy, spoléhá na technologii, která se označuje jako _virtualizace_. Většina počítačového hardwaru může být emulovaná v softwaru, protože většina hardwaru počítače je jednoduše sadou instrukcí trvale nebo částečně nakódovaných v silikonu. Pomocí vrstvy emulace, která mapuje pokyny pro software k hardwarovým pokynům, virtualizovaný hardware může být spuštěný v softwaru, jako by šlo o skutečný hardware.

Cloud je v podstatě sada fyzických serverů v jednom nebo několika datových centrech, které provádějí virtualizovaného hardwaru jménem zákazníků. Jak Cloud vytváří, spouští, zastavuje a odstraňuje miliony instancí virtualizovaného hardwaru pro miliony zákazníků současně?

Abychom to porozuměli, Podívejme se na architekturu hardwaru v datacentru. V každém datovém centru je kolekce serverů, které se nacházejí v rackech serveru. Každý stojan serveru obsahuje mnoho serverů a také síťový **přepínač, který** poskytuje síťové připojení a jednotku pro distribuci napájení (PDU) poskytující napájení. Stojany se někdy seskupují dohromady ve větších jednotkách známých jako _clustery_.

V rámci každého stojanu nebo clusteru je většina serverů určena ke spouštění těchto virtualizovaných hardwarových instancí jménem uživatele. Některé servery ale spouštějí software pro správu cloudu, který se označuje jako kontroler prostředků infrastruktury. _Kontroler prostředků infrastruktury_ je distribuovaná aplikace s mnoha zodpovědnostmi. Přiděluje služby, monitoruje stav serveru a služby, které jsou v něm spuštěné, a při selhání zaceleuje servery.

Každá instance kontroleru prostředků infrastruktury je připojená k jiné sadě serverů, na kterých je spuštěný software orchestrace cloudu, obvykle označovaný jako _front-end_. Front-end hostuje webové služby, rozhraní RESTful API a interní databáze Azure používané pro všechny funkce, které Cloud provádí.

Například front-end hostuje služby, které zpracovávají žádosti zákazníků o přidělení prostředků Azure, jako jsou [virtuální počítače](https://docs.microsoft.com/azure/virtual-machines), a služby, jako je [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction). Za prvé, front-end ověří uživatele a ověří, jestli má uživatel oprávnění přidělit požadované prostředky. V takovém případě front-end zkontroluje databázi, aby vyhledala serverovou skříň s dostatečnou kapacitou, a pak řadiči prostředků infrastruktury na daném stojanu přidělí prostředky.

Proto je Azure velkou kolekcí serverů a síťových hardwarových zařízení, na kterých je spuštěná složitá sada distribuovaných aplikací pro orchestraci konfigurace a provozu virtualizovaného hardwaru a softwaru na těchto serverech. Je to orchestrace, která zajišťuje, aby Azure tak výkonným&mdash;m uživatelům nezodpovídá za údržbu a upgradování hardwaru, protože Azure vše udělá na pozadí.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o přijetí cloudu pomocí [rozhraní pro přijetí Microsoft Cloud pro Azure](https://docs.microsoft.com/azure/cloud-adoption-framework).

> [!div class="nextstepaction"]
> [Další informace o rozhraní Microsoft Cloud pro přijetí pro Azure](https://docs.microsoft.com/azure/cloud-adoption-framework)
