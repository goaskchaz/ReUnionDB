# vwClassmatesDied

**Database:** ReUnionDB

## Overview

The **vwClassmatesDied** view returns a list of classmates who have been identified as deceased. It provides demographic and vital statistics information and calculates each classmate's age at death.

This view is intended for memorial reporting, reunion publications, statistical reporting, and other read-only queries.

---

## View Information

| Property | Value |
|----------|-------|
| View Name | vwClassmatesDied |
| Source Table | dbo.tblClassmates |
| Primary Purpose | Memorial and deceased classmate reporting |
| Updateable | No |

---

## Source

```sql
FROM dbo.tblClassmates
WHERE Flag_Died = 1
```

Only classmates where **Flag_Died = 1** are included.

---

## Columns

| Column | Source | Description |
|---------|--------|-------------|
| PKClassmateID | tblClassmates | Unique classmate identifier. |
| First_Name | tblClassmates | First name. |
| Middle_Initial | Calculated | First character of the middle name. |
| Last_Name | tblClassmates | Last name. |
| Vital_Gender | tblClassmates | Gender. |
| Vital_DOB | tblClassmates | Date of birth. |
| Vital_DOB_Loc | tblClassmates | Birth location. |
| Vital_DOD | tblClassmates | Date of death. |
| Vital_DOD_Loc | tblClassmates | Location of death. |
| Vital_Cause | tblClassmates | Cause of death, if known. |
| AgeAtDeath | Calculated | Age in completed years at the time of death. |

---

## Calculated Fields

### Middle_Initial

Returns only the first character of the classmate's middle name.

```sql
LEFT(Middle_Name,1)
```

Example

| Middle_Name | Middle_Initial |
|--------------|----------------|
| Allen | A |
| Marie | M |

---

### AgeAtDeath

Calculates the classmate's age at death.

The calculation:

- Uses the Date of Birth (`Vital_DOB`)
- Uses the Date of Death (`Vital_DOD`)
- Correctly adjusts for whether the birthday had occurred before the date of death.
- Returns **NULL** if either date is missing.

Example

| DOB | DOD | AgeAtDeath |
|------|------|-----------:|
| 1959-05-10 | 2022-04-15 | 62 |
| 1959-05-10 | 2022-06-20 | 63 |

---

## Business Rules

- Only deceased classmates are returned.
- A classmate is considered deceased when `Flag_Died = 1`.
- `AgeAtDeath` is calculated only when both birth and death dates are available.
- Missing birth or death dates result in a NULL age.
- The view is intended for reporting and should not be updated directly.

---

## Example Query

```sql
SELECT *
FROM vwClassmatesDied
ORDER BY Last_Name, First_Name;
```

---

## Typical Uses

- Reunion memorial booklet
- "In Memoriam" web pages
- Reunion statistics
- Historical reporting
- Demographic analysis of deceased classmates

---

## Dependencies

| Object | Type |
|---------|------|
| dbo.tblClassmates | Table |

---

## Revision History

| Date | Description |
|------|-------------|
| Initial Version | Created to simplify deceased classmate reporting and calculate age at death. |
