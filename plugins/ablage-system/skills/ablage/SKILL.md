---
name: ablage
description: Legt Dateien fuer Charles ab, benennt sie einheitlich und findet sie wieder. Nutze ihn, wenn etwas erstellt, gespeichert, umbenannt, verschoben oder gesucht wird, auch bei der Frage, wo etwas liegt.
---

# Ablage

Verbindliche Struktur für alles, was für Charles entsteht. Wird sie nicht
eingehalten, wachsen an allen Stellen neue Ordnerbäume — genau das Problem, das
dieser Aufbau löst. Auch das Dozenten-Cockpit liest und schreibt exakt diese
Pfade.

## Die Grundregel

**Niemals einen neuen Ordner auf oberster Ebene anlegen.** Es gibt sechs, und
sie stehen bereits. Alles Neue geht in einen davon oder tiefer.

## Zwei Ablageorte

**Geschäftlich → OneDrive des Optima-Kontos** (`charles.huetten@optima.ag`,
Microsoft-365-Connector). Dort liegen die fünf geschäftlichen Dächer.

**Privat → Google Drive** (Google-Drive-Connector). Privates gehört bewusst
nicht in den Firmen-Tenant: Die Optima Gruppe AG ist eine eigene juristische
Person, der Tenant gehört der Gesellschaft. Der leere Ordner `Privat` im
Optima-Konto ist **kein** Ablageort für Privates.

Steht der passende Connector nicht zur Verfügung, sag das offen, statt
ersatzweise woanders abzulegen.

## Die sechs Ordner im Optima-Konto

| Ordner | Was hineingehört |
|---|---|
| `Dozentur` | Alles zur Lehrtätigkeit — siehe unten |
| `Optima` | Kundenberatung, Schadenfälle, Provisionen, Gesellschaftsthemen (Aufsichtsrat, Hauptversammlung, Behörden), Verträge |
| `SCC` | Was noch zur SCC Service Center GmbH gehört (Bestand wird zum Jahreswechsel abgegeben — keine neuen Strukturen anlegen) |
| `FRMD PASN` | Framed Passion — Aufträge, Motive, Shop |
| `Coaching` | Coaching-Tätigkeit |
| `Privat` | Leer lassen — Privates geht nach Google Drive |

Unterordner unterhalb dieser Ebene dürfen entstehen, wenn sie gebraucht werden.
Erfinde sie aber nicht auf Vorrat.

## Dozentur im Detail

```
Dozentur/
├── Kurse/<Auftraggeber>/<Kategorie>/<Gesellschaft>/<Kurs>/
│      ├── Folien/
│      ├── Übungen-Fälle/
│      ├── Teilnehmerunterlagen/
│      └── Meetings/
│             └── Memos/
├── DIHK/<Thema>/Klausuren/
├── IHK-Sachkundeprüfungen/
│      ├── 34d Versicherungen/
│      ├── 34f Finanzanlagen/
│      └── 34i Immobiliardarlehen/
├── Aufträge/<Jahr>/
├── Abrechnungen/<Jahr>/
├── Newsletter/<Jahr>/
├── Skills/<skill-name>/
├── Sicherung/
└── Alte Unterlagen/
```

### Erlaubte Werte

- **Auftraggeber** (die Akademie, mit der abgerechnet wird):
  Going Public Akademie · BWV Rheinland · IHK Köln · Zinal · Global Finanz ·
  FHDW Mettmann
- **Kategorie:** Versicherung · Finanzanlage · Finanzierung · Immobilienmakler ·
  Kommunikation · Sonstiges
- **Gesellschaft:** Allgemein · Allianz · Astra · ÖVB — oder der tatsächliche
  Name. Steht keine fest, `Allgemein` verwenden.
- **Kurs:** der Seminarname, wie ihn der Auftraggeber führt, z. B.
  `Beratung & Verkauf`. Läuft bei einer Gesellschaft nur ein einziges Seminar,
  trägt der Ordner trotzdem dessen Namen — nicht `Allgemein`.

Zur Einordnung: Die Gesellschaft beauftragt die Akademie, die Akademie beauftragt
Charles. **Auftraggeber ist immer die Akademie**, auch wenn die Mail von der
Gesellschaft kam oder deren Name im Betreff steht.

Unter `Meetings/` liegen Agenden und Protokolle zum Kurs. Der Unterordner
`Memos/` ist für die strukturierten Notizen reserviert, die das Cockpit aus
Diktat oder Teams-Transkript erzeugt — dort schreibt die App hin, dort wird
nichts von Hand abgelegt.

## Dateinamen

Feste Form: **`<Typ>_<Kurzbeschreibung>_v<N>.<Endung>`**

Der Ordner nennt bereits Bereich, Auftraggeber, Kategorie und Gesellschaft —
die gehören deshalb **nicht** noch einmal in den Dateinamen.

| Kürzel | Wofür |
|---|---|
| `Folien_` | Präsentationen |
| `Übung_` | Fallübungen, Aufgaben |
| `Handout_` | Teilnehmerunterlagen |
| `Skript_` | Ausführliche Textunterlagen |
| `Klausur_` | DIHK-/IHK-Prüfungsaufgaben |
| `Auftrag_` | Auftragsbestätigungen |
| `Briefing_` | Newsletter-Ausgaben |

Beispiele: `Folien_Bausparen_v3.pptx` · `Übung_Bedarfsanalyse_v1.docx` ·
`Klausur_Vertriebsplanung-F2026_v2.pdf`

Regeln:
- Version **immer** mitführen, beginnend bei `_v1`. Neue Fassung heißt `_v2` —
  nicht „final", nicht „neu", nicht „überarbeitet".
- **Kein Datum** im Dateinamen. Das Änderungsdatum führt OneDrive selbst; ein
  Datum im Namen veraltet und erzeugt genau das Versionschaos, das vermieden
  werden soll. Ausnahmen sind Newsletter (`Briefing_<JJJJ-MM-TT>_…`) und
  Sicherungen, weil dort das Datum der Inhalt ist.
- Verbotene Zeichen: `\ / : * ? " < > | # %`
- Kurzbeschreibung in zwei bis vier Wörtern, mit Bindestrichen verbunden.

## Vorgehen beim Ablegen

1. **Erst prüfen, ob es die Datei schon gibt.** Existiert eine Vorversion, die
   neue Fassung mit der nächsthöheren Versionsnummer anlegen — nicht
   überschreiben.
2. Die vorherige Version nach `Dozentur/Alte Unterlagen/` verschieben, sobald
   die neue geprüft ist. Nie ungefragt löschen.
3. Fehlt ein Ordner der Struktur, ihn anlegen — aber ausschließlich innerhalb
   des vorgesehenen Aufbaus.
4. Nach dem Ablegen den vollständigen Pfad nennen.

## Skill-Dateien

Die Dateien eines Skills — `SKILL.md` und seine Begleitdateien — gehören nach:

```
<Dach>/Skills/<skill-name>/
```

Das Dach ist der Bereich, dem der Skill dient. Übergreifende Skills wie `ablage`
selbst liegen unter `Dozentur/Skills/`, weil dort ohnehin die meisten liegen und
auf oberster Ebene kein neuer Ordner entstehen darf.

**Die Namenskonvention gilt hier nicht.** Skill-Dateien behalten ihre exakten
Namen (`SKILL.md`, `quellen.md`, `themen.md`), sonst findet Claude sie nicht.
Keine Typ-Kürzel, keine Versionsnummer im Dateinamen.

**Verhältnis der beiden Fassungen:** OneDrive ist die **Quelle**, der in Claude
hochgeladene Skill die **laufende Kopie** — dasselbe Verhältnis wie GitHub zu
Cloudflare beim Cockpit. Wird ein Skill geändert, wird **beides** nachgezogen.
Eine Fassung allein zu aktualisieren erzeugt genau die zweite Wahrheit, die diese
Ablage verhindern soll.

## Was ausdrücklich NICHT nach OneDrive gehört

**Programmcode.** `index.html`, `sw.js`, `claude-proxy.js`, `gamma-proxy.js` und
alles andere aus dem Cockpit gehören ins GitHub-Repo
`charleshuetten-dot/Reisekosten-Cockpit`. Eine Kopie in OneDrive wäre eine
zweite Wahrheit und damit schlimmer als kein Ordner.

**Die Windows-Ordner.** `Desktop`, `Dokumente` und `Bilder` im Optima-Konto sind
die Windows-Ordnersicherung. Dort nichts hineinlegen und nichts daraus
verschieben — das bricht die Synchronisierung.

**System-Ordner.** `Besprechungen`, `Whiteboards`, `Aufnahmen`, `Attachments`,
`Microsoft Copilot Chat Files` und ähnliche legen Microsoft-Dienste selbst an.
Nicht anfassen, nicht befüllen.

## Altbestand

Aus Jahrzehnten gewachsene Ordner liegen überwiegend in seinem **persönlichen**
OneDrive und in Google Drive. Sie werden **nicht** in einem Rutsch umgezogen.
Wandert etwas, dann nur, wenn er es ohnehin gerade anfasst. Schlage einen Umzug
nur vor, wenn eine Datei aktiv gebraucht wird.

## Wenn etwas unklar ist

Fehlt Bereich, Auftraggeber, Kategorie oder Gesellschaft, **nachfragen statt
raten**. Eine falsch einsortierte Datei ist schlechter als eine kurze Rückfrage —
sie taucht im Cockpit am falschen Ort auf und wird später nicht gefunden.

Einzige Ausnahme: Ist nur die Gesellschaft unklar, `Allgemein` verwenden.

## Sonderfälle

- **Auftragsbestätigungen** → `Dozentur/Aufträge/<Jahr>/`, benannt
  `Auftrag_<Auftraggeber>_<Auftragsnummer>.pdf`
- **Bahntickets** → `Dozentur/Aufträge/<Jahr>/`, benannt
  `Bahn_<Buchungsnummer>_<Dateiname>`
- **Rechnungen an Auftraggeber** → `Dozentur/Abrechnungen/<Jahr>/`
- **DIHK-Klausuren** → `Dozentur/DIHK/<Thema>/Klausuren/`, nicht unter `Kurse/`
- **Kundenfälle der Sachkundeprüfungen** → in den jeweiligen Ordner unter
  `Dozentur/IHK-Sachkundeprüfungen/`
