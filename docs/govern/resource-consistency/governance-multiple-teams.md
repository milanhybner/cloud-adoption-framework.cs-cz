---
title: Návrh zásad správného řízení v Azure pro více týmů
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pokyny pro konfiguraci řízení zásad správného řízení Azure pro více týmů, více úloh a více prostředí.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8c052b5a9c3745a1d253b533086a9fdf4d86eae9
ms.sourcegitcommit: 945198179ec215fb264e6270369d561cb146d548
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2019
ms.locfileid: "71967803"
---
# <a name="governance-design-for-multiple-teams"></a>Návrh zásad správného řízení pro několik týmů

Cílem těchto pokynů je pomoci naučit se postup navrhování modelu zásad správného řízení prostředků v Azure za účelem podpory více týmů, více úloh a více prostředí. Nejdřív se podíváte na sadu hypotetických požadavků zásad správného řízení a potom si Projděte několik ukázkových implementací, které tyto požadavky splňují.

Požadavky:

- Enterprise plánuje přecházet nové cloudové role a zodpovědnosti na skupinu uživatelů, takže vyžaduje správu identit pro více týmů s různými požadavky na přístup k prostředkům v Azure. Tento systém správy identit je nutný k uložení identity následujících uživatelů:
  - Jednotlivec ve vaší organizaci zodpovědný za vlastnictví **předplatných**.
  - Osoba ve vaší organizaci, která je odpovědná za **prostředky sdílené infrastruktury** používané pro připojení místní sítě k virtuální síti Azure.
  - Dva uživatelé ve vaší organizaci odpovědní za správu **úloh**.
- Podpora více **prostředí**. Prostředí je logické seskupení prostředků, jako jsou virtuální počítače, virtuální sítě a služby směrování provozu sítě. Tyto skupiny prostředků mají podobné požadavky na správu a zabezpečení a jsou obvykle používány pro konkrétní účel, jako je testování nebo produkce. V tomto příkladu je požadavek pro čtyři prostředí:
  - **Prostředí sdílené infrastruktury** , které zahrnuje prostředky sdílené úlohami v jiných prostředích. Například virtuální síť s podsítí brány, která poskytuje připojení místně.
  - **Produkční prostředí** s nejpřísnějšími zásadami zabezpečení. Může zahrnovat interní nebo externí úlohy.
  - **Neprodukční prostředí** pro vývoj a testování práce. Toto prostředí má zásady zabezpečení, dodržování předpisů a nákladů, které se liší od těch, které jsou v produkčním prostředí. V Azure to má podobu Enterprise pro vývoj/testování předplatného.
  - **Prostředí izolovaného prostoru (sandbox)** pro testování konceptu a vzdělávání. Toto prostředí se obvykle přiřazuje jednomu zaměstnanci, který se účastní vývoje aktivit a má přísné procesní a provozní kontrolní mechanismy, aby se zabránilo vybudování firemních dat. V Azure mají tyto předplatné formu předplatných sady Visual Studio. Tato předplatná by _se taky neměla_ přivázat k podnikovým Azure Active Directory.
- **Model oprávnění s minimálním** oprávněním, ke kterému nemají uživatelé ve výchozím nastavení žádná oprávnění. Model musí podporovat následující:
  - Jeden důvěryhodný uživatel (kvazi účet služby) v oboru předplatného s oprávněním k přiřazení přístupových práv k prostředkům.
  - Každému vlastníkovi úlohy je ve výchozím nastavení odepřen přístup k prostředkům. Přístupová práva k prostředkům jsou výslovně udělena jedním důvěryhodným uživatelem v oboru skupiny prostředků.
  - Přístup pro správu prostředků sdílené infrastruktury omezený na vlastníci sdílené infrastruktury
  - Přístup pro správu pro každé zatížení omezený na vlastníka úlohy (v produkčním prostředí) a zvýšení úrovně řízení jako vývoj se zvyšuje od vývoje k testování na fázi výroby.
  - Společnost nechce spravovat role nezávisle na těchto třech hlavních prostředích, proto vyžaduje použití jenom [integrovaných rolí](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) dostupných v Azure řízení přístupu na základě role (RBAC). Pokud organizace naprosto vyžaduje vlastní role RBAC, budete potřebovat další procesy pro synchronizaci vlastních rolí v rámci tří prostředí.
- Sledování nákladů podle názvu vlastníka úlohy, prostředí nebo obojího.

## <a name="identity-management"></a>Správa identit

Než budete moct navrhovat správu identit pro model zásad správného řízení, je důležité pochopit čtyři hlavní oblasti, které zahrnuje:

- **Řízení** Procesy a nástroje pro vytváření, úpravy a odstraňování identity uživatele.
- **Přihlašovací** Ověřování identity uživatele pomocí ověřování přihlašovacích údajů, jako je uživatelské jméno a heslo.
- **Authorization:** Určení prostředků, ke kterým má ověřený uživatel přístup, nebo operací, ke kterým mají oprávnění provádět.
- **Auditování** Pravidelně kontrolujte protokoly a další informace a zjistěte problémy zabezpečení související s identitou uživatele. To zahrnuje kontrolu na podezřelé vzorce používání, pravidelnou kontrolu uživatelských oprávnění, abyste ověřili, že jsou správné a další funkce.

Služba Azure pro identitu důvěřuje jenom jedné službě, která je Azure Active Directory (Azure AD). Do Azure AD přidáte uživatele a použijete je pro všechny výše uvedené funkce. Než se naučíte konfigurovat Azure AD, je důležité pochopit privilegované účty, které se používají ke správě přístupu k těmto službám.

Pokud se vaše organizace zaregistrovala k účtu Azure, byl přiřazen alespoň jeden **vlastník účtu** Azure. Taky se vytvořil **tenant** Azure AD, pokud už stávající tenant není přidružený k používání jiných služeb Microsoftu, jako je třeba Office 365. **Globální správce** s úplnými oprávněními k TENANTOVI Azure AD byl přidružen při vytvoření.

Identity uživatelů pro vlastníka účtu Azure i globálního správce služby Azure AD jsou uložené ve vysoce zabezpečeném systému identit, který je spravovaný Microsoftem. Vlastník účtu Azure má oprávnění k vytváření, aktualizaci a odstraňování předplatných. Globální správce Azure AD má oprávnění provádět mnoho akcí v Azure AD, ale v tomto průvodci se zaměříte na vytváření a odstraňování identity uživatelů.

> [!NOTE]
> Vaše organizace už může mít existujícího tenanta Azure AD, pokud máte k vašemu účtu existující licenci Office 365, Intune nebo Dynamics.

Vlastník účtu Azure má oprávnění k vytváření, aktualizaci a odstraňování předplatných:

účet ![Azure se správcem účtů Azure a globálním správcem Azure AD @ no__t-1*Obrázek 1 – účet Azure se správcem účtů a globálním správcem služby Azure AD.*

**Globální správce** Azure AD má oprávnění k vytváření uživatelských účtů:

účet ![Azure se správcem účtů Azure a globálním správcem Azure AD @ no__t-1*Obrázek 2 – globální správce Azure AD vytvoří v tenantovi požadované uživatelské účty.*

První dva účty, vlastník **úlohy app1** a **vlastník úlohy app2** jsou spojené s jednotlivcem ve vaší organizaci, který je zodpovědný za správu úlohy. Účet **síťových operací** vlastní osoba, která je zodpovědná za sdílené prostředky infrastruktury. Nakonec je účet **vlastníka předplatného** přidružený k osobě zodpovědné za vlastnictví předplatných.

## <a name="resource-access-permissions-model-of-least-privilege"></a>Model oprávnění přístupu k prostředkům s nejnižším oprávněním

Teď, když jste vytvořili váš systém správy identit a uživatelské účty, se musíte rozhodnout, jak u každého účtu použít role řízení přístupu na základě rolí (RBAC), aby se podporoval model oprávnění s nejnižší úrovní oprávnění.

Existuje další požadavek, který uvádí, že prostředky přidružené ke každé úloze jsou izolované od sebe, takže nikdo jiný vlastník úlohy nemá přístup pro správu k žádným jiným úlohám, které nevlastní. Je taky potřeba implementovat tento model jenom pomocí integrovaných rolí řízení přístupu na základě role Azure.

Každá role RBAC se používá v jednom ze tří oborů v Azure: **předplatné**, **Skupina prostředků**a pak jeden **prostředek**. Role jsou zděděné v nižších oborech. Pokud má uživatel například přiřazenou [předdefinovanou roli vlastníka](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) na úrovni předplatného, tato role je přiřazená i pro daného uživatele ve skupině prostředků a na úrovni jednotlivých prostředků, pokud není přepsána.

Proto pokud chcete vytvořit model s nejnižším oprávněním, je nutné určit akce, které může určitý typ uživatele provést v každém z těchto tří oborů. Požadavek je například na to, aby vlastník úlohy měl oprávnění ke správě přístupu pouze k prostředkům přidruženým ke svým úlohám a žádnému z dalších. Pokud jste přidělili integrovanou roli vlastníka v oboru předplatného, bude mít každý vlastník úlohy přístup pro správu ke všem úlohám.

Pojďme se podívat na dva příklady modelů oprávnění, abyste tento koncept pochopili trochu lépe. V prvním příkladu model důvěřuje jenom správci služby a vytvoří skupiny prostředků. V druhém příkladu model přiřadí předdefinované role vlastníka pro každého vlastníka úlohy v oboru předplatného.

V obou příkladech je k dispozici Správce služby předplatného, kterému je přiřazena předdefinovaná role vlastníka v oboru předplatného. Odvolat, že předdefinovaná role vlastníka uděluje všechna oprávnění, včetně správy přístupu k prostředkům.
@no__t – Správce služby 0subscription s rolí vlastníka @ no__t-1*Obrázek 3 – předplatné se správcem služeb přiřadilo integrovanou roli vlastníka.*

1. V prvním příkladu je **vlastníkem úlohy A** bez oprávnění v oboru předplatného – nemají ve výchozím nastavení žádná práva pro správu přístupu k prostředkům. Tento uživatel chce nasadit a spravovat prostředky pro své úlohy. Musí požádat **Správce služby** o vytvoření skupiny prostředků.
    @no__t – vlastník 0workload žádá o vytvoření skupiny prostředků A @ no__t-1.
2. **Správce služby** zkontroluje svůj požadavek a vytvoří **skupinu prostředků a**. V tuto chvíli **vlastník úlohy** stále nemá oprávnění dělat cokoli.
    @no__t – správce 0service vytvoří skupinu prostředků A @ no__t-1.
3. **Správce služby** přidá **vlastníka úlohy a** do **skupiny prostředků** a a přiřadí [integrovanou roli přispěvatele](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Role přispěvatele uděluje všechna oprávnění pro **skupinu prostředků A** s výjimkou oprávnění ke správě přístupu.
    @no__t – správce 0service přidá vlastníka úlohy a do skupiny prostředků a @ no__t-1.
4. Řekněme, že **vlastník úlohy A** má požadavek na pár členů týmu, aby zobrazili data monitorování procesoru a sítě v rámci plánování kapacity pro zatížení. Vzhledem k tomu, že **vlastník úlohy a** má přiřazenou roli přispěvatel, nemají oprávnění přidat uživatele do **skupiny prostředků a**. Tyto požadavky musí odeslat **Správci služby**.
    @no__t – do skupiny prostředků @ no__t-1 se přidají přispěvatelé žádostí o vlastnictví pro 0workload.
5. **Správce služby** tuto žádost zkontroluje a přidá dva uživatele **Přispěvatel úloh** do **skupiny prostředků a**. Ani jeden z těchto dvou uživatelů nevyžaduje oprávnění ke správě prostředků, takže jim byla přiřazena [integrovaná role čtenáře](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor).
    @no__t – správce 0service přidá přispěvatele úloh do skupiny prostředků A @ no__t-1.
6. V dalším kroku **vlastník úlohy B** také vyžaduje, aby skupina prostředků obsahovala prostředky pro jejich úlohy. Stejně jako **vlastník úlohy a**, **vlastník úlohy B** zpočátku nemá oprávnění k provedení jakékoli akce v oboru předplatného, takže musí odeslat žádost **Správci služby**.
    ![workload vlastník B vyžádá vytvoření skupiny prostředků B @ no__t-1.
7. **Správce služby** zkontroluje požadavek a vytvoří **skupinu prostředků B**.  @no__t – správce 0Service vytvoří skupinu prostředků B @ no__t-1.
8. **Správce služby** pak přidá **vlastníka úlohy b** do **skupiny prostředků b** a přiřadí integrovanou roli přispěvatele.
    @no__t – správce 0Service přidá vlastníka úlohy B do skupiny prostředků B @ no__t-1.

V tomto okamžiku jsou jednotlivé vlastníky úloh izolované ve vlastní skupině prostředků. Žádný z vlastníků úloh nebo jejich členové týmu nemají přístup ke správě prostředků v žádné jiné skupině prostředků.

@no__t – 0subscription se skupinami prostředků a a B @ no__t-1*Obrázek 4 – předplatné se dvěma vlastníky úloh, které jsou izolované s vlastní skupinou prostředků.*

Tento model je modelem s nejnižšími oprávněními @ no__t-0each uživateli je přiřazeno správné oprávnění v oboru správy prostředků.

Zvažte však, že každý úkol v tomto příkladu byl proveden **správcem služby**. I když se jedná o jednoduchý příklad a nemusí se jednat o problém, protože existovaly jenom dva vlastníci úloh, můžete si snadno představit typy problémů, které by měly být výsledkem velké organizace. **Správce služby** se například může stát kritickým bodem s velkým počtem nevyřízených položek žádostí, jejichž výsledkem budou zpoždění.

Pojďme se podívat na druhý příklad, který snižuje počet úloh provedených **správcem služby**.

1. V tomto modelu má **vlastník úlohy A** přiřazenou předdefinovanou roli vlastníka v oboru předplatného, který jim umožní vytvořit vlastní skupinu prostředků: **Skupina prostředků A**.  @no__t – správce 0Service přidá vlastníka úlohy A do předplatného @ no__t-1.
2. Když se vytvoří **Skupina prostředků** a, **vlastník úlohy a** se přidá ve výchozím nastavení a zdědí integrovanou roli vlastníka z oboru předplatného.
    @no__t – vlastník 0Workload vytvoří skupinu prostředků A @ no__t-1
3. Předdefinovaná role vlastníka uděluje **vlastníkovi úlohy** oprávnění ke správě přístupu ke skupině prostředků. **Vlastník úlohy a** přidává dva **přispěvatele úloh** a přiřadí jim integrovanou roli čtenářů.
    @no__t – vlastník 0Workload A přidá přispěvatele úloh @ no__t-1.
4. **Správce služby** teď přidá **vlastníka úlohy B** k předplatnému s integrovanou rolí vlastníka.
    @no__t – správce 0Service přidá vlastníky úloh B do předplatného @ no__t-1.
5. **Vlastník úlohy b** vytvoří **skupinu prostředků b** a přidá se ve výchozím nastavení. **Vlastník úlohy B** pak zdědí integrovanou roli vlastníka z oboru předplatného.
    ![Workload vlastník B vytvoří skupinu prostředků B @ no__t-1.

Všimněte si, že v tomto modelu provedl **Správce služby** méně akcí než v prvním příkladu z důvodu delegování přístupu ke správě každé z individuálních vlastníků úloh.

@no__t – 0subscription se skupinami prostředků a a B @ no__t-1*Obrázek 5 – předplatné se správcem služby a dvěma vlastníky úloh, které má přiřazenou předdefinovanou roli vlastníka.*

Vzhledem k tomu, že **vlastník úlohy** a a **vlastník úlohy B** mají přiřazenou předdefinovanou roli vlastníka v oboru předplatného, mají každý z nich děděnou předdefinovanou roli vlastníka pro skupinu prostředků. To znamená, že nemají k dispozici jenom úplný přístup k prostředkům jiných zdrojů, můžou taky delegovat přístup pro správu do skupin prostředků ostatních. Například **vlastník úlohy B** má práva k přidání dalšího uživatele do **skupiny prostředků** a a může jim přiřadit libovolnou roli, včetně předdefinované role vlastníka.

Pokud každý příklad porovnáte s požadavky, uvidíte, že oba příklady podporují jednoho důvěryhodného uživatele v oboru předplatného s oprávněním pro udělení přístupových práv k prostředkům pro tyto dva vlastníky úloh. Každý ze dvou vlastníků úloh neměl ve výchozím nastavení přístup ke správě prostředků a vyžaduje, aby **Správce služby** explicitně přidělil oprávnění. Pouze první příklad však podporuje požadavek, aby prostředky přidružené k jednotlivým úlohám byly izolované od sebe, takže žádný vlastník úlohy nemá přístup k prostředkům žádné jiné úlohy.

## <a name="resource-management-model"></a>Model správy prostředků

Teď, když jste navrhli model oprávnění s minimálním oprávněním, pojďme přejít na, abyste se mohli podívat na některé praktické aplikace těchto modelů zásad správného řízení. Navrácení z požadavků, které musíte podporovat v následujících třech prostředích:

1. **Sdílená infrastruktura:** Skupina prostředků sdílených všemi úlohami. Jedná se o prostředky, jako jsou síťové brány, brány firewall a služby zabezpečení.
2. **Produkční** Několik skupin prostředků, které představují několik produkčních úloh. Tyto prostředky se používají pro hostování privátních a veřejných artefaktů aplikace. Tyto prostředky mají typicky nejpřísnější modely zásad správného řízení a zabezpečení, aby chránily prostředky, kód aplikace a data před neoprávněným přístupem.
3. **Neprodukční:** Několik skupin prostředků, které představují více úloh připravených k nevyužívání produktů Tyto prostředky se používají pro vývoj a testování. tyto prostředky můžou mít ještě uvolněný model zásad správného řízení, který umožňuje zvýšenou flexibilitu vývojářů. Zabezpečení v rámci těchto skupin by mělo zvýšit hodnotu "produkce", kterou proces vývoje aplikace získá.

Pro každé z těchto tří prostředí je potřeba sledovat nákladová data podle **vlastníka úlohy**, **prostředí**nebo obojího. To znamená, že budete chtít zjistit průběžné náklady na **sdílenou infrastrukturu**, náklady vzniklé jednotlivcům v prostředích, která **nejsou** v produkčním prostředí **, a nakonec** celkové náklady na **neprodukci** a  **provozní**prostředí.

Již jste se dozvěděli o tom, že prostředky jsou vymezeny na dvě úrovně: **předplatné** a **Skupina prostředků**. Proto první rozhodnutí slouží k uspořádání prostředí podle **předplatného**. K dispozici jsou pouze dvě možnosti: jedno předplatné nebo více předplatných.

Než se podíváte na příklady jednotlivých modelů, Podívejme se na strukturu správy předplatných v Azure.

Nahlaste se od požadavků, které máte jednotlivce v organizaci, který je zodpovědný za předplatná, a tento uživatel je vlastníkem účtu **vlastníka předplatného** v TENANTOVI Azure AD. Tento účet však nemá oprávnění k vytváření předplatných. Jenom **vlastník účtu Azure** má oprávnění k tomu:

Vlastník účtu Azure @no__t 0An vytvoří předplatné @ no__t-1*Obrázek 6 – vlastník účtu Azure vytvoří předplatné.*

Po vytvoření předplatného může **vlastník účtu Azure** přidat účet **vlastníka předplatného** k předplatnému s rolí **vlastníka** :

@no__t – vlastník účtu Azure přidá do předplatného uživatelský účet vlastníka předplatného s rolí vlastníka. ](../../_images/govern/design/governance-3-0c.png)
*Obrázek 7 – vlastník účtu Azure přidá uživatelský účet **vlastníka předplatného** k předplatnému s rolí **vlastníka** .*

**Vlastník předplatného** teď může vytvářet **skupiny prostředků** a delegovat správu přístupu k prostředkům.

Nejdřív se podíváme na ukázkový model správy prostředků s použitím jediného předplatného. Prvním rozhodnutím je postup, jak zarovnat skupiny prostředků do tří prostředí. Máte dvě možnosti:

1. Jednotlivá prostředí zarovnejte do jedné skupiny prostředků. Všechny prostředky sdílené infrastruktury se nasazují do jedné **sdílené** skupiny prostředků infrastruktury. Všechny prostředky přidružené k úlohám vývoje se nasazují do jedné **vývojářské** skupiny prostředků. Všechny prostředky přidružené k produkčním úlohám se nasazují do jedné **produkční** skupiny prostředků pro **produkční** prostředí.
2. Vytvořte samostatné skupiny prostředků pro každou úlohu a pomocí konvence pojmenování a značek zarovnejte skupiny prostředků se všemi třemi prostředími.

Pojďme začít vyhodnocením první možnosti. Budete používat model oprávnění, který byl popsán v předchozí části, s jedním správcem služby předplatného, který vytvoří skupiny prostředků a přidá k nim uživatele buď pomocí předdefinované role **Přispěvatel** nebo **Čtenář** .

1. První nasazená skupina prostředků představuje prostředí **sdílené infrastruktury** . **Vlastník předplatného** vytvoří skupinu prostředků pro prostředky sdílené infrastruktury s názvem `netops-shared-rg`.
    @no__t 0Creating skupiny prostředků @ no__t-1
2. **Vlastník předplatného** přidá **uživatelský účet síťové operace** do skupiny prostředků a přiřadí roli **přispěvatele** .
    @no__t – 0Adding uživatele síťové operace @ no__t-1
3. **Uživatel síťové operace** vytvoří [bránu VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) a nakonfiguruje ji pro připojení k místnímu zařízení VPN. Uživatel **síťových operací** také pro každý z prostředků používá dvojici [značek](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) : *prostředí: Shared* a *ManagedBy: netOps*. Když **Správce služby předplatného** exportuje sestavu nákladů, budou náklady zarovnány s každou z těchto značek. Díky tomu může **Správce služby předplatného** překlopit náklady pomocí značky *prostředí* a značky *ManagedBy* . Všimněte si počítadla **omezení prostředků** v pravém horním rohu obrázku. Každé předplatné Azure má [omezení služby](https://docs.microsoft.com/azure/azure-subscription-service-limits)a pomůže vám pochopit dopad těchto omezení, které se řídí limitem virtuální sítě pro každé předplatné. U každého předplatného je povolený limit 1000 virtuálních sítí a po nasazení první virtuální sítě je teď k dispozici 999.
    @no__t – 0Creating bránu VPN Gateway @ no__t-1
4. Nasadí se další dvě skupiny prostředků. První má název `prod-rg`. Tato skupina prostředků je zarovnána s provozním prostředím. Druhá má název `dev-rg` a je zarovnána s vývojovým prostředím. Všechny prostředky přidružené k produkčním úlohám se nasazují do provozního prostředí a všechny prostředky přidružené k úlohám vývoje se nasazují do vývojového prostředí. V tomto příkladu nasadíte do každého z těchto dvou prostředí jenom dvě úlohy, takže nebudete mít žádná omezení služby předplatného Azure. Vezměte ale v úvahu, že každá skupina prostředků má omezení 800 prostředků na skupinu prostředků. Pokud budete pokračovat v přidávání úloh do každé skupiny prostředků, pak se toto omezení dosáhne.
    @no__t 0Creating skupiny prostředků @ no__t-1
5. První **vlastník úlohy** pošle požadavek **Správci služby předplatného** a přidá se do každé skupiny prostředků vývojového a produkčního prostředí s rolí **Přispěvatel** . Jak už jste se naučili, role **přispěvatele** umožňuje uživateli provádět jakoukoli jinou operaci než přiřazení role jinému uživateli. První **vlastník úlohy** teď může vytvořit prostředky přidružené ke svým úlohám.
    @no__t – přispěvatelé 0Adding @ no__t-1
6. První **vlastník úlohy** vytvoří virtuální síť v každé ze dvou skupin prostředků s dvojicí virtuálních počítačů v každém z nich. První **vlastník úlohy** používá značky *prostředí* a *ManagedBy* pro všechny prostředky. Všimněte si, že čítač limit služby Azure je teď ve zbývajících 997 virtuálních sítích.
    virtuální sítě ![Creating @ no__t-1
7. Každá z těchto virtuálních sítí nemá při vytváření k dispozici připojení k místní síti. V tomto typu architektury musí být každá virtuální síť navázána na partnerský *virtuální* síť v prostředí **sdílené infrastruktury** . Partnerský vztah virtuálních sítí vytvoří připojení mezi dvěma oddělenými virtuálními sítěmi a umožňuje mezi nimi procházet síťový provoz. Všimněte si, že partnerský vztah virtuálních sítí není ve své podstatě přenosný. Partnerský vztah musí být zadán v každé ze dvou připojených virtuálních sítí, a pokud pouze jedna z těchto virtuálních sítí Určuje partnerský vztah, připojení je neúplné. Pro ilustraci tohoto účinku určuje první **vlastník úlohy** partnerský vztah mezi **pracovními skupinami a virtuální** sítí a **rozbočovačem**. Vytvoří se první partnerský vztah, ale žádný přenos toků, protože doplňkový partnerský vztah od **hub-VNet** k **produkční** síti ještě není zadaný. První **vlastník úlohy** kontaktuje uživatele **síťové operace** a požádá o toto komplementární propojení partnerských vztahů.
    @no__t – 0Creating připojení partnerského vztahu @ no__t-1
8. **Síťové operace** kontrolují požadavek, schválí ho a pak specifikuje partnerský vztah v nastavení pro **hub-VNet**. Připojení partnerského vztahu je teď dokončené a síťové přenosy mezi těmito dvěma virtuálními sítěmi.
    @no__t – 0Creating připojení partnerského vztahu @ no__t-1
9. Teď druhý **vlastník úlohy** pošle požadavek **Správci služby předplatného** a přidá se do existující skupiny prostředků **produkčního** a **vývojového** prostředí s rolí **Přispěvatel** . Druhý **vlastník úlohy** má stejná oprávnění pro všechny prostředky jako první **vlastník úlohy** v každé skupině prostředků.
    @no__t – přispěvatelé 0Adding @ no__t-1
10. Druhý **vlastník úlohy** vytvoří podsíť ve virtuální síti virtuální sítě **VNet** a pak přidá dva virtuální počítače. Druhý **vlastník úlohy** používá pro jednotlivé prostředky značky *prostředí* a *ManagedBy* .
    @no__t – podsítě 0Creating @ no__t-1

Tento ukázkový model správy prostředků nám umožňuje spravovat prostředky ve třech požadovaných prostředích. Sdílené prostředky infrastruktury jsou chráněné, protože v předplatném je jenom jeden uživatel s oprávněním pro přístup k těmto prostředkům. Všichni vlastníci úloh můžou používat sdílené prostředky infrastruktury bez jakýchkoli oprávnění ke samotným sdíleným prostředkům. Tento model správy ale nesplňuje požadavky na izolaci úloh – každé ze dvou **vlastníků úloh** může získat přístup k prostředkům druhé úlohy.

Tento model má další důležité hledisko, které nemusí být okamžitě zřejmé. V tomto příkladu byl **app1 vlastník úlohy** , který požádal o připojení partnerského vztahu k síti s **rozbočovačem-VNet** pro poskytování připojení k místnímu prostředí. **Síťové operace** vyhodnotily požadavek na základě prostředků nasazených s touto úlohou. Když **vlastník předplatného** přidal k roli **přispěvatele** **vlastníka úlohy app2** , měl by mít tento uživatel práva pro správu pro všechny prostředky ve skupině prostředků **prod-RG** .

![Diagram znázorňující přístupová práva pro správu](../../_images/govern/design/governance-3-10.png)

To znamená, že **vlastník úlohy app2** měl oprávnění k nasazení vlastní podsítě s virtuálními počítači ve virtuální síti **VNet** . Ve výchozím nastavení mají tyto virtuální počítače teď přístup k místní síti. Uživatel **síťových operací** si tyto počítače neví a neschválil své připojení k místnímu prostředí.

Teď se podívejme na jedno předplatné s několika skupinami prostředků pro různá prostředí a úlohy. Všimněte si, že v předchozím příkladu byly prostředky pro každé prostředí snadno identifikovatelné, protože byly ve stejné skupině prostředků. Teď, když už toto seskupení nemusíte, budete muset spoléhat na zásady vytváření názvů skupin prostředků, které tuto funkci poskytují.

1. Prostředky **sdílené infrastruktury** budou mít v tomto modelu stále samostatnou skupinu prostředků, takže to zůstane stejné. Každé zatížení vyžaduje dvě skupiny prostředků – jeden pro každé **vývojové** a **produkční** prostředí. Pro první úlohu vytvoří **vlastník předplatného** dvě skupiny prostředků. První má název **app1-prod-RG** a druhá má název **app1-dev-RG**. Jak už bylo popsáno výše, Tato konvence vytváření názvů identifikuje prostředky, které jsou přidruženy k prvnímu zatížení, **app1**a prostředím **vývoje** nebo **výroby** . Znovu vlastník *předplatného* přidá do skupiny prostředků **vlastníka úlohy app1** s rolí **přispěvatele** .
    @no__t – přispěvatelé 0Adding @ no__t-1
2. Podobně jako v prvním příkladu **app1 vlastník úlohy** nasadí virtuální síť s názvem **app1-prod-VNet** do **provozního** prostředí a další s názvem **app1-dev-VNet** do **vývojového** prostředí. **Vlastník úlohy app1** znovu odešle požadavek na uživatele **síťové operace** , aby vytvořil připojení partnerského vztahu. Všimněte si, že **vlastník úlohy app1** přidá stejné značky jako v prvním příkladu a čítač limit byl snížen na 997 virtuálních sítí zbývajících v rámci předplatného.
    @no__t – 0Creating připojení partnerského vztahu @ no__t-1
3. **Vlastník předplatného** teď vytvoří dvě skupiny prostředků pro **vlastníka úloh app2**. V rámci stejných konvencí jako u **vlastníka úloh app1**se skupiny prostředků nazývají **app2-prod-RG** a **app2-dev-RG**. **Vlastník předplatného** přidá do každé skupiny prostředků v roli **přispěvatele** **vlastníka úloh app2** .
    @no__t – přispěvatelé 0Adding @ no__t-1
4. *Vlastník úlohy app2* nasadí virtuální sítě a virtuální počítače do skupin prostředků se stejnými zásadami vytváření názvů. Přidávají se značky a čítač limit byl snížen na 995 virtuálních sítí zbývajících v rámci *předplatného*.
    virtuální sítě a virtuální počítače s @no__t 0Deploying @ no__t-1
5. *Vlastník úlohy app2* odesílá požadavek na uživatele *síťové operace* , aby se navázat na partnerský *virtuální síť app2-prod-VNet* s *rozbočovačem-VNet*. *Síťové operace* vytvoří připojení partnerského vztahu.
    @no__t – 0Creating připojení partnerského vztahu @ no__t-1

Výsledný model správy je podobný prvnímu příkladu s několika klíčovými rozdíly:

- Každá ze dvou úloh je izolována úlohou a prostředím.
- Tento model vyžadoval dvě virtuální sítě, než je první Vzorový model. I když se nejedná o důležitý rozdíl pouze se dvěma úlohami, teoretický limit počtu úloh pro tento model je 24.
- Prostředky se už neseskupují do jedné skupiny prostředků pro každé prostředí. Seskupení prostředků vyžaduje porozumění konvencím pojmenování používaných pro každé prostředí.
- Každé připojení s partnerskými virtuálními sítěmi bylo zkontrolováno a schváleno uživatelem *síťové operace* .

Teď se podívejme na model správy prostředků s použitím několika předplatných. V tomto modelu zarovnáváte každé ze tří prostředí do samostatného předplatného: předplatné **sdílených služeb** , **produkční** předplatné a nakonec **vývojové** předplatné. Požadavky pro tento model se podobají modelu s použitím jediného předplatného, které je potřeba rozhodnout o tom, jak se skupiny prostředků zarovnají s úlohami. Již bylo zjištěno, že vytvoření skupiny prostředků pro každou úlohu splňuje požadavek na izolaci úloh, takže v tomto příkladu vytvoříte tento model.

1. V tomto modelu existují tři *předplatná*: *sdílená infrastruktura*, *produkce*a *vývoj*. Každé z těchto tří předplatných vyžaduje *vlastníka předplatného*a v jednoduchém příkladu použijete stejný uživatelský účet pro všechny tři. *Sdílené prostředky infrastruktury* se spravují podobně jako první dva příklady a první úloha je přidružená k *app1-RG* v *produkčním* prostředí a skupině prostředků se stejným názvem ve *vývoji.* prostředí. *Vlastník úlohy app1* se přidá do každé skupiny prostředků s rolí *Přispěvatel* .
    @no__t – přispěvatelé 0Adding @ no__t-1
2. Stejně jako v předchozích příkladech vytvoří *vlastník úlohy app1* prostředky a požádá o připojení partnerského vztahu ke *sdílené infrastruktuře* virtuální sítě. *Vlastník úlohy app1* přidává jenom značku *ManagedBy* , protože už není potřeba tag *prostředí* . To znamená, že prostředky jsou pro každé prostředí seskupené ve stejném *předplatném* a značka *prostředí* je redundantní. Čítač limit je snížen na 999 virtuálních sítí zbývá.
    @no__t – 0Creating připojení partnerského vztahu @ no__t-1
3. Nakonec *vlastník předplatného* opakuje proces pro druhou úlohu a přidá skupiny prostředků s *vlastníkem úlohy app2* v roli Přispěvatel *. Čítač omezení pro každé předplatné prostředí se sníží na 998 virtuálních sítí.

Tento model správy má výhody druhého výše uvedeného příkladu. Zásadní rozdíl je ale v tom, že omezení jsou menší z důvodu toho, že jsou rozdělená do dvou *předplatných*. Nevýhodou je, že data nákladů sledovaná pomocí značek musí být agregována ve všech třech *předplatných*.

Proto můžete vybrat kterýkoli z těchto dvou příkladů modelů správy prostředků v závislosti na prioritě vašich požadavků. Pokud předpokládáte, že vaše organizace nedosáhne omezení služby pro jedno předplatné, můžete použít jedno předplatné s více skupinami prostředků. Naopak, pokud vaše organizace očekává mnoho úloh, může být více předplatných pro každé prostředí lepší.

## <a name="implementing-the-resource-management-model"></a>Implementace modelu správy prostředků

Seznámili jste se s několika různými modely pro řízení přístupu k prostředkům Azure. Nyní vás provedete kroky potřebnými k implementaci modelu správy prostředků s jedním předplatným pro každou **sdílenou infrastrukturu**, **produkční**prostředí a **vývoj** prostředí z Průvodce návrhem. Budete mít jednoho **vlastníka předplatného** pro všechna tři prostředí. Jednotlivé úlohy se budou izolovat ve **skupině prostředků** s **vlastníkem úlohy** přidaným s rolí **přispěvatele** .

> [!NOTE]
> Přečtěte si téma [porozumění přístupu k prostředkům v Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles) , kde se dozvíte víc o vztahu mezi účty Azure a předplatnými.

Postupujte následovně:

1. Vytvořte si [účet Azure](https://docs.microsoft.com/azure/active-directory/sign-up-organization) , pokud ho vaše organizace ještě nemá. Osoba, která se zaregistruje k účtu Azure, se stala správcem účtu Azure a vedoucí pracovník vaší organizace musí vybrat jednotlivce, aby tuto roli předpokládal. Tato osoba bude zodpovědná za:
    - Vytváření předplatných.
    - Vytváření a Správa tenantů [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) , které ukládají identitu uživatelů pro tyto odběry.
2. Tým vedoucího týmu rozhoduje o tom, kteří uživatelé zodpovídají za:
    - Správa identity uživatele; [tenant Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) se ve výchozím nastavení vytvoří, když se vytvoří účet Azure vaší organizace a správce účtu se ve výchozím nastavení přidá jako [globální správce Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) . Vaše organizace může pro správu identity uživatelů zvolit jiného uživatele tak [, že k tomuto uživateli přiřadí roli globálního správce Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-users-assign-role-azure-portal).
    - Předplatná, což znamená tyto uživatele:
        - Spravujte náklady spojené s využitím prostředků v tomto předplatném.
        - Implementujte a udržujte nejméně model oprávnění pro přístup k prostředkům.
        - Udržujte si přehled o omezeních služeb.
    - Sdílené služby infrastruktury (Pokud se vaše organizace rozhodne použít tento model), což znamená, že tento uživatel zodpovídá za:
        - Připojení k síti Azure v místním prostředí.
        - Vlastnictví síťového připojení v rámci Azure prostřednictvím partnerského vztahu virtuálních sítí.
    - Vlastníci úloh.
3. Globální správce Azure AD [vytvoří nové uživatelské účty](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) pro:
    - Osoba, která bude **vlastníkem předplatného** pro každé předplatné přidružené k jednotlivým prostředím. Všimněte si, že to je nezbytné jenom v případě, že se **Správce služby** předplatného nebude řídit správou přístupu k prostředkům pro každé předplatné nebo prostředí.
    - Osoba, která bude **uživatel síťového provozu**.
    - Lidé, kteří jsou **vlastníci úloh**.
4. Správce účtu Azure vytvoří následující tři předplatná pomocí [portálu účtu Azure](https://account.azure.com):
    - Předplatné pro prostředí **sdílené infrastruktury**
    - Předplatné pro **produkční** prostředí.
    - Předplatné pro **vývojové** prostředí.
5. Správce účtu Azure [přidá vlastníka služby předplatného do každého předplatného](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#to-assign-a-user-as-an-administrator).
6. Vytvořte schvalovací proces pro **vlastníky úloh** , které vyžádají vytvoření skupin prostředků. Proces schvalování se dá implementovat mnoha způsoby, například přes e-maily, nebo můžete použít nástroj pro správu procesů, například [pracovní postupy SharePointu](https://support.office.com/article/introduction-to-sharepoint-workflow-07982276-54e8-4e17-8699-5056eff4d9e3). Proces schvalování může postupovat podle těchto kroků:
    - **Vlastník úlohy** připraví množství materiálů pro požadované prostředky Azure ve **vývojovém** prostředí, v **produkčním** prostředí nebo v obou a odešle je **vlastníkovi předplatného**.
    - **Vlastník předplatného** zkontroluje množství materiálů a ověří požadované prostředky, aby bylo zajištěno, že požadované prostředky jsou vhodné pro jejich plánované použití, například kontrolu, zda jsou požadované [velikosti virtuálních počítačů](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) . odstranění.
    - Pokud žádost není schválena, **vlastník úlohy** se oznámí. Pokud je žádost schválená, **vlastník předplatného** [vytvoří požadovanou skupinu prostředků](https://docs.microsoft.com/azure/azure-resource-manager/manage-resource-groups-portal#create-resource-groups) podle [konvencí vytváření názvů](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)vaší organizace a [přidá **vlastníka úlohy** ](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal#add-a-role-assignment) do role [ **přispěvatele** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) . a pošle oznámení **vlastníkovi úlohy** , že se vytvořila skupina prostředků.
7. Vytvořte schvalovací proces pro vlastníky úloh, které vyžádají připojení partnerského vztahu virtuální sítě od vlastníka sdílené infrastruktury. Stejně jako v předchozím kroku se tento proces schvalování dá implementovat pomocí e-mailu nebo nástroje pro správu procesů.

Teď, když jste implementovali model zásad správného řízení, můžete nasadit své sdílené služby infrastruktury.

## <a name="related-resources"></a>Související prostředky

[Předdefinované role pro prostředky Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles)

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Další informace o nasazení základní infrastruktury](../../infrastructure/virtual-machines/basic-workload.md)
