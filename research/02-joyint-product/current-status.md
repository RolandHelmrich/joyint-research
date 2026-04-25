---
status: done
updated: 2026-04-25
---

# Joyint: Aktueller Entwicklungsstand

Quellen: GitHub Commits API, `docs/biz/BusinessModel.md`, `docs/biz/JonStrategy.md` — Stand 2026-04-25.

## Entwicklungstempo

Joy: 3–5 Commits pro Tag, letzter Push heute (2026-04-25). Sehr aktive Entwicklung, ein Entwickler (Horst Schwarz) + AI-Co-Authoring.
Jyn: letzte Aktivität 2026-04-20, Stabilisierungs-Releases.
Jon: letzte Aktivität 2026-04-19, Grundarchitektur im Aufbau.

## Joy (v0.8.x, aktiv)

**Was funktioniert:** Alle 10 Kernkommandos. AI Tool Mode (Claude Code, GitHub Copilot, Cursor als externe Tools). AI Agent Mode mit Job-Tracking und Cost-Logging. Shell-Completions (bash, zsh, fish). Event Log (Audit Trail). Tutorial. OAuth-Auth und Sync (`joy sync`, `joy clone`). Dogfooding seit v0.5.0.

**Heute in Arbeit:** Auth-Schema-Rename (ADR-035). Completion-Fixes für bash und case-insensitive member matching.

**Tests:** 270 lib tests, 184 bats-Integration-Tests — beide grün laut letztem Commit.

## Jyn (v0.6.2, Pre-Development)

**Was existiert:** Datenmodell (erbt joy-core 0.11.1). Grundlegende CLI-Struktur. Cargo-Dist für Multi-Platform-Binaries.

**Was noch fehlt:** CalDAV-Sync, wiederkehrende Aufgaben, vollständige Dispatch-Integration mit Joy.

**Namens-History:** Bis 2026-04-19 unter dem Namen "Jot" geführt. Umbenannt auf "Jyn" (umbrella-Entscheidung JI-00E3-C5). Das Whitepaper verwendet noch "Jot" — ist veraltet.

## Jon (Pre-Development, sehr früh)

**Was existiert:** Crate-Struktur (jon-cli als Library + jon als Binary). Grundarchitektur (Subprocess-Delegation an joy/jyn). JSON-Output-Vertrag als stabile Schnittstelle.

**Was noch fehlt:** Tier-0-Pattern-Router (30–50 Intents), Tier-2-LLM-Integration, Joyint-Pro-Anbindung.

**Rollout-Plan (aus JonStrategy.md):**

| Phase | Zeitraum | Inhalt |
|---|---|---|
| MVP Tier 0 | April–August 2026 | Pattern Router, 30–50 Intents, graceful degradation |
| Tier 2 eigener Key | August–Dezember 2026 | OpenAI/Anthropic/Ollama, Confirmation-Prompts |
| Tier 2 Joyint Pro | September–Dezember 2026 | Hosted LLM, Project Memory, Cross-Project-Intelligence |
| Tier 1 lokales LLM | 2027+ | Candle-Integration, niedrige Priorität |

## Pricing (Stand BusinessModel.md, März 2026)

| Tier | Preis | Kern-Features |
|---|---|---|
| Free | 0 | CLI, TUI, lokale App, eigener Git-Sync |
| Pro | 3 EUR/Monat | joyint.com Sync, WebUI, CalDAV, Notifications, 3 Automations, Jon Tier 2 |
| Teams | 6 EUR/User/Monat | Multi-User, Capabilities, AI-Dispatch, unlimitierte Automations |
| Enterprise | 15–20 EUR/User/Monat | On-Premises, SSO, Audit, Compliance, SLA, BYOG inklusive |
| BYOG Add-on | +2 EUR/Monat | GitHub/GitLab/Gitea als eigenes Git-Backend |

Break-Even bei wenigen hundert Usern (niedrige Infrastrukturkosten durch Git als Backend).

## Revenue-Szenarien (BusinessModel.md)

| Szenario | Zeitpunkt | Monatlich | Jährlich |
|---|---|---|---|
| Konservativ | Q3 2027 | ~2.600 EUR | ~31k EUR |
| Realistisch | Ende 2027 | ~6.600 EUR | ~80k EUR |
| Optimistisch | Mitte 2028 | ~28.800 EUR | ~346k EUR |
| Ambitioniert | Ende 2028 | ~101.000 EUR | ~1,21M EUR |

Das realistischste Szenario (~80k/Jahr) ist laut BusinessModel.md "solides Indie-SaaS, tragfähig für ein Kleinstteam, aber nicht Venture-tauglich." Enterprise-Segment hat höchstes Potenzial pro User.

## Whitepaper vs. Reality

| Whitepaper-Aussage | Befund |
|---|---|
| "Jot v0.2.0" | Falsch: heißt Jyn, ist bei v0.6.2 |
| "Drei Produkte (Joy/Jot/Jon)" | Intern korrekt, extern: zwei Produkte (Joy + Jyn), Jon ist Feature |
| "Joy v0.8.1 — 153/206 Items done" | Bestätigt: Joy aktiv weiterentwickelt |
| "AI Co-Authoring" | Bestätigt: `ai:claude@joy` in nahezu jedem Commit |
| "Dogfooding seit v0.5.0" | Bestätigt: Item-IDs in allen Commit-Messages |
| "AI im PM — unbesetztes Feld" | Veraltet: Linear for AI seit Mai 2025, Atlassian Rovo vorhanden |

## Offene Fragen

- Wann ist Jyn feature-complete für CalDAV-Sync?
- Gibt es bereits externe Nutzer ausserhalb Joydev?
- Was ist der genaue Status von joyint.com als Plattform (Repo privat)?
- Wie viel Entwicklungskapazität hat Joydev GmbH neben Horst Schwarz?
