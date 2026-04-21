# Section 09: Sex, Gender, and Civil Status

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 9.1 Sex at Birth

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `sex` |
| **Standard** | **ISO 5218:2004** — Codes for the representation of human sexes |
| **Allowed values** | `M` (Male), `F` (Female), `U` (Unknown / Undetermined) |
| **Data type** | `CHAR(1)` |
| **Source** | As recorded on the PSA birth certificate |
| **Required?** | **YES** |

ISO 5218 also defines code `9` (Not applicable). In the Philippine education context, use `NULL` rather than `U` or `9` only when the value is genuinely unavailable at the time of record creation — and update once confirmed.

> **Note:** `sex` records the biological sex as registered at birth in the civil registry. It is a distinct field from `gender_identity` (see 9.2).

---

## 9.2 Gender Identity (Optional)

Where collected for inclusivity, SOGIE-sensitive programming, or DepEd/CHED gender-responsive policies, gender identity **may** be stored in a separate, optional field.

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `gender_identity` |
| **Format** | Free text or locally-defined controlled vocabulary, `VARCHAR(50)` |
| **Required?** | NO — strictly voluntary |
| **Privacy** | **CONFIDENTIAL** — sensitive personal data under RA 10173. Access must be strictly role-restricted. Must not appear in standard reports without explicit consent. |

This field is **distinct from** `sex`. Systems **shall not** pre-fill or infer `gender_identity` from the `sex` field.

Refer to:
- DepEd Order No. 32, s. 2017 (Gender-Responsive Basic Education Policy)
- CHED Memorandum Order on gender and development
- DICT e-Government guidelines for handling sensitive personal categories

---

## 9.3 Civil Status

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `civil_status` |
| **Standard** | Based on PSA Civil Registry categories under the Family Code of the Philippines |
| **Data type** | `VARCHAR(20)` — controlled vocabulary |
| **Required?** | Conditional — required for CHED and TESDA adult learner records; optional for K–12 |

| Value | Description |
|-------|-------------|
| `SINGLE` | Never married |
| `MARRIED` | Currently married |
| `WIDOWED` | Spouse deceased |
| `SEPARATED` | Legally or de facto separated |
| `ANNULLED` | Marriage annulled by court order |
| `LIVE_IN` | In a live-in partnership (not legally married) |

---

*Previous: [Section 08 — Other Student Identifiers](08-other-identifiers.md)*
*Next: [Section 10 — Contact Information](10-contact-information.md)*
