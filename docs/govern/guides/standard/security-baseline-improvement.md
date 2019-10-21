---
title: 'Standardní příručka pro zásady správného řízení podniku: vylepšení pravidla směrného plánu zabezpečení'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Standardní příručka pro zásady správného řízení podniku: vylepšení pravidla směrného plánu zabezpečení'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b1f43bdf0e0d58c40f11e45caf0221f7983c9624
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547523"
---
# <a name="standard-enterprise-governance-guide-improve-the-security-baseline-discipline"></a>Standardní příručka pro zásady správného řízení podniku: vylepšení pravidla směrného plánu zabezpečení

Tento článek popisuje mluvený komentář přidáním ovládacích prvků zabezpečení, které podporují přesun chráněných dat do cloudu.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

Vedoucí oddělení IT a firmy si dosáhli výsledků experimentů z prvotní fáze od týmů pro IT, vývoj aplikací a BI. Aby bylo možné realizovat hmotné obchodní hodnoty z těchto experimentů, musí být těmto týmům povoleno integrovat chráněná data do řešení. Tím se aktivují změny firemních zásad, ale také se vyžaduje přírůstkové zlepšování implementací zásad správného řízení cloudu, než se chráněná data můžou vykládat v cloudu.

### <a name="changes-to-the-cloud-governance-team"></a>Změny týmu zásad správného řízení cloudu

Vzhledem k tomu, že je v současné době změna mluveného komentáře a podpory k dispozici, je teď tým zásad správného řízení cloudu zobrazen odlišně. Dva správci systému, kteří tým zahájili, se teď zobrazují jako zkušení cloudové architekty. V rámci tohoto mluveného komentáře se projeví, že se z cloudových starají posunou k většímu počtu rolí ochrany cloudu.

I když je rozdíl malý, je důležité rozlišovat při sestavování jazykové verze IT zaměřené na zásady správného řízení. Cloudový implicitní správce čistí přehledy, které udělal inovativní cloudové architekty. Tyto dvě role mají přirozený tření a protichůdné cíle. Na druhé straně strážce cloudu pomáhá udržet Cloud v bezpečí, takže ostatní cloudové architekty se můžou rychleji pohybovat, a to s menšími rychlostmi. K vytváření šablon, které urychlují nasazení a přijetí, se taky jedná o ochranu cloudu, která zrychluje nasazování a přijímání

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

Na začátku tohoto mluveného komentáře vývojové týmy aplikace i nadále pracovaly s kapacitou pro vývoj a testování a tým BI ještě v experimentální fázi. Provozuje se dvě prostředí hostované infrastruktury s názvem prod a DR.

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- Vývojový tým aplikace implementoval kanál CI/CD pro nasazení nativní cloudové aplikace s vylepšeným uživatelským prostředím. Tato aplikace ještě nekomunikuje s chráněnými daty, takže není připravené pro produkční prostředí.
- Tým Business Intelligence v rámci IT aktivně vystavuje data v cloudu z logistiky, inventáře a zdrojů třetích stran. Tato data se používají k řízení nových předpovědi, která by mohla tvarovat obchodní procesy. Nicméně tyto předpovědi a přehledy nejsou vhodné, dokud se zákazníci a finanční data nedají integrovat do datové platformy.
- IT tým pokračuje v plánech CIO a CFO na vyřazení datacentra DR. V datacentru DR bylo vyřazeno nebo Migrováno více než 1 000 prostředků 2 000.
- Volně definované zásady týkající se osobních údajů a finančních dat byly moderní. Nové podnikové zásady jsou ale závislé na implementaci souvisejících zásad zabezpečení a zásad správného řízení. Týmy jsou stále zablokované.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

Předčasné experimenty pro vývoj aplikací a týmy v oblasti BI ukazují možné vylepšení v oblasti zákazníků a rozhodování na základě dat. Oba týmy chtějí po dalších 18 měsících rozšířit přijetí cloudu nasazením těchto řešení do produkčního prostředí.

Během zbývajících šest měsíců bude tým zásad správného řízení pro Cloud implementovat požadavky na zabezpečení a zásady správného řízení, které umožní týmům v rámci cloudového přijímání migrovat chráněná data v těchto datových centrech.

Změny aktuálního a budoucího stavu zveřejňují nová rizika, která vyžadují nové příkazy zásad.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Porušení dat:** Při přijímání jakékoli nové datové platformy existuje podstatné zvýšení závazků souvisejících s potenciálním porušením dat. Technici pro přijímání cloudových technologií zvýšili zodpovědnost za implementaci řešení, která mohou toto riziko snížit. K zajištění toho, aby tyto technici splnily tyto zodpovědnosti, je nutné implementovat robustní strategii zabezpečení a zásad správného řízení.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

1. Klíčové aplikace nebo chráněná data se můžou neúmyslně nasadit.
2. Chráněná data mohou být během úložiště vystavena v důsledku slabých rozhodnutí o šifrování.
3. Oprávnění uživatelé můžou přistupovat k chráněným datům.
4. Externí vniknutí může mít za následek přístup k chráněným datům.
5. K externímu vniknutí nebo útokům DOS (Denial of Service) může dojít k výpadku firmy.
6. Změny organizace nebo zaměstnanosti můžou dovolit neoprávněný přístup k chráněným datům.
7. Nová zneužití můžou vytvořit nové příležitosti pro vniknutí nebo přístup.
8. Nekonzistentní procesy nasazení můžou mít za následek mezery v zabezpečení, což by mohlo vést k úniku nebo přerušením dat.
9. Aktualizace s posunem nebo chybějícím nastavením můžou vést k nezamýšleným bezpečnostním otvorům, což by mohlo vést k úniku nebo přerušením dat.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky. Seznam vypadá dlouhou dobu, ale přijetí těchto zásad může být snazší než jeho zobrazení.

1. Všechny nasazené prostředky musí být rozdělené do kategorií podle závažnosti a klasifikace dat. Klasifikace jsou přezkoumány týmem zásad správného řízení cloudu a vlastníkem aplikace před nasazením do cloudu.
2. Aplikace, které ukládají nebo mají přístup k chráněným datům, se budou spravovat jinak než ty, které ne. Aby nedocházelo k neúmyslnému přístupu k chráněným datům, měly by být segmentované.
3. Všechna chráněná data musí být v klidovém stavu zašifrovaná. I když se jedná o výchozí nastavení pro všechny účty Azure Storage, můžou být potřeba další strategie šifrování, včetně šifrování dat v rámci účtu úložiště, šifrování virtuálních počítačů a šifrování na úrovni databáze, pokud se využití SQL serveru používá ve virtuálním počítači (TDE a sloupec). šifrování).
4. Zvýšená oprávnění v jakémkoli segmentu, který obsahuje chráněná data, by měla být výjimka. Jakékoli takové výjimky budou zaznamenány s týmem zásad správného řízení cloudu a budou pravidelně auditovány.
5. Podsítě sítě obsahující chráněná data musí být izolované od všech ostatních podsítí. Síťový provoz mezi podsítěmi chráněných dat se pravidelně Audituje.
6. K žádné podsíti obsahující chráněná data se dá přímo získat přímý pøístup přes veřejný Internet nebo přes datová centra. Přístup k těmto podsítím musí být směrován prostřednictvím zprostředkujících podsítí. Všechny přístupy do těchto podsítí se musí nacházet prostřednictvím řešení brány firewall, které umožňuje provádět kontrolu paketů a blokující funkce.
7. Nástroje pro správu zásad správného řízení musí auditovat a vymáhat požadavky na konfiguraci sítě definované týmem správy zabezpečení.
8. Nástroje zásad správného řízení musí omezit nasazení virtuálního počítače jenom na schválené image.
9. Kdykoli je to možné, musí Správa konfigurace uzlů uplatňovat požadavky zásad na konfiguraci libovolného hostovaného operačního systému.
10. Nástroje správy zásad správného řízení musí vymáhat, že automatické aktualizace jsou povolené u všech nasazených prostředků. Porušení musí být přezkoumána s provozními týmy správy a opraveny v souladu se zásadami provozu. Prostředky, které se automaticky neaktualizují, musí být zahrnuté do procesů, které vlastní IT operace.
11. Vytvoření nových předplatných nebo skupin pro správu pro všechny důležité aplikace nebo chráněná data budou vyžadovat kontrolu od týmu zásad správného řízení cloudu, aby bylo zajištěno, že bude přiřazen řádný plán.
12. Model přístupu s minimálními oprávněními se použije pro jakoukoli skupinu pro správu nebo předplatné, které obsahují klíčové aplikace nebo chráněná data.
13. Trendy a zneužití, které by mohly ovlivnit nasazení v cloudu, by pravidelně kontroloval tým zabezpečení, aby poskytoval aktualizace nástrojů pro správu zabezpečení používaných v cloudu.
14. Nástroje pro nasazení musí schválit tým zásad správného řízení cloudu, aby se zajistilo průběžné řízení nasazených prostředků.
15. Skripty nasazení musí být udržovány v centrálním úložišti přístupném týmem zásad správného řízení cloudu pro pravidelnou kontrolu a auditování.
16. Procesy zásad správného řízení musí zahrnovat audity v místě nasazení a v pravidelných cyklech, aby se zajistila konzistence napříč všemi prostředky.
17. Nasazení všech aplikací, které vyžadují ověřování zákazníků, musí používat schváleného poskytovatele identity, který je kompatibilní s primárním zprostředkovatelem identity pro interní uživatele.
18. Procesy zásad správného řízení cloudu musí zahrnovat čtvrtletní recenze s týmy správy identit. Tyto recenze můžou přispět k identifikaci škodlivých aktérů nebo způsobů použití, které by měly být znemožněny konfigurací cloudového prostředku.

## <a name="incremental-improvement-of-governance-practices"></a>Postupné vylepšování postupů správného řízení

Návrh MVP pro zásady správného řízení se změní, aby zahrnoval nové zásady Azure a implementaci Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

1. Sítě a týmy zabezpečení IT budou definovat požadavky na síť. Tým zásad správného řízení pro Cloud bude tuto konverzaci podporovat.
2. Identita a týmy zabezpečení IT budou definovat požadavky na identitu a provádět všechny nezbytné změny v místní implementaci služby Active Directory. Tým zásad správného řízení pro Cloud bude kontrolovat změny.
3. Vytvořte v Azure DevOps úložiště, ve kterém se uloží a naplní všechny relevantní šablony Azure Resource Manager a skriptované konfigurace.
4. Azure Security Center implementace:
    1. Nakonfigurujte Azure Security Center pro všechny skupiny pro správu, které obsahují chráněné klasifikace dat.
    2. Nastavte Automatické zřizování na zapnuto ve výchozím nastavení, aby se zajistilo dodržování předpisů.
    3. Navažte konfigurace zabezpečení operačního systému. Tým zabezpečení IT bude definovat konfiguraci.
    4. Podporuje tým zabezpečení IT při prvotním použití Security Center. Převeďte Security Center k bezpečnostnímu týmu IT, ale Udržujte přístup za účelem neustálého zlepšování zásad správného řízení.
    5. Vytvořte šablonu Správce prostředků, která odráží změny požadované pro Security Center konfiguraci v rámci předplatného.
5. Aktualizovat zásady Azure pro všechna předplatná:
    1. Auditujte a vynutilte klíčovou a datovou klasifikaci napříč všemi skupinami pro správu a odběry k identifikaci všech předplatných s chráněnými klasifikacemi dat.
    2. Auditujte a vynutili použití jenom schválených imagí.
6. Aktualizujte zásady Azure pro všechna předplatná, která obsahují klasifikace chráněných dat:
    1. Auditujte a vynuťte jenom standardní role Azure RBAC.
    2. Auditujte a vynutili šifrování pro všechny účty úložiště a soubory v klidovém umístění na jednotlivých uzlech.
    3. Audituje a vynutila použití NSG pro všechny síťové karty a podsítě. NSG budou definovat sítě a týmy zabezpečení IT.
    4. Auditujte a vynutili použití schválené podsítě sítě a virtuální sítě na síťové rozhraní.
    5. Audituje a vynutil omezení uživatelem definovaných směrovacích tabulek.
    6. Použijte předdefinované zásady pro konfiguraci hostů následujícím způsobem:
        1. Audit, zda webové servery Windows používají zabezpečené komunikační protokoly.
        2. Auditovat správné nastavení zabezpečení hesla v počítačích se systémy Linux a Windows.
7. Konfigurace brány firewall:
    1. Identifikujte konfiguraci Azure Firewall, která splňuje nezbytné požadavky na zabezpečení. Případně můžete identifikovat kompatibilní zařízení třetí strany, které je kompatibilní s Azure.
    2. Vytvořte šablonu Správce prostředků pro nasazení brány firewall pomocí požadovaných konfigurací.
8. Podrobný plán Azure:
    1. Vytvořte nový podrobný plán s názvem `protected-data`.
    2. Přidejte do podrobného plánu šablony brány firewall a Azure Security Center.
    3. Přidejte nové zásady pro odběry chráněných dat.
    4. Publikovat podrobný plán do jakékoli skupiny pro správu, která aktuálně plánuje hostování chráněných dat.
    5. U každého ovlivněného předplatného můžete kromě existujících modrotisky použít nový plán.

## <a name="conclusion"></a>Závěr

Přidání výše uvedených procesů a změn do MVP pro řízení správného řízení vám pomůže napravit mnoho rizik spojených se zabezpečením zásad správného řízení. Společně přidávají nástroje pro monitorování sítě, identity a zabezpečení potřebné k ochraně dat.

## <a name="next-steps"></a>Další kroky

V případě, že se přijetí cloudu pokračuje a přináší další obchodní hodnoty, rizika a potřeby zásad správného řízení cloudu. Pro fiktivní společnost v tomto průvodci je dalším krokem podpora důležitých úloh. To je bod, když jsou potřebné ovládací prvky konzistence prostředků.

> [!div class="nextstepaction"]
> [Vylepšení konzistence prostředků](./resource-consistency-improvement.md)
