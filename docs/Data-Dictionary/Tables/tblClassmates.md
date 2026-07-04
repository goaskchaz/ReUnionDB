# tblClassmates

**Database:** ReunionDB

## Overview

The **tblClassmates** table is the primary table within the ReunionDB database. It stores demographic, contact, biographical, and reunion-related information for each classmate. Each record represents a single classmate and serves as the central record referenced by other database objects.

---

## Table Information

| Property | Value |
|----------|-------|
| Table Name | tblClassmates |
| Primary Key | PKClassmateID |
| Record Type | One record per classmate |
| Last Updated Field | LastUpdate |

---

## Primary Key

| Column | Description |
|---------|-------------|
| **PKClassmateID** | Unique identifier for each classmate. This value is never reused and uniquely identifies each record. |

---

## Columns

| # | Column | Data Type | Length | Nullable | Description |
|--:|--------|-----------|-------:|:--------:|-------------|
| 1 | PKClassmateID | int | — | No | Primary Key. Unique identifier for each classmate. |
| 2 | First_Name | varchar | 100 | Yes | Legal first name. |
| 3 | Middle_Name | varchar | 100 | Yes | Middle name or initial. |
| 4 | Last_Name | varchar | 100 | Yes | Legal last name. |
| 5 | Nick_Name | varchar | 100 | Yes | Preferred or commonly used nickname. |
| 6 | Suffix_Name | varchar | 50 | Yes | Name suffix (Jr., Sr., II, III, etc.). |
| 7 | Mate_First_Name | varchar | 100 | Yes | First name of spouse or significant other. |
| 8 | Mate_Last_Name | varchar | 100 | Yes | Last name of spouse or significant other. |
| 9 | Post_Address1 | varchar | 200 | Yes | Mailing address line 1. |
| 10 | Post_Address2 | varchar | 200 | Yes | Mailing address line 2 (Apartment, Suite, etc.). |
| 11 | Post_City | varchar | 100 | Yes | Mailing city. |
| 12 | Post_State | varchar | 50 | Yes | Mailing state or province. |
| 13 | Post_Code | varchar | 30 | Yes | ZIP or postal code. |
| 14 | Post_Country | varchar | 100 | Yes | Country of residence. |
| 15 | Contact_Phone_Num | varchar | 50 | Yes | Primary telephone number. |
| 16 | Contact_Cell_Num | varchar | 50 | Yes | Mobile phone number. |
| 17 | Contact_eMail | varchar | 255 | Yes | Primary email address used for reunion communications. |
| 18 | Elementry_School | varchar | 100 | Yes | Elementary school attended. |
| 19 | Notes | varchar | 1750 | Yes | General comments, research notes, or reunion information. |
| 20 | Flag_InAnnual | bit | — | Yes | Indicates the classmate appears in the school annual/yearbook. |
| 21 | Flag_Corespd | bit | — | Yes | Indicates correspondence has occurred with the classmate. |
| 22 | Flag_DNC | bit | — | Yes | Do Not Contact indicator. |
| 23 | Flag_Died | bit | — | Yes | Indicates the classmate is deceased. |
| 24 | Vital_DOB | date | — | Yes | Date of birth. |
| 25 | Vital_DOB_Loc | varchar | 200 | Yes | Birth location. |
| 26 | Vital_DOD | date | — | Yes | Date of death. |
| 27 | Vital_DOD_Loc | varchar | 200 | Yes | Location of death. |
| 28 | Vital_Obit | varchar(MAX) | MAX | Yes | Obituary text or obituary URL. |
| 29 | Vital_Cause | varchar | 200 | Yes | Cause of death, if known. |
| 30 | Vital_Gender | varchar | 50 | Yes | Gender of the classmate. |
| 31 | LastUpdate | datetime2 | — | No | Date and time the record was last modified. |
| 32 | GradYear_Int | int | — | Yes | Graduation year associated with the classmate. |
| 33 | LegacyID | int | — | Yes | Identifier from a previous reunion database or legacy system. |

---

## Business Rules

- Each classmate is represented by one record.
- `PKClassmateID` uniquely identifies each classmate.
- Contact information should always contain the most current verified information.
- `Flag_DNC` (Do Not Contact) should exclude the classmate from mailings and other communications.
- `Flag_Died` identifies deceased classmates and may be used for memorial pages.
- `LastUpdate` should be updated whenever any field within the record changes.
- `LegacyID` is maintained only for migration and historical reference.

---

## Field Groups

### Personal Information

- First_Name
- Middle_Name
- Last_Name
- Nick_Name
- Suffix_Name
- Vital_Gender
- GradYear_Int

### Spouse / Partner

- Mate_First_Name
- Mate_Last_Name

### Mailing Address

- Post_Address1
- Post_Address2
- Post_City
- Post_State
- Post_Code
- Post_Country

### Contact Information

- Contact_Phone_Num
- Contact_Cell_Num
- Contact_eMail

### Biography

- Elementry_School
- Notes

### Reunion Status

- Flag_InAnnual
- Flag_Corespd
- Flag_DNC

### Vital Records

- Flag_Died
- Vital_DOB
- Vital_DOB_Loc
- Vital_DOD
- Vital_DOD_Loc
- Vital_Obit
- Vital_Cause

### Audit Information

- LastUpdate
- LegacyID

---

## Relationships

| Relationship | Table | Description |
|--------------|-------|-------------|
| Primary Entity | tblClassmates | Parent record representing a classmate. |
| Future Relationships | TBD | Other ReunionDB tables may reference `PKClassmateID` as a foreign key. |

---

## Notes

- `varchar(MAX)` is reported by SQL Server metadata as a length of **-1**.
- The `LastUpdate` field is required and should be maintained automatically whenever possible.
- This table serves as the foundation for ReunionDB and is expected to be referenced by attendance, communication, event, photo, and other related tables.
