---
title: 'Standardní zásady správného řízení podniku: lepší řešení cloudu'
description: Rozhraní pro přijetí v cloudu pro Azure použijte k získání informací o několika cloudech a o tom, jak integrovat více cloudů do existujících operací.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a83e2b8a0892e216106890e0bed0066be527e974
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709256"
---
# <a name="standard-enterprise-governance-guide-multicloud-improvement"></a>Standardní příručka pro zásady správného řízení podniku: zlepšení cloudu

Tento článek popisuje mluvený komentář přidáním ovládacích prvků pro nasazení s více cloudy.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Společnost Microsoft rozpoznává, že zákazníci mohou pro konkrétní účely přijmout více cloudů. Fiktivní zákazník v tomto průvodci není výjimkou. Paralelně se svou cestou k přijetí Azure vedlo na úspěch firmy při získávání malého, ale doplňkového podnikání. Tato firma spouští všechny své IT operace na jiném poskytovateli cloudu.

Tento článek popisuje, jak se při integraci nové organizace mění. Pro účely mluveného komentáře předpokládáme, že tato společnost dokončila všechny iterace zásad správného řízení, které jsou uvedené v této příručce pro zásady správného řízení.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

V předchozí fázi tohoto mluveného komentáře společnost začala aktivně předávat produkční aplikace do cloudu prostřednictvím kanálů CI/CD.

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- Identita je řízena místní instancí služby Active Directory. Hybridní identita se usnadňuje prostřednictvím replikace do Azure Active Directory.
- Provoz IT nebo cloudové operace jsou převážně spravovány Azure Monitor a souvisejícími automatizacemi.
- Zotavení po havárii a kontinuitu podnikových aplikací řídí instance služby Azure trezor.
- Azure Security Center slouží k monitorování narušení zabezpečení a útoků.
- K monitorování zásad správného řízení cloudu se používají Azure Security Center a Azure Monitor.
- K automatizaci dodržování zásad se používají plány Azure, Azure Policy a skupiny pro správu Azure.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Cílem je integrovat společnost společnosti akvizic do stávajících operací, kdykoli je to možné.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Náklady na pořízení firmy:** Získání nové firmy se odhadne jako ziskové za přibližně pět let. Z důvodu pomalé návratnosti si karta chce řídit náklady na pořízení, co je to možné. Existuje riziko, že řízení nákladů a technická integrace jsou v konfliktu s navzájem.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

- Migrace do cloudu může způsobit další náklady na pořízení.
- Nové prostředí se nemusí správně řídit, což by mohlo vést k porušení zásad.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci Průvodce:

- Všechny prostředky v sekundárním cloudu se musí monitorovat pomocí stávajících nástrojů pro monitorování provozní správy a zabezpečení.
- Všechny organizační jednotky musí být integrovány do existujícího poskytovatele identity.
- Primární zprostředkovatel identity by měl řídit ověřování prostředků v sekundárním cloudu.

## <a name="incremental-improvement-of-governance-practices"></a>Postupné vylepšování postupů správného řízení

V této části článku se změní návrh MVP zásad správného řízení tak, aby zahrnoval nové zásady Azure a implementaci Azure Cost Management. Tyto změny návrhu společně budou plnit nové příkazy podnikové zásady.

1. Připojte sítě. Tento krok provádí sítě a týmy zabezpečení IT a podporuje tým zásad správného řízení pro Cloud. Přidáním připojení od poskytovatele MPLS/pronajatého řádku do nového cloudu budou integrovány sítě. Přidávání směrovacích tabulek a konfigurací brány firewall bude řídit přístup a provoz mezi prostředími.
2. Konsolidujte zprostředkovatele identity. V závislosti na zatíženích, která se hostují v sekundárním cloudu, je k dispozici celá řada možností konsolidace zprostředkovatele identity. Tady je několik příkladů:
    1. Pro aplikace, které se ověřují pomocí OAuth 2, je možné uživatele ze služby Active Directory v sekundárním cloudu jednoduše replikovat do stávajícího tenanta Azure AD. Tím se zajistí, že všichni uživatelé můžou být ověření v tenantovi.
    2. V druhé extrémní federaci umožňuje organizačním jednotkám tok do služby Active Directory místně a následně do instance služby Azure AD.
3. Přidejte assety do Azure Site Recovery.
    1. Azure Site Recovery byla navržena od začátku jako hybridní nebo cloudový nástroj.
    2. Virtuální počítače v sekundárním cloudu můžou být možné chránit stejnými Azure Site Recovery procesy, které slouží k ochraně místních prostředků.
4. Přidejte assety do Azure Cost Management.
    1. Azure Cost Management byla navržena od začátku jako pro cloudový nástroj.
    2. Virtuální počítače v sekundárním cloudu můžou být kompatibilní s Azure Cost Management pro některé poskytovatele cloudu. Mohou platit další náklady.
5. Přidejte assety do Azure Monitor.
    1. Azure Monitor byla navržena jako hybridní cloudový nástroj od zahájení.
    2. Virtuální počítače v sekundárním cloudu můžou být kompatibilní s agenty Azure Monitor, což umožňuje jejich zahrnutí do Azure Monitor pro monitorování provozu.
6. Přijmout nástroje vynucení zásad správného řízení.
    1. Vynucování zásad správného řízení je specifické pro Cloud.
    2. Podnikové zásady zřízené v příručce zásad správného řízení nejsou specifické pro Cloud. I když se implementace může od cloudu do cloudu lišit, zásady je možné použít u sekundárního zprostředkovatele.

K nasazení v cloudu by se mělo zahrnout tam, kde je to potřeba, na základě technických potřeb nebo specifických podnikových požadavků. Vzhledem k tomu, že se nasazení s více cloudy zvětšuje, má tak složitost a bezpečnostní riziko.

## <a name="conclusion"></a>Závěr

Tato série článků popisuje přírůstkový vývoj osvědčených postupů zásad správného řízení, které jsou v souladu se zkušenostmi této fiktivní společnosti. Od začátku malého, ale s pravou základem, může se společnost rychle přesunout a zároveň použít správnou úroveň správného řízení ve správný čas. MVP sám o sobě nechránil zákazníka. Místo toho vytvořil základ pro správu rizik a přidání ochrany. Odtud jsou k dispozici vrstvy zásad správného řízení, které by opravily hmotná rizika. Přesná cesta, která je zde uvedena, nebude zarovnávat 100% s prostředími všech čtenářů. Místo toho slouží jako vzor pro přírůstkové řízení. Tyto osvědčené postupy byste měli tvarovat, abyste vyhovovali vlastním jedinečným omezením a požadavkům zásad správného řízení.
