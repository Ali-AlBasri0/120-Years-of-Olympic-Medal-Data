# Olympics EDA: Is a Medal About the Athlete, or the Sport?

## Problem Statement

Across 261,507 Olympic athlete records from 1896 to 2016, win rate ranges from 4.9% in Alpine Skiing to 28.7% in Hockey among sports with more than 5,000 records, a nearly 6x gap. Judging sports on results alone, without accounting for this gap, can mislead decisions on where to develop athletes.

## Executive Summary

This project is an exploratory data analysis (EDA) of Olympic athlete records covering 66 sports and 757 events from 1896 to 2016. The data was cleaned, and new features were created: `Is_Win` (whether the athlete won any medal), plus age, height and weight groups. Win rate (the share of athlete entries that ended with a medal) was then compared across sports, seasons, sexes, and age, height and weight groups using pandas and matplotlib. No predictive models were built, so there are no model performance metrics. This is a descriptive analysis.

The overall win rate is 14.9%, but it differs a lot by sport. Among the 18 sports with more than 5,000 records, the highest win rates are in Hockey (28.7%), Rowing and Ice Hockey (about 28%) and Football (about 24%), all team sports where one medal counts for every player on the roster. The lowest are Alpine Skiing (4.9%), Cross Country Skiing (about 8.5%) and Gymnastics (about 8.6%). Summer Games win rate (about 15.6%) is higher than Winter (about 11.8%). Sex has almost no effect (about 15.2% for women vs 14.8% for men), and Gold, Silver and Bronze are each about 5% for both. Win rate peaks at ages 26-30 and rises with height and weight, although this probably reflects the sports those athletes compete in rather than body size itself. Early Games also had very high win rates (about 46% in the 1890s) because fields were tiny, compared with about 14% in modern decades.

In conclusion, medal chances depend heavily on the sport, so win rates should not be compared across sports without context. Team medals inflate win rates in team sports, and early-Games rates are not a fair benchmark for today. We recommend accounting for competition size and team versus individual medals before judging a sport, and using modern data for any comparison.

## File Directory

```
Olympics-EDA/
├── README.md
├── Data/
│   ├── athlete_events.csv
│   └── cleaned_athlete_events.csv
├── notebooks/
│   ├── 01_Data_Collection.ipynb
│   ├── 02_Data_Cleaning.ipynb
│   └── 03_EDA.ipynb
└── Presentation/
    └── Ali Yusuf Al Basri.pptx
```

| File                                   | Description                                          |
| -------------------------------------- | ---------------------------------------------------- |
| `Data/athlete_events.csv`              | Raw athlete-event records, as downloaded             |
| `Data/cleaned_athlete_events.csv`      | Cleaned records used for the analysis                |
| `notebooks/01_Data_Collection.ipynb`   | Loading the raw data and first look at its structure |
| `notebooks/02_Data_Cleaning.ipynb`     | Cleaning the raw data and saving the cleaned file    |
| `notebooks/3_EDA.ipynb`                | Feature engineering, exploratory analysis and charts |
| `Presentation/Ali Yusuf Al Basri.pptx` | Final slide deck                                     |

## Data and Data Dictionary

**Source:** The data comes from the "120 years of Olympic history: athletes and results" dataset on Kaggle, which was scraped from sports-reference.com. The raw file is `athlete_events.csv`, and `cleaned_athlete_events.csv` is the cleaned version used in this project: https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results

**Size:** 261,507 rows, covering 1896 to 2016, 66 sports and 757 events.

### Original features

> Check this list against `df.columns` in your notebook and edit it so it matches your final cleaned file exactly.

| Column   | Type  | Description                                     |
| -------- | ----- | ----------------------------------------------- |
| `ID`     | int   | Unique athlete number                           |
| `Name`   | str   | Athlete name                                    |
| `Sex`    | str   | `M` or `F`                                      |
| `Age`    | float | Age in years at the Games                       |
| `Height` | float | Height in cm                                    |
| `Weight` | float | Weight in kg                                    |
| `Team`   | str   | Team name                                       |
| `NOC`    | str   | National Olympic Committee, 3-letter code       |
| `Games`  | str   | Year and season of the Games                    |
| `Year`   | int   | Year of the Games                               |
| `Season` | str   | `Summer` or `Winter`                            |
| `City`   | str   | Host city                                       |
| `Sport`  | str   | Sport name                                      |
| `Event`  | str   | Event name                                      |
| `Medal`  | str   | `Gold`, `Silver`, `Bronze` or `Lose` (no medal) |

### Engineered features

| Column         | Type     | Description                                                                   |
| -------------- | -------- | ----------------------------------------------------------------------------- |
| `Is_Win`       | bool     | `True` if `Medal` is not `Lose`. Its mean is the win rate                     |
| `Age_Group`    | category | Under 18, 18-25, 26-30, 31-40, 41-50, 51+                                     |
| `Height_Group` | category | 125-150, 151-165, 166-180, 181-195, 196-210, 211-230 (cm)                     |
| `Weight_Group` | category | 25-50, 51-65, 66-80, 81-95, 96-110, 111-140, 141-220 (kg)                     |
| `Decade`       | int      | `(Year // 10) * 10`, used for the win rate over time                          |
| `Sport_Type`   | str      | Team or Individual (used only if you include the team vs individual analysis) |

## Conclusions and Recommendations

**Conclusions**

- Medal chances depend heavily on the sport, with a nearly 6x gap between the top and bottom sports.
- The sports with the highest win rates are team sports, where one medal is counted for every player on the roster.
- Summer Games win rate is higher than Winter.
- Sex does not change the chance of winning or the type of medal.
- Win rate peaks at 26-30 and rises with height and weight, but this likely reflects sport choice.
- Early-Games win rates were very high on tiny fields and are not comparable to today.

**Recommendations**

1. Compare sports fairly by accounting for competition size and team versus individual medals before judging a sport as easy or hard.
2. Favour sports with a strong medal return per athlete developed, using modern data only.
3. Do not use early-Games win rates as a benchmark.

**Limitations**

- A team medal is counted for each roster member, which inflates win rates in team sports.
- Small groups (for example, very young or very old athletes) can give unstable rates.
- This is a descriptive analysis, so it shows patterns, not causes.

## Areas for Further Research

- Measure athletes per event and model how much of a sport's win rate it explains.
- Count each team medal once, to remove the roster inflation.
- Repeat the analysis on recent Games only (for example since 1990).
- Compare countries (NOC) and see whether the sport effect holds within each country.

## Sources

- Griffin, R. (2018). *120 years of Olympic history: athletes and results.* Kaggle. https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results
- Sports-Reference.com Olympics data (original source of the scraped records).
- pandas and matplotlib documentation.
