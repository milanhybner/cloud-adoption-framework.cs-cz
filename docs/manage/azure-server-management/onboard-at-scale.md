---
title: Konfigurace služeb správy Azure pro předplatné
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Konfigurace služeb správy Azure pro předplatné
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7144e772da10cd6c7d581fba61c11677524b60c2
ms.sourcegitcommit: 945198179ec215fb264e6270369d561cb146d548
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2019
ms.locfileid: "71967304"
---
# <a name="configure-azure-management-services-at-scale"></a>Konfigurace škálovatelných služeb Azure Management Services

Zprovoznění služeb správy Azure na vaše servery zahrnuje dvě úlohy: nasazení agentů služeb na servery a povolení řešení pro správu. Tento článek se zabývá následujícími procesy, které vám umožní dokončit tyto úlohy:

- [Nasazení požadovaných agentů do virtuálních počítačů Azure pomocí Azure Policy](#deploy-extensions-to-azure-vms-using-azure-policy)
- [Nasazení požadovaných agentů na místní servery](#install-required-agents-on-on-premises-servers)
- [Povolení a konfigurace řešení](#enable-and-configure-solutions)

> [!NOTE]
> Před připojováním virtuálních počítačů ke službě Azure Management Services vytvořte požadovaný [Log Analytics pracovní prostor a Azure Automation účet](./prerequisites.md#create-a-workspace-and-automation-account) .

## <a name="deploy-extensions-to-azure-vms-using-azure-policy"></a>Nasazení rozšíření na virtuální počítače Azure pomocí Azure Policy

Všechna řešení pro správu popsaná v tématu [nástroje a služby pro správu Azure](./tools-services.md) vyžadují, aby byl agent Log Analytics nainstalovaný na virtuálních počítačích Azure a na místních serverech. Virtuální počítače Azure můžete připojit ke škálování pomocí Azure Policy. Přiřaďte zásady, abyste měli jistotu, že je agent nainstalovaný na všech vašich virtuálních počítačích Azure a připojený ke správnému pracovnímu prostoru Log Analytics.

Azure Policy má předdefinovanou [iniciativu zásad](/azure/governance/policy/concepts/definition-structure#initiatives) , která zahrnuje agenta Log Analytics i [agenta Microsoft Dependency agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), který je vyžadován Azure monitor pro virtuální počítače.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Další informace o různých agentech pro monitorování Azure najdete v tématu [Přehled agentů monitorování Azure](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Přiřadit zásady

Chcete-li přiřadit zásady uvedené v předchozí části:

1. V Azure Portal přejdete na **Azure Policy** > **přiřazení** > **přiřadit iniciativu**.

    ![Snímek obrazovky rozhraní zásad portálu](./media/onboarding-at-scale1.png)

2. Na stránce **přiřadit zásadu** vyberte **obor** kliknutím na tlačítko se třemi tečkami (...) a pak vyberte buď skupinu pro správu nebo předplatné. Volitelně můžete vybrat skupinu prostředků. Obor určuje, k jakým prostředkům nebo skupině prostředků je zásada přiřazena. Pak zvolte **Vybrat** v dolní části stránky **Rozsah** .

3. Vyberte tři tečky (...) vedle **definice zásady** a otevřete seznam dostupných definic. Definici iniciativy můžete filtrovat zadáním **Azure monitor** do **vyhledávacího** pole:

    ![Snímek obrazovky rozhraní zásad portálu](./media/onboarding-at-scale2.png)

4. **Název přiřazení** se automaticky vyplní názvem zásady, který jste vybrali, ale můžete ho změnit. Můžete také přidat volitelný popis, který poskytne další informace o tomto přiřazení zásady. Pole **přiřazeno** je automaticky vyplněno na základě toho, kdo je přihlášený. Toto pole je nepovinné a je možné zadat vlastní hodnoty.

5. Pro tuto zásadu vyberte **Log Analytics pracovní prostor** pro přidružení agenta Log Analytics.

    ![Snímek obrazovky rozhraní zásad portálu](./media/onboarding-at-scale3.png)

6. Ověřte **umístění spravované identity**. Pokud je tato zásada typ [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists), bude pro nasazení zásady vyžadovat spravovanou identitu. Na portálu se vytvoří účet, jak je uvedeno u výběru zaškrtávacího políčka.

7. Vyberte **Přiřadit**.

Po dokončení průvodce se přiřazení zásady nasadí do prostředí. Aby se zásady projevily, může trvat až 30 minut. Můžete ho otestovat vytvořením nových virtuálních počítačů po uplynutí 30 minut a potom zkontrolujte, jestli je ve výchozím nastavení ve virtuálním počítači povolená Microsoft Monitoring Agent (MMA).

## <a name="install-required-agents-on-on-premises-servers"></a>Instalovat požadované agenty na místních serverech

> [!NOTE]
> Před zprovozněním serverů do služby Azure Management Services vytvořte požadovaný [Log Analytics pracovní prostor a účet Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

U místních serverů budete muset stáhnout a nainstalovat [agenta Log Analytics a Microsoft Dependency agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) ručně a nakonfigurovat ho tak, aby se připojil ke správnému pracovnímu prostoru. To uděláte tak, že zadáte ID pracovního prostoru a informace o klíči, které najdete v pracovním prostoru Log Analytics v Azure Portal a výběr **nastavení** > **Upřesnit nastavení**.

![Snímek obrazovky s rozšířenými nastaveními Log Analytics pracovního prostoru v Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Povolení a konfigurace řešení

Chcete-li povolit řešení, je nutné nakonfigurovat Log Analytics pracovní prostor. Virtuální počítače Azure a místní servery získají řešení z Log Analytics pracovních prostorů, ke kterým jsou připojené.

V této části jsou uvedené následující řešení:

- [Správa aktualizací](#update-management)
- [Change Tracking a inventář](#change-tracking-and-inventory-solutions)
- [Protokol aktivit Azure](#azure-activity-log)
- [Agent Health Log Analytics Azure](#azure-log-analytics-agent-health)
- [Posouzení antimalwaru](#antimalware-assessment)
- [Azure Monitor pro virtuální počítače](#azure-monitor-for-vms)
- [Azure Security Center](#azure-security-center)

### <a name="update-management"></a>Update Management

Řešení Update Management, Change Tracking a inventáře vyžadují Log Analytics pracovní prostor i účet Automation. Abyste měli jistotu, že tyto prostředky jsou správně nakonfigurované, doporučujeme, abyste provedli účet Automation. Další informace najdete v tématu připojení [řešení Update Management, Change Tracking a inventáře](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Pro všechny servery doporučujeme povolit řešení Update Management. Pro virtuální počítače Azure a místní servery je Update Management zdarma. Pokud povolíte Update Management prostřednictvím svého účtu Automation, v pracovním prostoru se vytvoří [Konfigurace oboru](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) . Musíte ručně aktualizovat obor tak, aby zahrnoval počítače zahrnuté službou aktualizace.

Chcete-li pokrýt všechny existující servery i budoucí servery, je nutné odebrat konfiguraci oboru. Provedete to tak, že v Azure Portal zobrazíte svůj účet Automation a vyberete **Update Management** > **spravovat počítač** > **Povolit na všech dostupných a budoucích počítačích**. Povolením tohoto nastavení umožníte, aby se všechny virtuální počítače Azure připojené k pracovnímu prostoru používaly Update Management.

![Snímek obrazovky Update Management Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Řešení Change Tracking a inventáře

Při připojování řešení Change Tracking a inventáře použijte stejný postup jako u Update Management. Další informace o připojování těchto řešení z vašeho účtu Automation najdete v tématu věnovaném [řešení Update Management, Change Tracking a inventáře](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Řešení Change Tracking je zdarma pro virtuální počítače Azure a náklady $6 na uzel za měsíc pro místní servery. Tyto náklady zahrnují Change Tracking, inventář a konfiguraci požadovaného stavu. Pokud chcete zaregistrovat jenom konkrétní místní servery, můžete na těchto serverech vyjádřit souhlas. Doporučujeme, abyste všechny vaše provozní servery připojili.

#### <a name="opt-in-via-the-azure-portal"></a>Výslovný souhlas prostřednictvím Azure Portal

1. Přejít na účet Automation s povoleným Change Tracking a inventářem
2. Vyberte **sledování změn**.
3. V pravém horním podokně vyberte **spravovat počítače** .
4. Vyberte **Povolit na vybraných počítačích**a vyberte počítače, které chcete povolit, kliknutím na **Přidat** vedle názvu počítače.
5. Chcete-li povolit řešení pro tyto počítače, vyberte možnost **Povolit** .

![Snímek obrazovky Change Tracking Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Přihlášení pomocí uložených hledání

Případně můžete nakonfigurovat konfiguraci oboru tak, aby se na místních serverech mohla vyjádřit. Konfigurace oboru používá uložená hledání.

Chcete-li vytvořit nebo upravit uložené hledání, použijte následující postup:

1. Do pracovního prostoru Log Analytics, který je propojený s vaším účtem Automation, který jste nakonfigurovali v předchozích krocích.

2. V části **Obecné**vyberte možnost **uložená hledání**.

3. Do pole **Filtr** zadejte **Change Tracking** pro filtrování seznamu uložených hledání. Ve výsledcích vyberte **MicrosoftDefaultComputerGroup**.

4. Zadejte název počítače nebo VMUUID k zahrnutí počítačů, pro které chcete Change Tracking použít.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Název serveru se musí přesně shodovat s hodnotou zahrnutou ve výrazu a neměl by obsahovat příponu názvu domény.

5. Vyberte **Uložit**.

6. Ve výchozím nastavení je konfigurace oboru propojena s **MicrosoftDefaultComputerGroup** uloženým hledáním a bude automaticky aktualizována.

### <a name="azure-activity-log"></a>Protokol aktivit Azure

[Protokol aktivit Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) je také součástí Azure monitor. Poskytuje přehled o událostech na úrovni předplatného, ke kterým dochází v Azure.

Přidání tohoto řešení:

1. V Azure Portal otevřete **všechny služby** a vyberte **správa +** řízení  > **řešení**.
2. V zobrazení **řešení** vyberte **Přidat**.
3. Vyhledejte **Activity Log Analytics** a vyberte ji.
4. Vyberte **Vytvořit**.

Bude nutné zadat **název pracovního** prostoru, který jste vytvořili v předchozí části, kde je řešení povoleno.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics Agent Health

Řešení Azure Log Analytics Agent Health nabízí přehled o stavu, výkonu a dostupnosti serverů s Windows a Linux.

Přidání tohoto řešení:

1. V Azure Portal otevřete **všechny služby** a vyberte **správa +** řízení  > **řešení**.
2. V zobrazení **řešení** vyberte **Přidat**.
3. Vyhledejte **Stav agenta Azure Log Analytics** a vyberte ho.
4. Vyberte **Vytvořit**.

Bude nutné zadat **název pracovního** prostoru, který jste vytvořili v předchozí části, kde je řešení povoleno.

Po vytvoření se v instanci prostředku pracovního prostoru zobrazí **AgentHealthAssessment** , když vyberete možnost **Zobrazit** **řešení** > .

### <a name="antimalware-assessment"></a>Posouzení antimalwaru

Řešení Antimalware Assessment vám pomůže identifikovat servery, které jsou nakažené nebo zvyšují riziko infekce malwarem.

Přidání tohoto řešení:

1. V Azure Portal otevřete **všechny služby** a vyberte **správa +** řízení  > **řešení**.
2. V zobrazení **řešení** vyberte **Přidat**.
3. Vyhledejte **antimalware Assessment** a vyberte ji.
4. Vyberte **Vytvořit**.

Bude nutné zadat **název pracovního** prostoru, který jste vytvořili v předchozí části, kde je řešení povoleno.

Po vytvoření se v instanci prostředku pracovního prostoru zobrazí **antimalwarová** aplikace, když vyberete možnost **Zobrazit** **řešení** > .

### <a name="azure-monitor-for-vms"></a>Azure Monitor pro virtuální počítače

[Azure monitor pro virtuální počítače](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) můžete povolit prostřednictvím stránky zobrazení pro instanci virtuálního počítače, jak je popsáno v předchozím článku [Povolení služby správy na jednom virtuálním počítači pro vyhodnocení](./onboard-single-vm.md). Řešení byste neměli povolit přímo na stránce **řešení** , stejně jako u ostatních řešení popsaných v tomto článku. U rozsáhlých nasazení může být snazší pomocí [Automatizace](./onboarding-automation.md) povolit správná řešení v pracovním prostoru.

### <a name="azure-security-center"></a>Azure Security Center

V těchto pokynech doporučujeme, abyste ve výchozím nastavení napřipojili všechny servery do *bezplatné* úrovně Azure Security Center. Tato možnost poskytuje základní úroveň posouzení zabezpečení a užitečná doporučení zabezpečení pro vaše prostředí. Upgrade na úroveň *Standard* Security Center nabízí další výhody, které jsou podrobně popsány na [stránce s cenami Security Center](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Pokud chcete povolit Azure Security Center úroveň Free, použijte následující postup:

1. Přejít na stránku **Security Centerového** portálu.
2. V části **zásady &AMP; dodržování předpisů**vyberte **zásady zabezpečení** .
3. Vyhledejte prostředek pracovního prostoru Log Analytics, který jste vytvořili v pravém podokně.
4. Pro tento pracovní prostor vyberte **Upravit nastavení >** .
5. Vyberte **Cenová úroveň**.
6. Vyberte možnost **Free** .
7. Vyberte **Uložit**.

## <a name="next-steps"></a>Další kroky

Naučte se používat automatizaci k připojování serverů a vytváření výstrah.

> [!div class="nextstepaction"]
> [Automatizace zprovoznění a konfigurace výstrah](./onboarding-automation.md)
