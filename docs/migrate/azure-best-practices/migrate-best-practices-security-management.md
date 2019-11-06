---
title: Osvědčené postupy pro zabezpečení a správu úloh migrovaných do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si o osvědčených postupech pro provoz, správu a zabezpečení úloh po jejich migraci do Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 34659cb5cd3a223fe084ba8975f0f7a39b2b74f6
ms.sourcegitcommit: 3669614902627f0ca61ee64d97621b2cfa585199
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/06/2019
ms.locfileid: "73656711"
---
# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Osvědčené postupy pro zabezpečení a správu úloh migrovaných do Azure

Při plánování a návrhu migrace se kromě migrace samotné musíte zamyslet i nad modelem zabezpečení a správy v Azure po dokončení migrace. Tento článek popisuje plánování a osvědčené postupy týkající se zabezpečení nasazení Azure po provedení migrace a průběžných úkonů, díky kterým bude vaše nasazení běžet na optimální úrovni.

> [!IMPORTANT]
> Uvedené osvědčené postupy a názory popsané v tomto článku jsou založené na funkcích platformy a služeb Azure, které jsou k dispozici v době vzniku tohoto článku. Funkce a možnosti se postupem času mění.

## <a name="secure-migrated-workloads"></a>Zabezpečení migrovaných úloh

Nejdůležitější úkol po migraci spočívá v zabezpečení migrovaných úloh před interními a externími hrozbami. S tím vám můžou pomoct osvědčené postupy:

- [Práce s Azure Security Center](#best-practice-follow-azure-security-center-recommendations): Naučte se pracovat s monitorováním, posouzením a doporučeními, která poskytuje Azure Security Center.
- [Šifrování dat](#best-practice-encrypt-data): Získejte osvědčené postupy pro šifrování vašich dat v Azure.
- [Nastavení antimalwaru](#best-practice-protect-vms-with-antimalware): Chraňte své virtuální počítače před malwarem a škodlivými útoky.
- [Zabezpečené webové aplikace](#best-practice-secure-web-apps): Udržujte důvěrné informace v migrovaných webových aplikacích.
- [Kontrola předplatných](#best-practice-review-subscriptions-and-resource-permissions): Ověřte, kdo může po migraci získat přístup k předplatným Azure a prostředkům.
- [Práce s protokoly](#best-practice-review-audit-and-security-logs): pravidelně zkontrolujte auditování a protokoly zabezpečení Azure.
- [Kontrola dalších funkcí zabezpečení](#best-practice-evaluate-other-security-features): pochopení a vyhodnocení pokročilých funkcí zabezpečení, které Azure nabízí.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Osvědčený postup: Sledujte doporučení Azure Security Center

Microsoft usilovně pracuje na tom, aby měli správci tenantů Azure informace potřebné k povolení funkcí zabezpečení, které chrání úlohy před útoky. Azure Security Center poskytuje jednotnou správu zabezpečení. Security Center umožňuje uplatňovat zásady zabezpečení napříč úlohami, omezit vystavení vůči hrozbám, detekovat útoky a reagovat na ně. Security Center analyzuje prostředky a konfigurace napříč tenanty Azure a poskytuje doporučení v oblasti zabezpečení, například tato:

- **Centralizovaná správa zásad** – Zajistěte dodržování předpisů společnosti nebo soulad se zákonnými požadavky na zabezpečení díky centrální správě zásad zabezpečení napříč všemi hybridními cloudovými úlohami.
- **Nepřetržité posuzování zabezpečení** – Monitorujte stav zabezpečení počítačů, sítí, služeb úložiště, datových služeb a aplikací za účelem zjišťování potenciálních problémů se zabezpečením.
- **Užitečná doporučení** – Napravujte ohrožení zabezpečení dříve, než je budou moci zneužít útočníci, díky užitečným doporučením zabezpečení s určenou prioritou.
- **Výstrahy a incidenty s určenou prioritou** – Zaměřte se nejprve na nejdůležitější hrozby díky výstrahám a incidentům zabezpečení.

Vedle hodnocení a doporučení poskytuje Azure Security Center i další funkce zabezpečení, které se dají povolit pro konkrétní prostředky.

- **Přístup podle potřeby (JIT).** Zmenšete potenciální oblast útoku v síti pomocí řízeného přístupu k portům správy na virtuálních počítačích Azure podle potřeby.
  - Pokud má virtuální počítač na internetu otevřený port RDP 3389, je neustále vystavený činnosti pochybných aktérů. IP adresy Azure jsou dobře známé a hackeři je průběžně vystavují útokům na otevřené porty 3389.
  - Přístup podle potřeby využívá skupiny zabezpečení sítě a pravidla příchozích přenosů, které omezují dobu otevření určitého portu.
  - Když je povolený přístup podle potřeby, Security Center kontroluje, jestli má uživatel v rámci řízení přístupu na základě role přístupové oprávnění k zápisu do daného virtuálního počítače. Kromě toho můžete určit pravidla připojování uživatelů k virtuálním počítačům. Pokud jsou oprávnění v pořádku, dojde ke schválení žádosti o přístup a Security Center nakonfiguruje skupiny zabezpečení sítě, aby po zadanou dobu umožňovaly příchozí datové přenosy na vybrané porty. Po uplynutí této doby se skupiny zabezpečení sítě vrátí do předchozího stavu.
- **Adaptivní řízení aplikací.** Chraňte virtuální počítače před škodlivým softwarem a malwarem tím, že budete pomocí dynamických seznamů povolených aplikací určovat, které aplikace se na nich spouštějí.
  - Adaptivní řízení aplikací umožňuje schvalovat aplikace a bránit neautorizovaným uživatelům nebo správcům instalovat na vaše virtuální počítače neschválené nebo neprověřené softwarové aplikace.
    - Můžete blokovat pokusy o spuštění škodlivých aplikací nebo na ně upozorňovat, bránit použití nežádoucích nebo škodlivých aplikací a zajistit dodržování zásady zabezpečení aplikací ve vaší organizaci.
- **Monitorování integrity souborů.** Dbejte na integritu souborů spuštěných ve virtuálních počítačích.
  - Nemusíte instalovat software, abyste mohli způsobovat problémy s virtuálním počítačem. K selhání nebo snížení výkonu virtuálního počítače může vést i změna systémového souboru. Monitorování integrity souborů prověřuje, jestli nedošlo ke změnám systémových souborů a nastavení registru, a na případné aktualizace upozorní.
  - Security Center doporučuje, které soubory je vhodné monitorovat.

**Další informace:**

- Získejte [další informace](https://docs.microsoft.com/azure/security-center/security-center-intro) o službě Azure Security Center.
- Získejte [další informace](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) o přístupu k virtuálním počítačům podle potřeby.
- Získejte [další informace](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application) o použití adaptivního řízení aplikací.
- [Začněte pracovat](https://docs.microsoft.com/azure/security-center/security-center-file-integrity-monitoring) s monitorováním integrity souborů.

## <a name="best-practice-encrypt-data"></a>Osvědčený postup: šifrování dat

Šifrování dat tvoří důležitou součást postupů zabezpečení v Azure. Povolení šifrování na všech úrovních pomáhá zabránit neoprávněným stranám v získání přístupu k citlivým datům, včetně přenášených i neaktivních uložených dat.

### <a name="encryption-for-iaas"></a>Šifrování pro IaaS

- **Virtuální počítače:** Pro virtuální počítače můžete použít Azure Disk Encryption k šifrování disků virtuálních počítačů s Windows a Linux IaaS.
  - Služba Disk Encryption za pomoci nástroje BitLocker pro Windows a DM-Crypt pro Linux zajišťuje šifrování disků s operačním systémem a daty.
  - Můžete použít šifrovací klíč vytvořený Azure nebo vlastní šifrovací klíče uchované ve službě Azure Key Vault.
  - Služba Disk Encryption zabezpečuje neaktivní data uložená ve virtuálním počítači IaaS (na disku) i data při spouštění virtuálního počítače.
    - Azure Security Center vás upozorní v případě, že některé z vašich virtuálních počítačů nejsou šifrované.
- **Úložiště:** Chraňte v úložištích data uložená ve službě Azure Storage.
  - Data uložená na účtech Azure Storage je možné šifrovat pomocí klíčů AES generovaných Microsoftem, které jsou kompatibilní se standardem FIPS 140-2, případně můžete použít i vlastní klíče.
  - Šifrování služby Storage je povolené pro všechny nové a existující účty úložiště a nedá se zakázat.

### <a name="encryption-for-paas"></a>Šifrování pro PaaS

Na rozdíl od modelu IaaS, ve kterém spravujete virtuální počítače a infrastrukturu sami, u modelu PaaS spravuje platformu a infrastrukturu poskytovatel, takže se můžete plně soustředit na logiku aplikací a funkce. Vzhledem k tomu, že služeb PaaS existuje spousta typů, se každá služba pro účely zabezpečení vyhodnocuje zvlášť. Můžeme se například podívat, jak bychom povolili šifrování pro službu Azure SQL Database.

- **Always Encrypted:** Pomocí Průvodce Always Encrypted v SQL Server Management Studio můžete chránit neaktivní neaktivní data.
  - Vytvoříte klíč Always Encrypted pro zašifrování dat v jednotlivých sloupcích.
  - Klíče Always Encrypted můžou být v metadatech databáze uložené jako šifrované nebo se dají ukládat do důvěryhodných úložišť klíčů, jako je Azure Key Vault.
  - K použití této funkce bude nejspíš potřeba provést změny aplikace.
- **Transparentní šifrování dat (TDE):** Chraňte Azure SQL Database pomocí šifrování v reálném čase a dešifrování databáze, přidružených záloh a souborů protokolů transakcí v klidovém čase.
  - TDE umožňuje provádět šifrování bez změn ve vrstvě aplikace.
  - TDE může používat šifrovací klíče poskytované Microsoftem nebo můžete díky podpoře Bring Your Own Key používat vlastní klíče.

**Další informace:**

- Získejte [další informace](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-overview) o službě Azure Disk Encryption pro virtuální počítače IaaS.
- [Povolte](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-windows) šifrování pro virtuální počítače IaaS s Windows.
- [Přečtěte si](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) o šifrování služby Azure Storage neaktivní uložená data.
- [Přečtěte si](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault) přehled funkce Always Encrypted.
- [Přečtěte si](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-2017) o transparentním šifrování dat pro Azure SQL Database.
- [Přečtěte si](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql) o transparentním šifrování dat s využitím možnosti Bring Your Own Key.

## <a name="best-practice-protect-vms-with-antimalware"></a>Osvědčený postup: ochrana virtuálních počítačů pomocí antimalwarového programu

Konkrétně starší verze virtuálních počítačů migrovaných do Azure nemusí mít nainstalovanou odpovídající úroveň antimalwarového softwaru. Azure poskytuje bezplatné řešení pro koncové body, které pomáhá chránit virtuální počítače proti virům, spywaru a dalšímu malwaru.

- Microsoft Antimalware pro Azure generuje výstrahy při pokusech o instalaci známého škodlivého nebo nežádoucího softwaru.
- Je to řešení s jedním agentem, které běží na pozadí bez lidského zásahu.
- V Azure Security Center můžete snadno identifikovat virtuální počítače, které nemají spuštěnou ochranu koncových bodů, a podle potřeby nainstalovat Microsoft Antimalware.

![Antimalware pro virtuální počítače](./media/migrate-best-practices-security-management/antimalware.png)
*Antimalware pro virtuální počítače*

**Další informace:**

- Získejte [další informace](https://docs.microsoft.com/azure/security/azure-security-antimalware) o řešení Microsoft Antimalware.

## <a name="best-practice-secure-web-apps"></a>Osvědčený postup: zabezpečení webových aplikací

Migrované webové aplikace se setkávají s několika problémy:

- Většina starších webových aplikací mívá citlivé informace uložené v konfiguračních souborech. Soubory, které tyto informace obsahují, můžou při zálohování aplikací nebo při rezervování aplikačního kódu a jeho vracení se změnami v rámci správy zdrojového kódu představovat problémy se zabezpečením.
- Kromě toho, když migrujete webové aplikace obsažené ve virtuálním počítači, pravděpodobně i tento počítač přesouváte z místní sítě a prostředí chráněného bránou firewall do prostředí vystaveného internetu. Ujistěte se, že vytváříte řešení, které dokáže odvést stejnou práci jako ochranné prostředky v místním prostředí.

Azure poskytuje hned několik řešení:

- **Azure Key Vault:** V dnešní době vývojáři webových aplikací přibývají kroky k zajištění toho, aby citlivé informace z těchto souborů neunikly. Jeden ze způsobů, jak informace zabezpečit, spočívá v jejich extrakci ze souborů a uložení do služby Azure Key Vault.
  - Službu Key Vault můžete používat jako centralizované úložiště tajných kódů aplikací a můžete s ní ovládat jejich distribuci. Informace o zabezpečení tak už nemusíte ukládat do souborů aplikací.
  - Aplikace můžou bezpečně získat přístup k informacím v trezoru pomocí identifikátorů URI, aniž by vyžadovaly vlastní kód.
  - Azure Key Vault umožňuje uzamknout přístup prostřednictvím ovládacích prvků zabezpečení Azure a bez problémů implementovat obnovování klíčů. Microsoft nemůže vaše data zobrazit ani extrahovat.
- **App Service Environment:** Pokud aplikace, kterou migrujete, potřebuje dodatečnou ochranu, můžete zvážit přidání App Service Environment a firewallu webových aplikací, abyste chránili prostředky aplikace.
  - Azure App Service Environment poskytuje plně izolované a vyhrazené prostředí, ve kterém se spouštějí aplikace App Service, jako jsou webové aplikace pro Windows a Linux, kontejnery Dockeru, mobilní aplikace a funkce.
  - Tato služba je užitečná pro aplikace, které běží ve velmi velkém měřítku, vyžadují izolaci a zabezpečený přístup k síti nebo mají vysoké využití paměti.
- **Firewall webových aplikací:** Funkce Azure Application Gateway, která poskytuje centralizovanou ochranu pro webové aplikace.
  - Chrání webové aplikace bez nutnosti úprav back-endového kódu.
  - Dokáže za jednou bránou aplikací ochránit víc webových aplikací současně.
  - Brána firewall webových aplikací se dá monitorovat pomocí služby Azure Monitor a je integrovaná do Azure Security Center.

![Zabezpečení webových aplikací](./media/migrate-best-practices-security-management/web-apps.png)

*Azure Key Vault*

**Další informace:**

- [Podívejte se na přehled](https://docs.microsoft.com/azure/key-vault/key-vault-overview) služby Azure Key Vault.
- [Získejte informace](https://docs.microsoft.com/azure/application-gateway/waf-overview) o bráně firewall webových aplikací.
- [Přečtěte si úvod](https://docs.microsoft.com/azure/app-service/environment/intro) do služby App Service Environment.
- [Zjistěte](https://docs.microsoft.com/azure/key-vault/tutorial-web-application-keyvault), jak nakonfigurovat webovou aplikaci, aby četla tajné kódy ze služby Key Vault.
- [Získejte informace](https://docs.microsoft.com/azure/application-gateway/waf-overview) o bráně firewall webových aplikací.

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Osvědčený postup: Kontrola předplatných a oprávnění prostředků

Během migrace úloh a jejich spouštění k Azure dochází k obměnám personálu s přístupem k těmto úlohám. Váš tým zabezpečení by měl přístup k vašemu tenantovi Azure a skupinám prostředků pravidelně kontrolovat. Azure nabízí možnosti správy identit a zabezpečení řízení přístupu, včetně řízení přístupu na základě role (RBAC), které umožňují autorizaci oprávnění pro přístup k prostředkům Azure.

- Řízení přístupu na základě role přiřazuje přístupová oprávnění k objektům zabezpečení. Objekty zabezpečení představují uživatele, skupiny (sady uživatelů), objekty služeb (identita používaná aplikacemi a službami) a spravované identity (identita Azure Active Directory automaticky spravovaná Azure).
- RBAC může k objektům zabezpečení přiřazovat role, jako je vlastník, přispěvatel a čtenář, a definice rolí (kolekce oprávnění), které určují, jaké operace můžou role provádět.
- RBAC může také nastavit rozsahy určující hranice určité role. Rozsah se může nastavit na několika úrovních, třeba na úrovni skupiny pro správu, předplatného, skupiny prostředků nebo prostředku.
- Zajistěte, aby správci s přístupem k Azure měli přístup jenom k prostředkům, které mají povolené. Pokud předdefinované role v Azure nejsou dostatečně podrobné, můžete vytvořit vlastní role, které budou oddělovat a omezovat přístupová oprávnění.

![Řízení přístupu](./media/migrate-best-practices-security-management/subscription.png)
*Řízení přístupu – IAM*

**Další informace:**

- [O funkci](https://docs.microsoft.com/azure/role-based-access-control/overview) řízení přístupu na základě role.
- [Zjistěte](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal), jak spravovat přístup pomocí řízení přístupu na základě role a webu Azure Portal.
- Získejte [další informace](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) o vlastních rolích.

## <a name="best-practice-review-audit-and-security-logs"></a>Osvědčený postup: Kontrola protokolů auditu a zabezpečení

Azure Active Directory (Azure AD) poskytuje protokoly aktivit, které se zobrazují v Azure Monitoru. Protokoly zachycují operace provedené v architektuře tenantů Azure, čas jejich provedení a to, kdo je provedl.

- Protokoly auditu zobrazují historii úloh v tenantovi. Protokoly aktivit přihlašování uvádějí, kdo dané úlohy provedl.
- Přístup k sestavám zabezpečení závisí na vaší licenci služby Azure AD. V části bezplatné a základní získáte seznam rizikových uživatelů a přihlášení. V edicích Premium 1 a Premium 2 získáte informace o podkladových událostech.
- Protokoly aktivit můžete směrovat do různých koncových bodů za účelem dlouhodobého uchovávání nebo získávání přehledu o datech.
- Zvykněte si kontrolovat protokoly pravidelně nebo začněte používat nástroje pro správu akcí a informací o zabezpečení (SIEM), které budou automaticky kontrolovat abnormální hodnoty. Pokud nepoužíváte verzi Premium 1 nebo 2, budete muset sami nebo prostřednictvím systému SIEM provádět řadu analýz. K těmto analýzám patří vyhledávání rizikových přihlášení a událostí a dalších vzorců ukazujících na útok ze strany uživatelů.

![Uživatelé a skupiny](./media/migrate-best-practices-security-management/azure-ad.png)

*Uživatelé a skupiny Azure AD*

**Další informace:**

- Získejte [další informace](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor) o protokolech aktivit Azure AD ve službě Azure Monitor.
- [Naučte se](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) provádět audit sestav aktivit na portálu Azure AD.

## <a name="best-practice-evaluate-other-security-features"></a>Osvědčený postup: vyhodnocení dalších funkcí zabezpečení

Azure nabízí další funkce zabezpečení, které poskytují pokročilé možnosti zabezpečení. Některé z těchto osvědčených postupů vyžadují doplňkové licence a možnosti verze Premium.

- **Implementace jednotek pro správu (AU) Azure AD.** Delegování administrativních povinností na pracovníky podpory může být jen se základním řízením přístupu v Azure rizikové. Poskytnutí přístupu ke správě všech skupin v Azure AD pracovníkům podpory pravděpodobně není zrovna ideální přístup k zabezpečení na úrovni organizace. Jednotky pro správu umožňují rozdělit prostředky Azure do kontejnerů, stejně jako se to dělá u místních organizačních jednotek (OU). K používání jednotek AU je potřeba, aby měl správce jednotek pro správu licenci Azure AD. [Další informace](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Použití vícefaktorového ověřování.** Pokud máte licenci Azure AD Premium, můžete u svých účtů správce povolit a vyžadovat vícefaktorové ověřování. Phishing je nejběžnější způsob, jakým dochází k ohrožení zabezpečení přihlašovacích údajů k účtům. Jakmile získá přihlašovací údaje k účtu správce pochybný aktér, nic mu nezabrání provést něco, co může mít dalekosáhlé důsledky, například odstranit všechny skupiny prostředků. Vícefaktorové ověřování můžete nastavit několika způsoby, například tak, aby využívalo e-mail, ověřovací aplikaci a textové zprávy. Jako správce si můžete vybrat nejméně rušivou možnost. Vícefaktorové ověřování se integruje s analýzami hrozeb a zásadami podmíněného přístupu a náhodně vyžaduje odpověď na výzvu k vícefaktorovému ověřování. Přečtěte si další informace o [zabezpečení](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) a o tom, [jak nastavit vícefaktorové ověřování](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementace podmíněného přístupu.** Ve většině malých a středně velkých organizací se správci Azure a tým podpory pravděpodobné nacházejí v jedné geografické oblasti. V takovém případě bude většina přihlášení pocházet ze stejných míst. Pokud jsou IP adresy těchto umístění poměrně statické, je celkem logické, že byste neměli vídat přihlášení správců z míst, která se nacházejí mimo tyto oblasti. Pro případ, že se pochybnému aktérovi podaří ohrozit zabezpečení přihlašovacích údajů správce, můžete implementovat funkce zabezpečení, jako je podmíněný přístup kombinovaný s vícefaktorovým ověřováním, abyste zabránili přihlášení ze vzdálených umístění nebo z podvodných umístění s náhodnými IP adresami. Získejte [další informace](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) o podmíněném přístupu a [projděte si osvědčené postupy](https://docs.microsoft.com/azure/active-directory/conditional-access/best-practices) pro podmíněný přístup ve službě Azure AD.
- **Kontrola oprávnění podnikových aplikací.** V průběhu času můžou správci vybírat odkazy od Microsoftu a třetích stran, aniž by přesně věděli, jaký můžou mít dopad na organizaci. Odkazy můžou zobrazovat obrazovky pro vyjádření souhlasu, které přidělují oprávnění k aplikacím Azure a můžou umožnit přístup ke čtení dat služby Azure AD, nebo dokonce plný přístup ke správě celého předplatného Azure. Měli byste pravidelně kontrolovat aplikace, u kterých vaši správci a uživatelé povolili přístup k prostředkům Azure. Zajistěte, aby tyto aplikace měly jen nezbytně nutná oprávnění. Kromě toho můžete jednou za čtvrt nebo půl roku poslat uživatelům e-mail s odkazem na stránky aplikace, aby věděli, jakým aplikacím povolili přístup k datům organizace. [Přečtěte si víc](https://docs.microsoft.com/azure/active-directory/manage-apps/application-types) o typech aplikací a o tom, [jak řídit](https://docs.microsoft.com/azure/active-directory/manage-apps/remove-user-or-group-access-portal) přiřazení aplikací v Azure AD.

## <a name="managed-migrated-workloads"></a>Spravované migrované úlohy

V této části doporučujeme některé osvědčené postupy pro správu Azure, včetně těchto:

- [Správa prostředků](#best-practice-name-resource-groups): osvědčené postupy pro skupiny prostředků Azure a prostředky, včetně inteligentního pojmenovávání, prevence náhodného odstranění, správy oprávnění prostředků a efektivního označování prostředků.
- [Použití modrotisky](#best-practice-implement-blueprints): Získejte rychlý přehled o používání plánů pro vytváření a správu prostředí nasazení.
- [Přečtěte si architektury](#best-practice-review-azure-reference-architectures): Projděte si ukázkové architektury Azure a Naučte se, jak sestavovat nasazení po migraci.
- [Nastavení skupin pro správu](#best-practice-manage-resources-with-azure-management-groups): Pokud máte více předplatných, můžete je shromáždit do skupin pro správu a u těchto skupin použít nastavení zásad správného řízení.
- [Nastavení zásad přístupu](#best-practice-deploy-azure-policy): zásady dodržování předpisů aplikujte na prostředky Azure.
- [Implementujte strategii BCDR](#best-practice-implement-a-bcdr-strategy): Propojte strategii pro provozní kontinuitu a zotavení po havárii (BCDR), která zajistí bezpečnost dat, odolnost prostředí a prostředky v provozu, pokud dojde k výpadku.
- [Správa virtuálních počítačů](#best-practice-use-managed-disks-and-availability-sets): virtuální počítače skupiny do skupin dostupnosti pro odolnost a vysokou dostupnost. Pokud si navíc chcete usnadnit správu disků a úložišť virtuálních počítačů, použijte spravované disky.
- [Sledování využití prostředků](#best-practice-monitor-resource-usage-and-performance): umožňuje povolit protokolování diagnostiky pro prostředky Azure, vytvářet upozornění a playbooky pro proaktivní řešení potíží a používat řídicí panel Azure pro sjednocení vašeho stavu a stavu nasazení.
- [Správa podpory a aktualizace](#best-practice-manage-updates): Seznamte se s plánem podpory Azure a postupem jeho implementace, Získejte osvědčené postupy pro udržování aktuálnosti virtuálních počítačů a umístěte procesy do správy změn.

## <a name="best-practice-name-resource-groups"></a>Osvědčené postupy: pojmenování skupin prostředků

Když budou mít vaše skupiny prostředků smysluplné názvy, které správci a členové týmu podpory snadno rozpoznají a zorientují se v nich, významně to přispěje ke zvýšení produktivity a efektivity.

- Doporučujeme dodržovat zásady vytváření názvů Azure.
- Pokud synchronizujete místní službu Active Directory do Azure AD pomocí nástroje Azure AD Connect, zamyslete se, jestli by nebylo vhodné přizpůsobit názvy místních skupin zabezpečení názvům prostředků v Azure.

![Pojmenování](./media/migrate-best-practices-security-management/naming.png)

*Pojmenování skupin prostředků*

**Další informace:**

- [Získejte další informace](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) o zásadách vytváření názvů.

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Osvědčený postup: implementace zámků pro odstranění skupin prostředků

To poslední, co potřebujete, je nemoct najít některou skupinu prostředků, protože ji někdo omylem odstranil. Doporučujeme vám implementovat zámky odstranění, aby se takové nehody nestávaly.

![Zámky odstranění](./media/migrate-best-practices-security-management/locks.png)

*Zámky odstranění*

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) o uzamknutí prostředků, které brání neočekávaným změnám.

## <a name="best-practice-understand-resource-access-permissions"></a>Osvědčený postup: pochopení oprávnění pro přístup k prostředkům

Vlastník předplatného má přístup ke všem skupinám prostředků a prostředkům v rámci vašeho předplatného.

- Toto cenné oprávnění přidělujte uživatelům jen zřídka. Je důležité pochopit možné důsledky těchto typů oprávnění, aby vaše prostředí zůstalo zabezpečené a stabilní.
- Ujistěte se, že jsou prostředky umístěné ve vhodných skupinách prostředků:
  - Seskupujte prostředky s podobným životním cyklem. V ideálním případě by v případě, že chcete odstranit celou skupinu prostředků, nemělo být nutné žádný prostředek přesouvat.
  - Prostředky, které podporují určitou funkci nebo úlohu, by se měly v zájmu jednodušší správy umístit dohromady.

**Další informace:**

- [Získejte informace](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise) o uspořádání předplatných a skupin prostředků.

## <a name="best-practice-tag-resources-effectively"></a>Osvědčené postupy: efektivní označení prostředků

Použití jenom názvu skupiny prostředků, který se vztahuje k prostředkům, často neposkytne dostatek metadat pro efektivní implementaci mechanismů, jako je interní fakturace nebo správa v rámci předplatného.

- K osvědčeným postupům patří používat v Azure značky, které přidávají užitečná metadata. Na ta pak můžete zadávat dotazy nebo z nich vytvářet sestavy.
- Značky představují způsob, jak logicky uspořádat prostředky podle vlastností, které definujete. Značky se dají používat na skupiny prostředků nebo přímo na prostředky.
- Značky se dají použít na skupinu prostředků nebo přímo na konkrétní prostředek. Prostředky v určité skupině nedědí značky dané skupiny prostředků.
- Přidělování značek můžete automatizovat pomocí PowerShellu nebo služby Azure Automation, případně můžete označovat jednotlivé skupiny a prostředky. Automatický nebo samoobslužný přístup ke značkám. Pokud máte zavedený systém správy požadavků a změn, můžete snadno použít informace v požadavcích k vytvoření značek prostředků specifických pro vaši společnost.

![Použití značek](./media/migrate-best-practices-security-management/tagging.png)
*Použití značek*

**Další informace:**

- [Přečtěte víc](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) o použití značek a jejich omezeních.
- [Podívejte se](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags#powershell) na příklady, jak nastavit vytváření značek v PowerShellu a CLI, a zjistěte, jak použít značky skupiny prostředků na obsažené prostředky.
- [Přečtěte si](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) osvědčené postupy vytváření značek v Azure.

## <a name="best-practice-implement-blueprints"></a>Osvědčený postup: implementace modrotisky

Stejně jako technický nákres či podrobný plán (anglicky „blueprint“) umožňuje technikovi nebo architektovi načrtnout parametry návrhu projektu, služba Azure Blueprints umožňuje cloudovým architektům a centrálním oddělením IT definovat opakovatelnou sadu prostředků Azure, která implementuje a dodržuje standardy, vzory a požadavky organizace. Díky službě Azure Blueprints můžou vývojářské týmy rychle vytvářet nová prostředí, která vyhovují předpisům organizace a která obsahují sadu předdefinovaných komponent – třeba síťových – ke zrychlení vývoje a distribuce.

- Podrobné plány se dají použít k orchestraci nasazení skupin prostředků, šablon služby Azure Resource Manager a přiřazování zásad a rolí.
- Podrobné plány jsou uložené v globálně distribuované službě Azure Cosmos DB. Objekty podrobného plánu se replikují do několika oblastí Azure. Replikace zajišťuje nízkou latenci, vysokou dostupnost a konzistentní přístup k podrobným plánům bez ohledu na to, do které oblasti daný podrobný plán nasazuje prostředky.

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/governance/blueprints/overview) o podrobných plánech.
- [Prohlédněte si](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) příklad podrobného plánu, který slouží k urychlení AI ve zdravotnictví.

## <a name="best-practice-review-azure-reference-architectures"></a>Osvědčený postup: Kontrola referenčních architektur Azure

Vytváření zabezpečených, škálovatelných a snadno spravovatelných úloh v Azure může být náročný úkol. Vzhledem k nepřetržitým změnám může být těžké držet krok s různými funkcemi pro optimální prostředí. Při návrhu a migraci úloh může být užitečné mít po ruce referenční architektury, ze kterých se můžete poučit. Azure a partneři Azure vytvořili několik takových ukázkových referenčních architektur pro různé typy prostředí. Tyto ukázky jsou vytvořené tak, aby poskytovaly nápady, kterými se můžete inspirovat a na kterých můžete stavět.

Referenční architektury jsou uspořádané podle scénářů. Obsahují osvědčené postupy a Rady pro správu, dostupnost, škálovatelnost a zabezpečení.
Azure App Service Environment poskytuje plně izolované a vyhrazené prostředí, ve kterém se spouštějí aplikace App Service, včetně webových aplikací pro Windows a Linux, kontejnerů Dockeru, mobilních aplikací a funkcí. Služba App Service přináší vaší aplikaci možnosti Azure v podobě zabezpečení, vyrovnávání zatížení, automatického škálování a automatizované správy. Můžete také využívat její možnosti DevOps, jako jsou průběžné nasazování z Azure DevOps a GitHubu, správa balíčků, přípravná prostředí, vlastní doména a certifikáty SSL. Služba App Service je vhodná pro aplikace, které vyžadují izolaci a zabezpečený síťový přístup, nebo pro aplikace, které využívají velké množství paměti a jiných prostředků vyžadujících škálování.

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/architecture/reference-architectures) o referenčních architekturách v Azure.
- [Prohlédněte si](https://docs.microsoft.com/azure/architecture/example-scenario) ukázkové scénáře Azure.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Osvědčené postupy: Správa prostředků pomocí skupin pro správu Azure

Pokud má vaše organizace víc předplatných, musíte pro ně spravovat přístup, zásady a dodržování předpisů. Skupiny pro správu Azure představují úroveň rozsahu nad předplatnými.

- Předplatná uspořádáte do kontejnerů označovaných jako skupiny pro správu a na ně použijete své zásady správného řízení.
- Všechna předplatná ve skupině pro správu automaticky dědí podmínky příslušné skupiny pro správu.
- Skupiny pro správu umožňují správu na podnikové úrovni ve velkém měřítku bez ohledu na to, jaké typy předplatného máte.
- Můžete například použít zásadu skupiny pro správu, která omezuje oblasti, ve kterých se dají vytvářet virtuální počítače. Tato zásada se potom použije pro všechny skupiny pro správu, předplatná a prostředky v rámci dané skupiny pro správu.
- Můžete vytvořit flexibilní strukturu skupin pro správu a předplatných a uspořádat tak prostředky do hierarchie umožňující využít jednotné zásady a správu přístupu.

Následující diagram ukazuje příklad vytvoření hierarchie pro zásady správného řízení s využitím skupin pro správu.

![Skupiny pro správu](./media/migrate-best-practices-security-management/management-groups.png)
*Skupiny pro správu*

**Další informace:**

- [Přečtěte si víc](https://docs.microsoft.com/azure/governance/management-groups/index) o uspořádání prostředků do skupin pro správu.

## <a name="best-practice-deploy-azure-policy"></a>Osvědčený postup: nasazení Azure Policy

Azure Policy je služba v Azure, která slouží k vytváření, přiřazování a správě zásad.

- Zásady vynucují na vašich prostředcích různá pravidla a vlastnosti, aby tyto prostředky zůstaly kompatibilní s vašimi firemními standardy a smlouvami o úrovni služeb.
- Azure Policy vyhodnocuje vaše prostředky a hledá ty, které nejsou v souladu s vašimi zásadami.
- Můžete například vytvořit zásadu, která pro virtuální počítače ve vašem prostředí povoluje jenom určitou velikost SKU. Azure Policy vyhodnocuje toto nastavení při vytváření a aktualizaci prostředků a při kontrole existujících prostředků.
- Azure poskytuje některé předdefinované zásady, které můžete přiřadit, nebo můžete vytvořit zásady vlastní.

![Azure Policy](./media/migrate-best-practices-security-management/policy.png)
*Azure Policy*

**Další informace:**

- [Získejte přehled](https://docs.microsoft.com/azure/governance/policy/overview) o službě Azure Policy.
- [Získejte in](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) o vytváření a správě zásad, které umožňují prosazovat dodržování předpisů.

## <a name="best-practice-implement-a-bcdr-strategy"></a>Osvědčené postupy: implementace strategie BCDR

Plánování provozní kontinuity a zotavení po havárii (BCDR) je zásadně důležitý úkon, který byste měli provést během procesu plánování migrace do Azure. Řečeno jazykem práva, vaše smlouvy můžou zahrnovat doložku o zásazích vyšší moci, která vás zbavuje závazků v případě zásahu vyšší moci, například hurikánu nebo zemětřesení. Zároveň ale máte určité závazky týkající se vaší schopnosti zajistit v případě přírodní katastrofy funkčnost služeb a v případě potřeby provést jejich obnovení. Tato schopnost může rozhodnout o budoucnosti vaší společnosti.

Obecně řečeno by vaše strategie BCDR měla zahrnovat tyto body:

- **Zálohování dat:** Jak uchovávat data v bezpečí, abyste je mohli snadno obnovit, pokud dojde k výpadku.
- **Zotavení po havárii:** Jak udržet aplikace odolné a dostupné, pokud dojde k výpadku.

### <a name="set-up-bcdr"></a>Nastavení BCDR

Při migraci do Azure je důležité pochopit, že i když platforma Azure poskytuje integrované funkce zajišťující odolnost, je potřeba navrhnout nasazení Azure tak, aby využívalo funkce a služby Azure, které poskytují vysokou dostupnost, zotavení po havárii a zálohování.

- Vaše řešení BCDR bude záviset na cílech vaší společnosti a na vaší strategii nasazení v Azure. U nasazení využívajících model infrastruktury jako služby (IaaS) a platformy jako služby (PaaS) existují z hlediska BCDR odlišné výzvy.
- Jakmile vytvoříte řešení BCDR, měli byste je pravidelně testovat a kontrolovat, jestli je vaše strategie pořád vhodná.

### <a name="back-up-an-iaas-deployment"></a>Zálohování nasazení IaaS

Ve většině případů se místní úlohy po migraci vyřadí z provozu a strategii zálohování dat, kterou jste používali v místním prostředí, je potřeba rozšířit nebo nahradit. Pokud do Azure migrujete celé datacentrum, budete muset navrhnout a implementovat řešení úplného zálohování využívající technologie Azure nebo integrovaná řešení třetích stran.

U úloh běžících na virtuálních počítačích IaaS Azure můžete zvážit tato řešení zálohování:

- **Azure Backup:** Poskytuje zálohy konzistentní s aplikací pro virtuální počítače Azure s Windows a Linux.
- **Snímky úložiště:** Převezme snímky úložiště objektů BLOB.

#### <a name="azure-backup"></a>Azure Backup

Azure Backup vytváří body obnovení dat, které se ukládají do služby Azure Storage. Azure Backup může zálohovat disky virtuálních počítačů Azure a soubory služby Azure Files (ve verzi Preview). Služba Azure Files poskytuje sdílené složky v cloudu přístupné přes protokol SMB.

Azure Backup můžete použít k zálohování virtuálních počítačů několika způsoby.

- **Přímé zálohování z nastavení virtuálního počítače.** Virtuální počítače můžete pomocí Azure Backup zálohovat přímo z možností daného virtuálního počítače na webu Azure Portal. Virtuální počítač můžete zálohovat jednou za den a disk virtuálního počítače můžete obnovit podle potřeby. Azure Backup vytváří snímky dat s podporou aplikací (VSS) a na virtuální počítač se tedy neinstaluje žádný agent.
- **Přímé zálohování v trezoru služby Recovery Services.** Virtuální počítače IaaS můžete zálohovat nasazením trezoru Azure Backup Recovery Services. Ten poskytuje jedno umístění pro sledování a správu záloh a také podrobné možnosti zálohování a obnovení. Zálohování probíhá na úrovni souborů/složek až třikrát denně. Nezahrnuje podporu aplikací a nepodporuje Linux. Na každý virtuální počítač, který chcete zálohovat pomocí této metody, nainstalujte agenta MARS (Microsoft Azure Recovery Services).
- **Ochrana virtuálního počítače pomocí Azure Backup Serveru.** Azure Backup Server je ve službě Azure Backup k dispozici zdarma. Virtuální počítač se zálohuje do místního úložiště Azure Backup Serveru. Azure Backup Server potom zálohujete do Azure ve formě trezoru. Zálohování zahrnuje podporu aplikací a nabízí plnou kontrolu nad četností zálohování a dobou uchovávání záloh. Můžete zálohovat na úrovni aplikace, například zálohovat SQL Server nebo SharePoint.

Z důvodu zabezpečení Azure Backup průběžně šifruje data pomocí AES 256 a posílá je do Azure přes protokol HTTPS. Zálohovaná neaktivní uložená data v Azure se šifrují pomocí [šifrování služby Storage (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), včetně dat pro přenos a uložení.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
*Azure Backup*

**Další informace:**

- [Přečtěte si](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) o různých typech záloh.
- [Naplánujte infrastrukturu zálohování](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction) virtuálních počítačů v Azure.

#### <a name="storage-snapshots"></a>Snímky úložiště

Virtuální počítače Azure se ukládají jako objekty blob stránky do Azure Storage.

- Snímky zachycují stav objektu blob v určitém časovém bodě.
- Alternativní způsob zálohování disků virtuálních počítačů Azure spočívá v pořízení snímku objektů blob úložiště a jejich zkopírování do jiného účtu úložiště.
- Můžete zkopírovat celý objekt blob nebo pomocí přírůstkové kopie snímku zkopírovat jenom rozdílové změny, takže bude zabírat méně místa v úložišti.
- Pokud chcete udělat další preventivní opatření, můžete u účtů úložiště objektů blob povolit obnovitelné odstranění. Když je tato funkce povolená, odstraněné objekty blob se označí k odstranění, ale hned se nevyprázdní. Během přechodného období se dá objekt blob ještě obnovit.

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction) o službě Azure Blob Storage.
- [Zjistěte](https://docs.microsoft.com/azure/storage/blobs/storage-blob-snapshots), jak vytvořit snímek objektu blob.
- [Podívejte se na ukázkový scénář](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) zálohování úložiště objektů blob.
- [Přečtěte si](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete) o obnovitelném odstranění.
- [Zotavení po havárii a vynucené převzetí služeb při selhání (Preview) ve službě Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

#### <a name="third-party-backup"></a>Řešení zálohování třetích stran

Kromě toho můžete používat i řešení třetích stran, která zálohují virtuální počítače a kontejnery úložiště Azure do místního úložiště nebo u jiných poskytovatelů cloudu. [Získejte další informace](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1) o řešeních zálohování na webu Azure Marketplace.

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Nastavení zotavení po havárii pro aplikace IaaS

Vedle ochrany dat musí strategie provozní kontinuity a zotavení po havárii (BCDR) myslet na to, jak zajistit dostupnost aplikací a úloh v případě havárie. U úloh běžících na virtuálních počítačích IaaS Azure a v Azure Storage můžete zvážit tato řešení zálohování:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery je primární služba Azure, která dbá na to, aby se mohly virtuální počítače Azure při výpadcích přepnout do stavu online a aby byly dostupné aplikace na virtuálních počítačích.

Site Recovery replikuje virtuální počítače z primární do sekundární oblasti Azure. Pokud dojde k výpadku, dojde k převzetí služeb virtuálních počítačů z primární oblasti a je možné k nim získat přístup v sekundární oblasti. Když se provoz vrátí do normálu, můžete služby virtuálních počítačů navrátit do primární oblasti.

![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)

*Site Recovery*

**Další informace:**

- [Projděte si](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) scénáře zotavení po havárii pro virtuální počítače Azure.
- [Zjistěte](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-replicate-after-migration), jak po migraci nastavit u virtuálního počítače v Azure zotavení po havárii.

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Osvědčený postup: použití spravovaných disků a skupin dostupnosti

Azure logicky seskupuje virtuální počítače do skupin dostupnosti a virtuální počítače v určité skupině izoluje od ostatních prostředků. Virtuální počítače ve skupině dostupnosti jsou rozptýlené do víc domén selhání s oddělenými subsystémy, aby byly chráněné před místními selháními, a jsou taky rozptýlené do víc aktualizačních domén, aby se všechny virtuální počítače ve stejné skupině nerestartovaly ve stejnou chvíli.

Spravované disky Azure zjednodušují správu disků virtuálních počítačů Azure IaaS tím, že spravují účty úložiště přidružené k diskům virtuálních počítačů.

- Pokud je to možné, doporučujeme používat spravované disky. Stačí jenom zadat typ úložiště, který chcete použít, a velikost disku, který potřebujete, a Azure ho vytvoří a bude spravovat za vás, bez vašeho přispění.
- Existující disky můžete převést na spravované.
- Měli byste vytvořit virtuální počítače ve skupinách dostupnosti, které zajišťují vysokou odolnost a dostupnost. Pokud dojde k plánovanému nebo neplánovanému výpadku, skupiny dostupnosti zajistí, aby byl dál dostupný aspoň jeden virtuální počítač ze skupiny.

![Spravované disky](./media/migrate-best-practices-security-management/managed-disks.png)

*Spravované disky*

**Další informace:**

- [Přečtěte si přehled](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) informací o spravovaných discích.
- [Přečtěte si](https://docs.microsoft.com/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks) informace o převádění disků na spravované.
- [Naučte se](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) spravovat dostupnost virtuálních počítačů s Windows v Azure.

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Osvědčený postup: sledování využití a výkonu prostředků

Možná jste přesunuli úlohy do Azure kvůli obrovským možnostem škálování, které tato platforma nabízí. Přesunutí úlohy ale neznamená, že Azure automaticky implementuje škálování bez vašeho zásahu. Příklad:

- Pokud vaše marketingová organizace vydá novou televizní reklamu, která zvýší návštěvnost o 300 %, může to způsobit problémy s dostupností webu. Nově migrovaná úloha může narazit na přiřazené limity a selhat.
- Dalším příkladem může být distribuovaný útok s cílem odepření služeb (DDoS) na vaši migrovanou úlohu. V takovém případě možná nebudete chtít navýšit kapacitu, ale spíš zabránit zdroji útoků v tom, aby se dostal k vašim prostředkům.

Tyto dva případy mají různá řešení, u obou ale potřebujete získat přehled o tom, co se děje. K tomu vám pomůže monitorování využití a výkonu.

- Azure Monitor vám pomůže zjistit potřebné metriky a poskytne odezvu v podobě výstrah, automatického škálování, center událostí, aplikací logiky a dalších možností.
- Kromě monitorování Azure můžete taky integrovat aplikaci SIEM třetí strany, která bude monitorovat události auditu a výkonu v protokolech Azure.

![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
*Azure Monitor*

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/azure-monitor/overview) o službě Azure Monitor.
- [Projděte si osvědčené postupy](https://docs.microsoft.com/azure/architecture/best-practices/monitoring) v oblasti monitorování a diagnostiky.
- [Získejte informace](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling) o automatickém škálování.
- [Zjistěte](https://docs.microsoft.com/azure/security-center/security-center-export-data-to-siem), jak směrovat data z Azure do nástroje SIEM.

## <a name="best-practice-enable-diagnostic-logging"></a>Osvědčený postup: povolení protokolování diagnostiky

Prostředky Azure generují značný počet metrik protokolování a telemetrických dat.

- Ve výchozím nastavení nemá většina typů prostředků povolené protokolování diagnostiky.
- Když u svých prostředků povolíte protokolování diagnostiky, můžete zadávat dotazy na data protokolů a na jejich základě vytvářet výstrahy a playbooky.
- Jakmile povolíte protokolování diagnostiky, získá každý prostředek určitou sadu kategorií. Vyberete jednu nebo víc kategorií protokolování a umístění pro data protokolu. Protokoly je možné odesílat do účtu úložiště, do centra událostí nebo do protokolů služby Azure Monitor.

![Protokolování diagnostiky](./media/migrate-best-practices-security-management/diagnostics.png)
*Protokolování diagnostiky*

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) o shromažďovat a využívání dat protokolu.
- [Zjistěte](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema), jaká podpora je dostupná pro protokolování diagnostiky.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Osvědčený postup: nastavení výstrah a playbooky

Když u prostředků Azure povolíte protokolování diagnostiky, můžete začít na základě dat protokolů vytvářet vlastní výstrahy.

- Výstrahy proaktivně upozorňují na výskyt určitých podmínek v monitorovaných datech. Díky tomu můžete problémy řešit dřív, než si jich všimnou uživatelé. Výstrahy můžou upozorňovat na věci, jako jsou hodnoty metrik, dotazy na prohledávání protokolů, události v protokolu aktivit, stav platformy nebo dostupnost webu.
- Když se aktivují výstrahy, můžete spustit playbook aplikace logiky. Playbook pomáhá automatizovat a orchestrovat odezvu na určitou výstrahu. Playbooky jsou založené na službě Azure Logic Apps. Playbooky můžete vytvářet na základě šablon aplikací logiky, nebo si můžete vytvářet vlastní.
- Jako jednoduchý příklad můžeme uvést vytvoření výstrahy, která se aktivuje, když v určité skupině zabezpečení sítě dojde k prohledávání portů. Můžete nastavit playbook, který se spustí a uzamkne IP adresu místa původu prohledávání.
- Dalším příkladem může být aplikace s nevrácenou pamětí. Když využití paměti vzroste do určitého bodu, playbook může celý proces vrátit na začátek.

![Výstrahy](./media/migrate-best-practices-security-management/alerts.png)
*Výstrahy*

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-alerts) o výstrahách.
- [Získejte informace](https://docs.microsoft.com/azure/security-center/security-center-playbooks) o playboocích zabezpečení, které reagují na výstrahy služby Security Center.

## <a name="best-practice-use-the-azure-dashboard"></a>Osvědčený postup: Použití řídicího panelu Azure

Azure Portal je jednotná webová konzola, která umožňuje vytvářet, spravovat a sledovat všechno od jednoduchých webových aplikací až po složité cloudové aplikace. Zahrnuje přizpůsobitelné řídicí panely a možnosti usnadnění.

- Můžete vytvořit několik řídicích panelů a sdílet je s ostatními uživateli, kteří mají přístup k vašim předplatným Azure.
- V případě tohoto sdíleného modelu má váš tým přehled o prostředí Azure, což jeho členům umožňuje proaktivní přístup při správě systémů v cloudu.

![Řídicí panel Azure](./media/migrate-best-practices-security-management/dashboard.png)
*Řídicí panel Azure*

**Další informace:**

- [Zjistěte](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards), jak vytvořit řídicí panel.
- [Získejte informace](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-structure) o struktuře řídicích panelů.

## <a name="best-practice-understand-support-plans"></a>Osvědčený postup: principy plánů podpory

Dřív nebo později nastane situace, kdy budete potřebovat spolupracovat s pracovníky podpory ve vaší společnosti nebo s pracovníky podpory Microsoftu. Je zásadně důležité mít vytvořenou sadu zásad a postupů podpory pro případy, jako je zotavení po havárii. Kromě toho by měli vaši správci a pracovníci podpory umět tyto zásady implementovat.

- V nepravděpodobném případě, že vaši úlohu ovlivní nějaký problém se službou Azure, by měli správci vědět, jak co nejlépe a nejefektivněji odeslat Microsoftu lístek podpory.
- Seznamte se s různými plány podpory, které Azure nabízí. Doby odezvy sahají od možností určených pro vývojářské instance až po podporu Premier, která nabízí dobu odezvy kratší než 15 minut.

![Plány podpory](./media/migrate-best-practices-security-management/support.png)
*Plány podpory*

**Další informace:**

- [Získejte přehled](https://azure.microsoft.com/support/options) informací o plánech podpory Azure.
- [Získejte informace](https://azure.microsoft.com/support/legal/sla) o smlouvách o úrovni služeb (SLA).

## <a name="best-practice-manage-updates"></a>Osvědčené postupy: Správa aktualizací

Provádění pravidelných aktualizací operačního systému a softwaru virtuálních počítačů Azure představuje nesmírně náročný úkol. Je velmi důležité mít možnost přehledně si zobrazit všechny virtuální počítače, zjistit, jaké aktualizace potřebují, a tyto aktualizace automaticky nainstalovat.

- Ke správě aktualizací operačního systému počítačů s Windows a Linuxem, které jsou nasazené v Azure, v místním prostředí a v cloudech jiných poskytovatelů, můžete použít funkci Update Management ve službě Azure Automation.
- Pomocí nástroje Update Management můžete rychle vyhodnotit stav dostupných aktualizací na všech agentských počítačích a spravovat instalaci aktualizací.
- Nástroj Update Management můžete pro virtuální počítače povolit přímo z účtu Azure Automation. Jednotlivé virtuální počítače můžete také aktualizovat z příslušných stránek na webu Azure Portal.
- Kromě toho můžete virtuální počítače Azure zaregistrovat do nástroje System Center Configuration Manager. Úlohu Configuration Manageru potom můžete migrovat do Azure a vytvářet sestavy a aktualizovat software z jednoho webového rozhraní.

![Aktualizace virtuálních počítačů](./media/migrate-best-practices-security-management/updates.png)
*Aktualizace*

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/automation/automation-update-management) o správě aktualizací v Azure.
- [Zjistěte](https://docs.microsoft.com/azure/automation/oms-solution-updatemgmt-sccmintegration), jak do správy aktualizací zapojit Configuration Manager.
- [Přečtěte si nejčastější dotazy](https://docs.microsoft.com/sccm/core/understand/configuration-manager-on-azure) týkající se Configuration Manageru.

## <a name="implement-a-change-management-process"></a>Implementace procesu správy změn

Jak už to u produkčních systémů bývá, jakákoli změna může ovlivnit celé prostředí. Cenný přírůstkem do vašeho migrovaného prostředí tedy může být proces správy změn, který vyžaduje odesílání žádostí o změny v produkčních systémech.

- Můžete vytvářet rámce osvědčených postupů pro správu změn, které zvýší informovanost správců a pracovníků podpory.
- Můžete používat službu Azure Automation, která vám pomůže se správou konfigurace a sledováním změn u migrovaných úloh.
- Při vynucování procesu správy změn můžete používat protokoly auditu, které propojí protokoly změn Azure s domněle existujícími (nebo neexistujícími) žádostmi o změnu. Když pak uvidíte, že došlo ke změně bez odeslání příslušné žádosti o změnu, můžete začít zjišťovat, co se v procesu stalo.

Azure řešení sledování změn v rámci služby Azure Automation:

- Řešení sleduje změny softwaru a souborů systému Windows a Linux, klíčů registru Windows, služeb Windows a linuxových démonů.
- Změny na monitorovaných serverech se odesílají ke zpracování do služby Azure Monitor v cloudu.
- Na přijatá data se aplikuje logika a cloudová služba data zaznamená.
- Na řídicím panelu Sledování změn si můžete snadno prohlédnout změny provedené v serverové infrastruktuře.

![Správa změn](./media/migrate-best-practices-security-management/change.png)
*Správa změn*

**Další informace:**

- [Získejte informace](https://docs.microsoft.com/azure/automation/automation-change-tracking) o sledování změn.
- [Získejte informace](https://docs.microsoft.com/azure/automation/automation-intro) o možnostech služby Azure Automation.

## <a name="next-steps"></a>Další kroky

Projděte si další osvědčené postupy:

- [Osvědčené postupy](./migrate-best-practices-networking.md) pro síťové služby po migraci
- [Osvědčené postupy](./migrate-best-practices-costs.md) pro správu nákladů po migraci
