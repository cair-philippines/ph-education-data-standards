# Section 13: Data Privacy, Security, and Retention

**Status:** Normative
**Edition:** 1.0 (2026)

---

## 13.1 Applicable Laws and Standards

All education sector systems collecting, processing, or storing personal data **shall** comply with:

- **Republic Act No. 10173** — Data Privacy Act of 2012 (DPA) and its Implementing Rules and Regulations (IRR)
- **National Privacy Commission (NPC) Circulars** — particularly NPC Circular 16-01 (Security of Personal Information) and subsequent issuances
- **ISO/IEC 27001:2022** — Information Security Management Systems (ISMS) — recommended for all systems handling CONFIDENTIAL or higher data
- **ISO/IEC 27701:2019** — Privacy Information Management (extension to ISO 27001) — recommended for systems acting as Personal Information Controllers (PICs) under RA 10173
- **DICT e-Government Security Policy Framework** — for all government-operated systems

---

## 13.2 Personal Information Controller (PIC) Obligations

Each agency (DepEd, CHED, TESDA) and each institution operating an education information system is a **Personal Information Controller (PIC)** under RA 10173 and **shall**:

1. Register its data processing systems with the NPC as required
2. Designate a **Data Protection Officer (DPO)**
3. Maintain a **Privacy Impact Assessment (PIA)** for systems processing sensitive personal information
4. Implement **Privacy Notices** for data subjects (learners, parents, faculty, staff)
5. Establish a **Data Breach Response Policy** consistent with NPC Circular 16-03

---

## 13.3 Data Classification

| Classification | Examples | Minimum Handling Requirements |
|----------------|----------|-------------------------------|
| **STRICTLY CONFIDENTIAL** | PhilSys number; health/medical records; disciplinary records; court-ordered information | Encrypt at rest (AES-256 minimum) and in transit (TLS 1.3). Role-based access with MFA. Full audit log required. |
| **CONFIDENTIAL** | Student LRN; full name + birth date combination; contact details; grades; gender identity; civil status | Encrypt in transit (TLS 1.2+). Access restricted to authorized personnel. Audit log recommended. |
| **INTERNAL** | School ID; school name; region / PSGC codes; academic year; program codes; enrollment counts | Not for public disclosure without authorization. Internal systems access. |
| **PUBLIC** | Official school name; general school address; public accreditation status; aggregate statistics | May be disclosed per FOIA (RA 11032) and open data policies. |

---

## 13.4 Sensitive Personal Information

Under RA 10173 Section 3(l), the following categories are **Sensitive Personal Information (SPI)** and require heightened protection:

- Race, ethnic origin, or IP affiliation
- Marital status (in certain contexts)
- Age of minors (in combination with other fields)
- Health, education records, and genetic or sexual information
- Any proceeding for violation of law, judicial records, or suspicion of offenses
- Government-issued IDs (including LRN when combined with other fields)

SPI fields **shall not** be included in standard reports, data exports, or API responses without explicit authorization and logged consent.

---

## 13.5 Data Retention Periods

| Record Type | Minimum Retention Period | Basis |
|-------------|--------------------------|-------|
| Student academic records (transcripts, Form 137/138) | **Permanent** | DepEd / CHED regulations; PSA archiving policy |
| Enrollment records | 10 years after last enrollment or graduation | DepEd Order; NPC guidance |
| Disciplinary records | 5 years after case resolution, or until graduation (whichever is later) | RA 10173 IRR; DepEd Child Protection Policy |
| Admission application records (rejected applicants) | 1 year after notification | Minimum legal purpose |
| System access logs | 3 years | ISO/IEC 27001; NPC Circular 16-01 |
| TESDA training and assessment records | **Permanent** (National Certificate records) | TESDA regulations |
| Backup data | Same as source records | Must not be retained longer than source |

After the applicable retention period, records **shall** be securely disposed of using methods appropriate to the data classification level (e.g., secure deletion for digital records, shredding for physical records).

---

## 13.6 Data Subject Rights

Under RA 10173, all data subjects (learners, parents, faculty, staff) have the right to:

- **Be informed** — know what data is collected and why
- **Access** — obtain a copy of their personal data
- **Correction** — have inaccurate data corrected
- **Object** — oppose processing in certain circumstances
- **Erasure or blocking** — under specific conditions
- **Damages** — for privacy violations
- **Portability** — receive data in a structured, machine-readable format

Systems **shall** support processes for data subjects to exercise these rights.

---

## 13.7 Children's Data

All K–12 learners are minors under Philippine law. For learners under 18:

- Parental or guardian consent **shall** be obtained for collection of non-essential personal data
- Data minimization **shall** apply — collect only what is strictly necessary for education service delivery
- Profiling of minors for commercial purposes is **prohibited**
- DepEd's **Child Protection Policy** (DepEd Order No. 40, s. 2012) applies to all data handling involving learners

---

*Previous: [Section 12 — Program and Course Data](12-program-course-data.md)*
*Next: [Section 14 — Quick Reference Standards Index](14-standards-index.md)*
