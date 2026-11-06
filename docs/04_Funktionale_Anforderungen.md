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
- **FA-012** (Kann) Die App kann zusätzlich per Fingerabdruck (Biometrie) geschützt werden. Der Fingerabdruck wird nicht bei jedem Öffnen der App abgefragt.
- **FA-013** (Muss) Benutzerkonten werden manuell angelegt; es gibt vorerst keine Selbstregistrierung.

## Synchronisation

- **FA-014** (Muss) Aufnahmen und Metadaten werden zuerst lokal auf dem Gerät gespeichert.
- **FA-015** (Muss) Lokale Daten werden automatisch im Hintergrund auf den Server bzw. in den Cloud-Speicher hochgeladen.
- **FA-016** (Muss) Die Synchronisation erfolgt in beide Richtungen: Daten vom Server werden auf das Gerät übertragen (z. B. bei neuem Gerät oder mehreren Geräten).

## Offene Fragen

- FA-012: Wann wird der Fingerabdruck stattdessen abgefragt (z. B. nur bei erneuter Anmeldung)?
- FA-016: Wie werden Konflikte behandelt, wenn derselbe Eintrag auf zwei Geräten geändert wurde (z. B. letzte Änderung gewinnt)?
- FA-016: Sollen auf dem Gerät immer alle Audio-Dateien lokal vorliegen, oder werden ältere bei Bedarf nachgeladen (Speicherplatz)?

