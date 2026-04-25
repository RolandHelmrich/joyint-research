---
status: done
updated: 2026-04-25
---

# Joyint: Produktüberblick

Quellen: GitHub-Org joyint (public repos + internes project-Repo), `docs/biz/BusinessModel.md`, `docs/biz/JonStrategy.md`, `docs/dev/vision/README.md` — Stand 2026-04-25.

## Was ist Joyint?

Joyint ist ein Ökosystem aus CLI-Tools für Software-Entwicklungsteams. Kernidee: Projektmanagement-Daten liegen als YAML-Dateien direkt im Git-Repository — keine externe Datenbank, kein Cloud-Zwang, offline nutzbar. AI-Agenten werden nach demselben Governance-Modell gesteuert wie menschliche Teammitglieder.

Zentrale Differenzierung (laut BusinessModel.md): Joy ist das erste PM-Tool, das AI-Governance ins Datenmodell eingebaut hat — nicht nachträglich aufgesetzt. Kein bestehendes Tool beantwortet die Fragen: Welche AI hat was entschieden? Wer hat es freigegeben? Was hat es gekostet?

## Die Produkte (extern: zwei, intern: drei)

**Joy** — PM- und Governance-Layer. Backlogs, Milestones, Dependencies, Status-Workflow mit konfigurierbaren Gates, AI-Orchestrierung (Dispatch, Cost-Tracking, Budget-Limits), Audit Trail. Kern des Ökosystems. MIT-lizenziert, aktiv in Entwicklung, Dogfooding seit v0.5.0.

**Jyn** — Task-Dispatch-Layer und persönlicher Task-Manager. Verteilt Joy-Aufgaben per CalDAV an Apple Reminders oder Google Calendar (Menschen) oder per CLI/API an AI-Agenten. Eigenständig nutzbar als Todo-Tool. MIT-lizenziert, Pre-Development v0.6.2.

**Jon — intern eine Funktion, extern kein eigenständiges Produkt.** Laut `docs/biz/JonStrategy.md`: keine eigene Landing Page, kein eigenes Branding, keine eigene Preisseite. Extern lautet die Positionierung: *"Joy for planning. Jyn for tasks. Both understand natural language."* In Investoren-Materialien und technischer Dokumentation bleibt das Trio (Joy/Jyn/Jon) bestehen — nach außen tritt nur das Duo auf. Jon ist architektonisch ein dünner Subprocess-Layer ohne eigene Datenschicht.

## Die zwei-Produkt-Strategie: gegenseitige Verstärkung

Joy und Jyn verstärken sich in beide Richtungen (BusinessModel.md):

**Bottom-up (Jyn als Einstieg):** Entwickler entdeckt Jyn als lokales Todo-Tool → will Sync → joyint.com → braucht PM → entdeckt Joy → Team wächst → Teams/Enterprise-Tier.

**Top-down (Joy verbreitet Jyn):** Ein Joy-Team führt Joy ein → Status-Gates und AI-Dispatch erzeugen automatisch Jyn-Tasks für alle Beteiligten (Designer, QA, Stakeholder, AI) → jeder wird Jyn-Nutzer ohne PM-Bedarf. Ein Joy-Enterprise-Kunde mit 100 Usern erzeugt potenziell 100 Jyn-Pro-Lizenzen.

## Schwer kopierbare Vorteile

Laut BusinessModel.md sind diese sechs Punkte architekturbedingt nicht nachträglich auf bestehende Produkte aufzupfropfen:

1. Git-natives Datenformat
2. AI-Governance by Design (Gates, AI-Identität, Audit-Log, Cost-Tracking ins Datenmodell eingebaut)
3. E2E-Verschlüsselung — immer aktiv, kein Wettbewerber bietet das
4. Bring Your Own Git (BYOG) — senkt Vertrauenshürde radikal
5. CLI-first — natürlicher Kontrollpunkt für AI-gesteuerte Entwicklung
6. Niedrige Betriebskosten durch Git als Backend (keine Datenbank, kein Custom-Sync)

## Wettbewerbskontext

AI im PM ist seit 2025 kein unbesetztes Feld mehr. Linear hat seit Mai 2025 AI als First-Class Workspace Members (15+ integrierte Tools, Sessions, MCP-Server). Atlassian hat Rovo (nachträglich auf Jira aufgesetzt). Beide fehlt: Cost-Tracking, Budget-Limits, konfigurierbare Status-Gates. Das Sub-Feld "AI-Governance mit Audit-Trail" ist laut BusinessModel.md noch unbesetzt.

## Vollständiges Ökosystem

| Repo | Zweck | Lizenz | Sichtbar |
|---|---|---|---|
| joy | PM-CLI, AI-Governance, Kern | MIT | öffentlich |
| jyn | Todo-CLI, CalDAV, Dispatch | MIT | öffentlich |
| jon | NLP-Interface (Subprocess-Layer) | MIT | öffentlich |
| platform | joyint.com Server, CalDAV, Dispatch | Kommerziell | privat |
| app | Tauri-Apps (Desktop, Mobile, Web) | Kommerziell | privat |
| judge | Unabhängiger Audit-Layer | MIT | privat |
| crypt | E2E-Verschlüsselung, Key Management | MIT | privat |
| joyc | IOTA Settlement Layer | Kommerziell | privat |
| project | Internes Planungs-Repo | Privat | privat |

## Namens-Diskrepanz: Jot → Jyn

Das Whitepaper (April 2026) verwendet durchgehend den Namen **"Jot"**. Das Produkt heißt seit 19. April 2026 **"Jyn"** (umbrella-Entscheidung JI-00E3-C5). Das Whitepaper ist in diesem Punkt veraltet — die internen Docs (`BusinessModel.md`) verwenden bereits Jyn.

## Lead-Entwickler

Horst Schwarz (@joydev-horst, Joydev GmbH) — nahezu alle Commits, co-autorisiert von `ai:claude@joy`. Vermutlich der Mitgründer.
