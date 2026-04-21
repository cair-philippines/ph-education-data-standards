# Section 08: Other Student and Institutional Identifiers

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 8.1 PhilSys Number (PSN)

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `philsys_number` |
| **Issuing authority** | Philippine Statistics Authority (PSA) — Philippine Identification System (PhilSys) |
| **Legal basis** | Republic Act No. 11055 (Philippine Identification System Act) |
| **Format** | 16-digit numeric string |
| **Data type** | `VARCHAR(16)` |
| **Required?** | NO — collect when voluntarily provided. Must **not** be required as a prerequisite for enrollment. |
| **Privacy classification** | **STRICTLY CONFIDENTIAL** — sensitive personal data under RA 10173. Access must be role-restricted with audit logging. |

> ⚠️ RA 11055 explicitly prohibits requiring the PhilSys Number for access to services or benefits unless authorized by law. Enrollment must proceed regardless of whether the PSN is provided.

---

## 8.2 School Student ID

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `school_student_id` |
| **Format** | Locally assigned by the institution. Alphanumeric, `VARCHAR(50)`. |
| **Uniqueness** | Must be unique within the institution. Not unique across institutions. |
| **Required?** | YES at the institutional level. Optional in inter-agency data exchange. |

The school student ID **shall never** be used as a cross-institution or national identifier. It is a local, institution-scoped reference only.

---

## 8.3 CHED Student Number

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `ched_student_no` |
| **Issuing authority** | Assigned by HEIs; referenced in CHED's Higher Education Management Information System (HEMIS) |
| **Format** | As defined by the individual institution and CHED HEMIS requirements |
| **Required?** | YES for CHED-covered institutions in HEMIS data submissions |

---

## 8.4 TESDA Learner Reference

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `tesda_learner_ref` |
| **Issuing authority** | TESDA — Training Registration and Accreditation System (TRACER / TESD-MIS) |
| **Format** | As assigned by TESDA's registry system |
| **Required?** | YES for all TESDA-registered learners |

---

## 8.5 Identifier Priority for Record Matching

When matching learner records across systems or agencies, identifiers **shall** be used in this priority order:

| Priority | Identifier | Use When |
|---------|-----------|----------|
| 1st | `student_lrn` | Available — most reliable cross-agency key |
| 2nd | `philsys_number` | Available and consent given |
| 3rd | `last_name` + `first_name` + `birth_date` + `birth_municipality_code` | No national ID available |

Name-only matching (without a date or location component) **shall not** be used as the sole matching criterion due to high collision rates.

---

## 8.6 Future Identifiers

The DICT e-Government Interoperability Framework envisions a unified learner identity layer across agencies. As PhilSys registration reaches full population coverage, the PhilSys Number **may** evolve into the primary cross-agency education identifier. This handbook will be updated accordingly.

---

*Previous: [Section 07 — Learner Reference Number](07-lrn.md)*
*Next: [Section 09 — Sex, Gender, and Civil Status](09-sex-gender-civil-status.md)*
