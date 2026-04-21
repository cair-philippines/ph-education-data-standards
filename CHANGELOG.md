# Changelog

All notable changes to the Philippine Education Sector Data Standards Handbook are documented here.

This file follows the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.
Versions follow [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`

- **MAJOR** — breaking changes to field names, formats, or required values
- **MINOR** — new fields, sections, or non-breaking additions
- **PATCH** — corrections, clarifications, typo fixes

---

## [Unreleased]

_Proposed changes not yet released go here._

---

## [1.0.0] — 2026

### Added
- Initial publication of the Philippine Education Sector Data Standards Handbook
- Section 01: Scope and Governance
- Section 02: General Naming and Encoding Conventions (UTF-8, snake_case, NULL handling)
- Section 03: School Identification (school_name, school_id, school_sector)
- Section 04: Location Data (full PSGC hierarchy, ZIP, ISO 3166-1, ISO 6709 coordinates)
- Section 05: Dates and Time (ISO 8601, academic year, timestamp fields)
- Section 06: Personal Names (PSA conventions, diacritics, Title Case rules)
- Section 07: Learner Reference Number / LRN (12-digit, VARCHAR, cross-agency use)
- Section 08: Other Student Identifiers (PhilSys, school_student_id, CHED, TESDA)
- Section 09: Sex, Gender, and Civil Status (ISO 5218, PSA civil registry categories)
- Section 10: Contact Information (ITU-T E.164, IETF RFC 5321)
- Section 11: Language and Nationality (ISO 3166-1, ISO 639-3)
- Section 12: Program and Course Data (ISCED 2011, ISCED-F 2013, CHED/TESDA codes)
- Section 13: Data Privacy, Security, and Retention (RA 10173, ISO 27001, ISO 27701)
- Section 14: Quick Reference Standards Index
- Appendix A: Glossary
- Appendix B: Amendment Log

### Standards Referenced in v1.0
- ISO 8601:2019, ISO 3166-1, ISO 639-1, ISO 639-3, ISO 5218:2004, ISO 6709:2022
- ISO/IEC 11179, ISO/IEC 24760-1:2019, ISO/IEC 27001:2022, ISO/IEC 27701:2019
- ITU-T E.164, IETF RFC 5321/5322, IETF RFC 3629 (UTF-8)
- ISCED 2011, ISCED-F 2013 (UNESCO)
- PSA PSGC, PhilPost ZIP Directory
- RA 10173 (Data Privacy Act), RA 11055 (PhilSys Act)
