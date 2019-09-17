---
title: Počáteční stav organizace
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Tento článek obsahuje přehled počátečního stavu organizace.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: governance
ms.openlocfilehash: 5e425a61f6b9da7fed044d06ac9323306d728261
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71021929"
---
# <a name="initial-organization-alignment"></a>Počáteční stav organizace

**Digitální transformace** na cloud computing představuje přechod z místního provozu na provoz v cloudu. Tento přechod s sebou nese i nové způsoby podnikání – po digitální transformaci se například investiční náklady na software a hardware v datových centrech změní na provozní náklady spojené s využíváním cloudových prostředků. Pojďme se podívat, jak začít pomocí [architektury přechodu na cloud pro Azure od Microsoftu](../index.md).

## <a name="the-digital-transformation-process"></a>Proces digitální transformace

Aby bylo přijetí cloudu úspěšně, musí společnost připravit organizaci, lidi i procesy na digitální transformaci. Každá společnost má jinou organizační strukturu, takže k organizační připravenosti neexistuje žádný univerzální přístup. Tento dokument popisuje základní kroky, které vaší společnosti pomohou s přípravou. Vaše organizace se bude muset zaměřit na vypracování podrobného plánu, aby mohla splnit každý z níže uvedených kroků.

Základní proces digitální transformace je následující:

1. Vytvoření týmu cloudové strategie. Tento tým zodpovídá za vedení digitální transformace. V této fázi je také důležité vytvořit tým pro zásady správného řízení a tým pro zabezpečení digitální transformace.
2. Členové týmu cloudové strategie se seznámí s novinkami v oblasti cloudových technologií.
3. V rámci příprav společnosti sestaví tým cloudové strategie obchodní případ pro digitální transformaci – vytvoří výčet všech mezer v aktuální obchodní strategii a vymezí pro ně základní řešení.
4. Sladění základních řešení s obchodními skupinami. Identifikujte zúčastněné strany v každé obchodní skupině za účelem návrhu a implementace jednotlivých řešení.
5. Přizpůsobení stávajících rolí, dovedností a procesů tak, aby zahrnovaly cloudové role, dovednosti a procesy.

<!--6. Develop processes for operating in the cloud to make solutions more robust in terms of availability, resiliency, and security.
1. Optimize solutions for performance, scalability, and cost efficiency.-->

## <a name="step-1-create-a-cloud-strategy-team"></a>Krok 1: Vytvoření týmu cloudové strategie

Prvním krokem při digitální transformaci společnosti je zapojení nejvyšších manažerů z celé organizace do týmu cloudové strategie. Tento tým sestává z nejvyšších manažerů z oblasti financí, infrastruktury IT a aplikací. Jednotlivé týmy mohlo přispět ve fázi cloudové analýzy a experimentování.

Například tým cloudové strategie může být řízen technickým ředitelem a skládat se ze členů týmu podnikové architektury, financí a IT, vedoucích techniků z různých skupin aplikací IT (lidské zdroje, finance atd.) a manažerů týmů pro infrastrukturu, zabezpečení a sítě.

Kromě toho je důležité vytvořit dva další klíčové týmy: tým zásad správného řízení a tým zabezpečení. Ty jsou zodpovědné za návrh, implementaci a průběžné audity zásad správného řízení a zásad zabezpečení ve společnosti. Členové týmu zásad správného řízení musí mít zkušenosti s ochranou prostředků, správou nákladů, zásadami skupin a podobnými tématy. Členové týmu zabezpečení musí mít dobrý přehled o aktuálních oborových standardech v oblasti zabezpečení i požadavcích společnosti na zabezpečení.

![Tým cloudové strategie s týmem zásad správného řízení a týmem zabezpečení](../_images/ready/getting-started-overview-1.png)

Úkolem týmu zásad správného řízení je návrh a implementace cloudového modelu zásad správného řízení společnosti, stejně jako nasazení a údržba prostředků sdílené infrastruktury, které jsou součástí digitální transformace. Mezi tyto prostředky patří hardware, software a cloudové prostředky nutné k připojení místní sítě k virtuálním sítím v cloudu.

Tým zabezpečení je zodpovědný za návrh a implementaci cloudových zásad zabezpečení společnosti a úzce spolupracuje s týmem zásad správného řízení. Má k dispozici rozšíření hranice zabezpečení místní sítě, aby bylo možné zahrnout virtuální sítě v cloudu. To může mít podobu nakládání s branami firewall pro příchozí i odchozí provoz v cloudové virtuální síti, stejně jako zajišťování, že nástroje a zásady neumožní nasazení neautorizovaných prostředků.

## <a name="step-2-learn-whats-new-in-the-cloud"></a>Krok 2: Seznámení se s novinkami cloudu

V rámci dalšího kroku digitální transformace by členové týmu cloudové strategie měli zjistit, jakým způsobem změní cloudové technologie podnikání společnosti. Jedná se o fázi příprav a plánování změn, které budou mít vliv na vaši společnost, lidi a technologie. Je důležité, aby členové týmu cloudové strategie porozuměli novinkám a změnám, které cloudové prostředí (ve srovnání s místním prostředím) přinese.

![Týmy cloudové strategie, zásad správného řízení a zabezpečení se seznamují s osvědčenými postupy pro provoz v cloudu.](../_images/ready/getting-started-overview-2.png)

Výchozím bodem pro porozumění cloudu je seznámení se se základními [principy fungování Azure](../getting-started/what-is-azure.md). Následně je potřeba se seznámit se [zásadami správného řízení v Azure](../govern/resource-consistency/what-is-governance.md), které vám umožní pochopit [principy správy přístupu k prostředkům](../govern/resource-consistency/resource-access-management.md).

V rámci dalšího studia by si tým zásad správného řízení měl projít pojmy a průvodce návrhem v části obsahu věnované zásadám správného řízení. Části týkající se infrastruktury a úloh obsahují užitečné informace o typických architekturách a cloudových úlohách.

## <a name="step-3-identify-gaps-in-business-strategy"></a>Krok 3: Určení mezer v obchodní strategii

V rámci dalšího kroku by měl tým cloudové strategie vytvořit seznam obchodních problémů, které bude nutné digitální transformací vyřešit. Společnost může mít například místní datové centrum, jehož hardwaru končí životnost a potřebuje výměnu. Může mít také potíže s uváděním nových funkcí a služeb na trh a zaostávat tak za konkurencí. Tyto mezery představují _cíle_ digitální transformace vaší organizace.

Mezery v obchodní strategii lze rozdělit do těchto kategorií:

| Kategorie | Popis |
| --- | --- |
| Správa nákladů | Jedná se o mezery v oblasti plateb, které společnost vynakládá na technologie. |
| Zásady správného řízení | Jedná se o mezery v procesech, pomocí kterých chrání společnost své prostředky před nesprávným použitím, které by mohlo vést k překročení nákladů, potížím se zabezpečením nebo problémům s dodržováním předpisů. |
| Dodržování předpisů | Jedná se o mezery v tom, jak společnost dodržuje vlastní interní procesy a zásady, stejně jako externí zákony, předpisy a normy. |
| Zabezpečení | Jedná se o mezery v ochraně technologií a datových prostředků před externími vlivy. |
| Zásady správného řízení dat | Jedná se o mezery ve způsobech správy dat společnosti (a to zejména zákaznických dat). Například Obecné nařízení o ochraně osobních údajů (GDPR) Evropské unie vznáší přísné požadavky na ochranu zákaznických dat, které tak mohou vyžadovat nový hardware a software. |

Jakmile vaše společnost zařadí všechny mezery v obchodní strategii do těchto kategorií, bude potřeba pro každý problém najít základní řešení.

V následující tabulce je uvedeno několik příkladů:

|Mezera v obchodní strategii|Kategorie &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|Řešení &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|-----|-----|-----|
| Služby, které jsou v současnosti hostované v místním prostředí, mají problémy s dostupností, odolností a škálovatelností během špičky, což představuje přibližně 10 procent využití. Servery v místním datovém centru se blíží konci své životnosti. IT oddělení společnosti navrhuje nákup nového místního hardwaru pro datové centrum, které dokáže pokrývat nároky během špičky.| Správa nákladů | Migrace příslušných místních úloh do škálovatelných prostředků v cloudu s platbami za skutečné využití |
| Zákony a předpisy pro správu dat vyžadují, aby společnost dodržovala soubor pravidel, která předepisují šifrování neaktivních uložených dat, což s sebou nese nutnost pořízení nového hardwaru a softwaru. | Zásady správného řízení dat | Přesunutí dat do Šifrování služby Azure Storage pro neaktivní uložená data |
| Služby hostované v místním datovém centru (respektive veřejně přístupné služby) čelí distribuovaným útokům s cílem odepření služeb (DDoS). Tyto útoky není snadné omezit a efektivně by je bylo možné vyřešit jen pomocí nového hardwaru, softwaru a pracovníků zabezpečení. | Zabezpečení | Migrace služeb do Azure a využití služby Azure DDoS Protection|

Jakmile vytvoříte seznam všech mezer v obchodní strategii a stanovíte pro ně základní řešení, určete si u jednotlivých bodů prioritu. To můžete provést tak, že mezery v každé kategorii sladíte s krátkodobými a dlouhodobými cíli společnosti. Pokud má společnost například krátkodobý cíl snížit v následujících dvou fiskálních čtvrtletích náklady na IT, mohou obchodní mezery kategorie *správa nákladů* získat prioritu díky úsporám, které se vážou ke každé z nich.

Výstupem tohoto procesu pak bude seřazený seznam základních řešení sladěných s obchodními kategoriemi.

## <a name="step-4-align-high-level-solutions-with-business-groups-to-design-solutions"></a>Krok 4: Přidružení základních řešení k obchodním skupinám a návrh řešení

Teď, když jste stanovili cíle digitální transformace, přiřadili jim prioritu a navrhli základní řešení, bude dalším krokem týmu cloudové strategie sladit každé ze základních řešení s týmy návrhu a implementace v oblasti jednotlivých obchodních skupin.

Tyto týmy projdou seznamy se základními řešeními a jejich prioritami a na jejich základě navrhnou jednotlivá řešení. Tento proces zahrnuje specifikaci nové infrastruktury a nových úloh. Také může dojít ke změnám rolí pracovníků a procesů, které se k nim vztahují. V této fázi je také důležité, aby každý z týmů návrhu přizval i tým zásad správného řízení a tým zabezpečení, aby mohly návrhy zkontrolovat. Všechny návrhy musí splňovat zásady a postupy definované týmem zásad správného řízení a týmem zabezpečení. Oba tyto týmy se také musí zúčastnit konečného schvalování každého návrhu.

![Tým cloudové strategie dodá základní řešení týmům pro návrh a implementaci.](../_images/ready/getting-started-overview-3.png)

Navrhnout jednotlivá řešení není úplně jednoduché. Při vytváření návrhů je nutné brát ohled i na jiné návrhy zpracovávané ostatními týmy. Pokud je například výsledkem několika návrhů migrace stávajících místních aplikací a služeb do cloudu, může být efektivnější je seskupit a navrhnout celkovou strategii migrace. Jindy naopak nemusí být migrace některých z místních aplikací a služeb možná – v takovém případě se může nabízet řešení nahradit je nově vyvinutými službami, anebo službami třetích stran. Jako efektivnější se ale může zdát jejich seskupení a zjištění, kde se navzájem překrývají, aby bylo možné určit, zda některá z aplikací třetích stran zajistí více než jedno řešení.

Po vytvoření řešení přejde tým do implementační fáze každého návrhu. Tuto fázi lze provést za pomocí standardních procesů řízení projektů.

## <a name="step-5-adapt-existing-roles-skills-and-process-for-the-cloud"></a>Krok 5: Přizpůsobení stávajících rolí, dovedností a procesů cloudovému prostředí

V každé fázi historie IT byly nejvýznamnější oborové změny často spojené se změnami rolí pracovníků. Během přechodu ze sálových počítačů na model klient/server z velké části vymizely role pracovníků obsluhy počítače, které nahradili správci systému. Když přišla éra virtualizace, poptávka po pracovnících obsluhujících fyzické servery poklesla, ale naopak vyvstala potřeba odborníků na virtualizaci. Podobně se role pravděpodobně změní s tím, jak instituce přechází na cloud computing. Například odborníci na datová centra budou možná vystřídáni finančními analytiky pro cloud. Dokonce i tam, kde názvy pracovních pozic v oboru IT zůstaly nezměněné, došlo k velkému posunu v každodenních pracovních rolích.

Když si pracovníci oddělení IT uvědomí, že podpora cloudových řešení vyžaduje odlišný soubor dovedností, mohou pociťovat obavy ohledně svých rolí a pozic. Ti, kteří aktivně objevují nové cloudové technologie a učí se jim, ale obavy mít nemusí. Naopak mohou přijetí cloudových služeb vést a pomoci organizaci poznat a přijmout související změny.

### <a name="capturing-concerns"></a>Zachycení obav

Během digitální transformace by každý tým měl zaznamenat jakékoli obavy, které ze strany zaměstnanců vyvstanou. Při tom se zaměřte na následující aspekty:

- **Typy obav.** Pracovníci se například mohou bránit změnám pracovních povinností, které souvisejí s digitální transformací.
- **Co se stane, když nebudou obavy řešeny.** Neochota vůči digitální transformaci může například vést k tomu, že pracovníci budou provádět změny příliš pomalu.
- **Oblast, která se může obavami zabývat.** Pokud například nejsou pracovníci oddělení IT ochotní učit se novým dovednostem, má nejlepší předpoklady k řešení těchto obav oblast účastníků IT. U některých typů obav může být snadné zjistit, která oblast by se jimi měla zabývat, jindy může být nutné postoupit problém výkonnému vedení.

### <a name="identify-gaps"></a>Identifikace mezer

Dalším aspektem procesu digitální transformace společnosti je identifikace **mezer**. Mezera představuje roli, dovednost nebo proces, které jsou nutné pro digitální transformaci, ale kterými vaše společnost momentálně nedisponuje.

Začněte vytvořením výčtu nových odpovědností, které doprovází digitální transformaci, a při tom se zaměřte na to, které z nich jsou nové a které ze stávajících už nebudou potřeba. Určete oblast spojenou s každou odpovědností. U několika nových odpovědností určete, jak těsně s danou oblastí souvisí. Některé odpovědnosti mohou přesahovat do více oblastí, což představuje příležitost, jak lépe dovednosti a oblasti spojit (takový případ by měl být zaznamenaný jako obava). Pokud se pro žádnou oblast nenajdou odpovědnosti, označte ji jako mezeru.

Dále určete, jaké dovednosti bude odpovědnost vyžadovat a zjistěte, zda vaše společnost nějaké prostředky s takovými dovednostmi už má. Pokud nejsou žádné k dispozici, určete, jaké školicí programy nebo nábor talentů budete potřebovat. Stanovte si časový rámec, v rámci kterého bude nutné odpovědnost zajistit, aby digitální transformace probíhala podle plánu.

Na závěr určete role, které budou tyto dovednosti zajišťovat. Někteří z vašich stávajících pracovníků se mohou ujmout částí těchto rolí, v jiných případech bude potřeba vytvořit úplně novou roli.

### <a name="partner-across-teams"></a>Partneři napříč týmy

Schopnosti nutné k vyplnění mezer v digitální transformaci vaší společnosti se zpravidla nebudou omezovat na jedinou roli, a dokonce ani na jediné oddělení. K dovednostem se budou vázat vztahy a závislosti, které se mohou týkat jedné nebo i více rolí, a tyto role se mohou vyskytovat ve více odděleních. Například vlastník úlohy může potřebovat, aby pracovník v roli IT zajišťoval základní prostředky, jako jsou předplatná a skupiny prostředků.

Tyto závislosti představují nové procesy, které vaše organizace implementuje za účelem správy pracovních postupů mezi rolemi. Ve výše uvedeném příkladu může vztah mezi vlastníkem úlohy a rolí IT podporovat několik různých typů procesů. Pro správu procesu tak lze vytvořit nástroj pracovního postupu, nebo můžete použít jednoduchou e-mailovou šablonu.

Sledujte tyto závislosti a poznamenejte si procesy, které je podporují (a také to, zda takové procesy už existují). Pokud procesy vyžadují nástroje, zkontrolujte, že časová osa jejich nasazení odpovídá celkovému plánu digitální transformace.

## <a name="next-steps"></a>Další postup

Digitální transformace je iterativní proces a s každou iterací se zúčastněné týmy stávají efektivnějšími.

> [!div class="nextstepaction"]
> [Přečtěte si, jak funguje Azure.](../getting-started/what-is-azure.md)
