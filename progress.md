# Fortschritt – Krypto-Dashboard

Stand: 2026-11-14 (zwei weitere lokale Claude-Skills geprüft und eingerichtet: `video-edit` und `coingecko`, siehe Abschnitt "Lokale Claude-Skills" unten; beide erfolgreich getestet)

## Was ist das Projekt?
Ein eigenes HTML-Dashboard mit Live-Krypto-Kursen (6 Coins: Stellar/XLM, XDC Network, VELO, Canton Network, Zebec Network, SHX Stronghold). Lernprojekt von Alen mit Claude als Tutor.

## Wo läuft es?
- Live über GitHub Pages: https://allen1977-maker.github.io/Krypto-Dashboard/
- Code-Repo: https://github.com/allen1977-maker/Krypto-Dashboard (öffentlich, Branch `main`)

## Was kann es aktuell?
- Live-Preise in EUR über die CoinGecko-API, 24h-Veränderung
- Eingebettete TradingView-Mini-Charts je Coin (statt einfacher Sparkline)
- Farbiger Akzentstreifen auf jeder Coin-Karte
- Kurse werden im Browser zwischengespeichert (localStorage) – beim Öffnen sofort sichtbar, danach Hintergrund-Update
- Auto-Refresh alle 15 Minuten (vorher 60 Sekunden, auf Alens Wunsch verlängert); Statuszeile zeigt nur noch "Stand: [Uhrzeit]", ohne Refresh-Hinweis im Text
- Fester Hintergrund über die ganze Seite: stilisierte Punkt-Weltkarte mit 7 Hubs (inkl. Afrika und Australien) und animierten Transfer-Impulsen, die zwischen den Hubs entlanglaufen. Reines SVG/CSS (`position: fixed`, hinter allem Inhalt), keine zusätzliche Bibliothek. Dezente Länder-Flaggen zur Orientierung (ohne Namen, nur Flagge): 🇺🇸 Amerika, 🇧🇷 Lateinamerika, 🇪🇺 EU, 🇨🇭 Schweiz, 🇷🇺 Russland, Afrika (Text statt Flagge, da keine Kontinent-Flagge existiert), 🇦🇺 Australien. Labels wachsen bewusst zur Kartenmitte hin (nicht zum Rand), damit sie bei breiten Bildschirmen nicht abgeschnitten werden. Hinweis: Flaggen-Emojis zeigen unter Windows nur als Buchstabenkürzel (z. B. "EU" statt 🇪🇺), da Windows keine Flaggen-Glyphen rendert – auf Handy/Mac erscheinen echte Flaggen. Bewusst so belassen (Alens Entscheidung).
- `<h1>` hat `margin-top: 28vh` (mobil fest 60px), damit oben ein Streifen der Weltkarte sichtbar bleibt. Wichtig: feste px-Werte reichen bei breiten PC-Bildschirmen nicht, weil die Karte (`preserveAspectRatio="slice"`) sich an der Bildschirmhöhe hochskaliert – vh-Einheit skaliert proportional mit und funktioniert deshalb auf PC und Handy gleichermaßen.
- Karte passt sich per JS (`karteAnpassen()`, `index.html`) responsiv an: ab 480px Breite (PC/Tablet) wird `preserveAspectRatio` auf `xMidYMid meet` umgeschaltet (Karte komplett eingepasst, kein Beschnitt mehr an den Rändern – USA/Australien jetzt immer sichtbar), unter 480px (Handy) bleibt `slice` (bildschirmfüllend, wie von Alen am Handy bereits für gut befunden).
- Abschnitt "📱 Tangem erklärt": 4 Erklärvideos (Hochformat, responsives Grid) + Link zu Alens Tangem-Pro-Code
- Abschnitt "💰 Mein Portfolio": Menge je Coin eintragen, Dashboard zeigt Wert je Coin, Gesamtwert und heutige Veränderung in Euro. Mengen liegen **nur im Browser** (localStorage), nie im Code/Repo (Repo ist public). Live auf GitHub Pages (Commit `d70dd40`).
- Portfolio zusätzlich mit Einstiegspreis (Kaufpreis €) je Coin und Gewinn/Verlust-Anzeige (€ und %, grün/rot) pro Coin und als Gesamtsumme. Eigener localStorage-Key `kd_portfolio_einstiegspreise`, getrennt von den Mengen. Fehlt bei einem Coin der Kaufpreis, erscheint ein Hinweistext, dass die Gesamtsumme nur die Coins mit Kaufpreis umfasst. Live auf GitHub Pages (Commit `7c5ba9b`).
- Preisalarm je Coin-Karte, zwei Richtungen, beide Schwellenwerte nur im localStorage:
  - "Alarm ab [€]": sobald aktueller Preis ≥ Schwelle → kräftiger gelber Rahmen + "✅ Ziel erreicht"
  - "Alarm unter [€]" (Stop-Loss-Warnung, von Iva in der Stunde vom 2026-11-04 mündlich ergänzt): sobald aktueller Preis < Schwelle → roter Rahmen + "⚠️ Unter Zielwert"
- Willkommens-Kugel beim Öffnen der Seite: glühende Kugel erscheint mittig, öffnet sich kurz zu einer Kapsel mit "⚡ Willkommen beim Krypto-Dashboard", zieht sich wieder zusammen und verschwindet (~5,5 Sek., generisch für jeden Besucher, kein Name). Erst danach blendet sich der restliche Dashboard-Inhalt ein.

## Lokale Claude-Skills
Liegen in `.claude/skills/` im Projektordner. Reine Werkzeuge für die Arbeit mit Claude an diesem Projekt – kein Teil der Website, nichts davon läuft im Browser der Besucher.
- `mein-portfolio` – eigener Skill, fragt im Terminal je Coin nach der Menge, holt Live-Kurse, zeigt Tabelle + Gesamtsumme. Speichert nichts.
- `veroeffentlichen` – eigener Skill, prüft vor dem Veröffentlichen auf private Daten, schreibt in progress.md, committet, fragt vor dem Push nach Bestätigung.
- `video-edit` – von GitHub (agricidaniel/claude-video, nur den Unterordner `skills/video-edit` übernommen, nicht das ganze Repo wegen dessen globaler Hooks) für Videoschnitt (trimmen, Tempo, Overlays, Gesichter unkenntlich machen usw.) über FFmpeg. Am 2026-11-14 erfolgreich getestet: erstes Tangem-Video probeweise auf 49,5 Sek. gekürzt, um den veralteten Angebots-Screen zu entfernen (nur Übung, nicht live übernommen).
- `coingecko` – offizieller Skill von github.com/coingecko/skills, hilft Claude, bei Fragen zu Krypto-Marktdaten die richtigen CoinGecko-API-Endpunkte zu finden statt zu raten. Am 2026-11-14 erfolgreich getestet (Marktkapitalisierung XDC Network, 7-Tage-Verlauf Stellar).

## Letzte Änderungen (Commits)
- `8c0966c` – Neuer Claude-Skill `/mein-portfolio` angelegt (`.claude/skills/mein-portfolio/SKILL.md`): fragt im Terminal je Coin nach der Menge, holt Live-Kurse von CoinGecko, zeigt Tabelle und Gesamtsumme im Terminal aus; speichert nichts (keine Datei, kein Log)
- `137c078` – Neuer Claude-Skill `/veroeffentlichen` angelegt (`.claude/skills/veroeffentlichen/SKILL.md`): prüft vor jedem Veröffentlichen automatisch auf private Daten (Mengen, Kaufpreise, Alarme, Schlüssel), schreibt in progress.md, committet auf Deutsch, fragt vor dem Push nach Bestätigung, nennt am Ende Commit-Hash + Handy-Erinnerung
- `35adb24` – Karte am PC auf `preserveAspectRatio="meet"` umgestellt (responsiv per JS, nur ab 480px Breite), damit USA und Australien nicht mehr am Rand abgeschnitten werden; Handy-Darstellung unverändert
- `f064dfb` – Länder-Labels auf nur-Flagge (ohne Name) reduziert und zur Kartenmitte hin ausgerichtet, damit nichts mehr am Bildschirmrand abgeschnitten wird; Australien-Hub etwas nach innen gerückt
- `8424825` – Kartenabstand von fixem px-Wert auf 28vh umgestellt, da er am PC (breiter Bildschirm) nicht ausreichte und der Titel mit dem EU-Label überlappte
- `4c216b3` – Abstand oben eingebaut, damit die Weltkarte vor dem Dashboard-Inhalt sichtbar ist
- `7ef5089` – Länder-Labels (Flaggen + Namen) auf Hintergrundkarte ergänzt; Afrika und Australien bekommen eigene Hubs mit Verbindung + Signal
- `ff91b6d` – Sichtbaren Status-Text "(Auto-Refresh alle 60 Sek.)" entfernt, Statuszeile zeigt nur noch "Stand: [Uhrzeit]"
- `496c4e0` – Auto-Refresh-Intervall von 60 Sekunden auf 15 Minuten umgestellt
- `7c5ba9b` – Einstiegspreis (Kaufpreis €) und Gewinn/Verlust-Anzeige im Portfolio ergänzt
- `def0883` – Willkommens-Kugel beim Öffnen des Dashboards eingebaut (zuerst Begrüßungsanimation allein, danach Rest-Inhalt einblenden)
- `1e75005` – Weltkarten-Hintergrund mit Transfer-Impulsen eingebaut; 7-Tage-Liniendiagramm komplett entfernt (auf Alens Wunsch)
- `38b8467` – Ladeflackern beim Öffnen behoben; Preisalarm um Stop-Loss-Warnung (Alarm unter, rot) erweitert
- `d70dd40` – Portfolio-Abschnitt hinzugefügt (Menge pro Coin, Wert nur lokal gespeichert)
- `25dafcb` – Drei weitere Tangem-Videos (Cold Wallet vs. Börse) hinzugefügt
- `0a21be7` – Sparkline durch TradingView-Mini-Chart je Coin ersetzt
- `12a126a` – Farbiger Akzentstreifen auf Coin-Karten
- `b7bd585` – Kurse/7-Tage-Verlauf im Browser zwischengespeichert (localStorage)
- `5e61924` – Tangem-Erklärvideo samt Pro-Code-Link eingebaut

## Offene Punkte / Vorsicht
- **localStorage ist pro Webseite getrennt:** Werte, die lokal (Datei direkt im Browser geöffnet, `file://...`) eingetragen werden, und Werte auf der Live-Seite (`https://allen1977-maker.github.io/...`) sind zwei getrennte Speicherorte im Browser. Ein Preisalarm/Portfolio-Eintrag, der an einem Ort gemacht wird, taucht am anderen nicht auf – kein Fehler, sondern normales Browser-Verhalten.
- Bei einigen Coins sind die TradingView-Symbole nur Schätzungen (XDC, VELO, Canton Network, Zebec Network). Falls eines davon "Invalid symbol" zeigt: in `index.html` bei `TRADINGVIEW_SYMBOLE` korrigieren.
- Vor dem Löschen/Überschreiben von Dateien oder destruktiven Git-Befehlen: immer vorher nachfragen.
- Repo ist public – persönliche Zahlen (Portfolio-Mengen, Alarm-Schwellen) dürfen nie im Code landen, nur im localStorage des Nutzers.

## Wie geht's weiter?
Projekt ist offen für neue Feature-Wünsche. Bei neuen Ideen: kurz nachfragen (z. B. wo platziert, öffentlich sichtbar ja/nein), dann umsetzen, testen, committen, pushen.
