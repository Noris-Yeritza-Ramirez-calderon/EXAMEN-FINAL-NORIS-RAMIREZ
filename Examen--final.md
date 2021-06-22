ANALISIS FACTORIAL
================
NORIS YERITZA RAMIREZ CALDERON 1950198

\#IMPORTAR LA BASE DE DATOS

``` r
library(readxl)
datosd <- read_excel("C:/Users/Lenovo/Desktop/PARCIAL DE DISEÑO/datosd.xlsx")
```

\#TIPIFICACION O ESTANDARIZACION DE VARIABLES La tificacion permite que
todas las variables metricas gocen de una misma unidad de medida
estadistica.

``` r
DatosDDE <-datosd #Crear una nueva base de datos o data frame
DatosDDE <- scale(DatosDDE, center = T, scale = T)
```
