# Section 03: School Identification

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 3.1 School Name

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `school_name` |
| **Standard** | ISO/IEC 11179 (Metadata Registries) — consistent naming principles |
| **Data type** | `VARCHAR(200)`, UTF-8 |
| **Case** | Title Case. Capitalize each principal word. Do **not** use ALL CAPS. |
| **Abbreviations** | Spell out in full as the canonical name. Store abbreviation separately in `school_name_abbr` (VARCHAR 50). |
| **Language** | Filipino or English as officially registered with DepEd / CHED / TESDA |
| **Required?** | **YES — mandatory** |

The school name in the system **shall** match the name in the current Certificate of Registration (for private schools) or the relevant DepEd / CHED / TESDA recognition order. Colloquial or shortened names **shall not** be used as the canonical value.

> **Example:** Store `"Ateneo de Manila University"` — not `"ADMU"` or `"Ateneo"` in `school_name`. The abbreviation `"ADMU"` may be stored in `school_name_abbr`.

---

## 3.2 School ID

Because the three agencies maintain separate registry systems, school identifiers are agency-specific. All applicable IDs **shall** be stored.

| Agency | Field Name | Format | Notes |
|--------|-----------|--------|-------|
| DepEd | `school_id` | 6-digit numeric string, zero-padded. Example: `"123456"` | DepEd School ID (SCHID) from the Basic Education Information System (BEIS) |
| CHED | `ched_institution_code` | Alphanumeric, as assigned by CHED HEMIS | Higher Education Management Information System code |
| TESDA | `tesda_registry_no` | Alphanumeric, as assigned by TESDA TESD-MIS | TESDA institutional registry number |

**Required?** At least one applicable ID is **mandatory**. All applicable IDs for the institution's accreditation scope **shall** be stored.

> ⚠️ **Critical:** Store all ID fields as `VARCHAR`, not `INTEGER`. Leading zeros in DepEd School IDs must be preserved. Storing as integer will silently drop leading zeros and invalidate the identifier.

> ⚠️ Do not invent, pad, or guess IDs. Use only officially assigned identifiers from the respective agency registry.

---

## 3.3 Cross-Agency Institution Records

Where a single institution holds recognition from more than one agency (e.g., a school with both CHED-accredited programs and TESDA-registered TVET courses), all applicable IDs **shall** be stored in their respective fields in the same institution record.

---

## 3.4 School Type / Sector

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `school_sector` |
| **Data type** | `VARCHAR(30)` — controlled vocabulary |
| **Allowed values** | See table below |
| **Standard** | Based on DepEd / CHED classification categories; aligned with PSA FLEMMS and BEIS sector codes |
| **Required?** | **YES** |

| Value | Description |
|-------|-------------|
| `PUBLIC` | Government-funded basic education school (DepEd) |
| `PRIVATE` | Privately operated basic education school |
| `STATE_UNIVERSITY_COLLEGE` | SUC — chartered by national law |
| `LOCAL_UNIVERSITY_COLLEGE` | LUC — established by local government unit |
| `PRIVATE_HEI` | Privately operated higher education institution |
| `TVET_PUBLIC` | Public technical-vocational institution |
| `TVET_PRIVATE` | Private technical-vocational institution |

---

## 3.5 School Alias / Former Name

Where a school has undergone a name change (e.g., by virtue of a conversion law or board resolution), the former name **should** be stored in a separate `school_former_name` field (`VARCHAR(200)`) with an associated `school_former_name_until` date field (`DATE`). This supports historical record matching.

---

*Previous: [Section 02 — Naming and Encoding Conventions](02-naming-conventions.md)*
*Next: [Section 04 — Location Data](04-location-data.md)*
