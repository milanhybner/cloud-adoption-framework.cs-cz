---
title: 'Připraveno: Doporučené konvence pojmenování a označování'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: V tomto článku najdete podrobná doporučení týkající se tvorby názvů a značek prostředků, která jsou konkrétně zaměřena na podporu snah o přijetí podnikového cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: 9caeca52ba0ab3a909b0f42ac6f016d44033a4ee
ms.sourcegitcommit: 617c3f12a3657a8a1393fd08d261dd98eb81b65c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2019
ms.locfileid: "74086802"
---
# <a name="ready-recommended-naming-and-tagging-conventions"></a>Připraveno: Doporučené konvence pojmenování a označování

Uspořádání cloudových prostředků tak, aby pomáhaly provozní správě a podporovaly požadavky na účtování, představuje častou výzvu, se kterou se při snahách o přijetí cloudu můžete setkat. Když se na prostředky hostované v cloudu použijí správně definované konvence pro tvorbu názvů a značek metadat, mohou IT pracovníci prostředky rychle vyhledat a spravovat. Správně definované názvy a značky také usnadňují obchodním týmům nastavit náklady na využití cloudu prostřednictvím mechanismů vrácení peněz a účtování metodou showback.

[Pravidla a omezení pro pojmenování cetrum architektury Azure pro prostředky Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) poskytují obecná doporučení a omezení platforem. Následující diskuze tyto obecné pokyny rozšiřuje o podrobnější doporučení zaměřená zejména na podporu snah o přijetí podnikového cloudu.

Názvy prostředků může být obtížné změnit. Než zahájíte jakékoli větší nasazení cloudu, nastavte týmům pro přijetí cloudu prioritu, kterou je vytvoření ucelené konvence pro tvorbu názvů.

> [!NOTE]
> Každá společnost má jiné požadavky na organizaci a správu. Doporučení v tomto článku slouží jako výchozí bod pro diskuze v týmech pro přijetí cloudu.
>
> Během těchto diskuzí můžete použít následující šablonu, kam můžete zapisovat rozhodnutí ohledně názvů a značek, která jsou výsledkem srovnání těchto doporučení a vašich konkrétních obchodních potřeb.
>
> Stáhněte si [šablonu pro sledování konvencí pro tvorbu názvů a značek](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Pojmenovávání a označování prostředků

Strategie pro vytváření názvů a značek zahrnuje firemní a provozní údaje jako součásti názvů prostředků a značek metadat:

- Firemní údaje v této strategii zajišťují, aby názvy a značky prostředků obsahovaly informace organizace, které jsou potřeba k identifikaci týmů. Použijte prostředek společně s vlastníky, kteří zodpovídají za náklady na prostředky.
- Provozní údaje zajišťují, aby názvy a značky obsahovaly informace, které IT týmy používají k identifikaci úloh, aplikací, prostředí, závažností a dalších informací užitečných pro správu prostředků.

### <a name="resource-naming"></a>Pojmenovávání prostředků

Efektivní konvence pro tvorbu názvů sestavuje názvy prostředků tak, že jako části názvu prostředku používá důležité údaje o prostředku. Například pomocí doporučených konvencí pro tvorbu názvů [popsaných dále v tomto článku](#sample-naming-convention) je prostředek veřejné IP adresy pro produkční úlohu SharePointu pojmenovaný takto: `pip-sharepoint-prod-westus-001`.

Takový název vám umožní rychle identifikovat typ prostředku, jeho přidruženou úlohu, prostředí nasazení a oblast Azure, která ho hostuje.

#### <a name="naming-scope"></a>Obor názvů

Všechny typy prostředků Azure mají obor, který definuje úroveň, kterou názvy prostředků musí být jedinečné. Prostředek musí mít jedinečný název v rámci svého oboru.

Virtuální síť má například obor skupiny prostředků, což znamená, že v dané skupině prostředků může být jenom jedna síť s názvem `vnet-prod-westus-001`. Jiné skupiny prostředků ale můžou mít svou vlastní virtuální síť s názvem `vnet-prod-westus-001`. Podsítě, abychom uvedli další příklad, mají obory v rámci virtuálních sítí, což znamená, že každá podsíť ve virtuální síti musí mít jedinečný název.

Některé názvy prostředků, jako jsou služby PaaS s veřejnými koncovými body nebo názvy DNS virtuálního počítače, mají globální obory, což znamená, že musí být jedinečné napříč celou platformou Azure.

Délka názvů prostředků je omezená. Důležité je, abyste při vývoji konvencí pro tvorbu názvů vyvážili kontext vložený v názvu s jeho oborem a délkou názvu. Další informace o pravidlech tvorby názvů týkajících se povolených znaků, oborů a délek názvů pro typy prostředků najdete v tématu [Zásady vytváření názvů pro prostředky Azure](/azure/architecture/best-practices/resource-naming).

#### <a name="recommended-naming-components"></a>Doporučené komponenty názvů

Při vytváření konvence pro tvorbu názvů identifikujte klíčové části informace, které chcete aby název prostředku odrážel. Pro různé typy prostředků jsou relevantní různé informace. Následující seznam uvádí příklady informací, které jsou při vytváření názvů prostředků užitečné.

Snažte se, aby byly komponenty názvu krátké a předešli jste tak překročení omezení délky názvu prostředku.

| Komponenta názvu | Popis | Příklady |
| --- | --- | --- |
| Obchodní jednotka | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni V menších organizacích může tato komponenta představovat jeden organizační prvek nejvyšší úrovně. | *fin*, *mktg*, *product*, *it*, *corp* |
| Typ předplatného | Souhrnný popis účelu předplatného obsahujícího prostředek Často se dělí podle typu prostředí nasazení nebo konkrétních úloh. | *prod,* s*hared, client* |
| Název aplikace nebo služby | Název aplikace, úlohy nebo služby, do které prostředek patří | *navigator*, *emissions*, *sharepoint*, *hadoop* |
| Prostředí nasazení | Fáze životního cyklu vývoje pro úlohu, kterou prostředek podporuje | *prod, dev, qa, stage, test* |
| Oblast | Oblast Azure, ve které je prostředek nasazen | *westus, eastus2, westeurope, usgovia* |

#### <a name="recommended-resource-type-prefixes"></a>Doporučené předpony typu prostředku

Každá úloha se může skládat z mnoha jednotlivých prostředků a služeb. Zahrnutí předpon typu prostředku do názvů prostředků usnadňuje vizuální identifikaci komponent aplikace nebo služby.

Následující seznam obsahuje doporučené předpony typů prostředků Azure, které se mají používat při definování konvencí pro tvorbu názvů.

| Typ prostředku                       | Předpona názvu prostředku |
| ----------------------------------- | -------------------- |
| Skupina prostředků                      | rg-                  |
| Azure Virtual Network               | vnet-                |
| Brána virtuální sítě             | vnet-gw-             |
| Připojení brány                  | cn-                  |
| Podsíť                              | snet-                |
| Skupina zabezpečení sítě              | nsg-                 |
| Tabulka směrování                         | cestě               |
| Azure Virtual Machines              | vm-                  |
| Účet úložiště virtuálního počítače                  | stvm                 |
| Veřejná IP adresa                           | pip-                 |
| Nástroj pro vyrovnávání zatížení Azure                 | lb-                  |
| NIC                                 | nic-                 |
| Azure Key Vault                     | elektrické                  |
| Azure Kubernetes Service            | AKS                 |
| Azure Service Bus                   | sb-                  |
| Fronty Azure Service Bus            | sbq-                 |
| Aplikace služby Azure App Service              | azapp-               |
| Aplikace Azure Functions                | azfun-               |
| Azure Cloud Services                | azcs-                |
| Azure SQL Database                  | sqldb-               |
| Azure Cosmos DB (dříve Azure DocumentDB) | cosdb-               |
| Azure Cache for Redis               | redis-               |
| Azure Database for MySQL            | mysql-               |
| Azure SQL Data Warehouse            | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Azure Storage                       | stor                 |
| Azure StorSimple                    | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services            | cs-                  |
| Pracovní prostor služby Azure Machine Learning    | aml-                 |
| Azure Data Lake Storage             | dls                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight – Spark             | hdis-                |
| Azure HDInsight – Hadoop            | hdihd-               |
| Azure HDInsight – R Server          | hdir-                |
| Azure HDInsight – HBase             | hdihb-               |
| Power BI Embedded                   | pbiemb               |
| Azure Stream Analytics              | asa-                 |
| Azure Data Factory                  | df-                  |
| Azure Event Hubs                    | evh-                 |
| Azure IoT Hub                       | aih-                 |
| Azure Notification Hubs             | anh-                 |
| Obor názvů Azure Notification Hubs   | anhns-               |

### <a name="metadata-tags"></a>Značky metadat

Když použijete značky metadat na cloudové prostředky, můžete zahrnout informace o těch prostředcích, které nemohly být do názvu prostředku zahrnuty. Tyto informace můžete použít k propracovanějšímu filtrování prostředků a vytváření sestav o prostředcích. Tyto značky by měly obsahovat kontext týkající se úlohy nebo aplikace přiřazené k prostředku, provozních požadavků a informací o vlastnictví. Informace pak můžou využít IT týmy nebo obchodní týmy k vyhledání prostředků nebo k vygenerování sestav týkajících se využití prostředků a fakturace.

To, jaké značky se u prostředků používají a jaké značky jsou povinné nebo volitelné, se u jednotlivých organizací liší. Následující seznam uvádí příklady běžných značek, které obsahují důležitý kontext a informace o prostředku. Tento seznam slouží jako výchozí bod pro vytvoření vlastní konvence pro tvorbu značek.

| Název značky                  | Popis                                                                                                                                                                                                    | Klíč               | Příklad hodnoty                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Název aplikace          | Název aplikace, služby nebo úlohy, které je prostředek přidružen                                                                                                                                 | *NázevAplikace* | *{název aplikace}*                                    |
| Jméno schvalovatele             | Osoba odpovědná za schvalování nákladů souvisejících s tímto prostředkem                                                                                                                                               | *Schvalovatel*        | *{e-mail}*                                       |
| Požadovaný/schválený rozpočet  | Peníze přidělené pro tuto aplikaci, službu nebo úlohu                                                                                                                                                    | *VelikostRozpočtu*    | *{\$}*                                          |
| Obchodní jednotka             | Rozdělení vaší společnosti vlastnící předplatné nebo úlohu, do které prostředek patří, na nejvyšší úrovni V menších organizacích může tato značka představovat jeden organizační prvek nebo sdílený organizační prvek nejvyšší úrovně. | *ObchodníJednotka*    | *FINANCE, MARKETING,{Název produktu}, CORP, SHARED* |
| Nákladové středisko               | Účetní nákladové středisko přidružené tomuto prostředku                                                                                                                                                          | *NákladovéStředisko*      | *{číslo}*                                      |
| Zotavení po havárii         | Obchodní důležitost aplikace, úlohy nebo služby                                                                                                                                                | *DR*              | *Mission-critical, Critical, Essential*         |
| Koncové datum projektu   | Datum naplánovaného vyřazení aplikace, úlohy nebo služby z provozu                                                                                                                                  | *KoncovéDatum*         | *{datum}*                                        |
| Prostředí               | Prostředí nasazení aplikace, úlohy nebo služby                                                                                                                                              | *Prostředí*             | *Prod, Dev, QA, Stage, Test*                    |
| Jméno vlastníka                | Vlastník aplikace, úlohy nebo služby                                                                                                                                                                | *Vlastník*           | *{e-mail}*                                       |
| Jméno žadatele            | Uživatel, který požádal o vytvoření této aplikace                                                                                                                                                          | *Žadatel*       | *{e-mail}*                                       |
| Třída služby             | Úroveň smlouvy o úrovni služeb aplikace, úlohy nebo služby                                                                                                                                       | *TřídaSlužby*    | *Dev, Bronze, Silver, Gold*                     |
| Počáteční datum projektu | Datum prvního nasazení aplikace, úlohy nebo služby                                                                                                                                           | *PočátečníDatum*       | *{datum}*                                        |

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
| Virtuální brána virtuální sítě     | Virtuální síť | vnet-gw-v-\<Typ předplatného\>-\<Oblast\>-\<\#\#\#\>                 | <ul><li>vnet-gw-v-shared-eastus2-001 </li><li>vnet-gw-v-prod-westus-001 </li><li>vnet-gw-v-client-eastus2-001</li></ul>                   |
| Místní brána virtuální sítě       | Virtuální brána | vnet-gw-l-\<Typ předplatného\>-\<Oblast\>-\<\#\#\#\>                 | <ul><li>vnet-gw-l-shared-eastus2-001 </li><li>vnet-gw-l-prod-westus-001 </li><li>vnet-gw-l-client-eastus2-001</li></ul>                   |
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
| Nástroj pro vyrovnávání zatížení Azure      | Skupina prostředků | lb-\<název aplikace nebo role\>\<Prostředí\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| NIC                | Skupina prostředků | nic-\<\#\#\>-\<název virtuálního počítače\>-\<předplatné\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>Služby PaaS

| Typ assetu     | Rozsah  | Formát                                                              | Příklady                                                                                 |
|----------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure App Service    | Globální | azapp-\<Název aplikace\>-\<Prostředí\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azapp-navigator-prod-001.azurewebsites.net </li><li>azapp-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Aplikace Azure Functions   | Globální | azfun-\<Název aplikace\>-\<Prostředí\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azfun-navigator-prod-001.azurewebsites.net </li><li>azfun-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Globální | azcs-\<Název aplikace\>-\<Prostředí\>-\<\#\#\#\>.[{cloudapp.net}]       | <ul><li>azcs-navigator-prod-001.azurewebsites.net </li><li>azcs-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Typ assetu         | Rozsah       | Formát                                                     | Příklady                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Globální      | sb-\<Název aplikace\>-\<Prostředí\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Fronty Azure Service Bus | Service Bus | sbq-\<popisovač dotazu\>                                   | <ul><li>sbq-messagequery</li></ul>                   |

### <a name="databases"></a>Databáze

| Typ assetu                          | Rozsah              | Formát                                | Příklady                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Azure SQL Database                  | Globální             | sqldb-\<Název aplikace\>-\<Prostředí\>    | <ul><li>sqldb-navigator-prod </li><li>sqldb-emissions-dev</li></ul>       |
| Azure Cosmos DB (dříve DocumentDB) | Globální             | cosdb-\<Název aplikace\>-\<Prostředí\>    | <ul><li>cosdb-navigator-prod </li><li>cosdb-emissions-dev</li></ul>       |
| Azure Cache for Redis               | Globální             | redis-\<Název aplikace\>-\<Prostředí\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Globální             | mysql-\<Název aplikace\>-\<Prostředí\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure SQL Data Warehouse                  | Globální             | sqldw-\<Název aplikace\>-\<Prostředí\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Azure SQL Database | sqlstrdb-\<Název aplikace\>-\<Prostředí\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Úložiště

| Typ assetu                              | Rozsah  | Formát                                                                        | Příklady                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Účet služby Azure Storage – obecné použití     | Globální | st\<název úložiště\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Účet služby Azure Storage – diagnostické protokoly | Globální | stdiag\<první dvě písmena názvu předplatného a číslo\>\<oblast\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                              | Globální | ssimp\<Název aplikace\>\<Prostředí\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>AI a Machine Learning

| Typ assetu                       | Rozsah          | Formát                            | Příklady                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Globální         | srch-\<Název aplikace\>-\<Prostředí\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services               | Skupina prostředků | cs-\<Název aplikace\>-\<Prostředí\>   | <ul><li>cs-navigator-prod </li><li>cs-emissions-dev</li></ul>     |
| Pracovní prostor služby Azure Machine Learning | Skupina prostředků | aml-\<Název aplikace\>-\<Prostředí\>  | <ul><li>aml-navigator-prod </li><li>aml-emissions-dev</li></ul>   |

### <a name="analytics"></a>Analýzy

| Typ assetu                | Rozsah  | Formát                             | Příklady                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Globální | df-\<Název aplikace\>\<Prostředí\>     | <ul><li>df-navigator-prod </li><li>df-emissions-dev</li></ul>       |
| Azure Data Lake Storage   | Globální | dls\<Název aplikace\>\<Prostředí\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Azure Data Lake Analytics | Globální | dla\<Název aplikace\>\<Prostředí\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight – Spark         | Globální | hdis-\<Název aplikace\>-\<Prostředí\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight – Hadoop        | Globální | hdihd-\<Název aplikace\>-\<Prostředí\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight – R Server      | Globální | hdir-\<Název aplikace\>-\<Prostředí\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight – HBase         | Globální | hdihb-\<Název aplikace\>-\<Prostředí\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Power BI Embedded         | Globální | pbiemb\<Název aplikace\>\<Prostředí\>  | <ul><li>pbiem-navigator-prod </li><li>pbiem-emissions-dev</li></ul> |

### <a name="internet-of-things-iot"></a>Internet věcí (IoT)

| Typ assetu                         | Rozsah          | Formát                             | Příklady                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics na hraničních zařízeních IoT | Skupina prostředků | asa-\<Název aplikace\>-\<Prostředí\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Globální         | aih-\<Název aplikace\>-\<Prostředí\>   | <ul><li>aih-navigator-prod </li><li>aih-emissions-dev</li></ul>     |
| Azure Event Hubs                          | Globální         | evh-\<Název aplikace\>-\<Prostředí\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs                   | Skupina prostředků | anh-\<Název aplikace\>-\<Prostředí\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Obor názvů Azure Notification Hubs         | Globální         | anhns-\<Název aplikace\>-\<Prostředí\> | <ul><li>anhns-navigator-prod </li><li>anhns-emissions-dev</li></ul> |
