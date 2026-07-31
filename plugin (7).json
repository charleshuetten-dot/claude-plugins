---
name: dozenten-reiseplanung
description: Plant Dienstreisen zu Seminarterminen (Bahn vs. Auto) und erstellt danach die vollständige Reisekostenabrechnung für die SCC Service Center GmbH. Nutze diesen Skill IMMER, wenn der Nutzer eine Reise zu einem Seminar, einer Schulung, einer Prüfung oder einem beruflichen Termin plant, nach Bahnverbindungen oder Fahrtkosten fragt, eine Vorabendanreise erwähnt, oder eine Reisekostenabrechnung, Spesenabrechnung, km-Abrechnung oder Verpflegungspauschalen braucht — auch wenn er nicht ausdrücklich "Reiseplanung" sagt.
---

# Dozenten-Reiseplanung & Reisekostenabrechnung

Zwei Anwendungsfälle: **(A) Reise planen** (vor dem Termin) und **(B) Reise abrechnen** (nach dem Termin). Erkenne aus der Anfrage, welcher gemeint ist. Antworte auf Deutsch.

## Feste Rahmenbedingungen des Nutzers

- Startpunkt: Köln-Dellbrück (Zuhause), Start-Bahnhof **Köln-Dellbrück**, außer der Nutzer nennt einen anderen Ausgangsort.
- Ankunft am Seminarort: **60 Minuten Puffer** vor Seminarbeginn einplanen.
- Ticketwahl: **Hinfahrt Sparpreis mit Zugbindung ok, Rückfahrt immer Flexpreis** (Seminarende kann sich verschieben).
- Stammauftraggeber: **Going Public Akademie** (Berlin) und **BWV Rheinland** — bei diesen keine Grunddaten mehr abfragen, nur Ort/Termin des konkreten Seminars.
- Vorabendanreise, sobald die Fahrzeit zum Seminarort **mehr als 1 Stunde** beträgt (mit dem jeweils betrachteten Verkehrsmittel).
- Rückreise direkt am Ende des Seminartages — keine zweite Übernachtung.
- Hotel bucht und zahlt der **Auftraggeber** (in der Regel inkl. Frühstück → Kürzung der Verpflegungspauschale beachten).
- Bahn: bucht der Nutzer selbst, Kosten werden voll erstattet. **BahnCard 50, 2. Klasse.** Möglichst wenige Umstiege; Direktverbindung bevorzugen, wenn der Zeitverlust moderat ist.
- Sitzplatzreservierung Bahn: **Ruhebereich, Fensterplatz, möglichst letzte Reihe** (keine Sitze dahinter), **kein Tischplatz**. Bei der Buchungsempfehlung immer an die Reservierung mit diesen Kriterien erinnern.
- Auto: Abrechnung mit **0,38 €/km** (Firmenregelung der SCC Service Center GmbH).
- Abrechnung läuft über die SCC Service Center GmbH (Lohnabrechnung), Buchhaltung in DATEV Unternehmen online.

## (A) Reise planen

1. **Termin erfassen.** Frage nach Ort, Datum und Seminarzeiten (Standard, wenn nichts genannt: 9:00–17:00 Uhr) — oder lies den Termin aus dem **Outlook-Kalender** (Microsoft-365-Tools) aus, wenn der Nutzer darauf verweist ("mein Seminar nächste Woche"). Prüfe im Kalender auch, ob der Nutzer am Vortag bereits woanders ist (anderer Ausgangsort!). **Bei Terminkonflikten mit bestehenden Einträgen immer nachfragen, nie eigenmächtig verschieben.**
2. **Auto-Route ermitteln.** Per Websuche: Entfernung (km, einfache Strecke) und Fahrzeit Köln → Zielort. Kosten = km × 2 × 0,38 €.
3. **Bahnverbindung ermitteln.** Per Websuche/bahn.de: beste Verbindung (wenige Umstiege), Fahrzeit, Preis. Preise als Flexpreis UND Sparpreis nennen, jeweils **mit BahnCard 50** (Flexpreis −50 %, Sparpreis −25 %). Wenn keine aktuellen Preise auffindbar: realistisch schätzen und als Schätzung kennzeichnen.
4. **Vorabendanreise prüfen.** Fahrzeit > 1 h → Anreise am Vorabend einplanen; Hinweis, dass der Auftraggeber das Hotel bucht (ggf. Erinnerung formulieren, falls noch nicht bestätigt).
5. **Vergleich ausgeben.** Kompakte Tabelle: Kosten, reine Fahrzeit, Tür-zu-Tür-Zeit, Umstiege, Arbeitszeit im Zug nutzbar (ja/nein). Danach eine klare **Empfehlung mit Begründung** (Kosten sind wichtig, aber nutzbare Arbeitszeit im Zug und Stressfaktor mitgewichten).
6. **Auf Wunsch umsetzen:**
   - Bahn: bahn.de-Link mit der konkreten Verbindung erstellen (https://www.bahn.de/buchung/fahrplan/suche mit Parametern bzw. Verbindungsdaten nennen), damit der Nutzer nur noch kaufen muss. Erinnere an BahnCard 50 im Buchungsprofil.
   - Kalender: **Outlook-Termine** (Microsoft-365-Tools) für Anreise (ggf. Vorabend), Seminar-Reiseblock und Rückreise anlegen. Namenskonvention: Seminar = `<Auftraggeber> <Seminartitel>`, An-/Abreise = `Anreise <Auftraggeber> <Seminartitel>` bzw. `Abreise …`. **Im Ort/Standort-Feld immer die exakte Seminaradresse eintragen** (Straße, Hausnummer, PLZ, Ort) — die Reisekosten-App des Nutzers übernimmt sie beim Import wörtlich und berechnet daraus automatisch die km. In die Beschreibung die Eckdaten schreiben (Verbindung/Route, km, Zweck, Auftraggeber, Buchungsstatus) — das ist später die Datenbasis für die Abrechnung.

## (B) Reise abrechnen

Ziel: vollständige Reisekostenabrechnung als Ersatz für N2F. **Rhythmus: 1× pro Quartal als Sammelabrechnung** über alle Reisen des Quartals. Nach jeder einzelnen Reise werden nur die Daten festgehalten (Kalendereintrag/Notiz); das Abrechnungsdokument entsteht am Quartalsende — außer der Nutzer wünscht ausdrücklich eine Einzelabrechnung.

1. **Daten sammeln.** Aus dem Gespräch, dem Kalender (Reiseblöcke aus Phase A) und ggf. hochgeladenen Belegfotos (Bahnticket, Parkbeleg, Taxi …) — Claude liest Belegfotos direkt aus (Betrag, Datum, Anbieter). Fehlendes gezielt nachfragen: Abfahrts-/Rückkehrzeiten (für Pauschalen relevant!), Verkehrsmittel, Auftraggeber/Seminar.
2. **Positionen berechnen** nach `references/reisekosten-regeln.md` — diese Datei VOR jeder Abrechnung lesen.
3. **Abrechnung erstellen.** Word- oder PDF-Dokument (docx-/pdf-Skill nutzen) mit Briefkopf "SCC Service Center GmbH", plus eine Excel-Übersicht bei mehreren Reisen. Inhalt: Reisedaten (Anlass, Ziel, Zeiten), Einzelpositionen (Fahrtkosten, Verpflegungspauschalen inkl. ausgewiesener Kürzungen, sonstige Belege), Summen, Belegliste. Datei zum Download bereitstellen.
4. **Hinweis zur Ablage:** Belege und Abrechnung gehören in DATEV Unternehmen online (dort erfolgt die GoBD-konforme Archivierung); die Erstattung läuft über die Lohnabrechnung der GmbH.

## Grundsätze

- Rechne transparent: jede Pauschale und Kürzung einzeln ausweisen, nie nur Endsummen.
- Bei steuerlichen Detailfragen (z. B. Behandlung des 0,38-€-Satzes oberhalb des steuerfreien km-Satzes) auf den Steuerberater verweisen, nicht selbst abschließend beurteilen.
- Pauschalensätze können sich jährlich ändern — bei Unsicherheit die aktuellen Sätze per Websuche verifizieren, bevor abgerechnet wird.
