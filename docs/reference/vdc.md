---
title: Virtuální datové centrum Azure
description: Prostředky pro virtuální datové centrum Microsoft Azure
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
keywords: Azure
layout: LandingPage
ms.openlocfilehash: 39cb6ac3c31873431206d8c6c525c9ce3467653f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029442"
---
# <a name="azure-virtual-datacenter-and-the-enterprise-control-plane"></a>Virtuální datové centrum Azure a rovina podnikového řízení

Virtuální datové centrum Azure je přístup, který umožňuje využít možnosti cloudové platformy Azure na maximum a současně respektovat stávající zásady zabezpečení a využití sítě. Když obchodní jednotky a organizace IT nasazují podnikové úlohy do cloudu, musí zajistit rovnováhu mezi zásadami správného řízení a flexibilitou vývojářů. Virtuální datové centrum Azure poskytuje modely, které pomáhají této rovnováhy dosáhnout s důrazem na zásady správného řízení.

## <a name="resources"></a>Zdroje a prostředky

<!-- markdownlint-disable MD033 -->

<table>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Concepts"><img src="../_images/vdc/virtual-datacenter.svg" alt="Virtual Datacenter e-book" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Concepts">Virtuální datové centrum Azure: Koncepty</a></h3>
        <p>Tato elektronická kniha ukazuje, jak nasazovat podnikové úlohy do cloudové platformy Azure při zachování stávajících zásad sítě a zabezpečení.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="./networking-vdc.md"><img src="../_images/vdc/vdc-network.png" alt="Network Perspective" /></a></td>
    <td>
        <h3><a href="./networking-vdc.md">Virtuální datové centrum Azure: Z pohledu sítě</a></h3>
        <p>Tento online článek poskytuje přehled modelů a návrhů sítě umožňujících odstranit řadu překážek v podobě škálování architektury, výkonu a zabezpečení, se kterými se řada zákazníků setkává při úvahách o kompletním přechodu na cloudovou platformu.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Lift"><img src="../_images/vdc/vdc-lift-and-shift.png" alt="Lift and Shift Guide" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Lift">Virtuální datové centrum Azure: Průvodce metodou „lift and shift“</a></h3>
        <p>Tento dokument white paper popisuje proces, který umožňuje pracovníkům IT a osobám s rozhodovací pravomocí prozkoumat a naplánovat migraci aplikací a serverů do Azure pomocí metody „lift and shift“. Ta dovoluje snížit na minimum náklady na dodatečný vývoj a zároveň optimalizovat možnosti hostování cloudu.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Deck"><img src="../_images/vdc/vdc-deck.png" alt="Presentation Deck" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Deck">Virtuální datové centrum Azure: Sada prezentací</a></h3>
        <p>Tato sada prezentace zkoumá doporučení a nástroje virtuálního datového centra Azure. Pojednává o cílech virtuálního datového střediska, motivaci zákazníků, oblastech Azure, prvcích automatizace virtuálního datového střediska, industrializovaných a důvěryhodných virtuálních datových střediscích Azure a na závěr uvádí akční plán obsahující rady pro ředitele IT. Poskytuje taky informace o podpoře a školení.</p>
    </td>
</tr>
</table>

<!-- markdownlint-enable MD033 -->

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-azure-virtual-datacenter"></a>Co je to virtuální datové centrum Azure?

S nasazením úloh do cloudu přichází potřeba vývoje a zachování důvěryhodnosti v cloudu ve stejné míře, v jaké důvěřujete svým stávajícím datovým centrům. První model rad pro virtuální datové centrum Azure má za cíl uspokojit tuto potřebu pomocí uzamčeného přístupu k virtuální infrastruktuře. Tento přístup se nehodí pro každého. Je speciálně určený k tomu, aby pomohl podnikovým oddělením IT rozšířit jejich místní infrastrukturu na veřejný cloud Azure. Tomuto přístupu říkáme model rozšíření důvěryhodného datového centra. Postupem času nabídneme i několik dalších modelů, včetně takových, které umožňují zabezpečený přístup k internetu přímo z virtuálního datového centra.

<!-- markdownlint-disable MD033 -->

<img src="../_images/vdc/vdc-components.svg" alt="Virtual Datacenter components" style="max-width:700px;"/>

<!-- markdownlint-enable MD033 -->

Virtuální datové centrum Azure může fungovat díky těmto čtyřem komponentám: identita, šifrování, softwarově definované sítě a dodržování předpisů (včetně protokolů a vytváření sestav).

V modelu virtuální datového centra Azure můžete použít zásady izolace, přiblížit cloud fyzickým datovým centrům, která znáte, a dosáhnout požadovaných úrovní zabezpečení a důvěry. To je možné díky čtyřem komponentám, se kterými je obeznámený každý podnikový tým IT: softwarově definovaným sítím, šifrování, řízení identit a podkladových standardů a certifikací platformy Azure v oblasti dodržování předpisů. Tyto čtyři komponenty jsou klíčem k tomu, aby se mohlo virtuální datové centrum stát důvěryhodným rozšířením vaší dosavadní investice do infrastruktury.

Další informace si můžete přečíst v elektronické knize [Koncepty virtuálního datového centra Azure](https://azure.microsoft.com/resources/azure-virtual-datacenter).
