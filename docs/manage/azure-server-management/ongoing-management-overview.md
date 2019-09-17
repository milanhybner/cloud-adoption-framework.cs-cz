---
title: Průběžná správa a zabezpečení
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Průběžná správa a zabezpečení
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7b77181dd8ef6efe655b56489e5d4e6b210382b6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028139"
---
# <a name="phase-3-ongoing-management-and-security"></a>Fáze 3: Průběžná správa a zabezpečení

Po připojení služby Azure Management Services se budete muset zaměřit na operace a konfigurace zabezpečení, které budou podporovat vaše probíhající operace. Začneme s zabezpečením vašeho prostředí, a to kontrolou Azure Security Center. Pak nakonfigurujeme zásady, aby vaše servery byly v souladu s předpisy a automatizují běžné úlohy. Tato část obsahuje následující témata:

- **[Vyřešte doporučení pro zabezpečení.](#address-security-recommendations)** Azure Security Center poskytuje návrhy na vylepšení zabezpečení vašeho prostředí. Při implementaci těchto doporučení uvidíte dopad, který se projeví ve skóre zabezpečení.
- **[Povolte zásady konfigurace hostů.](./guest-configuration-policy.md)** Povolte funkci konfigurace hosta Azure Policy k auditování nastavení ve virtuálním počítači. Můžete například zjistit, jestli vyprší platnost jakýchkoli certifikátů.
- **[Sledovat kritické změny a upozorňovat na ně.](./enable-tracking-alerting.md)** Při řešení potíží je první otázka, kterou je třeba vzít v úvahu, "co se změnilo?" V tomto článku se dozvíte, jak sledovat změny a vytvářet výstrahy pro proaktivní monitorování důležitých součástí.
- **[Vytvořte plány aktualizací.](./update-schedules.md)** Naplánujte instalaci aktualizací, abyste zajistili, že všechny vaše servery budou mít nejnovější.
- **[Příklady běžných Azure Policy.](./common-policies.md)** V této části najdete příklady běžných zásad správy.

## <a name="address-security-recommendations"></a>Řešení bezpečnostních doporučení

Azure Security Center je centrální místo pro správu zabezpečení pro vaše prostředí. Zobrazí se obecná doporučení pro posouzení a cílení.

Doporučujeme, abyste zkontrolovali a implementovali doporučení poskytovaná touto službou. Informace o dalších výhodách Azure Security Center najdete v tématu [postup Azure Security Center doporučení](https://docs.microsoft.com/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Další postup

Naučte se [, jak povolit funkci konfigurace hosta Azure Policy](./guest-configuration-policy.md) .

> [!div class="nextstepaction"]
> [Zásada konfigurace hosta](./guest-configuration-policy.md)
