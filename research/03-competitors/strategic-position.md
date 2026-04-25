---
status: done
updated: 2026-04-25
---

# Wettbewerber: Strategische Position

Quelle: `docs/biz/Competition.md` (intern, Stand 2026-04-24).

## Wo Joyint gewinnt

1. **Entwickler mit Terminal-Fokus und Datenhoheit** — kein anderes PM-Tool bietet beides (Level 2 + git-nativ)
2. **Privacy- und Compliance-Teams** — E2E-Verschlüsselung als Alleinstellungsmerkmal
3. **AI-native Teams mit Kostenkontrolle** — Cost-Tracking und Budget-Enforcement, kein Wettbewerber hat das
4. **Regulierte Branchen** — Traceability via Judge (tamper-evident, unabhängige Instanz) und Settlement via JOYC (On-Chain)
5. **BYOG-Kunden** — "Wir wollen eure Daten nicht mal haben"
6. **Kostensensibler Teams** — 3–5x günstiger als Linear beim Kern-Feature-Set
7. **Microsoft-365-Shops** — Jyn via Graph API integriert in To Do, Planner, Outlook, Teams — ohne eigene App

## Wo Joyint nicht gewinnt (und es nicht muss)

1. **Teams die heute polished Web-UI brauchen** — Linear und Paperclip sind besser
2. **Große Orgs tief im Jira-Ökosystem** — Switching-Kosten zu hoch
3. **Solo-Operatoren die "AI-Companies" bauen** — Paperclip hat bessere Narrative
4. **Nicht-technische User** — Joy ist für Entwickler gemacht
5. **Python-Engineers die Custom Agent Pipelines bauen** — AutoGen, CrewAI, LangGraph sind dafür gemacht

## Timing: EU AI Act als Treiber

AI-Governance ist kein Zukunftsthema mehr — es ist teilweise bereits Pflicht:

- **Seit 2. Februar 2025:** EU AI Act Art. 4 (AI Literacy) und Art. 5 (Verbote) in Kraft
- **Seit 2. August 2025:** GPAI-Pflichten in Kraft
- **Seit 1. Januar 2026:** Texas TRAIGA und Illinois HB 3773 in Kraft
- **30. Juni 2026:** Colorado AI Act
- **2. August 2026:** Vollständige Anwendung EU AI Act (Hochrisiko-Anforderungen, Art. 50, Bußgelder)

Joyint positioniert sich als Tool das bestehende und unmittelbar bevorstehende Pflichten heute erfüllt — nicht als Vorwegnahme eines zukünftigen Markts.

## Hauptrisiken

**Linear und Atlassian** könnten Cost-Tracking und Budget-Features in 6–12 Monaten nachliefern. Schutz: Kombination aus Governance-Tiefe *und* strukturellen Differenzierern (git-nativ, E2E, BYOG, unabhängiger Audit) — keine einzelnen Features sind kopierbar.

**Paperclip** wächst schnell und besetzt Vocabulary ("budget enforcement", "approval gates", "hire an agent"). Schutz: PM-Tiefe (Level 2), Datenhoheit, Judge als unabhängige Instanz, JOYC, andere Zielgruppe.

**Enterprise-Käufer** könnten vor den EU AI Act Deadlines pragmatisch bei Linear oder Jira kaufen, die dann Governance-Features marketingseitig betonen. Schutz: Klare Positionierung, dass Joyints Traceability und Settlement strukturell nicht nachgerüstet werden können.

## Bridge-Strategie: Nicht entweder-oder

Die Sync-Features (JOY-006A/B/C für GitHub, Gitea, GitLab) und die Jyn-Integrationen (CalDAV, Graph API) senken die Wechselhürde. Teams können Joy intern einsetzen und GitHub oder GitLab als Mirror für Stakeholder behalten. Kein Entweder-oder — progressive Migration.
