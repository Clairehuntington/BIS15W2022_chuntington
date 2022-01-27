---
title: "Midterm 1"
author: "Claire Huntington "
date: "2022-01-26"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

This exam is due by 12:00p on Thursday, January 27.  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
## ✓ readr   2.1.1     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

## Questions  
Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  
In this definition for data science, it mentions working with large data sets and being able to extract data and knowledge from it. I feel like I have definitely practiced this throughout our class so far. For example, in our homework assignments we seem to work with pretty large data sets and using functions like dim() or colname() we are able to identify and learn much more about what exactly we are working with. We also use functions like group_by, filter, or summarize to sort through the data and create new data frames as well. 

2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  
All of this is very very new to me and has definitely been a journey where I have learned so much. I am a lot less scared than I was at the beginning and feel like the world of coding is a lot more approachable to me than it used to be. One thing that was very useful that I learned so far is being able to rename some of our items in data frames or data sets we work with. I think the ability to do this and rename objects is and will be useful in the future as well. Something that I personally feel I need more practice with is keeping everything neat, clean, and updated. I often find myself stuck on homework assignments and frustrated that I cannot move on when it is often due to a small mistake or something I missed previously. It has definitely proved important to keep things very neat and organized which I think I can improve on as well. 

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.
I loaded the data using readr::read_csv and used functions glimpse, colnames, and class to learn more about the data. 

```r
elephants <- readr::read_csv("data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
glimpse(elephants)
```

```
## Rows: 288
## Columns: 3
## $ Age    <dbl> 1.40, 17.50, 12.75, 11.17, 12.67, 12.67, 12.25, 12.17, 28.17, 1…
## $ Height <dbl> 120.00, 227.00, 235.00, 210.00, 220.00, 189.00, 225.00, 204.00,…
## $ Sex    <chr> "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M"…
```


```r
colnames(elephants)
```

```
## [1] "Age"    "Height" "Sex"
```


```r
class(elephants$Age)
```

```
## [1] "numeric"
```

```r
class(elephants$Height)
```

```
## [1] "numeric"
```

```r
class(elephants$Sex)
```

```
## [1] "character"
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.


```r
names(elephants)
```

```
## [1] "Age"    "Height" "Sex"
```

```r
elephants <- rename(elephants, age= Age, height= Height, sex=Sex)
```


```r
elephants$sex<-as.factor(elephants$sex)
```


```r
glimpse(elephants)
```

```
## Rows: 288
## Columns: 3
## $ age    <dbl> 1.40, 17.50, 12.75, 11.17, 12.67, 12.67, 12.25, 12.17, 28.17, 1…
## $ height <dbl> 120.00, 227.00, 235.00, 210.00, 220.00, 189.00, 225.00, 204.00,…
## $ sex    <fct> M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, M, …
```

5. (2 points) How many male and female elephants are represented in the data?

```r
elephants%>% 
  filter(sex== "M") 
```

```
## # A tibble: 138 × 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 128 more rows
```
By filtering the data in elephants for the sex to only be male, it gave us a total of 138 rows meaning there are 138 males in this data set. I also double checked with the code below where it confirms 138 males and there are 150 females present. 


```r
table(elephants$sex)
```

```
## 
##   F   M 
## 150 138
```
6. (2 points) What is the average age all elephants in the data?

```r
mean(elephants$age)
```

```
## [1] 10.97132
```
The average age of all the elephants in the data is about 10.97

7. (2 points) How does the average age and height of elephants compare by sex?

```r
male.elephants<- elephants%>% filter(sex=="M")
```


```r
female.elephants<- elephants%>% filter(sex=="F")
```



```r
summarise(elephants, female_age=mean(female.elephants$age), male_age= mean(male.elephants$age))
```

```
## # A tibble: 1 × 2
##   female_age male_age
##        <dbl>    <dbl>
## 1       12.8     8.95
```


```r
summarise(elephants, female_height=mean(female.elephants$height), male_height=mean(male.elephants$height))
```

```
## # A tibble: 1 × 2
##   female_height male_height
##           <dbl>       <dbl>
## 1          190.        185.
```
For age, it seems like the female elephants live longer than the male elephants by about four years. When looking at the height, the female elephants are also taller than the male elephants. 

8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  

```r
male.over.20 <- male.elephants%>% filter(age>20)
female.over.20 <- female.elephants%>% filter(age>20)
```

```r
mean(male.over.20$height)
```

```
## [1] 269.5931
```

```r
mean(female.over.20$height)
```

```
## [1] 232.2014
```
The average height of male elephants over 20 is around 269 which is taller than the average height of female elephants which is about 232. 

```r
max(male.over.20$height)
```

```
## [1] 304.06
```

```r
min(male.over.20$height)
```

```
## [1] 228.69
```
The max of males over twenty is 304 for their height and the min is a height of 228.

```r
max(female.over.20$height)
```

```
## [1] 277.8
```

```r
min(female.over.20$height)
```

```
## [1] 192.54
```
The max height of females over 20 is 277 and the min height is 192. 

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.

```r
gabon_data <- readr::read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
gabon_data$HuntCat <- as.factor(gabon_data$HuntCat)
gabon_data$LandUse <- as.factor(gabon_data$LandUse)
glimpse(gabon_data)
```

```
## Rows: 24
## Columns: 26
## $ TransectID              <dbl> 1, 2, 2, 3, 4, 5, 6, 7, 8, 9, 13, 14, 15, 16, …
## $ Distance                <dbl> 7.14, 17.31, 18.32, 20.85, 15.95, 17.47, 24.06…
## $ HuntCat                 <fct> Moderate, None, None, None, None, None, None, …
## $ NumHouseholds           <dbl> 54, 54, 29, 29, 29, 29, 29, 54, 25, 73, 46, 56…
## $ LandUse                 <fct> Park, Park, Park, Logging, Park, Park, Park, L…
## $ Veg_Rich                <dbl> 16.67, 15.75, 16.88, 12.44, 17.13, 16.50, 14.7…
## $ Veg_Stems               <dbl> 31.20, 37.44, 32.33, 29.39, 36.00, 29.22, 31.2…
## $ Veg_liana               <dbl> 5.78, 13.25, 4.75, 9.78, 13.25, 12.88, 8.38, 8…
## $ Veg_DBH                 <dbl> 49.57, 34.59, 42.82, 36.62, 41.52, 44.07, 51.2…
## $ Veg_Canopy              <dbl> 3.78, 3.75, 3.43, 3.75, 3.88, 2.50, 4.00, 4.00…
## $ Veg_Understory          <dbl> 2.89, 3.88, 3.00, 2.75, 3.25, 3.00, 2.38, 2.71…
## $ RA_Apes                 <dbl> 1.87, 0.00, 4.49, 12.93, 0.00, 2.48, 3.78, 6.1…
## $ RA_Birds                <dbl> 52.66, 52.17, 37.44, 59.29, 52.62, 38.64, 42.6…
## $ RA_Elephant             <dbl> 0.00, 0.86, 1.33, 0.56, 1.00, 0.00, 1.11, 0.43…
## $ RA_Monkeys              <dbl> 38.59, 28.53, 41.82, 19.85, 41.34, 43.29, 46.2…
## $ RA_Rodent               <dbl> 4.22, 6.04, 1.06, 3.66, 2.52, 1.83, 3.10, 1.26…
## $ RA_Ungulate             <dbl> 2.66, 12.41, 13.86, 3.71, 2.53, 13.75, 3.10, 8…
## $ Rich_AllSpecies         <dbl> 22, 20, 22, 19, 20, 22, 23, 19, 19, 19, 21, 22…
## $ Evenness_AllSpecies     <dbl> 0.793, 0.773, 0.740, 0.681, 0.811, 0.786, 0.81…
## $ Diversity_AllSpecies    <dbl> 2.452, 2.314, 2.288, 2.006, 2.431, 2.429, 2.56…
## $ Rich_BirdSpecies        <dbl> 11, 10, 11, 8, 8, 10, 11, 11, 11, 9, 11, 11, 1…
## $ Evenness_BirdSpecies    <dbl> 0.732, 0.704, 0.688, 0.559, 0.799, 0.771, 0.80…
## $ Diversity_BirdSpecies   <dbl> 1.756, 1.620, 1.649, 1.162, 1.660, 1.775, 1.92…
## $ Rich_MammalSpecies      <dbl> 11, 10, 11, 11, 12, 12, 12, 8, 8, 10, 10, 11, …
## $ Evenness_MammalSpecies  <dbl> 0.736, 0.705, 0.650, 0.619, 0.736, 0.694, 0.77…
## $ Diversity_MammalSpecies <dbl> 1.764, 1.624, 1.558, 1.484, 1.829, 1.725, 1.92…
```
10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?


```r
gabon_data %>%
  filter(HuntCat=="High" | HuntCat=="Moderate") %>% 
   select(TransectID, Diversity_BirdSpecies, Diversity_MammalSpecies)%>% 
  summarise(avg_bird_diversity=mean(Diversity_BirdSpecies), avg_mammal_diversity=mean(Diversity_MammalSpecies))
```

```
## # A tibble: 1 × 2
##   avg_bird_diversity avg_mammal_diversity
##                <dbl>                <dbl>
## 1               1.64                 1.71
```
Here we can see that the average bird diversity amongst moderate and high hunting intensity is slightly lower than the average mammal diversity of about 0.07 units. 


11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  


```r
gabon_data%>%
  filter(Distance<3)%>%
  summarise(across(c("RA_Apes","RA_Birds", "RA_Elephant", "RA_Monkeys", "RA_Rodent", "RA_Ungulate")))
```

```
## # A tibble: 2 × 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    0        85.0        0.29       9.09      3.74        1.86
## 2    0.24     68.2        0         25.6       4.05        1.88
```


```r
gabon_data%>%
  filter(Distance>25)%>%
  summarise(across(c("RA_Apes","RA_Birds", "RA_Elephant", "RA_Monkeys", "RA_Rodent", "RA_Ungulate")))
```

```
## # A tibble: 1 × 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    4.91     31.6           0       54.1      1.29        8.12
```
After looking at these data tables I made, it seems there are two transects that are less than 3 km away and one transect that is over 25km away. The relative abundance of apes is much higher in the greater than 25km group. For birds, the relative abundance is much higher when less than 3km away from a village. The elephant relative abundance was quite low for both with a value of 0 greater than 25km away and a high of 0.29 when less than 3 km away. RA of monkeys was higher when greater than 25 km away at a value of 54.12 and when less than 3 km away it was 9.09 and 25.58. RA of rodents was higher when less than 3km away from a village. Lastly, the RA of ungulates was much higher when more than 25km away from a village.

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`


```r
gabon_data%>%
  filter(LandUse=="Park")%>%
  summarise(across(c("Evenness_MammalSpecies", "Evenness_BirdSpecies")))
```

```
## # A tibble: 7 × 2
##   Evenness_MammalSpecies Evenness_BirdSpecies
##                    <dbl>                <dbl>
## 1                  0.736                0.732
## 2                  0.705                0.704
## 3                  0.65                 0.688
## 4                  0.736                0.799
## 5                  0.694                0.771
## 6                  0.776                0.801
## 7                  0.728                0.808
```
Here, I wanted look at comparing the evenness of mammal species and bird species spefically filtering for when the land use was for parks.  
