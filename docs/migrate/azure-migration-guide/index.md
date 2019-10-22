---
title: Úvod k průvodci migrací do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Podrobné pokyny vám pomůžou efektivně migrovat služby vaší organizace do Azure.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 2fa30c01de9d09af2c2947f940264d9156941589
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72698523"
---
::: zone target="docs"

# <a name="azure-migration-guide-before-you-start"></a>Průvodce migrací do Azure: Než začnete

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Než začnete

::: zone-end

Před migrací prostředků do Azure je potřeba zvolit metodu migrace a funkce, které použijete ke správnému řízení a zabezpečení vašeho prostředí. Tímto rozhodovacím procesem vás provede tento průvodce.

::: zone target="docs"

> [!TIP]
> Pokud chcete interaktivní prostředí, zobrazte tuto příručku na webu Azure Portal. Na webu Azure Portal přejděte do [Centra rychlého startu Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) a vyberte **Migrace prostředí do Azure**.

::: zone-end

# <a name="overviewtaboverview"></a>[Přehled](#tab/Overview)

Tento průvodce vás provede základy migrace aplikací a prostředků z místního prostředí do Azure. Je určený pro rozsahy migrace s minimální složitostí. Pokud chcete zjistit, jestli je tento průvodce vhodný pro vaši migraci, přejděte na kartu **Kdy použít tohoto průvodce**.

Při migraci do Azure můžete migrovat své aplikace tak, jak jsou, s využitím řešení virtuálních počítačů založených na modelu IaaS (označuje se jako změna hostitele nebo migrace metodou „lift and shift“) nebo můžete využít flexibilitu používat spravované služby a další funkce nativní pro cloud k modernizaci vašich aplikací. Další informace o těchto možnostech najdete na kartě **Možnosti migrace**. Při vývoji vaší strategie migrace byste měli zvážit následující:

- Budou migrované aplikace fungovat v cloudu?
- Jaká je nejlepší strategie (s ohledem na technologie, nástroje a migraci) pro aplikaci? Další informace najdete v [průvodci rozhodováním ohledně nástrojů pro migraci](../../decision-guides/migrate-decision-guide/index.md) architektury přechodu na Microsoft Cloud.
- Jak během migrace minimalizovat výpadky?
- Jak můžu řídit náklady?
- Jak sledovat náklady na prostředky a správně je účtovat?
- Jak zajistit dodržování předpisů a regulací?
- Jak v určitých zemích zajistím splnění zákonných požadavků na suverenitu dat?

Tento průvodce vám pomůže tyto otázky zodpovědět. Obsahuje návrhy úloh a funkcí ke zvážení při přípravě na nasazení prostředků v Azure, mezi které patří:

> [!div class="checklist"]
>
> - **Konfigurace požadavků:** Plánování a příprava migrace
> - **Posouzení technické způsobilosti:** Ověření technické připravenosti a vhodnosti k migraci
> - **Správa nákladů a fakturace:** Získání přehledu nákladů na prostředky
> - **Migrace služeb:** Provedení vlastní migrace
> - **Uspořádání prostředků:** Uzamčení prostředků důležitých pro systém a označení prostředků za účelem jejich sledování
> - **Optimalizace a transformace:** Možnost kontroly prostředků po migraci
> - **Zabezpečení a správa:** Zajištění správného zabezpečení a monitorování prostředí
> - **Získání pomoci:** Získání pomoci a podpory v průběhu migrace nebo aktivit po migraci

::: zone target="docs"

Další informace o uspořádání a strukturování předplatných, správě nasazených prostředků a zajištění souladu s požadavky vyplývajícími z firemních zásad najdete v tématu [Zásady správného řízení v Azure](https://docs.microsoft.com/azure/security/governance-in-azure).

::: zone-end

# <a name="when-to-use-this-guidetabwhentousethisguide"></a>[Kdy použít tohoto průvodce](#tab/WhenToUseThisGuide)

Nástroje popsané v tomto průvodci podporují širokou škálu scénářů migrace, ale tento průvodce se zaměřuje pouze na situace omezeného rozsahu s _minimální složitostí_. Pokud chcete zjistit, jestli je tento průvodce migrací vhodný pro váš projekt, zvažte, jestli pro vás platí následující podmínky:

- Migrujete homogenní prostředí.
- K dokončení migrace je potřeba spolupráce pouze několika obchodních jednotek.
- Nemáte v plánu celou migraci automatizovat.
- Migrujete malý počet serverů.
- Mapování závislostí komponent, které se mají migrovat, je snadno definovatelné.
- Ve vašem odvětví platí minimální zákonné požadavky týkající se této migrace.

Pokud některé z těchto podmínek pro vaši situaci _neplatí_, měli byste zvážit použití [rozšířeného průvodce](../expanded-scope/index.md). Při provádění migrací, které vyžadují rozšířeného průvodce, také doporučujeme požádat o pomoc některého z týmů nebo partnerů Microsoftu. Zákazníci, kteří se spojí s Microsoftem nebo certifikovanými partnery, dosahují v těchto scénářích lepších výsledků. Další informace o tom, jak požádat o pomoc, najdete v tomto průvodci.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Další informace naleznete v tématu:

- [Rozšířený průvodce](../expanded-scope/index.md)

::: zone-end

# <a name="migration-optionstabmigrationoptions"></a>[Možnosti migrace](#tab/MigrationOptions)

Migraci do cloudu můžete provést několika způsoby. Pro různé scénáře jsou některé vhodnější než ostatní. Při určování způsobu migrace vašeho prostředí a rozhodování ohledně strategie migrace zvažte následující možnosti:

- **Změna hostitele:** Při změně hostitele, označované také jako migrace metodou „lift and shift“, se přesune aktuální stav do Azure s minimálními změnami celkové architektury.
- **Refaktoring:** Možnosti PaaS (platforma jako služba) můžou snížit provozní náklady spojené s velkým počtem aplikací. Aplikace může být moudré mírně refaktorovat tak, aby vyhovovaly modelu PaaS. Týká se to také procesu refaktorování kódu při vývoji aplikací tak, aby aplikace mohly poskytovat nové obchodní příležitosti.
- **Změna architektury:** Některé stárnoucí aplikace nejsou kompatibilní s poskytovateli cloudu, a to kvůli rozhodnutím ohledně architektury přijatým při jejich vytváření. V takových případech možná bude potřeba v rámci migrace změnit architekturu aplikace.
- **Opětovné sestavení:** V některých scénářích můžou být změny potřebné k migraci aplikace příliš velké na to, aby ospravedlnily další investice, a řešení je potřeba sestavit znovu.
- **Nahrazení:** Řešení se obvykle implementují s využitím nejlepších technologií a technik, které jsou v danou chvíli k dispozici. V některých případech můžou veškeré funkce hostované aplikace plnit moderní aplikace SaaS (software jako služba). V takových scénářích je možné naplánovat budoucí nahrazení úlohy a tím ji odebrat z rozhodovacího procesu v rámci migrace.

::: zone target="chromeless"

Tyto metody se vzájemně nevylučují &mdash; vaše počáteční migrace může například využívat model **změny hostitele**, ale ve fázi optimalizace po migraci se můžete rozhodnout pro implementaci **refaktorování** nebo **změny architektury**. Tomuto se dále věnuje část **Optimalizace a transformace** tohoto průvodce.

::: zone-end

::: zone target="docs"

Tyto metody se vzájemně nevylučují &mdash; vaše počáteční migrace může například využívat model **změny hostitele**, ale ve fázi optimalizace po migraci se můžete rozhodnout pro implementaci **refaktorování** nebo **změny architektury**. Tomuto se dále věnuje část [Optimalizace a transformace](./optimize-and-transform.md) tohoto průvodce.

::: zone-end

![Infografika možností migrace](../../_images/migrate/migration-options.png)
