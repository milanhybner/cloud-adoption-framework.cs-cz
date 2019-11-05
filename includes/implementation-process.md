<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="dependent-decisions"></a>Závislá rozhodnutí

Následující rozhodnutí pocházejí od týmů mimo tým zásad správného řízení cloudu. Implementace každého z nich bude pocházet od stejných týmů. Tým zásad správného řízení cloudu je však zodpovědný za implementaci řešení pro ověření, že jsou tyto implementace konzistentně uplatněny.

### <a name="identity-baseline"></a>Standardní hodnoty identit

Základní výchozím bodem pro všechny zásady správného řízení je standardní hodnota identity. Než se pokusíte použít zásady správného řízení, musí být navázána identita. Vytvořená strategie identity se pak vynutila řešeními zásad správného řízení.
V této příručce zásad správného řízení implementuje tým správy identit vzor **[synchronizace adresářů](~/decision-guides/identity/index.md#directory-synchronization)** :

- RBAC vám poskytne služba Azure Active Directory (Azure AD), pomocí synchronizace adresářů nebo stejného přihlašování, které jste implementovali během migrace společnosti na Office 365. Pokyny k implementaci najdete v tématu [Referenční architektura pro integraci služby Azure AD](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad).
- Tenant Azure AD bude také řídit ověřování a přístup pro prostředky nasazené do Azure.

V rámci nástroje MVP pro kontrolu zásad správného řízení vynutil tým zásad správného použití replikovaného klienta prostřednictvím nástrojů pro řízení předplatného, které jsou popsané dále v tomto článku. V budoucích iteracích může tým zásad správného řízení ve službě Azure AD vyhovět bohatě nástrojů pro rozšiřování této možnosti.

### <a name="security-baseline-networking"></a>Standardní hodnoty zabezpečení: sítě

Softwarově definovaná síť je důležitý počáteční aspekt standardních hodnot zabezpečení. Zřizování MVP pro řízení MVP závisí na počátečních rozhodnutích od týmu správy zabezpečení a definování způsobu, jakým se dají sítě bezpečně konfigurovat.

Vzhledem k nedostatku požadavků se zabezpečení IT hraje v bezpečí a vyžaduje vzor **[Cloud DMZ](~/decision-guides/software-defined-network/cloud-dmz.md)** . To znamená, že zásady správného řízení nasazení Azure samy budou velmi lehké.

- Předplatná Azure se můžou připojovat k existujícímu datovému centru prostřednictvím sítě VPN, ale musí dodržovat všechny existující zásady zásad správného řízení IT, které se týkají připojení zóny demilitarizovaná k chráněným prostředkům. Pokyny k implementaci týkající se připojení k síti VPN najdete v tématu [Referenční architektura sítě VPN](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn).
- Rozhodnutí týkající se podsítě, brány firewall a směrování jsou momentálně odvoditelné na jednotlivé zájemce týkající se aplikací a úloh.
- Před vypuštěním libovolných chráněných dat nebo úloh, které jsou důležité pro kritické úlohy, se vyžaduje další analýza.

V tomto modelu se můžou cloudové sítě připojit jenom k místním prostředkům přes existující síť VPN, která je kompatibilní s Azure. Přenosy přes toto připojení se budou zacházet jako s jakýmkoli provozem ze zóny demilitarizovaná. K zabezpečenému zpracování provozu z Azure se můžou na místním hraničním zařízení vyžadovat další požadavky.

Tým zásad správného řízení cloudu proaktivně pozvaní členů sítě a týmů zabezpečení IT na pravidelné schůzky, aby bylo možné udržet počet požadavků a rizik v síti.

### <a name="security-baseline-encryption"></a>Standardní hodnoty zabezpečení: šifrování

Šifrování je další základní rozhodnutí v rámci oboru standardních hodnot zabezpečení. Protože společnost v současnosti zatím neukládá žádná chráněná data v cloudu, tým zabezpečení se rozhodl o méně agresivním vzoru pro šifrování.
V tomto okamžiku je **[vzor nativního cloudu pro šifrování](~/decision-guides/encryption/index.md#key-management)** navržený, ale nevyžaduje se u žádného vývojového týmu.

- Nejsou nastavené žádné požadavky zásad správného řízení, které se týkají použití šifrování, protože aktuální podnikové zásady nepovolují v cloudu kritická nebo chráněná data.
- Před uvolněním chráněných dat nebo úloh, které jsou důležité pro kritické úlohy, se vyžaduje další analýza.

## <a name="policy-enforcement"></a>Vynucování zásad

První rozhodnutí o urychlení nasazení je vzor pro vynucení. V tomto mluveném komentáři se tým zásad správného řízení rozhodl implementovat **[automatizovaný vzor vynucení](~/decision-guides/policy-enforcement/index.md#automated-enforcement)** .

- Azure Security Center budou zpřístupněny pro týmy zabezpečení a identity pro monitorování rizik zabezpečení. Oba týmy také nejspíš používají Security Center k identifikaci nových rizik a vylepšení podnikových zásad.
- Pro řízení vynucování ověřování se ve všech předplatných vyžaduje RBAC.
- Azure Policy bude publikována do každé skupiny pro správu a bude použita pro všechna předplatná. Úroveň vytvářených zásad se ale v tomto úvodním programu MVP pro dodržování zásad velmi omezí.
- I když se používají skupiny pro správu Azure, očekává se relativně jednoduchá hierarchie.
- Plány Azure budou použity k nasazení a aktualizaci předplatných pomocí požadavků na RBAC, Správce prostředků šablon a Azure Policy napříč skupinami pro správu.

## <a name="apply-the-dependent-patterns"></a>Použití závislých vzorů

Následující rozhodnutí reprezentují vzorce, které se mají vynucovat přes strategii vynucení zásad výše:

**Směrného plánu identity.** Azure modrotisky nastaví požadavky na RBAC na úrovni předplatného, aby se zajistilo, že se pro všechna předplatná nakonfigurují konzistentní identity.

**Standardní hodnoty zabezpečení: sítě** Tým zásad správného řízení cloudu udržuje šablonu Správce prostředků pro vytvoření brány VPN mezi Azure a místním zařízením VPN. Když tým aplikace vyžaduje připojení k síti VPN, tým zásad správného řízení cloudu použije šablonu Správce prostředků brány prostřednictvím Azure modrotisky.

**Standardní hodnoty zabezpečení: šifrování.** V tomto okamžiku není v této oblasti vyžadováno vynucování zásad. Tato akce bude znovu navštívena během pozdějších iterací.
