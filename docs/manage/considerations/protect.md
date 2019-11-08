---
title: Ochrana a obnovení – Správa a provoz cloudu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ochrana a obnovení – Správa a provoz cloudu
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 356d6c463e97553cb56d132c4f94e812a5b1c656
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752794"
---
# <a name="protect-and-recover-in-cloud-management"></a>Ochrana a obnovení ve správě cloudu

Až splní požadavky na [inventarizaci a viditelnost](./inventory.md) a [provozní dodržování předpisů](./operational-compliance.md), můžou týmy pro správu cloudu předpokládat a připravit se na potenciální výpadek úloh. Při plánování správy cloudu musí týmy začít s předpokladem, že se něco nepodaří.

Žádné technické řešení nemůže konzistentně nabízet smlouvu SLA o 100% provozu. Řešení s nejredundantními deklaracemi identity pro zajištění "šesti devítky" nebo 99,9999% provozu. Ale i řešení "šesté devítky" bude v kterémkoli daném roce v rozmezí 31,6 sekund. Bohužel je zřídka pro řešení, které zaručuje velkou, nepřetržitou provozní investici, která je nutná k dosažení "šesti devítky" doby provozu.

Příprava na výpadek umožňuje týmu detekovat chyby dřív a rychleji obnovit. Tato disciplína se zaměřuje na kroky, které jsou hned po chybě systému. Jak chráníte úlohy, aby je bylo možné rychle obnovit, když dojde k výpadku?

## <a name="translate-protection-and-recovery-conversations"></a>Přeložit konverzace o ochraně a obnovení

Úlohy, které se v rámci obchodních operací skládají z aplikací, dat, virtuálních počítačů a dalších prostředků. Každý z těchto prostředků může vyžadovat jiný přístup k ochraně a obnovení. Důležitým aspektem této disciplíny je vytvořit konzistentní závazek v rámci standardních hodnot správy, který může poskytovat výchozí bod během obchodních diskusí.

Minimálně každý Asset, který podporuje určitou úlohu, by měl mít základní přístup s jasným závazkem na rychlost obnovení (cíle doby obnovení nebo RTO) a riziko ztráty dat (cíle bodu obnovení nebo RPO).

### <a name="recovery-time-objectives-rto"></a>Cíle pro čas obnovení (RTO)

V případě, že dojde k započetí havárií, doba obnovení je čas, který by měl trvat k obnovení jakéhokoli systému do stavu před haváriemi. Pro každou úlohu by to zahrnoval dobu potřebnou k obnovení minimální nezbytné funkčnosti pro virtuální počítače a aplikace. Zahrnuje také množství času potřebného k obnovení dat vyžadovaných aplikacemi.

V rámci obchodních podmínek představuje RTO množství času, po který bude podnikový proces mimo provoz. Pro klíčové úlohy by měla být tato proměnná poměrně nízká, což umožňuje rychle obnovit obchodní procesy. U úloh s nižší prioritou nemusí standardní úroveň RTO mít znatelný dopad na výkon společnosti.

Základní plán správy by měl vytvořit standardní RTO pro nepostradatelné úlohy. Společnost pak může tento směrný plán využít jako způsob, jak zajistit další investice do doby obnovení.

### <a name="recovery-point-objectives-rpo"></a>Cíle bodu obnovení (RPO)

Ve většině systémů pro správu cloudu jsou data pravidelně zachycena a ukládána prostřednictvím určité formy ochrany dat. Čas posledního zachycení dat je označován jako bod obnovení. Pokud dojde k chybě systému, může být obnovena pouze na nejnovější bod obnovení.

Pokud má systém bod obnovení, který se měří v hodinách nebo dnech, může dojít k selhání systému při ztrátě dat za tyto hodiny nebo dny mezi posledním bodem obnovení a výpadkem. Jednorázová operace RPO by teoreticky způsobila ztrátu všech transakcí za den, který vede k selhání.

Pro důležité systémy je možné, že RPO, který se měří během minut nebo sekund, může být vhodnější použít k zamezení ztrátám v výnosech. Ale kratší cíl cíle má za následek zvýšení celkových nákladů na správu.

Pro lepší minimalizaci nákladů by se měly standardní hodnoty správy soustředit na nejdéle přijatelný bod RPO. Tým pro správu cloudu pak může rozšířit RPO konkrétních platforem nebo úloh, což by způsobilo větší investice.

## <a name="protect-and-recover-workloads"></a>Ochrana a obnovení úloh

Většina úloh v IT prostředí podporuje konkrétní obchodní nebo technické procesy. Systémy, které nemají systémovým dopadům na obchodní operace, nezaručují větší investice potřebné k rychlému obnovení nebo minimalizaci ztráty dat. Díky vytvoření směrného plánu může společnost jasně pochopit, jakou úroveň podpory obnovení je možné nabídnout v rámci konzistentního, spravovatelného cenového bodu. Toto porozumění pomáhá obchodním stranám zhodnotit hodnotu zvýšené investice do obnovení.

Pro většinu týmů pro správu cloudu poskytuje rozšířená základní hodnota s konkrétními závazky RPO/RTO pro různé prostředky nejužitečnější cestu k vzájemným obchodním závazkům. V následujících částech najdete několik běžných rozšířených směrných plánů, které organizacím umožňují snadno přidat funkce ochrany a obnovení prostřednictvím opakovaného procesu.

### <a name="protect-and-recover-data"></a>Ochrana a obnovení dat

Data se pravděpodobně z nejcennějších prostředků v digitální ekonomice. Možnost ochrany a obnovení dat efektivněji představuje nejběžnější rozšířené směrné plány. Pro data, která využívají provozní zatížení, může dojít ke ztrátě dat přímo na rozdíl od ztráty nebo ztráty ziskovosti. Obecně doporučujeme, aby týmy pro správu cloudu nabízely úroveň rozšířených standardních hodnot správy, které podporují běžné datové platformy.

Než týmy pro správu cloudu implementují operace platforem, je běžné, že budou podporovat vylepšené operace s datovou platformou PaaS (Platform as a Service). Tým pro správu cloudu je třeba snadno vymáhat vyšší četnost zálohování nebo replikace v rámci více oblastí pro Azure SQL Database nebo Azure Cosmos DB řešení. To umožňuje vývojovému týmu snadno zdokonalit RPO tím, že modernizaci své datové platformy.

Další informace o tomto myšlenkovém procesu najdete v tématu [obor provozu platformy](./platform.md).

### <a name="protect-and-recover-vms"></a>Ochrana a obnovení virtuálních počítačů

Většina úloh má určitou závislost na virtuálních počítačích, které hostují různé aspekty řešení. Aby úloha podporovala obchodní procesy po selhání systému, je potřeba rychle obnovit určitý počet virtuálních počítačů.

Každou minutu výpadků na těchto virtuálních počítačích by mohlo dojít ke ztrátě výnosů nebo snížení ziskovosti. Pokud má výpadek virtuálních počítačů přímý dopad na fiskální výkon firmy, je RTO velmi důležité. Virtuální počítače je možné rychleji obnovit pomocí replikace do sekundární lokality a automatizovaného obnovení, modelu, který se označuje jako model obnovení Hot-teple. V nejvyšší stav obnovení lze virtuální počítače replikovat do plně funkčního, sekundárního webového serveru. Tento dražší přístup se označuje jako model obnovení s vysokou dostupností nebo za horkou.

Každý z výše uvedených modelů snižuje RTO, což vede k rychlejšímu obnovení funkcí obchodních procesů. Každý model však také vede ke významně zvýšenému náklady na správu cloudu.

Další informace o tomto myšlenkovém procesu najdete v tématu [provozní obor úlohy](./workload.md).

## <a name="next-steps"></a>Další kroky

Po splnění této komponenty základního směrného plánu může tým vypadat předem, aby nedocházelo k výpadkům v [operacích platforem](./platform.md) a [operacích úloh](./workload.md).

> [!div class="nextstepaction"]
> Operace s [platformou](./platform.md)
> [úlohy](./workload.md)
