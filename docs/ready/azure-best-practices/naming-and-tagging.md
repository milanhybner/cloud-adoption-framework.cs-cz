---
title: Doporučené konvence pro tvorbu názvů a značek
description: V tomto článku najdete podrobná doporučení týkající se tvorby názvů a značek prostředků, která jsou konkrétně zaměřena na podporu snah o přijetí podnikového cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: b61c9a9ffd778e657854b4da1269eebdb762c73b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76799841"
---
# <a name="recommended-naming-and-tagging-conventions"></a>Doporučené konvence pro tvorbu názvů a značek

Uspořádání cloudových prostředků způsobem, který podporuje provozní správu a požadavky na monitorování účtů, je běžným problémem při snaze o přijetí velkého cloudu. Když se na prostředky hostované v cloudu použijí správně definované konvence pro tvorbu názvů a značek metadat, mohou IT pracovníci prostředky rychle vyhledat a spravovat. Správně definované názvy a značky také usnadňují obchodním týmům nastavit náklady na využití cloudu prostřednictvím mechanismů vrácení peněz a účtování metodou showback.

Pokyny pro Cetrum architektury Azure pro [pravidla a omezení pro prostředky Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) poskytují obecná doporučení a omezení platforem. Následující diskuze přesahují tyto pokyny s podrobnějšími doporučeními, která jsou speciálně zaměřená na podporu podnikového nasazení v cloudu.

Názvy prostředků může být obtížné změnit. Nastavte prioritu vytváření komplexních zásad vytváření názvů před zahájením jakéhokoli nasazení ve velkém cloudu.

> [!NOTE]
> Každá společnost má jiné požadavky na organizaci a správu. Tato doporučení poskytují výchozí bod pro diskuze v rámci týmů pro přijetí do cloudu.
>
> Jak budou tyto diskuze pokračovat, použijte následující šablonu k zaznamenání rozhodnutí o pojmenování a označování, která uděláte při zarovnání těchto doporučení podle konkrétních obchodních potřeb.
>
> Stáhněte si [šablonu pro sledování konvencí pro tvorbu názvů a značek](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Pojmenovávání a označování prostředků

Strategie pro vytváření názvů a značek zahrnuje firemní a provozní údaje jako součásti názvů prostředků a značek metadat:

- Podnikatelská strana této strategie zajišťuje, že názvy prostředků a značky obsahují informace o organizaci potřebné k identifikaci týmů. Použijte prostředek společně s vlastníky, kteří zodpovídají za náklady na prostředky.
- Provozní údaje zajišťují, aby názvy a značky obsahovaly informace, které IT týmy používají k identifikaci úloh, aplikací, prostředí, závažností a dalších informací užitečných pro správu prostředků.

### <a name="resource-naming"></a>Pojmenovávání prostředků

Efektivní konvence pro tvorbu názvů sestavuje názvy prostředků tak, že jako části názvu prostředku používá důležité údaje o prostředku. Například pomocí těchto [doporučených konvencí pojmenování](#sample-naming-convention)se prostředek veřejné IP adresy pro produkční úlohy služby SharePoint jmenuje takto: `pip-sharepoint-prod-westus-001`.

Takový název vám umožní rychle identifikovat typ prostředku, jeho přidruženou úlohu, prostředí nasazení a oblast Azure, která ho hostuje.

#### <a name="naming-scope"></a>Obor názvů

Všechny typy prostředků Azure mají obor, který definuje úroveň, kterou názvy prostředků musí být jedinečné. Prostředek musí mít jedinečný název v rámci svého oboru.

Virtuální síť má například obor skupiny prostředků, což znamená, že v dané skupině prostředků může být jenom jedna síť s názvem `vnet-prod-westus-001`. Jiné skupiny prostředků ale můžou mít svou vlastní virtuální síť s názvem `vnet-prod-westus-001`. Podsítě, abychom uvedli další příklad, mají obory v rámci virtuálních sítí, což znamená, že každá podsíť ve virtuální síti musí mít jedinečný název.

Některé názvy prostředků, jako jsou služby PaaS s veřejnými koncovými body nebo názvy DNS virtuálního počítače, mají globální obory, což znamená, že musí být jedinečné napříč celou platformou Azure.

Délka názvů prostředků je omezená. Důležité je, abyste při vývoji konvencí pro tvorbu názvů vyvážili kontext vložený v názvu s jeho oborem a délkou názvu. Další informace o pravidlech tvorby názvů týkajících se povolených znaků, oborů a délek názvů pro typy prostředků najdete v tématu [Zásady vytváření názvů pro prostředky Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming).

#### <a name="recommended-naming-components"></a>Doporučené komponenty názvů

Při vytváření konvence pro tvorbu názvů identifikujte klíčové části informace, které chcete aby název prostředku odrážel. Pro různé typy prostředků jsou relevantní různé informace. Následující seznam uvádí příklady informací, které jsou při vytváření názvů prostředků užitečné.

Snažte se, aby byly komponenty názvu krátké a předešli jste tak překročení omezení délky názvu prostředku.

| Komponenta názvu | Popis | Příklady |
| --- | --- | --- |
| Obchodní jednotka | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni V menších organizacích může tato komponenta představovat jeden organizační prvek nejvyšší úrovně. | _fin_, _mktg_, _product_, _it_, _corp_ |
| Typ předplatného | Souhrnný popis účelu předplatného obsahujícího prostředek Často se dělí podle typu prostředí nasazení nebo konkrétních úloh. | _prod_, _Shared_, _klient_ |
| Název aplikace nebo služby | Název aplikace, úlohy nebo služby, do které prostředek patří | _navigator_, _emissions_, _sharepoint_, _hadoop_ |
| Prostředí nasazení | Fáze životního cyklu vývoje pro úlohu, kterou prostředek podporuje | _prod_, _dev_, _QA_, _fáze_, _test_ |
| Region (Oblast) | Oblast Azure, ve které je prostředek nasazen | _westus_, _eastus2_, _westeurope_, _usgovia_ |

#### <a name="recommended-resource-type-prefixes"></a>Doporučené předpony typu prostředku

Každá úloha se může skládat z mnoha jednotlivých prostředků a služeb. Zahrnutí předpon typu prostředku do názvů prostředků usnadňuje vizuální identifikaci komponent aplikace nebo služby.

Následující seznam obsahuje doporučené předpony typů prostředků Azure, které se mají používat při definování konvencí pro tvorbu názvů.

| Typ prostředku                       | Předpona názvu prostředku |
| ----------------------------------- | -------------------- |
| Skupina prostředků                      | rg-                  |
| Skupina dostupnosti                    | využil               |
| Služba API Management              | API                 |
| Virtuální síť                     | vnet-                |
| Brána virtuální sítě             | vnetgw-              |
| Připojení brány                  | cn-                  |
| Podsíť                              | snet-                |
| Skupina zabezpečení sítě              | nsg-                 |
| Tabulka směrování                         | cestě               |
| Virtuální počítač                     | virtuální počítač                   |
| Účet úložiště virtuálního počítače                  | stvm                 |
| Veřejná IP adresa                           | pip-                 |
| Nástroj pro vyrovnávání zatížení                       | lb-                  |
| NIC                                 | nic-                 |
| Key Vault                           | elektrické                  |
| Cluster AKS                         | AKS                 |
| Kontejner AKS                       | př                 |
| Service Bus                         | sb-                  |
| Fronta Service Bus                   | sbq-                 |
| Service Bus téma                   | sbt-                 |
| Plán služby App Service                    | rozhraní                |
| Webová aplikace                             | aplikace                 |
| Function App                        | kláves                |
| Cloudová služba                       | nelze                 |
| Server Azure SQL Database           | SQL                 |
| Databáze Azure SQL                  | sqldb-               |
| Cosmos DB databáze                  | Cosmos              |
| Mezipaměť Azure pro Redis Cache         | redis-               |
| Databáze MySQL                      | mysql-               |
| Databáze PostgreSQL                 | psql                |
| Azure SQL Data Warehouse            | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Účet úložiště                     | St                   |
| Azure StorSimple                    | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services            | ozubeného kola                 |
| Pracovní prostor služby Azure Machine Learning    | mlw-                 |
| Azure Data Lake Storage             | dls                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight – Spark             | hdis-                |
| Azure HDInsight – Hadoop            | hdihd-               |
| Azure HDInsight – R Server          | hdir-                |
| Azure HDInsight – HBase             | hdihb-               |
| Power BI Embedded                   | PBI                 |
| Azure Stream Analytics              | asa-                 |
| Azure Data Factory                  | ADF                 |
| Centrum událostí                           | evh-                 |
| Centrum IoT                             | IoT                 |
| Centra oznámení                   | ntf-                 |
| Obor názvů Notification Hubs         | ntfns-               |

### <a name="metadata-tags"></a>Značky metadat

Když použijete značky metadat na cloudové prostředky, můžete zahrnout informace o těch prostředcích, které nemohly být do názvu prostředku zahrnuty. Tyto informace můžete použít k propracovanějšímu filtrování prostředků a vytváření sestav o prostředcích. Tyto značky by měly obsahovat kontext týkající se úlohy nebo aplikace přiřazené k prostředku, provozních požadavků a informací o vlastnictví. Informace pak můžou využít IT týmy nebo obchodní týmy k vyhledání prostředků nebo k vygenerování sestav týkajících se využití prostředků a fakturace.

To, jaké značky se u prostředků používají a jaké značky jsou povinné nebo volitelné, se u jednotlivých organizací liší. Následující seznam uvádí příklady běžných značek, které obsahují důležitý kontext a informace o prostředku. Tento seznam slouží jako výchozí bod pro vytvoření vlastní konvence pro tvorbu značek.

| Název značky                  | Popis                                                                                                                                                                                                    | Klíč               | Příklad hodnoty                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Název aplikace          | Název aplikace, služby nebo úlohy, které je prostředek přidružen                                                                                                                                 | _NázevAplikace_ | _{název aplikace}_                                    |
| Jméno schvalovatele             | Osoba odpovědná za schvalování nákladů souvisejících s tímto prostředkem                                                                                                                                               | _Schvalovatel_        | _{e-mail}_                                       |
| Požadovaný/schválený rozpočet  | Peníze přidělené pro tuto aplikaci, službu nebo úlohu                                                                                                                                                    | _VelikostRozpočtu_    | _{\$}_                                          |
| Obchodní jednotka             | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni V menších organizacích může tato značka představovat jeden organizační prvek nebo sdílený organizační prvek nejvyšší úrovně. | _ObchodníJednotka_    | _Finance_, _Marketing_, _{název produktu}_ , _Corp_, _Shared_ |
| Nákladové středisko               | Účetní nákladové středisko přidružené tomuto prostředku                                                                                                                                                          | _NákladovéStředisko_      | _{číslo}_                                      |
| Zotavení po havárii         | Obchodní důležitost aplikace, úlohy nebo služby                                                                                                                                                | _DR_              | _Klíčové,_ _kritické_, _nezbytné_         |
| Koncové datum projektu   | Datum naplánovaného vyřazení aplikace, úlohy nebo služby z provozu                                                                                                                                  | _KoncovéDatum_         | _{datum}_                                        |
| Prostředí               | Prostředí nasazení aplikace, úlohy nebo služby                                                                                                                                              | _Prostředí_             | _Prod_, _dev_, _QA_, _fáze_, _test_                    |
| Jméno vlastníka                | Vlastník aplikace, úlohy nebo služby                                                                                                                                                                | _Vlastník_           | _{e-mail}_                                       |
| Jméno žadatele            | Uživatel, který požádal o vytvoření této aplikace                                                                                                                                                          | _Žadatel_       | _{e-mail}_                                       |
| Třída služby             | Úroveň smlouvy o úrovni služeb aplikace, úlohy nebo služby                                                                                                                                       | _TřídaSlužby_    | _Vývoj_, _bronzová_, _stříbrná_, _zlatá_                     |
| Počáteční datum projektu | Datum prvního nasazení aplikace, úlohy nebo služby                                                                                                                                           | _PočátečníDatum_       | _{datum}_                                        |

## <a name="sample-naming-convention"></a>Ukázková konvence pro tvorbu názvů

V následující části najdete příklady schémat tvorby názvů pro běžné typy prostředků Azure, které se nasazují během nasazení podnikového cloudu.

<!-- markdownlint-disable MD033 -->

### <a name="subscriptions"></a>Předplatná

| Typ assetu   | Rozsah                        | Formát                                             | Příklady                                     |
|--------------|------------------------------|----------------------------------------------------|----------------------------------------------|
| Předplatné | Účet / smlouva Enterprise | \<Obchodní jednotka\>-\<Typ předplatného\>-\<\#\#\#\> | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul> |

### <a name="resource-groups"></a>Skupiny prostředků

| Typ assetu     | Rozsah        | Formát                                                     | Příklady                                                                            |
|----------------|--------------|------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Skupina prostředků | Předplatné | RG-\<název aplikace nebo služby\>-\<typ předplatného\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |

### <a name="virtual-networking"></a>Virtuální síť

| Typ assetu               | Rozsah           | Formát                                                                | Příklady                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Azure Virtual Network          | Skupina prostředků  | vnet-\<Typ předplatného\>-\<Oblast\>-\<\#\#\#\>                      | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                                  |
| Virtuální brána virtuální sítě     | Virtuální síť | vnetgw-v-\<typ předplatného\>-\<oblasti\>-\<\#\#\#\>                 | <ul><li>vnetgw-v-Shared-eastus2-001 </li><li>vnetgw-v-prod-westus-001 </li><li>vnetgw-v-Client-eastus2-001</li></ul>                   |
| Místní brána virtuální sítě       | Virtuální brána | Typ předplatného vnetgw-l-\<\>-\<oblasti\>-\<\#\#\#\>                 | <ul><li>vnetgw-l-Shared-eastus2-001 </li><li>vnetgw-l-prod-westus-001 </li><li>vnetgw-l-Client-eastus2-001</li></ul>                   |
| Připojení typu Site-to-Site | Skupina prostředků  | cn-\<název místní brány\>-to-\<název virtuální brány\>                 | <ul><li>cn-l-gw-shared-eastus2-001-to-v-gw-shared-eastus2-001 </li><li>cn-l-gw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| Připojení k virtuální síti         | Skupina prostředků  | cn-\<předplatné1\>\<oblast1\>-to-\<předplatné2\>\<oblast2\>-      | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-prod-eastus2-to-prod-westus</li></ul>                                     |
| Podsíť                   | Virtuální síť | snet-\<předplatné\>-\<podoblast\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                                  |
| Skupina zabezpečení sítě   | Podsíť nebo NIC   | nsg-\<název zásady nebo název aplikace\>-\<\#\#\#\>                             | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>                                  |
| Veřejná IP adresa                | Skupina prostředků  | pip-\<název virtuálního počítače nebo název aplikace\>-\<Prostředí\>-\<podoblast\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

| Typ assetu         | Rozsah          | Formát                                                              | Příklady                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure Virtual Machines    | Skupina prostředků | vm\<název zásady nebo název aplikace\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Účet úložiště virtuálního počítače | Globální         | stvm\<typ výkonu\>\<název aplikace nebo produkční název\>\<oblast\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Název DNS          | Globální         | \<Záznam virtuálního počítače\>.[\<oblast\>.cloudapp.azure.com]                  | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Skupina prostředků | lb-\<název aplikace nebo role\>\<Prostředí\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| NIC                | Skupina prostředků | nic-\<\#\#\>-\<název virtuálního počítače\>-\<předplatné\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>Služby PaaS

| Typ assetu           | Rozsah  | Formát                                                              | Příklady                                                                                 |
|----------------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure Web Apps       | Globální | Název aplikace\<aplikace\>-\<prostředí\>-\<\#\#\#\>. [{azurewebsites.net}] | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Funkce Azure      | Globální | Func-\<název aplikace\>-\<prostředí\>-\<\#\#\#\>. [{azurewebsites.net}] | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Globální | \<název aplikace\>-\<prostředí\>-\<\#\#\#\>. [{cloudapp.net}]       | <ul><li>could-navigator-prod-001.azurewebsites.net </li><li>could-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Typ assetu         | Rozsah       | Formát                                                     | Příklady                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Globální      | sb-\<Název aplikace\>-\<Prostředí\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Fronty Azure Service Bus | Service Bus | sbq-\<popisovač dotazu\>                                   | <ul><li>sbq-messagequery</li></ul>                   |
| Azure Service Bus témata | Service Bus | popisovač dotazu SBT\<\>                                   | <ul><li>sbt-messagequery</li></ul>                   |

### <a name="databases"></a>Databáze

| Typ assetu                          | Rozsah              | Formát                                | Příklady                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Server Azure SQL Database           | Globální             | Název aplikace v jazyce SQL\<\>-prostředí \<\>      | <ul><li>SQL-navigátor-prod </li><li>SQL – emise – dev</li></ul>           |
| Databáze SQL Azure                  | Databáze SQL Azure | SQLDB\<\<prostředí s názvem databáze\>| <ul><li>SQLDB – uživatelé – prod </li><li>SQLDB – uživatelé – dev</li></ul>               |
| Azure Cosmos DB                     | Globální             | Cosmos\<název aplikace\>-prostředí \<\>   | <ul><li>Cosmos-navigátor-prod </li><li>Cosmos – emise – dev</li></ul>       |
| Azure Cache for Redis               | Globální             | redis-\<Název aplikace\>-\<Prostředí\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Globální             | mysql-\<Název aplikace\>-\<Prostředí\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure Database for PostgreSQL       | Globální             | psql\<název aplikace\>-prostředí \<\>     | <ul><li>psql-navigátor-prod </li><li>psql – emise – dev</li></ul>         |
| Azure SQL Data Warehouse            | Globální             | sqldw-\<Název aplikace\>-\<Prostředí\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Databáze SQL Azure | sqlstrdb-\<Název aplikace\>-\<Prostředí\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Storage

| Typ assetu                              | Rozsah  | Formát                                                                        | Příklady                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Účet služby Azure Storage – obecné použití     | Globální | st\<název úložiště\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Účet služby Azure Storage – diagnostické protokoly | Globální | stdiag\<první dvě písmena názvu předplatného a číslo\>\<oblast\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                        | Globální | ssimp\<Název aplikace\>\<Prostředí\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>AI a Machine Learning

| Typ assetu                       | Rozsah          | Formát                            | Příklady                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Globální         | srch-\<Název aplikace\>-\<Prostředí\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services         | Skupina prostředků | ozubeného kola\<název aplikace\>-prostředí \<\>   | <ul><li>ozubeného kola-navigátor-prod </li><li>ozubeného kola – emise – dev</li></ul>     |
| Pracovní prostor služby Azure Machine Learning | Skupina prostředků | MLW\<název aplikace\>-prostředí \<\>   | <ul><li>MLW-navigátor-prod </li><li>MLW – emise – dev</li></ul>     |

### <a name="analytics"></a>Analýza

| Typ assetu                | Rozsah  | Formát                             | Příklady                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Globální | ADF –\<název aplikace\>\<prostředí\>    | <ul><li>ADF – navigátor – prod </li><li>ADF – emise – vývoj</li></ul>     |
| Azure Data Lake Storage   | Globální | dls\<Název aplikace\>\<Prostředí\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Azure Data Lake Analytics | Globální | dla\<Název aplikace\>\<Prostředí\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight – Spark   | Globální | hdis-\<Název aplikace\>-\<Prostředí\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight – Hadoop  | Globální | hdihd-\<Název aplikace\>-\<Prostředí\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight – R Server| Globální | hdir-\<Název aplikace\>-\<Prostředí\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight – HBase   | Globální | hdihb-\<Název aplikace\>-\<Prostředí\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Power BI Embedded         | Globální | PBI\<název aplikace\>\<prostředí\>    | <ul><li>PBI-navigátor-prod </li><li>PBI – emise – dev</li></ul> |

### <a name="data-streams--internet-of-things-iot"></a>Datové proudy/Internet věcí (IoT)

| Typ assetu                         | Rozsah          | Formát                             | Příklady                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics             | Skupina prostředků | asa-\<Název aplikace\>-\<Prostředí\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Globální         | Název aplikace pro IoT-\<\>-prostředí \<\>   | <ul><li>IoT-navigátor-prod </li><li>IoT – emise – dev</li></ul>     |
| Azure Event Hubs                   | Globální         | evh-\<Název aplikace\>-\<Prostředí\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs            | Skupina prostředků | NTF\<název aplikace\>-prostředí \<\>   | <ul><li>NTF-navigátor-prod </li><li>NTF – emise – dev</li></ul>     |
| Obor názvů Azure Notification Hubs  | Globální         | ntfns\<název aplikace\>-prostředí \<\> | <ul><li>ntfns-navigátor-prod </li><li>ntfns – emise – dev</li></ul> |
