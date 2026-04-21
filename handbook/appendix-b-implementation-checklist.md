# Appendix B: Implementation Checklist for System Developers

This checklist is a practical companion for developers and database administrators building or auditing education information systems against this handbook. It is **informative**, not normative.

---

## Database Setup

- [ ] All text fields use UTF-8 / `utf8mb4` collation (covers emoji and full Unicode range)
- [ ] All numeric ID fields that may have leading zeros (LRN, school_id, PSGC codes, ZIP) are `VARCHAR` or `CHAR`, **not** `INT` or `BIGINT`
- [ ] `NULL` and empty string (`""`) are handled distinctly — empty strings are rejected for required fields
- [ ] `TIMESTAMP WITH TIME ZONE` or equivalent is used for all datetime fields (not plain `VARCHAR`)
- [ ] Age is computed dynamically from `birth_date`, not stored as a static column

---

## School Records

- [ ] `school_name` matches the official DepEd / CHED / TESDA registration name
- [ ] `school_name` is in Title Case, not ALL CAPS
- [ ] `school_id` is stored as `VARCHAR`, zero-padded to 6 digits
- [ ] At least one agency ID (`school_id`, `ched_institution_code`, or `tesda_registry_no`) is present per record
- [ ] `school_sector` uses only the allowed values from Section 03.4

---

## Location Data

- [ ] Barangay code is the **full 9-digit PSGC code** (not a 2-digit segment)
- [ ] City/municipality code is the **7-digit PSGC prefix**
- [ ] Region code is the **2-digit PSGC code** (e.g., `"01"` not `"I"` or `"Region I"`)
- [ ] Province code is `NULL` (not `"N/A"`) for NCR / HUC entries
- [ ] Both name and code are stored for every geographic level (barangay, city/municipality, province, region)
- [ ] ZIP code is stored as `CHAR(4)` or `VARCHAR(4)`, not integer
- [ ] Country code is ISO 3166-1 alpha-2 (`"PH"`, not `"Philippines"`)
- [ ] PSGC codes validated against latest PSA quarterly release

---

## Dates

- [ ] All stored dates are in `YYYY-MM-DD` format (ISO 8601) — no `MM/DD/YYYY` in the database
- [ ] All stored timestamps include timezone offset (`+08:00`) or are documented as UTC
- [ ] `academic_year` uses the `YYYY-YYYY` format (e.g., `"2025-2026"`)
- [ ] `birth_date` does not include a time component
- [ ] Display formatting (DD Month YYYY) is applied only at the presentation layer

---

## Personal Names

- [ ] Names stored in UPPERCASE
- [ ] Name fields are stored separately (`last_name`, `first_name`, `middle_name`) — not concatenated
- [ ] `middle_name` is `NULL` (not `"N/A"` or blank) when absent
- [ ] Diacritics (ñ, é) are preserved — not stripped or replaced
- [ ] Compound surnames (`DE LA CRUZ`, `SANTOS-REYES`) are stored verbatim

---

## Learner Reference Number

- [ ] `student_lrn` is `VARCHAR(12)`, not `INTEGER`
- [ ] LRN validation rejects non-12-digit values
- [ ] LRN is stored separately from `school_student_id`
- [ ] CHED and TESDA systems capture LRN when available

---

## Sex, Gender, Civil Status

- [ ] `sex` uses only `M`, `F`, or `U` (ISO 5218) — not `"Male"`, `"Female"`, `1`, `2`
- [ ] `gender_identity` (if collected) is a separate field from `sex`
- [ ] `civil_status` uses the controlled vocabulary from Section 09.3

---

## Contact Information

- [ ] Phone numbers stored in E.164 format (`+639XXXXXXXXX`)
- [ ] Mobile and landline stored in separate fields
- [ ] Email addresses stored in lowercase
- [ ] Email length validated to 254 characters maximum

---

## Language and Nationality

- [ ] `nationality_code` uses ISO 3166-1 alpha-2 (2-letter uppercase)
- [ ] `mother_tongue_code` uses ISO 639-3 (3-letter lowercase)
- [ ] `language_of_instruction` uses ISO 639-1 or ISO 639-3

---

## Data Privacy

- [ ] PhilSys number (`philsys_number`) is not required for enrollment
- [ ] `philsys_number` is encrypted at rest
- [ ] Role-based access controls applied to STRICTLY CONFIDENTIAL and CONFIDENTIAL fields
- [ ] Data subjects can request access, correction, and deletion of their records
- [ ] Retention periods are configured and enforced per Section 13.5
- [ ] A Privacy Impact Assessment (PIA) has been completed for systems handling SPI
- [ ] A Data Protection Officer (DPO) is designated

---

## API Design (if applicable)

- [ ] API field names use `snake_case`
- [ ] API responses use ISO 8601 for all date/time values
- [ ] API responses use controlled vocabulary values (not display labels) for coded fields
- [ ] Sensitive fields are excluded from default API responses and require explicit scope/permission
- [ ] API documentation specifies data types, allowed values, and max lengths consistent with this handbook
