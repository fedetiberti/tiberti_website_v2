---
title: "Plotting equipment losses in the Ukraine War"
author: "Federico Tiberti"
date: "2022-08-25"
slug: "lost-tanks-ukraine"
categories: R
image:
  caption: ''
  focal_point: ''
  preview_only: yes
tags: Scraping, ggplot
---



In office hours, some students wanted to use data from the war in Ukraine for a problem set, so we looked at an interesting source. The [Oryx Project](https://www.oryxspioenkop.com/) uses open source information, like pictures and videos on social media, to rigorously document equipment losses in various conflicts. The data is not provided in a user-friendly format, but [this Github repo](https://github.com/leedrake5/Russia-Ukraine/tree/main/data/byType) publishes the daily updates in csv format. We first create a sequence of dates to automate the dowload of all the spreadsheets and vectorize that download.


```r
lapply(c("tidyverse", "janitor",
         "ggflags", "lubridate", "countrycode"), require, character.only=T)

initial_date <- ymd("2022-02-24")
last_date <- today() - days(1)

data_oryx <- paste0("https://raw.githubusercontent.com/leedrake5/Russia-Ukraine/main/data/byType/", seq(initial_date, last_date, by="days"), ".csv") %>% 
  lapply(read_csv) %>% 
  bind_rows() %>% clean_names()
```

With the data already processed and appended into one single data frame, we can filter for whatever type of equipment we want to. In this case, we will plot just lost tanks.


```r
data_oryx %>% 
  rowwise() %>% 
  mutate(total_lost = destroyed + abandoned + captured + damaged) %>% 
  ungroup() %>% 
  filter(equipment_type == "Tanks") %>% 
  group_by(country) %>% 
  mutate(code = tolower(countrycode(country, 
      origin = "country.name", destination="iso2c")), 
         maxdate=max(date), 
         lost_maxdate = total_lost[date==maxdate]) %>% 
  ggplot(aes(x=date, y=total_lost, color=country))+
  geom_line(show.legend = FALSE, size=0.8) +
  scale_y_continuous(breaks = seq(0, 30000, by=100)) +
  scale_x_date(breaks="1 month", date_labels="%b %Y")+
  geom_flag(aes(x=maxdate, y=lost_maxdate, country=code)) +
  theme_light() +
  labs(x="", y="", title="Tanks lost by Russia and Ukraine since the 2022 Russian Invasion", 
       caption = "Source: Visually confirmed equipment losses documented by Oryx Project") +
  theme(axis.text = element_text(face="bold"), 
        plot.title=element_text(face="bold"))
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-3-1.png" width="672" />


