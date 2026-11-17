---
name: wochenrueckblick
description: Fasst zusammen, was Alen in den letzten 7 Tagen am Krypto-Dashboard gemacht hat. Liest dafür das Git-Log der letzten Woche und die Datei progress.md, und gibt eine kurze Zusammenfassung im Terminal aus. Verwenden, wenn Alen "/wochenrueckblick" eingibt.
---

# Wochenrückblick

Führe diese Schritte in genau dieser Reihenfolge aus. Dieser Skill liest nur – er schreibt, committet und verändert nichts.

## 1. Git-Log der letzten 7 Tage holen
Führe im Projektordner aus:
```
git log --since="7 days ago" --pretty=format:"%ad | %s" --date=format:"%Y-%m-%d"
```
- Zeigt Datum + Commit-Nachricht für jeden Commit der letzten Woche.
- Gibt es keine Commits in den letzten 7 Tagen: das offen so sagen ("Diese Woche keine Änderungen committet"), nichts erfinden.

## 2. progress.md lesen
- Lies die Datei `progress.md` im Projektordner.
- Schau besonders auf die "Stand:"-Zeile oben und auf Einträge, die ein Datum aus den letzten 7 Tagen tragen (z. B. "Update 2026-11-14: ...").
- Ältere Einträge (länger als 7 Tage zurück) nicht in die Zusammenfassung aufnehmen.

## 3. Zusammenfassen
- Verbinde Git-Log und progress.md zu einer kurzen, verständlichen Zusammenfassung auf Deutsch, in einfacher Sprache.
- Reihenfolge: neueste Änderung zuerst.
- Technische Commit-Nachrichten (oft Englisch oder knapp) in normale Sätze übersetzen, nicht einfach roh ausgeben.
- Bei unklaren/kryptischen Commit-Nachrichten: so gut wie möglich einordnen, aber nichts dazuerfinden, was nicht aus Log oder progress.md hervorgeht.

## 4. Bericht im Terminal ausgeben
Format, z. B.:
```
📅 Wochenrückblick (letzte 7 Tage)

- [Datum]: [was gemacht wurde, in einfachen Worten]
- [Datum]: [...]

Insgesamt: [X] Commits diese Woche.
```

## 5. Nichts speichern
- Nur im Terminal ausgeben.
- Keine neue Datei anlegen, nichts an progress.md ändern, nichts committen oder pushen.
