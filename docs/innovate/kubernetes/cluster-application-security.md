---
title: Zabezpečení aplikací a clusterů
description: Přečtěte si o Kubernetes v rozhraní cloudu pro přijetí pro zabezpečení clusteru a aplikací.
author: sabbour
ms.author: asabbour
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c7d27fb64e03358876eb8384c09e3add5f5c433e
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527244"
---
<!-- cSpell:ignore asabbour sabbour kured -->

# <a name="cluster-and-application-security"></a>Zabezpečení aplikací a clusterů

Seznamte se s Kubernetes Security Essentials a Projděte si pokyny k zabezpečení nastavení clusterů a zabezpečení aplikací.

## <a name="plan-train-and-proof"></a>Plánování, výuka a kontrola

Po spuštění vám kontrolní seznam a zdroje informací pomůžou při plánování operací a zabezpečení clusteru. Měli byste být schopný odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Zkontrolovali jste model zabezpečení a hrozby Kubernetes clusterů?
> - Je váš cluster povolený pro řízení přístupu na základě rolí?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Seznamte se s dokumentací White paper k zabezpečení Essentials.** Primárními cíli zabezpečeného prostředí Kubernetes je zajistit, že aplikace, které spouštíte, jsou chráněné, že problémy se zabezpečením se dají identifikovat a rychle vyřešit a že se jim budou zabývat budoucí podobné problémy. | [Konečný průvodce zabezpečením Kubernetes (dokument White Paper)](https://clouddamcdnprodep.azureedge.net/gdc/gdc8LXmoZ/original)     |
> | **Projděte si nastavení posílení zabezpečení pro uzly clusteru.** Hostitelský operační systém s posíleným zabezpečením omezuje oblast útoku a umožňuje bezpečné nasazení kontejnerů. | [Posílení zabezpečení v hostitelích virtuálních počítačů s AKS](https://docs.microsoft.com/azure/aks/security-hardened-vm-host-image)     |
> | **Nastavení řízení přístupu na základě role clusteru (RBAC).** Tento řídicí mechanismus umožňuje přiřadit uživatele nebo skupiny uživatelů, oprávnění k provádění akcí, jako je vytváření nebo úpravy prostředků, nebo zobrazení protokolů ze spuštěných úloh aplikací. | [Principy řízení přístupu na základě role (RBAC) v Kubernetes (video)](https://www.youtube.com/watch?v=G3R24JSlGjY&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=12) <br/> [Integrace Azure AD se službou Azure Kubernetes](https://docs.microsoft.com/azure/aks/azure-ad-integration) <br/> [Omezte přístup ke konfiguračnímu souboru clusteru.](https://docs.microsoft.com/azure/aks/control-kubeconfig-access)   |

## <a name="deploy-to-production-and-apply-best-practices"></a>Nasazení do produkčního prostředí a použití osvědčených postupů

Při přípravě aplikace na produkční prostředí byste měli implementovat minimální sadu osvědčených postupů. V této fázi použijte kontrolní seznam níže. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Nakonfigurovali jste pravidla zabezpečení sítě pro příchozí a odchozí komunikaci a komunikaci uvnitř pod ní?
> - Je váš cluster nakonfigurovaný tak, aby automaticky nepoužívá aktualizace zabezpečení uzlů?
> - Používáte řešení pro kontrolu zabezpečení pro clustery a úlohy kontejnerů?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Řízení přístupu ke clusterům pomocí členství ve skupině.** Nakonfigurujte Kubernetes řízení přístupu na základě role (RBAC), abyste omezili přístup k prostředkům clusteru na základě identity uživatele nebo členství ve skupině. | [Řízení přístupu ke clusterům pomocí RBAC a skupin Azure AD](https://docs.microsoft.com/azure/aks/azure-ad-rbac)    |
> | **Vytvořte zásady správy tajných kódů.** Bezpečně nasaďte a spravujte citlivé informace, jako jsou hesla a certifikáty, pomocí správy tajných klíčů v Kubernetes. | [Pochopení správy tajných kódů v Kubernetes (video)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) |
> | **Zabezpečte síťový provoz uvnitř pod sebou pomocí zásad sítě.** Použijte princip nejnižších oprávnění k řízení toku provozu sítě mezi lusky v clusteru. | [Zabezpečení provozu uvnitř pod sebou pomocí zásad sítě](https://docs.microsoft.com/azure/aks/use-network-policies) |
> | **Omezte přístup k serveru rozhraní API pomocí autorizovaných IP adres.** Vylepšete zabezpečení clusteru a minimalizujte plochu útoku tím, že omezíte přístup k serveru rozhraní API na omezené sady rozsahů IP adres. | [Zabezpečený přístup k serveru rozhraní API](https://docs.microsoft.com/azure/aks/api-server-authorized-ip-ranges) |
> | **Omezte provoz odchozího provozu clusteru.** Zjistěte, jaké porty a adresy se mají povolit, pokud omezíte odchozí přenosy clusteru. K zabezpečení odchozího provozu a definování potřebných portů a adres můžete použít Azure Firewall nebo zařízení brány firewall jiného výrobce. | [Řízení přenosů dat pro uzly clusteru v AKS](https://docs.microsoft.com/azure/aks/limit-egress-traffic) |
> | **Zabezpečte provoz pomocí firewallu webových aplikací (WAF).** Pro clustery Kubernetes použijte Azure Application Gateway jako kontroler příchozího přenosu dat.  | [Konfigurace Azure Application Gateway jako řadiče pro příchozí přenosy dat](https://docs.microsoft.com/azure/application-gateway/ingress-controller-overview)    |
> | **Použijte aktualizace zabezpečení a jádra u pracovních uzlů.** Pochopení možnosti aktualizace uzlů AKS V zájmu ochrany clusterů se aktualizace zabezpečení automaticky aplikují na uzly Linux v AKS. Tyto aktualizace zahrnují opravy zabezpečení operačního systému nebo aktualizace jádra. Některé z těchto aktualizací vyžadují k dokončení procesu restart uzlu. | [Použití kured k automatickému restartování uzlů pro použití aktualizací](https://docs.microsoft.com/azure/aks/node-updates-kured) |
> | **Konfigurace řešení pro prohledávání kontejnerů a clusterů.** Prověřování kontejnerů, které se přehrály do Azure Container Registry a získají hlubší přehled o uzlech clusteru, cloudovém provozu a ovládacích prvcích zabezpečení. | [Azure Container Registry integrace s Security Center](https://docs.microsoft.com/azure/security-center/azure-container-registry-integration) <br/> [Integrace služby Azure Kubernetes s Security Center](https://docs.microsoft.com/azure/security-center/azure-kubernetes-service-integration)  |

## <a name="optimize-and-scale"></a>Optimalizace a škálování

Teď, když je aplikace v produkčním prostředí, jak můžete optimalizovat pracovní postup a připravit svoji aplikaci a tým pro škálování? Připravte ho pomocí kontrolního seznamu optimalizace a škálování. Měli byste být schopni odpovědět:

> [!div class="checklist"]
>
> - Můžete vynutili škálování zásad správného řízení a clusterů?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Vynutilit zásady zásad správného řízení clusteru.** Využijte vynucené vynucování a zabezpečení vašich clusterů v centralizovaném, konzistentním způsobem. | [Řízení nasazení pomocí Azure Policy](https://docs.microsoft.com/azure/governance/policy/concepts/rego-for-aks)    |
> | **Pravidelně otáčejte certifikáty clusteru.** Kubernetes používá certifikáty pro ověřování s mnoha jeho součástmi. Tyto certifikáty možná budete chtít pravidelně střídat z důvodů zabezpečení nebo zásad. | [Otočení certifikátů ve službě Azure Kubernetes (AKS)](https://docs.microsoft.com/azure/aks/certificate-rotation)    |
