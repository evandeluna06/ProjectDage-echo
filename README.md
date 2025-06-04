---

### 🧠 `echo_bot.py` (starter pattern recognition logic)

```python
import datetime
import json

# Sample input
current_entry = {
    "echo_code": "947–Serpent",
    "archetype": "Seer",
    "emotion": "Revelation",
    "dream_tags": ["mirror", "water", "light"],
    "timestamp": "2025-06-03T22:10:00Z"
}

# Simulated memory log (to be pulled from Sheets or Notion later)
past_entries = [
    {"archetype": "Seer", "emotion": "Fear", "dream_tags": ["mirror", "stairs", "smoke"], "timestamp": "2025-03-22"},
    {"archetype": "Healer", "emotion": "Joy", "dream_tags": ["fire", "river", "owl"], "timestamp": "2025-04-10"},
    {"archetype": "Seer", "emotion": "Clarity", "dream_tags": ["mirror", "light", "door"], "timestamp": "2025-05-01"}
]

# Pattern logic
def find_echoes(current, memory):
    matches = [entry for entry in memory if entry["archetype"] == current["archetype"]]
    symbols = []
    for entry in matches:
        overlap = list(set(entry["dream_tags"]) & set(current["dream_tags"]))
        if overlap:
            symbols.extend(overlap)

    echo_report = {
        "echo_flag": "Recurring" if matches else "First Entry",
        "echo_report": f"Archetype '{current['archetype']}' echoed {len(matches)}x. "
                       f"Symbols repeated: {list(set(symbols))}. "
                       f"Emotional path: {', '.join([e['emotion'] for e in matches])} → {current['emotion']}.",
        "echo_score": round(len(symbols) / 3, 2),
        "analyzed_by": "EchoBot-AI"
    }
    return echo_report

result = find_echoes(current_entry, past_entries)
print(json.dumps(result, indent=2))
