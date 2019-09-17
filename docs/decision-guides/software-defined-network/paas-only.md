---
title: 'Softwarově definované sítě: Jenom PaaS'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diskuzi o modelu PaaS, který je určený jenom pro softwarově definované sítě v cloudu.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 704dbb16be57c4203199ca972aa61b520eece3ca
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023549"
---
# <a name="software-defined-networking-paas-only"></a>Softwarově definované sítě: Jenom PaaS

Při implementaci prostředku Platform as a Service (PaaS) proces nasazení automaticky vytvoří předpokládanou základní síť s omezeným počtem ovládacích prvků v této síti, včetně vyrovnávání zatížení, blokování portů a připojení k ostatním PaaS. orgány.

V Azure můžete [nasadit](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services) několik typů prostředků PaaS nebo je [připojit k](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) virtuální síti, což umožňuje integraci těchto prostředků se stávající infrastrukturou virtuální sítě. Další služby, například [App Service prostředí](https://docs.microsoft.com/azure/app-service/environment/intro), [služby Azure Kubernetes](https://docs.microsoft.com/azure/aks/intro-kubernetes)a [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) musí být nasazeny v rámci virtuální sítě. Ale v mnoha případech je PaaS jenom síť architektury, která se spoléhá jenom na výchozí možnosti nativního síťového připojení, které poskytují prostředky PaaS, stačí, aby splnily požadavky na konektivitu a správu provozu úlohy.

Pokud zvažujete jenom PaaS síťovou architekturu, ujistěte se, že jste ověřili, že požadované předpoklady odpovídají vašim požadavkům.

## <a name="paas-only-assumptions"></a>Jenom PaaS předpoklady

Nasazení architektury síťové architektury jen pro PaaS předpokládá následující:

- Nasazená aplikace je samostatná aplikace nebo závisí jenom na dalších PaaSch prostředcích, které nevyžadují virtuální síť.
- Vaše provozní týmy IT můžou aktualizovat své nástroje, školení a procesy pro podporu správy, konfigurace a nasazení samostatných aplikací PaaS.
- Aplikace PaaS není součástí širšího úsilí cloudové migrace, které bude zahrnovat prostředky IaaS.

Tyto předpoklady představují minimální kvalifikátory zarovnané na nasazení sítě jen pro PaaS. I když tento přístup může být v souladu s požadavky jediného nasazení aplikace, každý tým pro přijetí cloudu by měl brát v úvahu tyto dlouhodobé otázky:

- Bude toto nasazení rozšířit v oboru nebo škálovat, aby se vyžadoval přístup k jiným nePaaSm prostředkům?
- Naplánovala se další nasazení PaaS nad rámec aktuálního řešení?
- Má organizace plány pro další budoucí migrace do cloudu?

Odpovědi na tyto otázky nebrání týmu v tom, aby si zvolili možnost PaaS, ale před konečným rozhodnutím byste měli zvážit.
