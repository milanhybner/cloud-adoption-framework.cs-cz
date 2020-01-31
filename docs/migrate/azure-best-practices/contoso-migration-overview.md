---
title: Přehled příkladů migrace aplikací pro Azure
description: Poskytuje přehled příkladů migrace aplikací zahrnutých jako součást oddílu Architektura přechodu na cloud věnovaného migraci.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c2e0a27e432141feee526d4cb5fe54380fcde583
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807372"
---
# <a name="application-migration-patterns-and-examples"></a>Příklady a vzory migrace aplikací

V této části příručky Architektura přechodu na cloud najdete příklady několika běžných scénářů migrace, které demonstrují, jak se dá místní infrastruktura migrovat do cloudu [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure).

## <a name="introduction"></a>Představení

Azure poskytuje přístup ke komplexní sadě cloudových služeb. Jako vývojáři a IT specialisté můžete pomocí těchto služeb sestavovat, nasazovat a spravovat aplikace s využitím celé řady nástrojů a rozhraní a globální sítě datacenter. Když vaše firma čelí výzvám souvisejícím s digitalizací, cloud Azure vám pomůže zjistit, jak optimalizovat prostředky a operace, zapojit zákazníky i zaměstnance a transformovat vaše produkty.

I přes všechny výhody, které cloud poskytuje z hlediska rychlosti a flexibility, minimalizace nákladů, vysokého výkonu a spolehlivost, si však v Azure uvědomujeme, že řada organizací bude potřebovat ještě nějakou dobu provozovat místní datacentra. V reakci na překážky přechodu do cloudu Azure poskytuje strategii hybridního cloudu, která propojí vaše místní datacentra s veřejným cloudem Azure. Pomocí cloudových prostředků Azure, jako je například služba Azure Backup, můžete zajistit ochranu místních prostředků nebo pomocí analýz Azure získat přehled o místních úlohách.

V rámci strategie hybridního cloudu poskytuje Azure stále větší počet řešení pro migraci místních aplikací a úloh do cloudu. Pomocí jednoduchých postupů můžete komplexně vyhodnotit své místní prostředky, abyste zjistili, jak si povedou v cloudu Azure. Když budete mít k dispozici podrobné posouzení, můžete bez obav migrovat prostředky do Azure. Po zprovoznění prostředků v Azure je můžete optimalizovat, abyste zachovali a vylepšili úroveň přístupu, flexibility, zabezpečení a spolehlivosti.

## <a name="migration-patterns"></a>Vzory migrace

Strategie migrace do cloudu se dají rozdělit do čtyř hlavních vzorů: změna hostování, refaktorování, změna architektury nebo opětovné sestavení. Strategie, kterou použijete, závisí na vašich obchodních faktorech a cílech migrace. Můžete také využít několik vzorů. Můžete se například rozhodnout, že změníte hostitele pro jednoduché aplikace nebo aplikace, které nejsou pro vaši firmu zásadní, ale u aplikací, které jsou složitější nebo slouží pro důležité obchodní informace, změníte architekturu. Podívejme se na tyto vzory blíž.

<!-- markdownlint-disable MD033 -->

**Vzor** | **Definice** | **Kdy ho použít**
--- | --- | ---
**Změna hostitele** | Často se označuje jako migrace _výtahu a posunutí_ . Tato možnost nevyžaduje změny kódu a umožňuje rychlou migraci stávajících aplikací do Azure. Každá aplikace se migruje tak, jak je, s výhodami cloudu a bez rizik a nákladů spojených se změnami kódu. | Když potřebujete rychle přesunout aplikace do cloudu.<br/><br/> Když chcete aplikaci přesunout a neměnit ji.<br/><br/> Když je architektura vašich aplikací navržená tak, aby po dokončení migrace mohly využívat škálovatelnost [Azure IaaS](https://azure.microsoft.com/overview/what-is-iaas).<br/><br/> Když jsou aplikace pro vaši firmu důležité, ale nepotřebujete okamžitě změny jejich funkcí.
**Refaktoring** | Refaktoring, který se často označuje jako „opětovné balení“, vyžaduje v aplikacích minimální změny, aby se mohly připojit [k Azure PaaS](https://azure.microsoft.com/overview/what-is-paas) a používat cloudové nabídky.<br/><br/> Můžete například existující aplikace migrovat do služeb Azure App Service nebo Azure Kubernetes Service (AKS).<br/><br/> Můžete také refaktorovat relační i nerelační databáze do služeb, jako jsou Azure SQL Database Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL nebo Azure Cosmos DB. | Pokud se vaše aplikace dá snadno znovu zabalit pro práci v Azure.<br/><br/> Pokud chcete použít inovativní postupy DevOps, které poskytuje Azure, nebo uvažujete o DevOps s využitím kontejnerové strategie pro úlohy.<br/><br/> V souvislosti s refaktoringem je potřeba uvažovat o přenositelnosti stávajícího základu kódu a dostupnosti dovedností pro vývoj.
**Změna architektury** | Změna architektury pro migraci se zaměřuje na úpravu a rozšíření funkčnosti aplikace a základu kódu s cílem optimalizovat architekturu aplikace pro zajištění cloudové škálovatelnosti.<br/><br/> Můžete například monolitickou aplikaci rozdělit do skupiny mikroslužeb, které fungují dohromady a snadno se škálují.<br/><br/> Nebo můžete změnit architekturu relačních i nerelačních databází na plně spravované databázové řešení, jako je Azure SQL Database Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL nebo Azure Cosmos DB. | Když vaše aplikace potřebuje velké úpravy pro za účelem začlenění nových funkcí nebo zajištění efektivnějšího fungování na cloudové platformě.<br/><br/> Pokud chcete využít stávající investice do aplikací, splnit požadavky na škálovatelnost, využít inovativní postupy Azure DevOps a minimalizovat použití virtuálních počítačů.
**Opětovné sestavení** | Opětovné sestavení jde ještě o krok dál a aplikaci znovu sestaví od začátku pomocí cloudových technologií Azure.<br/><br/> Můžete například sestavit úplně nové aplikace s využitím technologií [nativních pro cloud](https://azure.com/cloudnative), jako jsou Azure Functions, Azure AI, Spravovaná instance Azure SQL Database nebo Azure Cosmos DB. | Když chcete zajistit rychlý vývoj a vaše stávající aplikace mají omezené funkce a životnost.<br/><br/> Až budete připravení urychlit obchodní inovace (včetně postupů DevOps, které poskytuje Azure), sestavte nové aplikace pomocí technologií nativních pro cloud a využijte pokroky v oblasti AI, blockchainů a IoT.

<!-- markdownlint-enable MD033 -->

## <a name="migration-example-articles"></a>Články s příklady migrace

Články v této části obsahují příklady několika běžných scénářů migrace. Každý z těchto příkladů zahrnuje základní informace a podrobné scénáře nasazení, které ilustrují způsob nastavení infrastruktury migrace a vyhodnocení vhodnosti místních prostředků pro migraci. Postupně budeme do této části přidávat další články.

![Běžné projekty migrace/modernizace](./media/migration-patterns.png)

*Kategorie běžných projektů migrace a modernizace*

Články z této série jsou shrnuty níž.

- Každý scénář migrace je založený na trochu jiných obchodních cílech, které určují migrační strategii.
- Pro každý scénář nasazení poskytujeme informace o obchodních aspektech a cílech, navrženou architekturu, kroky pro realizaci migrace, doporučení pro vyčištění a další kroky po dokončení migrace.

### <a name="assessment"></a>Posouzení

**Článek** | **Podrobnosti**
--- | ---
[Posouzení vhodnosti místních prostředků k migraci do Azure](./contoso-migration-assessment.md) | Tento článek ukazuje, jak spustit posouzení místní aplikace běžící na VMware. V příkladu vzorová organizace posuzuje virtuální počítače aplikace pomocí služby Azure Migrate a databázi SQL Serveru aplikace pomocí Data Migration Assistanta.

### <a name="infrastructure"></a>Infrastruktura

**Článek** | **Podrobnosti**
--- | ---
[Nasazení infrastruktury Azure](./contoso-migration-infrastructure.md) | V tomto článku se dozvíte, jak organizace může připravit svoji místní infrastrukturu a infrastrukturu Azure pro migraci. Na příklad infrastruktury zavedený v tomto článku odkazují další ukázky uvedené v této části.

### <a name="windows-server-workloads"></a>Úlohy Windows Serveru

**Článek** | **Podrobnosti**
--- | ---
[Změna hostitele aplikace na virtuální počítače Azure](./contoso-migration-rehost-vm.md) | V tomto článku najdete příklad migrace místních virtuálních počítačů aplikace do virtuálních počítačů Azure pomocí služby Site Recovery.
[Změna architektury aplikace na kontejnery Azure a služby Azure SQL Database](./contoso-migration-rearchitect-container-sql.md) | Tento článek přináší příklad migrace aplikace při změně architektury webové vrstvy aplikace na kontejner Windows spuštěný ve službě Azure Service Fabric a databáze s využitím Azure SQL Database.

### <a name="linux-workloads"></a>Linuxové úlohy

**Článek** | **Podrobnosti**
--- | ---
[Změna hostitele linuxové aplikace na virtuální počítače Azure a Azure Database for MySQL](./contoso-migration-rehost-linux-vm-mysql.md) | Tento článek přináší příklad migrace aplikace hostované na Linuxu na virtuální počítače Azure pomocí Site Recovery. Migruje databázi aplikace do služby Azure Database for MySQL pomocí MySQL Workbenche.
[Změna hostitele linuxové aplikace na virtuální počítače Azure](./contoso-migration-rehost-linux-vm.md) | Tento příklad ukazuje, jak dokončit migraci aplikace založené na systému Linux a Shift do virtuálních počítačů Azure pomocí služby Site Recovery.

### <a name="sql-server-workloads"></a>Úlohy SQL Serveru

**Článek** | **Podrobnosti**
--- | ---
[Změna hostitele aplikace na virtuální počítač Azure a spravovanou instanci Azure SQL Database](./contoso-migration-rehost-vm-sql-managed-instance.md) | V tomto článku najdete příklad migrace typu výtah a Shift do Azure pro místní aplikaci. Zahrnuje migraci virtuálního počítače front-endu aplikace pomocí služby [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) a migraci databáze aplikace do spravované instance Azure SQL Database s využitím [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).
[Změna hostitele aplikace na virtuální počítače Azure a skupiny dostupnosti AlwaysOn pro SQL Server](./contoso-migration-rehost-vm-sql-ag.md) | Tento příklad ukazuje, jak migrovat aplikaci a data pomocí virtuálních počítačů s SQL Serverem hostovaných v Azure. K migraci virtuálních počítačů aplikace používá Site Recovery a k migraci databáze aplikace do clusteru SQL Server, který je chráněný skupinou dostupnosti Always On, používá službu Azure Database Migration Service.

### <a name="aspnet-php-and-java-apps"></a>Aplikace ASP.NET, PHP a Java

**Článek** | **Podrobnosti**
--- | ---
[Refaktoring aplikace do webové aplikace Azure a Azure SQL Database](./contoso-migration-refactor-web-app-sql.md) | Tento příklad ukazuje, jak migrovat místní aplikaci založenou na Windows do webové aplikace Azure, a databázi aplikace migruje do instance Azure SQL Serveru pomocí Data Migration Assistanta.
[Refaktoring linuxové aplikace do více oblastí pomocí služeb Azure App Service, Azure Traffic Manager a Azure Database for MySQL](./contoso-migration-refactor-linux-app-service-mysql.md) | Tento příklad ukazuje, jak místní linuxovou aplikaci migrovat do webové aplikace Azure ve více oblastech Azure pomocí Azure Traffic Manageru integrovaného s GitHubem pro průběžné doručování. Databáze aplikace se migruje do instance Azure Database for MySQL.
[Opětovné sestavení aplikace v Azure](./contoso-migration-rebuild.md) | Tento článek obsahuje příklad opětovného sestavení místní aplikace pomocí celé řady spravovaných služeb a funkcí Azure, včetně Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services a Azure Cosmos DB.
[Refaktoring Team Foundation Serveru do sady Azure DevOps Services](./contoso-migration-tfs-vsts.md) | Tento článek ukazuje příklad migrace místního nasazení Team Foundation Serveru do Azure DevOps Services v Azure.

### <a name="migration-scaling"></a>Škálování migrace

**Článek** | **Podrobnosti**
--- | ---
[Škálování migrace do Azure](./contoso-migration-scale.md) | Tento článek popisuje, jak se ukázková organizace připravuje na škálování kompletní migrace do Azure.

### <a name="demo-apps"></a>Ukázkové aplikace

V ukázkových článcích uvedených v této části se používají dvě ukázkové aplikace: SmartHotel360 a osTicket.

- **SmartHotel360:** Tato aplikace byla vyvinutá Microsoftem jako testovací aplikace, kterou můžete použít při práci s Azure. Je k dispozici jako open source a můžete si ji stáhnout z [GitHubu](https://github.com/Microsoft/SmartHotel360). Jde o aplikaci v ASP.NET připojenou k databázi SQL Serveru. Ve scénářích probíraných v těchto článcích je aktuální verze této aplikace nasazená na dvou virtuálních počítačích VMware, na kterých běží Windows Server 2008 R2 a SQL Server 2008 R2. Tyto virtuální počítače aplikace jsou hostované v místním prostředí a spravuje je vCenter Server.
- **osTicket:** Otevřená aplikace pro vytváření lístků ve zdrojové službě, která běží na Linux. Můžete si ji stáhnout z [GitHubu](https://github.com/osTicket/osTicket). Ve scénářích probíraných v těchto článcích je aktuální verze této aplikace nasazená v místním prostředí na dvou virtuálních počítačích VMware, na kterých běží Ubuntu 16.04 LTS, a to s využitím Apache 2, PHP 7.0 a MySQL 5.7
