# 🇵🇭 Philippine Education Sector Data Standards Handbook

**A proposed, open, community-maintained data standards reference for DepEd, CHED, and TESDA.**

> **Status:** Draft — Edition 1.0 (2026)
> **Maintained by:** Open contributors — see [CONTRIBUTING.md](CONTRIBUTING.md)
> **License:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE)

---

## What Is This?

This repository contains a **proposed data standards handbook** for the Philippine education sector — covering the Department of Education (DepEd), Commission on Higher Education (CHED), and the Technical Education and Skills Development Authority (TESDA).

It defines how common data elements — school names, school IDs, location data, student names, learner reference numbers, dates, and more — should be formatted, stored, and exchanged across education information systems in the Philippines.

The standards are grounded in **internationally recognized ISO standards**, **PSA geographic codes**, Philippine laws (RA 10173, RA 11055), and established government ICT frameworks.

**This is not an official government issuance.** It is a community-proposed standard intended to inform, support, and eventually influence official policy. We welcome participation from developers, data engineers, education administrators, researchers, and civil society.

---

## Why This Matters

Data inconsistency across Philippine education systems causes real problems:

- A student's name is spelled differently in DepEd's LIS, a university's SIS, and TESDA's registry
- Location data uses different barangay codes, ZIP codes, or free-text region names across agencies
- Dates are stored as `06/12/2026`, `12-Jun-26`, and `2026-06-12` in different systems — sometimes in the same agency
- There is no agreed format for phone numbers, making deduplication and contact validation unreliable

Standardization enables interoperability, longitudinal learner tracking, better policy analytics, and more reliable open data.

---

## Handbook Sections

| # | Section | Summary |
|---|---------|---------|
| [01](handbook/01-scope-governance.md) | Scope and Governance | Covered agencies, standards bodies referenced |
| [02](handbook/02-naming-conventions.md) | Naming and Encoding Conventions | Field naming, character encoding, nulls |
| [03](handbook/03-school-identification.md) | School Identification | School name, school ID (DepEd/CHED/TESDA), school type |
| [04](handbook/04-location-data.md) | Location Data | Full address hierarchy, PSGC codes, ZIP, country, coordinates |
| [05](handbook/05-dates.md) | Dates and Time | ISO 8601, academic year, timestamps, date fields |
| [06](handbook/06-personal-names.md) | Personal Names | Name fields, case rules, diacritics, PSA conventions |
| [07](handbook/07-lrn.md) | Learner Reference Number (LRN) | Format, uniqueness, cross-agency use |
| [08](handbook/08-other-identifiers.md) | Other Student Identifiers | PhilSys, school ID, CHED student no., TESDA learner ref |
| [09](handbook/09-sex-gender-civil-status.md) | Sex, Gender, Civil Status | ISO 5218, gender identity, civil status codes |
| [10](handbook/10-contact-information.md) | Contact Information | E.164 phone numbers, RFC 5321 email |
| [11](handbook/11-language-nationality.md) | Language and Nationality | ISO 3166, ISO 639-3, mother tongue, language of instruction |
| [12](handbook/12-program-course-data.md) | Program and Course Data | ISCED 2011, ISCED-F 2013, CHED/TESDA program codes |
| [13](handbook/13-data-privacy-security.md) | Data Privacy and Security | RA 10173, ISO 27001, data classification, retention |
| [14](handbook/14-standards-index.md) | Quick Reference: Standards Index | Master table of all standards applied |
| [Appendix A](handbook/appendix-a-glossary.md) | Glossary | Definitions of all acronyms and terms used |
| [Appendix B](handbook/appendix-b-implementation-checklist.md) | Implementation Checklist | Practical checklist for developers and DBAs |
| [Appendix C](handbook/appendix-c-sample-schema.md) | Sample SQL Schema | Reference DDL for MySQL/PostgreSQL/SQL Server |

---

## Downloadable Release

The formatted Word document version of the handbook is available in [Releases](https://github.com/cair-philippines/ph-education-data-standards/releases).

> **v1.0 (2026)** — Initial publication — [Download .docx](releases/)

---

## How to Contribute

We welcome contributions from anyone — developers, educators, data managers, policy analysts, or interested citizens.

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request or issue.

**Quick guide:**
- 🐛 **Found an error?** Open an [Issue](https://github.com/cair-philippines/ph-education-data-standards/issues)
- 💡 **Have a suggestion?** Start a [Discussion](https://github.com/cair-philippines/ph-education-data-standards/discussions)
- ✏️ **Want to propose a change?** Fork → edit → open a Pull Request

All proposed changes to normative content must cite a supporting standard, law, or documented practice.

---

## License

This handbook is released under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](LICENSE).

You are free to share and adapt this material for any purpose, including commercial use, as long as you give appropriate credit.

---

## Maintainers and Acknowledgments

This handbook was initiated as a community effort to fill a long-standing gap in Philippine education data governance. It draws on the work of the PSA, DepEd, CHED, TESDA, DICT, and international standards bodies.

To join as a maintainer, open a Discussion and introduce yourself.
