# Creating usual R environment

```
setwd("/Users/karolinamullokand/Desktop/ECO_B2000")
load("Household_Pulse_data_ph4c2.RData")
View(Household_Pulse_data)
install.packages("dplyr")
install.packages("plotly")
library(plotly)
library(dplyr)
library(ggplot2)
library(tidyverse)
```

# I feel like it's more convenient to have separate table for only variables that have strongest relationship to vaccination status

```
distincted_data <- distinct(Household_Pulse_data, TBIRTH_YEAR, EEDUC, EST_ST, RECVDVACC)
```
# Still valid version, but needs improvement
p <- ggplot(data = distincted_data,
            mapping = aes(x = TBIRTH_YEAR,
                          y = count(n))) 

# Final version

```
s <- ggplot(distincted_data, aes(x = TBIRTH_YEAR, y = n, color = EST_ST)) +
  geom_point() +
  labs(title = "Vaccination Status by Birth Year and Location",
       x = "Birth Year",
       y = "Count of Vaccinated Individuals",
       color = "Location") +
  theme_minimal()

ggplotly(s)
```

