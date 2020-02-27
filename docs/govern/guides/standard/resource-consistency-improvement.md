---
title: 'Standardní zásady správného řízení podniku: vylepšení konzistence prostředků'
description: Rozhraní pro přijetí v cloudu pro Azure vám umožní získat informace o vylepšení standardních hodnot zásad správného řízení a oprava rizik přidáním ovládacích prvků pro obnovení, změnu velikosti a monitorování.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e50d3e258a4b040d1f9cfaa1b274ed977c49b14d
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709103"
---
# <a name="standard-enterprise-governance-guide-improving-resource-consistency"></a>Standardní příručka pro zásady správného řízení podniku: vylepšení konzistence prostředků

Tento článek popisuje mluvený komentář přidáním ovládacích prvků konzistence prostředků, které budou podporovat klíčové aplikace.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Nová prostředí pro zákazníky, nové předpovědi nástrojů a migrovaná infrastruktura budou nadále postupovat. Firma je teď připravená začít používat tyto prostředky v produkční kapacitě.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

V předchozí fázi tohoto mluveného komentáře byly vývoj aplikací a týmy BI skoro připravené k integraci zákaznických a finančních dat do produkčních úloh. IT tým probíhal při vyřazování datacentra DR.

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- Překročili jsme 100% datacentra DR, před plánem. V tomto procesu se jako kandidáti na migraci cloudu identifikovaly sady prostředků v provozním datacentru.
- Vývojové týmy pro aplikace jsou teď připravené na provozní provoz.
- Tým BI je připravený k zakládání předpovědi a přehledů zpátky do operačních systémů v provozním datacentru.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Před použitím nasazení Azure v produkčních obchodních procesech musí být cloudové operace vyspělé. Kromě toho jsou potřeba další změny zásad správného řízení, které zajistí, že prostředky můžou být správně fungující.

Změny aktuálního a budoucího stavu zveřejňují nová rizika, která budou vyžadovat nové příkazy zásad.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Provozní přerušení:** Existuje riziko, že jakákoli nová platforma způsobuje přerušení důležitých podnikových procesů. Provozní tým IT a týmy spuštěné v různých prodaných cloudech jsou relativně v cloudových operacích. Tím se zvyšuje riziko přerušení a musí se napravit a řídit.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

1. K externímu vniknutí nebo útokům DOS (Denial of Service) může dojít k výpadku firmy.
2. Klíčové prostředky nemusí být správně zjištěny, a proto nemusí být správně provozovány.
3. Existující procesy provozní správy nemusí podporovat nezjištěné nebo neoznačené prostředky.
4. Konfigurace nasazených prostředků nemusí splňovat očekávání výkonu.
5. Protokolování nemusí být správně zaznamenáno a centralizované, aby bylo možné vyřešit problémy s výkonem.
6. Zásady obnovení můžou selhat nebo trvat déle, než se čekalo.
7. Nekonzistentní procesy nasazení můžou vést k bezpečnostním otvorům, které by mohly vést k úniku nebo přerušením dat.
8. Aktualizace s posunem nebo chybějícími opravami můžou vést k nezamýšleným bezpečnostním otvorům, které by mohly vést k úniku nebo přerušením dat.
9. Konfigurace nemusí vyhovět požadavkům definovaných SLA nebo potvrzených požadavků na obnovení.
10. Nasazené operační systémy nebo aplikace nemusí selhat, aby splňovaly požadavky na posílení zabezpečení.
11. Díky tomu mnoho týmů pracujících v cloudu existuje riziko nekonzistence.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky. Seznam vypadá dlouhou dobu, ale přijetí těchto zásad může být snazší než jeho zobrazení.

1. Všechny nasazené prostředky musí být rozdělené do kategorií podle závažnosti a klasifikace dat. Klasifikace jsou přezkoumány týmem zásad správného řízení cloudu a vlastníkem aplikace před nasazením do cloudu.
2. Podsítě, které obsahují klíčové aplikace, musí být chráněné řešením brány firewall schopnými detekovat vniknutí a reagovat na útoky.
3. Nástroje pro správu zásad správného řízení musí auditovat a vymáhat požadavky na konfiguraci sítě definované týmem správy zabezpečení.
4. Nástroje zásad správného řízení musí ověřit, že všechny prostředky související s nejdůležitějšími aplikacemi nebo chráněnými daty jsou zahrnuté do monitorování pro vyčerpání a optimalizaci prostředků.
5. Nástroje správy zásad správného řízení musí ověřit, jestli jsou shromažďovány odpovídající úrovně dat protokolování pro všechny klíčové aplikace nebo chráněná data.
6. Proces zásad správného řízení musí ověřit, jestli je zálohování, obnovení a dodržování SLA správně implementované pro klíčové aplikace a chráněná data.
7. Nástroje zásad správného řízení musí omezit nasazení virtuálních počítačů jenom na schválené image.
8. Nástroje zásad správného řízení musí vymáhat, že automatické aktualizace jsou zabráněno na všech nasazených assetech, které podporují klíčové aplikace. Porušení musí být přezkoumána s provozními týmy správy a opraveny v souladu se zásadami provozu. Prostředky, které se automaticky neaktualizují, musí být zahrnuté do procesů, které vlastní IT operace.
9. Nástroje řízení správného řízení musí ověřovat označování související s náklady, závažností, smlouvou SLA, aplikací a klasifikací dat. Všechny hodnoty musí být zarovnané na předdefinované hodnoty, které spravuje tým zásad správného řízení.
10. Procesy zásad správného řízení musí zahrnovat audity v místě nasazení a v pravidelných cyklech, aby se zajistila konzistence napříč všemi prostředky.
11. Trendy a zneužití, které by mohly ovlivnit nasazení v cloudu, by pravidelně kontroloval tým zabezpečení, aby poskytoval aktualizace nástrojů pro správu zabezpečení používaných v cloudu.
12. Před vydáním do produkčního prostředí je nutné do určeného řešení monitorování provozu přidat všechny klíčové aplikace a chráněná data. Prostředky, které nemohou být zjištěny vybranými nástroji IT operace, nelze uvolnit pro použití v produkčním prostředí. Všechny změny potřebné k tomu, aby byly prostředky zjistitelné, musí být provedeny pro příslušné procesy nasazení, aby bylo zajištěno, že prostředky budou v budoucích nasazeních zjistitelné.
13. Po zjištění budou týmy provozní správy měnit prostředky, aby bylo zajištěno, že prostředky splňují požadavky na výkon.
14. Nástroje pro nasazení musí schválit tým zásad správného řízení cloudu, aby se zajistilo průběžné řízení nasazených prostředků.
15. Skripty nasazení musí být udržovány v centrálním úložišti přístupném týmem zásad správného řízení cloudu pro pravidelnou kontrolu a auditování.
16. Procesy kontroly zásad správného řízení musí ověřit, jestli jsou nasazené prostředky správně nakonfigurované v rámci zarovnání s požadavky SLA a obnovení.

## <a name="incremental-improvement-of-governance-practices"></a>Postupné vylepšování postupů správného řízení

V této části článku se změní návrh MVP zásad správného řízení tak, aby zahrnoval nové zásady Azure a implementaci Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

1. Tým provozu cloudu bude definovat nástroje Operational monitoring a nástroje pro automatizované opravy. Tým zásad správného řízení pro Cloud bude tyto procesy zjišťování podporovat. V tomto případě se v cloudovém provozním týmu zvolí Azure Monitor jako primární nástroj pro monitorování důležitých podnikových aplikací.
2. Vytvořte v Azure DevOps úložiště, ve kterém se uloží a naplní všechny relevantní šablony Správce prostředků a skriptované konfigurace.
3. Implementace úložiště Azure Recovery Services:
    1. Definujte a nasaďte Azure Recovery Services trezor pro procesy zálohování a obnovení.
    2. Vytvořte šablonu Správce prostředků pro vytvoření trezoru v každém předplatném.
4. Aktualizovat Azure Policy pro všechna předplatná:
    1. Auditujte a vynutilte kritickou a klasifikaci dat napříč všemi předplatnými k identifikaci všech předplatných s důležitými klíčovými prostředky.
    2. Auditujte a vynutili použití jenom schválených imagí.
5. Azure Monitor implementace:
    1. Jakmile se identifikují důležité úlohy, vytvořte Azure Monitor pracovní prostor.
    2. Během testování nasazení nasadí tým operací cloudu nezbytné agenty a testy zjišťování.
6. Aktualizuje Azure Policy pro všechna předplatná, která obsahují klíčové aplikace.
    1. Audituje a vynutila použití NSG pro všechny síťové karty a podsítě. Sítě a zabezpečení IT definují NSG.
    2. Auditujte a vyvynuťte použití schválených podsítí sítě a virtuální sítě pro každé síťové rozhraní.
    3. Audituje a vynutil omezení uživatelem definovaných směrovacích tabulek.
    4. Audituje a vynutil nasazení Azure Monitor agentů pro všechny virtuální počítače.
    5. Proveďte audit a vyjistěte, aby v předplatném existovaly trezory služby Azure Recovery Services.
7. Konfigurace brány firewall:
    1. Identifikujte konfiguraci Azure Firewall, která splňuje požadavky na zabezpečení. Případně můžete identifikovat zařízení třetí strany, které je kompatibilní s Azure.
    1. Vytvořte šablonu Správce prostředků pro nasazení brány firewall pomocí požadovaných konfigurací.
8. Podrobný plán Azure:
    1. Vytvořte nový plán Azure s názvem `protected-data`.
    2. Přidejte do podrobného plánu šablony brány firewall a úložiště Azure.
    3. Přidejte nové zásady pro odběry chráněných dat.
    4. Publikujte podrobný plán do jakékoli skupiny pro správu, která bude hostovat klíčové aplikace.
    5. Použijte nový podrobný plán na všechny ovlivněné předplatné i na existující plány.

## <a name="conclusion"></a>Závěr

Tyto další procesy a změny v rámci řízení MVP vám pomůžou napravit mnoho rizik spojených se zásadou správného řízení prostředků. Společně přidávají ovládací prvky pro obnovení, změnu velikosti a monitorování, které podporují cloudové operace.

## <a name="next-steps"></a>Další kroky

V případě, že se přijetí do cloudu pokračuje a přináší další obchodní hodnotu, rizika a potřeby zásad správného řízení cloudu se změní také. V případě fiktivní společnosti v tomto průvodci je další aktivační událost v případě, že škálování nasazení přesáhne 100 prostředků do cloudu nebo měsíční útraty překračuje $1 000 za měsíc. V tomto okamžiku tým zásad správného řízení cloudu přidá ovládací prvky Cost Management.

> [!div class="nextstepaction"]
> [Vylepšení Cost Management](./cost-management-improvement.md)
