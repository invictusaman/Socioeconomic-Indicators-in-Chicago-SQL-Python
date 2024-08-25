# Socioeconomic Indicators in Chicago

*This project is to showcase my SQL and Python skills working with real world dataset and how to use them together.*  

## Objectives

*   Understand a dataset of selected socioeconomic indicators in Chicago
*   Read Dataset using Python and store data in an SQLite database.
*   Solve example problems to practice SQL skills   


### About the dataset

The city of Chicago released a dataset of socioeconomic data to the Chicago City Portal. This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” for each Chicago community area, for the years 2008 – 2012.

Scores on the hardship index can range from 1 to 100, with a higher index number representing a greater level of hardship.

A detailed description of the dataset can be found on [the city of Chicago's website](https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01), but to summarize, the dataset has the following variables:

*   **Community Area Number** (`ca`): Used to uniquely identify each row of the dataset

*   **Community Area Name** (`community_area_name`): The name of the region in the city of Chicago

*   **Percent of Housing Crowded** (`percent_of_housing_crowded`): Percent of occupied housing units with more than one person per room

*   **Percent Households Below Poverty** (`percent_households_below_poverty`): Percent of households living below the federal poverty line

*   **Percent Aged 16+ Unemployed** (`percent_aged_16_unemployed`): Percent of persons over the age of 16 years that are unemployed

*   **Percent Aged 25+ without High School Diploma** (`percent_aged_25_without_high_school_diploma`): Percent of persons over the age of 25 years without a high school education

*   **Percent Aged Under** 18 or Over 64:Percent of population under 18 or over 64 years of age (`percent_aged_under_18_or_over_64`): (ie. dependents)

*   **Per Capita Income** (`per_capita_income_`): Community Area per capita income is estimated as the sum of tract-level aggragate incomes divided by the total population

*   **Hardship Index** (`hardship_index`): Score that incorporates each of the six selected socioeconomic indicators

### Questions & SQL Queries

#### Problem 1 - How many rows are in the dataset?

```
%sql SELECT COUNT(*) AS TOTAL_ROWS FROM chicago_socioeconomic_data;
```

#### Problem 2 - How many community areas in Chicago have a hardship index greater than 50.0?

```
%%sql

SELECT COUNT(community_area_name) AS COMMUNITY_AREAS_WITH_BETTER_HARDSHIP_INDEX
FROM chicago_socioeconomic_data
WHERE hardship_index > 50.0;
```

#### Problem 3 - What is the maximum value of hardship index in this dataset?

```
%%sql

SELECT MAX(hardship_index) AS MAX_HARDSHIP_INDEX
FROM chicago_socioeconomic_data;
```

#### Problem 4 - Which community area which has the highest hardship index?

```
%%sql

SELECT community_area_name AS COMMUNITY_WITH_HIGHEST_INDEX
FROM chicago_socioeconomic_data
ORDER BY hardship_index DESC
LIMIT 1;
```

#### Problem 5 - Which Chicago community areas have per-capita incomes greater than $60,000?

```
%%sql

SELECT community_area_name AS COMMUNITY_WITH_PCI_GT_$60000
FROM chicago_socioeconomic_data
WHERE per_capita_income_ > 60000;
```

#### Problem 6 - Create a scatter plot using the variables `per_capita_income_` and `hardship_index`. Explain the correlation between the two variables.

```
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

perCapitaIncome_vs_hardshipIndex = %sql SELECT per_capita_income_, hardship_index FROM chicago_socioeconomic_data;
dfCopy = perCapitaIncome_vs_hardshipIndex.DataFrame()

plot = sns.jointplot(x ='per_capita_income_', y='hardship_index', data = dfCopy, height=10, ratio=2)

# Rename the axis labels
plot.set_axis_labels('Per Capita Income (USD)', 'Hardship Index')

# Adjust layout
plt.tight_layout()

# Display the plot
plt.show()
```



##### Important Links

[SQLite](https://www.sqlite.org/about.html)
[Pandas](https://pandas.pydata.org/)
[Seaborn](https://seaborn.pydata.org/)
[MatplotLib](https://matplotlib.org/)
[Coursera](https://www.coursera.org/professional-certificates/ibm-data-science)

---
##### Follow my data-analyst journey: [Portfolio_Link](https://www.amanbhattarai.com)
