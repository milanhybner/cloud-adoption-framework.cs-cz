---
title: Konfigurace služby Azure Server Management Services pro předplatné
description: Konfigurace služby Azure Server Management Services pro předplatné
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c3c44f3c53049f29be989616e1d5af041907e497
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808086"
---
# <a name="configure-azure-server-management-services-at-scale"></a>Konfigurace škálování služby Azure Server Management Services

Aby bylo možné na vaše servery připojit služby pro správu Azure serveru, musíte provést tyto dvě úlohy:
- Nasazení agentů služeb na vaše servery
- Povolit řešení pro správu

Tento článek se věnuje třem procesům, které jsou nutné k dokončení těchto úloh:

1. Nasazení požadovaných agentů do virtuálních počítačů Azure pomocí Azure Policy
1. Nasazení požadovaných agentů na místní servery
1. Povolení a konfigurace řešení

> [!NOTE]
> Před připojením virtuálních počítačů ke službám Azure Server Management vytvořte požadované [Log Analytics pracovní prostor a Azure Automation účet](./prerequisites.md#create-a-workspace-and-automation-account) .

## <a name="use-azure-policy-to-deploy-extensions-to-azure-vms"></a>Použití Azure Policy k nasazení rozšíření do virtuálních počítačů Azure

Všechna řešení pro správu, která jsou popsaná v tématu [služby a nástroje pro správu Azure](./tools-services.md) , vyžadují, aby byl agent Log Analytics nainstalovaný na virtuálních počítačích Azure a místních serverech. Virtuální počítače Azure můžete připojit ke škálování pomocí Azure Policy. Přiřaďte zásady, abyste měli jistotu, že je agent nainstalovaný na vašich virtuálních počítačích Azure a připojený ke správnému pracovnímu prostoru Log Analytics.

Azure Policy má předdefinovanou [iniciativu zásad](https://docs.microsoft.com/azure/governance/policy/concepts/definition-structure#initiatives) , která zahrnuje agenta Log Analytics a [agenta Microsoft Dependency agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), který je vyžadován Azure monitor pro virtuální počítače.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Další informace o různých agentech pro monitorování Azure najdete v tématu [Přehled agentů monitorování Azure](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Přiřazování zásad

Postup přiřazení zásad, které jsou popsané v předchozí části:

1. V Azure Portal na **Azure Policy** > **přiřazení** > **přiřadit iniciativu**.

    ![Snímek obrazovky rozhraní zásad portálu](./media/onboarding-at-scale1.png)

2. Na stránce **přiřadit zásadu** nastavte **obor** tak, že vyberete tři tečky (...) a pak vyberete buď skupinu pro správu nebo předplatné. Volitelně můžete vybrat skupinu prostředků. Pak zvolte **Vybrat** v dolní části stránky **Rozsah** . Obor určuje, k jakým prostředkům nebo skupině prostředků je zásada přiřazena.

3. Vyberte tři tečky ( **...** ) vedle **definice zásady** a otevřete seznam dostupných definic. Chcete-li filtrovat definice iniciativ, zadejte **Azure monitor** do **vyhledávacího** pole:

    ![Snímek obrazovky rozhraní zásad portálu](./media/onboarding-at-scale2.png)

4. **Název přiřazení** se automaticky vyplní názvem zásady, který jste vybrali, ale můžete ho změnit. Můžete také přidat volitelný popis, který poskytne další informace o tomto přiřazení zásady. Pole **přiřazeno** je automaticky vyplněno na základě toho, kdo je přihlášený. Toto pole je volitelné a podporuje vlastní hodnoty.

5. Pro tuto zásadu vyberte **Log Analytics pracovní prostor** pro přidružení agenta Log Analytics.

    ![Snímek obrazovky rozhraní zásad portálu](./media/onboarding-at-scale3.png)

6. Zaškrtněte políčko **spravované umístění identity** . Pokud se jedná o typ [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists), bude se pro nasazení zásady vyžadovat spravovaná identita. Na portálu se vytvoří účet, který je označen výběrem zaškrtávacího políčka.

7. Vyberte **Přiřadit**.

Po dokončení průvodce se přiřazení zásady nasadí do prostředí. Aby se zásady projevily, může trvat až 30 minut. Pokud ho chcete otestovat, vytvořte nové virtuální počítače po 30 minutách a zkontrolujte, jestli je ve výchozím nastavení povolená Microsoft Monitoring Agent na virtuálním počítači.

## <a name="install-agents-on-on-premises-servers"></a>Instalace agentů na místních serverech

> [!NOTE]
> Před zprovozněním služeb pro správu Azure serveru na servery vytvořte požadovaný [pracovní prostor Log Analytics a účet Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

U místních serverů je potřeba stáhnout a nainstalovat [agenta Log Analytics a Microsoft Dependency agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) ručně a nakonfigurovat ho tak, aby se připojil ke správnému pracovnímu prostoru. Je nutné zadat ID a informace klíče pracovního prostoru. Tyto informace získáte tak, že v Azure Portal přejdete do svého pracovního prostoru Log Analytics a vyberete **nastavení** > **Upřesnit nastavení**.

![Snímek obrazovky s rozšířenými nastaveními Log Analytics pracovního prostoru v Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Povolení a konfigurace řešení

Pokud chcete povolit řešení, musíte nakonfigurovat pracovní prostor Log Analytics. Virtuální počítače Azure a místní servery získají řešení z Log Analytics pracovních prostorů, ke kterým jsou připojené.

### <a name="update-management"></a>Správa aktualizací

Řešení Update Management, Change Tracking a inventáře vyžadují Log Analytics pracovní prostor i účet Automation. Abyste měli jistotu, že tyto prostředky jsou správně nakonfigurované, doporučujeme vám, abyste provedli účet Automation. Další informace najdete v tématu připojení [řešení Update Management, Change Tracking a inventáře](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Pro všechny servery doporučujeme povolit řešení Update Management. Pro virtuální počítače Azure a místní servery je Update Management zdarma. Pokud povolíte Update Management prostřednictvím svého účtu Automation, v pracovním prostoru se vytvoří [Konfigurace oboru](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) . Ručně aktualizujte obor tak, aby zahrnoval počítače, které jsou pokryté službou Update Management.

Chcete-li pokrýt stávající servery i budoucí servery, je nutné odebrat konfiguraci oboru. Provedete to tak, že v Azure Portal zobrazíte svůj účet Automation. Vyberte **Update Management** > **spravovat počítač** > **Povolit na všech dostupných a budoucích počítačích**. Toto nastavení umožňuje, aby se všechny virtuální počítače Azure připojené k pracovnímu prostoru používaly Update Management.

![Snímek obrazovky Update Management Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Řešení Change Tracking a inventáře

Při připojování řešení Change Tracking a inventáře použijte stejný postup jako u Update Management. Další informace o tom, jak tato řešení připojit z účtu Automation, najdete v článku připojení [řešení Update Management, Change Tracking a inventáře](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Řešení Change Tracking je zdarma pro virtuální počítače Azure a náklady $6 na uzel za měsíc pro místní servery. Tyto náklady zahrnují Change Tracking, inventář a konfiguraci požadovaného stavu. Pokud chcete zaregistrovat jenom konkrétní místní servery, můžete na těchto serverech vyjádřit souhlas. Doporučujeme, abyste všechny vaše provozní servery připojili.

#### <a name="opt-in-via-the-azure-portal"></a>Výslovný souhlas prostřednictvím Azure Portal

1. Přejít na účet Automation s povoleným Change Tracking a inventářem
2. Vyberte **sledování změn**.
3. V pravém horním podokně vyberte **spravovat počítače** .
4. Vyberte **Povolit na vybraných počítačích**. Pak vyberte **Přidat** vedle názvu počítače.
5. Chcete-li povolit řešení pro tyto počítače, vyberte možnost **Povolit** .

![Snímek obrazovky Change Tracking Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Přihlášení pomocí uložených hledání

Případně můžete nakonfigurovat konfiguraci oboru tak, aby se na místních serverech mohla vyjádřit. Konfigurace oboru používá uložená hledání.

Chcete-li vytvořit nebo upravit uložené hledání, postupujte podle následujících kroků:

1. Přejít do pracovního prostoru Log Analytics, který je propojený s účtem Automation, který jste nakonfigurovali v předchozích krocích.

1. V části **Obecné**vyberte možnost **uložená hledání**.

1. Do pole **Filtr** zadejte **Change Tracking** pro filtrování seznamu uložených hledání. Ve výsledcích vyberte **MicrosoftDefaultComputerGroup**.

1. Zadejte název počítače nebo VMUUID k zahrnutí počítačů, pro které chcete Change Tracking použít.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Název serveru musí přesně odpovídat hodnotě ve výrazu a nesmí obsahovat příponu názvu domény.

1. Vyberte **Uložit**. Ve výchozím nastavení je konfigurace oboru propojená s **MicrosoftDefaultComputerGroup** uloženým hledáním. Automaticky se aktualizuje.

### <a name="azure-activity-log"></a>Protokol aktivit Azure

[Protokol aktivit Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) je také součástí Azure monitor. Poskytuje přehled o událostech na úrovni předplatného, ke kterým dochází v Azure.

Postup při implementaci tohoto řešení:

1. V Azure Portal otevřete **všechny služby** a vyberte **Správa + zásady správného** řízení > **řešení**.
2. V zobrazení **řešení** vyberte **Přidat**.
3. Vyhledejte **Activity Log Analytics** a vyberte ji.
4. Vyberte **Create** (Vytvořit).

Je nutné zadat **název** pracovního prostoru, který jste vytvořili v předchozí části, kde je řešení povoleno.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics Agent Health

Řešení Azure Log Analytics Agent Health hlásí stav, výkon a dostupnost serverů s Windows a Linux.

Postup při implementaci tohoto řešení:

1. V Azure Portal otevřete **všechny služby** a vyberte **Správa + zásady správného** řízení > **řešení**.
2. V zobrazení **řešení** vyberte **Přidat**.
3. Vyhledejte **Stav agenta Azure Log Analytics** a vyberte ho.
4. Vyberte **Create** (Vytvořit).

Je nutné zadat **název** pracovního prostoru, který jste vytvořili v předchozí části, kde je řešení povoleno.

Po vytvoření se instance prostředku pracovního prostoru zobrazí **AgentHealthAssessment** , když vyberete **Zobrazit** > **řešení**.

### <a name="antimalware-assessment"></a>Posouzení antimalwaru

Řešení Antimalware Assessment vám pomůže identifikovat servery, které jsou nakažené nebo zvyšují riziko infekce malwarem.

Postup při implementaci tohoto řešení:

1. V Azure Portal otevřete **všechny služby** a vyberte **Správa + zásady správného** řízení > **řešení**.
2. V zobrazení **řešení** vyberte **Přidat**.
3. Vyhledejte a vyberte **antimalware Assessment**.
4. Vyberte **Create** (Vytvořit).

Je nutné zadat **název** pracovního prostoru, který jste vytvořili v předchozí části, kde je řešení povoleno.

Po vytvoření se v instanci prostředku pracovního prostoru po výběru **zobrazit** > **řešení**zobrazí **Antimalwarový** program.

### <a name="azure-monitor-for-vms"></a>Azure Monitor pro virtuální počítače

[Azure monitor pro virtuální počítače](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) můžete povolit prostřednictvím stránky zobrazení pro instanci virtuálního počítače, jak je popsáno v tématu [Povolení služeb správy na jednom virtuálním počítači pro vyhodnocení](./onboard-single-vm.md). Řešení byste neměli povolit přímo na stránce **řešení** , stejně jako u ostatních řešení, která jsou popsaná v tomto článku. U rozsáhlých nasazení může být snazší pomocí [Automatizace](./onboarding-automation.md) povolit správná řešení v pracovním prostoru. 

### <a name="azure-security-center"></a>Centrum zabezpečení Azure

Doporučujeme, abyste všechny servery připojili alespoň k Azure Security Center úrovně *Free* . Tato možnost poskytuje základní úroveň posouzení zabezpečení a užitečná doporučení zabezpečení pro vaše prostředí. Pokud upgradujete na úroveň *Standard* , získáte další výhody, které jsou podrobně popsány na [stránce s cenami Security Center](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Pokud chcete povolit Azure Security Center úroveň Free, postupujte takto:

1. Přejít na stránku **Security Centerového** portálu.
2. V části **zásady & dodržování předpisů**vyberte **zásady zabezpečení**.
3. Vyhledejte prostředek pracovního prostoru Log Analytics, který jste vytvořili v podokně na pravé straně.
4. Vyberte **Upravit nastavení** pro tento pracovní prostor.
5. Vyberte **Cenová úroveň**.
6. Vyberte možnost **Free** .
7. Vyberte **Uložit**.

## <a name="next-steps"></a>Další kroky

Naučte se používat automatizaci k připojování serverů a vytváření výstrah.

> [!div class="nextstepaction"]
> [Automatizace zprovoznění a konfigurace výstrah](./onboarding-automation.md)
