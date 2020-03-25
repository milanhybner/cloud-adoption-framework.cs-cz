---
title: Návrh a operace clusteru
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seznamte se s Kubernetes v rozhraní pro přijetí cloudu pro návrh a operace clusteru.
author: sabbour
ms.author: asabbour
ms.topic: guide
ms.date: 12/16/2019
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5b5aafd1c9470b566395201a46c75d96581306bd
ms.sourcegitcommit: 25cd1b3f218d0644f911737a6d5fd259461b2458
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80226565"
---
# <a name="cluster-design-and-operations"></a>Návrh a operace clusteru

Identifikujte konfiguraci clusteru a návrh sítě. Budoucí škálovatelnost díky automatizaci zřizování infrastruktury. Udržujte vysokou dostupnost díky plánování kontinuity podnikových aplikací a zotavení po havárii.

## <a name="plan-train-and-proof"></a>Plánování, výuka a kontrola

Po spuštění vám kontrolní seznam a prostředky pomůžou naplánovat návrh clusteru. Měli byste být schopný odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Identifikovali jste požadavky na návrh sítě pro váš cluster?
> - Máte úlohy s proměnlivými požadavky? Kolik fondů uzlů budete používat?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Prostředky |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Identifikujte požadavky na návrh sítě.** Pochopení požadavků na návrh sítě clusterů, porovnání síťových modelů a výběr modulu plug-in Kubernetes Networking, který vyhovuje vašim potřebám.    | [Kubenet a Azure Container Networking Interface (CNI)](https://docs.microsoft.com/azure/aks/concepts-network#azure-virtual-networks) <br/> [Používání sítě kubenet s vlastními rozsahy IP adres ve službě Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/configure-kubenet) <br/> [Konfigurace sítě Azure CNI ve službě Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/configure-azure-cni) <br/> [Zabezpečení návrhu sítě pro cluster AKS]] (https://github.com/Azure/sg-aks-workshop/blob/master/cluster-design/NetworkDesign.md)|
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
> | Kontrolní seznam  | Prostředky                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automatizujte zřizování clusteru.** Díky infrastruktuře jako kódu můžete automatizovat zřizování infrastruktury a zajistit tak větší odolnost během katastrof a získat flexibilitu pro rychlé nasazení infrastruktury podle potřeby.     | [Vytvoření clusteru Kubernetes pomocí služby Azure Kubernetes Service pomocí Terraformu](https://docs.microsoft.com/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks)|
> | **Plánování dostupnosti pomocí rozpočtů přerušení pod.** Chcete-li zachovat dostupnost aplikací, definujte v podsystému soubory PDB, aby bylo zajištěno, že během selhání hardwaru nebo upgrady clusteru bude v clusteru k dispozici minimální počet lusků. | [Plánování dostupnosti pomocí rozpočtů přerušení pod](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)  |
> | **Vynutili kvóty prostředků v oborech názvů.** Plánování a použití kvót prostředků na úrovni oboru názvů. Kvóty je možné nastavit u výpočetních prostředků, prostředků úložiště a počtu objektů.| [Vynutilit kvóty prostředků](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#enforce-resource-quotas)  |

## <a name="optimize-and-scale"></a>Optimalizace a škálování

Teď, když je aplikace v produkčním prostředí, jak můžete optimalizovat pracovní postup a připravit svoji aplikaci a tým pro škálování? Využijte kontrolní seznam optimalizace a škálování pro přípravu. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Máte plán pro provozní kontinuitu a zotavení po havárii?
> - Může vaše clusterový rozsah splňovat požadavky aplikace?
> - Můžete monitorovat stav svých clusterů a aplikací a přijímat výstrahy?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Prostředky |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automaticky Škálujte cluster tak, aby splňoval požadavky aplikace.** Aby se zajistilo splnění požadavků aplikace, může být potřeba upravit počet uzlů, které spouštějí vaše úlohy automaticky pomocí automatického škálování clusteru. | [Konfigurace automatického škálování clusteru Kubernetes](https://docs.microsoft.com/azure/aks/cluster-autoscaler)    |
> | **Plán pro provozní kontinuitu a zotavení po havárii.** Naplánujte nasazení ve více oblastech, vytvořte plán migrace úložiště a povolte geografickou replikaci pro Image kontejnerů. | [Osvědčené postupy pro nasazení ve více oblastech](https://docs.microsoft.com/azure/aks/operator-best-practices-multi-region)  <br/> [Azure Container Registry geografickou replikaci](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication)  |
> | **Nakonfigurujte monitorování a řešení potíží ve velkém měřítku.** Nastavte výstrahy a monitorování pro aplikace v Kubernetes. Přečtěte si o výchozí konfiguraci, postupu při integraci pokročilejších metrik a o tom, jak přidat vlastní monitorování a upozorňování, abyste mohli spolehlivě provozovat svoji aplikaci. | [Začínáme s monitorováním a upozorňováním na Kubernetes (video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Konfigurace výstrah pomocí Azure Monitor pro kontejnery](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Zkontrolujte protokoly diagnostiky pro hlavní součásti.](https://docs.microsoft.com/azure/aks/view-master-logs) <br/> [Diagnostika služby Azure Kubernetes (AKS)](https://docs.microsoft.com/azure/aks/concepts-diagnostics)    |
