---
title: Návrh a provoz clusterů
description: Seznamte se s Kubernetes v rozhraní pro přijetí cloudu pro návrh a operace clusteru.
author: sabbour
ms.author: asabbour
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 594b8ae3ce7949c3289d9a81ac9870889a5dba98
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527183"
---
<!-- cSpell:ignore asabbour sabbour autoscaler PDBs -->

# <a name="cluster-design-and-operations"></a>Návrh a provoz clusterů

Zjistěte vše nezbytné pro konfiguraci clusterů a návrh sítě. Budoucí škálovatelnost díky automatizaci zřizování infrastruktury. Udržujte vysokou dostupnost díky plánování pro zajištění provozní kontinuity a zotavení po havárii.

## <a name="plan-train-and-proof"></a>Plánování, výuka a kontrola

Po spuštění vám kontrolní seznam a prostředky pomůžou naplánovat návrh clusteru. Měli byste být schopný odpovědět na tyto otázky:

<!-- markdownlint-disable MD033 -->

> [!div class="checklist"]
>
> - Identifikovali jste požadavky na návrh sítě pro váš cluster?
> - Máte úlohy s proměnlivými požadavky? Kolik fondů uzlů budete používat?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Identifikujte požadavky na návrh sítě.** Pochopení požadavků na návrh sítě clusterů, porovnání síťových modelů a výběr modulu plug-in Kubernetes Networking, který vyhovuje vašim potřebám.    | [Kubenet a Azure Container Networking Interface (CNI)](https://docs.microsoft.com/azure/aks/concepts-network#azure-virtual-networks) <br/> [Používání sítě kubenet s vlastními rozsahy IP adres ve službě Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/configure-kubenet) <br/> [Konfigurace sítě Azure CNI ve službě Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/configure-azure-cni) <br/> [Zabezpečení návrhu sítě pro cluster AKS](https://github.com/Azure/sg-aks-workshop/blob/master/cluster-design/NetworkDesign.md)|
> | **Vytvořte více fondů uzlů.** Pokud chcete podporovat aplikace, které mají různé výpočetní prostředky nebo požadavky na úložiště, můžete nakonfigurovat cluster s několika fondy uzlů. Například použijte další fondy uzlů k poskytnutí GPU pro aplikace náročné na výpočetní výkon nebo přístup k vysoce výkonnému úložišti SSD.   | [Vytvoření a Správa fondů více uzlů pro cluster ve službě Azure Kubernetes](https://docs.microsoft.com/azure/aks/use-multiple-node-pools) |
> | **Rozhodněte o požadavcích na dostupnost.** Pokud chcete zajistit vyšší úroveň dostupnosti pro vaše aplikace, clustery je možné distribuovat napříč zónami dostupnosti. Tyto zóny jsou fyzicky oddělená datacentry v dané oblasti. Pokud jsou komponenty clusteru distribuované napříč několika zónami, může cluster tolerovat selhání v jedné z těchto zón. Vaše aplikace a operace správy jsou dál dostupné i v případě, že v celém datacentru dojde k problému.   | [Vytvoření clusteru služby Azure Kubernetes (AKS), který používá zóny dostupnosti](https://docs.microsoft.com/azure/aks/availability-zones) |

## <a name="go-to-production-and-apply-best-practices"></a>Přejít na produkční prostředí a použít osvědčené postupy

Při přípravě aplikace na produkční prostředí byste měli implementovat minimální sadu osvědčených postupů. V této fázi použijte kontrolní seznam níže. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Jste schopní bez obav znovu nasadit infrastrukturu clusteru?
> - Použili jste kvóty prostředků?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automatizujte zřizování clusteru.** Díky infrastruktuře jako kódu můžete automatizovat zřizování infrastruktury a zajistit tak větší odolnost během katastrof a získat flexibilitu pro rychlé nasazení infrastruktury podle potřeby.     | [Vytvoření clusteru Kubernetes pomocí služby Azure Kubernetes Service pomocí Terraformu](https://docs.microsoft.com/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks)|
> | **Plánování dostupnosti pomocí rozpočtů přerušení pod.** Chcete-li zachovat dostupnost aplikací, definujte v podsystému soubory PDB, aby bylo zajištěno, že během selhání hardwaru nebo upgrady clusteru bude v clusteru k dispozici minimální počet lusků. | [Plánování dostupnosti pomocí rozpočtů přerušení pod](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)  |
> | **Vynutili kvóty prostředků v oborech názvů.** Plánování a použití kvót prostředků na úrovni oboru názvů. Kvóty je možné nastavit u výpočetních prostředků, prostředků úložiště a počtu objektů.| [Vynutilit kvóty prostředků](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#enforce-resource-quotas)  |

## <a name="optimize-and-scale"></a>Optimalizace a škálování

Teď, když je aplikace v produkčním prostředí, jak můžete optimalizovat pracovní postup a připravit svoji aplikaci a tým pro škálování? Připravte ho pomocí kontrolního seznamu optimalizace a škálování. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Máte plán pro provozní kontinuitu a zotavení po havárii?
> - Může vaše clusterový rozsah splňovat požadavky aplikace?
> - Můžete monitorovat stav svých clusterů a aplikací a přijímat výstrahy?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automaticky Škálujte cluster tak, aby splňoval požadavky aplikace.** Aby se zajistilo splnění požadavků aplikace, může být potřeba upravit počet uzlů, které spouštějí vaše úlohy automaticky pomocí automatického škálování clusteru. | [Konfigurace automatického škálování clusteru Kubernetes](https://docs.microsoft.com/azure/aks/cluster-autoscaler)    |
> | **Plán pro provozní kontinuitu a zotavení po havárii.** Naplánujte nasazení ve více oblastech, vytvořte plán migrace úložiště a povolte geografickou replikaci pro Image kontejnerů. | [Osvědčené postupy pro nasazení oblastí](https://docs.microsoft.com/azure/aks/operator-best-practices-multi-region)  <br/> [Azure Container Registry geografickou replikaci](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication)  |
> | **Nakonfigurujte monitorování a řešení potíží ve velkém měřítku.** Nastavte výstrahy a monitorování pro aplikace v Kubernetes. Přečtěte si o výchozí konfiguraci, postupu při integraci pokročilejších metrik a o tom, jak přidat vlastní monitorování a upozorňování, abyste mohli spolehlivě provozovat svoji aplikaci. | [Začínáme s monitorováním a upozorňováním na Kubernetes (video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Konfigurace výstrah pomocí Azure Monitor pro kontejnery](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Zkontrolujte protokoly diagnostiky pro hlavní součásti.](https://docs.microsoft.com/azure/aks/view-master-logs) <br/> [Diagnostika služby Azure Kubernetes (AKS)](https://docs.microsoft.com/azure/aks/concepts-diagnostics)    |
