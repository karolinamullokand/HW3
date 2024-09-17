**Study group:** Karolina Mullokand & Jermaine

# 1
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

**Final version**

```
s <- ggplot(distincted_data, aes(x = TBIRTH_YEAR, fill = "RECVDVACC")) +
   geom_bar() +
   labs(title = "Vaccination Status by Birth Year",
        x = "Birth Year",
        y = "Vaccinated Count") +
   theme_minimal()
 
ggplotly(s)
```

# 2

**Creating usual R environment**

```
library(plotly)
library(dplyr)
library(ggplot2)
library(tidyverse)
setwd("/Users/karolinamullokand/Desktop/ECO_B2000")
load("Household_Pulse_data_ph4c2.RData")
```

```
distincted_data <- distinct(Household_Pulse_data, TBIRTH_YEAR, EEDUC, EST_ST, RECVDVACC)

levels(distincted_data$EEDUC)
```

**Recoding Education Levels**
```
distincted_data$education_level <- fct_recode(distincted_data$EEDUC,
                                              "HS diploma" = "HS diploma",
                                              "some coll" = "some coll",
                                              "assoc deg" = "assoc deg",
                                              "bach deg" = "bach deg",
                                              "adv deg" = "adv deg")
```

**Result**
```
p <- ggplot(data = distincted_data,
            mapping = aes(x = EEDUC,
                          y = count(n)))

s <- ggplot(distincted_data, aes(x = EEDUC, fill = RECVDVACC)) +
  geom_bar() +
  labs(title = "Vaccination Status by Education level",
       x = "Education Level",
       y = "Vaccinated Count") +
  theme_minimal()

ggplotly(s)
```

# 3
**Creating usual R environment**

```
library(plotly)
library(dplyr)
library(ggplot2)
library(tidyverse)
setwd("/Users/karolinamullokand/Desktop/ECO_B2000")
load("Household_Pulse_data_ph4c2.RData")

distincted_data <- distinct(Household_Pulse_data, TBIRTH_YEAR, EEDUC, EST_ST, RECVDVACC)
```
**Creating dataframe for future use in creating one more dataframe**

```
vaccination_summary <- distincted_data %>%
  group_by(EST_ST, RECVDVACC) %>%
  summarise(count = n(), .groups = 'drop')

democrat_states <- c("California", "New York", "Massachusetts", "Washington", "Oregon", "Illinois", "Maryland", "Colorado", "Connecticut", "Delaware", "District of Columbia", "Hawaii", "Maine", "Minnesota", "New Jersey", "Rhode Island", "Vermont",
"Washington")
republican_states <- c("Texas", "Alabama", "Oklahoma", "Utah", "Idaho", "Mississippi", "Wyoming", "Alaska", "Arkansas", "Kansas", "Kentucky", "Louisiana", "Missouri", "Montana", "Nebraska", "North Dakota", "South Carolina", "Tennessee", "West Virginia", "Wyoming")
swing_states <- c("Florida", "Ohio", "Pennsylvania", "Michigan", "Wisconsin", "Arizona", "Georgia", "Nevada", "Indiana", "Iowa", "New Hampshire", "New Mexico", "North Carolina", "Virginia")

democrat_data <- data.frame(EST_ST = democrat_states, political_identity = "Democrats")
repulicans_data <- data.frame(EST_ST = republican_states, political_identity = "Republicans")
swings_data <- data.frame(EST_ST = swing_states, political_identity = "Others")
```

**Grouping them together**

```
political_identity <- rbind(democrat_data, repulicans_data, swings_data)
data.frame(political_identity)

final_data <- merge(vaccination_summary, political_identity, by = "EST_ST")
```
**Creating a interactive graph**

```
s <- ggplot(final_data, aes(x = political_identity, fill = RECVDVACC)) +
       geom_bar() +
         labs(title = "Vaccination Status by State's Political Identity",
              x = "Political Idenitity",
              y = "Vaccinated Count") +
         theme_minimal()

ggplotly (s)
```


# Summary
During the process of creating a visual representation of these variables, I was struggling with finding it grouped correctly, ofthen had a syntax errors.
Creating a third one was a challenge! I'm still not sure if I counted all of the states, and for sure not all of them grouped correctly into political identity. I used some data from different websites, just to have a approximate political identity data







