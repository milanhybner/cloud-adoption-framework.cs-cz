---
title: 'Inovace v cloudu: interakce se zařízeními'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do cloudových inovací – interakce se zařízeními
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5a9ec9f38d89683482d7f98923aa0ef2ccf201b9
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683213"
---
# <a name="ambient-experiences-interact-with-devices"></a>Okolní prostředí: interakce se zařízeními

V rámci [sestavování pomocí soucit](./build.md)jsme probrali tři testy s skutečnými inovacemi, které zákazníka potřebují, aby se zákazníci mohli dál škálovat na základě základů zákaznických kohorty. Každý test vaší hypotézy bude vyžadovat úsilí a iterace na přístup k přijetí. Tento článek vám poskytne přehled o některých pokročilých přístupech k omezení tohoto úsilí prostřednictvím **okolních prostředí**. Díky interakci se zařízeními místo aplikace může být pro zákazníka pravděpodobnější, že nejprve zapnete řešení a splníte jejich potřebu.

## <a name="ambient-experiences"></a>Okolní prostředí

Okolní prostředí je digitální prostředí, které se vztahuje k bezprostřednímu okolí. Řešení, které nabízí okolí, se snaží dodržet zákazníka v okamžiku potřeby. Pokud je to možné, řešení splní požadavky zákazníka bez nutnosti opustit přirozený tok toho, co prováděl.

Životnost v digitální ekonomice je plná odčítání. Všechny bombarded se sociálními, e-maily, webovými, vizuálními a ústními zprávami, z nichž každá představuje riziko odčítání. Riziko rušivého navýšení se zvyšuje každou sekundu mezi zákazníkovým bodem potřeby a interakcí s řešením. Dlouhé zákazníci jsou v této krátké době ztraceni. Pro zvýšení jejich opětovného přijetí snižte počet odčítání tím, že zkrátíte čas na řešení (TTS).

## <a name="interacting-with-devices"></a>Interakce se zařízeními

Standardní prostředí pro vývoj aplikací, které se používá ke splnění potřeb zákazníka, je standardní webové prostředí. Předpokladem, který se vloženými do tohoto přístupu, je to, že zákazník bude před jeho počítačem. Pokud zákazník v rámci svého přenosného počítače konzistentně splňuje jejich potřebu, můžete si vytvořit webovou aplikaci. Tato webová aplikace bude pro tohoto zákazníka v takovém případě obsahovat "prostředí pro okolí". Ale ví, že tento scénář je stále méně pravděpodobný v moderní společnosti.

![Okolní prostředí](../../_images/innovate/ambient-experiences.png)

Okolní prostředí, jak je znázorněno výše, obvykle vyžaduje více než webovou aplikaci. Díky [měření](./measure.md) a [učení se zákazníkem](./learn.md) se chování, které vede k triggeru potřebě zákazníka, může sledovat, sledovat a používat k sestavování více okolních prostředí. Následující část shrnuje několik přístupů k integraci řešení v okolí do vaší hypotézy. Další podrobnosti najdete v následujících odstavcích.

- **[Mobilní prostředí](#mobile-experience)** : podobně jako přenosný počítač jsou mobilní aplikace většinou součástí okolí zákazníků. V některých scénářích to může poskytnout dostatečnou úroveň interaktivity, aby bylo řešení v okolí.
- **[Mixed reality](#mixed-reality):** V některých případech je třeba změnit přirozené okolí zákazníka, aby se zajistila interakce s okolím. Tím se vytvoří bitová kopie nepravdivého problému, ve kterém může zákazník s řešením pracovat a které musí splnit. V tomto případě je řešení okolí v rámci falešné reality.
- **[Integrovaná realita](#integrated-reality):** S ohledem na blížící se Ambience se integrovaná řešení realit zaměřují na použití zařízení, které existuje ve realitě zákazníka a integruje řešení do přirozeného chování. Virtuální asistent je skvělým příkladem integrace realit do okolního prostředí. Méně známou možností je používat technologie Internet věcí (IoT) k integraci zařízení, která už existují v okolí zákazníka.
- **[Upravená realita](#adjusted-reality):** Pokud některé z výše uvedených řešení používají prediktivní analýzu v cloudu k definování a poskytování interakce se zákazníkem prostřednictvím přirozeného okolí, řešení má upravenou realitu.

Porozumění potřebě zákazníků a měření dopadu zákazníků pomůže zjistit, jestli se bude vyžadovat interakce zařízení nebo okolní prostředí při ověřování hypotézy. U každého z těchto datových bodů vám v následujících částech pomůžou najít nejlepší řešení.

## <a name="mobile-experience"></a>Mobilní prostředí

První fází prostředí okolí je opustit počítač. Dnešní spotřebitelé a obchodní specialisté se dosouvají mezi mobilními a POČÍTAČovým zařízením plynule. Každá z platforem nebo zařízení, které zákazník používá, vytvoří pro zákazníka nové možnosti. Přidání mobilního prostředí, které rozšiřuje primární řešení, je nejrychlejší způsob, jak vylepšit integraci do bezprostředního okolí zákazníka. I když je mobilní zařízení daleko od okolí, může doblížit bod zákazníka, který potřebujete.

Když jsou zákazníci mobilní a často mění umístění, může to být nejrelevantnější forma prostředí pro dané řešení. Jedním z běžných zdrojů inovací za poslední desetiletí bylo rozšíření stávajících řešení pro integraci mobilního prostředí.

Příklady tohoto přístupu najdete v tématu Azure App Services. Během počátečních iterací se [funkce webové aplikace Azure App Service](/azure/app-service/overview) dá použít k otestování hypotézy. Protože je hypotéza složitější, [funkce mobilní aplikace služby Azure App Services](/azure/app-service-mobile/) může webovou aplikaci zvětšit tak, aby běžela na různých mobilních platformách.

## <a name="mixed-reality"></a>Mixed realita

Další úroveň zralosti pro okolní prostředí je rozšíření nebo replikace okolí zákazníka prostřednictvím hybridních řešení realit. V tomto přístupu se řešení postará o další okolí vytvořením rozšíření reality pro zákazníky, kteří pracují v rámci.

> [!IMPORTANT]
> Pokud je potřeba zařízení virtuální realita (VR) a ještě *není součástí jejich bezprostředního okolního nebo přirozeného chování*, pak rozšíření/virtuální realita je víc z alternativních možností a méně okolního prostředí.

Tato forma prostředí je stále častá pro vzdálené pracovní síly. Používání těchto prostředí roste ještě rychleji v odvětvích, která vyžadují spolupráci nebo specializované dovednosti, které nejsou na místním trhu snadno dostupné. Jedním z běžných scénářů, které vyžadují rozšířenou realitu v rámci přirozeného chování, je centralizovaná implementační podpora komplexního produktu pro vzdálenou práci. V těchto scénářích může tým centrální podpory a vzdálený zaměstnanec využít rozšířenou realitu k řešení potíží nebo instalaci produktu.

V případě výše uvedeného scénáře nebo podobných scénářů by se jako příklad prostředí okolí používaly prostorové kotvy. Prostorová ukotvení umožňují vytvořit hybridní prostředí realit s objekty, které v průběhu času uchovávají jejich umístění v rámci zařízení. Prostřednictvím prostorových ukotvení je možné zaznamenat, zaznamenat a trvale zajišťovat prostředí, a to i v případě, že uživatel pracuje v rámci tohoto rozšíření prostředí. [Prostorové kotvy Azure](https://docs.microsoft.com/azure/spatial-anchors/overview) je služba, která přesouvá tuto logiku do cloudu a umožňuje sdílení v různých zařízeních a dokonce i v různých řešeních.

## <a name="integrated-reality"></a>Integrovaná realita

Mimo mobilní realitu nebo dokonce smíšená realita je používání integrované reality. V rámci tohoto přístupu cílem je zcela odebrat digitální prostředí. Vše v okolí je zařízení s možnostmi výpočtů a možností připojení. Tato zařízení je možné použít ke shromažďování dat z bezprostředního okolí bez toho, aby zákazník musel podotknout telefon, přenosného zařízení nebo zařízení VR.

Tato forma prostředí je ideální, pokud je určitá forma zařízení konzistentně ve stejném okolí, ve kterém se zákazník potřebuje. Mezi běžné scénáře patří podlahová podlahová výroba, výtahy nebo dokonce automobil. Tyto typy velkých zařízení už obsahují výpočetní výkon. Můžete také použít data ze samotného zařízení k detekci chování zákazníka a odesílat tato chování do cloudu. Toto automatické zachycení dat o chování zákazníků významně snižuje potřebu zákazníka zadávat data. Kromě toho je možné používat webové, mobilní a prostředí v rámci zpětné vazby ke sdílení informací o tom, co se naučilo z řešení integrované reality.

Příklady integrované reality v Azure můžou zahrnovat:

- [Řešení azure Internet věcí (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), kolekci služeb v Azure, které každá pomoc při správě zařízení a tok dat z těchto zařízení do cloudu a back-endu koncovým uživatelům.
- [Azure sphere](/azure-sphere)kombinace hardwaru a softwaru Azure sphere je innately zabezpečený způsob, jak umožnit stávajícímu zařízení bezpečně přenášet data mezi zařízením a řešeními IoT v Azure.
- [Sada Developer Kit pro Azure Kinect](https://docs.microsoft.com/azure/Kinect-dk), senzory AI s pokročilými počítači a modely řeči, které mohou shromažďovat vizuální a zvukové údaje z bezprostředního okolí a podávat tyto vstupy do vašeho řešení.

Všechny tři lze použít ke shromažďování dat v rámci přirozeného okolí, a to v místě potřeby zákazníka. Odtud vaše řešení může reagovat na tyto datové vstupy a vyřešit potřebu, někdy ještě předtím, než zákazník zaznamená, že došlo k triggeru pro tuto potřebu.

## <a name="adjusted-reality"></a>Upravená realita

Nejvyšší forma prostředí okolí je upravena realitou, která se často označuje jako ambientní logika. Upravená realita je přístup k používání informací z vašeho řešení ke změně reality zákazníka, aniž by bylo nutné pracovat přímo s aplikací. V rámci tohoto přístupu aplikace, kterou jste původně vytvořili k prokázání vaší hypotézy, už nemusí být relevantní. Místo toho by zařízení v prostředí usnadnila vstupy a výstupy, aby splnily požadavky zákazníků.

Virtuální asistenti/inteligentní reproduktory můžou poskytovat skvělý příklad upravené reality. Pouze inteligentní mluvčí je příkladem jednoduché integrované reality. Přidejte smysl inteligentního osvětlení a pohybu do řešení pro inteligentní reproduktory a při zadávání místnosti je snadné vytvořit základní řešení se zapnutými indikátory.

Produkční podlaha po celém světě přináší další scénáře upravené reality. V počátečních fázích integrované reality se v zařízeních zjistily podmínky, jako je například přehřívání, a nahlásili potřebu změny člověka prostřednictvím aplikace. V upravené realitě může být zákazník stále zahrnutý. Smyčka zpětné vazby ale je užší. V upravené továrně služby realit by jedno zařízení zjistilo přehřívání v důležitém počítači někde v rámci řady sestavení. Někde jinde na podlaze se druhé zařízení zpomalí za mírné snížení provozu, aby se počítač mohl vychladnout a pokračovat v situaci, kdy se podmínka vyřešila. V tomto scénáři se jedná o druhou stranu zákazníka. Zákazník používá vaši aplikaci k nastavení pravidel a pochopení, jak tato pravidla mají vliv na produkci, ale nemusí být požadovanou součástí smyčky zpětné vazby.

Služby Azure v předchozí části, [řešení azure Internet věcí (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), [Azure sphere](/azure-sphere)a [Developer Kit pro Azure Kinect](https://docs.microsoft.com/azure/Kinect-dk) by mohly být součástí sady řešení s upravenou realitou. Vaše původní aplikace a obchodní logika budou sloužit jako prostředník mezi vstupem do prostředí a změnou, které by měly být provedeny ve fyzickém prostředí.

Dalším příkladem upravené reality je vytvoření digitálního vlákna, což je digitální reprezentace fyzického zařízení, která je prezentována prostřednictvím počítačů, mobilních nebo hybridních formátů. Na rozdíl od méně sofistikovaných 3D modelů zobrazuje digitální vlákna data shromážděná ze skutečného zařízení ve fyzickém prostředí. Díky tomu může uživatel pracovat s digitálním znázorněním způsobem, který nebylo možné nikdy provést v reálném světě. V tomto postupu se u fyzických zařízení upravuje prostředí hybridní reality. Řešení ale pořád shromažďuje data z integrovaného řešení realit a používá je k naformování reality aktuálního okolí zákazníka.

V Azure se digitální vlákna vytváří a přistupují prostřednictvím služby s názvem [digitální vlákna Azure](https://docs.microsoft.com/azure/digital-twins/about-digital-twins).

## <a name="next-steps"></a>Další kroky

Díky hlubšímu porozumění interakcím zařízení a okolnímu prostředí, které je pro vaše řešení nejvhodnější, teď můžete začít zkoumat závěrečnou disciplínu inovací, [předpovědi a vlivu](./predict.md).

> [!div class="nextstepaction"]
> [Předpověď a vliv](./predict.md)
