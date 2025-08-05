---
layout: math
title: 07 Moving Beyond Linearity
parent: Modelowanie
nav_order: 6
---

# Moving Beyond Linearity

1. It was mentioned in the chapter that a cubic regression spline with one knot at $\xi$ can be obtained using a basis of the form $x$, $x^2$, $x^3$, $(x − \xi)^3_+ = (x - \xi)^3$ if $x > \xi$ and equals 0 otherwise. We will now show that a function of the form 

    $$f(x) = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3 + \beta_4(x − \xi)^3_+$$

    is indeed a cubic regression spline, regardless of the values of $\beta_0$, $\beta_1$, $\beta_2$, $\beta_3$, $\beta_4$.

    _Hint: Parts (d) and (e) of this problem require knowledge of single-variable calculus. As a reminder, given a cubic polynomial_
    
    $$f_1(x) = a_1 + b_1x + c_1x^2 + d_1x^3$$

    _the first derivative takes the form_

    $$f'_1(x) = b_1 + 2c_1x + 3d_1x^2$$

    _and the second derivative takes the form_

    $$f''_1(x) = 2c_1 + 6d_1x.$$

    (a) Find a cubic polynomial 
    
    $$f_1(x) = a_1 + b_1x + c_1x^2 + d_1x^3$$
    
    such that $f(x) = f_1(x)$ for all $x \le \xi$. Express $a_1$, $b_1$, $c_1$, $d_1$ in terms of $\beta_0$, $\beta_1$, $\beta_2$, $\beta_3$, $\beta_4$.

    > Dla $x \le \xi$, wyraz $(x − \xi)^3_+$ jest równy $0$, stąd: 
    >
    > $$f(x) = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3$$
    > 
    > $$a_1 + b_1x + c_1x^2 + d_1x^3 = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3$$
    >
    > $$a_1 = \beta_0$$
    >
    > $$b_1 = \beta_1$$
    >
    > $$c_1 = \beta_2$$
    >
    > $$d_1 = \beta_3$$

    (b) Find a cubic polynomial 
    
    $$f_2(x) = a_2 + b_2x + c_2x^2 + d_2x^3$$

    such that $f(x) = f_2(x)$ for all $x > \xi$. Express $a_2$, $b_2$, $c_2$, $d_2$ in terms of $\beta_0$, $\beta_1$, $\beta_2$, $\beta_3$, $\beta_4$. We have now established that $f(x)$ is a piecewise polynomial.

    > Dla $x > \xi$, wyraz $(x − \xi)^3_+$ jest zdefiniowany jako $(x - \xi)^3$, stąd:
    >
    > $$f(x) = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3 + \beta_4(x - \xi)^3$$
    >
    > $$f(x) = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3 + \beta_4(x^3 - 3\xi x^2 + 3\xi^2 x - \xi^3)$$
    >
    > $$f(x) = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3 + \beta_4x^3 - 3\beta_4\xi x^2 + 3\beta_4\xi^2 x - \beta_4\xi^3$$
    >
    > $$f(x) = (\beta_0 - \beta_4\xi^3) + (\beta_1 + 3\beta_4\xi^2)x + (\beta_2 - 3\beta_4\xi)x^2 + (\beta_3 + \beta_4)x^3$$
    >
    > Porównując to z postacią $f_2(x) = a_2 + b_2x + c_2x^2 + d_2x^3$, dostajemy:
    >
    > $$a_2 = \beta_0 - \beta_4\xi^3$$
    >
    > $$b_2 = \beta_1 + 3\beta_4\xi^2$$
    >
    > $$c_2 = \beta_2 - 3\beta_4\xi$$
    >
    > $$d_2 = \beta_3 + \beta_4$$

    (c) Show that $f_1(\xi) = f_2(\xi)$. That is, $f(x)$ is continuous at $\xi$.

    > $$f_1(\xi) = \beta_0 + \beta_1\xi + \beta_2\xi^2 + \beta_3\xi^3$$
    > 
    > $$f_2(\xi) = (\beta_0 - \beta_4\xi^3) + (\beta_1 + 3\beta_4\xi^2)\xi + (\beta_2 - 3\beta_4\xi)\xi^2 + (\beta_3 + \beta_4)\xi^3$$
    >
    > $$f_2(\xi) = \beta_0 - \beta_4\xi^3 + \beta_1\xi + 3\beta_4\xi^3 + \beta_2\xi^2 - 3\beta_4\xi^3 + \beta_3\xi^3 + \beta_4\xi^3$$
    >
    > $$f_2(\xi) = \beta_0 + \beta_1\xi + \beta_2\xi^2 + \beta_3\xi^3 = f_1(\xi)$$

    (d) Show that $f'_1(\xi) = f'_2(\xi)$. That is, $f'(x)$ is continuous at $\xi$.

    > $$f'_1(x) = \beta_1 + 2\beta_2x + 3\beta_3x^2$$
    > 
    > $$f'_2(x) = b_2 + 2c_2x + 3d_2x^2$$
    >
    > $$f'_2(\xi) = (\beta_1 + 3\beta_4\xi^2) + 2(\beta_2 - 3\beta_4\xi)\xi + 3(\beta_3 + \beta_4)\xi^2$$
    > 
    > $$f'_2(\xi) = \beta_1 + 3\beta_4\xi^2 + 2\beta_2\xi - 6\beta_4\xi^2 + 3\beta_3\xi^2 + 3\beta_4\xi^2$$
    > 
    > $$f'_2(\xi) = \beta_1 + 2\beta_2\xi + 3\beta_3\xi^2 = f'_1(\xi)$$

    (e) Show that $f_1''(\xi) = f_2''(\xi)$. That is, $f\'\'(x)$ is continuous at $\xi$.

    > $$f''_1(x) = 2\beta_2 + 6\beta_3x$$
    > 
    > $$f''_2(x) = 2c_2 + 6d_2x$$
    > 
    > $$f''_2(\xi) = 2(\beta_2 - 3\beta_4\xi) + 6(\beta_3 + \beta_4)\xi$$
    > 
    > $$f''_2(\xi) = 2\beta_2 - 6\beta_4\xi + 6\beta_3\xi + 6\beta_4\xi$$
    > 
    > $$f''_2(\xi) = 2\beta_2 + 6\beta_3\xi = f''_1(\xi)$$

    Therefore, $f(x)$ is indeed a cubic spline.

3. Suppose that a curve $\hat{g}$ is computed to smoothly fit a set of $n$ points using the following formula:

    $$ \hat{g} = \arg\underset{g}{\min} \left( \sum_{i=1}^{n} (y_i - g(x_i))^2 + \lambda \int \left[g^{(m)}(x)\right]^2 dx \right), $$

    where $g^{(m)}$ represents the $m$th derivative of $g$ (and $g^{(0)} = g$). Provide example sketches of $\hat{g}$ in each of the following scenarios.

    > Celem jest znalezienie funkcji $g$, która minimalizuje:
    >
    > $$ \sum_{i=1}^{n} (y_i - g(x_i))^2 + \lambda \int [g^{(0)}(x)]^2 dx $$

    (a) $\lambda = \infty, m = 0$.

    > Ponieważ $\lambda = \infty$ musimy zająć się drugim członem w powyższym wyrażeniu.
    >
    > $m=0$, więc $g^{(0)}(x) = g(x)$. 
    >
    > Aby zminimalizować całe wyrażenie, całka z funkcji $[g(x)]^2$ musi być równa zero. Dla $g(x) = 0$ powyższy warunek jest spełniony stąd, $\hat{g} = 0$.

    (b) $\lambda = \infty, m = 1$.

    > Ponieważ $\lambda = \infty$ musimy zająć się drugim członem w powyższym wyrażeniu.
    >
    > Aby zminimalizować całe wyrażenie, całka z funkcji $[g^{(1)}(x)]^2$ musi być równa zero. Dla $g^{(1)}(x) = 0$ powyższy warunek jest spełniony, czyli funkcja $g$ musi mieć zerowe nachylenie stąd, $\hat{g}$ może być dowolną linią poziomą.

    (c) $\lambda = \infty, m = 2$.

    > Ponieważ $\lambda = \infty$ musimy zająć się drugim członem w powyższym wyrażeniu.
    >
    > Aby zminimalizować całe wyrażenie, całka z funkcji $[g^{(2)}(x)]^2$ musi być równa zero. Dla $g^{(2)}(x) = 0$ powyższy warunek jest spełniony, czyli funkcja $g^{(1)}(x)$ musi mieć zerowe nachylenie czyli może to być linia pozioma. Funkcja $g$ musi mieć więc jednostajne nachylenie stąd, $\hat{g}$ może być linią nachyloną pod dowolnym kątem.

    (d) $\lambda = \infty, m = 3$.

    > Ponieważ $\lambda = \infty$ musimy zająć się drugim członem w powyższym wyrażeniu.
    >
    > Aby zminimalizować całe wyrażenie, całka z funkcji $[g^{(3)}(x)]^2$ musi być równa zero. Dla $g^{(3)}(x) = 0$ powyższy warunek jest spełniony, czyli funkcja $g^{(2)}(x)$ musi mieć zerowe nachylenie czyli może to być linia pozioma. Funkcja $g^{(1)}(x)$ musi mieć więc jednostajne nachylenie, może być linią nachyloną pod dowolnym kątem. Funkcja $g$ musi mieć więc zmienne nachylenie stąd, $\hat{g}$ może być funkcją kwadratową.

    (e) $\lambda = 0, m = 3$.

    > Ponieważ $\lambda = 0$ to drugi człon znika.
    >
    > W tym przypadku trzeba zminimalizować pierwszy człon, w tym celu można użyć funkcji wielomianowej, stąd $\hat{g}$ jest funkcją wielomianową stopnia co najwyżej $n-1$, która będzie przechodzić przez wszystkie punkty.

3. Suppose we fit a curve with basis functions $b_1(X) = X$, $b_2(X) = (X-1)^2I(X \ge 1)$. (Note that $I(X \ge 1)$ equals 1 for $X \ge 1$ and 0 otherwise.) We fit the linear regression model

    $$ Y = \beta_0 + \beta_1 b_1(X) + \beta_2 b_2(X) + \epsilon, $$

    and obtain coefficient estimates $\hat{\beta}_0 = 1$, $\hat{\beta}_1 = 1$, $\hat{\beta}_2 = -2$. Sketch the estimated curve between $X = -2$ and $X = 2$. Note the intercepts, slopes, and other relevant information.

    ```R
    x <- seq(-2, 2, length.out = 1000)
    f <- function(x) 1 + x + -2 * (x - 1)^2 * I(x >= 1)
    plot(x, f(x), type = "l")
    grid()
    ```

    ![](img/07_3.png)

4. Suppose we fit a curve with basis functions $b_1(X) = I(0 \le X \le 2) - (X-1)I(1 \le X \le 2)$, $b_2(X) = (X-3)I(3 \le X \le 4) + I(4 < X \le 5)$. We fit the linear regression model
    $$ Y = \beta_0 + \beta_1 b_1(X) + \beta_2 b_2(X) + \epsilon, $$

    and obtain coefficient estimates $\hat{\beta}_0 = 1$, $\hat{\beta}_1 = 1$, $\hat{\beta}_2 = 3$. Sketch the estimated curve between $X = -2$ and $X = 6$. Note the intercepts, slopes, and other relevant information.

    ```R
    x <- seq(-2, 6, length.out = 1000)
    b1 <- function(x) I(0 <= x & x <= 2) - (x - 1) * I(1 <= x & x <= 2)
    b2 <- function(x) (x - 3) * I(3 <= x & x <= 4) + I(4 < x & x <= 5)
    f <- function(x) 1 + 1 * b1(x) + 3 * b2(x)
    plot(x, f(x), type = "l")
    grid()
    ```

    ![](img/07_4.png)

5. Consider two curves, $\hat{g}_1$ and $\hat{g}_2$, defined by

    $$ \hat{g}_1 = \arg\underset{g}{\min} \left( \sum_{i=1}^{n} (y_i - g(x_i))^2 + \lambda \int \left[g^{(3)}(x)\right]^2 dx \right), $$

    $$ \hat{g}_2 = \arg\underset{g}{\min} \left( \sum_{i=1}^{n} (y_i - g(x_i))^2 + \lambda \int \left[g^{(4)}(x)\right]^2 dx \right), $$
    
    where $g^{(m)}$ represents the $m$th derivative of $g$.

    (a) As $\lambda \to \infty$, will $\hat{g}_1$ or $\hat{g}_2$ have the smaller training RSS?

    > $\hat{g}_2$ jest bardziej elastyczne dlatego, że korzysta z pochodnej wyższego rzędu, dlatego będzie miało mniejsze RSS na zbiorze treningowym.

    (b) As $\lambda \to \infty$, will $\hat{g}_1$ or $\hat{g}_2$ have the smaller test RSS?

    > Nie można tego stwierdzić bez zbioru testowego.

    (c) For $\lambda = 0$, will $\hat{g}_1$ or $\hat{g}_2$ have the smaller training and test RSS?

    > RSS będzie taki sam dla obu funkcji, bo drugi człon wynosi 0.

6. In this exercise, you will further analyze the `Wage` data set considered throughout this chapter.

    (a) Perform polynomial regression to predict `wage` using `age`. Use cross-validation to select the optimal degree d for the polynomial. What degree was chosen, and how does this compare to the results of hypothesis testing using ANOVA? Make a plot of the resulting polynomial fit to the data.

    ```R
    library(ISLR2)
    library(boot)
    attach(Wage)

    cv.error <- rep(0, 10)
    for (i in 1:10) {
    glm.fit <- glm(wage ~ poly(age, i), data = Wage)
    cv.error[i] <- cv.glm(Wage, glm.fit, K = 10)$delta[1]
    }
    cv.error
    ```

    ```R
    [1] 1676.826 1600.763 1598.399 1595.651 1594.977 1596.061 1594.298
    [8] 1598.134 1593.913 1595.950
    ```

    ```R
    plot(cv.error, type="b", xlab="Degree", ylab="CV Error")
    ```

    ![](img/07_6a.png)

    > Nie widać poprawy modelu powyżej wielomianu 4 stopnia.

    ```R
    glm.fit = glm(wage ~ poly(age, 5), data = Wage)
    summary(glm.fit)
    ```

    ```R
    Call:
    glm(formula = wage ~ poly(age, 5), data = Wage)

    Coefficients:
                   Estimate Std. Error t value Pr(>|t|)    
    (Intercept)    111.7036     0.7288 153.278  < 2e-16 ***
    poly(age, 5)1  447.0679    39.9161  11.200  < 2e-16 ***
    poly(age, 5)2 -478.3158    39.9161 -11.983  < 2e-16 ***
    poly(age, 5)3  125.5217    39.9161   3.145  0.00168 ** 
    poly(age, 5)4  -77.9112    39.9161  -1.952  0.05105 .  
    poly(age, 5)5  -35.8129    39.9161  -0.897  0.36968    
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    (Dispersion parameter for gaussian family taken to be 1593.294)

        Null deviance: 5222086  on 2999  degrees of freedom
    Residual deviance: 4770322  on 2994  degrees of freedom
    AIC: 30642

    Number of Fisher Scoring iterations: 2
    ```

    > Na podstawie $p$-value 5 stopień wielomianu nie jest istotny statystycznie.

    ```R
    fit1 <- lm(wage ~ poly(age, 1), data = Wage)
    fit2 <- lm(wage ~ poly(age, 2), data = Wage)
    fit3 <- lm(wage ~ poly(age, 3), data = Wage)
    fit4 <- lm(wage ~ poly(age, 4), data = Wage)
    fit5 <- lm(wage ~ poly(age, 5), data = Wage)
    anova(fit1, fit2, fit3, fit4, fit5)
    ```

    ```R
    Analysis of Variance Table

    Model 1: wage ~ poly(age, 1)
    Model 2: wage ~ poly(age, 2)
    Model 3: wage ~ poly(age, 3)
    Model 4: wage ~ poly(age, 4)
    Model 5: wage ~ poly(age, 5)
    Res.Df     RSS Df Sum of Sq        F    Pr(>F)    
    1   2998 5022216                                    
    2   2997 4793430  1    228786 143.5931 < 2.2e-16 ***
    3   2996 4777674  1     15756   9.8888  0.001679 ** 
    4   2995 4771604  1      6070   3.8098  0.051046 .  
    5   2994 4770322  1      1283   0.8050  0.369682    
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    ```

    > Na podstawie $p$-value można stwierdzić, że model z wielomianem 5 stopnia nie jest istotny statystycznie. Ostatecznie trzeba wybrać model z wielomianem 4 stopnia.

    ```R
    agelims <- range(age)
    age.grid <- seq(from = agelims[1], to = agelims[2])
    preds <- predict(fit4, newdata = list(age = age.grid ), se = TRUE )
    se.bands <- cbind(preds$fit + 2 * preds$se.fit,
                      preds$fit - 2 * preds$se.fit)

    plot(age, wage, xlim = agelims, cex = .5, col = "darkgrey")
    title("Degree -4 Polynomial")
    lines(age.grid, preds$fit, lwd = 2, col = "blue")
    matlines(age.grid, se.bands, lwd = 1, col = "blue", lty = 3)
    ```

    ![](img/07_6a1.png)

    (b) Fit a step function to predict `wage` using `age`, and perform cross-validation to choose the optimal number of cuts. Make a plot of the fit obtained.

    ```R
    Wage_2 <- Wage
    attach(Wage_2)

    set.seed(1)
    cv.error = rep(0,9)
    for (i in 2:10) {
      Wage_2$age.cut = cut(age, i)
      step.fit = glm(wage ~ age.cut, data = Wage_2)
      cv.error[i-1] = cv.glm(Wage_2, step.fit, K=10)$delta[1]
    }
    cv.error
    ```

    ```R
    [1] 1734.489 1684.271 1635.552 1632.080 1623.415 1614.996 1601.318
    [8] 1613.954 1606.331
    ```

    ```R
    plot(2:10, cv.error, type="b", xlab="Index", ylab="CV Error")
    ```

    ![](img/07_6b.png)

    > Najmniejszy błąd dla 8 podziałów.

    ```R
    attach(Wage)
    step.fit <- glm(wage ~ cut(age, 8), data = Wage)

    preds <- predict(step.fit, newdata = list(age = age.grid), se = TRUE)
    se.bands <- cbind(preds$fit + 2 * preds$se.fit,
                      preds$fit - 2 * preds$se.fit)

    plot(age, wage, xlim = agelims, cex = .5, col = "darkgrey")
    title("Step function using 8 cuts")
    lines(age.grid, preds$fit, lwd = 2, col = "blue")
    matlines(age.grid, se.bands, lwd = 1, col = "blue", lty = 3)
    ```

    ![](img/07_6b1.png)