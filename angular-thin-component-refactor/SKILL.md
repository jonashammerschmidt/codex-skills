---
name: angular-thin-component-refactor
description: Refaktoriert Angular- und TypeScript-Komponenten in das Muster Thin Component plus ausgelagerte Feature- und Logic-Klassen, ohne Verhaltensänderung. Verwenden, wenn eine konkrete Komponente in klar getrennte Orchestrator-Komponente und plain TypeScript-Logikklassen umgebaut werden soll.
---

# Angular Thin-Component Refactor

Refaktoriere eine übergebene Angular-Komponente in das Muster `Thin Component + ausgelagerte Feature/Logic-Klassen`.

## Workflow

1. Analysiere die Komponente und markiere Verantwortungen.
2. Trenne orchestrierende Angular-Aufgaben von Fachlogik.
3. Erzeuge oder erweitere plain TypeScript-Logikklassen nahe der Komponente, bevorzugt unter `./logic/`.
4. Delegiere aus der Komponente in diese Klassen, ohne die öffentliche API der Komponente unerwartet zu ändern.
5. Prüfe Verhalten, Lesbarkeit, Benennung und Architektur gegen die Regeln unten.

## Refactoring-Regeln

### 1. Halte die Komponente als Orchestrator

- Belasse Angular-Metadaten, `inject()`, `input()`, `output()`, `viewChild`/`viewChildren` in der Komponente.
- Belasse Template-nahe `computed()` Werte in der Komponente.
- Belasse öffentliche Event-Handler in der Komponente und delegiere intern an Logic-Klassen.

### 2. Lagere Fachlogik in plain TypeScript-Klassen aus

- Verwende in Logic-Klassen keine Angular-Decorator.
- Platziere Logic-Klassen nah an der Komponente unter `./logic/` oder einem bestehenden Feature-Unterordner.
- Gib jeder Klasse genau eine klar abgegrenzte Verantwortung.

### 3. Übergib nur notwendige Abhängigkeiten

- Übergib nur benötigte Signals, Services, Callbacks, `ElementRef` oder Utility-Abhängigkeiten per Konstruktor.
- Verwende keine versteckten globalen Abhängigkeiten.
- Wenn `effect()` in Logic-Klassen nötig ist, initialisiere das aus der Komponente heraus, z. B. mit `runInInjectionContext` und übergebenem `Injector`.

### 4. Halte Logic-APIs klein und testbar

- Exponiere nur relevante readonly Signals/Computeds und klar benannte Methoden wie `setup`, `initialize`, `toggle`, `goUp`.
- Halte Methoden klein, deterministisch und gut unit-testbar.

### 5. Halte Angular-Stil konsistent

- Arbeite signals-first.
- Nutze `ChangeDetectionStrategy.OnPush`.
- Nutze keine `@HostBinding`/`@HostListener`.
- Vermeide Logikaufblähung im Template.

### 6. Sichere Ergebnisqualität

- Verändere Verhalten nicht.
- Verbessere Lesbarkeit der Komponente sichtbar.
- Verwende konsistente Benennung entsprechend bestehender Muster wie `Selection`, `Focus`, `Sort`, `ActiveDescendant`.

## Ergebnisformat

Liefere die Refaktorierung mit:

- den geänderten Komponentendateien,
- den neuen oder geänderten Logic-Klassen,
- einer kurzen Begründung der Aufteilung,
- einer kurzen Validierung, dass das Verhalten erhalten bleibt.
