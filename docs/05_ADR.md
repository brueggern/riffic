# 05 Architecture Decision Records

Vorlage:

```
## ADR-xxx: <Titel>
- Status: Vorgeschlagen | Akzeptiert | Abgelöst durch ADR-yyy | Verworfen
- Datum: JJJJ-MM-TT

**Kontext:** …
**Entscheid:** …
**Alternativen:** …
**Konsequenzen:** …
```

## ADR-001: Backblaze B2 als Cloud-Speicher für Audio-Dateien

- Status: Akzeptiert
- Datum: 2026-11-06

**Kontext:** Audio-Dateien sollen nicht auf dem VPS, sondern in einem separaten, sicheren Cloud-Speicher liegen (RB-003). Erwartetes Volumen ca. 10 GB, Kosten möglichst gering (RB-004). Es dürfen keine Dateien verloren gehen (QA-008), und der Speicher muss austauschbar sein (QA-009). Ein bestimmter Datenstandort ist nicht gefordert.

**Entscheid:** Backblaze B2 wird als Cloud-Speicher verwendet. Der Zugriff erfolgt ausschliesslich über die S3-kompatible API. Die Versionierung der Dateien wird aktiviert, um versehentliches Löschen oder Überschreiben (auch durch Fehler in der App) rückgängig machen zu können.

**Alternativen:**
- Cloudflare R2: 10 GB gratis, kein Egress. Weniger Schutzmechanismen gegen versehentliches Löschen.
- Hetzner Object Storage: EU-Standort, aber Pauschale (ca. €5–6.50/Monat) bei 10 GB teurer.
- Infomaniak Object Storage: Datenstandort Schweiz; wäre bei entsprechender Anforderung erste Wahl.
- Contabo Object Storage: günstig, aber beim gleichen Anbieter wie der VPS (keine Risikoverteilung).
- Google Drive: Für persönliche Nutzerdateien gedacht, nicht als App-Speicher; ungeeignet für gemeinsame Bereiche und Mandantentrennung (QA-005). Allenfalls später als Export-Funktion.
- Self-Hosting auf dem VPS: Verworfen wegen Risiko von Datenverlust und Aufwand für Backups.

**Konsequenzen:**
- Kosten bei ca. 10 GB praktisch null (erste 10 GB gratis, danach ca. $6.95/TB/Monat).
- Durch die reine Nutzung der S3-API kann der Anbieter später gewechselt werden (z. B. zu Infomaniak bei Bedarf nach Datenstandort Schweiz).
- Versionierung erhöht den Speicherbedarf leicht; alte Versionen müssen ggf. per Lifecycle-Regel aufgeräumt werden.

## ADR-002: AAC/M4A als Aufnahmeformat

- Status: Akzeptiert
- Datum: 2026-11-06

**Kontext:** Aufnahmen sollen platzsparend gespeichert werden (ca. 10 GB Gesamtvolumen, RB-003), die Aufnahme muss in unter 1 Sekunde starten (QA-002) und robust sein (QA-008). Android unterstützt die Aufnahme in MP3 nicht nativ.

**Entscheid:** Aufnahmen in der App werden im Format AAC in einem M4A-Container gespeichert und so auch in den Cloud-Speicher hochgeladen. Für den Download wird zusätzlich MP3 angeboten (FA-027).

**Alternativen:**
- MP3: Gängigstes Format, aber auf Android nur mit zusätzlicher Encoder-Bibliothek aufnehmbar; bei gleicher Dateigrösse eher schlechtere Qualität.
- WAV: Verlustfrei, aber rund 10-mal grösser; sprengt das Speicherziel.
- Opus/OGG: Sehr effizient, aber weniger verbreitet bei Abspielgeräten und DAWs.

**Konsequenzen:**
- Native Android-APIs können verwendet werden, keine zusätzliche Encoder-Bibliothek für die Aufnahme.
- Kleine Dateien bei guter Qualität.
- Für den MP3-Download ist eine Umwandlung nötig (im Backend, siehe ADR-003).
- Manuell hochgeladene Dateien (FA-017: MP3, WAV, M4A) werden im Originalformat gespeichert, sofern nichts anderes entschieden wird.

## ADR-003: MP3-Umwandlung im Backend beim Download

- Status: Akzeptiert
- Datum: 2026-11-06

**Kontext:** Aufnahmen werden als AAC/M4A gespeichert (ADR-002), für den Download soll MP3 angeboten werden (FA-027), sowohl in der Mobile App als auch in der Web-App (FA-028).

**Entscheid:** Die Umwandlung nach MP3 erfolgt im Backend, und zwar erst bei der Download-Anfrage (on demand). Dateien, die bereits als MP3 vorliegen, werden ohne Umwandlung ausgeliefert.

**Alternativen:**
- Umwandlung in der App bzw. im Browser: Wäre in Mobile App und Web-App doppelt umzusetzen und belastet das Gerät.
- MP3 nach Upload bzw. Synchronisation im Hintergrund erzeugen und zusätzlich speichern: Schnellerer Download, aber Job-Verarbeitung mit Fehlerbehandlung nötig, zwei Dateien pro Aufnahme konsistent zu halten und doppelter Speicherbedarf. Verworfen, da MP3-Downloads selten sind und weniger bewegliche Teile die Robustheit (QA-008) unterstützen.

**Konsequenzen:**
- Eine einzige Implementierung für alle Clients.
- Das Backend auf dem VPS benötigt ein Werkzeug zur Audio-Umwandlung (z. B. FFmpeg).
- Der Download dauert etwas länger, da die Datei zuerst aus dem Cloud-Speicher geladen und umgewandelt wird.
- Falls die Wartezeit stört, kann eine einmal erzeugte MP3 später im Backend zwischengespeichert werden (Option, noch nicht entschieden).

## ADR-004: PostgreSQL als Datenbank des Backends

- Status: Akzeptiert
- Datum: 2026-11-07

**Kontext:** Das Backend verwaltet Accounts, Bereiche (Mandanten), Mitgliedschaften und die Metadaten der Aufnahmen (Titel, Notizen, Gruppen, Tags, Datumsfelder). Die Daten der Bereiche müssen strikt getrennt sein (QA-005), und die Synchronisation braucht verlässliche Transaktionen (QA-008).

**Entscheid:** PostgreSQL wird als Datenbank verwendet und als Docker-Container auf dem VPS betrieben (RB-005).

**Alternativen:**
- MySQL/MariaDB: Ebenfalls gut geeignet und in Laravel verbreitet; PostgreSQL bietet aber mehr Möglichkeiten (z. B. Row-Level Security für die Mandantentrennung, bessere JSON-Unterstützung).
- SQLite: Für ein Backend mit mehreren gleichzeitigen Clients und späterem SaaS-Ausbau zu eingeschränkt.

**Konsequenzen:**
- Datenbank-Backups müssen eingerichtet werden (z. B. regelmässiger Dump in den Cloud-Speicher), da die Metadaten sonst nur auf dem VPS liegen.
