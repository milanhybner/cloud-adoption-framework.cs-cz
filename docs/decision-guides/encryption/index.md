---
title: Průvodce rozhodováním ohledně šifrování
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s šifrováním jako základní službou při migraci do Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ef608f27f75d5a47e3e23a568e576310b8962ea8
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817090"
---
# <a name="encryption-decision-guide"></a>Průvodce rozhodováním ohledně šifrování

Šifrování zajišťuje ochranu dat před neoprávněným přístupem. Správně implementované zásady šifrování zajišťují další úroveň zabezpečení cloudových úloh a ochranu před útočníky a dalšími neoprávněnými uživateli z vaší organizace a sítí i mimo ně.

Přejít na: [Správa klíčů](#key-management) | [Šifrování dat](#data-encryption) | [Další informace](#learn-more)

Strategie cloudového šifrování se soustředí na mandáty firemních zásad a dodržování předpisů. Šifrování prostředků je žádoucí a v řadě služeb Azure, jako jsou Azure Storage nebo Azure SQL Database, je šifrování povolené ve výchozím nastavení. S šifrováním jsou však spojené náklady, které můžou zvýšit latenci a celkové využití prostředků.

Pro náročné úlohy může být zásadní nalézt správnou rovnováhu mezi šifrováním a výkonem a určit vhodný způsob šifrování dat a provozu. Jednotlivé mechanismy šifrování se liší z hlediska nákladů a složitosti a rozhodování o způsobu implementace šifrování a ukládání a správy důležitých klíčů a tajných klíčů můžou ovlivnit technické požadavky i požadavky zásad.

Faktory, které mají největší vliv na plánování strategie šifrování, jsou firemní zásady a dodržování předpisů třetích stran. Azure poskytuje několik standardních mechanismů, které můžou splnit běžné požadavky na šifrování přenášených i neaktivních uložených dat. Pro zajištění podpory požadavků zásad a dodržování předpisů vyžadujících přísnější kontrolní mechanismy, jako je správa standardizovaných klíčů a tajných klíčů, šifrování používaných dat nebo šifrování specifické pro konkrétní data, však budete muset vyvinout sofistikovanější strategii šifrování.

## <a name="key-management"></a>Správa klíčů

Šifrování dat v cloudu je závislé na zabezpečeném ukládání, správě a provozním používání šifrovacích klíčů. Pro zajištění možnosti organizace vytvářet, ukládat a spravovat kryptografické klíče, stejně jako důležitá hesla, připojovací řetězce a další důvěrné informace o IT je zcela zásadní systém správy klíčů.

Moderní systémy správy klíčů, jako je služba Azure Key Vault, podporují ukládání a správu softwarově chráněných klíčů pro použití při vývoji a testování a klíčů chráněných modulem hardwarového zabezpečení (HSM) pro zajištění maximální ochrany produkčních úloh nebo citlivých dat.

Při plánování migrace do cloudu vám následující tabulka může pomoct s rozhodnutím, jak ukládat a spravovat šifrovací klíče, certifikáty a tajné klíče, které jsou důležité pro vytváření zabezpečených cloudových nasazení s možností správy:

| Otázka | Model nativní pro cloud | Používání vlastního klíče | Držení vlastního klíče |
|---------------------------------------------------------------------------------------------------------------------------------------|--------------|--------|-------------|
| Chybí ve vaší organizaci centrální správa klíčů a tajných klíčů?                                                                    | Ano          | Ne     | Ne          |
| Budete při používání klíčů v cloudu potřebovat omezit vytváření klíčů a tajných klíčů k zařízením na místní hardware? | Ne           | Ano    | Ne          |
| Existují ve vaší organizaci pravidla nebo zásady, které brání ukládání klíčů mimo místní prostředí?                | Ne           | Ne     | Ano         |

### <a name="cloud-native"></a>Model nativní pro cloud

V případě správy klíčů nativní pro cloud se všechny klíče a tajné klíče generují, spravují a ukládají v cloudovém trezoru, jako je například služba Azure Key Vault. Tento přístup zjednodušuje řadů úloh IT souvisejících se správou klíčů, jako je zálohování, ukládání a obnovování klíčů.

Při použití systému správy klíčů nativního pro cloud se předpokládá následující:

- S vytvářením, správou a hostováním klíčů a tajných klíčů vaší organizace důvěřujete cloudovému řešení pro správu klíčů.
- Všem místním aplikacím a službám, které se spoléhají na přístup k šifrovacím službám nebo tajným klíčům, povolíte přístup ke cloudovému systému správy klíčů.

### <a name="bring-your-own-key"></a>Používání vlastního klíče

V případě přístupu spočívajícího v používání vlastního klíče vygenerujete klíče na rezervovaném hardwaru HSM v rámci místního prostředí a pak tyto klíče bezpečně přenesete do cloudového systému správy, jako je služba Azure Key Vault, abyste je mohli používat v prostředcích hostovaných v cloudu.

**Předpoklady pro používání vlastního klíče:** Při generování klíčů v místním prostředí a jejich používání v cloudovém systému správy klíčů se předpokládá následující:

- S hostováním a používáním vašich klíčů a tajných klíčů důvěřujete základní infrastruktuře zabezpečení a řízení přístupu cloudové platformy.
- Vaše aplikace nebo služby hostované v cloudu mají přístup ke klíčům a tajným klíčům a můžou je používat robustním a bezpečným způsobem.
- Legislativní předpisy nebo zásady organizace vyžadují, abyste i nadále vytvářeli a spravovali klíče a tajné klíče vaší organizace v místním prostředí.

### <a name="on-premises-hold-your-own-key"></a>Místní prostředí (držení vlastního klíče)

V určitých scénářích můžou existovat legislativní nebo technické důvody nebo důvody vyplývající ze zásad, proč nemůžete ukládat klíče v cloudovém systému správy klíčů. V takových případech musíte generovat klíče s použitím místního hardwaru, ukládat a spravovat je pomocí místního systému správy klíčů a vytvořit mechanismus, kterým cloudovým prostředkům umožníte přístup k těmto klíčům pro účely šifrování. Nezapomeňte, že držení vlastního klíče nemusí být kompatibilní se všemi službami založenými na Azure.

**Předpoklady pro místní správu klíčů:** Při použití místního systému správy klíčů se předpokládá následující:

- Regulační zásady nebo zásady organizace vyžadují, abyste i nadále vytvářeli, spravovali a hostovali klíče a tajné klíče vaší organizace v místním prostředí.
- Všechny cloudové aplikace a služby, které se spoléhají na přístup k šifrovacím službám nebo tajným klíčům, mají přístup k místnímu systému správy klíčů.

## <a name="data-encryption"></a>Šifrování dat

Při plánování zásad šifrování berte v úvahu několik různých stavů dat s různými požadavky na šifrování:

| Stav dat | Data |
|-----|-----|
| Přenášená data | Interní síťový provoz, internetová připojení, připojení mezi datacentry nebo virtuálními sítěmi |
| Neaktivní uložená data    | Databáze, soubory, virtuální disky, úložiště PaaS |
| Používaná data     | Data načtená do mezipaměti RAM nebo mezipaměti procesoru |

### <a name="data-in-transit"></a>Přenášená data

Přenášená data jsou data přesouvaná mezi prostředky v interní síti, mezi datacentry nebo externími sítěmi nebo přes internet.

Šifrování přenášených dat se obvykle provádí vyžadováním protokolů SSL/TLS pro provoz. Provoz mezi vašimi prostředky hostovanými v cloudu a externí sítí nebo veřejným internetem by vždy měl být šifrovaný. Prostředky PaaS obecně také pro provoz vynucují šifrování SSL/TLS ve výchozím nastavení. Rozhodnout, jestli se má vynucovat šifrování provozu mezi prostředky IaaS hostovanými v rámci vašich virtuálních sítí, by měly učinit vaše týmy přechodu na cloud a vlastníci úloh. Obecně to doporučujeme.

**Předpoklady pro šifrování přenášených dat:** Implementace vhodných zásad šifrování pro přenášená data předpokládá následující:

- Všechny veřejně přístupné koncové body ve vašem cloudovém prostředí budou komunikovat s veřejným internetem pomocí protokolů SSL/TLS.
- Při propojování cloudových sítí s místními nebo jinými externími sítěmi přes veřejný internet budete používat šifrované protokoly VPN.
- Při propojování cloudových sítí s místními nebo jinými externími sítěmi prostřednictvím vyhrazeného připojení WAN, jako je ExpressRoute, budete používat zařízení VPN nebo jiné šifrovací zařízení v místním prostředí spárované s odpovídajícím zařízením VPN nebo šifrovacím zařízením nasazeným ve vaší cloudové síti.
- Pokud máte citlivá data, která se nesmí zobrazovat v protokolech provozu ani v jiných diagnostických sestavách, ke kterým mají přístup IT pracovníci, budete šifrovat veškerý provoz mezi prostředky ve vaší virtuální síti.

### <a name="data-at-rest"></a>Neaktivní uložená data

Neaktivní uložená data představují všechna data, která se aktivně nepřesouvají ani nezpracovávají, včetně souborů, databází, jednotek virtuálních počítačů, účtů úložiště PaaS nebo podobných prostředků. Šifrování uložených dat chrání virtuální zařízení nebo soubory před neoprávněným přístupem kvůli externímu průniku do sítě, od neautorizovaných interních uživatelů nebo kvůli náhodnému úniku.

Prostředky úložiště PaaS a databází obvykle vynucují šifrování ve výchozím nastavení. Prostředky IaaS je možné zabezpečit šifrováním dat na úrovni virtuálního disku nebo šifrováním celého účtu úložiště, který je hostitelem vašich virtuálních disků. Všechny tyto prostředky můžou využívat klíče spravované Microsoftem nebo zákazníkem a uložené ve službě Azure Key Vault.

Šifrování neaktivních uložených dat zahrnuje také pokročilejší techniky šifrování databáze, jako je šifrování na úrovni sloupců a řádků, které poskytují lepší kontrolu nad tím, jaká přesně data se zabezpečují.

Prostředky, které vyžadují šifrování, byste měli určit na základě celkových požadavků zásad a požadavků na dodržování předpisů, citlivosti ukládaných dat a požadavků na výkon vašich úloh.

**Předpoklady pro šifrování neaktivních uložených dat:** Při šifrování neaktivních uložených dat se předpokládá následující:

- Ukládáte data, která nejsou určená ke zveřejnění.
- Vaše úlohy zvládnou vyšší latenci spojenou s šifrováním disku.

### <a name="data-in-use"></a>Používaná data

Šifrování používaných dat zahrnuje zabezpečení dat v dočasném úložišti, jako je mezipaměť RAM nebo mezipaměť procesoru. Používání technologií, jako je úplné šifrování paměti, umožňuje využívat enklávy technologií, jako je Secure Guard Extensions (SGX) od společnosti Intel. To zahrnuje také kryptografické techniky, jako je homomorfní šifrování, které je možné využít k vytváření zabezpečených a důvěryhodných spouštěcích prostředí.

**Předpoklady pro šifrování používaných dat:** Při šifrování používaných dat se předpokládá následující:

- Za všech okolností musíte udržovat vlastnictví dat oddělené od základní cloudové platformy, a to i na úrovni paměti RAM a procesoru.

## <a name="learn-more"></a>Další informace

Další informace o šifrování a správě klíčů v Azure najdete tady:

- [Přehled šifrování Azure](/azure/security/security-azure-encryption-overview). Podrobný popis způsobu, jakým Azure využívá šifrování k zabezpečení přenášených i neaktivních uložených dat.
- [Azure Key Vault](/azure/key-vault/key-vault-overview). Služba Key Vault je hlavní systém pro správu klíčů, který umožňuje ukládání a správu kryptografických klíčů, tajných klíčů a certifikátů v Azure.
- [Osvědčené postupy šifrování a zabezpečení dat v Azure](/azure/security/azure-security-data-encryption-best-practices). Popis osvědčených postupů šifrování a zabezpečení dat v Azure.
- [Důvěrné výpočetní operace v Azure](https://azure.microsoft.com/solutions/confidential-compute/). Iniciativa důvěrných výpočetních operací v Azure poskytuje nástroje a technologie umožňující vytvářet důvěryhodná spouštěcí prostředí nebo další mechanismy šifrování pro zabezpečení používaných dat.

## <a name="next-steps"></a>Další kroky

Šifrování je pouze jednou ze základních komponent infrastruktury, která během procesu přechodu na cloud vyžaduje rozhodnutí na úrovni architektury. Navštivte [přehled průvodců rozhodováním](../index.md), kde se dozvíte o alternativních modelech nebo modelech určených pro rozhodování o návrzích pro jiné typy architektur.

> [!div class="nextstepaction"]
> [Průvodci rozhodováním ohledně architektury](../index.md)
