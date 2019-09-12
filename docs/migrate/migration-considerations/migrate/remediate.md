---
title: Náprava prostředků před migrací
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Náprava nekompatibilních prostředků před migrací
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 54621d366f0ae0a3e2e3504532ace183bc7f49c4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833450"
---
# <a name="remediate-assets-prior-to-migration"></a>Náprava prostředků před migrací

V procesu posouzení migrace se tým snaží identifikovat konfigurace, kvůli kterým je prostředek nekompatibilní se zvoleným poskytovatelem cloudu. *Náprava* je kontrolním bodem procesu migrace, který zajistí řešení těchto nekompatibilit. V tomto článku najdete informace o několika nejčastějších úlohách nápravy. Najdete v něm také kostru procesu, abyste se mohli rozhodnout, jestli je investice do nápravy rozumná.

## <a name="common-remediation-tasks"></a>Nejčastější úlohy nápravy

V každém firemním prostředí existuje technický dluh. Ten je do určité míry v pořádku a počítá se s ním. Rozhodnutí o architektuře, která se dobře hodila pro místní prostředí, ale nemusí být úplně vhodná pro cloudovou platformu. Každopádně platí, že běžné úlohy nápravy můžou být nutné při přípravě prostředků na migraci. Tady je několik příkladů:

- **Dílčí upgrady hostitele.** Někdy se může stát, že zastaralý hostitel před replikací vyžaduje upgrade.
- **Dílčí upgrady hostovaných operačních systémů.** Je velice pravděpodobné, že operační systém bude před replikací potřeba opravit nebo upgradovat.
- **Úpravy smlouvy SLA.** U cloudové platformy je zálohování a obnovení výrazně jiné. U prostředků bude pravděpodobně potřeba provést dílčí úpravy zálohovacího procesu, aby mohly dále fungovat v cloudu.
- **Migrace PaaS.** V některých případech možná bude potřeba urychlit nasazení tím, že nasadíte PaaS datové struktury nebo aplikace. Pokud chcete řešení připravit na nasazení PaaS, můžou být potřeba dílčí úpravy.
- **Změny kódu PaaS.** U vlastních aplikací není neobvyklé, že při přípravě na PaaS vyžadují dílčí úpravy kódu. Vezměme si například metody, které zapisují na místní disk nebo používají stav relace v paměti, ale jsou i další.
- **Změny konfigurace aplikace.** U migrovaných aplikací možná bude potřeba změnit proměnné, například síťové cesty, na související prostředky, změnit účet služby nebo aktualizovat související IP adresy.
- **Dílčí změny síťových cest.** Možná bude potřeba upravit vzorce směrování, aby správně směrovaly přenosy uživatelů na nové prostředky.
    > [!NOTE]
    > Nejedná se o produkční směrování na nové prostředky, ale o konfiguraci, která obecně umožňuje správné směrování na prostředky.

## <a name="large-scale-remediation-tasks"></a>Rozsáhlé úlohy nápravy

Pokud je datové centrum správně udržované, má nainstalované opravy a je aktualizované, náprava pravděpodobně nebude potřeba. Prostředí vyžadující rozsáhlou nápravu spíše najdete ve velkých organizacích a v organizacích, které procházejí výrazným zeštíhlováním IT. Platí to také o některých starších prostředích spravovaných služeb a o prostředích s velkým podílem akvizic. Ve všech těchto typech prostředí může náprava spotřebovat značnou část úsilí spojeného s migrací. Pokud se následující úlohy nápravy vyskytují často, což negativně ovlivňuje rychlost nebo jednotnost migrace, bude pravděpodobně rozumnější rozdělit nápravu do paralelních úloh a týmů (podobně jako běží paralelně osvojování cloudu a zásady správného řízení cloudu).

- **Časté upgrady hostitele.** Pokud je dokončení migrace podmíněno upgradem velkého počtu hostitelů, bude mít migrační tým pravděpodobně zpoždění. Proto může být rozumné rozdělit dotyčné aplikace a řešit nápravná opatření ještě předtím, než tyto aplikace zahrnete do plánovaných vydání verzí.
- **Časté upgrady OS hostitele.** Velké organizace mají často servery, na kterých běží zastaralé verze Linuxu nebo Windows. Když odhlédneme od zřejmých bezpečnostních rizik spočívajících v provozu zastaralého OS, jsou zde také problémy s nekompatibilitou, které brání migraci dotyčných úloh. Pokud nápravu OS vyžaduje velký počet virtuálních počítačů, může být rozumnější rozdělit tyto úkoly do paralelních iterací.
- **Rozsáhlé změny kódu.** Starší vlastní aplikace můžou vyžadovat podstatně větší úpravy, aby byly připraveny na nasazení PaaS. V takovém případě může být rozumnější, když je úplně odeberete z migračního backlogu a budete je spravovat ve zcela odděleném programu.

## <a name="decision-framework"></a>Rozhodovací platforma

U menších úloh může být náprava jednoduchá, což je i jeden z důvodů, proč se k počáteční migraci doporučuje menší úloha. Jakmile získáte s migracemi více zkušenností a začnete řešit větší úlohy, může být proces nápravy časově náročný a také nákladný. Například náprava při migraci Windows Serveru 2003, který zahrnuje fond prostředků čítající přes 5000 virtuálních počítačů, může migraci zpozdit o celé měsíce. Při rozhodování o takto rozsáhlých nápravách vám mohou pomoci následující otázky:

- Byly všechny úlohy, kterých se náprava týká, zjištěny a zaznamenány do migračního backlogu?
- Pokud se úloh náprava netýká, přinese jejich migrace podobnou návratnost investic (ROI)?
- Bude náprava dotyčných prostředků probíhat podle původní časové osy migrace? Jaký vliv mají změny na časové ose na návratnost investic?
- Je ekonomicky schůdné napravovat prostředky souběžně s migrací?
- Máte pro nápravu a migraci dostatečnou šířku pásma a dostatek personálu? Chcete do jednoho nebo obou úkolů zapojit partnera?

Pokud odpovědi na tyto otázky nebudou příznivé, měli byste zvážit některé alternativní postupy, které přesahují základní strategii změny hostitele IaaS:

- **Vytváření kontejnerů.** Některé prostředky můžete bez nápravy hostovat v kontejnerovém prostředí. V takovém případě může být výkon méně příznivý a můžou zůstat nevyřešené problémy týkající se zabezpečení nebo dodržování předpisů.
- **Automatizace.** V závislosti na požadavcích na úlohu a její nápravu můžete ke skriptování nasazení nových prostředků s výhodou použít přístup DevOps.
- **Přestavba.** Pokud jsou náklady na nápravu velmi vysoké a stejně vysoká je i obchodní hodnota, může být úloha vhodná, abyste ji přestavěli nebo znovu vytvořili její architekturu.

## <a name="next-steps"></a>Další postup

Po dokončení nápravy jsou připravené [replikační činnosti](./replicate.md).

> [!div class="nextstepaction"]
> [Replikace prostředků](./replicate.md)
