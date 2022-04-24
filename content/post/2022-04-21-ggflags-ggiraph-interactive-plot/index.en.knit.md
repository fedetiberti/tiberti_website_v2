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

For those looking for an alternative to plotly to create vectorized/interactive graphics keeping ggplot syntax: [ggiraph](https://davidgohel.github.io/ggiraph/#:~:text=ggiraph%20is%20a%20tool%20that,when%20used%20in%20shiny%20applications.) seems to be a great option. Brief example below. I downloaded [some data on wine consumption per capita](https://ourworldindata.org/grapher/wine-consumption-per-person) and joined it to data on GDP per capita, using the great [WDI](https://cran.r-project.org/web/packages/WDI/WDI.pdf) package to interact with the World Bank API (inspired by [a tweet by Andres Lopez](https://twitter.com/anlopez1962/status/1517211524615618560?s=20&t=h4b1KpWNbwA3bTkg8q1Jxw)). I use the awesome [ggflags package](https://github.com/jimjam-slam/ggflags) to plot each country with its flag instead of a point.







