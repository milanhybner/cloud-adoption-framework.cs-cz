---
title: Povolit sledování a upozorňování na kritické změny
description: Povolit sledování a upozorňování na kritické změny
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 0cd8776c71eae22fdb7a7894b656a3dc1948e45c
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808103"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Povolit sledování a upozorňování na kritické změny

Azure Change Tracking a inventář poskytují výstrahy týkající se stavu konfigurace hybridního prostředí a změny v tomto prostředí. Může ohlásit důležité změny souboru, služby, softwaru a registru, které mohou mít vliv na nasazené servery.

Ve výchozím nastavení služba Azure Automation Inventory Service nemonitoruje nastavení souborů nebo registru. Řešení nabízí seznam klíčů registru, které doporučujeme monitorovat. Pokud chcete tento seznam zobrazit, přejděte na účet Automation v Azure Portal a vyberte **inventář** > **Upravit nastavení**.

![Snímek obrazovky zobrazení inventáře Azure Automation v Azure Portal](./media/change-tracking1.png)

Další informace o jednotlivých klíčích registru najdete v tématu [sledování změn klíčů registru](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Vyberte libovolný klíč, který chcete vyhodnotit, a pak ho povolte. Nastavení se použije na všechny virtuální počítače, které jsou povolené v aktuálním pracovním prostoru.

Službu můžete použít také ke sledování důležitých změn souborů. Můžete například chtít sledovat soubor C:\Windows\System32\drivers\etc\hosts, protože OS používá nástroj k mapování názvů hostitelů na IP adresy. Změny v tomto souboru můžou způsobit problémy s připojením nebo přesměrovat provoz na nebezpečné weby.

Chcete-li povolit sledování obsahu souborů pro hostitele, postupujte podle kroků v části [Povolení sledování obsahu souborů](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

Můžete také přidat výstrahu pro změny souborů, které sledujete. Řekněme například, že chcete nastavit výstrahu pro změny v souboru Hosts. Na panelu příkazů vyberte **Log Analytics** nebo vyhledejte v Log Analytics pracovním prostoru propojení. V Log Analytics pomocí následujícího dotazu vyhledejte změny v souboru hosts:

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

## <a name="tracking-and-alerting-examples"></a>Příklady sledování a upozorňování

V této části najdete další běžné scénáře sledování a upozorňování, které byste mohli chtít použít.

### <a name="driver-file-changed"></a>Soubor ovladače se změnil.

Pomocí následujícího dotazu zjistíte, jestli se soubory ovladačů změnily, přidaly nebo odebraly. Je užitečné ke sledování změn důležitých systémových souborů.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Konkrétní služba byla zastavena.

Pomocí následujícího dotazu můžete sledovat změny důležitých systémových služeb.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Nově nainstalovaný software

Pro prostředí, která potřebují uzamknout softwarové konfigurace, použijte následující dotaz.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Konkrétní verze softwaru je nebo není nainstalovaná na počítači.

K vyhodnocení zabezpečení použijte následující dotaz. Tento dotaz odkazuje na `ConfigurationData`, která obsahuje protokoly pro inventarizaci a poskytuje poslední hlášený stav konfigurace, nikoli změny.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-the-registry"></a>Známá knihovna DLL se změnila prostřednictvím registru

Pomocí následujícího dotazu zjistíte změny známých klíčů registru.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Další kroky

Naučte se, jak pomocí Azure Automation [vytvořit plány aktualizací](./update-schedules.md) pro správu aktualizací vašich serverů.

> [!div class="nextstepaction"]
> [Vytvoření plánů aktualizací](./update-schedules.md)
