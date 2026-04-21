# Section 05: Dates and Time

**Status:** Normative
**Edition:** 1.0 (2026)

> **Core rule:** All date and time values **shall** be stored in ISO 8601 format. Display formatting is a presentation-layer concern only and must never affect stored values.

---

## 5.1 Date Format

| Attribute | Specification |
|-----------|--------------|
| **Standard** | **ISO 8601:2019** — Date and time format |
| **Storage format** | `YYYY-MM-DD` |
| **Example** | `2026-06-12` (12 June 2026) |
| **Prohibited formats (storage)** | `06/12/2026`, `12/06/2026`, `12-Jun-26`, `June 12, 2026` |

**Rationale:** `YYYY-MM-DD` is unambiguous across locales, lexicographically sortable, and universally machine-parseable. `MM/DD/YYYY` is ambiguous — `06/12` means June 12 in the US but December 6 in most of Europe. This ambiguity has caused real data corruption in multi-system environments.

**Display-only format (Philippine convention):** Forms and reports directed at Filipino end users **may** display dates as `DD Month YYYY` (e.g., `12 June 2026`) or `MM/DD/YYYY`. The stored database value **shall** always be ISO 8601.

---

## 5.2 Date-Time Format (Timestamps)

| Attribute | Specification |
|-----------|--------------|
| **Standard** | ISO 8601:2019 |
| **Storage format** | `YYYY-MM-DDTHH:MM:SS+08:00` |
| **Example** | `2026-06-12T08:30:00+08:00` |
| **Timezone** | Philippine Standard Time (PST) — UTC+8 |

Systems that store timestamps in UTC **shall** document this explicitly and convert to PST (+08:00) at the display layer.

Use the database-native `TIMESTAMP WITH TIME ZONE` or `DATETIME` type. Do **not** store timestamps as `VARCHAR` strings.

---

## 5.3 Academic Year

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `academic_year` |
| **Format** | `YYYY-YYYY` — the start and end calendar years |
| **Example** | `"2025-2026"` |
| **Data type** | `CHAR(9)` |

> ⚠️ A single year integer (e.g., `2026`) is ambiguous — it does not indicate whether the academic year starts in 2025 or 2026. Always use the two-year span format.

---

## 5.4 Grading Period / Semester

| Agency | Field name | Allowed Values |
|--------|-----------|----------------|
| DepEd (K–12) | `grading_period` | `Q1`, `Q2`, `Q3`, `Q4` |
| CHED (HEI) | `semester` | `SEM1`, `SEM2`, `SUMMER` |
| TESDA (TVET) | `semester` | `SEM1`, `SEM2`, `SUMMER` |

Do not use numeric-only values (`1`, `2`, `3`) without a prefix, as they are ambiguous across agency contexts.

---

## 5.5 Standard Date Fields

The following date fields are used across education sector records. All use `DATE` (not `DATETIME`) unless otherwise noted.

| Field Name | Format | Required? | Notes |
|-----------|--------|-----------|-------|
| `birth_date` | ISO 8601 `DATE` | **YES** | Must not include a time component. Source: PSA birth certificate. |
| `enrollment_date` | ISO 8601 `DATE` | YES | Date of official enrollment confirmation in the current school year. |
| `graduation_date` | ISO 8601 `DATE` | Conditional | Actual completion/graduation date, not ceremony date. |
| `withdrawal_date` | ISO 8601 `DATE` | Conditional | Date a learner officially withdrew; required if `enrollment_status = WITHDRAWN`. |
| `record_created_at` | ISO 8601 `DATETIME` with TZ | **YES** | System-generated; immutable after creation. |
| `record_updated_at` | ISO 8601 `DATETIME` with TZ | **YES** | System-generated; updated on every record modification. |

---

## 5.6 Age Calculation

Age **shall** be calculated dynamically from `birth_date` at query time. **Do not store age as a static field** — it becomes stale immediately and causes data quality issues.

Where a system requires an age field for display or reporting, it **should** be a computed/virtual column derived from `birth_date` and the current date.

---

*Previous: [Section 04 — Location Data](04-location-data.md)*
*Next: [Section 06 — Personal Names](06-personal-names.md)*
