---
title: Doporučené konvence pro tvorbu názvů a značek
description: Seznamte se s podrobnými doporučeními pro vytváření názvů a označování prostředků, která jsou určená speciálně při podpoře úsilí podnikového Cloud
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/05/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness, fasttrack-edit
ms.openlocfilehash: f3d92caa6d71451975c47c1c596fe2332264388f
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433931"
---
<!-- cSpell:ignore westeurope usgovia accountlookup messagequery -->

# <a name="recommended-naming-and-tagging-conventions"></a>Doporučené konvence pro tvorbu názvů a značek

Uspořádejte cloudové prostředky, aby podporovaly provozní správu a požadavky na monitorování účtů. Jasně definované konvence pojmenování a označování metadat vám pomůžou rychle vyhledat a spravovat prostředky. Tyto konvence také pomůžou spojit náklady na využití cloudu s obchodními týmy prostřednictvím účetních mechanismů vrácení peněz a showback.

Pokyny pro Cetrum architektury Azure pro [pravidla a omezení pro prostředky Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) poskytují obecná doporučení a omezení platforem. Následující diskuze přesahují tyto pokyny s podrobnějšími doporučeními, která jsou speciálně zaměřená na podporu podnikového nasazení v cloudu.

Změna názvů prostředků může být obtížná. Navažte ucelenou konvenci vytváření názvů před zahájením jakéhokoli nasazení v cloudu.

> [!NOTE]
> Každá společnost má jiné požadavky na organizaci a správu. Tato doporučení poskytují výchozí bod pro diskuze v rámci týmů pro přijetí do cloudu.
>
> Jak budou tyto diskuze pokračovat, použijte následující šablonu k zaznamenání rozhodnutí o pojmenování a označování, která uděláte při zarovnání těchto doporučení podle konkrétních obchodních potřeb.
>
> Stáhněte si [šablonu pro sledování konvencí pro tvorbu názvů a značek](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Pojmenovávání a označování prostředků

Strategie pro vytváření názvů a značek zahrnuje firemní a provozní údaje jako součásti názvů prostředků a značek metadat:

- Na straně podnikání této strategie je zajištěno, že názvy a značky prostředků obsahují informace o organizaci potřebné k identifikaci týmů. Použijte prostředek společně s vlastníky, kteří zodpovídají za náklady na prostředky.
- Provozní údaje zajišťují, aby názvy a značky obsahovaly informace, které IT týmy používají k identifikaci úloh, aplikací, prostředí, závažností a dalších informací užitečných pro správu prostředků.

## <a name="resource-naming"></a>Pojmenovávání prostředků

Efektivní konvence pro tvorbu názvů sestavuje názvy prostředků tak, že jako části názvu prostředku používá důležité údaje o prostředku. Například pomocí těchto [doporučených konvencí pojmenování](#example-names)se prostředek veřejné IP adresy pro produkční úlohy služby SharePoint jmenuje takto: `pip-sharepoint-prod-westus-001`.

Takový název vám umožní rychle identifikovat typ prostředku, jeho přidruženou úlohu, prostředí nasazení a oblast Azure, která ho hostuje.

### <a name="naming-scope"></a>Obor názvů

Všechny typy prostředků Azure mají obor, který definuje úroveň, kterou názvy prostředků musí být jedinečné. Prostředek musí mít jedinečný název v rámci svého oboru.

Virtuální síť má například obor skupiny prostředků, což znamená, že v dané skupině prostředků může být jenom jedna síť s názvem `vnet-prod-westus-001`. Jiné skupiny prostředků ale můžou mít svou vlastní virtuální síť s názvem `vnet-prod-westus-001`. Podsítě, abychom uvedli další příklad, mají obory v rámci virtuálních sítí, což znamená, že každá podsíť ve virtuální síti musí mít jedinečný název.

Některé názvy prostředků, jako jsou služby PaaS s veřejnými koncovými body nebo názvy DNS virtuálního počítače, mají globální obory, což znamená, že musí být jedinečné napříč celou platformou Azure.

Délka názvů prostředků je omezená. Důležité je, abyste při vývoji konvencí pro tvorbu názvů vyvážili kontext vložený v názvu s jeho oborem a délkou názvu. Další informace o pravidlech tvorby názvů týkajících se povolených znaků, oborů a délek názvů pro typy prostředků najdete v tématu [Zásady vytváření názvů pro prostředky Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming).

### <a name="recommended-naming-components"></a>Doporučené komponenty názvů

Při vytváření konvence pro tvorbu názvů identifikujte klíčové části informace, které chcete aby název prostředku odrážel. Pro různé typy prostředků jsou relevantní různé informace. Následující seznam uvádí příklady informací, které jsou při vytváření názvů prostředků užitečné.

Snažte se, aby byly komponenty názvu krátké a předešli jste tak překročení omezení délky názvu prostředku.

| Komponenta názvu            | Popis                                                                                                                                                                                                      | Příklady                                         |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| Obchodní jednotka               | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni V menších organizacích může tato komponenta představovat jeden organizační prvek nejvyšší úrovně. | _fin_, _mktg_, _product_, _it_, _corp_           |
| Typ předplatného           | Souhrnný popis účelu předplatného obsahujícího prostředek Často se dělí podle typu prostředí nasazení nebo konkrétních úloh.                                                       | _prod_, _Shared_, _klient_                       |
| Název aplikace nebo služby | Název aplikace, úlohy nebo služby, do které prostředek patří                                                                                                                                    | _navigator_, _emissions_, _sharepoint_, _hadoop_ |
| Prostředí nasazení      | Fáze životního cyklu vývoje pro úlohu, kterou prostředek podporuje                                                                                                                              | _prod_, _dev_, _QA_, _fáze_, _test_             |
| Oblast                      | Oblast Azure, ve které je prostředek nasazen                                                                                                                                                                 | _westus_, _eastus2_, _westeurope_, _usgovia_     |

### <a name="recommended-resource-type-prefixes"></a>Doporučené předpony typu prostředku

Každá úloha se může skládat z mnoha jednotlivých prostředků a služeb. Zahrnutí předpon typu prostředku do názvů prostředků usnadňuje vizuální identifikaci komponent aplikace nebo služby.

Následující seznam obsahuje doporučené předpony typů prostředků Azure, které se mají používat při definování konvencí pro tvorbu názvů.

<!-- cSpell:disable -->

### <a name="general"></a>Obecné

| Typ assetu                      | Předpona názvu |
|---------------------------------|-------------|
| Skupina prostředků                  | rg-         |
| Definice zásady               | politických     |
| Instance služby API Management | APIM       |

### <a name="networking"></a>Sítě

| Typ assetu                       | Předpona názvu |
|----------------------------------|-------------|
| Virtuální síť                  | vnet-       |
| Podsíť                           | snet-       |
| Síťové rozhraní (NIC)          | nic-        |
| Veřejná IP adresa                | pip-        |
| Load Balancer (interní)         | lbi-        |
| Load Balancer (externí)         | lbe-        |
| Skupina zabezpečení sítě (NSG)     | nsg-        |
| Skupina zabezpečení aplikace (ASG) | ASG        |
| Brána místní sítě            | lgw-        |
| Brána virtuální sítě          | vgw-        |
| Připojení VPN                   | cn-         |
| Application Gateway              | agw-        |
| Tabulka směrování                      | cestě      |
| Profil služby Traffic Manager          | traf-       |

### <a name="compute-and-web"></a>Výpočetní prostředí a Web

| Typ assetu                  | Předpona názvu |
|-----------------------------|-------------|
| Virtuální počítač             | vm          |
| Škálovací sada virtuálních počítačů   | VMSS       |
| Skupina dostupnosti            | využil      |
| Účet úložiště virtuálního počítače          | stvm        |
| Připojený počítač ke službě Azure ARC | arcm-       |
| Instance kontejneru          | ACI        |
| Cluster AKS                 | AKS        |
| Cluster Service Fabric      | SF         |
| Služba App Service Environment     | ASE        |
| Plán služby App Service            | rozhraní       |
| Webová aplikace                     | aplikace        |
| Function App                | kláves       |
| Cloudová služba               | nelze        |
| Notification Hubs           | ntf-        |
| Obor názvů Notification Hubs | ntfns-      |

### <a name="databases"></a>Databáze

| Typ assetu                     | Předpona názvu |
|--------------------------------|-------------|
| Server Azure SQL Database      | SQL        |
| Databáze Azure SQL             | sqldb-      |
| Cosmos DB databáze             | Cosmos     |
| Mezipaměť Azure pro instanci Redis | redis-      |
| Databáze MySQL                 | mysql-      |
| Databáze PostgreSQL            | psql       |
| Azure SQL Data Warehouse       | sqldw-      |
| Azure Synapse Analytics        | znaky        |
| SQL Server Stretch Database    | sqlstrdb-   |

### <a name="storage"></a>Úložiště

| Typ assetu       | Předpona názvu |
|------------------|-------------|
| Účet úložiště  | St          |
| Azure StorSimple | ssimp       |

### <a name="ai--machine-learning"></a>AI a Machine Learning

| Typ assetu                       | Předpona názvu |
|----------------------------------|-------------|
| Azure Cognitive Search           | srch-       |
| Azure Cognitive Services         | ozubeného kola        |
| Pracovní prostor služby Azure Machine Learning | mlw-        |

### <a name="analytics-and-iot"></a>Analýzy a IoT

| Typ assetu                      | Předpona názvu |
|---------------------------------|-------------|
| Server Azure Analysis Services  | formátu         |
| Pracovní prostor Azure Databricks      | dbw-        |
| Azure Stream Analytics          | asa-        |
| Azure Data Factory              | ADF        |
| Účet Data Lake Store         | dls         |
| Účet Data Lake Analytics     | dla         |
| Centrum událostí                       | evh-        |
| HDInsight – cluster Hadoop      | Hadoop     |
| Cluster HDInsight-HBA       | HBase      |
| Cluster HDInsight-Kafka       | Kafka      |
| Cluster HDInsight-Spark       | perlivých      |
| Cluster HDInsight-clustering       | chráněn      |
| Cluster služeb HDInsight-ML | MLS        |
| IoT Hub                         | IoT        |
| Power BI Embedded               | PBI        |

### <a name="integration"></a>Integrace

| Typ assetu        | Předpona názvu |
|-------------------|-------------|
| Logické aplikace        | postupu      |
| Service Bus       | sb-         |
| Service Bus | sbq-        |
| Téma služby Service Bus | sbt-        |

### <a name="management-and-governance"></a>Správa a zásady správného řízení

| Typ assetu              | Předpona názvu |
|-------------------------|-------------|
| Podrobného plánu               | kontrol         |
| Trezor klíčů               | elektrické         |
| Pracovní prostor služby Log Analytics | protokolu        |
| Application Insights    | appi-       |
| Trezor služby Recovery Services | rsv-        |

### <a name="migration"></a>Migrace

| Typ assetu                          | Předpona názvu |
|-------------------------------------|-------------|
| Azure Migrate projekt               | migr-       |
| Instance Database Migration Service | dokumentů        |
| Trezor služby Recovery Services             | rsv-        |

<!-- cSpell:enable -->

## <a name="metadata-tags"></a>Značky metadat

Když použijete značky metadat na cloudové prostředky, můžete zahrnout informace o těch prostředcích, které nemohly být do názvu prostředku zahrnuty. Tyto informace můžete použít k propracovanějšímu filtrování prostředků a vytváření sestav o prostředcích. Tyto značky by měly obsahovat kontext týkající se úlohy nebo aplikace přiřazené k prostředku, provozních požadavků a informací o vlastnictví. Informace pak můžou využít IT týmy nebo obchodní týmy k vyhledání prostředků nebo k vygenerování sestav týkajících se využití prostředků a fakturace.

To, jaké značky se u prostředků používají a jaké značky jsou povinné nebo volitelné, se u jednotlivých organizací liší. Následující seznam uvádí příklady běžných značek, které obsahují důležitý kontext a informace o prostředku. Tento seznam slouží jako výchozí bod pro vytvoření vlastní konvence pro tvorbu značek.

| Název značky                  | Popis                                                                                                                                                                                                          | Klíč               | Příklad hodnoty                                              |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|------------------------------------------------------------|
| Název aplikace          | Název aplikace, služby nebo úlohy, které je prostředek přidružen                                                                                                                                       | _NázevAplikace_ | _{název aplikace}_                                               |
| Jméno schvalovatele             | Osoba odpovědná za schvalování nákladů souvisejících s tímto prostředkem                                                                                                                                                     | _Schvalovatel_        | _{e-mail}_                                                  |
| Požadovaný/schválený rozpočet  | Peníze přidělené pro tuto aplikaci, službu nebo úlohu                                                                                                                                                          | _VelikostRozpočtu_    | _{\$}_                                                     |
| Obchodní jednotka             | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni V menších organizacích může tato značka představovat jeden organizační prvek nebo sdílený organizační prvek nejvyšší úrovně. | _ObchodníJednotka_    | _Finance_, _Marketing_, _{název produktu}_ , _Corp_, _Shared_ |
| Nákladové středisko               | Účetní nákladové středisko přidružené tomuto prostředku                                                                                                                                                                | _NákladovéStředisko_      | _{číslo}_                                                 |
| Zotavení po havárii         | Obchodní důležitost aplikace, úlohy nebo služby                                                                                                                                                       | _DR_              | _Klíčové,_ _kritické_, _nezbytné_                |
| Koncové datum projektu   | Datum naplánovaného vyřazení aplikace, úlohy nebo služby z provozu                                                                                                                                         | _KoncovéDatum_         | _{datum}_                                                   |
| Prostředí               | Prostředí nasazení aplikace, úlohy nebo služby                                                                                                                                                     | _Prostředí_             | _Prod_, _dev_, _QA_, _fáze_, _test_                       |
| Jméno vlastníka                | Vlastník aplikace, úlohy nebo služby                                                                                                                                                                      | _Vlastník_           | _{e-mail}_                                                  |
| Jméno žadatele            | Uživatel, který požádal o vytvoření této aplikace                                                                                                                                                                 | _Žadatel_       | _{e-mail}_                                                  |
| Třída služby             | Úroveň smlouvy o úrovni služeb aplikace, úlohy nebo služby                                                                                                                                              | _TřídaSlužby_    | _Vývoj_, _bronzová_, _stříbrná_, _zlatá_                          |
| Počáteční datum projektu | Datum prvního nasazení aplikace, úlohy nebo služby                                                                                                                                                  | _PočátečníDatum_       | _{datum}_                                                   |

## <a name="example-names"></a>Příklady názvů

V následující části najdete některé příklady názvů běžných typů prostředků Azure v podnikovém nasazení v podnikovém cloudu.

<!-- cSpell:disable -->

<!-- markdownlint-disable MD024 MD033 -->

### <a name="example-names-general"></a>Příklady názvů: Obecné

| Typ assetu                      | Rozsah                              | Formát                                                      | Příklady                                                                                                                |
|---------------------------------|------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Předplatné                    | Zohledňují <br/>Smlouva Enterprise | \<Obchodní jednotka\>-\<Typ předplatného\>-\<\#\#\#\>          | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul>                                        |
| Skupina prostředků                  | Předplatné                       | RG-\<název aplikace nebo služby\>-\<typ předplatného\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |
| Instance služby API Management | Globální                             | APIM-\<název aplikace nebo služby\>                                | APIM-navigátor-prod                                                                                                     |

### <a name="example-names-networking"></a>Příklady názvů: sítě

| Typ assetu                   | Rozsah           | Formát                                                               | Příklady                                                                                                                      |
|------------------------------|-----------------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Virtuální síť              | Skupina prostředků  | vnet-\<Typ předplatného\>-\<Oblast\>-\<\#\#\#\>                     | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                      |
| Podsíť                       | Virtuální síť | snet-\<předplatné\>-\<podoblast\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                      |
| Síťové rozhraní (NIC)      | Skupina prostředků  | nic-\<\#\#\>-\<název virtuálního počítače\>-\<předplatné\>\<\#\#\#\>                   | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>                 |
| Veřejná IP adresa            | Skupina prostředků  | pip-\<název virtuálního počítače nebo název aplikace\>-\<Prostředí\>-\<podoblast\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                              |
| Nástroj pro vyrovnávání zatížení                | Skupina prostředků  | lb-\<název aplikace nebo role\>\<Prostředí\>\<\#\#\#\>                     | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                                        |
| Skupina zabezpečení sítě (NSG) | Podsíť nebo NIC   | NSG\<název zásady nebo název aplikace\>-\<\#\#\#\>                           | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>             |
| Brána místní sítě        | Virtuální brána | LGW-\<typ předplatného\>-\<oblasti\>-\<\#\#\#\>                      | <ul><li>LGW-Shared-eastus2-001 </li><li>LGW-prod-westus-001 </li><li>LGW-Client-eastus2-001</li></ul>                         |
| Brána virtuální sítě      | Virtuální síť | vgw-\<typ předplatného\>-\<oblasti\>-\<\#\#\#\>                      | <ul><li>vgw-Shared-eastus2-001 </li><li>vgw-prod-westus-001 </li><li>vgw-Client-eastus2-001</li></ul>                         |
| Připojení Site-to-site      | Skupina prostředků  | cn-\<název místní brány\>-to-\<název virtuální brány\>                | <ul><li>CN-LGW-Shared-eastus2-001-to-vgw-Shared-eastus2-001 </li><li>CN-LGW-Shared-eastus2-001-to-Shared-westus-001</li></ul> |
| Připojení VPN               | Skupina prostředků  | cn-\<předplatné1\>\<oblast1\>-to-\<předplatné2\>\<oblast2\>-     | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-prod-eastus2-to-prod-westus</li></ul>                                  |
| Tabulka směrování                  | Skupina prostředků  | Route-\<název směrovací tabulky\>                                           | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                                        |
| Název DNS                    | Globální          | \<Záznam virtuálního počítače\>.[\<oblast\>.cloudapp.azure.com]                   | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                                      |

### <a name="example-names-compute-and-web"></a>Příklady názvů: COMPUTE a Web

| Typ assetu                  | Rozsah          | Formát                                                              | Příklady                                                                                                                          |
|-----------------------------|----------------|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Virtuální počítač             | Skupina prostředků | vm\<název zásady nebo název aplikace\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Účet úložiště virtuálního počítače          | Globální         | stvm\<typ výkonu\>\<název aplikace nebo produkční název\>\<oblast\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Webová aplikace                     | Globální         | Název aplikace\<aplikace\>-\<prostředí\>-\<\#\#\#\>. [{azurewebsites.net}]   | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Function App                | Globální         | Func-\<název aplikace\>-\<prostředí\>-\<\#\#\#\>. [{azurewebsites.net}]  | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul>                 |
| Cloudová služba               | Globální         | \<název aplikace\>-\<prostředí\>-\<\#\#\#\>. [{cloudapp.net}]        | <ul><li>could-navigator-prod-001.azurewebsites.net </li><li>could-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Centrum oznámení            | Skupina prostředků | NTF\<název aplikace\>-prostředí \<\>                                    | <ul><li>NTF-navigátor-prod </li><li>NTF – emise – dev</li></ul>                                                                   |
| Obor názvů Notification Hubs | Globální         | ntfns\<název aplikace\>-prostředí \<\>                                  | <ul><li>ntfns-navigátor-prod </li><li>ntfns – emise – dev</li></ul>                                                               |

### <a name="example-names-databases"></a>Příklady názvů: databáze

| Typ assetu                     | Rozsah              | Formát                                 | Příklady                                                                  |
|--------------------------------|--------------------|----------------------------------------|---------------------------------------------------------------------------|
| Server Azure SQL Database      | Globální             | Název aplikace v jazyce SQL\<\>-prostředí \<\>       | <ul><li>SQL-navigátor-prod </li><li>SQL – emise – dev</li></ul>           |
| Databáze Azure SQL             | Azure SQL Database | SQLDB\<>\<prostředí s názvem databáze\> | <ul><li>SQLDB – uživatelé – prod </li><li>SQLDB – uživatelé – dev</li></ul>               |
| Cosmos DB databáze             | Globální             | Cosmos\<název aplikace\>-prostředí \<\>    | <ul><li>Cosmos-navigátor-prod </li><li>Cosmos – emise – dev</li></ul>     |
| Mezipaměť Azure pro instanci Redis | Globální             | redis-\<Název aplikace\>-\<Prostředí\>     | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Databáze MySQL                 | Globální             | mysql-\<Název aplikace\>-\<Prostředí\>     | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Databáze PostgreSQL            | Globální             | psql\<název aplikace\>-prostředí \<\>      | <ul><li>psql-navigátor-prod </li><li>psql – emise – dev</li></ul>         |
| Azure SQL Data Warehouse       | Globální             | sqldw-\<Název aplikace\>-\<Prostředí\>     | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database    | Azure SQL Database | sqlstrdb-\<Název aplikace\>-\<Prostředí\>  | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="example-names-storage"></a>Příklady názvů: Storage

| Typ assetu                        | Rozsah  | Formát                                                                        | Příklady                                                              |
|-----------------------------------|--------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| Účet úložiště (obecné použití)     | Globální | st\<název úložiště\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Účet úložiště (diagnostické protokoly) | Globální | stdiag\<první dvě písmena názvu předplatného a číslo\>\<oblast\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                  | Globální | ssimp\<Název aplikace\>\<Prostředí\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="example-names-ai--machine-learning"></a>Příklady názvů: AI + Machine Learning

| Typ assetu                       | Rozsah          | Formát                            | Příklady                                                          |
|----------------------------------|----------------|-----------------------------------|-------------------------------------------------------------------|
| Azure Cognitive Search           | Globální         | srch-\<Název aplikace\>-\<Prostředí\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services         | Skupina prostředků | ozubeného kola\<název aplikace\>-prostředí \<\>  | <ul><li>ozubeného kola-navigátor-prod </li><li>ozubeného kola – emise – dev</li></ul>   |
| Pracovní prostor služby Azure Machine Learning | Skupina prostředků | MLW\<název aplikace\>-prostředí \<\>  | <ul><li>MLW-navigátor-prod </li><li>MLW – emise – dev</li></ul>   |

### <a name="example-names-analytics-and-iot"></a>Příklady názvů: analýzy a IoT

| Typ assetu                  | Rozsah          | Formát                              | Příklady                                                              |
|-----------------------------|----------------|-------------------------------------|-----------------------------------------------------------------------|
| Azure Data Factory          | Globální         | ADF –\<název aplikace\>\<prostředí\>     | <ul><li>ADF – navigátor – prod </li><li>ADF – emise – vývoj</li></ul>       |
| Azure Stream Analytics      | Skupina prostředků | asa-\<Název aplikace\>-\<Prostředí\>    | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>       |
| Účet Data Lake Analytics | Globální         | dla\<Název aplikace\>\<Prostředí\>      | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>           |
| Účet Data Lake Storage   | Globální         | dls\<Název aplikace\>\<Prostředí\>      | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>           |
| Centrum událostí                   | Globální         | evh-\<Název aplikace\>-\<Prostředí\>    | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>       |
| Cluster HDInsight-HBA   | Globální         | HBA –\<název aplikace\>-prostředí \<\>  | <ul><li>HBA – navigátor – výrobní číslo </li><li>HBA – emise – dev</li></ul>   |
| HDInsight – cluster Hadoop  | Globální         | Název aplikace\<Hadoop\>-prostředí \<\> | <ul><li>Hadoop-navigátor-prod </li><li>emise Hadoop – dev</li></ul> |
| Cluster HDInsight-Spark   | Globální         | Název aplikace Spark-\<\>-prostředí \<\>  | <ul><li>Spark-navigátor-prod </li><li>Spark – emise – dev </li></ul>  |
| IoT Hub                     | Globální         | Název aplikace pro IoT-\<\>-prostředí \<\>    | <ul><li>IoT-navigátor-prod </li><li>IoT – emise – dev</li></ul>       |
| Power BI Embedded           | Globální         | PBI\<název aplikace\>\<prostředí\>     | <ul><li>PBI-navigátor-prod </li><li>PBI – emise – dev</li></ul>       |

### <a name="example-names-integration"></a>Příklady názvů: integrace

| Typ assetu        | Rozsah       | Formát                                                     | Příklady                                                      |
|-------------------|-------------|------------------------------------------------------------|---------------------------------------------------------------|
| Service Bus       | Globální      | sb-\<Název aplikace\>-\<Prostředí\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Service Bus | Service Bus | sbq-\<popisovač dotazu\>                                   | <ul><li>sbq-messagequery</li></ul>                            |
| Téma služby Service Bus | Service Bus | popisovač dotazu SBT\<\>                                   | <ul><li>sbt-messagequery</li></ul>                            |
