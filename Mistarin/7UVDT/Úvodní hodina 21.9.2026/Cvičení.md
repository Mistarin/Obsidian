# Cvičení – Základní pojmy

Zpět na [[Úvodní hodina]].

## 1. Systém
- **Co to je:** Účelově **vymezený celek (abstrakce)** složený ze vzájemně propojených prvků a vazeb, který jako celek plní určitou funkci či cíl a **slouží k uchopení a zkoumání reality.**
- **Definice z přednášky:** $S = (P, R)$ – systém je účelově definovaná množina prvků $P=\{p_i\}$ (*univerzum systému*) a vazeb $R=\{r_{ij}\}$ (*struktura systému*).
- **Příklad:** Osobní automobil – skládá se z motoru, převodovky, kol a řízení; jednotlivé součásti samy o sobě dopravní funkci neplní, fungují až dohromady jako systém.
- **Podrobnosti:** [[Systém]]

## 2. Model
- **Co to je:** Zjednodušené zobrazení reality či systému, které zachycuje pouze podstatné vlastnosti a vazby pro daný účel a nepodstatné detaily vynechává.
- **Definice z přednášky:** Systém je odrazem – modelem – objektivní reality vytvořeným pro její zkoumání.
- **Příklad:** Turistická mapa – zobrazuje cesty, vrstevnice a památky, ale nezaznamenává jednotlivé stromy či kameny.
- **Podrobnosti:** [[Model]]

## 3. Informační systém s databází
- **Co to je:** Komplexní systém (software, hardware, data, lidé a procesy), který zajišťuje sběr, ukládání, zpracování a distribuci informací, přičemž jako spolehlivé centrální úložiště využívá databázi.
- **Definice z přednášky:** Systém pro sběr, uchovávání, vyhledávání a zpracování dat za účelem poskytnutí informace o daném vymezeném světě objektů.
- **Příklad:** Školní systém (např. Bakaláři) – učitelé zadávají známky přes aplikaci, systém počítá průměry a vše se bezpečně ukládá do databáze školy.
- **Podrobnosti:** [[Informační systém]]

## 4. Data
- **Co to je:** Jednotlivé nezpracované údaje, hodnoty, fakta či znaky získané pozorováním nebo měřením; bez kontextu a interpretace nemají samy o sobě konkrétní sdělný význam.
- **Definice z přednášky:** Údaje získané pozorováním, měřením atd. (čísla, znaky, slova, jména, obrázky, zvuky). Samy o sobě nemusí poskytovat informaci.
- **Příklad:** Číslo `39,5` nebo řetězec `Novák` – bez doplňujícího kontextu nevíme, zda jde o teplotu, cenu, velikost bot nebo jméno pacienta.
- **Podrobnosti:** [[Data a informace]]

## 5. Informace
- **Co to je:** Data zasazená do kontextu, interpretovaná a srozumitelná pro příjemce; přinášejí novou znalost, odstraňují neurčitost a mají praktický význam pro rozhodování.
- **Definice z přednášky:** Pouze taková data, která jsou k něčemu užitečná a dají se rozumně interpretovat. Sdělení, které odstraňuje v příjemci informace neurčitost, resp. neznalost.
- **Příklad:** „Pacient Novák má tělesnou teplotu 39,5 °C.“ – údaj má jasný význam i kontext a lékař ví, že pacient má vysokou horečku.
- **Podrobnosti:** [[Data a informace]]

## 6. SŘBD (Systém řízení báze dat)
- **Co to je:** Specializované programové vybavení (DBMS – Database Management System), které zajišťuje správu, ukládání, úpravy, vyhledávání, integritu a zabezpečení dat v databázi.
- **Definice z přednášky:** Programové vybavení, které řídí všechny procesy s daty (metadaty) a zajišťuje přístupy k datům v bázi dat ($\text{DBS} = \text{SŘBD} + \text{DB}$).
- **Příklad:** Oracle Database, PostgreSQL, MySQL nebo Microsoft SQL Server.
- **Podrobnosti:** [[Databázový systém]]

## 7. Báze dat (Databáze)
- **Co to je:** Uspořádaná množina perzistentních, vzájemně integrovaných a strukturovaných dat uložených na paměťovém médiu, se kterými SŘBD manipuluje.
- **Definice z přednášky:** Množina vzájemně propojených dat, které využívají aplikace. Data jsou uložena v paměti způsobem vylučujícím nežádoucí redundanci.
- **Příklad:** Samotná kolekce datových souborů a tabulek e-shopu (např. tabulky `Zákazníci`, `Objednávky`, `Položky`) uložená na serveru.
- **Podrobnosti:** [[Databázový systém]]

## 8. Integrita
- **Co to je:** Správnost, úplnost a platnost uložených dat podle definovaných pravidel (integritních omezení), která systém hlídá a vynucuje.
- **Definice z přednášky:** Doménová integrita (rozsah hodnot), entitní integrita (primární klíč) a referenční integrita (vazby a cizí klíče).
- **Příklad:** Věk nesmí být záporné číslo (doménová integrita), každý záznam má jedinečný primární klíč (entitní integrita) a objednávka nemůže odkazovat na neexistujícího zákazníka (referenční integrita).
- **Podrobnosti:** [[Integrita databáze]]

## 9. Konzistence
- **Co to je:** Bezrozpornost dat a jejich logický soulad s realitou i stanovenými pravidly za všech okolností (před i po provedení libovolné transakce).
- **Definice z přednášky:** Slučitelnost databáze. Chyby při aktualizaci redundantních dat vedou k narušení konzistence (slučitelnosti) databáze.
- **Příklad:** Bankovní převod – při převodu 500 Kč z účtu A na účet B se částka z účtu A odečte a na účet B přičte; nemůže nastat mezistav, kdy peníze z A zmizí, ale na B nepřibudou.
- **Podrobnosti:** [[Konzistence databáze]]

> [!info]- Kontext nových odkazů
> 7UVDT / [[Úvodní hodina]] / [[Systém]]
> 7UVDT / [[Úvodní hodina]] / [[Model]]
> 7UVDT / [[Úvodní hodina]] / [[Informační systém]]
> 7UVDT / [[Úvodní hodina]] / [[Data a informace]]
> 7UVDT / [[Úvodní hodina]] / [[Databázový systém]]
> 7UVDT / [[Úvodní hodina]] / [[Integrita databáze]]
> 7UVDT / [[Úvodní hodina]] / [[Konzistence databáze]]