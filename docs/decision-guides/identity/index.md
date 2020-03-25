---
title: Průvodce rozhodováním ohledně identity
description: Získejte informace o tom, jak služby pro správu identit a přístupu (IAM) umožňují spravovat řízení přístupu v cloudu.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 3fb64c89a36db98a4dbf186f2ff3609bae0c4a2b
ms.sourcegitcommit: 25cd1b3f218d0644f911737a6d5fd259461b2458
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80225934"
---
<!-- cSpell:ignore Kerberos NTLM SAML -->

# <a name="identity-decision-guide"></a>Průvodce rozhodováním ohledně identity

IT pracovníci v jakémkoli prostředí, ať už se jedná o místní, hybridní nebo výhradně cloudové prostředí, potřebují řídit, kteří správci, uživatelé a skupiny mají přístup k prostředkům. Služby pro správu identit a přístupu (IAM) umožňují spravovat řízení přístupu v cloudu.

![Diagram možností identity od nejjednodušších po nejsložitější, které odpovídají rychlým odkazům níže](../../_images/decision-guides/decision-guide-identity.png)

Přejít na: [Určení požadavků na integraci identit](#determine-identity-integration-requirements) | [Směrný plán cloudu](#cloud-baseline) | [Synchronizace adresářů](#directory-synchronization) | [Doménové služby hostované v cloudu](#cloud-hosted-domain-services) | [Active Directory Federation Services](#active-directory-federation-services) | [Další informace](#learn-more)

Pro správu identit v cloudovém prostředí je k dispozici několik možností. Tyto možnosti se liší náklady a složitostí. Klíčovým faktorem při strukturování cloudových služeb identit je požadovaná úroveň integrace se stávající místní infrastrukturou identit.

V Azure zajišťuje základní úroveň řízení přístupu a správy identit pro cloudové prostředky služba Azure Active Directory (Azure AD). Pokud ale místní infrastruktura Active Directory vaší organizace obsahuje složitou doménovou strukturu nebo přizpůsobené organizační jednotky, vaše cloudové úlohy mohou vyžadovat synchronizaci se službou Azure AD, která zajistí konzistenci identit, skupin a rolí mezi vaším místním a cloudovým prostředím. Pro zajištění podpory aplikací, které závisí na starších mechanismech ověřování, se může vyžadovat nasazení služby Active Directory Domain Services (AD DS) v cloudu.

Správa cloudových identit je iterativní proces. Při počátečním nasazení můžete začít s řešeními nativními pro cloud a malou skupinou uživatelů a odpovídajících rolí. S tím, jak se bude vaše migrace vyvíjet, možná budete potřebovat pomocí synchronizace adresářů integrovat řešení identit nebo do svých cloudových nasazení přidat doménové služby. V každé iteraci procesu migrace si znovu projděte svou strategii pro identity.

## <a name="determine-identity-integration-requirements"></a>Určení požadavků na integraci identit

| Otázka | Směrný plán cloudu | Synchronizace adresářů | Doménové služby hostované v cloudu | Active Directory Federation Services |
|------|------|------|------|------|
| Chybí vám v současnosti místní adresářová služba? | Ano | Ne | Ne | Ne |
| Potřebují vaše úlohy pracovat se sadou uživatelů a skupin společnou pro cloudové i místní prostředí? | Ne | Ano | Ne | Ne |
| Závisí vaše úlohy na starších mechanismech ověřování, jako jsou protokoly Kerberos nebo NTLM? | Ne | Ne | Ano | Ano |
| Vyžadujete jednotné přihlašování napříč různými zprostředkovateli identit? | Ne | Ne | Ne | Ano |

V rámci plánování migrace do Azure budete muset určit nejlepší způsob integrace vaší stávající správy identit a cloudových služeb identit. Následují běžné scénáře integrace.

### <a name="cloud-baseline"></a>Směrný plán cloudu

Azure AD je nativní systém správy identit a přístupu (IAM) umožňující udělovat uživatelům a skupinám přístup k funkcím správy na platformě Azure. Pokud vaší organizaci chybí důležité místní řešení identit a plánujete migrací úloh zajistit jejich kompatibilitu s mechanismy ověřování v cloudu, měli byste začít s vývojem infrastruktury identit a jako základ použít Azure AD.

**Předpoklady směrného plánu cloudu:** Při použití infrastruktury identit nativní čistě pro cloud se předpokládá následující:

- Vaše cloudové prostředky nebudou mít závislosti na místních adresářových službách ani serverech Active Directory, případně je možné úlohy upravit a tyto závislosti odebrat.
- Migrované úlohy aplikací nebo služeb buď podporují mechanismy ověřování kompatibilní se službou Azure AD, nebo je možné je snadno upravit tak, aby je podporovaly. Azure AD se spoléhá na mechanismy ověřování připravené pro internet, jako je SAML, OAuth nebo OpenID Connect. Stávající úlohy, které závisí na starších metodách ověřování s využitím protokolů, jako je Kerberos nebo NTLM, možná bude potřeba před migrací do cloudu refaktorovat podle vzoru směrného plánu cloudu.

> [!TIP]
> Kompletní migrací služeb identit do Azure AD se eliminuje potřeba udržovat vlastní infrastrukturu identit a tím se výrazně zjednoduší správa IT.
>
> Azure AD však není úplnou náhradou za tradiční místní infrastrukturu Active Directory. Funkce adresáře, jako jsou starší metody ověřování, správa počítačů nebo zásady skupin, nemusí být dostupné, dokud do cloudu nenasadíte další nástroje nebo služby.
>
> V případě scénářů, kdy s cloudovými nasazeními potřebujete integrovat místní identity nebo doménové služby, si níže můžete přečíst o modelech synchronizace adresářů a doménových služeb hostovaných v cloudu.

### <a name="directory-synchronization"></a>Synchronizace adresářů

Synchronizace adresářů je často nejlepším řešením pro organizace se stávající místní infrastrukturou Active Directory, kterým umožňuje zachovat stávající správu uživatelů a přístupu a zároveň poskytuje požadované funkce IAM pro správu cloudových prostředků. Tento proces průběžně replikuje informace o adresářích mezi Azure AD a místními adresářovými službami a díky tomu umožňuje uživatelům používat společné přihlašovací údaje a zajišťuje konzistentní systém identit, rolí a oprávnění v celé organizaci.

Poznámka: Je možné, že organizace, které přešly na Office 365, už mají implementovanou [synchronizaci adresářů](https://docs.microsoft.com/office365/enterprise/set-up-directory-synchronization) mezi místní infrastrukturou Active Directory a službou Azure Active Directory.

**Předpoklady synchronizace adresářů:** Při použití řešení synchronizovaných identit se předpokládá následující:

- V cloudové i místní IT infrastruktuře musíte udržovat společnou sadu uživatelských účtů a skupin.
- Vaše místní služby identit podporují replikaci pomocí služby Azure AD.

> [!TIP]
> Všechny cloudové úlohy, které závisí na starších mechanismech ověřování zajišťovaných místními servery Active Directory a které Azure AD nepodporuje, budou stále vyžadovat připojení k místním doménovým službám nebo virtuálním serverům v cloudovém prostředí, které tyto služby zajišťují. Používáním místních služeb identit také vznikají závislosti na možnostech připojení mezi cloudem a místními sítěmi.

### <a name="cloud-hosted-domain-services"></a>Doménové služby hostované v cloudu

Pokud máte úlohy, které závisí na ověřování na základě deklarace identity s využitím starších protokolů, jako je Kerberos nebo NTLM a které není možné refaktorovat tak, aby přijímaly moderní ověřovací protokoly, jako je SAML, OAuth nebo OpenID Connect, možná v rámci cloudového nasazení budete muset do cloudu migrovat i některé vaše doménové služby.

Tento model zahrnuje nasazení virtuálních počítačů se službou Active Directory do cloudových virtuálních sítí za účelem zajištění služby Active Directory Domain Services (AD DS) pro prostředky v cloudu. Všechny stávající aplikace a služby, které se migrují do vaší cloudové sítě, by s menšími úpravami měly být schopné používat tyto adresářové servery hostované v cloudu.

V místním prostředí se pravděpodobně budou i nadále používat stávající adresáře a doménové služby. V tomto scénáři doporučujeme využít také synchronizaci adresářů, která v cloudovém i místním prostředí zajistí společnou sadu uživatelů a rolí.

**Předpoklady pro doménové služby hostované v cloudu:** Při provádění migrace adresářů se předpokládá následující:

- Vaše úlohy závisí na ověřování na základě deklarace identity s využitím protokolů, jako je Kerberos nebo NTLM.
- Pro účely správy nebo uplatňování zásad skupin Active Directory musí být vaše virtuální počítače úloh připojené k doméně.

> [!TIP]
> Přestože kombinace migrace adresářů a doménových služeb hostovaných v cloudu poskytuje velkou flexibilitu při migraci stávajících úloh, hostováním virtuálních počítačů zajišťujících tyto služby ve vlastní cloudové virtuální síti se zvyšuje složitost úloh správy IT. S tím, jak se bude vaše migrace do cloudu vyvíjet, prozkoumejte požadavky na dlouhodobou údržbu spojenou s hostováním těchto serverů. Zvažte, jestli by potřebu těchto serverů hostovaných v cloudu nemohlo snížit refaktorování stávajících úloh a zajištění jejich kompatibility se zprostředkovateli cloudových identit, jako je Azure Active Directory.

### <a name="active-directory-federation-services"></a>Active Directory Federation Services

Federace identit vytváří vztahy důvěryhodnosti mezi různými systémy správy identit a umožňuje využívat společné možnosti ověřování a autorizace. V rámci vaší organizace nebo vašich systémů identit spravovaných vašimi zákazníky nebo obchodními partnery pak můžete zajistit podporu možností jednotného přihlašování napříč různými doménami.

Azure AD podporuje federaci místních domén Active Directory pomocí služby [Active Directory Federation Services](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-fed-whatis) (AD FS). Pokyny k implementaci v Azure najdete v referenční architektuře [Rozšíření služby AD FS do Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs).

## <a name="learn-more"></a>Další informace

Další informace o službách identit v Azure najdete tady:

- [Azure AD:](https://azure.microsoft.com/services/active-directory) Azure AD zajišťuje cloudové služby identit. Umožňuje spravovat přístup k prostředkům Azure a řídit správu identit, registrace zařízení, zřizování uživatelů, přístup k aplikacím a ochranu dat.
- [Azure AD Connect:](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity) Nástroj Azure AD Connect umožňuje propojit instance služby Azure AD se stávajícími řešeními pro správu identit, a tím umožnit synchronizaci stávajícího adresáře v cloudu.
- [Řízení přístupu na základě role (RBAC):](https://docs.microsoft.com/azure/role-based-access-control/overview) Azure AD zajišťuje řízení přístupu na základě role pro efektivní a bezpečnou správu přístupu k prostředkům v rovině řízení. Úlohy a povinnosti jsou uspořádané do rolí, které se přiřazují uživatelům. Řízení přístupu na základě role umožňuje řídit, kdo má přístup k jednotlivým prostředkům a jaké akce s nimi může provádět.
- [Azure AD Privileged Identity Management (PIM):](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) PIM zkracuje dobu expozice přístupových oprávnění k prostředkům a zlepšuje přehled o jejich využití prostřednictvím sestav a upozornění. Omezuje uživatele tím, že svá oprávnění můžou využívat podle potřeby, nebo přiřazováním oprávnění po kratší dobu, po které se automaticky odvolají.
- [Integrace místních domén Active Directory se službou Azure Active Directory:](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad) Tato referenční architektura obsahuje příklad synchronizace adresářů mezi místními doménami Active Directory a službou Azure AD.
- [Rozšíření služby Active Directory Domain Services (AD DS) do Azure:](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain) Tato referenční architektura obsahuje příklad nasazení serverů AD DS kvůli rozšíření doménových služeb na cloudové prostředky.
- [Rozšíření služby Active Directory Federation Services (AD FS) do Azure:](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs) V této referenční architektuře se služba Active Directory Federation Services (AD FS) nakonfiguruje tak, aby prováděla federované ověřování a autorizaci pro adresář Azure AD.

## <a name="next-steps"></a>Další kroky

Identita je pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. V [přehledu průvodců rozhodováním](../index.md) se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
