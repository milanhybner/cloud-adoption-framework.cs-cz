---
title: 'Komplexní řízení podniku: Vylepšete základnu standardních hodnot zabezpečení'
description: Pomocí architektury cloudového přijetí pro Azure se dozvíte, jak přidat bezpečnostní mechanismy, které podporují přesun chráněných dat do cloudu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6501871e909beba8d32cee0c5dd8c3dbe091f252
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706808"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-security-baseline-discipline"></a>Příručka zásad správného řízení pro komplexní podniky: zlepšení pravidla směrného plánu zabezpečení

Tento článek popisuje mluvený komentář přidáním ovládacích prvků zabezpečení, které podporují přesun chráněných dat do cloudu.

## <a name="advancing-the-narrative"></a>Posunutí mluveného komentáře

CIO věnovala měsíční spolupráci kolegům a právním pracovníkům společnosti. Konzultant s odbornými znalostmi v kyberbezpečnosti byl moci pomáhat stávajícímu zabezpečení IT a týmy pro řízení IT mají v konceptu nové zásady týkající se chráněných dat. Skupina dokázala podporovat podporu na panelu, aby nahradila stávající zásady a umožnila hostování citlivých osobních a finančních dat schválenými poskytovateli cloudu. K tomu je potřeba přijmout sadu požadavků na zabezpečení a proces zásad správného řízení pro ověření a dokumentování dodržování těchto zásad.

V posledních 12 měsících týmy pro přijetí v cloudu vymazaly většinu prostředků 5 000 od dvou datových center, které se mají vyřadit. Nekompatibilní assety 350 byly přesunuty do alternativního datového centra. Zůstanou jenom virtuální počítače 1 250, které obsahují chráněná data.

### <a name="changes-in-the-cloud-governance-team"></a>Změny v týmu zásad správného řízení cloudu

Tým zásad správného řízení cloudu se stále mění společně s mluveným komentářem. Dva nalezení členové týmu jsou teď mezi nejvíc respektovánými Cloud architekty ve firmě. Kolekce konfiguračních skriptů se zvětšila, protože nové týmy se zabývat inovativními novými nasazeními. Tým zásad správného řízení cloudu se také zvětšil. Nedávno členové týmu IT Operations mají k přípravě na cloudové operace připojené týmové aktivity zásad správného řízení cloudu. Cloudové architekty, které pomohly podpořit tuto komunitu, se zobrazují jako strážce cloudu i cloudové akcelerátory.

I když je rozdíl malý, je důležité rozlišovat při sestavování jazykové verze IT zaměřené na zásady správného řízení. Cloud implicitní správce vyčistí přehledy, které udělal inovativní cloudové architekty, a tyto dvě role mají přirozené tření a protichůdné cíle. Cloudový stráž pomáhá udržet Cloud v bezpečí, takže ostatní cloudové architekty se můžou rychleji pohybovat s menším počtem obav. Cloudový akcelerátor provádí obě funkce, ale je také součástí vytváření šablon pro urychlení nasazení a přijetí, stane se akcelerátorem inovace a také Defenderem pěti oborů zásad správného řízení cloudu.

### <a name="changes-in-the-current-state"></a>Změny v aktuálním stavu

V předchozí fázi tohoto mluveného komentáře společnost začala postup vyřazení dvou datových center. Toto průběžné úsilí zahrnuje migraci některých aplikací se staršími požadavky na ověření, které vyžadovaly přírůstkovou vylepšení směrného plánu identity popsané v [předchozím článku](./identity-baseline-improvement.md).

Od té doby se změnily některé věci, které budou mít vliv na zásady správného řízení:

- Do cloudu byly nasazeny tisíce IT a firemních prostředků.
- Vývojový tým aplikace implementoval kanál průběžné integrace a nasazování (CI/CD) pro nasazení nativní aplikace cloudu s vylepšeným uživatelským prostředím. Tato aplikace ještě nekomunikuje s chráněnými daty, takže není připravená pro produkční prostředí.
- Tým Business Intelligence v rámci IT aktivně vystavuje data v cloudu z logistiky, inventáře a dat třetích stran. Tato data se používají k řízení nových předpovědi, která by mohla tvarovat obchodní procesy. Nicméně tyto předpovědi a přehledy nejsou vhodné, dokud se zákazníci a finanční data nedají integrovat do datové platformy.
- IT tým pokračuje v plánech CIO a CFO, aby vyřazení dvou datových center. Téměř 3 500 prostředků ve dvou datacentrech bylo vyřazeno nebo Migrováno.
- Zásady týkající se citlivých osobních a finančních dat byly moderní. Nové podnikové zásady jsou ale závislé na implementaci souvisejících zásad zabezpečení a zásad správného řízení. Týmy jsou stále zablokované.

### <a name="incrementally-improve-the-future-state"></a>Přírůstkové zlepšení budoucího stavu

- Předčasné experimenty od vývoje aplikací a týmů BI ukázaly potenciální vylepšení v oblasti zákazníků a rozhodování na základě dat. Oba týmy chtějí po dalších 18 měsících rozšířit přijetí cloudu nasazením těchto řešení do produkčního prostředí.
- Vyvinuli jsme obchodní odůvodnění pro migraci pěti dalších datových center do Azure, což snižuje náklady na IT a zvyšuje flexibilitu firmy. V menším měřítku se očekává vyřazení těchto datových center na dvojnásobek celkové úspory nákladů.
- V případě dlouhodobých výdajů a rozpočtů provozních výdajů se schválila implementace požadovaných zásad zabezpečení a zásad správného řízení, nástrojů a procesů. Očekávaná úspora nákladů z odchodu datacentra je pro tuto novou iniciativu větší než dostatečná. IT a obchodní vedení jsou si jisti, že investice budou zrychlit realizaci návratnosti v jiných oblastech. Tým zásad správného řízení cloudu Grassroots se stal známým týmem s vyhrazeným vedoucím a personálem.
- Kolektivně týmy pro přijetí cloudu, tým zásad správného řízení cloudu, tým zabezpečení IT a tým pro řízení IT budou implementovat požadavky na zabezpečení a zásady správného řízení, které umožní týmům v rámci přijímání cloudu migrovat chráněná data do cloudu.

## <a name="changes-in-tangible-risks"></a>Změny v hmatatelných rizicích

**Porušení dat:** Při přijímání jakékoli nové datové platformy se v souvislosti s porušením dat vyskytlo podstatné zvýšení závazků. Technici pro přijímání cloudových technologií zvýšili zodpovědnost za implementaci řešení, která mohou toto riziko snížit. K zajištění toho, aby tyto technici splnily tyto zodpovědnosti, je nutné implementovat robustní strategii zabezpečení a zásad správného řízení.

Toto obchodní riziko se dá rozšířit na několik technických rizik:

1. Klíčové aplikace nebo chráněná data se můžou neúmyslně nasadit.
2. Chráněná data mohou být během úložiště vystavena v důsledku slabých rozhodnutí o šifrování.
3. Oprávnění uživatelé můžou přistupovat k chráněným datům.
4. Externí vniknutí by mohlo mít za následek přístup k chráněným datům.
5. K externímu vniknutí nebo útokům při odepření služby by mohlo dojít k výpadku firmy.
6. Změny organizace nebo zaměstnanosti můžou dovolit neoprávněný přístup k chráněným datům.
7. Nové zneužití můžou vytvořit příležitosti pro vniknutí nebo neoprávněný přístup.
8. Nekonzistentní procesy nasazení můžou vést k bezpečnostním otvorům, které by mohly vést k úniku nebo přerušením dat.
9. Aktualizace s posunem nebo chybějícími opravami můžou vést k nezamýšleným bezpečnostním otvorům, které by mohly vést k úniku nebo přerušením dat.
10. Různorodé hraniční zařízení může zvýšit náklady na síťové operace.
11. Různorodé konfigurace zařízení by mohly vést k dohledům v konfiguraci a ohrožení zabezpečení.
12. Kyberbezpečnosti tým naklade riziko, že zámek dodavatele od generování šifrovacích klíčů na platformě jednoho poskytovatele cloudu. I když je tato deklarace identity neodůvodněná, ji tým přijal za čas.

## <a name="incremental-improvement-of-the-policy-statements"></a>Přírůstkové zlepšování příkazů zásad

Následující změny zásad vám pomůžou opravit nová rizika a implementaci příručky. Seznam vypadá dlouhou dobu, ale přijetí těchto zásad může být jednodušší, než by se zobrazilo.

1. Všechny nasazené prostředky musí být rozdělené do kategorií podle závažnosti a klasifikace dat. Klasifikace jsou přezkoumány týmem zásad správného řízení cloudu a aplikací před nasazením do cloudu.
2. Aplikace, které ukládají nebo mají přístup k chráněným datům, se budou spravovat jinak než ty, které ne. Aby nedocházelo k neúmyslnému přístupu k chráněným datům, měly by být segmentované.
3. Všechna chráněná data musí být v klidovém stavu zašifrovaná.
4. Zvýšená oprávnění v jakémkoli segmentu, který obsahuje chráněná data, by měla být výjimka. Jakékoli takové výjimky budou zaznamenány s týmem zásad správného řízení cloudu a budou pravidelně auditovány.
5. Podsítě sítě obsahující chráněná data musí být izolované od všech ostatních podsítí. Síťový provoz mezi podsítěmi chráněných dat se pravidelně Audituje.
6. K žádné podsíti obsahující chráněná data se dá přímo získat přímý pøístup přes veřejný Internet nebo přes datová centra. Přístup k těmto podsítím musí být směrován prostřednictvím zprostředkujících podsítí. Všechny přístupy do těchto podsítí se musí nacházet prostřednictvím řešení brány firewall, které umožňuje provádět kontrolu paketů a blokující funkce.
7. Nástroje pro správu zásad správného řízení musí auditovat a vymáhat požadavky na konfiguraci sítě definované týmem správy zabezpečení.
8. Nástroje zásad správného řízení musí omezit nasazení virtuálního počítače jenom na schválené image.
9. Kdykoli je to možné, musí Správa konfigurace uzlů uplatňovat požadavky zásad na konfiguraci libovolného hostovaného operačního systému. Správa konfigurace uzlů by měla respektovat stávající investice do objektu Zásady skupiny Object (GPO) pro konfiguraci prostředků.
10. Nástroje zásad správného řízení budou auditovat, jestli jsou automatické aktualizace povolené u všech nasazených prostředků. Pokud je to možné, vynutily se automatické aktualizace. V případě, že nejsou vyhodnoceny nástroji, musí být porušení na úrovni uzlu přezkoumána s týmy provozní správy a opraveny v souladu se zásadami provozu. Prostředky, které se automaticky neaktualizují, musí být zahrnuté do procesů, které vlastní IT operace.
11. Vytvoření nových předplatných nebo skupin pro správu pro všechny klíčové aplikace nebo chráněná data vyžadují kontrolu od týmu zásad správného řízení cloudu, aby bylo zajištěno správné přiřazení podrobného plánu.
12. Model přístupu s minimálními oprávněními se použije u všech předplatných, která obsahují klíčové aplikace nebo chráněná data.
13. Dodavatel cloudu musí umožňovat integraci šifrovacích klíčů spravovaných existujícím místním řešením.
14. Dodavatel cloudu musí podporovat stávající řešení hraničního zařízení a všechny požadované konfigurace, aby se chránily všechny veřejně vystavené síťové hranice.
15. Dodavatel cloudu musí podporovat sdílené připojení k globální síti WAN a přenos dat směrovaný přes stávající řešení hraničního zařízení.
16. Trendy a zneužití, které by mohly ovlivnit nasazení v cloudu, by pravidelně kontroloval tým zabezpečení, aby poskytoval aktualizace nástroje pro základní hodnoty zabezpečení používané v cloudu.
17. Nástroje pro nasazení musí schválit tým zásad správného řízení cloudu, aby se zajistilo průběžné řízení nasazených prostředků.
18. Skripty nasazení musí být udržovány v centrálním úložišti přístupném týmem zásad správného řízení cloudu pro pravidelnou kontrolu a auditování.
19. Procesy zásad správného řízení musí zahrnovat audity v místě nasazení a v pravidelných cyklech, aby se zajistila konzistence napříč všemi prostředky.
20. Nasazení všech aplikací, které vyžadují ověřování zákazníků, musí používat schváleného poskytovatele identity, který je kompatibilní s primárním zprostředkovatelem identity pro interní uživatele.
21. Procesy zásad správného řízení cloudu musí zahrnovat čtvrtletní recenze s týmy standardních hodnot identity k identifikaci škodlivých aktérů nebo způsobů použití, které by měly být znemožněny konfigurací cloudového prostředku.

## <a name="incremental-improvement-of-the-best-practices"></a>Přírůstkové zlepšení osvědčených postupů

V této části se upraví návrh MVP pro řízení a zahrnutí nových zásad Azure a implementace Azure Cost Management. Tyto dvě změny návrhu společně budou plnit nové příkazy podnikové zásady.

Nové osvědčené postupy spadají do dvou kategorií: podniková IT (centra) a přijetí do cloudu (paprskový).

**Vytváření předplatného podnikového centra IT a paprsků pro centralizaci standardních hodnot zabezpečení:** V tomto osvědčeném postupu je stávající kapacita zásad správného řízení zabalená pomocí [topologie centra a paprsků se sdílenými službami](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)s několika přidanými klíči z týmu zásad správného řízení cloudu.

1. Úložiště Azure DevOps Vytvořte v Azure DevOps úložiště, ve kterém se uloží a naplní všechny relevantní šablony Azure Resource Manager a skriptované konfigurace.
2. Šablona centra a paprsků:
    1. Pokyny v [topologii centra a paprsků s](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) referenční architekturou sdílených služeb lze použít ke generování šablon Správce prostředků pro prostředky požadované v podnikovém centru IT.
    2. Pomocí těchto šablon se dá tato struktura provést opakovaně, a to v rámci centrální strategie zásad správného řízení.
    3. Kromě aktuální referenční architektury by se měla vytvořit šablona skupiny zabezpečení sítě, která bude zachytávání všech požadavků na blokování portů nebo povolených požadavků pro virtuální síť pro hostování brány firewall. Tato skupina zabezpečení sítě se liší od předchozích skupin, protože se jedná o první skupinu zabezpečení sítě, která umožňuje veřejný provoz do virtuální sítě.
3. Vytvořte zásady Azure. Vytvořte zásadu s názvem `Hub NSG Enforcement` k vykonání konfigurace skupiny zabezpečení sítě přiřazené k libovolné virtuální síti vytvořené v tomto předplatném. Použijte předdefinované zásady pro konfiguraci hostů následujícím způsobem:
    1. Audit, zda webové servery Windows používají zabezpečené komunikační protokoly.
    2. Auditovat správné nastavení zabezpečení hesla v počítačích se systémy Linux a Windows.
4. Podnikový plán IT
    1. Vytvořte podrobný plán Azure s názvem `corporate-it-subscription`.
    2. Přidejte šablony hub a paprsků a zásady `Hub NSG Enforcement`.
5. Probíhá rozbalování v hierarchii počátečních skupin pro správu.
    1. Pro každou skupinu pro správu, která požádala o podporu chráněných dat, `corporate-it-subscription-blueprint` podrobného plánu poskytuje řešení urychleného centra.
    2. Vzhledem k tomu, že skupiny pro správu v tomto fiktivním příkladu zahrnují kromě hierarchie obchodních jednotek i regionální hierarchii, bude tento podrobný plán nasazen v každé oblasti.
    3. Pro každou oblast v hierarchii skupiny pro správu vytvořte předplatné s názvem `Corporate IT Subscription`.
    4. Použijte `corporate-it-subscription-blueprint` podrobných plánů na každou místní instanci.
    5. Tím se vytvoří rozbočovač pro každou organizační jednotku v každé oblasti. Poznámka: můžete dosáhnout dalších úspor nákladů, ale sdílet centra napříč obchodními jednotkami v každé oblasti.
6. Integrace objektů zásad skupiny (GPO) přes konfiguraci požadovaného stavu (DSC):
    1. Převod objektu zásad skupiny na DSC – [projekt pro správu standardních hodnot Microsoft](https://github.com/Microsoft/BaselineManagement) v GitHubu může toto úsilí zrychlit. Nezapomeňte úložiště DSC ukládat do úložiště paralelně s Správce prostředků šablonou.
    2. Nasaďte konfiguraci stavu Azure Automation na jakékoli instance podnikového předplatného. Azure Automation lze použít k nasazení DSC na virtuální počítače nasazené v podporovaných předplatných ve skupině pro správu.
    3. Aktuální plán plánu umožňuje povolit vlastní zásady konfigurace hostů. Po vydání této funkce již nebude nutné používat Azure Automation v tomto osvědčeném postupu.

**Použití dodatečného řízení v rámci předplatného pro přijetí do cloudu (paprsky):** Při sestavování na `Corporate IT Subscription`se můžou v rámci každého předplatného, který je vyhrazený pro podporu aplikace archetypes, získat i drobné změny.

V předchozích iterativních změnách osvědčených postupů jsme definovali skupiny zabezpečení sítě k blokování veřejného provozu a povoleného interního provozu. Kromě toho Azure detailly dočasně vytvořil služby DMZ a funkce Active Directory. V této iteraci tyto assety přizpůsobíme trochu a vytvoříme novou verzi plánu Azure details.

1. Šablona partnerského vztahu k síti Tato šablona se bude navázat na virtuální síť v každém předplatném s virtuální sítí centra ve firemním předplatném.
    1. Referenční architektura z předchozí části, [topologie centra a paprsků se sdílenými službami](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)vygenerovala šablonu správce prostředků pro povolení partnerského vztahu virtuální sítě.
    2. Tuto šablonu lze použít jako vodítko pro úpravu šablony DMZ z předchozí iterace zásad správného řízení.
    3. Nyní přidáváme partnerský vztah virtuálních sítí k virtuální síti DMZ, která byla dříve připojena k místnímu hraničnímu zařízení přes síť VPN.
    4. SÍŤ VPN by se taky měla z této šablony odebrat a zároveň zajistit, aby se žádný provoz nesměroval přímo do místního datového centra bez předávání podnikového a bezpečnostního řešení v podniku. Tuto síť VPN můžete nastavit také jako okruh převzetí služeb při selhání v případě outge okruhu ExpressRoute.
    5. Azure Automation pro použití DSC na hostované virtuální počítače bude vyžadovat další [konfiguraci sítě](https://docs.microsoft.com/azure/automation/automation-dsc-overview#network-planning) .
2. Upravte skupinu zabezpečení sítě. Zablokuje všechny veřejné **a** přímé místní přenosy ve skupině zabezpečení sítě. Jediný příchozí provoz by měl projít partnerským vztahem virtuální sítě v podnikovém předplatném IT.
    1. V předchozí iteraci se vytvořila skupina zabezpečení sítě, která blokuje veškerý veřejný provoz a seznam povolených interních přenosů. Teď chceme tuto skupinu zabezpečení sítě posunout o bit.
    2. Nová konfigurace skupiny zabezpečení sítě by měla blokovat všechny veřejné přenosy společně se všemi přenosy z místního datacentra.
    3. Provoz přicházející do této virtuální sítě by měl pocházet jenom z virtuální sítě na druhé straně partnerského uzlu virtuální sítě.
3. Azure Security Center implementace:
    1. Nakonfigurujte Azure Security Center pro všechny skupiny pro správu, které obsahují chráněné klasifikace dat.
    2. Nastavte Automatické zřizování na zapnuto ve výchozím nastavení, aby se zajistilo dodržování předpisů.
    3. Navažte konfigurace zabezpečení operačního systému. Zabezpečení IT pro definování konfigurace.
    4. Při počátečním používání Azure Security Center podporují zabezpečení IT. Využijte k zabezpečení IT Security Center, ale Udržujte přístup pro účely průběžného zlepšování zásad správného řízení.
    5. Vytvořte šablonu Správce prostředků odrážející změny požadované pro Azure Security Center konfiguraci v rámci předplatného.
4. Aktualizuje Azure Policy pro všechna předplatná.
    1. Auditování a vykonání kritické klasifikace a klasifikace dat napříč všemi skupinami pro správu a odběry k identifikaci všech předplatných s chráněnými klasifikacemi dat.
    2. Používejte audit a vynuťte jenom schválené image operačního systému.
    3. Proveďte audit a vystavování konfigurací hostů na základě požadavků zabezpečení pro každý uzel.
5. Aktualizuje Azure Policy pro všechna předplatná, která obsahují chráněné klasifikace dat.
    1. Auditovat a vymáhat použití jenom standardních rolí
    2. Auditovat a vymáhat šifrování pro všechny účty úložiště a soubory v klidovém umístění na jednotlivých uzlech.
    3. Audit a prosazování aplikace nové verze skupiny zabezpečení sítě DMZ.
    4. Audituje a vynutil používání schválené podsítě sítě a virtuální sítě na síťové rozhraní.
    5. Audituje a vynutil omezení uživatelem definovaných směrovacích tabulek.
6. Podrobný plán Azure:
    1. Vytvořte podrobný plán Azure s názvem `protected-data`.
    2. Přidejte do podrobného plánu šablony VNet peer, Network Security Group a Azure Security Center.
    3. Ujistěte se, že šablona pro službu Active Directory z předchozí iterace **není** zahrnutá do podrobného plánu. Jakékoli závislosti na službě Active Directory poskytne firemní předplatné IT.
    4. Ukončete všechny existující virtuální počítače služby Active Directory nasazené v předchozí iteraci.
    5. Přidejte nové zásady pro odběry chráněných dat.
    6. Publikovat podrobný plán do jakékoli skupiny pro správu, která bude hostovat chráněná data.
    7. Použijte nový podrobný plán na všechny ovlivněné předplatné společně s existujícími plány.

## <a name="conclusion"></a>Závěr

Přidání těchto procesů a změn do procesu MVP pro řízení bezpečnosti pomáhá napravit mnoho rizik spojených se zabezpečením zásad správného řízení. Společně přidávají nástroje pro monitorování sítě, identity a zabezpečení potřebné k ochraně dat.

## <a name="next-steps"></a>Další kroky

V případě, že se přijetí cloudu pokračuje a přináší další obchodní hodnoty, rizika a potřeby zásad správného řízení cloudu. Pro fiktivní společnost v tomto průvodci je dalším krokem podpora důležitých úloh. To je bod, když jsou potřebné ovládací prvky konzistence prostředků.

> [!div class="nextstepaction"]
> [Zlepšení oboru konzistence prostředků](./resource-consistency-improvement.md)
