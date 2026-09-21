# Návrh schématu databáze

## Základní pojmy

Systém je abstrakce, kterou si lidé vytvářejí v procesu poznávání jako nástroj ke zkoumání reálných objektů.

Systém je tedy odrazem objektivní reality – [[Model|modelem]] vytvořeným pro její zkoumání.

### Data a informace

- Data jsou údaje získané pozorováním, měřením atd. Nemusí poskytovat informaci.
- Informace jsou taková data, která jsou k něčemu užitečná a dokážeme je interpretovat. Jde o sdělení, které odstraňuje neurčitost.
- Příklad: „Bylo?“ → ano/ne. Můžeme odpovědět a jde to změřit.

### Databázový systém

**Co je [[Databázový systém|databázový systém]]?** Systém řízení báze dat + báze dat (Oracle).

7UVDT / [[Model|modelem]] / [[Databázový systém|databázový systém]]

### Nezávislost dat

- Data a programy jsou nezávislé – není nutná změna programu při změně dat a naopak.
- **Fyzická nezávislost:** metoda uložení dat není podstatná.

### Přístup a sdílení dat

- Možnost sdílení různými uživateli a jednoduchost dostupnosti.
- Jak data ochráníme (práva atd.)?

### Redundance dat

*(Vztahuje se k relačním databázím.)*

- Dvě stejné informace v databázi na dvou různých místech.
- Chceme konzistenci.

### Konzistence databáze

- Slučitelnost s realitou.
- Optimální návrhy databáze.
- Při aktualizacích nesmí dojít k narušení konzistence.
- Transakční zpracování.

### Pojmy k vysvětlení

- **Integrita databáze:** můžeme ji ošetřit.
- **Konzistence:** integrita je nad databází.

#### Typy integrity

- **Doménová integrita:** dopředu definované hodnoty.
- **Entitní integrita:** primární klíč.
- Referenční integrita.
