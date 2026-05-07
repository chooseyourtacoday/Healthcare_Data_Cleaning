# Healthcare Patient Intake — Real World Data Cleaning
**Author:** Alejandro Molina  
**GitHub:** [chooseyourtacoday](https://github.com/chooseyourtacoday)  
**Tools:** Python, Pandas, NumPy, Matplotlib, Jupyter Notebook  

---

## Background

Every department and individual medical employee inputs patient information differently. Over time this inconsistency created confusion, delays, and gaps in patient records across the hospital system.

Recently, a patient with O- blood type was administered O+ blood during surgery and expired due to acute hemolytic transfusion reaction. A direct consequence of inaccurate data entry. In response, hospital leadership mandated the standardization of all patient data. This dataset was assigned to me for cleaning and reorganization to ensure accuracy and prevent recurrence of this tragic incident.

One person is too many for negligence.

---

## Dataset

- **Records:** 1,050 patient intake rows (including 50 duplicates)
- **Columns:** 16 fields covering patient demographics, clinical measurements, and contact information
- **Source:** Synthetic dataset modeled on realistic DFW healthcare patient intake records

---

## Problems Identified

| # | Issue | Records Affected |
|---|---|---|
| 1 | Inconsistent date formats — 5 different styles | ~400 |
| 2 | Inconsistent phone number formats — 5 different styles | ~1,050 |
| 3 | Messy blood type values — 20 unique values where 8 should exist | ~300 |
| 4 | Messy gender values — 16 variations where 4 categories should exist | ~350 |
| 5 | Messy state values — 8 variations all representing Texas | ~200 |
| 6 | Messy department names — abbreviations, misspellings, mixed casing | ~300 |
| 7 | Missing values across 8 critical columns | 684 pre-cleaning |
| 8 | Impossible clinical outliers — hemoglobin 99.9 g/dL, weight 999 lbs | ~75 |
| 9 | Duplicate patient records with name casing variations | 50 |
| 10 | Mixed case email addresses | ~150 |
| 11 | Leading and trailing whitespace in patient names | ~80 |
| 12 | Future admission dates entered as 12/31/2099 | 15 |
| 13 | Negative donation volume values | 10 |

---

## Cleaning Steps

1. **Names** — Stripped whitespace, standardized to title case
2. **Emails** — Lowercased and stripped of whitespace
3. **Dates** — Parsed across 5 formats, standardized to ISO 8601 (YYYY-MM-DD)
4. **Future Dates** — Admission dates of 12/31/2099 nulled and flagged for clinical review
5. **Blood Types** — Mapped 20 variations to 8 standard classifications
6. **Gender** — Mapped 16 variations to 4 standard categories, escalated clinical sex vs. gender distinction to leadership
7. **State** — Mapped all Texas variants to TX
8. **Departments** — Mapped all variations to 5 full department titles
9. **Clinical Outliers** — Nulled impossible hemoglobin, weight, visit count, and donation values
10. **Duplicates** — Removed 50 duplicate Patient IDs, retaining first occurrence
11. **Phone Numbers** — Extracted digits, reformatted to (XXX) XXX-XXXX standard

---

## Key Findings

- **A+ and O+** are the most common blood types in the patient population
- **O-** remains the most critically needed type due to universal donor status — accurate O- records are irreplaceable
- **20% of patients** selected Prefer not to say for gender — hemoglobin eligibility for this group must be verified through direct clinical testing
- **Cardiology, Phlebotomy, Emergency, and General** are the highest volume departments and the highest risk for data entry inconsistency under pressure
- **Blood type and hemoglobin** are the two fields most directly tied to patient survival — their missing value rates are the most urgent concern in the dataset
- **Declining admission trends** in recent years warrant investigation into financial barriers, community outreach, and patient trust

---

## Pre vs. Post Cleaning Comparison

| Metric | Before | After |
|---|---|---|
| Total Rows | 1,050 | 1,000 |
| Missing Values | 684 | 776* |
| Duplicate Patient IDs | 50 | 0 |
| Unique Blood Type Values | 20 | 8 |
| Unique Gender Values | 16 | 4 |
| Unique State Values | 8 | 1 |
| Unique Department Values | 12 | 5 |

*Missing values increased because impossible values (99.9 g/dL hemoglobin, 999 lb weight, future dates) were correctly nulled rather than retained as false data. Every remaining value is now clinically trustworthy.

---

## Clinical Recommendations

1. **Implement dropdown validation** on blood type, gender, state, and department fields at point of entry — eliminating free text variation entirely
2. **Enforce mandatory completion** of blood type and hemoglobin fields before any record can be saved
3. **Verify hemoglobin through direct testing** for all donors regardless of gender entry until a separate biological sex field is implemented
4. **Conduct manual review** of all 50 flagged duplicate records to ensure retained entries contain the most complete information
5. **Direct outreach** to all patients with missing blood type, hemoglobin, phone, or email records before those records are used in any care decision
6. **Quarterly data quality audits** across all departments to catch inconsistencies before they reach clinical staff
7. **Prioritize data entry training** in Cardiology, Phlebotomy, Emergency, and General — the four highest volume and highest risk departments

---

## A Note on Imputation

Missing clinical values in this dataset — blood type, hemoglobin, weight — were deliberately left as null rather than imputed using statistical methods. In a healthcare context, estimating biological measurements through mathematics is not analysis. It is negligence. These values must be obtained through direct clinical assessment of the patient or donor. No algorithm substitutes for a hemoglobin finger-stick test.

---

## Why This Project Matters

Data cleaning is rarely discussed in terms of life and death. In most industries a missing value is an inconvenience. In a blood bank it is an unresolved clinical risk.

The patient who expired during surgery did not die because of a complex system failure. They died because someone entered the wrong blood type. Because data entry was treated as optional when it never was.

This project exists to demonstrate that data quality is not a technical exercise — it is a patient safety requirement. Every field matters. Every entry matters. Every missing value is a gap in someone's safety net that must be closed.

---

## Repository Structure

```
healthcare_data_cleaning/
├── Healthcare_Data_Cleaning.ipynb   # Full cleaning notebook
├── patient_data_MESSY.csv           # Original uncleaned dataset
├── patient_data_CLEANED.csv         # Final cleaned output
└── README.md                        # This file
```

---

*Built by Alejandro Molina | [github.com/chooseyourtacoday](https://github.com/chooseyourtacoday)*  
*Informed by four years of clinical experience in blood banking and phlebotomy at Carter BloodCare, DFW*
