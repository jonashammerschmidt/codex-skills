---
name: angular-api-jsdoc-de
description: Standardisiert Angular- und TypeScript-Komponenten hinsichtlich API-Dokumentation und Sichtbarkeits-Ergänzung. Verwenden, wenn fehlende `public`-Modifier gezielt für Consumer-relevante API-Mitglieder ergänzt werden sollen, ohne bestehende Sichtbarkeiten zu verschärfen oder herabzustufen, und wenn deutschsprachige JSDoc-Kommentare mit konsistenter Ubiquitous Language erstellt oder vereinheitlicht werden sollen.
---

# Angular API/JSDoc (DE)

Überarbeite übergebene Angular-/TypeScript-Dateien so, dass Sichtbarkeit, API-Fläche und JSDoc konsistent sind, ohne Verhaltensänderung.

## Eingabe

Erwarte vom Aufrufer mindestens:

- Liste der zu bearbeitenden Komponenten-/Klassendateien und/oder Ziel-Ordner.

Nutze kein hartcodiertes Glossar im Skill.
- Bei Ordnern: rekursiv alle relevanten `*.ts`-Dateien unterhalb des angegebenen Ordners verarbeiten (mit Fokus auf Angular-Komponenten und zugehörige Klassen).

## Glossar-Quelle (verpflichtend)

1. Lies im Ziel-Repository die Datei `AGENTS.md`.
2. Suche dort den Abschnitt zur Ubiquitous Language bzw. den konfigurierten Glossar-Pfad.
3. Lade genau diese Glossar-Datei aus dem Ziel-Repository als Single Source of Truth.
4. Wenn in `AGENTS.md` kein Glossar-Pfad hinterlegt ist, frage nach dem gewünschten Ablageort und schlage als Default `docs/GLOSSAR.md` vor.
5. Wenn der Ablageort bestätigt ist, lege das Glossar bei Bedarf an und pflege anschließend `AGENTS.md` mit dem finalen Pfad.

## Unklare Begriffe (verpflichtend klären)

1. Erkenne unklare, neue oder mehrdeutige Fachbegriffe in den Ziel-Dateien.
2. Frage diese Begriffe vor Abschluss aktiv nach (kurz und konkret).
3. Kläre pro Begriff:
- bevorzugten Zielbegriff,
- Einordnung,
- kurze Bedeutung,
- zu vermeidende Synonyme.
4. Nutze bis zur Klärung neutrale Formulierungen oder markiere offene Stellen.
5. Sobald die Begriffe geklärt sind, pflege sie direkt im Repo-Glossar.
6. Pflege Begriffe im bestehenden Glossar-Stil des Repositories, inklusive Spalte `Zu vermeidende Synonyme`.

## Workflow

1. Ermittle die Ziel-Dateien aus den übergebenen Dateien/Ordnern und analysiere jede Klasse in bestehender Reihenfolge der Member (nicht umsortieren).
2. Identifiziere Member, die Teil der Consumer-API sind (z. B. Inputs/Outputs, bewusst von außen nutzbare Methoden/Properties).
3. Ergänze fehlende Sichtbarkeit ausschließlich in Richtung `public`, ohne die Reihenfolge der Deklarationen zu ändern.
4. Erstelle oder überarbeite Klassen-JSDoc auf Deutsch (mit korrekten Umlauten (`ä`, `ö`, `ü`, `Ä`, `Ö`, `Ü`) und `ß`): kurz und knapp erklären, was die Klasse im fachlichen/technischen Kontext tut, und bei Decorator-Klassen direkt über dem Decorator platzieren.
5. Erstelle oder überarbeite JSDoc für API-relevante `public`-Member auf Deutsch (mit korrekten Umlauten (`ä`, `ö`, `ü`, `Ä`, `Ö`, `Ü`) und `ß`).
6. Nutze bei Querverweisen `{@link ...}` auf verwandte Felder, Typen oder Klassen.
7. Gleiche Formulierungen und Fachbegriffe gegen das Repo-Glossar aus.
8. Erweitere das Repo-Glossar um neu geklärte Begriffe.
9. Vermeide in Kommentaren und JSDoc gezielt die im Glossar gelisteten Synonyme aus `Zu vermeidende Synonyme`.

## Sichtbarkeitsregeln

- Verwende `public` nur für echte Consumer-API.
- Ändere Sichtbarkeit nur durch Ergänzung von fehlendem `public`.
- Nimm keine Downgrades oder Umschaltungen vor (kein `public -> protected/private`, kein `protected <-> private`).
- Belasse bestehendes API-Verhalten; ändere keine Namen oder Signaturen ohne expliziten Auftrag.
- Ändere keine Member-Reihenfolge, außer es ist technisch zwingend.

## JSDoc-Regeln (Deutsch)

- Schreibe Kommentare in klarer deutscher Sprache.
- Ergänze für jede bearbeitete Klasse eine kurze Klassen-JSDoc mit der Kontextrolle der Klasse (was sie im Gesamtkontext tut).
- Halte Klassen-JSDoc kurz und knapp (1-2 Sätze).
- Platziere Klassen-JSDoc bei dekorierten Klassen immer direkt über dem Klassen-Decorator (z. B. über `@Component`).
- Erlaube englische Fachbegriffe nur, wenn sie im Repo-Glossar etabliert sind, oder sich auf Symbole bezogen wird.
- Beschreibe Zweck und Wirkung präzise statt Implementierungsdetails.
- Dokumentiere `public`-API vollständig und konsistent.
- Nutze `{@link TypOderMember}` für relevante Querverweise.
- Nutze keine Begriffe aus der Glossar-Spalte `Zu vermeidende Synonyme`.
- Ergänze bei Bedarf ein minimales Code-Beispiel für Komponenten, das deutsche Fachlichkeit zeigt (Domänensprache auf Deutsch), während technische Bestandteile wie Angular-/TypeScript-Symbole natürlich technisch benannt bleiben.

## Qualitätskriterien

- Keine Verhaltensänderung.
- Öffentliche API bewusst klein und klar.
- Konsistente Terminologie gemäß Repo-Glossar.
- Keine Nutzung verbotener Synonyme aus dem Glossar in neuem oder geändertem Text.
- Ergebnis diff-freundlich: minimale, zielgerichtete Anpassungen.

## Ausgabeformat

Liefere:

- geänderte Dateien,
- kurze Begründung der `public`-Ergänzungen (und explizite Notiz, dass keine Sichtbarkeits-Downgrades vorgenommen wurden),
- kurze Notiz mit dem verwendeten Glossar-Pfad aus `AGENTS.md` (oder dem neu vereinbarten Ablageort),
- kurze Liste der aktiv geklärten Begriffe und ihrer vermiedenen Synonyme,
- Hinweis auf offene Grenzfälle (falls unklar zwischen `public` und `protected`).
