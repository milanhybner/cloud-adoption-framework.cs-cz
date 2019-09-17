---
title: Vyhodnocení tolerance rizik
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vysvětlení obchodních rizik spojených s transformací cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: cd8bee6cf7cf0ff06cb2846b440263cc83757f5f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027702"
---
# <a name="evaluate-risk-tolerance"></a>Vyhodnocení tolerance rizik

Každé obchodní rozhodnutí vytvoří nová rizika. Investice do nějakého podílu vzniká rizikem ztrát. Nové produkty nebo služby vytvářejí rizika při selhání trhu. Změny stávajících produktů nebo služeb můžou snížit podíl na trhu. Transformace cloudu neposkytuje řešení Magical pro běžné obchodní riziko. V opačném případě připojená řešení (v cloudu nebo v místním prostředí) zavádějí nová rizika. Nasazení prostředků do libovolného zařízení připojeného k síti také rozbalí potenciální profil hrozeb tím, že odhalí slabiny zabezpečení mnohem širší a globální komunitě. Naštěstí poskytovatelé cloudu mají informace o změnách, zvýšení a přidání rizik. Investovaly do značné míry ke snížení a správě těchto rizik jménem svých zákazníků.

Tento článek se nezaměřuje na rizika cloudu. Místo toho se postará o obchodní rizika spojená s různými formami cloudové transformace. V níže uvedeném článku se diskuze přesune na diskuzi o způsobech, jak porozumět toleranci firmy při riziku.

<!-- markdownlint-disable MD026 -->

## <a name="what-business-risks-are-associated-with-a-cloud-transformation"></a>Jaká podniková rizika jsou přidružená k transformaci cloudu?

Skutečná obchodní rizika jsou založena na podrobnostech specifických transformací. Několik běžných rizik představuje úvodníka konverzace pro pochopení podnikových rizik.

> [!IMPORTANT]
> Než si přečtete následující, mějte na paměti, že je možné spravovat každé z těchto rizik. Cílem tohoto článku je informovat a připravit čtenáře pro lepší diskuzi o řízení rizik.

- **Porušení dat:** Počet rizik přidružených k jakékoli transformaci představuje ochranu dat. Nevracení dat může způsobit značnou škodu vaší společnosti, což vede ke ztrátě zákazníků, snížení obchodu nebo dokonce právní zodpovědnosti. Jakékoli změny způsobu, jakým se data ukládají, zpracovávají nebo využívají, vytváří riziko. Cloudové transformace vytvářejí vysoký stupeň změny v souvislosti se správou dat, takže by riziko nemělo být pokaždé lehce. Jednotlivé [standardní hodnoty zabezpečení](../security-baseline/index.md), [klasifikace dat](./data-classification.md)a [přírůstkové racionalizace](../../digital-estate/rationalize.md#incremental-rationalization) mohou spravovat toto riziko.

- **Přerušení služby:** Firemní operace a prostředí pro zákazníky spoléhají na technické operace. Cloudové transformace vytvoří změnu v provozu IT. V některých organizacích je tato změna malá a snadno upravena. V jiných organizacích můžou tyto změny vyžadovat přesazování, rekurzi nebo nové přístupy k podpoře cloudových operací. Větší změna, tím větší je možný dopad na obchodní provoz a prostředí pro zákazníky. Správa tohoto rizika bude vyžadovat zapojení firmy do plánování transformace. Plánování vydání a první výběr úloh v článku [přírůstkové racionalizace](../../digital-estate/rationalize.md#incremental-rationalization) projednávají způsoby, jak zvolit úlohy pro transformační projekty. Role firmy v této aktivitě je určena k sdělování rizik obchodních operací se změnou prioritních úloh. Pomoc při výběru úloh, které mají nižší dopad na operace, sníží celkové riziko.

- **Řízení rozpočtu:** Modely nákladů se mění v cloudu. Tato změna může vytvořit rizika spojená s přetečením nákladů nebo zvýšit náklady na prodané zboží (COGS), zejména přímo s atributy provozní výdaje. Když firmy úzce spolupracuje, je vhodné vytvořit transparentnost týkající se nákladů a služeb spotřebovaných různými obchodními jednotkami, programy nebo projekty. [Cost management](../cost-management/index.md) poskytuje příklady toho, jak firmy, tak i to, jak se může vymezit v tomto tématu.

Výše uvedené jsou některé z nejběžnějších rizik zmíněných zákazníky. Tým zásad správného řízení cloudu a týmy pro přijetí v cloudu můžou začít vyvíjet profil rizika, protože úlohy se migrují a připravují na produkční verzi. Připravte se na konverzace, abyste mohli definovat, zdokonalovat a spravovat rizika na základě požadovaných obchodních výsledků a jejich transformačního úsilí.

## <a name="understanding-risk-tolerance"></a>Princip tolerance rizik

Identifikace rizika je poměrně přímým procesem. Rizika související s IT jsou obecně standardně v různých oborech. Tolerance těchto rizik je však specifická pro každou organizaci. To je bod, ve kterém se v podnikových a IT konverzacích stává reagovat. Každá strana konverzace se v podstatě projeví v jiném jazyce. Následující porovnání a otázky jsou navržené tak, aby se spouštěly konverzace, které pomůžou každé straně lépe pochopit a vypočítat toleranci rizik.

## <a name="simple-use-case-for-comparison"></a>Jednoduchý případ použití pro porovnání

Abychom lépe pochopili toleranci rizik, prohlížíme zákaznická data. Pokud společnost v jakémkoli odvětví účtuje zákaznická data na nezabezpečeném serveru, je toto technické riziko napadených nebo odcizených dat zhruba stejné. Tolerance společnosti pro toto riziko se však bude rozlišovat volně, na základě povahy a potenciální hodnoty dat.

- Společnosti v oblasti zdravotnictví a finance v USA se řídí tuhými požadavky jiných výrobců. Předpokládá se, že osobní údaje nebo údaje týkající se zdravotní péče jsou mimořádně důvěrné. Existují závažné důsledky pro tyto typy společností, pokud se týkají výše uvedeného scénáře rizika. Jejich tolerance bude extrémně nízká. Všechna zákaznická data publikovaná v síti nebo mimo ni budou muset řídit tyto zásady dodržování předpisů třetích stran.
- Herní společnost, jejíž zákaznická data jsou omezená na uživatelské jméno, dobu přehrávání a vysoká skóre, se nepříznivě nesetkaly, pokud se o rizikovému chování zapojí výše. I když jsou všechna nezabezpečená data ohrožená, dopad tohoto rizika je malý. Proto tolerance rizika v tomto případě je vysoká.
- Středně velký podnik, který poskytuje čisticím službám pro koberce na tisíce zákazníků, je mezi těmito dvěma extrémními tolerancemi. Zákaznická data můžou být robustnější, a to s podrobnostmi, jako je adresa nebo telefonní číslo. Obě by se daly považovat za osobní údaje a měly by se chránit. Některé požadavky zásad správného řízení ale nemusí mandating, že data jsou zabezpečená. Z perspektivy IT je odpověď jednoduchá a zabezpečení dat. Z obchodní perspektivy to nemusí být jednoduché. Firma bude potřebovat další podrobnosti předtím, než by bylo možné určit úroveň tolerance pro toto riziko.

V další části se dozvíte několik ukázkových otázek, které by mohly přispět k tomu, že podnik určí úroveň tolerance rizika pro případ použití nad nebo ostatním.

## <a name="risk-tolerance-questions"></a>Otázky tolerance rizik

V této části jsou uvedené otázky týkající se konverzace provoking ve třech kategoriích: dopad ztráty, pravděpodobnost ztráty a náklady na nápravu. Když podnik a IT partner řeší každou z těchto oblastí, je možné snadno určit rozhodnutí o vynaložení úsilí na správu rizik a celkovou toleranci vůči určitému riziku.

**Dopad ztráty:** Otázky, které určují dopad rizika. Tyto otázky můžou být obtížné (někdy nemožné) na odpověď. Vyčíslení dopadu je nejlepší, ale někdy stačí pouze v konverzaci, aby bylo možné pochopit toleranci. Rozsahy jsou také přijatelné, zejména pokud obsahují předpoklady, které tyto rozsahy určily.

- Ruší toto riziko požadavky jiných výrobců na dodržování předpisů?
- Narušuje toto riziko interní podnikové zásady?
- Je možné, že tyto rizikové náklady zákazníci nebo podíl na trhu? Pokud ano, můžou se tyto náklady kvantifikovat?
- Mohlo by toto riziko vytvořit negativní prostředí pro zákazníky? Mají tato prostředí vliv na prodej nebo výnosy?
- Mohlo by toto riziko vytvořit novou právní odpovědnost? Pokud ano, má tato ocenění přednost před započetím škod v těchto typech případů?
- Mohlo dojít k zastavení obchodních operací? Pokud ano, jak dlouho budou operace provozu?
- Mohl by toto riziko zpomalit obchodní operace? Pokud ano, jak pomalé a jak dlouho?
- V této fázi transformace je toto riziko vypnuto nebo se bude opakovat?
- Zvyšuje se riziko při transformaci v četnosti nebo zmenšování?
- Zvyšuje riziko v průběhu času pravděpodobnost nebo snižuje pravděpodobnost?
- Rozlišuje se rizikový čas v podstatě? Bude riziko úspěch nebo bude horší, pokud není vyřešeno?

Tyto základní otázky budou mít spoustu dalších informací. Po prozkoumávání dialogu v pořádku je navrženo, že příslušná rizika budou zaznamenána a je-li možno kvantifikovaná.

**Náklady na nápravu rizik:** Otázky k určení nákladů na odebrání nebo jiné minimalizaci rizika. Tyto otázky mohou být poměrně přímé, zejména pokud jsou v rozsahu zastoupené.

- Je nějaké řešení jasné? Co to stojí?
- Existují možnosti prevence a minimalizace tohoto rizika? Jaký je rozsah nákladů na tato řešení?
- Co je potřeba od firmy k výběru nejlepšího řešení pro vymazání?
- Co je potřeba z firmy a ověřit náklady?
- Jaké další výhody můžou pocházet z řešení, které by toto riziko odebralo?

Tyto otázky oproti tomu zjednodušují technická řešení potřebná pro správu nebo odebrání rizik. Tyto otázky ale komunikují s těmito řešeními způsobem, který může firma rychle integrovat do rozhodovacího procesu.

**Pravděpodobnost ztráty:** Otázky, které vám pomohou zjistit, že riziko se stane realitou. Toto je nejobtížnější oblast pro kvantifikaci. Místo toho je doporučeno, aby tým zásad správného řízení cloudu vytvořil kategorie pro komunikaci pravděpodobnosti na základě podpůrných dat. Následující otázky mohou pomáhat při vytváření kategorií, které jsou smysluplné pro tým.

- Byl proveden nějaký výzkum týkající se pravděpodobnosti realizovaného rizika?
- Může dodavatel poskytnout odkazy nebo statistiky o pravděpodobnosti dopadu?
- Existují jiné společnosti v příslušném sektoru nebo vertikálně, na které se toto riziko dosáhlo?
- Podívejte se ještě na další společnosti, na které se toto riziko dosáhlo?
- Je toto riziko jedinečné pro něco, co tato společnost nedostatečně udělala?

Po zodpovězení těchto otázek spolu s otázkami, které určí tým zásad správného řízení pro Cloud, se pravděpodobnost seskupení pravděpodobnosti projeví. V následující části najdete několik ukázek seskupení, které vám pomůžou začít:

- **Bez indikace:** Pro zjištění pravděpodobnosti bylo dokončeno dostatečné množství výzkumu.
- **Nízké riziko:** Aktuální výzkum indikuje, že riziko je nepravděpodobné.
- **Budoucí riziko:** Aktuální pravděpodobnost je nízká. Pokračující přijetí ale vyžaduje novou analýzu.
- **Střední riziko:** Je pravděpodobnější, že riziko bude mít vliv na firmu.
- **Vysoké riziko:** V průběhu času je stále pravděpodobnější, že obchod bude toto riziko realizovat.
- **Odmítnutí rizika:** Riziko je střední až vysoké. Akce v tomto nebo obchodním oddělením ale snižují pravděpodobnost dopadu.

**Určování tolerance:**

Tři výše uvedené sady otázek by měly dostatek dat pro určení počáteční tolerance. Pokud jsou rizika a pravděpodobnost nízká a náklady na nápravu rizika jsou vysoké, je pravděpodobné, že společnost nebude investovat do nápravy. V případě vysoké rizikovosti a pravděpodobnosti, že se jedná o investici, je pravděpodobnost, že se bude jednat o investici, pokud náklady nepřekročí potenciální rizika.

## <a name="next-steps"></a>Další kroky

Tento typ konverzace může přispět k podnikání a efektivně vyhodnotit toleranci. Tyto konverzace se dají použít při vytváření zásad MVP a při přírůstkových kontrolách zásad.

> [!div class="nextstepaction"]
> [Definování podnikových zásad](./policy-definition.md)
