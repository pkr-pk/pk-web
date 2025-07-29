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
