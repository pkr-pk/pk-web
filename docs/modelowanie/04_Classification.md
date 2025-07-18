---
layout: math
title: 04 Classification
parent: Modelowanie
nav_order: 3
---

# Classification

1. Using a little bit of algebra, prove that (4.2) is equivalent to (4.3). In other words, the logistic function representation and logit representation for the logistic regression model are equivalent.

    $$p(X)=\frac{e^{\beta_0+\beta_1 X}}{1+e^{\beta_0+\beta_1 X}}$$

    $$p(X) + p(X)e^{\beta_0+\beta_1 X}=e^{\beta_0+\beta_1 X}$$

    $$p(X) =e^{\beta_0+\beta_1 X} - p(X)e^{\beta_0+\beta_1 X}$$

    $$p(X) =e^{\beta_0+\beta_1 X}(1-p(X))$$

    $$\frac{p(X)}{1-p(X)} =e^{\beta_0+\beta_1 X}$$

2. It was stated in the text that classifying an observation to the class for which (4.17) is largest is equivalent to classifying an observation to the class for which (4.18) is largest. Prove that this is the case. In other words, under the assumption that the observations in the kth class are drawn from a $N (\mu_k , \sigma^2)$ distribution, the Bayes classifier assigns an observation to the class for which the discriminant function is maximized.

    $$p_k(x)=\frac{\pi_k \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_k\right)^2\right)}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_l\right)^2\right)}$$

    $$p_k(x)=\frac{\pi_k \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x^2-2x\mu_k + \mu_k^2\right)\right)}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_l\right)^2\right)}$$

    $$p_k(x)=\frac{\frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{x^2}{2 \sigma^2}\right)}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_l\right)^2\right)} \cdot \pi_k \exp \left(\frac{x\mu_k}{\sigma^2}-\frac{\mu_k^2}{2\sigma^2}\right)$$

    Czynnik niezależny od $k$:

    $$c=\frac{\frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{x^2}{2 \sigma^2}\right)}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_l\right)^2\right)}$$

    $$p_k(x)=c \pi_k \exp \left(\frac{x\mu_k}{\sigma^2}-\frac{\mu_k^2}{2\sigma^2}\right)$$

    Logarytmowanie:

    $$\ln[p_k(x)]=\ln(c) +  \ln(\pi_k) + \frac{x\mu_k}{\sigma^2} - \frac{\mu_k^2}{2\sigma^2}$$

    Ostatecznie:

    $$\delta_k(x)=x\frac{\mu_k}{\sigma^2} - \frac{\mu_k^2}{2\sigma^2} + \ln(\pi_k)$$

3. This problem relates to the QDA model, in which the observations within each class are drawn from a normal distribution with a class specific mean vector and a class specific covariance matrix. We consider the simple case where $p = 1$; i.e. there is only one feature.

    Suppose that we have $K$ classes, and that if an observation belongs to the $k$th class then $X$ comes from a one-dimensional normal distribution, $X ∼ N(\mu_k, \sigma_k^2)$. Recall that the density function for the one-dimensional normal distribution is given in (4.16). Prove that in this case, the Bayes classifier is not linear. Argue that it is in fact quadratic.

    _Hint: For this problem, you should follow the arguments laid out in Section 4.4.1, but without making the assumption that $\sigma^2_1 =\ldots= \sigma_K^2$._

    $$p_k(x)=\frac{\pi_k \frac{1}{\sqrt{2 \pi} \sigma_k} \exp \left(-\frac{1}{2 \sigma_k^2}\left(x^2-2x\mu_k + \mu_k^2\right)\right)}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma_l} \exp \left(-\frac{1}{2 \sigma_l^2}\left(x-\mu_l\right)^2\right)}$$

    Czynnik niezależny od $k$:

    $$c=\frac{\frac{1}{\sqrt{2 \pi}}}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma_l} \exp \left(-\frac{1}{2 \sigma_l^2}\left(x-\mu_l\right)^2\right)}$$

    $$p_k(x)=c \frac{\pi_k}{\sigma_k} \exp \left(-\frac{1}{2 \sigma_k^2}\left(x^2-2x\mu_k + \mu_k^2\right)\right)$$

    $$p_k(x)=c \frac{\pi_k}{\sigma_k} \exp \left(-\frac{x^2}{2 \sigma_k^2} +\frac{x\mu_k^2}{\sigma_k^2}  -\frac{\mu_k^2}{2 \sigma_k^2}\right)$$

    Logarytmowanie:

    $$\ln[p_k(x)]=\ln(c) +  \ln\left(\frac{\pi_k}{\sigma_k}\right) - \frac{x^2}{2 \sigma_k^2} + \frac{x\mu_k^2}{\sigma_k^2}  -\frac{\mu_k^2}{2 \sigma_k^2}$$

    Ostatecznie dostajemy funkcję kwadratową.

4. When the number of features $p$ is large, there tends to be a deterioration in the performance of KNN and other local approaches that perform prediction using only observations that are near the test observation for which a prediction must be made. This phenomenon is known as the curse of dimensionality, and it ties into the fact that non-parametric approaches often perform poorly when $p$ is large. We will now investigate this curse.

    > Bez zbędnego utrudniania nie rozważam przypadków kiedy $x$ wpada w przedział $[0, 0.05] \cup [0.95, 1]$ i trzymam się tego w każdym podpunkcie z tego zadania.

    (a) Suppose that we have a set of observations, each with measurements on $p = 1$ feature, $X$. We assume that $X$ is uniformly (evenly) distributed on $[0, 1]$. Associated with each observation is a response value. Suppose that we wish to predict a test observation’s response using only observations that are within 10% of the range of $X$ closest to that test observation. For instance, in order to predict the response for a test observation with $X = 0.6$, we will use observations in the range $[0.55, 0.65]$. On average, what fraction of the available observations will we use to make the prediction?

    > Średnio używane jest 10% obserwacji.

    (b) Now suppose that we have a set of observations, each with measurements on $p = 2$ features, $X_1$ and $X_2$. We assume that $(X_1, X_2)$ are uniformly distributed on $[0, 1] \times [0, 1]$. We wish to predict a test observation’s response using only observations that are within 10 % of the range of $X_1$ and within 10% of the range of $X_2$ closest to that test observation. For instance, in order to predict the response for a test observation with $X_1 = 0.6$ and $X_2 = 0.35$, we will use observations in the range $[0.55, 0.65]$ for $X_1$ and in the range $[0.3, 0.4]$ for $X_2$. On average, what fraction of the available observations will we use to make the prediction?

    > Używamy $10\% \cdot 10\% = 1\%$ dostępnych obserwacji.

    (c) Now suppose that we have a set of observations on $p = 100$ features. Again the observations are uniformly distributed on each feature, and again each feature ranges in value from 0 to 1. We wish to predict a test observation’s response using observations within the 10% of each feature’s range that is closest to that test observation. What fraction of the available observations will we use to make the prediction?

    > Używamy $10\%^{100} \approx 0\%$ dostępnych obserwacji.

    (d) Using your answers to parts (a)–(c), argue that a drawback of KNN when $p$ is large is that there are very few training observations “near” any given test observation.

    > Widać, że wraz z kolejnym dodanym predykatorem spada ilość danych używanych do klasyfikacji w tempie wykładniczym.

    (e) Now suppose that we wish to make a prediction for a test observation by creating a $p$-dimensional hypercube centered around the test observation that contains, on average, 10% of the training observations. For $p = 1, 2$, and $100$, what is the length of each side of the hypercube? Comment on your answer.

    _Note: A hypercube is a generalization of a cube to an arbitrary number of dimensions. When $p = 1$, a hypercube is simply a line segment, when $p = 2$ it is a square, and when $p = 100$ it is a $100$-dimensional cube._

    > Kiedy $p=1$ to długość boku kostki wynosi $0.1$.
    >
    > Kiedy $p=2$ to długość boku kostki spełnia równanie $a^2 = 0.1$ a stąd $a = 0.1^{\frac{1}{2}} \approx 0.32$
    >
    > Kiedy $p=100$ to długość boku kostki wynosi $a = 0.1^{\frac{1}{100}} \approx 0.98$
    >
    > Widać, że wraz ze wzrostem $p$ długość boku kostki dąży do 1 czyli do 100% dostępnych danych.

5. We now examine the differences between LDA and QDA.

    (a) If the Bayes decision boundary is linear, do we expect LDA or QDA to perform better on the training set? On the test set?

    > QDA jest bardziej elastycznym modelem i zawsze będzie lepiej się sprawdzał na danych treningowych. LDA w tym przypadku będzie lepiej sprawdzał się na danych testowych.

    (b) If the Bayes decision boundary is non-linear, do we expect LDA or QDA to perform better on the training set? On the test set?

    > W obu przypadkach lepszy będzie model QDA.

    (c) In general, as the sample size $n$ increases, do we expect the test prediction accuracy of QDA relative to LDA to improve, decline, or be unchanged? Why?

    > Ogólnie model QDA sprawdza się lepiej od modelu LDA kiedy rozmiar próby jest większy.
    
    (d) True or False: Even if the Bayes decision boundary for a given problem is linear, we will probably achieve a superior test error rate using QDA rather than LDA because QDA is flexible enough to model a linear decision boundary. Justify your answer.

    > False. Model QDA może zostać przetrenowany przez to, że jest bardziej elastyczny dlatego może sprawować się dobrze na danych treningowych ale źle na danych testowych.

6. Suppose we collect data for a group of students in a statistics class with variables $X_1=$ hours studied, $X_2=$ undergrad GPA, and $Y=$ receive an A. We fit a logistic regression and produce estimated coefficient, $\hat{\beta}_0=-6, \hat{\beta}_1=0.05, \hat{\beta}_2=1$.

    (a) Estimate the probability that a student who studies for 40 h and has an undergrad GPA of 3.5 gets an A in the class.

    > Model logistyczny:
    >
    > $$p(X)=\frac{e^{\hat{\beta}_0+\hat{\beta}_1 X_1 + \hat{\beta}_2X_2}}{1+e^{\hat{\beta}_0+\hat{\beta}_1 X_1 + \hat{\beta}_2X_2}}$$
    >
    > $$p(X)=\frac{e^{-6+0.05\cdot40+1\cdot3.5}}{1+e^{-6+0.05\cdot40+1\cdot3.5}} = \frac{e^{-0.5}}{1+e^{-0.5}} \approx 0.38$$

    (b) How many hours would the student in part (a) need to study to have a 50% chance of getting an A in the class?

    > Model można zapisać w postaci:
    >
    > $$\ln\left(\frac{p(X)}{1-p(X)}\right) =\hat{\beta}_0+\hat{\beta}_1 X_1 + \hat{\beta}_2X_2$$
    >
    > $$\ln\left(\frac{0.5}{1-0.5}\right) =-6+0.05 X_1 + 1\cdot 3.5$$
    >
    >$$X_1 = 50$$
