# Missing Data Mechanisms (NDD, SDD and UDD) 

David J. Hand, in his book *Dark Data: Why What You Don't Know Matters*, describes missing data as data you don't have — perhaps data you wish you had, or hoped to have, or thought you had, but nonetheless data you don't have.

Missing data are everywhere and data scientists need to understand when which methods do and don't work. Missing data problems are at the heart of data analysis.

## Why missing data matters

1. It leads to uncertainty of estimates such as standard errors, confidence intervals, etc.
2. It affects the accuracy of predictive models.
3. On average, it leads to wrong estimates of interest (systematic bias).
4. It makes prediction errors seem better than they will be in reality (systematic bias).

Missing data are not just annoying but can also bias your analysis i.e  means, trends, covariances, prediction models, etc.

## How missing data is coded

There should be great attention to missing data during data wrangling. Missing data are coded differently depending on the tool:

| Tool | Missing value code |
|---|---|
| R data frames | `NA` |
| Python / Pandas | `NaN` |
| SQL | `NULL` |
| JavaScript / JSON | `null` |
| CSV files | `"NA"`, `""`, `"NULL"` |
| SPSS | `-999`, `99999` |

## The three types of missingness

There are three types of missingness, according to David Hand's definitions:

1. **Not Data Dependent (NDD)**, also called **Missing Completely At Random (MCAR)**.
   It is missing for reasons unrelated to the data — for example: *"sickness preventing a student from sitting an exam."*
   The probability of being missing is constant for all units.

2. **Seen Data Dependent (SDD)**, also called **Missing At Random (MAR)**.
   It is missing for reasons related to data you already have — for example: *"a school discouraging lower-performing students from sitting an exam."*
   The probability of being missing depends on observed data.

3. **Unseen Data Dependent (UDD)**, also called **Missing Not At Random (MNAR)**.
   It is missing because of the values you would have obtained — for example: *"a student realizing they revised the wrong material, so they did not sit the exam."*
   The probability of being missing depends on unobserved data.

MCAR, MAR, and MNAR nomenclature is due to Rubin. Hand's (2020) terms — NDD, SDD, and UDD — refer to the same concepts but have the advantage of being intelligible. Hand's terms are therefore preferred, and it is advised to switch to them.

## The general missing data model

Formally, all three mechanisms are versions of one general equation:

$$
Pr(R = 0 \mid Y_{\mathrm{obs}}, Y_{\mathrm{mis}}, \psi)
$$

where $R$ indicates whether a value is observed (1) or missing (0), $Y_{\mathrm{obs}}$ is the data you can see, $Y_{\mathrm{mis}}$ is the data you can't, and $\psi$ are parameters linking them to missingness. The three mechanisms differ in which terms on the right side actually matter:

- **NDD (MCAR):** $Pr(R = 0 \mid Y_{\mathrm{obs}}, Y_{\mathrm{mis}}, \psi) = Pr(R = 0 \mid \psi)$
- **SDD (MAR):** $Pr(R = 0 \mid Y_{\mathrm{obs}}, Y_{\mathrm{mis}}, \psi) = Pr(R = 0 \mid Y_{\mathrm{obs}}, \psi)$
- **UDD (MNAR):** no simplification possible — depends on $Y_{\mathrm{mis}}$ itself
