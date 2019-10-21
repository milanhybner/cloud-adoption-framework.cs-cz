---
title: Pokyny pro zabezpečení Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Jaké doprovodné materiály k zabezpečení poskytuje společnost Microsoft?
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8449878d46c939c58f690e585aac07fa0e827484
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548059"
---
<!-- markdownlint-disable MD026 -->

# <a name="microsoft-security-guidance"></a>Doprovodné materiály k zabezpečení Microsoftu

## <a name="tools"></a>Nástroje

Společnost Microsoft představila platformu a správce dodržování předpisů [Service trustu](https://servicetrust.microsoft.com) , která vám může pomáhat s těmito nástroji:

- Překonání problémů se správou dodržování předpisů.
- Plnění odpovědností za zákonné požadavky na splnění předpisů
- Provádějte audity samoobslužných služeb a posouzení rizik využívání podnikových cloudových služeb.

Tyto nástroje jsou navržené tak, aby pomáhaly organizacím, které splňují složité povinnosti dodržování předpisů a zlepšují možnosti ochrany dat při výběru a používání služby Microsoft Cloud Services.

**Platforma STP (Service Trust Platform)** poskytuje podrobné informace a nástroje, které vám pomůžou splnit vaše požadavky na používání služby Microsoft Cloud Services, včetně Azure, Office 365, Dynamics 365 a Windows. STP je jedním z důvodů zabezpečení, regulace, dodržování předpisů a ochrany osobních údajů, které souvisejí s Microsoft Cloud. V takovém případě zveřejňujeme informace a prostředky, které jsou potřeba k tomu, aby bylo možné vyhodnotit rizika pro službu Cloud Services a nástroje. Vytvořili jsme STP, který vám pomůže sledovat aktivity dodržování předpisů v rámci Azure, včetně těchto:

- **Správce dodržování předpisů:** Správce dodržování předpisů, nástroj pro vyhodnocení rizik na základě pracovního postupu na platformě Microsoft Service Trust Service, umožňuje sledovat, přiřazovat a ověřovat aktivity dodržování předpisů v souladu s Microsoft Cloud službami vaší organizace, jako je například Office 365, Dynamics. 365 a Azure. Další podrobnosti najdete v další části.
- **Dokumenty důvěryhodnosti:** V současné době existují tři kategorie průvodců, které vám poskytnou bohatou prostředky k vyhodnocení Microsoft Cloud; Přečtěte si o provozu Microsoftu v souvislosti se zabezpečením, dodržováním předpisů a ochranou soukromí a pomáhá vám působit na vylepšení funkcí ochrany dat. Mezi ně patří:
- **Sestavy auditování:** Sestavy auditu vám umožní udržet si aktuální informace o nejnovějších informacích o ochraně osobních údajů, zabezpečení a dodržování předpisů pro Microsoft Cloud služby. Patří mezi ně ISO, SOC, FedRAMP a další zprávy o auditu, mostové dopisy a materiály související s nezávislými audity třetích stran služby Microsoft Cloud Services, jako je Azure, Office 365, Dynamics 365 a další.
- **Průvodci ochranou dat:** Průvodci ochranou dat poskytují informace o tom, jak Microsoft Cloud služby chrání vaše data a jak můžete spravovat zabezpečení cloudových dat a dodržování předpisů pro vaši organizaci. Patří sem obsáhlé dokumenty White Paper, které poskytují podrobné informace o tom, jak Microsoft navrhuje a provozuje cloudové služby, nejčastější dotazy, zprávy o posouzení zabezpečení na konci roku, výsledky testů průniku a Rady, které vám pomůžou při vyhodnocování rizik a zlepšování vašich dat. možnosti ochrany.
- **Plán zabezpečení a dodržování předpisů v Azure:** Podrobné plány poskytují prostředky, které vám pomůžou vytvářet a spouštět cloudové aplikace, které vám pomohou dodržovat přísné předpisy a standardy. S více certifikacemi než s jakýmkoli jiným poskytovatelem cloudu můžete mít jistotu, že vaše nejdůležitější úlohy budou nasazovat do Azure s využitím plánů, které zahrnují:
  - Přehled a doprovodné materiály pro konkrétní obor
  - Tabulka odpovědností pro zákazníky
  - Referenční architektury s modely hrozeb.
  - Řízení matic implementace.
  - Automatizace pro nasazení referenčních architektur.
  - Zdroje informací o ochraně osobních údajů: dokumentace pro posouzení dopadu ochrany dat, žádosti subjektů údajů (PSÚ) a oznámení o porušení dat se začlení do vlastního programu pro zodpovědnosti v podpoře Obecné nařízení o ochraně osobních údajů (GDPR).
- **Začínáme s GDPR:** Produkty a služby společnosti Microsoft můžou organizacím splňovat požadavky GDPR při shromažďování nebo zpracování osobních údajů. STP je navržený tak, aby vám poskytl informace o schopnostech služeb Microsoft, které můžete použít k řešení konkrétních požadavků služby GDPR. Dokumentace může přispět k GDPR zodpovědnosti a porozumění technickým a organizačním opatřením. Dokumentace k posouzení dopadu na ochranu dat, žádosti subjektů údajů (PSÚ) a oznámení o porušení dat se začlení do vlastního programu pro zodpovědnosti v podpoře GDPR.
  - **Žádosti subjektu údajů:** GDPR uděluje jednotlivcům (nebo subjektům údajů) určitá práva v souvislosti se zpracováním jejich osobních údajů. To zahrnuje právo opravit nepřesná data, vymazat data nebo omezit jejich zpracování, jakož i přijmout data a splnit požadavek na přenos dat na jiný kontroler.
  - **Porušení dat:** GDPR vyžaduje požadavky na oznámení pro řadiče a procesory dat v případě porušení osobních údajů. STP poskytuje informace o tom, jak se společnost Microsoft snaží zabránit narušením prvního místa, jak společnost Microsoft zjistí porušení a jak bude Microsoft reagovat v případě porušení a upozorní vás jako řadič dat.
  - **Posouzení dopadu na ochranu dat:** Microsoft pomáhá řadičům doplňovat GDPRy dopadu na ochranu dat. GDPR poskytuje úplný seznam případů, ve kterých je nutné provést DPIAs, jako je automatické zpracování pro účely profilace a podobných aktivit. zpracování ve velkém měřítku speciálních kategorií osobních údajů a systematického monitorování veřejně přístupné oblasti ve velkém měřítku.
  - **Další zdroje informací:** Kromě pokynů uvedených v předchozích částech STP také poskytuje další zdroje, včetně regionálního dodržování předpisů, dalších prostředků pro Centrum zabezpečení a dodržování předpisů a nejčastější dotazy k platformě důvěryhodnosti služby. Správce dodržování předpisů a soukromí/GDPR.
- **Regionální dodržování předpisů:** STP poskytuje řadu dokumentů a pokynů pro dodržování předpisů pro Microsoft online služby, které splňují požadavky na dodržování předpisů pro různé oblasti, včetně České republiky, Polska a Rumunska.

## <a name="unique-intelligent-insights"></a>Jedinečné inteligentní přehledy

Jak se rozroste objem a složitost signálů zabezpečení, určení, jestli jsou tyto signály věrohodné, a pak jednají, trvá moc dlouho. Microsoft nabízí nesrovnatelnou škálu služby Security Intelligence poskytované v cloudovém měřítku, které vám pomůžou rychle detekovat a opravovat hrozby. [Další informace](https://docs.microsoft.com/azure/security-center/security-center-intro)

## <a name="azure-threat-intelligence"></a>Azure Threat Intelligence

Pomocí možnosti analýzy hrozeb, která je dostupná ve službě Security Center, můžou správci IT identifikovat bezpečnostní hrozby pro prostředí. Například můžou určit, jestli je konkrétní počítač součástí botnetu. Z počítačů se můžou stát uzly v botnetu, když útočníci neoprávněně nainstalují malware, který tajně připojí počítač k řídicímu serveru. Analýza hrozeb dokáže identifikovat také potenciální hrozby přicházející z alternativních komunikačních kanálů, jako je například dark web.

Služba Security Center k sestavení této analýzy hrozeb používá data přicházející z několika zdrojů v rámci Microsoftu. Security Center používá tuto možnost k identifikaci potenciálních hrozeb pro vaše prostředí. Podokno Analýza hrozeb se skládá ze tří hlavních možností:

- Zjištěné typy hrozeb
- Původ hrozeb
- Mapa analýzy hrozeb

## <a name="machine-learning-in-azure-security-center"></a>Machine Learning v Azure Security Center

Azure Security Center hluboko analyzuje širokou škálu dat z nejrůznějších řešení Microsoftu a partnerů, která vám pomůžou dosáhnout vyššího zabezpečení. Aby bylo možné využít tato data, společnost používá datové vědy a strojové učení pro prevenci, detekci a nakonec šetření hrozeb.

V podstatě Azure Machine Learning pomáhá dosáhnout dvou výsledků:

## <a name="next-generation-detection"></a>Zjišťování nové generace

Útočníci jsou stále častěji automatizovanější a sofistikovanější. Využívají taky datovou vědu. Poskytují zpětnou ochranu a systémy sestavování, které podporují mutace v chování. Maskují své aktivity jako šum a rychle se seznámí s chybami. Machine Learning nám pomáhá reagovat na tyto vývojy.

## <a name="simplified-security-baseline"></a>Zjednodušené standardní hodnoty zabezpečení

Efektivní rozhodování o zabezpečení není snadné. Vyžaduje prostředí zabezpečení a odbornost. I když některé velké organizace mají tyto odborníky na zaměstnance, mnoho společností ne. Azure Machine Learning zákazníkům umožňuje těžit z vyhodnocení informací získaných jiných organizací při rozhodování o zabezpečení.

## <a name="behavioral-analytics"></a>Behaviorální analýza

Behaviorální analýza je technika, která analyzuje a porovnává data se sadou známých schémat. Tato schémata však nepředstavují jednoduché příznaky. Jsou určeny prostřednictvím složitých algoritmů strojového učení, které jsou aplikovány na obrovský datový sklad. Určují se také prostřednictvím pečlivé analýzy škodlivého chování, kterou provádí zkušení analytici. Azure Security Center může pomocí analýzy chování identifikovat ohrožené prostředky na základě analýzy protokolů virtuálních počítačů, protokolů virtuálních síťových zařízení, protokolů prostředků infrastruktury, výpisů stavu systému a dalších zdrojů.
