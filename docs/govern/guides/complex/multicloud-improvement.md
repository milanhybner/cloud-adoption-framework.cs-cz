---
title: 'Komplexní řízení podniku: lepší řešení cloudu'
description: Rozhraní pro přijetí v cloudu pro Azure použijte k získání informací o několika cloudech a integraci více cloudových organizací pro komplexní podniky.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7fa026a06f2f42fda09783a29554e2a6c4797fcd
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434417"
---
<!-- cSpell:ignore MPLS -->

# <a name="governance-guide-for-complex-enterprises-multicloud-improvement"></a>Příručka zásad správného řízení pro komplexní podniky: lepší zlepšení cloudu

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Společnost Microsoft rozpoznává, že zákazníci mohou pro konkrétní účely přijmout více cloudů. Fiktivní společnost v tomto průvodci není žádná výjimka. Paralelně se svou cestou k přijetí Azure vedlo na úspěch firmy při získávání malého, ale doplňkového podnikání. Tato firma spouští všechny své IT operace na jiném poskytovateli cloudu.

Tento článek popisuje, jak se při integraci nové organizace mění. Pro účely mluveného komentáře předpokládáme, že tato společnost dokončila všechny iterace zásad správného řízení, které jsou uvedené v této příručce pro zásady správného řízení.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

V předchozí fázi tohoto mluveného komentáře společnost začala implementovat řízení nákladů a monitorování nákladů, protože cloudové výdaje se stávají součástí běžných provozních nákladů společnosti.

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- Identita je řízena místní instancí služby Active Directory. Hybridní identita se usnadňuje prostřednictvím replikace do Azure Active Directory.
- Provoz IT nebo cloudové operace jsou převážně spravovány Azure Monitor a souvisejícími možnostmi automatizace.
- Provozní kontinuita a zotavení po havárii (BCDR) se řídí instancemi trezoru Azure.
- Azure Security Center slouží k monitorování narušení zabezpečení a útoků.
- K monitorování zásad správného řízení cloudu se používají Azure Security Center a Azure Monitor.
- K automatizaci dodržování zásad se používají plány Azure, Azure Policy a skupiny pro správu.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Cílem je integrovat společnost společnosti akvizic do stávajících operací, kdykoli je to možné.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Náklady na pořízení firmy:** Získání nové firmy se odhadne jako ziskové za přibližně pět let. Z důvodu pomalé návratnosti si karta chce řídit náklady na pořízení, co je to možné. Existuje riziko, že řízení nákladů a technická integrace jsou v konfliktu s navzájem.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

- Existuje riziko migrace do cloudu, která vytváří další náklady na pořízení.
- Existuje také riziko, že nové prostředí se nepatřičně řídí nebo nevede k porušení zásad.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky.

- Všechny prostředky v sekundárním cloudu se musí monitorovat pomocí stávajících nástrojů pro monitorování provozní správy a zabezpečení.
- Všechny organizační jednotky musí být integrovány do existujícího poskytovatele identity.
- Primární zprostředkovatel identity by měl řídit ověřování prostředků v sekundárním cloudu.

## <a name="incremental-improvement-of-the-best-practices"></a>Přírůstkové zlepšení osvědčených postupů

Tato část článku vylepšuje návrh MVP zásad správného řízení, aby zahrnoval nové zásady Azure a implementaci Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

1. Připojte sítě. Je prováděno pomocí sítě a zabezpečení IT, které podporuje zásady správného řízení.
    1. Přidáním připojení od poskytovatele MPLS nebo pronajatého řádku do nového cloudu budou integrovány sítě. Přidávání směrovacích tabulek a konfigurací brány firewall bude řídit přístup a provoz mezi prostředími.
2. Konsolidujte zprostředkovatele identity. V závislosti na zatíženích, která se hostují v sekundárním cloudu, je k dispozici celá řada možností konsolidace zprostředkovatele identity. Tady je několik příkladů:
    1. Pro aplikace, které se ověřují pomocí OAuth 2, by se uživatelé ve službě Active Directory v sekundárním cloudu mohli jednoduše replikovat do stávajícího tenanta Azure AD.
    2. Na druhé straně federace mezi dvěma místními zprostředkovateli identity by mohli uživatelé z nových domén služby Active Directory replikovat do Azure.
3. Přidejte assety do Azure Site Recovery.
    1. Azure Site Recovery byla sestavena jako hybridní a cloudový nástroj od začátku.
    2. Virtuální počítače v sekundárním cloudu můžou být možné chránit stejnými Azure Site Recovery procesy, které se používají k ochraně místních prostředků.
4. Přidejte assety do Azure Cost Management.
    1. Azure Cost Management byla sestavena jako cloudový nástroj od začátku.
    2. Virtuální počítače v sekundárním cloudu můžou být kompatibilní s Azure Cost Management pro některé poskytovatele cloudu. Mohou platit další náklady.
5. Přidejte assety do Azure Monitor.
    1. Azure Monitor byl vytvořen jako hybridní cloudový nástroj od začátku.
    2. Virtuální počítače v sekundárním cloudu můžou být kompatibilní s agenty Azure Monitor, což umožňuje jejich zahrnutí do Azure Monitor pro monitorování provozu.
6. Nástroje pro vynucení zásad správného řízení.
    1. Vynucování zásad správného řízení je specifické pro Cloud.
    2. Podnikové zásady zřízené v příručce zásad správného řízení nejsou specifické pro Cloud. I když se implementace může od cloudu do cloudu lišit, můžete příkazy zásad použít pro sekundárního zprostředkovatele.

K nasazení v cloudu by se mělo zahrnout tam, kde je to potřeba, na základě technických potřeb nebo specifických podnikových požadavků. Vzhledem k tomu, že se nasazení s více cloudy zvětšuje, má tak složitost a bezpečnostní riziko.

## <a name="next-steps"></a>Další kroky

V mnoha velkých společnostech je pět oborů řízení cloudu, které je možné přijmout, blokovat. V dalším článku se dozvíte několik dalších nápadů týkajících se zásad správného řízení týmu sport, které vám pomůžou zajistit dlouhodobou úspěšnost v cloudu.

> [!div class="nextstepaction"]
> [Více vrstev zásad správného řízení](./multiple-layers-of-governance.md)
