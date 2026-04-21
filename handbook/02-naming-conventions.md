# Section 02: General Naming and Encoding Conventions

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 2.1 Character Encoding

All systems **shall** use **UTF-8** character encoding (IETF RFC 3629) for storage and data exchange.

**Rationale:** UTF-8 ensures correct handling of Filipino diacritics (e.g., ñ, ng ligature) and characters from local Philippine languages (Cebuano, Ilocano, Hiligaynon, Waray, Tausug, Kapampangan, and others). Systems that use legacy encodings (ISO-8859-1, Windows-1252) risk data corruption when these characters are present.

> **Reference:** IETF RFC 3629 — UTF-8, a transformation format of ISO 10646

---

## 2.2 Field Naming Convention

Database column names and API field names **shall** follow **snake_case** notation: lowercase words separated by underscores.

Human-readable labels in forms and reports **shall** use Title Case.

| Field Name (Technical / Storage) | Label (Human-Readable / Display) |
|----------------------------------|----------------------------------|
| `school_name` | School Name |
| `student_lrn` | Learner Reference Number |
| `birth_date` | Date of Birth |
| `region_code` | Region |
| `city_municipality_name` | City / Municipality |
| `mother_tongue_code` | Mother Tongue |

**Prohibited naming patterns:**
- `camelCase` (e.g., `schoolName`) — not permitted for storage fields
- `PascalCase` (e.g., `SchoolName`) — not permitted for storage fields
- Generic names like `field1`, `data`, `value` — always use descriptive names
- Abbreviations that are not widely understood (e.g., `brgy_cd` → use `barangay_code`)

---

## 2.3 NULL vs. Blank Values

Systems **shall** distinguish between:

| Value | Meaning | When to Use |
|-------|---------|-------------|
| `NULL` | Unknown, not available, or not applicable | When the value genuinely does not exist or is not known |
| `""` (empty string) | The field was presented but left blank by the user | Avoid in production records — treat as NULL on save |
| A populated value | The actual data | Normal case |

Fields marked **REQUIRED** in this handbook shall not be `NULL` or blank in finalized production records.

**Do not use placeholder strings** such as `"N/A"`, `"NONE"`, `"0"`, or `"-"` to represent the absence of a value. Use `NULL`.

---

## 2.4 Field Length and Data Types

| Data Category | Recommended Type | Notes |
|---------------|-----------------|-------|
| Short codes (country, sex) | `CHAR(n)` or `VARCHAR(n)` | Fixed-length codes use `CHAR`; variable use `VARCHAR` |
| Names, addresses | `VARCHAR(n)` with documented max | See individual sections for max lengths |
| Numeric IDs that may have leading zeros | `VARCHAR(n)` | **Never store as INTEGER** — leading zeros will be lost |
| Dates | `DATE` (native DB type) | Not `VARCHAR`; not `DATETIME` unless time is needed |
| Timestamps | `TIMESTAMP WITH TIME ZONE` or `DATETIME` | See [Section 05](05-dates.md) |
| Decimal coordinates | `DECIMAL(10,7)` | See [Section 04](04-location-data.md) |
| Boolean flags | `BOOLEAN` or `TINYINT(1)` | Use `TRUE`/`FALSE`; avoid `"Y"`/`"N"` strings |

---

## 2.5 Code Tables vs. Free Text

Where this handbook specifies a defined set of allowed values (e.g., `sex`, `region_code`, `civil_status`), systems **shall** validate input against that set. Free-text entry **shall not** be permitted for coded fields.

Code table values **shall** be stored in their canonical form as defined in this handbook (e.g., `"PH"` not `"Philippines"` for country_code; `"M"` not `"Male"` for sex).

---

## 2.6 Language of Data Entry

Data **shall** be entered in **Filipino or English** as appropriate to the field and the official documentation being transcribed (e.g., birth certificate, school registration). Systems should not force a language choice that conflicts with the source document.

---

*Previous: [Section 01 — Scope and Governance](01-scope-governance.md)*
*Next: [Section 03 — School Identification](03-school-identification.md)*
