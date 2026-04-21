# Appendix C: Sample SQL Schema

This appendix provides a **reference SQL schema** illustrating how the fields defined in this handbook map to database column definitions. This schema is **informative** — it is not prescriptive about database engine choice or overall system architecture.

The schema uses MySQL / MariaDB syntax. Adaptations for PostgreSQL, SQL Server, and other engines are noted where relevant.

---

## C.1 Institutions Table

```sql
CREATE TABLE institutions (
    -- Internal surrogate key (not exposed externally)
    id                          INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,

    -- School Identification (Section 03)
    school_name                 VARCHAR(200)    NOT NULL,
    school_name_abbr            VARCHAR(50)     NULL,
    school_former_name          VARCHAR(200)    NULL,
    school_former_name_until    DATE            NULL,
    school_sector               VARCHAR(30)     NOT NULL,   -- PUBLIC | PRIVATE | SUC | LUC | TVET_PUBLIC | TVET_PRIVATE

    -- Agency IDs (at least one required)
    school_id                   VARCHAR(10)     NULL,       -- DepEd SCHID, 6-digit zero-padded
    ched_institution_code       VARCHAR(20)     NULL,       -- CHED HEMIS code
    tesda_registry_no           VARCHAR(20)     NULL,       -- TESDA registry number

    -- Location (Section 04)
    address_line1               VARCHAR(200)    NOT NULL,
    address_line2               VARCHAR(200)    NULL,
    barangay_name               VARCHAR(100)    NOT NULL,
    barangay_code               CHAR(9)         NOT NULL,   -- Full 9-digit PSGC code
    city_municipality_name      VARCHAR(100)    NOT NULL,
    city_municipality_code      CHAR(7)         NOT NULL,   -- 7-digit PSGC prefix
    city_municipality_type      VARCHAR(30)     NOT NULL,   -- MUNICIPALITY | COMPONENT_CITY | ICC | HUC
    province_name               VARCHAR(100)    NULL,       -- NULL for HUC / NCR
    province_code               CHAR(4)         NULL,       -- NULL for HUC / NCR
    region_name                 VARCHAR(100)    NOT NULL,
    region_code                 CHAR(2)         NOT NULL,   -- 2-digit PSGC region code
    zip_code                    CHAR(4)         NOT NULL,   -- PhilPost ZIP, stored as string
    country_code                CHAR(2)         NOT NULL DEFAULT 'PH',  -- ISO 3166-1 alpha-2
    latitude                    DECIMAL(10,7)   NULL,       -- ISO 6709, WGS 84
    longitude                   DECIMAL(10,7)   NULL,

    -- Audit timestamps (Section 05)
    record_created_at           DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP,
    record_updated_at           DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    -- Constraints
    CONSTRAINT chk_school_sector
        CHECK (school_sector IN ('PUBLIC','PRIVATE','STATE_UNIVERSITY_COLLEGE',
                                  'LOCAL_UNIVERSITY_COLLEGE','PRIVATE_HEI',
                                  'TVET_PUBLIC','TVET_PRIVATE')),
    CONSTRAINT chk_country_code
        CHECK (country_code REGEXP '^[A-Z]{2}$'),
    CONSTRAINT chk_region_code
        CHECK (region_code REGEXP '^[0-9]{2}$'),
    CONSTRAINT chk_barangay_code
        CHECK (barangay_code REGEXP '^[0-9]{9}$'),
    CONSTRAINT chk_zip_code
        CHECK (zip_code REGEXP '^[0-9]{4}$'),
    CONSTRAINT chk_at_least_one_agency_id
        CHECK (school_id IS NOT NULL OR ched_institution_code IS NOT NULL OR tesda_registry_no IS NOT NULL)

) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

---

## C.2 Learners Table

```sql
CREATE TABLE learners (
    -- Internal surrogate key
    id                          INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,

    -- Learner Identifiers (Sections 07, 08)
    student_lrn                 VARCHAR(12)     NULL,       -- DepEd LRN; VARCHAR not INT
    philsys_number              VARCHAR(16)     NULL,       -- PSA PhilSys; sensitive data
    school_student_id           VARCHAR(50)     NOT NULL,   -- Local institution ID

    -- Personal Name (Section 06) — stored UPPERCASE
    last_name                   VARCHAR(100)    NOT NULL,
    first_name                  VARCHAR(100)    NOT NULL,
    middle_name                 VARCHAR(100)    NULL,       -- NULL if none (not 'N/A')
    name_suffix                 VARCHAR(10)     NULL,       -- JR | SR | II | III | IV | V
    name_prefix                 VARCHAR(10)     NULL,       -- MR | MRS | MS | DR | PROF
    preferred_name              VARCHAR(100)    NULL,

    -- Demographics
    birth_date                  DATE            NOT NULL,   -- ISO 8601 DATE only (no time)
    sex                         CHAR(1)         NOT NULL,   -- M | F | U (ISO 5218)
    gender_identity             VARCHAR(50)     NULL,       -- Optional; sensitive
    civil_status                VARCHAR(20)     NULL,       -- Section 09.3 controlled vocabulary
    nationality_code            CHAR(2)         NOT NULL DEFAULT 'PH',  -- ISO 3166-1 alpha-2
    mother_tongue_code          CHAR(3)         NULL,       -- ISO 639-3
    ip_community_affiliation    VARCHAR(100)    NULL,       -- Optional; sensitive

    -- Contact (Section 10)
    mobile_number               VARCHAR(15)     NULL,       -- E.164 format
    landline_number             VARCHAR(15)     NULL,       -- E.164 format
    email_address               VARCHAR(254)    NULL,       -- RFC 5322; stored lowercase

    -- Current Address (Section 04) — home address of learner
    address_line1               VARCHAR(200)    NULL,
    address_line2               VARCHAR(200)    NULL,
    barangay_name               VARCHAR(100)    NULL,
    barangay_code               CHAR(9)         NULL,
    city_municipality_name      VARCHAR(100)    NULL,
    city_municipality_code      CHAR(7)         NULL,
    province_name               VARCHAR(100)    NULL,
    province_code               CHAR(4)         NULL,
    region_name                 VARCHAR(100)    NULL,
    region_code                 CHAR(2)         NULL,
    zip_code                    CHAR(4)         NULL,
    country_code                CHAR(2)         NULL DEFAULT 'PH',

    -- Emergency Contact (Section 10.3)
    emergency_contact_name      VARCHAR(200)    NULL,
    emergency_contact_relation  VARCHAR(50)     NULL,
    emergency_contact_mobile    VARCHAR(15)     NULL,
    emergency_contact_email     VARCHAR(254)    NULL,

    -- Audit timestamps
    record_created_at           DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP,
    record_updated_at           DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    -- Constraints
    CONSTRAINT uq_student_lrn   UNIQUE (student_lrn),
    CONSTRAINT chk_sex
        CHECK (sex IN ('M', 'F', 'U')),
    CONSTRAINT chk_nationality
        CHECK (nationality_code REGEXP '^[A-Z]{2}$'),
    CONSTRAINT chk_mobile_e164
        CHECK (mobile_number IS NULL OR mobile_number REGEXP '^\\+[1-9][0-9]{7,14}$'),
    CONSTRAINT chk_lrn_format
        CHECK (student_lrn IS NULL OR student_lrn REGEXP '^[0-9]{12}$'),
    CONSTRAINT chk_philsys_format
        CHECK (philsys_number IS NULL OR philsys_number REGEXP '^[0-9]{16}$')

) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

---

## C.3 Enrollments Table

```sql
CREATE TABLE enrollments (
    id                          INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,

    -- Foreign keys
    learner_id                  INT UNSIGNED    NOT NULL,
    institution_id              INT UNSIGNED    NOT NULL,

    -- Academic context (Section 05, 12)
    academic_year               CHAR(9)         NOT NULL,   -- YYYY-YYYY format
    grading_period              VARCHAR(10)     NULL,       -- Q1|Q2|Q3|Q4 or SEM1|SEM2|SUMMER
    education_level             VARCHAR(30)     NOT NULL,   -- Section 12.1 controlled vocabulary
    isced_level                 TINYINT         NULL,       -- ISCED 2011 numeric level
    program_name                VARCHAR(200)    NULL,
    program_code                VARCHAR(20)     NULL,
    isced_field_code            CHAR(4)         NULL,       -- ISCED-F 2013
    shs_track                   VARCHAR(20)     NULL,       -- ACADEMIC|TVL|SPORTS|ARTS_DESIGN
    shs_strand                  VARCHAR(20)     NULL,
    tesda_qualification_title   VARCHAR(200)    NULL,
    tesda_qualification_code    VARCHAR(20)     NULL,
    language_of_instruction     VARCHAR(3)      NULL,       -- ISO 639-1 or 639-3

    -- Enrollment lifecycle (Section 05.5, 12.4)
    enrollment_date             DATE            NOT NULL,
    enrollment_status           VARCHAR(20)     NOT NULL DEFAULT 'ENROLLED',
    graduation_date             DATE            NULL,
    withdrawal_date             DATE            NULL,

    -- Agency-specific IDs
    ched_student_no             VARCHAR(50)     NULL,
    tesda_learner_ref           VARCHAR(50)     NULL,

    -- Audit
    record_created_at           DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP,
    record_updated_at           DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    -- Foreign key constraints
    CONSTRAINT fk_enrollment_learner
        FOREIGN KEY (learner_id) REFERENCES learners(id),
    CONSTRAINT fk_enrollment_institution
        FOREIGN KEY (institution_id) REFERENCES institutions(id),

    -- Value constraints
    CONSTRAINT chk_enrollment_status
        CHECK (enrollment_status IN ('ENROLLED','DROPPED','TRANSFERRED_OUT','TRANSFERRED_IN',
                                      'GRADUATED','COMPLETED','WITHDRAWN','ON_LEAVE','DECEASED')),
    CONSTRAINT chk_academic_year
        CHECK (academic_year REGEXP '^[0-9]{4}-[0-9]{4}$')

) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Index for common lookups
CREATE INDEX idx_enrollment_lrn
    ON enrollments (learner_id, academic_year);
CREATE INDEX idx_enrollment_institution
    ON enrollments (institution_id, academic_year);
```

---

## C.4 Notes for Other Database Engines

### PostgreSQL

- Replace `DATETIME` with `TIMESTAMPTZ` for timezone-aware timestamps
- Replace `AUTO_INCREMENT` with `SERIAL` or `GENERATED ALWAYS AS IDENTITY`
- Use `CHECK` constraints natively (PostgreSQL enforces them by default)
- Use `CITEXT` extension or `LOWER()` function for case-insensitive email uniqueness

### SQL Server

- Replace `DATETIME` with `DATETIMEOFFSET` for timezone-aware timestamps
- Replace `CHAR(n)` with `NCHAR(n)` and `VARCHAR(n)` with `NVARCHAR(n)` for Unicode support
- Use `COLLATE Latin1_General_100_CI_AI_SC_UTF8` or similar for UTF-8 collation (SQL Server 2019+)

---

*This schema is a starting point. Production implementations should adapt it to their specific system architecture, ORM conventions, and database engine requirements.*
