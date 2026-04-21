# Section 11: Language and Nationality

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 11.1 Nationality / Citizenship

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `nationality_code` |
| **Standard** | **ISO 3166-1 alpha-2** — Two-letter country codes (same standard as `country_code` in Section 04) |
| **Format** | `CHAR(2)`, uppercase |
| **Example** | `"PH"` (Filipino), `"US"` (American), `"CN"` (Chinese), `"JP"` (Japanese) |
| **Required?** | **YES** |

Store nationality as the **country of citizenship**, not ethnicity or place of birth.

For dual citizens, store the **primary citizenship** in `nationality_code` and the secondary in an optional `nationality_code_2` field.

---

## 11.2 Mother Tongue / First Language

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `mother_tongue_code` |
| **Standard** | **ISO 639-3** — Codes for the representation of names of languages (individual languages) |
| **Format** | 3-letter lowercase code, `CHAR(3)` |
| **Required?** | **Required for DepEd** (MTB-MLE compliance); recommended for CHED and TESDA |

**Common Philippine language codes (ISO 639-3):**

| Code | Language |
|------|---------|
| `fil` | Filipino (Tagalog-based national language) |
| `tgl` | Tagalog |
| `ceb` | Cebuano |
| `ilo` | Ilocano |
| `hil` | Hiligaynon (Ilonggo) |
| `war` | Waray |
| `pam` | Kapampangan |
| `bcl` | Central Bikol |
| `tsg` | Tausug |
| `mdh` | Maguindanao |
| `mrw` | Maranao |
| `bik` | Bikol (general) |
| `pag` | Pangasinan |
| `eng` | English |

> **Reference:** SIL International Ethnologue / ISO 639-3 Registration Authority (https://iso639-3.sil.org)

> **Note:** ISO 639-3 provides individual language codes with finer granularity than ISO 639-1 (which covers only major world languages and does not distinguish between, e.g., Cebuano and Hiligaynon). ISO 639-3 is the required standard for MTB-MLE implementation.

---

## 11.3 Language of Instruction

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `language_of_instruction` |
| **Standard** | **ISO 639-1** (2-letter codes) for major instruction languages; ISO 639-3 if more specificity is needed |
| **Format** | `CHAR(2)` for ISO 639-1; `CHAR(3)` for ISO 639-3 |
| **Common values** | `en` (English), `fil` (Filipino) |
| **Required?** | Required for DepEd school and classroom records; recommended for CHED |

For MTB-MLE classrooms at Grades K–3, store the regional language using ISO 639-3 (e.g., `ceb` for Cebuano-medium instruction).

---

## 11.4 Ethnicity / Indigenous Peoples Affiliation (Optional)

Where relevant for IP education programs (e.g., IPBED under DepEd Order No. 62, s. 2011), a learner's IP community affiliation **may** be recorded.

| Field Name | `ip_community_affiliation` |
|------------|--------------------------|
| Format | Free text or reference to the NCIP-recognized IP group name, `VARCHAR(100)` |
| Required? | NO — voluntary; handle with enhanced privacy protections |

> This field is sensitive in certain contexts. Consult the National Commission on Indigenous Peoples (NCIP) guidelines and RA 10173 for appropriate handling.

---

*Previous: [Section 10 — Contact Information](10-contact-information.md)*
*Next: [Section 12 — Program and Course Data](12-program-course-data.md)*
