---
title: Škálování s využitím několika předplatných Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naučte se škálovat s využitím několika předplatných Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: fbfe025b5e324ec685fcec3001cc8705ac001beb
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2019
ms.locfileid: "73243263"
---
# <a name="scaling-with-multiple-azure-subscriptions"></a>Škálování s využitím několika předplatných Azure

Organizace často potřebují více než jedno předplatné Azure v důsledku omezení prostředků a dalších doporučení týkajících se správy. Je důležité mít pro škálování předplatných strategii.

## <a name="production-and-nonproduction-workloads"></a>Produkční a nevýrobní úlohy

Při nasazování první provozní úlohy v Azure byste měli začít se dvěma předplatnými: jeden pro vaše provozní prostředí a jeden pro prostředí pro neproduktivní (vývoj/testování).

![Základní model předplatného, který zobrazuje klíče vedle polí označených jako produkce a neproduktivní](../../_images/ready/basic-subscription-model.png)

Tento přístup doporučujeme z několika důvodů:

- Azure má speciální nabídky předplatného pro úlohy vývoje/testování. Tyto nabídky poskytují zvýhodněné sazby za služby a licencování Azure.
- Vaše produkční a nevýrobní prostředí budou pravděpodobně mít různé sady zásad Azure. Využití samostatných předplatných usnadňuje použití jednotlivých sad zásad na úrovni předplatného.
- V předplatném pro vývoj/testování můžete chtít určit určité typy prostředků Azure pro účely testování. Pomocí samostatného předplatného můžete tyto typy prostředků používat, aniž byste je zpřístupnili v produkčním prostředí.
- Předplatná pro vývoj/testování můžete použít jako izolovaná prostředí sandboxu. Tyto sandboxy umožňují správcům a vývojářům rychle sestavovat a odstraňovat celé sady prostředků Azure. Tato izolace může také pomoct se záležitostmi ohledně ochrany dat a zabezpečení.
- Přijatelné prahové hodnoty nákladů se budou pravděpodobně lišit v rámci produkčních předplatných a předplatných pro vývoj/testování.

## <a name="other-reasons-for-multiple-subscriptions"></a>Další důvody pro více předplatných

Další předplatná můžou vyžadovat i další situace. Při rozšiřování cloudu mějte na paměti následující aspekty.

- Předplatná mají různá omezení pro různé typy prostředků. Například počet virtuálních sítí v předplatném je omezený. Když předplatné dosáhne jakéhokoli omezení, budete muset vytvořit další předplatné a umístit sem nové prostředky.

  Další informace najdete v tématu [Limity, kvóty a omezení předplatného a služeb Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).

- Každé předplatné může implementovat vlastní zásady pro nasaditelné typy prostředků a podporované oblasti.

- U předplatných v oblastech veřejného cloudu a v oblastech cloudových i státních organizací se liší omezení. Tato omezení jsou často řízena různými úrovněmi klasifikace dat v prostředích.

- Pokud z důvodů zabezpečení nebo dodržování předpisů úplně oddělíte různé sady uživatelů, můžete vyžadovat samostatná předplatná. Organizace státní správy například můžou potřebovat omezit přístup předplatného jenom na občany.

- Různá předplatná mohou mít různé typy nabídek, z nichž každá má své vlastní podmínky a výhody.

- Mezi vlastníky předplatného a vlastníkem prostředků, které se mají nasadit, mohou existovat problémy s důvěrou. Použití jiného předplatného s jiným vlastnictvím může tyto problémy zmírnit, ale jedna z nich musí také zvážit problémy s ochranou sítí a dat, které se v tomto nasazení projeví.

- Přísné finanční a geopolitické regulace mohou vyžadovat, aby některá předplatná měla oddělené finanční uspořádání. Tyto otázky mohou zahrnovat aspekty suverenity dat, společnosti s více pobočkami nebo samostatné účetní a fakturační služby pro obchodní jednotky v různých zemích a v různých měnách.

- Prostředky Azure vytvořené pomocí klasického modelu nasazení by měly být izolovány ve vlastním předplatném. Zabezpečení klasických prostředků se liší od zabezpečení prostředků nasazených prostřednictvím Azure Resource Manageru. Zásady Azure nejde použít u klasických prostředků.

- Správci služeb používající klasické prostředky mají stejná oprávnění jako vlastníci předplatného s řízením přístupu na základě role (RBAC). Zúžit přístup těchto správců služeb v rámci předplatného, které kombinuje klasické prostředky a prostředky Resource Manageru, je obtížné.

Další předplatná se také můžete rozhodnout vytvořit z jiných obchodních či technických důvodů specifických pro vaši organizaci. Mohou existovat další náklady související s příchozím přenosem dat a výchozím přenosem dat mezi předplatnými.

Řadu typů prostředků můžete přesouvat z jednoho předplatného do jiného, nebo můžete k migraci prostředků do jiného předplatného použít automatizovaná nasazení. Další informace najdete v tématu [Přesunutí prostředků do nové skupiny prostředků nebo předplatného](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="managing-multiple-subscriptions"></a>Správa více předplatných

Pokud máte jen několik předplatných, je poměrně snadné je spravovat nezávisle. Pokud ale máte velké množství předplatných, měli byste zvážit vytvoření hierarchie skupin pro správu, která zjednodušuje správu předplatných a prostředků.

Skupiny pro správu umožňují efektivní správu přístupu, zásad a dodržování předpisů u předplatných organizace. Každá skupina pro správu je kontejnerem pro jedno nebo více předplatných.

Skupiny pro správu jsou uspořádány v jedné hierarchii. Tuto hierarchii definujete v tenantovi Azure Active Directory (Azure AD), která se bude zarovnávat se strukturou a potřebami vaší organizace. Nejvyšší úroveň se označuje jako *kořenová skupina pro správu*. V hierarchii můžete definovat až šest úrovní skupin pro správu. Každé předplatné je obsaženo pouze v jedné skupině pro správu.

Azure poskytuje čtyři úrovně rozsahu správy: skupiny pro správu, předplatná, skupiny prostředků a prostředky. Jakýkoli přístup nebo zásady použité na jedné úrovni v hierarchii se dědí úrovněmi pod ní. Vlastník prostředku nebo vlastník předplatného nemůže zděděné zásady změnit. Toto omezení pomáhá zlepšit zásady správného řízení.

> [!NOTE]
> Všimněte si, že dědičnost značek není aktuálně k dispozici, ale bude brzy k dispozici.

Když se spoléháte na tento model dědičnosti, můžete uspořádat předplatná v hierarchii tak, aby každé předplatné odpovídalo příslušným zásadám a ovládacím prvkům zabezpečení.

![Čtyři úrovně rozsahu pro uspořádání prostředků Azure](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Všechna přiřazení přístupu nebo zásad v kořenové skupině pro správu se použijí pro všechny prostředky v rámci příslušného adresáře. Pečlivě zvažte, které položky v tomto oboru definujete. Zahrňte pouze ta přiřazení, která potřebujete.

Když na začátku definujete hierarchii skupin pro správu, nejprve vytvoříte kořenovou skupinu pro správu. Potom přesunete všechna existující předplatná v adresáři do kořenové skupiny pro správu. Nová předplatná se vždy vytvoří v kořenové skupině pro správu. Později je můžete přesunout do jiné skupiny pro správu.

Když přesunete předplatné do existující skupiny pro správu, zdědí zásady a přiřazení rolí z hierarchie skupin pro správu nad ní. Jakmile pro úlohy Azure vytvoříte více předplatných, měli byste vytvořit další předplatná, která by obsahovala služby Azure sdílené ostatními předplatnými.

![Příklad hierarchie skupiny pro správu](../../_images/ready/management-group-hierarchy.png)

Další informace najdete v tématu [Uspořádání vašich prostředků s využitím skupin pro správu Azure](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="tips-for-creating-new-subscriptions"></a>Tipy pro vytváření nových předplatných

- Určete, kdo bude za vytváření nových předplatných zodpovědný.
- Určete, které prostředky budou standardní součástí předplatného.
- Určete, jak by měla všechna standardní předplatná vypadat. Mezi požadavky patří přístup RBAC, zásady, značky a prostředky infrastruktury.
- Pokud je to možné, použijte k vytvoření nových předplatných [instanční objekt](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription). Definujte skupinu zabezpečení, která může vyžadovat nová předplatná prostřednictvím automatizovaného pracovního postupu.
- Pokud jste zákazníkem se smlouvou Enterprise, požádejte podporu Azure, aby pro vaši organizaci zablokovala vytváření předplatných bez smlouvy Enterprise.

## <a name="related-resources"></a>Související materiály

- [Základní koncepty Azure.](../considerations/fundamental-concepts.md)
- [Uspořádání prostředků s využitím skupin pro správu Azure.](https://docs.microsoft.com/azure/governance/management-groups)
- [Zvýšení úrovně přístupu pro správu všech předplatných Azure a skupin pro správu](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin)
- [Přesun prostředků Azure do jiné skupiny prostředků nebo předplatného](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources)

## <a name="next-steps"></a>Další kroky

Přečtěte si téma týkající se [doporučených konvencí pro tvorbu názvů a značek](./naming-and-tagging.md), které byste měli při nasazování prostředků Azure dodržovat.

> [!div class="nextstepaction"]
> [Doporučené konvence pro tvorbu názvů a značek](./naming-and-tagging.md)
