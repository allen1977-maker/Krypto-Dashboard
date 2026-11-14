---
name: mein-portfolio
description: Fragt Alen im Terminal je Coin (Stellar, XDC Network, VELO, Canton Network, Zebec Network, SHX Stronghold) nach der gehaltenen Menge, holt aktuelle Euro-Kurse von CoinGecko und gibt eine Tabelle mit Werten je Coin sowie die Gesamtsumme im Terminal aus. Verwenden, wenn Alen "/mein-portfolio" eingibt oder nach seinem Portfolio-Wert/einer Portfolio-Übersicht fragt. Speichert keine Mengen oder Werte in Dateien.
---

# Mein Portfolio

Führe diese Schritte in genau dieser Reihenfolge aus.

## 1. Mengen abfragen
Frage Alen **im Terminal, nacheinander**, nach der Menge für jeden der 6 Coins (gleiche Liste wie im Dashboard, `index.html`):

1. Stellar (XLM) — CoinGecko-ID `stellar`
2. XDC Network — CoinGecko-ID `xdce-crowd-sale`
3. VELO — CoinGecko-ID `velo`
4. Canton Network (CC) — CoinGecko-ID `canton-network`
5. Zebec Network — CoinGecko-ID `zebec-network`
6. SHX Stronghold — CoinGecko-ID `stronghold-token`

- Bei "0" oder leerer Eingabe: Menge = 0, aber Coin trotzdem in der Tabelle anzeigen.
- Nicht alle Fragen auf einmal stellen, sondern eine nach der anderen, damit es wie ein echter Dialog wirkt.

## 2. Aktuelle Kurse holen
- Rufe live die Euro-Kurse ab, mit dem gleichen Endpunkt wie im Dashboard:
  `https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&ids=stellar,xdce-crowd-sale,velo,canton-network,zebec-network,stronghold-token`
- Nutze dafür `curl` (Bash-Tool) oder WebFetch.
- Schlägt die Abfrage fehl (kein Internet, Rate-Limit, API-Fehler): das offen sagen, keine erfundenen Kurse verwenden, und fragen ob Alen es später erneut versuchen will.

## 3. Berechnen
- Für jeden Coin: Wert in € = Menge × aktueller Kurs.
- Gesamtsumme = Summe aller Werte.

## 4. Bericht im Terminal ausgeben
Tabelle mit Spalten: Coin | Menge | Kurs (€) | Wert (€), danach die Gesamtsumme fett/deutlich hervorgehoben.

Beispiel-Format:
```
Coin                  Menge       Kurs (€)      Wert (€)
Stellar (XLM)         ...         0,XXXX        ...
XDC Network           ...         0,XXXX        ...
VELO                  ...         0,XXXX        ...
Canton Network (CC)   ...         0,XXXX        ...
Zebec Network         ...         0,XXXX        ...
SHX Stronghold         ...         0,XXXX        ...

Gesamtwert Portfolio: ... €
```

## 5. Nichts speichern
- **Keine Datei schreiben** mit Mengen, Werten oder der Gesamtsumme — nicht in `progress.md`, nicht in einer neuen Datei, nirgends im Projekt.
- Die Zahlen existieren nur für diesen einen Terminal-Lauf und werden danach nicht aufbewahrt.
- Falls Alen fragt, ob das gespeichert werden soll: kurz erklären, dass der Skill das bewusst nicht tut (damit keine echten Bestände auf GitHub landen können), und nur auf ausdrücklichen Wunsch eine Ausnahme machen.
