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

7. Suppose that we wish to predict whether a given stock will issue a dividend this year ("Yes" or "No") based on $X$, last year's percent profit. We examine a large number of companies and discover that the mean value of $X$ for companies that issued a dividend was $\bar{X}=10$, while the mean for those that didn't was $\bar{X}=0$. In addition, the variance of $X$ for these two sets of companies was $\hat{\sigma}^2=36$. Finally, $80 \%$ of companies issued dividends. Assuming that $X$ follows a normal distribution, predict the probability that a company will issue a dividend this year given that its percentage profit was $X=4$ last year.

    _Hint: Recall that the density function for a normal random variable is $f(x)=\frac{1}{\sqrt{2 \pi \sigma^2}} e^{-(x-\mu)^2 / 2 \sigma^2}$. You will need to use Bayes' theorem._

    Korzystając z twierdzenia Bayesa dostajemy:

    $$p_k(x)=\frac{\pi_k \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_k\right)^2\right)}{\sum_{l=1}^K \pi_l \frac{1}{\sqrt{2 \pi} \sigma} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_l\right)^2\right)}$$

    W przypadku z zadania:

    $$p_{yes}(4)=\frac{\pi_{yes} \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_{yes}\right)^2\right)}{\sum_{l\in[yes, no]}^K \pi_l \exp \left(-\frac{1}{2 \sigma^2}\left(x-\mu_l\right)^2\right)}$$

    $$\pi_{yes} = 0.8$$

    $$\pi_{no} = 0.2$$

    $$p_{yes}(4)=\frac{0.8 \exp \left(-\frac{1}{2 \cdot 36}\left(4-10\right)^2\right)}{0.8 \exp \left(-\frac{1}{2 \cdot 36}\left(4-10\right)^2\right) + 0.2 \exp \left(-\frac{1}{2 \cdot 36}\left(4-0\right)^2\right)}$$

    $$p_{yes}(4)=\frac{0.8 \exp \left(-0.5\right)}{0.8 \exp \left(-0.5\right) + 0.2 \exp \left(-\frac{2}{9}\right)}$$

    $$p_{yes}(4)\approx 0.75$$

8. Suppose that we take a data set, divide it into equally-sized training and test sets, and then try out two different classification procedures. First we use logistic regression and get an error rate of 20% on the
training data and 30% on the test data. Next we use 1-nearest neighbors (i.e. $K = 1$) and get an average error rate (averaged over both test and training data sets) of 18%. Based on these results, which method should we prefer to use for classification of new observations? Why?

    KNN z $K=1$ będzie dopasowany do danych treningowych idealnie tzn. błąd będzie wynosił 0. Oznacza to, że błąd na zbiorze testowym będzie wynosił średnio 36%. Wyboru modelu dokonujemy na podstawie zbioru testowego na którym mniejszy błąd ma regresja logistyczna (30%) i ten model powinien zostać wybrany.

9. This problem has to do with odds.
    
    (a) On average, what fraction of people with an odds of 0.37 of defaulting on their credit card payment will in fact default?

    Odds jest zdefiniowany jako: $p(x)/(1-p(x))$.

    $$0.37 = \frac{p(x)}{1 - p(x)}$$

    $$p(x) = 0.27$$
    
    (b) Suppose that an individual has a 16% chance of defaulting on her credit card payment. What are the odds that she will default?

    $$odds = \frac{0.16}{1 - 0.16} = 0.19$$

10. Equation 4.32 derived an expression for $\log \left(\frac{\text{Pr}(Y=k \mid X=x)}{\text{Pr}(Y=K \mid X=x)}\right)$ in the setting where $p>1$, so that the mean for the $k$th class, $\mu_k$, is a $p$-dimensional vector, and the shared covariance $\boldsymbol{\Sigma}$ is a $p \times p$ matrix. However, in the setting with $p=1$, (4.32) takes a simpler form, since the means $\mu_1, \ldots, \mu_K$ and the variance $\sigma^2$ are scalars. In this simpler setting, repeat the calculation in (4.32), and provide expressions for $a_k$ and $b_{k j}$ in terms of $\pi_k, \pi_K, \mu_k, \mu_K$, and $\sigma^2$.

    $$\log\left(\frac{\text{Pr}(Y=k|X=x)}{\text{Pr}(Y=K|X=x)}\right) = \log\left(\frac{\pi_k f_k(x)}{\pi_K f_K(x)}\right) =$$
    
    $$ = \log\left(\frac{\pi_k \exp(-1/2((x-\mu_k)/\sigma)^2)}{\pi_K \exp(-1/2((x-\mu_K)/\sigma)^2)}\right) =$$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2} \left(\frac{x-\mu_k}{\sigma}\right)^2 + \frac{1}{2} \left(\frac{x-\mu_K}{\sigma}\right)^2 =$$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2\sigma^2} (x-\mu_k)^2 + \frac{1}{2\sigma^2} (x-\mu_K)^2 = $$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2\sigma^2} \left((x-\mu_k)^2 - (x-\mu_K)^2\right) = $$
    
    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2\sigma^2} \left(x^2-2x\mu_k+\mu_k^2 - x^2 + 2x\mu_K - \mu_K^2\right) = $$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2\sigma^2} \left(2x(\mu_K - \mu_k) + \mu_k^2 -\mu_K^2\right) = $$
 
    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{\mu_k^2 -\mu_K^2}{2\sigma^2} + x\frac{(\mu_k - \mu_K)}{\sigma^2} = $$

    $$ = a_k + b_kx$$

11. Work out the detailed forms of $a_k, b_{k j}$, and $b_{kjl}$ in (4.33). Your answer should involve $\pi_k, \pi_K, \mu_k, \mu_K, \boldsymbol{\Sigma}_k$, and $\boldsymbol{\Sigma}_K$.

    $$\log\left(\frac{\text{Pr}(Y=k|X=x)}{\text{Pr}(Y=K|X=x)}\right) = \log\left(\frac{\pi_k f_k(x)}{\pi_K f_K(x)}\right) =$$
    
    $$ = \log\left(\frac{\pi_k \exp(-\frac{1}{2}(x-\mu_k)^T\boldsymbol{\Sigma}_k^{-1}(x-\mu_k))}{\pi_K \exp(-\frac{1}{2}(x-\mu_K)^T\boldsymbol{\Sigma}_K^{-1}(x-\mu_K))}\right) =$$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) -\frac{1}{2}(x-\mu_k)^T\boldsymbol{\Sigma}_k^{-1}(x-\mu_k) + \frac{1}{2}(x-\mu_K)^T\boldsymbol{\Sigma}_K^{-1}(x-\mu_K) =$$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) -\frac{1}{2}(x^T-\mu_k^T)\boldsymbol{\Sigma}_k^{-1}(x-\mu_k) + \frac{1}{2}(x^T-\mu_K^T)\boldsymbol{\Sigma}_K^{-1}(x-\mu_K) = $$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}[x^T \boldsymbol{\Sigma}_k^{-1}(x-\mu_k)-\mu_k^T\boldsymbol{\Sigma}_k^{-1}(x-\mu_k)] $$
    
    $$ + \frac{1}{2}[x^T \boldsymbol{\Sigma}_K^{-1}(x-\mu_K)-\mu_K^T\boldsymbol{\Sigma}_K^{-1}(x-\mu_K)] =$$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}[x^T \boldsymbol{\Sigma}_k^{-1}x- x^T \boldsymbol{\Sigma}_k^{-1}\mu_k-\mu_k^T\boldsymbol{\Sigma}_k^{-1}x+\mu_k^T\boldsymbol{\Sigma}_k^{-1}\mu_k] + $$
    
    $$ + \frac{1}{2}[x^T \boldsymbol{\Sigma}_K^{-1}x- x^T \boldsymbol{\Sigma}_K^{-1}\mu_K-\mu_K^T\boldsymbol{\Sigma}_K^{-1}x+\mu_K^T\boldsymbol{\Sigma}_K^{-1}\mu_K] =$$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}[x^T \boldsymbol{\Sigma}_k^{-1}x + \mu_k^T\boldsymbol{\Sigma}_k^{-1}\mu_k - x^T \boldsymbol{\Sigma}_k^{-1}\mu_k-x^T \boldsymbol{\Sigma}_k^{-1}\mu_k] + $$
    
    $$ + \frac{1}{2}[x^T \boldsymbol{\Sigma}_K^{-1}x + \mu_K^T\boldsymbol{\Sigma}_K^{-1}\mu_K - x^T \boldsymbol{\Sigma}_K^{-1}\mu_K-x^T \boldsymbol{\Sigma}_K^{-1}\mu_K] = $$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}[x^T \boldsymbol{\Sigma}_k^{-1}x + \mu_k^T\boldsymbol{\Sigma}_k^{-1}\mu_k] + x^T \boldsymbol{\Sigma}_k^{-1}\mu_k$$
    
    $$ + \frac{1}{2}[x^T \boldsymbol{\Sigma}_K^{-1}x + \mu_K^T\boldsymbol{\Sigma}_K^{-1}\mu_K] - x^T \boldsymbol{\Sigma}_K^{-1}\mu_K = $$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}\mu_k^T\boldsymbol{\Sigma}_k^{-1}\mu_k + \frac{1}{2} \mu_K^T\boldsymbol{\Sigma}_K^{-1}\mu_K + $$

    $$ + x^T \boldsymbol{\Sigma}_k^{-1}\mu_k - x^T \boldsymbol{\Sigma}_K^{-1}\mu_K - $$
    
    $$ -\frac{1}{2} x^T \boldsymbol{\Sigma}_k^{-1}x + \frac{1}{2}x^T \boldsymbol{\Sigma}_K^{-1}x   = $$

    $$ = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}\mu_k^T\boldsymbol{\Sigma}_k^{-1}\mu_k + \frac{1}{2} \mu_K^T\boldsymbol{\Sigma}_K^{-1}\mu_K + $$

    $$ + x^T (\boldsymbol{\Sigma}_k^{-1}\mu_k - \boldsymbol{\Sigma}_K^{-1}\mu_K) + $$
    
    $$ + x^T \frac{1}{2}(\boldsymbol{\Sigma}_K^{-1} + \boldsymbol{\Sigma}_k^{-1})x   = $$

    $$= a_k + \sum\limits_{j=1}^pb_{kj}x_j + \sum\limits_{j=1}^p\sum\limits_{l=1}^p c_{kjl}x_jx_l$$

    gdzie:

    $a_k = \log\left(\frac{\pi_k}{\pi_K}\right) - \frac{1}{2}\mu_k^T\boldsymbol{\Sigma}_k^{-1}\mu_k + \frac{1}{2} \mu_K^T\boldsymbol{\Sigma}_K^{-1}\mu_K$

    $b_{kj}$ jest $j$-tym elementem wektora $\boldsymbol{\Sigma}_k^{-1}\mu_k - \boldsymbol{\Sigma}_K^{-1}\mu_K$

    $c_{kjl}$ jest elementem macierzy $\frac{1}{2}(\boldsymbol{\Sigma}_K^{-1} + \boldsymbol{\Sigma}_k^{-1})$ z $j$-tego wiersza i $l$-tej kolumny

12. Suppose that you wish to classify an observation $X \in \mathbb{R}$ into `apples` and `oranges`. You fit a logistic regression model and find that

    $$
    \widehat{\operatorname{Pr}}(Y=\text { orange } \mid X=x)=\frac{\exp \left(\hat{\beta}_0+\hat{\beta}_1 x\right)}{1+\exp \left(\hat{\beta}_0+\hat{\beta}_1 x\right)} .
    $$


    Your friend fits a logistic regression model to the same data using the _softmax_ formulation in (4.13), and finds that

    $$
    \begin{aligned}
    & \widehat{\operatorname{Pr}}(Y=\text { orange } \mid X=x)= \\
    & = \frac{\exp \left(\hat{\alpha}_{\text {orange} 0}+\hat{\alpha}_{\text {orange} 1} x\right)}{\exp \left(\hat{\alpha}_{\text {orange} 0}+\hat{\alpha}_{\text {orange} 1} x\right)+\exp \left(\hat{\alpha}_{\text {apple} 0}+\hat{\alpha}_{\text {apple} 1} x\right)} .
    \end{aligned}
    $$

    (a) What is the log odds of `orange` versus `apple` in your model?


    > $$\log\left(\frac{\widehat{\operatorname{Pr}}(Y=\text { orange } \mid X=x)}{1-\widehat{\operatorname{Pr}}(Y=\text { orange } \mid X=x)}\right) = \hat\beta_0 + \hat\beta_1x$$

    (b) What is the log odds of `orange` versus `apple` in your friend's model?

    > $$
    \begin{aligned}
    & \log\left(\frac{\widehat{\operatorname{Pr}}(Y=\text { orange } \mid X=x)}{\widehat{\operatorname{Pr}}(Y=\text { apple } \mid X=x)}\right) = \\
    & = (\hat\alpha_{orange0} - \hat\alpha_{apple0}) + (\hat\alpha_{orange1} - \hat\alpha_{apple1})x
    \end{aligned}
    $$

    (c) Suppose that in your model, $\hat{\beta}_0=2$ and $\hat{\beta}_1=-1$. What are the coefficient estimates in your friend's model? Be as specific as possible.

    > Można tylko stwierdzić, że $\hat\alpha_{orange0} - \hat\alpha_{apple0} = 2$ i $\hat\alpha_{orange1} - \hat\alpha_{apple1} = -1$
    >
    > Dokładnych wartości parametrów nie jesteśmy w stanie określić.

    (d) Now suppose that you and your friend fit the same two models on a different data set. This time, your friend gets the coefficient estimates $\hat{\alpha}_{\text {orange} 0}=1.2, \hat{\alpha}_{\text {orange} 1}=-2, \hat{\alpha}_{\text {apple} 0}=3, \hat{\alpha}_{\text {apple} 1}= 0.6$. What are the coefficient estimates in your model?

    > $\hat{\beta}_0 = 1.2 - 3 = -1.8$
    >
    > $\hat{\beta}_1 = -2 - 0.6 = -2.6$

    (e) Finally, suppose you apply both models from (d) to a data set with 2 000 test observations. What fraction of the time do you expect the predicted class labels from your model to agree with those from your friend’s model? Explain your answer.

    > Modele są takie same tylko z różną parametryzacją więc wyniki powinny być identyczne.
