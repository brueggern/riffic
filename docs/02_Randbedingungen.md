# 02 Randbedingungen

Vorgegebene Einschränkungen, die nicht verhandelbar sind bzw. von aussen kommen.

## Technische Randbedingungen

- **RB-001** Zielplattform ist Android (Smartphone des Projektinhabers). iOS ist nicht geplant, könnte aber später dazukommen (siehe QA-003). Zusätzlich muss Riffic auf dem Desktop als Web-App im Browser nutzbar sein (siehe FA-028).
- **RB-002** Ein eigener VPS (bei Contabo) und eine eigene Domain sind vorhanden und sollen für das Backend genutzt werden. Die Subdomain `riffic.brueggern.dev` ist bereits eingerichtet; weitere Subdomains können ergänzt werden.
- **RB-005** Auf dem VPS sind Docker und Traefik (Reverse Proxy) installiert. Die Dienste von Riffic laufen als Docker-Container und werden über Traefik-Labels in der Docker-Konfiguration eingebunden.
- **RB-006** Build und Deployment erfolgen über GitHub Actions.
- **RB-003** Die Audio-Dateien werden nicht auf dem VPS abgelegt, sondern in einem separaten, sicheren Cloud-Speicher (Anbieter noch offen). Kein Self-Hosting des Speichers, um das Risiko von Datenverlust und den Aufwand für Backups zu vermeiden. Erwartetes Datenvolumen: ca. 10 GB. Ein bestimmter Datenstandort (Schweiz/EU) ist derzeit nicht gefordert. Gewählt: Backblaze B2 (siehe ADR-001).

## Organisatorische Randbedingungen

- **RB-007** Der Projektinhaber entwickelt selbst und kennt Laravel, Vue, Tailwind, JavaScript und HTML5 gut. Neue Technologien sind möglich.
- **RB-004** Die Betriebskosten (insbesondere für den Cloud-Speicher) sollen möglichst gering sein.

## Rechtliche Randbedingungen

## Offene Fragen
