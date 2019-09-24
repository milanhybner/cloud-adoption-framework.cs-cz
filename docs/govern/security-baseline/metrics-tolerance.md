---
title: Metriky standardních hodnot zabezpečení, indikátory a tolerance rizik
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Metriky standardních hodnot zabezpečení, indikátory a tolerance rizik
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b8171839b79ffbe9e3849cf303180d1f1ee049f2
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222854"
---
# <a name="security-baseline-metrics-indicators-and-risk-tolerance"></a>Metriky standardních hodnot zabezpečení, indikátory a tolerance rizik

Tento článek vám pomůže kvantifikovat toleranci obchodního rizika v souvislosti se směrným plánem zabezpečení. Definování metrik a indikátorů vám pomůže vytvořit obchodní případ, který zajistí investici do splatnosti pravidla standardních hodnot zabezpečení.

## <a name="metrics"></a>Metriky

Základní bezpečnostní plán se obecně zaměřuje na identifikaci potenciálních ohrožení zabezpečení v cloudových nasazeních. V rámci analýzy rizik budete chtít shromažďovat data týkající se vašeho prostředí zabezpečení a zjistit, kolik rizika čelíte a jakým způsobem jsou důležité investice do zásad správného řízení zabezpečení standardních hodnot zabezpečení pro vaše plánovaná cloudová nasazení.

Každá organizace má různá prostředí zabezpečení a požadavky a různé potenciální zdroje dat zabezpečení. Následují příklady užitečných metrik, které byste měli shromáždit, abyste mohli vyhodnotit toleranci rizik v rámci základny standardních hodnot zabezpečení:

- **Klasifikace dat:** Počet dat uložených v cloudu a služeb, které nejsou klasifikovány na základě ochrany osobních údajů, dodržování předpisů nebo obchodních dopadů vaší organizace.
- **Počet citlivých úložišť dat:** Počet koncových bodů úložiště nebo databází, které obsahují citlivá data a měly by být chráněny.
- **Počet nešifrovaných úložišť dat:** Počet citlivých úložišť dat, která nejsou šifrována.
- **Plocha pro útok:** Kolik celkových zdrojů dat, služeb a aplikací bude hostovaných v cloudu. Jaké procento těchto zdrojů dat je klasifikovaných jako citlivé? Jaké procento těchto aplikací a služeb je klíčové?
- **Zahrnuté standardy:** Počet standardů zabezpečení, které jsou definovány bezpečnostním týmem.
- **Zahrnuté prostředky:** Nasazené prostředky, které jsou pokryté standardy zabezpečení.
- **Celkový soulad standardů:** Poměr kompatibility dodržování standardů zabezpečení.
- **Útoky podle závažnosti:** Kolik koordinovaných pokusů o narušování služeb hostovaných v cloudu, jako jsou útoky DDoS (Distributed Denial of Service), je prostředí vaší infrastruktury? Jaká je velikost a závažnost těchto útoků?
- **Ochrana proti malwaru:** Procento nasazených virtuálních počítačů, které mají nainstalované všechny požadované antimalwarové, firewallové nebo jiné bezpečnostní software.
- **Latence opravy:** Jak dlouho to bylo, vzhledem k tomu, že virtuální počítače měly použité operační systémy a opravy softwaru.
- **Doporučení pro stav zabezpečení:** Počet doporučení pro zabezpečení softwaru pro řešení standardů pro nasazení nasazených prostředků uspořádaných podle závažnosti

## <a name="risk-tolerance-indicators"></a>Indikátory tolerance rizik

Cloudové platformy poskytují základní sadu funkcí, které umožňují týmům malého nasazení nakonfigurovat základní nastavení zabezpečení bez rozsáhlého dalšího plánování. V důsledku toho malé vývojové a testovací nebo experimentální první pracovní zátěže, které neobsahují citlivé údaje, reprezentují relativně nízkou úroveň rizika a pravděpodobně nebudou potřebovat spoustu možností formálních zásad standardních hodnot zabezpečení. Po přesunu důležitých dat nebo důležitých funkcí do cloudu se však zvyšují rizika zabezpečení, zatímco tolerance těchto rizik se rychle sníží. S tím, jak jsou vaše data a funkce nasazené do cloudu, je pravděpodobnější, že budete potřebovat vyšší investice do oboru standardních hodnot zabezpečení.

V počátečních fázích přijetí cloudu Spolupracujte se svým týmem zabezpečení IT a podnikovými stranami, abyste zjistili [obchodní rizika](./business-risks.md) související se zabezpečením a pak určili přijatelný základ pro toleranci bezpečnostního rizika. V této části architektury pro přijetí do cloudu najdete příklady, ale podrobná rizika a směrné plány vaší společnosti nebo nasazení se můžou lišit.

Jakmile budete mít základnu, stanovte minimální srovnávací testy představující nepřijatelný nárůst zjištěných rizik. Tyto srovnávací testy fungují jako triggery, pokud potřebujete provést akci k nápravě těchto rizik. Tady je několik příkladů, jak metriky zabezpečení, jako jsou třeba výše popsané, můžou zvýšit investice do základny standardních hodnot zabezpečení.

- **Aktivační událost pro klíčové úlohy.** Společnost, která nasazuje klíčové úlohy do cloudu, by měla investovat do oboru standardních hodnot zabezpečení, aby se předešlo potenciálnímu výpadku služby nebo citlivému ohrožení dat.
- **Aktivační událost chráněných dat.** Společnost hostující data v cloudu, která může být klasifikována jako důvěrná, soukromá nebo jinak podléhající regulativním předpisům. Potřebují pravidla standardních hodnot zabezpečení, aby se zajistilo, že se tato data nevztahují ke ztrátě, expozici nebo krádeži.
- **Trigger externích útoků.** Společnost, která dosahuje vážných útoků na jejich síťovou infrastrukturu _x_ měsíčně, může těžit z oboru standardních hodnot zabezpečení.
- **Aktivační událost kompatibility standardů.** Společnost s více než _x%_ prostředků z hlediska dodržování standardů zabezpečení by měla investovat do směrného plánu zabezpečení, aby zajistila konzistenci standardů v infrastruktuře IT.
- **Aktivace velikosti majetku v cloudu** Společnost hostující více než _x_ aplikací, služeb nebo zdrojů dat. Nasazení ve velkém cloudu může těžit z investic do disciplíny standardních hodnot zabezpečení, aby bylo zajištěno, že jejich celkový způsob útoku bude správně chráněn před neoprávněným přístupem nebo jinými externími hrozbami.
- **Aktivační událost dodržování předpisů pro zabezpečení softwaru.** Společnost, kde je nainstalován veškerý požadovaný bezpečnostní software menší než _x%_ nasazených virtuálních počítačů. Pomocí pravidla směrného plánu zabezpečení je možné zajistit, že software bude nainstalován konzistentně na veškerý software.
- **Trigger opravy.** Společnost, ve které se nasadily virtuální počítače nebo služby, ve kterých se operační systémy nebo opravy softwaru nepoužívaly během posledních _x_ dnů. Pomocí pravidla standardních hodnot zabezpečení je možné zajistit, aby opravy byly v požadovaném plánu v aktuálním stavu.
- **Zaměřený na zabezpečení.** Některé společnosti budou mít silné požadavky na zabezpečení a důvěrnost dat, a to i pro testovací a experimentální úlohy. Tyto společnosti budou muset investovat do směrného plánu zabezpečení, aby mohli začít všechna nasazení.

Přesné metriky a triggery, které používáte k měření tolerance rizika a úroveň investic do směrného plánu zabezpečení, budou specifické pro vaši organizaci, ale výše uvedené příklady by měly sloužit jako užitečnou základnu pro diskuzi v rámci týmu zásad správného řízení v cloudu.

## <a name="next-steps"></a>Další kroky

Pomocí [šablony pro správu cloudu](./template.md), metriky dokumentů a indikátory tolerance, které odpovídají aktuálnímu plánu přijetí do cloudu.

Projděte si ukázkový základní zásady zabezpečení jako výchozí bod pro vývoj zásad, které řeší konkrétní podniková rizika, která odpovídají vašim plánům pro přijetí v cloudu.

> [!div class="nextstepaction"]
> [Kontrola ukázkových zásad](./policy-statements.md)
