---
title: "¿Está sobreestimada la población de La Matanza?"
author: "Federico Tiberti"
date: '2022-04-22'
slug: poblacion-la-matanza
categories: R
image:
  caption: ''
  focal_point: ''
  preview_only: yes
tags:
- La Matanza
- plot
- regression
---

Este post sintetiza algunos datos que compartimos con [Mauro Infantino](www.covidstats.com.ar) en una serie de hilos de Twitter ([este](https://twitter.com/plenque/status/1508414515372822535), [este](https://twitter.com/plenque/status/1513576305295564800) y [este](https://twitter.com/plenque/status/1526702449897111553?s=20&t=kP5nU-dn_pTOI_RABfwZfQ)) Desde que le dedicamos algo de tiempo a mirar las estadísticas de la pandemia, los resultados de La Matanza nos resultaron llamativos. La mortalidad por covid-19 en La Matanza, estandarizada por edades (es decir, ajustada para tener en cuenta las diferencias en la composición etaria por departamento en el último censo), es baja comparada con municipios de nivel de pobreza similar.

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-1-1.png" width="672" />


Si bien es posible que sea un caso de éxito en la gestión de la pandemia y que eso explique la divergencia positiva que muestra en mortalidad respecto de partidos de nivel socioeconómico similar, cuando a los datos de casos y fallecimientos se sumaron los datos de vacunación, la divergencia de La Matanza se hizo más llamativa. La vacunación llegó a cubrir a un porcentaje de la población muy bajo en comparación con municipios vecinos.


<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-2-1.png" width="672" />

Encontramos un desvīo similar mirando otro dato publicado durante la pandemia: el número de beneficiarios del Ingreso Familiar de Emergencia (IFE) por municipio. Cruzando beneficiarios de IFE cada 100 habitantes con la tasa de pobreza crónica por municipio, se ve una relación positiva. Previsiblemente, municipios con mayor pobreza crónica tuvieron un mayor porcentaje de su población como beneficiarios de IFE que municipios de baja pobreza. La Matanza, sin embargo, se desvía mucho en esa relación, con un porcentaje de población beneficiaria de IFE similar al de municipios de mucho menor pobreza crónica, como Morón o San Isidro.


<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-3-1.png" width="672" />

Ante la anomalía de La Matanza, que muestra baja mortalidad como porcentaje de la población, bajo nivel de vacunación como porcentaje de la población y bajo número de beneficiarios de IFE como porcentaje de la población para lo que es su nivel de pobreza, se nos ocurrió mirar si el problema, en vez de en los datos de la pandemia que se usan como numerador en estas proporciones, estaba en realidad en el denominador: el dato de población.

Para los años en que hay censos, el dato de población es el que surge de ellos. Para los demás, se usan las proyecciones de población que hace INDEC. La población proyectada de cada partido se calcula con base en el censo previo incorporando datos estimados (natalidad, mortalidad, migraciones) para cada año. Entonces, por ejemplo, el censo 2010 dio origen a las proyecciones hasta 2019. Ya con eso vimos un salto particular en 2010.

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-4-1.png" width="672" />


Para comprobar la verosimilitud de estos saltos en el ritmo de crecimiento de la población de La Matanza, se nos ocurrió mirar otros datos, no generados por los censos de INDEC ni las proyecciones resultantes de ellos, pero que deberían estar fuertemente correlacionados con la cantidad de habitantes. El primero que miramos fue el número de electores habilitados para votar en cada elección. Este dato se genera a partir de los padrones de la Cámara Nacional Electoral y son independientes de la información censal. A diferencia del dato de población que surge de los censos, la evolución del número de electores en La Matanza muestra un aumento más suave, sin saltos bruscos.


<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-5-1.png" width="672" />


Esto nos llevó a pensar en una relación entre ambas variables, y mirar cómo cambia con el tiempo el nuu4úmero de electores cada 100 habitantes. Como se trata de una población que "envejece", y hubo además una reforma electoral amplió el derecho al voto para incluir a los mayores de 16 años, es esperable que los electores cada vez representen un porcentaje mayor de la población. Sin embargo, en el año 2010 se produce un quiebre importante a la baja, por el salto en la población estimada a partir del censo de ese año que mostramos más arriba.


<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-6-1.png" width="672" />

Para ver si ese salto brusco era común a todos los partidos tras el censo de 2010 o el resultado de algo específico del partido de La Matanza, incluimos en el gráfico al resto de los municipios del conurbano. Se ve que la anomalía es exclusiva de La Matanza: el ratio de electores cada 100 habitantes mantiene su crecimiento suave en todos los municipios en 2010, pero en La Matanza cae bruscamente y se mantiene muy bajo a partir de ese año. Si bien hay algunos cambios mínimos de tendencia temporales en otros partidos, ninguno presenta una irregularidad tan marcada como La Matanza.


<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-7-1.png" width="672" />

Entonces: La Matanza muestra un ratio de electores habilitados cada 100 habitantes en línea con el resto de los municipios del conurbano hasta el año 2010, cuando su ratio cae bruscamente y se aleja de los demás partidos. Si bien esto es consistente con que la población de La Matanza haya sido sobreestimada en el censo 2010 y, en consecuencia, haya permanecido sobreestimada desde entonces, también es teóricamente posible pensar en algún shock demográfico que haya sucedido *únicamente en La Matanza* en 2010, incrementando en un salto discreto la proporción de población no habilitada para votar, por ejemplo, menores de 16 años. En definitiva, los electores habilitados para votar registran a la población adulta, y por eso tienden a subir como proporción de la población cuando esta envejece. Si hubiera habido, *solo en el año 2010 y solo en La Matanza*, un salto muy grande en la proporción de población menor de edad, eso explicaría el resultado anómalo que se ve en el gráfico de arriba.

Para ver si ese era el caso, buscamos otro dato, cuya evolución también debería acompañar a la de la población en general, pero que captura principalmente a la franja menor de edad: la matrícula escolar de los niveles inicial, primario y secundario. Como se ve en el gráfico de abajo, la matrícula en La Matanza crece a partir del año 2012, pero sin ningún salto discreto notable en ningún año.


<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-8-1.png" width="672" />

Como hicimos antes con el dato de electores, pasamos a calcular alumnos matriculados como proporción de la población. Al igual que con los electores registrados, se produce una caída muy fuerte en alumnos matriculados a partir del año 2010.

 
<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-9-1.png" width="672" />

Esto no ocurre del mismo modo en otros partidos del conurbano, que solo muestran cambios suaves antes y después del año 2010.
 
<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-10-1.png" width="672" />
 
 Al igual que con los electores registrados, La Matanza muestra una caída brusca en la matrícula escolar a partir de 2010, que no se replica en ningún otro partido. Esto es un resultado particularmente llamativo si se toma en cuenta el anterior. Si la explicación alternativa a una sobreestimación de la población era que hubiera habido un salto discreto en la población menor de edad en La Matanza en 2010, la explicación alternativa a que haya habido un salto discreto en la población mirando los datos de matrícula escolar es que haya habido un salto discreto en la población adulta. El súbito aparente crecimiento poblacional de La Matanza en 2010 no estuvo acompñado por un aumento semejante ni en alumnos de escuela ni en votantes en elecciones. Se llenó de población ni adulta ni joven. O, lo que suena más probable, se sobreestimó la población en 2010, y tanto electores cada 100 habitantes como alumnos cada 100 habitantes quedaron artificialmente subestimados. 
 
 De hecho, si uno cruza estos dos indicadores para los dos años más cercanos al censo que están disponibles, la mayoría de los municipios muestran una relación negativa. Es intuitivo: municipios con población más envejecida, como Vicente López, tienen muchos electores habilitados cada 100 habitantes, pero pocos alumnos matriculados. Del otro lado, municipios con población muy joven, como Presidente Perón, tienen muchos alumnos cada 100 habitantes, pero pocos electores. La Matanza, sin embargo, se destaca por tener el menor número, tanto de electores como de alumnos matriculados cada 100 habitantes. Tiene, al mismo tiempo, la población más joven y más envejecida. O, más probablemente, un número de población sobreestimado.
 
 
<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-11-1.png" width="672" />
 
 En conclusión, todo parece indicar que la población registrada por el censo del año 2010 fue mayor que la realmente existente en La Matanza. Si bien los datos que analizamos son solo sugestivos y no permiten concluirlo con plena certeza, la sobreestimación en el censo 2010 es la única hipótesis consistente con que se observen, solo en La Matanza y solo en 2010, discontinuidades tan marcadas en variables como electores o alumnos cada 100 habitantes. También explicaría la divergencia que muestra La Matanza en los resultados de la pandemia. No, no tuvo una mortalidad atípicamente baja. No tuvo, tampoco, una población particularmente reticente a vacunarse contra el coronavirus, ni particularmente desinteresada en recibir el Ingreso Familiar de Emergencia. Simplemente su población es menor que la que creíamos. Esperemos contar pronto con los resultados del censo de este año, para tener una mejor noción de un dato tan importante como el de la población de cada distrito.
 
 
 
 
 
 
 
 
 
 
 
 

