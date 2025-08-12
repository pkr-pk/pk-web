---
layout: math
title: 08 Tree-Based Methods
parent: Modelowanie
nav_order: 7
---

# Tree-Based Methods

1. Draw an example (of your own invention) of a partition of two-dimensional feature space that could result from recursive binary splitting. Your example should contain at least six regions. Draw a decision tree corresponding to this partition. Be sure to label all aspects of your figures, including the regions $R_1$, $R_2$, . . ., the cutpoints $t_1$, $t_2$, . . ., and so forth.

    _Hint: Your result should look something like Figures 8.1. and 8.2._

    ![](img/08_011.png)

    ![](img/08_012.png)

2. It is mentioned in Section 8.2.3 that boosting using depth-one trees (or stumps) leads to an additive model: that is, a model of the form
    
    $$f(X) = \sum\limits_{j=1}^p f_j (X_j).$$

    Explain why this is the case. You can begin with (8.12) in Algorithm 8.2.

    Model addytywny ma postać $f(X) = \sum\limits_{j=1}^p f_j (X_j)$, gdzie ostateczna prognoza jest sumą funkcji, z których każda zależy tylko od jednego predyktora.
    
    W przypadku boostingu z pniami (drzewami o głębokości 1), każde indywidualne drzewo $f^b(x)$ jest funkcją tylko jednej zmiennej (tej, która została użyta do podziału). Ostateczny model jest sumą wielu takich prostych drzew. Sumę tę można przegrupować tak, aby zsumować wszystkie funkcje zależne od $X_1$, wszystkie funkcje zależne od $X_2$ itd., co prowadzi bezpośrednio do addytywnej formy modelu.