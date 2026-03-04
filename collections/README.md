# 📋 Collections

## 👥 [teams](teams/)

> Agile teams — the root collection. Each team has its own set of mates, standup questions, and date records.

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| $ID | string | ✅ | |
| title | string | ❌ | |

### Example Records

| $ID | title |
|----|-------|
| alpha | Alpha Team |
| beta | Beta Team |

---

## 🧑‍💻 teams / mates

> Team members and their assigned roles within a team.

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| role | string | ❌ | e.g. developer, scrum_master, qa, product_owner |

### Example Records

| $ID (filename) | role |
|----------------|------|
| alice | developer |
| bob | scrum_master |
| carol | developer |
| dave | qa |

---

## ❓ teams / daily-questions

> Customizable standup questions per team. Stored as a single JSON file per team where each key is a question ID.

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| question | string | ✅ | |
| required | bool | ❌ | |

### Example Records

| $ID | question | required |
|----|----------|:--------:|
| q1 | What did you accomplish yesterday? | true |
| q2 | What will you work on today? | true |
| q3 | Are there any blockers or impediments? | false |

---

## 📅 teams / dates

> Standup dates for a team. Each date has a directory named after the date (ISO 8601).

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| is_holiday | bool | ❌ | When true, no standup records expected |

### Example Records

| $ID | is_holiday |
|----|:----------:|
| 2025-01-20 | false |
| 2025-01-21 | false |
| 2025-01-22 | true |

---

## 🙋 teams / dates / mates

> Records indicating a team member's participation on a specific standup date.

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| $ID | string | ❌ | |

### Example Records

Each file is `{mate_id}/mate.json` — e.g. `alice/mate.json`: `{}`

---

## 💬 teams / dates / mates / questions

> Question entry for a mate on a date. Each question corresponds to a daily-question key.

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| $ID | string | ❌ | |

### Example Records

Each file is `{question_id}/question.json` — e.g. `q1/question.json`: `{}`

---

## ✍️ teams / dates / mates / questions / answers

> Answers to standup questions, keyed by language code (e.g. `en`).

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| answer | string | ✅ | |

### Example Records

| $ID (language) | answer |
|----------------|--------|
| en | Completed the user authentication module |
