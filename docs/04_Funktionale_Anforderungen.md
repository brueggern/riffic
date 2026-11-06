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

- **FA-005** (Soll) Der Benutzer kann eine Aufnahme einer Gruppe (Ordner) zuordnen. Gruppen gehören zu einem Bereich. Eine Aufnahme gehört zu höchstens einer Gruppe; Aufnahmen ohne Gruppe sind erlaubt. Gruppen sind nicht verschachtelt (keine Unterordner).
- **FA-008** (Soll) Der Benutzer kann einer Aufnahme beliebig viele Tags zuweisen (z. B. für Stimmung). Tags gehören zu einem Bereich.
- **FA-009** (Soll) Der Benutzer kann jederzeit neue Tags erstellen.

## Import / Upload

- **FA-017** (Muss) Der Benutzer kann manuell einen Eintrag erstellen und eine bestehende Audio-Datei vom Gerät hochladen (z. B. eine Aufnahme aus einem anderen Recorder). Unterstützte Formate: MP3, WAV, M4A. Titel, Notizen, Gruppe und Tags werden wie bei einer normalen Aufnahme erfasst.
- **FA-027** (Soll) Der Benutzer kann eine Aufnahme als MP3-Datei herunterladen bzw. exportieren (unabhängig vom intern gespeicherten Format, siehe ADR-002).

## Benutzerkonto und Authentifizierung

- **FA-010** (Muss) Der Benutzer muss sich anmelden (Login), um die App bzw. seine Daten zu nutzen. Anmeldemethode: E-Mail/Passwort und/oder Passkey (Entscheid offen, siehe Architektur/ADR).
- **FA-011** (Muss) Nach dem Login bleibt der Benutzer angemeldet, damit QA-001/QA-002 eingehalten werden. Die Session bzw. das Token läuft nach ca. 14 Tagen ab. Ein Ablauf darf eine laufende Aufnahme nie unterbrechen. Auch nach Ablauf bleibt das lokale Aufnehmen und Bearbeiten ohne erneuten Login möglich; nur die Synchronisation pausiert bis zum erneuten Login.
- ~~**FA-012** (Kann) Die App kann zusätzlich per Fingerabdruck (Biometrie) geschützt werden.~~ *Verworfen: Fingerabdruck wird nicht umgesetzt.*
- **FA-013** (Muss) Es gibt keine Selbstregistrierung. Accounts werden manuell durch den Administrator per Backend-Befehl (z. B. CLI) angelegt.

## Accounts und Bereiche (Mandanten)

- **FA-020** (Muss) Es kann mehrere Accounts geben.
- **FA-021** (Muss) Jeder Account hat genau einen persönlichen Bereich für seine eigenen Aufnahmen. Dieser wird beim Anlegen des Accounts automatisch erstellt.
- **FA-022** (Muss) Zusätzlich gibt es gemeinsame Bereiche (z. B. „Band“), auf die mehrere Accounts Zugriff haben. Mitglieder eines Bereichs können dort Aufnahmen erstellen und hochladen sowie alle Aufnahmen des Bereichs ansehen und abspielen. Bearbeiten und löschen können sie nur ihre eigenen Aufnahmen. Bei jeder Aufnahme ist ersichtlich, welcher Account sie erstellt hat.
- **FA-023** (Muss) Ein Account kann Zugriff auf beliebig viele gemeinsame Bereiche haben und in der App zwischen seinem persönlichen Bereich und diesen Bereichen wechseln.
- **FA-026** (Soll) Der Benutzer kann eigene Aufnahmen von einem Bereich in einen anderen verschieben oder kopieren (z. B. vom persönlichen Bereich in „Band“). Tags werden im Zielbereich anhand des Namens übernommen bzw. dort neu angelegt; die Gruppe wird entfernt.
- **FA-024** (Muss) Gemeinsame Bereiche werden manuell durch den Administrator erstellt, und er weist ihnen Accounts zu (Einladung von Mitgliedern).
- **FA-025** (Muss) Für die Administration gibt es Backend-Befehle (z. B. CLI), mindestens zum Erstellen, Bearbeiten und Löschen von Accounts und Bereichen sowie zum Hinzufügen und Entfernen von Mitgliedern eines Bereichs.

## Desktop

- **FA-028** (Muss) Der Benutzer kann Riffic auch auf dem Desktop nutzen, insbesondere zum Gruppieren und Verwalten von Aufnahmen (Titel, Notizen, Gruppen, Tags, Bereiche). Es gelten dieselben Daten wie auf dem Smartphone (Synchronisation, FA-016).

## Synchronisation

- **FA-014** (Muss) Aufnahmen und Metadaten werden zuerst lokal auf dem Gerät gespeichert.
- **FA-015** (Muss) Lokale Daten werden automatisch im Hintergrund auf den Server bzw. in den Cloud-Speicher hochgeladen.
- **FA-016** (Muss) Die Synchronisation erfolgt in beide Richtungen: Daten vom Server werden auf das Gerät übertragen (z. B. bei neuem Gerät oder mehreren Geräten). Es werden alle Bereiche synchronisiert, auf die der Account Zugriff hat.
- **FA-018** (Muss) Bei Konflikten (derselbe Eintrag auf mehreren Geräten geändert) gewinnt die letzte Änderung.
- **FA-019** (Soll) Nicht alle Audio-Dateien müssen lokal vorliegen; Audio-Dateien, die nicht auf dem Gerät sind, werden bei Bedarf (z. B. beim Abspielen) vom Cloud-Speicher nachgeladen. Metadaten liegen immer vollständig lokal vor. Lokale Audio-Dateien werden nur manuell durch den Benutzer vom Gerät entfernt (nicht automatisch); die Kopie im Cloud-Speicher bleibt erhalten.

## Offene Fragen

- FA-028: Welche Funktionen braucht es auf dem Desktop zusätzlich: Abspielen, manueller Upload von Dateien (FA-017), MP3-Download (FA-027), Aufnehmen?
- FA-028: Muss der Desktop auch offline funktionieren, oder reicht Online-Betrieb?
- FA-027: Wo findet die Umwandlung nach MP3 statt (in der App oder im Backend)? → Architekturentscheid.
