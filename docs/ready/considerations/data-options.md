---
title: Zkontrolujte možnosti vašich dat.
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zkontrolujte možnosti vašich dat pro úlohy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 950465788053fa0977a158a5363cb6271e65b3e6
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73243146"
---
# <a name="review-your-data-options"></a>Zkontrolujte možnosti vašich dat.

Když své cílové prostředí připravujete na přechod do cloudu, musíte určit požadavky na data pro hostování vašich úloh. Databázové produkty a služby Azure podporují širokou škálu scénářů a funkcí pro ukládání dat. Způsob, jakým u cílového prostředí nakonfigurujete podporu datových požadavků, závisí na zásadách správného řízení, technických a obchodních požadavcích vašich úloh.

## <a name="identify-data-services-requirements"></a>Zjištění požadavků na datové služby

V rámci vyhodnocení a přípravy cílového prostředí musíte identifikovat všechna úložiště dat, která bude vaše cílové prostředí muset podporovat. Součástí tohoto procesu je posouzení všech aplikací a služeb, ze kterých jsou tvořeny vaše úlohy, a určení požadavků na ukládání a zpřístupnění jejich dat. Po zjištění a zdokumentování těchto požadavků můžete pro cílové prostředí vytvořit zásady, které na základě potřeb vašich úloh určují, jaké typy prostředků jsou povolené.

Pro každou aplikaci nebo službu, kterou nasadíte do cílového prostředí, použijte jako výchozí bod následující rozhodovací strom, který vám pomůže určit vhodné služby úložiště dat, které byste měli použít:

![Rozhodovací strom databázových služeb Azure](../../_images/ready/data-decision-tree.png)

### <a name="key-questions"></a>Klíčové otázky

Zodpovězení následujících otázek týkajících se vašich úloh vám pomůže při rozhodování na základě rozhodovacího stromu databázových služeb Azure:

- **Potřebujete mít úplnou kontrolu nad vlastnictvím databázového softwaru nebo hostitelského operačního systému?** Některé situace vyžadují, abyste vlastnili nebo měli vysoký stupeň kontroly nad konfigurací softwaru a servery, na kterých se hostují vaše databázové úlohy. V těchto situacích můžete nasadit vlastní virtuální počítače IaaS (infrastruktura jako služba), abyste měli úplnou kontrolu nad nasazením a konfigurací datových služeb. Pokud tyto požadavky nemáte, mohou služby spravované databáze PaaS (platforma jako služba) snížit náklady na správu a provoz.
- **Budou vaše úlohy používat technologii relačních databází?** Pokud ano, jakou technologii plánujete použít? Azure poskytuje spravované databázové funkce PaaS pro [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), [MySQL](https://docs.microsoft.com/azure/mysql/overview), [PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) a [MariaDB](https://docs.microsoft.com/azure/mariadb/overview).
- **Budou vaše úlohy používat SQL Server?** V Azure mohou vaše úlohy běžet na [SQL Serveru ve službě Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/sql-server), což je řešení IaaS, nebo v [hostované službě Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), což je řešení PaaS. Volba použité možnosti se primárně řídí otázkou, zda chcete spravovat databázi, instalovat opravy a provádět zálohování, nebo jestli tyto operace chcete delegovat na Azure. V některých situacích mohou problémy s kompatibilitou vyžadovat použití SQL Serveru hostovaného v řešení IaaS. Další informace o tom, jak zvolit správnou možnost pro vaše úlohy, najdete v tématu o [volbě správné možnosti SQL Serveru v Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).
- **Budou vaše úlohy používat databázové úložiště typu klíč/hodnota?** [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) nabízí vysoce výkonné řešení datového úložiště typu klíč/hodnota s mezipamětí, které obsluhuje rychlé a škálovatelné aplikace. [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) poskytuje také funkce úložiště typu klíč/hodnota pro obecné účely.
- **Budou vaše úlohy používat data dokumentů nebo grafů?** [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) je vícemodelová databázová služba, která podporuje širokou škálu datových typů a rozhraní API. Azure Cosmos DB poskytuje rovněž databázové funkce pro dokumenty a grafy.
- **Budou vaše úlohy používat data v rodinách sloupců?** [Apache HBase v Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview) využívá Apache Hadoop. Podporuje velké objemy nestrukturovaných a částečně strukturovaných dat v bezschématové databázi uspořádané podle rodin sloupců.
- **Budou vaše úlohy vyžadovat funkce vysokokapacitní analýzy dat?** K efektivnímu ukládání a dotazování strukturovaných dat v řádu petabajtů můžete použít [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is). Pro úlohy s nestrukturovanými velkými objemy dat můžete použít [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) umožňující ukládání a analýzu petabajtových souborů a biliónů objektů.
- **Budou vaše úlohy vyžadovat funkce vyhledávacího modulu?** K vytvoření cloudových vyhledávacích indexů vylepšených o umělou inteligenci, které lze integrovat do vašich aplikací, můžete použít [Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search).
- **Budou vaše úlohy používat data časových řad?** Služba [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-overview) je určená k ukládání, vizualizaci a dotazování velkých objemů dat časových řad, jako jsou například data generovaná zařízeními IoT.

> [!NOTE]
> Další informace o posouzení databázových možností pro jednotlivé aplikace nebo služby najdete v [příručce Aplikační architektura v Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-comparison).

## <a name="common-database-scenarios"></a>Běžné databázové scénáře

Následující tabulka obsahuje požadavky na několik běžných scénářů použití a doporučené databázové služby pro jejich obsluhu:

| **Scénář** | **Datová služba** |
|-----|-----|
| Potřebuji globálně distribuovanou vícemodelovou databázi s podporou možností NoSQL. | [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) |
| Potřebuji plně spravovanou relační databázi, která se rychle zřídí, průběžně škáluje a zahrnuje integrované inteligentní funkce a zabezpečení. | [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) |
| Potřebuji plně spravovanou škálovatelnou relační databázi MySQL s vysokou dostupností a integrovaným zabezpečením bez dalších poplatků. | [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) |
| Potřebuji plně spravovanou škálovatelnou relační databázi PostgreSQL s vysokou dostupností a integrovaným zabezpečením bez dalších poplatků. | [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) |
| Chci hostovat podnikové aplikace SQL Serveru v cloudu a mít plnou kontrolu nad operačním systémem serveru. | [SQL Server na virtuálních počítačích](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview) |
| Potřebuji plně spravovaný elastický datový sklad se zabezpečením na všech úrovních škálování bez dalších poplatků. | [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) |
| Potřebuji prostředky úložiště datového jezera, které podporují clustery Hadoop nebo data HDFS. | [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) |
| Potřebuji vysokou propustnost a stálý přístup k datům s nízkou latenci pro podporu rychlých a škálovatelných aplikací. | [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) |
| Potřebuji plně spravovanou škálovatelnou relační databázi MariaDB s vysokou dostupností a integrovaným zabezpečením bez dalších poplatků. | [Azure Database for MariaDB](https://docs.microsoft.com/azure/mariadb/overview) |

## <a name="regional-availability"></a>Regionální dostupnost

Azure vám umožňuje dodávat služby v měřítku, jaké potřebujete, abyste se mohli spojit se svými zákazníky a partnery,  _ať jsou kdekoli_. Klíčovým faktorem při plánování cloudového nasazení je určení, která oblast Azure bude hostovat prostředky vašich úloh.

Většina databázových služeb je všeobecně dostupná ve většině oblastí Azure. Několik oblastí, převážně zaměřených na zákazníky ze státní správy, však podporuje jen podmnožinu těchto produktů. Než se rozhodnete, ve kterých oblastech nasadíte databázové prostředky, doporučujeme na [stránce oblastí](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=data-factory,sql-server-stretch-database,redis-cache,database-migration,sql-data-warehouse,postgresql,mariadb,cosmos-db,mysql,sql-database)  zjistit nejnovější stav regionální dostupnosti.

Další informace o globální infrastruktuře Azure najdete na [stránce oblastí Azure](https://azure.microsoft.com/global-infrastructure/regions). Můžete si také prohlédnout  [produkty dostupné podle oblastí](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all), kde najdete konkrétní podrobnosti o celkových službách dostupných v jednotlivých oblastech Azure.

## <a name="data-residency-and-compliance-requirements"></a>Požadavky na rezidenci dat a dodržování předpisů

Na vaše úlohy se budou často vztahovat právní a smluvní požadavky týkající se datového úložiště. Tyto požadavky se mohou lišit v závislosti na sídle vaší organizace, jurisdikci, ve které se nacházejí fyzické prostředky, které hostují vaše uložená data, a příslušném obchodním sektoru. Mezi datové povinnosti, které je potřeba zvážit, patří klasifikace dat, umístění dat a individuální zodpovědnosti za ochranu dat v rámci sdíleného modelu odpovědnosti. Tyto požadavky jsou rozebrány v dokumentu white paper o  [zajištění odpovídající rezidence dat a zabezpečení s využitím Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Součástí vašeho úsilí o dodržování předpisů může být kontrola nad tím, kde jsou fyzicky umístěny vaše databáze. Oblasti Azure jsou uspořádané do skupin označovaných jako zeměpisné oblasti.  [Zeměpisná oblast Azure](https://azure.microsoft.com/global-infrastructure/geographies)  zaručuje, že se v rámci příslušných zeměpisných a politických hranic dodržují požadavky na rezidenci dat, suverenitu, dodržování předpisů a odolnost. Pokud vaše úlohy podléhají suverenitě dat nebo jiným požadavkům na dodržování předpisů, musíte prostředky úložiště nasadit do oblastí ve vyhovující geografické oblasti Azure.

## <a name="establish-controls-for-database-services"></a>Stanovení kontrolních mechanismů pro databázové služby

Při přípravě cílového prostředí můžete stanovit kontrolní mechanismy, které omezují, jaká úložiště dat mohou jednotliví uživatelé nasazovat. Kontrolní mechanismy vám pomohou s řízením nákladů a omezením rizik zabezpečení a zároveň umožní vývojářům a IT týmům nasazovat a konfigurovat prostředky potřebné pro podporu vašich úloh.

Po zjištění a zdokumentování požadavků na cílové prostředí můžete pomocí [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) určit databázové prostředky, které uživatelé mohou vytvářet. Kontrolní mechanismy mohou mít formu [povolení nebo zákazu vytváření různých typů databázových prostředků](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types). Uživatele můžete například omezit tak, aby mohli vytvářet jen prostředky Azure SQL Database. Pomocí zásad můžete také řídit přípustné možnosti při vytváření prostředku, například [omezit, jaké cenové úrovně SQL Database lze zřídit](https://docs.microsoft.com/azure/governance/policy/samples/allowed-sql-db-skus) nebo [povolit jen konkrétní verze SQL Serveru](https://docs.microsoft.com/azure/governance/policy/samples/require-sql-12), které lze nainstalovat na virtuální počítače IaaS.

Zásady mohou být vymezené na prostředky, skupiny prostředků, předplatná a skupiny pro správu. Tyto zásady můžete začlenit do definic [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) a opakovaně je používat v rámci svého cloudu.
