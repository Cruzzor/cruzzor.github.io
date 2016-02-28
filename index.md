---
title       : Shiny-App Pitch
subtitle    : Presenting the Shiny-App from Dev. Data Products
author      : MB
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Overview

1. Introduction
2. The App
3. Example

---

## Introduction

* App for the Coursera Course "Developing Data Products"
* Created with Shiny
* Uploaded on shinyapps.io (https://cruzzor.shinyapps.io/Shiny-App/)
* Basic functionality: Calculate the cross sum of a natural number

---

## The App: digits

* Most interesting component: server.R
* Function _digits_ separates natural number into digits


```r
library(slidify)  ## Loading slidify

digits <- function(x) {
  if(length(x) > 1 ) {
    lapply(x, digits)
  } else {
    n <- nchar(x)
    rev( x %/% 10^seq(0, length.out=n) %% 10 )
  }
}
```

---

## The App: shinyServer

* Function _sum_ is used to add up the digits


```r
shinyServer(function(input, output) {
   
  output$inputValue <- renderPrint({input$number})
  output$calculation <- renderPrint({sum(digits(input$number))})
  
})
```

```
## Error in eval(expr, envir, enclos): konnte Funktion "shinyServer" nicht finden
```

```r
## Example:
sum(digits(1234))
```

```
## [1] 10
```
