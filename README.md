# waqt-timetables

Published prayer timetables that the [Waqt](https://github.com/bachron/waqt) app downloads when its own copy does not cover a year.

| Folder | What | Source |
|---|---|---|
| `singapore/<year>.json` | Muslim prayer timetable for Singapore | MUIS (Majlis Ugama Islam Singapura), as published on [data.gov.sg](https://data.gov.sg/datasets/d_a6a206cba471fe04b62dd886ef5eaf22/view) |
| `london/<year>.json` | London Unified Prayer Timetable, begins times | As published by the [East London Mosque](https://www.eastlondonmosque.org.uk/prayer-times) |

The times belong to their publishers. They are re-published here, unchanged apart from being converted to 24-hour `HH:MM`, only so
the app can fetch them. This repository is not affiliated with MUIS, data.gov.sg or the East London Mosque. If you are a publisher
and want something changed or removed, open an issue.

## Format

```json
{"source": "…", "year": 2027, "columns": ["fajr", …], "days": {"2027-01-01": "06:26 08:03 …"}}
```

One string per day, times in 24-hour clock on the place's wall clock (London follows daylight saving). Files are only written when a
whole year parses and validates: every day present, every row in order.

## How it updates

A weekly job on the owner's always-on Mac runs `Scripts/timetables/run_update.sh` from the Waqt repo. It checks data.gov.sg and the
East London Mosque page for a new year, validates it, commits it here, and opens an issue in this repo if something needs a person.
