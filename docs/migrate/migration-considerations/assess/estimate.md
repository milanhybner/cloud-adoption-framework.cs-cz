---
title: Odhad nákladů na cloud před migrací
description: Seznamte se s faktory, které mohou ovlivnit rozhodování a aktivity spuštění, a také různé možnosti pro odhad nákladů na Cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4e245937f6990cd6d7d13ffaccae60a2301fcb23
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312063"
---
# <a name="estimate-cloud-costs"></a>Odhad nákladů na cloud

V průběhu migrace může rozhodovací a realizační kroky ovlivňovat několik faktorů. Tento článek představuje různé možnosti pro odhad nákladů na cloud, které vám pomůžou rozpoznat, které z nich jsou v konkrétních situacích vhodné.

## <a name="digital-estate-size"></a>Velikost digitálních aktiv

Velikost vašich digitálních aktiv má přímý vliv na rozhodnutí týkající se migrace. Náklady na migraci, která zahrnuje méně než 250 virtuálních počítačů, se odhadují snadněji než náklady na migraci s více než 10 000 počítači. Pro první migraci důrazně doporučujeme zvolit menší sadu funkcí. Váš tým se tak bude moct naučit odhadnout náklady na jednoduchou migraci a teprve pak se pokusí odhadnout výdaje na rozsáhlejší a složitější migraci.

Upozorňujeme však, že i migrace malého rozsahu, které zahrnují jednu sadu funkcí, mohou vyžadovat různě velké množství podpůrných prostředků. Pokud migrujete méně než tisíc virtuálních počítačů, pro shromažďování dat o inventáři a odhad nákladů vám pravděpodobně bude stačit nástroj, jako je [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview). Další nástroje, které můžete použít pro kalkulaci nákladů, najdete v článku zaměřeném na [výpočet nákladů na digitální aktiva](../../../digital-estate/calculate.md).

Pro 1000 + jednotka Digital Estates je stále možné rozdělit odhad na čtyři nebo pět možných iterací, což zajistí, že se proces odhadu dá spravovat. V případě rozsáhlejších aktiv nebo pokud potřebujete přesnější odhad, bude situace nejspíš vyžadovat komplexnější přístup, který je popsaný v části [Digitální aktiva](../../../digital-estate/index.md) v dokumentu Architektura přechodu na cloud.

## <a name="accounting-models"></a>Účetní modely

Účetní modely

Pokud znáte tradiční procesy nákupů v oblasti IT, odhad nákladů v prostředí cloudu může působit nezvykle. V průběhu nasazení cloudových technologií se přechází z modelu s pevně stanovenými, strukturovanými výdaji na model s proměnlivými provozními náklady. V případě tradičního modelu s kapitálovými výdaji by se IT tým pokusil konsolidovat kupní sílu pro několik sad funkcí napříč různými programy tak, aby vytvořil centralizovaný fond sdílených výpočetních prostředků, které by mohly podporovat každé z těchto řešení. V prostředí, které používá model s provozními náklady na cloud, je možné vynakládat finanční prostředky tak, aby se přímo řešily požadavky jednotlivých sad funkcí, týmů nebo obchodních jednotek. Tento přístup umožňuje cíleněji vynakládat finanční prostředky na podporu interních zákazníků. Při odhadování nákladů je důležité, abyste nejprve pochopili, kolik z těchto nových možností monitorování účtů bude používat IT tým.

Pokud chcete v oblasti financí pracovat podobně jako s původními metodami kalkulace kapitálových výdajů, pro výpočet základních ročních nákladů použijte výsledky některého z postupů uvedených ve výše uvedené části [Velikost digitálních aktiv](#digital-estate-size). Dále vynásobí tyto roční náklady obvyklým cyklem aktualizace hardwaru společnosti. Cyklus aktualizace hardwaru představuje období, po jehož uplynutí společnost nahrazuje stárnoucí hardware, a obvykle se měří v letech. Roční výdaje vynásobené cyklem aktualizace hardwaru vytvoří strukturu nákladů, která bude podobná investičnímu plánu kapitálových výdajů.

## <a name="next-steps"></a>Další kroky

Jakmile bude odhad nákladů hotový, migrace může začít. Před jejím zahájením vám ale doporučujeme přečíst si [možnosti podpory a spolupráce s partnery](./partnership-options.md).

> [!div class="nextstepaction"]
> [Vysvětlení možností partnerství](./partnership-options.md)
