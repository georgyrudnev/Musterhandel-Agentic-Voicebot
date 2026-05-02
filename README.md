# Musterhandel Agentic Voicebot in Genesys Cloud

> Ein agentischer Voicebot für einen fiktiven Großhändler – umgesetzt als hybride Lösung aus **Genesys Architect**, **AI Studio**, **Knowledge**, **Data Actions** und **Data Tables**.

## Überblick

Dieses Repository enthält **keine klassische Backend-Anwendung**, sondern die versionierbaren Exportartefakte einer laufenden Lösung in **Genesys Cloud**.

Der Kern der Implementierung liegt in der Plattform-Konfiguration:

- **Architect** orchestriert den Gesprächsablauf
- **AI Studio** definiert den agentischen Virtual Agent
- **Data Actions** verbinden externe Prozesse und Daten
- **Knowledge** beantwortet Produkt- und FAQ-Fragen
- **Data Tables** ermöglichen strukturierte Lookups, z. B. für PLZ → Markt
- **Workitems** bilden Folgevorgänge für manuelle Nachbearbeitung ab

Damit zeigt das Projekt sehr gut, wie sich moderne Conversational AI in einer Contact-Center-Plattform **ohne separates Custom-Backend** umsetzen lässt.

---

## Warum dieses Repository interessant ist

Dieses Projekt demonstriert einen praxisnahen **Hybrid-Ansatz**:

- klassische Bot-Logik mit **Intents, Entities und Tasks**
- kombiniert mit einem **agentischen Virtual Agent**
- ergänzt durch **Wissen, Tool-Aufrufe und Eskalationslogik**

Das Ergebnis ist eine Lösung, die sowohl strukturierte Prozesslogik als auch flexible agentische Interaktion abbildet.

---

## Repository-Inhalt

Das Repository bildet die Lösung als **versionierbare Konfiguration** ab:

| Datei | Typ | Zweck |
|---|---|---|
| `GR Testhandel AVA v2_v22-0.yaml` | Architect Bot Flow Export | Flow-Struktur, Variablen, Intents, Entities, Tasks, Eskalation und Übergabe an den Agentic Virtual Agent |
| `gro-handel-markt-finder---registrierung-export.json` | AI Studio Agent Export | Rolle, Guidelines, Guardrails, Tools, Events und fachliche Logik des agentischen Agents |
| `Handelsmärkte PLZ Standort.csv` | Data Table Import | PLZ-basierte Zuordnung zum nächstgelegenen Markt |

> **Wichtig:** Die Dateien machen die Logik nachvollziehbar, sind aber **nicht die vollständige Laufzeitumgebung**. In einer neuen Genesys-Organisation müssen Integrationen, Berechtigungen und Zuordnungen erneut eingerichtet werden.

---

## Architektur in Kürze

Die Lösung ist bewusst schlank gedacht und fokussiert sich auf die tatsächlich relevanten Bausteine des Projekts.

```mermaid
flowchart LR
    A[Anrufer / Voice Channel] --> B[Genesys Architect]
    B --> C[Agentic Virtual Agent<br/>AI Studio]
    C --> D[Knowledge aus Sharepoint]
    C --> E[Data Actions]
    E --> E1[Lieferstatus]
    E --> E2[Markt-Lookup]
    E --> E3[Workitem-Anlage]
    B --> F[Data Table<br/>PLZ -> Markt]
    C --> G[Eskalation / Exit Info]
    G --> H[Servicerouting / Mensch]
