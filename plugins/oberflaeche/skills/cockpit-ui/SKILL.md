---
name: cockpit-ui
description: Verbindliche Oberflächen-Regeln für Charles' eigene Apps (Dozenten-Cockpit, Seminar-Gamification-Portal, Tool-Stack, FRMD-PASN-Werkzeuge, U9-App). Nutze diesen Skill IMMER, wenn an einer dieser Apps etwas gebaut, umgebaut, gestaltet oder ergänzt wird — auch bei einer einzelnen neuen Karte, einem neuen Knopf oder einer neuen Liste, und auch dann, wenn nur von "Design", "Layout", "sieht komisch aus" oder "das passt nicht zum Rest" die Rede ist.
---

# Oberfläche für Charles' Apps

Alle Apps sind Einzeldatei-HTML, die Charles selbst über GitHub hochlädt.
Es gibt keinen Build-Schritt und kein Framework. Diese Regeln ersetzen jede
gestalterische Einzelentscheidung: Was hier steht, wird nicht neu abgewogen.

## Der Grundsatz

**Farbe gehört dem Status.** Die vier Statusfarben sind die einzigen bunten
Flächen. Die Hauptaktion wirkt durch Größe und Gewicht, nicht durch Farbe —
deshalb ist sie graphitschwarz. Wer eine fünfte Farbe einführen will, führt
in Wahrheit einen fünften Status ein und muss das erst begründen.

## Vorgehen

1. `assets/ui.css` als `<style>`-Block ganz oben in die Datei, vor allem
   anderen CSS. In einer App, die schon eigene Regeln hat: den Token-Block
   (`:root`) einsetzen und die vorhandenen Werte darauf umbiegen, nicht
   parallel führen.
2. Für jedes Element zuerst prüfen, ob es die Klasse schon gibt. Es gibt:
   `.karte`, `.karte-kopf`, `.karte.dringend`, `.btn`, `.btn-haupt`,
   `.btn-klein`, `.btn-gefahr`, `.btnreihe`, `.feld`, `.lbl-klein`,
   `.hinweis`, `.chip` (+ `-offen/-arbeit/-geliefert/-abgerechnet/-neutral`),
   `.chipreihe`, `.skel` (+ `.kurz/.mittel/.lang`), `.hilfe[data-tip]`,
   `.leer`, `.dropzone(.over)`, `.kennzahlen`, `.kennzahl`, `.balkenreihe`,
   `.balkenspur`, `.zahl`, `.frist-rot`, `.frist-gelb`.
3. Fehlt ein Bauteil, wird es in `ui.css` ergänzt und in `musterbogen.html`
   gezeigt — nicht als Einzelfall in der App gelöst.
4. `style="…"` direkt im HTML ist die Ausnahme und nur für Werte erlaubt,
   die aus Daten entstehen (Balkenbreite in Prozent, Sortierreihenfolge).

## Die Regeln

### Farbe
- offen `--offen` · in Arbeit `--arbeit` · geliefert `--geliefert` ·
  abgerechnet `--abgerechnet`. Dieselbe Bedeutung in jeder App.
- Frist-Ampel benutzt dieselben Farben: überfällig oder ≤3 Tage rot,
  ≤10 Tage gelb, sonst keine Farbe.
- Nie eine Hexzahl direkt schreiben. Immer die Variable.
- Farbe steht nie allein: der Chip trägt zusätzlich seinen Text, damit die
  Bedeutung auch ohne Farbwahrnehmung ankommt.
- Emoji ersetzt keinen Status. Chips statt 🔴🟡🟢.

### Größen und Abstände
- Abstände nur aus `--a1` … `--a7` (4/8/12/16/24/32/48). Nichts dazwischen.
- Hauptaktion 56 px hoch, normaler Knopf und **jedes** Eingabefeld 48 px,
  kleiner Knopf 40 px und nur direkt in einer Listenzeile.
- Am Handy ist die Hauptaktion volle Breite, am Desktop mindestens 260 px.
- Genau **eine** Hauptaktion je Bildschirm. Gibt es zwei gleichrangige, ist
  der Bildschirm falsch geschnitten.
- Fünf Schriftgrößen, mehr nicht: `--s-klein/-text/-karte/-teil/-seite`.

### Verhalten
- Laden zeigt `.skel`, **außer** der Text sagt etwas Inhaltliches
  („Suche Teams-Transkript …“, „Gamma erzeugt das Deck … (25 s)“).
  Ein anonymer Balken wäre dort ein Rückschritt.
- Jede Erklärung steckt in `.hilfe[data-tip]`. Kein Erklärabsatz im Interface.
- Jeder leere Zustand: ein Satz plus die passende Aktion. Vorbild:
  „Kein Seminar in Sicht.“
- Zahlen (Beträge, km, Stunden) rechtsbündig und mit `.zahl`.
- Tastaturfokus ist überall sichtbar; `outline:none` ist verboten.

### Sprache
- Neue Einträge heißen immer **erfassen**, nicht speichern/hinzufügen/anlegen.
- Der Knopf nennt die Handlung („Deck erzeugen“), und die Rückmeldung
  benutzt dasselbe Wort („Deck erzeugt“).
- Gleiche Dinge heißen überall gleich: Einstellungen (nicht Tools),
  Auftraggeber, Kategorie, Gesellschaft, Auftragsnummer, Zeitraum.
- Fehlermeldungen sagen, was schiefging und was jetzt hilft. Keine
  Entschuldigung, kein „Ein Fehler ist aufgetreten“.

## Wenn etwas unklar ist

Nachfragen statt raten — genauso wie im Ablage-Skill bei fehlendem
Auftraggeber. Insbesondere: eine neue Statusfarbe, ein zweiter Hauptknopf
auf einem Bildschirm oder eine sechste Schriftgröße werden nie still
eingeführt.

## Dateien

- `assets/ui.css` — Token und Bauteile, gehört in jede App.
- `assets/musterbogen.html` — zeigt alle Bauteile; im Browser öffnen, um
  eine Änderung gegen den Bestand zu prüfen.
