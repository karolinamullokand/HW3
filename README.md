**Creating usual R environment**

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

**I feel like it's more convenient to have separate table for only variables that have strongest relationship to vaccination status**

```
distincted_data <- distinct(Household_Pulse_data, TBIRTH_YEAR, EEDUC, EST_ST, RECVDVACC)
```
**Still valid version, but needs improvement**

```
p <- ggplot(data = distincted_data,
            mapping = aes(x = TBIRTH_YEAR,
                          y = count(n)))
```

# Final version

```
s <- ggplot(distincted_data, aes(x = TBIRTH_YEAR, fill = "RECVDVACC")) +
   geom_bar() +
   labs(title = "Vaccination Status by Birth Year",
        x = "Birth Year",
        y = "Vaccinated Count") +
   theme_minimal()
 
ggplotly(s)
```

# Summary
During the process of creating a visual representation of these variables, at first I thought that I would be able to place 






#2
library(plotly)
library(dplyr)
library(ggplot2)
library(tidyverse)
setwd("/Users/karolinamullokand/Desktop/ECO_B2000")
load("Household_Pulse_data_ph4c2.RData")

distincted_data <- distinct(Household_Pulse_data, TBIRTH_YEAR, EEDUC, EST_ST, RECVDVACC)

p <- ggplot(data = distincted_data,
            mapping = aes(x = EEDUC,
                          y = count(n)))

s <- ggplot(distincted_data, aes(x = "EEDUC", fill = "RECVDVACC")) +
  geom_bar() +
  labs(title = "Vaccination Status by Education level",
       x = "Education Level",
       y = "Vaccinated Count") +
  theme_minimal()

ggplotly(s)
