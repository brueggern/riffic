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
