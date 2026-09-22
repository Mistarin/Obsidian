# Návrh schématu databáze

## Základní pojmy

Systém je abstrakce, kterou si lidé vytvářejí v procesu poznávání jako nástroj ke zkoumání reálných objektů.

Systém je tedy odrazem objektivní reality – [[Model|modelem]] vytvořeným pro její zkoumání.

### Data a informace

- Data jsou údaje získané pozorováním, měřením atd. Nemusí poskytovat informaci.
- Informace jsou taková data, která jsou k něčemu užitečná a dokážeme je interpretovat. Jde o sdělení, které odstraňuje neurčitost.
- Příklad: „Bylo?“ → ano/ne. Můžeme odpovědět a jde to změřit.

Jakmile víme, jaká data potřebujeme a co znamenají, můžeme realitu popsat modelem a připravit návrh databáze.

<small><span style="color: gray;">Tento odstavec byl vygenerován AI. Ověřte správnost.</span></small>

### Databázový systém

**Co je [[Databázový systém|databázový systém]]?** Systém řízení báze dat + báze dat (Oracle).

Databázový systém poskytuje prostředí, ve kterém se databáze ukládá, spravuje a zpřístupňuje uživatelům.

<small><span style="color: gray;">Tento odstavec byl vygenerován AI. Ověřte správnost.</span></small>

### Pojmy k vysvětlení

Následující vlastnosti popisují, co od dobře navržené databáze očekáváme: data mají být dostupná, nemají se zbytečně opakovat a musí zůstat správná a konzistentní.

<small><span style="color: gray;">Tento odstavec byl vygenerován AI. Ověřte správnost.</span></small>

#### Nezávislost dat

**Hlavní myšlenka:** Data a programy jsou nezávislé – není nutná změna programu při změně dat a naopak.

**Podrobnosti:** [[Nezávislost dat]]

#### Přístup a sdílení dat

**Hlavní myšlenka:** Možnost sdílení různými uživateli a jednoduchost dostupnosti.

**Podrobnosti:** [[Přístup a sdílení dat]]

#### Redundance dat

**Hlavní myšlenka:** Dvě stejné informace v databázi na dvou různých místech.

**Podrobnosti:** [[Redundance dat]]

#### Konzistence databáze

**Hlavní myšlenka:** Slučitelnost s realitou.

**Podrobnosti:** [[Konzistence databáze]]

#### Integrita databáze

**Hlavní myšlenka:** Integrita databáze – můžeme ji ošetřit.

**Podrobnosti:** [[Integrita databáze]]

## Fáze definování báze dat

**Hlavní myšlenka:** Návrh databáze postupuje od pochopení požadavků uživatele přes logický návrh až k fyzické implementaci.

<small><span style="color: gray;">Tento odstavec byl vygenerován AI. Ověřte správnost.</span></small>

1. Analýza požadavků uživatele
2. Fáze logického návrhu
3. Fáze fyzické implementace

**Podrobnosti:** [[Fáze definování báze dat]]

> [!info]- Kontext nových odkazů
> 7UVDT / [[Databázový systém|databázový systém]] / [[Nezávislost dat]]
> 7UVDT / [[Databázový systém|databázový systém]] / [[Přístup a sdílení dat]]
> 7UVDT / [[Databázový systém|databázový systém]] / [[Redundance dat]]
> 7UVDT / [[Databázový systém|databázový systém]] / [[Konzistence databáze]]
> 7UVDT / [[Databázový systém|databázový systém]] / [[Integrita databáze]]
> 7UVDT / [[Databázový systém|databázový systém]] / [[Fáze definování báze dat]]
