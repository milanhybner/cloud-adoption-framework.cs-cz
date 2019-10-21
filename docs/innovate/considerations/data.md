---
title: 'Inovace v cloudu: Demokratizujte data'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Úvod do cloudových inovací – Demokratizujte data
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 0ce40f1d8b2a58b9a9c48a4181376e7b680b25c4
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557749"
---
# <a name="democratize-data"></a>Demokratizujte data

Uhlí, olej a lidský potenciál byly tři nejvýznamnější prostředky v průběhu průmyslové revoluce. Tyto prostředky sestavily společnosti, posunuly trhy a nakonec změnily národy. V digitální ekonomice existují tři stejně důležité prostředky: data, zařízení a lidský potenciál. V každém z těchto prostředků je to skvělý potenciál pro inovace. V rámci jakékoli inovační snahy je data novým olejem.

V současné době jsou v každé společnosti k dispozici kapsy dat, které by bylo možné využít k rychlejšímu vyhledávání a uspokojení potřeb zákazníků. Omlouváme se, ale proces dolování těchto dat pro účely inovace má dlouhou dobu náročné na čas. Mnohé z nejcennějších řešení potřebných pro zákazníky se nesplnění, protože k datům, která potřebují, nemůžou přistupovat žádné správné osoby.

Democratization dat je proces získávání těchto dat do správných rukou k zajištění inovace. Tento proces může trvat několik tvarů, ale obecně zahrnuje řešení pro ingestovaná nebo integrovaná neupravená data, centralizaci dat, sdílení dat a zabezpečení dat. Po úspěšném doznali odborníci na společnost data k testování hypotézy. V mnoha případech můžou týmy při přijímání v cloudu [sestavovat pomocí zákaznických soucit](./build.md) jenom data, což má za následek rychlý dopad na stávající potřeby zákazníků.

## <a name="process-of-democratizing-data"></a>Zpracování democratizing dat

Následující fáze vás provede rozhodnutími a přístupy potřebnými k přijetí řešení, které demokratizuje data. Každá z fází nemusí být nutná k sestavení konkrétního řešení. Při sestavování řešení pro zákazníka předpokládáme ale, že by se měly vyhodnocovat všechny. Každá z nich poskytuje jedinečný přístup pro vytváření inovativních řešení.

![Zpracování dat democratizing](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Sdílení dat

Při [sestavování s využitím Customer soucit](./build.md)se všechny procesy zaměřují na zákazníky, kteří potřebují prostřednictvím technického řešení. Democratizing data neobsahují žádnou výjimku, takže Začínáme se sdílením dat. Aby Demokratizujte data, musí zahrnovat řešení, které sdílí data s příjemcem dat. Spotřebitel dat může být přímým zákazníkem nebo proxy, který pro zákazníky provádí rozhodnutí. Schválení příjemci dat mají schopnost analyzovat, dotazování a sestavovat centralizované údaje bez podpory od zaměstnanců IT.

Mnohé úspěšné inovace se spustily jako MVP, které přinášejí ručním procesům řízeným daty jménem zákazníka. V tomto modelu concierge je zaměstnanec dat příjemcem. Tento zaměstnanec používá data k podpoře zákazníka. Pokaždé, když zákazník zahájí ruční podporu, může být hypotéza testována a ověřena. Tento přístup je často nákladově efektivní způsob testování předpokladu zaměřeného na zákazníky ještě před investicí do integrovaných řešení.

Primární nástroje pro sdílení dat přímo s příjemci dat zahrnují samoobslužné vytváření sestav nebo data integrovaná do jiných prostředí pomocí nástrojů, jako je [Power BI](https://docs.microsoft.com/power-bi).

> [!NOTE]
> Před sdílením dat je důležité mít na paměti následující oddíly. Sdílení dat může vyžadovat, aby zásady správného řízení poskytovaly ochranu pro sdílená data. Dále je možné, že data budou rozložena mezi více cloudy a mohou vyžadovat centralizaci. Většina dat může být sudá i v aplikacích, které budou vyžadovat shromažďování dat před jejich sdílením.

### <a name="govern-data"></a>Řídit data

Sdílení dat může rychle vydávat MVP, který se dá použít v zákaznických konverzacích. Pouze data jsou však pouze data. K tomu, aby se tato sdílená data přepnula na konkrétní znalosti, se často vyžaduje. Po ověření hypotézy prostřednictvím sdílení dat je další fáze vývoje často zásad správného řízení dat.

Řízení dat je široké téma, které by mohlo vyžadovat vlastní vyhrazenou architekturu. Toto je mimo rozsah architektury pro přijetí do [cloudu](../../index.md). Existuje však několik aspektů zásad správného řízení dat, které by měly být zváženy, jakmile je zákazníkem hypotéza. Následuje několik příkladů těchto otázek:

- **Je citlivá sdílená data?** [Data by se měla klasifikovat](../../govern/policy-compliance/data-classification.md) před jakýmkoli veřejným sdílením, aby se chránily zájmy zákazníků a společnosti.
- **Pokud jsou data citlivá, jsou zabezpečená?** Ochrana citlivých dat by měla být požadavek na všechna democratized data. Příklad úlohy zaměřené na [zabezpečení datových řešení](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions.md) poskytuje několik odkazů na zabezpečení dat.
- **Je data v katalogu?** Shromažďování podrobností o datech, která se sdílejí, bude pomoci při dlouhodobé správě dat. Nástroje pro dokumentování dat, jako je Azure Data Catalog, můžou tento proces v cloudu mnohem jednodušeji udělat. Pokyny týkající se [poznámek na data](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) a [dokumentaci zdrojů dat](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) vám pomůžou zrychlit proces.

V případě, že democratization dat je důležité pro hypotézy zaměřené na zákazníky, by řízení sdílených dat mělo být někde v plánu vydávání verzí, aby se chránily zákazníci, spotřebitelé dat a společnost.

### <a name="centralize-data"></a>Centralizace dat

Pokud dojde k přerušení dat napříč IT prostředím, mohou být příležitosti pro inovace extrémně omezené, nákladné a časově náročné. Cloud nabízí nové příležitosti pro centralizaci dat napříč různými silami dat. Při [sestavování s využitím zákaznických soucit](./build.md) může Cloud zrychlit testování hypotéz.

> [!CAUTION]
> Centralizované navýšení dat je běžným rizikovým bodem při jakémkoli inovačním procesu. Když je centrální [špička v podobě technického špičky](./build.md#reduce-complexity-and-delay-technical-spikes), na rozdíl od zdroje hodnoty zákazníka, je navržena pro odložené centralizaci, dokud se zákaznická hypotéza neověří.

Pokud je potřeba centralizované navýšení dat, je prvním krokem definování vhodného úložiště dat pro centralizovaná data. Doporučujeme, abyste navázali datový sklad v cloudu. Tato přizpůsobitelná možnost zajistí centrální umístění pro všechna data. Tento typ řešení je k dispozici v možnostech online analytického zpracování (OLAP) nebo ve volbách pro velké objemy dat.

Referenční architektury pro řešení [OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing) a velkých objemů [dat](https://docs.microsoft.com/azure/architecture/data-guide/big-data) mohou pomoci při výběru nejrelevantnějšího řešení v Azure. Pokud je třeba hybridní řešení, referenční architektura pro [rozšiřování místních dat](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) může také přispět k urychlení vývoje řešení.

> [!IMPORTANT]
> V závislosti na potřebách zákazníka a zarovnaných řešeních může stačit jednodušší řešení. Cloudový architekt by měl vyzkoušet tým, aby zvážil nižší nákladová řešení, která by mohla vést k rychlejšímu ověření zákaznických předpokladů, zejména při prvotním vývoji. V části o shromažďování dat níže se dozvíte několik scénářů, které se mohou vyzvat k použití jiného řešení.

### <a name="collect-data"></a>Shromažďování dat

Když je potřeba, aby data byla centralizovaná za účelem dodání zákazníka, je velmi pravděpodobný, aby se data mohla shromažďovat i z různých zdrojů a přesunula se do centralizovaného úložiště dat. Existují dvě primární formy shromažďování dat: integrace a ingestování. Každá z nich poskytuje různé způsoby shromažďování dat.

**Integrace:** Existující data, která se nacházejí v existujícím úložišti dat, je možné integrovat do centralizovaného úložiště dat pomocí tradičních technik přesunu dat. To je zvlášť běžné pro scénáře, které zahrnují cloudové úložiště dat. Tyto techniky sestávají z extrakce dat z existujícího úložiště dat. Pak se data načítají do centrálního úložiště dat. V určitém okamžiku tohoto procesu jsou data často transformovaná tak, aby byla lépe dostupná a relevantní v centrálním úložišti.

Nástroje založené na cloudu tyto techniky přepínají na nástroje pro platby za použití, což snižuje překážku pro shromažďování a centralizaci dat. Nástroje, jako je služba migrace dat a Data Factory, jsou dva běžné příklady v Azure. Referenční architektura pro [datovou továrnu s úložištěm dat OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) poskytuje příklad takového řešení.

Ingestování **:** Některá data nejsou v žádném existujícím úložišti dat. V případě, že jsou tato přechodná data primárním zdrojem inovací, je vhodné zvážit alternativní přístupy. Přechodná data můžete najít v nejrůznějších existujících zdrojích, jako jsou aplikace, rozhraní API, datové streamy, zařízení IoT, blockchain, mezipaměť aplikací, mediální obsah nebo dokonce ploché soubory.

Tyto různé formy dat mohou být integrovány do centrálního úložiště dat v řešení OLAP nebo v řešení pro velké objemy dat. U počátečních iterací cyklů sestavování a seznámení s více instancemi ale může být řešení transakčního zpracování (OLTP) více než dostačující k ověření zákazníka hypotézy. Řešení OLTP nejsou nejlepší kvalitou pro všechny scénáře vytváření sestav. Při [sestavování s zákaznickým soucit se](./build.md) však zaměřuje na zákazníky, kteří mají přednost před technickými rozhodnutími. Jakmile se u zákazníka předpokládá škálování, je možné, že bude potřeba, aby lépe vyhovovala platforma. Referenční architektura v [úložištích OLTP dat](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) může pomoci při určování, které úložiště dat je pro vaše řešení nejvhodnější.

**Virtualizovat:** Integrace a přijímání dat může někdy zpomalit inovace. Je-li řešení pro virtualizaci dat již k dispozici, může to být konkrétnější přístup. Ingestování a integrace může způsobit i duplicitní požadavky na úložiště i vývoj, přidat latenci dat, zvýšit prostor pro útoky, založit problémy s kvalitou a zvýšit úsilí týkající se zásad správného řízení. Virtualizace dat je výhodnější alternativou, která původní data opustí v jednom umístění a vytváří předávací dotazy nebo dotazy na zdrojová data uložená v mezipaměti.

SQL Server 2017 a Azure SQL Data Warehouse obě [základní](/sql/relational-databases/polybase/polybase-guide) podpory, což je přístup k virtualizaci dat, který se nejčastěji používá v Azure.

## <a name="next-steps"></a>Další kroky

V dalším kroku se strategií pro democratizing data vyhodnocuje přístupy, které [zákazníkům přinášejí](./apps.md).

> [!div class="nextstepaction"]
> [Poutaví zákazníci prostřednictvím aplikací](./apps.md)
