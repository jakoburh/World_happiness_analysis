# World Happiness Report 2021 Analysis

Exploratory analysis of national happiness and socio-economic indicators using Microsoft Excel.

This was an independent data-analysis project based on the World Happiness Report 2021 dataset. I used data from 149 countries to explore how national happiness scores are associated with GDP per capita, social support, healthy life expectancy, freedom to make life choices, generosity and perceptions of corruption.

The project was primarily an exercise in developing my Excel, statistical analysis and data-visualization skills while learning how easily conclusions can change depending on methodology, variable selection and sample size.

## Questions

I focused on several questions:

- Which socio-economic factors are most strongly associated with national happiness scores?
- How do happiness and GDP differ between world regions?
- Does the relationship between GDP and happiness remain similar within individual regions?
- What is the relationship between freedom to make life choices and perceptions of corruption?
- Is generosity associated with healthy life expectancy?
- How do rankings change when I construct my own composite wellbeing score?
- What happens when I try to model a hypothetical increase in GDP in African countries?
- Can a six-variable regression model estimate national happiness scores?

## Dataset

The dataset contains observations for **149 countries** from the World Happiness Report 2021.

The main outcome used in this analysis was the **Ladder score**, representing national average life evaluation.

The explanatory variables I examined were:

- logged GDP per capita
- social support
- healthy life expectancy
- freedom to make life choices
- generosity
- perceptions of corruption

The World Happiness Report uses these variables to help explain differences in life evaluations between countries. The Ladder score itself is based on people's reported life evaluations rather than being calculated directly from these six variables.

The dataset also contained a regional indicator, which I used for comparisons between different parts of the world.

## Tools

**Microsoft Excel**

The project involved:

- `CORREL`
- `AVERAGEIFS`
- `COUNTIFS`
- `RANK`
- `IFS`
- `MIN` / `MAX`
- pivot tables
- conditional formatting
- Pearson correlation coefficients
- normalization
- linear and polynomial trend lines
- multiple linear regression
- data visualization

I also experimented with constructing new indicators and using existing variables for simple scenario modelling.

## Data cleaning

When the dataset was imported into Excel, some decimal values were interpreted incorrectly because of decimal-separator formatting.

For example, a healthy life expectancy value such as `71.600` could be interpreted as `71600`.

I corrected the affected numerical columns before performing the analysis. The dataset otherwise required relatively little cleaning.

## Analysis

### Correlation with happiness

I calculated Pearson correlation coefficients between the Ladder score and the six explanatory variables.

The strongest linear associations with happiness were:

| Variable | Pearson r |
| --- | ---: |
| Logged GDP per capita | **0.79** |
| Healthy life expectancy | **0.77** |
| Social support | **0.76** |
| Freedom to make life choices | **0.61** |
| Perceptions of corruption | **-0.42** |
| Generosity | **-0.02** |

GDP, healthy life expectancy and social support showed the strongest positive relationships with happiness in this dataset.

Generosity showed almost no linear relationship with the Ladder score.

Perceptions of corruption showed a negative relationship: countries where corruption was perceived as more widespread tended to have lower happiness scores.

These correlations describe associations and should not be interpreted as evidence that one variable directly causes changes in happiness.

### Regional comparison

I used pivot tables to compare average happiness scores, logged GDP per capita and the number of countries within each region.

For example:

- **North America and ANZ** had the highest average happiness score at approximately **7.13**, but contained only four countries.
- **Western Europe** had an average happiness score of approximately **6.92** and the highest average logged GDP per capita.
- **Sub-Saharan Africa** contained the largest number of countries in the dataset (**36**) and had an average happiness score of approximately **4.49**.
- **South Asia** had an average happiness score of approximately **4.44**.

The comparison also demonstrated why sample size matters. An average based on four countries can be influenced much more strongly by a single observation than an average calculated from 36 countries.

### GDP and happiness within regions

The overall dataset showed a strong positive relationship between GDP and happiness, but I wanted to see whether the same pattern remained visible inside individual regions.

I compared countries within **North America and ANZ** and **Sub-Saharan Africa**.

North America and ANZ appeared to show a similar relationship between GDP and happiness, but the region contained only four countries, making the pattern unreliable.

Sub-Saharan Africa provided more observations and showed considerably more variation. Countries with similar GDP values could still have noticeably different happiness scores.

This helped demonstrate that a strong relationship across the complete dataset does not necessarily behave identically within every subgroup.

### Freedom and perceptions of corruption

I calculated a correlation of approximately **r = -0.40** between freedom to make life choices and perceptions of corruption.

This suggests a negative linear association in the full dataset, but regional averages did not follow a perfectly consistent pattern.

The result therefore does not imply that greater reported freedom automatically corresponds to lower perceived corruption in every country or region.

### Generosity and life expectancy

I also examined the relationship between generosity and healthy life expectancy.

The correlation was approximately:

**r = -0.16**

with:

**R² ≈ 0.026**

The scatterplot showed considerable variation and no meaningful linear pattern between the two variables.

### Normalization

Some variables were measured on very different scales, making direct visual comparisons difficult.

To explore this problem, I normalized GDP and perceptions of corruption using min-max normalization:

`normalized value = (value - minimum) / (maximum - minimum)`

I then compared regional averages of the normalized variables and used conditional formatting to highlight differences.

This was mainly an exercise in learning why variables often need to be transformed before they can be compared visually.

### Custom wellbeing ranking

I experimented with creating my own simple composite indicator:

`Wellbeing score = GDP + Social support + Freedom - Corruption`

I then ranked countries using both this score and their original Ladder score.

Only four countries kept exactly the same ranking position:

- Slovenia
- Sweden
- Canada
- Cyprus

The exercise demonstrated how strongly country rankings can change when different variables and weights are selected.

This custom score was not intended as a scientifically validated wellbeing index. The variables were not normalized to the same scale or assigned theoretically justified weights, so the exercise primarily demonstrates the sensitivity of composite rankings to methodological choices.

### GDP scenario for African countries

I also experimented with modelling how higher GDP values might affect predicted happiness scores for African countries.

I compared linear, polynomial and other trend models. Even the better-fitting polynomial model had a low R², making the resulting predictions unreliable.

There was also an important methodological limitation in my original implementation: the dataset contains **logged GDP per capita**, and I applied the hypothetical increase directly to the logged variable. Multiplying logged GDP by 1.20 is not mathematically equivalent to increasing actual GDP per capita by 20%.

Because of this, I consider this section a useful modelling experiment rather than a valid economic simulation.

### Multiple linear regression

I built a multiple linear regression model using all six explanatory variables:

- logged GDP per capita
- social support
- healthy life expectancy
- freedom to make life choices
- generosity
- perceptions of corruption

The fitted model produced an average absolute difference of approximately **0.41 Ladder-score points** between fitted and observed happiness scores.

However, this error was calculated using the same dataset used to construct the model. I did not create a separate training and test set, so the result should be interpreted as **in-sample model fit**, not evidence of predictive performance on unseen countries.

The remaining prediction errors also reinforced that national happiness cannot be fully represented by these six variables alone.

## Main findings

Based on this dataset:

- logged GDP per capita showed the strongest positive linear association with happiness (**r ≈ 0.79**);
- healthy life expectancy (**r ≈ 0.77**) and social support (**r ≈ 0.76**) were similarly strongly associated with happiness;
- freedom to make life choices showed a positive association (**r ≈ 0.61**);
- generosity showed almost no linear relationship with happiness (**r ≈ -0.02**);
- perceptions of corruption were negatively associated with happiness (**r ≈ -0.42**);
- relationships observed across all countries were not always equally clear within individual regions;
- changing the variables and weights used to construct a ranking substantially changed country positions;
- the six-variable regression reproduced happiness scores with an average in-sample absolute error of approximately **0.41 points**, but this should not be interpreted as out-of-sample predictive accuracy.

Overall, the analysis suggested that national happiness is associated with several economic and social factors rather than being adequately explained by a single variable.

## Limitations

The project has several important limitations.

The analysis is observational, so correlations cannot establish causality.

Regional sample sizes differed substantially. For example, North America and ANZ contained only four countries while Sub-Saharan Africa contained 36.

Some variables and their original methodology were not well documented in the Kaggle version of the dataset I used at the time, which made interpretation more difficult.

The custom wellbeing score used an arbitrary formula and did not normalize all variables or establish meaningful statistical weights before combining them.

The GDP scenario was applied to logged GDP rather than transforming a genuine 20% increase in GDP per capita onto the logarithmic scale, so it should not be treated as a valid economic prediction.

The regression model was evaluated on the same observations used to fit it and therefore provides no estimate of its ability to generalize to unseen data.

Finally, happiness is a complex outcome affected by many factors not represented here, including inequality, education, political stability, culture, family circumstances and individual psychology.

## What I learned

This project expanded my understanding of data analysis beyond basic descriptive statistics.

It taught me how to:

- calculate and interpret Pearson correlations;
- distinguish correlation from causation;
- compare aggregate patterns with patterns inside individual groups;
- work with pivot tables and conditional aggregation;
- normalize variables measured on different scales;
- build and critically evaluate a simple composite index;
- experiment with linear and nonlinear models;
- construct a multiple linear regression model;
- recognize the difference between fitting existing observations and predicting unseen ones;
- question whether the mathematical transformation used in a simulation actually represents the scenario being described;
- recognize how methodological decisions can substantially change the apparent conclusion of an analysis.

Looking back at the project also makes several weaknesses in my original methodology more obvious, which is useful in itself. Later work with R, Python and statistical modelling gave me a better understanding of how these analyses could be made more reproducible and rigorous.

## Repository contents

- `world-happiness-report-2021_analysis.xlsx` — Excel workbook containing the data cleaning, calculations, pivot tables, models and visualizations
- `world_happines2021_analysis_report.pdf` — written analysis describing the methodology, results and original interpretation

## Possible future improvements

If I revisited this project, I would:

- reproduce the complete analysis in Python or R;
- document the source and definition of every variable before analysis;
- create a reproducible data-cleaning pipeline;
- separate exploratory analysis from confirmatory statistical testing;
- use confidence intervals and formal significance testing where appropriate;
- evaluate regression models using train/test separation or cross-validation;
- correctly transform hypothetical percentage changes when working with logarithmic variables;
- normalize variables before constructing composite indices;
- justify any weights used in a wellbeing index;
- investigate additional variables such as inequality, education and political stability;
- compare alternative models rather than assuming linear relationships.
