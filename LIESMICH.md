# Design Summit 2026 – Org Chart (Web-Formular)

Lieferanten bekommen einen Link, tragen ihr Design-Team ein, laden am Ende
eine Datei herunter und schicken sie per E-Mail an
**designconnects@delta-sport.com**. Wir importieren die Dateien und bekommen
Organigramm, Excel und PDF.

Es wird **nichts automatisch verschickt** und es gibt keinen Server. Alle
Eingaben liegen nur im Browser dessen, der die Seite geöffnet hat.

---

## 1. Die zwei Links

| Für wen | Link |
|---------|------|
| **Lieferanten** | `https://alexiiio2012.github.io/summit-org/` |
| **Wir (Admin)** | `https://alexiiio2012.github.io/summit-org/?admin` |

Beide Ansichten kommen aus denselben Dateien; `?admin` schaltet um.
Im Admin gibt es oben den Knopf **„Lieferanten-Link kopieren"**.

Der Admin-Bereich hat keine PIN mehr. Das ist kein Leck: Er zeigt nur, was im
eigenen Browser gespeichert ist. Ein Lieferant, der `?admin` anhängt, sieht
also höchstens seine eigenen Einträge – nie die anderer Firmen.

---

## 2. Ablauf für die Lieferanten

1. Link öffnen, **Firmennamen** eingeben, „Start".
2. **Jede Person** erfassen und „Person hinzufügen" drücken. Nur der Name ist
   Pflicht.
3. Oben **„Datei herunterladen"**. Danach erscheint ein Fenster mit der
   Adresse, einem Knopf „E-Mail öffnen" (Empfänger und Betreff sind
   vorausgefüllt) und dem Hinweis, die Datei anzuhängen.

Was dabei hilft:

- **Die Leiste oben** zeigt jederzeit, wie viele Personen erfasst sind und ob
  die Datei schon heruntergeladen wurde. Wird danach noch etwas geändert,
  springt sie auf „Seit dem letzten Download geändert".
- **Vergessene Eingaben:** Steht beim Download noch eine Person im Formular,
  die nicht hinzugefügt wurde, fragt die App nach.
- **Neu laden oder später weitermachen** geht: Firma und Personen bleiben im
  Browser gespeichert.
- „Ändern" neben dem Firmennamen **benennt um** (z. B. bei Tippfehler), legt
  keine zweite Firma an.
- Sprache EN/DE oben rechts, Vorgabe ist Englisch.

**Die Felder:**

| Feld | Pflicht | Inhalt |
|------|---------|--------|
| Name | ja | — |
| E-Mail, Telefon | nein | E-Mail wird auf Plausibilität geprüft |
| Core Categories / product groups | nein | Die **erste** Angabe bestimmt die Gruppe im Organigramm |
| Languages | nein | Vorauswahl German, English, Mandarin |
| 3D Software | nein | Vorauswahl SolidWorks, Rhino 3D, KeyShot |
| 2D Software | nein | Vorauswahl Adobe Photoshop, Illustrator, InDesign |
| AI Software | nein | Vorauswahl Vizcom, Claude, ChatGPT, Google Gemini |
| Team responsible | nein | Wer angehakt ist, steht im Organigramm oben |

Jede Auswahlzeile hat ein Freitextfeld für eigene Einträge.

Die Datei heißt `design-summit-2026_<firma>.json`. Sie enthält nur die Werte,
die tatsächlich ausgewählt sind – Tippfehler, die der Lieferant wieder
abgewählt hat, landen nicht in unseren Filterlisten.

---

## 3. Eingegangene Dateien übernehmen (Admin)

*Daten & Einstellungen → JSON-Dateien importieren*, dann **alle Dateien auf
einmal** auswählen.

- Eine Meldung fasst zusammen, wie viele Dateien und Personen übernommen
  wurden, und nennt Dateien, die nicht lesbar waren.
- Schickt ein Lieferant **zweimal**, fragt die App: *Zusammenführen* ergänzt
  nur fehlende Personen (erkannt über Name + E-Mail), *Abbrechen* übernimmt
  diese Datei nicht.
- Vor dem Import wird **ein** Wiederherstellungspunkt für den ganzen Stapel
  angelegt.

Danach wie gewohnt: Organigramm, Filter, **Excel-Arbeitsmappe**,
**Organigramm als PDF**.

---

## 4. Speicherung im Admin

Der Admin-Stand liegt im Browser, mit dem du `?admin` öffnest – auf einem
anderen Rechner oder in einem anderen Browser ist er nicht da.

- **Regelmäßig *JSON-Sicherung → Sicherung speichern*.** Wer die Browserdaten
  löscht, verliert sonst den Stand. Die Lieferanten-Dateien aus dem Postfach
  sind ein zweites Backup: Sie lassen sich jederzeit neu importieren.
- Wiederherstellungspunkte: bei jedem Öffnen und vor jedem Import, die fünf
  neuesten bleiben.
- Rote Hinweise: **„Kein Speicher"** = privater Modus, **„Speicher voll"** =
  letzte Eingaben nicht gespeichert, sofort sichern.

Lieferanten-Formular und Admin nutzen getrennte Speicher. Wenn du das Formular
im eigenen Browser ausprobierst, landet das nicht in deinem Admin-Bestand.

---

## 5. Dateien im Repo

| Datei / Ordner | Zweck |
|----------------|-------|
| `index.html`, `app.css`, `app.js` | Die App (beide Ansichten) |
| `sw.js` | Baut den Offline-Speicher der alten iPad-Version ab – siehe unten |
| `fonts/` | Mulish, lokal (SIL Open Font License 1.1) |
| `vendor/` | xlsx, html2canvas, jsPDF – lädt nur der Admin |
| `icons/` | Browser-Symbol |
| `_lokal_testen.ps1` | Testserver für den Windows-Rechner, nicht Teil der App |
| `.nojekyll` | Sorgt dafür, dass GitHub Pages die Ordner unverändert ausliefert |

Es gibt keine Verbindung nach außen: kein CDN, keine Google-Fonts, kein Tracking.

**Zu `sw.js`:** Die frühere iPad-Version hat sich als Offline-App
eingerichtet und die Seite aus einem eigenen Speicher ausgeliefert. Wer sie
einmal geöffnet hat, würde ohne `sw.js` dauerhaft den alten Stand sehen. Die
jetzige `sw.js` räumt das beim nächsten Aufruf ab und lädt die Seite neu.
**Nicht löschen.** Nach Änderungen an der App ist kein Hochzählen von
Versionen mehr nötig – GitHub Pages liefert direkt aus (ggf. einmal mit
Strg+F5 neu laden).

---

## 6. Vor dem Versand testen

Rechtsklick auf `_lokal_testen.ps1` → „Mit PowerShell ausführen". Der Browser
öffnet `http://localhost:8099/` (Lieferanten-Ansicht); `http://localhost:8099/?admin`
ist die Admin-Ansicht.

---

## 7. Organigramm-Logik

**Wurzel:** Wer **Team responsible** angehakt hat, steht oben. Sind mehrere
Personen so markiert, wird die erste zur Wurzel, die anderen behalten ihre
Kennzeichnung. Ist niemand markiert, bildet ein Firmenknoten die Wurzel.

**Gruppierung:** Maßgeblich ist die **erste** Kategorie einer Person. Die Zahl
im schwarzen Kreis am Label ist die Personenzahl der Gruppe.

- Kategorien mit **mehreren** Personen: eigene Zeile, Label links, Personen
  nebeneinander, Spalten bündig.
- Kategorien mit **genau einer** Person: gemeinsam in der letzten Zeile.
- Ohne Kategorie: Sammelgruppe **„Sonderprojekte"** (*Special projects*),
  änderbar in `app.js` beim Schlüssel `chart.noCat`.

Filter blenden Nichttreffer ab, entfernen sie aber nicht. Zoomen über
**+ / − / Einpassen**; der PDF-Export ist immer vollständig und ungefiltert.
