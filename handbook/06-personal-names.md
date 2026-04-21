# Section 06: Personal Names

**Status:** Normative
**Edition:** 1.0 (2026)

Applies to: students, learners, faculty, staff, parents/guardians, and all individuals recorded in education sector systems.

---

## 6.1 Name Fields

| Field Name | Description | Max Length | Required? |
|-----------|-------------|-----------|-----------|
| `last_name` | Family name / surname as on PSA birth certificate or passport | `VARCHAR(100)` | **YES** |
| `first_name` | Given name(s) — all given names, space-separated | `VARCHAR(100)` | **YES** |
| `middle_name` | Middle name (typically the mother's maiden surname in Philippine practice) | `VARCHAR(100)` | Conditional (see 6.2) |
| `name_suffix` | Generational suffix: `JR`, `SR`, `II`, `III`, `IV`, `V`. Store without periods. | `VARCHAR(10)` | NO |
| `name_prefix` | Honorific: `MR`, `MRS`, `MS`, `DR`, `PROF`. Store without periods. | `VARCHAR(10)` | NO |
| `preferred_name` | Name the person prefers to be called, if different from legal name. Not used in official records. | `VARCHAR(100)` | NO |

> ⚠️ **Never concatenate name fields for storage.** Store all name components separately. Concatenation for display (e.g., `"DELA CRUZ, JUAN P."`) is a presentation-layer operation only.

---

## 6.2 Middle Name Policy

Middle name **shall** be stored as provided on the PSA birth certificate.

If a person has no middle name (e.g., single-parent birth registration, foreign nationals, or individuals with legally registered single names), `middle_name` **shall** be `NULL` — not `"N/A"`, `"NONE"`, `-`, or empty string.

Systems **shall** accommodate `NULL` middle names without error or validation failure.

---

## 6.3 Name Storage Rules

| Rule | Specification |
|------|--------------|
| **Case — Storage** | Store in **UPPERCASE**, consistent with PSA civil registry documents. |
| **Case — Display** | Convert to Title Case for display. Particles such as `de`, `dela`, `ng`, `van`, `san` **should** be rendered in lowercase unless they appear at the start of the displayed name. |
| **Diacritics** | **Preserve all diacritics** as provided (ñ, é, etc.). Do not strip, transliterate, or substitute accented characters. UTF-8 encoding (Section 02) is required. |
| **Compound surnames** | Hyphenated surnames (e.g., `SANTOS-REYES`) and space-separated surnames (e.g., `DE LA CRUZ`) are stored verbatim as registered. |
| **Sorting** | Sort by `last_name` ASC, then `first_name` ASC, then `middle_name` ASC. Use locale-aware collation (Philippine locale). |

---

## 6.4 Name Matching and Deduplication

Name fields alone are unreliable for deduplication. The **Learner Reference Number (LRN)** (Section 07) or **PhilSys Number** (Section 08) **shall** be the primary matching key when available.

Where ID-based matching is not possible, a combination of `last_name` + `first_name` + `birth_date` + `birth_municipality` **should** be used. Exact-string matching on names alone is insufficient due to spelling variations, nickname use, and diacritics handling differences across legacy systems.

---

## 6.5 Legal Basis

Name conventions follow the Philippine Civil Registry as administered by the PSA under:
- Republic Act No. 9048 (Clerical Error Law) — authorizes correction of clerical errors in civil registry documents
- Republic Act No. 10172 — extends RA 9048 to correct birth date and sex entries

For international learners and foreign nationals, ISO/IEC 24760 (IT Security — Identity Management) provides guidance on identity attribute management across jurisdictions.

---

*Previous: [Section 05 — Dates and Time](05-dates.md)*
*Next: [Section 07 — Learner Reference Number](07-lrn.md)*
