---
name: preisalarm-vorschlag
description: Holt live die aktuellen Euro-Kurse der 6 Dashboard-Coins (Stellar, XDC Network, VELO, Canton Network, Zebec Network, SHX Stronghold) von CoinGecko und schlägt für jeden Coin sinnvolle Standard-Schwellen für "Alarm ab" (höher) und "Alarm unter" (tiefer) vor, z. B. ±10 % vom aktuellen Kurs. Verwenden, wenn Alen "/preisalarm-vorschlag" eingibt oder Standardwerte/Vorschläge für die Preisalarm-Schwellen im Dashboard möchte. Schlägt nur vor, speichert nichts und ändert ohne Rückfrage keinen Code.
---

# Preisalarm-Vorschlag

Führe diese Schritte in genau dieser Reihenfolge aus.

## 1. Prozentsatz klären
- Frage Alen kurz, welchen Abstand er für den Vorschlag möchte (Standard: **10 %** nach oben und unten, falls er nichts anderes sagt).

## 2. Aktuelle Kurse holen
- Rufe live die Euro-Kurse ab, mit dem gleichen Endpunkt wie die anderen Skills:
  `https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&ids=stellar,xdce-crowd-sale,velo,canton-network,zebec-network,stronghold-token`
- Nutze dafür `curl` (Bash-Tool) oder WebFetch.
- Schlägt die Abfrage fehl (kein Internet, Rate-Limit, API-Fehler): das offen sagen, keine erfundenen Kurse verwenden, und fragen ob Alen es später erneut versuchen will.

## 3. Vorschläge berechnen
Für jeden Coin:
- "Alarm ab"-Vorschlag = aktueller Kurs × (1 + Prozentsatz)
- "Alarm unter"-Vorschlag = aktueller Kurs × (1 − Prozentsatz)
- Sinnvoll runden (bei Kursen unter 1 € auf 4 Nachkommastellen, sonst auf 2).

## 4. Tabelle im Terminal ausgeben
Spalten: Coin | Aktueller Kurs (€) | Vorschlag "Alarm ab" (€) | Vorschlag "Alarm unter" (€)

Beispiel-Format:
```
Coin                  Kurs (€)   Alarm ab (€)   Alarm unter (€)
Stellar (XLM)         0,XXXX     0,XXXX         0,XXXX
XDC Network           0,XXXX     0,XXXX         0,XXXX
VELO                  0,XXXX     0,XXXX         0,XXXX
Canton Network (CC)   0,XXXX     0,XXXX         0,XXXX
Zebec Network         0,XXXX     0,XXXX         0,XXXX
SHX Stronghold        0,XXXX     0,XXXX         0,XXXX
```

## 5. Einordnen
- Kurz erklären: Das sind **Vorschläge auf Basis des heutigen Kurses**, keine Kauf- oder Verkaufsempfehlung, und keine Garantie für die Zukunft – der Kurs kann sich jederzeit ändern.

## 6. Nachfragen, was damit passieren soll
Frage Alen, ob er:
- (a) die Vorschläge nur sehen wollte (dann nichts weiter tun), oder
- (b) möchte, dass diese Beispielwerte als **Platzhalter-Text** (`placeholder`-Attribut, z. B. "z. B. 0,15") in den Eingabefeldern in `index.html` ergänzt werden, damit Besucher eine Orientierung sehen.

Bei (b):
- Nur das `placeholder`-Attribut ändern, **nicht** das `value`-Attribut – es dürfen keine echten, gespeicherten Schwellenwerte im Code landen (Repo ist public, siehe `progress.md` unter "Offene Punkte / Vorsicht").
- Änderung zeigen und Alen bestätigen lassen, bevor etwas committet wird.
- Für Veröffentlichung auf den Skill `/veroeffentlichen` verweisen (dieser Skill committet/pusht nicht selbst).

## 7. Nichts automatisch speichern
- Dieser Skill schreibt nichts automatisch in `progress.md` oder in den Code. Das passiert nur nach ausdrücklicher Bestätigung in Schritt 6.
