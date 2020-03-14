---
title: Pokyny k testování firmy během migrace
description: Přečtěte si, jak se obchodní testování používá k vyžádání ověření, že výkon řešení je v souladu se očekáváními a nebrání obchodním procesům.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 675eda4aeb2109c21c2e3f47a100a985fd6e2861
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311746"
---
# <a name="guidance-for-business-testing-uat-during-migration"></a>Pokyny pro obchodní testování (UAT) během migrace

Testování přijetí uživateli, které se tradičně pojímá jako funkce IT, může během obchodní transformace organizovat výhradně IT. Tato funkce se však často nejúčinněji spouští jako obchodní funkce. IT poté podporuje tuto obchodní aktivitu tím, že usnadňuje testování, vyvíjí plány testování a automatizuje testy, pokud je to možné. I když může IT často sloužit jako zástupce pro testování, neexistuje žádná náhrada za pozorování reálných uživatelů, kteří se snaží využít nové řešení v kontextu skutečného nebo replikovaného obchodního procesu.

> [!NOTE]
> Pokud je k dispozici, automatizované testování je mnohem efektivnější a účinější způsob testování jakéhokoli systému. Migrace do cloudu se ale často zaměřují na starší verze systémů nebo aspoň na stabilní produkční systémy. Tyto systémy často nejsou spravovány důkladnými a dobře udržovanými automatizovanými testy. V tomto článku se předpokládá, že v době migrace nejsou k dispozici žádné takové testy.

Za automatizovaným testováním následuje testování procesu a technologických změn zkušenými uživateli. Zkušení uživatelé jsou lidé, kteří běžně provádějí reálný proces, který vyžaduje interakce s technologickým nástrojem nebo sadou nástrojů. Můžou být reprezentováni externím zákazníkem používajícím web elektronického obchodování k získávání zboží nebo služeb. Zkušení uživatelé můžou být také reprezentováni skupinou zaměstnanců, kteří provádějí obchodní proces, jako jsou například pracovníci call centra obsluhující zákazníky a zaznamenávající své zkušenosti.

Cílem podnikového testování je vyžádat si ověření od zkušených uživatelů, aby bylo možné potvrdit, že nové řešení probíhá v souladu se očekáváními a neohrožuje obchodní procesy. Pokud se tento cíl nesplní, obchodní testování slouží jako smyčka zpětné vazby, která může přispět k definování, proč a jak sada funkcí neplní očekávání.

## <a name="business-activities-during-business-testing"></a>Obchodní aktivity během obchodního testování

Během obchodního testování se první vývoj ručně řídí přímo se zákazníky. Jedná se o nejčistší, ale nejvíc časově náročnou formu smyčky zpětné vazby.

- **Identifikace zkušených uživatelů.** Obchodní oddělení má obecně lepší povědomí o zkušených uživatelích, kteří jsou nejvíc ovlivnění technickou změnou.
- **Srovnání a příprava zkušených uživatelů.** Zajistěte, aby zkušení uživatelé pochopili obchodní cíle, požadované výsledky a očekávané změny v obchodních procesech. Připravte je a jejich řídicí strukturu pro proces testování.
- **Zapojení do interpretace smyček zpětné vazby.** Pomozte pracovníkům IT pochopit dopad různých bodů zpětné vazby od zkušených uživatelů.
- **Upřesnění změny procesu.** Když transformace může spustit změnu v obchodních procesech, vykomunikujte tuto změnu a její případné důsledky.
- **Nastavení priority zpětné vazby.** Pomozte týmu IT určit prioritu zpětné vazby na základě obchodního dopadu.

V některých případech může IT využít analytiky nebo vlastníky produktů, kteří můžou sloužit jako zástupci pro rozdělené aktivity obchodního testování. Účast je ale vysoce doporučovaná a může tak produkovat uspokojivé obchodní výsledky.

## <a name="it-activities-during-business-testing"></a>Aktivity IT během obchodního testování

IT slouží jako jeden z příjemců výstupu obchodního testování. Smyčky zpětné vazby objevené během obchodního testování se nakonec můžou stát pracovními položkami, které definují technickou změnu nebo změnu procesu. Od IT jako příjemce se očekává, že bude pomáhat při usnadňování, shromažďování zpětné vazby a správě výsledných technických akcí. Mezi obvyklé aktivity, které IT provádí při obchodním testování, patří:

- Poskytnutí struktury a logistiky při obchodním testování
- Pomoc při usnadnění během testování
- Poskytnutí prostředků a procesů pro záznam zpětné vazby
- Pomoc obchodnímu oddělení s určením priority a ověřením zpětné vazby
- Vývoj plánů pro akce na základě technických změny
- Identifikace existujících automatizovaných testů, které by mohly zjednodušit testování zkušenými uživateli
- U změn, které by mohly vyžadovat opakované nasazení nebo testování, prostudování procesů testování, definování srovnávacích testů a vytváření automatizace pro další zjednodušení testování zkušenými uživateli

## <a name="next-steps"></a>Další kroky

V souvislosti s obchodním testováním může [optimalizace migrovaných aktiv](./optimize.md) vyladit náklady a výkon sady funkcí.

> [!div class="nextstepaction"]
> [Srovnávací testování a změna velikosti cloudových prostředků](./optimize.md)
