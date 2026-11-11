# Workout-Formate für Intervals.icu → Garmin

Getestet mit dem MCP-Server `mvilanova/intervals-mcp-server` und einer Garmin Descent Mk2. Andere Garmin-Uhren verhalten sich ähnlich.

## Grundregeln
- Name: `<Wochentag kurz> <TT.MM.> <Typ> <Dauer>` → `Do 12.11. Easy Run 40' + Steigerungen`
- `workout_type`: `Run`
- `moving_time` in Sekunden setzen (Gesamtdauer)
- Jeder Schritt braucht ein **Ziel** (HF-Zone oder Pace), sonst zeigt die Uhr nur „Laufen".
- HF-Zonen beziehen sich auf die in Intervals eingetragene Schwellen-HF.

## Easy Run / Long Run (Schritte als JSON)

```json
{
  "workout_type": "Run",
  "name": "Di 10.11. Easy Run 40'",
  "start_date": "2026-11-10",
  "moving_time": 2400,
  "workout_doc": {
    "description": "Lockerer Dauerlauf. HF unter 138 halten, sonst langsamer.",
    "steps": [
      {"duration": 300,  "hr": {"value": 1, "units": "hr_zone"}, "warmup": true,   "text": "Einlaufen"},
      {"duration": 1800, "hr": {"value": 1, "units": "hr_zone"},                    "text": "Locker HF unter 138"},
      {"duration": 300,  "hr": {"value": 1, "units": "hr_zone"}, "cooldown": true, "text": "Auslaufen"}
    ]
  }
}
```

Long Run identisch, nur längerer Mittelteil und Hinweis „Gehpausen erlaubt; bei Beschwerden abbrechen".

## Lauf mit Belastung/Pause (Steigerungen, Intervalle) – Textformat

Das JSON-Schrittformat hat bei Belastungs-/Pausenschritten auf der Uhr nur „Laufen" gezeigt. Zuverlässig funktioniert das **Intervals-Textformat in der Beschreibung** mit leerer `steps`-Liste:

```json
{
  "workout_type": "Run",
  "name": "Do 12.11. Easy Run 40' + Steigerungen",
  "start_date": "2026-11-12",
  "moving_time": 2520,
  "workout_doc": {
    "description": "Lockerer Lauf mit 6 Steigerungen. Steigerung = 20 s zügig, kein Sprint.\n\nWarmup\n- Einlaufen 10m Z1 HR\n\n- Locker laufen 20m Z1 HR\n\n6x\n- STEIGERUNG zuegig 20s 4:45-5:15/km Pace intensity=interval\n- PAUSE locker traben 1m Z1 HR intensity=recovery\n\nCooldown\n- Auslaufen 4m Z1 HR",
    "steps": []
  }
}
```

Hinweise:
- Umlaute in Schrittnamen vermeiden („zuegig"), manche Uhren zeigen sie falsch.
- Pace-Ziel immer als Bereich, z. B. `4:45-5:15/km Pace`.
- Für Pace-Ziele muss in Intervals ein Schwellentempo eingetragen sein.

## Kraft & Mobility – nur als Notiz

```json
{
  "name": "Mo 09.11. Kraft A Hüfte – 2 Runden (auf Uhr: „Kraft A Hüfte")",
  "start_date": "2026-11-09",
  "color": "blue",
  "description": "Garmin-Workout „Kraft A Hüfte\" starten ... Übungen + Videolinks"
}
```
Tool: `add_or_update_note`. Farbe: blau = Kraft, grün = Mobility.

## Aufräumen
Nach der Auswertung alle vergangenen geplanten Events mit `delete_event` löschen (IDs aus `get_events`). Aktivitäten (IDs mit `i…`) nie löschen.
