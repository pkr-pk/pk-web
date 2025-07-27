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
