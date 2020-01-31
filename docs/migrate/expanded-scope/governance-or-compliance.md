---
title: Strategie pro zásady správného řízení nebo dodržování předpisů
description: Strategie pro zásady správného řízení nebo dodržování předpisů
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 17952dc4c3ff28f2fcfe1a378a9efb969d65925b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803122"
---
# <a name="governance-or-compliance-strategy"></a>Strategie pro zásady správného řízení nebo dodržování předpisů

Když se v průběhu migrace vyžadují zásady správného řízení nebo dodržování předpisů, je zapotřebí rozšířit rozsah. Následující pokyny rozšíří rozsah [Průvodce migrací do Azure](../azure-migration-guide/index.md) o různé přístupy při řešení požadavků na zásady správného řízení nebo dodržování předpisů.

## <a name="general-scope-expansion"></a>Obecné rozšíření rozsahu

Při požadavku na zásady správného řízení nebo dodržování předpisů jsou nejvíce ovlivněny aktivity související s předpoklady. Během posouzení, migrace a optimalizace mohou být vyžadovány další úpravy.

## <a name="suggested-prerequisites"></a>Doporučené požadavky

Konfigurace základního prostředí Azure se při integraci požadavků na zásady správného řízení nebo dodržování předpisů může významně změnit. Abyste měli představu o tom, jak se předpoklady změní, je důležité pochopit charakter těchto požadavků. Před zahájením jakékoli migrace, která vyžaduje zásady správného řízení nebo dodržování předpisů, by se měl zvolit některý přístup a implementovat v cloudovém prostředí. Následuje přehled několika přístupů, které se během migrace běžně používají:

**Společný přístup pro řízení přístupu:** Pro většinu organizací je [model zásad správného řízení v cloudu](../../govern/guides/index.md) , který se skládá z implementace minimální životaschopného produktu (MVP), a za ním i cílené iterace v rámci předplatných, která řeší hmotná rizika zjištěná v plánu přijetí. Tento přístup poskytuje minimální nástroje potřebné ke stanovení konzistentních zásad správného řízení, aby se tým mohl s těmito nástroji seznámit. Následně se rozšíří na nástroje, které řeší obecné záležitosti zásad správného řízení.

**Plány kompatibility ISO 27001:** Pro zákazníky, kteří musí dodržovat standardy dodržování předpisů ISO, ukázky podrobného plánu pro [sdílené služby iso 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared/index) můžou sloužit jako efektivnější MVP k vytváření rozsáhlejších omezení zásad správného řízení dříve v iterativním procesu. [Ukázka App Service Environment/SQL Database ISO 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload) rozšiřuje tento podrobný plán o mapování kontrol a nasazení společné architektury pro prostředí aplikace. Další vydané podrobné plány dodržování předpisů zde budou rovněž zmíněny.

**Virtuální datové centrum:** Je možné, že bude potřeba mít robustnější počáteční bod zásad správného řízení. V takových případech uvažujte o [virtuálním datacentru Azure](../../reference/vdc.md). Tento přístup se během přechodu do cloudu na podnikové úrovni navrhuje běžně, zejména v případech s více než 10 000 prostředky. Je to také faktická volba pro komplexní scénáře zásad správného řízení, kdy se vyžaduje zajištění dodržování předpisů třetích stran ve velkém objemu, hluboké znalosti domén nebo parita s vyspělými zásadami správného řízení IT a požadavky dodržování předpisů.

### <a name="partnership-option-to-complete-prerequisites"></a>Volba partnerství pro dokončení předpokladů

**Služby Microsoftu:** Služby společnosti Microsoft poskytují nabídky řešení, které se dají zarovnat k modelu zásad správného řízení v cloudu, plánů dodržování předpisů nebo k možnostem virtuálního datového centra, abyste zajistili nejvhodnější model zásad správného řízení nebo dodržování předpisů. Pomocí nabídky řešení [SCI (Secure Cloud Insights)](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) vytvořte daty řízený obrázek zákaznického nasazení v Azure a během toho, co budete zjišťovat optimalizaci existujících architektur nasazení a eliminovat rizika související se zabezpečením a dostupností zásad správného řízení, ověřte vyspělost zákaznické implementace v Azure. Na základě těchto poznatků o zákazníkovi byste měli přijít s následujícími přístupy:

- **Cloud Foundation:** Stanovte základní návrhy Azure, vzory a architekturu zásad správného řízení pomocí nabídky řešení [Hybrid Cloud Foundation (HCF)](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) . Namapujte požadavky zákazníka na nejvhodnější referenční architekturu. Implementujte minimální realizovatelný produkt sestávající ze sdílených služeb a úloh IaaS.
- **Modernizace cloudu:** Řešení [moderního cloudu](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) nabízíme jako ucelený přístup k přesunu aplikací, dat a infrastruktury do cloudu připraveného pro podniky a také k optimalizaci a modernizovatí po nasazení cloudu.
- Inovace **pomocí cloudu:** Zapojte zákazníka prostřednictvím inovativního a jedinečného řešení [Cloud Center vynikajícího cloudu (CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) , které vytvoří moderní organizaci IT, která umožní flexibilitu ve velkém měřítku s DevOps a přitom zůstává v řízení. Implementuje agilní přístup k zaznamenání firemních požadavků, opakovanému použití balíčků nasazení v souladu se zásadami zabezpečení, dodržování předpisů a správy služeb, a udržuje platformu Azure v souladu s provozními postupy.

## <a name="assess-process-changes"></a>Změny procesu posouzení

Během posuzování je potřeba učinit další rozhodnutí, aby bylo vše v souladu s požadovaným přístupem k zásadám správného řízení. Tým zásad správného řízení cloudu by měl všem členům týmu přechodu na cloud před posouzením úlohy poskytnout všechny zprávy o zásadách, pokyny k architektuře nebo požadavky na zásady správného řízení/dodržování předpisů.

### <a name="suggested-action-during-the-assess-process"></a>Navrhovaná akce během procesu vyhodnocení

Požadavky na posouzení zásad správného řízení a dodržování předpisů jsou příliš zákaznicky specifické, takže nelze poskytnout obecné pokyny pro skutečný postup posuzování. Proces by ale měl zahrnovat úlohy a časová přidělení pro "zarovnání na dodržování předpisů/požadavky zásad správného řízení". Další informace o těchto požadavcích najdete pod následujícími odkazy:

Chcete-li lépe porozumět zásadám správného řízení, přečtěte si přehled [Pět disciplín zásad správného řízení v cloudu](../../govern/governance-disciplines.md). Tato část Architektury přechodu na cloud obsahuje také šablony pro dokumentaci zásad, pokynů a požadavků pro každý z těchto pěti oddílů:

- [Správa nákladů:](../../govern/cost-management/template.md)
- [Standardní hodnoty zabezpečení](../../govern/security-baseline/template.md)
- [Konzistence prostředků].. /.. /govern/resource-consistency/template.md)
- [Směrný plán identity]... /.. /govern/identity-baseline/template.md)
- [Zrychlení nasazení](../../govern/deployment-acceleration/template.md)

Rady k vytvoření pokynů pro zásady správného řízení na základě modelu zásad správného řízení Architektury přechodu na cloud najdete v článku [Implementace strategie zásad správného řízení v cloudu](../../govern/corporate-policy.md).

## <a name="optimize-and-promote-process-changes"></a>Změny procesu optimalizace a povýšení

V rámci optimalizačních a propagačních procesů tým zásad správného řízení cloudu měli investovat čas do testování a ověřování dodržování standardů dodržování předpisů a dodržování předpisů. V tomto kroku je také vhodné předat týmu zásad správného řízení cloudu procesy pro výběr šablon, které by u budoucích projektů mohly dále [urychlit nasazení](../../govern/deployment-acceleration/index.md).

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Navrhovaná akce během procesu optimalizace a povýšení

Během tohoto procesu by měl plán projektu zahrnovat časovou kapacitu pro tým zásad správného řízení cloudu, aby mohl spustit kontrolu dodržování předpisů pro jednotlivé úlohy plánované pro zvýšení produkčního prostředí.

## <a name="next-steps"></a>Další kroky

Jako poslední položku v [rozbaleném kontrolním seznamu oboru](./index.md)se vraťte do kontrolního seznamu a znovu vyhodnoťte všechny další požadavky na rozsah pro účely migrace.

> [!div class="nextstepaction"]
> [Kontrolní seznam pro rozšířený rozsah](./index.md)
