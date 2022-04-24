---
title: "Using ggiraph for interactive plot in report"
author: "Federico Tiberti"
date: '2022-04-23'
lastMod: '2022-04-23'
slug: ggiraph-interactive-plot
categories: R
tags:
- R Markdown
- plot
- regression
---

For those looking for an alternative to plotly to create vectorized/interactive graphics keeping ggplot syntax: [ggiraph](https://davidgohel.github.io/ggiraph/#:~:text=ggiraph%20is%20a%20tool%20that,when%20used%20in%20shiny%20applications.) seems to be the solution. Brief example below:



```
## [[1]]
## [1] TRUE
## 
## [[2]]
## [1] TRUE
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] TRUE
## 
## [[5]]
## [1] TRUE
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-1-1.png" width="672" />








```r
 vino %>% 
  mutate(log_gdp = log(gdppc), 
         log_wine = log(wine)) %>% 
  ggplot(aes(x=log_gdp, y=wine)) +
 theme_classic() +
  geom_point_interactive(aes(tooltip = country.x, data_id = country.x)) +
  labs(x="Log GDP per capita, PPP, 2019", y="Wine consumption per capita, 2019") +
  theme(axis.text = element_text(face="bold", size=8), 
        axis.title = element_text(face= "bold", size=12), 
        plot.caption = element_text(size=6),
        plot.title = element_text(size=18, face="bold"))
```

```
## Warning: Removed 9 rows containing missing values (geom_interactive_point).
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-2-1.png" width="672" />


