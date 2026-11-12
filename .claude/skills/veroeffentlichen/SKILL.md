---
name: veroeffentlichen
description: Veröffentlicht Änderungen am Krypto-Dashboard auf GitHub. Verwenden, wenn Alen "/veroeffentlichen" eingibt. Prüft vorher automatisch auf private Daten (Mengen, Kaufpreise, Alarme, Schlüssel), schreibt die Änderung in progress.md, committet auf Deutsch, fragt vor dem Push nach Bestätigung und nennt am Ende den Commit-Hash.
---

# Veröffentlichen

Führe diese Schritte in genau dieser Reihenfolge aus.

## 1. Git-Status prüfen
- `git status` ausführen.
- Alen eine kurze, verständliche Liste zeigen: welche Dateien neu, geändert oder gelöscht sind (in 1–2 Sätzen erklärt, keine reine Rohausgabe).

## 2. Sicherheits-Check: keine privaten Daten
- Die Änderungen durchsehen (`git diff`).
- Gezielt suchen nach:
  - Mengen/Stückzahlen von Coins (Portfolio-Mengen)
  - Kaufpreisen/Einstiegspreisen in €
  - Alarm-Schwellen (Preisalarm, Stop-Loss)
  - Schlüsseln/Secrets (API-Keys, Tokens, Passwörter)
- Wird etwas davon gefunden: **sofort anhalten**, Fundstelle (Datei + Stelle) zeigen und Alen fragen, ob es raus soll – nicht von selbst weitermachen.
- Nur wenn nichts gefunden wurde: weiter zu Schritt 3.

## 3. progress.md aktualisieren
- Neuen Eintrag unter "Letzte Änderungen (Commits)" ergänzen, im bestehenden Stil, der kurz beschreibt, was sich geändert hat.

## 4. Commit erstellen
- Nur die relevanten Dateien gezielt stagen (nicht blind alles, auf Secrets/Zufallsdateien achten).
- Commit mit kurzer deutscher Beschreibung (1 Satz, was sich geändert hat).
- Attribution-Zeile wie gewohnt anhängen.

## 5. Vor dem Push: Bestätigung einholen
- Zeigen, was committet wurde (Nachricht + Dateien).
- Explizit fragen: "Soll ich jetzt pushen? (ja)"
- **Erst nach klarem "ja"/"da" pushen.** Ohne Bestätigung nicht pushen.

## 6. Nach dem Push
- `git push` ausführen.
- Commit-Hash in progress.md nachtragen (wie im Projekt üblich, eigener kleiner Folge-Commit) und mitpushen.
- Alen am Ende kurz sagen:
  - den Commit-Hash
  - dass die Änderung jetzt live geht
  - Erinnerung: "Schau in ca. 2 Minuten auf dem Handy nach, ob es übernommen wurde."

Wichtig: Schritt 2 darf nie übersprungen werden, auch wenn die Änderung harmlos aussieht.
