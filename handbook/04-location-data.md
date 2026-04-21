# Section 04: Location Data

**Status:** Normative
**Edition:** 1.0 (2026)

---

## Overview

Location data **shall** adhere to the **Philippine Standard Geographic Code (PSGC)** maintained by the Philippine Statistics Authority (PSA). The PSGC is updated quarterly and is the authoritative geocode system for the Philippines.

> **Reference:** PSA PSGC — https://psa.gov.ph/classification/psgc

> ⚠️ Always validate PSGC codes against the most recent PSA quarterly release. Barangay mergers, reclassifications, and new barangay creations are reflected in PSGC updates and may invalidate older codes.

---

## 4.1 Address Field Structure

The canonical Philippine address structure, from smallest to largest geographic unit:

| Level | Field Name(s) | Standard / Source | Required? |
|-------|--------------|-------------------|-----------|
| Street / Building | `address_line1` | Free text | YES |
| Barangay | `barangay_name` + `barangay_code` | PSA PSGC | YES |
| City / Municipality | `city_municipality_name` + `city_municipality_code` | PSA PSGC | YES |
| Province | `province_name` + `province_code` | PSA PSGC | Conditional (see 4.4) |
| Region | `region_name` + `region_code` | PSA PSGC | YES |
| ZIP Code | `zip_code` | PhilPost | YES |
| Country | `country_code` | ISO 3166-1 alpha-2 | YES |

> ⚠️ **Always store both the human-readable name and the PSGC code** for barangay, city/municipality, province, and region. Geographic names may change over time through legislation or presidential proclamation; codes enable consistent longitudinal matching even when names change.

---

## 4.2 Street / Building Address

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `address_line1` |
| **Format** | Free text, UTF-8, `VARCHAR(200)` |
| **Content** | Building name, unit/floor number, street number, street name — in that order where applicable |
| **Example** | `"Unit 4B, Rizal Building, 123 P. Burgos Street"` |

A second line `address_line2` (`VARCHAR(200)`) **may** be used for additional location detail (e.g., subdivision name, compound name) where `address_line1` is insufficient.

---

## 4.3 Barangay

| Attribute | Specification |
|-----------|--------------|
| **Field names** | `barangay_name` (`VARCHAR(100)`) and `barangay_code` (`CHAR(9)`) |
| **Standard** | PSA Philippine Standard Geographic Code (PSGC) |
| **Code format** | **9-digit numeric string** — the full PSGC 9-digit code uniquely identifies a barangay |
| **Example** | Code: `"097306001"`, Name: `"Barangay Ayala"` |

**PSGC 9-digit structure:**

```
[ RR ][ PP ][ MMM ][ BB ]
  ↑      ↑      ↑      ↑
Region  Province  Mun/City  Barangay
(2)      (2)      (3)       (2)
```

> ⚠️ **Always use the full 9-digit code.** Do not store a standalone 2-digit barangay segment — it is meaningless without the parent codes and will cause lookup failures.

---

## 4.4 City / Municipality

| Attribute | Specification |
|-----------|--------------|
| **Field names** | `city_municipality_name` (`VARCHAR(100)`) and `city_municipality_code` (`CHAR(7)`) |
| **Standard** | PSA PSGC |
| **Code format** | 7-character prefix of the full PSGC code: `RRPPMMM` |
| **Example** | `"0973060"` for a municipality in Zamboanga del Sur |

### City / Municipality Type

The PSGC distinguishes between four types. This distinction **shall** be stored in a separate field:

| Field | `city_municipality_type` (`VARCHAR(30)`) |
|-------|----------------------------------------|
| `MUNICIPALITY` | Standard municipality |
| `COMPONENT_CITY` | Component city (within a province) |
| `INDEPENDENT_COMPONENT_CITY` | ICC — not part of any province |
| `HUC` | Highly Urbanized City — independent of province |

> **NCR note:** Cities in the National Capital Region (NCR / Metro Manila) do not belong to a province. The `province_code` and `province_name` fields **shall** be `NULL` for NCR entries — not `"N/A"` or blank.

---

## 4.5 Province

| Attribute | Specification |
|-----------|--------------|
| **Field names** | `province_name` (`VARCHAR(100)`) and `province_code` (`CHAR(4)`) |
| **Standard** | PSA PSGC |
| **Code format** | 4-character prefix: `RRPP` |
| **Required?** | Conditional — `NULL` for HUCs and NCR cities (which have no province); required for all others |

---

## 4.6 Region

| Attribute | Specification |
|-----------|--------------|
| **Field names** | `region_name` (`VARCHAR(100)`) and `region_code` (`CHAR(2)`) |
| **Standard** | PSA PSGC |
| **Code format** | 2-digit numeric string |
| **Required?** | **YES** |

### Current Region Codes (PSGC, as of 2025)

| Code | Name | Common Abbreviation |
|------|------|---------------------|
| `01` | Ilocos Region | Region I |
| `02` | Cagayan Valley | Region II |
| `03` | Central Luzon | Region III |
| `04` | CALABARZON | Region IV-A |
| `17` | MIMAROPA | Region IV-B |
| `05` | Bicol Region | Region V |
| `06` | Western Visayas | Region VI |
| `07` | Central Visayas | Region VII |
| `08` | Eastern Visayas | Region VIII |
| `09` | Zamboanga Peninsula | Region IX |
| `10` | Northern Mindanao | Region X |
| `11` | Davao Region | Region XI |
| `12` | SOCCSKSARGEN | Region XII |
| `13` | National Capital Region | NCR |
| `14` | Cordillera Administrative Region | CAR |
| `15` | Bangsamoro Autonomous Region in Muslim Mindanao | BARMM |
| `16` | Caraga | Region XIII |

> **Note:** Region IV-B (MIMAROPA) uses code `17` in PSGC, not `04` or `4B`. Always use the PSGC numeric code, not the Roman numeral abbreviation, in stored data.

---

## 4.7 ZIP Code

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `zip_code` |
| **Standard** | Philippine Postal Corporation (PhilPost) ZIP Code Directory |
| **Format** | 4-digit numeric string (`CHAR(4)`), stored as string to preserve leading zeros |
| **Example** | `"0900"` for parts of Zamboanga City; `"1000"` for parts of Manila |
| **Required?** | **YES** |

> ⚠️ ZIP codes are assigned by PhilPost and do **not** map 1:1 with PSGC barangay codes. Both fields must be maintained independently. Do not derive one from the other.

> ⚠️ Store as `CHAR(4)` or `VARCHAR(4)`, never as `INTEGER`. The code `"0900"` stored as integer becomes `900`, which is incorrect.

---

## 4.8 Country Code

| Attribute | Specification |
|-----------|--------------|
| **Field name** | `country_code` |
| **Standard** | **ISO 3166-1 alpha-2** — Two-letter country codes |
| **Format** | `CHAR(2)`, uppercase |
| **Default** | `"PH"` for all domestic institutions |
| **Examples** | `"PH"` (Philippines), `"US"` (United States), `"JP"` (Japan) |
| **Required?** | **YES** |
| **Reference** | https://www.iso.org/iso-3166-country-codes.html |

This field is particularly relevant for:
- International student records
- Foreign institution references in transfer credentials
- Study abroad program data

---

## 4.9 Geographic Coordinates (Recommended)

While optional, geographic coordinates are strongly recommended for all institution records to support mapping, proximity analysis, and disaster preparedness data.

| Attribute | Specification |
|-----------|--------------|
| **Field names** | `latitude` (`DECIMAL(10,7)`) and `longitude` (`DECIMAL(10,7)`) |
| **Standard** | **ISO 6709:2022** — Standard representation of geographic point location by coordinates |
| **Datum** | WGS 84 |
| **Format** | Decimal degrees (DD). Latitude: positive = north, negative = south. Longitude: positive = east, negative = west. |
| **Precision** | Minimum 4 decimal places (~11 m accuracy); 7 decimal places recommended |
| **Example** | Latitude: `14.5995`, Longitude: `120.9842` (Manila) |

---

## 4.10 Address for Campuses and Annexes

Where an institution has multiple campuses or annexes, each campus **shall** have its own location record linked to the parent institution via `school_id`. The parent institution record **should** store the address of the main/administrative campus.

---

*Previous: [Section 03 — School Identification](03-school-identification.md)*
*Next: [Section 05 — Dates and Time](05-dates.md)*
