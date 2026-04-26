---
status: done
updated: 2026-04-26
---

# EU AI Act: Requirements-Mapping auf Joydev-Implementierung

Quellen: `research/01-eu-ai-act/risk-categories.md`, `joyint-relevance.md`, `research/02-joyint-product/architecture.md`, Stand 2026-04-26.

## Vorbemerkung: Zwei Perspektiven

Joyint GmbH tritt in zwei Rollen auf:

1. **Als Anbieter (Art. 3 Abs. 3):** Entwickler von Joy, Jyn, Jon. Stufe 4 → keine spezifischen EU-AI-Act-Pflichten.
2. **Als Betreiber (Art. 3 Abs. 4):** Einsatz externer KI-Agenten in der eigenen Entwicklung (Dogfooding) und Bereitstellung von Governance-Infrastruktur für Kunden, die KI in regulierten Branchen einsetzen.

Das strategische Argument: Joydevs Governance-Architektur implementiert strukturell die Pflichten, die der EU AI Act Betreibern von Hochrisiko-KI auferlegt — und verkauft diese Compliance-Infrastruktur weiter.

---

## Teil A: Pflichten als Anbieter (Joyint GmbH → Joy/Jyn/Jon)

### Stufe 4: Minimales Risiko (Joy, Jyn)

Keine spezifischen EU-AI-Act-Anforderungen. Nur allgemeines Recht gilt.

| Anforderung | Quelle | Status |
|---|---|---|
| DSGVO-Konformität | DS-GVO | Offen — keine personenbezogenen Daten im Kern; Billing via Drittanbieter |
| Produkthaftungsrecht | ProdHaftG | Keine kritischen Safety-Features → niedrig |
| Keine Verbotshandlungen (Art. 5) | EU AI Act | Erfüllt — kein Social Scoring, keine Gesichtserkennung, keine Manipulation |

### Stufe 3: Begrenztes Risiko (Jon)

| Anforderung | EU AI Act Artikel | Joydev-Implementierung | Komponente |
|---|---|---|---|
| Offenlegung als Maschinensystem | Art. 50 Abs. 1 | Jon ist CLI-Tool; kein simuliertes menschliches Gegenüber. Keine aktive Offenlegungspflicht, aber Dokumentation empfohlen. | jon-CLI (öffentlich, MIT) |
| Keine täuschende Darstellung | Art. 50 Abs. 4 | Entfällt — Jon simuliert keine Person | — |

**Handlungsbedarf:** README/Docs sollen explizit benennen, dass Jon kein menschliches Gegenüber simuliert. Low-Effort-Absicherung.

---

## Teil B: Pflichten als Betreiber (Joyint nutzt KI-Agenten)

Gilt für: Dogfooding von Joy AI mit Claude Code / GitHub Copilot bei der eigenen Produktentwicklung.

| Pflicht | EU AI Act Artikel | Beschreibung | Joydev-Implementierung | Komponente |
|---|---|---|---|---|
| Menschliche Aufsicht sicherstellen | Art. 26 Abs. 1 | Betreiber muss sicherstellen, dass KI-Ausgaben durch Menschen überwacht werden | 5 Orchestration Modes (autonomous → approval → pairing). In regulierten Kontexten: Approval-Mode als Default | joy-ai (öffentlich, MIT) |
| Capability-Beschränkung für KI-Agenten | Art. 26 Abs. 2 | Einsatz von KI nur im Rahmen definierter Aufgaben und Zwecke | Trustship: Ed25519-Keys + Capabilities + Delegation Tokens — KI-Agenten erhalten nur granular freigegebene Rechte | platform (privat, kommerziell) |
| Schreiboperationen validieren | Art. 26 Abs. 1 | Keine unkontrollierten Systemveränderungen durch KI | Guardianship: Guard fängt alle Schreiboperationen ab und validiert gegen Trust Model | joy-core (öffentlich, MIT) |
| Audit Trail führen | Art. 26 Abs. 5 | Aufzeichnung von KI-Aktionen für nachträgliche Prüfung | Traceability: Append-only Event Log in `.joy/logs/`, kryptografisch signiert; Judge als unabhängiges Audit-Binary | joy-core + judge (judge privat) |
| Kostenkontrolle / Budget-Limits | — (Best Practice, kein direkter Artikel) | Nicht gesetzlich vorgeschrieben, aber betrieblicher Risikoschutz | Settlement: Token- und Kostenerfassung pro AI-Job, `max_cost_per_job`-Limits | joy-ai (öffentlich, MIT) |

---

## Teil C: Joyint als Enabler für Kunden in Hochrisiko-Branchen

Das ist das strategische Kernargument. Kunden, die KI in regulierten Bereichen einsetzen (Finanz, Gesundheit, Behörden), müssen als Betreiber von Hochrisiko-KI folgende Pflichten erfüllen — die Joydevs Architektur out-of-the-box bereitstellt:

| Pflicht (Hochrisiko, Art. 9–17) | EU AI Act Artikel | Joydev-Lösung | Komponente |
|---|---|---|---|
| Risikomanagementsystem einrichten und dokumentieren | Art. 9 | Konfigurierbare Gates in `project.yaml`: definiere welche KI-Aktionen welches Review brauchen | joy-core (öffentlich) |
| Datensatz-Governance (Qualität, Repräsentativität) | Art. 10 | Nicht direkt adressiert — Joyint ist kein ML-Training-Tool | — |
| Technische Dokumentation führen | Art. 11 | Joyint-Architektur ist open source + vollständig dokumentiert; Kunden-Governance via `.joy/project.yaml` + Audit-Log | joy-core (öffentlich) |
| Protokollierung und Rückverfolgbarkeit | Art. 12 | Judge: append-only, kryptografisch signiertes Event-Log. JOYC: optional On-Chain-Settlement für tamper-evident Nachweis | judge (privat) + joyc (privat) |
| Transparenz gegenüber Nutzern | Art. 13 | Traceability: alle KI-Aktionen sind im Log nachvollziehbar; Kunden können Logs exportieren | joy-core (öffentlich) |
| Menschliche Aufsicht ermöglichen | Art. 14 | Orchestration Modes + Approval Gates: explizite Mensch-in-der-Schleife-Konfiguration pro Team/Kontext | joy-ai (öffentlich) + platform (privat) |
| Genauigkeit, Robustheit, Cybersicherheit | Art. 15 | E2E-Verschlüsselung (AES-256-GCM), client-seitige Keys; Git-native Unveränderlichkeit des Audit Trails | joy-core + crypt (privat) |
| Qualitätsmanagementsystem | Art. 17 | Guardianship validiert jede Schreiboperation; konfigurierbare Review-Workflows | joy-core (öffentlich) |
| Registrierungspflicht (EU-Datenbank) | Art. 49 | Betrifft Hochrisiko-Anbieter — Joyint ist Anbieter von Stufe-4-Tools, nicht Hochrisiko-Anbieter | — |

**Wichtig:** Joyint erfüllt diese Anforderungen für den Kunden auf der *Werkzeug*-Ebene — der Kunde bleibt verantwortlicher Betreiber. Joyint liefert die Infrastruktur zur Compliance, nicht die Compliance selbst.

---

## Offene Fragen / Handlungsbedarf

| Frage | Priorität | Nächster Schritt |
|---|---|---|
| JOYC als Finanzinstrument? MiCA-Pflichten? | Mittel | Rechtsberatung sobald JOYC-Launch näher rückt |
| Mitverantwortung als Plattformanbieter bei Enterprise-Hochrisiko-Kunden? | Mittel | AGB und ToS entsprechend gestalten; Kundenpflichten vertraglich auf Kunden abwälzen |
| Jon-Dokumentation: Maschinenidentität explizit benennen | Niedrig | Ein Satz in README / Docs reicht |
| Bundesnetzagentur-Praxis zu AI-Orchestrierungstools | Niedrig | Beobachten, noch keine Präzedenzfälle |

---

## Zusammenfassung

Joyint selbst hat **keine aktiven EU-AI-Act-Compliance-Lasten** (Stufe 4 als Anbieter). Die Governance-Architektur, die im Produkt steckt, ist primär als **B2B-Verkaufsargument** relevant: Sie befähigt Kunden in regulierten Branchen, ihre eigenen Hochrisiko-Pflichten zu erfüllen — ohne eigenen Engineering-Aufwand.

Das macht den EU AI Act zu einem **Marktöffner**, nicht zu einem Compliance-Risiko für Joyint.
