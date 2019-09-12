<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="policy-statements"></a>Příkazy zásad

Následující příkazy zásad určují požadavky potřebné k nápravě definovaných rizik. Tyto zásady definují funkční požadavky pro MVP pro zásady správného řízení. Každé bude reprezentovat v implementaci MVP pro řízení.

Cost Management:

- Pro účely sledování musí být všechny prostředky přiřazeny vlastníkovi aplikace v rámci jedné z hlavních obchodních funkcí.
- V případě, že dojde k cenovým obavám, budou se finančnímu týmu navázat další požadavky na řízení.

Základní hodnoty zabezpečení:

- Každý Asset nasazený do cloudu musí mít schválenou klasifikaci dat.
- Do cloudu se nedají nasadit žádné prostředky identifikované s chráněnou úrovní dat, dokud nebudou schválené a implementované dostatečné požadavky na zabezpečení a zásady správného řízení.
- Dokud se nemůžou ověřit a řídit minimální požadavky na zabezpečení sítě, cloudová prostředí se zobrazují jako demilitarizovaná zóna a musí splňovat podobné požadavky na připojení jiným datovým centrům nebo interním sítím.

Konzistence prostředků:

- Vzhledem k tomu, že v této fázi nejsou nasazeny žádné zásadní úlohy, nemusíte mít žádné požadavky na smlouvu SLA, výkon nebo BCDR.
- Pokud jsou nasazené úlohy kritické, budou se pro IT operace navázat další požadavky na zásady správného řízení.

Směrné plány identity:

- Všechny prostředky nasazené do cloudu by se měly řídit pomocí identit a rolí schválených aktuálními zásadami správného řízení.
- Všechny skupiny v místní infrastruktuře služby Active Directory, které mají zvýšená oprávnění, by měly být namapované na schválenou roli RBAC.

Akcelerace nasazení:

- Všechny prostředky musí být seskupené a označené podle definovaných strategií seskupení a označování.
- Všechny prostředky musí používat schválený model nasazení.
- Jakmile se pro poskytovatele cloudu zřídí základ zásad správného řízení, musí být všechny nástroje pro nasazení kompatibilní s nástroji definovanými týmem zásad správného řízení.

## <a name="processes"></a>Procesy

Nebylo přiděleno žádné rozpočty pro průběžné monitorování a vynucování těchto zásad správného řízení. Z toho důvodu má tým zásad správného pro Cloud nějaké možnosti, jak sledovat dodržování příkazů zásad.

- **Školení** Tým zásad správného řízení cloudu umožňuje investovat na základě průvodců zásad správného řízení, které tyto zásady podporují, k informování týmů pro přijímání cloudu.
- **Recenze nasazení:** Před nasazením jakékoli assetu si tým zásad správného řízení v cloudu přezkoumá Průvodce zásadou správného řízení s týmy pro přijetí v cloudu.
