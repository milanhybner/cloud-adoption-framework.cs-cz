---
title: Interakce se zařízeními prostřednictvím digitálního vynálezu
description: Přečtěte si o rozšířených přístupech, abyste snížili úsilí prostřednictvím interakce zákazníků s okolními prostředími a zařízeními, nikoli aplikacemi.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 05fc3e3b4ddb0ae630feaee57a345aec8870ea08
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171221"
---
# <a name="ambient-experiences-interact-with-devices"></a>Okolní prostředí: interakce se zařízeními

V rámci [sestavování s Customer soucit](./build.md)jsme probrali tři testy s skutečnými inovacemi, které zákazníka potřebují, ponechte zákazníka zpátky a škálovat na základě základů zákaznických kohorty. Každý test vaší hypotézy vyžaduje úsilí a iterace při přístupu k přijetí. Tento článek nabízí přehledy o některých pokročilých přístupech k omezení tohoto úsilí prostřednictvím *okolních prostředí*. Díky interakci se zařízeními místo aplikace může být u zákazníka pravděpodobnější, že se vaše řešení nejprve zapíná.

## <a name="ambient-experiences"></a>Okolní prostředí

Okolní prostředí je digitální prostředí, které se vztahuje k bezprostřednímu okolí. Řešení, které nabízí okolí, se snaží dodržet zákazníka v okamžiku potřeby. Pokud je to možné, řešení splňuje požadavky zákazníků, aniž by musel opustit tok aktivity, který ji aktivoval.

Životnost v digitální ekonomice je plná odčítání. Všechny bombarded se sociálními, e-maily, webovými, vizuálními a ústními zprávami, z nichž každá představuje riziko nedodržení. Toto riziko se zvyšuje za každou sekundu, který uplyne mezi zákazníkovým bodem potřeby a okamžikem, kdy se k řešení zaznamená. Dlouhé se ztratí za tuto krátkou časovou mezeru. Chcete-li zvýšit počet opakování přijetí, je třeba snížit počet odčítání tím, že zkrátíte čas na řešení (TTS).

## <a name="interacting-with-devices"></a>Interakce se zařízeními

Standardní prostředí pro vývoj aplikací, které se používá ke splnění potřeb zákazníka, je standardní webové prostředí. Tento přístup předpokládá, že zákazník je před jeho počítačem. Pokud zákazník v rámci svého přenosného počítače konzistentně splňuje jejich potřebu, můžete si vytvořit webovou aplikaci. Tato webová aplikace nabídne prostředí pro daného zákazníka v tomto scénáři. Víme ale, že tento scénář je méně pravděpodobný a v našem aktuálním období je méně pravděpodobný.

![Okolní prostředí](../../_images/innovate/ambient-experiences.png)

Okolní prostředí obvykle vyžaduje více než webovou aplikaci pro tyto dny. Díky [měření](./measure.md) a [učení se zákazníkem](./learn.md) se chování, které aktivuje potřeby zákazníka, může pozorovat, sledovat a používat k sestavování více prostředí okolí. Následující seznam shrnuje několik přístupů k integraci ambientních řešení do vaší hypotézy. Další podrobnosti najdete v následujících odstavcích.

- **[Mobilní prostředí](#mobile-experience):** Jako u notebooků se mobilní aplikace všudypřítomný v zákaznických prostředích. V některých situacích to může poskytnout dostatečnou úroveň interaktivity, aby bylo řešení v okolí.
- **[Mixed reality](#mixed-reality):** V některých případech je třeba změnit typické okolí zákazníka, aby se interakce provedla v okolí. Tento faktor vytvoří něco z nepravdivého realitu, ve kterém zákazník komunikuje s řešením a má nezbytnou splnění. V tomto případě je řešení okolí v rámci falešné reality.
- **[Integrovaná realita](#integrated-reality):** S ohledem na blížící se k true Ambience se integrovaná řešení realit zaměřují na použití zařízení, které existuje ve skutečnosti zákazníka, a integrovat řešení do jejich přirozených chování. Virtuální asistent je skvělým příkladem integrace realit do okolního prostředí. Neznámou možnost se týká Internet věcí (IoT) technologií, které integrují zařízení, která už existují v okolí zákazníka.
- **[Upravená realita](#adjusted-reality):** Pokud některá z těchto ambientních řešení používají prediktivní analýzu v cloudu k definování a poskytování interakce se zákazníkem prostřednictvím přirozeného okolí, řešení má upravenou realitu.

Porozumění potřebě zákazníků a měření dopadu zákazníků vám pomůže určit, jestli je interakce zařízení nebo okolní prostředí nutná k ověření hypotézy. U každého z těchto datových bodů vám následující části pomůžou najít nejlepší řešení.

## <a name="mobile-experience"></a>Mobilní webové prostředí

V první fázi okolního prostředí se uživatel od počítače přesune jinam. Dnešní spotřebitelé a obchodní specialisté se dosouvají mezi mobilními a POČÍTAČovým zařízením plynule. Každá z platforem nebo zařízení, které zákazník používá, vytvoří nové možnosti. Přidání mobilního prostředí, které rozšiřuje primární řešení, je nejrychlejší způsob, jak vylepšit integraci do bezprostředního okolí zákazníka. I když je mobilní zařízení daleko od okolí, může to být blíže k bodu zákazníka, který potřebujete.

Když jsou zákazníci mobilní a často mění umístění, mohou představovat nejrelevantnější formu prostředí pro konkrétní řešení. Za poslední desetiletí byly inovace často aktivované integrací stávajících řešení s mobilním prostředím.

Azure App Services je skvělým příkladem tohoto přístupu. Během počátečních iterací se [funkce webové aplikace služby Azure App Services](https://docs.microsoft.com/azure/app-service/overview) dá použít k otestování hypotézy. Protože je hypotéza složitější, [funkce mobilní aplikace služby Azure App Services](https://docs.microsoft.com/azure/app-service-mobile) může webovou aplikaci zvětšit tak, aby běžela na různých mobilních platformách.

## <a name="mixed-reality"></a>Smíšená realita

Hybridní řešení realit reprezentují další úroveň zralosti pro okolní prostředí. Tento přístup rozšiřuje nebo replikuje okolí zákazníka; Vytvoří rozšíření realit pro zákazníka, který bude fungovat v rámci.

> [!IMPORTANT]
> Pokud je potřeba zařízení virtuální reality (VR) a ještě není *součástí bezprostředního okolního nebo přirozeného chování zákazníka*, rozšíření nebo virtuální realita je více než v alternativním prostředí a méně okolních prostředí.

Hybridní práce ve realitách je stále častá mezi vzdálenými zaměstnanci. Jejich použití roste ještě rychleji v odvětvích, které vyžadují spolupráci nebo specializované dovednosti, které nejsou na místním trhu snadno dostupné. V situacích, které vyžadují centralizovanou implementaci pro komplexní produkt pro vzdálené pracovní síly, se pro rozšířenou realitu zvlášť úrodný základ. V těchto scénářích může tým centrální podpory a vzdálení zaměstnanci využívat rozšířenou skutečnost pro práci na, řešení potíží a instalaci produktu.

Zvažte například velikost prostorových ukotvení. Prostorová ukotvení umožňují vytvořit hybridní prostředí realit s objekty, které v průběhu času uchovávají jejich umístění v rámci zařízení. Prostřednictvím prostorových ukotvení lze konkrétní chování zachytit, zaznamenat a zachovat a tím zajistit prostředí okolí při příštím fungování v rámci tohoto rozšíření prostředí. [Prostorové kotvy Azure](https://docs.microsoft.com/azure/spatial-anchors/overview) je služba, která přesouvá tuto logiku do cloudu a umožňuje sdílení v různých zařízeních a dokonce i v různých řešeních.

## <a name="integrated-reality"></a>Integrovaná realita

Nad rámec mobilní reality nebo dokonce i smíšená realita je integrovaná realita. Integrovaná realita má za cíl zcela odebrat digitální prostředí. Vše v okolí je zařízení s možnostmi výpočtů a možností připojení. Tato zařízení je možné použít ke shromažďování dat z bezprostředního okolí bez toho, aby zákazník musel podotknout telefon, přenosného zařízení nebo zařízení VR.

Toto prostředí je ideální, pokud je určitá forma zařízení konzistentně ve stejném okolí, ve kterém se zákazník potřebuje. Mezi běžné scénáře patří podlahová podlahová výroba, výtahy a dokonce i vaše auto. Tyto typy velkých zařízení už obsahují výpočetní výkon. Můžete také použít data ze samotného zařízení k detekci chování zákazníka a odesílat tato chování do cloudu. Toto automatické zachycení dat o chování zákazníků významně snižuje potřebu zákazníka zadávat data. Kromě toho může webové, mobilní nebo uživatelské prostředí fungovat jako smyčka zpětné vazby a sdílet tak, co se naučilo z integrovaného řešení realit.

Příklady integrované reality v Azure můžou zahrnovat:

- [Řešení azure Internet věcí (IoT)](https://docs.microsoft.com/azure/iot-fundamentals)– kolekce služeb v Azure, které každá pomoc při správě zařízení a tok dat z těchto zařízení do cloudu a back-endu koncovým uživatelům.
- [Azure sphere](https://docs.microsoft.com/azure-sphere)kombinace hardwaru a softwaru. Azure Sphere je innately zabezpečený způsob, jak umožnit stávajícímu zařízení bezpečně přenášet data mezi zařízením a řešeními IoT v Azure.
- [Azure Kinect Developer Kit](https://docs.microsoft.com/azure/Kinect-dk), senzory AI s pokročilými modely počítačových a řeči. Tyto senzory můžou shromažďovat vizuální a zvukové údaje z bezprostředního okolí a obdávat tyto vstupy do vašeho řešení.

Pomocí všech tří z těchto nástrojů můžete shromažďovat data z přirozeného okolí a z hlediska potřeby zákazníka. Odtud vaše řešení může reagovat na tyto datové vstupy a vyřešit potřebu, někdy ještě předtím, než zákazník zaznamená, že došlo k triggeru pro tuto potřebu.

## <a name="adjusted-reality"></a>Upravená realita

Nejvyšší forma prostředí okolí je upravena realitou, která se často označuje jako *ambientní logika*. Upravená realita je přístup k používání informací z vašeho řešení ke změně reality zákazníka, aniž by bylo nutné, aby spolupracovali s aplikací přímo. V rámci tohoto přístupu aplikace, kterou jste původně vytvořili k prokázání vaší hypotézy, už nemusí být relevantní. Místo toho zařízení v prostředí umožňují modulaci vstupů a výstupů, aby splňovaly potřeby zákazníků.

Virtuální asistenti a inteligentní reproduktory nabízejí skvělé příklady upravené reality. Pouze inteligentní mluvčí je příkladem jednoduché integrované reality. Ale přidejte senzor inteligentního světla a pohybu do řešení Smart mluvčí a je snadné vytvořit základní řešení, které při zadávání místnosti zapne světla.

Produkční podlaha po celém světě poskytují další příklady upravené reality. V počátečních fázích integrované reality se na zařízeních zjistily podmínky, jako je třeba přehřívání, a pak se pomocí aplikace upozorní na člověka. V upravené realitě se zákazník může stále účastnit, ale smyčka zpětné vazby je užší. Na upravenou podlahovou základnu realit může jedno zařízení detekovat přehřívání v důležitém počítači někam podél čáry sestavení. Někde jinde na podlaze druhé zařízení zpomaluje produkci mírně, aby bylo možné počítač vychladnout a pak obnovit plný tempo při vyřešení podmínky. V takové situaci je zákazníkem druhý účastník. Zákazník používá vaši aplikaci k nastavení pravidel a pochopení, jak tato pravidla mají vliv na produkci, ale nejsou nutná pro smyčku zpětné vazby.

Služby Azure popsané v [řešeních azure Internet věcí (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), [Azure sphere](https://docs.microsoft.com/azure-sphere)a [Developer Kit pro Azure Kinect](https://docs.microsoft.com/azure/Kinect-dk) by mohly být součástí sady řešení s upravenou realitou. Vaše původní aplikace a obchodní logika by pak sloužily jako prostředník mezi vstupem v prostředí a změnou, která by se měla provádět ve fyzickém prostředí.

Digitální vlákna je dalším příkladem upravené reality. Tento pojem označuje digitální reprezentaci fyzického zařízení, které jsou k dispozici prostřednictvím počítačů, mobilních nebo hybridních formátů. Na rozdíl od méně sofistikovaných 3D modelů zobrazuje digitální vlákna data shromážděná ze skutečného zařízení ve fyzickém prostředí. Toto řešení umožňuje uživateli interakci s digitální reprezentací způsobem, který nebylo možné nikdy provést v reálném světě. V tomto přístupu fyzické zařízení upravují hybridní prostředí realit. Řešení však stále shromažďuje data z integrovaného řešení realit a používá tato data k vytvarování reality aktuálního okolí zákazníka.

V Azure se digitální vlákna vytváří a přistupují prostřednictvím služby s názvem [digitální vlákna Azure](https://docs.microsoft.com/azure/digital-twins/about-digital-twins).

## <a name="next-steps"></a>Další kroky

Teď, když máte hlubší přehled o interakcích zařízení a okolním prostředí, které je pro vaše řešení nejvhodnější, jste připraveni prozkoumat konečnou disciplínu inovací, [předpovědi a vlivu](./predict.md).

> [!div class="nextstepaction"]
> [Předpověď a vliv](./predict.md)
