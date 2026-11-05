# Fortschritt – Krypto-Dashboard

Stand: 2026-11-05

## Was ist das Projekt?
Ein eigenes HTML-Dashboard mit Live-Krypto-Kursen (6 Coins: Stellar/XLM, XDC Network, VELO, Canton Network, Zebec Network, SHX Stronghold). Lernprojekt von Alen mit Claude als Tutor.

## Wo läuft es?
- Live über GitHub Pages: https://allen1977-maker.github.io/Krypto-Dashboard/
- Code-Repo: https://github.com/allen1977-maker/Krypto-Dashboard (öffentlich, Branch `main`)

## Was kann es aktuell?
- Live-Preise in EUR über die CoinGecko-API, 24h-Veränderung
- Eingebettete TradingView-Mini-Charts je Coin (statt einfacher Sparkline)
- Gemeinsames 7-Tage-Liniendiagramm für alle 6 Coins (normiert in %)
- Farbiger Akzentstreifen auf jeder Coin-Karte, passend zur Chart-Farbe
- Kurse und 7-Tage-Verlauf werden im Browser zwischengespeichert (localStorage) – beim Öffnen sofort sichtbar, danach Hintergrund-Update
- Auto-Refresh alle 60 Sekunden
- Abschnitt "📱 Tangem erklärt": 4 Erklärvideos (Hochformat, responsives Grid) + Link zu Alens Tangem-Pro-Code
- Abschnitt "💰 Mein Portfolio": Menge je Coin eintragen, Dashboard zeigt Wert je Coin, Gesamtwert und heutige Veränderung in Euro. Mengen liegen **nur im Browser** (localStorage), nie im Code/Repo (Repo ist public). Live auf GitHub Pages (Commit `d70dd40`).
- Preisalarm je Coin-Karte, zwei Richtungen, beide Schwellenwerte nur im localStorage:
  - "Alarm ab [€]": sobald aktueller Preis ≥ Schwelle → kräftiger gelber Rahmen + "✅ Ziel erreicht"
  - "Alarm unter [€]" (Stop-Loss-Warnung, von Iva in der Stunde vom 2026-11-04 mündlich ergänzt): sobald aktueller Preis < Schwelle → roter Rahmen + "⚠️ Unter Zielwert"
- Mehrfaches Neuzeichnen beim Öffnen behoben: `verlaufLaden()` zeichnet jetzt erst, wenn alle 6 Coin-Verläufe geladen sind, statt nach jedem einzelnen Coin – vorher sprang das Liniendiagramm beim Laden 6-8 Mal.

## Letzte Änderungen (Commits)
- *(ausstehend)* – Ladeflackern beim Öffnen behoben; Preisalarm um Stop-Loss-Warnung (Alarm unter, rot) erweitert
- `d70dd40` – Portfolio-Abschnitt hinzugefügt (Menge pro Coin, Wert nur lokal gespeichert)
- `25dafcb` – Drei weitere Tangem-Videos (Cold Wallet vs. Börse) hinzugefügt
- `0a21be7` – Sparkline durch TradingView-Mini-Chart je Coin ersetzt
- `12a126a` – Farbiger Akzentstreifen auf Coin-Karten
- `b7bd585` – Kurse/7-Tage-Verlauf im Browser zwischengespeichert (localStorage)
- `5e61924` – Tangem-Erklärvideo samt Pro-Code-Link eingebaut

## Offene Punkte / Vorsicht
- Bei einigen Coins sind die TradingView-Symbole nur Schätzungen (XDC, VELO, Canton Network, Zebec Network). Falls eines davon "Invalid symbol" zeigt: in `index.html` bei `TRADINGVIEW_SYMBOLE` korrigieren.
- Vor dem Löschen/Überschreiben von Dateien oder destruktiven Git-Befehlen: immer vorher nachfragen.
- Repo ist public – persönliche Zahlen (Portfolio-Mengen, Alarm-Schwellen) dürfen nie im Code landen, nur im localStorage des Nutzers.

## Wie geht's weiter?
Projekt ist offen für neue Feature-Wünsche. Bei neuen Ideen: kurz nachfragen (z. B. wo platziert, öffentlich sichtbar ja/nein), dann umsetzen, testen, committen, pushen.
