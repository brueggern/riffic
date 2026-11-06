# Riffic – Hinweise für Claude

Riffic ist eine Mobile App zur Aufnahme von Songideen (Audio-Aufnahmen mit Titel und Notizen, Gruppierung, manuelle Einträge, Upload usw.).

Das Projekt befindet sich in der Konzeptphase. Der Benutzer schildert seine Ideen schrittweise; Claude legt sie im passenden Dokument unter `docs/` ab.

## Dokumentstruktur

| Dokument | Inhalt | ID-Präfix |
|---|---|---|
| `docs/01_Zielsetzung.md` | Vision, Zweck, Zielgruppe, Nutzen, Abgrenzung (was Riffic nicht ist) | `Z-` |
| `docs/02_Randbedingungen.md` | Vorgegebene Einschränkungen: Technik, Plattformen, Budget, Organisation, Recht | `RB-` |
| `docs/03_Qualitätsanforderungen.md` | Nicht-funktionale Anforderungen (Performance, Zuverlässigkeit, Usability, Sicherheit, Wartbarkeit …) | `QA-` |
| `docs/04_Funktionale_Anforderungen.md` | Was die App können muss, gruppiert nach Funktionsbereichen | `FA-` |
| `docs/05_ADR.md` | Architecture Decision Records: getroffene Entscheide mit Kontext, Alternativen und Begründung | `ADR-` |
| `docs/06_Architektur.md` | Architekturbeschreibung: Kontext, Bausteine, Datenmodell, Laufzeitsicht, Deployment | – |

## Vorgehen beim Erfassen

1. Aussagen des Benutzers dem richtigen Dokument zuordnen. Eine Aussage kann mehrere Dokumente betreffen (z. B. ein Technologie-Entscheid ist ein ADR und ggf. eine Randbedingung) – dann in beiden ablegen und gegenseitig per ID referenzieren.
2. Jeder Eintrag erhält eine fortlaufende, stabile ID (`FA-001`, `QA-001`, `ADR-001` …). IDs werden nie neu vergeben oder umnummeriert; verworfene Einträge werden als *verworfen* markiert statt gelöscht.
3. Formulierungen kurz und prüfbar halten. Funktionale Anforderungen als „Der Benutzer kann …“ bzw. „Die App muss …“. Qualitätsanforderungen möglichst messbar.
4. Bei Unklarheiten oder Widersprüchen zu bestehenden Einträgen kurz nachfragen statt raten. Offene Punkte im Abschnitt „Offene Fragen“ des jeweiligen Dokuments festhalten.
5. Priorität bei Anforderungen angeben, sofern bekannt: **Muss**, **Soll**, **Kann**.
6. Nur das dokumentieren, was der Benutzer gesagt hat. Eigene Vorschläge klar als Vorschlag kennzeichnen und erst nach Bestätigung übernehmen.
7. Nach jeder Erfassung committen und auf den Arbeitsbranch pushen.

## ADR-Format

Jeder ADR in `docs/05_ADR.md` hat: Titel, Status (Vorgeschlagen / Akzeptiert / Abgelöst durch ADR-xxx / Verworfen), Datum, Kontext, Entscheid, betrachtete Alternativen, Konsequenzen.

## Sprache und Schreibweise

- Dokumentation auf Deutsch.
- Umlaute ä, ö, ü verwenden (nicht ae, oe, ue).
- Kein Eszett: immer „ss“ statt „ß“.
