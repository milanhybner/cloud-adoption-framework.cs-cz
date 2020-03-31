---
title: Pochopení podnikového rizika při migraci do cloudu
description: Pomocí architektury cloudového prostředí pro Azure se naučíte procesy řízení rizik, které vám pomůžou vyhodnotit, porozumět, vyrovnávat a opravovat rizika migrace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: b868600361f500f2ae6d6b55a4fad66b4d9945ee
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434183"
---
<!-- markdownlint-disable MD026 -->

# <a name="understand-business-risk-during-cloud-migration"></a>Pochopení podnikového rizika při migraci do cloudu

Porozumění obchodním rizikům je jedním z nejdůležitějších prvků jakékoli cloudové transformace. Zásady pro rizikové jednotky a mají vliv na požadavky na monitorování a vynucování. Riziko silně ovlivňuje způsob, jakým spravujeme digitální nemovitosti, místní i cloudové.

<!-- markdownlint-enable MD026 -->

## <a name="relativity-of-risk"></a>Relativita rizika

Riziko je relativní. Malá společnost s několika IT prostředky v uzavřeném sestavách má malé riziko. Přidejte uživatele a připojení k Internetu s přístupem k těmto assetům, riziko se zvyšuje. Když malá společnost roste na stav Fortune 500, rizika budou exponenciálně větší. Jako výnosy, obchodní procesy, počty zaměstnanců a assety IT se shromažďují, zvyšují se rizika a přicoalesce. Prostředky IT, které pomáhají při vygenerování výnosů, jsou při výpadku zastavování těchto příjmů v případě výpadku. Každý okamžik výpadku se rovná ztrátám. Stejně tak, jak se data shromažďují, riziko poškození zákazníků roste.

V tradičním místním světě se týmy zásad správného řízení IT zaměřují na posuzování rizik, vytváření procesů pro správu těchto rizik a nasazování systémů, které zajistí úspěšnou implementaci nápravných opatření. Tato snaha pracuje na rovnováhu mezi riziky potřebnými pro provoz v připojeném a moderním podnikovém prostředí.

## <a name="understand-business-risks-in-the-cloud"></a>Pochopení obchodních rizik v cloudu

Během transformace existují stejná relativní rizika.

- Během předčasného experimentování je několik prostředků nasazených s malým množstvím dat, které není relevantní. Riziko je malé.
- Při nasazení prvního zatížení se riziko trochu sníží. Toto riziko se dá snadno opravit tak, že vyberete podstatu aplikace s nízkým rizikem s malým uživatelským základem.
- S tím, jak další úlohy přicházejí do režimu online, se rizika mění v každé vydané verzi. Nové aplikace budou jít o živá a změní se jejich rizika.
- Když společnost přináší první 10-20 aplikací v režimu online, profil rizika je mnohem jiný, než když aplikace 1000th přejdou do produkčního prostředí v cloudu.

Prostředky, které se shromáždily v tradičním, místním majetku, se nejspíš časem sčítají. Splatnost podnikových a IT týmů se nejspíš rozrůstá podobným způsobem. Tento paralelní růst může vést k vytvoření některých zbytečných zavazadel zásad.

Během převodu do cloudu mají firmy i týmy k dispozici možnost resetovat tyto zásady a vytvářet nové s vyspělým místo.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-business-risk-mvp"></a>Co je MVP pro obchodní rizika?

**Minimální životaschopný produkt** se běžně používá k definování nejmenší jednotky něčeho, která může vytvořit hmotná hodnota. V programu MVP pro obchodní riziko začíná tým zásad správného řízení cloudu předpokladem, že některé prostředky budou nasazeny do cloudového prostředí v určitém časovém okamžiku. Je známo, co jsou v tuto chvíli assety, a tým si nemusí Pojisti, jaké typy dat budou na těchto prostředcích uloženy.

Při plánování podnikového rizika by tým zásad správného řízení cloudu mohl sestavit pro nejhorší případ a namapovat všechny možné zásady do cloudu. Zjištění všech potenciálních obchodních rizik pro všechny scénáře použití cloudu ale může trvat značnou dobu a úsilí, což může způsobit zpoždění implementace zásad správného řízení pro vaše cloudové úlohy. To se nedoporučuje, ale je to možnost.

Přístup MVP naopak může týmu dovolit, aby definoval počáteční počáteční bod a sadu předpokladů, které by byly pravdivé pro většinu/všechny prostředky. Tento MVP pro obchodní rizika bude podporovat počáteční řešení malého rozsahu nebo testování cloudových nasazení a pak bude sloužit jako základ pro postupně identifikující a oprava nová rizika v případě potřeby obchodních potřeb nebo se do vašeho cloudového prostředí přidávají další úlohy. Tento proces vám umožní uplatňovat zásady správného řízení během procesu přijetí do cloudu.

Následuje několik základních příkladů obchodních rizik, která lze zahrnout jako součást MVP:

- Všechny prostředky jsou ohroženy odstraněním (prostřednictvím chyby, chyby nebo údržby).
- Všechny prostředky jsou ohrožené generováním příliš velkého množství útraty.
- Všechny prostředky můžou být ohrožené slabými hesly nebo nezabezpečenými nastaveními.
- Jakékoli assety s otevřenými porty vystavenými Internetu jsou ohroženy ohrožením zabezpečení.

Výše uvedené příklady jsou určeny k navázání obchodních rizik MVP jako teorie. Skutečný seznam bude jedinečný pro každé prostředí.
Jakmile se zřídí MVP pro obchodní riziko, dá se převést na [zásady](./index.md) , aby se každé riziko napravilo.

<!-- markdownlint-enable MD026 -->

## <a name="incremental-risk-mitigation"></a>Zvýšení rizika rizik

Jak vaše organizace nasazuje více úloh do cloudu, vývojové týmy využívají větší množství cloudových prostředků. V každé iteraci se vytvoří a připravíte nové prostředky. V každé vydané verzi jsou úlohy připravené na zvýšení produkčního prostředí. Každý z těchto cyklů má potenciál k zavedení dříve neidentifikovaných obchodních rizik.

Za předpokladu, že je MVP pro obchodní riziko výchozím bodem pro vaše počáteční úsilí o přijetí cloudu, může se správce zahájit paralelně s rostoucím využitím cloudových prostředků. Když tým zásad správného řízení cloudu pracuje paralelně s týmy přijímání v cloudu, růst obchodních rizik se dá řešit podle jejich identifikace a zajistit stabilní průběžný model pro vývoj splatnosti zásad správného řízení.

Jednotlivé připravené prostředky lze snadno klasifikovat podle rizika. Dokumenty klasifikace dat se dají sestavit nebo vytvořit paralelně s přípravnými cykly. Můžete také zdokumentovat profil rizika a body expozice. V průběhu času se velmi jasný pohled na obchodní riziko zaměřuje na celou organizaci.

V každé iteraci tým zásad správného řízení cloudu může spolupracovat s týmem cloudové strategie, aby rychle komunikovala nová rizika, strategie zmírňování, kompromisy a potenciální náklady. To umožňuje obchodním účastníkům a vedoucím IT vedoucím v vyspělých a dobře se informovaných rozhodnutích. Tato rozhodnutí pak informují o zralosti zásad. V případě potřeby se zásady změní na nové pracovní položky pro dobu zralosti základních systémů infrastruktury. Když se vyžadují změny v připravených systémech, týmy pro přijetí v cloudu mají dostatek času na provedení změn, zatímco podnik testuje připravené systémy a vyvíjí plán přijetí uživateli.

Tento přístup minimalizuje rizika a zároveň umožňuje týmu, aby se rychle přesunul. Také zajišťuje, aby rizika byla před nasazením vyřešena a vyřešena.

## <a name="next-steps"></a>Další kroky

Přečtěte si, jak vyhodnotit toleranci rizik během přijetí cloudu.

> [!div class="nextstepaction"]
> [Vyhodnotit toleranci rizika](./risk-tolerance.md)
