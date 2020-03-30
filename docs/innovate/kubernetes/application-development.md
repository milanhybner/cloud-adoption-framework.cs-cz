---
title: Vývoj a nasazení aplikací
description: Přečtěte si o používání Kubernetes v rozhraní cloudu pro přijetí pro vývoj a architekturu aplikací.
author: sabbour
ms.author: asabbour
ms.topic: guide
ms.date: 03/20/2020
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 6ad36a6dfbce83b23bfcee382ff44daeb9db5f7f
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392765"
---
<!-- cSpell:ignore asabbour sabbour autoscaler Istio Linkerd -->

# <a name="application-development-and-deployment"></a>Vývoj a nasazení aplikací

Prostudujte si vzory a postupy pro vývoj aplikací, nakonfigurujte kanály DevOps a implementujte osvědčené postupy SRE (Site Reliability Engineering).

## <a name="plan-train-and-proof"></a>Plánování, výuka a kontrola

Jak začít, níže uvedený kontrolní seznam a prostředky vám pomůžou naplánovat vývoj a nasazení aplikací. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Připravili jste vývojové prostředí a nastavení pracovního postupu?
> - Jak budete strukturovat složku projektu pro podporu vývoje aplikací Kubernetes?
> - Identifikovali jste požadavky na stav, konfiguraci a úložiště vaší aplikace?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam | Zdroje |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Připravte vývojové prostředí.** Nakonfigurujte své prostředí pomocí nástrojů, které potřebujete k vytvoření kontejnerů, a nastavte pracovní postup vývoje. | [Práce s Docker v Visual Studio Code](https://code.visualstudio.com/docs/azure/docker) <br/>[Práce&nbsp;s&nbsp;Kubernetes&nbsp;v&nbsp;Visual&nbsp;Studio Code](https://code.visualstudio.com/docs/azure/kubernetes) <br/> [Úvod do Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/about) |
> | **Kontejnerizace svoji aplikaci.** Seznamte se s komplexním vývojářským prostředím Kubernetes, včetně aplikačních rozhraní, pracovních postupů vnitřních smyček, architektur pro správu aplikací, CI/CD kanálů, agregace protokolů, monitorování a metriky aplikací. | [Kontejnerizace své aplikace pomocí Docker a Kubernetes (elektronická kniha)](https://azure.microsoft.com/resources/containerize-your-apps-with-docker-and-kubernetes) <br/> [Komplexní vývojové prostředí Kubernetes v Azure (webinář)](https://info.microsoft.com/AU-AzureApp-WBNR-FY20-11Nov-12-ContainerizeYourApplicationswithKubernetesonAzure-SRDEM10557_LP02OnDemandRegistration-ForminBody.html) |
> | **Kontrola běžných scénářů Kubernetes.** Kubernetes se často domníval jako platforma pro poskytování mikroslužeb, ale je to mnohem širší platforma. Podívejte se na toto video, kde se dozvíte o běžných Kubernetes scénářích, jako jsou dávkové analýzy a pracovní postupy.    | [Běžné scénáře&nbsp;&nbsp;&nbsp;použít&nbsp;&nbsp;(video)](https://www.youtube.com/watch?v=zd8vYhrFXp4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=7) |
> | **Připravte aplikaci pro Kubernetes.** Připravte rozložení systému souborů aplikace pro Kubernetes a uspořádejte si týdenní nebo denní vydání. Přečtěte si, jak proces nasazení Kubernetes umožňuje spolehlivé a nulové výpadky. | [Návrh a rozložení projektu pro úspěšné aplikace Kubernetes (webinář)](https://info.microsoft.com/ww-OnDemandRegistration-successful-kubernetes-applications-webinar.html) <br/> [Jak fungují Kubernetes nasazení (video)](https://www.youtube.com/watch?v=mNK14yXIZF4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=3) </br> [Projděte si AKS Workshop](https://aka.ms/learn/aksworkshop) |
> | **Spravujte úložiště aplikace.** Seznamte se s požadavky na výkon a přístupové metody pro lusky, abyste mohli poskytnout vhodné možnosti úložiště. Měli byste naplánovat také způsoby, jak zálohovat a otestovat proces obnovení pro připojené úložiště. | [Základní informace o stavových aplikacích v Kubernetes (video)](https://www.youtube.com/watch?v=GieXzb91I40&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=9) <br/> [Stav a data v aplikacích Docker](https://docs.microsoft.com/dotnet/architecture/microservices/architect-microservice-container-applications/docker-application-state-data) <br/>[Možnosti úložiště ve službě Azure Kubernetes](https://docs.microsoft.com/azure/aks/operator-best-practices-storage) |
> | **Správa tajných klíčů aplikací.** Neukládejte přihlašovací údaje v kódu aplikace. Trezor klíčů by měl sloužit k ukládání a načítání klíčů a přihlašovacích údajů.  | [Jak funguje Správa Kubernetes a konfigurace (video)](https://www.youtube.com/watch?v=vRcQOZLnKUk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=11) <br/> [Pochopení správy tajných kódů v Kubernetes (video)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) <br/>[Použití Azure Key Vault s Kubernetes](https://github.com/Azure/kubernetes-keyvault-flexvol) <br/>[Ověření a přístup k prostředkům Azure pomocí identity pod](https://github.com/Azure/aad-pod-identity) |

## <a name="deploy-to-production-and-apply-best-practices"></a>Nasazení do produkčního prostředí a použití osvědčených postupů

Při přípravě aplikace na produkční prostředí byste měli implementovat minimální sadu osvědčených postupů. V této fázi použijte kontrolní seznam níže. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Můžete monitorovat všechny aspekty aplikace?
> - Definovali jste požadavky na prostředky pro vaši aplikaci? Jak se mění požadavky na škálování?
> - Máte možnost nasadit nové verze aplikace, aniž by to ovlivnilo produkční systémy?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Nakonfigurujte připravenost a kontroly stavu živých.** Kubernetes používá kontroly připravenosti a živého využívání k tomu, abyste věděli, kdy je vaše aplikace připravená přijmout provoz a kdy je potřeba ji restartovat. Bez definování takových kontrol nebude Kubernetes moct zjistit, jestli je vaše aplikace spuštěná.   | [Živý a kontrol připravenosti](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes) |
> | **Konfigurace protokolování, monitorování aplikací a upozorňování.** Monitorování kontejnerů je důležité, zejména v případě, že spouštíte produkční cluster ve velkém měřítku, s několika aplikacemi.  Doporučená metoda protokolování pro kontejnery aplikací je zapsána do datových proudů standardního výstupu (stdout) a Standard Error (stderr).   | [Přihlášení Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging) <br/> [Začínáme s monitorováním a upozorňováním na Kubernetes (video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Azure Monitor pro kontejnery](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Povolení a kontrola protokolů hlavních uzlů Kubernetes ve službě Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/view-master-logs)  <br/> [Zobrazit protokoly Kubernetes, události a metriky pod v reálném čase](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-livedata-overview) |
> | **Definujte požadavky na prostředky pro aplikaci.** Primárním způsobem správy výpočetních prostředků v rámci clusteru Kubernetes se používají požadavky a omezení pod. Tyto požadavky a omezení říká plánovači Kubernetes, k čemu by se měly přiřadit výpočetní prostředky.     | [Definování&nbsp;pod&nbsp;prostředků&nbsp;požadavky&nbsp;a&nbsp;omezení](https://docs.microsoft.com/azure/aks/developer-best-practices-resource-management) |
> | **Nakonfigurujte požadavky na škálování aplikace.** Kubernetes podporuje automatické škálování vodorovně pod, aby bylo možné upravit počet lusků v nasazení v závislosti na využití procesoru nebo jiných metrikách SELECT. Aby bylo možné používat automatické škálování, musí mít všechny kontejnery v luskech požadavky na procesor a omezení.    | [Konfigurovat horizontální automatické škálování pod](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale#autoscale-pods) |
> | **Nasaďte aplikace s využitím automatizovaného kanálu a DevOps.**  Úplná automatizace všech kroků mezi potvrzením kódu do produkčního nasazení umožňuje týmům soustředit se na tvorbu kódu a v ručních krocích rutinní odebrat režijní a potenciální lidskou chybu. Nasazení nového kódu je rychlejší a méně riskantní, což týmům pomáhá pružnější, větší produktivitu a spolehlivější informace o jejich běžícím kódu.    | [Vývoj postupů DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices) <br/> [Nastavení kanálu sestavení Kubernetes (video)](https://www.youtube.com/watch?v=5irsAdKoEBU&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=6) <br/> [Centrum nasazení pro službu Azure Kubernetes](https://docs.microsoft.com/azure/aks/deployment-center-launcher) <br/> [Akce GitHubu pro nasazení do služby Azure Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-action) <br/>  [CI/CD do služby Azure Kubernetes pomocí Jenkinse](https://docs.microsoft.com/azure/aks/jenkins-continuous-deployment) |

## <a name="optimize-and-scale"></a>Optimalizace a škálování

Teď, když je aplikace v produkčním prostředí, jak můžete optimalizovat pracovní postup a připravit svoji aplikaci a tým pro škálování? Připravte ho pomocí kontrolního seznamu optimalizace a škálování. Měli byste být schopni odpovědět na tyto otázky:

> [!div class="checklist"]
>
> - Jsou problémy s aplikací, které jsou pro křížové aplikace z vaší aplikace abstraktní?
> - Je možné udržet si spolehlivost systému a aplikací a zároveň stále provádět iteraci na nových funkcích a verzích?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Kontrolní seznam  | Zdroje                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Nasaďte bránu API.** Brána API slouží jako přední dveře ke mikroslužbám, rozděluje klienty od vašich mikroslužeb, přidává další vrstvu zabezpečení a snižuje složitost vašich mikroslužeb tím, že odstraňuje zatížení pro zpracování průřezů.     | [Použití Azure API Management s mikroslužbami nasazenými ve službě Azure Kubernetes](https://docs.microsoft.com/azure/api-management/api-management-kubernetes) |
> | **Nasaďte síť.** Síť nabízí možnosti, jako je Správa provozu, odolnost, zásady, zabezpečení, silná identita a pozorování vašich úloh. Vaše aplikace je oddělená od těchto provozních schopností a síť je přesune z aplikační vrstvy do vrstvy infrastruktury.     | [Jak služba&nbsp;&nbsp;sítě&nbsp;pracovní&nbsp;ve&nbsp;Kubernetes&nbsp;(video)](https://www.youtube.com/watch?v=izVWk7rYqWI&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=15&t=0s) <br/> [Seznamte se s sítí pro služby](https://docs.microsoft.com/azure/aks/servicemesh-about) <br/> [Použití Istio se službou Azure Kubernetes](https://docs.microsoft.com/azure/aks/servicemesh-istio-about) <br/> [Použití linkeru se službou Azure Kubernetes](https://docs.microsoft.com/azure/aks/servicemesh-linkerd-about) <br/> [Použití Consul se službou Azure Kubernetes](https://docs.microsoft.com/azure/aks/servicemesh-consul-about) |
> | **Implementujte postupy pro řízení spolehlivosti sítě (SRE).**  Správa spolehlivosti sítě (SRE) je osvědčeným přístupem k zajištění spolehlivosti zásadního systému a aplikace při iteraci na základě rychlosti na webu Marketplace.   | [Úvod do strojírenství (SRE) pro spolehlivost webu](https://docs.microsoft.com/learn/modules/intro-to-site-reliability-engineering) <br/> [DevOps v Microsoftu: SRE pro streamování her](https://azure.microsoft.com/resources/devops-at-microsoft-game-streaming-sre) |
