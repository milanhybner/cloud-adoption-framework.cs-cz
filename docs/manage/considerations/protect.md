---
title: Ochrana a obnovení – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ochrana a obnovení – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ab00e80297dc85aa028550faef8ff1a66f098c22
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557515"
---
# <a name="protect-and-recover-in-cloud-management"></a>Ochrana a obnovení ve správě cloudu

Až se splní požadavky na [inventarizaci a viditelnost](./inventory.md) a [provozní dodržování předpisů](./operational-compliance.md) , můžou týmy pro správu cloudu zobrazit další informace a připravit se na potenciální výpadek úlohy. Při plánování správy cloudu musí tým začínat předpokladem, že se něco nepodaří.

Žádné technické řešení nemůže konzistentně nabízet smlouvu SLA o 100% provozu. Řešení s nejredundantními deklaracemi identity se dodávají na šest devítky nebo v 99,9999% provozu. Ale i řešení "šesté devítky" bude v kterémkoli daném roce v rozmezí 31,6 sekund. Bohužel, zřídka se v provozním investování vyžaduje, aby se dosáhlo "šesti devítky" doby provozu.

Příprava na výpadky umožní týmu detekovat chyby dřív a rychleji obnovit. Tato disciplína se zaměřuje na další kroky, které následují po chybě systému. Jak chráníte úlohy, aby je bylo možné rychle obnovit, když dojde k výpadku.

## <a name="translating-protection-and-recovery-conversations"></a>Překládání konverzací ochrany a obnovení

Úlohy, které se v rámci obchodních operací skládají z aplikací, dat, virtuálních počítačů a dalších prostředků. Každá z těchto prostředků může vyžadovat jiný přístup k ochraně a obnovení. Důležitým aspektem této disciplíny je vytvořit konzistentní závazek v rámci standardních hodnot správy a poskytnout tak výchozí bod během obchodních diskusí.

Každý prostředek podporující určitou úlohu by měl mít základní přístup s jasným závazkem na rychlost obnovení (cíle doby obnovení nebo RTO) a riziko ztráty dat (cíle bodu obnovení nebo RPO).

### <a name="recovery-time-objectives-rto"></a>Cíle pro čas obnovení (RTO)

V případě, že dojde k havárii, RTO je doba, kterou by měl trvat k obnovení všech daných systémů do stavu před haváriemi. Pro každou úlohu by to zahrnoval dobu potřebnou k obnovení minimální nezbytné funkčnosti pro virtuální počítače a aplikace. Zahrnuje také množství času potřebného k obnovení dat vyžadovaných aplikacemi.

V rámci obchodních podmínek představuje RTO množství času, po který bude podnikový proces mimo provoz. Pro klíčové úlohy by měla být tato proměnná poměrně nízká, což umožňuje rychle obnovit obchodní procesy. U úloh s nižší prioritou nemusí standardní úroveň RTO mít znatelný dopad na výkon společnosti.

Standardní hodnota pro správu by měla vytvořit plán pro nepostradatelné úlohy. Společnost pak může tento směrný plán využít jako způsob, jak zajistit další investice do doby obnovení.

### <a name="recovery-point-objectives-rpo"></a>Cíle bodu obnovení (RPO)

Ve většině systémů pro správu cloudu jsou data pravidelně zachycena a ukládána prostřednictvím určité formy ochrany dat. Čas posledního zachycení dat je označován jako bod obnovení. Pokud dojde k chybě systému, může být obnoven pouze do nejnovějšího bodu obnovení.

Pokud má systém cíl bodu obnovení měřený v hodinách nebo dnech, může dojít ke ztrátě dat za tyto hodiny nebo dny mezi posledním bodem obnovení a výpadkem. RPO za 1 den by teoreticky způsobilo ztrátu všech transakcí za den, který se zavede až k selhání.

Pro důležité systémy je možné, že cíl RPO měřený v minutách nebo sekundách může být vhodnější, aby se předešlo ztrátám v výnosech. Ale kratší cíl cíle má za následek zvýšení celkových nákladů na správu.

Standardní hodnoty pro správu by se měly soustředit na nejdelší přijatelný bod RPO, aby se minimalizovaly náklady. Tým pro správu cloudu pak může rozšířit RPO konkrétních platforem nebo úloh, což by způsobilo větší investice.

## <a name="protect-and-recover-workloads"></a>Ochrana a obnovení úloh

Většina úloh v IT prostředí podporuje velmi malý obchodní nebo technický proces. Systémy, které nemají systémový dopad na obchodní operace, nezaručují větší investice potřebné k rychlému obnovení nebo minimalizaci ztráty dat. Stanovení standardních hodnot umožní podniku jasně pochopit, jakou úroveň podpory obnovení je možné nabídnout v konzistentním, spravovatelném cenovém bodě. To pomáhá obchodním účastníkům zhodnotit hodnotu zvýšené investice do obnovení.

Pro většinu týmů pro správu cloudu má rozšířená základní hodnota s konkrétními závazky cílení na RPO/RTO pro různé prostředky a poskytuje nejužitečnější cestu pro vzájemné obchodní závazky. V následujících částech najdete několik běžných rozšířených směrných plánů, které organizacím umožňují snadno přidat funkce ochrany a obnovení prostřednictvím opakovaného procesu.

### <a name="protect-and-recover-data"></a>Ochrana a obnovení dat

Data se pravděpodobně z nejcennějších prostředků v digitální ekonomice. Možnost ochrany a obnovení dat efektivněji představuje nejběžnější rozšířené směrné plány. Pro data, která využívají provozní zatížení, může dojít ke ztrátě dat přímo na rozdíl od ztráty nebo ztráty ziskovosti. Obecně se doporučuje, aby týmy Cloud managementu poskytovaly úroveň rozšířené standardní hodnoty pro správu, která podporuje běžné datové platformy.

Před implementací operací platforem je běžné, že týmy pro správu cloudu podporují vylepšené operace pro platformu jako datovou platformu služby. Tým pro správu cloudu je třeba snadno vymáhat vyšší četnost zálohování nebo replikace více oblastí pro řešení Azure SQL nebo Cosmo DB. Díky tomu může vývojový tým snadno vylepšit RPO tím, že jednoduše modernizaci své datové platformy.

Tento myšlenkový postup se podrobněji přeskočí v [oboru operací platformy](./platform.md).

### <a name="protect-and-recover-vms"></a>Ochrana a obnovení virtuálních počítačů

Většina úloh má určitou závislost na virtuálních počítačích. Tyto virtuální počítače hostují různé aspekty řešení. Aby úloha podporovala obchodní procesy po selhání systému, musí se rychle obnovit řada těchto virtuálních počítačů.

Každé minuty výpadků na těchto virtuálních počítačích by mohlo být rovno ztrátám nebo nižší ziskovosti. Když výpadky na virtuálních počítačích mají přímý vliv na fiskální výkon firmy, RTO je velmi důležité. Virtuální počítače se dají rychleji obnovit pomocí replikace do sekundární lokality a automatizovaného obnovení. Tento model se označuje jako model obnovení Hot-teplý. V nejvyšší stav obnovení lze virtuální počítače replikovat do plně funkčního, sekundárního webového serveru. Tento dražší přístup se označuje jako model obnovení s vysokou dostupností nebo za běhu.

Každé z výše uvedených modelů zkracuje čas obnovení, což vede k rychlejšímu obnovení funkcí obchodních procesů. Každý model však také vede ke významně zvýšenému náklady na správu cloudu.

Tento myšlenkový postup se podrobněji přeskočí v [provozním oboru úloh](./workload.md).

## <a name="next-steps"></a>Další kroky

Po splnění této komponenty základního směrného plánu může tým ještě víc vymezit a vyhnout se výpadkům [operací platforem](./platform.md) a [úloh](./workload.md).

> [!div class="nextstepaction"]
> Operace s [platformou](./platform.md) 
> [úlohy](./workload.md)
