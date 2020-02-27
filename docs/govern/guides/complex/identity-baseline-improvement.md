---
title: 'Komplexní řízení podniku: zvýšení oboru standardních hodnot identity'
description: Rozhraní pro přijetí v cloudu pro Azure vám umožní získat informace o přidání kontrolních prvků identity na minimální životaschopný produkt (MVP) pro zásady správného řízení.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/06/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 05a3ce3eb018a9b15f66b90749782def260c66d7
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707607"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-identity-baseline-discipline"></a>Příručka zásad správného řízení pro komplexní podniky: zlepšení pravidla směrného plánu identity

Tento článek popisuje mluvený komentář přidáním ovládacích prvků pro kontrolu základní identity do MVP pro řízení.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Obchodní odůvodnění migrace těchto dvou datových center do cloudu schválila finanční ŘEDITELka. Během studie technické proveditelnosti se zjistilo několik překážek:

- Chráněná data a klíčové aplikace reprezentují 25% úloh v obou datových centrech. Není možné je odstranit, dokud nebudou moderní zásady správného řízení týkající se citlivých osobních údajů a důležitých aplikací.
- 7% prostředků v těchto datacentrech není kompatibilních s cloudem. Před ukončením smlouvy Datacenter budou přesunuty do alternativního datového centra.
- 15% prostředků v datacentru (750 virtuálních počítačů) má závislost na starší verzi ověřování nebo Multi-Factor Authentication třetích stran.
- Připojení VPN, které spojuje stávající datová centra a Azure, nenabízí dostatečné rychlosti přenosu dat ani latenci pro migraci objemu prostředků v rámci časové osy dvou let pro vyřazení datacentra.

První dvě překážek jsou spravovány paralelně. Tento článek bude řešit řešení třetího a čtvrtého překážek.

### <a name="expand-the-cloud-governance-team"></a>Rozbalení týmu zásad správného řízení cloudu

Tým zásad správného řízení cloudu rozšiřuje. Vzhledem k tomu, že je potřeba další podpora týkající se správy identit, se správce systémů od týmu standardních hodnot identity teď účastní týdenní schůzky, aby si stávající členové týmu dozvěděli změny.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

IT tým má souhlas s přesunem v rámci plánů CIO a ŘEDITELe za účelem vyřazení dvou datových center. Je však dotčeno 750 (15%) z prostředků v těchto datacentrech se bude muset přesunout jinam než Cloud.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Nové plány stavů v budoucnosti vyžadují pro migraci virtuálních počítačů s 750 se staršími požadavky na ověření robustnější základní řešení identity. Kromě těchto dvou datových center se očekává, že tato výzva má vliv na podobné procentuální podíly assetů v jiných datových centrech.

Budoucí stav teď také vyžaduje připojení od poskytovatele cloudu k řešení MPLS nebo pronajatého řádku společnosti.

Změny aktuálního a budoucího stavu zveřejňují nová rizika, která budou vyžadovat nové příkazy zásad.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Pracovní přerušení během migrace.** Migrace do cloudu vytvoří řízené, časově vázané riziko, které se dá spravovat. Přesunutí hardwaru pro stárnutí do jiné části světa je mnohem vyšší riziko. K tomu, aby nedocházelo k přerušení obchodních operací, je potřeba strategie zmírňování.

**Existující závislosti identity.** Závislosti na stávajícím ověřování a službách identity můžou zpozdit nebo bránit migraci některých úloh do cloudu. Po neúspěšném vrácení těchto dvou datových center se za miliony dolarů v datacentrech zapůjčení účtuje miliony dolarů.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

- Starší verze ověřování nemusí být k dispozici v cloudu, což omezuje nasazení některých aplikací.
- Aktuální řešení Multi-Factor Authentication od třetí strany nemusí být k dispozici v cloudu, což omezuje nasazení některých aplikací.
- Převádění nebo přesouvání může způsobit výpadky nebo přidat náklady.
- Rychlost a stabilita sítě VPN může bránit migraci.
- Provoz přicházející do cloudu může způsobit problémy se zabezpečením v jiných částech globální sítě.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky.

- Zvolený poskytovatel cloudu musí nabídnout způsob ověřování pomocí starších metod.
- Zvolený poskytovatel cloudu musí nabídnout způsob ověřování s aktuálním řešením Multi-Factor Authentication od třetí strany.
- Mezi poskytovatelem cloudu a poskytovatelem výpovědi společnosti by se mělo vytvořit vysokorychlostní privátní připojení, které poskytovatel cloudu připojí k globální síti datových center.
- Dokud nebudou navázány dostatečné požadavky na zabezpečení, nebude mít žádný příchozí veřejný provoz přístup k prostředkům společnosti hostovaným v cloudu. Všechny porty jsou blokované z libovolného zdroje mimo globální síť WAN.

## <a name="incremental-improvement-of-the-best-practices"></a>Přírůstkové zlepšení osvědčených postupů

Návrh MVP pro zásady správného řízení zahrnuje nové zásady Azure a implementaci služby Active Directory na virtuálním počítači. Tyto dvě změny návrhu společně splní nové příkazy firemních zásad.

Nové osvědčené postupy:

- Podrobný **plán zabezpečení hybridní virtuální sítě:** Místní strana hybridní sítě by měla být nakonfigurovaná tak, aby umožňovala komunikaci mezi následujícím řešením a místními servery služby Active Directory. Tento osvědčený postup vyžaduje, aby DMZ povolil Active Directory Domain Services přes hranice sítě.
- **Šablony Azure Resource Manager:**
    1. Definujte NSG pro blokování externích přenosů a povolte interní provoz.
    2. Nasaďte dva virtuální počítače služby Active Directory ve dvojici s vyrovnáváním zatížení na základě zlaté image. Při prvním spuštění tento obrázek spustí skript PowerShellu, který se připojí k doméně a zaregistruje se pomocí doménových služeb. Další informace najdete v tématu věnovaném [rozšiřování Active Directory Domain Services (služba AD DS) do Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain).
- Azure Policy: použijte NSG pro všechny prostředky.
- Podrobný plán Azure:
    1. Vytvořte podrobný plán s názvem `active-directory-virtual-machines`.
    2. Jednotlivé šablony a zásady služby Active Directory přidejte do podrobného plánu.
    3. Publikovat podrobný plán do jakékoli příslušné skupiny pro správu.
    4. Použijte podrobný plán na jakékoli předplatné, které vyžaduje starší verze nebo Multi-Factor Authentication třetí strany.
    5. Instance Active Directory běžící v Azure se teď dá použít jako rozšíření místního řešení Active Directory, což umožňuje integraci s existujícím nástrojem Multi-Factor Authentication a poskytování ověřování založeného na deklaracích. existující funkce služby Active Directory.

## <a name="conclusion"></a>Závěr

Přidáním těchto změn do MVP pro kontrolu zásad správného řízení můžete napravit mnoho rizik v tomto článku, což umožňuje každému týmu přijetí v rámci cloudu rychle přesunout za tento roadblock.

## <a name="next-steps"></a>Další kroky

V případě, že se přijetí do cloudu pokračuje a přináší další obchodní hodnotu, rizika a potřeby zásad správného řízení cloudu se změní také. Níže jsou uvedené některé změny, ke kterým může dojít. U této fiktivní společnosti je další triggerem zahrnutí chráněných dat do plánu přijetí do cloudu. Tato změna vyžaduje další ovládací prvky zabezpečení.

> [!div class="nextstepaction"]
> [Zlepšení pravidla směrného plánu zabezpečení](./security-baseline-improvement.md)
