---
status: done
updated: 2026-04-25
---

# Joyint: Technische Architektur

Quellen: Cargo.toml, CONTRIBUTING.md, `docs/biz/BusinessModel.md`, `docs/dev/vision/README.md` — joyint/joy, joyint/jyn, joyint/jon + internes project-Repo, Stand 2026-04-25.

## Kernprinzipien

**Git-nativ.** Alle Projektdaten liegen in `.joy/` als YAML-Dateien im Repository. Kein Datenbank-Server. Versionshistorie identisch mit Code-History.

**Single Binary.** Keine Runtime-Dependencies. Installation per `curl get.joyint.com/joy | sh` oder `cargo install joy-cli`. Zielgröße: unter 200ms CLI-Antwortzeit.

**Offline-first.** Joy und Jyn funktionieren vollständig ohne Server. joyint.com ist optional.

## Datenmodell

```
.joy/
├── config.yaml
├── credentials.yaml   (gitignored)
├── project.yaml       (Mitglieder, Capabilities, Gates)
├── items/             (ein YAML-File pro Item)
├── milestones/
├── ai/                (gitignored)
├── jobs/              (versioniert — AI-Job-Tracking)
└── logs/              (versioniert, append-only — Audit Trail)
```

Item-Typen: epic, story, task, bug, rework, decision, idea.
Status-Workflow: `new → open → in-progress → review → closed`, mit `deferred` als Seitenausgang.

Jyn erweitert das Basis-Item via `serde(flatten)` um Recurring-Logik (RRULE, RFC 5545). Jot-Items sind gültige Joy-Items mit Zusatzfeldern — volle Rückwärtskompatibilität.

## Technologie-Stack

**Sprache:** Rust 2021 Edition, alle Repos.
**Joy-Dependencies:** tokio 1.43, serde + serde_yaml_ng, clap 4.5, chrono 0.4, thiserror 2.0, anyhow 1.0, minijinja 2.18.
**Shared Core:** Jyn bindet `joy-core = "0.11.1"` — gemeinsame Datenschicht, zero Jyn-spezifischer Code in joy-core.
**Jon:** minimale Dependencies (clap, anyhow), kein LLM-Framework im aktuellen MVP.
**Platform/Server:** gRPC (protobuf als API-Vertrag), gitoxide (pure-Rust Git) für serverseitige Git-Operationen.
**Frontend:** React 19 / Next.js 15, Tailwind CSS v4, Tauri 2.x für native Apps.

## Workspace-Struktur (joy)

```
joy/
├── crates/
│   ├── joy-core/    (Datenmodell, YAML-I/O, Guard, Git-Integration)
│   ├── joy-cli/     (CLI-Interface, 10 Kernkommandos)
│   └── joy-ai/      (AI-Dispatch, Job-Tracking, Cost-Logging)
└── Cargo.toml       (workspace)
```

## Governance-Architektur (5 Säulen)

Guard ist in joy-core eingebettet und fängt alle Schreiboperationen ab. Bei Solo-Setup ohne Gates: Passthrough ohne Overhead. Bei konfigurierten Gates: vollständige Validierung.

| Säule | Funktion |
|---|---|
| Trustship | Identität (Ed25519-Keys), Capabilities, Delegation Tokens für AI-Agenten |
| Guardianship | Laufzeit-Validierung jeder Schreiboperation gegen Trust Model |
| Orchestration | Job-Erstellung, Dispatch, 5 Collaboration Modes (autonomous → pairing) |
| Traceability | Append-only Event Log in `.joy/logs/`, kryptografisch signiert (Judge als unabhängiges Binary) |
| Settlement | Token- und Kostenerfassung pro AI-Job, Budget-Limits (`max_cost_per_job`) |

## Server-Architektur: Git als Backend

joyint.com hat keine Anwendungsdatenbank für Geschäftsdaten. Der Server ist ein Gateway zu Git:

- CLI-Nutzer syncen per `git push/pull` — kein Server nötig
- WebUI/CalDAV-Nutzer gehen über gRPC-Service, der joy-core auf serverseitigen Git-Repos aufruft
- Für serverseitige Git-Ops: gitoxide mit einem Writer-Task pro Bare Repository (tokio::mpsc-Channel eliminiert konkurrierende Schreibkonflikte ohne File-Locking)

Nur operativer Zustand in DB: Sessions, Job-Queue, Notifications, Billing. Massiv niedrigere Betriebskosten als klassisches SaaS.

## CalDAV als Mobile-Bridge (Jyn)

Statt einer eigenen iOS-App betreibt joyint.com einen CalDAV-Server. Apple Reminders, Google Calendar, Thunderbird funktionieren als Jyn-Frontend — inkl. Siri, Apple Watch, Widgets. Kein App Store, keine 30%-Gebühr. VTODO deckt alle Jyn-Felder ab (Title, Due Date, Priority, Recurring via RRULE, Tags).

Einschränkung: verschachtelte Projekte nur in der WebUI — CalDAV-Clients unterstützen RELATED-TO inkonsistent.

## Bring Your Own Git (BYOG)

Nutzer wählen beim Anmelden, wo Daten liegen:
1. joyint.com — Git-Hosting inklusive, immer E2E-verschlüsselt
2. GitHub / GitLab / Gitea — Daten im eigenen Git-Account, joyint.com ist reiner Service-Layer

BYOG als +2 EUR/Monat Add-on (außer Enterprise, dort inklusive). Senkt Vertrauenshürde: "Wir wollen eure Daten nicht mal haben."

## E2E-Verschlüsselung

AES-256-GCM auf joyint.com. Schlüssel bleibt auf dem Client-Device.

- Verschlüsselt: Titel, Beschreibung, Kommentare (Item-Inhalte)
- Cleartext-Metadaten: ID, Status, Priorität, Fälligkeitsdatum — nötig für Notifications und CalDAV-Scheduling
- CLI: entschlüsselt lokal
- WebUI: entschlüsselt clientseitig via Web Crypto API
- CalDAV: explizites Opt-in des Nutzers nötig (`jyn key share`)

## Testing-Strategie

TDD als Default, Coverage-Ziel >80% auf Core-Libraries.

```sh
just test-unit     # 270 lib tests (Stand 2026-04-25)
just test-cmd      # Snapshot-Tests (trycmd)
just test-int      # 184 Integration-Tests (bats)
```

## Distribution

- Binaries via Cargo-Dist (Linux, macOS, Windows; x86_64 + aarch64)
- Homebrew: `brew install joydev/tap/joyint`
- crates.io: `joyint-cli` (joy), `jyn-cli` (jyn)
- Installations-Script: `get.joyint.com/{joy|jyn|jon}` oder `get.joyint.com/all`
