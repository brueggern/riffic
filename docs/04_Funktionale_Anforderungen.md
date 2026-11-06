# 04 Funktionale Anforderungen

Gruppiert nach Funktionsbereichen. Priorität: Muss / Soll / Kann.

## Aufnahme

- **FA-001** (Muss) Der Benutzer kann direkt vom Startbildschirm eine neue Audio-Aufnahme starten.
- **FA-002** (Muss) Der Benutzer kann eine laufende Aufnahme beenden; die Aufnahme wird gespeichert.

## Verwaltung von Einträgen

- **FA-003** (Muss) Nach der Aufnahme kann der Benutzer optional einen Titel vergeben. Ohne Eingabe erhält die Aufnahme den Standardtitel „Aufnahme {ID}“.
- **FA-004** (Muss) Nach der Aufnahme kann der Benutzer optional Notizen hinzufügen.
- **FA-006** (Muss) Jede Aufnahme hat ein Erstelldatum und ein Bearbeitungsdatum. Beide werden automatisch gesetzt bzw. aktualisiert und sind für den Benutzer sichtbar.
- **FA-007** (Muss) Die Aufnahmen werden nach Bearbeitungsdatum sortiert angezeigt (zuletzt bearbeitete zuoberst).

## Gruppierung

- **FA-005** (Soll) Der Benutzer kann eine Aufnahme einer Gruppe (Ordner) zuordnen. Eine Aufnahme gehört zu höchstens einer Gruppe; Aufnahmen ohne Gruppe sind erlaubt. Gruppen sind nicht verschachtelt (keine Unterordner).
- **FA-008** (Soll) Der Benutzer kann einer Aufnahme beliebig viele Tags zuweisen (z. B. für Stimmung).
- **FA-009** (Soll) Der Benutzer kann jederzeit neue Tags erstellen.

## Import / Upload

- **FA-017** (Muss) Der Benutzer kann manuell einen Eintrag erstellen und eine bestehende Audio-Datei vom Gerät hochladen (z. B. eine Aufnahme aus einem anderen Recorder). Unterstützte Formate: MP3, WAV, M4A. Titel, Notizen, Gruppe und Tags werden wie bei einer normalen Aufnahme erfasst.

## Benutzerkonto und Authentifizierung

- **FA-010** (Muss) Der Benutzer muss sich anmelden (Login), um die App bzw. seine Daten zu nutzen. Vorerst gibt es nur einen Benutzer. Anmeldemethode: E-Mail/Passwort und/oder Passkey (Entscheid offen, siehe Architektur/ADR).
- **FA-011** (Muss) Nach dem Login bleibt der Benutzer angemeldet, damit QA-001/QA-002 eingehalten werden. Die Session bzw. das Token läuft nach ca. 14 Tagen ab. Ein Ablauf darf eine laufende Aufnahme nie unterbrechen. Auch nach Ablauf bleibt das lokale Aufnehmen und Bearbeiten ohne erneuten Login möglich; nur die Synchronisation pausiert bis zum erneuten Login.
- ~~**FA-012** (Kann) Die App kann zusätzlich per Fingerabdruck (Biometrie) geschützt werden.~~ *Verworfen: Fingerabdruck wird nicht umgesetzt.*
- **FA-013** (Muss) Benutzerkonten werden manuell angelegt; es gibt vorerst keine Selbstregistrierung.

## Synchronisation

- **FA-014** (Muss) Aufnahmen und Metadaten werden zuerst lokal auf dem Gerät gespeichert.
- **FA-015** (Muss) Lokale Daten werden automatisch im Hintergrund auf den Server bzw. in den Cloud-Speicher hochgeladen.
- **FA-016** (Muss) Die Synchronisation erfolgt in beide Richtungen: Daten vom Server werden auf das Gerät übertragen (z. B. bei neuem Gerät oder mehreren Geräten).
- **FA-018** (Muss) Bei Konflikten (derselbe Eintrag auf mehreren Geräten geändert) gewinnt die letzte Änderung.
- **FA-019** (Soll) Nicht alle Audio-Dateien müssen lokal vorliegen; Audio-Dateien, die nicht auf dem Gerät sind, werden bei Bedarf (z. B. beim Abspielen) vom Cloud-Speicher nachgeladen. Metadaten liegen immer vollständig lokal vor. Lokale Audio-Dateien werden nur manuell durch den Benutzer vom Gerät entfernt (nicht automatisch); die Kopie im Cloud-Speicher bleibt erhalten.

## Offene Fragen


