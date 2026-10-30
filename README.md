# Aviation Accident Analysis

## Project Overview

This project analyzes aviation accident data for an airline and aircraft insurance client. The aim is to identify professionally built aircraft makes and models associated with lower rates of total destruction and lower rates of serious or fatal passenger injuries when an accident occurs.

The original dataset covers aviation accidents from 1948 to 2023. To focus on aircraft that could potentially still be active, the analysis keeps airplane accidents from 1983 onward and excludes amateur-built aircraft. Small and large airplanes are assessed separately using a threshold of 20 passengers.

## Business Questions

The analysis addresses the following questions:

1. Which aircraft makes and models have relatively low serious/fatal passenger injury rates?
2. Which aircraft makes have relatively low aircraft destruction rates?
3. How do results differ between small and large airplanes?
4. What other conditions are associated with accident severity?

## Data and Methods

The project uses `AviationData.csv`. The analysis was completed in two notebooks:

- `Aviation_Accidents_Cleaning.ipynb`
- `Aviation_Accidents_Data_Analysis.ipynb`

Python libraries used include Pandas, NumPy, Matplotlib, and Seaborn.

## Data Cleaning

The main cleaning and transformation steps were:

- Converted `Event.Date` to a datetime format.
- Retained airplane records from 1983 onward.
- Excluded amateur-built aircraft.
- Filled missing injury counts with zero.
- Estimated `Total.Passengers` by adding fatal, serious, minor, and uninjured persons.
- Created `Serious.Fatal.Injuries` and `Serious.Fatal.Injury.Rate`.
- Excluded records with zero estimated passengers because an injury rate could not be calculated.
- Removed records with missing aircraft-damage information.
- Created `Aircraft.Destroyed`, where 1 represents destroyed and 0 represents not destroyed.
- Standardized make and model names and created a combined `Make_Model` identifier.
- Retained aircraft makes with at least 50 accident records for more reliable comparisons.
- Standardized unknown values in engine type and weather condition.
- Treated records showing zero engines as missing.

The cleaned dataset contains **16,370 records and 36 columns** and is saved as `data/cleaned_aviation_data.csv`.

## Exploratory Data Analysis

Aircraft were divided into:

- **Small airplanes:** 20 passengers or fewer, with 15,946 records.
- **Large airplanes:** more than 20 passengers, with 424 records.

Mean serious/fatal injury rate and mean aircraft destruction rate were compared across aircraft makes. Sample sizes and injury-rate distributions were also reviewed to avoid relying only on averages from very small groups.

## Key Findings

### Small Aircraft

Among the small-aircraft makes with relatively low mean serious/fatal injury rates and sufficient observations were:

- **Maule:** mean injury rate of approximately 16.5%, based on 215 records.
- **Boeing:** approximately 16.5%, based on 204 records.
- **Aviat Aircraft Inc:** approximately 16.7%, based on 75 records.
- **Grumman Acft Eng Cor-Schweizer:** approximately 20.7%, based on 58 records.
- **Stinson:** approximately 21.6%, based on 129 records.

Maule, Grumman Acft Eng Cor-Schweizer, Stinson, Aeronca, Bellanca, and Diamond Aircraft Ind Inc also appeared among the small-aircraft makes with comparatively low destruction rates. Injury-rate distributions nevertheless varied within each make, so the averages should be interpreted together with sample sizes and the distribution plots.

### Large Aircraft

After excluding large-aircraft makes with very small samples, the most defensible comparison was among McDonnell Douglas, Boeing, Embraer, and Airbus:

- **McDonnell Douglas** had the lowest mean serious/fatal injury rate at approximately 0.8%, based on 36 records.
- **Boeing** recorded approximately 10.1%, based on 282 records.
- **Embraer** recorded approximately 10.5%, based on 45 records.
- **Airbus** recorded approximately 18.5%, based on 53 records.

For destruction rates:

- **Embraer:** approximately 8.9%.
- **Boeing:** approximately 9.6%.
- **McDonnell Douglas:** approximately 11.1%.
- **Airbus:** approximately 17.0%.

## Other Safety Factors

### Weather Condition

Accidents recorded under instrument meteorological conditions (IMC) were associated with more severe outcomes than accidents under visual meteorological conditions (VMC):

- IMC mean serious/fatal injury rate: **66.3%**.
- VMC mean serious/fatal injury rate: **23.7%**.
- IMC aircraft destruction rate: **37.3%**.
- VMC aircraft destruction rate: **7.2%**.

These results show an association, not proof that weather condition alone caused the outcomes. Records classified as unknown should also be interpreted cautiously.

### Number of Engines

The mean serious/fatal injury and destruction rates differed across engine-count groups:

- Two-engine aircraft had the highest mean serious/fatal injury rate at approximately **32.7%** and a destruction rate of approximately **17.6%**.
- Three-engine aircraft had the lowest mean serious/fatal injury rate at approximately **10.5%** and a destruction rate of approximately **6.3%**.

These comparisons require caution because the engine groups contain different numbers of accident records, and some groups are small. The results show association rather than causation.

## Recommendations

### Small Aircraft

Consider **Maule** and **Aviat Aircraft Inc** as leading candidates because their injury rates were relatively low and their sample sizes were more defensible than very small groups. **Grumman Acft Eng Cor-Schweizer** and **Stinson** also merit consideration because they combined relatively low injury rates with low destruction rates.

Final selection should be made at the specific model level and should consider sample size, operational purpose, age, maintenance history, and the full distribution of accident outcomes.

### Large Aircraft

Consider **Boeing**, **Embraer**, and **McDonnell Douglas** for further review:

- Boeing provides the strongest sample size and a comparatively low destruction rate.
- Embraer has the lowest destruction rate among the qualifying large-aircraft makes.
- McDonnell Douglas has the lowest mean serious/fatal injury rate among the qualifying large-aircraft makes.

Because this analysis is based only on accident records, the findings should not be interpreted as overall accident probabilities. Fleet exposure, flight hours, aircraft age, route characteristics, and maintenance information would be needed for a complete underwriting or purchasing decision.

## Key Visualizations

The analysis notebook includes:

- Mean serious/fatal injury rates for small and large aircraft makes.
- Injury-rate distributions for small aircraft using a violin plot.
- Injury-rate distributions for large aircraft using a strip plot.
- Aircraft destruction rates by make.
- Safety outcomes by weather condition.
- Safety outcomes by number of engines.

## Repository Structure

```text
dsc-course0-m8-lab/
├── data/
│   ├── AviationData.csv
│   ├── USState_Codes.csv
│   └── cleaned_aviation_data.csv
├── Aviation_Accidents_Cleaning.ipynb
├── Aviation_Accidents_Data_Analysis.ipynb
├── README.md
└── LICENSE
```

## How to Run

1. Clone the repository.
2. Open `Aviation_Accidents_Cleaning.ipynb` and run all cells.
3. Confirm that `data/cleaned_aviation_data.csv` is created.
4. Open `Aviation_Accidents_Data_Analysis.ipynb` and run all cells.

## Limitations

- The dataset contains accident and incident records, not total flights or flight hours, so it cannot directly estimate each aircraft make's overall probability of having an accident.
- Missing values were retained in some contextual variables where reliable imputation was not possible.
- Results for groups with few observations are less reliable.
- The findings identify associations and do not establish causation.



