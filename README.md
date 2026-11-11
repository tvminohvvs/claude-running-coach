# 🏃 Claude Running Coach – Intervals.icu + Garmin

Mach Claude zu deinem persönlichen Lauf-Coach: Er liest deine echten Garmin-Daten, fragt zuerst deine Ziele ab, bestimmt deine Herzfrequenz-Zonen, plant jede Woche neu und schickt die Trainings direkt auf deine Garmin-Uhr.

*Turn Claude into your running coach using your real Garmin data via Intervals.icu. Guide is in German.*

## Was es kann

- 🎯 **Onboarding:** fragt Ziel (5 km bis Marathon), Ausgangslage, Läufe pro Woche, Beschwerden, Extras
- 📊 **Zonen aus deinen Daten:** HFmax, Schwellen-HF, Schwellentempo aus deinen bisherigen Läufen
- 📅 **Wochenplan:** immer nur die nächste Woche, passt sich an verpasste Trainings, Pausen und Beschwerden an
- ⌚ **Direkt auf die Uhr:** strukturierte Läufe mit HF-/Pace-Zielen, Datum im Namen, Belastung vs. Pause klar angezeigt
- 💪 **Kraft & Mobility:** fertige Garmin-Workouts für Hüfte/IT-Band, EMOM und eine einfache Dehnroutine
- 🔍 **Wochenauswertung** mit Zahlen: Fortschritt bei gleicher HF, zu schnelle Steigerungen, Kadenz, Ruhepuls
- 🧹 **Aufräumen:** erledigte Trainings verschwinden automatisch aus Garmin Connect
- 📝 Optional: sachliche **Strava-Titel/Beschreibungen** pro Lauf

## So funktioniert's

```
Garmin-Uhr ⇄ Garmin Connect ⇄ Intervals.icu ⇄ MCP-Server ⇄ Claude Desktop + Skill
```

## Installation (ca. 30–45 min, kein Programmieren nötig)

👉 **[Schritt-für-Schritt-Anleitung](skill/running-coach/references/setup-guide.md)**

Kurzfassung:
1. Intervals.icu-Konto, Garmin verbinden (Aktivitäten, Wellness, geplante Trainings)
2. API-Key + Athlete-ID kopieren
3. `uv` installieren, [intervals-mcp-server](https://github.com/mvilanova/intervals-mcp-server) klonen
4. Config aus [`config/`](config/) in Claude Desktop einfügen, neu starten
5. `running-coach.zip` in Claude unter Skills hochladen
6. Chat starten: **„Sei mein Lauf-Coach."**

## Beispiel-Prompts

- „Sei mein Lauf-Coach."
- „Bestimm meine Zonen aus meinen bisherigen Läufen."
- „Die Woche ist fertig, plan mir die neue."
- „Ich habe Freitag ausgelassen, was jetzt?"
- „Ich war 9 Tage krank, pass den Plan an."
- „Verschieb den Lauf auf heute."
- „Worauf soll ich heute beim Lauf achten?"

## Inhalt

| Pfad | Was |
|---|---|
| `skill/running-coach/SKILL.md` | Der Claude-Skill (Coach-Logik) |
| `skill/running-coach/references/setup-guide.md` | Installationsanleitung |
| `skill/running-coach/references/workout-formats.md` | Getestete Workout-Formate für Intervals → Garmin |
| `skill/running-coach/references/garmin-workouts.md` | Kraft A, Kraft B (EMOM), Mobility zum Anlegen in Garmin Connect |
| `config/` | Vorlagen für `claude_desktop_config.json` (Mac/Windows) |
| `running-coach.zip` | Fertiger Skill zum Hochladen in Claude |

## Kosten

- Intervals.icu: kostenlos (Supporter-Abo freiwillig)
- MCP-Server: Open Source (GPL-3.0, von [mvilanova](https://github.com/mvilanova/intervals-mcp-server))
- Claude: bestehendes Abo mit Claude Desktop
- Garmin-Uhr

## Hinweise

- Teile deinen API-Key nie öffentlich und committe ihn nie in ein Repo.
- Kein Ersatz für ärztlichen Rat. Bei anhaltenden Schmerzen: Physio/Arzt.
- Getestet mit Garmin Descent Mk2; andere Garmin-Modelle sollten gleich funktionieren.

## Lizenz

Inhalte dieses Repos: MIT. Der verlinkte MCP-Server hat seine eigene Lizenz (GPL-3.0).
