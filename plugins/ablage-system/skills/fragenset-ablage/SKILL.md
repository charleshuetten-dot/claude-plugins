---
name: fragenset-ablage
description: Legt Fragensets für Charles' Seminar-Gamification-Portal in OneDrive ab, benennt sie einheitlich und findet sie wieder. Nutze diesen Skill IMMER, wenn ein Fragenset, Quiz, Jeopardy-, Voting-, Escape-, Schätz-, Blitz- oder Wortwolken-Block erstellt, erweitert, überarbeitet, gespeichert, umbenannt oder gesucht wird — auch wenn nur beiläufig von "ablegen", "speichern", "neue Version" oder "wo liegt das Set …" die Rede ist, und auch dann, wenn zunächst nur eine JSON-Datei zum Download gebaut wird.
---

# Ablage und Benennung — Fragensets Gamification-Portal

Fragensets sind Portal-Material, kein Kursmaterial. Sie gehören deshalb **nicht**
unter `Kurse/` und folgen nicht dem Schema aus `ablage`, sondern liegen
alle unter einem eigenen Dach.

## Die Struktur

```
Dozenten-Cockpit/
└── Gamification-Portal/
    ├── Fragensets/<Bereich>/     ← hier liegen die .json-Dateien
    ├── Vorlagen/                 ← Formatmuster, leeres Gerüst
    └── Archiv/                   ← abgelöste Versionen
```

Innerhalb von `Gamification-Portal/` keine weiteren Ebenen erfinden. Wächst ein
Bereich, wird er ein neuer Ordner unter `Fragensets/` — nicht ein Unterordner im
Unterordner.

### Bereich

Ein Bereich ist entweder eine **Zielgruppe** oder ein **Fachthema**:

- Zielgruppen: `Kinder-6-9`, `Kinder-10-13`, `Azubis`, `Erwachsene-Allgemein`
- Fachthemen: `Versicherung`, `Finanzanlage`, `Finanzierung`, `Immobilienmakler`,
  `Kommunikation`, `Sonstiges`

Passt beides (z. B. ein Versicherungsquiz für Azubis), entscheidet das Fachthema —
danach sucht Charles im Seminarbetrieb. Ist der Bereich unklar, **nachfragen statt
raten**: ein falsch einsortiertes Set taucht beim nächsten Seminar nicht auf.

Existiert der Bereichsordner noch nicht, anlegen — aber ausschließlich direkt
unter `Fragensets/`.

## Dateinamen

Feste Form: **`Quiz_<Thema>-Set<N>_v<M>.json`**

- `<Thema>` — zwei bis vier Wörter, mit Bindestrichen verbunden. Der Ordner nennt
  bereits den Bereich; er gehört nicht noch einmal in den Dateinamen, außer die
  Zielgruppe ist Teil des Themas.
- `Set<N>` — laufende Nummer innerhalb eines Themas, immer mitführen, auch beim
  ersten Set. So passt ein späteres Set 2 ohne Umbenennung daneben.
- `v<M>` — Version, beginnend bei `v1`. Eine überarbeitete Fassung heißt `v2`,
  nicht "final", nicht "neu", nicht "überarbeitet".
- **Kein Datum** im Dateinamen. Das Änderungsdatum führt OneDrive selbst; ein
  Datum im Namen veraltet und erzeugt genau das Versionschaos, das hier vermieden
  werden soll.
- Verbotene Zeichen: `\ / : * ? " < > | # %`

Beispiele:

- `Quiz_Allgemeinwissen-Kinder-6-9-Set1_v1.json`
- `Quiz_Sachkunde-34d-Set2_v3.json`
- `Quiz_Bedarfsanalyse-Set1_v1.json`

Das Feld `"name"` **innerhalb** der JSON-Datei ist davon unabhängig: Es steht am
Beamer und darf ausgeschrieben und lesbar sein, z. B.
`"Allgemeinwissen für Kinder (6-9) - Set 2: Tiere, Körper & Märchen"`.

## Vorgehen beim Ablegen

1. **Erst die Datei bauen und lokal ablegen**, damit Charles sie herunterladen und
    prüfen kann (`/mnt/user-data/outputs/`, danach `present_files`).
2. **Prüfen, ob es das Set schon gibt** — mit `sharepoint_search` oder durch Lesen
    des Bereichsordners. Existiert eine Vorversion, die neue Fassung mit der
    nächsthöheren Versionsnummer hochladen. Niemals mit `conflictBehavior: replace`
    überschreiben; `fail` ist die richtige Einstellung, ein Namenskonflikt ist ein
    Hinweis, kein Hindernis.
3. **Hochladen** nach `Fragensets/<Bereich>/` (Microsoft-365-Connector,
    `sharepoint_upload_file`).
4. **Vollständigen Pfad nennen**, damit Charles ihn nachvollziehen kann.
5. Die abgelöste Version erst nach `Archiv/` verschieben, wenn die neue geprüft
    ist — und nie ungefragt löschen.

### Bekannte IDs (Abkürzung, kein Ersatz für die Suche)

OneDrive von Charles, `optimagruppeag-my.sharepoint.com`:

| Ordner | itemId |
|---|---|
| driveId (gesamtes Laufwerk) | `b!wQQoktPNzEGI2AG-9oQFvuOhBXqahkJOq30Rlqn-7LHIinO4kKxeTLBAoIka3lOj` |
| `Gamification-Portal` | `01AJ6YK2ORUM7APIZCNVA3LU7RCU6THZ7H` |
| `Fragensets` | `01AJ6YK2J2SFIWH2DPUBAY62EIGQXD6QAD` |
| `Fragensets/Kinder-6-9` | `01AJ6YK2IW4SIHB2XG6RB2KHD5GIQJQGUC` |
| `Vorlagen` | `01AJ6YK2JTKKQSCLW2TBC2JMCNAZCEKCV6` |
| `Archiv` | `01AJ6YK2K7AAHEZNH3PZD3BIOSHPJLVBYJ` |

Schlägt eine ID fehl (Ordner umbenannt oder verschoben), mit
`sharepoint_folder_search` neu auflösen statt raten.

## Vor dem Hochladen prüfen

Eine Datei, die das Portal nicht laden kann, ist schlimmer als gar keine — der
Fehler fällt erst im Seminar auf. Deshalb vor jedem Upload:

- Gültiges JSON, UTF-8, **keine Kommentare**, kein Text drumherum.
- Blockstruktur und Blockgrenzen wie in den Projektvorgaben (Jeopardy 3-4
  Kategorien à 3 Fragen, Voting 3-5, Escape genau 5 Rätsel, Schätzen 3-5, Blitz
  4-8, Wortwolke 1-3).
- `schaetzen[].antwort` ist eine reine Zahl, keine Zeichenkette, keine Einheit.
- `blitz[].richtig` ist ein Index ab 0 und zeigt auf eine existierende Option.
- `escape.raetsel[].loesung` enthält alle plausiblen Schreibweisen (mit und ohne
  Artikel, Ziffer und ausgeschriebene Zahl, gängige Synonyme); verglichen wird
  ohne Groß- und Kleinschreibung.
- Jedes Rätsel hat `"bild"`, notfalls `null`.
- Keine Frage doppelt innerhalb einer Datei — und bei einem Folgeset auch nicht
  gegen die bereits abgelegten Sets desselben Bereichs.

## Mehrere Sets statt eines großen

Die Blockgrenzen sind pro Datei bindend. Sollen mehr Fragen dazukommen, als in
die Blöcke passen, entsteht ein **neues Set** im selben Bereich
(`…-Set2_v1.json`) — kein aufgeblähtes Einzelset und keine erfundenen
Zusatzblöcke. Jedes Set bleibt für sich spielbar.
