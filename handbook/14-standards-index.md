# Section 14: Quick Reference — Standards Index

**Status:** Informative
**Edition:** 1.0 (2026)

This section consolidates all standards and references cited in this handbook for quick lookup.

---

## 14.1 ISO Standards

| Standard | Title | Applied To |
|----------|-------|-----------|
| **ISO 8601:2019** | Date and time — Representations for information interchange | All date and timestamp fields (Section 05) |
| **ISO 3166-1 alpha-2** | Codes for the representation of names of countries and their subdivisions | `country_code`, `nationality_code` (Sections 04, 11) |
| **ISO 639-1** | Codes for the representation of names of languages (major languages) | `language_of_instruction` (Section 11) |
| **ISO 639-3** | Codes for the representation of names of languages (individual languages) | `mother_tongue_code` (Section 11) |
| **ISO 5218:2004** | Codes for the representation of human sexes | `sex` field (Section 09) |
| **ISO 6709:2022** | Standard representation of geographic point location by coordinates | `latitude`, `longitude` (Section 04) |
| **ISO/IEC 11179** | Metadata registries — Data element principles | Field naming and data element definitions (Section 02) |
| **ISO/IEC 24760-1:2019** | IT Security — Identity management framework | LRN, PhilSys, identifier design (Sections 07, 08) |
| **ISO/IEC 27001:2022** | Information security management systems | Data classification, security controls (Section 13) |
| **ISO/IEC 27701:2019** | Privacy information management (PIMS) | Data privacy compliance, PIC obligations (Section 13) |

---

## 14.2 IETF / ITU Standards

| Standard | Title | Applied To |
|----------|-------|-----------|
| **ITU-T E.164** | The international public telecommunication numbering plan | `mobile_number`, `landline_number` (Section 10) |
| **IETF RFC 5321** | Simple Mail Transfer Protocol | `email_address` max length (Section 10) |
| **IETF RFC 5322** | Internet Message Format | `email_address` format validation (Section 10) |
| **IETF RFC 3629** | UTF-8, a transformation format of ISO 10646 | All text fields — character encoding (Section 02) |

---

## 14.3 UNESCO Standards

| Standard | Title | Applied To |
|----------|-------|-----------|
| **ISCED 2011** | International Standard Classification of Education | `education_level`, ISCED level mapping (Section 12) |
| **ISCED-F 2013** | International Standard Classification of Education — Fields | `isced_field_code` (Section 12) |

---

## 14.4 Philippine Government References

| Reference | Issuing Body | Applied To |
|-----------|-------------|-----------|
| **PSGC (Philippine Standard Geographic Code)** | PSA — updated quarterly | `barangay_code`, `city_municipality_code`, `province_code`, `region_code` (Section 04) |
| **PhilPost ZIP Code Directory** | Philippine Postal Corporation | `zip_code` (Section 04) |
| **PhilSys** | PSA — RA 11055 | `philsys_number` (Section 08) |
| **BEIS (Basic Education Information System)** | DepEd | `school_id` (Section 03) |
| **HEMIS (Higher Education MIS)** | CHED | `ched_institution_code`, `ched_student_no` (Sections 03, 08) |
| **TESD-MIS / TRACER** | TESDA | `tesda_registry_no`, `tesda_learner_ref` (Sections 03, 08) |
| **LIS (Learner Information System)** | DepEd | `student_lrn` (Section 07) |

---

## 14.5 Philippine Laws and Regulations

| Law / Regulation | Title | Relevant Sections |
|-----------------|-------|------------------|
| **RA 10173** | Data Privacy Act of 2012 | Section 13 throughout |
| **RA 11055** | Philippine Identification System Act | Section 08 (`philsys_number`) |
| **RA 9048** | Clerical Error Law | Section 06 (name corrections) |
| **RA 10172** | Amendment to RA 9048 (birth date / sex correction) | Section 06 |
| **RA 11032** | Ease of Doing Business and Efficient Government Service Delivery Act (FOIA provisions) | Section 13 (public data) |
| **RA 10533** | Enhanced Basic Education Act of 2013 (K–12 Law) | Sections 03, 07, 12 |
| **DepEd Order No. 40, s. 2012** | Child Protection Policy | Section 13 |
| **DepEd Order No. 32, s. 2017** | Gender-Responsive Basic Education Policy | Section 09 |

---

## 14.6 Master Field Reference

A consolidated list of all standardized fields defined in this handbook:

| Field Name | Type | Section | Required? |
|-----------|------|---------|-----------|
| `school_name` | `VARCHAR(200)` | 03 | YES |
| `school_name_abbr` | `VARCHAR(50)` | 03 | NO |
| `school_id` | `VARCHAR(10)` | 03 | Conditional |
| `ched_institution_code` | `VARCHAR(20)` | 03 | Conditional |
| `tesda_registry_no` | `VARCHAR(20)` | 03 | Conditional |
| `school_sector` | `VARCHAR(30)` | 03 | YES |
| `address_line1` | `VARCHAR(200)` | 04 | YES |
| `address_line2` | `VARCHAR(200)` | 04 | NO |
| `barangay_name` | `VARCHAR(100)` | 04 | YES |
| `barangay_code` | `CHAR(9)` | 04 | YES |
| `city_municipality_name` | `VARCHAR(100)` | 04 | YES |
| `city_municipality_code` | `CHAR(7)` | 04 | YES |
| `city_municipality_type` | `VARCHAR(30)` | 04 | YES |
| `province_name` | `VARCHAR(100)` | 04 | Conditional |
| `province_code` | `CHAR(4)` | 04 | Conditional |
| `region_name` | `VARCHAR(100)` | 04 | YES |
| `region_code` | `CHAR(2)` | 04 | YES |
| `zip_code` | `CHAR(4)` | 04 | YES |
| `country_code` | `CHAR(2)` | 04 | YES |
| `latitude` | `DECIMAL(10,7)` | 04 | NO |
| `longitude` | `DECIMAL(10,7)` | 04 | NO |
| `birth_date` | `DATE` | 05 | YES |
| `enrollment_date` | `DATE` | 05 | YES |
| `graduation_date` | `DATE` | 05 | Conditional |
| `academic_year` | `CHAR(9)` | 05 | YES |
| `grading_period` | `VARCHAR(10)` | 05 | YES |
| `record_created_at` | `TIMESTAMP` | 05 | YES |
| `record_updated_at` | `TIMESTAMP` | 05 | YES |
| `last_name` | `VARCHAR(100)` | 06 | YES |
| `first_name` | `VARCHAR(100)` | 06 | YES |
| `middle_name` | `VARCHAR(100)` | 06 | Conditional |
| `name_suffix` | `VARCHAR(10)` | 06 | NO |
| `name_prefix` | `VARCHAR(10)` | 06 | NO |
| `preferred_name` | `VARCHAR(100)` | 06 | NO |
| `student_lrn` | `VARCHAR(12)` | 07 | YES (DepEd) |
| `philsys_number` | `VARCHAR(16)` | 08 | NO |
| `school_student_id` | `VARCHAR(50)` | 08 | YES (local) |
| `ched_student_no` | `VARCHAR(50)` | 08 | Conditional |
| `tesda_learner_ref` | `VARCHAR(50)` | 08 | Conditional |
| `sex` | `CHAR(1)` | 09 | YES |
| `gender_identity` | `VARCHAR(50)` | 09 | NO |
| `civil_status` | `VARCHAR(20)` | 09 | Conditional |
| `mobile_number` | `VARCHAR(15)` | 10 | Conditional |
| `landline_number` | `VARCHAR(15)` | 10 | NO |
| `email_address` | `VARCHAR(254)` | 10 | Conditional |
| `nationality_code` | `CHAR(2)` | 11 | YES |
| `mother_tongue_code` | `CHAR(3)` | 11 | YES (DepEd) |
| `language_of_instruction` | `VARCHAR(3)` | 11 | Conditional |
| `ip_community_affiliation` | `VARCHAR(100)` | 11 | NO |
| `education_level` | `VARCHAR(30)` | 12 | YES |
| `isced_level` | `TINYINT` | 12 | NO |
| `program_name` | `VARCHAR(200)` | 12 | YES |
| `program_code` | `VARCHAR(20)` | 12 | Conditional |
| `isced_field_code` | `CHAR(4)` | 12 | NO |
| `enrollment_status` | `VARCHAR(20)` | 12 | YES |
| `shs_track` | `VARCHAR(20)` | 12 | Conditional |
| `shs_strand` | `VARCHAR(20)` | 12 | Conditional |

---

*Previous: [Section 13 — Data Privacy and Security](13-data-privacy-security.md)*

---

*End of Handbook — Edition 1.0 (2026)*
*Philippine Education Sector Data Standards — DepEd • CHED • TESDA*
*Licensed under CC BY 4.0*
