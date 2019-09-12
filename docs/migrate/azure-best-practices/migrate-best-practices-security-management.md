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
ms.openlocfilehash: b7d2ac8d624115c9d843ded8a045cd68f4050650
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825858"
---
# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Osvědčené postupy pro zabezpečení a Správa úloh migrovat do Azure

Jako je plánování a návrh pro migraci, kromě přemýšlení o migraci, je potřeba zvážit zabezpečení a správu modelu ve službě Azure po migraci. Tento článek popisuje plánování a osvědčené postupy pro zabezpečení vašeho nasazení Azure po migraci a pro probíhající úlohy, aby vaše nasazení, spuštění na optimální úrovni.

> [!IMPORTANT]
> Osvědčené postupy a názory, které jsou popsané v tomto článku jsou založené na platformě Azure a služby funkce dostupné v době zápisu. Funkce a možnosti v průběhu času měnit.

## <a name="secure-migrated-workloads"></a>Zabezpečit přenášená zatížení

Po dokončení migrace nejdůležitějších úloh je zabezpečit přenášená zatížení z interních a externích hrozeb. S tím vám můžou pomoct osvědčené postupy:

- [Práce se službou Azure Security Center:](#best-practice-follow-azure-security-center-recommendations) Naučte se pracovat s monitorováním, hodnoceními a doporučeními, která poskytuje Azure Security Center.
- [Šifrování dat:](#best-practice-encrypt-data) Získejte osvědčené postupy šifrování vašich dat v Azure.
- [Nastavení antimalwaru:](#best-practice-protect-vms-with-antimalware) Chraňte své virtuální počítače před malwarem a škodlivými útoky.
- [Zabezpečení webových aplikací:](#best-practice-secure-web-apps) Chraňte citlivé informace v migrovaných webových aplikacích.
- [Kontrola předplatných:](#best-practice-review-subscriptions-and-resource-permissions) Po migraci ověřte, kdo má přístup k předplatným a prostředkům Azure.
- [Práce s protokoly:](#best-practice-review-audit-and-security-logs) Pravidelně kontrolujte protokoly auditů a zabezpečení v Azure.
- [Kontrola dalších funkcí zabezpečení:](#best-practice-evaluate-other-security-features) Seznamte se s pokročilými funkcemi zabezpečení, které nabízí Azure, a vyhodnoťte si je.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Osvědčený postup: Dodržování doporučení služby Azure Security Center

Microsoft usilovně pracuje na tom, aby měli správci tenantů Azure informace potřebné k povolení funkcí zabezpečení, které chrání úlohy před útoky. Azure Security Center zajišťuje jednotnou správu zabezpečení. Ze služby Security Center můžete používat zásady zabezpečení napříč úlohami, omezení rizika ohrožení a detekovat a reagovat vůči útokům. Security Center analyzuje prostředky a konfigurací tenantů Azure a poskytuje doporučení zabezpečení, včetně:

- **Centralizovaná správa zásad** – Zajistěte dodržování předpisů společnosti nebo soulad se zákonnými požadavky na zabezpečení díky centrální správě zásad zabezpečení napříč všemi hybridními cloudovými úlohami.
- **Nepřetržité posuzování zabezpečení** – Monitorujte stav zabezpečení počítačů, sítí, služeb úložiště, datových služeb a aplikací za účelem zjišťování potenciálních problémů se zabezpečením.
- **Užitečná doporučení** – Napravujte ohrožení zabezpečení dříve, než je budou moci zneužít útočníci, díky užitečným doporučením zabezpečení s určenou prioritou.
- **Výstrahy a incidenty s určenou prioritou** – Zaměřte se nejprve na nejdůležitější hrozby díky výstrahám a incidentům zabezpečení.

Vedle hodnocení a doporučení poskytuje Azure Security Center i další funkce zabezpečení, které se dají povolit pro konkrétní prostředky.

- **Přístup podle potřeby (JIT).** Zmenšete potenciální oblast útoku v síti pomocí řízeného přístupu k portům správy na virtuálních počítačích Azure podle potřeby.
  - Pokud má virtuální počítač na internetu otevřený port RDP 3389, je neustále vystavený činnosti pochybných aktérů. Azure IP adresy jsou dobře známé a hackerům průběžně sběru dat je pro útoky na otevřené porty 3389.
  - Pouze v zabezpečení sítě používá čas skupiny (Nsg) a příchozí pravidla tohoto limitu množství času, které konkrétní port je otevřený.
  - S za běhu povoleno, Security Center kontroluje, zda uživatel má přístup na základě role (RBAC) zápisu oprávnění k přístupu pro virtuální počítač. Kromě toho určete pravidla, jak můžou uživatelé připojit k virtuálním počítačům. Pokud jsou oprávnění OK, žádosti o přístup se schválí a Security Center je nakonfiguruje skupiny Nsg umožňuje příchozí provoz do vybrané porty množství času, který je zadat. Po uplynutí této doby se skupiny zabezpečení sítě vrátí do předchozího stavu.
- **Adaptivní řízení aplikací.** Chraňte virtuální počítače před škodlivým softwarem a malwarem tím, že budete pomocí dynamických seznamů povolených aplikací určovat, které aplikace se na nich spouštějí.
  - Adaptivní řízení aplikací umožňuje schvalovat aplikace a bránit neautorizovaným uživatelům nebo správcům instalovat na vaše virtuální počítače neschválené nebo neprověřené softwarové aplikace.
    - Můžete blokovat pokusy o spuštění škodlivých aplikací nebo na ně upozorňovat, bránit použití nežádoucích nebo škodlivých aplikací a zajistit dodržování zásady zabezpečení aplikací ve vaší organizaci.
- **Monitorování integrity souborů.** Dbejte na integritu souborů spuštěných ve virtuálních počítačích.
  - Problémy s virtuálním počítačem nemusí způsobit jenom nainstalovaný software. Změna souboru systému může také způsobit snížení selhání nebo výkonu virtuálních počítačů. Soubor integrity monitorování zkontroluje systémové soubory a nastavení registru pro změny a upozorní, pokud něco se aktualizuje.
  - Security Center doporučuje, které soubory, které jste měli byste sledovat.

**Víc se uč:**

- [Další informace](/azure/security-center/security-center-intro) o službě Azure Security Center.
- [Další informace](/azure/security-center/security-center-just-in-time) o právě přístup podle potřeby.
- [Další informace o](/azure/security-center/security-center-adaptive-application) použít adaptivní řízení aplikací.
- [Začněte pracovat](/azure/security-center/security-center-file-integrity-monitoring) s monitorováním integrity souborů.

## <a name="best-practice-encrypt-data"></a>Osvědčený postup: Šifrování dat

Šifrování dat tvoří důležitou součást postupů zabezpečení v Azure. Povolení šifrování na všech úrovních pomáhá zabránit neoprávněným stranám v získání přístupu k citlivým datům, včetně přenášených i neaktivních uložených dat.

### <a name="encryption-for-iaas"></a>Šifrování pro IaaS

- **Virtuální počítače:** U virtuálních počítačů můžete zašifrovat disky virtuálních počítačů IaaS s Windows nebo Linuxem pomocí služby Azure Disk Encryption.
  - Služba Disk Encryption za pomoci nástroje BitLocker pro Windows a DM-Crypt pro Linux zajišťuje šifrování disků s operačním systémem a daty.
  - Můžete použít šifrovací klíč vytvořený Azure nebo vlastní šifrovací klíče uchované ve službě Azure Key Vault.
  - Šifrování disků, se šifrují data virtuálních počítačů IaaS v klidovém stavu (na disk) a při spuštění virtuálního počítače.
    - Azure Security Center vás upozorní v případě, že některé z vašich virtuálních počítačů nejsou šifrované.
- **Úložiště:** Chraňte neaktivní data uložená ve službě Azure Storage.
  - Data uložená na účtech Azure Storage je možné šifrovat pomocí klíčů AES generovaných Microsoftem, které jsou kompatibilní se standardem FIPS 140-2, případně můžete použít i vlastní klíče.
  - Šifrování služby Storage je povolená pro všechny účty nová a existující úložiště a nejde zakázat.

### <a name="encryption-for-paas"></a>Šifrování pro PaaS

Na rozdíl od modelu IaaS, ve kterém spravujete virtuální počítače a infrastrukturu sami, u modelu PaaS spravuje platformu a infrastrukturu poskytovatel, takže se můžete plně soustředit na logiku aplikací a funkce. Vzhledem k tomu, že služeb PaaS existuje spousta typů, se každá služba pro účely zabezpečení vyhodnocuje zvlášť. Můžeme se například podívat, jak bychom povolili šifrování pro službu Azure SQL Database.

- **Funkce Always Encrypted:** Neaktivní uložená data aplikace SQL Server Management Studio můžete ochránit pomocí průvodce funkcí Always Encrypted.
  - Vytvoříte klíč Always Encrypted pro zašifrování dat v jednotlivých sloupcích.
  - Always Encrypted klíčů lze uložit jako šifrovaný v databázi metadat nebo uložené v důvěryhodného klíče úložišť, jako je Azure Key Vault.
  - K použití této funkce bude nejspíš potřeba provést změny aplikace.
- **Transparentní šifrování dat (TDE):** Chraňte službu Azure SQL Database pomocí transparentního šifrování a dešifrování databáze, souvisejících záloh a uložených souborů protokolů transakcí.
  - TDE umožňuje provádět šifrování bez změn ve vrstvě aplikace.
  - Transparentní šifrování dat můžete použít šifrovací klíče poskytovaných microsoftem, nebo můžete zadat vlastní klíče s využitím podpory vlastního klíče.

**Víc se uč:**

- [Další informace o](/azure/security/azure-security-disk-encryption-overview) Azure Disk Encryption pro virtuální počítače IaaS.
- [Povolit](/azure/security/azure-security-disk-encryption-windows) šifrování pro virtuální počítače IaaS s Windows.
- [Další informace o](/azure/storage/common/storage-service-encryption) šifrování služby Azure Storage pro neaktivní uložená data.
- [Čtení](/azure/sql-database/sql-database-always-encrypted-azure-key-vault) Přehled funkce Always Encrypted.
- [Přečtěte si informace o](/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-2017) transparentní šifrování dat pro službu Azure SQL Database.
- [Přečtěte si](/azure/sql-database/transparent-data-encryption-byok-azure-sql) o transparentním šifrování dat s využitím možnosti Bring Your Own Key.

## <a name="best-practice-protect-vms-with-antimalware"></a>Osvědčený postup: Ochrana virtuálních počítačů pomocí antimalwarového softwaru

Konkrétně starší verze virtuálních počítačů migrovaných do Azure nemusí mít nainstalovanou odpovídající úroveň antimalwarového softwaru. Azure poskytuje bezplatné řešení pro koncové body, které pomáhá chránit virtuální počítače proti virům, spywaru a dalšímu malwaru.

- Microsoft Antimalware pro Azure generuje výstrahy, když je známo, že škodlivý nebo nežádoucí software pokusí nainstalovat.
- Je řešení jednoho agenta, které běží na pozadí bez zásahu člověka.
- Ve službě Azure Security Center můžete snadno identifikovat virtuální počítače, které nemáte spuštění služby endpoint protection a podle potřeby instalaci Microsoft Antimalware.

![Antimalware pro virtuální počítače](./media/migrate-best-practices-security-management/antimalware.png)
*Antimalware pro virtuální počítače*

**Víc se uč:**

- Získejte [další informace](/azure/security/azure-security-antimalware) o řešení Microsoft Antimalware.

## <a name="best-practice-secure-web-apps"></a>Osvědčený postup: Zabezpečení webových aplikací

Migrované webové aplikace se setkávají s několika problémy:

- Většina starší verze webové aplikace obvykle obsahují citlivé informace v konfiguračních souborech. Soubory, které obsahují tyto informace mohou způsobovat potíže se zabezpečením, když jsou zálohované aplikací, nebo když kód aplikace je zaregistrované do nebo ze správy zdrojového kódu.
- Kromě toho, když migrujete webové aplikace obsažené ve virtuálním počítači, pravděpodobně i tento počítač přesouváte z místní sítě a prostředí chráněného bránou firewall do prostředí vystaveného internetu. Ujistěte se, že vytváříte řešení, které dokáže odvést stejnou práci jako ochranné prostředky v místním prostředí.

Azure poskytuje hned několik řešení:

- **Azure Key Vault:** Vývojáři webových aplikací se v dnešní době snaží dbát na to, aby z těchto souborů nemohly uniknout citlivé informace. Jeden ze způsobů, jak informace zabezpečit, spočívá v jejich extrakci ze souborů a uložení do služby Azure Key Vault.
  - Můžete centralizovat úložiště tajných částí aplikace pomocí služby Key Vault a řídit jejich distribuci. Informace o zabezpečení tak už nemusíte ukládat do souborů aplikací.
  - Aplikace můžou bezpečně získat přístup k informacím v trezoru pomocí identifikátorů URI, aniž by vyžadovaly vlastní kód.
  - Azure Key Vault umožňuje uzamknout přístup prostřednictvím ovládacích prvků zabezpečení Azure a bez problémů implementovat obnovování klíčů. Microsoft nemůže vaše data zobrazit ani extrahovat.
- **App Service Environment:** Pokud migrovaná aplikace potřebuje dodatečnou ochranu, můžete přidat prostředí App Service Environment a bránu firewall webových aplikací, které ochrání prostředky aplikace.
  - Azure App Service Environment poskytuje plně izolované a vyhrazené prostředí, ve kterém se spouštějí aplikace App Service, jako jsou webové aplikace pro Windows a Linux, kontejnery Dockeru, mobilní aplikace a funkce.
  - Tato služba je užitečná pro aplikace, které běží ve velmi velkém měřítku, vyžadují izolaci a zabezpečený přístup k síti nebo mají vysoké využití paměti.
- **Brána firewall webových aplikací:** Funkce služby Azure Application Gateway, která poskytuje centralizovanou ochranu webových aplikací.
  - Chrání webové aplikace bez nutnosti úprav back-endového kódu.
  - Dokáže za jednou bránou aplikací ochránit víc webových aplikací současně.
  - Brána firewall webových aplikací se dá monitorovat pomocí služby Azure Monitor a je integrovaná do Azure Security Center.

![Zabezpečení webových aplikací](./media/migrate-best-practices-security-management/web-apps.png)

*Azure Key Vault*

**Další informace:**

- [Podívejte se na přehled](/azure/key-vault/key-vault-overview) služby Azure Key Vault.
- [Získejte informace](/azure/application-gateway/waf-overview) o bráně firewall webových aplikací.
- [Přečtěte si úvod](/azure/app-service/environment/intro) do služby App Service Environment.
- [Zjistěte](/azure/key-vault/tutorial-web-application-keyvault), jak nakonfigurovat webovou aplikaci, aby četla tajné kódy ze služby Key Vault.
- [Získejte informace](/azure/application-gateway/waf-overview) o bráně firewall webových aplikací.

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Osvědčený postup: Kontrola předplatných a oprávnění prostředků

Během migrace úloh a jejich spouštění k Azure dochází k obměnám personálu s přístupem k těmto úlohám. Váš tým zabezpečení by měl přístup k vašemu tenantovi Azure a skupinám prostředků pravidelně kontrolovat. Azure nabízí možnosti správy identit a zabezpečení řízení přístupu, včetně řízení přístupu na základě role (RBAC), které umožňují autorizaci oprávnění pro přístup k prostředkům Azure.

- Řízení přístupu na základě role přiřazuje přístupová oprávnění k objektům zabezpečení. Objekty zabezpečení představuje uživatele, skupiny (skupinu uživatelů), instanční (identitu používanou aplikací a služeb) a spravovat identity (automaticky spravuje Azure identity Azure Active Directory).
- RBAC můžete přiřadit role principů zabezpečení, jako je například vlastník, Přispěvatel a Čtenář a role definice (kolekce oprávnění), které definují operace, které může role provádět.
- RBAC může také nastavit rozsahy určující hranice určité role. Rozsah se může nastavit na několika úrovních, třeba na úrovni skupiny pro správu, předplatného, skupiny prostředků nebo prostředku.
- Zajistěte, aby správci s přístupem k Azure měli přístup jenom k prostředkům, které mají povolené. Pokud předdefinované role v Azure nejsou dostatečně podrobné, můžete vytvořit vlastní role, které budou oddělovat a omezovat přístupová oprávnění.

![Řízení přístupu](./media/migrate-best-practices-security-management/subscription.png)
*řízení přístupu – IAM*

**Víc se uč:**

- [O](/azure/role-based-access-control/overview) RBAC.
- [Přečtěte si](/azure/role-based-access-control/role-assignments-portal) ke správě přístupu pomocí RBAC a webu Azure portal.
- Získejte [další informace](/azure/role-based-access-control/custom-roles) o vlastních rolích.

## <a name="best-practice-review-audit-and-security-logs"></a>Osvědčený postup: Kontrola protokolů auditu a zabezpečení

Azure Active Directory (Azure AD) poskytuje protokoly aktivit, které se zobrazují v Azure Monitoru. Protokoly zachycují operace provedené v architektuře tenantů Azure, čas jejich provedení a to, kdo je provedl.

- Protokoly auditu zobrazit historii úloh v tenantovi. Zobrazit, který provedl úlohy protokoly aktivit přihlašování.
- Přístup k sestavám zabezpečení závisí na vaší licenci služby Azure AD. Ve verzích Free a Basic získáte seznam rizikových uživatelů a přihlášení. Ve verzích Premium 1 a Premium 2 získáte informace o podkladových událostech.
- Protokoly aktivit můžete směrovat do různých koncových bodů za účelem dlouhodobého uchovávání nebo získávání přehledu o datech.
- Zvykněte si kontrolovat protokoly pravidelně nebo začněte používat nástroje pro správu akcí a informací o zabezpečení (SIEM), které budou automaticky kontrolovat abnormální hodnoty. Pokud nepoužíváte Premium 1 nebo 2, musíte udělat spoustu sami, nebo pomocí vašeho systému SIEM. K těmto analýzám patří vyhledávání rizikových přihlášení a událostí a dalších vzorců ukazujících na útok ze strany uživatelů.

![Uživatelé a skupiny](./media/migrate-best-practices-security-management/azure-ad.png)

*Uživatelé a skupiny Azure AD*

**Další informace:**

- [Další informace o](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor) protokoly aktivit Azure AD ve službě Azure Monitor.
- [Naučte se](/azure/active-directory/reports-monitoring/concept-audit-logs) provádět audit sestav aktivit na portálu Azure AD.

## <a name="best-practice-evaluate-other-security-features"></a>Osvědčený postup: Vyhodnocení dalších funkcí zabezpečení

Azure nabízí další funkce zabezpečení, které poskytují pokročilé možnosti zabezpečení. Některé z těchto osvědčených postupů vyžadují doplňkové licence a možnosti verze Premium.

- **Implementace jednotek pro správu (AU) Azure AD.** Delegování administrativních povinností na pracovníky podpory může být jen se základním řízením přístupu v Azure rizikové. Poskytnutí přístupu ke správě všech skupin v Azure AD pracovníkům podpory pravděpodobně není zrovna ideální přístup k zabezpečení na úrovni organizace. Použití AU umožňuje oddělit prostředků Azure do kontejnerů v podobným způsobem jako v místním organizační jednotky (OU). Použití AU AU správce musí mít licenci Azure AD premium. [Další informace](/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Použití vícefaktorového ověřování.** Pokud máte licenci Azure AD Premium, můžete u svých účtů správce povolit a vyžadovat vícefaktorové ověřování. Phishing je nejběžnější způsob, jakým dochází k ohrožení zabezpečení přihlašovacích údajů k účtům. Jakmile získá přihlašovací údaje k účtu správce pochybný aktér, nic mu nezabrání provést něco, co může mít dalekosáhlé důsledky, například odstranit všechny skupiny prostředků. Vícefaktorové ověřování můžete nastavit několika způsoby, například tak, aby využívalo e-mail, ověřovací aplikaci a textové zprávy. Jako správce si můžete vybrat nejméně rušivou možnost. Vícefaktorové ověřování se integruje s analýzami hrozeb a zásadami podmíněného přístupu a náhodně vyžaduje odpověď na výzvu k vícefaktorovému ověřování. Přečtěte si další informace o [zabezpečení](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) a o tom, [jak nastavit vícefaktorové ověřování](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementace podmíněného přístupu.** Ve většině malých a středně velkých organizací se správci Azure a tým podpory pravděpodobné nacházejí v jedné geografické oblasti. V takovém případě bude většina přihlášení pocházet ze stejných míst. Pokud jsou IP adresy těchto umístění poměrně statické, je celkem logické, že byste neměli vídat přihlášení správců z míst, která se nacházejí mimo tyto oblasti. Pro případ, že se pochybnému aktérovi podaří ohrozit zabezpečení přihlašovacích údajů správce, můžete implementovat funkce zabezpečení, jako je podmíněný přístup kombinovaný s vícefaktorovým ověřováním, abyste zabránili přihlášení ze vzdálených umístění nebo z podvodných umístění s náhodnými IP adresami. Získejte [další informace](/azure/active-directory/conditional-access/overview) o podmíněném přístupu a [projděte si osvědčené postupy](/azure/active-directory/conditional-access/best-practices) pro podmíněný přístup ve službě Azure AD.
- **Kontrola oprávnění podnikových aplikací.** V průběhu času můžou správci vybírat odkazy od Microsoftu a třetích stran, aniž by přesně věděli, jaký můžou mít dopad na organizaci. Odkazy můžou zobrazovat obrazovky pro vyjádření souhlasu, které přidělují oprávnění k aplikacím Azure a můžou umožnit přístup ke čtení dat služby Azure AD, nebo dokonce plný přístup ke správě celého předplatného Azure. Měli byste pravidelně kontrolovat aplikace, u kterých vaši správci a uživatelé povolili přístup k prostředkům Azure. Zajistěte, aby tyto aplikace měly jen nezbytně nutná oprávnění. Kromě toho můžete jednou za čtvrt nebo půl roku poslat uživatelům e-mail s odkazem na stránky aplikace, aby věděli, jakým aplikacím povolili přístup k datům organizace. [Další informace](/azure/active-directory/manage-apps/application-types) o typech aplikací, a [jak ovládací prvek](/azure/active-directory/manage-apps/remove-user-or-group-access-portal) přiřazení aplikací ve službě Azure AD.

## <a name="managed-migrated-workloads"></a>Spravované migrované úlohy

V této části doporučujeme některé osvědčené postupy pro správu Azure, včetně těchto:

- [Správa prostředků:](#best-practice-name-resource-groups) Osvědčené postupy pro skupiny prostředků a prostředky Azure, včetně inteligentního pojmenovávání, prevence nechtěného odstranění, správy oprávnění prostředků a efektivního označování prostředků.
- [Použití podrobných plánů:](#best-practice-implement-blueprints) Získejte rychlý přehled o použití podrobných plánů vytváření a správy prostředí nasazení.
- [Přehled architektur:](#best-practice-review-azure-reference-architectures) Podívejte se na ukázky na architektur Azure, ze kterých můžete čerpat poznatky při vytváření nasazení po migraci.
- [Nastavení skupin pro správu:](#best-practice-manage-resources-with-azure-management-groups) Pokud máte více předplatných, můžete je shromáždit do skupin pro správu a u těchto skupin uplatňovat nastavení zásad správného řízení.
- [Nastavení zásad přístupu:](#best-practice-deploy-azure-policy) Uplatňujte u svých prostředků Azure zásady dodržování předpisů.
- [Implementace strategie BCDR:](#best-practice-implement-a-bcdr-strategy) Sestavte si strategii pro provozní kontinuitu a zotavení po havárii (BCDR), která vám zajistí zabezpečení dat, odolnost prostředí a funkčnost prostředků i v případě, že dojde k výpadku.
- [Správa virtuálních počítačů:](#best-practice-use-managed-disks-and-availability-sets) Seskupte virtuální počítače do skupin dostupnosti, které zajistí odolnost a vysokou dostupnost. Pokud si navíc chcete usnadnit správu disků a úložišť virtuálních počítačů, použijte spravované disky.
- [Monitorování využití prostředků:](#best-practice-monitor-resource-usage-and-performance) Povolte protokolování diagnostiky pro prostředky Azure, vytvářejte upozornění a playbooky pro aktivní odstraňování potíží a používejte řídicí panel Azure, který nabízí jednotný pohled na stav vašeho nasazení.
- [Správa podpory a aktualizací:](#best-practice-manage-updates) Seznamte se s plánem podpory Azure a jeho implementací, získejte osvědčené postupy pro zajištění aktuálnosti virtuálních počítačů a zaveďte procesy správy změn.

## <a name="best-practice-name-resource-groups"></a>Osvědčený postup: Pojmenování skupin prostředků

Když budou mít vaše skupiny prostředků smysluplné názvy, které správci a členové týmu podpory snadno rozpoznají a zorientují se v nich, významně to přispěje ke zvýšení produktivity a efektivity.

- Doporučujeme dodržovat zásady vytváření názvů Azure.
- Pokud synchronizujete místní službu Active Directory do Azure AD pomocí nástroje Azure AD Connect, zamyslete se, jestli by nebylo vhodné přizpůsobit názvy místních skupin zabezpečení názvům prostředků v Azure.

![pojmenování](./media/migrate-best-practices-security-management/naming.png)

*Pojmenování skupin prostředků*

**Další informace:**

- [Získejte další informace](/azure/architecture/best-practices/naming-conventions) o zásadách vytváření názvů.

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Osvědčený postup: Implementace zámků odstranění pro skupiny prostředků

To poslední, co potřebujete, je nemoct najít některou skupinu prostředků, protože ji někdo omylem odstranil. Doporučujeme vám implementovat zámky odstranění, aby se takové nehody nestávaly.

![Zámky odstranění](./media/migrate-best-practices-security-management/locks.png)

*Zámky odstranění*

**Další informace:**

- [Získejte informace](/azure/azure-resource-manager/resource-group-lock-resources) o uzamknutí prostředků, které brání neočekávaným změnám.

## <a name="best-practice-understand-resource-access-permissions"></a>Osvědčený postup: Principy oprávnění pro přístup k prostředkům

Vlastník předplatného má přístup ke všem skupinám prostředků a prostředkům v rámci vašeho předplatného.

- Přidáte lidi střídmě tento cenný přiřazení. Principy následky tyto typy oprávnění je důležité pro zachování prostředí zabezpečené a stabilní.
- Ujistěte se, že umístíte do příslušné prostředky skupiny prostředků:
  - Prostředky se podobá životním cyklem odpovídat společně. V ideálním případě by neměli byste potřebovat přesunout prostředek, pokud musíte odstranit celou skupinu prostředků.
  - Prostředky, které podporují funkci nebo úlohy umístit společně pro zjednodušení správy.

**Víc se uč:**

- [Získejte informace](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise) o uspořádání předplatných a skupin prostředků.

## <a name="best-practice-tag-resources-effectively"></a>Osvědčený postup: Efektivní označování prostředků

Použití jenom názvu skupiny prostředků, který se vztahuje k prostředkům, často neposkytne dostatek metadat pro efektivní implementaci mechanismů, jako je interní fakturace nebo správa v rámci předplatného.

- Jako osvědčený postup používejte přidat užitečná metadata, která se jde dotazovat a ohlášeny chyby v Azure značky.
- Značky poskytují způsob, jak logicky uspořádat prostředky s vlastnostmi, které definujete. Značky lze použít ke skupinám prostředků nebo prostředky přímo.
- Značky lze použít pro skupinu prostředků nebo u jednotlivých prostředků. Prostředky v určité skupině nedědí značky dané skupiny prostředků.
- Přidělování značek můžete automatizovat pomocí PowerShellu nebo služby Azure Automation, případně můžete označovat jednotlivé skupiny a prostředky. Automatický nebo samoobslužný přístup ke značkám. Pokud máte zavedený systém správy požadavků a změn, můžete snadno použít informace v požadavcích k vytvoření značek prostředků specifických pro vaši společnost.

![Použití značek](./media/migrate-best-practices-security-management/tagging.png)
*Použití značek*

**Víc se uč:**

- [Další informace o](/azure/azure-resource-manager/resource-group-using-tags) označování a označit omezení.
- [Kontrola](/azure/azure-resource-manager/resource-group-using-tags#powershell) příklady prostředí PowerShell a rozhraní příkazového řádku k nastavení označování a chcete použít značky ze skupiny prostředků na prostředky.
- [Přečtěte si](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) osvědčené postupy vytváření značek v Azure.

## <a name="best-practice-implement-blueprints"></a>Osvědčený postup: Implementace podrobných plánů

Stejně jako technický nákres či podrobný plán (anglicky „blueprint“) umožňuje technikovi nebo architektovi načrtnout parametry návrhu projektu, služba Azure Blueprints umožňuje cloudovým architektům a centrálním oddělením IT definovat opakovatelnou sadu prostředků Azure, která implementuje a dodržuje standardy, vzory a požadavky organizace. Díky službě Azure Blueprints můžou vývojářské týmy rychle vytvářet nová prostředí, která vyhovují předpisům organizace a která obsahují sadu předdefinovaných komponent – třeba síťových – ke zrychlení vývoje a distribuce.

- Podrobné plány se dají použít k orchestraci nasazení skupin prostředků, šablon služby Azure Resource Manager a přiřazování zásad a rolí.
- Podrobné plány jsou uložené v globálně distribuované službě Azure Cosmos DB. Objekty podrobného plánu se replikují do několika oblastí Azure. Replikace poskytuje nízkou latenci, vysokou dostupnost a jednotný přístup k podrobný plán, bez ohledu na oblast, do které podrobný plán nasadí prostředků.

**Víc se uč:**

- [Čtení](/azure/governance/blueprints/overview) o podrobné plány.
- [Prohlédněte si](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) příklad podrobného plánu, který slouží k urychlení AI ve zdravotnictví.

## <a name="best-practice-review-azure-reference-architectures"></a>Osvědčený postup: Procházení referenčních architektur v Azure

Vytváření zabezpečených, škálovatelných a snadno spravovatelných úloh v Azure může být náročný úkol. Průběžné změny může být obtížné udržovat tempo s různými funkcemi pro optimální prostředí. S odkazem na Učte se od může být užitečné při navrhování a migraci vašich úloh. Azure a Azure partneři vytvořili několik ukázkové referenční architektury pro různé typy prostředí. Tyto ukázky jsou navržené tak poskytovat návrhy, které mohou být zdrojem cenných a sestavení.

Referenční architektury jsou uspořádané podle scénářů. Obsahují doporučené postupy a rady týkající se správy, dostupnosti, škálovatelnosti a zabezpečení.
Azure App Service Environment poskytuje plně izolované a vyhrazené prostředí, ve kterém se spouštějí aplikace App Service, včetně webových aplikací pro Windows a Linux, kontejnerů Dockeru, mobilních aplikací a funkcí. App Service přidá výkon Azure pro vaši aplikaci, se zabezpečení, Vyrovnávání zatížení, automatické škálování a automatizovanou správu. Můžete taky využít výhod její možnosti DevOps, jako jsou průběžné nasazování z Githubu, Správa balíčků, přípravná prostředí, vlastní domény a certifikáty SSL a Azure DevOps. App Service je užitečné pro aplikace, které potřebují izolace a bezpečný přístup k síti a ty, které používají vysoké množství paměti a dalších prostředků, které je potřeba škálovat.

**Víc se uč:**

- [Další informace o](/azure/architecture/reference-architectures) referenční architektury Azure.
- [Prohlédněte si](/azure/architecture/example-scenario) ukázkové scénáře Azure.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Osvědčený postup: Správa prostředků pomocí skupin pro správu Azure

Pokud má vaše organizace víc předplatných, musíte pro ně spravovat přístup, zásady a dodržování předpisů. Skupiny pro správu Azure představují úroveň rozsahu nad předplatnými.

- Předplatná uspořádáte do kontejnerů označovaných jako skupiny pro správu a na ně použijete své zásady správného řízení.
- Všechna předplatná ve skupině pro správu automaticky dědí podmínky příslušné skupiny pro správu.
- Skupiny pro správu umožňují správu na podnikové úrovni ve velkém měřítku bez ohledu na to, jaké typy předplatného máte.
- Můžete například použít zásadu skupiny pro správu, která omezuje oblasti, ve kterých se dají vytvářet virtuální počítače. Tato zásada se potom použije pro všechny skupiny pro správu, předplatná a prostředky v rámci dané skupiny pro správu.
- Můžete vytvořit flexibilní strukturu skupin pro správu a předplatných a uspořádat tak prostředky do hierarchie umožňující využít jednotné zásady a správu přístupu.

Následující diagram ukazuje příklad vytvoření hierarchie pro zásady správného řízení s využitím skupin pro správu.

![Skupiny pro správu](./media/migrate-best-practices-security-management/management-groups.png)
*skupin pro správu*

**Víc se uč:**

- [Přečtěte si víc](/azure/governance/management-groups/index) o uspořádání prostředků do skupin pro správu.

## <a name="best-practice-deploy-azure-policy"></a>Osvědčený postup: Nasazení Azure Policy

Azure Policy je služba v Azure, která slouží k vytváření, přiřazování a správě zásad.

- Zásady vynucují různá pravidla a efekty u vašich prostředků, aby tyto prostředky i nadále odpovídaly vašim firemním standardům a smlouvám o úrovni.
- Služba Azure Policy vyhodnotí prostředky, vyhledává ty, které nejsou kompatibilní s vašimi zásadami.
- Můžete například vytvořit zásadu, která umožňuje pouze určité velikosti skladové položky virtuálních počítačů ve vašem prostředí. Služba Azure Policy vyhodnotí toto nastavení při vytváření a aktualizaci prostředků a při kontrole stávajících prostředků.
- Azure poskytuje několik integrovaných zásad, které můžete přiřadit nebo můžete vytvořit svoje vlastní.

![Služba Azure Policy](./media/migrate-best-practices-security-management/policy.png)
*Azure Policy*

**Víc se uč:**

- [Získejte přehled](/azure/governance/policy/overview) o službě Azure Policy.
- [Získejte in](/azure/governance/policy/tutorials/create-and-manage) o vytváření a správě zásad, které umožňují prosazovat dodržování předpisů.

## <a name="best-practice-implement-a-bcdr-strategy"></a>Osvědčený postup: Implementace strategie BCDR

Plánování provozní kontinuity a zotavení po havárii (BCDR) je zásadně důležitý úkon, který byste měli provést během procesu plánování migrace do Azure. Řečeno jazykem práva, vaše smlouvy můžou zahrnovat doložku o zásazích vyšší moci, která vás zbavuje závazků v případě zásahu vyšší moci, například hurikánu nebo zemětřesení. Zároveň ale máte určité závazky týkající se vaší schopnosti zajistit v případě přírodní katastrofy funkčnost služeb a v případě potřeby provést jejich obnovení. Tato schopnost může rozhodnout o budoucnosti vaší společnosti.

Obecně řečeno by vaše strategie BCDR měla zahrnovat tyto body:

- **Zálohování dat:** Jak uchovávat data v bezpečí, abyste je mohli snadno obnovit, pokud dojde k výpadku.
- **Zotavení po havárii:** Jak zajistit odolnost a dostupnost aplikací v případě výpadku.

### <a name="set-up-bcdr"></a>Nastavení BCDR

Při migraci do Azure je důležité pochopit, že i když platforma Azure poskytuje integrované funkce zajišťující odolnost, je potřeba navrhnout nasazení Azure tak, aby využívalo funkce a služby Azure, které poskytují vysokou dostupnost, zotavení po havárii a zálohování.

- Vaše řešení BCDR bude záviset na cílech vaší společnosti a na vaší strategii nasazení v Azure. U nasazení využívajících model infrastruktury jako služby (IaaS) a platformy jako služby (PaaS) existují z hlediska BCDR odlišné výzvy.
- Jakmile vytvoříte řešení BCDR, měli byste je pravidelně testovat a kontrolovat, jestli je vaše strategie pořád vhodná.

### <a name="back-up-an-iaas-deployment"></a>Zálohování nasazení IaaS

Ve většině případů se místní úlohy po migraci vyřadí z provozu a strategii zálohování dat, kterou jste používali v místním prostředí, je potřeba rozšířit nebo nahradit. Pokud do Azure migrujete celé datacentrum, budete muset navrhnout a implementovat řešení úplného zálohování využívající technologie Azure nebo integrovaná řešení třetích stran.

U úloh běžících na virtuálních počítačích IaaS Azure můžete zvážit tato řešení zálohování:

- **Azure Backup:** Poskytuje zálohy konzistentní s aplikacemi pro virtuální počítače Azure s Windows a Linuxem.
- **Snímky úložiště:** Vytváří se snímky úložiště objektů blob.

#### <a name="azure-backup"></a>Azure Backup

Azure Backup vytváří body obnovení dat, které se ukládají do služby Azure Storage. Azure Backup může zálohovat disky virtuálních počítačů Azure a soubory služby Azure Files (ve verzi Preview). Služba soubory Azure poskytují sdílené složky v cloudu, přístupné přes protokol SMB.

Azure Backup můžete použít k zálohování virtuálních počítačů několika způsoby.

- **Přímé zálohování z nastavení virtuálního počítače.** Virtuální počítače můžete pomocí Azure Backup zálohovat přímo z možností daného virtuálního počítače na webu Azure Portal. Virtuální počítač můžete zálohovat jednou denně a podle potřeby obnovit jeho disk. Azure Backup vytváří snímky dat s podporou aplikací (VSS) a na virtuální počítač se tedy neinstaluje žádný agent.
- **Přímé zálohování v trezoru služby Recovery Services.** Virtuální počítače IaaS můžete zálohovat nasazením trezoru Azure Backup Recovery Services. Ten poskytuje jedno umístění pro sledování a správu záloh a také podrobné možnosti zálohování a obnovení. Zálohování probíhá na úrovni souborů/složek až třikrát denně. Nezahrnuje podporu aplikací a nepodporuje Linux. Na každý virtuální počítač, který chcete zálohovat pomocí této metody, nainstalujte agenta MARS (Microsoft Azure Recovery Services).
- **Ochrana virtuálního počítače pomocí Azure Backup Serveru.** Azure Backup Server je ve službě Azure Backup k dispozici zdarma. Virtuální počítač se zálohuje do místního úložiště Azure Backup Serveru. Azure Backup Server potom zálohujete do Azure ve formě trezoru. Zálohování zahrnuje podporu aplikací a nabízí plnou kontrolu nad četností zálohování a dobou uchovávání záloh. Můžete zálohovat na úrovni aplikace, například zálohovat SQL Server nebo SharePoint.

Z důvodu zabezpečení Azure Backup průběžně šifruje data pomocí AES 256 a posílá je do Azure přes protokol HTTPS. Zálohovaná neaktivní uložená data v Azure se šifrují pomocí [šifrování služby Storage (SSE)](/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), včetně dat pro přenos a uložení.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
*Azure Backup*

**Víc se uč:**

- [Další informace o](/azure/backup/backup-introduction-to-azure-backup) různých typech zálohování.
- [Plánování infrastruktury zálohování](/azure/backup/backup-azure-vms-introduction) pro virtuální počítače Azure.

#### <a name="storage-snapshots"></a>Snímky úložiště

Virtuální počítače Azure jsou uložené jako objekty BLOB stránky ve službě Azure Storage.

- Snímky zachycují stav objektů blob v konkrétním bodě v čase.
- Jako alternativní záložní metoda pro disky virtuálních počítačů Azure můžete pořídit snímek úložiště objektů BLOB a zkopírujte je do jiného účtu úložiště.
- Můžete zkopírovat celý objekt blob, nebo použijte přírůstkový snímek kopírování pro kopírování jenom rozdílové změny a zmenšení prostoru úložiště.
- Jako další opatření můžete povolit obnovitelného odstranění pro účty blob storage. Když je tato funkce povolená, odstraněné objekty blob se označí k odstranění, ale hned se nevyprázdní. Během přechodného období se dá objekt blob ještě obnovit.

**Další informace:**

- [Další informace o](/azure/storage/blobs/storage-blobs-introduction) úložiště objektů blob v Azure.
- [Zjistěte, jak](/azure/storage/blobs/storage-blob-snapshots) vytvořit snímek objektu blob.
- [Projděte si ukázkový scénář](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) pro zálohování úložiště objektů blob.
- [Přečtěte si](/azure/storage/blobs/storage-blob-soft-delete) o obnovitelném odstranění.
- [Zotavení po havárii a vynucené převzetí služeb při selhání (Preview) ve službě Azure Storage](/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

#### <a name="third-party-backup"></a>Řešení zálohování třetích stran

Kromě toho můžete použít řešení třetích stran pro zálohování virtuálních počítačů Azure a kontejnery úložiště do místního úložiště nebo jiných poskytovatelů cloudových služeb. [Získejte další informace](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1) o řešeních zálohování na webu Azure Marketplace.

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Nastavení zotavení po havárii pro aplikace IaaS

Vedle ochrany dat musí strategie provozní kontinuity a zotavení po havárii (BCDR) myslet na to, jak zajistit dostupnost aplikací a úloh v případě havárie. U úloh běžících na virtuálních počítačích IaaS Azure a v Azure Storage můžete zvážit tato řešení zálohování:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery je primární služby Azure pro zajištění, které virtuální počítače Azure mohou být přepne do online režimu a aplikací virtuálního počítače k dispozici, když dojde k výpadku.

Site Recovery replikuje virtuální počítače z primární do sekundární oblasti Azure. V případě náhlé havárie převzetí služeb při selhání virtuálních počítačů z primární oblasti a i nadále přístup je k běžným způsobem v sekundární oblasti. Když se provoz vrátí do normálu, můžete služby virtuálních počítačů navrátit do primární oblasti.

![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)

*Site Recovery*

**Další informace:**

- [Kontrola](/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) scénáře zotavení po havárii pro virtuální počítače Azure.
- [Zjistěte](/azure/site-recovery/azure-to-azure-replicate-after-migration), jak po migraci nastavit u virtuálního počítače v Azure zotavení po havárii.

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Osvědčený postup: Použití spravovaných disků a skupin dostupnosti

Azure logicky seskupuje virtuální počítače do skupin dostupnosti a virtuální počítače v určité skupině izoluje od ostatních prostředků. Virtuální počítače ve skupině dostupnosti jsou rozptýlené do víc domén selhání s oddělenými subsystémy, aby byly chráněné před místními selháními, a jsou taky rozptýlené do víc aktualizačních domén, aby se všechny virtuální počítače ve stejné skupině nerestartovaly ve stejnou chvíli.

Spravované disky Azure zjednodušují správu disků virtuálních počítačů Azure IaaS tím, že spravují účty úložiště přidružené k diskům virtuálních počítačů.

- Pokud je to možné, doporučujeme používat spravované disky. Stačí jenom zadat typ úložiště, které chcete použít a jaké velikosti disku potřebujete, a Azure vytvoří a spravuje disk za vás na pozadí.
- Můžete převést existující disky jej spravovat.
- Měli byste vytvořit virtuální počítače do skupiny dostupnosti z důvodu vysoké odolnosti a dostupnosti. Pokud dojde k plánovanému nebo neplánovanému výpadku, skupiny dostupnosti zajistí, aby byl dál dostupný aspoň jeden virtuální počítač ze skupiny.

![Spravované disky](./media/migrate-best-practices-security-management/managed-disks.png)

*Spravované disky*

**Další informace:**

- [Získejte přehled](/azure/virtual-machines/windows/managed-disks-overview) spravovaných disků.
- [Další informace o](/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks) převod na spravované disky.
- [Naučte se](/azure/virtual-machines/windows/manage-availability) spravovat dostupnost virtuálních počítačů s Windows v Azure.

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Osvědčený postup: Monitorování využití a výkonu prostředků

Možná jste přesunuli úlohy do Azure kvůli obrovským možnostem škálování, které tato platforma nabízí. Přesun úloh však ale neznamená, že Azure bude automaticky provádět škálování bez nutnosti váš vstup. Jako příklad:

- Pokud organizaci marketingové nabízených oznámení nové oznámení TV, která řídí provoz 300 % další, to může způsobit problémy s dostupností lokality. Nově vydaný, migrovaný úloha pravděpodobně dojde k přiřazené limity a havárií.
- Dalším příkladem můžou být distribuované útoky (DDoS) denial-of-service na migrovanou pracovní zátěž. V tomto případě není vhodné pro škálování, ale zdroj útoků zabránit v dosažení vašich prostředků.

Tyto dva případy mají různá řešení, ale pro obě budete potřebovat přehled o tom, co se děje s monitorování výkonu a využití.

- Azure Monitor může pomoct tyto metriky a poskytne odpověď výstrahy, automatické škálování, služby event hubs, logic apps a další.
- Kromě monitorování Azure, můžete integrovat aplikace třetích stran SIEM pro monitorování Azure protokoly pro události auditu a výkonu.

![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
*Azure Monitor*

**Víc se uč:**

- [Další informace o](/azure/azure-monitor/overview) Azure Monitor.
- [Získejte doporučené postupy](/azure/architecture/best-practices/monitoring) pro monitorování a diagnostiku.
- [Další informace o](/azure/architecture/best-practices/auto-scaling) automatického škálování.
- [Zjistěte](/azure/security-center/security-center-export-data-to-siem), jak směrovat data z Azure do nástroje SIEM.

## <a name="best-practice-enable-diagnostic-logging"></a>Osvědčený postup: Povolení protokolování diagnostiky

Prostředky Azure generují značný počet metrik protokolování a telemetrických dat.

- Ve výchozím nastavení většina typů prostředků nemají povolené protokolování diagnostiky.
- Povolením protokolování diagnostiky napříč vašimi prostředky můžete dotazovat data protokolování a vytvářet výstrahy a na jejím základě playbooky.
- Když povolíte protokolování diagnostiky, každý zdroj bude mít konkrétní sadu kategorií. Vyberete jednu nebo víc kategorií protokolování a umístění pro data protokolu. Protokoly je možné odesílat do účtu úložiště, do centra událostí nebo do protokolů služby Azure Monitor.

![Protokolování diagnostiky](./media/migrate-best-practices-security-management/diagnostics.png)
*Protokolování diagnostiky*

**Víc se uč:**

- [Další informace o](/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) shromažďování a používání dat protokolu.
- [Zjistěte](/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema), jaká podpora je dostupná pro protokolování diagnostiky.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Osvědčený postup: Nastavení výstrah a playbooků

Když u prostředků Azure povolíte protokolování diagnostiky, můžete začít na základě dat protokolů vytvářet vlastní výstrahy.

- Proaktivně upozornění se zobrazí při podmínky se nacházejí ve vašich dat z monitorování. Potom mohli vyřešit problémy dříve, než uživatelé systému Všimněte si, že je. Může upozornit na věci, jako je hodnoty metriky, vyhledávací dotazy protokolů, události protokolu aktivit, platforma stav a dostupnost webu.
- Když se aktivují upozornění, můžete spustit Playbook aplikace logiky. Playbooku vám umožní automatizovat a orchestrovat reakci na určité upozornění. Playbooky jsou založené na Azure Logic Apps. Šablony aplikace logiky můžete vytvořit playbooky, nebo vytvořte svoje vlastní.
- Jako jednoduchý příklad můžete vytvořit výstrahu, která se aktivuje, když kontroly portu zranitelnosti skupinu zabezpečení sítě. Můžete nastavit playbooku, který spouští a zamezí IP adresa původu kontroly.
- Dalším příkladem mohou být aplikace pomocí nevracení paměti. Když do určité míry získá využití paměti, můžete provést recyklaci playbooku procesu.

![Výstrahy](./media/migrate-best-practices-security-management/alerts.png)
*výstrahy*

**Víc se uč:**

- [Další informace o](/azure/monitoring-and-diagnostics/monitoring-overview-alerts) výstrahy.
- [Získejte informace](/azure/security-center/security-center-playbooks) o playboocích zabezpečení, které reagují na výstrahy služby Security Center.

## <a name="best-practice-use-the-azure-dashboard"></a>Osvědčený postup: Použití řídicího panelu Azure

Azure Portal je jednotná webová konzola, která umožňuje vytvářet, spravovat a sledovat všechno od jednoduchých webových aplikací až po složité cloudové aplikace. Zahrnuje přizpůsobitelné řídicí panely a možnosti usnadnění.

- Můžete vytvořit více řídicích panelů a sdílet je s ostatními uživateli, kteří mají přístup k předplatným Azure.
- V tomto modelu sdílené má váš tým Přehled prostředí Azure, což jim umožní provádět proaktivně při správě systémy v cloudu.

![Řídicí panel Azure](./media/migrate-best-practices-security-management/dashboard.png)
*řídicí panel Azure*

**Víc se uč:**

- [Zjistěte, jak](/azure/azure-portal/azure-portal-dashboards) vytvoření řídicího panelu.
- [Získejte informace](/azure/azure-portal/azure-portal-dashboards-structure) o struktuře řídicích panelů.

## <a name="best-practice-understand-support-plans"></a>Osvědčený postup: Principy plánů podpory

Dřív nebo později nastane situace, kdy budete potřebovat spolupracovat s pracovníky podpory ve vaší společnosti nebo s pracovníky podpory Microsoftu. Je zásadně důležité mít vytvořenou sadu zásad a postupů podpory pro případy, jako je zotavení po havárii. Kromě toho by měli vaši správci a pracovníci podpory umět tyto zásady implementovat.

- V nepravděpodobném případě, že vaši úlohu ovlivní nějaký problém se službou Azure, by měli správci vědět, jak co nejlépe a nejefektivněji odeslat Microsoftu lístek podpory.
- Seznamte se s různými plány podpory, které Azure nabízí. V rozsahu od doby odezvy vyhrazený pro vývojáře instancí na plán Premier support s dobou odezvy kratší než 15 minut.

![Plány podpory](./media/migrate-best-practices-security-management/support.png)
*plány podpory*

**Víc se uč:**

- [Získejte přehled](https://azure.microsoft.com/support/options) plány podpory Azure.
- [Získejte informace](https://azure.microsoft.com/support/legal/sla) o smlouvách o úrovni služeb (SLA).

## <a name="best-practice-manage-updates"></a>Osvědčený postup: Správa aktualizací

Provádění pravidelných aktualizací operačního systému a softwaru virtuálních počítačů Azure představuje nesmírně náročný úkol. Možnost prezentovat všechny virtuální počítače k tomu, které aktualizace, které potřebují a o automaticky nasdílení změn je velmi důležité tyto aktualizace.

- Správa aktualizací ve službě Azure Automation můžete použít ke správě aktualizací operačního systému pro počítače s Windows a Linuxem počítačů, které jsou nasazené v Azure, místně a v jiných poskytovatelů cloudových služeb.
- Update Management můžete rychle vyhodnotit stav dostupných aktualizací na všech počítačích agenta a spravovat instalaci aktualizací.
- Můžete povolit správu aktualizací pro virtuální počítače přímo z účtu Azure Automation. Můžete také aktualizovat jenom jeden virtuální počítač z virtuálního počítače stránky na webu Azure Portal.
- Kromě toho virtuální počítače Azure lze registrovat pomocí nástroje System Center Configuration Manager. Může migrace úloh nástroje Configuration Manager do Azure a provádět vytváření sestav a aktualizací softwaru z jediného webového rozhraní.

![Aktualizace virtuálního počítače](./media/migrate-best-practices-security-management/updates.png)
*aktualizace*

**Víc se uč:**

- [Další informace o](/azure/automation/automation-update-management) update management v Azure.
- [Zjistěte, jak](/azure/automation/oms-solution-updatemgmt-sccmintegration) integrovat správu aktualizací nástroje Configuration Manager.
- [Nejčastější dotazy](/sccm/core/understand/configuration-manager-on-azure) o Configuration Manageru v Azure.

## <a name="implement-a-change-management-process"></a>Implementace procesu správy změn

Jak už to u produkčních systémů bývá, jakákoli změna může ovlivnit celé prostředí. Cenný přírůstkem do vašeho migrovaného prostředí tedy může být proces správy změn, který vyžaduje odesílání žádostí o změny v produkčních systémech.

- Můžete sestavit nejlepší postup rozhraní pro zvýšení povědomí ve Správci a pracovníci podpory úroveň řízení změn.
- Pomocí Azure Automation může pomoct se správou konfigurace a sledování změn pro migrované pracovních postupů.
- Při vynucování procesu správy změn, můžete použít protokolů auditu Azure změnit propojení protokoly pravděpodobně (nebo nemusíte) existující žádosti o změnu. Když pak uvidíte, že došlo ke změně bez odeslání příslušné žádosti o změnu, můžete začít zjišťovat, co se v procesu stalo.

Azure řešení sledování změn v rámci služby Azure Automation:

- Řešení sleduje změny softwaru a souborů systému Windows a Linux, klíčů registru Windows, služeb Windows a linuxových démonů.
- Změny na monitorovaných serverech se odesílají ke zpracování do služby Azure Monitor v cloudu.
- Na přijatá data se aplikuje logika a cloudová služba data zaznamená.
- Na řídicím panelu řešení Change Tracking můžete snadno zobrazit změny, které byly provedeny v serverové infrastruktuře.

![Správa změn](./media/migrate-best-practices-security-management/change.png)
*Správa změn*

**Víc se uč:**

- [Další informace o](/azure/automation/automation-change-tracking) Change Tracking.
- [Další informace o](/azure/automation/automation-intro) možnosti Azure Automation.

## <a name="next-steps"></a>Další postup

Přečtěte si doporučené postupy:

- [Osvědčené postupy](migrate-best-practices-networking.md) sítě po migraci.
- [Osvědčené postupy](migrate-best-practices-costs.md) cost Management po migraci.
