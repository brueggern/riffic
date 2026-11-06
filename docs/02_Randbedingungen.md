# 02 Randbedingungen

Vorgegebene Einschränkungen, die nicht verhandelbar sind bzw. von aussen kommen.

## Technische Randbedingungen

- **RB-001** Zielplattform ist Android (Smartphone des Projektinhabers). iOS ist nicht geplant, könnte aber später dazukommen (siehe QA-003). Zusätzlich muss die App auf dem Desktop nutzbar sein (siehe FA-028).
- **RB-002** Ein eigener VPS (bei Contabo) und eine eigene Domain sind vorhanden und sollen für das Backend genutzt werden.
- **RB-003** Die Audio-Dateien werden nicht auf dem VPS abgelegt, sondern in einem separaten, sicheren Cloud-Speicher (Anbieter noch offen). Kein Self-Hosting des Speichers, um das Risiko von Datenverlust und den Aufwand für Backups zu vermeiden. Erwartetes Datenvolumen: ca. 10 GB. Ein bestimmter Datenstandort (Schweiz/EU) ist derzeit nicht gefordert. Gewählt: Backblaze B2 (siehe ADR-001).

## Organisatorische Randbedingungen

- **RB-004** Die Betriebskosten (insbesondere für den Cloud-Speicher) sollen möglichst gering sein.

## Rechtliche Randbedingungen

## Offene Fragen

- RB-001: Desktop als Web-App im Browser oder als installierte Anwendung? Welche Betriebssysteme?
