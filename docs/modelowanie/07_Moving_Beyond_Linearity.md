---
layout: math
title: 07 Moving Beyond Linearity
parent: Modelowanie
nav_order: 6
---

# Moving Beyond Linearity

1. It was mentioned in the chapter that a cubic regression spline with one knot at $\xi$ can be obtained using a basis of the form $x$, $x^2$, $x^3$, $(x − \xi)^3_+$, where $(x− \xi)^3_+ = (x - \xi)^3$ if $x > \xi$ and equals 0 otherwise.
We will now show that a function of the form 

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
    > $$f(x) = (\beta_0 - \beta_4\xi^3) + (\beta_1 + 3\beta_4\xi^2)x + (\beta_2 - 3\beta_4\xi)x^2 + (\beta_3 + \beta_4)x^3$$
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

    (e) Show that $f''_1(\xi) = f''_2(\xi)$. That is, $f''(x)$ is continuous at $\xi$.

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
