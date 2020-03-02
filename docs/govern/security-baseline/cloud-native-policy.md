---
title: Základní zásady zabezpečení pro Cloud – nativní
description: Podívejte se na ukázkovou nativní cloudovou zásadu pro směrný plán zabezpečení, ve kterém jsou nástroje a platformy Azure dostačující ke správě obchodních rizik.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ce5b1a77396479b2621afab5cac025b983f14469
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223739"
---
# <a name="cloud-native-security-baseline-policy"></a>Základní zásady zabezpečení pro Cloud – nativní

[Základní úroveň zabezpečení](./index.md) je jedním z [pěti oborů zásad správného řízení cloudu](../governance-disciplines.md). Tato disciplína se zaměřuje na obecná témata zabezpečení, včetně ochrany sítě, digitálních prostředků, dat atd. Jak je uvedeno v příručce pro [kontrolu zásad](../policy-compliance/cloud-policy-review.md), rozhraní pro přijetí do cloudu zahrnuje tři úrovně vzorových zásad: cloudové nativní, podnikové a cloudové zásady pro jednotlivé obory. Tento článek popisuje ukázkovou zásadu cloudového nativního řešení pro základnu standardních hodnot zabezpečení.

> [!NOTE]
> Společnost Microsoft není k dispozici pro diktování podnikových nebo firemních zásad. Tento článek vám pomůže připravit se na interní kontrolu zásad. Před pokusem o její použití se předpokládá, že tyto ukázkové zásady budou rozšířeny, ověřeny a testovány proti podnikovým zásadám. Nedoporučuje se používat Tato vzorová zásada jako.

## <a name="policy-alignment"></a>Zarovnání zásad

Tato ukázková zásada syntetizuje scénář cloudového nativního řešení, což znamená, že nástroje a platformy, které Azure poskytuje, jsou dostačující ke správě obchodních rizik, která se podílejí na nasazení. V tomto scénáři se předpokládá, že jednoduchá konfigurace výchozích služeb Azure zajišťuje dostatečnou ochranu prostředků.

## <a name="cloud-security-and-compliance"></a>Zabezpečení a dodržování předpisů v cloudu

Zabezpečení je integrované do všech aspektů Azure a nabízí jedinečné výhody zabezpečení odvozené z globálních nástrojů pro zabezpečení, sofistikované ovládací prvky zaměřené na zákazníky a zabezpečenou a posílenou infrastrukturou. Tato účinná kombinace pomáhá chránit vaše aplikace a data, podporuje snahu o dodržování předpisů a poskytuje nákladově efektivní zabezpečení pro organizace všech velikostí. Tento přístup vytvoří silnou počáteční pozici pro jakékoli zásady zabezpečení, ale neočekává se, že se neshodují stejně silné postupy zabezpečení související s používanými službami zabezpečení.

### <a name="built-in-security-controls"></a>Integrované ovládací prvky zabezpečení

Je těžké udržovat silnou bezpečnostní infrastrukturu, když ovládací prvky zabezpečení nejsou intuitivní a je nutné je nakonfigurovat samostatně. Azure obsahuje integrované bezpečnostní prvky pro celou řadu služeb, které vám pomůžou rychle chránit data a úlohy a spravovat rizika napříč hybridními prostředími. Integrovaná Partnerská řešení také umožňují snadno převést stávající ochranu do cloudu.

### <a name="cloud-native-identity-policies"></a>Cloud – nativní zásady identity

Identita se stává novou rovinou ovládacího prvku hranice pro zabezpečení a přebírá tuto roli z tradiční perspektivy zaměřené na síť. Hraniční sítě se staly stále Porous a tato ochrana hraničních přenosů nemůže být tak efektivní, protože byla předtím, než nástupem Přineste vlastní zařízení (BYOD) a cloudové aplikace. Správa identit a řízení přístupu v Azure umožňuje bezproblémový a zabezpečený přístup ke všem vašim aplikacím.

Ukázková nativní zásada cloudu pro identitu napříč cloudem a místními adresáři může zahrnovat požadavky podobné následujícímu:

- Autorizovaný přístup k prostředkům s řízením přístupu na základě role (RBAC), Multi-Factor Authentication a jednotným přihlašováním (SSO).
- Rychlé zmírnění identity uživatelů podezřelých z ohrožení.
- Just-in-time (JIT), stačí mít k dispozici dostatečný přístup na základě úkolů, který omezí riziko ohrožení pověření správce s překročenou úrovní oprávnění.
- Rozšířená identita uživatelů a přístup k zásadám v rámci více prostředí prostřednictvím Azure Active Directory.

I když je důležité porozumět [směrnému plánu identity](../identity-baseline/index.md) v souvislosti s směrným plánem zabezpečení, [pět oborů zásad správného řízení cloudu](../index.md) volá stejnou [úroveň identity](../identity-baseline/index.md) jako svůj vlastní obor a liší se od standardních hodnot zabezpečení.

### <a name="network-access-policies"></a>Zásady přístupu k síti

Řízení sítě zahrnuje konfiguraci, správu a zabezpečení síťových prvků, jako jsou virtuální sítě, Vyrovnávání zatížení, DNS a brány. Ovládací prvky poskytují služby pro komunikaci a spolupráci. Azure zahrnuje robustní a zabezpečenou síťovou infrastrukturu pro podporu požadavků vaší aplikace a připojení služby. Mezi prostředky umístěnými v Azure, mezi místními a hostovanými prostředky Azure a a z Internetu a Azure se může připojit k síti.

Zásady nativní pro Cloud pro síťové ovládací prvky mohou zahrnovat požadavky podobné následujícímu:

- Hybridní připojení k místním prostředkům se nemusí v zásadách nativního cloudu povolit. V případě potřeby se hybridní připojení ukáže jako nezbytné, což je robustnější ukázka zásad zabezpečení společnosti.
- Uživatelé mohou vytvořit zabezpečená připojení k a v rámci Azure pomocí virtuálních sítí a skupin zabezpečení sítě.
- Nativní Windows Azure Firewall chrání hostitele před škodlivým síťovým provozem pomocí omezeného přístupu k portu. Dobrým příkladem těchto zásad je požadavek na blokování (nebo nepovolení) přenosu přímo do virtuálního počítače přes SSH/RDP.
- Služby, jako jsou Firewall webových aplikací Application Gateway Azure (WAF) a Azure DDoS Protection chrání aplikace a zajišťují dostupnost virtuálních počítačů spuštěných v Azure. Tyto funkce by neměly být zakázány.

### <a name="data-protection"></a>Ochrana dat

Jedním z klíčů k ochraně dat v cloudu je monitorování účtů možných stavů, ve kterých můžou být vaše data, a to, jaké ovládací prvky jsou k dispozici pro jednotlivé stavy. Pro účely osvědčených postupů zabezpečení a šifrování dat Azure se zaměřte na následující stavy dat:

- Ovládací prvky šifrování dat jsou integrované do služeb z virtuálních počítačů do úložiště a SQL Database.
- Vzhledem k tomu, že se data mezi cloudy a zákazníky pohybují, můžou být chráněná pomocí standardních šifrovacích protokolů.
- Azure Key Vault umožňuje uživatelům chránit a řídit kryptografické klíče, hesla, připojovací řetězce a certifikáty používané v cloudových aplikacích a službách.
- Azure Information Protection vám pomůže klasifikovat, označovat a chránit citlivá data v aplikacích.

I když jsou tyto funkce integrované do Azure, každá z nich vyžaduje konfiguraci a může zvýšit náklady. Důrazně se navrhuje zarovnání jednotlivých funkcí nativního cloudu s [strategií klasifikace dat](../policy-compliance/data-classification.md) .

### <a name="security-monitoring"></a>Monitorování zabezpečení

Sledování zabezpečení je proaktivní strategie, která Audituje vaše prostředky k identifikaci systémů, které nesplňují standardy organizace ani osvědčené postupy. Azure Security Center poskytuje jednotné základní hodnoty zabezpečení a pokročilou ochranu před hrozbami napříč hybridními cloudových úlohami. Pomocí Security Center můžete použít zásady zabezpečení napříč vašimi úlohami, omezit vystavení hrozbám a rozpoznávat a reagovat na útoky, včetně těchto:

- Jednotné zobrazení zabezpečení napříč všemi místními i cloudovou úlohou pomocí Azure Security Center.
- Průběžné monitorování a posuzování zabezpečení pro zajištění dodržování předpisů a nápravy jakýchkoli ohrožení zabezpečení.
- Interaktivní nástroje a kontextová analýza hrozeb pro zjednodušené šetření.
- Rozsáhlé protokolování a integrace s existujícími informacemi o zabezpečení
- Omezuje potřebu nákladných, neintegrovaných a odstraněných řešení zabezpečení.

### <a name="extending-cloud-native-policies"></a>Rozšíření zásad nativních pro Cloud

Používání cloudu může snížit některé z bezpečnostních břemen. Microsoft poskytuje fyzické zabezpečení pro datacentra Azure a pomáhá chránit cloudovou platformu proti hrozbám infrastruktury, jako je DDoS útok. Vzhledem k tomu, že společnost Microsoft má každý den tisíce kyberbezpečnosti specialistů pracujících na zabezpečení, jsou prostředky pro detekci, prevenci a zmírnění kyberútokům značné. I když se organizace použily pro starosti s tím, že Cloud byl zabezpečený, nejvíc teď chápe, že úroveň investic v lidech a specializované infrastruktuře od dodavatelů, jako je Microsoft, vede k bezpečnějšímu zabezpečení cloudu než většina místních datových center.
Používání cloudu může snížit některé z bezpečnostních břemen. Microsoft poskytuje fyzické zabezpečení pro datacentra Azure a pomáhá chránit cloudovou platformu proti hrozbám infrastruktury, jako je DDoS útok. Vzhledem k tomu, že společnost Microsoft má každý den tisíce kyberbezpečnosti specialistů pracujících na zabezpečení, jsou prostředky pro detekci, prevenci a zmírnění kyberútokům značné. I když se organizace použily pro starosti s tím, že Cloud byl zabezpečený, nejvíc teď chápe, že úroveň investic v lidech a specializované infrastruktuře od dodavatelů, jako je Microsoft, vede k bezpečnějšímu zabezpečení cloudu než většina místních datových center.

I v případě této investice do nativního směrného plánu zabezpečení v cloudu doporučujeme, aby všechny zásady standardních hodnot zabezpečení rozšířily výchozí zásady cloudu Native. Následují příklady rozšířených zásad, které je vhodné zvážit, i v cloudovém nativním prostředí:

- **Zabezpečte virtuální počítače.** Zabezpečení by měla být nejvyšší prioritou každé organizace a její efektivita vyžaduje několik věcí. Musíte vyhodnotit stav zabezpečení, chránit před bezpečnostními hrozbami a pak rychle detekovat a reagovat na hrozby, ke kterým dojde.
- **Ochrana obsahu virtuálního počítače.** Nastavení pravidelných automatizovaných záloh je nezbytné pro ochranu před chybami uživatelů. To ještě není dost, ale; musíte se také ujistit, že vaše zálohy jsou bezpečné z kyberútokům a jsou dostupné, když je potřebujete.
- **Monitorujte aplikace.** Tento model zahrnuje několik úloh, včetně přehledu o stavu vašich virtuálních počítačů, porozumění interakcím mezi nimi a vytváření způsobů monitorování aplikací, které tyto virtuální počítače spouštějí. Všechny tyto úlohy jsou nezbytné v případě, že vaše aplikace běží kolem času.
- **Zabezpečení a audit přístupu k datům.** Organizace by měly auditovat veškerý přístup k datům a využívat pokročilé možnosti strojového učení a volat odchylky od běžných vzorů přístupu.
- **Postup převzetí služeb při selhání.** Cloudové operace s nízkou odolností proti chybám musí být schopné převzít služby při selhání nebo obnovení z kyberbezpečnosti nebo incidentu platformy. Tyto postupy se nesmí jednoduše zdokumentovat, ale měly by se procvičit čtvrtletně.

## <a name="next-steps"></a>Další kroky

Teď, když jste si [prohlédli](../policy-compliance/cloud-policy-review.md) ukázkovou zásadu standardních hodnot zabezpečení pro nativní cloudová řešení, se vraťte do průvodce pro kontrolu zásad, kde můžete začít sestavovat v této ukázce, abyste mohli vytvořit vlastní zásady pro přijetí do cloudu.

> [!div class="nextstepaction"]
> [Sestavování vlastních zásad pomocí Průvodce kontrolou zásad](../policy-compliance/cloud-policy-review.md)
