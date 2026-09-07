# 🎲 Würfel — Zufalls-Satzgenerator

Eine kleine, verspielte Web-App mit **gemeinsamer Satzliste**: Alle Besucher sehen dieselben
Sätze und können neue eintragen. Der Würfel wählt zufällig einen aus — mit einem Klick in die
Zwischenablage kopiert.

**➡️ Live: <https://norocketscience.github.io/wuerfel/>**

## Funktionen

- 🎲 Animierter 3D-Würfel wählt zufällig einen Satz aus (kein Satz zweimal direkt hintereinander)
- 🌍 Gemeinsame Satzliste für alle Besucher — neue Sätze sind sofort für alle sichtbar
- 📋 Ergebnis mit einem Klick in die Zwischenablage kopieren
- 🔒 Einträge sind über die App nicht lösch- oder änderbar (Schutz vor Vandalismus)
- ⬇️ Export der Satzliste als `.txt`-Datei
- 📶 Offline-Fallback: Ohne Verbindung zeigt die App den zuletzt geladenen Stand
- 📱 Responsiv, respektiert `prefers-reduced-motion`

## Technik

Eine einzige `index.html` — reines HTML, CSS und Vanilla-JavaScript, ohne Build-Schritt.
Das Hosting übernimmt GitHub Pages ([`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)
deployt bei jedem Push auf `main`).

Die gemeinsame Satzliste liegt in einer **Firebase Realtime Database** und wird über deren
REST-API gelesen und beschrieben (`GET`/`POST` auf `/saetze.json`). Die Datenbankregeln sind
append-only: Jeder darf lesen und neue Sätze anlegen, aber niemand kann bestehende Einträge
über die API ändern oder löschen.

### Datenbankregeln (Firebase → Realtime Database → Regeln)

```json
{
  "rules": {
    "saetze": {
      ".read": true,
      "$id": {
        ".write": "!data.exists()",
        ".validate": "newData.isString() && newData.val().length > 0 && newData.val().length <= 500"
      }
    }
  }
}
```

### Moderation

Einträge löschen oder korrigieren: In der [Firebase-Konsole](https://console.firebase.google.com)
→ Realtime Database → Knoten `saetze` → Eintrag bearbeiten/entfernen. Änderungen sind sofort
für alle Besucher wirksam (beim nächsten Laden bzw. „Aktualisieren").

## Lokal entwickeln

Wegen des Datenbank-Zugriffs per `fetch` sollte die Seite über einen lokalen Server laufen,
z. B. `python3 -m http.server` im Projektordner, dann <http://localhost:8000> öffnen.
