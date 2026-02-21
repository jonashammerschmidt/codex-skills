---
name: angular-thin-component-refactor
description: Refaktoriert Angular- und TypeScript-Komponenten in das Muster Thin Component plus ausgelagerte Feature- und Logic-Klassen, ohne Verhaltensänderung. Verwenden, wenn eine konkrete Komponente in klar getrennte Orchestrator-Komponente und plain TypeScript-Logikklassen umgebaut werden soll.
---

# Angular Thin-Component Refactor

## Purpose

Refaktoriere eine bestehende Angular-Komponente in das Muster `Thin Component + ausgelagerte Logic-Klassen`, ohne das Laufzeitverhalten oder die öffentliche API unerwartet zu ändern.

## When to use

Nutze diesen Skill, wenn mindestens eine Bedingung erfüllt ist:
1. Eine konkrete Komponente ist fachlich überladen und soll als Orchestrator verschlankt werden.
2. Fachlogik soll in plain TypeScript-Klassen ausgelagert werden.
3. Die bestehende API (Inputs, Outputs, öffentliche Handler) soll stabil bleiben.
4. Der Nutzer verlangt explizit Thin-Component-Refactoring.

## When not to use

Nutze diesen Skill nicht, wenn:
1. Ein vollständiges Redesign oder fachliche Verhaltensänderung gefordert ist.
2. Keine konkrete Zielkomponente benannt oder ableitbar ist.
3. Nur eine minimale lokale Korrektur ohne strukturelles Refactoring gewünscht ist.
4. Eine globale Architektur-Migration über mehrere Domänen ohne klaren Scope verlangt wird.

## Inputs

Erwarte vom Aufrufer:
1. `TARGET_COMPONENT`: Pfad zur Komponente (`.ts`, optional Template/Styles im Umfeld).
2. Optional `SCOPE_HINT`: Grenzen der Refaktorierung (z. B. nur eine Datei, nur bestimmte Verantwortungen).
3. Optional `BEHAVIOR_CONSTRAINTS`: explizite No-Go-Änderungen.

Eingaberegeln:
1. Wenn nur ein Ordner genannt ist, bestimme die primäre Zielkomponente eindeutig; sonst stoppen und Rückfrage stellen.
2. Ändere nur Dateien im direkten Feature-Kontext der Zielkomponente.
3. Keine stillen Scope-Erweiterungen auf weitere Features.

## Outputs

Liefere immer:
1. Geänderte Komponentendatei(en) als Thin-Component-Orchestrator.
2. Neue oder angepasste Logic-Klasse(n) nahe der Komponente, bevorzugt unter `./logic/`.
3. Kurze Begründung der Verantwortungsaufteilung.
4. Explizite Validierung, dass Verhalten und öffentliche API erhalten wurden.
5. Liste offener Risiken oder nicht auflösbarer Grenzfälle (falls vorhanden).

## Procedure

1. **Scope fixieren**
- Identifiziere exakt eine Zielkomponente und ihre direkten Begleitdateien.
- Stoppe bei mehrdeutigem Scope und fordere Klärung an.

2. **Verantwortungen schneiden**
- Markiere Angular-Orchestrierung vs. Fachlogik.
- Behalte in der Komponente: Angular-Metadaten, `inject()`, `input()`, `output()`, `viewChild`/`viewChildren`, template-nahe `computed()`, öffentliche Event-Handler.

3. **Logic-Struktur festlegen**
- Erzeuge oder erweitere plain TypeScript-Klassen im Feature-Kontext (`./logic/` bevorzugt).
- Eine Klasse = eine klar abgegrenzte Verantwortung.
- Keine Angular-Decorator in Logic-Klassen.

4. **Abhängigkeiten explizit übergeben**
- Übergebe nur notwendige Signals, Services, Callbacks, `ElementRef` und Utilities per Konstruktor.
- Keine versteckten globalen Abhängigkeiten.
- Falls `effect()` in Logic nötig ist: Initialisierung aus der Komponente (z. B. via `runInInjectionContext` und `Injector`).

5. **Delegation implementieren**
- Halte öffentliche Handler in der Komponente stabil und delegiere intern in Logic.
- Exponiere in Logic nur kleine, testbare APIs (`initialize`, `setup`, `toggle`, etc.).
- Vermeide Template-Logikaufblähung.

6. **Repo-Konventionen absichern**
- Signals-first arbeiten.
- `ChangeDetectionStrategy.OnPush` beibehalten/einhalten.
- Kein `@HostBinding` oder `@HostListener`.
- Domänenterminologie gemäß `docs/GLOSSAR.md` konsistent halten.

7. **Abschlussprüfung durchführen**
- Prüfe alle Punkte aus `Verification`.
- Wenn Verhaltenserhalt nicht sicher belegbar ist, transparent markieren statt behaupten.

## Edge Cases and Safety Checks

1. **Mehrdeutiger Komponenten-Scope**
- Nicht raten; stoppen und gezielte Rückfrage stellen.

2. **Starke Seiteneffekte in bestehender Logik**
- Reihenfolge und Triggerpunkte unverändert lassen.
- Bei Unsicherheit konservativ delegieren und Risiko dokumentieren.

3. **Tight Coupling mit Template**
- Template-nahe `computed()` in der Komponente belassen.
- Nur reine Fachtransformationen auslagern.

4. **API-Risiko durch Refactor**
- Keine unbeauftragte Umbenennung öffentlicher Member.
- Keine Signaturänderungen ohne expliziten Auftrag.

5. **Fehlende sichere Verifikation**
- Keine unbelegte Gleichheitsbehauptung.
- Explizit angeben, was nur statisch geprüft wurde.

## Repo-Specific Conventions

1. Bearbeite den produktiven Code unter `frontend/projects`.
2. Wiederverwendbare Library-Änderungen liegen unter `frontend/projects/fst/common/src/lib`.
3. Öffentliche Exporte bei Bedarf in `frontend/projects/fst/common/src/public-api.ts` synchron halten.
4. Für nachvollziehbare manuelle Checks Demo-Anpassungen in `frontend/projects/fst-common-demo` berücksichtigen, wenn vom Refactor betroffen.
5. Verwende Terminologie aus `docs/GLOSSAR.md` als Single Source of Truth.
6. Führe keine Tests aus, außer der Nutzer fordert dies explizit an.

## Verification

Vor Abschluss müssen alle Punkte erfüllt oder als offen markiert sein:
1. Die Komponente ist sichtbar dünner und primär Orchestrator.
2. Ausgelagerte Logic enthält keine Angular-Decorator.
3. Öffentliche API der Komponente blieb stabil (Namen, Signaturen, Bindings).
4. Verhalten wurde nicht absichtlich verändert; kritische Flows wurden statisch gegengeprüft.
5. Abhängigkeiten sind explizit und minimal übergeben; keine versteckten Globals.
6. Angular-Konventionen sind eingehalten (`OnPush`, signals-first, keine Host-Decorator).
7. Änderungen sind auf den definierten Scope begrenzt.
