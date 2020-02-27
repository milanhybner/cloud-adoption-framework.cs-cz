---
title: 'Komplexní řízení podniku: vylepšení oboru konzistence prostředků'
description: Rozhraní pro přijetí v cloudu pro Azure vám umožní získat informace o kontrolách obnovení, velikosti a monitorování za účelem zlepšení standardních hodnot zásad správného řízení a nápravy rizik.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d7148df4bb06a0dc4ca035b89f7077888fb7306c
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708933"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-resource-consistency-discipline"></a>Příručka zásad správného řízení pro komplexní podniky: vylepšení oboru konzistence prostředků

Tento článek popisuje mluvený komentář přidáním ovládacích prvků konzistence prostředků do MVP pro kontrolu zásad správného řízení pro podporu důležitých aplikací.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Týmy pro přijetí v cloudu splnily všechny požadavky na přesun chráněných dat. Díky těmto aplikacím přijdete o závazky smlouvy SLA na firmu a potřebujete podporu z provozu IT. Napravo od týmu migrují dvě datová centra, vývoj více aplikací a týmy BI jsou připravené začít spouštět nová řešení do produkčního prostředí. Operace IT jsou pro cloudové operace nové a potřebují rychle integrovat stávající provozní procesy.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

- Aktivně přesouvá provozní úlohy s chráněnými daty do Azure. Některé úlohy s nízkou prioritou obsluhují provozní provoz. Víc se dá přejímat, jakmile se v něm operace odhlásí na připravenost pro podporu úloh.
- Vývojové týmy pro aplikace jsou připravené na provozní provoz.
- Tým BI je připravený k integraci předpovědi a přehledů do systémů, které spouštějí operace pro tři obchodní jednotky.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

- Operace IT jsou pro cloudové operace nové a potřebují rychle integrovat stávající provozní procesy.
- Změny aktuálního a budoucího stavu zveřejňují nová rizika, která budou vyžadovat nové příkazy zásad.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Provozní přerušení:** Existuje riziko, že jakákoli nová platforma způsobuje přerušení důležitých podnikových procesů. Provozní tým IT a týmy spuštěné v různých prodaných cloudech jsou relativně v cloudových operacích. Tím se zvyšuje riziko přerušení a musí se napravit a řídit.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

1. Nezarovnané provozní procesy můžou vést k výpadkům, které se nedají detekovat nebo zmírnit rychleji.
2. K externímu vniknutí nebo útokům DOS (Denial of Service) může dojít k výpadku firmy.
3. Klíčové prostředky nemusí být správně zjištěny, a proto nejsou správně provozovány.
4. Existující procesy provozní správy nemusí podporovat nezjištěné nebo neoznačené prostředky.
5. Konfigurace nasazených prostředků nemusí splňovat očekávání výkonu.
6. Protokolování nemusí být správně zaznamenáno a centralizované, aby bylo možné vyřešit problémy s výkonem.
7. Zásady obnovení můžou selhat nebo trvat déle, než se čekalo.
8. Nekonzistentní procesy nasazení můžou vést k bezpečnostním otvorům, které by mohly vést k úniku nebo přerušením dat.
9. Aktualizace s posunem nebo chybějícími opravami můžou vést k nezamýšleným bezpečnostním otvorům, které by mohly vést k úniku nebo přerušením dat.
10. Konfigurace nemusí vyhovět požadavkům definovaných SLA nebo potvrzených požadavků na obnovení.
11. Nasazené operační systémy nebo aplikace nemusí splňovat požadavky na operační systém a posílení zabezpečení aplikací.
12. Existuje riziko nekonzistence z důvodu více týmů pracujících v cloudu.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky. Seznam vypadá dlouhou dobu, ale přijetí těchto zásad může být jednodušší, než by se zobrazilo.

1. Všechny nasazené prostředky musí být rozdělené do kategorií podle závažnosti a klasifikace dat. Klasifikace jsou přezkoumány týmem zásad správného řízení cloudu a vlastníkem aplikace před nasazením do cloudu.
2. Podsítě, které obsahují klíčové aplikace, musí být chráněné řešením brány firewall schopnými detekovat vniknutí a reagovat na útoky.
3. Nástroje zásad správného řízení musí auditovat a vymáhat požadavky na konfiguraci sítě definované týmem standardních hodnot zabezpečení.
4. Nástroje zásad správného řízení musí ověřit, že všechny prostředky související s důležitými aplikacemi nebo chráněnými daty jsou zahrnuté do monitorování pro vyčerpání a optimalizaci prostředků.
5. Nástroje správy zásad správného řízení musí ověřit, jestli jsou shromažďovány odpovídající úrovně dat protokolování pro všechny klíčové aplikace nebo chráněná data.
6. Proces zásad správného řízení musí ověřit, jestli je zálohování, obnovení a dodržování SLA správně implementované pro klíčové aplikace a chráněná data.
7. Nástroje zásad správného řízení musí omezit nasazení virtuálních počítačů jenom na schválené image.
8. Nástroje zásad správného řízení musí vymáhat, že automatické aktualizace jsou **zabráněno** na všech nasazených assetech, které podporují klíčové aplikace. Porušení musí být přezkoumána s provozními týmy správy a opraveny v souladu se zásadami provozu. Prostředky, které se automaticky neaktualizují, musí být zahrnuty do procesů, které vlastní IT operace, pro rychlé a efektivní aktualizace těchto serverů.
9. Nástroje řízení správného řízení musí ověřovat označování související s náklady, závažností, smlouvou SLA, aplikací a klasifikací dat. Všechny hodnoty musí být zarovnané na předdefinované hodnoty, které spravuje tým zásad správného řízení pro Cloud.
10. Procesy zásad správného řízení musí zahrnovat audity v místě nasazení a v pravidelných cyklech, aby se zajistila konzistence napříč všemi prostředky.
11. Trendy a zneužití, které by mohly ovlivnit nasazení v cloudu, by pravidelně kontroloval tým zabezpečení, aby poskytoval aktualizace nástroje pro základní hodnoty zabezpečení používané v cloudu.
12. Před vydáním do produkčního prostředí je nutné do určeného řešení monitorování provozu přidat všechny klíčové aplikace a chráněná data. Prostředky, které nelze zjistit zvolenými nástroji Operations Tool, nelze uvolnit pro použití v produkčním prostředí. Všechny změny potřebné k tomu, aby byly prostředky zjistitelné, musí být provedeny pro příslušné procesy nasazení, aby bylo zajištěno, že prostředky budou v budoucích nasazeních zjistitelné.
13. Po zjištění se velikost assetu ověří pomocí týmů provozní správy a ověří se, jestli Asset splňuje požadavky na výkon.
14. Nástroje pro nasazení musí schválit tým zásad správného řízení cloudu, aby se zajistilo průběžné řízení nasazených prostředků.
15. Skripty nasazení musí být udržovány v centrálním úložišti přístupném týmem zásad správného řízení cloudu pro pravidelnou kontrolu a auditování.
16. Procesy kontroly zásad správného řízení musí ověřit, jestli jsou nasazené prostředky správně nakonfigurované v rámci zarovnání s požadavky SLA a obnovení.

## <a name="incremental-improvement-of-the-best-practices"></a>Přírůstkové zlepšení osvědčených postupů

V této části článku se vylepšit návrh MVP pro řízení a zahrnutí nových zásad Azure a implementace Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

Po zkušenostech tohoto fiktivního příkladu se předpokládá, že se změny chráněných dat již nastaly. Při sestavování tohoto osvědčeného postupu budou přidány požadavky na operační monitorování, které jsou připravené k odběru pro klíčové aplikace.

**Firemní předplatné IT:** Do firemního předplatného, které funguje jako centrum, přidejte následující.

1. V rámci externí závislosti bude tým provozu cloudu potřebovat definovat nástroje pro monitorování provozu, provozní kontinuitu a zotavení po havárii (BCDR) a automatizované nástroje pro nápravu. Tým zásad správného řízení cloudu pak může podporovat potřebné procesy zjišťování.
    1. V tomto případě se v cloudovém provozním týmu zvolí Azure Monitor jako primární nástroj pro monitorování důležitých podnikových aplikací.
    2. Tým také zvolí Azure Site Recovery jako primární nástroj BCDR.
2. Implementace Azure Site Recovery.
    1. Definujte a nasaďte Azure Site Recovery trezor pro procesy zálohování a obnovení.
    2. Vytvořte šablonu správy prostředků Azure pro vytvoření trezoru v každém předplatném.
3. Implementace Azure Monitor.
    1. Po určení důležitého předplatného se dá vytvořit pracovní prostor Log Analytics.

**Předplatné pro přijetí individuálního cloudu:** Následující postup zajistí, že je každé předplatné zjistitelné řešením monitorování a je připravené k zařazení do BCDR postupů.

1. Azure Policy pro klíčové uzly:
    1. Auditujte a vynuťte pouze použití standardních rolí.
    2. Audituje a vynutil používání šifrování pro všechny účty úložiště.
    3. Audituje a vynutil používání schválené podsítě sítě a virtuální sítě na síťové rozhraní.
    4. Audituje a vynutil omezení uživatelem definovaných směrovacích tabulek.
    5. Proveďte audit a vynuťte nasazení agentů Log Analytics pro virtuální počítače s Windows a Linux.
2. Podrobný plán Azure:
    1. Vytvořte podrobný plán s názvem `mission-critical-workloads-and-protected-data`. Tento podrobný plán bude používat prostředky kromě podrobného plánu dat.
    2. Přidejte nové zásady Azure do podrobného plánu.
    3. Použijte podrobný plán na jakékoli předplatné, které se očekává pro hostování důležité aplikace.

## <a name="conclusion"></a>Závěr

Přidání těchto procesů a změn do procesu MVP pro řízení systému vám pomůže napravit mnoho rizik spojených se zásadou správného řízení prostředků. Společně přidávají ovládací prvky pro obnovení, změnu velikosti a monitorování, které jsou nezbytné k zajištění operací s podporou cloudu.

## <a name="next-steps"></a>Další kroky

Protože při přijetí cloudu roste a přináší další obchodní hodnotu, změní se také rizika a požadavky zásad správného řízení cloudu. V případě fiktivní společnosti v tomto průvodci je další aktivační událost v případě, že škálování nasazení přesáhne 1 000 prostředků do cloudu nebo měsíční útraty překračuje $10 000 USD za měsíc. V tomto okamžiku tým zásad správného řízení cloudu přidá ovládací prvky Cost Management.

> [!div class="nextstepaction"]
> [Zlepšení Cost Management disciplíny](./cost-management-improvement.md)
