---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 02-Reading-text-files.md in _episodes_rmd/
title: "Reading text files"
teaching: 0
exercises: 0
questions:
- "What is a data.frame?"
- "How can I read a complete csv file into R?"
- "How can I get basic summary information about my dataset?"
- "How can I change the way R treats strings in my dataset?"
- "Why would I want strings to be treated differently?"
- "How are dates represented in R and how can I change the format?"

objectives:
- "Understand what a data.frame is"
- "Use read.csv to read a csv file into an R data.frame"
- "Examine the structure and contents of a data.frame"
- "Differentiate between a factor and a string"
- "Indicate that R should treat strings as factors or treat factors as strings"
- "Examine and change date formats in R"

keypoints:
- "First key point."
---





## Loading a datafile into the R environment

In most practical scenarios you will want to read data into the R environment from a dataset.

RStudio provides an interface for reading a variety of commonly available data formats produced by other commercial statistical packages such as SPSS and Stata.

We will demonstrate this functionality by importing the SN7577 dataset in both the tab delimited (SN7577.tab) and the SPSS (SN7577_spss.sav) formats.

Full details of the SN7577 dataset are available [here]



The import dataset option is available from the toolbar in the environment tab.

![Import Dataset](../fig/R_02_Import_Dataset_01.png)


There is no option to import a tab delimited file so we choose the csv option.

The wizard guides you through selecting a file and allows you to set or change various characteristics of the data.

In our case although we are using the import csv option the file itself is a tab delimitted dataset so we need to change the seperator character from `,` to `\t`.

Notice how changing this option fixes the display in the preview pane and reveals a nicely formatted table structure.

RStudio performs the import by generating valid R code based on your options and copying the code to the console and running it. You can see the code that it will use in the bottom left pane of the Wizard window.

When you click the import button, the dataset is imported. The code used is copied to to the console window and executed.

To import the tab delimitted version of the SN7577 file the following code was produced and ran


~~~
library(readr)
SN7577_tab <- read_delim("SN7577.tab", "\t", escape_double = FALSE, trim_ws = TRUE)
~~~
{: .language-r}



~~~
Error: 'SN7577.tab' does not exist in current working directory ('/home/francois/git/r-socialsci/_episodes_rmd').
~~~
{: .error}

The `library(readr)` line tells the R environment to import the 'readr' library of functions for use. the `read.delim()` function is part of the 'readr' library, and is a generalised version of the `read_csv()` function. There is also a `read_tsv()` function which we could have used as well.


~~~
SN7577_csv <- read_delim("SN7577.tab", "\t")
~~~
{: .language-r}



~~~
Error: 'SN7577.tab' does not exist in current working directory ('/home/francois/git/r-socialsci/_episodes_rmd').
~~~
{: .error}



~~~
SN7577_csv <- read_tsv("SN7577.tab")
~~~
{: .language-r}



~~~
Error: 'SN7577.tab' does not exist in current working directory ('/home/francois/git/r-socialsci/_episodes_rmd').
~~~
{: .error}

> ## Exercise
>
> Use the import dataset wizard to import the SN7577_spss.sav dataset.
> Notice the different library being used.
> Notice that there are far fewer option to play with
>
> When the data is imported, compare it with the SN7577_tab data.
> Can you find two differences in how the data is shown?
> > ## Solution
> >
> > 1. On the tab file the headers are just the question numbers and on the spss file they include the question itself.
> > 2. On the spss file missing data is denoted as NA, however in the tab version missing data is typically shown as -1.
> >
> {: .solution}
{: .challenge}

For the rest of this episode we will focus only the the SN7577_tab version.

When we imported the dataset the wizard automatically include a `View(SN7577_tab)` line of code. This shows (part of) the contents of the variable as tabular data in a grid in the top pane.

You could also just type the variable name into the console to see the data (or part of it).

If we use the `class()` function to find the type of this cariable, you will see that it appears to have 3 different types.


~~~
class(SN7577_spss)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_spss' not found
~~~
{: .error}

## Data.frames

Data.frames are the de facto data structure for most tabular data, and what we use for statistics and plotting.

A data.frame can be created by hand, but most commonly they are generated by the functions `read.csv()`, `read_delim()`, `read_tsv()`, or `read.table()`; in other words, when importing external datasets into the R environment.

A data.frame is the representation of data in the format of a table, very much as you see in a spreadsheet, where the columns are vectors that all have the same length and are of the same type.

Apart from viewing the data by typing the variable name into the console there are several other functions which can be used to find out information about a data.frame.


~~~
dim(SN7577_tab)        # number of rows and columns
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
nrow(SN7577_tab)       # number of rows
~~~
{: .language-r}



~~~
Error in nrow(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}



~~~
ncol(SN7577_tab)       # number of columns
~~~
{: .language-r}



~~~
Error in ncol(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}



~~~
head(SN7577_tab)       # shows first 6 rows (but truncates the variables)
~~~
{: .language-r}



~~~
Error in head(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}



~~~
tail(SN7577_tab)       # shows last 6 rows (but truncates the variables)
~~~
{: .language-r}



~~~
Error in tail(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}



~~~
names(SN7577_tab)      # lists all of the column names
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
names(SN7577_spss)     # Despite the extra text in the 'View' the column names for the spss variable
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_spss' not found
~~~
{: .error}



~~~
                       # are the same as the csv version
rownames(SN7577_tab)   # list the column names, esentialy index numbers which we don't really need
~~~
{: .language-r}



~~~
Error in rownames(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}



~~~
str(SN7577_tab)        # Show the overall structure of the variable, similar but more complex to what
~~~
{: .language-r}



~~~
Error in str(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}



~~~
                       # what we have seen for other variables.
summary(SN7577_tab)    # displays summary statistics for the different columns.
~~~
{: .language-r}



~~~
Error in summary(SN7577_tab): object 'SN7577_tab' not found
~~~
{: .error}

## Slicing and Dicing a Data.frame

Data.frames are 2-dimensional; we describe them as having rows and columns.

If we want to extract some specific data from a data.frame we need to specify the "coordinates" of the data. We give the row numbers first and then the column numbers. This is the opposite to Excel, where we normally give the column letter and then the row number.

There are a variety of ways of indicating the rows and columns of interest. How you specify this can affect the data type of what is returned.


~~~
SN7577_tab[1, 1]   # 1st column of the 1st row of the data.frame (as a vector)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
SN7577_tab[1, 6]   # the 6th column in 1st row (as a vector)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
SN7577_tab[, 1]    # all of the 1st column values in the data.frame (as a vector)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
SN7577_tab[1]      # all of the 1st column values in the data.frame (as a data.frame)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
SN7577_tab[1:3, 7] # the 7th column from the 1st three rows in the data.frame (as a vector)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}



~~~
SN7577_tab[3, ]    # all of the columns in the 3rd row of the data.frame (as a data.frame)
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'SN7577_tab' not found
~~~
{: .error}

`:` is a special function that creates numeric vectors of integers in increasing
or decreasing order, test `1:10` and `10:1` for instance.

You can also exclude certain parts of a data.frame using the `-` sign:


~~~
SN7577_tab[, -1]          # The whole data.frame, except the first column
SN7577_tab[-c(7:34786), ] # Equivalent to head(surveys)
~~~
{: .language-r}

As well as using numeric values to subset a data.frame (or matrix), columns
can be called by name, using one of the four following notations:


~~~
SN7577_tab["Q2"]       # Result is a data.frame
SN7577_tab[, "Q2"]     # Result is a vector
SN7577_tab[["Q2"]]     # Result is a vector
SN7577_tab$Q2          # Result is a vector
~~~
{: .language-r}

For our purposes, the last three notations are equivalent. If you run the code you will notice differences in the display.
>>>>>>> 9c0d83130e7eab175966f19e2b6cecd3804abea7:_episodes_rmd/02-Reading text files.Rmd

RStudio knows about the columns in your data.frame, so you can take advantage of the auto-completion feature (pressing the "tab" key on your keyboard with only the first few characters entered) to get the full and correct column name


> ## Exercise
>
> 1. Create a data.frame (`SN7577_200`) containing only the observations from
>    row 200 of the `SN7577_tab` dataset.
>
> 2. Notice how `nrow()` gave you the number of rows in a data.frame?
>
>      * Use that number to pull out just that last row in the data.frame.
>      * Compare that with what you see as the last row using `tail()` to make
>        sure it's meeting expectations.
>      * Pull out that last row using `nrow()` instead of the row number.
>      * Create a new data.frame object (`surveys_last`) from that last row.
>
> 3. Use `nrow()` to extract the row that is in the middle of the data
>    frame. Store the content of this row in an object named `SN7577_middle`.
>
> 4. Combine `nrow()` with the `-` notation above to reproduce the behavior of
>    `head(SN7577_tab)` keeping just the first through 6th rows of the SN7577_tab
>    dataset.
>
> > ## Solution
> >
> > SN7577_200 <- SN7577_tab[200, ]
> > SN7577_200
> > SN7577_last <- SN7577_tab[nrow(SN7577_tab), ]
> > SN7577_last
> > SN7577_middle <- SN7577_tab[nrow(SN7577_tab)/2, ]
> > SN7577_middle
> > SN7577_head <- SN7577_tab[-c(7:nrow(SN7577_tab)), ]
> > SN7577_head
> > ```
> >
> {: .solution}
{: .challenge}


## Factors

Factors are used to represent categorical data. Factors can be ordered or unordered, and understanding them is necessary for statistical analysis and for plotting.

Although the mjority of the data in the `SN7577_tab` data.frame are in fact categorical data, it is represented as numerical values. Instead, we will load a copy of our SAFI dataset and use that to discuss factors.


~~~
SAFI_results <- read_csv("SAFI_results.csv")
~~~
{: .language-r}



~~~
Error: 'SAFI_results.csv' does not exist in current working directory ('/home/francois/git/r-socialsci/_episodes_rmd').
~~~
{: .error}

Initially the dataset is loaded without any of the columns designated as factors; all the columns containing text are defined as characters.


~~~
str(SAFI_results$C01_respondent_roof_type)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$C01_respondent_roof_type): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$C02_respondent_wall_type)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$C02_respondent_wall_type): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$C03_respondent_floor_type)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$C03_respondent_floor_type): object 'SAFI_results' not found
~~~
{: .error}

You can see from the output of the `str()` functions that these columns appear to have only a few different string values, suggesting that they are better considered categorical.

We can explicitly change them from characters to factors using the `as.factor()` function.


~~~
SAFI_results$C01_respondent_roof_type <- as.factor(SAFI_results$C01_respondent_roof_type)
~~~
{: .language-r}



~~~
Error in is.factor(x): object 'SAFI_results' not found
~~~
{: .error}



~~~
SAFI_results$C02_respondent_wall_type <- as.factor(SAFI_results$C02_respondent_wall_type)
~~~
{: .language-r}



~~~
Error in is.factor(x): object 'SAFI_results' not found
~~~
{: .error}



~~~
SAFI_results$C03_respondent_floor_type <- as.factor(SAFI_results$C03_respondent_floor_type)
~~~
{: .language-r}



~~~
Error in is.factor(x): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$C01_respondent_roof_type)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$C01_respondent_roof_type): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$C02_respondent_wall_type)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$C02_respondent_wall_type): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$C03_respondent_floor_type)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$C03_respondent_floor_type): object 'SAFI_results' not found
~~~
{: .error}

(If you want to convert a factor into a character string, you can use the `as.character()` function.)

Notice the output of the `str` function. It tells you how many "levels"" (unique values) there are and what they are, and which rows have which level. (This output may be truncated if it is too long to display in the console.)

This last point can be a bit subtle, as all you see is a list of integers. The reason for this is that when the Factors are created, they are stored in alphabetical order and allocated an integer value starting at 1 for the first and so on. It is these integer values that are displayed, one per record, at the end of the `str()` output.

For any factor, apart from using `str()` , you can find out how many levels there are and what they are called, using specific functions:


~~~
nlevels(SAFI_results$C02_respondent_wall_type)
~~~
{: .language-r}



~~~
Error in levels(x): object 'SAFI_results' not found
~~~
{: .error}



~~~
levels(SAFI_results$C02_respondent_wall_type)
~~~
{: .language-r}



~~~
Error in levels(SAFI_results$C02_respondent_wall_type): object 'SAFI_results' not found
~~~
{: .error}

Sometimes, the order of the factors does not matter, other times you might want to specify the order because it is meaningful (e.g., "low", "medium", "high"), it improves your visualization, or it is required by a particular type of analysis. Here, one way to reorder our levels in the `sex` vector would be


~~~
levels(SAFI_results$C02_respondent_wall_type)   # before
~~~
{: .language-r}



~~~
Error in levels(SAFI_results$C02_respondent_wall_type): object 'SAFI_results' not found
~~~
{: .error}



~~~
SAFI_results$C02_respondent_wall_type <- factor(SAFI_results$C02_respondent_wall_type,
                                      levels = c("muddaub", "sunbricks", "burntbricks", "cement"))
~~~
{: .language-r}



~~~
Error in factor(SAFI_results$C02_respondent_wall_type, levels = c("muddaub", : object 'SAFI_results' not found
~~~
{: .error}



~~~
levels(SAFI_results$C02_respondent_wall_type)   # after
~~~
{: .language-r}



~~~
Error in levels(SAFI_results$C02_respondent_wall_type): object 'SAFI_results' not found
~~~
{: .error}

### Plotting factors

When your data is stored as a factor, you can use the `plot()` function to get a quick glance at the number of observations represented by each factor level.


~~~
## bar plot of the different roof types:
plot(SAFI_results$C01_respondent_roof_type)
~~~
{: .language-r}



~~~
Error in plot(SAFI_results$C01_respondent_roof_type): object 'SAFI_results' not found
~~~
{: .error}


The bar chart plot appears in the plots pane. In this case there are the expected 3 bars one for each differnet roof type. Using simple plots like this gives a quick indication of the spread of the data.

The bar chart plot appears in the plots pane. In this case there are the expected 3 bars one for each different roof type. Using simple plots like this gives a quick indication of the distribution of the data.

## Formatting Dates

One of the most common issues that new (and experienced!) R users have is converting date and time information into a variable that is appropriate and usable during analyses. As a reminder from the Excel lesson when we spoke about dates, one good practice for dealing with date data is to ensure that each component of your date is stored as a separate variable.

In the SAFI_results dataset, we have three date fields

A01_interview_date
A04_start
A05_end

If we look at the structure of these fields


~~~
str(SAFI_results$A01_interview_date)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$A01_interview_date): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$A04_start)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$A04_start): object 'SAFI_results' not found
~~~
{: .error}



~~~
str(SAFI_results$A05_end)
~~~
{: .language-r}



~~~
Error in str(SAFI_results$A05_end): object 'SAFI_results' not found
~~~
{: .error}

we can see that the first is a character string and the other two are of a type called 'POSIXct', but they look like stings. As humans we have no difficulty in reading the dates and date/times. To get a computer to read them we need to be a bit more specific about the layout.

However, it is clear that when R imported the SAFI_results datasets, it was able to recognise the last two as date formats.

What we want to do is to extract the various parts of the date and time from these fields and to create seperate fields for the day, month, and year. We will use the `A04_start` column as an example.

To make this job easier, we are going to use the functions provided by a library called 'lubridate'. This library is part of the 'tidyverse' library, so if you have installed 'tidyverse' it will already be available.

Within this library there are a set of appropriately named functions to extract date and time parts.


~~~
year(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in year(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "year"
~~~
{: .error}



~~~
month(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in month(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "month"
~~~
{: .error}



~~~
day(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in day(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "day"
~~~
{: .error}



~~~
hour(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in hour(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "hour"
~~~
{: .error}



~~~
minute(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in minute(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "minute"
~~~
{: .error}



~~~
second(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in second(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "second"
~~~
{: .error}

Although `A04_start` has been recognised as a 'POSIXct' type, we still use the `as.POSIXCT()` function because we need to specify the format that the date field is in.

The tricky part is getting the format string right. The `"%"` character indicates that the next character has special meaning, while the other characters are interpreted literally.

Just looking at the special characters we have used, and knowing that the data are in a date and time format, we can make some guesses as to what special code represents (for example, that `"%Y"` represents a 4-digit year. You can find a comprehennsive list by looking at the help page for `as.POSIXct()` (`?as.POSIXct` in the console).

Having split the components of the date and time, we can add them as new columns to the SAFI_results data.frame.


~~~
SAFI_results$A04_year <- year(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in year(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "year"
~~~
{: .error}



~~~
SAFI_results$A04_month <- month(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in month(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "month"
~~~
{: .error}



~~~
SAFI_results$A04_day <- day(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in day(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "day"
~~~
{: .error}



~~~
SAFI_results$A04_hour <- hour(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in hour(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "hour"
~~~
{: .error}



~~~
SAFI_results$A04_minute <- minute(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in minute(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "minute"
~~~
{: .error}



~~~
SAFI_results$A04_second <- second(as.POSIXct(SAFI_results$A04_start, format="%Y-%m-%d %H:%M:%S"))
~~~
{: .language-r}



~~~
Error in second(as.POSIXct(SAFI_results$A04_start, format = "%Y-%m-%d %H:%M:%S")): could not find function "second"
~~~
{: .error}



~~~
View(SAFI_results)
~~~
{: .language-r}



~~~
Error in as.data.frame(x): object 'SAFI_results' not found
~~~
{: .error}

> ## Exercise
>
> Use appropriate functions from 'lubridate' to add three new columns to the `SAFI_results` data.frame, representing the day, month, and year of the `A01_interview_date` column
>
> > ## Solution
> >
> > 
> > ~~~
> > SAFI_results$A01_year <- year(as.POSIXct(SAFI_results$A01_interview_date,format="%d/%m/%Y"))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > Error in year(as.POSIXct(SAFI_results$A01_interview_date, format = "%d/%m/%Y")): could not find function "year"
> > ~~~
> > {: .error}
> > 
> > 
> > 
> > ~~~
> > SAFI_results$A01_month <- month(as.POSIXct(SAFI_results$A01_interview_date,format="%d/%m/%Y"))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > Error in month(as.POSIXct(SAFI_results$A01_interview_date, format = "%d/%m/%Y")): could not find function "month"
> > ~~~
> > {: .error}
> > 
> > 
> > 
> > ~~~
> > SAFI_results$A01_day <- day(as.POSIXct(SAFI_results$A01_interview_date,format="%d/%m/%Y"))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > Error in day(as.POSIXct(SAFI_results$A01_interview_date, format = "%d/%m/%Y")): could not find function "day"
> > ~~~
> > {: .error}
> >
> {: .solution}
{: .challenge}


If we want to process in the opposite direction; that is combine seperate components into a date format, we can do that as well.

Again using functions from 'lubridate', we can create dates in a variety of formats.



~~~
my_date <- ymd("2018-01-29")
~~~
{: .language-r}



~~~
Error in ymd("2018-01-29"): could not find function "ymd"
~~~
{: .error}



~~~
str(my_date)
~~~
{: .language-r}



~~~
Error in str(my_date): object 'my_date' not found
~~~
{: .error}



~~~
my_date <- dmy("30-01-2018")
~~~
{: .language-r}



~~~
Error in dmy("30-01-2018"): could not find function "dmy"
~~~
{: .error}



~~~
str(my_date)
~~~
{: .language-r}



~~~
Error in str(my_date): object 'my_date' not found
~~~
{: .error}



~~~
my_date <- mdy("01-31-2018")
~~~
{: .language-r}



~~~
Error in mdy("01-31-2018"): could not find function "mdy"
~~~
{: .error}



~~~
str(my_date)
~~~
{: .language-r}



~~~
Error in str(my_date): object 'my_date' not found
~~~
{: .error}

To combine our seperate components together, we can use the `paste()` function. We need to choose the 'lubridate' function which matches the order in which we have combined the individual components. Finally, just to make it interesting, we will increment the date to the following day by adding 1 to it.



~~~
SAFI_results$A01_next_day <-  1 + dmy(paste(SAFI_results$A01_day, SAFI_results$A01_month, SAFI_results$A01_year, sep = '-'))
~~~
{: .language-r}



~~~
Error in dmy(paste(SAFI_results$A01_day, SAFI_results$A01_month, SAFI_results$A01_year, : could not find function "dmy"
~~~
{: .error}