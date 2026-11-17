# Data dictionary

**File:** `bank-additional-full.csv` (semicolon separated, 41,188 rows, 21 columns, 5.8 MB). Read it with `pd.read_csv("bank-additional-full.csv", sep=";")`.

**Source:** UCI Machine Learning Repository, "Bank Marketing" (dataset 222), https://archive.ics.uci.edu/dataset/222/bank+marketing. Licence CC BY 4.0.

**Citation:** Moro, S., Cortez, P. and Rita, P. (2014). A data-driven approach to predict the success of bank telemarketing. Decision Support Systems, 62, 22-31.

`bank-additional-names.txt` is the authors' original description of the file.

Each row is the last phone contact with one client in a campaign of a Portuguese retail bank. Rows are in date order from May 2008 to November 2010. Missing values are written as the text `unknown`.

## Raw columns

| Column | Type | Meaning |
|---|---|---|
| `age` | number | Age of the client in years (17 to 98) |
| `job` | text | Type of job (12 categories, including `unknown`) |
| `marital` | text | `married`, `single`, `divorced` (includes widowed), `unknown` |
| `education` | text | Highest education level (8 categories, including `unknown`) |
| `default` | text | Has credit in default? `yes`, `no`, `unknown` |
| `housing` | text | Has a housing loan? `yes`, `no`, `unknown` |
| `loan` | text | Has a personal loan? `yes`, `no`, `unknown` |
| `contact` | text | Contact channel: `cellular` (mobile) or `telephone` (landline) |
| `month` | text | Month of the last contact (`mar` to `dec`; there are no contacts in January or February) |
| `day_of_week` | text | Weekday of the last contact (`mon` to `fri`) |
| `duration` | number | Length of the last call in seconds. Known only after the call, so it must not be used to decide whom to call |
| `campaign` | number | Number of contacts with this client during this campaign, including the last one |
| `pdays` | number | Days since the client was last contacted in a previous campaign. **999 is a code meaning "never contacted before"** |
| `previous` | number | Number of contacts with this client before this campaign |
| `poutcome` | text | Outcome of the previous campaign: `success`, `failure`, `nonexistent` |
| `emp.var.rate` | number | Employment variation rate (quarterly national indicator) |
| `cons.price.idx` | number | Consumer price index (monthly national indicator) |
| `cons.conf.idx` | number | Consumer confidence index (monthly national indicator) |
| `euribor3m` | number | Euribor 3-month interest rate in percent (daily indicator) |
| `nr.employed` | number | Number of employees in thousands (quarterly national indicator) |
| `y` | text | Did the client subscribe to a term deposit? `yes` or `no` |

## Columns created in the notebook (not stored in the file)

| Column | How it is made |
|---|---|
| `subscribed` | 1 if `y` is `yes`, otherwise 0 |
| `contacted_before` | `no` if `pdays` is 999, otherwise `yes` |
| `month_number` | `month` as a number (3 to 12) |
| `year` | 2008, 2009 or 2010. Rebuilt from the row order: a new year starts whenever the month goes backwards |
| `month_start` | First day of the contact's month as a date, built from `year` and `month_number` |
| `age_band` | 17-24, 25-34, 35-44, 45-54, 55-64, 65+ |
| `calls_band` | `campaign` with everything from 6 upwards grouped as `6+` |
| `channel` | `mobile` for `cellular`, `landline` for `telephone` |
| `duration_minutes` | `duration` divided by 60 |

## Known quirks

- 12 rows are exact duplicates of another row. The notebook removes them (41,176 rows remain).
- 4,110 rows have `poutcome` = `failure` although `pdays` = 999. The official notes do not explain the disagreement.
- 4 rows have a `duration` of 0 seconds.
