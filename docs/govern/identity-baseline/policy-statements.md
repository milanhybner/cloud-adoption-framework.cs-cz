---
title: Příkazy zásad ukázkového směrného plánu identity
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Příkazy zásad ukázkového směrného plánu identity
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 39742436ab6c4a176e40ce8188c13cca55f23521
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222127"
---
# <a name="identity-baseline-sample-policy-statements"></a>Příkazy zásad ukázkového směrného plánu identity

Jednotlivé příkazy zásad cloudu jsou pokyny pro řešení konkrétních rizik zjištěných během procesu posouzení rizik. Tyto příkazy by měly poskytnout stručné shrnutí rizik a plánů, které je třeba řešit. Každá definice příkazu by měla obsahovat tyto informace:

- **Technické riziko:** Souhrn rizika, které tato zásada bude řešit.
- **Prohlášení o zásadách:** Jasné souhrnné vysvětlení požadavků zásad.
- **Možnosti návrhu:** Užitečná doporučení, specifikace nebo další pokyny, které mohou týmy IT a vývojáři použít při implementaci těchto zásad.

Následující vzorové příkazy zásad řeší běžná obchodní rizika související s identitou. Tyto příkazy jsou příklady, na které můžete odkazovat při konceptech příkazů zásad, které řeší potřeby vaší organizace. Tyto příklady se nepovažují za podrobné a některé možnosti zásad se týkají každého identifikovaného rizika. Pracujte úzce s podnikáním a týmy IT a Identifikujte nejlepší zásady pro Vaši jedinečnou sadu rizik.

## <a name="lack-of-access-controls"></a>Nedostatek ovládacích prvků přístupu

**Technické riziko:** Nedostatečné nebo ad hoc nastavení řízení přístupu může způsobit riziko neoprávněného přístupu k citlivým nebo důležitým prostředkům.

**Prohlášení o zásadách:** Všechny prostředky nasazené do cloudu by se měly řídit pomocí identit a rolí schválených aktuálními zásadami správného řízení.

**Možné možnosti návrhu:** [Azure Active Directory podmíněný přístup](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) je výchozím mechanismem řízení přístupu v Azure.

## <a name="overprovisioned-access"></a>Zajištěný přístup

**Technické riziko:** Uživatelé a skupiny, kteří mají kontrolu nad prostředky nad rámec jejich zodpovědnosti, můžou vést k neoprávněným úpravám vedoucím k výpadkům zabezpečení nebo k ohrožení zabezpečení.

**Prohlášení o zásadách:** Implementují se tyto zásady:

- Model přístupu s minimálními oprávněními se použije na všechny prostředky, které jsou součástí důležitých aplikací nebo chráněných dat.
- Zvýšená oprávnění by měla být výjimka a jakékoli takové výjimky musí být zaznamenány pomocí týmu zásad správného řízení cloudu. Výjimky budou pravidelně auditovány.

**Možné možnosti návrhu:** Projděte si [osvědčené postupy pro správu identit Azure](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) , které implementují strategii řízení přístupu na základě rolí (RBAC), která omezuje přístup na základě [potřeb znalostních](https://wikipedia.org/wiki/Need_to_know) a [minimálních](https://wikipedia.org/wiki/Principle_of_least_privilege) principů zabezpečení.

## <a name="lack-of-shared-management-accounts-between-on-premises-and-the-cloud"></a>Nedostatek sdílených účtů pro správu mezi místním prostředím a cloudem

**Technické riziko:** Administrativní pracovníci IT nebo správci, kteří mají účty v místní službě Active Directory, nemusí mít dostatečný přístup k prostředkům cloudu, ale nemusí být schopni efektivně vyřešit provozní nebo bezpečnostní problémy.

**Prohlášení o zásadách:** Všechny skupiny v místní infrastruktuře služby Active Directory, které mají zvýšená oprávnění, by měly být namapované na schválenou roli RBAC.

**Možné možnosti návrhu:** Implementujte řešení hybridní identity mezi vaší cloudovou Azure Active Directory a místní službou Active Directory a přidejte požadované místní skupiny do rolí RBAC potřebných ke své práci.

## <a name="weak-authentication-mechanisms"></a>Slabé mechanismy ověřování

**Technické riziko:** Systémy správy identit s nedostatečným zabezpečením metod ověřování uživatele, jako jsou například základní kombinace uživatel/heslo, mohou vést k ohrožení zabezpečení nebo napadených hesel a poskytují tak zásadní riziko neoprávněného přístupu k zabezpečeným cloudovým systémům.

**Prohlášení o zásadách:** Všechny účty se vyžadují pro přihlášení k zabezpečeným prostředkům pomocí metody Multi-Factor Authentication.

**Možné možnosti návrhu:** V případě Azure Active Directory implementujte [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) jako součást procesu autorizace uživatele.

## <a name="isolated-identity-providers"></a>Izolovaní zprostředkovatelé identity

**Technické riziko:** Nekompatibilní zprostředkovatelé identity můžou mít za následek nemožnost sdílet prostředky a služby se zákazníky nebo jinými obchodními partnery.

**Prohlášení o zásadách:** Nasazení všech aplikací, které vyžadují ověřování zákazníků, musí používat schváleného poskytovatele identity, který je kompatibilní s primárním zprostředkovatelem identity pro interní uživatele.

**Možné možnosti návrhu:** Implementujte [federaci s Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed) mezi interními a zákaznickými poskytovateli identity nebo využijte [Azure Active Directory B2B](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b) .

## <a name="identity-reviews"></a>Revize identity

**Technické riziko:** V průběhu času se můžou přidáním nových cloudových nasazení a dalších otázek zabezpečení zvýšit riziko neoprávněného přístupu k zabezpečeným prostředkům.

**Prohlášení o zásadách:** Procesy zásad správného řízení cloudu musí zahrnovat čtvrtletní kontrolu s týmy správy identit k identifikaci škodlivých aktérů nebo vzorů použití, které by měly být znemožněny konfigurací cloudového prostředku.

**Možné možnosti návrhu:** Navažte čtvrtletní kontrolu zabezpečení, která zahrnuje členy týmu zásad správného řízení i pracovníky IT zodpovědné za správu služby identity. Projděte si stávající data a metriky zabezpečení a zaveďte mezery v aktuálních zásadách a nástrojích pro správu identit a aktualizujte zásady tak, aby opravily všechna nová rizika.

## <a name="next-steps"></a>Další kroky

Ukázky uvedené v tomto článku použijte jako výchozí bod pro vývoj zásad pro řešení konkrétních obchodních rizik, která odpovídají vašim plánům pro přijetí v cloudu.

Pokud chcete začít vyvíjet vlastní příkazy zásad týkající se standardních hodnot identity, Stáhněte si [šablonu směrného plánu identity](./template.md).

Pokud chcete zrychlit přijetí této disciplíny, vyberte [akčního Průvodce zásad správného řízení](../guides/index.md) , který nejlépe zarovnává vaše prostředí. Pak upravte návrh tak, aby zahrnoval konkrétní podniková rozhodnutí o zásadách.

Sestavování rizik a tolerance, zavedení procesu řízení a komunikace s dodržováním zásad standardních hodnot identity.

> [!div class="nextstepaction"]
> [Vytváření procesů dodržování zásad](./compliance-processes.md)
