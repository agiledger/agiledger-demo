# 👥 teams

> Agile teams — the root collection linking team members, standup questions, and date records.

| Column | Type | Required | Constraints |
|--------|------|:--------:|-------------|
| $ID | string | ✅ | |
| title | string | ❌ | |

### Example Records

| $ID | title |
|----|-------|
| alpha | Alpha Team |
| beta | Beta Team |

## Subcollections

- [mates](./) — Team members and their roles
- [daily-questions](./) — Customizable standup questions
- [dates](./) — Standup dates, with nested mate participations and answers

---

## Collection Definition

```yaml
record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml
columns:
  "$ID":
    type: string
    primaryKey: true
  title:
    type: string
columns_order:
  - "$ID"
  - title
```
