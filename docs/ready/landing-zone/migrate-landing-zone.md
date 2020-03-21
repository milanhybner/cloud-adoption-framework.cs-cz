---
title: Nasazení cílové zóny migrace v Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Přečtěte si, jak cílovou zónu migrace v Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1727bb9c77298663f30e6205a9a3230ce65be3c1
ms.sourcegitcommit: 5d7e93540a679252f1c7207e62cb2ee7213a6ae9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80069752"
---
<!-- cSpell:ignore vCPUs jumpbox -->

# <a name="deploy-a-migration-landing-zone"></a>Nasazení cílové zóny migrace

Termín *cílová zóna migrace* se používá k popisu prostředí, které je zřízené a připravené k hostování úloh migrovaných z místního prostředí do Azure.

## <a name="deploy-the-first-landing-zone"></a>Nasazení první cílové zóny

Předtím, než použijete cílovou zónu migrace v rámci architektury pro přijetí do cloudu, prostudujte si následující předpoklady, rozhodnutí a pokyny k implementaci. Pokud se tyto pokyny zarovnají s požadovaným plánem přijetí do cloudu, je možné pomocí [kroků nasazení][deploy-sample]nasadit [cílovou zónu migrace](https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/index) .

> [!div class="nextstepaction"]
> [Nasazení ukázky podrobného plánu][deploy-sample]

## <a name="assumptions"></a>Předpoklady

Tato počáteční cílová zóna zahrnuje následující předpoklady nebo omezení. Pokud tyto předpoklady odpovídají vašim omezením, můžete podrobný plán použít k vytvoření první cílové zóny. Plán lze také rozšířit a vytvořit tak podrobný plán cílové zóny, který vyhovuje vašim jedinečným omezením.

- **Omezení předplatného:** Toto úsilí o přijetí neočekává překročení [limitů předplatného](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Dodržování předpisů:** V této cílové zóně nejsou potřeba žádné požadavky na dodržování předpisů od jiných výrobců.
- **Složitost architektury:** Složitost architektury nevyžaduje další produkční odběry.
- **Sdílené služby:** V Azure nejsou žádné sdílené služby, které vyžadují, aby se toto předplatné zpracovalo jako paprskový uzel v architektuře hvězdicové architektury.
- **Omezený rozsah produkčního prostředí:** Tato cílová zóna by mohla být hostitelem produkčních úloh. Nejedná se však o vhodné prostředí pro citlivá data ani pro klíčové úlohy.

Pokud tyto předpoklady odpovídají vašim požadavkům na přijetí, může být tento plán výchozím bodem pro vytváření cílové zóny.

## <a name="decisions"></a>Rozhodnutí

V podrobném plánu cílové zóny jsou zastoupena následující rozhodnutí.

| Komponenta                    | Rozhodnutí                                                                                         | Alternativní přístupy                                                                                                                                                                                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nástroje pro migraci              | Nasadí se Azure Site Recovery a vytvoří se projekt Azure Migrate.                | [Průvodce rozhodováním ohledně nástrojů pro migraci](../../decision-guides/migrate-decision-guide/index.md)                                                                                                                                                                                              |
| Protokolování a monitorování       | Bude zřízený pracovní prostor Operational Insights a účet úložiště pro diagnostiku.                |                                                                                                                                                                                                                                                                                      |
| Síť                      | Vytvoří se virtuální síť s podsítěmi pro bránu, firewall, jumpbox a cílovou zónu.  | [Rozhodnutí o síti](../considerations/networking-options.md)                                                                                                                                                                                                                      |
| Identita                     | Předpokládá se, že předplatné je už přidružené k instanci Azure Active Directory. | [Osvědčené postupy správy identit](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) |
| Zásady                       | Tento podrobný plán v současné době předpokládá, že se nemají použít žádné zásady Azure.                        |                                                                                                                                                                                                                                                                                      |
| Návrh předplatného          | Neuvedeno – Navrženo pro jedno produkční předplatné.                                              | [Škálování předplatných](../azure-best-practices/scaling-subscriptions.md)                                                                                                                                                                                                            |
| Skupiny pro správu            | Neuvedeno – Navrženo pro jedno produkční předplatné.                                              | [Škálování předplatných](../azure-best-practices/scaling-subscriptions.md)                                                                                                                                                                                                            |
| Skupiny prostředků              | Neuvedeno – Navrženo pro jedno produkční předplatné.                                              | [Škálování předplatných](../azure-best-practices/scaling-subscriptions.md)                                                                                                                                                                                                            |
| Data                         | NEUŽÍVÁ SE.                                                                                               | [Výběr správné možnosti SQL Server v dokumentaci k Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) a [Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview)                      |
| Úložiště                      | NEUŽÍVÁ SE.                                                                                               | [Pokyny k Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                                       |
| Standardy pojmenování a označování | NEUŽÍVÁ SE.                                                                                               | [Osvědčené postupy pojmenování a označování](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                                                   |
| Správa nákladů              | NEUŽÍVÁ SE.                                                                                               | [Sledování nákladů](../azure-best-practices/track-costs.md)                                                                                                                                                                                                                             |
| Výpočty                      | NEUŽÍVÁ SE.                                                                                               | [Možnosti služby Compute](../considerations/compute-options.md)                                                                                                                                                                                                                              |

## <a name="customize-or-deploy-a-landing-zone"></a>Přizpůsobení nebo nasazení cílové zóny

Přečtěte si další informace a Stáhněte si referenční ukázku v tématu Postup migrace cílové zóny pro nasazení nebo přizpůsobení z [Azure Blueprint Samples][deploy-sample].

> [!div class="nextstepaction"]
> [Nasazení ukázky podrobného plánu][deploy-sample]

Pokyny k přizpůsobení, která by se měla provádět v tomto podrobném plánu nebo v výsledné cílové zóně, najdete v tématu věnovaném [hlediskům cílové zóny](../considerations/index.md).

## <a name="next-steps"></a>Další kroky

Po nasazení první cílové zóny budete připraveni [rozšířit cílovou zónu](../considerations/index.md) .

> [!div class="nextstepaction"]
> [Rozšířit cílovou zónu](../considerations/index.md)

<!-- links -->

[deploy-sample]: https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/deploy
