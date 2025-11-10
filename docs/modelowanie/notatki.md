---
layout: math
title: Notatki
parent: Modelowanie
nav_order: 99
---

# Effective Statistical Learning Methods for Actuaries I

## 4: Uogólnione modele liniowe (GLMs)

**4.2: Czym jest interakcja w kontekście czynników ryzyka ubezpieczeniowego i dlaczego różni się od korelacji?**

Interakcja w kontekście czynników ryzyka ubezpieczeniowego odnosi się do sytuacji, w której wpływ jednego czynnika ryzyka na prawdopodobieństwo wystąpienia szkody zależy od obecności innego czynnika ryzyka. Oznacza to, że efekty dwóch (lub więcej) zmiennych nie są jedynie sumą ich indywidualnych wpływów, ale mogą się wzmacniać lub osłabiać w zależności od ich wzajemnego oddziaływania.

Różnica między interakcją a korelacją:
* Korelacja mierzy stopień współzmienności dwóch zmiennych, czyli na ile ich wartości są statystycznie powiązane (np. wzrost jednej zmiennej towarzyszy wzrostowi drugiej).
* Interakcja odnosi się do sposobu, w jaki jedna zmienna modyfikuje wpływ drugiej na określone zjawisko, np. ryzyko szkody. Może oznaczać, że efekt jednej zmiennej występuje tylko pod warunkiem obecności drugiej.

Korelacja sama w sobie nie oznacza interakcji – dwie zmienne mogą być silnie skorelowane, ale nie muszą wpływać na siebie nawzajem w sposób interakcyjny. Dlatego w analizie ryzyka ubezpieczeniowego ważne jest stosowanie modeli, które uwzględniają nie tylko współzależności, ale także potencjalne efekty interakcji między czynnikami.

---
**4.4: Krótko omów współczynnik zależności V Cramera. Wskaż jakie może przyjmować wartości i co one oznaczają w kontekście analizy siły zależności między zmiennymi. W jakich przypadkach można stosować ten współczynnik? Czy jest on ograniczony tylko do zmiennych jakościowych, czy może być używany także dla zmiennych ilościowych? Jeżeli tak, to w jaki sposób można go obliczyć?**

Współczynnik V Craméra jest miarą siły związku (asocjacji) między dwiema zmiennymi, często wykorzystywaną w badaniach ubezpieczeniowych. Jego obliczenia opierają się na statystyce chi-kwadrat ($\chi^2$) z tablicy kontyngencji, która zestawia ze sobą parę analizowanych cech. Jest on zdefiniowany wzorem:

$$
V = \sqrt{\frac{\chi^2/n}{\min\{k_1 - 1, k_2 - 1\}}}
$$

gdzie:
*   $\chi^2$ to wartość statystyki chi-kwadrat Pearsona dla testu niezależności.
*   $n$ to liczba obserwacji.
*   $k_1$ i $k_2$ to liczba kategorii (poziomów) dla pierwszej i drugiej zmiennej.

Współczynnik V Craméra przyjmuje wartości z przedziału $(0,1)$. Interpretacja tych wartości jest następująca:
*   Wartość 0 - oznacza całkowitą niezależność między zmiennymi.
*   Wartość 1 - oznacza idealną (pełną) zależność między zmiennymi.

Może być używany do oceny siły zależności dla różnych typów zmiennych, w tym:
*   binarnych,
*   kategorycznych (jakościowych),
*   dyskretnych (skokowych).

Współczynnik V Craméra może być stosowany również dla zmiennych ciągłych (ilościowych), jednak wymaga to ich wcześniejszego przygotowania. Proces ten polega na dyskretyzacji (nazywanej również grupowaniem lub "bandingiem"), czyli podziale dziedziny zmiennej ciągłej na rozłączne przedziały. Po takim przekształceniu zmienna ilościowa jest traktowana jak zmienna dyskretna lub kategoryczna.

---
**4.4: Jak wykluczenie zmiennej silnie skorelowanej z innymi cechami wpływa na oszacowanie pozostałych współczynników regresji? Jak nazywa się to zjawisko?**

Wykluczenie zmiennej, która jest silnie skorelowana zarówno ze zmienną objaśnianą, jak i z innymi cechami uwzględnionymi w modelu, prowadzi do obciążenia oszacowań pozostałych współczynników regresji.

Oszacowany współczynnik dla danej zmiennej nie odzwierciedla już jej rzeczywistego, odizolowanego wpływu na zmienną objaśnianą. Zamiast tego, "pochłania" on część efektu, który wnosiła pominięta, skorelowana zmienna. W rezultacie oszacowany współczynnik staje się mieszanką prawdziwego efektu danej cechy oraz efektu cechy pominiętej. Może to prowadzić do błędnej interpretacji, w tym do zmiany wartości, a nawet znaku współczynnika.

Zjawisko to nazywa się błędem pominiętej zmiennej.

---
**4.5: Podaj definicje dewiancji i skalowanej dewiancji (scaled deviance). Wskaż, której wielkości, związanej z jakością modelu regresji liniowej, odpowiada dewiancja. Jaki rozkład ma skalowana dewiancja?**

Dewiancja stanowi uogólnienie sumy kwadratów reszt i jest zdefiniowana jako: 

$$D(\mathbf{y}, \hat{\mathbf{\mu}}) = 2 \phi (L_{full} - L(\hat{\beta}))$$

gdzie:

$\phi$ - parametr dyspersji. Dla niektórych rozkładów, takich jak rozkład Poissona czy dwumianowy, parametr ten jest stały i wynosi 1. Dla innych, jak rozkład Gamma, musi być estymowany.

$L_{full}$ - logarytm wiarygodności modelu pełnego (nasyconego). Jest to najwyższa możliwa wartość logarytmu wiarygodności, jaką można osiągnąć dla danych przy użyciu określonego rozkładu.

$L(\hat{\beta})$ - logarytm wiarygodności analizowanego modelu, obliczony dla estymowanych parametrów $\hat{\beta}$.

Dewiancja skalowana jest zdefiniowana jako:

$$\tilde{D}(\mathbf{y}, \hat{\mathbf{\mu}}) = \frac{D(\mathbf{y}, \hat{\mathbf{\mu}})}{\phi}$$

Dla dużych prób, rozkład dewiancji skalowanej można przybliżyć rozkładem chi-kwadrat ($\chi^2$) z liczbą stopni swobody równą $n - (p + 1)$, gdzie $n$ to liczba obserwacji, a $p+1$ to liczba szacowanych parametrów w modelu.

---
**4.5: Wyjaśnij, dlaczego dewiancja modelu nasyconego wynosi 0.**

Model nasycony dokładnie odtwarza dane co oznacza, że nie ma żadnych reszt. Brak „straty dopasowania” oznacza, że dewiancja = 0.

---
**4.5 Twoim zadaniem jest wybór modelu o najlepszych zdolnościach predykcyjnych spośród zagnieżdżonych uogólnionych modeli liniowych. Wyjaśnij dlaczego podczas wyboru takiego modelu nie tylko dewiancja powinna zostać uwzględniona.**
 
Dzieje się tak, ponieważ dodanie kolejnych zmiennych do modelu prawie zawsze zmniejszy jego dewiancję (lub w najgorszym przypadku pozostawi ją bez zmian). Prowadzi to do ryzyka stworzenia modelu, który jest zbyt skomplikowany i świetnie dopasowuje się do danych uczących, ale traci zdolność do przewidywania nowych obserwacji.

---
**4.6: Zinterpretuj wartość $\frac{D}{df}$, gdzie $df$ oznacza liczę stopni swobody reszt (residua degrees of freedom) dla tego modelu. Czy bardzo mała wartość $\frac{D}{df}$ jest zawsze dobrą wiadomością? Odpowiedź uzasadnij.**

Jest to estymator dyspersji. W dobrze dopasowanym modelu Poissona oczekujemy $\frac{D}{df} \approx 1.$ Bardzo mała wartość tego wskaźnika nie jest jednak dobrą wiadomością - może wskazywać na zbyt małe reszty, nadmierne dopasowanie (overfitting) lub błędną specyfikację modelu. W efekcie testy istotności mogą być zbyt optymistyczne, a wnioski – mylące.

Estymowana dyspersja mniejsza od 1 mówi o tym, że wariancja w dopasowanym modelu jest za niska, wartość większa od 1 mówi o zbyt dużej wariancji w dopasowanym modelu.

---
**4.8: Podaj definicję obserwacji wpływowej (influential observation).**

Obserwacja wpływowa to taka obserwacja, która, jeśli zostanie nieznacznie zmieniona lub pominięta, w istotny sposób zmodyfikuje oszacowania parametrów modelu.

---
**4.8: Opisz jedną z metod identyfikacji obserwacji wpływowych.**

Odległość Cooka mierzy odległość między $\hat{\beta}$ a $\hat{\beta}_{(-i)},$ (ostatnie to wektor dopasowanych współczynników na zbiore bez $i$-tej obserwacji) przy czym duże wartości wskazują na obserwacje, które mają wpływ na oszacowane współczynniki regresji. Odległość Cooka służy do zbadania, jak każda obserwacja wpływa na cały wektor parametrów $\hat{\beta}$.

---
**4.9: W jaki sposób oblicza się reszty dewiancyjne (deviance residuals)?**

Reszty dewiancyjne ($r_{i}^D$) są zdefiniowane jako pierwiastek kwadratowy z wkładu i-tej obserwacji do łącznej dewiancji modelu, z uwzględnieniem znaku reszty prostej. Wzór:

$$r_{i}^D = \text{sign}(y_i - \hat{\mu}_i)\sqrt{d_i} \text{}$$

gdzie:
* $y_i$ to i-ta obserwowana wartość zmiennej odpowiedzi.
* $\hat{\mu}_i$ to i-ta dopasowana (przewidywana) wartość średnia z modelu.
* $d_i$ to wkład i-tej obserwacji do całkowitej dewiancji modelu, $D(y, \hat{\mu})$.
* $$\text{sign}(y_i - \hat{\mu}_i) = \begin{cases} 1 & \text{jeżeli } y_i > \hat{\mu}_i \\ -1 & \text{w p.p.} \end{cases}$$

---
**4.9: Dlaczego reszty dewiancyjne są często preferowaną formą reszt w modelach GLM? Jakie są główne zalety ich wykorzystania w porównaniu z innymi rodzajami reszt?**

Reszty dewiancyjne są często preferowaną formą w Uogólnionych Modelach Liniowych (GLM), ponieważ w przeciwieństwie do innych typów reszt, uwzględniają one kształt rozkładu zmiennej odpowiedzi, w tym jego skośność. Jest to kluczowe w zastosowaniach aktuarialnych, gdzie rozkłady rzadko są symetryczne.

Główne zalety ich wykorzystania w porównaniu z innymi rodzajami reszt to:

* Lepsze dopasowanie do założeń GLM: w przeciwieństwie do reszt Pearsona, które wywodzą się z modeli liniowych, reszty dewiancyjne są bezpośrednio powiązane z funkcją wiarygodności przyjętego rozkładu z rodziny wykładniczej, co czyni je bardziej odpowiednimi dla struktury GLM.
* Wykrywanie obserwacji słabo dopasowanych: pozwalają zidentyfikować te obserwacje, które w największym stopniu przyczyniają się do wzrostu dewiancji, a więc wskazują na miejsca, w których model niedostatecznie dobrze dopasowuje się do danych.
* Korekta na heteroskedastyczność: podobnie jak reszty Pearsona, ale w przeciwieństwie do reszt prostych (surowych), korygują one fakt, że wariancja w modelach GLM często zależy od wartości średniej. Reszty proste mogą być przez to mniej informatywne.
* Lepsza interpretacja dla danych dyskretnych: chociaż indywidualne reszty dla danych dyskretnych (np. liczby szkód) mogą być trudne do interpretacji, reszty dewiancyjne obliczone dla zagregowanych grup ryzyka dają znacznie lepsze wskazówki co do poprawności dopasowania modelu.

---
**4.9: Wyjaśnij, dlaczego w przypadku diagnostyki uogólnionych modeli liniowych korzystniejsze jest stosowanie reszt Pearsona zamiast zwykłych reszt (raw residuals,response residuals).**

Reszty Pearsona są preferowane, ponieważ poprzez normalizację (dzielenie zwykłych reszt przez odchylenie standardowe i wagę) "stabilizują" wariancję reszt. Dzięki temu są one bardziej porównywalne w całym zakresie wartości dopasowanych i pozwalają na trafniejszą ocenę dopasowania modelu oraz identyfikację obserwacji odstających, bez zakłóceń wynikających z naturalnej zależności wariancji od średniej w rodzinie rozkładów wykładniczych.

## 6: Uogólnione modele addytywne (GAMs)

**6.1: Krótko przedstaw ideę uogólnionych modeli addytywnych (Generalized Additive Models – GAM). Wskaż dlaczego weszły do zestawu narzędzi aktuariusza.**

Uogólnione modele addytywne (GAM) to rozszerzenie uogólnionych modeli liniowych (GLM), które pozwala na modelowanie nieliniowych zależności między predyktorami a zmienną odpowiedzi, zachowując przy tym addytywną strukturę. Zamiast zakładać, że każdy predyktor ma liniowy wpływ na odpowiedź (np. $\beta_1 x_1$), GAM dopasowuje gładką, nieliniową funkcję dla każdego predyktora (np. $f_1(x_1)$). Model końcowy jest sumą tych indywidualnych funkcji:

$$Y = \beta_0 + f_1(X_1) + f_2(X_2) + \dots + f_p(X_p) + \epsilon.$$ 

Taka budowa pozwala na dużą elastyczność w modelowaniu złożonych wzorców, jednocześnie zachowując możliwość interpretacji wpływu każdego predyktora z osobna.

Dzięki GAM aktuariusze mogą:
* Precyzyjnie modelować nieliniowe zależności i interakcje między zmiennymi, takimi jak wiek i płeć kierowcy czy dane geograficzne.
* Analizować indywidualne dane dotyczące śmiertelności przy użyciu regresji Poissona bez konieczności wstępnego, subiektywnego grupowania danych.

---
**6.3: Podaj definicję funkcji sklejanej stopnia 3 (splajnu kubicznego).**

Splajn sześcienny z $K$ węzłami można zamodelować jako:

$$y_i = \beta_0 + \beta_1 b_1(x_i) + \beta_2 b_2(x_i) + \dots + \beta_{K+3} b_{K+3}(x_i) + \epsilon_i,$$

dla odpowiedniego wyboru funkcji bazowych $b_1, b_2,...,b_{K+3}$. Najbardziej bezpośrednim sposobem reprezentacji splajnu sześciennego przy użyciu powyższej jest rozpoczęcie od bazy dla wielomianu sześciennego – mianowicie, $b_1(x_i) = x_i$, $b_2(x_i) = x_i^2$, i $b_3(x_i) = x_i^3$ a następnie dodanie jednej potęgowej funkcji bazowej na każdy węzeł. Potęgowa funkcja bazowa jest zdefiniowana jako:

$$h(x_i, \xi_i) = (x_i - \xi_i)^3_+ = \begin{cases} (x_i - \xi_i)^3 & \text{jeśli } x_i > \xi_i \\ 0 & \text{w przeciwnym razie}, \end{cases}$$

gdzie $\xi_i$ jest $i$-tym węzłem. Przykład:

$$y = \beta_0 + \beta_1 x + \beta_2 x^2 + \beta_3 x^3 + \beta_4 (x - \xi)^3_+$$

## 7: Double GLMs and GAMs for Location, Scale and Shape (GAMLSS)

**7.2: Jaki jest związek między wartością parametru $\xi$ (exponent parameter) a stopniem heteroskedastyczności (zmienności) w modelach aktuarialnych opartych na rodzinie rozkładów Tweedie?**

W modelach aktuarialnych opartych na rodzinie rozkładów Tweedie, parametr $\xi$ kontroluje zależność wariancji od wartości oczekiwanej, co bezpośrednio wpływa na heteroskedastyczność modelu. Związek ten opisuje równanie wariancji:

$$Var(Y) = \phi \mu^\xi$$

gdzie: $\phi$ – parametr skali, $\mu$ – wartość oczekiwana, $\xi$ – parametr kształtu (exponent parameter).

Im większe $\xi$, tym silniejsza heteroskedastyczność, co oznacza, że wariancja bardziej zależy od wartości oczekiwanej.

---
**7.2: Omów zastosowanie rozkładu Tweedie w uogólnionych modelach liniowych (GLM) w kontekście modelowania roszczeń. Zwróć uwagę na rolę zmiennych objaśniających, które mogą wpływać zarówno na liczbę roszczeń, jak i na ich wysokość.**

Modele te są szczególnie przydatne, gdy aktuariusze dysponują jedynie łączną kwotą roszczeń, która jest zerowa z dodatnim prawdopodobieństwem, ale w pozostałych przypadkach ma rozkład ciągły.

Kluczową zaletą modeli Tweedie jest możliwość jednoczesnego modelowania łącznej kwoty roszczeń bez konieczności oddzielnego modelowania częstotliwości i wysokości szkód. To upraszcza analizę, zwłaszcza w kontekście rezerwacji strat, gdzie dane często występują w formie trójkątów.

W ramach uogólnionych modeli liniowych (GLM), zmienne objaśniające (cechy ryzyka) są włączane do modelu w celu wyjaśnienia zarówno systematycznych, jak i losowych wahań w danych dotyczących roszczeń.

W modelu Tweedie, założenie o stałym parametrze dyspersji $\phi$ narzuca istotne ograniczenie. Oznacza to, że każdy czynnik ryzyka, który wpływa na oczekiwaną wysokość szkody, musi również wpływać na oczekiwaną częstotliwość roszczeń w tym samym kierunku.

---
**7.2: Dlaczego podwójny GLM jest szczególnie istotny w modelowaniu, w którym wykorzystuje się regresję Tweedie’ego (uogólnionego modelu liniowego ze zmienną zależną o rozkładzie Tweedie z indeksem 1 < p < 2)?**

DGLM pozwala, aby parametr dyspersji był modelowany w zależności od cech ryzyka. Dzięki temu model jest w stanie poprawnie odwzorować przeciwstawne trendy, co czyni go znacznie bardziej elastycznym i adekwatnym do analiz aktuarialnych.

---
**7.3: Przedstaw koncepcję modelu DGLM (Double Generalized Linear Model) oraz krótko omów sposób estymacji jego parametrów.**

W klasycznym modelu GLM zakłada się, że parametr dyspersji $\phi$ jest stały dla wszystkich obserwacji. DGLM znoszą to ograniczenie, pozwalając, aby parametr dyspersji $\phi$ również zależał od cech danej obserwacji. W efekcie DGLM składa się z dwóch powiązanych ze sobą modeli:
* modelu dla wartości średniej (tak jak w standardowym GLM),
* modelu dyspersji.

Dzięki temu model może lepiej dopasować się do danych, w których zmienność nie jest stała.

Estymacja parametrów jest procesem iteracyjnym:

1. Dopasowanie GLM dla średniej odpowiedzi, ze stałym parametrem dyspersji $\phi$ dla wszystkich obserwacji.

2. Obliczenie wkładu każdej obserwacji do dewiacji i obliczenie kwadratu Pearsona lub dewiancji reszt $R_i^2$.

3. Dopasowanie GLM dla dyspersji, przyjmując jako zmienną objaśnianą $R_i^2$. Przyjmuje się rozkład Gamma i na tym etapie nie uwzględnia się wag. Dopasowane wartości stają się nowym parametrem dyspersji dla każdej obserwacji.

4. Dopasowanie GLM dla wartości średniej, ale tym razem z wykorzystaniem specyficznego dla każdej obserwacji parametru dyspersji (dzieląc wagę przez parametr dyspersji dla danej obserwacji uzyskany w poprzednim kroku).

5. Obliczenie kwadratu Pearsona lub dewiancji reszt $R_i^2$ i powtarzanie kolejnych kroków aż do osiągnięcia zbieżności parametrów (zmiany między kolejnymi iteracjami będą znikome).

---
**7.3: Przedstaw kluczowe etapy iteracyjnego procesu szacowania podwójnego uogólnionego modelu liniowego (DGLM - Double Generalized Linear Model). W jaki sposób model średniej i model dyspersji „współdziałają” podczas tego procesu?**

1. Dopasowanie GLM dla średniej odpowiedzi, ze stałym parametrem dyspersji $\phi$ dla wszystkich obserwacji.

2. Obliczenie wkładu każdej obserwacji do dewiacji i obliczenie kwadratu Pearsona lub dewiancji reszt $R_i^2$.

3. Dopasowanie GLM dla dyspersji, przyjmując jako zmienną objaśnianą $R_i^2$. Przyjmuje się rozkład Gamma i na tym etapie nie uwzględnia się wag. Dopasowane wartości stają się nowym parametrem dyspersji dla każdej obserwacji.

4. Dopasowanie GLM dla wartości średniej, ale tym razem z wykorzystaniem specyficznego dla każdej obserwacji parametru dyspersji (dzieląc wagę przez parametr dyspersji dla danej obserwacji uzyskany w poprzednim kroku).

5. Obliczenie kwadratu Pearsona lub dewiancji reszt $R_i^2$ i powtarzanie kolejnych kroków aż do osiągnięcia zbieżności parametrów (zmiany między kolejnymi iteracjami będą znikome).

* Model średniej $\rightarrow$ Model dyspersji: Model dla średniej dostarcza reszt ($R_i^2$), które są miarą tego, jak dobrze model ten pasuje do danych. Reszty te stają się zmienną objaśnianą dla modelu dyspersji. Duże reszty dla pewnych obserwacji wskazują na większą zmienność (dyspersję) w tej części danych.

* Model dyspersji $\rightarrow$ Model średniej: Model dyspersji, na podstawie analizy reszt, szacuje indywidualne parametry dyspersji $\phi_i$ dla każdej obserwacji. Parametry te są następnie wykorzystywane do aktualizacji wag w kolejnej iteracji dopasowania modelu dla średniej. Obserwacje o wyższej oszacowanej dyspersji (większej zmienności) otrzymują mniejszą wagę w procesie estymacji.

## 9: Teoria wartości ekstremalnych

**9.1: Krótko przedstaw czym zajmuje się Teoria Wartości Ekstremalnych (Extreme Value Theory, EVT) i wskaż możliwości jej wykorzystania przez aktuariusza.**

Teoria Wartości Ekstremalnych to gałąź statystyki służąca do modelowania rzadkich, ekstremalnych zdarzeń, które znajdują się w "ogonach" rozkładów prawdopodobieństwa. EVT umożliwia prognozowanie prawdopodobieństwa wystąpienia rzadkich zdarzeń o wartościach wyższych niż kiedykolwiek zaobserwowane.

Wykorzystanie przez aktuariusza:
* Modelowanie śmiertelności w najstarszych latach w celu zamykania tablic trwania życia, co jest niezbędne przy kalkulacji rent dożywotnich.
* Obliczania wysokich kwantyli (Value-at-Risk) na potrzeby wymogów kapitałowych.

---
**9.5: Jednym z głównych podejść wykorzystywanych w EVT jest analiza przekroczeń progu POT (Peaks Over Threshold). Krótko omów to podejście.**

Podstawową ideą metody POT jest założenie, że jeśli interesuje nas ogon rozkładu (np. bardzo wysokie roszczenia ubezpieczeniowe), możemy wybrać wysoki próg $u$ i analizować wszystkie wartości, które ten próg przekroczyły. Analizuje się nie same wartości, ale ich nadwyżki ponad ten próg, czyli wartości $Y−u$, pod warunkiem, że $Y>u.$

---
**9.5: Wskaż dlaczego w metodzie POT kluczową rolę odgrywa ustalenie progu przekroczeń na właściwym poziomie. Uzasadnij dlaczego w tym celu (ustaleniu progu) można wykorzystać funkcję wartości oczekiwanej nadwyżki (mean excess function).**

Ustalenie progu:
* Zbyt niski próg: jeśli wybierzemy zbyt niski próg, uwzględnimy w analizie obserwacje, które w rzeczywistości nie należą do "ekstremalnego" ogona rozkładu. Włączenie danych spoza ogona prowadzi do tego, że model jest niedopasowany, a uzyskane estymaty parametrów są obciążone (błędne).
* Zbyt wysoki próg: spowoduje, że będziemy mieli bardzo mało danych (nadwyżek) do analizy. Mała próba danych prowadzi do estymacji parametrów o dużej wariancji.

Funkcja wartości oczekiwanej nadwyżki:
* ma liniową postać po przekroczeniu odpowiedniego progu $u.$

---
**9.5: Wyjaśnij (odwołując się do odpowiedniego twierdzenia) dlaczego w modeluPOT (Peak Over Threshold) nadwyżki $Y=X-u\mid X>u$ ponad wysoki próg umodeluje się uogólnionym rozkładem Pareto (GPD). Zinterpretuj parametr kształtu $\xi$ (znak i konsekwencje dla „grubości” ogona) oraz podaj dwie praktyczne przesłanki wyboru progu $u$. Odpowiedź ogranicz do kilku precyzyjnych zdań.**

Użycie uogólnionego rozkładu Pareto (GPD) do modelowania nadwyżki $Y = X - u | X > u$ ponad wysoki próg $u$ w modelu POT (Peak Over Threshold) jest uzasadnione twierdzeniem Pickandsa-Balkemy-de Haana. Twierdzenie to wskazuje, że dla odpowiednio wysokich progów $u$, rozkład nadwyżek ponad ten próg może być dobrze przybliżony przez uogólniony rozkład Pareto.

Parametr kształtu $\xi$ (nazywany również indeksem ogona lub indeksem wartości ekstremalnej) określa zachowanie ogona rozkładu:
* $\xi > 0$: odpowiada rozkładom o grubych ogonach (heavy-tailed). Wskazuje to, że ogon zanika wolno, jak w przypadku funkcji potęgowej.
*   $\xi = 0$: granica wykładnicza, odpowiada rozkładom o lekkich ogonach.
*   $\xi < 0$: Odpowiada rozkładom o ograniczonym z góry nośniku (krótkim ogonie).

Dwie praktyczne przesłanki przy wyborze progu $u$ wynikają z kompromisu między obciążeniem a wariancją:
1. Na wykresie Mean-excess plot od danego rozpoczyna się stabilny, w przybliżeniu liniowy trend wzrostowy.
2. Na wykresie Hilla estymator parametru kształtu stabilizuje się w pewnym płaskim regionie, co wskazuje na znalezienie właściwego początku ogona rozkładu.

# Effective Statistical Learning Methods for Actuaries II

## 3: Drzewa regresyjne

**3.2: Wskaż co najmniej cztery reguły określające, kiedy węzeł w drzewie regresyjnym jest przyjmowany za końcowy (jest uznawany za liść).**

Węzeł jest uznawany za końcowy:
* jeśli zawiera mniej niż z góry określoną liczbę obserwacji.
* gdy jego głębokość (czyli odległość od korzenia drzewa) osiągnie ustalony limit.
* jeśli w wyniku tego podziału co najmniej jeden z nowo powstałych węzłów potomnych (liści) zawierałby mniej niż z góry określoną liczbę obserwacji.
* jeśli najlepszy możliwy podział tego węzła nie przynosi spadku dewiancji (miary błędu) o wartość większą niż ustalony próg.

---
**3.2: Omów jedną wybraną regułę określającą, kiedy węzeł w drzewie regresyjnym jest przyjmowany za końcowy (jest uznawany za liść).**

Proces podziału drzewa jest zatrzymywany, gdy osiągnie ono zdefiniowaną liczbę poziomów (głębokość). Głębokość węzła jest liczona od korzenia drzewa (który ma głębokość zero), a jego bezpośredni potomkowie mają głębokość o jeden większą.


---
**3.3: Na czym polega i w jakim celu stosuje się przycinanie drzewa regresyjnego?**

Przycinanie polega budowaniu maksymalnie rozbudowanego drzewa, pozwalając mu rosnąć aż do momentu, gdy dalsze podziały nie są możliwe (np. w liściach zostaje zbyt mało obserwacji lub wszystkie mają tę samą wartość). Takie drzewo jest bardzo złożone i idealnie dopasowane do danych treningowych. Następnie, w sposób systematyczny, usuwa się (przycina) całe gałęzie drzewa, czyli węzły wraz z ich potomkami. Celem jest znalezienie optymalnego poddrzewa, które stanowi najlepszy kompromis między prostotą a dokładnością predykcji.

## 4: Bagging Trees and Random Forests

**4.6: Przedstaw ideę i sposób konstrukcji wykresów PDP (Partial Dependence Plot).**

Główną ideą wykresów PDP jest pokazanie, jak zmiana wartości jednej lub dwóch wybranych cech wpływa na średnią predykcję modelu, przy jednoczesnym uśrednieniu efektów wszystkich pozostałych cech. Innymi słowy, wykres PDP ilustruje efekt krańcowy (marginalny) wybranej cechy na prognozę modelu.

Pozwala to na zrozumienie, czy zależność między cechą a predykcją jest liniowa, monotoniczna, czy bardziej złożona, co jest szczególnie przydatne w przypadku modeli takich jak lasy losowe czy sieci neuronowe.

Konstrukcja wykresu częściowej zależności dla pojedynczej cechy $x_S$ przebiega w następujących krokach:

1.  Wybór siatki wartości: Dla analizowanej cechy $x_S$ wybiera się zbiór interesujących wartości (tzw. siatkę), dla których będzie badany jej wpływ.
2.  Modyfikacja danych: Dla każdej obserwacji w zbiorze danych (np. uczącym) i dla każdej wartości z siatki:
    * Sztucznie ustawia się wartość cechy $x_S$ na daną wartość z siatki.
    * Wartości wszystkich pozostałych cech ($x_{\bar{S}}$) pozostawia się bez zmian.
3.  Predykcja: Model generuje predykcję dla każdej tak zmodyfikowanej obserwacji.
4.  Uśrednianie: Oblicza się średnią ze wszystkich predykcji uzyskanych w poprzednim kroku. Wynik jest pojedynczym punktem na wykresie PDP, odpowiadającym jednej wartości z siatki dla cechy $x_S$.
5.  Wizualizacja: Powtarza się kroki 2-4 dla wszystkich wartości z siatki, a następnie tworzy wykres, na którym oś X reprezentuje wartości cechy $x_S$, a oś Y – odpowiadające im średnie predykcje.

## 6: Inne miary do porównywania modeli

**6.3: Jakie są kluczowe różnice między krzywą Lorentza (Lorenz curve, $LC[\hat{\mu}(X);\alpha]$) a krzywą koncentracji (concentration curve, $CC[\mu(X), \hat{\mu}(X);\alpha]$) w kontekście oceny predyktora $\hat{\mu}(X)$.**

Główna różnica polega na tym, co każda z krzywych mierzy dla danego odsetka $\alpha$ polis o najniższych przewidywanych składkach:

* Krzywa Koncentracji (CC): Mierzy skumulowany udział rzeczywistych strat Y (lub, co jest równoważne, rzeczywistej, ale nieobserwowalnej, składki czystej $\mu(X)$). Innymi słowy, pokazuje, jaka część całkowitej szkody w portfelu jest generowana przez $\alpha\%$ polis uznanych przez predyktor za najbezpieczniejsze.
* Krzywa Lorenza (LC): Mierzy skumulowany udział przewidywanej składki $\hat{\mu}(X)$. Pokazuje, jaką część całkowitej sumy przewidywanych składek w portfelu stanowią składki zebrane od $\alpha\%$ polis uznanych za najbezpieczniejsze.

Podsumowując, krzywa Lorenza opisuje, jak predyktor rozdziela przewidywane składki, podczas gdy krzywa koncentracji ocenia, jak trafny jest ten podział w odniesieniu do rzeczywistych strat. Różnica między nimi jest miarą niedoskonałości modelu predykcyjnego.

---
**6.3: W jaki sposób porównanie krzywej Lorentza i krzywej koncentracji pozwala ocenić jakość predyktora $\hat{\mu}(X)$?**

W praktyce aktuarialnej celem jest, aby przewidywane składki $\hat{\mu}(X)$ były jak najbliższe rzeczywistym składkom $\mu(X)$. Dlatego porównanie obu krzywych jest kluczowym narzędziem oceny modelu:

* Odległość między krzywymi: Duża różnica między krzywą koncentracji a krzywą Lorenza sugeruje, że predyktor słabo przybliża prawdziwą składkę techniczną. Celem jest, aby wykresy obu krzywych były jak najbliżej siebie.
*  Miara ABC (Area Between Curves): Mniejsza wartość ABC oznacza, że predyktor jest lepszy, ponieważ jego struktura cenowa lepiej odzwierciedla strukturę rzeczywistego ryzyka.

---
**6.3: Co to jest „uporządkowana” krzywa Lorenza (ordered Lorenz curve)? W jaki sposób może być wykorzystana w taryfikacji?**

Uporządkowana krzywa Lorenza to narzędzie graficzne służące do porównywania predykcyjnej mocy dwóch modeli taryfikacji składek ubezpieczeniowych, na przykład starego modelu z nowym. Pozwala ocenić, czy nowy model lepiej identyfikuje grupy ryzyka, które były niedokładnie wycenione w starym modelu, minimalizując w ten sposób ryzyko selekcji negatywnej. Podstawowym elementem jest pojęcie względności (relativity), czyli stosunku nowej składki do starej dla każdego klienta:

$$R = \frac{\hat{\mu}_2(X)}{\hat{\mu}_1(X)}$$

Główne zastosowanie polega na identyfikacji segmentów portfela, które są źle wycenione przez obecny model, co naraża ubezpieczyciela na selekcję negatywną.

# An Introduction to Statistical Learning with Applications in R

## 2: Uczenie statystyczne

**2.2: Co rozumiemy przez pojęcia wariancja i obciążenie metody uczenia statystycznego?**

1. Wariancja odnosi się do tego, jak bardzo oszacowanie funkcji $\hat{f}$ zmieniłoby się, gdybyśmy je oszacowali na innym zbiorze danych treningowych. Mierzy ona wrażliwość modelu na niewielkie wahania w danych treningowych.
2. Obciążenie odnosi się do błędu, który jest wprowadzany przez przybliżenie bardzo skomplikowanego, rzeczywistego problemu za pomocą znacznie prostszego modelu. Innymi słowy, jest to błąd wynikający z założeń upraszczających, które przyjmujemy, aby ułatwić trenowanie funkcji docelowej.

## 4: Klasyfikacja

**4.4: Krótko omów wykorzystanie krzywej ROC do oceny modeli logistycznych.**

Idealna krzywa ROC "przytula" lewy górny róg wykresu, co oznacza wysoki odsetek prawdziwie pozytywnych wyników przy jednoczesnym niskim odsetku fałszywie pozytywnych wyników. Ogólna wydajność klasyfikatora, zsumowana dla wszystkich możliwych progów, jest podana przez pole pod krzywą ROC (AUC). Idealny klasyfikator ma AUC bliskie 1, podczas gdy klasyfikator, który działa nie lepiej niż losowe zgadywanie, ma AUC równe 0,5.

## 5: Metody repróbkowania

**5.1: Wyjaśnij w jaki sposób przeprowadza się k-krotną walidację krzyżową.**

K-krotna walidacja krzyżowa (k-fold CV) to procedura służąca do oszacowania błędu testowego modelu statystycznego poprzez wielokrotne dzielenie danych na zbiory uczące i walidacyjne.

Proces K-krotnej walidacji krzyżowej:

1. Podział danych: Dostępny zbiór obserwacji jest losowo dzielony na $k$ grup (nazywanych też *zbiorami* lub *foldami*) o w przybliżeniu równej wielkości.

2. Iteracyjne trenowanie i walidacja:
    * Pierwsza grupa (zbiór 1) jest traktowana jako zbiór walidacyjny, a model jest trenowany na pozostałych $k-1$ grupach (które łącznie tworzą zbiór uczący).
    * Oblicza się błąd predykcji (np. błąd średniokwadratowy, MSE) dla obserwacji w zbiorze walidacyjnym.
    * Proces ten jest powtarzany $k$ razy, przy czym za każdym razem inna grupa pełni rolę zbioru walidacyjnego.

3.  Obliczenie ostatecznego wyniku: Po przeprowadzeniu $k$ iteracji uzyskuje się $k$ różnych estymacji błędu testowego ($MSE_1, MSE_2, ..., MSE_k$). Ostateczną estymacją błędu w metodzie k-krotnej walidacji krzyżowej jest średnia z tych wartości:

    $$CV_{(k)} = \frac{1}{k}\sum_{i=1}^{k} MSE_i$$

---
**5.1: Podaj na czym polega walidacja za pomocą metody LOOCV (Leave-one-out cross-validation).**

Walidacja krzyżowa z pominięciem jednej obserwacji (Leave-one-out cross-validation, LOOCV) to intensywna obliczeniowo, ale czasami użyteczna metoda szacowania błędu testowego modelu statystycznego. Jest to szczególny przypadek k-krotnej walidacji krzyżowej, w którym liczba podzbiorów $(k)$ jest równa liczbie obserwacji $(n)$ w zbiorze danych.

Proces polega na wielokrotnym dopasowywaniu modelu, gdzie za każdym razem jedna obserwacja jest wykluczana ze zbioru uczącego i używana do walidacji.

---
**5.1: Jakie są zalety i wady k-krotnej walidacji krzyżowej w porównaniu z:**
* **i. podejściem wykorzystującym jedynie jeden zbiór walidacyjny,**
* **ii. metodą LOOCV.**

**W odpowiedzi uwzględnij problem kompromisu między obciążeniem a wariancją modelu.**

Wybór $k$ w walidacji krzyżowej to kompromis między obciążeniem a wariancją.
* LOOCV $(k=n)$ ma niskie obciążenie, ale wysoką wariancję.
* Podejście z jednym zbiorem walidacyjnym (odpowiednik $k=2$) ma wysokie obciążenie, ale niską wariancję.

K-krotna walidacja krzyżowa z wartościami $k=5$ lub $k=10$ jest w praktyce złotym środkiem. Empirycznie wykazano, że takie wartości prowadzą do estymacji błędu testowego, które nie cechują się ani nadmiernie wysokim obciążeniem, ani bardzo wysoką wariancją.

## 8: Metody oparte na drzewach

**8.1: Krótko przedstaw algorytm budowy binarnego drzewa klasyfikacyjnego.**

1.  Start (korzeń drzewa): Algorytm rozpoczyna się od jednego węzła (korzenia), który zawiera wszystkie obserwacje z zestawu treningowego.

2.  Znalezienie najlepszego podziału:
    *   Algorytm iteracyjnie przeszukuje wszystkie predyktory (zmienne) i wszystkie możliwe punkty podziału dla każdego z nich.
    *   Dla każdego potencjalnego podziału obliczana jest miara "czystości" (lub "zanieczyszczenia") nowo powstałych węzłów potomnych. Najczęściej stosowane miary to:
        *   Indeks Giniego (*Gini Index*)
        *   Entropia (*Entropy*)
    *   Wybierany jest ten predyktor i ten punkt podziału, który prowadzi do największego zysku informacyjnego, czyli największej redukcji zanieczyszczenia w węzłach potomnych w porównaniu do węzła macierzystego.

3.  Podział (rekurencja): Dane są dzielone na dwa nowe węzły (regiony) zgodnie z wybraną w kroku 2 regułą. Proces z kroku 2 jest następnie powtarzany rekurencyjnie dla każdego z nowo powstałych węzłów.

4.  Kryterium zatrzymania: Proces dzielenia jest zatrzymywany, gdy spełniony zostanie jeden z warunków, np.:
    *   Węzeł jest idealnie "czysty" (zawiera obserwacje tylko jednej klasy).
    *   Osiągnięto maksymalną, zdefiniowaną wcześniej głębokość drzewa.
    *   Liczba obserwacji w węźle spadła poniżej określonego progu.

---
**8.1: Co to jest kryterium dobroci podziału (goodness of split criterion) wykorzystywane w konstrukcji takiego drzewa. Omów jedno wybrane kryterium dobroci podziału.**

To funkcja matematyczna używana w algorytmie budowy drzewa decyzyjnego do oceny, jak "dobry" jest każdy potencjalny podział węzła. Celem jest znalezienie takiego podziału (czyli takiej zmiennej i takiego jej progu), który w najlepszy sposób dzieli obserwacje na dwie grupy, które są jak najbardziej jednorodne pod względem klasyfikacji.

Indeks Giniego jest zdefiniowany wzorem:

$$
G = \sum_{k=1}^{K} \hat{p}_{mk}(1 - \hat{p}_{mk}),
$$

jest to miara całkowitej wariancji we wszystkich $K$ klasach. Nietrudno zauważyć, że indeks Giniego przyjmuje małą wartość, jeśli wszystkie $\hat{p}_{mk}$ są bliskie zera lub jedynki. Z tego powodu indeks Giniego jest określany jako miara *czystości* węzła — mała wartość wskazuje, że węzeł zawiera w przeważającej mierze obserwacje z pojedynczej klasy.

---
**8.2: Krótko przedstaw ideę statystycznych metod uczenia zespołowego (Ensemble Statistical Learning).**

Metody uczenia zespołowego to podejścia, które łączą wiele prostych modeli w celu uzyskania jednego, lepszego modelu predykcyjnego. Głównym celem jest zmniejszenie wariancji i poprawa dokładności predykcyjnej w porównaniu do pojedynczego modelu poprzez uśrednienie wyników z wielu modeli zbudowanych na różnych próbkach danych. Ogólny wynik staje się bardziej stabilny i mniej podatny na specyfikę pojedynczego zbioru treningowego.

---
**8.2: Wymień co najmniej trzy takie metody wykorzystujące drzewa (Tree Ensemble Methods)**

* Bagging (agregacja bootstrapowa).
* Lasy losowe (Random Forests).
* Boosting.
* Bayesowskie addytywne drzewa regresyjne (Bayesian Additive Regression Trees, BART).

---
**8.2: Opisz jedną metodę spośród Tree Ensemble Methods**

Bagging

Mechanizm działania opiera się na idei, że uśrednianie zbioru obserwacji redukuje wariancję. Ponieważ zazwyczaj nie mamy dostępu do wielu niezależnych zbiorów treningowych, Bagging tworzy je sztucznie za pomocą techniki bootstrapu, czyli losowania ze zwracaniem z oryginalnego zbioru danych.

Proces składa się z następujących kroków:
1.  Tworzenie zbiorów bootstrapowych: z oryginalnego zbioru treningowego o $n$ obserwacjach tworzy się $B$ nowych zbiorów treningowych, każdy o rozmiarze $n$, poprzez losowanie ze zwracaniem. Każdy z tych zbiorów jest nieco inny.
2.  Budowanie modeli: na każdym z $B$ "bootstrapowych" zbiorów danych budowane jest osobne, głębokie i nieprzycinane drzewo decyzyjne. Każde z tych drzew ma niskie obciążenie (bias), ale wysoką wariancję.
3.  Agregacja predykcji: aby uzyskać ostateczną predykcję dla nowej obserwacji, wyniki z $B$ drzew są łączone:
    * W przypadku regresji (odpowiedź ilościowa), predykcje są uśredniane.
    * W przypadku klasyfikacji (odpowiedź jakościowa), ostateczna predykcja jest wynikiem głosowania większościowego – wybierana jest klasa najczęściej wskazywana przez poszczególne drzewa.

---
**8.2: Jako aktuariusz wykorzystujesz modele bazujące na drzewach decyzyjnych. Chcesz skonstruować model o jak najlepszych zdolnościach predykcyjnych. Rozważasz możliwość wykorzystania metody uczenia zespołowego boosting.**
* **a) Krótko opisz na czym polega ta metoda. Czy metoda boosting może być stosowana zarówno dla problemów regresji, jak i klasyfikacji?**
* **b) W jaki sposób metoda boosting różni się od metody bagging pod względem sposobu wykorzystania danych treningowych?**
* **c) Wymień i krótko opisz co najmniej dwa parametry dostrajania w metodzie boosting.**

a)

*Boosting* to metoda uczenia zespołowego, która, podobnie jak *bagging*, łączy wiele prostych modeli, zwanych "słabymi uczniami" (w tym kontekście drzewami decyzyjnymi), w jeden potężny model o wysokiej zdolności predykcyjnej.

Kluczową cechą tej metody jest to, że drzewa są budowane sekwencyjnie. Każde kolejne drzewo jest tworzone na podstawie informacji z drzew już istniejących w modelu. W przypadku problemu regresji, boosting działa w następujący sposób:
1.  Dopasowuje się drzewo decyzyjne do danych.
2.  Następnie kolejne drzewo jest dopasowywane nie do pierwotnej zmiennej odpowiedzi, ale do rezyduów (błędów) z poprzedniego modelu.
3.  Nowo utworzone drzewo jest dodawane do dopasowanej funkcji w celu aktualizacji rezyduów.

Dzięki temu podejściu model "uczy się powoli", stopniowo poprawiając swoje dopasowanie w obszarach, w których dotychczas działał słabo.

Metoda *boosting* jest podejściem ogólnym i może być stosowana zarówno w problemach regresji, jak i klasyfikacji.

b)

*Bagging* tworzy wiele niezależnych drzew na losowych próbkach z oryginalnego zbioru danych, podczas gdy *boosting* buduje drzewa sekwencyjnie, gdzie każde kolejne drzewo uczy się na błędach poprzednich, wykorzystując zmodyfikowaną wersję oryginalnego zbioru danych.

c)

1.  Liczba drzew $B$: liczba ta mówi ile razy model jest ponownie trenowany, jeśli liczba drzew B jest zbyt duża model może zostać przetrenowany. Z tego powodu parametr ten dobiera się za pomocą cross-walidacji.
2.  Parametr kurczenia (shrinkage) $\lambda$: Jest to mała dodatnia liczba, która kontroluje tempo, w jakim *boosting* się uczy. Typowe wartości to 0.01 lub 0.001. Mniejsze wartości $\lambda$ wymagają zazwyczaj większej liczby drzew $B$, aby osiągnąć dobrą wydajność.

## 12: Uczenie nienadzorowane

**12.1: Dlaczego PCA jest uważana za metodę uczenia bez nadzoru (unsupervised)?**

W metodach uczenia bez nadzoru model jest trenowany wyłącznie na podstawie danych wejściowych bez wiedzy o konkretnym wyniku czy klasie, do której miałby przyporządkować obserwacje. PCA analizuje wyłącznie struktury i zależności między zmiennymi w danych wejściowych, identyfikując ich korelacje, a następnie przekształca zbiór danych tak, aby uzyskać nowy zestaw zmiennych (składowe główne). W praktyce oznacza to, że PCA szuka wzorców i ukrytych struktur w danych, co czyni ją idealnym narzędziem do eksploracyjnej analizy danych, segmentacji czy redukcji wymiarowości,bez konieczności przypisania punktów danych do określonych kategorii czy przewidywania wyników.

---
**12.2: W jaki sposób analiza składowych głównych (PCA, Principal ComponentAnalysis) może być wykorzystana do analizy danych ubezpieczeniowych, takich jak ryzyko klienta lub analiza szkód?**

Na przykład do:
* redukcji zmiennych wpływających na profil ryzyka,
* segmentacji klientów według ryzyka,
* identyfikacji klientów o nietypowych profilach ryzyka,
* identyfikacji kluczowych czynników wpływających na wielkość szkód,
* monitorowania zmian w szkodowości portfela.

---
**12.4 Przedstaw przebieg procesu grupowania hierarchicznego według algorytmu aglomeracyjnego.**

1.  Inicjalizacja: na początku każda z $n$ obserwacji jest traktowana jako osobny, jednoelementowy klaster. Następnie obliczana jest macierz odległości (lub braku podobieństwa) między wszystkimi parami obserwacji, najczęściej przy użyciu odległości Euklidesowej.

2.  Iteracyjne łączenie: algorytm w każdym kroku zmniejsza liczbę klastrów o jeden.
    * Identyfikowane są dwa najbliższe (najbardziej podobne) klastry na podstawie wybranej miary odległości.
    * Te dwa klastry są łączone w jeden nowy, większy klaster.
    * Obliczana jest odległość nowo utworzonego klastra od wszystkich pozostałych.
    * Proces jest powtarzany $n-1$ razy, aż wszystkie obserwacje znajdą się w jednym, ostatecznym klastrze, tworząc kompletny dendrogram.

Wysokość, na której dwa klastry łączą się w dendrogramie, odpowiada odległości (brakowi podobieństwa) między nimi.

Łączenie pełne (Complete Linkage): odległość między dwoma klastrami to odległość między *najdalszymi* od siebie obserwacjami należącymi do tych klastrów.

---
**12.4: Co oznacza wykonanie „poziomego cięcia” na dendrogramie?**

Dendrogram to drzewiasta struktura, która przedstawia sposób łączenia obiektów w grupy (skupienia, klastry) na różnych poziomach podobieństwa. Poziome cięcie na określonej wysokości oznacza usunięcie połączeń powyżej tej wartości, co prowadzi do podziału obiektów na skupienia. Ich liczba zależy od wysokości, na której wykonano cięcie – im niżej, tym więcej mniejszych skupień, im wyżej, tym mniej większych.

---
**12.4: Dlaczego wysokość połączenia na dendrogramie jest ważna przy interpretacji wyników grupowania?**

Wysokość połączenia odzwierciedla odległość (niepodobieństwo) między grupowanymi obiektami lub skupieniami. Im wyżej następuje połączenie, tym większe różnice między skupieniami. Pomaga to wybrać odpowiednią liczbę skupień oraz zrozumieć strukturę danych.

# Regression Modeling with Actuarial and Financial Applications

## 7: Modelowanie trendów

**7.3: Wymień warunki stacjonarności (słabej) szeregu czasowego.**

Szereg czasowy $(y_t)_{t\in\mathbb{Z}}$ jest stacjonarny (słabo stacjonarny) jeżeli:
* wartość oczekiwana $E(y_t)$ nie zależy od $t$ $(E(y_t) = \mu, t \in \mathbb{Z}),$
* kowariancja między $y_s$ a $y_t$ zależy tylko od $\mid s - t\mid$ $(cov(y_s, y_t) = cov(y_s + k,y_t+k), s, t, k \in \mathbb{Z}).$

---
**7.4: Podaj definicję procesu błądzenia losowego.**

Proces błądzenia losowego definiuje się w następujący sposób: $y_t = y_{t-1} + c_t,$ gdzie $c_t$ jest procesem białego szumu.

---
**7.4: Wskaż i krótko przedstaw co najmniej dwie metody identyfikacji procesu błądzenia losowego.**

1. Czy przyrosty $y_t - y_{t-1}$ stanowią proces białego szumu. Proces białego szumu jest stacjonarny i nie wykazuje żadnych widocznych wzorców w czasie. W praktyce polega to na stworzeniu nowego szeregu $c_t = y_t - y_{t-1}$ i graficznej ocenie, czy jest on stacjonarny.
2. Czy odchylenie standardowe szeregu przyrostów jest istotnie mniejsze w porównaniu z odchyleniem standardowym oryginalnego szeregu.

# Statistical Foundations of Actuarial Learning and its Applications

## 4: Predictive Modeling and Forecast Evaluation

**4.3: Krótko przedstaw ideę metod bootstrapowych.**

Metody bootstrapowe należą do klasy metod symulacyjnych polegających na wnioskowaniu o interesującej nas wielkości na podstawie wielokrotnych replikacji oryginalnej próby. Przy czym replikacje uzyskuje się poprzez wielokrotne losowanie ze zwracaniem z próby (bootstrap nieparametryczny) lub założenie, że oryginalna próba pochodzi z ustalonej rodziny rozkładów, oszacowaniu jej parametrów (na podstawie oryginalnej próby), a następnie wylosowaniu z tego rozkładu replikacji (bootstrap parametryczny).

---
**4.3: Przedstaw algorytm postępowania w przypadku stosowania:**
* **nieparametrycznej metody bootstrapowej,**
* **parametrycznej metody bootstrapowej.**

Nieparametryczna metoda bootstrapowa:

1. Symulacja próby bootstrapowej: z oryginalnego zbioru danych $(Y_1, \dots, Y_n)$ losujemy $n$ obserwacji ze zwracaniem. Oznacza to, że każda obserwacja ma taką samą szansę na wylosowanie, a raz wylosowana obserwacja może zostać wylosowana ponownie. W ten sposób tworzymy nową, sztuczną próbkę danych $Y^*.$
2. Obliczenie estymatora: na podstawie nowo utworzonej próbki bootstrapowej $Y^*$

    obliczamy interesujący nas estymator (np. średnią, wariancję, współczynnik regresji), stosując tę samą regułę decyzyjną $A$, co dla oryginalnej próbki. Otrzymujemy w ten sposób pojedynczą estymatę bootstrapową $\hat{\theta}^* = A(Y^*).$
3. Powtórzenie: kroki 1 i 2 powtarzamy dużą liczbę razy, np. $M = 1000$ lub więcej, uzyskując zbiór $M$ estymat bootstrapowych 

    $$(\hat{\theta}^{*(1)}, \dots, \hat{\theta}^{*(M)}).$$

4. Analiza wyników: otrzymany zbiór estymat tworzy empiryczny rozkład bootstrapowy. Na jego podstawie możemy oszacować właściwości pierwotnego estymatora $\hat{\theta}$, takie jak jego błąd standardowy, lub skonstruować dla niego przedziały ufności.

Parametryczna metoda bootstrapowa:

1. Estymacja parametrów: na podstawie oryginalnego zbioru danych $(Y_1, \dots, Y_n)$ estymujemy nieznane parametry założonego rozkładu. Na przykład, jeśli zakładamy rozkład Poissona, estymujemy jego parametr $\lambda$. Otrzymujemy w ten sposób estymatę $\hat{\theta}$.
2. Symulacja próby bootstrapowej: generujemy nową, sztuczną próbkę danych $Y^*$ o wielkości $n$, losując obserwacje z dopasowanego rozkładu parametrycznego $F(\cdot; \hat{\theta})$. W przeciwieństwie do metody nieparametrycznej, nie losujemy tutaj z oryginalnych danych, lecz z rozkładu teoretycznego z wyestymowanymi parametrami.
3. Obliczenie estymatora: na podstawie nowo wygenerowanej próbki $Y^*$ 

    obliczamy interesujący nas estymator $\hat{\theta}^* = A(Y^*).$
4. Powtórzenie: kroki 2 i 3 powtarzamy dużą liczbę razy ($M$), uzyskując zbiór $M$ estymat bootstrapowych 

    $$( \hat{\theta}^{*(1)}, \dots, \hat{\theta}^{*(M)} ).$$

5. Analiza wyników: podobnie jak w metodzie nieparametrycznej, otrzymany zbiór estymat tworzy empiryczny rozkład bootstrapowy, który służy do analizy właściwości pierwotnego estymatora $\hat{\theta}$.

# Loss Models: From Data to Decisions

## 11: Estymacja metodą największej wiarygodności

**Na czym polega różnica między obserwacjami uciętymi (truncated data) a obserwacjami cenzurowanymi (censored data)? Wskaż i omów co najmniej jedną sytuację, w której aktuariusz może wykorzystywać:**
* **i. obserwacje ucięte,**
* **ii. obserwacje cenzurowane.**

Podstawowa różnica polega na ilości informacji dostępnej o obserwacji. W przypadku danych uciętych obserwacje spoza pewnego zakresu są całkowicie niewidoczne i nie są w ogóle rejestrowane. W przypadku danych cenzurowanych wiemy o istnieniu obserwacji, ale jej dokładna wartość jest nieznana.

Obserwacje ucięte (truncated data)

Obserwacja jest ucięta od dołu (left truncated) w punkcie $d$, jeśli jest rejestrowana tylko wtedy, gdy jej wartość jest większa od $d$. Jeżeli wartość jest równa lub mniejsza od $d$, obserwacja w ogóle nie jest zapisywana, a badacz nie wie o jej istnieniu.

i. Obserwacje ucięte

Aktuariusz analizuje dane dotyczące szkód komunikacyjnych. Polisy posiadają franszyzę integralną w wysokości $d = 1000$ zł. Ubezpieczony, którego szkoda jest niższa niż $1000$ zł, nie zgłasza jej, ponieważ nie otrzymałby odszkodowania.

ii. Obserwacje cenzurowane

Polisa ubezpieczeniowa pokrywa szkody do maksymalnej wysokości $u = 100 000$ zł. Jeśli rzeczywista szkoda jest wyższa (np. wynosi $150 000$ zł), ubezpieczyciel wypłaca $100 000$ zł i tylko ta informacja jest precyzyjnie rejestrowana.

## 14: Konstrukcja modeli empirycznych

**14.3: Podaj definicję danych prawostronnie cenzurowanych (right censoring). Wskaż i omów co najmniej dwie sytuacje, w których aktuariusz analizuje tego typu dane.**

Obserwacja cenzurowana prawostronnie w punkcie $u$, jeśli gdy jest równa lub większa od $u$, jest zapisywana jako równa 
$u$, ale gdy jest poniżej $u$, jest zapisywana z jej obserwowaną wartością.

W danych dotyczących roszczeń ubezpieczeniowych, obecność limitu polisy może prowadzić do prawostronnie cenzurowanych obserwacji. Gdy kwota szkody jest równa lub przekracza limit 
$u$, świadczenia powyżej tej wartości nie są wypłacane, więc dokładna wartość zazwyczaj nie jest rejestrowana. Wiadomo jednak, że wystąpiła szkoda o wartości co najmniej $u$.

Podczas przeprowadzania badania śmiertelności ludzi, jeśli osoba żyje w momencie zakończenia badania, nastąpiło cenzurowanie prawostronne. Wiek osoby w chwili śmierci nie jest znany, ale wiadomo, że jest on co najmniej tak duży jak wiek w momencie zakończenia badania.

---
**14.6: Jakie są najważniejsze zalety i ograniczenia jądrowej estymacji funkcji gęstości w porównaniu z innymi technikami, takimi jak histogramy czy estymatory parametryczne?**

Zalety estymacji jądrowej funkcji gęstości:
* Metoda nieparametryczna, nie wymaga założenia konkretnego rozkładu, co pozwala na bardziej ogólną analizę danych.
* Za jej pomocą otrzymuje się gładką funkcję gęstości, która może lepiej odzwierciedlać rzeczywisty rozkład danych niż histogramy, szczególnie gdy dane są mało liczne lub mają skomplikowany rozkład.
* Dzięki stałej wygładzania (szerokości jądra) można kontrolować stopień wygładzenia estymowanej gęstości. Większa wartość stałej prowadzi do bardziej wygładzonej funkcji gęstości, podczas gdy mniejsza bardziej precyzyjnie
odwzorowuje dane.
* Pozwala na porównywanie rozkładów różnych zestawów danych.

Ograniczenia jądrowej estymacji funkcji gęstości:
* Wymaga wyboru odpowiedniego jądra (np. gaussowskiego, Epanechikowa) oraz stałej wygładzania. Dobór tych parametrów może być subiektywny i wpływać na wyniki, a niewłaściwy ich wybór może prowadzić do błędnej estymacji rozkładu danych.
* Może być wymagająca obliczeniowo, szczególnie przy dużej ilości danych.
* Może niedokładnie odwzorować ogon rozkładu danych.

## 15: Selekcja modeli

**15.3: Przedstaw ideę i konstrukcję wykresu prawdopodobieństwo-prawdopodobieństwo (p-p plot, probability plot). Wskaż zastosowanie tego wykresu.**

Wykres prawdopodobieństwo-prawdopodobieństwo jest to jedna z graficznych metod oceny dopasowania modelu.
Konstrukcja:
* Wartości próbki porządkujemy w kolejności niemalejącej: $x_1 \le x_2 \le \cdots \le x_n.$
* W układzie współrzędnych zaznaczamy punkty o współrzędnych $(F_n(x_j), F(x_j)),$ $j = 1,2, ...,$ gdzie $F_n(x_j)$ są wartościami dystrybuanty empirycznej $F_n(x_j) = \frac{j}{n+1},$ a $F(x_j)$ – wartościami dystrybuanty dopasowanego rozkładu. Model jest dobrze dopasowany, jeśli punkty te leżą blisko linii $y=x.$

---
**15.4: Przedstaw ideę i konstrukcję testu ilorazu wiarygodności. Zapisz hipotezę zerową i alternatywną i wskaż czy różnią się one od hipotez (zerowej i alternatywnej) stawianych w testach zgodności (np. chi-kwadrat, Kołmogorowa-Smirnowa). Podaj postać statystyki testowej i jej rozkład.**

Test ilorazu wiarygodności jest narzędziem statystycznym służącym do porównywania dwóch konkurencyjnych modeli (rozkładów prawdopodobieństwa) w celu określenia, który z nich lepiej pasuje do obserwowanych danych.

Podstawowa idea polega na tym, że jeśli model bardziej złożony (hipoteza alternatywna) jest prawdziwy, to wymuszenie dopasowania prostszego modelu (hipoteza zerowa) powinno skutkować znacząco niższą wartością funkcji wiarygodności. 

Hipotezy:

$H_0$: Dane pochodzą z populacji o rozkładzie A (model prostszy).

$H_1$: Dane pochodzą z populacji o rozkładzie B (model bardziej złożony).

Kluczowym warunkiem jest, aby model w hipotezie zerowej był zagnieżdżony w modelu z hipotezy alternatywnej. Oznacza to, że model A można otrzymać z modelu B przez nałożenie ograniczeń na jego parametry (np. model wykładniczy jest szczególnym przypadkiem modelu gamma, gdy jeden z parametrów jest ustalony na 1).

Hipotezy w teście ilorazu wiarygodności różnią się od tych w testach zgodności, takich jak test chi-kwadrat czy test Kołmogorowa-Smirnowa. Testy zgodności sprawdzają, czy dane pochodzą z jednego, konkretnego rozkładu:

$H_0$: Dane pochodzą z populacji o danym rozkładzie.

$H_1$: Dane nie pochodzą z populacji o danym rozkładzie.

Statystyka testowa:

$T = 2 \ln\left(\frac{L_1}{L_0}\right) = 2(\ln L_1 - \ln L_0),$

gdzie $L_0$, $L_1$ to wiarygodności modeli z hipotezy zerowej i alternatywnej.

Dla dużych prób statystyka testowa $T$ ma w przybliżeniu rozkład chi-kwadrat ($\chi^2$). Liczba stopni swobody tego rozkładu jest równa różnicy w liczbie wolnych (niezależnych) parametrów między modelem z hipotezy alternatywnej a modelem z hipotezy zerowej.

# Quantitative Risk Management: Concepts, Techniques and Tools

## 3: Empiryczne własności danych finansowych

**3.1: Wymień i krótko scharakteryzuj trzy wybrane właściwości finansowych szeregów czasowych (tzw. stylizowane fakty).**

1. Brak rozkładu normalnego i grube ogony (heavy tails):
rozkład stóp zwrotu w finansowych szeregach czasowych nie jest rozkładem normalnym oraz posiada grubsze ogony. W praktyce oznacza to, że ekstremalne wartości (zarówno bardzo wysokie zyski, jak i straty) pojawiają się znacznie częściej, niż sugerowałby to standardowy model normalny. Jest to kluczowa właściwość z punktu widzenia zarządzania ryzykiem, ponieważ modele oparte na rozkładzie normalnym mogą systematycznie niedoszacowywać realnego ryzyka.
2. Grupowanie się zmienności (volatility clustering): jest to tendencja, zgodnie z którą okresy dużej zmienności (wysokich wahań cen) przeplatają się z okresami względnego spokoju (niskiej zmienności). Innymi słowy, duże zmiany cenowe często następują po sobie, tworząc "skupiska" lub "klastry", niezależnie od tego, czy są to wzrosty, czy spadki. Ta właściwość jest widoczna, gdy analizuje się szeregi wartości bezwzględnych lub kwadratów stóp zwrotu, które wykazują silną autokorelację.
3. Brak autokorelacji w surowych szeregach zwrotów: same stopy zwrotu są zazwyczaj nieskorelowane w czasie, co oznacza, że na podstawie przeszłych stóp zwrotu nie da się przewidzieć przyszłych. Jednak ich wartości bezwzględne (lub kwadraty), które są miarą zmienności, wykazują istotną, dodatnią i wolno wygasającą autokorelację. Jest to matematyczne potwierdzenie zjawiska grupowania się zmienności.

## 4: Finansowe szeregi czasowe

**4.1: Wymień etapy statystycznej analizy szeregów czasowych danych $y_1, y_2,..., y_t$. Krótko opisz jeden z nich.**

Etapy statystycznej analizy szeregów czasowych:
* Analiza wstępna
* Analiza w dziedzinie czasu
* Dopasowanie modelu
* Analiza reszt i porównanie modeli 

Analiza wstępna:

Jest to pierwszy etap, w którym dane są wizualizowane na wykresie w celu oceny, czy zastosowanie pojedynczego modelu stacjonarnego jest zasadne. Analiza wstępna obejmuje również rozważenie, czy konieczna jest wstępna obróbka danych, na przykład w celu usunięcia trendów lub sezonowości. Istotnym elementem tego etapu jest wybór odpowiedniej długości okna czasowego dla danych, co wiąże się z kompromisem między potrzebą korzystania z najbardziej aktualnych informacji a koniecznością posiadania wystarczająco dużej próbki do precyzyjnej estymacji statystycznej.

---
**4.1: Przedstaw sposób prognozowania szeregów czasowych za pomocą modeli ARMA. Podaj ogólne założenia i wskaż ideę.**

Podstawowym założeniem jest to, że dane pochodzą z odwracalnego modelu ARMA, a innowacje (błędy) procesu mają własność różnicy martyngałowej. Oznacza to, że oczekiwana wartość przyszłej innowacji, biorąc pod uwagę historię procesu, jest równa zero.

Główną ideą jest wykorzystanie warunkowej wartości oczekiwanej $E(X_{t+h} \mid \mathcal{F}_t)$ jako predyktora, gdzie $\mathcal{F}_t$ reprezentuje historię procesu do czasu $t$. Ten predyktor minimalizuje średniokwadratowy błąd prognozy. Prognozy oblicza się rekurencyjnie. Wartości losowe do czasu $t$ są traktowane jako "znane", a oczekiwane wartości przyszłych innowacji (dla $h \ge 1$) wynoszą zero. W praktyce, ponieważ pełna historia procesu nie jest znana, do obliczeń wykorzystuje się reszty z dopasowanego modelu. W miarę wydłużania horyzontu prognozy, przewidywana wartość zbiega do bezwarunkowej średniej procesu.

---
**4.1: Jakie cechy powinny posiadać reszty poprawnie zidentyfikowanego modelu ARMA?**

Powinny zachowywać się jak realizacja procesu białego szumu. Oznacza to, że reszty nie powinny wykazywać autokorelacji i mieć stałą wariancję.

---
**4.1: W jakim celu stosuje się test Ljunga–Boxa?**

Test Ljunga-Boxa jest używany do sprawdzania, czy w szeregu czasowym występuje autokorelacja, czyli zależność między wartościami tego szeregu w różnych momentach czasowych.

---
**4.1: Czym jest wygładzanie wykładnicze (exponential smoothing) i jakie jest jego główne zastosowanie w analizie szeregów czasowych?**

Wygładzanie wykładnicze to jedna z metod prognozowania i analizy szeregów czasowych, która nadaje większą wagę nowszym obserwacjom, jednocześnie stopniowo zmniejszając wpływ starszych danych. Jest to technika używana do wygładzania fluktuacji w danych, co ułatwia identyfikację trendów i wzorców. Główne zastosowania:
* Prognozowanie krótkoterminowe.
* Wygładzanie danych – redukcja szumów w danych poprzez eliminowanie nagłych skoków i anomalii.
* Modelowanie trendów i sezonowości – bardziej zaawansowane wersje, jak podwójne i potrójne wygładzanie wykładnicze (Holt-Winters), pozwalają uwzględniać trend i sezonowość w danych. 

Rodzaje wygładzania wykładniczego:
* Proste wygładzanie wykładnicze – stosowane do danych bez wyraźnego trendu ani sezonowości.
* Wygładzanie podwójne (Holt's method) – uwzględnia zarówno poziom, jak i trend.
* Wygładzanie potrójne (Holt-Winters method) – dodatkowo uwzględnia sezonowość.

Wygładzanie wykładnicze jest szczególnie cenione za swoją prostotę i skuteczność w prognozowaniu, zwłaszcza gdy dane wykazują krótkoterminowe fluktuacje.

---
**4.2: Podaj definicję procesu GARCH(p, q).**

Dla $t\in\mathbb{Z}$, niech $(Z_t)$ będzie procesem typu ścisły biały szum SWN(0, 1). Proces $(X_t)$ jest procesem $\text{GARCH}(p, q)$, jeśli jest ściśle stacjonarny i dla każdego $t \in \mathbb{Z}$ oraz dla pewnego procesu $(\sigma_t)$ o wartościach dodatnich spełnia równania:

$X_t = \sigma_t Z_t$

$\sigma_t^2 = \alpha_0 + \sum_{i=1}^{p} \alpha_i X_{t-i}^2 + \sum_{j=1}^{q} \beta_j \sigma_{t-j}^2$

gdzie: $\alpha_0 > 0$, $\alpha_i \ge 0$ dla $i=1,...,p$ oraz $\beta_j \ge 0$ dla $j=1,...,q$.

---
**4.2: Do jakich celów służą modele klasy GARCH?**

Modele klasy GARCH służą przede wszystkim do modelowania i prognozowania zmienności szeregów czasowych, zwłaszcza w kontekście finansowym. Ich głównym celem jest uchwycenie kluczowych empirycznych właściwości finansowych szeregów czasowych, których nie potrafią opisać prostsze modele.

* Modelowanie zmienności warunkowej.
* Uchwycenie grupowania zmienności: jest to kluczowe zjawisko na rynkach finansowych, gdzie okresy dużej zmienności (dużych wahań cen) przeplatają się z okresami względnego spokoju.
* Prognozowanie przyszłej zmienności.
* Obliczanie miar ryzyka finansowego: prognozy zmienności uzyskane z modeli GARCH są kluczowym wkładem do estymacji miar ryzyka, takich jak Value-at-Risk (VaR) i Expected Shortfall (ES). Umożliwiają one tworzenie warunkowych miar ryzyka, które dostosowują się do aktualnej sytuacji na rynku.
* Opisywanie dynamiki szeregów czasowych zwrotów z aktywów.

## 5: Teoria wartości ekstremalnych

**5.2: Krótko opisz podejście Hilla do modelowania ogonów rozkładów (m in. podaj założenia odnośnie rozkładów i przedstaw odpowiedni estymator).**

Metoda Hilla jest podejściem stosowanym do modelowania i estymacji ogonów rozkładów prawdopodobieństwa, zwłaszcza tych o grubych ogonach (heavy-tailed). Służy do oszacowania parametru kształtu ogona, znanego jako indeks ogona.

Podstawowym założeniem metody Hilla jest to, że funkcja przeżycia (ogon) badanego rozkładu dla dużych wartości $x$ zachowuje się jak funkcja potęgowa:

$$\bar{F}(x) = x^{-\alpha}L(x)$$

gdzie:
* $\alpha > 0$ to indeks ogona, który opisuje "ciężkość" ogona (im mniejsze $\alpha,$ tym grubszy ogon).
* $L(x)$ jest funkcją wolno zmienną, co oznacza, że zmienia się wolniej niż jakakolwiek funkcja potęgowa.

Estymator Hilla:

$$\hat{\alpha}^{(H)}_{k,n} = \left( \frac{1}{k} \sum_{j=1}^{k} \ln X_{j,n} - \ln X_{k,n} \right)^{-1}$$

gdzie:
* $k$ to liczba największych obserwacji użytych do estymacji $(2 \le k \le n).$
* $X_{j,n}$ to $j$-ta największa obserwacja w próbie.

---
**5.2: Przedstaw konstrukcję wykresu Hilla (Hill plot) i wskaż w jakim celu jest wykorzystywany.**

Aby wybrać optymalną wartość $k$, tworzy się tzw. wykres Hilla, który przedstawia wartości estymatora $\hat{\alpha}^{(H)}_{k,n}$ w funkcji $k$. Następnie poszukuje się na wykresie stabilnego regionu, w którym estymaty są względnie stałe, i na tej podstawie wybiera się ostateczne oszacowanie indeksu ogona $\alpha$.

Aby $k$-ty moment statystyczny (jak średnia czy wariancja) był skończony, wartość indeksu $\alpha$ musi być od tego $k$ większa. Np. wariancja (związana z 2 momentem, $k = 2$) jest skończona, jeśli $\alpha > 2$.

---
**5.2: Co to jest estymator Hilla i w jaki sposób jest używany do analizy danych?**

Estymator Hilla to narzędzie statystyczne należące do teorii wartości ekstremalnych (EVT), które służy do analizy rozkładów o tzw. "ciężkich ogonach" (heavy tails). Jego głównym celem jest oszacowanie indeksu ogona (tail index), oznaczanego jako $\alpha$.

---
**5.2: W jaki sposób estymator Hilla może być wykorzystany do modelowania dużych szkód w ubezpieczeniach majątkowych?**

Estymator Hilla znajduje zastosowanie w sytuacjach, gdzie kluczowe jest modelowanie szkód ekstremalnych (tzn. zdarzeń rzadkich, ale potencjalnie o dużej wartości). W ubezpieczeniach majątkowych jego użycie pozwala na lepsze zarządzanie ryzykiem i wycenę produktów ubezpieczeniowych. Jako przykład można wskazać:
* Wyznaczanie wysokości składki reasekuracyjnej. Firma ubezpieczeniowa zawiera umowę reasekuracyjną, aby zabezpieczyć się przed nadmiernymi stratami wynikającymi z ekstremalnych szkód (np. klęski żywiołowe). Estymator Hilla służy do oszacowania parametru grubości ogona rozkładu strat. Pozwala to na określenie prawdopodobieństwa wystąpienia szkody powyżej ustalonego progu.
* Modelowanie katastroficznych szkód majątkowych. W regionach zagrożonych katastrofami naturalnymi (huragany, powodzie) ubezpieczyciel musi oszacować wartość strat wynikających z rzadkich, ale ekstremalnych zdarzeń. Estymator Hilla pozwala na modelowanie ryzyka ekstremalnych szkód w oparciu o dane historyczne.

# Reinsurance: Actuarial and Statistical Aspects

## 9: Symulacje

**9.2: Wskaż, w których etapach procesu modelowania ryzyka: (i) kalibracja parametrów; (ii) wycena/ustalanie składek; (iii) kalkulacja kapitału (np. VaR/TVaR, SCR); (iv) stress testy/scenariusze, metoda Monte Carlo jest szczególnie użyteczna? Dla jednego ze wskazanych etapów podaj krótkie uzasadnienie (2-3 zdania), wskazując konkretny powód (np. złożoność modelu, brak formuł zamkniętych, zależności/ogony, nieliniowe wypłaty, itp.).**

(i) Kalibracja parametrów modelu

Kalibracja to proces dopasowywania parametrów modelu statystycznego do danych historycznych w taki sposób, aby model jak najlepiej odzwierciedlał rzeczywistość. W przypadku prostych modeli parametry można estymować analitycznie (np. metodą największej wiarygodności). Jednak w złożonych modelach funkcja wiarygodności może być niemożliwa do bezpośredniej maksymalizacji.

Metoda Monte Carlo jest szczególnie użyteczna, gdy nie ma zamkniętego wzoru na wiarygodność albo model obejmuje zależności i ciężkie ogony (np. kopule, mieszaniny,cenzurowanie). Umożliwia symulacyjną estymację parametrów (np. MLE wspierane symulacją, indirect inference czy Approximate Bayesian Computation) nawet wtedy, gdy gęstość jest trudna do zapisania. Dzięki temu można dopasować realistyczne modele bez upraszczania założeń.

(ii) Wycena i ustalanie składek

Wycena produktów ubezpieczeniowych (ustalanie składki) wymaga oszacowania wartości oczekiwanej przyszłych strat (tzw. składki czystej). Dla prostych produktów można to zrobić analitycznie. Jednak wiele nowoczesnych produktów ma skomplikowaną strukturę, która uniemożliwia proste obliczenia.

Metoda Monte Carlo pozwala na symulację ogromnej liczby możliwych scenariuszy przyszłych strat. Dla każdego scenariusza obliczana jest wartość wypłaty z ubezpieczenia. Średnia arytmetyczna z tych wypłat jest estymatorem wartości oczekiwanej straty. Pozwala to na wycenę nawet najbardziej skomplikowanych instrumentów. Metoda sprawdza się doskonale przy wycenie produktów, których wartość zależy od wielu skorelowanych czynników ryzyka (np. stopy procentowe, inflacja, kursy walut) oraz zawiera opcje, franszyzy, limity i inne nieliniowości. Przykładem może być wycena obligacji katastroficznych (CAT bonds), gdzie wypłata zależy od wystąpienia i skali zdarzenia naturalnego (np. huraganu), którego modelowanie jest niezwykle złożone.

(iii) Kalkulacja kapitału (VaR/TVaR, SCR)

Instytucje finansowe muszą utrzymywać kapitał na pokrycie nieoczekiwanych strat. Miary ryzyka takie jak Value-at-Risk (VaR) i Tail Value-at-Risk (TVaR) są standardem w ocenie wymogów kapitałowych (np. SCR w Solvency II). Obliczenie tych miar wymaga znajomości rozkładu prawdopodobieństwa zagregowanych strat całego portfela, co jest trywialne tylko w teorii.

Agregacja wielu zależnych od siebie ryzyk i modelowanie ogonów rozkładu. Analityczne wyznaczenie rozkładu sumy wielu zależnych zmiennych losowych o różnych rozkładach (często z grubymi ogonami) jest praktycznie niemożliwe. Metoda Monte Carlo pozwala "brutalną siłą" obliczeniową zbudować ten rozkład i precyzyjnie zmierzyć ryzyko w jego ekstremalnych obszarach (ogonach), co jest kluczowe dla wymogów kapitałowych.

(iv) Stress Testy i Analiza Scenariuszy

Stress testy polegają na ocenie, jak portfel lub cała instytucja zachowa się w warunkach ekstremalnych, ale prawdopodobnych kryzysów (np. krach na giełdzie, gwałtowny wzrost inflacji, wielka powódź). Celem jest zrozumienie odporności na szoki, które wykraczają poza standardowe założenia modelu.

Stresy są z natury wieloczynnikowe (np. skok częstości + wysokie szkody + szok rynkowy) i mogą obejmować nieliniowe efekty oraz zależności pomiędzy liniami/rynkami. MC pozwala generować spójne scenariusze i rozkłady wyników pod narzuconymi szokami, porównać wpływ na wyniki, rezerwy, kapitał oraz przeprowadzić odwrotny test warunków skrajnych i analizy wrażliwości bez przebudowy całego modelu.

**9.2: Opisz schemat estymacji metodą Monte Carlo składki $\pi = E[(S - d)^+]$ dla $S = \sum_{i=1}^{N} X_i$ (gdzie $N$ – zmienna losowa dla liczby szkód w okresie, $X_i$ – zmienne losowe dla wysokości szkód, $d$ - próg):**

* **co losujemy i w jakiej kolejności,**
* **jak definiujemy estymator $\hat{\pi}$ i jak szacujemy jego niepewność,**
* **w jednym zdaniu wskaż, jak w praktyce uwzględnia się zależności między szkodami w tym schemacie.**

1. Co losujemy i w jakiej kolejności

    Dla ścieżek $m = 1, \dots, n$:
    1.  Liczba szkód: wylosuj $N^{(m)}$ z dopasowanego rozkładu (np. Poissona, ujemnego dwumianowego).
    2.  Wysokość szkód: wylosuj niezależnie $X_1^{(m)}, \dots, X_{N^{(m)}}^{(m)}$ z dopasowanego rozkładu (np. lognormalnego, gamma, Pareto).
    3.  Agregacja i wypłata: policz $S^{(m)} = \sum_{i=1}^{N^{(m)}} X_i^{(m)}$ oraz $Y^{(m)} = (S^{(m)} - d)^+$.

2. Niepewność
    * Estymator składki (MC):
        $$
        \hat{\pi} = \frac{1}{n} \sum_{m=1}^{n} Y^{(m)}
        $$
    * Niepewność:

        $SE(\hat{\pi}) = \frac{\hat{s}}{\sqrt{n}}$, gdzie $\hat{s}^2 = \frac{1}{n-1} \sum_{m=1}^{n} (Y^{(m)} - \hat{\pi})^2$

        Przedział ufności dla poziomu $1 - \alpha$:

        $\hat{\pi} \pm u_{1-\alpha/2} \hat{s}$ ($u_{1-\alpha/2}$ - kwantyl rozkładu normalnego standardowego).

3. Zależności między szkodami w obrębie portfela, między liniami lub między $N$ i $X_i$ uwzględnia się na etapie generowania przez wspólny czynnik (*latent factor*, *common shock*) lub kopułę.

# Krajowy standard aktuarialny - praktyka aktuarialna

## 2: Właściwe praktyki

**2.5: Przedstaw wytyczne Krajowego Standardu Aktuarialnego w zakresie stosowania modeli (tj. wyboru, tworzenia, modyfikowania i przeliczania modeli) dotyczące:**
* **a) ryzyka modelu,**
* **b) walidacji modeli,**
* **c) wykorzystania wyników przebiegu modelu.**

a) Aktuariusz powinien zapewnić, że ryzyka modelu zostały zidentyfikowane, ocenione i że istnieją odpowiednie działania mające na celu ograniczenie takich ryzyk, takie jak odpowiednia walidacja modelu, dokumentacja i kontrola.

b) Aktuariusz powinien mieć pewność, że została przeprowadzona odpowiednia walidacja modelu. Walidacja modelu obejmuje ocenę, czy:
* Model jest dopasowany do zamierzonego celu prac. Kwestie, które aktuariusz powinien rozważyć, tam gdzie mają one zastosowanie, obejmują dostępność, poziom szczegółowości i  jakość danych wejściowych wymaganych przez modele, adekwatność rozpoznanych powiązań oraz zdolność modelu do generowania odpowiedniego zakresu wyników wokół oczekiwanych wartości;
* Model spełnia specyfikacje; oraz
* Pełne lub częściowe wyniki modelu są powtarzalne lub czy jakiekolwiek różnice są objaśnialne.

Walidacja modelu powinna być przeprowadzona przez osobę (osoby), która nie tworzyła modelu, chyba że spowoduje to obciążenie niewspółmierne do ryzyka modelu.

c) Aktuariusz powinien wykorzystując wyniki przebiegu modelu:
* Być przekonanym, że spełnione zostały warunki zastosowania modelu;
* Być przekonanym, że do danych wejściowych i wyjściowych są zastosowane odpowiednie kontrole;
* Rozważyć, czy walidację modelu opisaną w pkt. b) należy przeprowadzić w całości czy częściowo;
* Rozumieć, a w stosownych przypadkach, wyjaśnić istotne różnice między różnymi uruchomieniami modelu i być przekonanym, że istnieje odpowiedni proces kontroli uruchomień modelu. W przypadku modeli stochastycznych aktuariusz stosujący model powinien się upewnić, że wykonano wystarczającą liczbę uruchomień modelu i rozumieć
znaczące różnice między poszczególnymi przebiegami modelu;
* Rozumieć wszystkie działania zarządu lub reakcje zarządcze przyjęte w modelu. We wszystkich raportach aktuariusz powinien ujawnić takie zakładane działania zarządu lub reakcje zarządcze (ang. management actions) przyjęte w modelu oraz ich szeroko rozumiane implikacje.
* Udokumentować, w stosownych przypadkach, ograniczenia, dane wejściowe, kluczowe założenia, cel zastosowania i wyniki modelu.

---
**2.10 Przedstaw wytyczne Krajowego Standardu Aktuarialnego w zakresie jakości danych dotyczące:**
* **walidacji danych,**
* **braku danych.**

Walidacja danych: aktuariusz powinien podjąć uzasadnione kroki w celu sprawdzenia spójności, kompletności i dokładności wykorzystywanych danych. Możliwe kroki to między innymi:

* a. Uzgodnienie z audytowanymi sprawozdaniami finansowymi, zestawieniami obrotów i sald lub innymi stosownymi dokumentami, jeżeli są one dostępne;
* b. Przetestowanie danych pod kątem racjonalności w stosunku do zewnętrznych lub niezależnych danych;
* c. Przetestowanie danych pod kątem wewnętrznej spójności i spójności z innymi istotnymi informacjami; oraz
* d. Porównywanie danych z danymi za poprzedni okres lub okresy. Aktuariusz powinien opisać te kroki we wszystkich tworzonych raportach.

Brak danych: aktuariusz powinien wziąć pod uwagę możliwy wpływ wszelkich braków w danych (takich jak nieadekwatność, niespójność i niekompletność) na wyniki pracy. Braki, które prawdopodobnie nie będą miały istotnego wpływu na wyniki, nie muszą być dalej rozpatrywane. Jeżeli aktuariusz nie może znaleźć zadowalającego sposobu usunięcia braków, powinien rozważyć:

* a. Odmowę podjęcia lub kontynuowania świadczenia usług zawodowych;
* b. Współpracę ze zleceniodawcą w celu modyfikacji usług zawodowych lub uzyskania odpowiednich dodatkowych danych lub innych informacji; lub
* c. Z zastrzeżeniem zgodności z kodeksem etyki zawodowej, wykonanie usług zawodowych w najlepszy możliwy sposób i ujawnienie braków danych we wszystkich raportach (oraz wskazując potencjalny wpływ tych braków w danych).

# Actuarial Aspects of ERM for InsuranceCompanies

## 3: Enterprise Risk Management System

**3.5: Wymień co najmniej 4 czynniki, które należy wziąć pod uwagę podczas projektowania modelu. Krótko opisz dwa spośród nich.**

1. Cel i proporcjonalność.
2. Czy model jest odpowiedni do mierzonych ryzyk.
3. Czas wykonania.
4. Ograniczenia.

* Czas wykonania: modele wewnętrzne mogą wiązać się z długim czasem wykonania, zwłaszcza jeśli stosowane są scenariusze stochastyczne. Dostępnych jest kilka technik pomagających skrócić czas wykonania, a aktuariusz powinien rozważyć i ocenić każdy potencjalny negatywny wpływ na dokładność. Przykłady technik skracających czas obejmują grupowanie danych w punkty modelowe, stosowanie scenariuszy deterministycznych zamiast stochastycznych dla portfeli bez opcji, równoważne rozwiązania analityczne (w postaci zamkniętej), zmniejszenie liczby scenariuszy stochastycznych oraz redukcję granularności czasowej. Ponadto, czasy wykonania można poprawić, stosując techniki redukcji wariancji podczas generowania scenariuszy stochastycznych, takie jak zmienne antytetyczne.

* Ograniczenia: modele zawsze będą miały ograniczenia statystyczne i teoretyczne. Nigdy nie można oczekiwać, że wyniki w pełni odwzorują świat rzeczywisty. Ważne jest, aby pamiętać o tych ograniczeniach podczas projektowania modelu i komunikowania jego wyników. Ważnym aspektem jest dokumentacja wszelkich istotnych ograniczeń w celu zapewnienia, że użytkownicy modelu są ich świadomi.

# Reinsurance: Actuarial and Statistical Aspects

## 9: Symulacje

**9.2: Opisz koncepcję redukcji wariancji w metodzie Monte Carlo za pomocą metody próbkowania ważonego (metody IS - importance sampling).**

Załóżmy ponownie, że $F_X$ dopuszcza gęstość $f_X$. Ideą próbkowania z wagami jest teraz przejście z $f_X$ na inną gęstość $f_{\tilde{X}}$, która koncentruje się bardziej na interesującym nas regionie. Taka nowa gęstość $f_{\tilde{X}}$ może być uzyskana z $f_X$ przez przesunięcie, przeskalowanie, przekształcenie itp. Wielkość $f_X(x)/f_{\tilde{X}}(x)$ nazywana jest funkcją ilorazu wiarygodności i jest równa naszej wadze. Mamy wtedy

$$ E(X) = \int x f_X(x)dx = \int \left(x \frac{f_X(x)}{f_{\tilde{X}}(x)}\right) f_{\tilde{X}}(x)dx = E\left(\tilde{X} \frac{f_X(\tilde{X})}{f_{\tilde{X}}(\tilde{X})}\right). $$

Zamiast tego symulujemy $n$ niezależnych replikacji $\tilde{X_1}, \dots, \tilde{X_n}$ z nowej zmiennej losowej $\tilde{X}$ (o gęstości $f_{\tilde{X}}$) i używamy estymatora próbkowania z wagami

$$ \hat{\mu}_{n}^I = \frac{1}{n} \sum_{i=1}^{n} \tilde{X}_i \frac{f_X(\tilde{X}_i)}{f_{\tilde{X}}(\tilde{X}_i)}. $$

# Inne

**Czy histogram dystrybuanty jest przydatny w ocenie jakości oszacowanych modeli, odpowiedź uzasadnij.**

Histogram dystrybuanty jest bardzo przydatne w ocenie jakości oszacowanych modeli. Histogram dystrybuanty to histogram wartości otrzymanych z tzw. transformaty całkowej prawdopodobieństwa (Probability Integral Transform - PIT). Jeżeli ciągła zmienna losowa $X$ posiada dystrybuantę $F$, to $F(X) \sim U(0, 1)$, gdzie $U(0, 1)$ oznacza rozkład jednostajny na przedziale $(0,1).$ Oznacza to, że idealny histogram powinien być płaski – wszystkie słupki powinny mieć zbliżoną wysokość, oscylującą wokół czerwonej linii (gęstość równa 1).

---
**Wyjaśnij związek między wiarygodnością L, a kryterium informacyjnym AIC i wskaż kiedy każdy z tych mierników może być użyty do porównania różnych modeli.**

$\text{AIC} = 2p - 2\ln(L),$

czyli AIC jest zdefiniowane za pomocą wiarygodności.

* Wiarygodność może być użyta, gdy porównywane modele są zagnieżdżone (jeden model jest uproszczoną wersją drugiego).
* Kryterium AIC może być użyte, gdy modele nie są zagnieżdżone lub gdy zakładają różne rozkłady dla zmiennej odpowiedzi.

---
**Wyjaśnij do czego służy odległość Cooka (Cook's distance) i dlaczego jest różna dla różnych modeli.**

Odległość Cooka jest wykorzystywana w analizie regresji jako miara wpływu poszczególnych obserwacji na wyniki regresji. Umożliwia wykrycie obserwacji, które znacząco wpływają na wyniki regresji, a tym samym pozwala zbadać ich wpływ na model.W mierze Cooka uwzględnia się reszty modeli dlatego jej wartość jest różna dla różnych modeli.

---
**Jaką rolę w wykrywaniu oszustw ubezpieczeniowych odgrywają techniki statystyczne, takie jak test chi-kwadrat czy analiza regresji?**

Techniki statystyczne, jak test chi-kwadrat i analiza regresji pomagają identyfikować podejrzane wzorce i anomalia w danych, co może świadczyć o nieuczciwych działaniach. Test chi-kwadrat pozwala na szybkie wykrycie nietypowych rozkładów lub zależności,podczas gdy analiza regresji umożliwia głębsze zrozumienie zmiennych wpływających na ryzyko oszustwa. 

Na przykład:
* Zastosowanie testu chi-kwadrat:o Analiza liczby zgłaszanych roszczeń w określonych kategoriach (np.rodzaj szkody, czas zgłoszenia) w celu identyfikacji nietypowych wzorców.
    * Porównanie rozkładu częstości zgłaszanych roszczeń w różnych segmentach klientów, aby wykryć nadreprezentację podejrzanych roszczeń.
    * Sprawdzenie, czy występuje istotna statystycznie różnica między częstotliwością podejrzanych roszczeń a ogólną liczbą zgłoszeń.
* Zastosowanie regresji:
    * Ocena wpływu czynników, takich jak wiek zgłaszającego, liczba wcześniejszych roszczeń, miejsce zamieszkania, typ polisy na prawdopodobieństwo wystąpienia oszustwa.
    * Budowa modeli predykcyjnych, które klasyfikują zgłoszenia jako podejrzane lub prawidłowe.
    * Analiza reszt, aby identyfikować odstające obserwacje, które mogą sugerować nietypowe i potencjalnie oszukańcze zachowania.

Techniki statystyczne są często stosowane w połączeniu z metodami eksploracji danych(data mining) i uczeniem maszynowym, co zwiększa skuteczność wykrywania oszustw.