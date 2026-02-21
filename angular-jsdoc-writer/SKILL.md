---
name: angular-jsdoc-writer
description: Standardisiert Angular- und TypeScript-Komponenten hinsichtlich API-Dokumentation und gezielter public-Sichtbarkeit für Consumer-relevante API-Mitglieder, inklusive deutschsprachiger JSDoc im Einklang mit dem Repo-Glossar.
---

# Angular API/JSDoc (DE)

## Purpose

Überarbeite bestehende Angular-/TypeScript-Dateien ohne Verhaltensänderung, sodass:
- Consumer-relevante API-Mitglieder fehlendes `public` erhalten,
- JSDoc in deutscher Sprache konsistent und präzise ist,
- Terminologie verbindlich aus dem Repository-Glossar stammt.

## When to use

Nutze diesen Skill, wenn mindestens eine der folgenden Bedingungen erfüllt ist:
1. Fehlende `public`-Modifier bei bewusst konsumierbarer API sollen ergänzt werden.
2. Klassen-/Member-JSDoc soll vereinheitlicht oder ergänzt werden.
3. Fachbegriffe in Kommentaren sollen an die Ubiquitous Language des Repositories angepasst werden.
4. Interfaces sollen vollständig kommentiert werden (alle Properties und Methoden).

## When not to use

Nutze diesen Skill nicht, wenn:
1. Eine Verhaltensänderung, API-Redesign oder Signaturänderung gefordert ist.
2. Sichtbarkeiten verschärft oder herabgesetzt werden sollen (`public/protected/private`-Wechsel außer fehlendes `public`).
3. Nur eine minimale Einzelkorrektur ohne strukturelle Dokumentationsarbeit gewünscht ist.
4. Kein Zugriff auf die Ziel-Dateien möglich ist.

## Inputs

Erwarte vom Aufrufer:
1. `TARGETS`: Liste von Dateien und/oder Ordnern.
2. Optional `SCOPE_HINT`: Fokus (z. B. nur Komponenten, nur Interfaces, nur bestimmte Module).
3. Optional `TERM_CLARIFICATIONS`: bereits geklärte Begriffsvorgaben.

Eingaberegeln:
1. Bei Ordnern rekursiv relevante `*.ts`-Dateien verarbeiten.
2. Fokus auf Angular-Komponenten und zugehörige Klassen/Interfaces.
3. Keine Datei außerhalb der übergebenen Ziele verändern.

## Outputs

Liefere immer:
1. Angepasste Dateien mit minimalen, diff-freundlichen Änderungen.
2. Kurze Begründung je `public`-Ergänzung.
3. Explizite Bestätigung: keine Sichtbarkeits-Downgrades/Umschaltungen durchgeführt.
4. Verwendeter Glossar-Pfad aus `AGENTS.md`.
5. Liste neu geklärter Begriffe inkl. „Zu vermeidende Synonyme“ (falls vorhanden).
6. Offene Grenzfälle (nur wenn Zuordnung `public` vs. nicht-`public` fachlich unklar blieb).

## Procedure

1. **Zielmenge bestimmen**
- Expandiere `TARGETS` auf konkrete `*.ts`-Dateien.
- Behalte bestehende Member-Reihenfolge pro Klasse bei.

2. **Glossar-Quelle bestimmen (verpflichtend)**
- Lies `AGENTS.md` im Ziel-Repository.
- Ermittle dort den offiziellen Glossar-Pfad.
- Lade genau diese Datei als Single Source of Truth.
- Falls kein Pfad angegeben ist: `docs/GLOSSAR.md` als Default vorschlagen und nach Bestätigung verwenden.

3. **Terminologie-Lage prüfen**
- Erkenne unklare/mehrdeutige Begriffe in Ziel-Dateien.
- Falls Klärung nötig ist: Begriffe gesammelt und konkret nachfragen (Begriff, Bedeutung, zu vermeidende Synonyme).
- Bis zur Klärung neutrale Formulierung verwenden oder Stelle als offen markieren.

4. **Consumer-API identifizieren**
- Markiere bewusst extern nutzbare Member (z. B. Inputs/Outputs, dokumentierte API-Methoden/-Properties).
- Ergänze fehlendes `public` nur bei diesen Membern.

5. **Sichtbarkeit anpassen (streng begrenzt)**
- Erlaube nur: fehlendes `public` ergänzen.
- Verboten: jedes Downgrade/Upgrade zwischen `public/protected/private` außer fehlendes `public`.
- Keine Namens-, Signatur- oder Verhaltensänderungen.

6. **JSDoc erstellen/überarbeiten**
- Klassen-JSDoc auf Deutsch, 1-2 Sätze, fachlich/technischer Zweck.
- Bei dekorierten Klassen JSDoc direkt über dem Decorator platzieren.
- API-relevante `public`-Member präzise dokumentieren.
- Bei Interfaces jede Property und Methode kommentieren.
- `{@link ...}` für relevante Querverweise nutzen.

7. **Glossar-Abgleich und Pflege**
- Neue/angepasste Formulierungen gegen Glossar prüfen.
- Begriffe aus „Zu vermeidende Synonyme“ nicht verwenden.
- Geklärte neue Begriffe im bestehenden Glossar-Stil ergänzen.

8. **Abschlussprüfung und Ausgabe**
- Prüfe alle Verifikationspunkte (siehe Abschnitt `Verification`).
- Gib Ergebnisse exakt im erwarteten Ausgabeformat aus.

## Edge Cases and Safety Checks

1. **Unklarer API-Status eines Members**
- Keine aggressive `public`-Ergänzung.
- Als Grenzfall kennzeichnen und transparent berichten.

2. **Fehlendes oder widersprüchliches Glossar**
- Keine Begriffe erfinden.
- Standardpfad `docs/GLOSSAR.md` vorschlagen und bis zur Klärung neutrale Formulierungen nutzen.

3. **Gemischte Sprache im Codebestand**
- Neue/angepasste JSDoc grundsätzlich deutsch verfassen.
- Englische Begriffe nur bei technischen Symbolen oder wenn im Glossar etabliert.

4. **Große Dateien mit vielen Membern**
- Änderungen strikt auf API/JSDoc/Sichtbarkeit begrenzen.
- Keine Umordnung, keine Formatierungs-Massenänderungen.

5. **Decorator-Klassen ohne Klassen-JSDoc**
- JSDoc ergänzen und direkt über dem Decorator platzieren.

## Repo-Specific Conventions

1. `AGENTS.md` ist die verbindliche Quelle für den Glossar-Pfad.
2. Glossar ist Single Source of Truth für Ubiquitous Language.
3. Glossar-Stil des Repositories beibehalten, inklusive Spalte `Zu vermeidende Synonyme`.
4. Änderungen müssen diff-freundlich und minimal bleiben.
5. Keine Verhaltensänderung an Angular-/TypeScript-Code.

## Verification

Vor Abschluss müssen alle Punkte erfüllt sein:
1. Jede geänderte Datei enthält nur zielgerichtete Anpassungen an `public`/JSDoc/Terminologie.
2. Kein Member wurde umsortiert.
3. Keine Sichtbarkeit wurde herab- oder umgestellt (außer fehlendes `public` ergänzt).
4. Keine Namen, Signaturen oder Laufzeitlogik wurden verändert.
5. Klassen-JSDoc ist bei dekorierten Klassen korrekt über dem Decorator platziert.
6. Interfaces sind vollständig kommentiert.
7. Keine verbotenen Synonyme aus dem Glossar wurden in neuen/geänderten Texten verwendet.
8. Ausgabe enthält alle geforderten Output-Bestandteile vollständig.
