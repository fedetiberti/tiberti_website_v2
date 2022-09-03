---
title: "¿Cuántos paquetes necesito para completar el álbum de figuritas de Qatar 2022?"
author: "Federico Tiberti"
date: "2022-08-25"
slug: "probabilidades-album"
categories: R
image:
  caption: ''
  focal_point: ''
  preview_only: yes
tags: Simulations
---

<script src="{{< blogdown/postref >}}index.en_files/twitter-widget/widgets.js"></script>

En estos días tuvo bastante difusión un tuit mío en el que calculaba la cantidad de paquetes necesarios para completar el álbum de figuritas del mundial, suponiendo en distintos escenarios que uno no intercambia figuritas con nadie o que sí lo hace.

<blockquote class="twitter-tweet" data-width="550" data-lang="en" data-dnt="true" data-theme="light"><p lang="es" dir="ltr">Coleccionando solo, se necesitan 1170 paquetes para tener 90% de probabilidad de completar el álbum.<br><br>Coleccionando de a dos (cambiando repetidas con otra persona), se necesitan 745 paquetes.<br><br>De a cinco, se necesitan 450.<br><br>De a diez, 340.<br><br>Hay que intercambiar! <a href="https://t.co/GciOZfd7Rm">https://t.co/GciOZfd7Rm</a> <a href="https://t.co/cIrVOSZ7QQ">pic.twitter.com/cIrVOSZ7QQ</a></p>&mdash; Federico Tiberti (@fedetiberti) <a href="https://twitter.com/fedetiberti/status/1562098816312123394?ref_src=twsrc%5Etfw">August 23, 2022</a></blockquote>

Voy a describir la simulación y mostrar el código que la genera. Primero, es importante aclarar que en esta simulación estoy partiendo de un supuesto clave: no existen las figuritas difíciles. Esto implica que todas las figuritas tienen la misma probabilidad de aparecer en un paquete. Sí, unos cuantos me cuestionaron este supuesto en las respuestas del tuit, pero [Panini afirma que todas las figuritas son fabricadas en las mismas cantidades y no existen algunas más difíciles de encontrar que otras](https://www.losandes.com.ar/mas-deportes/hablo-panini-el-misterio-de-la-figurita-dificil-y-el-metodo-para-completar-el-album-qatar-2022/).

Una característica adicional del proceso aleatorio de muestreo de figuritas en paquetes, que desconozco, es si cada figurita es una selección aleatoria con reemplazo del conjunto total de 638 figuritas, o si es sin reemplazo hasta completar el paquete. Esto es, si una misma figurita puede aparecer más de una vez en un mismo paquete o no. Como no sé la respuesta a esto, voy a hacer las simulaciones suponiendo una cosa u otra.

Para empezar, podemos simular un paquete de figuritas como un muestreo aleatorio de cinco de las 638 figuritas posibles, sin reemplazo.

``` r
sample(1:638, 5, replace = FALSE)
```

    ## [1] 123 460 485 461 187

Podemos simular, digamos, 100 paquetes, de la misma forma:

``` r
paquetes100 <- unlist(lapply(vector("list", 100), 
   function(x) if (length(x) == 0) sample(1:638, 5, replace = FALSE) else x))
paquetes100
```

    ##   [1] 307 137 397 476 435 113 105 284 243 323 217 156  47 482 290  41  27  68
    ##  [19] 314 162 499  20 152 600 432 417  93 179 345 303 515 337 207 335 546 474
    ##  [37]  49 522 141 189 340 309 579 616 224 377 115 348 175 552 230 410 205 211
    ##  [55]  70 251 153 489 344 429  55 592 515 535 370 163 314 235 493 215 234 324
    ##  [73] 555 129 393 557 303 498 247 469  68 564 241 352 254 205 552 241 269 271
    ##  [91] 339 113 109 231 294 184  86 630 132 188 577 540 531  26 520 405 418 609
    ## [109] 262 572 325 239 137 631  41 355 397 557 270 188 142 477 263 616 467 178
    ## [127] 324 518 421 288 638 192  99 490 527   1  23 150 540 244 359  23 385 556
    ## [145] 240 208 190 437 368 429 251 570 407 608 308 228 482 591 385 465 449 276
    ## [163] 258 428 551 265 261 191 507 296 140 581 168 180 236 489 253 439 432 192
    ## [181] 269 622  43  93 227 633 556 224 461  84 236  22  33 317 508  61 486 488
    ## [199] 609   7 481 367 555 226 522 608 244 404 187 401 518 203 252  44 350 184
    ## [217] 124 452 288  89 632 412 236  53  32 170 214 137 610 597 631 409 487 144
    ## [235] 311 199 148 438 209 409 187 372 328 591 490 115  98 532 624 416 488 180
    ## [253] 195 275 456 346 233 522 274 422 387  50 432  14 429 173 184 416 182 322
    ## [271] 230 519  83 600 300 156 368 584  51 230 322 411 594  78 609 217 395 150
    ## [289] 243 444 329 142 527 588 370 583 164 175 579 466 297 321 387 242 113 422
    ## [307] 440 295 338 314 447 325 633 604 368 457  60 623 311 155  59 402 280  78
    ## [325] 606 118 411 540 534 129 502 544 549 146  93 299 233 635 409 605 535 510
    ## [343] 450 585 421 267 274  18 543 169 613 318 327 357 596 376 346 506 276 451
    ## [361] 313 564 408 232 160 522 135 575 151 139 291 341 625 551  17 194 393 286
    ## [379] 147 315 305 396 553  42 503 175  79 369 146 448  78 549 225 537 634 529
    ## [397]  70 134  38 452 317 524 396  40 430 275  87 471 546 407 286 497 600 228
    ## [415] 307  76  94 327  32 369   6 147 470 636 161 584  89 341 120 464 168 485
    ## [433] 222 324 508 242 265 496 233 225   5 318 125 316 524 451  20 554 549 123
    ## [451] 554 421  78 358 312 198 292 242  62 212 612 375  75 289  57 340 114 413
    ## [469] 389   4 180 187 300 244 287 520 625 255 452 127  92 574 115 557 253 209
    ## [487] 586 608 254 498 136  32 557  28 585 627  87 235  44 422

Se puede ver fácilmente que algunos números se repiten. Con la función `table()` podemos ver cuántas veces se repite cada elemento en el vector de números de figuritas:

``` r
paquetes100 %>% table()
```

    ## .
    ##   1   4   5   6   7  14  17  18  20  22  23  26  27  28  32  33  38  40  41  42 
    ##   1   1   1   1   1   1   1   1   2   1   2   1   1   1   3   1   1   1   2   1 
    ##  43  44  47  49  50  51  53  55  57  59  60  61  62  68  70  75  76  78  79  83 
    ##   1   2   1   1   1   1   1   1   1   1   1   1   1   2   2   1   1   4   1   1 
    ##  84  86  87  89  92  93  94  98  99 105 109 113 114 115 118 120 123 124 125 127 
    ##   1   1   2   2   1   3   1   1   1   1   1   3   1   3   1   1   1   1   1   1 
    ## 129 132 134 135 136 137 139 140 141 142 144 146 147 148 150 151 152 153 155 156 
    ##   2   1   1   1   1   3   1   1   1   2   1   2   2   1   2   1   1   1   1   2 
    ## 160 161 162 163 164 168 169 170 173 175 178 179 180 182 184 187 188 189 190 191 
    ##   1   1   1   1   1   2   1   1   1   3   1   1   3   1   3   3   2   1   1   1 
    ## 192 194 195 198 199 203 205 207 208 209 211 212 214 215 217 222 224 225 226 227 
    ##   2   1   1   1   1   1   2   1   1   2   1   1   1   1   2   1   2   2   1   1 
    ## 228 230 231 232 233 234 235 236 239 240 241 242 243 244 247 251 252 253 254 255 
    ##   2   3   1   1   3   1   2   3   1   1   2   3   2   3   1   2   1   2   2   1 
    ## 258 261 262 263 265 267 269 270 271 274 275 276 280 284 286 287 288 289 290 291 
    ##   1   1   1   1   2   1   2   1   1   2   2   2   1   1   2   1   2   1   1   1 
    ## 292 294 295 296 297 299 300 303 305 307 308 309 311 312 313 314 315 316 317 318 
    ##   1   1   1   1   1   1   2   2   1   2   1   1   2   1   1   3   1   1   2   2 
    ## 321 322 323 324 325 327 328 329 335 337 338 339 340 341 344 345 346 348 350 352 
    ##   1   2   1   3   2   2   1   1   1   1   1   1   2   2   1   1   2   1   1   1 
    ## 355 357 358 359 367 368 369 370 372 375 376 377 385 387 389 393 395 396 397 401 
    ##   1   1   1   1   1   3   2   2   1   1   1   1   2   2   1   2   1   2   2   1 
    ## 402 404 405 407 408 409 410 411 412 413 416 417 418 421 422 428 429 430 432 435 
    ##   1   1   1   2   1   3   1   2   1   1   2   1   1   3   3   1   3   1   3   1 
    ## 437 438 439 440 444 447 448 449 450 451 452 456 457 461 464 465 466 467 469 470 
    ##   1   1   1   1   1   1   1   1   1   2   3   1   1   1   1   1   1   1   1   1 
    ## 471 474 476 477 481 482 485 486 487 488 489 490 493 496 497 498 499 502 503 506 
    ##   1   1   1   1   1   2   1   1   1   2   2   2   1   1   1   2   1   1   1   1 
    ## 507 508 510 515 518 519 520 522 524 527 529 531 532 534 535 537 540 543 544 546 
    ##   1   2   1   2   2   1   2   4   2   2   1   1   1   1   2   1   3   1   1   2 
    ## 549 551 552 553 554 555 556 557 564 570 572 574 575 577 579 581 583 584 585 586 
    ##   3   2   2   1   2   2   2   4   2   1   1   1   1   1   2   1   1   2   2   1 
    ## 588 591 592 594 596 597 600 604 605 606 608 609 610 612 613 616 622 623 624 625 
    ##   1   2   1   1   1   1   3   1   1   1   3   3   1   1   1   2   1   1   1   2 
    ## 627 630 631 632 633 634 635 636 638 
    ##   1   1   2   1   2   1   1   1   1

Entonces, podemos definir como un éxito el caso en que (1) aparecen las 638 figuritas y (2) aparecen tantas veces cada una como personas estén intentando completar el album en el escenario que estemos simulando.

``` r
personas <- 1
exito  <- ifelse(length(unique(paquetes100))==638 & min(data.frame(table(paquetes100))$Freq)>=personas, TRUE, FALSE)
exito
```

    ## [1] FALSE

En este caso, obviamente no completamos el album, ya que con 100 paquetes ni siquiera se llega a tener 670 figuritas. Para saber qué probabilidad tenemos de completar el álbum con, digamos, 600 paquetes, podemos hacer la misma simulación mil veces pero cambiando la cantidad de paquetes y ver cuántas veces nos alcanza con esos 600 paquetes para completarlo.

``` r
simulaciones <- 1000
personas <- 1
paquetes <- 600
exito <- NULL  
for(j in 1:simulaciones){
 figus<- NULL
for(k in 1:paquetes){figus <- c(figus, sample(1:638, 5, replace = FALSE))}
figus <-  figus %>% table() %>% as.data.frame()
exito[j] <- ifelse(nrow(figus)==638 & min(figus$Freq)>=personas, TRUE, FALSE)}

exitos <- sum(exito)
exitos
```

    ## [1] 3

Con 600 paquetes, en 10000 simulaciones solo se llegó a completar el album 3 veces, lo que muestra que aunque no sea imposible sigue siendo extremadamente improbable conseguir las 638 figuritas distintas con 600 paquetes sin intercambio.

El paso siguiente es hacer las simulaciones para distintas cantidades de paquetes, para calcular la probabilidad de completar el álbum con distintos números de paquetes. Cuando terminan de generarse las simulaciones para cada número de paquetes (el loop interno), se guarda el porcentaje de simulaciones “exitosas” (o sea, en que se completó la cantidad deseada de álbumes) en un objeto que luego servirá para ver qué probabilida de éxito hay con cada cantidad de paquetes.

Como mencioné más arriba, primero haré las simulaciones suponiendo que no puede salir una misma figurita dos veces en un paquete, y luego suponiendo que cada figurita es independiente de las demás del paquete.
