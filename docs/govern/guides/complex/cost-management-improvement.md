---
title: 'Příručka zásad správného řízení pro komplexní podniky: Zlepšení Cost Management disciplíny'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Příručka zásad správného řízení pro komplexní podniky: Zlepšení Cost Management disciplíny'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5dbb92053e12ec9aee795c54271ab45d56d6722c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220182"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-cost-management-discipline"></a>Příručka zásad správného řízení pro komplexní podniky: Zlepšení Cost Management disciplíny

Tento článek popisuje mluvený komentář přidáním řízení nákladů do zásad správného řízení pro minimální životaschopný produkt (MVP).

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Přijetí přesáhlo ukazatel tolerance definovaný v MVP MVP pro řízení. Zvýšení útraty nyní odůvodňuje investici z týmu zásad správného řízení cloudu za účelem monitorování a řízení vzorů útraty.

Jako jasný ovladač inovace se už nezobrazuje hlavně jako nákladové středisko. Vzhledem k tomu, že organizace IT nabízí větší hodnotu, CIO a finanční ředitel souhlasí, že doba je vhodná k posunu role, kterou hraje ve společnosti. Kromě dalších změn chce finanční ředitel testovat přímý placený přístup ke cloudovým účtováním pro kanadskou větev jedné z obchodních jednotek. Jedno ze dvou vyřazených datových center bylo exkluzivně hostovaných assetů pro kanadské obchodní jednotky. V tomto modelu se kanadská pobočka obchodní jednotky bude účtovat přímo za provozní náklady související s hostovanými prostředky. Tento model umožňuje oddělení IT méně soustředit se na správu útraty někoho jiného a dalších při vytváření hodnoty. Před zahájením tohoto přechodu ale můžete začít Cost Management nástrojů.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

V předchozí fázi tohoto mluveného komentáře mohl IT tým aktivně přesouvat produkční úlohy s chráněnými daty do Azure.

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- prostředky 5 000 byly odebrány ze dvou datových center označených pro vyřazení. Nákup a zabezpečení IT teď ruší zřízení zbývajících fyzických prostředků.
- Vývojové týmy pro aplikace implementovaly kanály CI/CD pro nasazení některých cloudových aplikací, které významně ovlivňují prostředí zákazníků.
- Tým BI vytvořil agregační, léčebné, analytické a předpovědní procesy, které řídí hmotné přínosy pro obchodní operace. Tyto předpovědi nyní umožňují kreativní nové produkty a služby.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Do cloudového řešení by se měly přidat náklady monitorování a generování sestav. Vytváření sestav by mělo spojovat s přímými provozními náklady na funkce, které spotřebovávají náklady na Cloud. Další vytváření sestav by mělo umožňovat monitorování útraty a poskytování technických pokynů pro řízení nákladů. Pro kanadskou větev se oddělení účtuje přímo.

## <a name="changes-in-risk"></a>Změny v nebezpečí

**Řízení rozpočtu:** Existuje riziko, že funkce samoobslužné služby budou mít za následek nadměrné a neočekávané náklady na novou platformu. Procesy zásad správného řízení pro monitorování nákladů a zmírnění probíhajících nákladů na zpracování musí být zavedeny, aby se zajistilo pokračující sblížení s plánovaným rozpočtem.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

- Existuje riziko, že se v rámci plánu navyšuje skutečné náklady.
- Obchodní podmínky se změní. V takovém případě budou existovat případy, kdy obchodní funkce potřebuje spotřebovat více cloudových služeb, než se očekávalo, což vede k nepravidelnosti útraty. Existuje riziko, že tyto dodatečné náklady budou považovány za překročení limitu, a to na rozdíl od požadované úpravy plánu. V případě úspěchu by měl kanadský experiment přispět k nápravě tohoto rizika.
- Hrozí riziko nadměrného zřizování systémů, což vede k překročení útraty.

## <a name="changes-to-the-policy-statements"></a>Změny v příkazech zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky.

- Všechny náklady na Cloud by se měly monitorovat na týden podle týmu zásad správného řízení pro Cloud. Vykazování odchylek mezi náklady na Cloud a plánem se sdílí s vedením IT a finančními službami měsíčně. Všechny náklady na Cloud a plán aktualizací by se měly kontrolovat s využitím IT a finančních prostředků měsíčně.
- Všechny náklady musí být přiděleny obchodní funkci pro účely zodpovědnosti.
- Cloudové prostředky by se měly průběžně monitorovat podle možností optimalizace.
- Nástroje pro řízení cloudu musí omezit možnosti změny velikosti Assetu na schválený seznam konfigurací. Nástroj musí zajistit, aby všechny prostředky byly zjistitelné a sledované řešením pro monitorování nákladů.
- Během plánování nasazení by se měly zdokumentovat všechny požadované cloudové prostředky spojené s hostováním produkčních úloh. Tato dokumentace vám pomůže Upřesnit rozpočty a připravit další nástroje pro automatizaci, aby nedocházelo k používání dražších možností. Během tohoto procesu by se mělo předávat různým nástrojům diskontování nabízeným poskytovatelem cloudu, jako jsou rezervované instance nebo snížení nákladů na licence.
- Všichni vlastníci aplikací se budou muset zúčastnit školení o postupech pro optimalizaci úloh, aby lépe ovládají náklady na Cloud.

## <a name="incremental-improvement-of-the-best-practices"></a>Přírůstkové zlepšení osvědčených postupů

V této části článku se vylepšit návrh MVP pro řízení a zahrnutí nových zásad Azure a implementace Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

1. Proveďte změny v Azure Enterprise Portal, abyste mohli fakturovat správce oddělení pro kanadské nasazení.
2. Implementujte Azure Cost Management.
    1. Vytvořte správnou úroveň oboru přístupu, která se má sjednotit podle vzoru předplatného a vzoru seskupení prostředků. Za předpokladu, že se přizpůsobuje přizpůsobení MVP MVP definovaného v předchozích článcích, vyžaduje přístup k **oboru účtu registrace** pro tým zásad správného řízení pro Cloud, který běží na vytváření sestav vysoké úrovně. Další týmy mimo zásady správného řízení, jako je tým kanadských zakázek, budou vyžadovat přístup k **oboru skupiny prostředků** .
    2. Vytvořte rozpočet v Azure Cost Management.
    3. Projděte si úvodní doporučení a vyjednání s nimi. Doporučuje se mít opakovaný proces pro podporu procesu vytváření sestav.
    4. Nakonfigurujte a spusťte vytváření sestav Azure Cost Management, jak počáteční, tak i opakovaný.
3. Azure Policy aktualizace.
    1. Audit značek, skupin pro správu, předplatných a hodnot skupin prostředků k identifikaci jakékoli odchylky.
    2. Vytvořte možnosti velikosti SKU pro omezení nasazení na SKU uvedené v dokumentaci plánování nasazení.

## <a name="conclusion"></a>Závěr

Přidání výše uvedených procesů a změn do MVP pro řízení správného řízení pomáhá napravit mnoho rizik spojených se správou nákladů. Dohromady vytvářejí viditelnost, zodpovědnost a optimalizaci potřebné k řízení nákladů.

## <a name="next-steps"></a>Další kroky

V důsledku toho, že při přijetí cloudu roste a přináší další obchodní hodnotu, rizika a potřeby zásad správného řízení cloudu se také změní. V rámci této fiktivní společnosti je dalším krokem použití této investice do zásad správného řízení pro správu více cloudů.

> [!div class="nextstepaction"]
> [Zlepšení pro více cloudů](./multicloud-improvement.md)
