
# Analysis of trends in Dairy Consumption in the United States

#### Aidan Bobholz and Gavin Anderson

## Introduction

The goal of this project is to explore data sets around the Dairy Industry to better understand trends in the usage of dairy commodities. As with most agricultural markets there have been notable events that occur in which cause massive changes in the usage of agricultural commodities. Analysis on this topic can give us as students in agriculture a better insight into the ways in which the dairy market is effected. Our end goal is to identify the major trends in dairy commodity usages and find reasons that may be attributed to the increased or decreased usages.

To follow this goal we will explore further into these questions:

 1. What is the most consumed dairy commodity?
 
 2. What are the trends in consumption of dairy products?
 
 3. Does corn production trends follow the trends of dairy consumption?
 
 4. Does the sale price of Alfalfa production effect dairy consumption?
 
 5. How does Average price paid for milk effect dairy consumption?
 
 6. Does milk cow costs have an effect on dairy consumption?
 
## Data
 
### Structure

The link to our datasets can be found at <https://www.ers.usda.gov/data-products/dairy-data.aspx>. We are using the "Dairy products: Per capita consumption, United States (Annual)" as our major dataset and will have additional datasets added to compare trends in; corn production, milk alternative commodities, and the Annual milk production and factors affecting supply (Annual). 







### Cleaning

**Steps of cleaning the dataset to be included at a later point here**

### Variables

- X: Definition of variable

## Results

#### What is the most consumed dairy commodity?

Reply #1

#### What are the trends in consumption of dairy products?

Reply #2

#### Does corn production trends follow the trends of dairy consumption?

Reply #3

#### Does the sale price of Alfalfa production effect dairy consumption?

Reply #4

#### How does Average price paid for milk effect dairy consumption?

Reply #5

#### Does milk cow costs have an effect on dairy consumption?

Reply #6

## Conclusion

In the conculusion...















# This is all extra to be added in or deleted


```{R, include = FALSE}

# Load the readxl package
library(tidyverse)
library(readxl)


library(readr)

# Read the CSV file from GitHub

dataset <- read.csv("pcconsp_1_csv.csv")

```

```{R}

str(dataset)

```

```{R}

summary(dataset)

```

# Questions:
## What is the current trend of dairy products?

```{R}

# Load necessary libraries
library(ggplot2)
library(reshape2)
library(viridis)


my_palette <- viridis(22)

# Reshape data into long format
melted_data <- melt(dataset, id.vars = "Year")



# Create density plot
ggplot(melted_data, aes(x = Year, y = value , color = variable)) +
  geom_line()+
  theme(axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5))+
  scale_color_manual(values = my_palette)





```

*This visual will be in works of improvements but as a start helps show the major variables in this dataset. Also we can find that the value of fluid beverage milk has been on a constant decline. By working on this visual further we may see even more trends with dairy products.*


## What is the most popularly consumed dairy product?

```{R}

head(dataset)

```

```{R}

my_palette <- viridis(22)

# Reshape data into long format
melted_data <- melt(dataset, id.vars = "Year")

melted_data_products <- melted_data %>%
  filter(variable != "Milk_fat_basis", variable != "Skim_solids_basis")

# Create density plot
ggplot(melted_data_products, aes(x = variable, y = value)) +
  geom_boxplot()+
  theme(axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5))


melted_data_below100 <- melted_data %>% 
  filter(value <= 100)

ggplot(melted_data_below100, aes(x = variable, y = value)) +
  geom_boxplot()+
  theme(axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5))

ggplot(melted_data_below100, aes(x = Year, y = value , color = variable)) +
  geom_line()+
  theme(axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5))+
  scale_color_manual(values = my_palette)

```

```R

head(melted_data, 3)

```

```{R}

#Creating catgories based on the variable identifier

categorize <- function(variable_name) {
  if (grepl("American_Cheese", variable_name, ignore.case = TRUE)) {
    return("Cheese")
  } else if (grepl("Other_than_American_Cheese", variable_name, ignore.case = TRUE)) {
    return("Cheese")
  } else if (grepl("Cottage_Cheese", variable_name, ignore.case = TRUE)) {
    return("Cheese")
  } else if (grepl("Dry_Whole_Milk", variable_name, ignore.case = TRUE)) {
    return("Dry_products")
  } else if (grepl("Nonfat_and_Skim_milk_powder", variable_name, ignore.case = TRUE)) {
    return("Dry_products")
  } else if (grepl("Dry_Butter_Milk", variable_name, ignore.case = TRUE)) {
    return("Dry_products")
  } else if (grepl("Dry_Whey_and_Whey_Protein_Concentrate", variable_name, ignore.case = TRUE)) {
    return("Dry_products")
  } else if (grepl("Regular_Ice_Cream", variable_name, ignore.case = TRUE)) {
    return("Frozen_products")
  } else if (grepl("Low_Fat_Ice_Cream", variable_name, ignore.case = TRUE)) {
    return("Frozen_products")
  } else if (grepl("Sherbet", variable_name, ignore.case = TRUE)) {
    return("Frozen_products")
  } else if (grepl("Other_Frozen_Dairy", variable_name, ignore.case = TRUE)) {
    return("Frozen_products")
  } else if (grepl("Water_And_Juices", variable_name, ignore.case = TRUE)) {
    return("Frozen_products")
  } else if (grepl("Whole_Condensed_Milk_Canned", variable_name, ignore.case = TRUE)) {
    return("Evaporated_Condensed_Milk")
  } else if (grepl("Whole_Condensed_Milk_Bulk", variable_name, ignore.case = TRUE)) {
    return("Evaporated_Condensed_Milk")
  } else if (grepl("Skim_Condensed_Milk_Bulk_Canned", variable_name, ignore.case = TRUE)) {
    return("Evaporated_Condensed_Milk")
  } else {
    return("Other")
  }
}


```


```{R}

melted_data$Category <- sapply(melted_data$variable, categorize)

head(melted_data)

```

```{R}

melted_data_categories <- melted_data %>% 
  filter(melted_data$Category != "Other")

ggplot(melted_data_categories, aes(x = Year, y = value, color = variable)) +
  geom_line() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5))+
  facet_wrap(~ Category, scales = "free_y")


```




**More questions are to come as we continue to go through this dataset**
