# Section 10: Contact Information

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 10.1 Phone Numbers

| Attribute | Specification |
|-----------|--------------|
| **Standard** | **ITU-T E.164** — The international public telecommunication numbering plan |
| **Storage format** | E.164: `+[country code][subscriber number]` |
| **Data type** | `VARCHAR(15)` (E.164 maximum is 15 digits + `+` prefix) |

**Field names:**

| Field | Description | Example |
|-------|-------------|---------|
| `mobile_number` | Mobile / cellular number | `+639171234567` |
| `landline_number` | Fixed-line / landline with area code | `+63221234567` |

> ⚠️ Store mobile and landline numbers in **separate fields**. Do not combine them in a single generic `contact_number` field — this prevents proper validation, formatting, and automated contact workflows.

**Philippine number formats in E.164:**

| Type | Format | Example |
|------|--------|---------|
| Mobile (Globe/TM) | `+6391XXXXXXXX` | `+639171234567` |
| Mobile (Smart/Sun/TNT) | `+6392XXXXXXXX` | `+639211234567` |
| Mobile (DITO) | `+6395XXXXXXXX` | `+639951234567` |
| Metro Manila landline | `+6328XXXXXXX` (new 8-digit) | `+63287654321` |
| Provincial landline | `+63[area code][number]` | `+63321234567` (Cebu) |

**Display formats (presentation layer only):**

| Type | Display Format |
|------|---------------|
| Mobile | `0917-123-4567` or `(0917) 123-4567` |
| Landline (Metro Manila) | `(02) 8765-4321` |
| Landline (provincial) | `(032) 123-4567` |

> ⚠️ Display formatting **shall not** affect the stored E.164 value. The `+` prefix is mandatory in storage.

---

## 10.2 Email Address

| Attribute | Specification |
|-----------|--------------|
| **Standard** | IETF RFC 5321 (SMTP) and RFC 5322 (Internet Message Format) |
| **Format** | Lowercase for storage. Validate format on input. |
| **Data type** | `VARCHAR(254)` — RFC 5321 maximum is 254 characters |
| **Field name** | `email_address` |
| **Required?** | Conditional — required for CHED and TESDA learners; recommended for senior high and adult basic education learners |

**Uniqueness:** Email addresses **shall** be unique per person record within a system. Duplicate email addresses indicate a data entry error or a shared family email — flag for review.

**Case handling:** Store in lowercase. On input, convert to lowercase before saving (`juan.delacruz@gmail.com`, not `Juan.DeLaCruz@Gmail.com`).

**Validation pattern (minimum):** Must contain exactly one `@`, a domain with at least one `.`, and no invalid characters. Full RFC 5322 validation is recommended.

---

## 10.3 Emergency Contact

For learner records, an emergency contact **should** be stored using the following fields:

| Field Name | Type | Notes |
|-----------|------|-------|
| `emergency_contact_name` | `VARCHAR(200)` | Full name, same naming conventions as Section 06 |
| `emergency_contact_relationship` | `VARCHAR(50)` | e.g., `MOTHER`, `FATHER`, `GUARDIAN`, `SIBLING`, `SPOUSE` |
| `emergency_contact_mobile` | `VARCHAR(15)` | E.164 format |
| `emergency_contact_email` | `VARCHAR(254)` | RFC 5322 format |

---

*Previous: [Section 09 — Sex, Gender, and Civil Status](09-sex-gender-civil-status.md)*
*Next: [Section 11 — Language and Nationality](11-language-nationality.md)*
