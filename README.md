# 📊 Suicide Bombing Attacks Analysis (R Project)

## 📁 Project Overview

This project analyzes suicide bombing attack data using **R**. It explores trends over time, geographical distribution, casualties, and environmental conditions.

---

## 📂 Dataset

* File name: `Suicide_bombing_attacks.csv`
* Place the dataset in your working directory or update the file path accordingly:

```r
data <- read_csv("Suicide_bombing_attacks.csv")
```

---

## 🛠️ Libraries Used

```r
library(readr)
library(dplyr)
library(ggplot2)
```

---

## 📥 Load and Prepare Data

```r
data <- read_csv("Suicide_bombing_attacks.csv")

str(data)

data <- data %>%
  mutate(Year = as.numeric(substring(Date, nchar(Date)-3, nchar(Date))))
```

---

## 📈 Visualizations

### 1. Number of Attacks per Year

```r
ggplot(data, aes(x = Year)) +
  geom_bar() +
  labs(title = "Number of Suicide Bombing Attacks Over Time",
       x = "Year",
       y = "Number of Attacks")
```

---

### 2. Number of Attacks by City

```r
city_attack_count <- data %>%
  group_by(City) %>%
  summarise(Count = n())

ggplot(city_attack_count, aes(x = reorder(City, Count), y = Count)) +
  geom_bar(stat = "identity") +
  coord_flip() +
  labs(title = "Number of Attacks by City",
       x = "City",
       y = "Number of Attacks")
```

---

### 3. Number of Attacks by Province

```r
province_attack_count <- data %>%
  group_by(Province) %>%
  summarise(Count = n())

ggplot(province_attack_count, aes(x = reorder(Province, Count), y = Count)) +
  geom_bar(stat = "identity") +
  labs(title = "Number of Attacks by Province",
       x = "Province",
       y = "Number of Attacks")
```

---

### 4. Casualties Over Time

```r
casualty_summary <- data %>%
  group_by(Year) %>%
  summarise(
    Killed_Max = sum(as.numeric(Killed_Max), na.rm = TRUE),
    Injured_Max = sum(as.numeric(Injured_Max), na.rm = TRUE)
  )

ggplot(casualty_summary, aes(x = Year)) +
  geom_line(aes(y = Killed_Max, color = "Killed Max")) +
  geom_line(aes(y = Injured_Max, color = "Injured Max")) +
  labs(title = "Casualties from Suicide Bombing Attacks Over Time",
       x = "Year",
       y = "Number of Casualties")
```

---

### 5. Attacks by Day Type

```r
day_type_count <- data %>%
  group_by(Blast_Day_Type) %>%
  summarise(Count = n())

ggplot(day_type_count, aes(x = Blast_Day_Type, y = Count)) +
  geom_bar(stat = "identity") +
  labs(title = "Number of Attacks by Blast Day Type",
       x = "Day Type",
       y = "Number of Attacks")
```

---

### 6. Sect Targeting Analysis

```r
sect_targeting <- data %>%
  filter(!is.na(Targeted_Sect_if_any)) %>%
  group_by(Targeted_Sect_if_any) %>%
  summarise(Count = n())

ggplot(sect_targeting, aes(x = reorder(Targeted_Sect_if_any, Count), y = Count)) +
  geom_bar(stat = "identity") +
  coord_flip() +
  labs(title = "Number of Attacks Targeting Different Sects",
       x = "Targeted Sect",
       y = "Number of Attacks")
```

---

### 7. Temperature Distribution During Attacks

```r
data <- data %>%
  mutate(
    Temperature_C = as.numeric(Temperature_C),
    Temperature_F = as.numeric(Temperature_F)
  )

ggplot(data, aes(x = Temperature_C)) +
  geom_histogram(binwidth = 1) +
  labs(title = "Temperature Distribution During Attacks (Celsius)",
       x = "Temperature (C)",
       y = "Frequency")
```

---

## ▶️ How to Run

1. Install required packages:

```r
install.packages(c("readr", "dplyr", "ggplot2"))
```

2. Place `Suicide_bombing_attacks.csv` in your project folder.

3. Run the script in RStudio or any R environment.

---

## 📊 Insights You Can Derive

* Yearly trends in attacks
* Most affected cities and provinces
* Casualty patterns over time
* Targeted sect distribution
* Environmental factors (temperature)

---

## 📌 Notes

* Ensure column names in CSV match the script.
* Handle missing values carefully.
* You can extend this with advanced analytics (ML models, forecasting).

---

## 📎 Repository Structure

```
project-folder/
│── README.md
│── analysis.R
│── Suicide_bombing_attacks.csv
```

---

## ⭐ Contribution

Feel free to fork, improve visualizations, or add predictive models!

---
