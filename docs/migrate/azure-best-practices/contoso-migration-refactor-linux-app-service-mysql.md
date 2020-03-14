---
title: Refaktorování aplikace pro Linux do Azure App Service a databáze pro MySQL
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak refaktorovat aplikaci pro Linux Service Desk, aby Azure App Service a Azure Database for MySQL.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3a4ebcb2264ff863200071363b8369d8a76549d3
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311485"
---
# <a name="refactor-a-linux-app-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Refaktoring linuxové aplikace do více oblastí pomocí služeb Azure App Service, Traffic Manager a Azure Database for MySQL

V tomto článku se dozvíte, jak fiktivní firma Contoso refaktoruje dvouvrstvou linuxovou aplikaci Apache MySQL PHP (LAMP) tím, že ji migruje z místního prostředí do Azure pomocí Azure App Service s integrací GitHubu a Azure Database for MySQL.

Aplikace technické podpory osTicket používaná v tomto příkladu je poskytována jako open source. Pokud ji chcete použít pro vlastní testovací účely, můžete si ji stáhnout z [GitHubu](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Obchodní faktory

Tým vedení IT těsně spolupracoval s obchodními partnery, aby zjistil, čeho chtějí dosáhnout:

- **Řešení obchodního růstu.** Firma Contoso roste a přesouvá se na nové trhy. Potřebuje další agenty zákaznických služeb.
- **Škálování** Toto řešení by mělo být vytvořené tak, aby firma Contoso mohla s rozvojem podnikání přidávat další agenty zákaznických služeb.
- **Zvýšení odolnosti.**  V minulosti ovlivňovaly problémy se systémem jen interní uživatele. U nového obchodního modelu budou ovlivněni externí uživatelé a Contoso potřebuje, aby tato aplikace byla neustále provozuschopná.

## <a name="migration-goals"></a>Cíle migrace

Cloudový tým Contoso vytyčil cíle pro tuto migraci, aby bylo možné určit nejlepší způsob migrace:

- Aplikace by se měla škálovat nad rámec aktuální místní kapacity a výkonu. Firma Contoso aplikaci přesouvá, aby v Azure využila výhod škálování na vyžádání.
- Contoso chce základ kódu aplikace přesunout do kanálu průběžného doručování. Při sdílení změn aplikace do GitHubu chce Contoso tyto změny nasazovat bez úkolování provozního personálu.
- Aplikace musí být odolná a schopná růstu a převzetí služeb při selhání. Contoso chce aplikaci nasadit do dvou různých oblastí Azure a nastavit u ní automatické škálování.
- Po přesunu aplikace do cloudu chce Contoso minimalizovat úlohy správce databáze.

## <a name="solution-design"></a>Návrh řešení

Po vytyčení cílů a požadavků Contoso navrhne a zkontroluje řešení nasazení a identifikuje proces migrace včetně služeb Azure, které se k migraci využijí.

## <a name="current-architecture"></a>Současná architektura

- Aplikace je rozložená na dva virtuální počítače (OSTICKETWEB a OSTICKETMYSQL).
- Tyto virtuální počítače jsou umístěné na hostiteli VMware ESXi **contosohost1.contoso.com** (verze 6.5).
- Správu prostředí VMware zajišťuje vCenter Server 6.5 (**vcenter.contoso.com**) provozovaný na virtuálním počítači.
- Společnost Contoso má místní datacentrum (contoso-datacenter) s místním řadičem domény (**contosodc1**).

![Současná architektura](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Navrhovaná architektura

Zde je navrhovaná architektura:

- Aplikace webové vrstvy na počítači OSTICKETWEB bude migrována vytvořením Azure App Service ve dvou oblastech Azure. Azure App Service pro Linux se bude implementovat pomocí kontejneru Dockeru PHP 7.0.
- Kód aplikace se přesune do GitHubu a u webové aplikace Azure App Service bude nakonfigurováno průběžné doručování pomocí GitHubu.
- Aplikační servery Azure budou nasazeny jak v primární oblasti (USA – východ 2), tak v sekundární oblasti (USA – střed).
- V obou oblastech bude před těmito dvěma webovými aplikacemi nastaven Traffic Manager.
- Traffic Manager bude nakonfigurován v režimu priority a vynucovat provoz přes USA – východ 2.
- Pokud je Azure App Server v oblasti USA – východ 2 offline, mohou uživatelé získat přístup k aplikaci v oblasti USA – střed, která převzala služby.
- Databáze aplikace bude do služby Azure Database for MySQL migrována pomocí nástrojů MySQL Workbench. Místní databáze bude zálohována místně a obnovena přímo do Azure Database for MySQL.
- Tato databáze se bude nacházet v primární oblasti USA – východ 2 v databázové podsíti (PROD-DB-EUS2) v produkční síti (VNET-PROD-EUS2):
- Protože se migruje produkční úloha, budou se prostředky Azure nacházet v produkční skupině prostředků **ContosoRG**.
- Prostředek Traffic Manager bude nasazen ve skupině prostředků infrastruktury Contoso **ContosoInfraRG**.
- Po dokončení migrace se místní virtuální počítače v datacentru Contoso vyřadí z provozu.

![Architektura scénáře](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Proces migrace

Contoso dokončí proces migrace následujícím způsobem:

1. V prvním kroku správci Contoso nastaví infrastrukturu Azure včetně zřízení Azure App Service, nastavení Traffic Manageru a zřízení instance Azure Database for MySQL.
2. Po přípravě Azure migrují databázi nástrojem MySQL Workbench.
3. Po spuštění databáze v Azure vytvoří privátní úložiště GitHubu pro Azure App Service s průběžným doručováním a načtou do něho aplikaci osTicket.
4. Na webu Azure Portal načtou aplikaci z GitHubu do kontejneru Dockeru, ve kterém běží Azure App Service.
5. Upraví nastavení DNS a nakonfigurují u aplikace automatické škálování.

![Proces migrace](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Služby Azure

**Služba** | **Popis** | **Náklady**
--- | --- | ---
[Azure App Service](https://azure.microsoft.com/services/app-service) | Služba běží a škáluje aplikace pomocí služby Azure PaaS pro weby. | Cena vychází z velikosti instancí a potřebných funkcí. [Další informace](https://azure.microsoft.com/pricing/details/app-service/windows).
[Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | Nástroj pro vyrovnávání zatížení, který pomocí DNS směruje uživatele do Azure nebo na externí weby a služby. | Cena vychází z počtu přijatých dotazů DNS a počtu monitorovaných koncových bodů. | [Další informace](https://azure.microsoft.com/pricing/details/traffic-manager).
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Tato databáze je založená na opensourcovém stroji MySQL Server. Poskytuje plně spravovanou podnikovou komunitní databázi MySQL jako službu pro vývoj a nasazení aplikací. | Cena vychází z požadavků na výpočetní výkon, úložiště a zálohování. [Další informace](https://azure.microsoft.com/pricing/details/mysql).

## <a name="prerequisites"></a>Předpoklady

Zde zjistíte, co Contoso potřebuje k realizaci tohoto scénáře.

<!-- markdownlint-disable MD033 -->

**Požadavky** | **Podrobnosti**
--- | ---
**Předplatné Azure** | Firma Contoso vytvořila předplatná v dřívějším článku v této sérii. Pokud ještě nemáte předplatné Azure, vytvořte si [bezplatný účet](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Pokud vytvoříte bezplatný účet, jste správcem vašeho předplatného a můžete provádět všechny akce.<br/><br/> Pokud používáte existující předplatné a nejste správcem, musíte správce požádat, aby vám udělil oprávnění Vlastník nebo Přispěvatel.
**Infrastruktura Azure** | Společnost Contoso nastaví svoji infrastrukturu Azure podle popisu v článku [Infrastruktura Azure pro migraci](./contoso-migration-infrastructure.md).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Kroky scénáře

Contoso dokončí migraci tímto způsobem:

> [!div class="checklist"]
>
> - **Krok 1: zřízení Azure App Service.** Správci Contoso zřídí webové aplikace v primární a sekundární oblasti.
> - **Krok 2: nastavte Traffic Manager.** Nastaví Traffic Manager před webovými aplikacemi pro účely směrování provozu a vyrovnávání zatížení.
> - **Krok 3: zřízení MySQL** V Azure zřídí instanci Azure Database for MySQL.
> - **Krok 4: migrace databáze** Migrují databázi nástrojem MySQL Workbench.
> - **Krok 5: nastavení GitHubu.** Nastaví místní úložiště GitHubu pro weby a kód aplikace.
> - **Krok 6: nasaďte webové aplikace.** Nasadí webové aplikace z GitHubu.

## <a name="step-1-provision-azure-app-service"></a>Krok 1: zřízení Azure App Service

Správci Contoso zřídí dvě webové aplikace (jednu v každé oblasti) využívající Azure App Service.

1. Z Azure Marketplace vytvoří prostředek webové aplikace v primární oblasti USA – východ 2 (**osticket-eus2**).
2. Tento prostředek umístí do produkční skupiny prostředků **ContosoRG**.

    ![Aplikace Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. Vytvoří nový plán služby App Service v primární oblasti (**APP-SVP-EUS2**) s využitím standardní velikosti.

     ![Aplikace Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Vyberou sadu operačního systému Linux s PHP 7.0, což je kontejner Dockeru.

    ![Aplikace Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Vytvoří druhou webovou aplikaci (**osticket-cus**) a plán služby Azure App Service pro oblast USA – střed.

    ![Aplikace Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Potřebujete další pomoc?**

- Seznamte se s [webovými aplikacemi Azure App Service](https://docs.microsoft.com/azure/app-service/overview).
- Seznamte se se službou [Azure App Service v Linuxu](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Krok 2: nastavení Traffic Manager

Správci Contoso nastaví Traffic Manager tak, aby příchozí webové žádosti byly směrovány na webové aplikace běžící na webové vrstvě osTicket.

1. Vytvoří prostředek Traffic Manager (**osticket.trafficmanager.net**) z Azure Marketplace. Použijí prioritní směrování tak, aby USA – východ 2 bylo primární lokalitou. Umístí tento prostředek do skupiny prostředků infrastruktury (**ContosoInfraRG**). Traffic Manager je globální a není vázaný na konkrétní umístění.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Nyní u Traffic Manageru nakonfigurují koncové body. Přidají webovou aplikaci USA – východ 2 jako primární lokalitu (**osticket-eus2**) a aplikaci USA – střed jako sekundární (**osticket-cus**).

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. Po přidání mohou koncové body monitorovat.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Potřebujete další pomoc?**

- Seznamte se s [Traffic Managerem](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Seznamte se se [směrováním provozu do prioritního koncového bodu](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Krok 3: zřízení Azure Database for MySQL

Správci Contoso zřídí v primární oblasti USA – východ 2 instanci databáze MySQL.

1. Na webu Azure Portal vytvoří prostředek Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Přidají k databázi Azure název **contosoosticket**. Přidají tuto databázi do produkční skupiny prostředků **ContosoRG** a zadají pro ni přihlašovací údaje.
3. Místní databáze MySQL je verze 5.7, takže tuto verzi vyberou pro zajištění kompatibility. Použijí výchozí velikosti, které odpovídají jejich požadavkům na databázi.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. Jako **Možnosti redundance zálohy** vyberou **Geograficky redundantní**. Tato možnost jim v případě výpadku umožňuje obnovit databázi v sekundární oblasti USA – střed. Tuto možnost mohou nakonfigurovat jenom při zřizování databáze.

    ![Redundance](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Nastaví zabezpečení připojení. V databázi > **Zabezpečení připojení** nastaví pravidla firewallu, která umožní databázi přistupovat ke službám Azure.

6. Do počátečních a koncových IP adres přidají místní IP adresu klienta pracovní stanice. Webovým aplikacím a klientovi databáze, který provádí migraci, to umožní získat přístup k databázi MySQL.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Krok 4: migrace databáze

Správci Contoso migrují databázi pomocí zálohování a obnovení s využitím nástrojů MySQL. Nainstalují MySQL Workbench, zálohují databázi z počítače OSTICKETMYSQL a pak ji obnoví na server Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Instalace aplikace MySQL Workbench

1. Zkontrolují [předpoklady a stáhnou MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Nainstalují MySQL Workbench pro Windows podle [pokynů k instalaci](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Počítač, na který tento nástroj instalují, musí být přístupný virtuálnímu počítači OSTICKETMYSQL a Azure přes internet.
3. V nástroji MySQL Workbench vytvoří připojení MySQL k OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. Exportují databázi jako **osticket** do místního samostatného souboru.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. Po dokončení místního zálohování databáze vytvoří připojení k instanci Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Teď mohou ze samostatného souboru naimportovat (obnovit) databázi do této instance Azure Database for MySQL. Pro instanci se vytvoří nové schéma (osticket).

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. Po obnovení lze data dotazovat nástrojem Workbench a zobrazí se na webu Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Nakonec potřebují aktualizovat informace o databázi ve webových aplikacích. V instanci MySQL otevřou **Připojovací řetězce**.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. V seznamu řetězců vyhledají nastavení webové aplikace a vyberou jejich zkopírování.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. Otevřou okno Poznámkového bloku, vloží řetězec do nového souboru a aktualizují ho tak, aby odpovídal databázi osticket, instanci MySQL a nastavení přihlašovacích údajů.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. V instanci MySQL na webu Azure Portal mohu ověřit název serveru a přihlášení v oblasti **Přehled**.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Krok 5: nastavení GitHubu

Správci Contoso vytvoří nové privátní úložiště GitHubu a v Azure Database for MySQL nastaví připojení k databázi osTicket. Pak načtou webovou aplikaci do Azure App Service.

1. Přejdou do veřejného úložiště GitHubu se softwarem OsTicket a vytvoří fork do účtu Contoso na GitHubu.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. Po vytvoření forku přejdou do složky **include** a najdou soubor **ost-config.php**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Soubor se otevře v prohlížeči, kde ho upraví.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. V editoru aktualizují podrobnosti databáze, konkrétně **DBHOST** a **DBUSER**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Pak potvrdí změny.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Pro každou webovou aplikaci (**osticket-eus2** a **osticket-cus**) upraví **Nastavení aplikace** na webu Azure Portal.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Zadají přihlašovací řetězec s názvem **osticket** a zkopírují řetězec z Poznámkového bloku do **oblasti hodnot**. V rozevíracím seznamu vedle tohoto řetězce vyberou **MySQL** a uloží nastavení.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Krok 6: Konfigurace webových aplikací

V posledním kroku tohoto procesu migrace nakonfigurují správci Contoso u webových aplikací weby osTicket.

1. V primární webové aplikaci (**osticket-eus2**) otevřou **Možnost nasazení** a nastaví zdroj na **GitHub**.

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Vyberou možnosti nasazení.

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. Po nastavení možností se tato konfigurace na webu Azure Portal zobrazí jako nevyřízená.

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. Po aktualizaci konfigurace a načtení webové aplikace osTicket z GitHubu do kontejneru Dockeru, ve kterém běží Azure App Service, se tato lokalita zobrazí jako aktivní.

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Zopakují výše uvedený postup u sekundární webové aplikace (**osticket-cus**).
6. Po nakonfigurování je lokalita přístupná přes profil Traffic Manageru. Název DNS je nové umístění aplikace osTicket. [Další informace](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Firma Contoso chce název DNS, který je snadno zapamatovatelný. V DNS na řadičích domény vytvoří záznam aliasu (CNAME) **osticket.contoso.com**, který odkazuje na název Traffic Manageru.

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. U webových aplikací **osticket-eus2** a **osticket-cus** nakonfigurují možnost vlastních názvů hostitele.

    ![Konfigurace aplikace](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Nastavení automatického škálování

Nakonec u aplikace nastaví automatické škálování. Tím se zajistí, že při používání aplikace agenty se instance aplikace budou zvyšovat nebo snižovat podle potřeby firmy.

1. V App Service **APP-SRV-EUS2** otevřou možnost **Jednotka škálování**.
2. Nakonfigurují nové nastavení automatického škálování s jedním pravidlem, které zvýší počet instancí o jednu, když je procento využití procesoru u aktuální instance vyšší než 70 % po dobu 10 minut.

    ![Automatické škálování](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Konfigurací stejného nastavení pro **APP-SRV-CUS** zajistí totožné chování, pokud služby aplikace převezme sekundární oblast. Jediným rozdílem je, že výchozí instanci nastaví na hodnotu 1, protože slouží jen k převzetí služeb při selhání.

   ![Automatické škálování](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Vyčištění po migraci

Po dokončení migrace je aplikace osTicket refaktorovaná tak, aby běžela ve webové aplikaci Azure App Service s průběžným doručováním pomocí privátního úložiště GitHubu. Kvůli zvýšené odolnosti se aplikace provozuje ve dvou oblastech. Po migraci na platformu PaaS se databáze osTicket provozuje v Azure Database for MySQL.

Při vyčištění Contoso musí:

- Odebrat virtuální počítače VMware z inventáře vCenter.
- Odebrat místní virtuální počítače ze zálohovacích úloh.
- Aktualizovat interní dokumentaci o nová umístění a IP adresy.
- Zkontrolovat všechny prostředky, které spolupracují s místními virtuálními počítači, a aktualizovat všechna související nastavení nebo dokumentaci tak, aby odrážely novou konfiguraci.
- Překonfigurovat monitorování na adresu URL osticket-trafficmanager.net, aby bylo možné sledovat, jestli je aplikace v provozu.

## <a name="review-the-deployment"></a>Revize nasazení

Aplikace je teď spuštěná a firma Contoso ji teď potřebuje v nové infrastruktuře plně zprovoznit a zabezpečit.

### <a name="security"></a>Zabezpečení

Tým zabezpečení Contoso zkontroloval aplikaci a určil případné problémy se zabezpečením. Zjistil, že u komunikace mezi aplikací osTicket a instancí databáze MySQL není nakonfigurovaný protokol SSL. Touto konfigurací bude potřeba zajistit, aby provoz databáze nebylo možné prolomit. [Další informace](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).

### <a name="backups"></a>Zálohování

- Webové aplikace osTicket neobsahují stavová data, takže je není potřeba zálohovat.
- Nepotřebují konfigurovat zálohování databáze. Azure Database for MySQL automaticky vytváří a ukládá zálohy serveru. Rozhodli se u databáze využít geografickou redundanci, takže je odolná a připravená pro produkční prostředí. Zálohy lze použít k obnovení serveru do určitého bodu v čase. [Další informace](https://docs.microsoft.com/azure/mysql/concepts-backup).

### <a name="licensing-and-cost-optimization"></a>Licencování a optimalizace nákladů

- U nasazení PaaS nejsou žádné licenční problémy.
- Contoso povolí službu Azure Cost Management licencovanou společností Cloudyn, dceřinou společností Microsoftu. To je multicloudové řešení pro řízení nákladů, které pomáhá s využitím a správou Azure a dalších cloudových prostředků. [Informace](https://docs.microsoft.com/azure/cost-management/overview) o službě Azure Cost Management
