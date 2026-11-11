# Setup-Anleitung: Claude als Lauf-Coach mit Intervals.icu + Garmin

Dauer: ca. 30–45 Minuten. Du brauchst: eine Garmin-Uhr, einen Computer (Mac oder Windows), Claude Desktop und ein Claude-Abo.

Ablauf: **Garmin → Intervals.icu → MCP-Server → Claude Desktop → Skill**

---

## Schritt 1 – Intervals.icu-Konto & Garmin verbinden (10 min)

1. Auf https://intervals.icu kostenlos registrieren.
2. **Einstellungen → Verbindungen → Garmin** verbinden und **alle drei** Häkchen setzen:
   - ✅ Aktivitäten herunterladen
   - ✅ Wellness herunterladen (Ruhepuls, Schlaf, HRV)
   - ✅ Geplante Trainings hochladen
3. Im selben Bereich **ältere Aktivitäten importieren** (z. B. die letzten 3–6 Monate).

> ⚠️ Nur Strava zu verbinden reicht nicht: Läufe, die über Strava reinkommen, gibt Intervals nicht an Claude weiter. Garmin muss direkt verbunden sein. Strava kann zusätzlich verbunden bleiben.

## Schritt 2 – API-Key & Athlete-ID holen (2 min)

1. Intervals → **Einstellungen → Developer Settings / API** → **API-Key erzeugen**. Kopieren und sicher aufbewahren (wie ein Passwort, nie öffentlich teilen).
2. **Athlete-ID**: steht in der Adresszeile, wenn du in Intervals eingeloggt bist, z. B. `i123456`.

## Schritt 3 – Werkzeuge installieren (5 min)

**Python-Paketmanager `uv` installieren:**
- Mac: Programm „Terminal" öffnen und einfügen:
  ```
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- Windows: „PowerShell" öffnen und einfügen:
  ```
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
Danach das Terminal schließen und neu öffnen.

**Git** wird zum Herunterladen benötigt (Mac: fragt beim ersten `git`-Befehl automatisch nach Installation; Windows: https://git-scm.com).

## Schritt 4 – MCP-Server herunterladen (5 min)

Im Terminal / in PowerShell:
```
cd ~
git clone https://github.com/mvilanova/intervals-mcp-server.git
cd intervals-mcp-server
uv venv --python 3.12
uv sync
```

Pfad zu `uv` herausfinden (brauchst du gleich):
- Mac: `which uv` → z. B. `/Users/DEINNAME/.local/bin/uv`
- Windows: `where.exe uv` → z. B. `C:\Users\DEINNAME\.local\bin\uv.exe`

## Schritt 5 – Claude Desktop konfigurieren (5 min)

1. Claude Desktop → **Einstellungen → Entwickler → Konfiguration bearbeiten**. Das öffnet `claude_desktop_config.json`.
2. Den passenden Block aus `config/claude_desktop_config.mac.json` bzw. `config/claude_desktop_config.windows.json` (im Repo) einfügen und ersetzen:
   - `DEINNAME` → dein Benutzername
   - `<ATHLETE_ID>` → deine Athlete-ID (Schritt 2)
   - `<API_KEY>` → dein API-Key (Schritt 2)
3. Speichern, **Claude Desktop komplett beenden und neu starten**.
4. Test: In einem neuen Chat fragen: *„Zeig mir meine letzten 5 Aktivitäten aus Intervals."*

Gibt es schon andere Einträge unter `"mcpServers"`, den Intervals-Block innerhalb der geschweiften Klammern dazusetzen (Komma nicht vergessen).

## Schritt 6 – Skill installieren (2 min)

1. `running-coach.zip` herunterladen.
2. Claude → **Einstellungen → Fähigkeiten / Skills → Skill hochladen** → ZIP auswählen.
3. Empfohlen: in Claude ein **Projekt** „Lauftraining" anlegen und dort chatten – dann merkt sich Claude dein Profil und deine Vorlieben.

## Schritt 7 – Loslegen

Schreib: **„Sei mein Lauf-Coach."**
Claude fragt dann deine Ziele ab, bestimmt deine Zonen aus deinen Daten und plant die erste Woche.

## Schritt 8 – Einmalig in Garmin Connect (optional, 15 min)

Wenn du Kraft- und Dehn-Einheiten willst: die drei Workouts aus `garmin-workouts.md` einmal in Garmin Connect anlegen (Training → Workouts → Workout erstellen). Claude sagt dir dann im Kalender, wann welches dran ist.

Außerdem in Garmin Connect empfohlen:
- HF-Zonen gleich wie in Intervals (Max-HF + Laktatschwelle) einstellen
- Garmin-eigene Trainingsvorschläge / Garmin Coach abschalten (sonst doppelte Pläne)
- Uhr nachts tragen (Schlaf, HRV, Ruhepuls)

---

## Fehlerbehebung

| Problem | Lösung |
|---|---|
| Claude sieht keine Intervals-Tools | Claude Desktop ganz beenden und neu starten; JSON auf Tippfehler/fehlende Kommas prüfen (z. B. auf jsonlint.com) |
| Fehler `spawn uv ENOENT` | Bei `command` den **vollen Pfad** zu uv eintragen (Schritt 4) |
| Windows: Änderungen wirken nicht | Bei Microsoft-Store-Installation liegt die Datei unter `C:\Users\DEINNAME\AppData\Local\Packages\Claude_pzs8sxrjxfjjc\LocalCache\Roaming\Claude\claude_desktop_config.json`; Pfade im JSON mit doppelten Backslashes `\\` |
| Claude findet keine Läufe | Garmin direkt mit Intervals verbinden (nicht nur Strava), alte Aktivitäten importieren |
| Nutzung vom Handy aus | Funktioniert, solange der Computer mit Claude Desktop läuft und mit dem Chat verknüpft ist |
