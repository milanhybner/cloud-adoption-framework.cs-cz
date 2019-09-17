---
title: Definování podnikových zásad pro zásady správného řízení cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se vytvářet zásady, které odpovídají a napravují rizika.
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/02/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 699fe253048ba33d3964bdc3093aa4f335aaccc8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027915"
---
# <a name="define-corporate-policy-for-cloud-governance"></a>Definování podnikových zásad pro zásady správného řízení cloudu

Až budete pro cestu k transformaci cloudu vaší organizace analyzovat známá rizika a související rizikové odchylky, je dalším krokem vytvoření zásad, které budou tato rizika explicitně řešit a definovat kroky potřebné k jejich nápravě, pokud je to možné.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-corporate-it-policy-become-cloud-ready"></a>Jak se dají zásady IT připravit pro cloud?

V tradičních zásadách správného řízení i inkrementálních zásadách správného řízení se funkční definice zásad správného řízení skládá z firemních zásad. Cílem většiny akcí zásad správného řízení v oblasti IT je implementovat technologii umožňující monitorovat, vynucovat, provozovat a automatizovat tyto firemní zásady. Zásady správného řízení cloudu jsou postavené na podobných konceptech.

![Obory řízení a řízení podniku](../../_images/operational-transformation-govern-highres.png)

*Obrázek 1: Firemní zásady a disciplíny správného řízení*

Obrázek výše znázorňuje vztah mezi obchodními riziky, zásadami a dodržováním předpisů a mechanismy monitorování a vynucování, které budou muset spolupracovat jako součást vaší strategie zásad správného řízení. Pět oborů zásad správného řízení pro Cloud vám umožní spravovat tyto interakce a realizovat strategii.

Zásady správného řízení v cloudu jsou výsledkem průběžného úsilí o přechod, protože skutečně dlouhodobé transformace nejde dosáhnout přes noc. Pokusy o rychlé a agresivní zajištění kompletních zásad správného řízení v cloudu před vyřešením klíčových změn firemních zásad zřídka vedou k požadovaným výsledkům. Místo toho doporučujeme inkrementální přístup.

K tomu, co se liší v rámci architektury pro přijetí v cloudu, je to cyklus nákupu a může umožnit autentickou transformaci. Vzhledem k tomu, že neexistují žádné požadavky na pořízení velkých výdajů, můžou technici začít experimentovat a přijímat dřív. Ve většině firemních kultur odstranění překážky pro přechod v podobě kapitálových výdajů může vést k těsnějším smyčkám zpětné vazby, organickému růstu a inkrementální realizaci.

Posun k přechodu na cloud vyžaduje posun v zásadách správného řízení. V řadě organizací transformace firemních zásad umožňuje zlepšit zásady správného řízení a zvýšit míru jejich dodržování prostřednictvím inkrementálních změn zásad a automatizovaného vynucování těchto změn, které zajišťují nově definované funkce, které můžete nakonfigurovat u svého poskytovatele cloudových služeb.

<!-- markdownlint-enable MD026 -->

## <a name="review-existing-policies"></a>Kontrola stávajících zásad

Principem řízení je průběžný proces. zásady by se měly pravidelně kontrolovat u zaměstnanců IT a zúčastněných stran, aby se zajistilo, že prostředky hostované v cloudu budou i nadále zajišťovat dodržování celkových podnikových cílů a požadavků. Díky porozumění novým rizikům a přijatelné toleranci můžete [zkontrolovat stávající zásady](./cloud-policy-review.md) a určit požadovanou úroveň zásad správného řízení, která je vhodná pro vaši organizaci.

> [!TIP]
> Pokud vaše organizace používá dodavatele nebo jiné důvěryhodné obchodní partnery, jedno z největších obchodních rizik, které je potřeba vzít v úvahu, může být nedostatečným dodržováním [předpisů v souladu se zákonnými předpisy](./regulatory-compliance.md) těchto externích organizací. Toto riziko se často nedá opravit a místo toho může vyžadovat přísné dodržování požadavků všemi smluvními stranami. Než začnete s kontrolou zásad, ujistěte se, že jste identifikovali a pochopili všechny požadavky na dodržování předpisů od jiných výrobců.

## <a name="create-cloud-policy-statements"></a>Vytváření příkazů zásad cloudu

Cloudové zásady IT stanovují požadavky, standardy a cíle, které budou potřebovat oddělení IT a automatizované systémy. Rozhodnutí zásad jsou primární faktor v [návrhu architektury cloudu](./governance-alignment.md) a způsob, jakým budete implementovat [procesy](./processes.md)přizpůsobující zásady.

Jednotlivé příkazy zásad cloudu jsou pokyny pro řešení konkrétních rizik zjištěných během procesu posouzení rizik. I když se tyto zásady dají integrovat do širší podnikové dokumentace zásad, příkazy cloudových zásad, které jsou popsány v celém návodu k nasazení v cloudu, jsou stručnější Shrnutí rizik a plánů, které je potřeba řešit. Každá definice by měla obsahovat tyto informace:

- **Obchodní riziko:** Souhrn rizika, které tato zásada bude řešit.
- **Prohlášení o zásadách:** Stručné vysvětlení požadavků a cílů zásad.
- **Návrh nebo technické pokyny:** Užitečná doporučení, specifikace nebo jiné pokyny k podpoře a prosazování těchto zásad, které mohou týmy IT a vývojáři použít při navrhování a sestavování jejich nasazení v cloudu.

Pokud potřebujete nápovědu k definování zásad, Projděte si [pravidla zásad správného řízení](../governance-disciplines.md) zavedená v tématu Přehled oddílu zásad správného řízení. Články pro každou z těchto oborů obsahují příklady běžných obchodních rizik zjištěných při přechodu do cloudu a ukázkové zásady používané k nápravě těchto rizik (například najdete v tématu [definice ukázkových zásad](../cost-management/policy-statements.md)cost management).

## <a name="incremental-governance-and-integrating-with-existing-policy"></a>Přírůstkové řízení a integrace se stávajícími zásadami

Plánované přídavky do vašeho cloudového prostředí by se měly vždycky prověřené na dodržování předpisů se stávajícími zásadami a zásady se aktualizovaly na účet pro všechny problémy, které ještě nejsou popsané. Měli byste taky provést pravidelnou [kontrolu cloudových zásad](./cloud-policy-review.md) , abyste měli jistotu, že vaše zásady cloudu jsou aktuální a synchronizované se všemi novými podnikovými zásadami.

Potřeba integrovat zásady cloudu se staršími zásadami IT závisí hlavně na splatnosti vašich procesů zásad správného řízení cloudu a na velikosti vaší cloudové služby. Přečtěte si článek o [přírůstkovém řízení a MVP pro zásady](./index.md) , kde najdete širší diskuzi o řešení problémů s integrací zásad v cloudové transformaci.

## <a name="next-steps"></a>Další kroky

Po definování zásad můžete vytvořit návrh Průvodce návrhem architektury, který poskytne pracovníkům IT a vývojářům užitečné doprovodné materiály.

> [!div class="nextstepaction"]
> [Zarovnání Průvodce návrhem zásad správného řízení k podnikovým zásadám](./governance-alignment.md)
