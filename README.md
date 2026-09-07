# 🎲 Würfel — Zufalls-Satzgenerator

Eine kleine, verspielte Web-App: Sätze eingeben, würfeln, und der Zufall wählt einen aus —
mit einem Klick in die Zwischenablage kopiert.

**➡️ Live: <https://norocketscience.github.io/wuerfel/>**

## Funktionen

- 🎲 Animierter 3D-Würfel wählt zufällig einen deiner Sätze aus
- 📋 Ergebnis mit einem Klick in die Zwischenablage kopieren
- ✏️ Sätze hinzufügen und einzeln oder alle löschen
- 💾 Speicherung lokal im Browser (`localStorage`) — keine Daten verlassen dein Gerät
- ⬆️⬇️ Import und Export der Satzliste als `.txt`-Datei (ein Satz pro Zeile)
- 📱 Responsiv, funktioniert auf Handy und Desktop; respektiert `prefers-reduced-motion`

## Technik

Eine einzige `index.html` — reines HTML, CSS und Vanilla-JavaScript, ohne Build-Schritt und
ohne Abhängigkeiten. Das Deployment übernimmt GitHub Actions
([`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)): Bei jedem Push auf `main`
wird die Seite automatisch auf GitHub Pages veröffentlicht.

## Lokal nutzen

Einfach die `index.html` im Browser öffnen — fertig.
