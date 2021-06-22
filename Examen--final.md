ANALISIS FACTORIAL
================
NORIS YERITZA RAMIREZ CALDERON 1950198

\#IMPORTAR LA BASE DE DATOS

``` r
library(readxl)
datosd <- read_excel("C:/Users/Lenovo/Desktop/PARCIAL DE DISEÑO/datosfinales.xlsx")
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
H1: No normalidad multivariante  
Confianza= 95%  
Alfa= 5%= 0,05  
P value es mayor (&gt;) a alfa: No se rechaza la hipotesis nula H0
(Normalidad)  
P value es menor (&lt;) a alfa: Se rechaza la hipotesis nula H0 (No
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
    ## 1 Mardia Skewness   71.2960829636944 0.0817887961977343    YES
    ## 2 Mardia Kurtosis -0.331180532676477  0.740508123968739    YES
    ## 3             MVN               <NA>               <NA>    YES
    ## 
    ## $univariateNormality
    ##           Test                  Variable Statistic   p value Normality
    ## 1 Shapiro-Wilk           Edad               0.9540  0.2162      YES   
    ## 2 Shapiro-Wilk      Años de estudio         0.8818  0.0031      NO    
    ## 3 Shapiro-Wilk     Horas de trabajo         0.7562  <0.001      NO    
    ## 4 Shapiro-Wilk   Tiempo libre (horas)       0.8994  0.0081      NO    
    ## 5 Shapiro-Wilk Horas que hacen ejercicio    0.7533  <0.001      NO    
    ## 6 Shapiro-Wilk     Horas en familia         0.7892  <0.001      NO    
    ## 
    ## $Descriptives
    ##                            n          Mean Std.Dev     Median       Min
    ## Edad                      30 -2.012279e-16       1 -0.2370471 -1.570437
    ## Años de estudio           30  2.562530e-16       1 -0.2631218 -1.249828
    ## Horas de trabajo          30  2.183299e-16       1  0.2483991 -2.235592
    ## Tiempo libre (horas)      30 -9.439787e-17       1 -0.4219836 -1.326234
    ## Horas que hacen ejercicio 30  5.179595e-17       1  0.5962565 -1.029898
    ## Horas en familia          30 -1.035928e-16       1  0.3010399 -1.204159
    ##                                Max       25th      75th       Skew   Kurtosis
    ## Edad                      2.281579 -0.6815105 0.8000341  0.3945008 -0.8928403
    ## Años de estudio           1.512950 -0.8551457 0.7235849  0.3110506 -1.4027015
    ## Horas de trabajo          0.869397 -0.3725987 0.8693970 -1.2759523  0.5260578
    ## Tiempo libre (horas)      2.290768 -0.4219836 0.4822670  0.3770279 -0.8231338
    ## Horas que hacen ejercicio 2.222410 -1.0298975 0.5962565  0.3643991 -0.8229562
    ## Horas en familia          1.806239 -1.2041595 0.3010399  0.2182539 -0.8755990

Como el P value es mayor (&gt;) a alfa, no se rechaza la hipotesis nula
H0, por lo tanto, existe normalidad multivariante.
