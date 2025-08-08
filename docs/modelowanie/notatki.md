---
layout: math
title: Notatki
parent: Modelowanie
nav_order: 99
---

## Dewiancja GLM

W kontekście uogólnionych modeli liniowych (GLM), dewiancja jest miarą jakości dopasowania modelu. Służy ona do oceny, jak dobrze dany model pasuje do obserwowanych danych.

**Koncepcja Dewiancji**

Dewiancja stanowi uogólnienie sumy kwadratów reszt, znanej z klasycznej regresji liniowej z rozkładem normalnym, na wszystkie modele z rodziny GLM. Kwantyfikuje ona zmienność w danych, która nie została wyjaśniona przez analizowany model.

Koncepcja dewiancji opiera się na porównaniu dopasowania dwóch modeli:

* Modelu analizowanego: Modelu, którego jakość dopasowania chcemy ocenić.

* Modelu nasyconego (pełnego): Modelu, który idealnie pasuje do danych, posiadając tyle samo parametrów, co obserwacji. W tym modelu wartość dopasowana dla każdej obserwacji jest równa jej wartości obserwowanej ($\hat{\mu} = y_i$). Jest to najlepsze możliwe dopasowanie, jakie można uzyskać dla danej rodziny rozkładów.

**Wzór Koncepcyjny:**

$$D(\mathbf{y}, \hat{\mathbf{\mu}}) = 2 \phi (L_{full} - L(\hat{\beta}))$$

gdzie:

$\phi$ - parametr dyspersji. Dla niektórych rozkładów, takich jak rozkład Poissona czy dwumianowy, parametr ten jest stały i wynosi 1. Dla innych, jak rozkład Gamma, musi być estymowany.

$L_{full}$ - logarytm wiarygodności modelu pełnego (nasyconego). Jest to najwyższa możliwa wartość logarytmu wiarygodności, jaką można osiągnąć dla danych przy użyciu określonego rozkładu.

$L(\hat{\beta})$ - logarytm wiarygodności analizowanego modelu, obliczony dla estymowanych parametrów $\hat{\beta}$.

**Wzór ogólny:**

$$D(\mathbf{y}, \hat{\mathbf{\mu}}) = 2 \sum_{i=1}^{n} \nu_i [y_i(\tilde{\theta}_i - \hat{\theta}_i) - a(\tilde{\theta}_i) + a(\hat{\theta}_i)]$$

gdzie:

$D(\mathbf{y}, \hat{\mathbf{\mu}})$ - dewiancja, która jest miarą rozbieżności między wektorem obserwowanych danych $\mathbf{y}$ a wektorem wartości dopasowanych przez model $\hat{\mathbf{\mu}}$.

$\nu_i$ - waga przypisana $i$-tej obserwacji. Umożliwia uwzględnienie różnej "ważności" lub wolumenu informacji dla poszczególnych punktów danych.

$\tilde{\theta}_i$ - estymata parametru kanonicznego dla i-tej obserwacji w modelu pełnym (nasyconym). Model pełny to model, który ma tyle parametrów, ile jest obserwacji, i w rezultacie idealnie dopasowuje się do danych (co oznacza, że dopasowana średnia jest równa obserwowanej wartości, $\hat{\mu}_i = y_i$).

$\hat{\theta}_i$ - estymata parametru kanonicznego dla i-tej obserwacji w analizowanym (testowanym) modelu.

$a(\cdot)$ - funkcja kumulacyjna, która jest unikalna dla każdego rozkładu z wykładniczej rodziny rozkładów (ED family). Definiuje ona związek między parametrem kanonicznym a średnią rozkładu.

## Metoda Hilla

Metoda Hilla jest alternatywą dla modelowania opartego na uogólnionym rozkładzie Pareto (GPD), przeznaczoną specjalnie dla rozkładów ciężkoogonowych (należących do dziedziny przyciągania rozkładu Frécheta).

Główne punkty:

* Cel metody: głównym celem Metody Hilla nie jest modelowanie całej dystrybucji nadwyżek ponad próg, lecz bezpośrednie oszacowanie indeksu ogona ($\alpha$). Indeks ten opisuje, jak szybko maleje prawdopodobieństwo w ogonie rozkładu.

* Estymator Hilla: estymacja odbywa się za pomocą estymatora Hilla, który jest funkcją $k$ największych statystyk pozycyjnych z próby $n$ obserwacji.

* Wykres Hilla: w praktyce, kluczowym narzędziem jest wykres Hilla, który przedstawia wartość estymowanego indeksu ogona w zależności od liczby użytych statystyk pozycyjnych ($k$). Analityk poszukuje na wykresie stabilnego regionu, który sugeruje właściwą wartość indeksu ogona. Interpretacja wykresu może być jednak trudna.

* Estymacja ogona rozkładu: wyestymowany indeks ogona jest następnie używany do skonstruowania estymatora ogona Hilla, który pozwala szacować prawdopodobieństwa w ogonie rozkładu strat powyżej progu.

## Krzywa Lorenza i krzywa koncentracji

Kluczowe różnice

* Mierzona wartość:

    * Krzywa Koncentracji $(CC[\mu(X), \hat{\mu}(X);\alpha])$ mierzy skumulowany udział rzeczywistej składki (lub straty, $\mu(X)$) dla $\alpha$ procent polis o najniższych wartościach predyktora $\hat{\mu}(X)$. Innymi słowy, pokazuje, jaka część całkowitej szkody przypada na portfel uznany przez model za najmniej ryzykowny.

    * Krzywa Lorentza $(LC[\hat{\mu}(X);\alpha])$ mierzy skumulowany udział prognozowanej składki $\hat{\mu}(X)$ dla $\alpha$ procent polis o najniższych wartościach tego samego predyktora $\hat{\mu}(X)$. Pokazuje, jaką część całkowitej zebranej składki stanowią polisy o najniższych prognozach.

* Cel i interpretacja:

    * Krzywa Koncentracji ocenia, jak dobrze uporządkowanie ryzyka przez predyktor odpowiada rzeczywistemu rozkładowi strat. Pokazuje, co powinno zostać zebrane z danego segmentu portfela.
    
    * Krzywa Lorenza opisuje wewnętrzną zmienność samego predyktora – jak bardzo różnicuje on składki. Pokazuje, co model proponuje zebrać z danego segmentu.

Jak działa porównanie?

* Idealny predyktor: dla doskonałego predyktora, gdzie prognozowana składka jest równa składce rzeczywistej $(\hat{\mu}(X) = \mu(X))$, obie krzywe pokrywają się.

* Ocena rozbieżności: różnica między krzywymi wskazuje na niedopasowanie modelu do ryzyka. Jeśli dla najmniej ryzykownych polis krzywa koncentracji leży powyżej krzywej Lorenza, oznacza to, że segment ten generuje większy udział w szkodach niż w zebranych składkach, co świadczy o ryzyku selekcji negatywnej (ang. adverse selection).

* Miara ilościowa: jakość predyktora można skwantyfikować za pomocą wskaźnika ABC (Area Between Curves), czyli pola powierzchni między krzywą koncentracji a krzywą Lorenza. Mniejsza wartość ABC oznacza, że struktura cenowa modelu jest bliższa rzeczywistej strukturze ryzyka, co świadczy o wyższej jakości predyktora.