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

## Benutzerkonto und Authentifizierung

- **FA-010** (Muss) Der Benutzer muss sich anmelden (Login), um die App bzw. seine Daten zu nutzen. Vorerst gibt es nur einen Benutzer. Anmeldemethode: E-Mail/Passwort und/oder Passkey (Entscheid offen, siehe Architektur/ADR).
- **FA-011** (Muss) Nach dem ersten Login bleibt der Benutzer dauerhaft angemeldet, damit QA-001/QA-002 eingehalten werden.
- **FA-012** (Kann) Die App kann zusätzlich per Fingerabdruck (Biometrie) geschützt werden.
- **FA-013** (Muss) Benutzerkonten werden manuell angelegt; es gibt vorerst keine Selbstregistrierung.

## Synchronisation

- **FA-014** (Muss) Aufnahmen und Metadaten werden zuerst lokal auf dem Gerät gespeichert.
- **FA-015** (Muss) Lokale Daten können auf den Server bzw. in einen Cloud-Speicher hochgeladen werden.

## Offene Fragen

- FA-012: Soll der Fingerabdruck bei jedem Öffnen der App abgefragt werden? Das kostet Zeit vor der Aufnahme (QA-002).
- FA-015: Erfolgt der Upload automatisch im Hintergrund oder manuell durch den Benutzer?
- FA-015: Ist eine Synchronisation in beide Richtungen nötig (z. B. neues Gerät, mehrere Geräte), oder dient der Upload nur als Backup?

