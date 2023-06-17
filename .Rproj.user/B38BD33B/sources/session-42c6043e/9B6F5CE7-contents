#   Housekeeping
    #   Clear environment
rm(list = ls())
options(scipen = 999)

source("utilities/aesthetics.R") #  Get plot themes
pacman::p_load(dplyr, ggplot2, tidyverse, stringr, tidytext, ggridges, wordcloud2, ggmap, readxl, maps,
               viridis, lubridate, ggstream)


#   Load Data
path <- "data/Covid/"

file <- "Deaths_by_cause.csv"
df_deaths <- read_csv(paste0(path, file))

file <- "owid-covid-data.csv"
df_covid <- read_csv(paste0(path, file))

#   Exploratory analysis
    #   Africa vs other regions
# Aggregate the data
df_covid_continent <- df_covid %>%
    filter(!is.na(continent)) %>%    # remove rows where continent is NA
    group_by(date, continent) %>%
    summarize(
        cases = sum(new_cases_per_million, na.rm = TRUE),
        deaths = sum(new_deaths_per_million, na.rm = TRUE),
        .groups = "drop"
    )

#   Convert data from wide to long format
df_covid_long <- df_covid_continent %>%
    pivot_longer(cols = c(cases, deaths), names_to = "category", values_to = "count")

# Create custom labels for facets
custom_labels <- as_labeller(c(cases = "New Cases (per million)", deaths = "New Deaths (per million)"))

# Create a faceted streamgraph
df_covid_long %>%
    ggplot(aes(x = date, y = count, fill = continent)) +
    geom_stream() +
    scale_fill_manual(values = palette) +
    facet_wrap(~ category, scales = "free", ncol = 1, labeller = custom_labels) +
    th +
    theme(panel.grid.major = element_blank(),
          panel.grid.minor = element_blank(),
          axis.text.x.top = element_blank(),
          axis.text.y = element_blank(),
          axis.title.y = element_blank()) +
    labs(title = "COVID-19 cases and deaths over time by continent",
         x = "Date",
         y = "Count",
         fill = "Continent")


