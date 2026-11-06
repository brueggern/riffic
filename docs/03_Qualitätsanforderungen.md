# 03 Qualitätsanforderungen

Nicht-funktionale Anforderungen, möglichst messbar formuliert.

| ID | Kategorie | Anforderung | Priorität |
|---|---|---|---|
| QA-001 | Usability / Reaktionszeit | Eine neue Aufnahme muss mit minimalem Aufwand startbar sein: App öffnen, „Neue Aufnahme“ wählen, Aufnahme läuft. Keine weiteren Eingaben vor dem Start. | Muss |
| QA-002 | Reaktionszeit | Die Aufnahme beginnt in weniger als 1 Sekunde nach dem Antippen von „Neue Aufnahme“. | Muss |
| QA-003 | Portierbarkeit | Eine spätere iOS-Version soll durch technische Entscheide nicht verbaut werden (siehe RB-001). | Kann |
| QA-004 | Sicherheit | Alle Daten (Aufnahmen, Notizen, Metadaten) sind durch Authentifizierung geschützt und nur für den angemeldeten Benutzer zugänglich. | Muss |
| QA-005 | Erweiterbarkeit | Ein späterer Ausbau zu einer mandantenfähigen SaaS-Lösung (Multi-Tenant) soll durch technische Entscheide nicht verbaut werden. | Kann |

## Offene Fragen

- QA-004: Ist mit dem Login ein Server/Cloud-Speicher verbunden (Daten liegen online), oder bleiben die Daten vorerst lokal auf dem Gerät?
