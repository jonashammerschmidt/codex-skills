---
name: angular-public-api-visibility-jsdoc-de
description: Standardisiert Angular- und TypeScript-Komponenten hinsichtlich Sichtbarkeit und API-Dokumentation. Verwenden, wenn `public` gezielt nur fuer Consumer-relevante API-Mitglieder ergaenzt werden soll, template-exklusive Member auf `protected` gefuehrt werden sollen, interne Details `private` bleiben sollen, und deutschsprachige JSDoc-Kommentare mit konsistenter Ubiquitous Language erstellt oder vereinheitlicht werden sollen.
---

# Angular Public API + JSDoc (DE)

Ueberarbeite uebergebene Angular-/TypeScript-Dateien so, dass Sichtbarkeit, API-Flaeche und JSDoc konsistent sind, ohne Verhaltensaenderung.

## Eingabe

Erwarte vom Aufrufer mindestens:

- Liste der zu bearbeitenden Komponenten-/Klassendateien.

Nutze kein hartcodiertes Glossar im Skill.

## Glossar-Quelle (verpflichtend)

1. Lies im Ziel-Repository die Datei `AGENTS.md`.
2. Suche dort den Abschnitt zur Ubiquitous Language bzw. den konfigurierten Glossar-Pfad.
3. Lade genau diese Glossar-Datei aus dem Ziel-Repository als Single Source of Truth.
4. Wenn in `AGENTS.md` kein Glossar-Pfad hinterlegt ist, frage nach dem gewuenschten Ablageort und schlage als Default `frontend/projects/fst/common/docs/GLOSSAR.md` vor.
5. Wenn der Ablageort bestaetigt ist, lege das Glossar bei Bedarf an und pflege anschliessend `AGENTS.md` mit dem finalen Pfad.

## Unklare Begriffe (verpflichtend klaeren)

1. Erkenne unklare, neue oder mehrdeutige Fachbegriffe in den Ziel-Dateien.
2. Frage diese Begriffe vor Abschluss aktiv nach (kurz und konkret).
3. Nutze bis zur Klaerung neutrale Formulierungen oder markiere offene Stellen.
4. Sobald die Begriffe geklaert sind, pflege sie direkt im Repo-Glossar.
5. Pflege Begriffe im bestehenden Glossar-Stil des Repositories (z. B. Einordnung, Bedeutung, Artikelkonventionen).

## Workflow

1. Analysiere jede Klasse in bestehender Reihenfolge der Member (nicht umsortieren).
2. Klassifiziere jeden Member:
- `public`: Teil der Consumer-API (z. B. Inputs/Outputs, bewusst von aussen nutzbare Methoden/Properties).
- `protected`: Nur fuer Template- oder Vererbungszugriff, nicht Teil der externen API.
- `private`: Rein interne Implementierung.
3. Ergaenze fehlende Sichtbarkeiten explizit (`public`/`protected`/`private`) ohne die Reihenfolge der Deklarationen zu aendern.
4. Erstelle oder ueberarbeite JSDoc fuer API-relevante `public`-Member auf Deutsch.
5. Nutze bei Querverweisen `{@link ...}` auf verwandte Felder, Typen oder Klassen.
6. Gleiche Formulierungen und Fachbegriffe gegen das Repo-Glossar aus.
7. Erweitere das Repo-Glossar um neu geklaerte Begriffe.

## Sichtbarkeitsregeln

- Verwende `public` nur fuer echte Consumer-API.
- Belasse bestehendes API-Verhalten; aendere keine Namen oder Signaturen ohne expliziten Auftrag.
- Verwende `protected` fuer Template-nahe Member, sofern sie nicht als externe API gedacht sind.
- Verwende `private` fuer interne Hilfslogik.
- Aendere keine Member-Reihenfolge, ausser es ist technisch zwingend.

## JSDoc-Regeln (Deutsch)

- Schreibe Kommentare in klarer deutscher Sprache.
- Erlaube englische Fachbegriffe nur, wenn sie im Repo-Glossar etabliert sind, oder sich auf Symbole bezogen wird.
- Beschreibe Zweck und Wirkung praezise statt Implementierungsdetails.
- Dokumentiere `public`-API vollstaendig und konsistent.
- Nutze `{@link TypOderMember}` fuer relevante Querverweise.

## Qualitaetskriterien

- Keine Verhaltensaenderung.
- Oeffentliche API bewusst klein und klar.
- Konsistente Terminologie gemaess Repo-Glossar.
- Ergebnis diff-freundlich: minimale, zielgerichtete Anpassungen.

## Ausgabeformat

Liefere:

- geaenderte Dateien,
- kurze Begruendung der Sichtbarkeitsentscheidungen,
- kurze Notiz mit dem verwendeten Glossar-Pfad aus `AGENTS.md` (oder dem neu vereinbarten Ablageort),
- kurze Liste der aktiv geklaerten Begriffe,
- Hinweis auf offene Grenzfaelle (falls unklar zwischen `public` und `protected`).
