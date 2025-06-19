# R-code: R Practice and Data Visualization

This repository contains R code, notebooks, and datasets for practising data manipulation, analysis, and visualisation using R and ggplot2. It features hands-on exercises with real datasets (`cdc.csv`, `gapminder.csv`), R Markdown notebooks, and their generated HTML outputs.

---

## Repository Contents

- **Practise R.Rmd** — R Markdown notebook for data filtering and manipulation exercises with `gapminder.csv`.
- **Practise R.nb.html** — HTML version of the above notebook.
- **Practise visualisation in R with ggplot2.Rmd** — R Markdown notebook for visualizations using `ggplot2` and the `cdc.csv` dataset.
- **Practise visualisation in R with ggplot2.nb.html** — HTML version of the above visualization notebook.
- **cdc.csv** — Health survey sample data (height, weight, health status, etc.).
- **gapminder.csv** — Country-level data (population, GDP, life expectancy, etc.).

---

## Data Description

### cdc.csv

Sample columns:
- `genhlth`: General health (e.g., good, fair, excellent)
- `exerany`: Exercise any (0 = no, 1 = yes)
- `hlthplan`: Health plan (0/1)
- `smoke100`: Ever smoked 100 cigarettes (0/1)
- `height`, `weight`, `wtdesire`, `age`
- `gender`: 'm' or 'f'

### gapminder.csv

Sample columns:
- `year`
- `country`
- `region`
- `population`
- `gdp_per_capita`
- `life_expectancy`

---

## Example Analysis & Code

### Data Manipulation with gapminder.csv

**1. Filter countries with population < 1,000,000**

```r
data <- read.csv('gapminder.csv')
small_countries <- subset(data, data$population < 1000000)
head(small_countries)
```

**2. List countries in 2011 with GDP per capita > 60,000**

```r
gdp_per_capita_filter <- subset(data, year == 2011 & gdp_per_capita > 60000)
gdp_per_capita_filter <- gdp_per_capita_filter[order(gdp_per_capita_filter$gdp_per_capita), ]
head(gdp_per_capita_filter)
```

**3. Europe, life expectancy > 82**

```r
europe_82 <- subset(data, region == 'Europe' & data$life_expectancy >= 82)
unique(europe_82$country)
```

### Visualization with cdc.csv and ggplot2

**1. Prepare Data**

```r
data <- read.csv('cdc.csv')
data$smoke100 <- ifelse(data$smoke100 == 1, "yes", "no")
data$exerany <- ifelse(data$exerany == 1, "yes", "no")
data$hlthplan <- ifelse(data$hlthplan == 1, "yes", "no")
```

**2. Scatterplot: Height vs Weight (males), colored by health, shaped by smoker**

```r
library(ggplot2)
males <- data[data$gender == 'm',]
ggplot(data = males, aes(x = weight, y = height, color = genhlth, shape = smoke100)) +
  geom_point() +
  labs(title = "Male Height vs Weight", x = "Weight (lbs)", y = "Height (inches)")
```

**3. Bar plot of general health**

```r
ggplot(data, aes(x = genhlth)) +
  geom_bar(fill = "steelblue") +
  labs(title = "Count of People by General Health")
```

**4. Proportional bar plot by gender**

```r
ggplot(data, aes(x = genhlth, fill = gender)) +
  geom_bar(position = "fill") +
  labs(title = "Proportion of General Health by Gender", y = "Proportion") +
  scale_y_continuous(labels = scales::percent)
```

---

## Example Visualizations

- **Scatterplots** (height vs weight, colored by health, smoker status)
- **Facetted scatterplots** (by health, gender)
- **Line plots** (height vs weight for males and females)
- **Bar plots** (count and proportion by general health)

*See the HTML notebooks for rendered outputs and interactive navigation.*

---

## Getting Started

**Requirements:**  
R, RStudio, and the following packages: `ggplot2`, `dplyr` (optional), `readr`, `scales`.

**How to Run:**
1. Clone/download this repository.
2. Open the `.Rmd` files in RStudio and run cells interactively.
3. View the `.nb.html` files in your browser for completed examples.

---

## References

- [gapminder.org](https://www.gapminder.org/data/)
- [Centers for Disease Control and Prevention (CDC) sample data](https://www.cdc.gov/)

---

Feel free to expand or modify this README as you add more exercises or datasets!

If you want specific sections expanded, or more code/visualization examples included, let me know!
