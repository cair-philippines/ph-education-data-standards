# Section 12: Program and Course Data

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 12.1 Education Level

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `education_level` |
| **Standard** | **ISCED 2011** (International Standard Classification of Education) — UNESCO; mapped to Philippine level equivalents |
| **Data type** | `VARCHAR(30)` — controlled vocabulary |
| **Required?** | **YES** |

### Allowed Values

| Value | Philippine Context | ISCED 2011 Level |
|-------|--------------------|-----------------|
| `KINDERGARTEN` | DepEd Kindergarten | ISCED 0 |
| `GRADE_1` through `GRADE_6` | DepEd Elementary | ISCED 1 |
| `GRADE_7` through `GRADE_10` | DepEd Junior High School | ISCED 2 |
| `GRADE_11` or `GRADE_12` | DepEd Senior High School | ISCED 3 |
| `TVET_NC1` | TESDA National Certificate I | ISCED 3 / 4 |
| `TVET_NC2` | TESDA National Certificate II | ISCED 3 / 4 |
| `TVET_NC3` | TESDA National Certificate III | ISCED 4 / 5 |
| `TVET_NC4` | TESDA National Certificate IV | ISCED 5 |
| `TVET_COC` | TESDA Certificate of Competency | ISCED 3 |
| `BACHELOR` | CHED Bachelor's Degree (4–5 years) | ISCED 6 |
| `POST_BACCALAUREATE` | CHED Post-Baccalaureate certificate/diploma | ISCED 6 |
| `MASTER` | CHED Master's Degree | ISCED 7 |
| `DOCTORATE` | CHED Doctoral Degree | ISCED 8 |

Store the Philippine-context value in `education_level`. Store the ISCED numeric level in a separate optional field `isced_level` (`TINYINT`) for international reporting.

---

## 12.2 Program Name and Code

### For CHED-covered programs:

| Field | Specification |
|-------|--------------|
| `program_name` | Official program name per CHED CMO or institution's program description. `VARCHAR(200)`, UTF-8. |
| `program_code` | CHED program classification code per the relevant CHED Memorandum Order. `VARCHAR(20)`. |

### For TESDA qualifications:

| Field | Specification |
|-------|--------------|
| `tesda_qualification_title` | Full qualification title as per the TESDA Training Regulation (TR). `VARCHAR(200)`. Example: `"Bread and Pastry Production NC II"` |
| `tesda_qualification_code` | TESDA qualification code from the applicable TR. `VARCHAR(20)`. |

### For DepEd Senior High School tracks and strands:

| Field | Allowed Values |
|-------|---------------|
| `shs_track` | `ACADEMIC`, `TVL`, `SPORTS`, `ARTS_DESIGN` |
| `shs_strand` | e.g., `STEM`, `HUMSS`, `ABM`, `GAS`, `TVL_ICT`, `TVL_HE`, `TVL_IA`, `TVL_AFA` |

---

## 12.3 ISCED Fields of Education (for international reporting)

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `isced_field_code` |
| **Standard** | **ISCED-F 2013** (Fields of Education and Training 2013) — UNESCO |
| **Format** | 4-digit numeric string, `CHAR(4)` |
| **Required?** | Recommended for CHED and TESDA records submitted to UNESCO / international bodies |

**Selected ISCED-F 2013 codes relevant to the Philippines:**

| Code | Field |
|------|-------|
| `0111` | Education science |
| `0114` | Teacher training — early childhood |
| `0188` | Teacher training — other |
| `0211` | Fine arts |
| `0231` | Language acquisition |
| `0311` | Economics |
| `0312` | Political science and civic culture |
| `0410` | Business and administration (general) |
| `0613` | Software and applications development |
| `0711` | Chemical engineering |
| `0712` | Environmental protection |
| `0721` | Medicine |
| `0911` | Hotel, restaurants, catering |
| `0912` | Travel, tourism, leisure |

> **Reference:** UNESCO ISCED-F 2013 publication — https://uis.unesco.org/en/topic/international-standard-classification-education-isced

---

## 12.4 Enrollment Status

| Field | `enrollment_status` |
|-------|---------------------|
| **Allowed values** | `ENROLLED`, `DROPPED`, `TRANSFERRED_OUT`, `TRANSFERRED_IN`, `GRADUATED`, `COMPLETED`, `WITHDRAWN`, `ON_LEAVE`, `DECEASED` |
| **Required?** | YES |

---

*Previous: [Section 11 — Language and Nationality](11-language-nationality.md)*
*Next: [Section 13 — Data Privacy and Security](13-data-privacy-security.md)*
