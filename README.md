# Zählerbuch als PWA für das iPhone

Die App speichert alle Daten **nur auf deinem iPhone** (im Speicher der Web-App). Auf dem Server liegt nur der Programmcode, keine Zählerstände.

## Inhalt

| Datei | Wozu |
|---|---|
| `index.html` | Die App |
| `manifest.webmanifest` | Name, Farben, Symbol für den Home-Bildschirm |
| `sw.js` | Macht die App offline nutzbar |
| `icons/` | App-Symbole |

**Nicht** die JSON-Datei mit deinen Zählerständen mit hochladen. Sie bleibt bei dir.

## 1. Veröffentlichen (einmalig, kostenlos)

Eine PWA muss über **https** ausgeliefert werden. Drei einfache Wege:

**GitHub Pages**
1. Auf github.com ein neues Repository anlegen (für kostenloses Pages muss es öffentlich sein).
2. ZIP entpacken und den Inhalt (`index.html`, `sw.js`, `manifest.webmanifest`, Ordner `icons`) hochladen.
3. Unter *Settings → Pages* den Branch `main` und den Ordner `/ (root)` wählen.
4. Nach etwa einer Minute ist die App unter `https://<name>.github.io/<repository>/` erreichbar.

**Netlify Drop** (am schnellsten): auf app.netlify.com/drop den entpackten Ordner hineinziehen. Du bekommst sofort eine https-Adresse.

**Cloudflare Pages**: Projekt anlegen und „Direct Upload“ wählen.

Die Adresse ist öffentlich erreichbar, aber ohne deine Daten nutzlos. Wähle bei Bedarf einen nicht erratbaren Namen.

## 2. Auf dem iPhone installieren

1. Die Adresse in **Safari** öffnen (nicht in einem anderen Browser).
2. **Teilen → Zum Home-Bildschirm → Hinzufügen**.
3. Die App ab jetzt **über das Symbol auf dem Home-Bildschirm** starten.

Beim ersten Start ist Internet nötig, damit Diagramme und Schriften einmalig geladen werden. Danach läuft die App auch ohne Netz.

## 3. Alte Daten einspielen

**Wichtig:** Die installierte App hat einen eigenen Speicher, getrennt von Safari. Spiel die Daten deshalb **in der App vom Home-Bildschirm** ein, nicht im Safari-Tab.

1. JSON-Datei (`zaehlerbuch-import-2025-2026.json`) auf das iPhone bringen, zum Beispiel per AirDrop oder iCloud Drive, und in der Dateien-App ablegen.
2. In der App: **Daten → Sicherung einspielen …** und die Datei wählen.
3. Unter **Tarife** den Wasserpreis eintragen und speichern.

## 4. Sicherung

Unter **Daten → Sicherung herunterladen (JSON)** öffnet sich das iOS-Teilen-Menü. Wähle **In Dateien sichern** (oder AirDrop, Mail an dich selbst). Mach das regelmäßig, zum Beispiel monatlich.

Die Daten gehen verloren, wenn du die App vom Home-Bildschirm löschst oder die Website-Daten in den Safari-Einstellungen entfernst. Mit der Sicherung stellst du alles in einer Minute wieder her.

## 5. Updates

Neue Version der Dateien hochladen und in `sw.js` die Zahl bei `CACHE` erhöhen (`zaehlerbuch-v2` usw.). Beim nächsten Start mit Netz lädt die App die neue Version, spätestens beim zweiten Öffnen.

## Hinweis zu den Schriften

Die Schriften kommen von Google Fonts und die Diagramme von cdnjs. Beide werden beim ersten Start geladen und danach auf dem Gerät zwischengespeichert. Wer das nicht möchte, kann die Dateien selbst mit hochladen und die Adressen in `index.html` und `sw.js` anpassen.

## Sicherung immer in denselben Ordner (Synology, per Kurzbefehl)

Eine Web-App darf unter iOS nicht selbständig in einen festen Ordner der Dateien-App schreiben. Das geht nur über einen Kurzbefehl, den du einmal anlegst:

1. **Kurzbefehle**-App öffnen, **+** tippen, den Kurzbefehl **Zählerbuch sichern** nennen (genau so, mit ä).
2. Aktion **Zwischenablage abrufen** hinzufügen.
3. Aktion **Datei sichern** hinzufügen. **Beim Sichern nachfragen** ausschalten, als Ziel den Ordner auf deiner DiskStation wählen, als Unterpfad `zaehlerbuch-sicherung.json` eintragen und **Überschreiben, falls vorhanden** einschalten.
4. In der App unter **Daten** auf **Sicherung per Kurzbefehl (fester Ordner)** tippen. Die App kopiert die Daten in die Zwischenablage und startet den Kurzbefehl.

Hinweise: Die DiskStation muss dabei im Heimnetz erreichbar und in der Dateien-App verbunden sein. Wird die Datei als `.txt` gespeichert, lässt sie sich trotzdem unter **Sicherung einspielen …** laden. Die Zwischenablage enthält danach deine Daten, bis du etwas anderes kopierst.
