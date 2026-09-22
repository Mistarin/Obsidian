# Rekurze a vyhledávání

## Rekurze jako programátorská technika

- **Definice:** Popisuje programátorskou techniku a způsob řešení.
- **Návrhový přístup:** Podobná návrhovému vzoru (jak vyřešit nějaký problém).
- **Základní princip:** Volání kódu v sobě samém.
- **Způsoby řešení úloh:**
  - Věci můžeme řešit **rekurzivně** (technika myšlení, nikoli samotná implementace v kódu) i **iterativně** (pomocí smyček).

### Typy rekurze

- **Přímá rekurze:** $A \to A$ (funkce $A$ volá přímo samu sebe).
- **Nepřímá rekurze:** $A \to B$ a $B \to A$ (funkce $A$ volá $B$ a funkce $B$ volá $A$).

## Principy a pravidla rekurze

- **Dekompozice problému:** Rozložení problému na podproblémy – řešíme jednotlivé podproblémy a zkombinováním řešení těchto subproblémů vyřešíme hlavní problém.
- **Ukončovací podmínka (zarážka):** U rekurze je nevýhoda, že nemáme ukončovací podmínku – musíme ji definovat **(zarážka)**.
- **Využití v praxi:**
  - Rekurze se vyplatí u složitějšího problému. Pokud máme něco složitého, logicky by to akorát komplikovalo.
  - U exponenciálních posloupností používáme spíše smyčky.
  - *„Co nevíš, nemůžeš se za to zeptat.“*

### Výkon a efektivita

- **Režie zásobníku:** Rekurzivní metody bývají např. o 5 % pomalejší – je tam zásobník.
  > [!info]- Poznámka z výuky
  > JE TAM ZÁSOBNÍK – GRAJ VIBES SMH
- **Efektivita kódu:** Chceme psát efektivní kód (`čitelný != nejefektivnější`).
- **Produktivita:** 8 řádků do produkce za den $\Rightarrow$ najdu si snad práci už.

## Příklad kódu: Rekurze vs. smyčka

```python
# Iterativní řešení (pomocí smyčky / cyklu)
def faktorial_smycka(n):
    vysledek = 1
    for i in range(2, n + 1):
        vysledek *= i
    return vysledek

# Rekurzivní řešení (volání funkce v sobě samé)
def faktorial_rekurze(n):
    # Ukončovací podmínka (zarážka)
    if n <= 1:
        return 1
    # Rekurzivní volání
    return n * faktorial_rekurze(n - 1)
```

Porovnání iterativního a rekurzivního přístupu na výpočtu faktoriálu: Iterativní verze provádí výpočet v rámci jednoho rámce na zásobníku a opakuje smyčku, což šetří paměť. Rekurzivní verze při každém volání ukládá nový kontext na zásobník (call stack) a čeká na návrat hodnoty z hlubšího zanoření. Bez definované **zarážky** (`if n <= 1`) by rekurze pokračovala donekonečna a způsobila přetečení zásobníku (*stack overflow*).

<small><span style="color: gray;">Tento odstavec byl vygenerován AI. Ověřte správnost.</span></small>

## Vyhledávání

### Lineární vyhledávání

- Primitivní vyhledávání index po indexu.
- Obyčejná smyčka.

### Binární vyhledávání

- **Podmínka:** Data musí být předem **seřazená**.
- **Princip:** Půlení intervalu (algoritmus typu *rozděl a panuj*).
- **Postup:**
  1. Hledaný prvek se porovná s prvkem uprostřed intervalu.
  2. Shodují-li se, prvek je nalezen.
  3. Je-li hledaný prvek menší, vyhledávání pokračuje v levé polovině; je-li větší, v pravé polovině.
  4. Postup se opakuje, dokud prvek není nalezen nebo se interval nevyprázdní.
- **Implementace:** Lze realizovat iterativně (cyklem) i rekurzivně.
- **Složitost:** Časová složitost je $O(\log n)$ (výrazně efektivnější než lineární vyhledávání s $O(n)$).

<small><span style="color: gray;">Tento odstavec byl vygenerován AI. Ověřte správnost.</span></small>
