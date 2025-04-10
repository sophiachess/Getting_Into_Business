    # Load necessary libraries
    library(httr)  # For making authenticated requests
    library(utils) # For downloading and unzipping

    # Define the Kaggle dataset URL (Make sure your API token is set up)
    url <- "https://www.kaggle.com/api/v1/datasets/download/fratzcan/usa-house-prices"

    # Define download destination
    destfile <- "./usa-house-prices.zip"

    # Download the file
    download.file(url, destfile, mode = "wb")

    # Extract the ZIP file
    unzip(destfile, exdir = "./usa-house-prices")

    # List the extracted files to check the exact CSV file name
    list.files("./usa-house-prices")

    ## [1] "USA Housing Dataset.csv"

    # Read the CSV file (Replace with the actual extracted filename)
    housing_data <- read.csv("./usa-house-prices/USA Housing Dataset.csv")

# Understanding the Data

## When was the data acquired?

Based on our analysis, the data appears to be from **2014**.
Specifically, all date entries in the dataset follow the `"2014-05-09"`
format. This suggests the dataset represents a **snapshot** of the
housing market from May to July 2014, rather than a **time series
spanning multiple years**.

    # Checking unique dates in the dataset by inspecting the date column
    unique(housing_data$date)

    ##  [1] "2014-05-09 00:00:00" "2014-05-10 00:00:00" "2014-05-11 00:00:00"
    ##  [4] "2014-05-12 00:00:00" "2014-05-13 00:00:00" "2014-05-14 00:00:00"
    ##  [7] "2014-05-15 00:00:00" "2014-05-16 00:00:00" "2014-05-17 00:00:00"
    ## [10] "2014-05-18 00:00:00" "2014-05-19 00:00:00" "2014-05-20 00:00:00"
    ## [13] "2014-05-21 00:00:00" "2014-05-22 00:00:00" "2014-05-23 00:00:00"
    ## [16] "2014-05-24 00:00:00" "2014-05-25 00:00:00" "2014-05-26 00:00:00"
    ## [19] "2014-05-27 00:00:00" "2014-05-28 00:00:00" "2014-05-29 00:00:00"
    ## [22] "2014-05-30 00:00:00" "2014-05-31 00:00:00" "2014-06-01 00:00:00"
    ## [25] "2014-06-02 00:00:00" "2014-06-03 00:00:00" "2014-06-04 00:00:00"
    ## [28] "2014-06-05 00:00:00" "2014-06-06 00:00:00" "2014-06-07 00:00:00"
    ## [31] "2014-06-08 00:00:00" "2014-06-09 00:00:00" "2014-06-10 00:00:00"
    ## [34] "2014-06-11 00:00:00" "2014-06-12 00:00:00" "2014-06-13 00:00:00"
    ## [37] "2014-06-14 00:00:00" "2014-06-15 00:00:00" "2014-06-16 00:00:00"
    ## [40] "2014-06-17 00:00:00" "2014-06-18 00:00:00" "2014-06-19 00:00:00"
    ## [43] "2014-06-20 00:00:00" "2014-06-21 00:00:00" "2014-06-22 00:00:00"
    ## [46] "2014-06-23 00:00:00" "2014-06-24 00:00:00" "2014-06-25 00:00:00"
    ## [49] "2014-06-26 00:00:00" "2014-06-27 00:00:00" "2014-06-28 00:00:00"
    ## [52] "2014-06-29 00:00:00" "2014-06-30 00:00:00" "2014-07-01 00:00:00"
    ## [55] "2014-07-02 00:00:00" "2014-07-03 00:00:00" "2014-07-04 00:00:00"
    ## [58] "2014-07-05 00:00:00" "2014-07-06 00:00:00" "2014-07-07 00:00:00"
    ## [61] "2014-07-08 00:00:00" "2014-07-09 00:00:00" "2014-07-10 00:00:00"
    ## [64] "2014-05-02 00:00:00" "2014-05-08 00:00:00" "2014-05-06 00:00:00"
    ## [67] "2014-05-05 00:00:00" "2014-05-07 00:00:00"

## Where was the data acquired?

The dataset covers housing properties in the state of **Washington
(WA)**, primarily focusing on the **Seattle metropolitan area and
surrounding regions**.

    # Viewing unique city names
    unique(housing_data$city)

    ##  [1] "Seattle"            "Carnation"          "Issaquah"          
    ##  [4] "Maple Valley"       "Kent"               "Redmond"           
    ##  [7] "Clyde Hill"         "Shoreline"          "Mercer Island"     
    ## [10] "Auburn"             "Bellevue"           "Duvall"            
    ## [13] "Renton"             "Sammamish"          "Woodinville"       
    ## [16] "Kirkland"           "Burien"             "Federal Way"       
    ## [19] "Normandy Park"      "Vashon"             "Kenmore"           
    ## [22] "Yarrow Point"       "SeaTac"             "Newcastle"         
    ## [25] "Covington"          "Lake Forest Park"   "Snoqualmie"        
    ## [28] "Des Moines"         "Fall City"          "Ravensdale"        
    ## [31] "Tukwila"            "North Bend"         "Medina"            
    ## [34] "Bothell"            "Enumclaw"           "Snoqualmie Pass"   
    ## [37] "Pacific"            "Black Diamond"      "Beaux Arts Village"
    ## [40] "Algona"             "Preston"            "Milton"            
    ## [43] "Skykomish"

## How was the data acquired?

The dataset does not explicitly state its source, but based on its
structured format and detailed attributes, it appears to be compiled
from: 1. **Real estate transaction records** 2. **Multiple Listing
Service (MLS) data**

## What are the attributes of this dataset?

The date of transaction, sale price, number of bedrooms and bathrooms,
interior square footage, land square footage, number of floors, whether
or not it is a waterfront property, quality of its view (rating),
condition of house (rating), square footage above ground level, square
footage of basement, year house was built, year of last renovation, and
address details including street name, city, state, zip code, and
country.

    # Checking structure of dataset
    str(housing_data)

    ## 'data.frame':    4140 obs. of  18 variables:
    ##  $ date         : chr  "2014-05-09 00:00:00" "2014-05-09 00:00:00" "2014-05-09 00:00:00" "2014-05-09 00:00:00" ...
    ##  $ price        : num  376000 800000 2238888 324000 549900 ...
    ##  $ bedrooms     : num  3 4 5 3 5 3 4 4 3 4 ...
    ##  $ bathrooms    : num  2 3.25 6.5 2.25 2.75 2.5 2 1 2.5 2.5 ...
    ##  $ sqft_living  : int  1340 3540 7270 998 3060 2130 2520 1940 1350 2160 ...
    ##  $ sqft_lot     : int  1384 159430 130017 904 7015 6969 6000 9533 1250 5298 ...
    ##  $ floors       : num  3 2 2 2 1 2 1 1 3 2.5 ...
    ##  $ waterfront   : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ view         : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ condition    : int  3 3 3 3 5 3 3 3 3 4 ...
    ##  $ sqft_above   : int  1340 3540 6420 798 1600 2130 1400 1080 1270 2160 ...
    ##  $ sqft_basement: int  0 0 850 200 1460 0 1120 860 80 0 ...
    ##  $ yr_built     : int  2008 2007 2010 2007 1979 2003 1921 1962 2006 1902 ...
    ##  $ yr_renovated : int  0 0 0 0 0 0 2007 2003 0 0 ...
    ##  $ street       : chr  "9245-9249 Fremont Ave N" "33001 NE 24th St" "7070 270th Pl SE" "820 NW 95th St" ...
    ##  $ city         : chr  "Seattle" "Carnation" "Issaquah" "Seattle" ...
    ##  $ statezip     : chr  "WA 98103" "WA 98014" "WA 98029" "WA 98117" ...
    ##  $ country      : chr  "USA" "USA" "USA" "USA" ...

## What type of data do these attributes hold?

Data Type Attributes **Nominal** (Categorical, Unordered): street, city,
state, zip code, country **Ordinal** (Categorical, Ordered): view,
condition, waterfront **Numerical (Interval)**: None detected
**Numerical (Ratio)**: sale price, num bedrooms, num bathrooms,
sqft\_living, sqft\_lot, num floors, sqft\_above, sqft\_basement,
yr\_built, yr\_renovated, date of transaction

    classify_data_types <- function(df) {
      # Initialize empty lists for each type
      nominal <- c()
      ordinal <- c()
      interval <- c()
      ratio <- c()
      
      for (colname in names(df)) {
        col <- df[[colname]]
        
        # Guessing types
        if (is.character(col) || is.factor(col)) {
          # Factors *might* be ordinal if they have levels with order
          if (is.ordered(col)) {
            ordinal <- c(ordinal, colname)
          } else {
            nominal <- c(nominal, colname)
          }
        } else if (is.numeric(col)) {
          # Assume ratio by default (true zero exists)
          ratio <- c(ratio, colname)
        } else if (inherits(col, "Date") || inherits(col, "POSIXct")) {
          # Dates are often treated as interval or ratio depending on use
          interval <- c(interval, colname)
        } else {
          nominal <- c(nominal, colname)  # fallback
        }
      }
      
      # Create markdown table
      cat("## Data Types of Attributes\n\n")
      cat("| **Data Type** | **Attributes** |\n")
      cat("|---------------|----------------|\n")
      cat(sprintf("| **Nominal** | %s |\n", paste(nominal, collapse = ", ")))
      cat(sprintf("| **Ordinal** | %s |\n", paste(ordinal, collapse = ", ")))
      cat(sprintf("| **Interval** | %s |\n", ifelse(length(interval) > 0, paste(interval, collapse = ", "), "*(None detected)*")))
      cat(sprintf("| **Ratio** | %s |\n", paste(ratio, collapse = ", ")))
    }

    housing_data$view <- factor(housing_data$view, ordered = TRUE)
    housing_data$condition <- factor(housing_data$condition, ordered = TRUE)
    housing_data$waterfront <- factor(housing_data$waterfront)  # If 0/1 or Yes/No

    classify_data_types(housing_data)

    ## ## Data Types of Attributes
    ## 
    ## | **Data Type** | **Attributes** |
    ## |---------------|----------------|
    ## | **Nominal** | date, waterfront, street, city, statezip, country |
    ## | **Ordinal** | view, condition |
    ## | **Interval** | *(None detected)* |
    ## | **Ratio** | price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, sqft_above, sqft_basement, yr_built, yr_renovated |

# Data Summary & Initial Insights

    # View first few rows
    head(housing_data)

    ##                  date   price bedrooms bathrooms sqft_living sqft_lot floors
    ## 1 2014-05-09 00:00:00  376000        3      2.00        1340     1384      3
    ## 2 2014-05-09 00:00:00  800000        4      3.25        3540   159430      2
    ## 3 2014-05-09 00:00:00 2238888        5      6.50        7270   130017      2
    ## 4 2014-05-09 00:00:00  324000        3      2.25         998      904      2
    ## 5 2014-05-10 00:00:00  549900        5      2.75        3060     7015      1
    ## 6 2014-05-10 00:00:00  320000        3      2.50        2130     6969      2
    ##   waterfront view condition sqft_above sqft_basement yr_built yr_renovated
    ## 1          0    0         3       1340             0     2008            0
    ## 2          0    0         3       3540             0     2007            0
    ## 3          0    0         3       6420           850     2010            0
    ## 4          0    0         3        798           200     2007            0
    ## 5          0    0         5       1600          1460     1979            0
    ## 6          0    0         3       2130             0     2003            0
    ##                       street         city statezip country
    ## 1    9245-9249 Fremont Ave N      Seattle WA 98103     USA
    ## 2           33001 NE 24th St    Carnation WA 98014     USA
    ## 3           7070 270th Pl SE     Issaquah WA 98029     USA
    ## 4             820 NW 95th St      Seattle WA 98117     USA
    ## 5          10834 31st Ave SW      Seattle WA 98146     USA
    ## 6 Cedar to Green River Trail Maple Valley WA 98038     USA

    # Load necessary libraries 
    library(tidyverse)

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.4     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

    library(naniar)      # For missing data visualization
    library(ggcorrplot)  # For correlation plots
    library(gridExtra)   # For arranging multiple plots

    ## 
    ## Attaching package: 'gridExtra'
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

    library(scales)      # For formatting labels

    ## 
    ## Attaching package: 'scales'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

    library(knitr)
    library(dplyr)

    # Read the dataset
    # Assuming the CSV file is in the working directory
    housing_data <- read.csv("USA Housing Dataset.csv")

    # 1. Basic Structure and Overview
    # ----------------------------------
    # Display dataset structure
    str(housing_data)

    ## 'data.frame':    4140 obs. of  18 variables:
    ##  $ date         : chr  "2014-05-09 00:00:00" "2014-05-09 00:00:00" "2014-05-09 00:00:00" "2014-05-09 00:00:00" ...
    ##  $ price        : num  376000 800000 2238888 324000 549900 ...
    ##  $ bedrooms     : num  3 4 5 3 5 3 4 4 3 4 ...
    ##  $ bathrooms    : num  2 3.25 6.5 2.25 2.75 2.5 2 1 2.5 2.5 ...
    ##  $ sqft_living  : int  1340 3540 7270 998 3060 2130 2520 1940 1350 2160 ...
    ##  $ sqft_lot     : int  1384 159430 130017 904 7015 6969 6000 9533 1250 5298 ...
    ##  $ floors       : num  3 2 2 2 1 2 1 1 3 2.5 ...
    ##  $ waterfront   : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ view         : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ condition    : int  3 3 3 3 5 3 3 3 3 4 ...
    ##  $ sqft_above   : int  1340 3540 6420 798 1600 2130 1400 1080 1270 2160 ...
    ##  $ sqft_basement: int  0 0 850 200 1460 0 1120 860 80 0 ...
    ##  $ yr_built     : int  2008 2007 2010 2007 1979 2003 1921 1962 2006 1902 ...
    ##  $ yr_renovated : int  0 0 0 0 0 0 2007 2003 0 0 ...
    ##  $ street       : chr  "9245-9249 Fremont Ave N" "33001 NE 24th St" "7070 270th Pl SE" "820 NW 95th St" ...
    ##  $ city         : chr  "Seattle" "Carnation" "Issaquah" "Seattle" ...
    ##  $ statezip     : chr  "WA 98103" "WA 98014" "WA 98029" "WA 98117" ...
    ##  $ country      : chr  "USA" "USA" "USA" "USA" ...

    # Display first few rows
    head(housing_data)

    ##                  date   price bedrooms bathrooms sqft_living sqft_lot floors
    ## 1 2014-05-09 00:00:00  376000        3      2.00        1340     1384      3
    ## 2 2014-05-09 00:00:00  800000        4      3.25        3540   159430      2
    ## 3 2014-05-09 00:00:00 2238888        5      6.50        7270   130017      2
    ## 4 2014-05-09 00:00:00  324000        3      2.25         998      904      2
    ## 5 2014-05-10 00:00:00  549900        5      2.75        3060     7015      1
    ## 6 2014-05-10 00:00:00  320000        3      2.50        2130     6969      2
    ##   waterfront view condition sqft_above sqft_basement yr_built yr_renovated
    ## 1          0    0         3       1340             0     2008            0
    ## 2          0    0         3       3540             0     2007            0
    ## 3          0    0         3       6420           850     2010            0
    ## 4          0    0         3        798           200     2007            0
    ## 5          0    0         5       1600          1460     1979            0
    ## 6          0    0         3       2130             0     2003            0
    ##                       street         city statezip country
    ## 1    9245-9249 Fremont Ave N      Seattle WA 98103     USA
    ## 2           33001 NE 24th St    Carnation WA 98014     USA
    ## 3           7070 270th Pl SE     Issaquah WA 98029     USA
    ## 4             820 NW 95th St      Seattle WA 98117     USA
    ## 5          10834 31st Ave SW      Seattle WA 98146     USA
    ## 6 Cedar to Green River Trail Maple Valley WA 98038     USA

    # Basic dimensions
    cat("Dataset dimensions:", dim(housing_data)[1], "rows and", dim(housing_data)[2], "columns\n")

    ## Dataset dimensions: 4140 rows and 18 columns

    # 2. Summary Statistics
    # ---------------------
    # Numerical variable summaries
    summary(housing_data)

    ##      date               price             bedrooms     bathrooms    
    ##  Length:4140        Min.   :       0   Min.   :0.0   Min.   :0.000  
    ##  Class :character   1st Qu.:  320000   1st Qu.:3.0   1st Qu.:1.750  
    ##  Mode  :character   Median :  460000   Median :3.0   Median :2.250  
    ##                     Mean   :  553063   Mean   :3.4   Mean   :2.163  
    ##                     3rd Qu.:  659125   3rd Qu.:4.0   3rd Qu.:2.500  
    ##                     Max.   :26590000   Max.   :8.0   Max.   :6.750  
    ##   sqft_living       sqft_lot           floors        waterfront      
    ##  Min.   :  370   Min.   :    638   Min.   :1.000   Min.   :0.000000  
    ##  1st Qu.: 1470   1st Qu.:   5000   1st Qu.:1.000   1st Qu.:0.000000  
    ##  Median : 1980   Median :   7676   Median :1.500   Median :0.000000  
    ##  Mean   : 2144   Mean   :  14698   Mean   :1.514   Mean   :0.007488  
    ##  3rd Qu.: 2620   3rd Qu.:  11000   3rd Qu.:2.000   3rd Qu.:0.000000  
    ##  Max.   :10040   Max.   :1074218   Max.   :3.500   Max.   :1.000000  
    ##       view          condition       sqft_above   sqft_basement   
    ##  Min.   :0.0000   Min.   :1.000   Min.   : 370   Min.   :   0.0  
    ##  1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:1190   1st Qu.:   0.0  
    ##  Median :0.0000   Median :3.000   Median :1600   Median :   0.0  
    ##  Mean   :0.2466   Mean   :3.452   Mean   :1831   Mean   : 312.3  
    ##  3rd Qu.:0.0000   3rd Qu.:4.000   3rd Qu.:2310   3rd Qu.: 602.5  
    ##  Max.   :4.0000   Max.   :5.000   Max.   :8020   Max.   :4820.0  
    ##     yr_built     yr_renovated       street              city          
    ##  Min.   :1900   Min.   :   0.0   Length:4140        Length:4140       
    ##  1st Qu.:1951   1st Qu.:   0.0   Class :character   Class :character  
    ##  Median :1976   Median :   0.0   Mode  :character   Mode  :character  
    ##  Mean   :1971   Mean   : 808.4                                        
    ##  3rd Qu.:1997   3rd Qu.:1999.0                                        
    ##  Max.   :2014   Max.   :2014.0                                        
    ##    statezip           country         
    ##  Length:4140        Length:4140       
    ##  Class :character   Class :character  
    ##  Mode  :character   Mode  :character  
    ##                                       
    ##                                       
    ## 

    numerical_summary <- housing_data %>%
      select(price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, 
             waterfront, view, condition, sqft_above, sqft_basement, 
             yr_built, yr_renovated) %>%
      summary()

    print(numerical_summary)

    ##      price             bedrooms     bathrooms      sqft_living   
    ##  Min.   :       0   Min.   :0.0   Min.   :0.000   Min.   :  370  
    ##  1st Qu.:  320000   1st Qu.:3.0   1st Qu.:1.750   1st Qu.: 1470  
    ##  Median :  460000   Median :3.0   Median :2.250   Median : 1980  
    ##  Mean   :  553063   Mean   :3.4   Mean   :2.163   Mean   : 2144  
    ##  3rd Qu.:  659125   3rd Qu.:4.0   3rd Qu.:2.500   3rd Qu.: 2620  
    ##  Max.   :26590000   Max.   :8.0   Max.   :6.750   Max.   :10040  
    ##     sqft_lot           floors        waterfront            view       
    ##  Min.   :    638   Min.   :1.000   Min.   :0.000000   Min.   :0.0000  
    ##  1st Qu.:   5000   1st Qu.:1.000   1st Qu.:0.000000   1st Qu.:0.0000  
    ##  Median :   7676   Median :1.500   Median :0.000000   Median :0.0000  
    ##  Mean   :  14698   Mean   :1.514   Mean   :0.007488   Mean   :0.2466  
    ##  3rd Qu.:  11000   3rd Qu.:2.000   3rd Qu.:0.000000   3rd Qu.:0.0000  
    ##  Max.   :1074218   Max.   :3.500   Max.   :1.000000   Max.   :4.0000  
    ##    condition       sqft_above   sqft_basement       yr_built   
    ##  Min.   :1.000   Min.   : 370   Min.   :   0.0   Min.   :1900  
    ##  1st Qu.:3.000   1st Qu.:1190   1st Qu.:   0.0   1st Qu.:1951  
    ##  Median :3.000   Median :1600   Median :   0.0   Median :1976  
    ##  Mean   :3.452   Mean   :1831   Mean   : 312.3   Mean   :1971  
    ##  3rd Qu.:4.000   3rd Qu.:2310   3rd Qu.: 602.5   3rd Qu.:1997  
    ##  Max.   :5.000   Max.   :8020   Max.   :4820.0   Max.   :2014  
    ##   yr_renovated   
    ##  Min.   :   0.0  
    ##  1st Qu.:   0.0  
    ##  Median :   0.0  
    ##  Mean   : 808.4  
    ##  3rd Qu.:1999.0  
    ##  Max.   :2014.0

    # Summary Statistics for Data Type of the Attributes
    # --- Define variables by data type ---
    nominal_vars <- c("street", "city", "statezip", "country", "waterfront")
    ordinal_vars <- c("view", "condition")
    ratio_vars <- c("price", "bedrooms", "bathrooms", "sqft_living", "sqft_lot",
                    "floors", "sqft_above", "sqft_basement", "yr_built", "yr_renovated")

    # --- Helper function to calculate mode ---
    get_mode <- function(x) {
      ux <- na.omit(unique(x))
      ux[which.max(tabulate(match(x, ux)))]
    }

    # --- Summary for Nominal Variables ---
    nominal_summary <- housing_data %>%
      select(all_of(nominal_vars)) %>%
      summarise(across(everything(),
                       list(
                         Mode = ~as.character(get_mode(.)),
                         Missing = ~as.character(sum(is.na(.)))
                       )))

    # Now pivot — no type mismatch since everything is character
    nominal_summary_long <- nominal_summary %>%
      pivot_longer(
        everything(),
        names_to = c("Variable", ".value"),
        names_sep = "_"
      )

    # Display nicely
    kable(nominal_summary_long, caption = "Summary of Nominal Variables (Mode & Missing Count)")

<table>
<caption>Summary of Nominal Variables (Mode &amp; Missing
Count)</caption>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: left;">Mode</th>
<th style="text-align: left;">Missing</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">street</td>
<td style="text-align: left;">2520 Mulberry Walk NE</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">city</td>
<td style="text-align: left;">Seattle</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">statezip</td>
<td style="text-align: left;">WA 98103</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">country</td>
<td style="text-align: left;">USA</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="odd">
<td style="text-align: left;">waterfront</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
</tr>
</tbody>
</table>

Summary of Nominal Variables (Mode & Missing Count)

    # --- Summary for Ordinal Variables (Frequency counts) ---
    ordinal_summary <- lapply(housing_data[ordinal_vars], function(x) as.data.frame(table(x)))
    names(ordinal_summary) <- ordinal_vars

    # Display each ordinal variable as a separate table
    for (var in names(ordinal_summary)) {
      cat("\n\n")
      cat("### Frequencies for Ordinal Variable:", var, "\n")
      print(kable(ordinal_summary[[var]], col.names = c(var, "Frequency")))
    }

    ## 
    ## 
    ## ### Frequencies for Ordinal Variable: view 
    ## 
    ## 
    ## |view | Frequency|
    ## |:----|---------:|
    ## |0    |      3722|
    ## |1    |        56|
    ## |2    |       186|
    ## |3    |       111|
    ## |4    |        65|
    ## 
    ## 
    ## ### Frequencies for Ordinal Variable: condition 
    ## 
    ## 
    ## |condition | Frequency|
    ## |:---------|---------:|
    ## |1         |         5|
    ## |2         |        27|
    ## |3         |      2596|
    ## |4         |      1114|
    ## |5         |       398|

    # --- Summary for Ratio Variables ---
    ratio_summary <- housing_data %>%
      select(all_of(ratio_vars)) %>%
      summarise(across(everything(),
                       list(
                         Mean = ~round(mean(., na.rm = TRUE), 2),
                         Median = ~median(., na.rm = TRUE),
                         Min = ~min(., na.rm = TRUE),
                         Max = ~max(., na.rm = TRUE),
                         Range = ~max(., na.rm = TRUE) - min(., na.rm = TRUE),
                         SD = ~round(sd(., na.rm = TRUE), 2),
                         Missing = ~sum(is.na(.))
                       ))) %>%
      pivot_longer(everything(),
                   names_to = c("Variable", ".value"),
                   names_sep = "_")

    ## Warning: Expected 2 pieces. Additional pieces discarded in 42 rows [22, 23, 24, 25, 26,
    ## 27, 28, 29, 30, 31, 32, 33, 34, 35, 43, 44, 45, 46, 47, 48, ...].

    kable(ratio_summary, caption = "Summary of Ratio Variables")

<table>
<caption>Summary of Ratio Variables</caption>
<colgroup>
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 3%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 6%" />
<col style="width: 7%" />
<col style="width: 8%" />
<col style="width: 6%" />
<col style="width: 7%" />
<col style="width: 6%" />
<col style="width: 7%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: right;">Mean</th>
<th style="text-align: right;">Median</th>
<th style="text-align: right;">Min</th>
<th style="text-align: right;">Max</th>
<th style="text-align: right;">Range</th>
<th style="text-align: right;">SD</th>
<th style="text-align: right;">Missing</th>
<th style="text-align: right;">living</th>
<th style="text-align: right;">lot</th>
<th style="text-align: right;">above</th>
<th style="text-align: right;">basement</th>
<th style="text-align: right;">built</th>
<th style="text-align: right;">renovated</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">price</td>
<td style="text-align: right;">553062.88</td>
<td style="text-align: right;">4.60e+05</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">2.659e+07</td>
<td style="text-align: right;">2.659e+07</td>
<td style="text-align: right;">583686.45</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">bedrooms</td>
<td style="text-align: right;">3.40</td>
<td style="text-align: right;">3.00e+00</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">8.000e+00</td>
<td style="text-align: right;">8.000e+00</td>
<td style="text-align: right;">0.90</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">bathrooms</td>
<td style="text-align: right;">2.16</td>
<td style="text-align: right;">2.25e+00</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">6.750e+00</td>
<td style="text-align: right;">6.750e+00</td>
<td style="text-align: right;">0.78</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">2143.64</td>
<td style="text-align: right;">14697.64</td>
<td style="text-align: right;">1831.35</td>
<td style="text-align: right;">312.29</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">1980.00</td>
<td style="text-align: right;">7676.00</td>
<td style="text-align: right;">1600.00</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">370.00</td>
<td style="text-align: right;">638.00</td>
<td style="text-align: right;">370.00</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">10040.00</td>
<td style="text-align: right;">1074218.00</td>
<td style="text-align: right;">8020.00</td>
<td style="text-align: right;">4820.00</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">9670.00</td>
<td style="text-align: right;">1073580.00</td>
<td style="text-align: right;">7650.00</td>
<td style="text-align: right;">4820.00</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">957.48</td>
<td style="text-align: right;">35876.84</td>
<td style="text-align: right;">861.38</td>
<td style="text-align: right;">464.35</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">sqft</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">floors</td>
<td style="text-align: right;">1.51</td>
<td style="text-align: right;">1.50e+00</td>
<td style="text-align: right;">1</td>
<td style="text-align: right;">3.500e+00</td>
<td style="text-align: right;">2.500e+00</td>
<td style="text-align: right;">0.53</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">1970.81</td>
<td style="text-align: right;">808.37</td>
</tr>
<tr class="odd">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">1976.00</td>
<td style="text-align: right;">0.00</td>
</tr>
<tr class="even">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">1900.00</td>
<td style="text-align: right;">0.00</td>
</tr>
<tr class="odd">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">2014.00</td>
<td style="text-align: right;">2014.00</td>
</tr>
<tr class="even">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">114.00</td>
<td style="text-align: right;">2014.00</td>
</tr>
<tr class="odd">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">29.81</td>
<td style="text-align: right;">979.38</td>
</tr>
<tr class="even">
<td style="text-align: left;">yr</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">0.00</td>
<td style="text-align: right;">0.00</td>
</tr>
</tbody>
</table>

Summary of Ratio Variables

    # 3. Missing Value Analysis
    # -------------------------
    # Check for missing values
    missing_values <- colSums(is.na(housing_data))
    cat("Missing values per column:\n")

    ## Missing values per column:

    print(missing_values)

    ##          date         price      bedrooms     bathrooms   sqft_living 
    ##             0             0             0             0             0 
    ##      sqft_lot        floors    waterfront          view     condition 
    ##             0             0             0             0             0 
    ##    sqft_above sqft_basement      yr_built  yr_renovated        street 
    ##             0             0             0             0             0 
    ##          city      statezip       country 
    ##             0             0             0

    # Visualize missing data pattern (if there are missing values)
    if(sum(missing_values) > 0) {
      miss_plot <- gg_miss_var(housing_data) + 
        labs(title = "Missing Values by Variable")
      print(miss_plot)
    }

    # 7. Calculate price per square foot
    # ---------------------------------
    housing_data$price_per_sqft <- housing_data$price / housing_data$sqft_living

    # Get the top 10 cities by count
    top_cities <- names(sort(table(housing_data$city), decreasing = TRUE)[1:10])

    # Filter for those cities
    city_data <- housing_data %>%
      filter(city %in% top_cities)

    # Box plot of price per square foot by city
    p11 <- ggplot(city_data, aes(x = reorder(city, price_per_sqft, FUN = median), y = price_per_sqft)) +
      geom_boxplot(fill = "lightblue") +
      scale_y_continuous(labels = scales::dollar_format()) +
      labs(title = "Price per Square Foot by City (Top 10 Cities)", 
           x = "City", 
           y = "Price per Square Foot") +
      theme_minimal() +
      theme(axis.text.x = element_text(angle = 45, hjust = 1))

    print(p11)

![](README_files/figure-markdown_strict/unnamed-chunk-11-1.png)

# Explanation/Findings from the Box Plot

It helps **visualize the distribution of price per square foot** for the
top 10 cities in the dataset. It also compares how housing affordability
varies across different locations.

**Observations:**

1.  There is a clear variability in pricing across cities, with some
    cities showing much higher median prices.
2.  A few cities have wider interquartile ranges and outliers,
    indicating greater pricing diversity within those areas.
3.  Other cities appear more uniform, suggesting consistent pricing per
    square foot.

<!-- -->

    # 8. Correlation Analysis
    # ----------------------
    # Create correlation matrix for numerical variables
    corr_vars <- housing_data %>%
      select(price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, 
             waterfront, view, condition, sqft_above, sqft_basement, yr_built)

    correlation_matrix <- cor(corr_vars, use = "complete.obs")
    print(correlation_matrix)

    ##                    price     bedrooms   bathrooms sqft_living     sqft_lot
    ## price         1.00000000  0.188765142  0.31778537  0.41852804  0.045964114
    ## bedrooms      0.18876514  1.000000000  0.54254861  0.59010981  0.065746672
    ## bathrooms     0.31778537  0.542548608  1.00000000  0.76035347  0.097497448
    ## sqft_living   0.41852804  0.590109813  0.76035347  1.00000000  0.194226060
    ## sqft_lot      0.04596411  0.065746672  0.09749745  0.19422606  1.000000000
    ## floors        0.14318033  0.178908025  0.48746202  0.34512959 -0.001112735
    ## waterfront    0.13140126 -0.001286433  0.08015190  0.12615741  0.019229232
    ## view          0.21755312  0.105511845  0.21059005  0.30809811  0.071264029
    ## condition     0.03032722  0.016502829 -0.12302399 -0.06931461  0.012016272
    ## sqft_above    0.35521393  0.478124189  0.68767943  0.87488138  0.203190003
    ## sqft_basement 0.20406557  0.329862245  0.29217050  0.43905256  0.023567347
    ## yr_built      0.02706675  0.153513567  0.47081384  0.29654499  0.047224097
    ##                     floors   waterfront        view    condition  sqft_above
    ## price          0.143180328  0.131401260  0.21755312  0.030327216  0.35521393
    ## bedrooms       0.178908025 -0.001286433  0.10551184  0.016502829  0.47812419
    ## bathrooms      0.487462017  0.080151904  0.21059005 -0.123023992  0.68767943
    ## sqft_living    0.345129590  0.126157414  0.30809811 -0.069314611  0.87488138
    ## sqft_lot      -0.001112735  0.019229232  0.07126403  0.012016272  0.20319000
    ## floors         1.000000000  0.021278110  0.03060383 -0.275212288  0.52477696
    ## waterfront     0.021278110  1.000000000  0.35923652  0.004027085  0.08107594
    ## view           0.030603835  0.359236521  1.00000000  0.064440140  0.16727035
    ## condition     -0.275212288  0.004027085  0.06444014  1.000000000 -0.18359889
    ## sqft_above     0.524776955  0.081075940  0.16727035 -0.183598893  1.00000000
    ## sqft_basement -0.261825961  0.109736316  0.32500205  0.197656172 -0.05103939
    ## yr_built       0.470138622 -0.031891233 -0.06785850 -0.400394294  0.41652546
    ##               sqft_basement    yr_built
    ## price            0.20406557  0.02706675
    ## bedrooms         0.32986225  0.15351357
    ## bathrooms        0.29217050  0.47081384
    ## sqft_living      0.43905256  0.29654499
    ## sqft_lot         0.02356735  0.04722410
    ## floors          -0.26182596  0.47013862
    ## waterfront       0.10973632 -0.03189123
    ## view             0.32500205 -0.06785850
    ## condition        0.19765617 -0.40039429
    ## sqft_above      -0.05103939  0.41652546
    ## sqft_basement    1.00000000 -0.16119668
    ## yr_built        -0.16119668  1.00000000

    # Visualize correlation matrix
    p12 <- ggcorrplot(correlation_matrix, 
                      hc.order = TRUE, 
                      type = "lower", 
                      lab = TRUE, 
                      lab_size = 3,
                      colors = c("#6D9EC1", "white", "#E46726")) +
      labs(title = "Correlation Matrix of Housing Features")

    print(p12)

![](README_files/figure-markdown_strict/unnamed-chunk-12-1.png)

    # 9. Outlier Detection
    # ------------------
    # Calculate z-scores for price
    housing_data$price_zscore <- (housing_data$price - mean(housing_data$price)) / sd(housing_data$price)

    # Identify outliers (z-score > 3 or < -3)
    price_outliers <- housing_data %>%
      filter(abs(price_zscore) > 3) %>%
      select(price, bedrooms, bathrooms, sqft_living, city, price_zscore) %>%
      arrange(desc(price_zscore))

    cat("Number of price outliers:", nrow(price_outliers), "\n")

    ## Number of price outliers: 26

    print(head(price_outliers, 10))

    ##       price bedrooms bathrooms sqft_living          city price_zscore
    ## 1  26590000        3      2.00        1180          Kent    44.607746
    ## 2  12899000        3      2.50        2190       Seattle    21.151660
    ## 3   7062500        5      4.50       10040      Bellevue    11.152284
    ## 4   4668000        5      6.75        9640 Mercer Island     7.049910
    ## 5   4489000        4      3.00        6430      Bellevue     6.743239
    ## 6   3800000        5      5.50        7050    Clyde Hill     5.562810
    ## 7   3710000        4      3.50        5550        Medina     5.408618
    ## 8   3100000        6      4.25        6980 Mercer Island     4.363536
    ## 9   3000000        4      4.25        4850      Kirkland     4.192212
    ## 10  2888000        5      6.25        8670       Seattle     4.000328

    # 10. Analyze bedrooms to bathrooms ratio
    # -------------------------------------
    housing_data$bed_bath_ratio <- housing_data$bedrooms / housing_data$bathrooms

    p13 <- ggplot(housing_data, aes(x = bed_bath_ratio)) +
      geom_histogram(fill = "purple", color = "black", bins = 30, alpha = 0.7) +
      labs(title = "Distribution of Bedroom to Bathroom Ratio", 
           x = "Bedrooms/Bathrooms Ratio", 
           y = "Count") +
      theme_minimal()

    print(p13)

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-markdown_strict/unnamed-chunk-12-2.png)

    # 11. Summary of Key Findings
    # --------------------------
    cat("\n----- KEY FINDINGS FROM EXPLORATORY DATA ANALYSIS -----\n")

    ## 
    ## ----- KEY FINDINGS FROM EXPLORATORY DATA ANALYSIS -----

    # Calculate and print key metrics
    average_price <- mean(housing_data$price)
    median_price <- median(housing_data$price)
    price_range <- max(housing_data$price) - min(housing_data$price)
    avg_price_per_sqft <- mean(housing_data$price_per_sqft)
    top_price_cities <- housing_data %>%
      group_by(city) %>%
      summarise(avg_price = mean(price),
                count = n()) %>%
      filter(count >= 20) %>%
      arrange(desc(avg_price)) %>%
      head(3)

    cat("Average home price: $", formatC(average_price, format="f", digits=2, big.mark=","), "\n")

    ## Average home price: $ 553,062.88

    cat("Median home price: $", formatC(median_price, format="f", digits=2, big.mark=","), "\n")

    ## Median home price: $ 460,000.00

    cat("Price range: $", formatC(price_range, format="f", digits=2, big.mark=","), "\n")

    ## Price range: $ 26,590,000.00

    cat("Average price per square foot: $", formatC(avg_price_per_sqft, format="f", digits=2), "\n")

    ## Average price per square foot: $ 265.84

    cat("Top 3 most expensive cities (min 20 properties):\n")

    ## Top 3 most expensive cities (min 20 properties):

    print(top_price_cities)

    ## # A tibble: 3 × 3
    ##   city          avg_price count
    ##   <chr>             <dbl> <int>
    ## 1 Mercer Island  1111306.    81
    ## 2 Bellevue        861636.   260
    ## 3 Sammamish       677731.   158

    # Calculate strongest correlations with price
    price_correlations <- correlation_matrix[1, ]
    top_correlated <- sort(abs(price_correlations), decreasing = TRUE)[2:4]
    cat("Strongest correlations with price:\n")

    ## Strongest correlations with price:

    for(i in 1:3) {
      var_name <- names(top_correlated)[i]
      corr_value <- price_correlations[var_name]
      cat(var_name, ": ", round(corr_value, 3), "\n")
    }

    ## sqft_living :  0.419 
    ## sqft_above :  0.355 
    ## bathrooms :  0.318

    # Print dataset quality assessment
    cat("\nDataset Quality Assessment:\n")

    ## 
    ## Dataset Quality Assessment:

    cat("- Missing values: ", if(sum(missing_values) == 0) "None" else sum(missing_values), "\n")

    ## - Missing values:  None

    cat("- Detected outliers: ", nrow(price_outliers), "\n")

    ## - Detected outliers:  26

    cat("- Most common property type: ", 
        names(which.max(table(housing_data$bedrooms))), 
        "-bedroom homes (", 
        round(max(table(housing_data$bedrooms))/nrow(housing_data)*100, 1), 
        "%)\n", sep="")

    ## - Most common property type: 3-bedroom homes (44.3%)

# Expanding Investment Knowledge

## Additional Data Source: House Price Index (HPI)

Beyond the USA Housing Dataset, incorporating additional data sources
can significantly enhance investment decision-making. One such dataset
is the **All-Transactions House Price Index (HPI)** for
Washington-Arlington-Alexandria, provided by the **Federal Reserve
Economic Data (FRED)**:

**Dataset Link:** [FRED HPI -
Washington-Arlington-Alexandria](https://fred.stlouisfed.org/series/ATNHPIUS47894Q)

------------------------------------------------------------------------

## Why is this dataset useful?

This dataset is valuable because it provides **macroeconomic context**
for real estate trends. Key benefits include:

1.  **Forward-looking indicators** – Helps predict housing market trends
    based on historical price movements.
2.  **Regional economic health assessment** – A rising index may
    indicate a strong local economy, while a declining index may suggest
    potential risks.
3.  **Long-term trends analysis** – Unlike transaction-based datasets,
    this allows for a broader understanding of **housing appreciation**
    over time.

## How does this dataset complement our current data analysis?

While the **USA Housing Dataset** focuses on **individual property
characteristics and sales prices**, the **HPI dataset** provides a
**time-series perspective**, allowing us to:

1.  **Identify market cycles** – Recognize housing booms and downturns
    to optimize investment timing.
2.  **Assess neighborhood growth potential** – Determine which areas are
    experiencing sustained property value appreciation.
3.  **Perform risk assessment** – Compare micro-level data (individual
    home sales) with macroeconomic trends to mitigate investment risks.

------------------------------------------------------------------------

## Integrating the HPI dataset in R

We can retrieve this dataset directly from FRED using the `quantmod`
package in R:

    # Load necessary package
    library(quantmod)

    ## Loading required package: xts

    ## Loading required package: zoo

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

    ## 
    ## ######################### Warning from 'xts' package ##########################
    ## #                                                                             #
    ## # The dplyr lag() function breaks how base R's lag() function is supposed to  #
    ## # work, which breaks lag(my_xts). Calls to lag(my_xts) that you type or       #
    ## # source() into this session won't work correctly.                            #
    ## #                                                                             #
    ## # Use stats::lag() to make sure you're not using dplyr::lag(), or you can add #
    ## # conflictRules('dplyr', exclude = 'lag') to your .Rprofile to stop           #
    ## # dplyr from breaking base R's lag() function.                                #
    ## #                                                                             #
    ## # Code in packages is not affected. It's protected by R's namespace mechanism #
    ## # Set `options(xts.warn_dplyr_breaks_lag = FALSE)` to suppress this warning.  #
    ## #                                                                             #
    ## ###############################################################################

    ## 
    ## Attaching package: 'xts'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     first, last

    ## Loading required package: TTR

    ## Registered S3 method overwritten by 'quantmod':
    ##   method            from
    ##   as.zoo.data.frame zoo

    # Retrieve the HPI data from FRED
    getSymbols("ATNHPIUS47894Q", src = "FRED")

    ## [1] "ATNHPIUS47894Q"

    # View the first few rows
    head(ATNHPIUS47894Q)

    ##            ATNHPIUS47894Q
    ## 1975-07-01          31.52
    ## 1975-10-01          31.05
    ## 1976-01-01          31.14
    ## 1976-04-01          32.41
    ## 1976-07-01          33.42
    ## 1976-10-01          33.19

    # Plot the data to visualize trends
    plot(ATNHPIUS47894Q, 
         main = "All-Transactions House Price Index (Washington-Arlington-Alexandria)",
         col = "blue", lwd = 2,
         ylab = "HPI", xlab = "Year")

## ![](README_files/figure-markdown_strict/unnamed-chunk-13-1.png)

## Why is this plot important?

It shows the **All-Transactions House Price Index (HPI)** for the
Washington-Arlington-Alexandria region over time.

This visualization helps understand how housing prices have changed in
this metropolitan area.

**Observations:** 1. There is a steady increase in housing prices over
the past few decades, especially after the 2012 recovery 2. There is a
noticeable dip around 2008–2010, aligning with the U.S. housing market
crash during the financial crisis 3. There is a recent rapid growth in
prices, likely reflecting the pandemic-era housing demand surge and
market inflation

------------------------------------------------------------------------
