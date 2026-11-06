# 02 Randbedingungen

Vorgegebene Einschränkungen, die nicht verhandelbar sind bzw. von aussen kommen.

## Technische Randbedingungen

- **RB-001** Zielplattform ist Android (Smartphone des Projektinhabers). iOS ist nicht geplant, könnte aber später dazukommen (siehe QA-003).
- **RB-002** Ein eigener VPS und eine eigene Domain sind vorhanden und sollen für das Backend genutzt werden.
- **RB-003** Die Audio-Dateien werden nicht auf dem VPS abgelegt, sondern in einem separaten, sicheren Cloud-Speicher (Anbieter noch offen). Kein Self-Hosting des Speichers, um das Risiko von Datenverlust und den Aufwand für Backups zu vermeiden. Erwartetes Datenvolumen: ca. 10 GB.

## Organisatorische Randbedingungen

- **RB-004** Die Betriebskosten (insbesondere für den Cloud-Speicher) sollen möglichst gering sein.

## Rechtliche Randbedingungen

## Offene Fragen

- RB-003: Welcher Cloud-Speicher (Anbieter, Standort/Region, Kosten)? → Entscheid als ADR.
