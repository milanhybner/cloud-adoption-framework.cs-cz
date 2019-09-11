<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->
> [!NOTE]
>V případě změny vašich obchodních požadavků vám skupiny pro správu Azure umožní snadno reorganizovat hierarchii správy a přiřazení skupin předplatných. Mějte však na paměti, že přiřazení zásad a rolí skupině pro správu dědí všechna předplatná, která jsou v hierarchii pod touto skupinou. Pokud chcete změnit přiřazení předplatných mezi skupinami pro správu, ujistěte se, že znáte všechny potenciální dopady změn přiřazení zásad a rolí. Další informace najdete v [dokumentaci ke skupinám pro správu Azure](/azure/governance/management-groups).

### <a name="governance-of-resources"></a>Zásady správného řízení prostředků

Základní úroveň vynucování zásad správného řízení vám poskytne sada globálních zásad a rolí RBAC. Pro splnění požadavků zásad týmu zásad správného řízení v cloudu vyžaduje implementace MVP zásad správného řízení dokončení následujících úloh:

1. Identifikace definic Azure Policy potřebných k vynucování obchodních požadavků To může zahrnovat použití integrovaných definic a vytvoření nových vlastních definic.
2. Vytvoření definice podrobného plánu s využitím těchto integrovaných a vlastních zásad a přiřazení rolí, které vyžaduje MVP zásad správného řízení
3. Globální použití zásad a konfigurace přiřazením definice podrobného plánu všem předplatným

#### <a name="identify-policy-definitions"></a>Identifikace definic zásad

Azure poskytuje několik předdefinovaných zásad a definic rolí, které můžete přiřadit jakékoli skupině pro správu, předplatnému nebo skupině prostředků. Mnoho běžných požadavků zásad správného řízení můžete zpracovat pomocí integrovaných definic. Je ale pravděpodobné, že budete také muset vytvořit vlastní definice zásad pro zpracování vašich specifických požadavků.

Vlastní definice zásad se ukládají do skupiny pro správu nebo předplatného a dědí se v rámci hierarchie skupiny pro správu. Pokud je umístěním pro uložení definice zásad skupina pro správu, je tato definice zásad k dispozici pro přiřazení k jakýmkoli podřízeným skupinám pro správu nebo předplatným této skupiny pro správu.

Vzhledem k tomu, že by zásady požadované k zajištění podpory MVP zásad správného řízení měly platit pro všechna aktuální předplatná, následující obchodní požadavky se implementují se pomocí kombinace integrovaných a vlastních definic vytvořených v kořenové skupině pro správu:

1. Omezení seznamu dostupných přiřazení rolí na sadu předdefinovaných rolí Azure autorizovaných týmem zásad správného řízení v cloudu To bude vyžadovat [vlastní definici zásad](https://github.com/Azure/azure-policy/tree/master/samples/Authorization/allowed-role-definitions). 
2. Vyžadování použití následujících značek u všech prostředků: *Oddělení/fakturační jednotka*, *Geografická oblast*, *Klasifikace dat*, *Důležitost*, *Smlouva SLA*, *Prostředí*, *Archetyp aplikace*, *Aplikace* a *Vlastník aplikace*. To můžete zpracovat pomocí integrované definice Vyžadovat určenou značku.
3. Vyžadování, aby značka *Aplikace* u prostředků odpovídala názvu příslušné skupiny prostředků To můžete zpracovat pomocí integrované definice Vyžadovat značku a její hodnotu.

Informace o definování vlastních zásad najdete v [dokumentaci ke službě Azure Policy](/azure/governance/policy/tutorials/create-custom-policy-definition). Pokyny a příklady vlastních zásad najdete na [webu s ukázkami pro službu Azure Policy](/azure/governance/policy/samples) a v přidruženém [úložišti GitHub](https://github.com/Azure/azure-policy).

#### <a name="assign-azure-policy-and-rbac-roles-using-azure-blueprints"></a>Přiřazování rolí Azure Policy a RBAC s využitím služby Azure Blueprints

Zásady Azure můžou být přiřazené na úrovni skupiny prostředků, předplatného a skupiny pro správu a můžou být součástí [Azure Blueprints](/azure/governance/blueprints/overview). Přestože se požadavky zásad definované v tomto MVP zásad správného řízení vztahují na všechna aktuální předplatná, je velmi pravděpodobné, že budoucí nasazení budou vyžadovat výjimky nebo alternativní zásady. Z tohoto důvodu přiřazování zásad s využitím skupin pro správu, kde tato přiřazení dědí všechna podřízená předplatná, nemusí být dostatečně flexibilní pro zajištění podpory těchto scénářů.

Služba Azure Blueprints umožňuje konzistentní přiřazování zásad a rolí, používání šablon Resource Manageru a nasazování skupin prostředků do několika předplatných. Stejně jako definice zásad se definice podrobných plánů ukládají do skupin pro správu nebo předplatných a díky dědičnosti jsou k dispozici pro všechny podřízené prvky v hierarchii skupiny pro správu.

Tým zásad správného řízení v cloudu se rozhodl implementovat vynucování požadovaných přiřazení Azure Policy a RBAC napříč předplatnými prostřednictvím služby Azure Blueprints a přidružených artefaktů.

1. V kořenové skupině pro správu vytvořte definici podrobného plánu `governance-baseline`.
2. Do definice podrobného plánu přidejte následující artefakty podrobného plánu:
    1. Přiřazení zásad pro vlastní definice Azure Policy definované v kořenové skupině pro správu
    2. Definice skupin prostředků pro všechny požadované skupiny v předplatných vytvořených nebo řízených prostřednictvím MVP zásad správného řízení
    3. Standardní přiřazení rolí požadovaná v předplatných vytvořených nebo řízených prostřednictvím MVP zásad správného řízení
3. Publikujte definici podrobného plánu.
4. Přiřaďte definici podrobného plánu `governance-baseline` všem předplatným.

Další informace o vytváření a používání definic podrobných plánů najdete v [dokumentaci ke službě Azure Blueprints](/azure/governance/blueprints/overview).

### <a name="secure-hybrid-vnet"></a>Zabezpečená hybridní síť VNet

Konkrétní předplatná často vyžadují určitou úroveň přístupu k místním prostředkům. To je běžné ve scénářích migrace nebo vývoje, ve kterých se závislé prostředky nacházejí v místním datacentru.

Dokud se s cloudovým prostředím úplně nenaváže vztah důvěryhodnosti, je důležité pečlivě kontrolovat a monitorovat veškerou povolenou komunikaci mezi místním prostředím a cloudovými úlohami, stejně jako zabezpečení místní sítě před potenciálním neoprávněným přístupem z cloudových prostředků. Pro zajištění podpory těchto scénářů přidává MVP zásad správného řízení následující osvědčené postupy:

1. Vytvořte zabezpečenou hybridní cloudovou síť VNet.
    1. [Referenční architektura sítě VPN](/azure/architecture/reference-architectures/hybrid-networking/vpn) stanovuje vzor a model nasazení pro vytvoření služby VPN Gateway v Azure.
    2. Ověřte, že místní mechanismy zabezpečení a správy provozu pracují s připojenými cloudovými sítěmi jako s nedůvěryhodnými. Prostředky a služby hostované v cloudu by měly mít přístup pouze k autorizovaným místním službám.
    3. Ověřte, že je místní hraniční zařízení v místním datacentru kompatibilní s [požadavky služby Azure VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpn-devices) a že jeho konfigurace umožňuje přístup k veřejnému internetu.
1. V kořenové skupině pro správu vytvořte druhou definici podrobného plánu `secure-hybrid-vnet`.
    1. Jako artefakt k definici podrobného plánu přidejte šablonu Resource Manageru pro službu VPN Gateway.
    2. Jako artefakt k definici podrobného plánu přidejte šablonu Resource Manageru pro virtuální síť.
    3. Publikujte definici podrobného plánu.
1. Přiřaďte definici podrobného plánu `secure-hybrid-vnet` všem předplatným, která vyžadují možnosti připojení k místnímu prostředí. Tuto definici byste měli přiřadit navíc k definici podrobného plánu `governance-baseline`.

Jednou z největších obav týmů zabezpečení IT a tradičních týmů zásad dodržování předpisů je riziko, že přechod na cloud v počáteční fázi ohrozí zabezpečení stávajících prostředků. Výše uvedený přístup umožňuje týmům přechodu na cloud vytvářet a migrovat hybridní řešení s menším rizikem pro místní prostředky. S tím, jak se bude důvěra v cloud prohlubovat, se můžou v dalších fázích evoluce tato dočasná řešení odebrat.

> [!NOTE]
> Výše je popsaný výchozí bod pro rychlé vytvoření základního MVP zásad správného řízení. Toto je pouze začátek cesty k zásadám správného řízení. S tím, jak společnost bude pokračovat v přechodu na cloud a přijímat další rizika, bude potřeba další vývoj v následujících oblastech:
>
> - Klíčové úlohy
> - Chráněná data
> - Správa nákladů
> - Scénáře s více cloudy
>
> Konkrétní podrobnosti o tomto MVP navíc vycházejí z příkladu cesty fiktivní společnosti popsané v následujících článcích. Před implementací tohoto osvědčeného postupu doporučujeme, abyste se seznámili s dalšími články v této sérii.
