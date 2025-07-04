---
layout: math
title: 03 Linear Regression
parent: Modelowanie
nav_order: 2
---

# Linear Regression

1. Describe the null hypotheses to which the p-values given in Table 3.4 correspond. Explain what conclusions you can draw based on these $p$-values. Your explanation should be phrased in terms of `sales`, `TV`, `radio`, and `newspaper`, rather than in terms of the coefficients of the linear model.

    Hipotezy zerowe dla tabeli 3.4:

    $(TV) H_0: \beta_0 = 0$

    $(Radio) H_0: \beta_1 = 0$

    $(Newspaper) H_0: \beta_2 = 0$
    
    $p$-values dla TV i Radio są małe, co oznacza, że hipotezy zerowe muszą być odrzucone. Pokazuje to, że zmienna objaśniana silnie zależy od wspomnianych dwóch zmiennych objaśniających. $p$-value dla Newspaper jest duże co oznacza, że $\beta_2=0$ czyli ta zmienna nie ma wpływu na zmienną objaśnianą.

2. Carefully explain the differences between the KNN classifier and KNN regression methods.

    KNN odnosi się do nieparametrycznych metod, które mogą zostać użyte do klasyfikacji lub regresji. 
    
    Klasyfikator KNN określa $K$ najbliższych punktów wokół obserwacji $x_0$ w celach klasyfikacji. Następnie estymuje prawdopodobieństwo tego, że $x_0$ należy do danej klasy na podstawie sąsiednich obserwacji. Klasyfikator KNN daje odpowiedź jakościową.

    Regresja KNN działa podobnie do klasyfikatora KNN jednak wyznaczana jest w tym przypadku ilościowa predykcja zależności $f(x_0)$.

3. Suppose we have a data set with five predictors, $X_1 = \text{GPA}$, $X_2 = \text{IQ}$, $X_3 = \text{Level}$ (1 for College and 0 for High School), $X_4 = $ Interaction between $\text{GPA}$ and $\text{IQ}$, and $X_5 =$ Interaction between $\text{GPA}$ and $\text{Level}$. The response is starting salary after graduation (in thousands
of dollars). Suppose we use least squares to fit the model, and get $\hat{β}_0 = 50$, $\hat{β}_1 = 20$, $\hat{β}_2 = 0.07$, $\hat{β}_3 = 35$, $\hat{β}_4 = 0.01$, $\hat{β}_5 =−10$.

    (a) Which answer is correct, and why?

    > Model z zadania wygląda następująco: 
    >
    > $Y = 50 + 20\cdot\text{GPA} + 0.07\cdot\text{IQ} + 35\cdot\text{Level} + 0.01\cdot\text{GPA}\cdot\text{IQ} - 10\cdot\text{GPA}\cdot\text{Level}$
    
    i. For a fixed value of $\text{IQ}$ and $\text{GPA}$, high school graduates earn more, on average, than college graduates.

    > Fałsz, gdy $\text{Level} = 0$ to zarobki w modelu będą niższe.

    ii. For a fixed value of $\text{IQ}$ and $\text{GPA}$, college graduates earn more, on average, than high school graduates.

    > Fałsz, w modelu jest czynnik $- 10\cdot\text{GPA}\cdot\text{Level}$ i dla odpowiednio wysokiego $\text{GPA}$ high school zarabia więcej od college.

    iii. For a fixed value of $\text{IQ}$ and $\text{GPA}$, high school graduates earn more, on average, than college graduates provided that the $\text{GPA}$ is high enough.

    > Prawda.
    
    iv. For a fixed value of $\text{IQ}$ and $\text{GPA}$, college graduates earn more, on average, than high school graduates provided that the GPA is high enough.

    > Fałsz.

    (b) Predict the salary of a college graduate with $\text{IQ}$ of 110 and a $\text{GPA}$ of 4.0.

    > 137.1

    (c) True or false: Since the coefficient for the $\text{GPA/IQ}$ interaction term is very small, there is very little evidence of an interaction effect. Justify your answer.

    > Fałsz, niski współczynnik nie oznacza braku dowodu na interakcję. Ostatecznie trzeba określić $p$-value i wtedy zdecydować.

4. I collect a set of data ($n = 100$ observations) containing a single predictor and a quantitative response. I then fit a linear regression model to the data, as well as a separate cubic regression, i.e. $Y = \beta_0 + \beta_1X + \beta_2X^2 + \beta_3X^3 + \epsilon$.
    
    (a) Suppose that the true relationship between $X$ and $Y$ is linear, i.e. $Y = \beta_0 + \beta_1X + \epsilon$. Consider the training residual sum of squares (RSS) for the linear regression, and also the training RSS for the cubic regression. Would we expect one to be lower than the other, would we expect them to be the same, or is there not enough information to tell? Justify your answer.

    > Dodanie kolejnego czynnika wielomianowego spowoduje bliższe dopasowanie do danych treningowych przez co RSS będzie mniejszy niż w przypadku prostej regresji liniowej.
    
    (b) Answer (a) using test rather than training RSS.

    > Prawdziwa zależność jest liniowa więc statystyka F powinna wynosić więcej niż 1. W przypadku modelu wielomianowego powinniśmy spodziewać się wartości bliskiej 1 co oznacza, że jeden z współczynników wynosi 0.
    
    (c) Suppose that the true relationship between $X$ and $Y$ is not linear, but we don’t know how far it is from linear. Consider the training RSS for the linear regression, and also the training RSS for the cubic regression. Would we expect one to be lower than the other, would we expect them to be the same, or is there not enough information to tell? Justify your answer.

    > Dodanie kolejnego czynnika wielomianowego spowoduje bliższe dopasowanie do danych treningowych przez co RSS będzie mniejszy niż w przypadku prostej regresji liniowej.
    
    (d) Answer (c) using test rather than training RSS.

    > Prawdopodobnie uzyskamy wartości statystyki F powyżej 1 co oznacza, że jeden z współczynników nie wynosi 0.

5. Consider the fitted values that result from performing linear regression without an intercept. In this setting, the $i$-th fitted value takes the form 

    $$\hat{y}_i=x_i\hat{\beta},$$

    where 
        
    $$\hat{\beta}=\left(\sum\limits_{i=1}^n x_i y_i \right) /  \left(\sum\limits_{i'=1}^n x_{i'}^2\right).$$

    Show that we can write

    $$\hat{y}_i = \sum\limits_{i'=1}^n a_{i'}y_{i'}$$

    What is $a_{i'}$?
    
    _Note: We interpret this result by saying that the fitted values from linear regression are linear combinations of the response values._

    $$
    \hat{y}_i = x_i\hat{\beta} = x_i \frac{\sum\limits_{i'=1}^n x_{i'} y_{i'}}{\sum\limits_{j=1}^n x_{j}^2} = \sum\limits_{i'=1}^n\frac{x_{i'} x_i}{\sum\limits_{j=1}^n x_{j}^2}y_{i'} = \sum\limits_{i'=1}^n a_{i'}y_{i'}
    $$

    $$a_{i'} = \frac{x_{i'} x_i}{\sum\limits_{j=1}^n x_{j}^2}$$

6. Using (3.4), argue that in the case of simple linear regression, the least squares line always passes through the point $(\bar{x},\bar{y})$.

    $$\hat{\beta}_1 = \frac{\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})}{\sum_{i=1}^n(x_i-\bar{x})^2}$$

    $$\hat{\beta}_0 = \bar{y} - \hat{\beta}_1\bar{x}$$

    $$\hat{y}_j = \hat{\beta}_0 + \hat{\beta}_1x_j$$

    gdy $x_j = \bar{x}$, to:

    $$\hat{y}_j = \bar{y} - \hat{\beta}_1\bar{x} + \hat{\beta}_1\bar{x} = \bar{y}$$

    Jeżeli $x_j = \bar{x}$ to linia regresji przechodzi przez punkt $(\bar{x}, \bar{y})$.

7. It is claimed in the text that in the case of simple linear regression of $Y$ onto $X$, the $R^2$ statistic (3.17) is equal to the square of the correlation between $X$ and $Y$ (3.18). Prove that this is the case. For
simplicity, you may assume that $\bar{x} = \bar{y} = 0$.

    $$R^2 = \frac{TSS-RSS}{TSS}$$

    $$RSS = \sum_{i=1}^n(y_i-\hat{y}_i)^2$$

    $$TSS = \sum_{i=1}^ny_i^2$$

    $$\hat{y}_i = \hat{\beta}_1x_i$$

    $$\hat{\beta}_1 = \frac{\sum_{i=1}^nx_iy_i}{\sum_{i=1}^nx_i^2}$$

    $$\begin{aligned}R^2 &= \frac{TSS-RSS}{TSS} = \frac{\sum_{i=1}^ny_i^2 - \sum_{i=1}^n(y_i-\hat{y}_i)^2}{\sum_{i=1}^ny_i^2} = \\
    &= \frac{\sum_{i=1}^ny_i^2 - \sum_{i=1}^n(y_i^2 - 2y_i\hat{y}_i +\hat{y}_i^2)}{\sum_{i=1}^ny_i^2} = \\
    &= \frac{2\sum_{i=1}^ny_i\hat{y}_i - \sum_{i=1}^n\hat{y}_i^2}{\sum_{i=1}^ny_i^2} = \\
    &= \frac{2\sum_{i=1}^ny_i\hat{\beta}_1x_i - \sum_{i=1}^n\hat{\beta}_1^2x_i^2}{\sum_{i=1}^ny_i^2} = \\      
    &= \frac{2\sum_{i=1}^ny_ix_i\frac{\sum_{i=1}^nx_iy_i}{\sum_{i=1}^nx_i^2} - \sum_{i=1}^nx_i^2 \left(\frac{\sum_{i=1}^nx_iy_i}{\sum_{i=1}^nx_i^2}\right)^2}{\sum_{i=1}^ny_i^2} = \\
    &= \frac{2\frac{\left(\sum_{i=1}^nx_iy_i\right)^2}{\sum_{i=1}^nx_i^2} - \frac{\left(\sum_{i=1}^nx_iy_i\right)^2}{\sum_{i=1}^nx_i^2}}{\sum_{i=1}^ny_i^2} = \\
    &= \frac{\frac{\left(\sum_{i=1}^nx_iy_i\right)^2}{\sum_{i=1}^nx_i^2}}{\sum_{i=1}^ny_i^2} = \\
    &= \frac{\left(\sum_{i=1}^nx_iy_i\right)^2}{\sum_{i=1}^nx_i^2\sum_{i=1}^ny_i^2} = \\ 
    &= Cor^2(X,Y)\end{aligned}$$

8. This question involves the use of simple linear regression on the `Auto` data set.
    
    (a) Use the `lm()` function to perform a simple linear regression with `mpg` as the response and `horsepower` as the predictor. Use the `summary()` function to print the results. Comment on the output.

    ```R
    > library(ISLR)
    > data(Auto)
    > mpg_pwr = lm(mpg ~ horsepower, data = Auto)
    > summary(mpg_pwr)

    Call:
    lm(formula = mpg ~ horsepower, data = Auto)

    Residuals:
         Min       1Q   Median       3Q      Max 
    -13.5710  -3.2592  -0.3435   2.7630  16.9240 

    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 39.935861   0.717499   55.66   <2e-16 ***
    horsepower  -0.157845   0.006446  -24.49   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 4.906 on 390 degrees of freedom
    Multiple R-squared:  0.6059,	Adjusted R-squared:  0.6049 
    F-statistic: 599.7 on 1 and 390 DF,  p-value: < 2.2e-16
    ```

    For example:
    
    i. Is there a relationship between the predictor and the response?

    > Na podstawie $p$-value bliskiego zeru można stwierdzić, że istnieje zależność.
    
    ii. How strong is the relationship between the predictor and the response?

    > Statystyka $R^2$ wynosi 0.61 co oznacza, że 61% wariancji zmiennej `mpg` jest objaśniane przez model z `horsepower`, oznacza to, że ponad połowa zmienności jest objaśniana przez model.
    
    iii. Is the relationship between the predictor and the response positive or negative?

    > Zależność jest negatywna. Na każdy 1 koń mechaniczny, `mpg` spada o 0.158.
    
    iv. What is the predicted `mpg` associated with a `horsepower` of 98? What are the associated 95 % confidence and prediction intervals?

    ```R
    > predict(mpg_pwr, data.frame(horsepower=c(98)), interval='prediction')

           fit     lwr      upr
    1 24.46708 14.8094 34.12476
    ```

    ```R
    > predict(mpg_pwr, data.frame(horsepower=c(98)), interval='confidence')
    
           fit      lwr      upr
    1 24.46708 23.97308 24.96108
    ```

    (b) Plot the response and the predictor. Use the `abline()` function to display the least squares regression line.

    ```R
    > plot(mpg~horsepower,main= "Scatter plot of mpg vs. horsepower", data=Auto)
    > abline(mpg_pwr, lwd =3, col ="red")
    ```

    ![](img/03_8b.png)
    
    (c) Use the `plot()` function to produce diagnostic plots of the least squares regression fit. Comment on any problems you see with the fit.

    ```R
    > par(mfrow=c(2,2))
    > plot(mpg_pwr)
    ```

    ![](img/03_8c.png)

    * Residuals vs Fitted - widać pewną zależność w kształcie litery U co mówi o tym, że dane nie są liniowe.
    * Residuals v leverage - wskazuje na pewne obserwacje z dużym wpływem na model.
    * Scale-Location - wskazuje, że mogą występować pewne obserwacje odstające. Można je znaleźć używając komendy: 
    ```R
    > rstudent(mpg_pwr)[which(rstudent(mpg_pwr)>3)]

         323      330 
    3.508709 3.149671 
    ```

9. This question involves the use of multiple linear regression on the `Auto` data set.

    (a) Produce a scatterplot matrix which includes all of the variables in the data set.

    ```R
    > library(ISLR)
    > data(Auto)
    > Auto <- Auto[,1:8] # usuwam kolumnę name z danych
    > pairs(Auto)
    ```

    ![](img/03_9a.png)
    
    (b) Compute the matrix of correlations between the variables using the function `cor()`. You will need to exclude the `name` variable, which is qualitative.

    ```R
    > cor(Auto)

                        mpg  cylinders displacement horsepower     weight acceleration
    mpg           1.0000000 -0.7776175   -0.8051269 -0.7784268 -0.8322442    0.4233285
    cylinders    -0.7776175  1.0000000    0.9508233  0.8429834  0.8975273   -0.5046834
    displacement -0.8051269  0.9508233    1.0000000  0.8972570  0.9329944   -0.5438005
    horsepower   -0.7784268  0.8429834    0.8972570  1.0000000  0.8645377   -0.6891955
    weight       -0.8322442  0.8975273    0.9329944  0.8645377  1.0000000   -0.4168392
    acceleration  0.4233285 -0.5046834   -0.5438005 -0.6891955 -0.4168392    1.0000000
    year          0.5805410 -0.3456474   -0.3698552 -0.4163615 -0.3091199    0.2903161
    origin        0.5652088 -0.5689316   -0.6145351 -0.4551715 -0.5850054    0.2127458
                       year     origin
    mpg           0.5805410  0.5652088
    cylinders    -0.3456474 -0.5689316
    displacement -0.3698552 -0.6145351
    horsepower   -0.4163615 -0.4551715
    weight       -0.3091199 -0.5850054
    acceleration  0.2903161  0.2127458
    year          1.0000000  0.1815277
    origin        0.1815277  1.0000000
    ```
    
    (c) Use the `lm()` function to perform a multiple linear regression with `mpg` as the response and all other variables except `name` as the predictors. Use the `summary()` function to print the results. Comment on the output.

    ```R
    > mpg_all = lm(mpg ~ .,data=Auto)
    > summary(mpg_all)

    Call:
    lm(formula = mpg ~ ., data = Auto)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -9.5903 -2.1565 -0.1169  1.8690 13.0604 

    Coefficients:
                   Estimate Std. Error t value Pr(>|t|)    
    (Intercept)  -17.218435   4.644294  -3.707  0.00024 ***
    cylinders     -0.493376   0.323282  -1.526  0.12780    
    displacement   0.019896   0.007515   2.647  0.00844 ** 
    horsepower    -0.016951   0.013787  -1.230  0.21963    
    weight        -0.006474   0.000652  -9.929  < 2e-16 ***
    acceleration   0.080576   0.098845   0.815  0.41548    
    year           0.750773   0.050973  14.729  < 2e-16 ***
    origin         1.426141   0.278136   5.127 4.67e-07 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 3.328 on 384 degrees of freedom
    Multiple R-squared:  0.8215,	Adjusted R-squared:  0.8182 
    F-statistic: 252.4 on 7 and 384 DF,  p-value: < 2.2e-16
    ```
    
    For instance:

    i. Is there a relationship between the predictors and the response?

    > Jest związek ponieważ $p$-value wynosi w przybliżeniu 0 w teście dla statystyki F wynoszącej 252.4.
    
    ii. Which predictors appear to have a statistically significant relationship to the response?

    > `displacement`, `weight`, `year`, `origin`, ponieważ ich $p$-value jest mniejsze od 0.05.
    
    iii. What does the coefficients for the `year` variable suggest?

    > Zwiększając rok o 1, `mpg` wzrośnie o 0.75 zakładając, że reszta zmiennych jest stała.
    
    (d) Use the `plot()` function to produce diagnostic plots of the linear regression fit. Comment on any problems you see with the fit. Do the residual plots suggest any unusually large outliers? Does the leverage plot identify any observations with unusually high leverage?

    ```R
    > par(mfrow=c(2,2))
    > plot(mpg_all)
    ```

    ![](img/03_9d.png)

    > * Residuals vs Fitted - widać pewną zależność w kształcie litery U co mówi o tym, że dane nie są liniowe.
    * Residuals v leverage - wskazuje, że obserwacja 14 ma duży wpływ na model.
    * Scale-Location - wskazuje, że mogą występować pewne obserwacje odstające. Można je znaleźć używając komendy:

    ```R
    > rstudent(mpg_all)[which(rstudent(mpg_all)>3)]

         245      323      326      327 
    3.390068 4.029537 3.494823 3.690246 
    ```
    
    (e) Use the `*` and `:` symbols to fit linear regression models with interaction effects. Do any interactions appear to be statistically significant?

    ```R
    > mpg_interaction = lm(mpg ~ . + year:cylinders + acceleration:horsepower 
                           + weight:displacement,data=Auto)
    > summary(mpg_interaction)

    Call:
    lm(formula = mpg ~ . + year:cylinders + acceleration:horsepower + 
        weight:displacement, data = Auto)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -8.4059 -1.5831  0.0088  1.2438 12.8486 

    Coefficients:
                              Estimate Std. Error t value Pr(>|t|)    
    (Intercept)             -6.684e+01  1.153e+01  -5.796 1.43e-08 ***
    cylinders                1.078e+01  2.177e+00   4.953 1.10e-06 ***
    displacement            -7.013e-02  1.055e-02  -6.651 1.01e-10 ***
    horsepower               2.725e-02  2.447e-02   1.114  0.26618    
    weight                  -8.598e-03  8.379e-04 -10.262  < 2e-16 ***
    acceleration             5.021e-01  1.531e-01   3.281  0.00113 ** 
    year                     1.462e+00  1.473e-01   9.929  < 2e-16 ***
    origin                   5.099e-01  2.511e-01   2.031  0.04296 *  
    cylinders:year          -1.350e-01  2.799e-02  -4.824 2.04e-06 ***
    horsepower:acceleration -5.436e-03  1.732e-03  -3.138  0.00183 ** 
    displacement:weight      1.852e-05  2.291e-06   8.087 8.25e-15 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 2.821 on 381 degrees of freedom
    Multiple R-squared:  0.8727,	Adjusted R-squared:  0.8694 
    F-statistic: 261.2 on 10 and 381 DF,  p-value: < 2.2e-16
    ```

    > Dodanie interakcji zwiększyło wskaźnik R^2 adjusted czyli model jest lepiej dopasowany. Interakcje są istotne ponieważ ich $p$-value jest mniejszy od 0.05.
    
    (f) Try a few different transformations of the variables, such as $\log(X)$, $\sqrt{X}$, $X^2$. Comment on your findings.

    ```R
    > mpg_ope = lm(mpg ~ . + log(weight) + log(acceleration) + sqrt(displacement) 
                   + I(cylinders^2), data=Auto)
    > summary(mpg_ope)

    Call:
    lm(formula = mpg ~ . + log(weight) + log(acceleration) + sqrt(displacement) + 
        I(cylinders^2), data = Auto)

    Residuals:
         Min       1Q   Median       3Q      Max 
    -10.0014  -1.6217  -0.1169   1.6178  12.5279 

    Coefficients:
                         Estimate Std. Error t value Pr(>|t|)    
    (Intercept)        293.415553  51.474048   5.700 2.40e-08 ***
    cylinders            0.960831   1.496776   0.642  0.52130    
    displacement         0.040087   0.032271   1.242  0.21493    
    horsepower          -0.042899   0.013118  -3.270  0.00117 ** 
    weight               0.007242   0.002314   3.130  0.00188 ** 
    acceleration         1.989149   0.469850   4.234 2.89e-05 ***
    year                 0.804299   0.045146  17.816  < 2e-16 ***
    origin               0.505488   0.270580   1.868  0.06251 .  
    log(weight)        -35.552480   7.175205  -4.955 1.09e-06 ***
    log(acceleration)  -33.141292   7.682303  -4.314 2.05e-05 ***
    sqrt(displacement)  -1.222754   0.987784  -1.238  0.21653    
    I(cylinders^2)      -0.094503   0.122199  -0.773  0.43979    
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 2.918 on 380 degrees of freedom
    Multiple R-squared:  0.8642,	Adjusted R-squared:  0.8603 
    F-statistic: 219.8 on 11 and 380 DF,  p-value: < 2.2e-16
    ```

    > Nastąpiła poprawa modelu względem bazowego patrząc na R^2 adjusted ale transformacje `sqrt(displacement)` i `cylinders^2` są zbędne ponieważ ich $p$-value wynosi powyżej 0.05.

10. This question should be answered using the `Carseats` data set.

    (a) Fit a multiple regression model to predict `Sales` using `Price`, `Urban`, and `US`.

    ```R
    > library(ISLR)
    > carseats_lm = lm(Sales~Price+Urban+US,data=Carseats)
    > summary(carseats_lm)

    Call:
    lm(formula = Sales ~ Price + Urban + US, data = Carseats)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -6.9206 -1.6220 -0.0564  1.5786  7.0581 

    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 13.043469   0.651012  20.036  < 2e-16 ***
    Price       -0.054459   0.005242 -10.389  < 2e-16 ***
    UrbanYes    -0.021916   0.271650  -0.081    0.936    
    USYes        1.200573   0.259042   4.635 4.86e-06 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 2.472 on 396 degrees of freedom
    Multiple R-squared:  0.2393,	Adjusted R-squared:  0.2335 
    F-statistic: 41.52 on 3 and 396 DF,  p-value: < 2.2e-16
    ```
    
    (b) Provide an interpretation of each coefficient in the model. Be careful — some of the variables in the model are qualitative!

    > * Intercept - reprezentuje średnią sprzedaż gdy inne zmienne są zaniedbywalne.
    * Price - sprzedaż spada gdy cena rośnie.
    * UrbanYes - sprzedaż spada gdy sklep jest w mieście.
    * USYes - sprzedaż rośnie gdy sklep jest w USA.
    
    (c) Write out the model in equation form, being careful to handle the qualitative variables properly.

    ```R
    > contrasts(Carseats$Urban)

        Yes
    No    0
    Yes   1

    > contrasts(Carseats$US)

        Yes
    No    0
    Yes   1
    ```

    > $$Sales = \begin{cases}
    13.04 - 0.05Price - 0.02 + 1.2 & \text{ gdy Urban = 1, US = 1} \\
    13.04 - 0.05Price - 0.02 & \text{ gdy Urban = 1, US = 0} \\
    13.04 - 0.05Price + 1.2 & \text{ gdy Urban = 0, US = 1} \\
    13.04 - 0.05Price & \text{ gdy Urban = 0, US = 0} \\
    \end{cases}$$
    
    (d) For which of the predictors can you reject the null hypothesis $H_0: \beta_j = 0$?

    ```R
    > carseats_all = lm(Sales~.,data=Carseats)
    > summary(carseats_all)

    Call:
    lm(formula = Sales ~ ., data = Carseats)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -2.8692 -0.6908  0.0211  0.6636  3.4115 

    Coefficients:
                      Estimate Std. Error t value Pr(>|t|)    
    (Intercept)      5.6606231  0.6034487   9.380  < 2e-16 ***
    CompPrice        0.0928153  0.0041477  22.378  < 2e-16 ***
    Income           0.0158028  0.0018451   8.565 2.58e-16 ***
    Advertising      0.1230951  0.0111237  11.066  < 2e-16 ***
    Population       0.0002079  0.0003705   0.561    0.575    
    Price           -0.0953579  0.0026711 -35.700  < 2e-16 ***
    ShelveLocGood    4.8501827  0.1531100  31.678  < 2e-16 ***
    ShelveLocMedium  1.9567148  0.1261056  15.516  < 2e-16 ***
    Age             -0.0460452  0.0031817 -14.472  < 2e-16 ***
    Education       -0.0211018  0.0197205  -1.070    0.285    
    UrbanYes         0.1228864  0.1129761   1.088    0.277    
    USYes           -0.1840928  0.1498423  -1.229    0.220    
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 1.019 on 388 degrees of freedom
    Multiple R-squared:  0.8734,	Adjusted R-squared:  0.8698 
    F-statistic: 243.4 on 11 and 388 DF,  p-value: < 2.2e-16
    ```
    
    > `CompPrice`, `Income`, `Advertising`, `Price`, `ShelveLocGood`, `ShelveLocMedium`, `Age`, opierając się na $p$-value > 0.05

    (e) On the basis of your response to the previous question, fit a smaller model that only uses the predictors for which there is evidence of association with the outcome.

    ```R
    > carseats_lm2 = lm(Sales~.-Education-Urban-US-Population,data=Carseats)
    > summary(carseats_lm2)

    Call:
    lm(formula = Sales ~ . - Education - Urban - US - Population, 
        data = Carseats)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -2.7728 -0.6954  0.0282  0.6732  3.3292 

    Coefficients:
                     Estimate Std. Error t value Pr(>|t|)    
    (Intercept)      5.475226   0.505005   10.84   <2e-16 ***
    CompPrice        0.092571   0.004123   22.45   <2e-16 ***
    Income           0.015785   0.001838    8.59   <2e-16 ***
    Advertising      0.115903   0.007724   15.01   <2e-16 ***
    Price           -0.095319   0.002670  -35.70   <2e-16 ***
    ShelveLocGood    4.835675   0.152499   31.71   <2e-16 ***
    ShelveLocMedium  1.951993   0.125375   15.57   <2e-16 ***
    Age             -0.046128   0.003177  -14.52   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 1.019 on 392 degrees of freedom
    Multiple R-squared:  0.872,	Adjusted R-squared:  0.8697 
    F-statistic: 381.4 on 7 and 392 DF,  p-value: < 2.2e-16
    ```
    
    (f) How well do the models in (a) and (e) fit the data?

    > Statystyka $R^2$ adjusted wzrosła znacząco z 0.23 w (a) do 0.86 w (e). F-statistic również zwiększyło się. Oznacza to, że nowy model jest lepszy.
    
    (g) Using the model from (e), obtain 95 % confidence intervals for the coefficient(s).
    
    ```R
    > confint(carseats_lm2)
                          2.5 %      97.5 %
    (Intercept)      4.48236820  6.46808427
    CompPrice        0.08446498  0.10067795
    Income           0.01217210  0.01939784
    Advertising      0.10071856  0.13108825
    Price           -0.10056844 -0.09006946
    ShelveLocGood    4.53585700  5.13549250
    ShelveLocMedium  1.70550103  2.19848429
    Age             -0.05237301 -0.03988204
    ```
    
    (h) Is there evidence of outliers or high leverage observations in the model from (e)?

    ```R
    par(mfrow=c(2,2))
    plot(carseats_lm2)
    ```

    ![](img/03_10h.png)

    > * Residuals v leverage - wskazuje, że jakaś obserwacja ma duży wpływ na model.

    ```R
    > hatvalues(carseats_lm2)[order(hatvalues(carseats_lm2), decreasing = T)][1]

           311 
    0.06154635
    ```

    > * Scale-Location - wskazuje, że mogą występować pewne obserwacje odstające.

    ```R
    > rstudent(carseats_lm2)[which(rstudent(carseats_lm2)>3)]

        358 
    3.34075 
    ```

11. In this problem we will investigate the t-statistic for the null hypothesis $H_0 : \beta = 0$ in simple linear regression without an intercept. To begin, we generate a predictor `x` and a response `y` as follows.

    ```R
    > set.seed(1)
    > x <- rnorm(100)
    > y <- 2 * x + rnorm(100)
    ```

    (a) Perform a simple linear regression of `y` onto `x`, _without_ an intercept. Report the coefficient estimate $\hat{\beta}$, the standard error of this coefficient estimate, and the $t$-statistic and $p$-value associated with the null hypothesis $H_0 : \beta = 0$. Comment on these results. (You can perform regression without an intercept using the command `lm(y~x+0)`.)

    ```R
    > set.seed(1)
    > x <- rnorm(100)
    > y <- 2 * x + rnorm(100)
    > lm.fit <- lm(y~x+0)
    > summary(lm.fit)

    Call:
    lm(formula = y ~ x + 0)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -1.9154 -0.6472 -0.1771  0.5056  2.3109 

    Coefficients:
      Estimate Std. Error t value Pr(>|t|)    
    x   1.9939     0.1065   18.73   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 0.9586 on 99 degrees of freedom
    Multiple R-squared:  0.7798,	Adjusted R-squared:  0.7776 
    F-statistic: 350.7 on 1 and 99 DF,  p-value: < 2.2e-16
    ```
    
    (b) Now perform a simple linear regression of `x` onto `y` _without_ an intercept, and report the coeﬀicient estimate, its standard error, and the corresponding $t$-statistic and $p$-values associated with the null hypothesis $H_0 : \beta = 0$. Comment on these results.

    ```R
    > lm.fit2 = lm(x~y+0)
    > summary(lm.fit2)

    Call:
    lm(formula = x ~ y + 0)

    Residuals:
        Min      1Q  Median      3Q     Max 
    -0.8699 -0.2368  0.1030  0.2858  0.8938 

    Coefficients:
      Estimate Std. Error t value Pr(>|t|)    
    y  0.39111    0.02089   18.73   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    Residual standard error: 0.4246 on 99 degrees of freedom
    Multiple R-squared:  0.7798,	Adjusted R-squared:  0.7776 
    F-statistic: 350.7 on 1 and 99 DF,  p-value: < 2.2e-16
    ```
    
    (c) What is the relationship between the results obtained in (a) and (b)?
    
    > W modelu zostały zamienione osie więc statystyki testowe mają takie same wartości podobnie jak R-squared i Adjusted R-squared.

    (d) For the regression of Y onto X without an intercept, the $t$-statistic for $H_0 : \beta = 0$ takes the form $\hat{\beta}/SE(\hat{\beta})$, where $\hat{\beta}$ is given by (3.38), and where

    $$SE(\hat{\beta}) = \sqrt{\frac{\sum_{i=1}^n (y_i - x_i\hat{\beta})^2}{(n-1)\sum_{i'=1}^n x_{i'}^2}}$$
    
    (These formulas are slightly different from those given in Sections 3.1.1 and 3.1.2, since here we are performing regression without an intercept.) Show algebraically, and confirm numerically in `R`, that the $t$-statistic can be written as

    > $$\frac{(\sqrt{n-1})\sum_{i=1}^n x_iy_i}{\sqrt{\left(\sum_{i=1}^n x_i^2\right)\left(\sum_{i'=1}^n y_{i'}^2\right) - \left(\sum_{i'=1}^n x_{i'}y_{i'}\right)^2}}$$
    >
    > $$\begin{aligned}t^2 &= \frac{\hat{\beta}^2}{SE^2(\hat{\beta})} = \frac{(n-1)\sum_{i'=1}^n x_{i'}^2\hat{\beta}^2}{\sum_{i=1}^n (y_i - x_i\hat{\beta})^2} = \\
    &= \frac{(n-1)\sum_{i'=1}^n x_{i'}^2\hat{\beta}^2}{\sum_{i=1}^n (y_i^2 - 2y_ix_i\hat{\beta} + x_i^2\hat{\beta}^2)} = \\
    &= \frac{(n-1)\sum_{i'=1}^n x_{i'}^2\hat{\beta}^2}{\sum_{i=1}^ny_i^2 - 2\sum_{i=1}^ny_ix_i\hat{\beta} + \sum_{i=1}^nx_i^2\hat{\beta}^2} = \\
    &= \frac{(n-1)\sum_{i'=1}^n x_{i'}^2\frac{\left(\sum_{i=1}^nx_iy_i \right)^2}{\left(\sum_{i'=1}^nx_{i'}^2 \right)^2}}{\sum_{i=1}^ny_i^2 - 2\sum_{i=1}^ny_ix_i\frac{\sum_{i=1}^nx_iy_i}{\sum_{i'=1}^nx_{i'}^2} + \sum_{i=1}^nx_i^2\frac{\left(\sum_{i=1}^nx_iy_i \right)^2}{\left(\sum_{i'=1}^nx_{i'}^2 \right)^2}} = \\
    &= \frac{(n-1)\frac{\left(\sum_{i=1}^nx_iy_i \right)^2}{\sum_{i'=1}^nx_{i'}^2}}{\frac{\sum_{i'=1}^nx_{i'}^2\sum_{i=1}^ny_i^2}{\sum_{i'=1}^nx_{i'}^2} - 2\frac{\left(\sum_{i=1}^nx_iy_i\right)^2}{\sum_{i'=1}^nx_{i'}^2} + \frac{\left(\sum_{i=1}^nx_iy_i \right)^2}{\sum_{i'=1}^nx_{i'}^2}} = \\
    &= \frac{(n-1)\frac{\left(\sum_{i=1}^nx_iy_i \right)^2}{\sum_{i'=1}^nx_{i'}^2}}{\frac{\sum_{i'=1}^nx_{i'}^2\sum_{i=1}^ny_i^2}{\sum_{i'=1}^nx_{i'}^2} - \frac{\left(\sum_{i=1}^nx_iy_i\right)^2}{\sum_{i'=1}^nx_{i'}^2}} = \\
    &= \frac{(n-1)\left(\sum_{i=1}^nx_iy_i \right)^2}{\sum_{i'=1}^nx_{i'}^2\sum_{i=1}^ny_i^2 - \left(\sum_{i=1}^nx_iy_i\right)^2}\end{aligned}$$
    >
    > $$t = \frac{(\sqrt{n-1})\sum_{i=1}^n x_iy_i}{\sqrt{\left(\sum_{i'=1}^n x_{i'}^2\right)\left(\sum_{i=1}^n y_{i}^2\right) - \left(\sum_{i=1}^n x_{i}y_{i'}\right)^2}}$$

    ```R
    > numerator = sqrt(length(x)-1)*sum(x*y)
    > denumerator = sqrt(sum(x^2)*sum(y^2) - sum(x*y)^2)
    > t_statistic = numerator/denumerator
    > t_statistic

    [1] 18.72593
    ```

    > Wyszło tyle co w modelu.

    (e) Using the results from (d), argue that the $t$-statistic for the regression of `y` onto `x` is the same as the $t$-statistic for the regression of `x` onto `y`.

    > Widać od razu, że zamiana `x` z `y` da ten sam wzór końcowy.
    
    (f) In `R`, show that when regression is performed _with_ an intercept, the $t$-statistic for $H_0 : \beta_1 = 0$ is the same for the regression of `y` onto `x` as it is for the regression of `x` onto `y`.

    ```R
    > lm.fit3 = lm(y~x)
    > summary(lm.fit3)$coefficients[2,3]

    [1] 18.5556

    > lm.fit4 = lm(x~y)
    > summary(lm.fit4)$coefficients[2,3]

    [1] 18.5556
    ```

12. This problem involves simple linear regression without an intercept.

    (a) Recall that the coefficient estimate $\hat{\beta}$ for the linear regression of $Y$ onto $X$ without an intercept is given by (3.38). Under what circumstance is the coefficient estimate for the regression of $X$ onto $Y$ the same as the coefficient estimate for the regression of $Y$ onto $X$?

    > $$\hat{\beta}_x = \frac{\sum_{i=1}^nx_iy_i}{\sum_{i=1}^nx_i^2}$$
    >
    > $$\hat{\beta}_y = \frac{\sum_{i=1}^nx_iy_i}{\sum_{i=1}^ny_i^2}$$
    >$\hat{\beta}_x = \hat{\beta}_y$, gdy $\sum_{i=1}^nx_i^2 = \sum_{i=1}^ny_i^2$
    
    (b) Generate an example in `R` with $n = 100$ observations in which the coefficient estimate for the regression of $X$ onto $Y$ is different from the coefficient estimate for the regression of $Y$ onto $X$.

    ```R
    > set.seed(1)
    > x <- rnorm(100)
    > y <- 2 * x + rnorm(100)
    ```
    
    (c) Generate an example in `R` with $n = 100$ observations in which the coefficient estimate for the regression of $X$ onto $Y$ is the same as the coefficient estimate for the regression of $Y$ onto $X$.

    ```R
    set.seed(1)
    x <- rnorm(100)
    y <- sample(x) # sample miesza liczby z x, lepiej widać, że wystarczy, że suma obserwacji jest równa żeby dostać ten sam współczynnik
    ```