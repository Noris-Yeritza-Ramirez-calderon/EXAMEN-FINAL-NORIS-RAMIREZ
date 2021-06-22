ANALISIS FACTORIAL
================
NORIS YERITZA RAMIREZ CALDERON 1950198

\#IMPORTAR LA BASE DE DATOS

``` r
library(readxl)
datosd <- read_excel("C:/Users/Lenovo/Desktop/PARCIAL DE DISEÑO/datos1.xlsx")
```

\#TIPIFICACION O ESTANDARIZACION DE VARIABLES La tipificacion permite
que todas las variables metricas gocen de una misma unidad de medida
estadistica.

``` r
DatosDDE <- datosd #Crear una nueva base de datos o data frame
DatosDDE <- scale(DatosDDE, center = T, scale = T)
DatosDDE <- as.data.frame(DatosDDE)
```

\#NORMALIDAD MULTIVARIANTE H0: Normalidad multivariante  
H1: No normalidad multivariante Confianza= 95% Alfa= 5%= 0,05 P value es
mayor (&gt;) a alfa: No se rechaza la hipotesis nula H0 (Normalidad) P
value es menor (&lt;) a alfa: Se rechaza la hipotesis nula H0 (No
normalidad)

``` r
library(MVN)
```

    ## Registered S3 method overwritten by 'GGally':
    ##   method from   
    ##   +.gg   ggplot2

    ## sROC 0.1-2 loaded

``` r
mvn(DatosDDE[2:7])
```

    ## $multivariateNormality
    ##              Test          Statistic            p value Result
    ## 1 Mardia Skewness   77.6031448297931 0.0295915751502919     NO
    ## 2 Mardia Kurtosis -0.477113186812492  0.633281525010301    YES
    ## 3             MVN               <NA>               <NA>     NO
    ## 
    ## $univariateNormality
    ##           Test                Variable Statistic   p value Normality
    ## 1 Shapiro-Wilk          Edad              0.9540  0.2162      YES   
    ## 2 Shapiro-Wilk     Años de estudio        0.8818  0.0031      NO    
    ## 3 Shapiro-Wilk   Ingresos mensuales       0.7612  <0.001      NO    
    ## 4 Shapiro-Wilk    Horas de trabajo        0.7562  <0.001      NO    
    ## 5 Shapiro-Wilk  Tiempo libre (horas)      0.8994  0.0081      NO    
    ## 6 Shapiro-Wilk Horas en redes sociales    0.7910  <0.001      NO    
    ## 
    ## $Descriptives
    ##                          n          Mean Std.Dev     Median        Min      Max
    ## Edad                    30 -2.012279e-16       1 -0.2370471 -1.5704372 2.281579
    ## Años de estudio         30  2.562530e-16       1 -0.2631218 -1.2498284 1.512950
    ## Ingresos mensuales      30 -9.367507e-17       1 -0.6044713 -0.9143083 1.874225
    ## Horas de trabajo        30  2.183299e-16       1  0.2483991 -2.2355922 0.869397
    ## Tiempo libre (horas)    30 -9.439787e-17       1 -0.4219836 -1.3262342 2.290768
    ## Horas en redes sociales 30 -1.481020e-17       1  0.2255597 -0.9022389 2.481157
    ##                               25th      75th       Skew   Kurtosis
    ## Edad                    -0.6815105 0.8000341  0.3945008 -0.8928403
    ## Años de estudio         -0.8551457 0.7235849  0.3110506 -1.4027015
    ## Ingresos mensuales      -0.6614813 0.6348766  0.9767262 -0.6816130
    ## Horas de trabajo        -0.3725987 0.8693970 -1.2759523  0.5260578
    ## Tiempo libre (horas)    -0.4219836 0.4822670  0.3770279 -0.8231338
    ## Horas en redes sociales -0.9022389 0.2255597  0.9524952  0.1501908
