# Section 07: Learner Reference Number (LRN)

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 7.1 Definition and Purpose

The **Learner Reference Number (LRN)** is the national, permanent, unique identifier assigned to every learner in the Philippine education system by the Department of Education (DepEd) through the Learner Information System (LIS).

The LRN is the **canonical person identifier** for the Philippine education sector. It does not change across schools, grade levels, school years, or agencies.

---

## 7.2 Field Specification

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `student_lrn` |
| **Issuing authority** | Department of Education (DepEd) — Learner Information System (LIS) |
| **Format** | 12-digit numeric string, zero-padded |
| **Data type** | `VARCHAR(12)` — **never `INTEGER` or `BIGINT`** |
| **Example** | `"123456789012"` |
| **Required?** | **YES** for all DepEd learners. Strongly recommended for CHED and TESDA records. |

> ⚠️ Store as `VARCHAR(12)`. An LRN stored as `INTEGER` or `BIGINT` risks losing leading zeros, producing an invalid and unmatchable identifier.

---

## 7.3 Uniqueness and Permanence

- The LRN is **permanent** — it is assigned once and does not change, even if the learner transfers schools, repeats a grade, or re-enrolls after a gap.
- The LRN is **unique** — no two learners share the same LRN.
- Systems **shall not** create new LRNs locally. LRNs are issued exclusively by DepEd through the LIS.

---

## 7.4 Cross-Agency Use

| Agency | Requirement |
|--------|------------|
| DepEd | **Mandatory** — primary identifier in all LIS records |
| CHED | **Strongly recommended** — store when the student previously enrolled in basic education |
| TESDA | **Strongly recommended** — store when the learner previously enrolled in basic education |

CHED and TESDA systems **should** collect and store the LRN to enable longitudinal tracking of a learner's progression from basic education through higher education or technical-vocational training. This supports national education outcome analytics and conditional cash transfer (CCT / 4Ps) monitoring.

---

## 7.5 LRN vs. School Student ID

The LRN is **not** the same as a school-assigned student ID.

| | LRN | School Student ID |
|--|-----|------------------|
| Scope | National | Institution-local |
| Issuer | DepEd | Individual school |
| Portability | Follows the learner across all schools | Valid only within the issuing school |
| Field name | `student_lrn` | `school_student_id` |
| Required for? | DepEd LIS submissions | Internal school records |

Both identifiers **may** coexist in the same learner record under their respective field names.

---

## 7.6 Standard Reference

The LRN design aligns with **ISO/IEC 24760-1:2019** (Framework for identity management), which defines principles for persistent, unique identity attributes within and across systems.

---

*Previous: [Section 06 — Personal Names](06-personal-names.md)*
*Next: [Section 08 — Other Student Identifiers](08-other-identifiers.md)*
