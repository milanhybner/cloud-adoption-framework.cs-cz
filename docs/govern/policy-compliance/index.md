---
title: Příprava firemních zásad pro cloud
description: Vysvětlení konceptu firemních zásad v souvislosti se zásadami správného řízení v cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b2a260868a873828a1bc47584f479f129b6b255a
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806080"
---
<!-- markdownlint-disable MD026 -->

# <a name="prepare-corporate-it-policy-for-the-cloud"></a>Příprava firemních zásad pro cloud

Zásady správného řízení v cloudu jsou výsledkem průběžného úsilí o přechod, protože skutečně dlouhodobé transformace nejde dosáhnout přes noc. Pokusy o rychlé a agresivní zajištění kompletních zásad správného řízení v cloudu před vyřešením klíčových změn firemních zásad zřídka vedou k požadovaným výsledkům. Místo toho doporučujeme inkrementální přístup.

Čím se naše architektura přechodu na cloud odlišuje, je nákupní cyklus a způsob, jakům může umožnit autentickou transformaci. Vzhledem k tomu, že na pořízení nejsou potřeba velké kapitálové výdaje, můžou technici začít s experimentováním a přechodem dříve. Ve většině firemních kultur odstranění překážky pro přechod v podobě kapitálových výdajů může vést k těsnějším smyčkám zpětné vazby, organickému růstu a inkrementální realizaci.

Posun k přechodu na cloud vyžaduje posun v zásadách správného řízení. V řadě organizací transformace firemních zásad umožňuje zlepšit zásady správného řízení a zvýšit míru jejich dodržování prostřednictvím inkrementálních změn zásad a automatizovaného vynucování těchto změn, které zajišťují nově definované funkce, které můžete nakonfigurovat u svého poskytovatele cloudových služeb.

Tento článek popisuje klíčové aktivity, které vám pomůžou utvářet firemní zásady a zajistit tak podporu rozšířeného modelu zásad správného řízení.

## <a name="define-corporate-policy-to-mature-cloud-governance"></a>Definování firemních zásad pro vyspělejší zásady správného řízení v cloudu

V tradičních zásadách správného řízení i inkrementálních zásadách správného řízení se funkční definice zásad správného řízení skládá z firemních zásad. Cílem většiny akcí zásad správného řízení v oblasti IT je implementovat technologii umožňující monitorovat, vynucovat, provozovat a automatizovat tyto firemní zásady. Zásady správného řízení v cloudu vycházejí z podobných konceptů.

![Firemní zásady správného řízení a disciplíny správného řízení](../../_images/operational-transformation-govern-highres.png)

*Obrázek 1: Firemní zásady a disciplíny správného řízení*

Obrázek výše znázorňuje interakce mezi obchodními riziky, zásadami a dodržováním předpisů a monitorováním a vynucováním, které tvoří strategii zásad správného řízení. Dále ukazuje Pět disciplín zásad správného řízení v cloudu, které můžete využít k realizaci vlastní strategie.

## <a name="review-existing-policies"></a>Kontrola stávajících zásad

Na obrázku výše začíná strategie zásad správného řízení (riziko, zásady a dodržování předpisů, monitorování a vynucování) rozpoznáním obchodních rizik. Pochopení, jak se [obchodní rizika](./business-risk.md) mění v cloudu, je prvním krokem k vytvoření trvalé strategie zásad správného řízení v cloudu. Když ve spolupráci s vašimi obchodními jednotkami získáte přesnou [míru tolerance vaší firmy k riziku](./risk-tolerance.md), pomůže vám to zjistit, na jaké úrovni je potřeba rizika odstraňovat. Díky porozumění novým rizikům a přijatelné toleranci můžete [zkontrolovat stávající zásady](./cloud-policy-review.md) a určit požadovanou úroveň zásad správného řízení, která je vhodná pro vaši organizaci.

> [!TIP]
> Pokud se vaše organizace řídí dodržováním předpisů třetích stran, jedním z největších obchodních rizik, které byste měli zvážit, je riziko porušení [dodržování legislativní předpisů](./regulatory-compliance.md). Toto riziko často není možné odstranit, a místo toho může vyžadovat zajištění striktního dodržování. Před zahájením kontroly zásad se ujistěte, že rozumíte požadavkům na dodržování předpisů třetích stran.

## <a name="an-incremental-approach-to-cloud-governance"></a>Inkrementální přístup k zásadám správného řízení v cloudu

Inkrementální přístup k zásadám správného řízení v cloudu předpokládá, že je nepřijatelné překročit [toleranci firmy k riziku](./risk-tolerance.md). Místo toho předpokládá, že účelem zásad správného řízení je zrychlit obchodní změny, pomoct technikům porozumět pokynům k architektuře a zajistit pravidelné informování a odstraňování [obchodních rizik](./business-risk.md). Tradiční role zásad správného řízení se případně může stát překážkou pro přechod techniků nebo celé firmy.

V případě inkrementálního přístupu k zásadám správného řízení v cloudu občas dochází k přirozenému tření mezi týmy vytvářejícími nová obchodní řešení a týmy zajišťujícími ochranu firmy před riziky. V tomto modelu se však tyto dva týmy můžou stát partnery a pracovat v přírůstcích nebo sprintech. Jako partneři můžou tým zásad správného řízení v cloudu a týmy přechodu na cloud začít společně pracovat na zveřejňování, vyhodnocování a odstraňování obchodních rizik. Při tomto přístupu může docházet k přirozenému snižování tření a podpoře spolupráce mezi týmy.

## <a name="minimum-viable-product-mvp-for-policy"></a>MVP (Minimum Viable Product) pro zásady

Prvním krokem v nově vznikajícím partnerství mezi týmy zásad správného řízení v cloudu a přechodu na cloud je shodnout se na MVP zásad. Váš MVP pro zásady správného řízení v cloudu by měl zohledňovat, že obchodní rizika jsou zpočátku malá, ale s tím, jak vaše organizace bude postupně přecházet na další cloudové služby, se budou pravděpodobně zvětšovat.

Například firma nasazující pět virtuálních počítačů, které neobsahují žádná data HBI (High Business Impact), bude čelit malým obchodním rizikům. V pozdější fázi procesu přechodu na cloud, když počet virtuálních počítačů dosáhne 1 000 a firma začne přesouvat data HBI, obchodní rizika porostou.

MVP zásad se pokouší definovat požadovaný základ zásad požadovaných k nasazení prvních _x_ virtuálních počítačů nebo prvních _x_ aplikací, kde _x_ představuje malé ale smysluplné množství jednotek. Tato sada zásad nevyžaduje mnoho omezení, ale bude obsahovat základní aspekty potřebné k rychlému růstu od jednoho inkrementálního přechodu na cloud k dalšímu. Díky inkrementálnímu vývoji zásad se tato strategie zásad správného řízení bude v průběhu času vyvíjet. Prostřednictvím drobných a pomalých posunů MVP zásad postupně dosáhne parity funkcí s výstupy cvičení kontroly zásad.

## <a name="incremental-policy-growth"></a>Inkrementální vývoj zásad

Inkrementální vývoj zásad je klíčovým mechanismem pro vývoj zásad a zásad správného řízení v cloudu v průběhu času. Zároveň se jedná o klíčový požadavek při zavádění inkrementálního modelu do zásad správného řízení. Pro správné fungování tohoto modelu je potřeba, aby se tým zásad správného řízení zavázal v každém sprintu věnovat po určitou přidělenou dobu vyhodnocení a implementaci měnících se disciplín správného řízení.

**Časové požadavky na sprint:** Na začátku každé iterace všechny týmy přechodu na cloud vytvoří seznam prostředků, které se mají v aktuální iteraci migrovat nebo zavést. Tým zásad správného řízení v cloudu by měl poskytnout dostatek času na kontrolu seznamu, ověření klasifikací dat pro prostředky, vyhodnocení případných nových rizik spojených s jednotlivými prostředky, aktualizaci pokynů k architektuře a informování týmu o změnách. Tyto závazky obvykle v každém sprintu zaberou 10 až 30 hodin. Na této úrovni zapojení se také očekává, že alespoň jeden zaměstnanec bude muset být vyhrazený pro správu zásad správného řízení v rámci rozsáhlého přechodu na cloud.

**Časové požadavky na vydání:** Na začátku každého vydání by týmy přechodu na cloud a tým cloudové strategie měly určit prioritu aplikací nebo úloh na seznamu, které se mají migrovat v aktuální iteraci, a také všech aktivit obchodních změn. Tyto datové body umožní týmu zásad správného řízení v cloudu rychle se seznámit s novými obchodními riziky. Díky tomu bude mít dostatek času na sladění s obchodní činností a vyhodnotit toleranci firmy k riziku.

## <a name="next-steps"></a>Další kroky

Efektivní strategie zásad správného řízení cloudu začíná pochopením obchodních rizik.

> [!div class="nextstepaction"]
> [Principy obchodních rizik](./business-risk.md)
