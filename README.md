# Assignment 1: due Tuesday, September 15th [(_click here_)](Assignment_1_BRFSS.Rmd)  

---  

## Video Tutorials  
[**Video 1: Introduction to R**](https://vimeo.com/1220660708?fl=ip&fe=ec&share=copy)  
[**Video 2: The Console**](https://vimeo.com/1220660709?fl=ip&fe=ec&share=copy)  
[**Video 3: Vectors**](https://vimeo.com/1220660711?fl=ip&fe=ec&share=copy)  
[**Video 4: Help and Hashes**](https://vimeo.com/1220660710?fl=ip&fe=ec&share=copy)  
[**Video 5: Errors**](https://vimeo.com/1220660719?fl=ip&fe=ec&share=copy)  
[**Video 6: Scripts**](https://vimeo.com/1220660748?fl=ip&fe=ec&share=copy)  
[**Video 7: Packages**](https://vimeo.com/1220660753?fl=ip&fe=ec&share=copy)  
[**Video 8: Working with Data**](https://vimeo.com/1220660760?fl=ip&fe=ec&share=copy)

## Installing R  
View the documentation and install R by clicking [**here.**](https://www.r-project.org/)  

## Installing RStudio
View the documentation and install RStudio by clicking [**here.**](https://posit.co/downloads)  

## A brief introduction to R packages  
Packages are curated collections of functions and/or compiled code for use in R. Some commonly-downloaded, popular packages include sample data and documentation to explain and demonstrate implementation.  
Packages can be downloaded from the Comprehensive R Archive Network (CRAN), the primary repository for R packages. Each package submitted to CRAN is reviewed and tested thoroughly before release. Every package is released with a version number, and the most popular packages are frequently updated and released with a new version number.  

CRAN is a trusted source for up-to-date, consistent versions of R packages, and allows package accessibility across multiple servers in multiple regions called 'mirrors'. Packages can also be downloaded through GitHub, but we'll get to that later.  

View the cheat sheets for `tidyverse` packages by clicking [**here.**](https://rstudio.github.io/cheatsheets/)

## 1. Using `install.packages()`  

One of the most useful packages in R is `tidyverse`.  
The `install.packages()` function is the easiest method to download packages from CRAN.  
View the documentation for `install.packages()` by clicking [**here.**](https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/install.packages)  


## 2. The `library()` function  

Once the package is downloaded, the package must be called into virtual memory before it is used. In order to use the package, call it into virtual memory with the `library()` command.  
When downloading packages, the package name must be in quotation marks. When called into virtual memory with the `library()` command, no quotation marks are needed.  


## 3. Viewing package version with `packageVersion()`  

In an R Markdown document, you can begin a new code chunk by adding three tick marks followed by a lower case r enclosed in curly brackets: ` ```{r} `  

Close the code chunk by typing three tick marks: ` ``` `.  
View the documentation for `packageVersion()` by clicking [**here.**](https://www.rdocumentation.org/packages/Biobase/versions/2.32.0/topics/package.version)  


## 4. Importing a .csv file with `read.csv`  

Hint: include the file path when reading the file, and remember to either double backslashes (`\`) or use forward slashes (`/`) in the file path.  
View the documentation for `read.csv()` by clicking [**here.**](https://www.rdocumentation.org/packages/COVID19/versions/2.0.3/topics/read.csv)  


## 5. The `colnames()` function  

How many columns are in the dataframe?  
View the documentation for `colnames()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/row+colnames)  
View additional methods for retrieving column names and details by clicking [**here.**](https://www.r-bloggers.com/2024/10/mastering-column-names-in-base-r-a-beginners-guide/)  


## 6. Using `sapply()` to view column type  

View the documentation for `sapply()` by clicking [**here.**](https://www.rdocumentation.org/packages/functools/versions/0.2.0/topics/Sapply)  


## 7. The `table()` function  

View the documentation for `table()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/table)  


## 8. Viewing the number of rows with `nrow()`  

View the documentation for `nrow()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/nrow)  

# Assignment 2: due Tuesday, October 13th  

---  

## 1. The BRFSS Codebook: Height  

The Behavioral Risk Factor Surveillance Survey (BRFSS) data in the `brtri` dataframe have a codebook with the following information:  

Label: Reported Height in Feet and Inches  
Section Name: Demographics  

Type of Variable: Num  
Variable Name: HEIGHT3  

Question:  About how tall are you without shoes?  (If respondent answers in metrics, put a 9 in the first column)[Round fractions down.]  

| Value | Value Label | Frequency | Percentage | Weighted Percentage |  
|:------------|:---------------------------------|----------:|-----------:|--------------------:|  
| 200-711 | Height (ft/inches) | | | |  
| | Notes: 0 _ / _ _ = feet / inches | 425,837 | 95.85 | 94.10 |    
| 7777 | Don't know/Not sure | 4,198 | 0.94 | 1.49 |  
| 9061-9998 | Height (meters/centimeters) | | | |  
| | Notes: The initial '9' indicates | | | |  
| | this was a metric value. | 7,793 | 1.75 | 2.91 |    
| 9999 | Refused | 6,442 |        1.45 | 1.50 |  
| BLANK | Not asked or Missing | 13,400 | | |  
  
  
Given the information in the table above, what range of values would you say are in feet and inches in column `HEIGHT3`?  
What range of values would you say are in centimeters?  
View the documentation for `table()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/table)  


## 2. Extracting height: feet, inches  

According to the information in the BRFSS codebook, values from 200 to 711 in the `HEIGHT3` column represent height in feet and inches.  
For example, the value '511' actually represents a height of 5 feet and 11 inches.  
The codebook also explains that values beginning with the number '9' in the `HEIGHT3` column precede digits that represent height recorded in centimeters.  
The number '9' only signifies that the remaining digits are recorded in centimeters and should not be included in the measurement values.  
In order to compare height of each respondent, we will need to convert all height values to inches or centimeters.  

We will accomplish this step by step:
1. Where height is recorded in feet and inches, for example '511', we'11 separate values of feet and values of inches into separate `HEIGHTft` and `HEIGHTin` columns.
2. Where height is measured in centimeters, for example '9170', we will need to extract the last three digits--the values following the leading'9'--and store as values of centimeters in a separate `HEIGHTcm` column.
3. After we have three new columns (`HEIGHTft`, `HEIGHTin`, `HEIGHTcm`), we can convert values conditionally by row until each respondent has height recorded in inches and centimeters.  

You can use Stack Overflow as a resource on conditional methods with logical indexing by clicking [**here.**](https://stackoverflow.com/questions/13871614/replacing-values-from-a-column-using-a-condition-in-r)  
View the documentation for `substr()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/substr)  


## 3. Transforming height: total inches  

Create a new column called `HEIGHTtotin` and populate it with values in total inches using column operations and the new `HEIGHTft` and `HEIGHTin` columns we just created.  
You should be able to create the column and populated it with values in a single line of code.  


## 4. Extracting height: centimeters  

1. Create a new column called `HEIGHTcm` and populate it with `NA` values.  
2. Extract the height of each respondent recorded in centimeters from the `HEIGHT3` column conditionally--only if `brtri$HEIGHT3>=9061 & brtri$HEIGHT3<=9998`.  
3. Use conditional methods with logical indexing and the `substr()` function to populate with the correct digits from the `HEIGHT3` column.
   Remember that the last three digits of the `HEIGHT3` column represent respondent height in centimeters if the leading digit is a '9'.  
5. When subsetting columns, `NA` values are not allowed, so remember to include `!is.na(brtri$HEIGHT3)` in the logical indexing.  


## 5. Transforming height: total centimeters  

1. Create a new column called `HEIGHTtotcm` by simply copying the column `brtri$HEIGHTcm`.
   This new column `HEIGHTtotcm` will hold the height of each respondent in centimeters.
   For rows with height recorded in inches, we will convert from inches to centimeters and populate `HEIGHTtotcm` with converted values.  
2. Use the `round()` function to round to the nearest whole centimeter.  

View the documentation for `round()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/Round)  


## 6. Transforming height: total meters  

1. Create a new column called `HEIGHTtotm` by simply converting the column `brtri$HEIGHTtotcm` to meters.  
2. Use the `round()` function to round values to four decimal places.  


## 7. Transforming height: total centimeters to total inches  

1. Create a new column called `HEIGHTtotin` by simply converting the column `brtri$HEIGHTtotcm` to inches.  
2. Use the `round()` function to round values to the nearest whole inch.  

# Assignment 3: due Tuesday, October 27th  

---  

## 1. Respondent Sex: Creating a factor  

The Behavioral Risk Factor Surveillance Survey (BRFSS) data in the `brtri` dataframe have a codebook with the following information:  

Label: Sex of Respondent  
Section Name: Respondent Sex  

Type of Variable: Num  
Variable Name: SEXVAR  

Question:  Sex of Respondent  

| Value | Value Label | Frequency | Percentage | Weighted Percentage |  
|:------------|:---------------------------------|----------:|-----------:|--------------------:|  
| 1 | Male: Code=1 if LANDSEX3=1 or CELLSEX3=1 | 217,487 | 47.52 | 49.12 |  
| 2 | Female: Code=2 if LANDSEX3=2 or CELLSEX3=2 | 240,183 | 52.48 | 50.88 |  


1. Create a new variable `SEX` and populate it with empty values ("").
2. Use conditional logic and indexing to code the value of `SEX` for all rows where `SEXVAR==1` as 'Male'.  
3. Use conditional logic and indexing to code the value of `SEX` for all rows where `SEXVAR==2` as 'Female'.  
4. Use the `factor()` function to convert `brtri$SEX` to a factor.  

View the documentation for `factor()` by clicking [**here.**](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/factor)  


## 2. Plotting an histogram of (unweighted) height stratified by sex  

View the documentation for `ggplot()` by clicking [**here.**](https://www.rdocumentation.org/packages/ggplot2/versions/0.9.0/topics/ggplot)  
View the documentation for `geom_histogram()` by clicking [**here.**](https://www.rdocumentation.org/packages/ggplot2/versions/0.9.1/topics/geom_histogram)  
View a gallery of R code and histograms with several groups by clicking [**here.**](https://r-graph-gallery.com/histogram_several_group.html)  


## 3. Compare our calculated `HEIGHTtotin` column values to BRFSS height column values in inches  

Use the `head()` function to view the first rows of the `HEIGHTtotin` and `HTIN4` columns in the `brtri` dataframe.  

View the documentation for `head()` by clicking [**here.**](https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/head)  


## 4. Compare our calculated `HEIGHTtotm` column values to BRFSS height column values in meters  

Use the `head()` function to view the first rows of the `HEIGHTtotm` and `HTM4` columns in the `brtri` dataframe.   

# Assignment 4: due Tuesday, November 17th  

---  

## 1. The BRFSS Codebook: Weight  

The Behavioral Risk Factor Surveillance Survey (BRFSS) data in the `brtri` dataframe have a codebook with the following information:  

Label: Reported Weight in Pounds  
Section Name: Demographics  

Type of Variable: Num  
Variable Name: WEIGHT2  

Question:  About how much do you weigh without shoes?  (If respondent answers in metrics, put a 9 in the first column)[Round fractions up.]  

| Value | Value Label | Frequency | Percentage | Weighted Percentage |  
|:------------|:---------------------------------|----------:|-----------:|--------------------:|  
| 50-0776 | Weight (pounds) | | | |  
| | Notes: 0 _  _ _ = weight in pounds | 417,106 | 93.66 | 93.36 |    
| 7777 | Don't know/Not sure | 7,740 | 1.74 | 2.11 |  
| 9023-9352 | Weight (kilograms) | | | |  
| | Notes: The initial '9' indicates | | | |  
| | this was a metric value. | 4,190 | 0.94 | 1.36 |    
| 9999 | Refused | 16,301 |        3.66 | 3.17 |  
| BLANK | Not asked or Missing | 12,333 | | |  


Given the information in the table above, what range of values would you say are in pounds in column `WEIGHT2`?  
What range of values within the column `WEIGHT2` are recorded in kilograms?  


## 2. Extracting weight: pounds  

1. Create a new column called `WEIGHTlb` and populate it with `NA` values.  
2. Extract the weight of each respondent recorded in pounds from the `WEIGHT2` column conditionally--only if `brtri$WEIGHT2>=50 & brtri$WEIGHT2<=776`.  
3. Use conditional methods with logical indexing and the `substr()` function to populate with the correct digits from the `WEIGHT2` column.  
Remember that the last three digits of the `WEIGHT2` column represent respondent weight in kilograms if the leading digit is a '9'.  
4. Convert values to pounds where necessary.  

When subsetting columns, `NA` values are not allowed, so remember to include `!is.na(brtri$WEIGHT2)` in the logical indexing.  


## 3. Extracting weight: kilograms  

1. Create a new column called `WEIGHTkg` and populate it with `NA` values.  
2. Extract the weight of each respondent recorded in kilograms from the `WEIGHT2` column conditionally--only if `brtri$WEIGHT2>=9023 & brtri$WEIGHT2<=9352`.  
3. Use conditional methods with logical indexing and the `substr()` function to populate with the correct digits from the `WEIGHT2` column.  
Remember that the last three digits of the `WEIGHT2` column represent respondent height in centimeters if the leading digit is a '9'.  
4. Convert values to kilograms where necessary.  

When subsetting columns, `NA` values are not allowed, so remember to include `!is.na(brtri$WEIGHT2)` in the logical indexing.  


## 4. Compare our calculated `WEIGHTkg` column values to BRFSS weight column values  

The Behavioral Risk Factor Surveillance Survey (BRFSS) data in the `brtri` dataframe have a codebook with the following information:  

Label: Computed Weight in Kilograms  
Section Name: Calculated Variables  

Type of Variable: Num  
Variable Name: WTKG3  

Question:  Reported weight in kilograms  

| Value | Value Label | Frequency | Percentage | Weighted Percentage |  
|:------------|:---------------------------------|----------:|-----------:|--------------------:|  
| 2300-29500 | Weight in kilograms | | | |
|            | [2 implied decimal places] | | | |
|            | Notes: 0001 <= WEIGHT2 <= 650 | | | |
|            | or 9023 <= WEIGHT2 <= 9295 | | | |
|            | (non-metric WEIGHT2 value divided | | | |  
|            | by 2.2046) | 421,278 | 100.00 | 100.00 |  
| BLANK | 	Don't know/Refused/Not asked or Missing | | | |
|       | Notes: WEIGHT2 = 7777 or 9999 | | | |
|       | or not in accepted values | | | |  
|       | or WEIGHT2 = Missing | 36,392 | | |  


Use the `head()` function to view the first rows of the `WEIGHTlb`, `WEIGHTkg`, and `WTKG3` columns in the `brtri` dataframe.   
Based on what you see, how do the values of the column `WEIGHTkg` compare to the column `WTKG3`?  


## 5. Calculate BMI for each respondent from `WEIGHTkg` and `HEIGHTtotm`  

From respondent weight in kilograms and height in meters, create a new column `BMIall` by calculating BMI in kilograms per meters squared.  


## 6. Compare our calculated `BMIall` column values to BRFSS BMI column values  

The Behavioral Risk Factor Surveillance Survey (BRFSS) data in the `brtri` dataframe have a codebook with the following information:  

Label: Computed body mass index  
Section Name: Calculated Variables  

Type of Variable: Num  
Variable Name: BMI5  

Question:  Body Mass Index (BMI)  

| Value | Value Label | Frequency | Percentage | Weighted Percentage |  
|:------------|:---------------------------------|----------:|-----------:|--------------------:|  
| 1-9999 | 1 or greater | | | |
|            | Notes: WTKG3/(HTM4*HTM4) | | | |
|            | (Has 2 implied decimal places) | 414,633 | 100.00 | 100.00 |  
| BLANK | Don't know/Refused/Missing | | | |
|       | Notes: WTKG3 = 777 or 999 or HTM4 = 777 or 999 | | | |  


Use the `head()` function to view the first rows of the `BMIall` and `BMI5` columns in the `brtri` dataframe.  
Based on what you see, how do the values of the column `BMIall` compare to the column `BMI5`?  

