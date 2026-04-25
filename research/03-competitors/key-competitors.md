---
status: done
updated: 2026-04-25
---

# Wettbewerber: Die wichtigsten Konkurrenten

Quelle: `docs/biz/Competition.md` (intern, Stand 2026-04-24).

## Paperclip — direkteste Bedrohung auf Level 4

**Was es ist:** Dedizierter AI-Agenten-Orchestrator. Pitch: "Run a company of AI agents." User definiert Ziele, Rollen, Budgets, Approval-Gates. AI-Agenten (Claude Code, Codex, Cursor, OpenClaw, beliebige HTTP-Tools) bearbeiten Tasks. Eingebettetes PostgreSQL, Onboarding per `npx paperclipai onboard`.

**Warum bedrohlich:** Über 36.000 GitHub Stars in unter vier Wochen. Starke Community-Dynamik. Adressiert explizit Level-4-Features: Approval-Gates, per-Agent-Budgets, atomic Task-Checkout mit Budget-Enforcement, Immutable Log.

**Wo Paperclip schwächer ist:**
- Kein git-natives Datenformat (PostgreSQL — schwer nachzurüsten)
- Kein PM-Tiefe: nur Goals + Tasks, keine Epics/Stories/Milestones
- Kein E2E, keine Runtime-Protection auf Capability-Ebene
- Audit-Log lebt im selben Datensystem wie die Daten (kein unabhängiger Audit wie Judge)
- Kein On-Chain-Settlement
- Zielgruppe: Solo-Operator und Agenturen — nicht regulierte Dev-Teams

**Fazit:** Paperclip validiert die Kategorie AI-Governance als Markt — ohne Joyints strukturelle Tiefe zu erreichen. Kein direkter Verdrängungswettbewerb, da unterschiedliche Zielgruppen.

---

## Linear — stärkster Konkurrent auf Level 2–3

**Was es ist:** Modernes PM-Tool, 25.000+ Unternehmen, sub-50ms UI, starke Brand im Startup-Ökosystem. Seit Mai 2025: "Linear for Agents" mit 15+ integrierten AI-Tools (Cursor, Copilot, Codex, Devin, Windsurf u.a.), MCP-Server, bidirektionales MCP.

**Wo Linear stark ist:** Polierte UI, Geschwindigkeit, Breite der Integrationen, Enterprise-Readiness (SAML, SCIM, SOC 2, HIPAA). Monatliche Updates seit Mai 2025.

**Wo Linear schwächer ist:**
- Keine git-nativen Daten (Cloud-DB, CSV-Export auf 2.000 Issues limitiert — Lock-in)
- Kein Cost-Tracking, keine Budget-Limits, keine konfigurierbaren Gates (alles Level-4-Lücke)
- Keine E2E-Verschlüsselung
- Kein BYOG
- Kann Governance-Tiefe nicht nachträglich einbauen ohne Kern-Rebuild

**Fazit:** Für Teams die UI-Polishing und Integrationsbreite priorisieren ist Linear heute besser. Joyint konkurriert nicht auf UI-Polishing, sondern auf Datenhoheit und Governance-Tiefe.

---

## Jira / Atlassian Rovo — etabliertes Enterprise-Tool

**Was es ist:** Marktführer im Enterprise-PM. Atlassian hat mit Rovo AI-Features nachgerüstet.

**Wo Jira stark ist:** Marktdurchdringung, Feature-Tiefe, Enterprise-Integrationen, bestehende Kaufkanäle.

**Wo Jira schwächer ist:** Langsam, komplex, teuer, bei Entwicklern unbeliebt. Rovo ist auf ein bestehendes Datenmodell aufgesetzt — kein feingranularer AI-Workflow, kein unabhängiger Audit. Administration ist ein Vollzeit-Job.

**Fazit:** Jira nicht frontal angreifen. Entwickler die Jira hassen finden Joy als leichtgewichtige Alternative. Enterprise-Einstieg kommt über Level 4, nicht über Feature-Parität mit Jira.

---

## GitHub Projects / GitLab / Gitea

**Was sie sind:** PM-Features integriert in Code-Hosting-Plattformen.

**Stärke:** Enge PR/CI-Integration, Netzwerkeffekte, teilweise kostenlos.

**Schwäche:** PM-Features als Nebenfunktion, kein dedizierter Workflow-Layer, kein AI-Governance.

**Joyint-Strategie:** Nicht ersetzen, ergänzen. Joy-Sync-Features (JOY-006A/B/C) erlauben Joy als Source of Truth mit GitHub/GitLab als Mirror für externe Stakeholder.

---

## Nicht-Konkurrenten (häufige Verwechslung)

**nWave:** Workflow-Pack für Claude Code. Disziplin-Layer *innerhalb* einer Coding-Session, kein PM-Tool. Komplementär zu Joyint, kein Wettbewerber.

**AutoGen, CrewAI, LangGraph:** Agent-Orchestrierungs-Frameworks auf Library-Ebene. Andere Zielgruppe (Engineers die Custom-Pipelines bauen). Kein PM, keine Governance-UI.

**Fiddler, Weights & Biases Weave, Arize:** AI-Governance im Sinne von Modell-Performance-Monitoring — anderer Markt.
