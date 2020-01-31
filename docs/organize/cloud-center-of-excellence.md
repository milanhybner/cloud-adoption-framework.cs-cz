---
title: Vedoucí centrum cloudu
description: Popisuje vytvoření cloudové centra excelence (CCoE).
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: ca5e016ac07702711d38b671d767969cd4280bd3
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801116"
---
# <a name="cloud-center-of-excellence"></a>Vedoucí centrum cloudu

Provozní a technické flexibility představují základní cíle většiny IT organizací. Cloudová centra vynikajících funkcí (CCoE) je funkce, která vytváří rovnováhu mezi rychlostí a stabilitou.

## <a name="function-structure"></a>Struktura funkce

Model CCoE vyžaduje spolupráci mezi všemi následujícími možnostmi:

- Přijetí do cloudu (konkrétně architekti řešení)
- Strategie cloudu (konkrétně správci programu a projektů)
- Zásady správného řízení cloudu
- Cloudová platforma
- Automatizace cloudu

## <a name="impact-and-cultural-change"></a>Dopad a kulturní změna

Když je tato funkce správně strukturovaná a podporovaná, můžou účastníci zrychlit inovace a migrovat úsilí a zároveň snížit celkové náklady na změnu a zvýšit flexibilitu firmy. Po úspěšné implementaci může tato funkce způsobit výrazné snížení času na uvedení na trh. Jako vyspělé týmové postupy se zlepšují indikátory kvality, včetně spolehlivosti, efektivity výkonu, zabezpečení, udržovatelnosti a spokojenosti zákazníků. Tyto zisky v efektivitě, flexibilitě a kvalitě jsou obzvláště důležité, pokud společnost plánuje implementaci úsilí zaměřeného na migraci do cloudu nebo chce Cloud používat k testování inovací spojených s rozlišením trhu.

Po úspěšném vytvoření se v modelu CCoE vytvoří významný kulturní posun. Základem CCoE přístupu je to, že slouží jako zprostředkovatel, partner nebo zástupce firmy. Tento model je paradigma posunutí od tradičního zobrazení jako jednotka operací nebo abstrakcní vrstva mezi podnikem a IT prostředky.

Následující obrázek poskytuje analogii pro tuto kulturní změnu. Bez přístupu k CCoE se v zájmu zaměřit na poskytování řízení a centrální zodpovědnosti, která působí jako semafory v průniku. Po úspěšném CCoEi se fokus zaměřuje na svobodu a delegovanou zodpovědnost, která se v průniku podobá Roundabout.

![Analogie pro CCoE paradigma Shift](../_images/ready/ccoe-paradigm-shift.png)

Ani jeden z přístupů zobrazených v analogické imagi není správný nebo špatný, jsou to pouze alternativní zobrazení zodpovědnosti a správy. Pokud je žádoucí vytvořit model samoobslužné služby, který obchodním jednotkám umožní učinit svá vlastní rozhodnutí v souladu se sadou pokynů a navázanými, opakujícími se ovládacími prvky, CCoE model by se mohl vejít do strategie technologického postupu.

## <a name="key-responsibilities"></a>Klíčové zodpovědnosti

Hlavním clem týmu CCoE je zrychlit přijímání cloudu prostřednictvím nativních nebo hybridních řešení cloudu.

Cílem CCoE je:

- Pomůžete vytvořit moderní organizaci IT prostřednictvím agilních přístupů k zachycení a implementaci podnikových požadavků.
- Použijte opakovaně použitelné balíčky pro nasazení, které odpovídají zásadám zabezpečení, dodržování předpisů a správy služeb.
- Udržujte funkční platformu Azure v souvislosti s provozními postupy.
- Zkontrolujte a schvalte používání cloudových nativních nástrojů.
- V průběhu času, standardizace a automatizace běžně potřebných komponent a řešení pro platformu.

## <a name="meeting-cadence"></a>Tempo schůzky

CCoE je funkce, kterou si zaměstnanci připracovali čtyřmi týmy pro vysokou poptávku. Je důležité zajistit ekologickou spolupráci a sledovat růst prostřednictvím společného úložiště nebo katalogu řešení. Maximalizujte přirozené interakce, ale minimalizujte schůzky. Když je tato funkce vyspělá, týmy by se měly snažit omezit vyhrazené schůzky. Účast na opakovaných schůzkách, jako jsou schůzky vydané verze hostované týmem pro přijetí v cloudu, bude poskytovat vstupy dat. Paralelně může schůze po každém plánu vydaných verzí poskytnout minimální dotykový bod pro tento tým.

## <a name="solutions-and-controls"></a>Řešení a ovládací prvky

Každý člen CCoEu se vystavuje pomocí porozumění potřebným omezením, rizikům a ochranám, které vedly k aktuální sadě ovládacích prvků IT. Kolektivní úsilí služby CCoE by mělo toto porozumění do nativních nebo hybridních řešení nebo ovládacích prvků, které umožňují požadované výsledky samoobslužné služby, zapínat. Při vytváření řešení se sdílí s různými týmy ve formě ovládacích prvků nebo automatizace, které slouží jako guardrails pro různé úsilí. Tyto guardrailsy usnadňují směrování aktivit v oblasti bezplatného toku různých týmů a zároveň přiděluje zodpovědnost účastníkům v různých případech migrace nebo inovace.

Příklady tohoto přechodu:

| Scénář | Řešení před CCoE | Řešení po CCoE |
|---------|---------|---------|
| Zřízení produkčního SQL Server | Týmy sítě, IT a datové platformy zřídí různé komponenty v průběhu dnů nebo dokonce týdnů. | Tým, který vyžaduje, aby server nasadil instanci PaaS Azure SQL Database. Alternativně můžete použít předschválenou šablonu k nasazení všech prostředků IaaS do cloudu v hodinách. |
| Zřízení vývojového prostředí | Týmy sítě, IT, vývoje a DevOps souhlasí s specifikací a nasazením prostředí. | Vývojový tým definuje své vlastní specifikace a nasadí prostředí na základě přiděleného rozpočtu. |
| Aktualizace bezpečnostních požadavků pro zlepšení ochrany dat | Sítě, IT a týmy zabezpečení aktualizují různá síťová zařízení a virtuální počítače v různých prostředích a přidávají tak ochranu. | Nástroje zásad správného řízení cloudu se používají k aktualizaci zásad, které se dají okamžitě použít pro všechny prostředky ve všech cloudových prostředích. |

## <a name="negotiations"></a>Hájí

V kořenu jakéhokoli úsilí CCoE je probíhající proces vyjednávání. Tým CCoE se domlouvá se stávajícími funkcemi IT, aby se snížil střed ovládacího prvku. Kompromisy pro podnikání v tomto jednání jsou svobodu, flexibilita a rychlost. Hodnota kompromisů pro stávající IT týmy je dodávána jako nová řešení. Nová řešení poskytují stávajícímu týmu IT s jednou nebo více následujícími výhodami:

- Možnost automatizovat běžné problémy.
- Vylepšení konzistence (snížení v každodenním frustrations).
- Možnost učit se a nasazovat nová technická řešení
- Snížení incidentů s vysokou závažností (méně rychlých oprav nebo zpožděných odpovědí s mimořádnými nočními poplatky).
- Možnost rozšířit svůj technický rozsah a řešit širší témata.
- Účast na obchodních řešeních vyšší úrovně, které řeší dopad technologie.
- Snížení úloh údržby menial
- Zvyšte strategii a automatizaci technologie.

V systému Exchange pro tyto výhody může stávající funkce IT proměňovat následující hodnoty, ať už reálné, nebo vnímané:

- Smyslem řízení z procesu ručního schválení.
- Smysl stability od řízení změn.
- Smysl zabezpečení úlohy od dokončení nezbytných úloh, které se ještě opakují.
- Smysl konzistence, která přichází z hlediska dodržování stávajících dodavatelů řešení IT.

V zdravých společnostech předávaných v cloudu je tento proces vyjednávání dynamická konverzace mezi partnerskými a partnerskými týmy IT. Technické podrobnosti můžou být složité, ale dají se spravovat, když rozumí cíli a podporují CCoE úsilí. Pokud je menší než podpora, následující část týkající se povolení úspěchu CCoE může pomoci překonat kulturní blokování.

## <a name="enable-ccoe-success"></a>Povolit úspěch CCoE

Než budete pokračovat v tomto modelu, je důležité ověřit toleranci společnosti pro růst místo a je to dobré, aby se uvolnily střední zodpovědnosti. Jak je uvedeno výše, účelem CCoE je vyměňovat si řízení flexibility a rychlosti.

Tento typ změny přebírá čas, experimentování a vyjednávání. V rámci tohoto procesu maturation se budou nastavovat a vracet. Pokud ale tým zůstane pečlivé vylaďování a z experimentu se nedoporučuje, existuje vysoká pravděpodobnost úspěchu v vylepšení flexibility, rychlosti a spolehlivosti. Jedním z největších faktorů, které úspěch nebo neúspěch služby CCoE, je podpora vedoucích a klíčových zúčastněných stran.

### <a name="key-stakeholders"></a>Klíčové účastníky

Vedoucí oddělení IT je první a nejvíce zjevný účastník. Manažeři IT budou hrát důležitou část. V průběhu tohoto procesu se ale vyžaduje podpora CIO a dalších vedoucích IT.

Méně zřejmější je nutnost obchodních zúčastněných stran. Flexibilita firmy a doba uvedení na trh jsou klíčové motivace pro vytváření CCoE. V takovém případě by měly mít hlavní účastníci v těchto oblastech svěřený zájem. Příklady obchodních účastníků zahrnují obchodní vedoucí pracovníky, finanční ředitele, vedoucí pracovníky a vlastníky obchodních produktů.

### <a name="business-stakeholder-support"></a>Podpora obchodních účastníků

CCoE úsilí se dá urychlit díky podpoře od obchodních účastníků. Většina zaměření na CCoE úsilí je zaměřená na vytváření dlouhodobých vylepšení flexibility a rychlosti firmy. Definování vlivu aktuálních operačních modelů a zvýšení hodnoty je užitečné jako průvodce a nástroj pro vyjednávání pro CCoE. Pro podporu CCoE je navržena dokumentace k následujícím položkám:

- Vytvořte sadu obchodních výsledků a cílů, které se očekávají v důsledku flexibility a rychlosti podniku.
- Jasně definujte bolesti, které vytváří aktuální IT procesy (například rychlost, flexibilitu, stabilitu a problémy s náklady).
- Jasně definujte historický dopad těchto bolestních bodů (například ztracené podíly na trhu, zisk konkurence v funkcích a funkcích, špatné zkušenosti zákazníků a zvýšení rozpočtu).
- Definujte příležitosti pro zlepšení obchodu blokované aktuálními a provozními modely.
- Navažte časové osy a metriky týkající se těchto příležitostí.

Tyto datové body nezpůsobují útok. Místo toho se jim postará o CCoEi a navázat reálné nevyřízené položky a naplánujte zlepšení.

**Průběžná podpora a zapojení:** CCoE týmy můžou Ukázat rychlé návratnosti v některých oblastech. Cíle vyšší úrovně, jako je například flexibilita firmy a doba uvedení na trh, můžou trvat mnohem déle. Během maturation existuje vysoké riziko, že CCoE se nedoporučuje ani nebudete muset se soustředit na jiné úsilí v oblasti IT.

V průběhu prvních šesti až devíti měsíců CCoEho úsilí doporučujeme, aby obchodní účastníci přidělili čas k tomu, aby splnili každý měsíc a CCoE. K těmto schůzkám není potřeba formální procedury. Pouhým zobrazením CCoE členů a jejich vedoucím z hlediska důležitosti tohoto programu se můžete setkat s tím, jak CCoE úspěch.

Kromě toho doporučujeme, aby zúčastněné obchodní strany informovaly o průběhu a blokování, ke kterým má tým CCoE zkušenosti. Mnohé z jejich snahy se jeví jako technické minutiae. Je ale důležité, aby obchodní účastníci porozuměli pokroku v plánu, aby se mohli zapojit do situace, kdy tým ztratí páry nebo se může odvolávat jinými prioritami.

### <a name="it-stakeholder-support"></a>Podpora účastníků IT

**Podpora vize:** Úspěšné CCoE úsilí vyžaduje Skvělé vyjednávání se stávajícími členy IT týmu. Pokud to bude hotové, přispívá se k řešení a má jistotu, že se změna nehodí. V takovém případě se může stát, že někteří členové stávajícího IT týmu budou chtít, aby na základě různých důvodů měli na řídicí mechanismy. Podpora zúčastněných stran IT bude zásadní pro úspěch CCoE, když dojde k těmto situacím. Povzbuzování a posílení celkových cílů CCoE je důležité k překladu blokování na správné vyjednávání. Ve výjimečných případech můžou účastníci IT dokonce ještě potřebovat krokování a přerušit zablokování nebo vázaný hlas, aby CCoE pokrok.

**Zachovat fokus:** CCoE může být významným závazkem pro libovolný tým, který je omezený na prostředky. Odebrání silných architektů z krátkodobých projektů za účelem soustředění na dlouhodobé zisky může vytvořit problémy pro členy týmu, kteří nejsou součástí CCoEu. Je důležité, aby vedoucí oddělení IT a jeho zúčastněné strany zaměřily na cíle CCoE. Podpora vedoucích IT a zúčastněných stran je nutná k tomu, aby bylo možné snížit prioritu přerušení každodenních operací ve prospěch CCoEch cel.

**Vytvořit vyrovnávací paměť:** Tým CCoE bude experimentovat s novými přístupy. Některé z těchto přístupů nebudou správně zarovnány se stávajícími operacemi nebo technickými omezeními. Existuje reálné riziko, že při selhání experimentů dochází k CCoEům nebo jiným týmům. Důležitá je podpora a ukládání do vyrovnávací paměti týmu z důsledků možností učení "rychlé selhání". Je stejně důležité, aby měl tým účet k růstu místo a zajistil, že se z těchto experimentů učí a vyhledává lepší řešení.

## <a name="next-steps"></a>Další kroky

Model CCoE vyžaduje [Možnosti cloudové platformy](./cloud-platform.md) i [Možnosti automatizace cloudu](./cloud-automation.md). Dalším krokem je zarovnat [Možnosti cloudové platformy](./cloud-platform.md).

> [!div class="nextstepaction"]
> [Možnosti zarovnání cloudové platformy](./cloud-platform.md)
