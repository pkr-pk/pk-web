---
layout: math
title: 05 Resampling Methods
parent: Modelowanie
nav_order: 3
---

# Resampling Methods

1. Using basic statistical properties of the variance, as well as single variable calculus, derive (5.6). In other words, prove that α given by (5.6) does indeed minimize $Var(\alpha X + (1 − \alpha)Y)$.

    $$f(X) = Var(\alpha X + (1 − \alpha)Y) = $$
    
    $$= \alpha^2 Var(X) + (1-\alpha)^2 Var(Y) + 2\alpha(1-\alpha)Cov(X,Y) =$$

    $$= \alpha^2 \sigma_X^2 + (1-\alpha)^2 \sigma_Y^2 + 2\alpha(1-\alpha)\sigma_{XY}$$

    Obliczam pochodną po $\alpha$:

    $$f'(X)= 2 \alpha \sigma_X^2 - 2(1-\alpha) \sigma_Y^2 + 2(1-2\alpha)\sigma_{XY} =$$

    $$= 2 \alpha \sigma_X^2 - 2\sigma_Y^2 + 2\alpha\sigma_Y^2 + 2\sigma_{XY} - 4\alpha\sigma_{XY}$$

    Przyrównuję do zera:

    $$2 \alpha \sigma_X^2 + 2\alpha\sigma_Y^2 - 4\alpha\sigma_{XY} = 2\sigma_Y^2 - 2\sigma_{XY} /:2$$

    $$\alpha \sigma_X^2 + \alpha\sigma_Y^2 - 2\alpha\sigma_{XY} = \sigma_Y^2 - \sigma_{XY}$$

    $$\alpha (\sigma_X^2 + \sigma_Y^2 - 2\sigma_{XY}) = \sigma_Y^2 - \sigma_{XY}$$

    $$\alpha = \frac{\sigma_Y^2 - \sigma_{XY}}{\sigma_X^2 + \sigma_Y^2 - 2\sigma_{XY}}$$

2. We will now derive the probability that a given observation is part of a bootstrap sample. Suppose that we obtain a bootstrap sample from a set of $n$ observations.

    > Bootstrap to losowanie ze zwracaniem i będę korzystał z tej informacji w kolejnych podpunktach.
    
    (a) What is the probability that the first bootstrap observation is _not_ the $j$th observation from the original sample? Justify your answer.

    > $A$ - zdarzenie polegające na nie wylosowaniu $j$-tej obserwacji w pierwszym losowaniu.
    >
    > Prawdopodobieństwo wylosowania $j$-tej obserwacji w pierwszym losowaniu wynosi $1/n$ czyli korzystając ze zdarzenia przeciwnego: 
    >
    > $P(A) = 1-\frac{1}{n}$

    (b) What is the probability that the second bootstrap observation is _not_ the $j$th observation from the original sample?

    > $B$ - zdarzenie polegające na nie wylosowaniu $j$-tej obserwacji w drugim losowaniu.
    >
    > Prawdopodobieństwo wylosowania $j$-tej obserwacji w drugim losowaniu wynosi $1/n$ czyli korzystając ze zdarzenia przeciwnego: 
    >
    > $P(B) = 1-\frac{1}{n}$

    (c) Argue that the probability that the $j$th observation is _not_ in the bootstrap sample is $(1− 1/n)^n$.

    > $C$ - zdarzenie polegające na nie wylosowaniu $j$-tej w ogóle.
    >
    > Tutaj mamy prawdopodobieństwo, że $j$-ta obserwacja nie zostanie wylosowana w pierwszym losowaniu ani w drugim ani w trzecim itd.:
    >
    > $P(C) = (1-1/n)\cdot(1-1/n)\cdot...\cdot(1-1/n) = (1− 1/n)^n$

    (d) When $n = 5$, what is the probability that the $j$th observation is in the bootstrap sample?

    ```R
    prob <- function(n) {
      return(1-(1-1/n)^n)
    }

    prob(5)
    ```

    ```R
    [1] 0.67232
    ```

    (e) When $n = 100$, what is the probability that the $j$th observation is in the bootstrap sample?

    ```R
    prob(100)
    ```

    ```R
    [1] 0.6339677
    ```
    
    (f) When $n = 10000$, what is the probability that the $j$th observation is in the bootstrap sample?

    ```R
    prob(10000)
    ```

    ```R
    [1] 0.632139
    ```
    
    (g) Create a plot that displays, for each integer value of $n$ from $1$ to $100000$, the probability that the $j$th observation is in the bootstrap sample. Comment on what you observe.

    ```R
    plot(1:100000, prob(1:100000), xlab = "Index", ylab = "Probs", log = "xy")
    ```

    ![](img/05_2g.png)

    > Prawdopodobieństwo dąży do wartości 0.63.
    >
    > $\lim\limits_{n \to \infty} 1 - (1-\frac{1}{n})^n = 1-e^{-1} \approx 0.63$

    (h) We will now investigate numerically the probability that a bootstrap sample of size $n = 100$ contains the $j$th observation. Here $j = 4$. We repeatedly create bootstrap samples, and each time we record whether or not the fourth observation is contained in the bootstrap sample.

    ```R
    > store <- rep(NA , 10000)
    > for(i in 1:10000) {
        store[i] <- sum(sample (1:100 , rep=TRUE) == 4) > 0
    }
    > mean(store)
    ```

    Comment on the results obtained.

    ```R
    [1] 0.6339
    ```

    > Zgodnie z oczekiwaniem prawdopodobieństwo jest bliskie 0.63.

3. We now review $k$-fold cross-validation.
    
    (a) Explain how $k$-fold cross-validation is implemented.

    > W walidacji $k$-fold zbiór danych treningowych jest losowo dzielony na $k$ grup o jednakowym rozmiarze. Pierwsza grupa jest traktowana jako zbiór testowy, model jest dopasowywany do pozostałych $k-1$ grup, są to zbiory treningowe. MSE jest obliczane używając zbioru testowego. Procedura jest powtarzana $k$ razy, za każdym podejściem zbiór testowy i zbiory treningowe są inne. Ostatecznie obliczany jest średni MSE i jest to wynik końcowy procedury.

    (b) What are the advantages and disadvantages of $k$-fold cross-validation relative to:
    
    i. The validation set approach?

    > W tym przypadku trenujemy model na małej porcji danych, ponieważ musimy podzielić dane na zbiór treningowy i testowy. Może to powodować zawyżenie test error rate. Metoda jest też czuła na to które dane znajdą się w zbiorze treningowym i testowym. Zaletą jest niski koszt obliczeniowy dzięki czemu zyskujemy na szybkości.
    
    ii. LOOCV?

    > W tym przypadku trenujemy model na $n-1$ obserwacjach, kolejne modele są jednak trenowane na bardzo podobnych zbiorach bo za każdym razem usuwamy tylko jedną obserwację. W rezultacie LOOCV może mieć wysoką wariancję, kolejną wadą jest też wysoki koszt obliczeniowy.

4. Suppose that we use some statistical learning method to make a prediction for the response $Y$ for a particular value of the predictor $X$. Carefully describe how we might estimate the standard deviation of our prediction.

    Możemy w tym celu użyć metody bootstrap. Procedura polegna na wielokrotnym próbkowaniu zbioru danych i trenowaniu modelu. Na podstawie dopasowanych modeli możemy za każdym razem obliczyć odchylenie standardowe. Końcowym rezultatem będzie uśrednione odchylenie standardowe.

5. In Chapter 4, we used logistic regression to predict the probability of `default` using `income` and `balance` on the `Default` data set. We will now estimate the test error of this logistic regression model using the validation set approach. Do not forget to set a random seed before beginning your analysis.
    
    (a) Fit a logistic regression model that uses `income` and `balance` to predict `default`.

    ```R
    library(ISLR2)
    attach(Default)

    fit.log <- glm(default ~ income + balance, data = Default,
                   family = binomial)
    fit.log.pred <- predict(fit.log, Default, type = "response") > 0.5
    t <- table(fit.log.pred, Default$default)
    sum(diag(t)) / sum(t)
    ```

    ```R
    [1] 0.9737
    ```
    
    (b) Using the validation set approach, estimate the test error of this model. In order to do this, you must perform the following steps:
    
    i. Split the sample set into a training set and a validation set.
    
    ii. Fit a multiple logistic regression model using only the training observations.
    
    iii. Obtain a prediction of default status for each individual in the validation set by computing the posterior probability of default for that individual, and classifying the individual to the `default` category if the posterior probability is greater than 0.5.
    
    iv. Compute the validation set error, which is the fraction of the observations in the validation set that are misclassified.

    ```R
    set.seed(1)
    train <- sample(nrow(Default), nrow(Default) / 2)

    fit.log <- glm(default ~ income + balance, data = Default[train, ],
                   family = binomial)
    fit.log.pred <- predict(fit.log, Default[-train, ], type = "response") > 0.5
    t <- table(fit.log.pred, Default[-train, ]$default)
    sum(diag(t)) / sum(t)
    ```

    ```R
    [1] 0.9746
    ```
    
    (c) Repeat the process in (b) three times, using three different splits of the observations into a training set and a validation set. Comment on the results obtained.

    ```R
    set.seed(12)
    train <- sample(nrow(Default), nrow(Default) / 2)

    fit.log <- glm(default ~ income + balance, data = Default[train, ],
                   family = binomial)
    fit.log.pred <- predict(fit.log, Default[-train, ], type = "response") > 0.5
    t <- table(fit.log.pred, Default[-train, ]$default)
    sum(diag(t)) / sum(t)
    ```

    ```R
    [1] 0.973
    ```

    ```R
    set.seed(123)
    train <- sample(nrow(Default), nrow(Default) / 2)

    fit.log <- glm(default ~ income + balance, data = Default[train, ],
                   family = binomial)
    fit.log.pred <- predict(fit.log, Default[-train, ], type = "response") > 0.5
    t <- table(fit.log.pred, Default[-train, ]$default)
    sum(diag(t)) / sum(t)
    ```

    ```R
    [1] 0.9724
    ```

    ```R
    set.seed(1234)
    train <- sample(nrow(Default), nrow(Default) / 2)

    fit.log <- glm(default ~ income + balance, data = Default[train, ],
                   family = binomial)
    fit.log.pred <- predict(fit.log, Default[-train, ], type = "response") > 0.5
    t <- table(fit.log.pred, Default[-train, ]$default)
    sum(diag(t)) / sum(t)
    ```

    ```R
    [1] 0.9748
    ```

    > Wynik za każdym razem się zmienia bo zależy od wyboru zbioru treningowego i testowego.
    
    (d) Now consider a logistic regression model that predicts the probability of `default` using `income`, `balance`, and a dummy variable for `student`. Estimate the test error for this model using the validation set approach. Comment on whether or not including a dummy variable for `student` leads to a reduction in the test error rate.

    ```R
    set.seed(1)
    train <- sample(nrow(Default), nrow(Default) / 2)

    fit.log <- glm(default ~ income + balance + student, data = Default[train, ],
                   family = binomial)
    fit.log.pred <- predict(fit.log, Default[-train, ], type = "response") > 0.5
    t <- table(fit.log.pred, Default[-train, ]$default)
    sum(diag(t)) / sum(t)
    ```

    ```R
    [1] 0.974
    ```

    > Można powtórzyć dopasowanie kilka razy dla różnych ziaren ale wprowadzenie dodatkowej zmiennej do modelu nie powoduje widocznej poprawy.

6. We continue to consider the use of a logistic regression model to predict the probability of `default` using `income` and `balance` on the `Default` data set. In particular, we will now compute estimates for the standard errors of the `income` and `balance` logistic regression coefficients in two different ways: (1) using the bootstrap, and (2) using the standard formula for computing the standard errors in the `glm()` function. Do not forget to set a random seed before beginning your analysis.

    (a) Using the `summary()` and `glm()` functions, determine the estimated standard errors for the coefficients associated with `income` and `balance` in a multiple logistic regression model that uses both predictors.
    
    (b) Write a function, `boot.fn()`, that takes as input the `Default` data set as well as an index of the observations, and that outputs the coefficient estimates for `income` and `balance` in the multiple logistic regression model.
    
    (c) Use the `boot()` function together with your `boot.fn()` function to estimate the standard errors of the logistic regression coefficients for `income` and `balance`.
    
    (d) Comment on the estimated standard errors obtained using the `glm()` function and using your bootstrap function.