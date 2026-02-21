---
name: skill-upskiller
description: Verbessert einen bestehenden Codex-Skill strukturell und deterministisch, mit optionalem Evidenzmodus ueber lokale Codex-Session-Logs.
---

# Skill Upskiller

Verbessere einen vorhandenen Skill reproduzierbar und deterministisch. Standard ist Strukturarbeit; Evidenzanalyse ist optional.

## Zweck

- Skills strukturell vereinheitlichen.
- Mehrdeutigkeit reduzieren.
- Outputs und Ablauf deterministisch machen.

## Wann nutzen

- Der Nutzer will einen vorhandenen Skill verbessern oder upskillen.
- Es gibt eine konkrete Skill-Path-Angabe (z. B. `.codex/skills/<skill-name>`).
- Der Nutzer erwartet eine vollstaendige Neufassung der Skill-Datei.

## Wann nicht nutzen

- Es soll ein komplett neuer Skill ohne vorhandene Ausgangsdatei erstellt werden.
- Es geht nur um eine kleine Textkorrektur.

## Eingaben

Erwarte mindestens:

1. `SKILL_PATH` (Ordner oder direkte `SKILL.md`)
2. `MODE`:
- `structure-only` (Default)
- `evidence-based` (optional)

Optional:

1. Gewuenschte Schwerpunkte (z. B. Inputs/Outputs, Safety, Verification)
2. Formatvorgaben fuer den finalen Bericht

## Datenschutz und Sicherheit

- Keine Secrets oder sensiblen Rohdaten ausgeben.
- Keine Evidenz erfinden.
- Wenn `MODE=evidence-based`: Logs nur paraphrasiert und minimal referenzieren.

## Vorgehen

1. Zielskill laden:
- Vollstaendige `SKILL.md` lesen.
- Aktuelle Struktur und Luecken erfassen.

2. Struktur-Zielbild festlegen:
- Der neue Skill MUSS folgende Sektionen enthalten:
  1. Purpose
  2. When to use
  3. When not to use
  4. Inputs
  5. Outputs
  6. Procedure
  7. Edge Cases and Safety Checks
  8. Repo-Specific Conventions (falls zutreffend)
  9. Verification

3. Deterministische Schaerfung:
- Vage Formulierungen durch klare Regeln ersetzen.
- Entscheidungs- und Stop-Bedingungen explizit machen.
- Output-Format verbindlich machen.
- Reihenfolgen und Prioritaeten festlegen.

4. Optionaler Evidenzmodus (`MODE=evidence-based`):
- `CODEX_HOME` ermitteln (`$CODEX_HOME` oder `~/.codex`).
- `rollout-*.jsonl` unter `$CODEX_HOME/sessions` auswerten.
- Nur belegte Muster uebernehmen.
- Bei fehlenden Logs: transparent markieren und auf Repo-Evidenz wechseln.

5. Vollstaendige Neufassung schreiben:
- Gesamte `SKILL.md` ersetzen, kein Teil-Patch-Stil.
- Ursprungsintention beibehalten, aber Struktur haerten.

## Verifikationsregeln

- Endversion enthaelt alle Pflichtsektionen.
- Keine widerspruechlichen Regeln.
- Inputs/Outputs/Procedure sind konkret genug fuer wiederholbare Ausfuehrung.
- Bei Evidenzmodus: keine erfundenen Sessions oder Zitate.

## Ausgabeformat

Bei `MODE=structure-only`:

1. `## Structural Summary`
2. `## Updated SKILL FILE (full content)`
3. `## Change Log`
4. `## Added Files (if any)`

Bei `MODE=evidence-based`:

1. `## Evidence Summary`
2. `## Updated SKILL FILE (full content)`
3. `## Change Log`
4. `## Added Files (if any)`
