---
title: Seznámení s dodržováním předpisů
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznámení s dodržováním předpisů
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b0bc28f46671c4ccf62bba9f3fa68f14e2b79aee
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028936"
---
# <a name="introduction-to-regulatory-compliance"></a>Seznámení s dodržováním předpisů

Toto je úvodní článek o dodržování předpisů, proto není určený pro implementaci strategie dodržování předpisů. Je jenom pro obecné povědomí. Podrobnější informace o [nabídkách dodržování předpisů Azure](https://aka.ms/allcompliance) jsou k dispozici na [webu Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx). Veškerá dokumentace ke stažení je navíc k dispozici pro některé zákazníky Azure na [portálu Microsoft Trust Service](https://servicetrust.microsoft.com).

Dodržování legislativních předpisů odkazuje na disciplínu a proces zajištění toho, aby společnost dodržovala právní předpisy, kterými se řídí orgány v jejich geografických nebo pravidelch, které musí dobrovolně přijmout oborové standardy. Pro dodržování předpisů v oblasti IT můžou lidé a procesy monitorovat firemní systémy ve snaze zjistit a zabránit porušení zásad a postupů, které vytvořily tyto zákony, předpisy a standardy. To zase platí pro nejrůznější procesy monitorování a vynucení. V závislosti na oboru a zeměpisné oblasti se můžou tyto procesy navzájem zdlouhavé a složitě.

Dodržování předpisů je náročné u více národních organizací, zejména v silně regulovaných oborech, jako je zdravotní péče a finanční služby. Normy a předpisy Abound a v některých případech se můžou často měnit, takže podniky budou mít jistotu, že se měnícími se mezinárodními elektronickými zákony na zpracování dat.

Stejně jako u bezpečnostních mechanismů by organizace měly pochopit rozdělení odpovědností na dodržování legislativních předpisů v cloudu. Poskytovatelé cloudu usilují o zajištění kompatibility jejich platforem a služeb. Ale organizace musí také potvrdit, že jejich aplikace, infrastruktura těchto aplikací závisí na službách, které poskytují třetí strany, jsou také certifikované jako vyhovující.

Níže jsou uvedeny popisy předpisů v oblasti dodržování předpisů v různých odvětvích a zeměpisných oblastech:

## <a name="hipaa"></a>HIPAA

Aplikace zdravotní péče, která zpracovává chráněné informace o stavu (FÍ), podléhá pravidlu ochrany osobních údajů a bezpečnostnímu pravidlu, které se zahrnuje v rámci přenositelnosti informací o stavu a jednání s zodpovědností (HIPAA). HIPAA pravděpodobně vyžaduje, aby zdravotní péče od poskytovatele cloudu obdržela písemná ujištění od poskytovatele cloudu, že bude chránit případné obdržené nebo vytvořené FÍ.

## <a name="pci"></a>PCI

Standard zabezpečení dat v odvětví platebních karet (PCI DSS) je bezpečnostní standard pro organizace, které zpracovávají kreditní karty od hlavních systémů, včetně víz, MasterCard, American Express, Discover a JCB. Standard PCI se řídí značkami karet a spravuje se v rámci Rady standardů zabezpečení v oboru platební karty. Byl vytvořen Standard, který zvyšuje ovládací prvky kolem dat karty SmartCard, aby se snížilo podvodná platební karta. Ověřování dodržování předpisů se provádí jednou ročně, buď pomocí externího nástroje QUALIFIED Security ASSESSOR (External Qualified Security posuzovatel), nebo pomocí nástroje ISA (Internal Security hodnotitel), který vytváří zprávu o dodržování předpisů (ROC) pro organizace, které zpracovávají velké objemy transakcí, nebo Dotazník pro samočinný odhad (SAQ) pro společnosti.

## <a name="personal-data"></a>Osobní údaje

Osobní údaje jsou informace, které se dají použít k identifikaci spotřebitele, zaměstnance, partnera nebo jakékoli jiné živé nebo právnické osoby. Řada nově vznikajících zákonů, zejména těch, které se týkají ochrany osobních údajů a osobních údajů, vyžadují, aby podniky samy dodržovaly a nahlásily dodržování předpisů a všechna porušení, která by mohla nastat.

## <a name="gdpr"></a>GDPR

Jedním z nejdůležitějších vývojů v této oblasti je poslední enactment v rámci Evropské Komise Obecné nařízení o ochraně osobních údajů (GDPR), která je určená k posílení ochrany dat pro jednotlivce v rámci Evropské unie. GDPR vyžaduje, aby data týkající se jednotlivců (například jméno, adresa domů, fotografie, e-mailová adresa, informace o bance, příspěvky na webech sociálních sítí, lékařské informace nebo IP adresy počítače) byla udržována na serverech v rámci EU a nepřenesly se. z nich. Také vyžaduje, aby společnosti oznámily jednotlivcům na všechna porušení dat a pověření, která mají společnosti inspektor ochrany dat (DPO). Jiné země mají nebo vyvíjí podobné typy předpisů.

## <a name="compliant-foundation-in-azure"></a>Vyhovující základ v Azure

Pro pomoc zákazníkům, kteří splnili vlastní povinnosti dodržování předpisů napříč regulovanými průmyslovými odvětvími a trhy po celém světě,&mdash;Azure udržuje největší portfolio dodržování předpisů v oboru (celkový počet nabídek) a také hloubku (počet služby pro zákazníky v oboru posouzení. Nabídky dodržování předpisů Azure se seskupují do čtyř segmentů: globálně použitelné, státní správa USA, Oborová, specifická pro konkrétní odvětví a oblast nebo země.

Nabídky dodržování předpisů Azure vycházejí z různých typů ujištění, včetně formálních certifikací, atestů, ověření, autorizací a hodnocení vyprodukovaných nezávislými společnostmi auditování třetích stran, jakož i smluvních změn. samoobslužné posouzení a dokumenty s pokyny pro zákazníky, které vytvořil Microsoft. Popis každé nabídky v tomto dokumentu poskytuje aktuální příkaz Scope, který označuje, které služby Azure zaměřené na zákazníky jsou v oboru pro posouzení, a odkazy na materiály ke stažení, které pomáhají zákazníkům s jejich vlastním dodržováním předpisů. povinnosti.

Podrobnější informace o nabídkách dodržování předpisů Azure jsou k dispozici na [webu Microsoft Trust Center](https://www.microsoft.com/trustcenter/compliance/complianceofferings). Veškerá dokumentace ke stažení je navíc k dispozici pro určité zákazníky Azure z [portálu Trust Service](https://servicetrust.microsoft.com) v následujících částech:

- **Sestavy auditování:** Obsahuje oddíly pro sestavy FedRAMP, GRC Assessment, ISO, PCI DSS a SOC.
- **Prostředky ochrany dat:** Zahrnuje Průvodce dodržováním předpisů, nejčastější dotazy a dokumenty White Paper a části posouzení zabezpečení a testování zabezpečení.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o připravenosti cloudového zabezpečení.

> [!div class="nextstepaction"]
> [Připravenost na zabezpečení cloudu](./cloud-security-readiness.md)
