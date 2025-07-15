# Product Requirements Document (PRD)

**Product Name:** Scoreboard Buddy  
**Platform:** Android  
**Owner:** Dirk Schnelle-Walka
**Date:** July 13, 2025  
**Version:** 1.2

---

## 1 · Overview

### 1.1 Purpose  
Scoreboard Buddy lets players track and calculate scores during board or card games. With Google Play Games Cloud Save, import/export of templates, and offline‑first operation, users can customize and share scoring setups across devices and with others.

### 1.2 Target Users  
- Board/card game players  
- Game night hosts  
- Gamers with multiple devices  
- Users who want to share custom scoring templates with others

---

## 2 · Problem Statement

Many games have different or custom scoring systems. Manually entering rules each time is tedious. Users need a way to save, reuse, and share templates — even across devices or with others — in addition to persisting scores in the cloud.

---

## 3 · Goals & Success Metrics

| Goal                           | Metric                                           |
|-------------------------------|--------------------------------------------------|
| Fast, accurate, flexible scoring | < 3 s per score entry                          |
| Game template reuse/sharing     | ≥ 40% of users save or import templates        |
| Positive reviews                | ≥ 4.5 ★ on Google Play after 3 months           |
| Cloud backup & restore          | ≥ 95% successful restores across devices        |

---

## 4 · Key User Stories

1. As a user, I want to create a custom template for my game’s scoring rules.  
2. As a user, I want to export my templates to share with others.  
3. As a user, I want to import a template from another device or friend.  
4. As a user, I want my templates to sync via Google Play Games Cloud Save.  
5. As a user, I want to browse and apply saved templates when starting a new game.
6. As a player or spectator, I want to view a graph of score progression across all games in a match so that I can visualize performance trends and compare players over time.


---

## 5 · Features & Requirements

| Id    | Feature                 | Description                                                                  | Priority |
|-------|-------------------------|------------------------------------------------------------------------------|----------|
| RF_1  | Player Management       | Add/edit/remove players and teams                                            | High     |
| RF_2  | Score Entry             | Per-turn/round entry with undo/edit                                          | High     |
| RF_3  | Automatic Totaling      | Auto-update cumulative scores                                                | High     |
| RF_4  | Game Templates          | Built-in + user-defined templates (name, description, rules)                 | High     |
| RF_5  | Template Export         | Export custom templates to JSON (via file or share intent)                   | High     |
| RF_6  | Template Import         | Import templates from JSON file or share intent                              | High     |
| RF_7  | Turn/Round Tracker      | Manage round flow, display history                                           | Medium   |
| RF_8  | Win Conditions          | Support flexible end-game rules                                              | Medium   |
| RF_9  | Save & Resume           | Auto-save progress                                                           | High     |
| RF_10 | Cloud Sync              | Use GPGS Saved Games for scores and templates                                | High     |
| RF_11 | Score History View      | Round-by-round breakdown                                                     | Medium   |
| RF_12 | Export Final Scores     | Export scoreboard as PDF/CSV                                                 | Low      |
| RF_13 | Offline Support         | Full functionality offline with later sync                                   | High     |
| RF_14 | Score Progression Graph | Visualize the score progression for each player across all games in a match. | Medium   | 

---

## 6 · Out of Scope (v1.0)

- Online multiplayer with invites/sync  
- Template marketplace or in-app community  
- Voice or OCR score entry  
- Real-time collaborative template editing

---

## 7 · UX / UI Notes

**New Screens & Flows:**  
- **Template Manager Screen:** View/edit/import/export/delete templates  
- **Import Flow:** Accept `.json` file via file picker or share Intent  
- **Export Flow:** Share exported templates via file or other apps  

**Template Format (example):**
```json
{
  "name": "Custom Uno",
  "description": "Includes house rules for Wild Draw 4",
  "winCondition": "first_to_500",
  "scoringRules": [
    { "name": "Number Card", "value": "as_entered" },
    { "name": "Draw Two", "value": 20 },
    { "name": "Wild Draw 4", "value": 50 }
  ]
}
```

---

## 8 · Technical Requirements

| Aspect                    | Specification                                                       |
|--------------------------|----------------------------------------------------------------------|
| Language                 | Java                                                                 |
| Min Android Version      | Android 13 (API 33)                                                 |
| UI Framework             | XML Layouts + Android Views                                         |
| Architecture             | MVVM or MVP (Java)                                                  |
| Local Storage            | Room DB (games & templates)                                         |
| Template Import/Export   | FileProvider, JSON via file and share intents                       |
| Cloud Sync               | Google Play Games Saved Games (Snapshots API)                       |
| Dependencies             | AndroidX (Room, Lifecycle, Navigation), Material Components, GPGS v2, iText/Apache POI |


---

## 9 · Risks & Mitigations

| Risk                                    | Mitigation                                                    |
|-----------------------------------------|---------------------------------------------------------------|
| Invalid/corrupted template imports      | Validate JSON schema; show descriptive errors to users        |
| Abuse of template sharing (spam import) | Restrict sharing to manual file exchange, not online library  |
| Conflicting templates across devices    | Use timestamps; prompt user to choose which version to keep   |
