---
title: Povolit sledování a upozorňování na kritické změny
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Povolit sledování a upozorňování na kritické změny
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 93449f754e3908e092fa64c55ad62fc604b4ba5b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029416"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Povolit sledování a upozorňování na kritické změny

Azure Change Tracking a inventář poskytuje výstrahy týkající se stavu konfigurace hybridního prostředí a změn v tomto prostředí. Můžete monitorovat důležité změny souboru, služby, softwaru a registru, které mohou mít vliv na nasazené servery.

Ve výchozím nastavení služba Azure Automation Inventory Service nemonitoruje nastavení souborů nebo registru. Řešení nabízí seznam klíčů registru, které doporučujeme monitorovat. Pokud chcete zobrazit tento seznam, přejděte na účet Automation v Azure Portal a vyberte**nastavení úprav** **inventáře** > :

![Snímek obrazovky zobrazení inventáře Azure Automation v Azure Portal](./media/change-tracking1.png)

Další informace o jednotlivých klíčích registru najdete v tématu [sledování změn klíčů registru](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Můžete vyhodnotit a pak povolit každý klíč tak, že ho vyberete. Toto nastavení se použije u všech virtuálních počítačů povolených v aktuálním pracovním prostoru.

Můžete také sledovat důležité změny souborů. Můžete například chtít sledovat soubor C:\Windows\System32\drivers\etc\hosts, protože OS používá nástroj k mapování názvů hostitelů na IP adresy. Změny v tomto souboru můžou způsobit problémy s připojením nebo přesměrovat provoz na nebezpečné weby.

Chcete-li povolit sledování obsahu souborů pro hostitele, postupujte podle kroků v části [Povolení sledování obsahu souborů](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

Můžete také přidat výstrahu pro změny provedené v souborech, které sledujete. Řekněme například, že chcete nastavit výstrahu pro změny provedené v souboru Hosts. Začněte tím, že na panelu příkazů kliknete na Log Analytics **Log Analytics** , nebo když otevřete hledání protokolu pro propojený Log Analytics pracovní prostor. Až budete v Log Analytics, vyhledejte změny obsahu v souboru Hosts pomocí následujícího dotazu:

```kusto
ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
```

![Snímek obrazovky s editorem dotazů Log Analytics v Azure Portal](./media/change-tracking2.png)

Tento dotaz vyhledá změny v obsahu souborů, které mají cestu obsahující slovo "hostitelé". Konkrétní soubor můžete vyhledat také tak, že změníte parametr cesty. (Například `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`.)
  
Jakmile dotaz vrátí výsledky, vyberte **nové pravidlo výstrahy** a otevřete Editor pravidel výstrah. Tento editor můžete také získat pomocí Azure Monitor v Azure Portal.

V editoru pravidel výstrah zkontrolujte dotaz a v případě potřeby změňte logiku výstrahy. V takovém případě chceme, aby se výstraha vyvolala v případě, že se v jakémkoli počítači v prostředí zjistí nějaké změny.

![Snímek obrazovky s editorem pravidel výstrah Log Analytics v Azure Portal](./media/change-tracking3.png)

Po nastavení logiky podmínky můžete přiřadit skupiny akcí k provádění akcí v reakci na danou výstrahu. V tomto příkladu se při vyvolání výstrahy odesílají e-maily a vytvoří se lístek ITSM. Můžete provádět spoustu dalších užitečných akcí, jako je aktivace funkce Azure, Azure Automation Runbooku, Webhooku nebo aplikace logiky.

![Snímek obrazovky s ukázkou Shrnutí pravidla výstrah v Azure Portal](./media/change-tracking4.png)

Po nastavení všech parametrů a logiky použijte upozornění pro prostředí.

## <a name="more-tracking-and-alerting-examples"></a>Další příklady sledování a upozorňování

Tady je několik dalších běžných scénářů pro sledování a upozorňování, které byste mohli chtít vzít v úvahu:

### <a name="driver-file-changed"></a>Soubor ovladače se změnil.

Zjištění, zda jsou soubory ovladačů změněny, přidány nebo odebrány. Hodí se ke sledování změn důležitých systémových souborů.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Konkrétní služba byla zastavena.

Hodí se ke sledování změn pro důležité systémové služby.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Nově nainstalovaný software

Užitečné pro prostředí, která potřebují zamknout konfigurace softwaru.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Konkrétní verze softwaru je nebo není nainstalovaná na počítači.

Užitečné pro vyhodnocování zabezpečení. Všimněte si, že tento `ConfigurationData`dotaz odkazuje na, který obsahuje protokoly pro inventarizaci a oznamuje poslední nahlášený stav konfigurace, nikoli změny.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-registry"></a>Známá knihovna DLL se změnila prostřednictvím registru

Užitečné pro detekci změn známých klíčů registru.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Další kroky

Naučte se spravovat aktualizace svých serverů vytvořením [plánů aktualizací](./update-schedules.md) pomocí Azure Automation.

> [!div class="nextstepaction"]
> [Vytvoření plánů aktualizací](./update-schedules.md)
