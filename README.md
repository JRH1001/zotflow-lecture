# ZotFlow – Lecture Pro Edition

Ein Fork-Patchset für den **Zotero-Reader in Obsidian (ZotFlow 1.7.1)**, gebaut für Tablet und Stift:

- **Stift markiert, Finger scrollt.** Ist ein Markieren-, Unterstreichen- oder Zeichen-Werkzeug aktiv, zeichnet nur der Stift. Der Finger scrollt und zoomt weiter, ein aufliegender Handballen wird ignoriert (solange der Stift aufliegt und 0,7 s danach). Ein Fingertipp wählt eine Annotation aus.
- **Preset-Leiste** (schwebend am unteren Rand, einklappbar, große Tippflächen): Überschrift 1–4 und Titel (Markierungen), Fakt, Fett, Beispiel, Definition, offene Frage (Unterstreichungen), dazu Notiz, Bild, Zeichnen und der Schalter „Pen only“. Die Belegung entspricht dem Lecture-Pro-Plugin (gelb/rot/grün/blau/violett/orange).
- **Automatisch zurück zu „Fakt“:** Nach einer Überschrift, einem Titel, Fett, Beispiel, Definition, Frage, einer Notiz, einem Bild oder Text springt das Werkzeug auf die gelbe Unterstreichung zurück. „Fakt“ selbst bleibt aktiv, Zeichnen ebenfalls.
- Einstellungen unter **ZotFlow → Reader → Annotation Tools** (je ein Schalter, Neustart des Readers nötig).

Alles andere ist der unveränderte ZotFlow 1.7.1. Die Edition ersetzt ZotFlow 1:1 (gleiche Plugin-ID `zotflow`): deine Bibliothek, Einstellungen und Synchronisation bleiben erhalten.

## So bekommst du das Plugin (ohne Programmieren)

**1. Repository anlegen (einmalig, am PC im Browser)**
1. Auf github.com anmelden → **New repository** → Name z. B. `zotflow-lecture-pro` → **Public** → *Create repository*.
2. **Add file → Upload files**: die Ordner `patches` und die Dateien `README.md`, `UPSTREAM.md`, `LICENSE` hineinziehen → *Commit changes*.
3. Der Ordner `.github` wird beim Hochladen oft übersprungen. Dann: **Add file → Create new file**, als Namen `.github/workflows/build.yml` eintippen (die Schrägstriche legen die Ordner an), den Inhalt der mitgelieferten Datei `workflow-build.yml` einfügen → *Commit changes*.

**2. Bauen lassen (GitHub macht das kostenlos in etwa 10–20 Minuten)**
1. Im Repository **Releases → Create a new release**, bei *Tag* eintippen `1.7.1-lp.1` → *Create new tag* → **Publish release**.
2. Unter **Actions** siehst du den Lauf „Build ZotFlow (Lecture Pro Edition)“. Ist er grün, hängen `main.js`, `manifest.json` und `styles.css` am Release.
3. Wird er rot: den Lauf öffnen, auf den roten Schritt klicken und mir die letzten Zeilen schicken.

**3. Aufs Tablet (am einfachsten mit BRAT)**
1. In Obsidian das Community-Plugin **BRAT** installieren und aktivieren.
2. BRAT → **Add beta plugin** → `DEIN-GITHUB-NAME/zotflow-lecture-pro` einfügen → *Add plugin*.
3. Obsidian neu starten, ZotFlow-Reader öffnen. Unten erscheint die Preset-Leiste; Einstellungen unter ZotFlow → Reader → Annotation Tools.

(Alternativ `main.js`, `manifest.json`, `styles.css` aus dem Release in `<Vault>/.obsidian/plugins/zotflow/` kopieren und Obsidian neu starten.)

## Hinweise
- Du solltest in den ZotFlow-Einstellungen **keine automatischen Updates** für dieses Plugin zulassen, sonst überschreibt Obsidian die Edition mit dem Original.
- Lizenz: AGPL-3.0 wie ZotFlow und der Zotero-Reader (siehe `LICENSE`). Die Patches stehen als Quelltext unter `patches/`.
- Pinned Versionen und Update-Vorgehen: `UPSTREAM.md`.
## Prüfstand (ehrlich)
**Geprüft (in einer Linux-Sandbox, gegen die festgeschriebenen Original-Stände):**
- Alle Patches greifen sauber auf frischen Checkouts von ZotFlow 1.7.1 und dem Reader-Stand `e6dfec2`.
- Die 12 neuen Tests (Stift-Logik, Presets, Auto-Rückkehr) und die 14 bestehenden Reader-Tests laufen (zwei weitere bestehende Tests brauchen Pakete, die in der Sandbox fehlen).
- Das Stylesheet kompiliert, PDF.js und der Reader-Webpack bauen durch und enthalten Leiste, Stift-Logik und Auto-Rückkehr. Einziger Fehler dort: ein Download von Zoteros Dokument-Worker aus Amazon S3, den die Sandbox-Netzwerksperre blockiert (in GitHub Actions ist das Netz offen).
- Das ZotFlow-Plugin besteht `tsc` und esbuild mit den Änderungen.

**Nicht geprüft:**
- Der gesamte Ablauf in Obsidian und **das Verhalten mit echtem Stift und Finger auf einem Tablet**. Android-WebView, Stift-Hardware und Handballen-Erkennung verhalten sich geräteabhängig. Dafür ist die Testliste unten da.
- Die Optik der Leiste (Größe, Überdeckung des Textes) auf deinem Bildschirm.

## Testliste für das Tablet (5 Minuten)
1. PDF öffnen, in der Leiste **F** (Fakt) tippen, mit dem Stift Text überstreichen → es entsteht eine gelbe Unterstreichung.
2. Mit dem **Finger** auf der Seite wischen → die Seite scrollt, es entsteht keine Markierung. Mit zwei Fingern zoomen.
3. Handballen beim Schreiben auflegen → die Seite darf nicht wegrutschen.
4. **H1** tippen, Text markieren → gelbe Markierung, danach ist wieder **F** aktiv.
5. **Note** tippen, auf die Seite tippen → Notiz, danach wieder **F**.
6. Schalter **Pen only** ausschalten → der Finger markiert wieder wie im Original.
