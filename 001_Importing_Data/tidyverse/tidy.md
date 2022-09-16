---
title: Importing Data with Tidyverse
---


## Table of Contents

- [1. What is Tidyverse?](#what-is-tidyverse)

	- [1.1 How to install Tidyverse?](#how-to-install-tidyverse)

- [2. The ``readr`` Package](#the-readr-package)


- [3. Example Data](#example-data)

- [4. Reading Tab Delimited Files](#reading-tab-delimited-files)

- [5. Comma Delimited Files](#comma-delimited-files)

- [6. Space Delimited Files](#space-delimited-files)

- [7. Reading Files from a Web Address](#reading-files-from-a-web-address)





<br><br><br><br><br><br>
<br><br><br><br><br><br>
<br><br><br><br><br><br>
<br><br><br><br><br><br>



## 1. What is Tidyverse?

Tidyverse is a [family of packages](https://tidyverse.org) envisioned by [Hadley Wickham](https://had.co.nz) who is currently the chief scientist at Rstudio Corp. Following packages are currently available:


<br>
<center>
<img src="tidyverse.png" width=400 />
</center>
<br>


One of these packages, ``readr`` provides functions that offer significant improvements over base-R functions to read files into R's memory. In this section, we will look at some examples that employ these functions.


<br>

### 1.1 How to install Tidyverse?

There are several ways of installing this family of packages. You can, as always install them one by one, but a combined install is also available as follows:


- Installing stable version from CRAN 

```r
install.packages("tidyverse")
```

- Installing latest developmental version from Github

```r
library(devtools)  # if this fails, first install devtools packages

devtools::install_github("hadley/tidyverse")
```

- This will install all 8 packages and their dependencies on your computer.  Make sure you can load them:

```r
library(tidyverse)

── Attaching packages ────────────────────── tidyverse 1.3.1.9000 ──
✔ ggplot2 3.3.4     ✔ purrr   0.3.4
✔ tibble  3.1.2     ✔ dplyr   1.0.7
✔ tidyr   1.1.3     ✔ stringr 1.4.0
✔ readr   1.4.0     ✔ forcats 0.5.1
── Conflicts ─────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
> 
```


<br><Br>

## 2. The ``readr`` Package

This package provides following functions to read rectangular style data (rows and columns):

- ``read_csv()``: comma-separated values (CSV) files
- ``read_tsv()``: tab-separated values (TSV) files
- ``read_delim()``: delimited files (CSV and TSV are important special cases)
- ``read_fwf()``: fixed-width files
- ``read_table()``: whitespace-separated files
- ``read_log()``: web log files


- These names look very similar to their base-r variants (replace ``.`` with ``_``) but they provide additional options and functionality.

- If you are curious about what all options are available in each of these functions, call the help menu:


```r
?read_delim()
```


<br><br>


## 3. Example Data

We need some example data sets to practice using these ``readr`` functions. These data are available in the following location:


```r
setwd("~/EDAwithR/001_Importing_Data/tidyverse/data/")

list.files()

[1] "Acorn_Woodpecker.txt"        "black_walnut.csv"           
[3] "covid_colleges.csv"          "covid_prison_facilities.csv"
[5] "covid_us-counties.csv"       "covid_us-states.csv"        
[7] "mortgage.table"             

```

- You will notice several different file types here e.g. ``.csv``, ``.txt``, and ``.table``. Let's read them using ``readr`` functions.


<br><br>

## 4. Reading Tab Delimited Files


- Let's read in the file that contains data on Acorn Woodpeckers. Make sure that tidyverse is loaded in R's memory


```r
library(tidyverse)

acorn <- read_tsv("Acorn_Woodpecker.txt")

Rows: 1539 Columns: 25                                                                                             
── Column specification ─────────────────────────────────────────────────────
Delimiter: "\t"
chr  (6): State, Genus, Species, Common_Name, Kingdom, Phenophase_Description
dbl (19): Site_ID, Latitude, Longitude, Elevation_in_Meters, Species_ID, Ind...

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

- Note how tidyverse shows column specifications. This data set contains only two types of data:

	- character vectors (``chr``)
	- numbers (``dbl``)

- The output also tells you that using ``spec()`` function will show complete column specification data. Let's try it:

```r
spec(acorn)

cols(
  Site_ID = col_double(),
  Latitude = col_double(),
  Longitude = col_double(),
  Elevation_in_Meters = col_double(),
  State = col_character(),
  Species_ID = col_double(),
  Genus = col_character(),
  Species = col_character(),
  Common_Name = col_character(),
  Kingdom = col_character(),
  Individual_ID = col_double(),
  Phenophase_ID = col_double(),
  Phenophase_Description = col_character(),
  First_Yes_Year = col_double(),
  First_Yes_Month = col_double(),
  First_Yes_Day = col_double(),
  First_Yes_DOY = col_double(),
  First_Yes_Julian_Date = col_double(),
  NumDays_Since_Prior_No = col_double(),
  Last_Yes_Year = col_double(),
  Last_Yes_Month = col_double(),
  Last_Yes_Day = col_double(),
  Last_Yes_DOY = col_double(),
  Last_Yes_Julian_Date = col_double(),
  NumDays_Until_Next_No = col_double()
)
```

- Note the ``acorn`` object we created to hold the contents of this file. Let's call that object from R's memory:


```r
acorn

# A tibble: 1,539 × 25
   Site_ID Latitude Longitude Elevation_in_Meters State Species_ID Genus Species
     <dbl>    <dbl>     <dbl>               <dbl> <chr>      <dbl> <chr> <chr>  
 1   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 2   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 3   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 4   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 5   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 6   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 7   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 8   18465     39.7    -122.                   61 CA          1229 Mela… formic…
 9    9465     34.5    -112.                 1693 AZ          1229 Mela… formic…
10   16442     39.4     -76.6                 120 MD          1229 Mela… formic…
# … with 1,529 more rows, and 17 more variables: Common_Name <chr>,
#   Kingdom <chr>, Individual_ID <dbl>, Phenophase_ID <dbl>,
#   Phenophase_Description <chr>, First_Yes_Year <dbl>, First_Yes_Month <dbl>,
#   First_Yes_Day <dbl>, First_Yes_DOY <dbl>, First_Yes_Julian_Date <dbl>,
#   NumDays_Since_Prior_No <dbl>, Last_Yes_Year <dbl>, Last_Yes_Month <dbl>,
#   Last_Yes_Day <dbl>, Last_Yes_DOY <dbl>, Last_Yes_Julian_Date <dbl>,
#   NumDays_Until_Next_No <dbl>
```

- R says the dataset is now a tibble containing 1539 rows and 25 columns. What is a tibble? It's a method for formatting data frames using tidyverse syntax. You may recall that using base-r, if you called the object, the entire file will be printed to the screen, which is not only inefficient but also annoying. Tidyverse avoids doing that instead printing only first 10 rows and the number of columns allowed by the character width setting of your system.

- Let's change character width of the display

```r
options(width=120)

acorn

# A tibble: 1,539 × 25
   Site_ID Latitude Longitude Elevation_in_Meters State Species_ID Genus      Species  Common_Name Kingdom Individual_ID
     <dbl>    <dbl>     <dbl>               <dbl> <chr>      <dbl> <chr>      <chr>    <chr>       <chr>           <dbl>
 1   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 2   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 3   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 4   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 5   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 6   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 7   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 8   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 9    9465     34.5    -112.                 1693 AZ          1229 Melanerpes formici… acorn wood… Animal…         63480
10   16442     39.4     -76.6                 120 MD          1229 Melanerpes formici… acorn wood… Animal…         64152
```

- Suddenly, we have more columns displayed. You can choose to display even more or all columns using the pipe function:


```r
acorn %>% print(n=14, width=150)

   Site_ID Latitude Longitude Elevation_in_Meters State Species_ID Genus      Species  Common_Name Kingdom Individual_ID
     <dbl>    <dbl>     <dbl>               <dbl> <chr>      <dbl> <chr>      <chr>    <chr>       <chr>           <dbl>
 1   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 2   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 3   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 4   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 5   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 6   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 7   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 8   18465     39.7    -122.                   61 CA          1229 Melanerpes formici… acorn wood… Animal…         72940
 9    9465     34.5    -112.                 1693 AZ          1229 Melanerpes formici… acorn wood… Animal…         63480
10   16442     39.4     -76.6                 120 MD          1229 Melanerpes formici… acorn wood… Animal…         64152
11    6213     34.2    -119.                  304 CA          1229 Melanerpes formici… acorn wood… Animal…         66431
12    6213     34.2    -119.                  304 CA          1229 Melanerpes formici… acorn wood… Animal…         66431
13   17307     35.9    -106.                 2303 NM          1229 Melanerpes formici… acorn wood… Animal…         66541
14   17707     37.4    -122.                   97 CA          1229 Melanerpes formici… acorn wood… Animal…         68607
   Phenophase_ID Phenophase_Description      First_Yes_Year First_Yes_Month First_Yes_Day First_Yes_DOY First_Yes_Julia…
           <dbl> <chr>                                <dbl>           <dbl>         <dbl>         <dbl>            <dbl>
 1           292 Live individuals                      2013              10             3           276          2456569
 2           293 Calls or song (birds)                 2013              10             3           276          2456569
 3           297 Nest building (birds)                 2013              10             3           276          2456569
 4           310 Fruit/seed consumption                2013              12             2           336          2456629
 5           312 Flower visitation                     2013              10             3           276          2456569
 6           446 Feeding                               2013              10            27           300          2456593
 7           457 Insect consumption                    2013              10            27           300          2456593
 8           458 Individuals at a feeding s…           2013              10             3           276          2456569
 9           292 Live individuals                      2014               7             2           183          2456841
10           292 Live individuals                      2014               5             8           128          2456786
11           292 Live individuals                      2014               6             2           153          2456811
12           293 Calls or song (birds)                 2014               6             2           153          2456811
13           292 Live individuals                      2014               3            22            81          2456739
14           292 Live individuals                      2014               4            23           113          2456771
```

<br><br>


## 5. Comma Delimited Files

- Let's read the covid-19 data from New York Times for all USA states (``covid_us-states.csv``)

```r
states <- read_csv("covid_us-states.csv")

Rows: 51302 Columns: 5                                                                                                
── Column specification ────────────────────────────────────────
Delimiter: ","
chr  (2): state, fips
dbl  (2): cases, deaths
date (1): date

ℹ Use `spec()` to retrieve the full column specification for this data.
```

- As in the last example, try the ``spec()`` function:


```r
spec(states)

cols(
  date = col_date(format = ""),
  state = col_character(),
  fips = col_character(),
  cases = col_double(),
  deaths = col_double()
)
```

- Check the tibble

```r
states

# A tibble: 51,302 × 5
   date       state      fips  cases deaths
   <date>     <chr>      <chr> <dbl>  <dbl>
 1 2020-01-21 Washington 53        1      0
 2 2020-01-22 Washington 53        1      0
 3 2020-01-23 Washington 53        1      0
 4 2020-01-24 Illinois   17        1      0
 5 2020-01-24 Washington 53        1      0
 6 2020-01-25 California 06        1      0
 7 2020-01-25 Illinois   17        1      0
 8 2020-01-25 Washington 53        1      0
 9 2020-01-26 Arizona    04        1      0
10 2020-01-26 California 06        2      0
# … with 51,292 more rows
```

- How would you print 20 rows from this tibble?

```r
states %>% print(n=20)

# A tibble: 51,302 × 5
   date       state      fips  cases deaths
   <date>     <chr>      <chr> <dbl>  <dbl>
 1 2020-01-21 Washington 53        1      0
 2 2020-01-22 Washington 53        1      0
 3 2020-01-23 Washington 53        1      0
 4 2020-01-24 Illinois   17        1      0
 5 2020-01-24 Washington 53        1      0
 6 2020-01-25 California 06        1      0
 7 2020-01-25 Illinois   17        1      0
 8 2020-01-25 Washington 53        1      0
 9 2020-01-26 Arizona    04        1      0
10 2020-01-26 California 06        2      0
11 2020-01-26 Illinois   17        1      0
12 2020-01-26 Washington 53        1      0
13 2020-01-27 Arizona    04        1      0
14 2020-01-27 California 06        2      0
15 2020-01-27 Illinois   17        1      0
16 2020-01-27 Washington 53        1      0
17 2020-01-28 Arizona    04        1      0
18 2020-01-28 California 06        2      0
19 2020-01-28 Illinois   17        1      0
20 2020-01-28 Washington 53        1      0
# … with 51,282 more rows
```

- Now try reading one of the remaining csv files in this folder.


<br><br>


## 6. Space Delimited Files

Sometimes you may encounter files with unusual formatting. The file ``black_walnut.table`` is one such example where fields (columns) are separated by one or more space.  We can use the delim function to read it.


```r
walnut <- read_table("black_walnut.table")

── Column specification ──────────────────────────────────────────────────────────────────────────────────────────────────────────
cols(
  .default = col_double(),
  State = col_character(),
  Genus = col_character(),
  Species = col_character(),
  Common_Name = col_character(),
  Kingdom = col_character(),
  Individual_ID = col_character(),
  First_Yes_Year = col_character(),
  First_Yes_Month = col_character(),
  First_Yes_Day = col_character(),
  First_Yes_DOY = col_character(),
  First_Yes_Julian_Date = col_character(),
  NumDays_Since_Prior_No = col_character()
)

```

```r
walnut

# A tibble: 4,113 × 25
   Site_ID Latitude Longitude Elevation_in_Meters State Species_ID Genus   Species Common_Name Kingdom Individual_ID
     <dbl>    <dbl>     <dbl>               <dbl> <chr>      <dbl> <chr>   <chr>   <chr>       <chr>   <chr>        
 1     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 2     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 3     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 4     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 5     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 6     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 7     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 8     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
 9     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae      
10     720     38.5     -77.2                  25 MD            80 Juglans nigra   black       walnut  Plantae 
```

<br><br>

## 7. Reading Files from a Web Address

- Tidyverse makes it extremely easy to read files directly from the web.  Let's go to [https://github.com/nytimes/covid-19-data](https://github.com/nytimes/covid-19-data). In this repo, you will find a file named ``us-counties.csv``. Click on its name and then choose ``view raw``. On the resulting page, copy of the web address of the file. Then use it to read the file with ``read_csv`` function:


```r
counties <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-counties.csv")

Rows: 2502832 Columns: 6                                                                                              
── Column specification ───────────────────────────────────────────────────
Delimiter: ","
chr  (3): county, state, fips
dbl  (2): cases, deaths
date (1): date
```

```r
counties

# A tibble: 2,502,832 × 6
   date       county      state      fips  cases deaths
   <date>     <chr>       <chr>      <chr> <dbl>  <dbl>
 1 2020-01-21 Snohomish   Washington 53061     1      0
 2 2020-01-22 Snohomish   Washington 53061     1      0
 3 2020-01-23 Snohomish   Washington 53061     1      0
 4 2020-01-24 Cook        Illinois   17031     1      0
 5 2020-01-24 Snohomish   Washington 53061     1      0
 6 2020-01-25 Orange      California 06059     1      0
 7 2020-01-25 Cook        Illinois   17031     1      0
 8 2020-01-25 Snohomish   Washington 53061     1      0
 9 2020-01-26 Maricopa    Arizona    04013     1      0
10 2020-01-26 Los Angeles California 06037     1      0
# … with 2,502,822 more rows
```

- You just read a web file with over 2 million rows of data in under 10 seconds. 










































<br><br><br><br><br><br>
<br><br><br><br><br><br>
<br><br><br><br><br><br>
<br><br><br><br><br><br>

