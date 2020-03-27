---
title: Vylepšení oboru směrného plánu identity
description: Seznamte se s potenciálními úkoly, které společnost provádí při vývoji a zralosti směrného plánu identity v každé fázi přijímání v rámci cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 44b6c2dc910068f70645e54c372e3f4290d02669
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356996"
---
<!-- cSpell:ignore offboarding preintegration -->

# <a name="identity-baseline-discipline-improvement"></a>Vylepšení oboru směrného plánu identity

Disciplína směrného plánu identity se zaměřuje na způsoby vytváření zásad, které zajišťují konzistenci a kontinuitu identit uživatelů bez ohledu na poskytovatele cloudu, který hostuje aplikaci nebo úlohu. V pěti oborech řízení cloudu zahrnuje základní údaje o rozhodnutích, která se týkají [strategie hybridních identit](../../decision-guides/identity/index.md), vyhodnocování a rozšíření úložišť identit, implementace jednotného přihlašování (stejné přihlášení), auditování a monitorování pro neoprávněné použití nebo škodlivé objekty actor. V některých případech může také dotýkat rozhodnutí modernizovat, konsolidace nebo integrace více zprostředkovatelů identity.

Tento článek popisuje některé možné úkoly, které může vaše společnost zapojit do vývoje a vyspělosti směrného plánu identity. Tyto úlohy je možné rozdělit na plánování, sestavování, přijímání a provozní fáze implementace cloudového řešení, které se pak iterovat na to, že umožní vývoj [přírůstkového přístupu ke správě cloudu](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Čtyři fáze přijetí](../../_images/govern/adoption-phases.png)

*Obrázek 1 – fáze přijetí přírůstkového přístupu ke zásadám správného řízení cloudu.*

U každého dokumentu není možné brát v úvahu požadavky všech společností. Tento článek popisuje navrhované minimální a potenciální příklady aktivit pro každou fázi procesu maturation zásad správného řízení. Počáteční cíl těchto aktivit vám pomůže vytvořit [MVP pro zásady](../guides/index.md#an-incremental-approach-to-cloud-governance) a vytvořit rozhraní pro přírůstkové zlepšování zásad. Váš tým zásad správného řízení vašeho cloudu bude muset rozhodnout, kolik z nich investovat do těchto aktivit, aby vylepšili možnosti zásad správného řízení vaší identity.

> [!CAUTION]
> Minimální ani potenciální aktivity, které jsou uvedené v tomto článku, jsou zarovnané na konkrétní podnikové zásady nebo požadavky na dodržování předpisů třetích stran. Tento návod je navržený tak, aby usnadnil konverzace, které vedou k vyrovnání obou požadavků s modelem zásad správného řízení pro Cloud.

## <a name="planning-and-readiness"></a>Plánování a připravenost

Tato fáze předběžných postupů řízení vypořádání mostů mezi obchodními výsledky a strategiemi, které se s nimi možné. Během tohoto procesu vedoucí týmu definuje konkrétní metriky, mapuje tyto metriky na digitální nemovitosti a zahájí plánování celkové snahy o migraci.

**Minimální navrhované aktivity:**

- Vyhodnoťte možnosti vaší [identity sada nástrojů](./toolchain.md) a implementujte hybridní strategii, která je vhodná pro vaši organizaci.
- Vývoj konceptu pokynů k architektuře a distribuce pro klíčové účastníky
- Informujte a zapojte lidi a týmy, kterých se týkalo vývoje pokynů pro architekturu.

**Potenciální aktivity:**

- Definujte role a přiřazení, které budou řídit správu identit a přístupu v cloudu.
- Definujte místní skupiny a namapujte je na odpovídající cloudové role.
- Poskytovatelé identit inventáře (včetně identit řízených databází používaných vlastními aplikacemi).
- Konsolidujte a integrujte zprostředkovatele identity tam, kde duplicity existují, abyste zjednodušili celkové řešení identit a snížili rizika.
- Vyhodnoťte hybridní kompatibilitu stávajících zprostředkovatelů identity.
- Pro zprostředkovatele identity, kteří nejsou kompatibilní s hybridem, vyhodnoťte možnosti konsolidace nebo nahrazení.

## <a name="build-and-predeployment"></a>Sestavení a přednasazení

K úspěšné migraci prostředí je nutné provést několik technických a netechnických požadavků. Tento proces se zaměřuje na rozhodování, připravenost a základní infrastrukturu, která pokračuje v migraci.

**Minimální navrhované aktivity:**

- Před implementací [Sada nástrojů identity](./toolchain.md)zvažte pilotní test a ujistěte se, že zjednodušuje uživatelské prostředí co nejvíc.
- Použijte zpětnou vazbu z pilotních testů do přednasazení. Opakujte, dokud nebudou přijatelné výsledky.
- Aktualizujte dokument s pokyny pro architekturu tak, aby zahrnoval plány nasazení a přijetí uživatelů a distribuovat do klíčových účastníků.
- Zvažte vytvoření programu na začátku a zavedení do omezeného počtu uživatelů.
- Pokračujte ve vzdělávání lidí a týmů, které jsou ovlivněny pokyny pro architekturu.

**Potenciální aktivity:**

- Vyhodnoťte svou logickou a fyzickou architekturu a určete [strategii hybridních identit](../../decision-guides/identity/index.md).
- Namapujte zásady správy přístupu k identitám, jako je přiřazení ID přihlášení, a vyberte vhodnou metodu ověřování pro Azure AD.
  - V případě federovaného povolte omezení tenanta pro účty správců.
- Integrujte své místní a cloudové adresáře.
- Zvažte použití následujících přístupových modelů:
  - Model [přístupu s minimálními oprávněními](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models) .
  - Model přístupu [podle směrného plánu privilegované identity](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) .
- Dokončete všechny podrobnosti o předintegraci a Projděte si [osvědčené postupy pro identitu](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices).
  - Povolte jedinou identitu, jednotné přihlašování (SSO) nebo bezproblémové jednotné přihlašování.
  - Nakonfigurujte službu Multi-Factor Authentication pro správce.
  - Konsolidujte nebo integrujte zprostředkovatele identity, pokud je to potřeba.
  - Implementujte nástroje potřebné k centralizaci správy identit.
  - Povolení přístupu JIT (just-in-time) a výstrahy změny role.
  - Proveďte analýzu rizik pro aktivity Správce klíčů pro přiřazení k předdefinovaným rolím.
  - Vezměte v úvahu aktualizované zavedení silnějšího ověřování pro všechny uživatele.
  - Pro další administrativní role povolte privilegovanou identitu (PIM) pro JIT (s použitím časově omezené aktivace).
  - Oddělte uživatelské účty z účtů globálních správců (abyste se ujistili, že správci nechtěně neotevřou e-maily nebo nespouštějí programy přidružené k účtům globálních správců).

## <a name="adopt-and-migrate"></a>Přijmout a migrovat

Migrace je přírůstkový proces, který se zaměřuje na přesun, testování a přijetí aplikací nebo úloh v existující digitální nemovitosti.

**Minimální navrhované aktivity:**

- Migrujte své [Sada nástrojů identity](./toolchain.md) z vývoje do produkčního prostředí.
- Aktualizujte dokument s pokyny pro architekturu a distribuujte je klíčovým stranám.
- Vývoj vzdělávacích materiálů a dokumentace, povědomí o komunikaci, pobídek a dalších programech, které vám pomůžou při přijímání uživatelů

**Potenciální aktivity:**

- Ověřte, zda jsou osvědčené postupy definované během fází předsazování sestavení správně provedeny.
- Ověřte a upřesněte [strategii hybridních identit](../../decision-guides/identity/index.md).
- Zajistěte, aby každá aplikace nebo úloha dál odpovídaly strategii identity před vydáním.
- Ověřte, že jednotné přihlašování (SSO) a bezproblémové jednotné přihlašování fungují podle očekávání pro vaše aplikace.
- Snižte nebo eliminujte počet alternativních úložišť identit.
- Posoudí nutnost jakéhokoli úložiště identity v aplikaci nebo v databázi. Identity, které spadají mimo správného poskytovatele identity (první strana nebo třetí strana), můžou představovat riziko pro aplikaci a uživatele.
- Povolte podmíněný přístup pro [místní federované aplikace](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup).
- Distribuujte identitu napříč globálními oblastmi v několika centrech pomocí synchronizace mezi oblastmi.
- Zřídí federaci centrálního řízení přístupu na základě role (RBAC).

## <a name="operate-and-post-implementation"></a>Provoz a následné implementace

Po dokončení transformace musí být zásady správného řízení a provoz v provozu v rámci přirozeného životního cyklu aplikace nebo zátěže. Tato fáze řízení splatnosti se zaměřuje na aktivity, které se běžně přidávají po implementaci řešení, a cyklus transformace začíná stabilizovat.

**Minimální navrhované aktivity:**

- Přizpůsobte si [Sada nástrojů své identity](./toolchain.md) podle změn potřeb vaší organizace na změnu identity.
- Automatizujte oznámení a sestavy, které vám upozorní na potenciální škodlivé hrozby.
- Monitorování a hlášení o využití systému a průběhu přijímání uživatelů
- Ohlaste metriky po nasazení a distribuujte je účastníkům.
- Upřesněte pokyny k architektuře a provedou budoucí procesy přijímání.
- Pravidelně komunikujte a průběžně informujte s ovlivněnými týmy, aby se zajistilo průběžné dodržování pravidel architektury.

**Potenciální aktivity:**

- Provádějte pravidelné audity zásad identity a postupů dodržování předpisů.
- Zajistěte, aby u citlivých uživatelských účtů (například účtů vedoucích společnosti) byla vždy povolená aplikace Multi-Factor Authentication a neobvyklé rozpoznávání přihlášení.
- Pravidelně kontrolují škodlivé objekty actor a porušení dat, zejména těch, které se týkají podvodů s totožností, jako je například potenciální převzetí účtu správce.
- Nakonfigurujte Nástroj pro monitorování a vytváření sestav.
- Zvažte lepší integraci se zabezpečením a systémy ochrany před podvody.
- Pravidelně kontrolujte přístupová práva pro uživatele nebo role se zvýšenými oprávněními.
  - Identifikujte každého uživatele, který má nárok na aktivaci oprávnění správce.
- Projděte si procesy registrace, zrušení a aktualizace přihlašovacích údajů.
- Prozkoumejte zvýšené úrovně automatizace a komunikace mezi moduly správy přístupu identit (IAM).
- Zvažte implementaci přístupu k operacím vývojového zabezpečení (DevSecOps).
- Proveďte analýzu dopadů k posouzení výsledků na náklady, zabezpečení a přijetí uživatelů.
- Pravidelně vytváří zprávu o dopadu, která zobrazuje změny metriky vytvořené systémem a odhad obchodních dopadů [strategie hybridních identit](../../decision-guides/identity/index.md).
- Navázat integrované monitorování, které doporučuje [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro).

## <a name="next-steps"></a>Další kroky

Teď, když rozumíte konceptu zásad správného řízení identity v cloudu, Projděte si [základní sada nástrojů identity](./toolchain.md) a Identifikujte nástroje a funkce Azure, které budete potřebovat při vývoji pravidel zásad správného řízení identity na platformě Azure.

> [!div class="nextstepaction"]
> [Sada nástrojů úrovně identity pro Azure](./toolchain.md)
