# 03 Qualitätsanforderungen

Nicht-funktionale Anforderungen, möglichst messbar formuliert.

| ID | Kategorie | Anforderung | Priorität |
|---|---|---|---|
| QA-001 | Usability / Reaktionszeit | Eine neue Aufnahme muss mit minimalem Aufwand startbar sein: App öffnen, „Neue Aufnahme“ wählen, Aufnahme läuft. Keine weiteren Eingaben vor dem Start. | Muss |
| QA-002 | Reaktionszeit | Die Aufnahme beginnt in weniger als 1 Sekunde nach dem Antippen von „Neue Aufnahme“. | Muss |
| QA-003 | Portierbarkeit | Eine spätere iOS-Version soll durch technische Entscheide nicht verbaut werden (siehe RB-001). | Kann |
| QA-004 | Sicherheit | Alle Daten (Aufnahmen, Notizen, Metadaten) sind durch Authentifizierung geschützt und nur für Accounts zugänglich, die Zugriff auf den jeweiligen Bereich haben. | Muss |
| QA-005 | Sicherheit / Mandantenfähigkeit | Die Daten der Bereiche (Mandanten) sind strikt voneinander getrennt. Ein späterer Ausbau zu einer SaaS-Lösung soll nicht verbaut werden. | Muss |
| QA-006 | Verfügbarkeit | Aufnehmen und Bearbeiten funktionieren vollständig ohne Netzverbindung (Offline-First, siehe FA-014). | Muss |
| QA-007 | Usability | Upload und Synchronisation beeinträchtigen die Bedienung der App nicht (laufen im Hintergrund, blockieren keine Eingaben). | Muss |

## Offene Fragen
