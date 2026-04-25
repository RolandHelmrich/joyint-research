# Joyint Research

Recherche-Projekt zur Gruendung der Joyint GmbH (50/50 mit Mitgruender,
Roland als CEO) und zum Joint Venture "Werklust".

## Quellen

- PDFs in `refs/` (WhitePaper, Competition, Werklust-Workshop-Vorbereitung)
- Joyint GitHub Org: https://github.com/joyint
- Projekt-Docs: https://github.com/joyint/project/tree/main/docs
- Web-Recherche (EU AI Act, Markt, Wettbewerber)

## Output-Konventionen

- Ergebnisse nach `research/<thema>/` schreiben
- Ein Markdown-File pro Unterthema, z.B. `research/01-eu-ai-act/grundlagen.md`
- Dateinamen: Kleinbuchstaben, Bindestriche, keine Leerzeichen
- Jedes File beginnt mit YAML-Frontmatter:

  ```yaml
  ---
  status: backlog | in-progress | done | blocked
  updated: YYYY-MM-DD
  ---
  ```

- Zentrale Statusuebersicht in `research/STATUS.md` aktuell halten

## Git

- Alle Git-Aktionen fuehrt der User manuell aus
- Claude liefert Copy-Paste-Befehle und Commit-Messages
- Konventionelle Commits: docs:, research:, chore:
- Remote: https://github.com/RolandHelmrich/joyint-research

## Recherche-Regeln

- Inline-Attribution: "Laut [Quelle, Datum](URL) ..."
- Primaerquellen vor Aggregatoren
- Bei volatilen Inhalten (Gesetze, Preise): Stand/Datum nennen
- Fakt, Interpretation und Spekulation klar trennen
