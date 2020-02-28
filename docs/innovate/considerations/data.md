---
title: Demokratizujte dat pomocí digitálního vynálezu
description: Přečtěte si o democratization, procesu získávání dat do správných rukou při testování hypotéz a inovace.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 1ee86c13d94f62770e21e3a8208e9c0695725ba5
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170218"
---
# <a name="democratize-data"></a>Demokratizace dat

Uhlí, olej a lidský potenciál byly tři nejdůležitější prostředky během revoluce v průmyslu. Tyto prostředky sestavily společnosti, posunuly trhy a nakonec změnily národy. V digitální ekonomice existují tři stejně důležité prostředky: data, zařízení a lidský potenciál. Každý z těchto prostředků má skvělé možnosti inovace. Pro jakékoli inovace v moderních obdobích jsou data novým olejem.

V současné době jsou v každé společnosti k dispozici kapsy dat, které by bylo možné použít k efektivnějšímu vyhledání a splnění potřeb zákazníků. Omlouváme se, ale proces dolování těchto dat pro účely inovace má dlouhou dobu náročné na čas. Mnohé z nejcennějších řešení potřebných pro zákazníky se nesplnění, protože k datům, která potřebují, nemůžou přistupovat žádné správné osoby.

Democratization dat je proces získávání těchto dat do správných rukou k zajištění inovace. Tento proces může mít několik forem, ale obecně zahrnuje řešení pro ingestovaná nebo integrovaná neupravená data, centralizaci dat, sdílení dat a zabezpečení dat. Po úspěšném provedení těchto metod mohou odborníci na společnosti použít data k otestování hypotézy. V mnoha případech můžou týmy při přijímání v cloudu [sestavovat pomocí zákaznických soucit](./build.md) jenom data a rychle řešit stávající potřeby zákazníků.

## <a name="process-of-democratizing-data"></a>Zpracování democratizing dat

Následující fáze vás provede rozhodnutími a přístupy potřebnými k přijetí řešení, které demokratizuje data. Ne každá fáze bude nutně nutná k sestavení konkrétního řešení. Měli byste však vyhodnotit každou fázi při sestavování řešení pro zákaznickou hypotézu. Každá z nich poskytuje jedinečný přístup pro vytváření inovativních řešení.

![Zpracování dat democratizing](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Sdílení dat

Při [sestavování pomocí zákaznických soucit](./build.md)budou všechny procesy zvyšovat potřebu zákazníků prostřednictvím technického řešení. Vzhledem k tomu, že democratizing data neobsahují žádnou výjimku, začneme sdílením dat. Aby Demokratizujte data, musí zahrnovat řešení, které sdílí data s příjemcem dat. Příjemce dat může být přímým zákazníkem nebo proxy serverem, který provádí rozhodnutí pro zákazníky. Schválení spotřebitelé dat mohou analyzovat, dotazování a sestavovat centralizované údaje bez podpory od zaměstnanců IT.

Mnohé úspěšné inovace byly spuštěny jako minimální životaschopný produkt (MVP), který poskytuje ruční procesy řízené daty jménem zákazníka. V tomto modelu concierge je zaměstnanec dat příjemcem. Tento zaměstnanec používá data k podpoře zákazníka. Pokaždé, když zákazník zahájí ruční podporu, může být hypotéza testována a ověřena. Tento přístup je často nákladově efektivní způsob testování hypotézy zaměřené na zákazníky před tím, než budete investovat do integrovaných řešení.

Primární nástroje pro sdílení dat přímo s příjemci dat zahrnují samoobslužné vytváření sestav nebo data integrovaná do jiných prostředí pomocí nástrojů, jako je [Power BI](https://docs.microsoft.com/power-bi).

> [!NOTE]
> Než budete sdílet data, ujistěte se, že jste si přečetli následující oddíly. Sdílení dat může vyžadovat, aby zásady správného řízení poskytovaly ochranu pro sdílená data. Tato data se taky můžou rozložit mezi několika cloudy a můžou vyžadovat centralizaci. Většina dat se může dokonce nacházet v aplikacích, což bude vyžadovat shromažďování dat předtím, než je budete moct sdílet.

### <a name="govern-data"></a>Řízení dat

Sdílení dat může rychle vydávat MVP, který můžete použít v zákaznických konverzacích. Pokud ale chcete, aby se tato sdílená data mohla využít k užitečným znalostem, je potřeba trochu víc. Po ověření hypotézy prostřednictvím sdílení dat je v další fázi vývoje obvykle řízení dat.

Řízení dat je široké téma, které by mohlo vyžadovat vlastní vyhrazenou architekturu. Tato úroveň členitosti je mimo rozsah architektury pro přijetí do [cloudu](../../index.md). Existuje však několik aspektů zásad správného řízení dat, které byste měli zvážit, jakmile bude ověřena zákaznická hypotéza. Příklad:

- **Je citlivá sdílená data?** [Data by měla být klasifikována](../../govern/policy-compliance/data-classification.md) před veřejným sdílením, aby chránila zájmy zákazníků a společnosti.
- **Pokud jsou data citlivá, jsou zabezpečená?** Ochrana citlivých dat by měla být požadavek na všechna democratized data. Příklad úlohy zaměřené na [zabezpečení datových řešení](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions) poskytuje několik odkazů na zabezpečení dat.
- **Je data v katalogu?** Shromažďování podrobností o datech, která se sdílejí, bude pomoci při dlouhodobé správě dat. Nástroje pro dokumentování dat, jako je Azure Data Catalog, můžou tento proces v cloudu mnohem jednodušeji udělat. Pokyny týkající se [poznámek na data](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) a [dokumentaci zdrojů dat](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) vám pomůžou zrychlit proces.

Pokud je democratization dat důležité pro hypotézu zaměřenou na zákazníky, ujistěte se, že zásady správného řízení sdílených dat jsou někde v plánu vydání. To vám pomůže ochránit zákazníky, spotřebitele dat a společnost.

### <a name="centralize-data"></a>Centralizace dat

Pokud dojde k přerušení dat napříč IT prostředím, můžou být příležitosti pro inovace extrémně omezené, nákladné a časově náročné. Cloud poskytuje nové příležitosti pro centralizaci dat napříč siloy dat. Pokud se k [sestavování s využitím zákaznických soucit](./build.md)vyžaduje centralizaci více zdrojů dat, Cloud dokáže zrychlit testování hypotézy.

> [!CAUTION]
> Centralizované navýšení dat představuje rizikové body v jakémkoli inovačním procesu. Když je centralizaci dat [technickým špičkem](./build.md#reduce-complexity-and-delay-technical-spikes) (na rozdíl od zdroje zákaznické hodnoty), doporučujeme, abyste zpozdili centralizaci až do ověření hypotézy zákazníka.

Pokud je třeba centralizované navýšení dat, je nutné nejprve definovat příslušné úložiště dat pro centralizovaná data. Je dobrým zvykem vytvořit datový sklad v cloudu. Tato přizpůsobitelná možnost poskytuje centrální umístění pro všechna vaše data. Tento typ řešení je k dispozici v možnostech online analytického zpracování (OLAP) nebo ve volbách pro velké objemy dat.

Referenční architektury pro řešení [OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing) a pro [velké](https://docs.microsoft.com/azure/architecture/data-guide/big-data) objemy dat vám pomůžou vybrat nejrelevantnější řešení v Azure. Pokud se vyžaduje hybridní řešení, referenční architektura pro [rozšiřování místních dat](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) může také přispět k urychlení vývoje řešení.

> [!IMPORTANT]
> V závislosti na potřebě zákazníka a zarovnaných řešeních může stačit jednodušší přístup. Cloudový architekt by měl vyzkoušet tým, aby zvážil nižší nákladová řešení, která by mohla vést k rychlejšímu ověření zákaznických předpokladů, zejména při prvotním vývoji. Následující část týkající se shromažďování dat se zabývá některými scénáři, které mohou navrhnout jiné řešení pro vaši situaci.

### <a name="collect-data"></a>Shromažďování dat

Pokud potřebujete, aby data byla centralizovaná za účelem vyřešení potřeb zákazníků, je velmi pravděpodobně nutné shromáždit data z různých zdrojů a přesunout je do centralizovaného úložiště dat. Existují dvě primární formy shromažďování dat: *integrace* *a*ingestování.

**Integrace:** Data, která se nacházejí v existujícím úložišti dat, můžete integrovat do centralizovaného úložiště dat pomocí tradičních technik přesunu dat. To je zvlášť běžné pro scénáře, které zahrnují cloudové úložiště dat. Tyto techniky zahrnují extrakci dat z existujícího úložiště dat a jejich načtení do centrálního úložiště dat. V určitém okamžiku tohoto procesu jsou data obvykle transformovaná tak, aby byla větší použitelnost a relevantní v centrálním úložišti.

Cloudové nástroje tyto techniky přepnuly na nástroje pro platby za použití, čímž se sníží překážka záznamu pro shromažďování a centralizaci dat. Nástroje jako Azure Database Migration Service a Azure Data Factory jsou dva příklady. Referenční architektura pro [datovou továrnu s úložištěm dat OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) je příkladem takového řešení.

**Přijímání:** Některá data se nenacházejí v existujícím úložišti dat. Když jsou tato přechodovaná data primárním zdrojem inovací, budete chtít zvážit alternativní přístupy. Přechodná data můžete najít v nejrůznějších existujících zdrojích, jako jsou aplikace, rozhraní API, datové streamy, zařízení IoT, blockchain, mezipaměť aplikace, multimediální obsah nebo dokonce i v plochých souborech.

Tyto různé formy dat můžete integrovat do centrálního úložiště dat v řešení OLAP nebo pro velké objemy dat. U počátečních iterací v cyklech sestavení – měření – učení, ale řešení online mezitransakčního zpracování (OLTP) může být pro ověření zákaznické hypotézy lepší, než je dostatečné. Řešení OLTP nejsou ve scénářích vytváření sestav nejvyšší kvality. Pokud ale [sestavíte se zákaznickým soucit](./build.md), je důležité se soustředit na potřeby zákazníků, než na technických rozhodnutích nástroje. Po ověření škálování zákaznických předpokladů se může vyžadovat lepší platforma. Referenční architektura v [úložištích dat OLTP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) vám pomůže určit, které úložiště dat je pro vaše řešení nejvhodnější.

**Virtualizovat:** Integrace a přijímání dat může někdy zpomalit inovace. Je-li řešení pro virtualizaci dat již k dispozici, může představovat přiměřenější přístup. Ingestování a integrace může způsobit i duplicitní požadavky na úložiště i vývoj, přidat latenci dat, zvýšit prostor pro útoky, aktivovat problémy s kvalitou a zvyšovat úsilí týkající se zásad správného řízení. Virtualizace dat je důležitější alternativa, která původní data opustí v jednom umístění a vytváří předávací dotazy nebo dotazy na zdrojová data uložená v mezipaměti.

SQL Server 2017 a Azure SQL Data Warehouse obě [základní](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) podpory, což je přístup k virtualizaci dat, který se nejčastěji používá v Azure.

## <a name="next-steps"></a>Další kroky

Díky strategii pro democratizing data můžete dál vyhodnocovat přístupy k [poutavým zákazníkům prostřednictvím aplikací](./apps.md).

> [!div class="nextstepaction"]
> [Poutaví zákazníci prostřednictvím aplikací](./apps.md)
