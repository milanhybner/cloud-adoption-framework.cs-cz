---
title: Přehled migrace mainframů
description: Migrujte úlohy, aplikace a databáze z mainframů do Azure a zajistěte si prověřenou, vysoce dostupnou a škálovatelnou infrastrukturu bez řady nevýhod, které sálové počítače mají.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b38408033231a4ac1d8debe889117c2f5220c676
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223670"
---
<!-- cspell:ignore nanra njray dbspaces dbextents VSAM RACF LPARS ASSGN DLBL EXTENT LIBDEF EXEC IPLs -->

# <a name="mainframe-migration-overview"></a>Přehled migrace mainframů

Řada společností a organizací s výhodou využívá přesun některých nebo všech mainframových úloh, aplikací a databází do cloudu. Azure poskytuje funkce podobné jako mainframy v cloudovém měřítku a bez řad nevýhod, které jsou se sálovými počítači spojené.

Pojem sálový počítač obecně označuje velký počítačový systém, ale velká většina aktuálně nasazených sálových počítačů jsou servery IBM System Z nebo systémy kompatibilní s IBM, na kterých běží MVS, DOS, VSE, OS/390 nebo Z/OS. Sálové systémy se v mnoha odvětvích i nadále používají ke spouštění důležitých informačních systémů a mají své místo ve vysoce specifických scénářích, jako jsou rozsáhlá IT prostředí s velkými nároky na transakce.

Migrace do cloudu umožňuje společnostem modernizovat jejich infrastrukturu. Prostřednictvím cloudových služeb můžete mainframové aplikace a jejich funkce zpřístupnit jako úlohy, kdykoli to vaše organizace potřebuje. Řadu úloh je možné přenést do Azure jenom s drobnými změnami kódu, jako je třeba aktualizace názvů databází. Složitější úlohy můžete migrovat pomocí fázovaného přístupu.

Většina společností Fortune 500 už pro důležité úlohy využívá Azure. Hnacím faktorem celé řady migračních projektů jsou významné výhody, které Azure nabízí. Společnosti obvykle do Azure nejdřív přenesou úlohy vývoje a testování a za nimi následuje DevOps, e-mail a zotavení po havárii jako služba.

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Pokud zvažujete migraci nebo doplnění cloudových služeb do vašeho IT prostředí, je tento průvodce určený právě pro vás.

Tyto materiály pomáhají IT organizacím zahájit diskuzi o migraci. Je pravděpodobné, že Azure a cloudové infrastruktury znáte lépe než sálové počítače, proto na začátku tohoto průvodce najdete přehled toho, jak sálové počítače fungují. Dál následují různé strategie pro určení, co a jak migrovat.

## <a name="mainframe-architecture"></a>Architektura sálových počítačů

Sálové počítače byly navrženy na sklonku 50. let minulého století jako škálovací servery pro spouštění dávkového zpracování a online transakcí s velkým objemem. Z tohoto důvodu sálové počítače mají software pro online transakční formuláře (někdy označované jako zelené obrazovky) a vysoce výkonné vstupně-výstupní systémy pro zpracování dávkových běhů.

Sálové počítače jsou známé vysokou spolehlivostí a dostupností a také schopností spouštět obrovské online transakce a dávkové úlohy. Transakce je výsledkem zpracování iniciovaného jedním požadavkem, zpravidla od uživatele na terminálu. Transakce mohou také pocházet z řady dalších zdrojů, včetně webových stránek, vzdálených pracovních stanic a aplikací z jiných informačních systémů. Transakce se také může aktivovat automaticky v předdefinovaném čase, jak ukazuje následující obrázek.

![Komponenty typické architektury sálového počítače IBM](../../_images/mainframe-migration/mainframe-architecture.png)

Typická architektura sálového počítače IBM zahrnuje tyto komponenty:

- **Front-endové systémy:** Uživatelé mohou iniciovat transakce z terminálů, webových stránek nebo vzdálených pracovních stanic. Mainframové aplikace často mají vlastní uživatelská rozhraní, která se po migraci do Azure dají zachovat. Pro přístup k mainframových aplikacím se stále využívají emulátory terminálů (označují se také jako terminály se zelenou obrazovkou).

- **Aplikační vrstva:** Sálové počítače obvykle zahrnují systém CICS (Customer Information Control System), špičkovou sadu pro správu transakcí pro mainframy IBM z/OS, která se často využívá se systémem IBM Information Management System (IMS), což je správce transakcí založený na zprávách. Dávkové systémy zpracovávají aktualizace dat s velkou propustností pro velké objemy záznamů účtů.

- **Kód:** Mezi programovací jazyky používané sálovými počítači patří COBOL, FORTRAN, PL/I a Natural. Pro práci se z/OS se využívá jazyk JCL (Job Control Language).

- **Databázová vrstva:** . Běžným systémem pro správu relačních databází (DBMS) pro z/OS je IBM DD2. Spravuje datové struktury označované jako *dbspace*, které obsahují jednu nebo několik tabulek a které jsou přiřazené fondům úložiště fyzických datových sad označovaných jako *dbextent*. Dvěma důležitými databázovými komponentami jsou adresář, který identifikuje umístění dat ve fondech úložiště, a protokol, který obsahuje záznam operací provedených pro příslušnou databázi. Podporují se různé datové formáty plochých souborů. DB2 pro z/OS obvykle k ukládání dat využívá metodu VSAM (Virtual Storage Access Method).

- **Vrstva správy:** Sálové počítače IBM zahrnují plánovací software, například TWS-OPC, nástroje pro správu výstupu a tisku, jako jsou CA-SAR a SPOOL, a systém správy zdrojového kódu. Zabezpečené řízení přístupu pro z/OS zajišťuje RACF (Resource Access Control Facility). Správce databáze poskytuje přístup k datům v databázi a běží ve vlastním oddílu v prostředí z/OS.

- **LPAR:** Logické oddíly (označované jako LPAR) se využívají k dělení počítačových prostředků. Fyzický sálový počítač je rozdělený do několika LPAR.

- **z/OS:** 64bitový operační systém, který se nejčastěji využívá pro sálové počítače IBM.

Systémy IBM využívají monitor transakcí, jako je třeba CICS, ke sledování a správě všech aspektů obchodních transakcí. CICS spravuje sdílení prostředků, integritu dat a určení priority spouštění. CICS autorizuje uživatele, přiděluje prostředky a předává databázové požadavky z aplikace do správce databáze, jako je IBM DB2.

Pro zajištění lepší optimalizace se CICS obvykle využívá s IMS/TM (dřív IMS/Data Communications nebo IMS/DC). Systém IMS byl navržený k omezení redundance dat prostřednictvím správy jedné jejich kopie. Doplňuje CICS jako transakční monitor – udržuje stav v průběhu celého procesu a zaznamenává obchodní funkce do úložiště dat.

## <a name="mainframe-operations"></a>Mainframové operace

Následuje přehled typických mainframových operací:

- **Online:** Úlohy zahrnují zpracování transakcí, správu databází a připojení. Často se implementují s využitím konektorů IBM DB2, CICS a z/OS.

- **Dávka:** Úlohy běží bez zásahu uživatele, zpravidla podle pravidelného rozvrhu, například každý pracovní den ráno. Dávkové úlohy se mohou spouštět na systémech založených na Windows nebo Linuxu pomocí emulátoru JCL, jako je Micro Focus Enterprise Server nebo software BMC Control-M.

- **Jazyk JCL (Job Control Language):** Určuje prostředky nutné ke zpracování dávkových úloh. JCL předává tyto informace do z/OS prostřednictvím sady příkazů pro řízení úloh. Základní JCL obsahuje šest typů příkazů: JOB, ASSGN, DLBL, EXTENT, LIBDEF a EXEC. Úloha může obsahovat několik příkazů EXEC (kroků) a každý krok může mít několik příkazů LIBDEF, ASSGN, DLBL a EXTENT.

- **Počáteční načtení programu (IPL):**  Označuje načtení kopie operačního systému z disku do reálného úložiště procesoru a její spuštění. IPL se používá k zotavení po výpadku. IPL je obdobou spuštění operačního systému ve virtuálních počítačích s Windows nebo Linuxem.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Mýty a fakta](./myths-and-facts.md)
