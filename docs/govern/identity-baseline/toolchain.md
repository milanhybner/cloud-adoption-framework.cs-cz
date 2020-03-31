---
title: Nástroje pro základní identitu identity v Azure
description: Podívejte se, jak můžou Azure Native Tools pomoci při vyspělých zásadách a procesech, které podporují obor zásad správného řízení identity.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 368d2811bb54ef373be8df036d96452023891b83
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434959"
---
# <a name="identity-baseline-tools-in-azure"></a>Nástroje pro základní identitu identity v Azure

[Standardní hodnota identity](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na způsoby vytváření zásad, které zajišťují konzistenci a kontinuitu identit uživatelů bez ohledu na poskytovatele cloudu, který hostuje aplikaci nebo úlohu.

V průvodci zjišťováním pro hybridní identitu jsou k dispozici následující nástroje.

**Služba Active Directory (místní):** Active Directory je poskytovatel identity, který se nejčastěji používá v podniku k ukládání a ověřování přihlašovacích údajů uživatele.

**Azure Active Directory:** Software jako služba (SaaS) ekvivalentní službě Active Directory, která je schopná federování s místní službou Active Directory.

**Služba Active Directory (IaaS):** Instance aplikace Active Directory běžící na virtuálním počítači v Azure.

Identita je řídicí rovinou pro zabezpečení IT. Ověřování je tedy ochrana přístupu ke cloudu v organizaci. Organizace potřebují rovinu řízení identit, která posílí jejich zabezpečení a udržuje jejich cloudové aplikace v bezpečí před narušiteli.

## <a name="cloud-authentication"></a>Cloudové ověřování

Výběr správné metody ověřování je první záležitost, kterou organizace chtějí přesunout své aplikace do cloudu.

Když zvolíte tuto metodu, Azure AD bude zpracovávat přihlašovací proces uživatelů. V kombinaci s bezproblémové jednotné přihlašování (SSO) se uživatelé můžou přihlašovat ke cloudovým aplikacím bez nutnosti opětovného zadání přihlašovacích údajů. Pomocí cloudového ověřování si můžete vybrat ze dvou možností:

**Synchronizace hodnot hash hesel Azure AD:** Nejjednodušší způsob, jak povolit ověřování pro místní adresářové objekty ve službě Azure AD. Tuto metodu můžete také použít s libovolnou metodou jako záložní metodu ověřování převzetí služeb při selhání v případě, že váš místní server přestane být funkční.

**Předávací ověřování Azure AD:** Poskytuje trvalé ověřování hesla pro služby ověřování Azure AD pomocí softwarového agenta, který běží na jednom nebo několika místních serverech.

> [!NOTE]
> Společnosti, které mají požadavek na zabezpečení hned za účelem okamžitého vymáhání místních stavů uživatelských účtů, zásad hesel a hodin přihlášení, by měly vzít v úvahu metodu předávacího ověřování.

**Federované ověřování:**

Když si zvolíte tuto metodu, Azure AD předá proces ověřování samostatnému systému ověřování, jako je místní Active Directory Federation Services (AD FS) (AD FS) nebo poskytovatel federačních třetích stran, aby ověřil heslo uživatele.

Článek [Výběr správné metody ověřování pro Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn) obsahuje rozhodovací strom, který vám umožní vybrat nejlepší řešení pro vaši organizaci.

Následující tabulka obsahuje seznam nativních nástrojů, které mohou pomoci při vyspělosti zásad a procesů, které podporují tento obor řízení.

<!-- markdownlint-disable MD033 -->

|Aspekty|Synchronizace hodnot hash hesel + bezproblémové jednotné přihlašování|Předávací ověřování + bezproblémové jednotné přihlašování|Federace se službou AD FS|
|:-----|:-----|:-----|:-----|
|Kde k ověřování dochází?|V cloudu|V cloudu po výměně zabezpečeného ověřování hesla pomocí místního ověřovacího agenta|Lokálně|
|Jaké jsou požadavky na místní server nad rámec zřizovacího systému: Azure AD Connect?|Žádná|Jeden server pro každého dalšího ověřovacího agenta|Dva nebo více AD FS serverů<br><br>Dva nebo více serverů WAP v hraniční/DMZ síti|
|Jaké jsou požadavky na místní Internet a sítě mimo zřizovací systém?|Žádná|[Odchozí internetový přístup](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-quick-start) ze serverů používajících ověřovací agenty|[Příchozí internetový přístup](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/ad-fs-requirements) k serverům WAP v hraniční síti<br><br>Příchozí síťový přístup k serverům AD FS ze serverů WAP v hraniční síti<br><br>Vyrovnávání zatížení sítě|
|Existuje požadavek na certifikát SSL?|Ne|Ne|Ano|
|Existuje nějaké řešení pro monitorování stavu?|Nepožadováno|Stav agenta poskytnutý [centrem pro správu Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication)|[Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)|
|Přihlašuje uživatelé k prostředkům cloudu jednotné přihlašování ze zařízení připojených k doméně v podnikové síti?|Ano, [bez problémů s jednotným PŘIhlašováním](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Ano, [bez problémů s jednotným PŘIhlašováním](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Ano|
|Jaké typy přihlašování se podporují?|UserPrincipalName + heslo<br><br>Integrované ověřování systému Windows pomocí [bezproblémového jednotného PŘIhlašování](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Alternativní ID přihlášení](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-custom)|UserPrincipalName + heslo<br><br>Integrované ověřování systému Windows pomocí [bezproblémového jednotného PŘIhlašování](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Alternativní ID přihlášení](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-faq)|UserPrincipalName + heslo<br><br>sAMAccountName + heslo<br><br>Integrované ověřování systému Windows<br><br>[Ověřování pomocí certifikátu a čipové karty](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication)<br><br>[Alternativní ID přihlášení](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)|
|Podporuje se Windows Hello pro firmy?|[Klíčový model vztahu důvěryhodnosti](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Model důvěryhodnosti certifikátu s Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Klíčový model vztahu důvěryhodnosti](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Model důvěryhodnosti certifikátu s Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Klíčový model vztahu důvěryhodnosti](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Model vztahu důvěryhodnosti certifikátu](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs)|
|Jaké možnosti Multi-Factor Authentication?|[Multi-Factor Authentication Azure](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Vlastní ovládací prvky s podmíněným přístupem *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Multi-Factor Authentication Azure](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Vlastní ovládací prvky s podmíněným přístupem *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Multi-Factor Authentication Azure](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Server Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfaserver-deploy)<br><br>[Multi-Factor Authentication třetí strany](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)<br><br>[Vlastní ovládací prvky s podmíněným přístupem *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|
|Jaké stavy uživatelských účtů se podporují?|Zakázané účty<br>(až 30 minut zpoždění)|Zakázané účty<br><br>Účet uzamčen<br><br>Platnost účtu vypršela.<br><br>Platnost hesla vypršela.<br><br>Přihlašovací hodiny|Zakázané účty<br><br>Účet uzamčen<br><br>Platnost účtu vypršela.<br><br>Platnost hesla vypršela.<br><br>Přihlašovací hodiny|
|Jaké jsou možnosti podmíněného přístupu?|[Podmíněný přístup Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Podmíněný přístup Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Podmíněný přístup Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)<br><br>[AD FS pravidla deklarace identity](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator)|
|Je podporováno blokování starších verzí protokolů?|[Ano](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Ano](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Ano](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/access-control-policies-w2k12)|
|Můžete přizpůsobit logo, obrázek a popis na přihlašovacích stránkách?|[Ano, s Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Ano, s Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Ano](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#customlogo)|
|Jaké pokročilé scénáře jsou podporovány?|[Inteligentní uzamčení hesla](https://docs.microsoft.com/azure/active-directory/active-directory-secure-passwords)<br><br>[Nevrácené sestavy pověření](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events)|[Inteligentní uzamčení hesla](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-smart-lockout)|Systém ověřování s nízkou latencí ve více lokalitách<br><br>[AD FS uzamčení extranetu](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection)<br><br>[Integrace se systémy identit třetích stran](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-compatibility)|

<!-- markdownlint-enable MD033 -->

> [!NOTE]
> Vlastní ovládací prvky ve službě Azure AD podmíněný přístup aktuálně nepodporují registraci zařízení.

## <a name="next-steps"></a>Další kroky

Dokument [White paper k rozhraní Digital Transforming pro hybridní identitu](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html) popisuje kombinace a řešení pro výběr a integraci každé z těchto součástí.

[Nástroj Azure AD Connect](https://aka.ms/aadconnectwiz) vám pomůže integrovat místní adresáře do služby Azure AD.
