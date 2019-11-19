---
title: Osvědčené postupy pro podniky, které přesouvají do Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Popisuje generování uživatelského rozhraní, které podniky můžou použít k zajištění zabezpečeného a spravovatelného prostředí.
author: rdendtler
ms.author: rodend
ms.date: 09/22/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: 3ad84a52b35a98744f59b0d719e61f2c83a61af0
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160456"
---
# <a name="azure-enterprise-scaffold-prescriptive-subscription-governance"></a>Azure Enterprise lešení: zásady správného řízení předplatného

> [!NOTE]
> Prostředí Azure Enterprise vygenerovaná v rámci rozhraní Microsoft Cloud pro přijetí bylo integrováno. Obsah tohoto článku je nyní reprezentován v oddílu [připraveném](../ready/index.md) v novém rozhraní. Tento článek bude v brzké 2020 zastaralý. Pokud chcete začít používat nový proces, přečtěte si téma [připravený přehled](../ready/index.md), [Vytvoření první cílové zóny](../ready/azure-setup-guide/migration-landing-zone.md)a [informace o cílové zóně](../ready/considerations/index.md).

Podniky stále stále přijímají veřejný cloud pro zajištění flexibility a flexibility. Spoléhají na síly cloudu, aby vygenerovaly výnosy a optimalizují využití prostředků pro firmu. Microsoft Azure poskytuje spoustu služeb a schopností, které podniky sestavují jako stavební bloky pro řešení nejrůznějších úloh a aplikací.

Rozhodnutí o použití Microsoft Azure je pouze prvním krokem pro dosažení výhody cloudu. Druhým krokem je porozumět, jak může podnik efektivně využívat Azure a identifikovat základní možnosti, které je potřeba řešit na otázky, jako jsou:

- "Mám obavy ohledně suverenity dat; Jak se dá zajistit, aby data a systémy splňovaly naše zákonné požadavky? "
- "Návody vědět, co jednotlivé prostředky podporují, aby je bylo možné vystavit a vracet je přesně?"
- "Chci se ujistit, že všechno, co nasazujeme nebo ve veřejném cloudu začíná místo zabezpečením, jak to můžu usnadnit?"

Potenciální zákazník pro prázdné předplatné bez guardrails je těžké. Toto volné místo může mít za to, že se váš přesun do Azure neomezuje.

Tento článek poskytuje výchozí bod pro technické odborníky, který řeší nutnost řízení a vyrovnávání IT s nutností flexibility. Zavádí pojem podnikového uživatelského rozhraní, který pomáhá organizacím v implementaci a správě prostředí Azure zabezpečeným způsobem. Poskytuje rozhraní pro vývoj efektivních a efektivních ovládacích prvků.

## <a name="need-for-governance"></a>Nutné pro řízení

Při přechodu na Azure musíte vyřešit téma zásad správného řízení včas, abyste zajistili úspěšné použití cloudu v rámci podniku. Čas a bureaucracy vytváření komplexního systému zásad správného řízení (bohužel) znamená, že některé obchodní skupiny přecházejí přímo na poskytovatele bez nutnosti podnikového oddělení IT. Tento přístup může nechat podnik otevřený, aby mohl ohrozit zabezpečení, pokud prostředky nejsou správně spravované. Charakteristiky veřejného cloudu &mdash;agility, flexibility a ceny založené na spotřebě &mdash;are důležité pro obchodní skupiny, které potřebují rychle splnit požadavky zákazníků (interní i externí). Podniková IT oddělení ale musí zajistit, aby data a systémy byly efektivně chráněné.

Při vytváření sestavení se používá generování uživatelského rozhraní pro vytvoření základu struktury. Toto uživatelské rozhraní provede základní osnovu a poskytuje kotevní body pro připojení dalších trvalých systémů. Podniková generátorová aplikace je stejná: sada flexibilních ovládacích prvků a možností Azure, které poskytují strukturu pro prostředí, a kotvy služeb postavených na veřejném cloudu. Poskytuje tvůrcům (IT a firemním skupinám) základ pro vytváření a připojování nových služeb, které zajišťují rychlost doručování.

Generování uživatelského rozhraní je založené na postupech, které jsme shromáždili z mnoha zapojení s klienty různých velikostí. Tyto klienty se rozvíjejí od malých organizací, které využívají řešení v cloudu až po velké nadnárodní společnosti a nezávislé dodavatele softwaru, kteří migrují úlohy a vývoj řešení nativních pro Cloud. Podniková generátorová služba je navržená jako "účelově sestavená", aby podporovala tradiční úlohy IT i agilní úlohy, jako jsou vývojáři vytvářející aplikace SaaS (software jako služba) na základě schopností platformy Azure.

Podnikové uživatelské rozhraní může sloužit jako základ pro každé nové předplatné v rámci Azure. Umožňuje správcům zajistit, aby úlohy splňovaly minimální požadavky na zásady správného řízení v organizaci, aniž by museli podnikovým skupinám a vývojářům rychle plnit své vlastní cíle. Naše zkušenosti ukazují, že se tím významně zrychluje a nebrání ve veřejném cloudu.

> [!NOTE]
> Společnost Microsoft vydala ve verzi Preview novou funkci nazvanou [plány Azure](https://docs.microsoft.com/azure/governance/blueprints/overview) , která vám umožní zabalit, spravovat a nasazovat běžné image, šablony, zásady a skripty napříč předplatnými a skupinami pro správu. Tato možnost je most mezi účelem generování uživatelského rozhraní jako referenční model a nasazení tohoto modelu do vaší organizace.
>
Následující obrázek ukazuje komponenty uživatelského rozhraní. Základ spoléhá na plný plán pro hierarchii a odběry správy. Pilíře sestávají ze zásad Správce prostředků a silných standardů pojmenovávání. Zbývající část uživatelského rozhraní jsou základními funkcemi a funkcemi Azure, které umožňují a spojují zabezpečené a spravovatelné prostředí.

![podnikové generování uživatelského rozhraní](../_images/reference/scaffoldv2.png)

## <a name="define-your-hierarchy"></a>Definovat hierarchii

Základem tohoto uživatelského rozhraní je hierarchie a vztah registrace Azure Enterprise k předplatným a skupinám prostředků. Podniková registrace definuje tvar a používání služeb Azure v rámci vaší společnosti ze smluvního hlediska. V rámci smlouva Enterprise můžete prostředí dále rozdělit do oddělení, účtů, předplatných a skupin prostředků, aby odpovídaly struktuře vaší organizace.

![Hierarchie](../_images/reference/agreement.png)

Předplatné Azure je základní jednotkou, kde jsou všechny prostředky obsažené. Definuje také několik omezení v rámci Azure, jako je počet jader, virtuálních sítí a dalších prostředků. Skupiny prostředků slouží k dalšímu upřesnění modelu předplatného a k zajištění více přirozeného seskupení prostředků.

Každá organizace je odlišná a hierarchie na výše uvedeném obrázku umožňuje značnou flexibilitu při organizování Azure ve vaší společnosti. Modelování hierarchie tak, aby odrážela, že vaše společnost má fakturace, správu prostředků a požadavky na přístup k prostředkům, je první a nejdůležitější rozhodnutí, které uděláte při spuštění ve veřejném cloudu.

### <a name="departments-and-accounts"></a>Oddělení a účty

Existují tři běžné vzory pro registrace do Azure:

- **Funkční** vzor:

  ![Funkční vzor](../_images/reference/functional.png)

- Vzor **obchodní jednotky** :

  ![Vzor organizační jednotky](../_images/reference/business.png)

- **Zeměpisný** vzor:

  ![Zeměpisný vzor](../_images/reference/geographic.png)

I když má každý z těchto vzorů své místo, je pro svou flexibilitu při modelování nákladového modelu organizace stále důležitější, a to i v případě **, že se** odráží rozsah řízení. Microsoft Core Engineering and Operations Group vytvořila efektivní podmnožinu vzorů **organizační jednotky** ve formátu **federální**, **státní**a **místní**. Další informace najdete v tématu [uspořádání předplatných a skupin prostředků v rámci podniku](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).

### <a name="azure-management-groups"></a>Skupiny pro správu Azure

Microsoft teď poskytuje další způsob modelování hierarchie: [skupiny pro správu Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview). Skupiny pro správu jsou flexibilnější než oddělení a účty a můžou být vnořené až na šest úrovní. Skupiny pro správu vám umožní vytvořit hierarchii oddělenou od fakturační hierarchie, a to výhradně pro efektivní správu prostředků. Skupiny pro správu mohou zrcadlit svou fakturační hierarchii a často se společnostmi spouštějí. Výkon skupin pro správu je ale při jejich používání k modelování vaší organizace, seskupení souvisejících předplatných (bez ohledu na jejich umístění ve fakturační hierarchii) a přiřazování běžných rolí, zásad a iniciativ. Možné příklady:

- **Výroba vs. nevýroba.** Některé podniky vytvářejí skupiny pro správu, které identifikují své výrobní a neproduktivní odběry. Skupiny pro správu těmto uživatelům umožňují snadnější správu rolí a zásad. Například předplatné mimo produkt může vývojářům dovolit přístup přispěvatelům, ale v produkčním prostředí mají jenom přístup čtenář.
- **Interní služby a externí služby.** Podniky mají často různé požadavky, zásady a role pro interní služby a služby s přístupem zákazníků.

Dobře navržené skupiny pro správu jsou společně s Azure Policy a iniciativami páteř efektivního řízení Azure.

### <a name="subscriptions"></a>Předplatná

Při rozhodování o vašich odděleních a účtech (nebo skupinách pro správu) se primárně naučíte, jak budete dělit prostředí Azure, aby odpovídalo vaší organizaci. Předplatná však představují situaci, kde se skutečně pracuje, a vaše rozhodnutí zde ovlivňují zabezpečení, škálovatelnost a fakturaci. Mnoho organizací se při jejich průvodcích dívá na tyto vzory:

- **Aplikace/služba:** Předplatná reprezentují aplikaci nebo službu (portfolio aplikací).
- **Životní cyklus:** Předplatná představuje životní cyklus služby, jako je například výroba nebo vývoj.
- **Oddělení:** Předplatná reprezentují oddělení v organizaci.

První dva vzorce jsou nejčastěji používané a obě jsou důrazně Doporučené. Přístup k životnímu cyklu je vhodný pro většinu organizací. V tomto případě obecně doporučujeme použít dvě základní předplatná `Production` a `Nonproduction` a potom skupiny prostředků použít k dalšímu oddělení prostředí.

### <a name="resource-groups"></a>Skupiny prostředků

Azure Resource Manager vám umožní umístit prostředky do smysluplných skupin pro účely správy, fakturace nebo přirozeného spřažení. Skupiny prostředků jsou kontejnery prostředků, které mají společný životní cyklus nebo sdílejí atribut, jako jsou "všechny servery SQL" nebo "Application A".

Skupiny prostředků není možné vnořovat a prostředky můžou patřit pouze do jedné skupiny prostředků. Některé akce se můžou provádět se všemi prostředky ve skupině prostředků. Například odstraněním skupiny prostředků se odstraní všechny prostředky v rámci skupiny prostředků. Podobně jako u předplatných existují běžné vzory pro vytváření skupin prostředků, které se liší od "tradičních úloh" v oddělení IT až po "agilní úlohy".

- "Tradiční úlohy IT" se nejčastěji seskupují podle položek v rámci stejného životního cyklu, jako je například aplikace. Seskupení podle aplikace umožňuje správu jednotlivých aplikací.
- "Agilní" úlohy se zaměřují na externí cloudové aplikace zaměřené na zákazníky. Skupiny prostředků často odráží vrstvy nasazení (například webové vrstvy nebo aplikační vrstvy) a správu.

> [!NOTE]
> Porozumění vašim úlohám vám pomůže vyvíjet strategii skupiny prostředků. Tyto vzory se dají kombinovat a porovnat. Například skupina prostředků sdílené služby ve stejném předplatném jako "agilní" skupiny prostředků.

## <a name="naming-standards"></a>Standardy pro vytváření názvů

První pilíř uživatelského rozhraní je konzistentní standardní pojmenování. Dobře navržené standardy pojmenování umožňují identifikovat prostředky na portálu, na faktuře a ve skriptech. Pravděpodobně už máte stávající standardy pojmenování pro místní infrastrukturu. Když do svého prostředí přidáte Azure, měli byste tyto standardy pro vytváření názvů rozšířit i na prostředky Azure.

> [!TIP]
> Pro konvence pojmenování:
>
> - Projděte si, a kdykoli to bude možné, začněte aplikovat [pokyny k vzorům a postupům](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming). V těchto pokynech se můžete rozhodnout pro smysluplný Standard pojmenování a poskytujeme rozsáhlé příklady.
> - Použití zásad Správce prostředků, které vám pomůžou vymáhat standardy pojmenování.
>
> Mějte na paměti, že později je obtížné změnit názvy, a to za pár minut teď ušetříte problémy později.

Soustřeďte se na tyto prostředky, které se častěji používají a prohledávají, na základě standardů pojmenování. Například všechny skupiny prostředků by měly pro přehlednost dodržovat silný Standard.

### <a name="resource-tags"></a>Značky prostředku

Značky prostředků jsou úzce zarovnané na standardy pojmenování. Protože se prostředky přidávají do předplatných, je stále důležitější je logicky kategorizovat pro účely fakturace, správy a provozní potřeby. Další informace najdete v tématu [použití značek k uspořádání prostředků Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

> [!IMPORTANT]
> Značky mohou obsahovat osobní údaje a mohou podklesnout předpisy GDPR. Pečlivě Naplánujte správu značek. Pokud hledáte Obecné informace o GDPR, přečtěte si část GDPR na [portálu Trust Service](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Značky se používají v mnoha způsobech nad rámec fakturace a správy. Často se používají jako součást automatizace (viz další část). To může způsobit konflikty, pokud se nepovažují za přední. Osvědčeným postupem je určit všechny běžné značky na úrovni podniku (například ApplicationOwner a CostCenter) a použít je konzistentně při nasazení prostředků pomocí automatizace.

## <a name="azure-policy-and-initiatives"></a>Azure Policy a iniciativy

Druhý pilíř uživatelského rozhraní zahrnuje použití [Azure Policy a iniciativ](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction) pro řízení rizik vynucením pravidel (s účinky) nad prostředky a službami ve vašich předplatných. Iniciativa Azure jsou kolekce zásad, které jsou navržené tak, aby dosáhly jednoho cíle. Zásady a iniciativy se pak přiřazují oboru prostředků, aby se tyto zásady začaly uplatňovat.

Zásady a iniciativy jsou ještě výkonnější, pokud se používají se skupinami pro správu zmíněnými výše. Skupiny pro správu umožňují přiřazení iniciativ nebo zásad k celé sadě předplatných.

### <a name="common-uses-of-resource-manager-policies"></a>Běžné použití Správce prostředkůch zásad

Zásady a iniciativy jsou výkonným nástrojem v sadě Azure Toolkit. Zásady umožňují společnostem poskytovat ovládací prvky pro běžné úlohy IT, které umožňují stabilitu potřebnou pro obchodní aplikace a zároveň umožňují "agilní" úlohy &mdash;for například, vývoj zákaznických aplikací bez zveřejnění podniku pro další riziko. Nejběžnějšími vzorci pro zásady jsou:

- **Geografické dodržování předpisů a suverenita dat.** Azure obsahuje stále rostoucí seznam oblastí po celém světě. Podniky často potřebují zajistit, aby prostředky v konkrétním oboru zůstaly v geografické oblasti pro řešení zákonných požadavků.
- **Vyhněte se zveřejňování serverů veřejně.** Azure Policy může zakázat nasazení určitých typů prostředků. Je běžné vytvořit zásadu, která zamítne vytvoření veřejné IP adresy v rámci určitého oboru, a vyhne se nezamýšlené expozici serveru na internetu.
- **Správa nákladů a jejich metadata.** Značky prostředků se často používají k přidávání důležitých fakturačních dat do prostředků a skupin prostředků, jako jsou CostCenter, Owner a další. Tyto značky jsou nevýznamné pro přesné fakturace a správu prostředků. Zásady můžou vyhovět použití značek prostředků u všech nasazených prostředků, což usnadňuje správu.

### <a name="common-uses-of-initiatives"></a>Běžné použití iniciativ

Iniciativy poskytují podnikům možnost seskupovat logické zásady a sledovat je jako jediná entita. Iniciativa nám pomůžou podnik řešit potřeby agilních i tradičních úloh. Mezi běžné použití iniciativ patří:

- **Povolí monitorování v Azure Security Center.** Toto je výchozí iniciativa v Azure Policy a skvělým příkladem toho, co jsou iniciativy. Umožňuje zásady, které identifikují nešifrované databáze SQL, chyby zabezpečení virtuálního počítače (VM) a další běžné požadavky související se zabezpečením.
- **Iniciativa pro konkrétní předpisy.** Podniky často používají zásady skupiny, které jsou společné pro zákonné požadavky (například HIPAA), aby se ovládací prvky a dodržování předpisůy těchto ovládacích prvků sledovaly efektivně.
- **Typy prostředků a SKU.** Vytvoření iniciativy, která omezuje typy prostředků, které mohou být nasazeny, i SKU, které lze nasadit, může pomoci řídit náklady a zajistit, aby vaše organizace nasadila pouze prostředky, které má váš tým dovednostní sadu a postupy pro podporu.

> [!TIP]
> Doporučujeme místo definic zásad vždycky používat definice iniciativ. Po přiřazení iniciativy k oboru, jako je například předplatné nebo skupina pro správu, můžete k iniciativě snadno přidat další zásady, aniž byste museli měnit jakékoli přiřazení. To vám umožní pochopit, co se aplikuje a co nejsnáze sleduje dodržování předpisů.

### <a name="policy-and-initiative-assignments"></a>Přiřazení zásad a iniciativ

Po vytvoření zásad a jejich seskupení do logických iniciativ musíte zásadu přiřadit k oboru bez ohledu na to, jestli se jedná o skupinu pro správu, předplatné nebo dokonce skupinu prostředků. Přiřazení umožňují také vyloučit podobory z přiřazení zásady. Pokud například odepřete vytváření veřejných IP adres v rámci předplatného, můžete vytvořit přiřazení s vyloučením pro skupinu prostředků připojenou k chráněnému DMZ.

Najdete v něm několik příkladů zásad, které ukazují, jak se dají zásady a iniciativy použít u různých prostředků v Azure v tomto úložišti [GitHubu](https://github.com/Azure/azure-policy) .

## <a name="identity-and-access-management"></a>Správa identit a přístupu

Jedním z prvních a nejdůležitějších otázek, se kterými se můžete dotazovat při zahájení s veřejným cloudem, je "kdo má mít přístup k prostředkům?" a "Jak lze řídit tento přístup?" Řízení přístupu k Azure Portal a prostředkům na portálu je důležité pro dlouhodobou bezpečnost vašich assetů v cloudu.

Pokud chcete zabezpečit přístup k prostředkům, nakonfigurujete nejprve poskytovatele identity a pak nakonfigurujete role a přístup. Azure Active Directory (Azure AD), která je připojená k místní službě Active Directory, je základem identity Azure. To znamená, že Azure AD *není stejný* jako místní služba Active Directory a je důležité pochopit, co je TENANT Azure AD a jak se vztahuje k registraci v Azure. Projděte si dostupné [informace](../govern/resource-consistency/resource-access-management.md) , které vám pomůžou získat Solid Foundation v Azure AD a v místní službě Active Directory. Pokud chcete připojit a synchronizovat službu Active Directory s Azure AD, nainstalujte a nakonfigurujte [nástroj Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) v místním prostředí.

![Diagram architektury AD](../_images/reference/ad-architecture.png)

Po prvním vydání Azure byly řízení přístupu k předplatnému základní: správce nebo spolusprávce. Přístup k předplatnému v klasickém modelu má implicitní přístup ke všem prostředkům na portálu. Tento nedostatek jemně odstupňovaného řízení vedlo k tomu, že se předplatným poskytuje úroveň přiměřeného řízení přístupu k registraci Azure. Toto šíření předplatných už není potřeba. Díky řízení přístupu na základě role (RBAC) můžete přiřadit uživatele ke standardním rolím, které poskytují společný přístup, jako je vlastník, přispěvatel nebo čtenář, nebo dokonce vytvořit vlastní role.

Při implementaci přístupu založeného na rolích se důrazně doporučuje následující:

- Řízení správce nebo spolusprávce předplatného, protože tyto role mají rozsáhlá oprávnění. Pokud potřebují ke spravovaným nasazením Azure Classic, stačí přidat vlastníka předplatného jako spolusprávce.
- Skupiny pro správu použijte k přiřazení [rolí](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview#management-group-access) napříč několika předplatnými a snížení zatížení při jejich správě na úrovni předplatného.
- Přidejte uživatele Azure do skupiny (například vlastníci aplikace X) ve službě Active Directory. Pomocí synchronizovaných skupin poskytněte členům skupiny příslušná práva ke správě skupiny prostředků obsahující aplikaci.
- Dodržujte princip udělení **nejnižších oprávnění** potřebných k provedení očekávané práce.

> [!IMPORTANT]
>Zvažte použití [Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure), možností Azure [Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted) a [podmíněného přístupu](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) k zajištění lepšího zabezpečení a lepší viditelnosti akcí správy napříč vaším Azure. odběru. Tyto možnosti pocházejí z platné licence Azure AD Premium (v závislosti na funkci) k dalšímu zabezpečení a správě vaší identity. Azure AD PIM umožňuje přístup pro správu za běhu s pracovním postupem schválení a také úplné auditování aktivací a aktivit správců. Azure Multi-Factor Authentication je další kritická schopnost a umožňuje dvoustupňové ověřování pro přihlášení k Azure Portal. V kombinaci s ovládacími prvky podmíněného přístupu můžete efektivně spravovat riziko ohrožení bezpečnosti.

Plánování a příprava pro vaše identity a řízení přístupu a následující osvědčené postupy pro správu identit Azure ([odkaz](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices)) představuje jednu z osvědčených strategií pro zmírnění rizik, které můžete využít, a měla by se pro každé nasazení považovat za povinnou.

## <a name="security"></a>Zabezpečení

Jeden z největších blokování na přijetí do cloudu se tradičně dotýká zabezpečení. Správci rizik IT a bezpečnostní oddělení musí zajistit, aby prostředky v Azure byly ve výchozím nastavení chráněné a zabezpečené. Azure poskytuje možnosti, které můžete použít k ochraně prostředků při odhalování a odstraňování hrozeb na těchto prostředcích.

### <a name="azure-security-center"></a>Centrum zabezpečení Azure

Kromě rozšířené ochrany před internetovými útoky nabízí [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) jednotný přehled o stavu zabezpečení prostředků v celém prostředí. Azure Security Center je otevřená platforma, která umožňuje partnerům Microsoftu vytvářet software, který se připojuje a vylepšuje jeho schopnosti. Základní schopnosti Azure Security Center (bezplatná úroveň) poskytují vyhodnocení a doporučení, která zlepšují stav zabezpečení. Jeho placené úrovně umožňují další a cenné možnosti, jako je například přístup správce za běhu a adaptivní řízení aplikací (přidávání do seznamu povolených).

> [!TIP]
>Azure Security Center je výkonný nástroj, který se pravidelně vylepšuje díky novým funkcím, které můžete použít ke zjišťování hrozeb a ochraně vašeho podniku. Důrazně doporučujeme vždy povolit Azure Security Center.

### <a name="locks-for-azure-resources"></a>Zámky pro prostředky Azure

Vzhledem k tomu, že vaše organizace přidává základní služby k předplatným, bude stále důležitější, aby nedocházelo k výpadkům firmy. K jednomu běžnému přerušení dochází, když skript nebo nástroj, který provádí v rámci předplatného Azure, neúmyslně odstraní prostředek. [Zamkne](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) omezení operací na vysoce hodnotových prostředcích, kde jejich změna nebo odstranění by významně ovlivnila. Můžete použít zámky u předplatných, skupin prostředků nebo jednotlivých prostředků. Použijte zámky na základní prostředky, jako jsou virtuální sítě, brány, skupiny zabezpečení sítě a účty úložiště klíčů.

### <a name="secure-devops-kit-for-azure"></a>Zabezpečená sada DevOps pro Azure

Sada Secure DevOps Kit for Azure (AzSK) je kolekce skriptů, nástrojů, rozšíření a možností automatizace, které původně vytvořil vlastní IT tým Microsoftu a [vydali jako open source prostřednictvím GitHubu](https://github.com/azsk/devopskit-docs). AzSK stravování do komplexního předplatného Azure a zabezpečení prostředků pro týmy, které využívají rozsáhlou automatizaci a hladce integrují zabezpečení do nativních pracovních postupů DevOps, pomáhají dosáhnout zabezpečení DevOps s těmito šesti oblastmi:

- Zabezpečení předplatného
- Povolit zabezpečený vývoj
- Integrace zabezpečení do CI/CD
- Nepřetržitá záruka
- Výstrahy a monitorování
- Řízení rizik v cloudu

![Diagram s přehledem sady Secure DevOps Kit pro Azure](../_images/reference/secure-devops-kit.png)

AzSK je bohatá sada nástrojů, skriptů a informací, které jsou důležitou součástí úplného plánu zásad správného řízení Azure a jejich zahrnutí do vašeho uživatelského rozhraní je důležité pro podporu vašich organizací pro řízení rizik.

### <a name="azure-update-management"></a>Update Management Azure

Jedna z klíčových úloh, které můžete udělat, abyste zajistili bezpečnost svého prostředí, zajistíte, aby byly servery opraveny s nejnovějšími aktualizacemi. I když existuje mnoho nástrojů k tomu, Azure poskytuje řešení [azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management) , které řeší identifikaci a zavedení důležitých oprav operačního systému. Používá Azure Automation, popsaný v části [Automatizace](#automate) dále v této příručce.

## <a name="monitor-and-alerts"></a>Monitorování a výstrahy

Shromažďování a analýza telemetrie, která poskytuje přehled o aktivitách, metrikách výkonu, stavu a dostupnosti služeb, které používáte v rámci předplatných Azure, je zásadní pro proaktivní správu vašich aplikací a infrastruktura a je základní potřebou každého předplatného Azure. Každá služba Azure vygeneruje telemetrii ve formě protokolů aktivit, metrik a diagnostických protokolů.

- **Protokoly aktivit** popisují všechny operace prováděné s prostředky ve vašich předplatných.
- **Metriky** jsou číselné informace vydávané prostředkem, který popisuje výkon a stav prostředku.
- **Diagnostické protokoly** vysílá služba Azure a poskytují bohatou a častou informace o provozu této služby.

Tyto informace lze zobrazit a zpracovávat na více úrovních a jsou neustále vylepšeny. Azure poskytuje možnosti **sdíleného**, **základního**a **hloubkového** monitorování prostředků Azure prostřednictvím služeb uvedených v následujícím diagramu.

![Sledování](../_images/reference/monitoring.png)

### <a name="shared-capabilities"></a>Sdílené možnosti

- **Výstrahy:** Můžete shromažďovat všechny protokoly, události a metriky z prostředků Azure, ale bez možnosti upozorňování na kritické podmínky a jednání, jsou tato data užitečná jenom pro historické účely a forenzní. Výstrahy Azure proaktivně upozorňují na podmínky, které definujete napříč všemi vašimi aplikacemi a infrastrukturou. Pravidla upozornění můžete vytvářet napříč protokoly, událostmi a metrikami, které pomocí skupin akcí upozorňují na sady příjemců. Skupiny akcí také poskytují možnost automatizace nápravy pomocí externích akcí, jako jsou Webhooky, pro spouštění Azure Automation runbooků a Azure Functions.

- **Řídicí panely:** Řídicí panely umožňují agregovat zobrazení monitorování a kombinovat data napříč prostředky a předplatnými, které vám poskytnou přehled o telemetrie prostředků Azure v celém podniku. Můžete vytvářet a konfigurovat vlastní zobrazení a sdílet je s ostatními. Můžete například vytvořit řídicí panel skládající se z různých dlaždic pro správce databáze a poskytnout informace napříč všemi databázovými službami Azure, včetně Azure SQL DB, Azure DB for PostgreSQL a Azure DB for MySQL.

- **Průzkumník metrik:** Metriky jsou číselné hodnoty generované prostředky Azure (například% CPU nebo disk v/v), které poskytují přehled o provozu a výkonu vašich prostředků. Pomocí Průzkumník metrik můžete definovat a odesílat metriky, které vás zajímají Log Analytics pro agregaci a analýzu.

### <a name="core-monitoring"></a>Základní monitorování

- **Azure monitor:** Azure Monitor je základní služba platformy, která poskytuje jeden zdroj pro monitorování prostředků Azure. Rozhraní Azure Portal Azure Monitor poskytuje centralizované můstky pro všechny funkce monitorování v rámci Azure, včetně hloubkového monitorování Application Insights, Log Analytics, monitorování sítě, řešení pro správu a Mapy služeb. Díky Azure Monitor můžete vizualizovat metriky a protokoly, které pocházejí z prostředků Azure napříč celou cloudovou službou, dotazování, směrování, archivace a reagovat na ně. Kromě portálu můžete načíst data prostřednictvím rutin monitorování PowerShellu, rozhraní příkazového řádku pro více platforem nebo Azure Monitor rozhraní REST API.

- **Azure Advisor:** Azure Advisor průběžně monitorovat telemetrii napříč předplatnými a prostředími a poskytuje doporučení týkající se osvědčených postupů pro optimalizaci prostředků Azure za účelem úspory peněz a zlepšení výkonu, zabezpečení a dostupnosti prostředků. vytváření aplikací.

- **Service Health:** Azure Service Health identifikuje všechny problémy se službami Azure, které můžou ovlivnit vaše aplikace, a pomůže vám při plánování plánovaných časových období údržby.

- **Protokol aktivit:** Protokol aktivit popisuje všechny operace s prostředky ve vašich předplatných. Poskytuje záznam pro audit k určení "What", "kdo" a "when" pro všechny operace CREATE, Update a DELETE u prostředků. Události protokolu aktivit jsou uloženy v platformě a jsou k dispozici pro dotaz na 90 dní. Protokoly aktivit můžete ingestovat do Log Analytics pro delší dobu uchování a hlubší dotazování a analýzu napříč několika prostředky.

### <a name="deep-application-monitoring"></a>Hloubkové monitorování aplikace

- **Application Insights:** Application Insights umožňuje shromažďovat telemetrie specifickou pro aplikace a monitorovat výkon, dostupnost a využití aplikací v cloudu nebo místně. Instrumentací aplikace s podporovanými sady SDK pro různé jazyky, včetně jazyků .NET, JavaScript, JAVA, Node. js, Ruby a Pythonu. Události Application Insights jsou ingestované do stejného Log Analytics úložiště dat, které podporuje infrastrukturu a monitorování zabezpečení, a umožňuje tak korelovat a agregovat události v čase prostřednictvím jazyka bohatých dotazů.

### <a name="deep-infrastructure-monitoring"></a>Hloubkové monitorování infrastruktury

- **Log Analytics:** Log Analytics hraje centrální roli v monitorování Azure shromažďováním telemetrie a dalších dat z nejrůznějších zdrojů a poskytováním dotazovacího jazyka a analytického modulu, který vám poskytne přehled o fungování vašich aplikací a prostředků. Můžete buď přímo komunikovat s Log Analyticsmi daty prostřednictvím rychlých prohledávání a zobrazení protokolů, nebo můžete použít analytické nástroje v dalších službách Azure, které ukládají svá data v Log Analytics, jako je například Application Insights nebo Azure Security Center.

- **Monitorování sítě:** Služby monitorování sítě v Azure umožňují získat přehled o toku, výkonu, zabezpečení, připojení a kritických síťových přenosech. Dobře naplánovaný návrh sítě by měl zahrnovat konfiguraci služeb monitorování sítě Azure, například Network Watcher a monitorování ExpressRoute.

- **Řešení pro správu:** Řešení pro správu jsou zabalené sady logiky, přehledů a předdefinovaných Log Analytics dotazů pro aplikace nebo služby. Spoléhají na Log Analytics jako základem pro ukládání a analýzu dat událostí. Ukázková řešení pro správu zahrnují kontejnery monitorování a analýzy Azure SQL Database.

- **Service map:** Service Map poskytuje grafické zobrazení komponent infrastruktury, jejich procesů a vzájemných závislostí na jiných počítačích a externích procesech. Provádí integraci událostí, údajů o výkonu a řešení pro správu v Log Analytics.

> [!TIP]
> Před vytvořením jednotlivých výstrah vytvořte a udržujte sadu sdílených skupin akcí, které se dají používat v rámci výstrah Azure. To vám umožní centrálně udržovat životní cyklus seznamů příjemců, způsob doručení oznámení (e-mail, telefonní čísla SMS) a Webhooky k externím akcím (Azure Automation Runbooky, Azure Functions a Logic Apps, ITSM).

## <a name="cost-management"></a>Správa nákladů

Jednou z hlavních změn, které se projeví při přesunu z místního cloudu do veřejného cloudu, je přechod z kapitálu (nákup hardwaru) na provozní výdaje (při jejich používání platí za službu). Tento přepínač také vyžaduje pečlivé řízení vašich nákladů. Výhodou cloudu je, že můžete v podstatě a v podstatě ovlivnit náklady na službu, kterou používáte, a to jenom v případě, že ji vypínáte nebo měníte jejich velikost, když ji nepotřebujete. Úmyslné řízení vašich nákladů v cloudu je osvědčeným postupem a jedním z nich je každý den v vyspělých zákaznících.

Microsoft poskytuje několik nástrojů, které vám umožní vizualizovat, sledovat a spravovat vaše náklady. Poskytujeme také kompletní sadu rozhraní API, která vám umožní přizpůsobit a integrovat správu nákladů do vlastních nástrojů a řídicích panelů. Tyto nástroje se volně seskupují do možností Azure Portal a externích možností.

### <a name="azure-portal-capabilities"></a>Možnosti Azure Portal

Tyto nástroje poskytují rychlé informace o nákladech a také možnost provádět akce.

- **Náklady na prostředky předplatného:** V zobrazení [Analýza nákladů Azure](https://docs.microsoft.com/azure/cost-management/overview) získáte rychlý přehled o vašich nákladech a o denních výdajích podle prostředků nebo skupin prostředků na portálu.
- **Azure cost management:** Tento produkt je výsledkem nákupu Cloudyn společností Microsoft a umožňuje spravovat a analyzovat útraty Azure a také to, co strávíte na jiných poskytovatelích veřejného cloudu. Existují bezplatné i placené úrovně s velkou spoustou možností, jak je vidět v [přehledu](https://docs.microsoft.com/azure/cost-management/overview).
- **Rozpočty Azure a skupiny akcí:** Znalost toho, co něco stojí a co s tím dělá, dokud nebylo nedávno více ručního cvičení. Díky zavedení rozpočtů Azure a jeho rozhraní API je teď možné vytvářet akce (jak je vidět v [tomto příkladu](https://channel9.msdn.com/Shows/Azure-Friday/Managing-costs-with-the-Azure-Budgets-API-and-Action-Groups)), když náklady narazí na prahovou hodnotu. Například vypínáte skupinu prostředků "test", když má za to 100% svého rozpočtu nebo [jiný příklad].
- **Azure Advisor** Znalost toho, jaké jsou náklady jenom na polovinu výročí; Druhá polovina má na vědomí, co dělat s těmito informacemi. [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) poskytuje doporučení k akcím, které je potřeba provést za účelem úspory peněz, zvýšení spolehlivosti nebo dokonce i zvýšení zabezpečení.

### <a name="external-cost-management-tools"></a>Nástroje pro externí správu nákladů

- **Power BI Azure Consumption Insights:** Chcete vytvořit vlastní vizualizace pro vaši organizaci? Pokud ano, pak Azure Consumption Insights balíčku obsahu pro Power BI je vámi zvolený nástroj. Pomocí tohoto balíčku obsahu a Power BI můžete vytvořit vlastní vizualizace, které reprezentují vaši organizaci, dělat hlubší analýzu nákladů a přidávat je do dalších zdrojů dat pro další obohacení.

- **Rozhraní API pro vyčerpání:** [Rozhraní API pro spotřebu](https://docs.microsoft.com/rest/api/consumption) poskytují programový přístup k datům o nákladech a využití navíc k informacím o rozpočtech, rezervovaných instancích a poplatkům na webu Marketplace. Tato rozhraní API jsou přístupná jenom pro podnikové registrace a některé webové přímé odběry, ale poskytují možnost integrovat vaše nákladová data do vlastních nástrojů a datových skladů. [K těmto rozhraním API můžete přistupovat taky přes Azure CLI](https://docs.microsoft.com/cli/azure/consumption?view=azure-cli-latest).

Zákazníci, kteří jsou dlouhodobým a vyspělým cloudovým uživatelům, používají určité osvědčené postupy:

- **Aktivně monitorujte náklady.** Organizace, které jsou vyspělými uživateli Azure, neustále monitorují náklady a v případě potřeby mohou provádět akce. Některé organizace si dokonce vyhradou analýzu a navrhují změny v používání a tyto osoby se účtují při prvním vyhledání nevyužitého clusteru HDInsight, který je spuštěný v měsících.
- **Použijte rezervované instance virtuálních počítačů.** Další klíčovou principemou pro správu nákladů v cloudu je použití pravého nástroje pro úlohu. Pokud máte virtuální počítač s IaaS, který musí zůstat nepřetržitě, pak se při použití rezervované instance virtuálního počítače ušetří vaše významné peníze. Hledání správného zůstatku mezi automatizací vypnutí virtuálních počítačů a využitím rezervovaných instancí virtuálních počítačů se zachováním a analýzou.
- **Používejte automatizaci efektivněji.** Mnohé úlohy není potřeba spouštět každý den. Vypnutí virtuálního počítače po dobu čtyř hodin každý den vám ušetří 15% vašich nákladů. Automatizace bude platit okamžitě.
- **Pro viditelnost použijte značky prostředků.** Jak jsme uvedli jinde v tomto dokumentu, použití značek prostředků umožní lepší analýzu nákladů.

Cost Management je disciplína, která je základem efektivního a efektivního provozu veřejného cloudu. Podniky, které dosahují úspěchu, můžou řídit jejich náklady a odpovídat na jejich skutečnou poptávku, místo toho, aby nemuseli překupovat a doufá že poptávku.

## <a name="automate"></a>Automatizace

Jednou z mnoha možností, které odlišují dobu zralosti organizací pomocí poskytovatelů cloudu, je úroveň automatizace, kterou si zazahrnuli. Automatizace je nikdy nekonečný proces a když vaše organizace přesouvá do cloudu, je to Libovolná oblast, kterou potřebujete k investicím prostředků a času při sestavování. Automatizace obsluhuje mnoho účelů, včetně konzistentního zavedení prostředků (kde se přizpůsobuje přímo k dalšímu základnímu principu uživatelského rozhraní, šablonám a DevOps) k nápravě problémů. Automatizace je "propojovací tkáň" rozhraní Azure a propojuje jednotlivé oblasti.

Několik nástrojů vám může pomáhat při sestavování této funkce, od nástrojů od první strany, jako jsou Azure Automation, Event Grid a Azure CLI, až po rozsáhlou řadu nástrojů třetích stran, jako jsou Terraformu, Jenkinse,, a Puppet. Mezi základní nástroje pro automatizaci patří Azure Automation, Event Grid a Azure Cloud Shell.

- **Azure Automation** Je cloudová funkce, která umožňuje vytvářet Runbooky (v PowerShellu nebo Pythonu) a umožňuje automatizovat procesy, konfigurovat prostředky a dokonce i použít opravy. [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) má rozsáhlou škálu funkcí pro různé platformy, které jsou pro vaše nasazení nedílnou součástí, ale jsou moc velké, aby je bylo možné zakrýt podrobněji.
- **Event Grid** je plně spravovaný systém směrování událostí, který umožňuje reagovat na události v prostředí Azure. Stejně jako Azure Automation je připojená tkáň vyspělých cloudových organizací, [Event Grid](https://docs.microsoft.com/azure/event-grid) je propojovací tkáň dobré automatizace. Pomocí Event Grid můžete vytvořit jednoduchou akci bez serveru k odeslání e-mailu správci při každém vytvoření nového prostředku a zaznamenání tohoto prostředku do databáze. Stejné Event Grid mohou upozorňovat na odstranění prostředku a odebrat položku z databáze.
- **Azure Cloud Shell** je interaktivní [prostředí](https://docs.microsoft.com/azure/cloud-shell/overview) založené na prohlížeči pro správu prostředků v Azure. Poskytuje kompletní prostředí pro PowerShell nebo bash, které se spustí podle potřeby (a udržuje se za vás), abyste měli konzistentní prostředí, ze kterého se mají spouštět skripty. Azure Cloud Shell poskytuje přístup k dalším klíčovým nástrojům, už je nainstalovaný – pro automatizaci vašeho prostředí včetně [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), [terraformu](https://docs.microsoft.com/azure/virtual-machines/linux/terraform-install-configure) a rostoucího seznamu dalších [nástrojů](https://azure.microsoft.com/updates/cloud-shell-new-cli-tools-and-font-size-selection) pro správu kontejnerů, databází (Sqlcmd) a aktuálnější.

Automatizace je úloha v plném rozsahu a rychle se stane jednou z nejdůležitějších provozních úloh v rámci vašeho cloudového týmu. Organizace, které přijímají přístup "automatizovat první", mají větší úspěšnost při používání Azure:

- **Správa nákladů:** Aktivně hledající příležitosti a vytváření automatizace pro změnu velikosti prostředků, horizontální navýšení nebo snížení kapacity a vypnutí nepoužívaných prostředků.
- **Flexibilita provozu:** Díky automatizaci (spolu se šablonami a DevOps) získáte úroveň opakovatelnosti, která zvyšuje dostupnost, zvyšuje zabezpečení a umožňuje vašemu týmu soustředit se na řešení obchodních problémů.

## <a name="templates-and-devops"></a>Šablony a DevOps

Jak je zvýrazněné v části automatizovat, váš cíl jako organizace by měl být cílem zřídit prostředky prostřednictvím šablon a skriptů spravovaných zdrojem a minimalizovat interaktivní konfiguraci vašich prostředí. Tento přístup "infrastruktury jako kódu" společně s oborem DevOps procesu pro průběžné nasazování může zajistit konzistenci a snížit snížení úrovně napříč prostředími. Skoro každý prostředek Azure je možno nasadit prostřednictvím [šablon Azure Resource Manager JSON](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) ve spojení s PowerShellem nebo pomocí rozhraní příkazového řádku (CLI) pro různé platformy Azure, jako je například Terraformu z Hashicorp (který má první podporu a integrovaný do Azure Cloud Shell).

Článek, jako například [osvědčené postupy pro používání šablon Azure Resource Manager](https://blogs.msdn.microsoft.com/mvpawardprogram/2018/05/01/azure-resource-manager) , nabízí vynikající diskuzi o osvědčených postupech a lekcích, které se naučily při použití přístupu DevOps k Azure Resource Manager šablonám pomocí [Azure DevOps](https://docs.microsoft.com/azure/devops/user-guide/?view=vsts) sada nástrojů. . Vezměte v úvahu čas a úsilí pro vývoj základní sady šablon specifických pro požadavky vaší organizace a pro vývoj průběžných kanálů doručování s využitím DevOps sady nástrojů (jako je Azure DevOps, Jenkinse, Bamboo, TeamCity a další), zejména pro vaše produkční prostředí a prostředí pro kontrolu kvality. Existuje rozsáhlá knihovna šablon pro [rychlý Start Azure](https://github.com/Azure/azure-quickstart-templates) na GitHubu, kterou můžete použít jako výchozí bod pro šablony, a můžete rychle vytvořit cloudové kanály pro doručování s využitím Azure DevOps.

Jako osvědčený postup pro produkční předplatná nebo skupiny prostředků by měl váš cíl používat zabezpečení RBAC, aby ve výchozím nastavení nepovoloval interaktivní uživatele a používal automatizované kanály průběžného doručování založené na instančních objektech ke zřízení všech prostředků a doručovat veškerý kód aplikace. Žádný správce nebo vývojář by se neměl dotknout Azure Portal k interaktivní konfiguraci prostředků. Tato úroveň DevOps využívá sladěné úsilí a používá všechny koncepty generování uživatelského rozhraní Azure a poskytuje konzistentní a bezpečnější prostředí, které bude vyhovovat potřebě škálování vaší organizace.

> [!TIP]
> Při navrhování a vývoji složitých šablon Azure Resource Manager použijte [propojené šablony](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-linked-templates) k organizování a refaktorování složitých vztahů prostředků ze souborů JSON monolitické. To vám umožní spravovat prostředky jednotlivě a usnadnit čitelnost, testovatelné a opakovaně použitelné šablony.

Azure je poskytovatel cloudu s měřítkem. Při přesunu organizace z místních serverů do cloudu se spoléháte na stejné koncepty jako poskytovatelé cloudu a SaaS aplikace, které vaší organizaci pomůžou reagovat na potřeby firmy mnohem efektivnější.

## <a name="core-network"></a>Základní síť

Poslední součástí referenčního modelu Azure pro generování uživatelského rozhraní je základní informace o tom, jak vaše organizace přistupuje k Azure zabezpečeným způsobem. Přístup k prostředkům může být buď interní (uvnitř sítě společnosti), nebo externí (přes Internet). Uživatelé ve vaší organizaci můžou nechtěně vkládat prostředky do nesprávného místa a můžou je otevřít pro škodlivý přístup. Stejně jako u místních zařízení podniky musí přidat vhodné ovládací prvky, aby se zajistilo, že uživatelé Azure budou mít správná rozhodnutí. Pro zásady správného řízení předplatného identifikujeme základní prostředky, které poskytují základní kontrolu nad přístupem. Základní prostředky sestávají z těchto:

- **Virtuální sítě** jsou objekty kontejneru pro podsítě. I když není nezbytně nutné, často se používá při připojování aplikací k interním podnikovým prostředkům.
- **Trasy definované uživatelem** umožňují manipulaci s tabulkou směrování v rámci podsítě, která vám umožní odesílat přenosy přes síťové virtuální zařízení nebo na vzdálenou bránu v partnerské virtuální síti.
- **Partnerské vztahy virtuálních sítí** umožňují bezproblémové připojení dvou nebo více virtuálních sítí Azure a vytváření složitějších návrhů hub a paprsků nebo sítí sdílených služeb.
- **Koncové body služby.** V minulosti se PaaS služby spoléhaly na různé metody zabezpečení přístupu k těmto prostředkům z vašich virtuálních sítí. Koncové body služby umožňují zabezpečený přístup k povoleným službám PaaS **jenom** z připojených koncových bodů. tím se zvyšuje celkové zabezpečení.
- **Skupiny zabezpečení** jsou rozsáhlá sada pravidel, která poskytují možnost povolit nebo odepřít příchozí a odchozí provoz z prostředků Azure. [Skupiny zabezpečení](https://docs.microsoft.com/azure/virtual-network/security-overview) se skládají z pravidel zabezpečení, která se dají rozšířit pomocí **značek služeb** (které definují běžné služby Azure, jako je Azure Key Vault nebo Azure SQL Database), a **skupin zabezpečení aplikací** (které definují a aplikace struktura, například webové servery nebo aplikační servery).

> [!TIP]
> Používejte značky služeb a skupiny zabezpečení aplikací ve skupinách zabezpečení sítě, nejen ke zlepšení čitelnosti vašich pravidel, &mdash;which je důležité pochopit, co &mdash;but taky povolit efektivní mikrosegmentaci v rámci větší podsítě. zmenšení neustálému zvětšování a zvýšení flexibility.

### <a name="azure-virtual-datacenter"></a>Virtuální datové centrum Azure

Azure nabízí interní funkce a funkce třetích stran z naší rozsáhlé partnerské sítě, která vám umožní mít efektivní potřebujete pomoc podporují zabezpečení. Důležitější je, že Microsoft poskytuje osvědčené postupy a pokyny ve formě [Azure Virtual datacentra (VDC)](./networking-vdc.md). Při přesunu z jedné úlohy do několika úloh, které používají hybridní funkce, vám průvodce VDC poskytne "recepty", které umožní flexibilní síť, která se bude zvětšovat jako vaše zatížení v Azure.

## <a name="next-steps"></a>Další kroky

Zásady správného řízení jsou zásadní pro úspěch Azure. Tento článek se zaměřuje na technickou implementaci podnikového uživatelského rozhraní, ale jenom se dotýká širšího procesu a vztahů mezi komponentami. Zásady správného řízení zásad jsou vypočítány shora dolů a jsou určeny podle toho, co firma chce dosáhnout. Vytváření modelu zásad správného řízení pro Azure přirozeně zahrnuje i zástupce z něj, ale důležitější je, že by měl mít silné vyjádření od vedoucích obchodních skupin a zabezpečení a řízení rizik. V konečném případě je podniková generátor z důvodu zmírnění podnikového rizika, aby se usnadnila poslání a cíle organizace.

Teď, když jste se seznámili se zásadou správného řízení předplatného, je čas zobrazit tato doporučení v praxi. Další informace najdete v tématu [osvědčené postupy pro připravenost na Azure](../ready/azure-best-practices/index.md).
