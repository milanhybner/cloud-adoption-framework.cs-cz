---
title: Pochopení standardních hodnot zabezpečení cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si o standardních hodnotách zabezpečení cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 40bcd90d632bedd4e924942ac6efae5034cc0af8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221783"
---
# <a name="understand-the-cloud-security-baseline"></a>Pochopení standardních hodnot zabezpečení cloudu

Toto je úvodní článek v obecném tématu základního plánu zabezpečení cloudu, který sestaví [pět oborů zásad správného řízení cloudu](../governance-disciplines.md) , které vytváří rozhraní zásad správného řízení. Podrobnější informace o zabezpečení cloudu jsou k dispozici z [důvěryhodného cloudu Azure](https://azure.microsoft.com/overview/trusted-cloud). Přístupy k vylepšení stav zabezpečení vaší organizace najdete v [katalogu Cloud Service Security](https://www.microsoft.com/security/information-protection) .

> [!NOTE]
> V tomto článku není očekáváno poskytování dostatečného kontextu, který umožňuje čtenářům implementovat strategii zabezpečení. Je jenom pro obecné povědomí.

## <a name="cloud-security"></a>Zabezpečení cloudu

Zabezpečení cloudu je rozšíření tradičních postupů zabezpečení informací. Tradiční IT zabezpečení by zahrnovalo zásady a ovládací prvky řízení zabezpečení počítače, zabezpečení sítě, ochrany dat, využití informací a tak dále. V cloudu jsou potřeba stejné zásady a ovládací prvky. Během jakékoli transformace cloudu je potřeba, aby se ředitelka zabezpečení informací aktivně účastnila a pochopila cloudovou na šířku a zajistila tak, aby se starší zásady IT mapovaly na správné úrovně kontroly v cloudu.

Minimální strategii cloudového zabezpečení byste měli zvážit v následujících tématech:

- **Klasifikace dat.** Správná klasifikace dat pro pochopení jakýchkoli zdrojů dat, které jsou soukromé, chráněné nebo vysoce důvěrné. To vám pomůže se správou rizik během plánování.
- **Naplánujte Scénář hybridního cloudu.** Porozumět způsobu, jakým se starší verze a místní sítě připojí ke cloudu, pomůžou ředitelka zabezpečení informací identifikovat a opravit rizika.
- **Plánování útoků a chyb.** V prvních několika měsících transformace budou provedeny chyby, jak se tým učí. Začněte s nízkým rizikem a vysoce omezeným nasazením, abyste se mohli bezpečně dozvědět.
- **Nastavte prioritu ochrany osobních údajů.** V celé transformaci by měl mít celý tým na mysli soukromí zákazníků a zaměstnanců. Vaše data jsou v cloudu bezpečná, ale při práci s citlivými daty by měl být v týmu vědomá a zvýšená opatrnost.

## <a name="protecting-data-and-privacy"></a>Ochrana dat a ochrany osobních údajů

Pro organizace v celém světě&mdash;, zda se vlády, neziskové&mdash;nebo podnikové cloud computingu staly klíčovou součástí své probíhající strategie IT. Služba Cloud Services poskytuje organizacím všech velikostí přístup k prakticky neomezenému úložišti dat a přitom je uvolňuje z nutnosti kupovat, udržovat a aktualizovat vlastní sítě a počítačové systémy. Microsoft a další poskytovatelé cloudu nabízejí infrastrukturu IT, platformu a software jako službu (SaaS) a umožňují zákazníkům rychle škálovat nahoru nebo dolů podle potřeby a platit jenom za výpočetní výkon a úložiště, které používají.

Jelikož ale organizace i nadále využívají výhod cloudových služeb, jako je větší volba, flexibilita a flexibilita při zvyšování efektivity a snížení nákladů na IT, musí zvážit, jak by zavedení cloudových služeb mělo vliv na jejich Ochrana osobních údajů, zabezpečení a dodržování předpisů stav. Společnost Microsoft pracovala tak, aby své cloudové nabídky nejen škálovatelná, spolehlivá a spravovatelná, ale taky zajistila ochranu a používání dat našich zákazníků transparentním způsobem.

Zabezpečení je základní součástí silné ochrany dat ve všech prostředích online computingu. Ale samotná zabezpečení není dostačující. Ochota spotřebitelů a firem používat konkrétní cloudový výpočetní produkt závisí také na jejich schopnosti důvěřovat, že soukromí svých informací bude chráněno a že jejich data budou použita pouze způsobem konzistentním se očekáváním zákazníků. . Další informace o přístupu Microsoftu k [ochraně dat a osobních údajů v cloudu](https://go.microsoft.com/fwlink/?LinkId=808242&clcid=0x409)

## <a name="risk-mitigation"></a>Omezení rizik

Dvě největší rizika v jakémkoli datacentru se dají seskupovat do dvou zdrojů: Systémy pro stárnutí a lidská chyba. Ochrana před těmito dvěma riziky je při definování strategie zabezpečení IT minimální. Totéž platí i v cloudu. Následuje několik příkladů ovládacích prvků, které je možné zavést k nápravě rizik a posílení strategie cloudového zabezpečení.

- **Starší verze systémů:** Mnohé součásti v místních řešeních datového centra se skládají z softwaru, hardwaru a procesů, které jsou aktuálními bezpečnostními riziky v aktuálním stavu. Pokud je to možné, opravte, nahraďte nebo vyřaďte tyto systémy během transformace cloudu. Samozřejmě to není vždy proveditelné. Pokud všechny starší systémy zůstanou v produkčním prostředí v hybridním řešení, je důležité, aby tyto systémy byly v inventáři a rozuměly při návrhu virtuálního datacentra. Tím umožníte týmu návrhu eliminovat nebo řídit přístup k těmto systémům z cloudu.
- **Procesy zabezpečení IT a ovládací prvky:** Minimálně by měly být týmy pro návrh cloudu aktualizovány na stávající procesy zabezpečení IT a ovládací prvky, které jsou předávány do cloudu. V ideálním scénáři by byl člen týmu IT Security vyškolený v kyberbezpečnosti a vyhrazený jako člen týmů pro návrh a implementaci.
- **Monitorování a auditování:** Při navrhování procesů a nástrojů zásad správného řízení zajistěte, aby řešení monitorování a auditování zahrnovala bezpečnostní rizika nebo porušení.

> [!NOTE]
> **Odhalení technického dluhu:** V tomto tématu chybí další kroky, které by bylo možné provést. Články týkající se přidání budou v průběhu času rozšířeny na toto téma. Podrobnější informace o zabezpečení cloudu jsou k dispozici z [důvěryhodného cloudu Azure](https://azure.microsoft.com/overview/trusted-cloud). Přístupy k vylepšení stav zabezpečení vaší organizace najdete v [katalogu Cloud Service Security](https://www.microsoft.com/security/information-protection) .
