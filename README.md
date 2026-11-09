# econ3916-midterm

# Do districts that spend more on instruction graduate more students?

ECON 3916 midterm project. Instructional spending and the 2018 graduation rate in California and Texas school districts.

[Open the notebook in Colab](https://colab.research.google.com/github/Ethan-Tse/econ3916-midterm/blob/main/Midterm%20Project/Econ_3916_Midterm.ipynb) · [Report (PDF)](Midterm%20Project/Midterm_Report.pdf)

## Question

Across regular school districts in California and Texas, how is a district's average per-pupil instructional spending over 2015–2018 (in 2018 dollars, logged) associated with its 2018 cohort graduation rate (the percent of ninth graders who graduate within four years), holding state and district size constant?

## Data

| File | Source | What it holds |
|---|---|---|
| `Data/GraduationRates.csv` | [Urban Institute Education Data Portal](https://educationdata.urban.org/), school-district graduation rates (EDFacts) | district ID, name, state, agency type, enrollment, and the graduation rate (`grad_rate_midpt`, the midpoint of the reported range). Values exist for 2018 only. |
| `Data/Expenditures_Finances.csv` | Education Data Portal, Common Core of Data finance | total current expenditures for instruction and enrollment, 2018–2020 (only 2018 is used) |
| `Data/Finance_2015_2017.csv` | Education Data Portal, Common Core of Data finance | the same variables for 2015, 2016 and 2017, so each district has a four-year average |
| `Data/cpi_annual.csv` | [FRED, CPIAUCNS](https://fred.stlouisfed.org/series/CPIAUCNS) (BLS CPI-U) | annual average CPI-U for 2015–2018, to restate spending in 2018 dollars; the notebook writes this file each time it reaches FRED |

The graduation file and the 2018–2020 finance file were downloaded on 2026-11-05, the 2015–2017 finance file on 2026-11-08. One row is one district; the analysis keeps regular local school districts and drops County Offices of Education.

## How to run

1. Open the notebook in Colab (link above) and choose **Runtime › Restart session and run all**.
2. The loading cell reads the three CSV files from this repository by their raw GitHub address (the `BASE` line at the top of that cell) and downloads the CPI from FRED. If FRED is unreachable it falls back to `Data/cpi_annual.csv`.
3. To use local copies instead, upload the files to Colab and set `BASE = ""`.

Every number in the report is printed by the notebook's last code cell, "Numbers my report quotes".

## Finding

A district that spent 10% more per pupil over 2015–2018 (about $654 at the median, in 2018 dollars) had a 2018 graduation rate 0.90 percentage points lower than a district in the same state and of the same size (95% CI −1.35 to −0.46, N = 1,366). The coefficient on log spending is −9.48 (robust HC3 standard error 2.36). Without controls it is −12.69; adding district size accounts for most of the shrinkage.

This is a conditional association, not a causal effect. District poverty and student need, which are not in these data, can produce a negative sign by themselves, since higher-need districts tend to get more money and graduate fewer students.

## Limits worth knowing

- The sample is 1,366 of 1,958 regular districts in 2018: 587 have no graduation rate (many California districts have no high school, and small districts' rates are suppressed), so the results describe districts with a high school and a reported rate, and lean toward Texas and larger districts.
- 105 small districts are reported at exactly 75%, a range midpoint, not an observed rate.
- The estimate moves with which districts are included (0.62 to 0.97 points per 10% more spending in the checks in Section 4 of the report), but it is negative in every version.

## Files

| Path | What it is |
|---|---|
| `Midterm Project/Econ_3916_Midterm.ipynb` | the final notebook |
| `Midterm Project/Midterm_Report.pdf` | the written report |
| `Model_Draft.ipynb` | the model-draft checkpoint |
| `Data/` | the data files above |
