# 20713479-DatSci-Prac
Repository for Data Science 871 Practical Test. The repository is intended to house all code, figures, tables, and write-ups for the Data Science 871 module. There are five questions in total, with each question in its own folder.

I also created a folder named `utilities` that contains some global scripts, such as `aesthetics.R` which defines a set of plot themes and palettes to ensure consistency across plot aesthetics.

##  Libraries/Packages Required
* `tidyverse` (including `ggplot2`, `dplyr`, `tidytext`, `magrittr`, `stringr`)
* `texevier`
* `readxl`
* `pacman`
* `ggridges`
* `maps`
* `lubridate`
* `ggstream`
* `modelsummary`
* `gt`
* `knitr`
* `ggrepel`
* `zoo`
* `rnaturalearth`
* `rnaturalearthdata`
* `sf`
* `lwgeom`

##  Question 1: Covid
This question has been stored in the folder named `question-1-covid`. The following section explains step by step how the questions were answered. 

### The folllowing questions guide the analysis:
The first important thing to notice is the nature of the data - time-series. This implies that data visualisation techniques must exhibit not just differences between how countries experienced covid, but also differences within the countries themselves.
* What are the larger trends in covid cases and deaths?
  * Streamgraphs and lineplots
* What are the differences in cases and death trends by continent?
  * Geospatial analysis with choropleth maps; proportion of deaths to cases
* Why do African countries have so few reported cases and deaths as compared to other regions?
 * Line plot of total tests and positivity rates.
* How do some country level specifics influence the impact of covid?
  * Line plots by quartiles with bubbles.
* How did infrastructure development contribute to the impact relief?
  * Line plots by quartiles.


### Some more on plotting techniques being used:
* Streamgraph – Shows changes in values relative to each other. A good way to visualise differences over time.
* Simple line plots – Shows physical values and how they change over time.
* Choropleth maps – Although static, having a few choropleth maps from different t may help to show geographical differences.

### Pitfalls along the way:
There are some data operations, such as aggregating the covid cases and deaths by continent. I created a function to do this, but this turned out to be much slower than just coding the transformation for specific code chunks.
When calculating totals per hunderd/thousand/million by continent, I calculated it by summing the amount for each continent and dividing that by the population for the continent and then dividing by hunder/thousand/million. There are some columns that measure this, but as soon as these are summed by continent, you do not get true totals per hundred.
Kable was given me several issues with printing a table, and I was unable to rectify the issue. I then opted to use the `gt` package to create a table. 

## Question 2: London Weather
This question has been stored in the folder named `question-2-londonWeather`. The following section explains step by step how the questions were answered.

### Small data operations performed:
* Format the dates in the data.

### The following questions guide the analysis:
The plan is to create some quirky, but visually appealing graphs.
* What is the temperature usually like in London?
  * Create a colour gradient ridgeline plot
* What is the weather like?
  * Create a raincloud plot (basically a violin plot) to visualise rainfall
  * Create an area plot to show sunshine and cloud coverage
* Compare Cpt temperature and rainfall with London
  * Line plots

### Some pitfalls along the way:
The London data set contains basically the same information as the detailed set. Unfortunately, some of the variables, like hours of sunshine, wind, and fog, were not present in the data. As far as I could see, detailed data for weather on Cape town is blocked by paywalls. In this regard, I compiled a small monthly aggregate data set for Cape Town temperatures and rainfall.

## Question 3: Coldplay vs Metallica
This question has been stored in the folder named `question-3-MusicTaste`. The following section explains step by step how the questions were answered.

### Data operations completed:
* Filter data for studio albums
  * I used some string operations to acheive this.
* Merge Metallica and Coldplay data.
* Merge Spotify Data
* Many observations in `duration` are missing. I created the function `convert_duration()` to deal with this. It uses data from another column, `duration_ms`, to calculate missing values.
* Remove observations from the data that contain the words "Live", "Remix", and "Remastered", to compare original songs with one another.

### The following questions guide the analysis:
First, let's take look at the data as a whole.
* How did the artist evolve over time?
  * Create a Streamgraph to present this.
  * A summary statistics table also included.
* How did the albums produced by the evolve?
  * Boxplots
  * Summary statistics
* What trends are there in the characteristics of the music?
  * Scatterplots with trend lines.
* How do the artists' live performances differ from their studio music?
  * Violin plots

### Functions created:
I created multiple functions for this analysis. Here is a short summary of what they do:
* `convert_duration`: This function checks the duration of a song and converts it to seconds if the duration is missing (NA) but the duration in milliseconds is available. It takes two arguments, duration and duration_ms, and returns the converted duration in seconds.

* `contains_filter_word`: This function checks if a song name contains any of the specified filter words. It takes a song name as an argument and returns TRUE if any of the filter words are found, otherwise FALSE.

* `calculate_days_since_first_release`: This function calculates the number of days since the first release for each artist in the dataset. It arranges the data by artist and release date, groups it by artist, and adds two new columns: first_release_date (the earliest release date for the artist) and days_since_first_release (the number of days since the first release). The function returns the updated dataset.

* `is_live_version`: This function checks if a song name contains the word "Live" (case-insensitive). It takes a song name as an argument and returns TRUE if the word "Live" is found, otherwise FALSE.

## Question 4: Netflix
This question has been stored in the folder named `question-4-Netflix`. The following section explains step by step how the questions were answered.

### Data operations completed:
* Determine main genres from `df_titles` by taking the first genre mentioned.
* Calculate audience score by genre.
* Calculate mean profitability by genre.

### The following questions guide the analysis:
* What Genres do Netlix host the most?
  * Bar plot showing number of titles
  * With `df_titles`
* What genres have favourable audience scores?
  * Another bar plot, but with `df_movies`
* What genres are the most profitable?
  * Create a table with `df_movies`

## Question 5: Google Play
This question has been stored in the folder named `question-5-googlePlay`. The following section explains step by step how the questions were answered.

### Data operations completed:
* Data Cleaning: The datasets, df_reviews and df_app, were cleaned to ensure data integrity. Duplicate rows were removed, irrelevant columns were dropped, and missing values were handled.

* Column Formatting: The 'Last Updated' column in the df_app dataset was converted to a date format. The 'Installs' and 'Price' columns were cleaned by removing non-numeric characters and converting them to numeric. The 'Size' column was cleaned by removing 'M' and converting kilobytes (k) to megabytes (MB).

### The following questions guide the analysis:
* Which app categories are the most profitable?
  * The profitability of app categories was determined by calculating the mean total revenue for each category. The 'Price' and 'Installs' columns were multiplied to obtain the total revenue. The categories were then ordered based on total revenue, and a lollipop plot was created to visualize the profitability.

* What are the average app sizes by category?
  * The average app size for each category was calculated by taking the mean of the 'Size' column within each category. The results were sorted in descending order of average app size, and a table was created to display the average app size and mean total revenue by category.
