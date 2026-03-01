# WVS Wave 7: Institutional Trust and Economic Performance

## Research Question
**"Institutional Trust and Economic Performance: Does National Wealth Buffer the Impact of Individual Socio-Economic Status on Trust in Government?"**

This research aims to investigate whether the relationship between an individual's perceived social class and their confidence in political institutions is moderated by the national economic context (GDP per capita).

## Dataset Overview
The dataset used for this analysis is a multi-source compilation combining individual survey responses with national economic indicators.

* **Individual Level Data:** Subset of the World Values Survey (WVS) Wave 7 (2017-2022).
    * **Source:** World Values Survey Association (www.worldvaluessurvey.org).
    * **Sample Size:** A random subsample of 2,000 respondents (stratified by country) from the `2000_WVS_data.csv` file.
* **Macro Level Data:** External economic indicators not present in the original WVS dataset.
    * **Source:** World Bank - World Development Indicators (WDI).
    * **Data Points:** GDP (current USD), GDP PPP (current international $), GDP per capita (PPP), and Total Population.
    * **Method:** These variables are retrieved dynamically via the WDI API in the `cleaning.R` script, matching the specific `A_YEAR` of the survey for each country.

## Key Variables
The study focuses on the following 14 variables:

| Variable ID | Label | Description | Source |
| :--- | :--- | :--- | :--- |
| B_COUNTRY_ALPHA | Country Code | ISO 3166-1 alpha-3 code. | WVS |
| A_YEAR | Survey Year | Year of the interview (2017-2022). | WVS |
| Q71 | Confidence: Government | Confidence in national government (1-4). | WVS |
| Q69 | Confidence: Police | Confidence in the police (1-4). | WVS |
| Q73 | Confidence: Parliament | Confidence in parliament (1-4). | WVS |
| Q74 | Confidence: Civil Services | Confidence in civil services (1-4). | WVS |
| Q57 | General Trust | "Most people can be trusted" (1-2). | WVS |
| Q260 | Sex | Respondent's sex (1: Male, 2: Female). | WVS |
| Q262 | Age | Respondent's age in years. | WVS |
| Q275 | Education | Highest educational level (1-8). | WVS |
| Q288 | Income Decile | Household income scale (1-10). | WVS |
| Q287 | Social Class | Subjective social class (1-5). | WVS |
| GDP_USD_PPP_pc | GDP per capita | National GDP (PPP) per capita. | World Bank |
| Population | Total Population | Total national population. | World Bank |

## Descriptive Statistics
The following table presents descriptive statistics for the 5 most important individual-level variables based on the `2000_WVS_data.csv` sample. 

> **Note:** Negative values representing "No answer" or "Don't know" in the raw data were treated as missing (`NA`).

| Variable | Mean | StdDev | Min | Max | N |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Q71 (Gov. Trust) | 2.54 | 0.98 | 1 | 4 | 1,892 |
| Q287 (Social Class) | 3.21 | 1.05 | 1 | 5 | 1,945 |
| Q262 (Age) | 43.12 | 16.85 | 18 | 98 | 2,000 |
| Q275 (Education) | 4.85 | 2.15 | 1 | 8 | 1,978 |
| Q288 (Income Decile) | 4.92 | 2.31 | 1 | 10 | 1,812 |

## Survey Timing and Consequences
The Wave 7 survey spans a significant period of global change (2017–2022).

* **Pandemic Effects:** Data collected after 2019 may reflect heightened sensitivity to government performance due to COVID-19 management.
* **Economic Matching:** National GDP values (from World Bank) are matched to the specific survey year for each country. This ensures that a respondent surveyed in 2017 is compared against 2017 economic metrics, while a 2021 respondent is compared against 2021 metrics.
* **Cross-Country Comparison:** Because not all countries were surveyed in the same year, cross-country variance in "Trust" might be partially attributed to the global political climate of a specific year rather than just national characteristics.

## Directory Structure
```text
project-root/
├─ data/
│  ├─ raw/        ← World Values Survey raw files
│  └─ clean/      ← Outputs (subsetted and merged files)
└─ scripts/
   └─ cleaning.R  ← R script for cleaning, sampling, and WDI merging
