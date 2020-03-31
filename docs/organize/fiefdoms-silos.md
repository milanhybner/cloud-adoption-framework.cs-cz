---
title: Sila a fiefdoms
description: Přečtěte si o antipatternech, které můžou v organizacích zablokovat růst místo. Konkrétně se dozvíte o přízpůsobech sila a fiefdom.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 1586b6322b34e10f989934c9580e81583061d83c
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80428328"
---
# <a name="organizational-antipatterns-silos-and-fiefdoms"></a>Antipatterny organizace: sila a fiefdoms

Úspěch v rámci jakékoli zásadní změny firemních postupů, jazykové verze nebo technologických operací vyžaduje růst místo. Na srdci růstu místo je přijetí změn a možnost vést k nejednoznačnosti.

Některé antipatterny můžou blokovat růst místo v organizacích, které chtějí růst a transformovat, včetně mikrořízení, odchýlení a vyloučení postupů. Mnohé z těchto blokování představují osobní výzvy, které pro každého mají za úkol vytvořit osobní možnosti růstu. Ale dva běžné antipatterny v nich vyžadují více než jednotlivý nárůst nebo splatnost: sila a fiefdoms.

![Porovnání zdravých týmů a antipatternů organizace](../_images/ready/fiefdom-and-silo.png)

Tyto antipatterny jsou výsledkem organických změn v různých týmech, což vede k nesprávnému chování organizace. Pro vyřešení rezistence způsobené jednotlivými antivzorci je důležité pochopit hlavní příčinu tohoto vytvoření.

## <a name="healthy-organic-it-teams"></a>V pořádku, organické IT týmy

Je přirozené vytvořit divizi práce v rámci IT. Je v pořádku, aby se navázaly týmy, které mají podobné znalosti, sdílené procesy, společný cíl a zarovnaný výhled. Pro tyto týmy je také přirozené, že mají vlastní mikrojazykovou kulturu, sdílené normy a perspektivy.

V dobrém týmu IT se zaměřuje na spolupráci s ostatními týmy, aby bylo možné povýšit úspěšné dokončení jejich povinností. V dobrém týmu IT jsou porozumět obchodním cílům, na které je jejich podíl na technologii podporován. Podrobnosti a finanční dopady můžou být fuzzy, ale příspěvek na hodnotu týmu je často srozumitelný v rámci týmu.

I když v dobrém týmu IT jsou zaujetí pro technologii, kterou podporují, jsou otevřené ke změně a ochotni vyzkoušet nové věci. Tyto týmy jsou často nejstaršími a nejsilnějšími přispěvateli úsilí [Cloud Center of vynikající (CCoE)](./cloud-center-of-excellence.md) . Jejich příspěvek by měl být silně povzbuzený.

### <a name="natural-resistance-to-change"></a>Přírodní odolnost ke změně

V některých případech mohou mikrojazykové verze v rámci týmů IT, které jsou v pořádku, reagovat špatně na výkonné nebo nejshora dolů rozhodnutí o změně. Tato reakce je přirozená, protože kolektivních lidí se sdílenými normami často spolupracují při překonání externích hrozeb.

Změny, které mají vliv na každodenní úlohy týmu, smyslem zabezpečení nebo autonomii, se dají zobrazit jako rizika pro kolektivní účely. Známky rezistence jsou často indikátorem, který členy týmu nevyhovují, protože jsou součástí procesu rozhodování.

Když cloudové architekti a další vedoucí investovali do odstranění osobních bias a řízení pro zahrnutí stávajících IT týmů, je možné, že je tato odolnost v průběhu času v čase rychlá a nevyřešená. K dispozici je jeden nástroj pro cloudové architekty a vedoucí k vytvoření celkového rozhodování o tom, že je založen na CCoE.

### <a name="healthy-friction"></a>Tření v dobrém stavu

Odolnost proti tření se snadno Zaměňujte. Stávající týmy IT můžou být v souvislosti s minulými chybami, hmotnými riziky, samosprávné poznatky o řešeních a nedokumentovanými technickými dluhy. V rámci konkrétního technického řešení bohužel může healthiest IT tým přejít do depeše s popisem těchto důležitých datových bodů, které by se neměly měnit. Tento přístup ke komunikačním maskám komunikuje týmy a vytváří vnímání rezistence.

Poskytováním těchto týmů mechanizmus pro komunikaci v budoucnosti, která se díváte na budoucnost, bude přidávat datové body, identifikovat mezery a vytvářet dobré potíže kolem navrhovaných řešení. Tento dodatečný tření bude sestavovat hrubou hranu na řešeních a řídit dlouhodobé hodnoty. Pouhá změna konverzace může vytvořit přehlednost kolem složitých témat a generovat energii pro zajištění více úspěšných řešení.

Pokyny k [definování podnikových zásad](../govern/corporate-policy.md) se zaměřené na to, aby se v obchodních zúčastněných podnicích usnadnily konverzace na základě rizik. Stejný model se ale dá použít k usnadnění konverzací s týmy, které jsou vnímané jako odolné vůči cloudům. V případě, že je vnímání rezistence širší, může být vhodné zahrnout postupy rozlišení rezistence do chartu pro [tým zásad správného řízení cloudu](./cloud-governance.md).

## <a name="antipatterns"></a>Antipatterny

Ekologický a reagující růst v něm, který vytváří zdravé týmy IT, může také vést k antipatternům, které blokují transformaci a přijetí cloudu. Siloy IT a fiefdoms se liší od přirozených jazykových kultur v zdravých IT týmech. V obou vzorcích se zaměřuje fokus týmu na ochranu svých "Turf". Pokud jsou členové týmu zakryti s příležitostí k řízení operací změny a zlepšení, budou investovat více času a energie na blokování změny než hledání pozitivního řešení.

Jak už bylo zmíněno dříve, IT týmy v pořádku můžou vytvářet přirozené odpory a pozitivní tření. Sila a fiefdoms jsou jinou výzvou. Pro antipattern není k dispozici žádný dokumentovaný indikátor začátku. Tyto antipatterny se obvykle identifikují po měsících [cloudové centra excelence](./cloud-center-of-excellence.md) a [týmu zásad správného řízení cloudu](./cloud-governance.md) . Jsou zjištěny jako výsledek průběžné rezistence.

I v toxických kulturách by snaha CCoE a tým zásad správného řízení cloudu měla pomáhat při rozšiřování kulturního růstu a technického pokroku. Po měsících je možné, že několik týmů stále nezobrazuje žádné příznaky celkového chování a stálou firmu v jejich rezistenci ke změně. Tyto týmy jsou nejspíš v jednom z následujících modelů antipattern: sila a fiefdoms. I když tyto modely mají podobné příznaky, hlavní příčina a přístupy k odolnosti proti nim jsou mezi nimi rozdílné.

## <a name="it-silos"></a>Sila IT

Členové týmu v silu IT mohou definovat sami sebe prostřednictvím jejich zarovnání na malý počet dodavatelů IT nebo oblasti technické specializace. Nepleťte si ale své sila s IT fiefdoms. Siloy by měly být založené na pohodlí a zaujetí a siloy často usnadňují jejich překonání než u obav řízených fiefdoms.

Tento antipattern často vystává ze společného zaujetí pro konkrétní řešení. Siloy IT se pak posílí pokročilou dovedností týmu v důsledku investic do tohoto konkrétního řešení. Tato nadřazená dovednost může být akcelerátorem snahy o přijetí do cloudu, pokud se odolnost proti změnám může překonat. Může se také stát hlavním blokováním, pokud jsou sila rozčleněné nebo pokud členové týmu nemůžou přesně vyhodnotit možnosti. Naštěstí se siloy IT můžou často překonat bez jakýchkoli podstatných změn v organizačním diagramu.

### <a name="address-resistance-from-it-silos"></a>Odolnost proti adresám od sila IT

Siloy IT se dají řešit pomocí následujících přístupů. Nejlepší přístup bude záviset na hlavní příčině rezistence.

**Vytvořit virtuální týmy:** Oddíl [připravenost organizace](./index.md) v rámci architektury cloudového přijetí popisuje vícevrstvou strukturu pro integraci a definování čtyř virtuálních týmů (v-Teams). Jednou z výhod této struktury je viditelnost a zahrnutí mezi různými organizacemi. Představujeme [cloudové centrum špičkového](./cloud-center-of-excellence.md) týmu vytvoří vysoce profilující nedostatečný tým, na který se budou chtít zapojit technici. To pomáhá vytvářet nová zarovnání mezi řešeními, která nejsou svázána s omezeními organizačního grafu, a bude zajišťovat zahrnutí špičkových techniků, kteří byli chráněni v silech IT.

Zavedení [týmu cloudové strategie](./cloud-strategy.md) vytvoří okamžitou viditelnost příspěvků IT v souvislosti s úsilím o přijetí do cloudu. Když silou v boji bojují oddělení, tato viditelnost může pomoci motivům IT a podnikatelským vedoucím zajistit správnou podporu těchto rezistentních členů týmu. Tento proces je rychlou cestou k zapojení účastníků a podpoře.

**Zvažte experimentování a expozici:** Členové týmu v silu IT se pravděpodobně omezili tak, aby si určitý čas museli zabývat nějakým způsobem. Přerušení jednoho záznamu je prvním krokem k adresování rezistence.

Experimentování a vystavení jsou výkonné nástroje pro rozdělení překážek v silech. Členové týmu mohou být odolní vůči konkurenčním řešením, takže je nebudete moci považovat za experimenty, které soutěží se stávajícím řešením. V rámci první zátěžového testu cloudu ale organizace by měla implementovat konkurenční řešení. Silou týmu by měl být přizván, aby se mohl zúčastnit jako vstup a kontrola zdroje, ale ne jako tvůrce rozhodnutí. To by mělo být jasně sděleno týmu, společně s závazkem zapojit tým jako tvůrce rozhodnutí před přechodem do produkčních řešení.

Během revize konkurenčního řešení použijte postupy uvedené v tématu [definování podnikových zásad](../govern/corporate-policy.md) , které vám pomůžou zdokumentovat hmotná rizika experimentu a vytvořit zásady, které pomůžou silou týmu lépe vyhovovat vašemu budoucímu stavu. Tím zveřejníte tým pro nová řešení a posílíte budoucí řešení.

**Být "bez ohraničení":** Týmy, které řídí přijetí v oblasti cloudu, usnadňují nabízení hranic tím, že budou zkoumat zajímavá a nová řešení nativní pro Cloud. Jedná se o jednu polovinu přístupu k odebrání hranic. To však může dál posílit silou IT. Příliš rychlé doručování změn a bez ohledu na stávající jazykové verze může způsobit nefunkční tření a vede k přirozené rezistenci.

Když siloy začnou odolat, je důležité mít ve svých vlastních řešeních "hranici bez omezení". Je potřeba mít na vědomí jednu jednoduchou pravdivost: Cloud-Native není vždy nejlepším řešením. Uvažujte o hybridních řešeních, která by vám mohla nabídnout možnost roztáhnout stávající investice do sila IT do budoucna.

Zvažte také cloudové verze řešení, které tým silou IT používá nyní. Experimentujte s těmito řešeními a vystavte si je na pohled těch, kteří žijí v silu IT. V případě potřeby získáte novou perspektivu. V mnoha situacích se může stát, že se dodrží dostatečný ohled na to, jak snížit odolnost.

**Investovat do vzdělávání:** Mnoho lidí žijících v silu IT se stal zapálených o aktuálním řešení v důsledku rozšiřování jejich vlastního vzdělávání. Investice do vzdělávání těchto týmů je zřídka Neumístěná. Přidělte čas těmto jednotlivcům, aby se zapojili do samoobslužného vzdělávání, tříd nebo dokonce konferencí a přerušili si každodenní fokus na aktuálním řešení.

Pro vzdělávání, které by mohlo být investicem, se musí v důsledku výdajů nacházet nějaká vrácení. V systému Exchange pro investice může tým předvést navržené řešení do zbytku týmů zapojených do přijetí v rámci cloudu. Můžou také poskytnout dokumentaci k hmotným rizikům, přístupům pro řízení rizik a požadovaným zásadám při přijímání navrženého řešení. Každá z nich bude tyto týmy zapojit do řešení a pomůže vám využít jejich samosprávné znalosti.

**Převeďte překážek na rychlost:** Siloy IT mohou zpomalit nebo zastavit jakoukoli transformaci. Experimentování a iterace se vyhledají způsobem, ale jenom v případě, že se projekt stále přesouvá. Zaměřte se na to, jak překážek zapínat do pouze rychlosti. Můžete definovat zásady, se kterými se v systému Exchange budou moct všichni dočasně považovat za pokračující průběh.

Pokud je například zabezpečení roadblock, protože jeho řešení zabezpečení nemůže monitorovat ohrožení chráněných dat v cloudu, vytvořte zásady klasifikace dat. Zabraňte nasazení klasifikovaných dat do cloudu, dokud nebudete moct najít přijmoutelné řešení. Pozvěte zabezpečení IT na experimentování s hybridními nebo nativními řešeními cloudu a monitorujte chráněná data.

Pokud síťový tým funguje jako silo, identifikujte úlohy, které jsou samostatně obsažené, a síťové závislosti. Paralelně, Experimentujte, zveřejňujte a pedagogujte síťový tým při práci na hybridních nebo alternativních řešeních.

**Musí být pacient a musí obsahovat:** Nachází se na to, že se přesunete bez podpory jeho sila. Toto rozhodnutí ale způsobí přerušení a překážekí provozu. Změna mozky ve členech silou IT může nějakou dobu trvat. Musí být pacientem přirozené rezistence – převeďte ho na hodnotu. Přistavte se do zdravého tření a vylepšete budoucí řešení.

**Nikdy nesoutěžte:** Z důvodu existuje silou IT. Z důvodu trvá. Existuje investice do zachování řešení, o které členové týmu zapálenýchi. Přímé konkurenční řešení nebo silou IT se navíc z reálného cíle na dosažení obchodních výsledků. Tato depeše zablokovala mnoho transformačních projektů.

Zajistěte si zaměření na cíl, a to na rozdíl od jediné součásti cíle. Pomůžou vám dodávat pozitivní aspekty řešení IT sila a pomáhat členům týmu při rozhodování o nejvhodnějších řešeních pro budoucnost. Neinsult ani negradujte aktuální řešení, protože by counterproductive.

**Partner s firmou:** Pokud silou IT neblokuje obchodní výsledky, proč se vám postará? Neexistuje žádný dokonalý řešení ani dokonalý dodavatel IT. V důsledku existuje konkurence; Každá z nich má své výhody.

Zapojte se do rozmanitosti a zahrňte do svého podnikání podporu a zarovnejte ho se silným [týmem cloudové strategie](./cloud-strategy.md). Když silo IT podporuje řešení, které blokuje obchodní výsledky, bude snazší komunikovat s roadblock bez hluku technického squabbles. Podpora neblokování vydaných silou IT vám umožní partnerům považovat za požadované obchodní výsledky. V případě, že silo IT prezentuje legitimní blokování, budou tyto snahy získávat větší ohled a větší podporu firmy.

## <a name="it-fiefdoms"></a>Fiefdoms IT

Členové týmu v IT fiefdom mohou definovat sami sebe prostřednictvím jejich zarovnání na konkrétní proces nebo oblast zodpovědnosti. Tým funguje za předpokladu, že vnější vliv na jeho oblast odpovědnosti vede k problémům. Fiefdoms se může jednat o Nespor řízený antipattern, který bude vyžadovat významnou podporu vedoucí k překonání.

Fiefdoms jsou obzvláště běžné v organizacích, které mají zkušenosti IT možnost, časté turbulence v IT odděleních nebo nekvalitním vedoucím IT. Když se obchodní oddělení uvidí výhradně jako nákladové středisko, fiefdoms je mnohem pravděpodobnější.

Obecně platí, že fiefdoms je výsledkem správce linky, který obavy ztrátu týmu a přidružené napájecí základny. Tyto vedoucí často mají smysl ke svému týmu a potřebují chránit své podřízené položky před negativními důsledky. Fráze, jako je například "Ochrana týmu před změnou" a "Ochrana týmu před přerušením procesu", mohou být indikátory překrytého manažera, který může vyžadovat větší podporu od vedoucího procesu.

### <a name="address-resistance-from-it-fiefdoms"></a>Odolnost proti adresám od IT fiefdoms

Fiefdoms může předvést určitý nárůst pomocí přístupů za účelem [vyřešení rezistence pro sila IT](#address-resistance-from-it-silos). Před pokusem o vyřešení rezistence od IT fiefdom doporučujeme, abyste před týmem nacházeli jako s silou IT. Pokud tyto typy přístupů nepřinesou značnou změnu, může být odolný tým trpící antipatternem IT fiefdom. Hlavní příčinou IT fiefdoms je poněkud složitější adresa, protože tento odolnost je zavedená od přímého manažera line (nebo vedoucího navýšení v organizačním grafu). Problémy, které jsou řízeny silou, jsou obvykle jednodušší k překonání.

Pokud je pokračující odolnost od IT fiefdoms zablokuje úsilí o přijetí cloudu, může být vhodné vzít v kombinaci úsilí, aby vyhodnotila situaci se stávajícími vedoucími IT. Před provedením rozhodnutí by měli vedoucí IT pečlivě zvážit poznatky z [týmu cloudové strategie](./cloud-strategy.md), [cloudové centra excelence](./cloud-center-of-excellence.md)a [týmu zásad správného řízení cloudu](./cloud-governance.md) .

> [!NOTE]
> Vedoucí by nikdy neměli provádět změny v organizačním diagramu lehce. Měly by taky ověřovat a analyzovat zpětnou vazbu ze všech pomocných týmů. Nicméně transformační úsilí, jako je třeba testování v cloudu, je v úmyslu zvětšit základní problémy, které se před tímto úsilím neinformovaly nebo nevyřešily dlouho. V případě, že fiefdoms brání úspěchu společnosti, je pravděpodobná změna vedoucího prvku.
>
> Naštěstí odebrání vedoucího procesu fiefdom často nekončí ukončením. Tyto silné zapálených vedoucí se často můžou po krátké době reflexe přesunout do role správy. Díky správné podpoře může být tato změna v pořádku pro vedoucí fiefdom a aktuální tým.

<!-- -->

> [!CAUTION]
> Pro správce IT fiefdoms je ochrana týmu před rizikovou hodnotou jasného vedoucího. Mezi ochranou a izolací je ale dostačit čára. Pokud je tým zablokován z účasti na změnách v řízení, může mít psychologický a profesionální důsledky pro tým. Považovat za nevhodný nárok na změnu může být silná, zejména v době viditelné změny.
>
> Správce kteréhokoli izolovaného týmu může nejlépe předvést růst místoi experimentováním s pokyny spojenými s dobrými týmy IT v předchozích částech. Aktivní a optimistická účast v činnostech zásad správného řízení a CCoE může vést k osobnímu růstu. Správci IT fiefdoms jsou nejlépe umístěním, aby změnili Stifling mindsets a mohli týmu přispět k vývoji nových nápadů.

Fiefdoms může být znaménkem systémových potíží s vedoucími. Aby bylo možné překonat IT fiefdom, vedoucí oddělení IT potřebují schopnost provádět změny operací, odpovědností a občas i osob, které poskytují správu řádků konkrétních týmů. Pokud jsou tyto změny požadovány, je vhodné tyto změny řešit pomocí jasných a defensible datových bodů.

K zajištění potřebné změny se může vyžadovat sblížení obchodních zúčastněných stran, motivů v podniku a výsledků firmy. Partnerství s [týmem cloudové strategie](./cloud-strategy.md), [cloudovou službou excelence](./cloud-center-of-excellence.md)a [týmem zásad správného řízení cloudu](./cloud-governance.md) můžou poskytovat datové body, které jsou potřebné pro defensible pozici. V případě potřeby by měly být tyto týmy zapojené do eskalace skupiny, aby se vyřešily výzvy, které se nedají řešit samotným vedoucím IT.

## <a name="next-steps"></a>Další kroky

Přerušení práce v organizaci je úsilím týmu. K tomu, abyste mohli pracovat s těmito pokyny, Projděte si Úvod k organizaci připravenosti organizace a Identifikujte správné týmové struktury a účastníky:

> [!div class="nextstepaction"]
> [Identifikujte správné týmové struktury a účastníky](./index.md)
