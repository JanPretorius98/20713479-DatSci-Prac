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

##  Question 1: Covid
This question has been stored in the folder named `Question-1-Covid`. The following section explains step by step how the questions were answered.

The first important thing to notice is the nature of the data - time-series. This implies that data visualisation techniques must exhibit not just differences between how countries experirenced covid, but also differences within the countries themselves. These changes are best presented with line plots. 

The following plotting techniques are used:
* Streamgraph – Shows changes in values relative to each other. A good way to visualise differences over time.
* Simple line plots – Shows physical values and how they change over time.
* Choropleth maps – Although static, having a few choropleth maps from different t may help to show geographical differences.
* Scatterplots – Help us to relate different variables to each other.

There are some data operations, such as aggregating the covid cases and deaths by continent. I created a cuntion to do this, but this turned out to be much slower than just coding the transformation for specific code chunks.
