---
title: Přehled migrace sálového počítače
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrujte aplikace z sálových prostředí do Azure, osvědčené, vysoce dostupné a škálovatelné infrastruktury pro systémy, které se aktuálně spouštějí na sálových počítačích.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ab3692702744e5cca174fcae55ea7b9d34e72998
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70831045"
---
# <a name="mainframe-migration-overview"></a>Přehled migrace sálového počítače

Mnohé společnosti a organizace mají za úkol přesunout některé nebo všechny své sálové úlohy, aplikace a databáze do cloudu. Azure poskytuje funkce podobné sálovým službám v cloudovém měřítku bez řady nevýhod spojených s sálovými počítače.

Pojem sálový počítač obecně označuje velký počítačový systém, ale velká většina aktuálně nasazených sálových počítačů je IBM System Z nebo IBM kompatibilních systémů, které používají MVS, DOS, VSE, OS/390 nebo Z/OS. Sálové systémy se v mnoha odvětvích i nadále používají ke spouštění důležitých informačních systémů a mají místo ve vysoce specifických scénářích, jako jsou velká, vysoce objemná, rozsáhlá IT prostředí, která se náročné na transakce.

Migrace do cloudu umožňuje společnostem, aby si modernizovat svou infrastrukturu. U Cloud Services můžete vytvářet sálové aplikace a hodnotu, kterou poskytují, k dispozici jako úlohu, kdykoli ji vaše organizace potřebuje. Mnohé úlohy je možné přenést do Azure s pouze drobnými změnami kódu, jako je například aktualizace názvů databází. Složitější úlohy můžete migrovat pomocí dvoufázového přístupu.

Většina společností Fortune 500 už používá Azure pro důležité úlohy. Důležité pobídky na konci řádku pro Azure motivují mnoho projektů migrace. Společnosti obvykle přesunou vývojové a testovací úlohy do Azure, následované DevOps, e-mailem a zotavením po havárii jako služba.

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Pokud zvažujete migraci nebo přidání cloudových služeb jako možnosti pro IT prostředí, tato příručka je určena pro vás.

Tyto doprovodné materiály pomáhají IT organizacím zahájit konverzaci s migrací. Můžete být obeznámeni s Azure a cloudovou infrastrukturou, než jste v rámci sálových počítačů, takže tato příručka začíná přehledem toho, jak sálové počítače fungují a pokračuje s různými strategiemi pro určení toho, co a jak migrovat.

## <a name="mainframe-architecture"></a>Architektura sálového počítače

V pozdní 1950s byly sálové počítače navržené jako servery se škálováním na více počítačů, aby se spouštěly online transakce s vysokým objemem a dávkové zpracování. Z tohoto důvodu mají sálové počítače software pro online transakční formuláře (někdy označované jako zelené obrazovky) a vysoce výkonné vstupně-výstupní systémy pro zpracování dávkových běhů.

Sálové počítače mají reputaci s vysokou spolehlivostí a dostupností a jsou známé pro jejich schopnost spouštět obrovský online transakce a dávkové úlohy. Transakce je výsledkem zpracování iniciované jedním požadavkem, obvykle od uživatele v terminálu. Transakce mohou také pocházet z několika dalších zdrojů, včetně webových stránek, vzdálených pracovních stanic a aplikací z jiných informačních systémů. Transakci lze také automaticky aktivovat v předdefinovaném čase, jak ukazuje následující obrázek.

![Komponenty v typické architektuře sálového počítače IBM](../../_images/mainframe-migration/zOS-architectural-layers.png)

Typická Sálová architektura IBM zahrnuje tyto společné součásti:

- **Systémy front-end:** Uživatelé mohou iniciovat transakce z terminálů, webových stránek nebo vzdálených pracovních stanic. Sálové aplikace často mají vlastní uživatelská rozhraní, která je možné po migraci do Azure zachovat. Emulátory terminálu se pořád používají pro přístup k sálovým aplikacím a označují se také jako terminály zelené obrazovky.

- **Aplikační vrstva:** Sálové počítače obvykle zahrnují systém CICS (Customer Information Control System), vedoucí sadu pro správu transakcí pro sálový počítač IBM z/OS, který se často používá se správcem transakcí v systému IBM Information Management System (IMS). Systémy Batch zpracovávají vysoce propustnosti aktualizace dat pro velké objemy záznamů účtů.

- **Znakovou** Programovací jazyky, které používají sálové počítače, zahrnují COBOL, FORTRAN, PL/I a přirozené. Jazyk řízení úloh (JCL) se používá pro práci s z/OS.

- **Databázová vrstva:** Běžný systém pro správu relačních databází (DBMS) pro z/OS je IBM DD2. Spravuje datové struktury s názvem *dbspaces* , které obsahují jednu nebo více tabulek a jsou přiřazeny k fondům úložiště fyzických datových sad s názvem *dbextents*. Mezi dvě důležité databázové komponenty patří adresář, který určuje umístění dat ve fondech úložiště, a protokol, který obsahuje záznam operací provedených v databázi. Podporovány jsou různé datové formáty s plochými soubory. DB2 pro z/OS obvykle používá datové sady VSAM (Virtual Storage Access Method) k ukládání dat.

- **Úroveň správy:** Sálové počítače IBM zahrnují plánování softwaru, jako je TWS-OPC, nástroje pro tisk a správu výstupu, jako je například certifikační autorita a zařazení, a systém správy zdrojového kódu. Řízení zabezpečeného přístupu pro z/OS se zpracovává funkcí řízení přístupu k prostředkům (RACF). Správce databáze poskytuje přístup k datům v databázi a spouští se ve vlastním oddílu v prostředí z/OS.

- **LPAR:** K rozdělení výpočetních prostředků se používají logické oddíly nebo LPARs. Fyzický sálový disk je rozdělený na více LPARs.

- **z/OS:** 64 operační systém, který se nejčastěji používá pro sálové počítače IBM.

Systémy IBM používají monitorování transakcí, jako je CICS, ke sledování a správě všech aspektů obchodní transakce. CICS spravuje sdílení prostředků, integritu dat a stanovení priorit provádění. CICS autorizuje uživatele, přidělí prostředky a předává požadavky databáze aplikaci do správce databáze, jako je například IBM DB2.

Pro přesnější ladění se CICS běžně používá s IMS/TM (dříve IMS/data Communications nebo IMS/DC). Služba IMS byla navržena tak, aby se snížila redundance dat tím, že uchovává jednu kopii dat. Doplňuje CICS jako monitorování transakcí tím, že udržuje stav během celého procesu a zaznamenání obchodních funkcí do úložiště dat.

## <a name="mainframe-operations"></a>Operace sálového počítače

Následuje několik typických operací sálových počítačů:

- **Online** Úlohy zahrnují zpracování transakcí, správu databází a připojení. Často se implementují pomocí konektorů IBM DB2, CICS a z/OS.

- **Partie** Úlohy se spouštějí bez zásahu uživatele, obvykle podle pravidelného plánu, jako je například každý den v týdnu ráno. Dávkové úlohy lze spustit na systémech založených na systému Windows nebo Linux pomocí emulátoru JCL, jako je například Micro Enterprise Server nebo software BMC Control-M.

- **Jazyk řízení úloh (JCL):** Zadejte prostředky potřebné ke zpracování dávkových úloh. JCL tyto informace předává z/OS prostřednictvím sady příkazů řízení úloh. Základní JCL obsahuje šest typů příkazů: JOB, ASSGN, DLBL, rozsah, LIBDEF a EXEC. Úloha může obsahovat několik příkazů EXEC (kroky) a každý krok může mít několik příkazů LIBDEF, ASSGN, DLBL a rozsah.

- **Počáteční načtení programu (IPL):**  Odkazuje na načtení kopie operačního systému z disku do reálného úložiště procesoru a jeho spuštění. IPLs se používají k zotavení po výpadku. IPL je jako spouštění operačního systému na virtuálních počítačích se systémem Windows nebo Linux.

## <a name="next-steps"></a>Další postup

> [!div class="nextstepaction"]
> [Mýty a fakta](myths-and-facts.md)
