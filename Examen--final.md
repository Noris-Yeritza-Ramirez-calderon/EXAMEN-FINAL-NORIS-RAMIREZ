ANALISIS FACTORIAL
================
NORIS YERITZA RAMIREZ CALDERON 1950198

# IMPORTAR LA BASE DE DATOS

``` r
library(readxl)
datosd <- read_excel("C:/Users/Lenovo/Desktop/PARCIAL DE DISEÑO/datosfinales.xlsx")
```

# TIPIFICACION O ESTANDARIZACION DE VARIABLES

La tipificacion permite que todas las variables metricas gocen de una
misma unidad de medida estadistica.

``` r
DatosDDE <- datosd #Crear una nueva base de datos o data frame
DatosDDE <- scale(DatosDDE, center = T, scale = T)
DatosDDE <- as.data.frame(DatosDDE)
```

# NORMALIDAD MULTIVARIANTE

H0: Normalidad multivariante  
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

# MATRIZ DE CORRELACIONES

H0: La correlacion entre las variables es = 0 (No hay correlacion)  
H1: La correlacion es diferente a 0 (Si hay correlacion)

Cuando no se rechaza la hipotesis nula H0, entonces no se aplica el
Analisis Factorial Exprovatorio (AFE).

``` r
library(psych)
corr.test(DatosDDE[,2:7])
```

    ## Warning in abbreviate(rownames(r), minlength = minlength): abreviatura utilizada
    ## con caracteres no ASCII

    ## Warning in abbreviate(colnames(r), minlength = minlength): abreviatura utilizada
    ## con caracteres no ASCII

    ## Warning in abbreviate(dimnames(ans)[[2L]], minlength = abbr.colnames):
    ## abreviatura utilizada con caracteres no ASCII

    ## Call:corr.test(x = DatosDDE[, 2:7])
    ## Correlation matrix 
    ##                            Edad Años de estudio Horas de trabajo
    ## Edad                       1.00            0.72            -0.11
    ## Años de estudio            0.72            1.00             0.12
    ## Horas de trabajo          -0.11            0.12             1.00
    ## Tiempo libre (horas)       0.46            0.11            -0.72
    ## Horas que hacen ejercicio  0.12           -0.07            -0.75
    ## Horas en familia           0.35            0.41            -0.24
    ##                           Tiempo libre (horas) Horas que hacen ejercicio
    ## Edad                                      0.46                      0.12
    ## Años de estudio                           0.11                     -0.07
    ## Horas de trabajo                         -0.72                     -0.75
    ## Tiempo libre (horas)                      1.00                      0.51
    ## Horas que hacen ejercicio                 0.51                      1.00
    ## Horas en familia                          0.27                      0.15
    ##                           Horas en familia
    ## Edad                                  0.35
    ## Años de estudio                       0.41
    ## Horas de trabajo                     -0.24
    ## Tiempo libre (horas)                  0.27
    ## Horas que hacen ejercicio             0.15
    ## Horas en familia                      1.00
    ## Sample Size 
    ## [1] 30
    ## Probability values (Entries above the diagonal are adjusted for multiple tests.) 
    ##                           Edad Años de estudio Horas de trabajo
    ## Edad                      0.00            0.00              1.0
    ## Años de estudio           0.00            0.00              1.0
    ## Horas de trabajo          0.56            0.53              0.0
    ## Tiempo libre (horas)      0.01            0.57              0.0
    ## Horas que hacen ejercicio 0.52            0.71              0.0
    ## Horas en familia          0.06            0.02              0.2
    ##                           Tiempo libre (horas) Horas que hacen ejercicio
    ## Edad                                      0.12                      1.00
    ## Años de estudio                           1.00                      1.00
    ## Horas de trabajo                          0.00                      0.00
    ## Tiempo libre (horas)                      0.00                      0.04
    ## Horas que hacen ejercicio                 0.00                      0.00
    ## Horas en familia                          0.15                      0.42
    ##                           Horas en familia
    ## Edad                                  0.52
    ## Años de estudio                       0.25
    ## Horas de trabajo                      1.00
    ## Tiempo libre (horas)                  1.00
    ## Horas que hacen ejercicio             1.00
    ## Horas en familia                      0.00
    ## 
    ##  To see confidence intervals of the correlations, print with the short=FALSE option

``` r
Correlaciones <- corr.test(DatosDDE[,2:7]) #Se crea la matriz de correlaciones
```

    ## Warning in abbreviate(rownames(r), minlength = minlength): abreviatura utilizada
    ## con caracteres no ASCII

    ## Warning in abbreviate(colnames(r), minlength = minlength): abreviatura utilizada
    ## con caracteres no ASCII

    ## Warning in abbreviate(dimnames(ans)[[2L]], minlength = abbr.colnames):
    ## abreviatura utilizada con caracteres no ASCII

``` r
Correlaciones$r #Esta es la matriz de correlaciones
```

    ##                                 Edad Años de estudio Horas de trabajo
    ## Edad                       1.0000000      0.71580233       -0.1104043
    ## Años de estudio            0.7158023      1.00000000        0.1183227
    ## Horas de trabajo          -0.1104043      0.11832272        1.0000000
    ## Tiempo libre (horas)       0.4601134      0.10665739       -0.7241900
    ## Horas que hacen ejercicio  0.1212917     -0.07008322       -0.7451909
    ## Horas en familia           0.3506514      0.40970763       -0.2385162
    ##                           Tiempo libre (horas) Horas que hacen ejercicio
    ## Edad                                 0.4601134                0.12129175
    ## Años de estudio                      0.1066574               -0.07008322
    ## Horas de trabajo                    -0.7241900               -0.74519088
    ## Tiempo libre (horas)                 1.0000000                0.51381268
    ## Horas que hacen ejercicio            0.5138127                1.00000000
    ## Horas en familia                     0.2722155                0.15192533
    ##                           Horas en familia
    ## Edad                             0.3506514
    ## Años de estudio                  0.4097076
    ## Horas de trabajo                -0.2385162
    ## Tiempo libre (horas)             0.2722155
    ## Horas que hacen ejercicio        0.1519253
    ## Horas en familia                 1.0000000

``` r
r <- as.matrix(Correlaciones$r)
```

Af: 0,05  
P value es mayor (&gt;) a alfa: No se rechaza la hipotesis nula H0  
P value es menor (&lt;) a alfa: Se rechaza la hipotesis nula H0, estamos
en esta situacion por lo tanto, si es aplicable el Analisis Factorial
Exploratorio (AFE).

# INDICADORES DE APLICABILIDAD DEL AFE (BONDAD DEL AJUSTE)

## CONTRASTE DE ESFERICIDAD DE BARTLETT

H0: En las correlaciones teoricas entre cada par de variable es nulo  
H1: Las correlaciones teoricas entre cada par de variables no es nulo

P value es mayor (&gt;) a alfa: No se aplica el AFE (no se rechaza H0)  
P value es menor (&lt;) a alfa: Si Se aplica el AFE (no se rechaza H1)

``` r
dim(DatosDDE) #Tamaño de muestra= 30 personas
```

    ## [1] 30  7

``` r
cortest.bartlett(r, n= 30)
```

    ## $chisq
    ## [1] 81.14841
    ## 
    ## $p.value
    ## [1] 4.304182e-11
    ## 
    ## $df
    ## [1] 15

Como el P value es menor a alfa, se rechaza la hipotesis nula H0, por lo
tanto, las correlaciones teoricas entre cada par de variables es nulo,
es decir, si es aplicable el analisis factorial exploratorio (AFE)

# MEDIDA DE ADECUACION MUESTRAL DE KAISER, MEYER Y OKLIN (KMO)

Estudia variables, si son o no aceptadas en el modelo para hacer AFE.
(Que variables elimino o mantengo)  
Se mantiene una variable en el modelo, si el KMO es igual o mayor a
0,7.  
Se elimina una variable del modelo, si el KMO es menor a 0,7.

``` r
KMO(r)
```

    ## Kaiser-Meyer-Olkin factor adequacy
    ## Call: KMO(r = r)
    ## Overall MSA =  0.58
    ## MSA for each item = 
    ##                      Edad           Años de estudio          Horas de trabajo 
    ##                      0.51                      0.53                      0.57 
    ##      Tiempo libre (horas) Horas que hacen ejercicio          Horas en familia 
    ##                      0.59                      0.67                      0.76

El KMO= 0,58 el modelo es miserable, si es adecuado para realizar
analisis factorial.  
KMO edad= 0,51 (Miserable)  
KMO años de estudio= 0,53 (Miserable)  
KMO horas de trabajo= 0,57 (Miserable)  
KMO tiempo libre= 0,59 (Miserable)  
KMO horas que hacen ejercicio= 0,67 (Middling)  
KMO horas en familia= 0,76 (Middling)

## DETERMINACION DEL NUMERO DE FACTORES A EXTRAER

## Metodo de las componentes principales iteradas (Ejes principales)

Este metodo de las Ejes principales es de naturaleza no parametrica, es
decir, que se ocupa, cuando no hay normalidad multivariante; pero
tambien es valido para modelos parametricos (normalidad multivariante).

``` r
fa.parallel(r, "pa", n.obs=30, ylabel="Eigenvalues")
```

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

![](Examen--final_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

    ## Parallel analysis suggests that the number of factors =  2  and the number of components =  2

Con el metodo de los ejes principales se extraerian solo 2 factores.

## Metodo de las componentes principales

Metodo parametrico, sirve solo para modelos con normalidad
multivariante.

``` r
fa.parallel(r, "pc", n.obs=30, ylabel= "Eigenvalues")
```

    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fac(r = r, nfactors = nfactors, n.obs = n.obs, rotate = rotate, : An
    ## ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## An ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## An ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## An ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## An ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## An ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## The estimated weights for the factor scores are probably incorrect. Try a
    ## different factor score estimation method.

    ## Warning in fa.stats(r = r, f = f, phi = phi, n.obs = n.obs, np.obs = np.obs, :
    ## An ultra-Heywood case was detected. Examine the results carefully

    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used
    ## factor method not specified correctly, minimum residual (unweighted least squares  used

![](Examen--final_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

    ## Parallel analysis suggests that the number of factors =  2  and the number of components =  2

Con el metodo de las componentes principales se recomienda extraer 2
factores.

## Metodo de la maxima verosimilidad

Metodo parametrico, sirve solo para modelos con normalidad
multivariante.

``` r
fa.parallel(r, "ml", n.obs=30, ylabel= "Eigenvalues")
```

![](Examen--final_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

    ## Parallel analysis suggests that the number of factors =  2  and the number of components =  2

Con el metodo de la maxima verosimilidad se recomienda extraer 2
factores.

## Metodo paralelo con iteraciones

Metodo parametrico, sirve solo para nodelos con normalidad
multivariante.

``` r
library(paran)
```

    ## Loading required package: MASS

``` r
paran(r, iterations= 1000, graph= T)
```

    ## 
    ## Using eigendecomposition of correlation matrix.
    ## Computing: 10%  20%  30%  40%  50%  60%  70%  80%  90%  100%
    ## 
    ## 
    ## Results of Horn's Parallel Analysis for component retention
    ## 1000 iterations, using the mean estimate
    ## 
    ## -------------------------------------------------- 
    ## Component   Adjusted    Unadjusted    Estimated 
    ##             Eigenvalue  Eigenvalue    Bias 
    ## -------------------------------------------------- 
    ## 1           1.436823    3.199016      1.762192
    ## 2           1.311848    2.010276      0.698427
    ## -------------------------------------------------- 
    ## 
    ## Adjusted eigenvalues > 1 indicate dimensions to retain.
    ## (2 components retained)

![](Examen--final_files/figure-gfm/unnamed-chunk-10-1.png)<!-- --> Con
el metodo Horn´s (metodo paralelo con iteraciones) se recomienda extraer
2 factores.

Resumen:  
Ejes principales= 2 factores  
Componentes principales= 2 factores  
Maxima verosimilitud= 2 factores  
Metodo paralelo con iteraciones (Horn´s )= 2 factores

Conclucion:  
Vamos a extraer 2 factores
