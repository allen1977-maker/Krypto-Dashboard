# Fortschritt – Krypto-Dashboard

Stand: 2026-11-14 (Hintergrund von Weltkarte auf Video umgestellt: Reisfeld/Nachthimmel-Clip, von Alen nach Vergleichstest am Handy ausgewählt; alte Weltkarte bleibt als Reserve im Code)

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
- **Update 2026-11-14:** Fester Hintergrund ist jetzt ein Video (`hintergrund-video.mp4`, Nachthimmel/Milchstraße über japanischen Reisterrassen, Pixabay-ID 283431, lizenzfrei, komprimiert von 25 MB auf 732 KB: 720×1280, 30fps, kein Ton, `autoplay muted loop playsinline`, `object-fit: cover`). Zur Wahl standen zwei Kandidaten (Reisfeld-Video und ein Sternenhimmel-Video, Pixabay-ID 42665) – Alen hat beide am Handy verglichen und sich für das Reisfeld-Video entschieden ("ist besser"). Die bisherige SVG-Weltkarte (Punkt-Karte mit 7 Hubs und Transfer-Impulsen) bleibt als Reserve im Code erhalten, nur per `style="display:none"` ausgeblendet (`#welt-karte-svg`) – auf Alens Wunsch nicht gelöscht, falls er später zurück möchte. Alte Beschreibung der Weltkarte (für den Fall der Rückkehr): stilisierte Punkt-Weltkarte mit 7 Hubs (inkl. Afrika und Australien) und animierten Transfer-Impulsen, reines SVG/CSS, dezente Länder-Flaggen (🇺🇸🇧🇷🇪🇺🇨🇭🇷🇺 Afrika-Text 🇦🇺), Labels wachsen zur Kartenmitte hin. Flaggen-Emojis zeigen unter Windows nur als Buchstabenkürzel, auf Handy/Mac echte Flaggen (bewusst so belassen).
- `<h1>` hat `margin-top: 28vh` (mobil fest 60px), damit oben ein Streifen der Weltkarte sichtbar bleibt. Wichtig: feste px-Werte reichen bei breiten PC-Bildschirmen nicht, weil die Karte (`preserveAspectRatio="slice"`) sich an der Bildschirmhöhe hochskaliert – vh-Einheit skaliert proportional mit und funktioniert deshalb auf PC und Handy gleichermaßen.
- Karte passt sich per JS (`karteAnpassen()`, `index.html`) responsiv an: ab 480px Breite (PC/Tablet) wird `preserveAspectRatio` auf `xMidYMid meet` umgeschaltet (Karte komplett eingepasst, kein Beschnitt mehr an den Rändern – USA/Australien jetzt immer sichtbar), unter 480px (Handy) bleibt `slice` (bildschirmfüllend, wie von Alen am Handy bereits für gut befunden).
- Abschnitt "📱 Tangem erklärt": 2 Highlight-Videos (Deutsch + Englisch, Hochformat, responsives Grid) + Link zu Alens Tangem-Pro-Code. Ersetzen seit 2026-11-14 die bisherigen 4 Einzelvideos (siehe Abschnitt "Tangem-Highlight-Video" weiter unten).
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

## Tangem-Highlight-Video (TikTok + evtl. Dashboard)
Auf Alens Wunsch aus seinem TikTok-Rohmaterial (Zip-Datei mit ~60 eigenen Videos/Fotos, aus Downloads entpackt in einen eigenen Ordner `C:\Users\allen\tangem-videos-rohmaterial\`, **nicht** im Projektordner) zwei fertige Zusammenfassungs-Videos gebaut:
- `tangem_highlight_DE.mp4` (82,6 Sek.) und `tangem_highlight_EN.mp4` (77,9 Sek.), in `tangem-videos-rohmaterial/build/`.
- Aufbau: Hook ("Exchange gehackt") aus `tangem_panik_cafe_*` → ausführlicher Erklärteil (wasserdicht, EAL6+ Sicherheitschip, mobiles Kaufen/Verkaufen, Face ID) aus `tangem_erklaert_hell_faceid_*` → neue Abschluss-Karte mit nur dem Link `tangem.com/invite/ALEN` (bewusst ohne Rabatt-% oder Datum, da die alte Promo-Karte in allen Original-Videos ein abgelaufenes Datum "17. Oktober 2026" zeigte).
- Musik komplett ersetzt: lizenzfreie Spannungsmusik (Pixabay, `sub_clair`) beim Börsen-Crash-Hook, Übergang zu einer lizenzfreien "Für Elise"-Aufnahme (Pixabay, `konstantinpazuzustudio`) sobald die Cold-Wallet-Lösung kommt.
- **Wichtiger Lerneffekt:** `ffmpeg -ss <Zeit> -i Datei` (Suche vor `-i`) springt beim schnellen Suchen ungenau auf einen nahen Keyframe und kann Vorschaubilder mehrere Sekunden daneben zeigen. Für exakte Schnittpunkte (z. B. "letzter Frame vor einer Überblendung") immer `-i Datei -ss <Zeit>` (Suche nach `-i`) verwenden, auch wenn es langsamer ist. In diesem Fall hätte die schnelle Variante sonst zweimal einen Rest der alten, abgelaufenen Promo-Karte mit ins fertige Video gelassen (erst bei einer zweiten, genauen Prüfung bemerkt und korrigiert).
- Update: Beide Videos sind jetzt live im Abschnitt "📱 Tangem erklärt" eingebaut und ersetzen dort die bisherigen 4 Einzelvideos (`tangem_erklaert_hell_EN_9x16.mp4`, `tangem_ledger_seedless_9x16_EN.mp4`, `tangem_werbung_coldwallet_1.mp4`, `tangem_werbung_coldwallet_2.mp4` aus dem Repo entfernt, bleiben aber in der Git-Historie erhalten). Alen hat die Live-Seite geprüft und bestätigt ("passt"). Noch nicht separat auf TikTok gepostet.

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
