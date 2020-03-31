---
title: Vytvořit týmové struktury
description: Pomocí těchto příkladů běžných týmových struktur můžete najít organizační strukturu, která nejlépe odpovídá vašim provozním potřebám.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 09f85e383623f52212eb9621b34342d54ad747b7
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80428383"
---
<!-- cSpell:ignore ccoe -->

# <a name="establish-team-structures"></a>Vytvořit týmové struktury

Všechny funkce cloudu poskytuje někdo při každém úsilí o přijetí do cloudu. Tato přiřazení a týmové struktury mohou být vyvíjeny organicky, nebo mohou být záměrně navrženy tak, aby odpovídaly definované struktuře týmu.

Vzhledem k tomu, že je potřeba dosáhnout růstu, je potřeba vyvážit a strukturovat. Tento článek popisuje příklady běžných týmových struktur v různých fázích organizace splatnosti. Následující obrázek a seznam popisují tyto struktury na základě typických fází maturation. Pomocí těchto příkladů můžete najít organizační strukturu, která nejlépe odpovídá vašim provozním potřebám.

![Cyklus vyspělosti organizace](../_images/ready/org-ready-maturity.png)

Organizační struktury se obvykle pohybují v rámci běžného modelu splatnosti, který je zde popsaný:

1. [Jenom tým pro přijetí do cloudu](#cloud-adoption-team-only)
2. [Osvědčený postup MVP](#best-practice-minimum-viable-product-mvp)
3. [Centrální IT oddělení](#central-it)
4. [Strategické zarovnání](#strategic-alignment)
5. [Provozní zarovnání](#operational-alignment)
6. [Cloudové centrum excelence (CCoE)](#cloud-center-of-excellence)

Většina společností začíná s malým množstvím týmu, než je *tým pro přijetí v cloudu*. Doporučujeme však vytvořit organizační strukturu, která bude lépe podobná struktuře [osvědčených postupů MVP](#best-practice-minimum-viable-product-mvp) .

## <a name="cloud-adoption-team-only"></a>Jenom tým pro přijetí do cloudu

Nucleus všech úsilí o přijetí cloudu je tým pro přijetí cloudu. Tento tým řídí technické změny, které umožňují přijetí. V závislosti na cílech úsilí o přijetí může tento tým zahrnovat nejrůznější členy týmu, kteří zpracovávají širokou škálu technických a obchodních úkolů.

![Tým pro přijetí do cloudu s týmy pro řízení a zabezpečení](../_images/ready/org-ready-adoption-only.png)

V případě snahy o řešení v malém měřítku nebo v rané fázi může být tento tým malým jménem jedné osoby. Ve velkém měřítku nebo v pozdní fázi je běžné, že máte několik týmů pro přijímání v cloudu, z nichž každý má zhruba šest techniků. Bez ohledu na velikost nebo úkoly je konzistentní aspekt každého týmu pro přijetí cloudu tím, že poskytuje prostředky k registraci řešení do cloudu. V některých organizacích může být to dostatečná organizační struktura. Článek o [přijetí do cloudu](./cloud-adoption.md) poskytuje více informací o struktuře, složení a funkci týmu pro přijetí cloudu.

> [!WARNING]
> V provozu *jenom* tým pro přijetí do cloudu (nebo několik týmů pro přijetí v cloudu) se považuje za *antipattern* a je třeba se jim vyhnout. Měli byste minimálně zvážit [osvědčené postupy MVP](#best-practice-minimum-viable-product-mvp).

## <a name="best-practice-minimum-viable-product-mvp"></a>Osvědčený postup: minimální životaschopný produkt (MVP)

Doporučujeme, abyste měli dva týmy, abyste vytvořili rovnováhu mezi úsilím při přijímání v rámci cloudu. Tyto dva týmy zodpovídají za různé možnosti během úsilí o přijetí.

- **Tým pro přijetí cloudu:** Tento tým je popsaný pro technická řešení, obchodní zarovnání, řízení projektů a operace pro přijatá řešení.
- **Tým zásad správného řízení cloudu:** Aby bylo možné vyvážit tým pro přijetí do cloudu, tým zásad správného řízení cloudu je vyhrazen k zajištění vynikajících řešení v přijatých řešeních. Tým zásad správného řízení cloudu je pro vypořádání platforem, operací platforem, zásad správného řízení a automatizace účet.

![Přijetí do cloudu s využitím zásad správného řízení cloudu](../_images/ready/org-ready-best-practice.png)

Tento prověřený přístup se považuje za MVP, protože nemusí být udržitelný. Každý tým má spoustu Hats, jak je uvedeno v odpovědných, prodaných, prodaných, příslušně, [ *informách* (RACI) grafech](./raci-alignment.md).

V následujících částech jsou popsány plně personální a prověřené organizační struktury spolu s přístupy k zajištění odpovídající struktury pro vaši organizaci.

## <a name="central-it"></a>Centrální IT

V rámci škálování přijetí se tým zásad správného řízení cloudu může bojovat, aby se zajistilo, že bude postupovat od několika týmů při přijímání inovací. To platí zejména v prostředích, která mají vysoké požadavky na dodržování předpisů, operace nebo zabezpečení. V této fázi je běžné, že společnosti přesouvá odpovědnost za Cloud do stávajícího centrálního IT týmu. Pokud může tento tým přehodnotit nástroje, procesy a lidi, aby lépe podporovaly přijetí do cloudu ve velkém měřítku, včetně centrálního IT týmu může přidat významnou hodnotu. Díky tomu, že odborníci na danou problematiku z provozu, automatizaci, zabezpečení a správu modernizovat centrální IT oddělení IT můžou řídit účinné provozní inovace.

![Přechod do cloudu s centrálním IT modelem](../_images/ready/org-ready-central-it.png)

Hlavní fáze IT bohužel může být jednou z fází nejrizikovějších organizace. Ústřední IT tým musí přijít do tabulky se silným růstovým místoem. Pokud tým prohlíží Cloud jako příležitost k růstu a přizpůsobení jejich schopností, může v celém procesu poskytnout skvělou hodnotu. Pokud ale centrální tým IT prohlíží Cloud jako hrozbu pro svůj stávající model, pak se tým oddělení IT stal překážkou týmů pro přijetí cloudu a podnikovým cílům, které podporují. Někteří týmy centrálního IT strávily měsíce nebo dokonce roky, které se snaží vynutit, aby Cloud vynutil vyrovnání s místními přístupy a jenom negativní výsledky. Cloud nevyžaduje, aby se všechno změnilo v centrálním IT oddělení, ale vyžaduje změnu. Pokud se odolnost proti změnám přestává v rámci centrálního IT týmu, může se tato fáze zralosti rychle stát kulturním antipatternem.

Plány pro přijetí do cloudu jsou silně zaměřené na platformu jako službu (PaaS), DevOps nebo jiná řešení, která vyžadují méně provozu, se v této fázi zralosti méně nejspíš zobrazí hodnota. V opačném případě jsou tyto typy řešení pravděpodobně překážkované nebo blokované pokusy o jeho centralizaci. Vyšší úroveň zralosti, jako je [cloudová centra excelence (CCoE)](#cloud-center-of-excellence), je pravděpodobnější pro tyto typy transformačního úsilí s cílem dosáhnout pozitivních výsledků. Informace o rozdílech mezi centrálním IT v cloudu a CCoE najdete v tématu [cloudové centrum vynikajících](./cloud-center-of-excellence.md)informací.

## <a name="strategic-alignment"></a>Strategické zarovnání

V důsledku toho, že investice do cloudového přijetí roste a že se účtují obchodní hodnoty, se obchodní strany často stávají zabývají. Definovaný tým cloudové strategie, jak znázorňuje následující obrázek, zarovnává tyto obchodní účastníky a maximalizuje hodnotu, kterou zajímá investice do cloudu.

![Přidat tým definované cloudové strategie](../_images/ready/org-ready-strategy-aligned.png)

V případě, že splatnost probíhá organicky, v důsledku snahy o přijetí cloudu, která má za následek strategické zarovnání, obvykle předchází zásadám správného řízení nebo centrálnímu týmu IT. Když snaha o přijetí cloudu vede k činnosti, zaměřuje se na provozní model a organizace, která je v minulosti. Kdykoli je to možné, obchodní výsledky a tým cloudových strategií by se měly definovat v počátečním procesu.

## <a name="operational-alignment"></a>Provozní zarovnání

Provozní hodnota z úsilí o přijetí do cloudu vyžaduje stabilní operace. Operace v cloudu můžou vyžadovat nové nástroje, procesy nebo dovednosti. V případě, že se pro dosažení obchodních výsledků vyžadují stabilní operace IT, je důležité přidat tým definovaného cloudového provozu, jak je znázorněno zde.

![Přidání týmu definovaného cloudového provozu](../_images/ready/org-ready-operations-aligned.png)

Cloudové operace mohou být doručovány stávajícími provozními rolemi IT. Není to ale běžné pro to, aby cloudové operace byly delegované na jiné strany mimo IT oddělení. Poskytovatelé spravovaných služeb, DevOps týmy a obchodní jednotka často předpokládají zodpovědnosti spojené s cloudovou operací s podporou a guardrails poskytovanými IT operacemi. To je stále častější pro úsilí při přijímání v cloudu, které se zaměřuje na nasazení DevOps nebo PaaS.

## <a name="cloud-center-of-excellence"></a>Vedoucí centrum cloudu

V nejvyšším stavu zralosti cloudové centrum kvality zarovnává týmy kolem moderního modelu s prvním cloudovým provozem. Tento přístup poskytuje centrální IT funkce jako zásady správného řízení, zabezpečení, platformy a automatizace.

![Vedoucí centrum cloudu](../_images/ready/org-ready-ccoe.png)

Hlavním rozdílem mezi touto strukturou a centrální strukturou IT je zaměření na samoobslužné služby. Týmy v této struktuře organizují s úmyslem delegovat řízení co nejvíce. Zarovnávání postupů zásad správného řízení a dodržování předpisů pro cloudová nativní řešení vytváří mechanismy guardrails a ochrany. Na rozdíl od centrálního IT modelu maximalizuje cloudový přístup inovace a minimalizuje provozní režii. Aby se tento model přijal, bude se od podnikání a vedoucího IT potřebovat vzájemná dohoda o modernizovat IT procesech. Tento model se pravděpodobně nevyskytuje organicky a často vyžaduje výkonnou podporu.

## <a name="next-steps"></a>Další kroky

Po zarovnání na určitou fázi zralosti organizační struktury můžete použít [grafy RACI](./raci-alignment.md) k zarovnávání zodpovědnosti a zodpovědnosti napříč každým týmem.

> [!div class="nextstepaction"]
> [Zarovnat příslušný graf RACI](./raci-alignment.md)
