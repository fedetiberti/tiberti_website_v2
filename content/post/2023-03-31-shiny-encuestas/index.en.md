---
title: "Una Shiny App para visualizar encuestas electorales de Argentina"
author: "Federico Tiberti"
date: "2023-03-31"
slug: "shiny-app-encuestas"
runtime: shiny
categories: R
image:
  caption: ''
  focal_point: ''
  preview_only: yes
tags: R, ggplot
---



Hace un par de semanas, dando vueltas por internet, me encontré con el [Observatorio de Encuestas de La Política Online](http://observatorio.lapoliticaonline.com/presidente). Me pareció una buena idea. Es un producto que es muy frecuente en años electorales en Estados Unidos: un agregador de encuestas electorales, que te muestra algunos simples promedios móviles de la intención de voto de cada partido, algunas líneas de tendencia y, cuando quieren arriesgar un poco, proyecciones o estimaciones de lo que consideran más probable que pase finalmente en la elección, como las famosas agujas del New York Times o los porcentajes de probabilidad de FiveThirtyEight. 

Sin embargo, el de LPO me llamò la atención por la poca cantidad de encuestas que enumera. Solo hay 14 en los últimos 6 meses, cuando en los diarios aparecen una o dos nuevas por semana. Unos días después, un amigo de Twitter me compartió [una página de Wikipedia](https://es.wikipedia.org/wiki/Anexo:Encuestas_de_intenci%C3%B3n_de_voto_para_las_elecciones_presidenciales_de_Argentina_de_2023) donde algún héroe anónimo viene listando muchas más encuestas.

Scrapeé las tablas (quizás deje el código en otro posteo, pero las últimas actualizaciones de [rvest](https://rvest.tidyverse.org/) lo dejaron funcionando _muy_ bien y a prueba de gente que sepa _muy_ poco de html, como es mi caso) y armé una app en Shiny muy sencilla para visualizar las encuestas. La dejo abajo.



<iframe src="https://fedetiberti.shinyapps.io/encuestas_app/?showcase=0" width="672" height="400px" data-external="1"></iframe>

