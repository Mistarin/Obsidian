# Obsidian Vault — Trezor (Mistarin)

Tento repozitář obsahuje znalostní bázi a studijní poznámky v rámci trezoru **Mistarin** (např. předměty `7UVDT`, `7GALP`).

---

## Pravidla a konvence formátování poznámek

Při vytváření a úpravách poznámek aktivně využíváme bohaté formátování v Markdownu pro maximální přehlednost a rychlou orientaci v textu:

- **Tučné písmo (`**text**`)**: Zvýraznění klíčových pojmů, hlavních myšlenek a základních stavebních kamenů látky.
- *Kurzíva (`*text*`)*: Doplňující vysvětlení, technická terminologie v angličtině či latině, proměnné a jemné nuance.
- ==Zvýraznění (`==text==`)==: Zvýraznění stěžejních částí definic, kritických zkouškových chytáků a bodů nutných k zapamatování.
- **Citace a callouty (`> text`)**: Doslovné citace definic z přednášek, pravidla a Obsidian callouty pro zdůraznění kontextu či poznámek:
  ```markdown
  > [!NOTE] Title
  > Contents
  ```
  (lze použít i další typy calloutů jako `> [!info]`, `> [!example]`, `> [!tip]`).
- **Oddělovač / divider (`---`)**: Vodorovná čára pro čisté a přehledné vizuální oddělení logických celků, témat a sekcí v poznámce.

### Zákaz AI disclaimerů
Do poznámek se **nepřidávají žádné automatické disclaimery o generování obsahu pomocí AI** (např. `<small>Tento odstavec byl vygenerován AI...</small>`). Poznámky zůstávají čisté a přirozené.

### Terminologická přesnost (zejména pro 7UVDT: data vs. informace)
Důsledně rozlišovat pojmy **data** a **informace** a nikdy je nezaměňovat:
- **Data (údaje)**: Surové, nezpracované hodnoty získané pozorováním či měřením (čísla, text, surové hodnoty bez kontextu), které samy o sobě neodstraňují neurčitost.
- **Informace**: Data zasazená do kontextu, která mají význam, dají se rozumně interpretovat a odstraňují v příjemci neurčitost či neznalost (*„Informace je sdělení, které odstraňuje v příjemci informace neurčitost, resp. neznalost.“*).
- V databázovém kontextu (např. *redundance dat*) nepoužívat slovo informace jako synonymum pro data.

### Srozumitelný a lidský jazyk (psát lidsky)
Vyvarovat se přehnaně komplikovaných akademických definic a suchopárné hantýrky. Texty psát přirozeně, srozumitelně a lidsky:
- **Přednost běžným a intuitivním slovům**: Kde existuje běžný a jasný výraz, dát mu přednost (např. místo *perzistentní* psát *trvalý / stálý (uložený na disk)*, místo *konkurentní* psát *souběžný* apod.).
- **Vysvětlení selským rozumem**: Každý složitější koncept nebo formální definici doplnit jednoduchým lidským vysvětlením či příkladem ze života.
- **Faktická přesnost bez akademického balastu**: Zachovat přesný smysl látky, ale formulovat ji tak, aby byla okamžitě pochopitelná při prvním čtení.

---

## Práce s odkazy a strukturou

- **Konvence vytváření nových odkazů:**
  Při vzniku nových odkazů uvádíme kontextový řádek v přesné šabloně:
  ```text
  <složka> / <existující_odkaz> / <nový_odkaz>
  ```
- **Složky `Odkaz/`:**
  Když téma vyžaduje více než krátké shrnutí, vytvoří se samostatná podrobná podstránka v podsložce `Odkaz/` daného tématu/předmětu a hlavní poznámka na ni pouze odkazuje.

---

## Návod pro agenty
Kompletní a detailní operační pravidla pro AI asistenty a nástroje se nacházejí v [AGENTS.md](file:///home/martin/Main/Cloud/Trezor/AGENTS.md).
