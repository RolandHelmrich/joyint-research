---
status: done
updated: 2026-04-26
---

# Joyint: Offline-Datenspeicherung

Quellen: `research/02-joyint-product/architecture.md`, github.com/joyint/joy README (Stand 2026-04-26).

## Kernprinzip: Git ist die Datenbank

Joyint speichert alle Projektdaten als YAML-Dateien in einem `.joy/`-Verzeichnis innerhalb des Git-Repositories. Es gibt keinen separaten Datenbankserver. Die Versionshistorie der Projektdaten ist identisch mit der Code-History.

## .joy/-Verzeichnisstruktur

```
.joy/
├── config.yaml          # Tool-Konfiguration (remote, encryption-settings)
├── credentials.yaml     # Tokens, Keys — gitignored
├── project.yaml         # Mitglieder, Capabilities, Gates-Konfiguration
├── items/               # Ein YAML-File pro Item (Epic, Story, Task, Bug…)
├── milestones/          # Milestone-Definitionen
├── ai/                  # AI-Job-Cache — gitignored
├── jobs/                # AI-Job-Tracking — versioniert
└── logs/                # Audit Trail, append-only, kryptografisch signiert — versioniert
```

`credentials.yaml` und `ai/` sind gitignored: sensible Daten bleiben lokal, der Rest ist versioniert.

## Offline-Betrieb

Joy und Jyn laufen **vollständig offline** — kein Server, kein Internet erforderlich.

- Alle Lese- und Schreiboperationen laufen direkt auf dem Dateisystem
- Guard (Governance-Validierung) läuft lokal als Teil des Single Binary
- AI-Features erfordern eine LLM-API-Verbindung — PM-Kernfunktionen nicht
- CalDAV-Sync (Jyn) erfordert Netzwerkzugang zu Apple/Google, nicht zu joyint.com

## Online-Sync

Synchronisation funktioniert über **Standard-Git-Operationen**:

```sh
git push   # Änderungen hochladen
git pull   # Änderungen abrufen
```

joyint.com ist kein klassisches SaaS-Backend, sondern ein **Git-Gateway**:

- CLI-Nutzer brauchen joyint.com nicht — sie können jeden beliebigen Git-Remote nutzen
- WebUI- und CalDAV-Nutzer gehen über einen gRPC-Service, der serverseitig joy-core auf Bare-Git-Repos aufruft
- Auf joyint.com liegt **keine Anwendungsdatenbank für Nutzdaten** — nur operativer Zustand: Sessions, Job-Queue, Notifications, Billing

## BYOG (Bring Your Own Git)

Nutzer wählen beim Onboarding:

| Option | Datenlage | joyint.com-Rolle |
|---|---|---|
| joyint.com Hosting | Git-Repo bei joyint.com | Host + Service |
| GitHub / GitLab / Gitea | Eigenes Git-Konto | Reiner Service-Layer |

BYOG kostet +2 EUR/Monat (außer Enterprise). Ergebnis: Joyint sieht die Rohdaten der Nutzer nicht.

## E2E-Verschlüsselung

Wenn Cloud-Sync aktiv:

- Verschlüsselt: Titel, Beschreibung, Kommentare (AES-256-GCM, Schlüssel liegt auf dem Client)
- Cleartext: ID, Status, Priorität, Fälligkeitsdatum (nötig für Notifications und CalDAV-Scheduling)

Lokal (offline): keine Verschlüsselung — Plaintext-YAML auf dem eigenen Gerät.

## Bewertung für die Mitgründer-Entscheidung

| Aspekt | Einschätzung |
|---|---|
| Technische Solidität | Hoch — kein proprietäres Dateiformat, kein Vendor-Lock-in |
| Vertrauensargument | Stark — "Wir wollen eure Daten nicht mal haben" (BYOG) |
| Betriebskosten | Extrem niedrig — kein DB-Server, Git ist Infrastruktur |
| Komplexität für Nutzer | Gering — `git push/pull` als bekannte Primitive |
| Offline-Garantie | Vollständig für PM-Kern; AI-Features brauchen LLM-API |
