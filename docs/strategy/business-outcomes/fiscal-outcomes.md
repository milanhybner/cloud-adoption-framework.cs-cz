---
title: Příklady fiskální výsledků
description: Příklady fiskální výsledků
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 43cd9dd0d155849c8ed5dda277252e445507f6d8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806845"
---
# <a name="examples-of-fiscal-outcomes"></a>Příklady fiskální výsledků

Na nejvyšší úrovni se finanční konverzace skládají ze tří základních konceptů:

- **Tržby:** V důsledku prodeje zboží nebo služeb bude do firmy přijít více peněz.
- **Náklady:** V rámci vytváření, uvádění na trh, prodeji nebo poskytování zboží nebo služeb bude méně peněz.
- **Zisk:** I když jsou některé z nich vzácné, můžou se u některých transformací zvýšit výnosy i snížit náklady. Toto je výsledek zisku.

Zbývající část tohoto článku vysvětluje tyto daňové výsledky v kontextu transformace cloudu.

> [!NOTE]
> Následující příklady jsou hypotetické a při přijímání jakékoli cloudové strategie by se neměly považovat za záruku vrácení.

## <a name="revenue-outcomes"></a>Výsledky výnosů

### <a name="new-revenue-streams"></a>Nové streamy příjmů

Cloud může přispět k vytváření příležitostí k poskytování nových produktů zákazníkům nebo k novému poskytování stávajících produktů novým způsobem. Nové streamy příjmů jsou inovativní, podnikatelé a zajímavé pro spoustu lidí v obchodním světě. Nové streamy příjmů jsou také náchylné k selhání a považují se za vysoce rizikové mnoho společností. V případě, že je jejich výsledky navržena v souvislosti s tržbami, pravděpodobně dojde k rezistenci. Pokud chcete k těmto výsledkům přidružit důvěryhodnost, partner s podnikovým vedoucím, který je prověřený jako inovační. Ověření datového proudu výnosů včas v procesu pomáhá předcházet překážek z firmy.

- **Příklad:** Společnost vydávala knihy po dobu více než sto let. Zaměstnanec společnosti si uvědomuje, že obsah může být elektronicky dodán. Zaměstnanec vytvoří zařízení, které se dá prodávat v knihkupectví, což umožňuje, aby se stejné knihy stáhly přímo, aby se $Xa v nové knize Prodej.

### <a name="revenue-increases"></a>Nárůst výnosů

V případě globálního škálování a digitálního dosahu může Cloud pomáhat firmám zvýšit tržby z existujících streamů příjmů. Tento typ výsledku je často vyrovnaný od zarovnání k prodejnímu nebo marketingovému vedoucímu.

- **Příklad:** Společnost, která prodává widgety, by mohla prodávat další widgety, pokud prodejci můžou bezpečně přistupovat k digitálnímu katalogu společnosti a k úrovním zásob. Tato data jsou bohužel jenom v systému ERP společnosti, ke kterému se dá dostat jenom přes zařízení připojená přes síť. Vytvořením fasády služeb pro rozhraní s ERP a vystavení seznamu katalogu a necitlivých úrovní zásob do aplikace v cloudu by mohli prodejci získat přístup k potřebným datům během pracoviště pomocí zákazníka. Rozšíření místní služby Active Directory pomocí Azure Active Directory (Azure AD) a integrace přístupu na základě role do aplikace umožní společnosti zajistit, aby data zůstala v bezpečí. Tento jednoduchý projekt může ovlivnit tržby z existující produktové řady o _x%_ .

### <a name="profit-increases"></a>Zisk se zvyšuje

Zřídka se jedná o jedno úsilí současně zvýšit výnosy a snížit náklady. Pokud k tomu ale dojde, zarovnejte příkazy výsledku z jednoho nebo více výsledků výnosů s jedním nebo více výstupy nákladů a sdělte tak požadovaný výsledek.

## <a name="cost-outcomes"></a>Náklady – výstup

### <a name="cost-reduction"></a>Snížení nákladů

Cloud Computing může snížit kapitálové výdaje na hardware a software, nastavovat datová centra, spouštět datacentra na pracovišti atd. Náklady na racky serverů, kulatou elektřinu pro napájení a chlazení a odborníky na IT, kteří spravují infrastrukturu, rychle přidávají. Vypnutí datacentra může snížit závazky kapitálových výdajů. Tato možnost se obvykle označuje jako "získávání z podnikového datacentra." Snížení nákladů se obvykle měří v dolarech v aktuálním rozpočtu, což může zahrnovat jeden až pět let v závislosti na tom, jak ředitel spravuje finanční informace.

- **Příklad #1:** Datové centrum společnosti spotřebovává vysoké procento ročního rozpočtu na IT. Rozhodne se provést migraci do cloudu a přenese prostředky v tomto datovém centru do řešení infrastruktury jako služby (IaaS), čímž se vytvoří snížení nákladů na tři roky.
- **Příklad #2:** Holdingová společnost nedávno získala novou firmu. V rámci akvizice výrazy určují, že by nová entita měla být z aktuálních datových center odebrána do šesti měsíců. Pokud to neuděláte, bude výsledkem 1 000 000 USD za měsíc holdingové společnosti. Přesunutí digitálních prostředků do cloudu v rámci migrace do cloudu může umožňovat rychlé vyřazení starých prostředků z provozu.
- **Příklad #3:** Podniková daňová společnost, která se v průběhu prvních tří měsíců v roce v rámci svých ročních příjmů dorazí na 70 procent svých ročních výnosů. Ve zbytku roku je jeho investice do značné klidové velikosti poměrně neaktivní. Migrace do cloudu by mohla dovolit nasazovat výpočetní nebo hostitelskou kapacitu potřebnou pro tyto tři měsíce. Během zbývajících devíti měsíců se IaaS náklady výrazně snížily tím, že se zmenší výpočetní nároky.

### <a name="example-coverdell"></a>Příklad: Coverdell

Coverdell modernizes své infrastruktury a zaznamenejte úspory nákladů pomocí Azure. Coverdell rozhodnutí investovat do Azure a rozhodovat svou síť webů, aplikací, dat a infrastruktury v rámci tohoto prostředí, což vedlo k většímu množství úspor za cenu, než jakou mohla společnost očekávat. Migrace do prostředí jenom pro Azure vyloučila 54 000 USD za měsíční náklady na služby pro společné umístění. S novou infrastrukturou společnosti, která je samostatná, Coverdell očekává, že během příštích dvou let ušetří odhadované 1 000 000 USD.

> "Přístup k technologickému zásobníku Azure otevírá dvířka pro některá škálovatelná, snadno implementovaná a vysoce dostupná řešení, která jsou nákladově efektivní. Naše architekti tak můžou být mnohem více kreativní pomocí řešení, která poskytují. "  
> Ryan Sorensen  
> Ředitel pro vývoj aplikací a podnikovou architekturu  
> Coverdell

### <a name="cost-avoidance"></a>Vyhnout se nákladům

Ukončení datového centra může také zabránit tomu, že se zabrání budoucím aktualizačním cyklům. Cyklus obnovování je proces nákupu nového hardwaru a softwaru, který nahradí místní systémy. V Azure jsou hardware a operační systém rutinně udržované, opravené a aktualizované bez dalších nákladů na zákazníky. Z tohoto hlediska může ředitel odebrat plánované budoucí výdaje z dlouhodobých finančních předpovědí. Vyhněte se nákladům se měří v dolarech. Liší se od snížení nákladů a obecně se zaměřuje na budoucí rozpočet, který ještě není plně schválený.

- **Příklad:** Firemní datacentrum je pro prodloužení platnosti zapůjčené po dobu šesti měsíců. Datové centrum bylo v provozu po dobu osmi let. Před 4 lety byly všechny servery aktualizovány a virtualizované, náklady na miliony dolarů společnosti. V příštím roce společnost plánuje znovu aktualizovat hardware a software. Migrace prostředků v tomto datovém centru jako součást migrace do cloudu umožňuje vyhnout se nákladům odebráním plánované aktualizace z předpokládaného rozpočtu příštího roku. Snížení nákladů také může snížit náklady na zapůjčení v reálném čase.

### <a name="capital-expenses-vs-operating-expenses"></a>Náklady na velká a provozní výdaje

Než proberete cenové výsledky, je důležité pochopit možnosti obou primárních nákladů: kapitálové výdaje a provozní výdaje.

Následující termíny vám pomůžou porozumět rozdílům mezi kapitálovými náklady a provozními náklady během obchodních diskusí o cestě transformace.

- **Velká písmena** jsou peníze a prostředky vlastněné podnikem, které přispívají k určitému účelu, jako je například zvýšení kapacity serveru nebo vytváření aplikací.
- **Kapitálové výdaje** za dlouhou dobu generují výhody. Tyto výdaje jsou všeobecně neopakované a vedou k získání trvalých prostředků. Sestavování aplikace může být kvalifikováno jako kapitálové výdaje.
- **Provozní výdaje** představují průběžné náklady na podnikání. Využívání cloudových služeb v modelu průběžných plateb se může kvalifikovat jako provozní výdaje.
- **Assety** jsou ekonomické prostředky, které mohou být vlastněny nebo kontrolovány, aby vznikly hodnoty. Všechny servery, datové jezera a aplikace je možné považovat za prostředky.
- **Odpisy** se snižují v hodnotě prostředku v průběhu času. Důležitější je, že náklady na majetek se přiřazují v obdobích, ve kterých se používají, a je tak důležitější, že se jedná o kapitálové náklady a na konverzaci s provozními náklady. Pokud například sestavíte aplikaci na tento rok, ale očekáváte, že bude mít průměrnou dobu použitelnosti pět let (jako je většina komerčních aplikací), náklady na tým a nezbytné nástroje, které jsou nutné k vytvoření a nasazení základu kódu, budou odepsány rovnoměrně za pět. letech.
- **Ocenění** je proces odhadu toho, kolik stojí společnost. Ve většině odvětví je ocenění založené na schopnosti společnosti generovat výnosy a zisk a zároveň přitom respektuje provozní náklady potřebné k vytvoření zboží, které tyto výnosy poskytují. V některých odvětvích, jako jsou maloobchodní nebo v některých typech transakcí, jako je například soukromý jmění, prostředky a odpisy, mohou hrát velkou část ocenění společnosti.

Často se jedná o bezpečný dokument, který obsahuje různé vedoucí pracovníky, včetně hlavního investičního důstojníka (CIO), které dopravuje nejlepší využití kapitálu a rozšiřují společnost v požadovaném směru. CIO a způsob převodu konverzací contentious na kapitálové náklady na jasnou odpovědnost za provozní výdaje by mohla být atraktivním výsledkem. V mnoha odvětvích aktivně finanční ředitelé (finanční ředitele) hledají způsoby, jak lépe přidružit daňovou odpovědnost za náklady na prodávané zboží.

Než však přiřadíte cestu k transformaci s tímto typem kapitálu a převodem nákladů na provoz, je vhodné se spojit se členy týmu CFO nebo CIO, aby viděli, kterou strukturu nákladů upřednostňují. V některých organizacích je vysoce *nežádoucí* výsledek snížit kapitálové výdaje ve prospěch provozních nákladů. Jak už bylo zmíněno, tento přístup se někdy zobrazuje v maloobchodních, obchodních a soukromých kapitálových společnostech, které na tradiční modely účetnictví vydávají vyšší hodnotu, což na úrovni protokolu IP je malá hodnota. Také se zobrazuje v organizacích s negativním prostředím, když je zaměstnanci oddělení IT nebo jiné funkce v minulosti.

Pokud je žádoucí model nákladů na operační systém, může být následujícím příkladem životaschopný obchodní výsledek:

- **Příklad:** Vaše datacentrum společnosti se v současnosti za další tři roky vyplatí v hodnotě _x USD_ za rok. Očekává se, že budete potřebovat další _y USD_ k aktualizaci hardwaru v příštím roce. Kapitálové výdaje můžeme převést na model provozní výdaje, a to i v hodnotě _z USD_ za měsíc, což umožňuje lepší správu a zodpovědnost za provozní náklady na provoz technologie.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o [výsledcích flexibility](./agility-outcomes.md).

> [!div class="nextstepaction"]
> [Výsledky flexibility](./agility-outcomes.md)
