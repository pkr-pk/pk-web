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

**Dewiancja skalowana** (ang. *scaled deviance*) to dewiancja podzielona przez parametr dyspersji:

$$\tilde{D}(\mathbf{y}, \hat{\mathbf{\mu}}) = \frac{D(\mathbf{y}, \hat{\mathbf{\mu}})}{\phi}$$

Dla dużych prób, **rozkład dewiancji skalowanej** można przybliżyć **rozkładem chi-kwadrat ($\chi^2$)** z liczbą stopni swobody równą $n - p - 1$, gdzie $n$ to liczba obserwacji, a $p+1$ to liczba szacowanych parametrów w modelu.

**Dlaczego dewiancja jest niewystarczająca**

Podczas wyboru najlepszego modelu predykcyjnego spośród zagnieżdżonych uogólnionych modeli liniowych, sama dewiancja nie jest wystarczającą miarą. Dzieje się tak, ponieważ **dodanie kolejnych zmiennych do modelu prawie zawsze zmniejszy jego dewiancję** (lub w najgorszym przypadku pozostawi ją bez zmian). Prowadzi to do ryzyka **przeuczenia** (ang. *overfitting*), czyli stworzenia modelu, który jest zbyt skomplikowany i świetnie dopasowuje się do danych uczących, ale traci zdolność do generalizacji i przewidywania nowych obserwacji.

Dlatego, aby dokonać właściwego wyboru, należy uwzględnić kompromis między **dobrocią dopasowania** (niską dewiancją) a **złożonością modelu** (liczbą parametrów). Służą do tego **kryteria informacyjne**, takie jak **kryterium informacyjne Akaikego (AIC)** lub **Bayesowskie kryterium informacyjne (BIC)**, które "karzą" model za posiadanie większej liczby parametrów. Model o niższej wartości kryterium informacyjnego jest uznawany za lepszy, ponieważ oferuje najlepszy kompromis między dopasowaniem a złożonością.

---

## Metoda Hilla

Metoda Hilla jest alternatywą dla modelowania opartego na uogólnionym rozkładzie Pareto (GPD), przeznaczoną specjalnie dla rozkładów ciężkoogonowych (należących do dziedziny przyciągania rozkładu Frécheta).

Główne punkty:

* Cel metody: głównym celem Metody Hilla nie jest modelowanie całej dystrybucji nadwyżek ponad próg, lecz bezpośrednie oszacowanie indeksu ogona ($\alpha$). Indeks ten opisuje, jak szybko maleje prawdopodobieństwo w ogonie rozkładu.

* Estymator Hilla: estymacja odbywa się za pomocą estymatora Hilla, który jest funkcją $k$ największych statystyk pozycyjnych z próby $n$ obserwacji.

* Wykres Hilla: w praktyce, kluczowym narzędziem jest wykres Hilla, który przedstawia wartość estymowanego indeksu ogona w zależności od liczby użytych statystyk pozycyjnych ($k$). Analityk poszukuje na wykresie stabilnego regionu, który sugeruje właściwą wartość indeksu ogona. Interpretacja wykresu może być jednak trudna.

* Estymacja ogona rozkładu: wyestymowany indeks ogona jest następnie używany do skonstruowania estymatora ogona Hilla, który pozwala szacować prawdopodobieństwa w ogonie rozkładu strat powyżej progu.

Estymator Hilla to narzędzie statystyczne służące do estymacji (szacowania) indeksu ogona rozkładu prawdopodobieństwa. Indeks ogona, oznaczany jako $\alpha$, jest miarą "ciężkości" ogona rozkładu. Rozkłady o ciężkich ogonach charakteryzują się tym, że prawdopodobieństwo wystąpienia wartości ekstremalnych (bardzo dużych lub bardzo małych) jest znacznie wyższe niż w przypadku rozkładów o lekkich ogonach, takich jak rozkład normalny.

Estymator Hilla znajduje zastosowanie w sytuacjach, gdzie kluczowe jest modelowanie szkód ekstremalnych (tzn. zdarzeń rzadkich, ale potencjalnie o dużej wartości). W ubezpieczeniach majątkowych jego użycie pozwala na lepsze zarządzanie ryzykiem i wycenę produktów ubezpieczeniowych. Jako przykład można wskazać:

* Wyznaczanie wysokości składki reasekuracyjnej. Firma ubezpieczeniowa zawiera umowę reasekuracyjną, aby zabezpieczyć się przed nadmiernymi stratami wynikającymi z ekstremalnych szkód (np. klęski żywiołowe). Estymator Hilla służy do oszacowania parametru grubości ogona rozkładu strat. Pozwala to na określenie prawdopodobieństwa wystąpienia szkody powyżej ustalonego progu.

* Modelowanie katastroficznych szkód majątkowych. W regionach zagrożonych katastrofami naturalnymi (huragany, powodzie) ubezpieczyciel musi oszacować wartość strat wynikających z rzadkich, ale ekstremalnych zdarzeń. Estymator Hilla pozwala na modelowanie ryzyka ekstremalnych szkód w oparciu o dane historyczne.

---

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

## Uporządkowana krzywa Lorenza

Uporządkowana krzywa Lorenza to narzędzie graficzne służące do porównywania predykcyjnej mocy dwóch modeli taryfikacji składek ubezpieczeniowych, na przykład starego modelu z nowym. Pozwala ocenić, czy nowy model lepiej identyfikuje grupy ryzyka, które były niedokładnie wycenione w starym modelu, minimalizując w ten sposób ryzyko selekcji negatywnej.

Uporządkowana krzywa Lorenza to wykres, który powstaje przez porównanie dwóch modeli predykcyjnych: starego ($\hat{\mu}_1$) i nowego ($\hat{\mu}_2$). Kluczowym elementem jest pojęcie **względności (relativity)**, czyli stosunku nowej składki do starej dla każdego klienta:

$$R = \frac{\hat{\mu}_2(X)}{\hat{\mu}_1(X)}$$

Niska wartość $R$ oznacza, że nowy model proponuje znacznie niższą składkę niż stary, co sugeruje, że dany klient przepłacał w dotychczasowej taryfie.

Krzywa jest wykreślana w następujący sposób:
1.  **Sortowanie:** Wszystkie polisy z portfela (zestawu walidacyjnego) są sortowane według rosnącej wartości wskaźnika względności $R$.
2.  **Osie wykresu:** Wykres przedstawia punkty, których współrzędne to skumulowane udziały:
    * **Oś X:** Udział sumy składek ze **starego modelu** ($\hat{\mu}_1$) dla polis o najniższej względności.
    * **Oś Y:** Udział sumy **rzeczywistych szkód** (lub prawdziwej, choć nieobserwowalnej, składki technicznej $\mu(X)$) dla tej samej grupy polis.

Każdy punkt $(x, y)$ na krzywej oznacza, że grupa polis stanowiąca $x\%$ sumy starych składek (tych, którym nowy model najbardziej obniża cenę) odpowiada za $y\%$ sumy wszystkich szkód.

**Jak jest wykorzystywana w taryfikacji?**

Uporządkowana krzywa Lorenza jest praktycznym narzędziem do oceny, czy nowy model taryfikacji ($\hat{\mu}_2$) przynosi poprawę w stosunku do starego modelu ($\hat{\mu}_1$).

Główne zastosowanie polega na identyfikacji segmentów portfela, które są źle wycenione przez obecny model, co naraża ubezpieczyciela na **selekcję negatywną**.

Interpretacja wykresu jest następująca:
* Jeśli krzywa znajduje się **powyżej linii równości** (przekątnej 45 stopni), oznacza to, że dla danego segmentu polis udział w szkodach jest niższy niż udział w składkach pobieranych według starej taryfy.
* Taka sytuacja wskazuje, że stary model **zawyżał składki** dla tej grupy klientów. Nowy model prawidłowo to identyfikuje, proponując im niższe ceny (co skutkuje niską wartością względności $R$).

**Praktyczny wniosek:** Identyfikacja takiego segmentu jest kluczowa, ponieważ konkurenci z dokładniejszymi modelami mogliby zaoferować tym klientom niższe składki, "podbierając" ich z portfela. Ubezpieczyciel straciłby w ten sposób rentownych klientów. Uporządkowana krzywa Lorenza wizualizuje więc zdolność nowego modelu do lepszego dopasowania składek do rzeczywistego ryzyka i obrony portfela przed konkurencją.

---

## Wygładzanie wykładnicze

Wygładzanie wykładnicze to jedna z metod prognozowania i analizy szeregów czasowych, która nadaje większą wagę nowszym obserwacjom, jednocześnie stopniowo zmniejszając wpływ starszych danych. Jest to technika używana do wygładzania fluktuacji w danych, co ułatwia identyfikację trendów i wzorców. Główne zastosowania:

* Prognozowanie krótkoterminowe.
* Wygładzanie danych – redukcja szumów w danych poprzez eliminowanie nagłych skoków i anomalii.
* Modelowanie trendów i sezonowości – bardziej zaawansowane wersje, jak podwójne i potrójne wygładzanie wykładnicze (Holt-Winters), pozwalają uwzględniać trend i sezonowość w danych.

Rodzaje wygładzania wykładniczego:

* Proste wygładzanie wykładnicze – stosowane do danych bez wyraźnego trendu ani sezonowości.
* Wygładzanie podwójne (Holt's method) – uwzględnia zarówno poziom, jak i trend.
* Wygładzanie potrójne (Holt-Winters method) – dodatkowo uwzględnia sezonowość. Wygładzanie wykładnicze jest szczególnie cenione za swoją prostotę i skuteczność w prognozowaniu, zwłaszcza gdy dane wykazują krótkoterminowe fluktuacje.

---

## Interakcja czynników ryzyka

Interakcja w kontekście czynników ryzyka ubezpieczeniowego odnosi się do sytuacji, w której wpływ jednego czynnika ryzyka na prawdopodobieństwo wystąpienia szkody zależy od obecności innego czynnika ryzyka. Oznacza to, że efekty dwóch (lub więcej) zmiennych nie są jedynie sumą ich indywidualnych wpływów, ale mogą się wzmacniać lub osłabiać w zależności od ich wzajemnego oddziaływania. Różnica między interakcją a korelacją:

* Korelacja mierzy stopień współzmienności dwóch zmiennych, czyli na ile ich wartości są statystycznie powiązane (np. wzrost jednej zmiennej towarzyszy wzrostowi drugiej).
* Interakcja odnosi się do sposobu, w jaki jedna zmienna modyfikuje wpływ drugiej na określone zjawisko, np. ryzyko szkody. Może oznaczać, że efekt jednej zmiennej występuje tylko pod warunkiem obecności drugiej. 

Korelacja sama w sobie nie oznacza interakcji – dwie zmienne mogą być silnie skorelowane, ale nie muszą wpływać na siebie nawzajem w sposób interakcyjny. Dlatego w analizie ryzyka ubezpieczeniowego ważne jest stosowanie modeli, które uwzględniają nie tylko współzależności, ale także potencjalne efekty interakcji między czynnikami.

---

## Techniki statystyczne w wykrywaniu oszustw

Techniki statystyczne, jak test chi-kwadrat i analiza regresji pomagają identyfikować podejrzane wzorce i anomalia w danych, co może świadczyć o nieuczciwych działaniach. Test chi-kwadrat pozwala na szybkie wykrycie nietypowych rozkładów lub zależności, podczas gdy analiza regresji umożliwia głębsze zrozumienie zmiennych wpływających na ryzyko oszustwa. Na przykład:

* Zastosowanie testu chi-kwadrat: 
    * Analiza liczby zgłaszanych roszczeń w określonych kategoriach (np.rodzaj szkody, czas zgłoszenia) w celu identyfikacji nietypowych wzorców.
    * Porównanie rozkładu częstości zgłaszanych roszczeń w różnych segmentach klientów, aby wykryć nadreprezentację podejrzanych roszczeń.
    * Sprawdzenie, czy występuje istotna statystycznie różnica między częstotliwością podejrzanych roszczeń a ogólną liczbą zgłoszeń.

* Zastosowanie regresji:
    * Ocena wpływu czynników, takich jak wiek zgłaszającego, liczba wcześniejszych roszczeń, miejsce zamieszkania, typ polisy na prawdopodobieństwo wystąpienia oszustwa.
    * Budowa modeli predykcyjnych, które klasyfikują zgłoszenia jako podejrzane lub prawidłowe.
    * Analiza reszt, aby identyfikować odstające obserwacje, które mogą sugerować nietypowe i potencjalnie oszukańcze zachowania.

Techniki statystyczne są często stosowane w połączeniu z metodami eksploracji danych(data mining) i uczeniem maszynowym, co zwiększa skuteczność wykrywania oszustw.

---

## Rozkład Tweedie

W modelach aktuarialnych opartych na rodzinie rozkładów Tweedie, parametr $\xi$ kontroluje zależność wariancji od wartości oczekiwanej, co bezpośrednio wpływa na heteroskedastyczność modelu. Związek ten opisuje równanie wariancji:

$$Var(Y) = \phi \mu^\xi$$

gdzie: 

$\phi$ – parametr skali,

$\mu$ – wartość oczekiwana,

$\xi$ – parametr kształtu (exponent parameter). Im większe $\xi$, tym silniejsza heteroskedastyczność, co oznacza, że wariancja bardziej zależy od wartości oczekiwanej.

Rozkład Tweedie w ramach uogólnionych modeli liniowych (GLM) jest stosowany do modelowania łącznej kwoty roszczeń, która jest wypadkową zarówno ich liczby, jak i wysokości. Rozkłady te, dla parametru potęgowego (wykładnika) $\xi$ z przedziału (1, 2), odpowiadają złożonemu rozkładowi Poissona z sumami o rozkładzie Gamma.

W tym podejściu:

* Liczba roszczeń (składnik częstotliwości) jest modelowana przy użyciu rozkładu Poissona.
* Wysokość pojedynczego roszczenia (składnik szkodowości) jest modelowana przy użyciu rozkładu Gamma.

**Rola zmiennych objaśniających i ograniczenia modelu**

Głównym ograniczeniem standardowego modelu Tweedie GLM jest założenie o stałym parametrze dyspersji $\phi$. To założenie narzuca istotne ograniczenie na wpływ zmiennych objaśniających na składniki ryzyka:

* Każdy czynnik ryzyka (zmienna objaśniająca), który wpływa na oczekiwaną wysokość roszczenia (składnik Gamma), musi również wpływać na oczekiwaną liczbę roszczeń (składnik Poissona) w tym samym kierunku. Oznacza to, że jeśli dany czynnik zwiększa średnią szkodę, musi również zwiększać średnią częstotliwość roszczeń, aby parametr dyspersji $\phi$ pozostał stały.

Ograniczenie to często jest sprzeczne z rzeczywistymi obserwacjami w ubezpieczeniach. Na przykład:

* W rezerwach szkodowych oczekiwana liczba wypłat zazwyczaj maleje w kolejnych latach rozwoju szkody, podczas gdy średnia kwota wypłaty rośnie.
* W ubezpieczeniach komunikacyjnych czynniki geograficzne mogą działać w przeciwnych kierunkach – w dużych miastach obserwuje się wyższą częstotliwość szkód, ale niższą ich średnią wysokość.

Ze względu na te przeciwstawne tendencje, stosowanie modelu Tweedie z stałym parametrem dyspersji może prowadzić do zniekształcenia analizy.

---

## Dendrogram

Dendrogram to drzewiasta struktura, która przedstawia sposób łączenia obiektów w grupy (skupienia, klastry) na różnych poziomach podobieństwa. Poziome cięcie na określonej wysokości oznacza usunięcie połączeń powyżej tej wartości, co prowadzi do podziału obiektów na skupienia. Ich liczba zależy od wysokości, na której wykonano cięcie – im niżej, tym więcej mniejszych skupień, im wyżej, tym mniej większych.

Wysokość połączenia odzwierciedla odległość (niepodobieństwo) między grupowanymi obiektami lub skupieniami. Im wyżej następuje połączenie, tym większe różnice między skupieniami. Pomaga to wybrać odpowiednią liczbę skupień oraz zrozumieć strukturę danych.

---

## POT peaks over threshold

Wybór odpowiedniego progu `u` jest kluczowy, ponieważ wiąże się z fundamentalnym kompromisem między **obciążeniem** (błędem systematycznym) a **wariancją** (niestabilnością) oszacowań parametrów.

Konsekwencje niewłaściwego wyboru progu są następujące:
* **Wybór zbyt wysokiego progu `u`**: Powoduje, że do analizy trafia bardzo mało obserwacji (nadwyżek ponad próg). Prowadzi to do oszacowań o dużej wariancji, co oznacza, że są one **niestabilne i mało precyzyjne**.
* **Wybór zbyt niskiego progu `u`**: Skutkuje włączeniem do analizy obserwacji, które nie pochodzą z ekstremalnego ogona rozkładu. Dla tych danych założenie o uogólnionym rozkładzie Pareto (GPD) może nie być spełnione, co prowadzi do uzyskania **obciążonych, czyli systematycznie błędnych, oszacowań**.

Celem jest znalezienie najniższego możliwego progu, powyżej którego model GPD staje się trafną aproksymacją zachowania danych w ogonie rozkładu.

---

## Dane cenzurowane i ucięte

1. **Cenzurowanie z prawej strony** (ang. *right censored*) ma miejsce, gdy dla obserwacji osiągającej lub przekraczającej pewną wartość `u`, rejestruje się jedynie fakt, że wartość ta została osiągnięta, ale jej dokładna wielkość pozostaje nieznana. Obserwacje poniżej progu `u` są rejestrowane z ich dokładną wartością.

2. **Okrojenie z lewej strony** (ang. *left truncated*) występuje, gdy obserwacje poniżej pewnego progu `d` w ogóle nie są rejestrowane. W przypadku okrojenia nie wiedzielibyśmy nawet o istnieniu szkód, których wartość nie przekroczyła jakiegoś progu.

3. **Przykład dla danych cenzurowanych** Jeśli obserwacja ubezpieczonego kończy się przed jego śmiercią, jedyne, co wiemy, to to, że zgon następuje w pewnym momencie po czasie ostatniej obserwacji. Inną częstą sytuacją jest limit polisy, w przypadku którego, jeśli rzeczywista strata przekracza limit, wiadomo jedynie, że limit został przekroczony.

4. **Przykład dla danych uciętych** W przypadku polis sprzedanych przed rozpoczęciem okresu obserwacji, część ubezpieczonych umrze, podczas gdy inni dożyją, by rozpocząć obserwację. Nie tylko czasy ich zgonów nie zostaną zarejestrowane, ale nawet nie będziemy wiedzieć, ile ich było. Inną częstą sytuacją jest franszyza redukcyjna. Szkody poniżej franszyzy nie są rejestrowane i nie ma danych o tym, ile szkód było poniżej jej wartości.

---

## PDP Partial Dependence Plot

Głównym problemem w interpretacji złożonych modeli jest trudność w zwizualizowaniu funkcji predykcyjnej, gdy zależy ona od więcej niż dwóch zmiennych (cech). Wykresy częściowej zależności (Partial Dependence Plots) rozwiązują ten problem, pokazując **marginalny wpływ** wybranego, małego podzbioru cech na wynik predykcji modelu.

Koncepcja polega na uśrednieniu wpływu wszystkich pozostałych cech, co pozwala na wyizolowanie i graficzne przedstawienie zależności między analizowaną cechą a prognozą. Innymi słowy, wykres pokazuje, jak zmieniłaby się średnia predykcja modelu, gdybyśmy zmieniali wartość jednej cechy, zachowując jednocześnie rozkład pozostałych cech z całego zbioru danych.

### Sposób Konstrukcji

Konstrukcja wykresu PDP dla jednej wybranej cechy $x_S$ odbywa się poprzez następujące kroki, które stanowią estymację funkcji częściowej zależności na podstawie zbioru treningowego:

1.  **Wybierz cechę**, której wpływ chcesz zbadać (np. wiek kierowcy).
2.  **Wybierz konkretną wartość** dla tej cechy (np. wiek = 30 lat).
3.  Dla **każdej obserwacji** w zbiorze danych:
    * Zastąp oryginalną wartość wybranej cechy ustaloną wartością (np. dla każdego kierowcy w zbiorze ustaw wiek na 30 lat).
    * Pozostaw wartości wszystkich pozostałych cech bez zmian.
4.  Dla każdej tak zmodyfikowanej obserwacji **wygeneruj predykcję** za pomocą modelu.
5.  **Uśrednij wszystkie uzyskane predykcje**. Wynik to pojedynczy punkt na wykresie częściowej zależności dla wartości "wiek = 30 lat".
6.  **Powtórz kroki 2-5** dla całego zakresu interesujących wartości wybranej cechy (np. dla wieku od 18 do 90 lat), aby uzyskać pełny wykres.

W ten sposób wykres pokazuje, jak zmienia się średnia predykcja modelu w zależności od wartości jednej cechy, po uśrednieniu efektów wszystkich innych zmiennych.

---

## Model ARMA

Reszty (ang. *residuals*) poprawnie zidentyfikowanego modelu ARMA powinny posiadać cechy **białego szumu** (ang. *white noise*). Oznacza to, że reszty powinny być **nieskorelowane w czasie** i mieć **stałą wariancję**.

Test Ljunga-Boxa jest używany do sprawdzania, czy w szeregu czasowym występuje autokorelacja, czyli zależność między wartościami tego szeregu w różnych momentach czasowych.

---

## DGLM - Double Generalized Linear Model

Proces estymacji podwójnego uogólnionego modelu liniowego (DGLM) jest **procesem iteracyjnym**, który naprzemiennie dopasowuje model dla wartości średniej i model dla dyspersji, aż do osiągnięcia zbieżności. Modele te "współdziałają" ze sobą, wymieniając się informacjami na każdym etapie.

### Kluczowe etapy procesu

1. Dopasuj GLM dla wartości średniej, ze stałym $\phi$ dla wszystkich obserwacji.

2. Oblicz wkład każdej obserwacji do dewiacji i oblicz kwadrat Pearsona lub dewiancję residuów $R_i^2$.

3. Dopasuj GLM dla dyspersji, przyjmując jako zmienną objaśnianą kwadraty residuów $R_i^2$. Przyjmuje się rozkład Gamma i na tym etapie nie uwzględnia się wag. Dopasowane wartości stają się nowym parametrem dyspersji dla każdej obserwacji.

4. Dopasuj GLM dla wartości średniej, ale tym razem z wykorzystaniem specyficznego dla każdej obserwacji parametru dyspersji (dzieląc wagę przez parametr dyspersji dla danej obserwacji, uzyskany w poprzednim kroku).

5. Oblicz kwadrat Pearsona lub dewiancję residuów $R_i^2$ i powtórz poprzednie kroki.

### Współdziałanie modeli

Model średniej i model dyspersji są ze sobą ściśle powiązane i wymieniają się informacjami w każdej iteracji:

* **Model średniej dostarcza informacji modelowi dyspersji**: Poprzez obliczonie $R_i^2$, model średniej informuje model dyspersji, które obserwacje są bardziej zmienne.
* **Model dyspersji dostarcza informacji modelowi średniej**: Poprzez oszacowane, indywidualne parametry dyspersji ($\phi_i$), model dyspersji informuje model średniej, jaką wagę nadać każdej obserwacji. Obserwacjom o wyższej zmienności (większej dyspersji) przypisuje się mniejszą wagę w procesie estymacji modelu dla wartości średniej, co pozwala na ignorowanie szumu i wychwytywanie sygnału.

### Ograniczenie standardowego modelu Tweedie GLM

Podwójny uogólniony model liniowy (DGLM) jest szczególnie istotny w modelowaniu z wykorzystaniem regresji Tweedie’ego, ponieważ standardowy model Tweedie GLM narzuca **nierealistyczne ograniczenie** dotyczące wpływu czynników ryzyka na częstość i wysokość szkód.

W standardowym modelu GLM parametr dyspersji $\phi$ musi być **stały** dla wszystkich obserwacji. W przypadku rozkładu Tweedie, który jest modelem złożonym Poissona-Gamma, parametr dyspersji $\phi$ zależy zarówno od parametrów rozkładu częstości szkód (Poisson), jak i rozkładu wysokości pojedynczej szkody (Gamma).

To założenie o stałości $\phi$ prowadzi do następującego, kluczowego ograniczenia:
> Każdy czynnik ryzyka, który zwiększa oczekiwaną wysokość szkody, musi również zwiększać oczekiwaną częstość szkód (i odwrotnie). Wpływ danego czynnika na częstość i wysokość szkody **musi iść w tym samym kierunku**.

Podwójny GLM (DGLM) rozwiązuje ten problem, ponieważ **pozwala, aby parametr dyspersji $\phi$ również zależał od zmiennych objaśniających**. Modelując dyspersję za pomocą osobnego zestawu predyktorów, DGLM uwalnia sztywną zależność między komponentami częstości i wysokości szkody. Dzięki temu model może prawidłowo odzwierciedlić sytuacje, w których dany czynnik ryzyka ma różny lub nawet przeciwstawny wpływ na częstość i wysokość szkód, co prowadzi do znacznie bardziej wiarygodnych wyników.

---

## Krzywa ROC

### Podniesienie progu

Podwyższenie progu sprawia, że model zmniejsza liczbę przypadków oznaczonych jako oszukańcze. Oznacza to, że więcej rzeczywistych oszustw pozostaje niewykrytych. Firma traci pieniądze na wypłatach, które nie powinny mieć miejsca.Koszt niewykrycia jednego oszustwa może być wysoki, zwłaszcza gdy wartość roszczenia jest duża. W przypadku bardzo wysokich kosztów niewykrycia oszustwa wzrost progu może prowadzić do znacznych strat, szczególnie jeśli oznacza to liczne,niewykryte przypadki oszustwa.

### Obniżenie progu

Obniżenie progu skutkuje większą liczbą przypadków oznaczonych jako oszustwa,nawet gdy są to faktycznie roszczenia prawdziwe. Wiąże się to z tym, że więcej niewinnych roszczeń zostaje błędnie sklasyfikowanych jako oszukańcze. Może to generować koszty administracyjne, ponieważ każda podejrzana sprawa wymaga dodatkowego procesu weryfikacji. Dodatkowo odrzucone niesłusznie roszczenia mogą prowadzić do niezadowolenia klientów, zwiększenia liczby reklamacji i potencjalnych strat związanych z utratą klientów. Jeżeli zatem koszty dodatkowej weryfikacji i utraty klientów przeważają nad korzyściami wykrycia dodatkowych oszustw, obniżenie progu może zmniejszać zyski firmy.

Krzywa ROC (Receiver Operating Characteristic) to narzędzie graficzne służące do oceny jakości modeli klasyfikacyjnych, w tym modeli regresji logistycznej. Ilustruje ona zdolność modelu do rozróżniania między dwiema klasami (np. klient przedłuży umowę vs. nie przedłuży).

* Osie wykresu: Krzywa ROC jest wykreślana w dwuwymiarowej przestrzeni, gdzie:

    * Oś Y reprezentuje czułość (Sensitivity), czyli odsetek przypadków pozytywnych (Y=1), które zostały prawidłowo sklasyfikowane. Inaczej nazywana jest wskaźnikiem trafień (True Positive Rate).

    * Oś X reprezentuje 1 - swoistość (1 - Specificity), czyli odsetek przypadków negatywnych (Y=0), które zostały błędnie sklasyfikowane jako pozytywne. Nazywana jest wskaźnikiem fałszywych alarmów (False Positive Rate).

* Interpretacja krzywej: Każdy punkt na krzywej ROC odpowiada parze (czułość, 1-swoistość) dla określonego progu klasyfikacji. Idealny model miałby krzywą przebiegającą blisko lewego górnego rogu wykresu, co oznaczałoby wysoką czułość i wysoką swoistość (niski wskaźnik fałszywych alarmów) jednocześnie. Linia przerywana pod kątem 45 stopni reprezentuje model losowy (nieposiadający żadnej mocy predykcyjnej).

* Pole pod krzywą (AUC): Jakościową miarą podsumowującą całą krzywą jest pole pod krzywą ROC (AUC - Area Under the Curve). Przyjmuje ono wartości od 0 do 1, gdzie:

    * AUC = 1 oznacza klasyfikator idealny.

    * AUC = 0.5 oznacza klasyfikator losowy.

    * AUC > 0.5 oznacza, że model ma zdolność predykcyjną lepszą niż losowa. Im wartość AUC jest bliższa 1, tym lepsza jest ogólna zdolność modelu do rozróżniania klas, niezależnie od wybranego progu klasyfikacji.

---

## PCA principal component analysis

W jaki sposób analiza składowych głównych (PCA, Principal Component Analysis) może być wykorzystana do analizy danych ubezpieczeniowych, takich jak ryzyko klienta lub analiza szkód?

Na przykład do:
* redukcji zmiennych wpływających na profil ryzyka,
* segmentacji klientów według ryzyka,
* identyfikacji klientów o nietypowych profilach ryzyka,
* identyfikacji kluczowych czynników wpływających na wielkość szkód,
* monitorowania zmian w szkodowości portfela.

Dlaczego PCA jest uważana za metodę uczenia bez nadzoru (unsupervised)?

W metodach uczenia bez nadzoru model jest trenowany wyłącznie na podstawie danych wejściowych bez wiedzy o konkretnym wyniku czy klasie, do której miałby przyporządkować obserwacje. PCA analizuje wyłącznie struktury i zależności między zmiennymi w danych wejściowych, identyfikując ich korelacje, a następnie przekształca zbiór danych tak, aby uzyskać nowy zestaw zmiennych (składowe główne). W praktyce oznacza to, że PCA szuka wzorców i ukrytych struktur w danych, co czyni ją idealnym narzędziem do eksploracyjnej analizy danych, segmentacji czy redukcji wymiarowości,bez konieczności przypisania punktów danych do określonych kategorii czy przewidywania wyników.

---

## Regresja liniowa

**Obserwacja wpływowa** to taka, której niewielka zmiana lub pominięcie w zbiorze danych w istotny sposób modyfikuje oszacowania parametrów modelu.

Wpływ obserwacji na model można ocenić za pomocą kilku miar:

* **Dźwignia** (Leverage): Jest to ogólna miara wpływu, zdefiniowana jako wielkość pochodnej i-tej dopasowanej wartości względem j-tej wartości odpowiedzi. Wartości dźwigni, nazywane również hat values, wskazują na potencjalny wpływ obserwacji na dopasowane wartości. Duża dźwignia zazwyczaj oznacza, że cechy danej obserwacji są nietypowe w porównaniu z resztą danych.
* **Odległość Cooka** (Cook's Distance): Ta miara ocenia, jak bardzo zmienia się cały wektor szacowanych współczynników regresji po pominięciu pojedynczej obserwacji. Mierzy ona odległość między parametrami oszacowanymi na pełnym zbiorze danych a parametrami oszacowanymi na zbiorze z pominiętą i-tą obserwacją. Duże wartości wskazują na obserwacje, które znacząco wpływają na oszacowania współczynników.

---

## Reszty Pearsona

W diagnostyce uogólnionych modeli liniowych (GLM) stosowanie reszt Pearsona jest korzystniejsze niż zwykłych reszt (surowych), ponieważ reszty Pearsona mają w przybliżeniu stałą wariancję, co ułatwia ich interpretację i porównywanie.

* **Zwykłe reszty**, definiowane jako $r_i = y_i - \hat{\mu}_i$, mają wadę polegającą na tym, że ich wariancja nie jest stała. W wielu rozkładach z rodziny ED, w tym w rozkładzie Poissona, wariancja zmiennej odpowiedzi zależy od jej wartości oczekiwanej ($Var(Y_i) = \mu_i$). To oznacza, że im większa jest przewidywana wartość $\hat{\mu}_i$, tym większej wariancji reszty surowej możemy się spodziewać. Utrudnia to ocenę, czy dana reszta jest "duża" – ta sama wartość reszty może być nieistotna dla obserwacji o dużej wariancji, a bardzo znacząca dla obserwacji o małej wariancji.
* **Reszty Pearsona** rozwiązują ten problem poprzez standaryzację. Dzielą one zwykłą resztę przez oszacowane odchylenie standardowe zmiennej odpowiedzi ($\sqrt{Var(\hat{\mu}_i)}$). Dzięki temu skalowaniu, reszty Pearsona mają (przynajmniej w przybliżeniu) stałą wariancję, niezależną od wartości dopasowanej $\hat{\mu}_i$. Umożliwia to bezpośrednie porównywanie reszt dla różnych obserwacji i ułatwia identyfikację obserwacji odstających oraz sprawdzanie założeń modelowych, takich jak poprawność wybranej funkcji wariancji.

---

## Wytyczne w zakresie stosowania modeli

### Walidacja modelu

Walidacja modelu obejmuje ocenę, czy:

* **Model jest dopasowany do zamierzonego celu pracy**. W tym kontekście aktuariusz powinien wziąć pod uwagę takie aspekty jak:
    * Dostępność, jakość i poziom szczegółowości danych wejściowych wymaganych przez model.
    * Adekwatność powiązań rozpoznanych w modelu.
    * Zdolność modelu do generowania odpowiedniego zakresu wyników wokół oczekiwanych wartości.
* **Model spełnia swoje specyfikacje**.
* **Wyniki modelu (pełne lub częściowe) są powtarzalne**, a wszelkie ewentualne różnice dają się wyjaśnić.

Standard wskazuje, że walidacja modelu **powinna być przeprowadzona przez osobę lub osoby, które nie tworzyły danego modelu**. Odstępstwo od tej zasady jest możliwe tylko wtedy, gdyby jej zastosowanie powodowało obciążenie niewspółmierne do ryzyka związanego z modelem. Dodatkowo, przy wykorzystywaniu wyników z konkretnego uruchomienia modelu, aktuariusz powinien rozważyć, czy walidacja nie powinna zostać przeprowadzona ponownie w całości lub w części.

### Walidacja Danych

Aktuariusz powinien podjąć uzasadnione kroki w celu sprawdzenia spójności, kompletności i dokładności wykorzystywanych danych. Możliwe działania obejmują między innymi:

* **Uzgodnienie z dokumentami finansowymi**: Porównanie danych z zaudytowanymi sprawozdaniami finansowymi, zestawieniami obrotów i sald lub innymi odpowiednimi dokumentami, jeśli są dostępne.
* **Testowanie racjonalności**: Porównanie danych z danymi zewnętrznymi lub niezależnymi w celu oceny ich racjonalności.
* **Sprawdzenie spójności wewnętrznej**: Przetestowanie danych pod kątem ich wewnętrznej spójności oraz spójności z innymi istotnymi informacjami.
* **Porównanie z danymi historycznymi**: Zestawienie danych z danymi za poprzedni okres lub okresy.

Aktuariusz jest zobowiązany opisać podjęte kroki walidacyjne we wszystkich tworzonych raportach.

### Postępowanie w Przypadku Braku Danych

W przypadku stwierdzenia braków w danych (takich jak nieadekwatność, niespójność czy niekompletność), aktuariusz musi wziąć pod uwagę ich możliwy wpływ na wyniki pracy.

1.  **Ocena istotności**: Jeżeli braki w danych prawdopodobnie nie będą miały istotnego wpływu na wyniki, nie muszą być dalej rozpatrywane.
2.  **Postępowanie przy istotnych brakach**: Jeżeli aktuariusz nie jest w stanie w zadowalający sposób usunąć istotnych braków, powinien rozważyć jedną z poniższych opcji:
    * **Odmówić lub przerwać świadczenie usług** zawodowych.
    * **Współpracować ze zleceniodawcą** w celu modyfikacji zlecenia lub uzyskania dodatkowych, odpowiednich danych.
    * **Wykonać usługi w najlepszy możliwy sposób**, jednocześnie ujawniając we wszystkich raportach informacje o brakach w danych oraz wskazując ich potencjalny wpływ na wyniki.

---

## Drzewa

### Na czym polega metoda *boosting* i czy można ją stosować do problemów regresji i klasyfikacji?

**Boosting** (wzmacnianie) to metoda uczenia zespołowego (ang. *ensemble learning*), która polega na sekwencyjnym budowaniu modeli predykcyjnych, najczęściej drzew decyzyjnych. Każdy kolejny model jest trenowany w taki sposób, aby korygować błędy popełnione przez poprzednie modele. W przeciwieństwie do jednoczesnego budowania wielu niezależnych modeli (jak w metodzie *bagging*), *boosting* uczy się powoli, iteracyjnie poprawiając dopasowanie do danych.

Proces ten wygląda następująco:
1.  Rozpoczyna się od dopasowania prostego modelu do danych.
2.  Następnie analizuje się błędy (rezydua) tego modelu.
3.  Kolejny model jest budowany tak, aby przewidywać te błędy (rezydua).
4.  Nowy model jest dodawany do zespołu, a prognozy są aktualizowane. Rezydua są ponownie obliczane na podstawie prognoz całego, zaktualizowanego zespołu.
5.  Kroki 3 i 4 są powtarzane wielokrotnie, co pozwala na stopniowe udoskonalanie modelu w obszarach, w których jego dotychczasowe działanie było najsłabsze.

Metoda **boosting może być stosowana zarówno do problemów regresji, jak i klasyfikacji**.

### W jaki sposób metoda *boosting* różni się od metody *bagging* pod względem sposobu wykorzystania danych treningowych?

Główna różnica między metodami *boosting* i *bagging* polega na sposobie budowania modeli i wykorzystania danych treningowych:

* **Bagging (Bootstrap Aggregating):**
    * **Niezależne i równoległe budowanie modeli:** Każde drzewo decyzyjne jest budowane niezależnie od pozostałych.
    * **Próbkowanie bootstrapowe:** Każde drzewo jest trenowane na innej, losowej próbce danych treningowych, utworzonej przez losowanie ze zwracaniem (*bootstrap*). Oznacza to, że każda próbka treningowa jest nieco inna, ale pochodzi z tej samej oryginalnej puli danych.

* **Boosting:**
    * **Sekwencyjne i zależne budowanie modeli:** Drzewa są budowane jedno po drugim, a każde nowe drzewo jest tworzone z uwzględnieniem informacji o wynikach poprzednich drzew.
    * **Brak próbkowania bootstrapowego:** *Boosting* nie polega na losowaniu próbek ze zwracaniem. Zamiast tego, każde drzewo jest trenowane na zmodyfikowanej wersji oryginalnego zbioru danych.

---

### Parametry dostrajania w metodzie *boosting*.

1.  **Liczba drzew:** Jest to całkowita liczba drzew decyzyjnych, które zostaną sekwencyjnie zbudowane i włączone do modelu. W przeciwieństwie do *baggingu* i losowych lasów, zbyt duża liczba drzew w *boostingu* może prowadzić do przeuczenia (*overfittingu*), chociaż zjawisko to postępuje zazwyczaj powoli. Optymalną liczbę drzew często wybiera się przy użyciu walidacji krzyżowej.

2.  **Współczynnik kurczenia ($\lambda$, ang. *shrinkage parameter* lub *learning rate*):** Jest to mała dodatnia liczba, która kontroluje tempo, w jakim *boosting* uczy się na błędach. Niższe wartości $\lambda$ (np. 0.01 lub 0.001) spowalniają proces uczenia, co zazwyczaj wymaga większej liczby drzew do osiągnięcia dobrych wyników.

3.  **Głębokość interakcji (d, ang. *interaction depth*):** Określa maksymalną liczbę podziałów w każdym drzewie, co kontroluje złożoność pojedynczego "słabego ucznia". Często dobrze sprawdza się wartość `d = 1`, co oznacza, że każde drzewo jest tzw. pniem decyzyjnym (ang. *stump*) z jednym podziałem.

---

## Statystyczne metody uczenia zespołowego (Ensemble Statistical Learning)

**Idea statystycznych metod uczenia zespołowego (Ensemble Statistical Learning)**

Metody uczenia zespołowego to podejścia, które **łączą wiele prostych modeli, zwanych "słabymi uczniami" (weak learners), w celu uzyskania jednego, potężnego modelu predykcyjnego**. Zamiast polegać na jednym, skomplikowanym modelu, metody te agregują predykcje z wielu prostszych modeli. Głównym celem jest **zmniejszenie wariancji** i poprawa dokładności predykcyjnej w porównaniu do pojedynczego modelu. Poprzez uśrednienie wyników z wielu modeli zbudowanych na różnych próbkach danych, ogólny wynik staje się bardziej stabilny i mniej podatny na specyfikę pojedynczego zbioru treningowego.

**Metody zespołowe wykorzystujące drzewa (Tree Ensemble Methods)**

* **Bagging** (agregacja bootstrapowa).
* **Lasy losowe** (Random Forests).
* **Boosting**.
* **Bayesowskie addytywne drzewa regresyjne** (Bayesian Additive Regression Trees, BART).

**Opis Bagging**

**Bagging**, czyli agregacja bootstrapowa (ang. *bootstrap aggregation*), to ogólna procedura mająca na celu zmniejszenie wariancji w metodach uczenia statystycznego, szczególnie skuteczna w przypadku drzew decyzyjnych, które charakteryzują się wysoką wariancją.

Mechanizm działania opiera się na idei, że uśrednianie zbioru obserwacji redukuje wariancję. Ponieważ zazwyczaj nie mamy dostępu do wielu niezależnych zbiorów treningowych, Bagging tworzy je sztucznie za pomocą techniki **bootstrapu**, czyli losowania ze zwracaniem z oryginalnego zbioru danych.

**Proces składa się z następujących kroków:**
1.  **Tworzenie zbiorów bootstrapowych:** Z oryginalnego zbioru treningowego o `n` obserwacjach tworzy się `B` nowych zbiorów treningowych, każdy o rozmiarze `n`, poprzez losowanie ze zwracaniem. Każdy z tych zbiorów jest nieco inny.
2.  **Budowanie modeli:** Na każdym z `B` "bootstrapowych" zbiorów danych budowane jest osobne, **głębokie i nieprzycinane drzewo decyzyjne**. Każde z tych drzew ma niską obciążalność (bias), ale wysoką wariancję.
3.  **Agregacja predykcji:** Aby uzyskać ostateczną predykcję dla nowej obserwacji, wyniki z `B` drzew są łączone:
    * W przypadku **regresji** (odpowiedź ilościowa), predykcje są uśredniane.
    * W przypadku **klasyfikacji** (odpowiedź jakościowa), ostateczna predykcja jest wynikiem **głosowania większościowego** – wybierana jest klasa najczęściej wskazywana przez poszczególne drzewa.

**Zalety i wady**

Główną zaletą metody Bagging jest **znacząca poprawa dokładności predykcyjnej** w porównaniu do pojedynczego drzewa, dzięki redukcji wariancji. Użycie dużej liczby drzew `B` nie prowadzi do przeuczenia (overfittingu).

Podstawową wadą jest **utrata interpretoalności**. Zamiast jednego, łatwego do zwizualizowania drzewa, otrzymujemy setki lub tysiące drzew, których nie da się przedstawić w prostej, graficznej formie.

**Estymacja błędu Out-of-Bag (OOB)**

Bagging oferuje efektywny sposób estymacji błędu testowego bez konieczności stosowania walidacji krzyżowej. Każde drzewo jest budowane na około 2/3 unikalnych obserwacji z oryginalnego zbioru. Pozostała 1/3 obserwacji, niewykorzystana do budowy danego drzewa, to tzw. obserwacje **Out-of-Bag (OOB)**. Dla każdej obserwacji w zbiorze treningowym można uzyskać predykcję OOB, uśredniając wyniki tylko z tych drzew, dla których była ona obserwacją OOB. Błąd OOB, obliczony na podstawie tych predykcji, jest wiarygodnym estymatorem błędu testowego.

---

## Drzewa regresyjne

Jedną z reguł stosowanych do określenia, kiedy węzeł w drzewie regresyjnym staje się węzłem końcowym (liściem), jest **osiągnięcie przez niego z góry ustalonej, maksymalnej głębokości**.

Głębokość węzła jest definiowana na podstawie jego "generacji" w strukturze drzewa. Węzeł główny (tzw. korzeń), od którego zaczyna się całe drzewo, ma głębokość zero. Jego bezpośredni potomkowie (węzły-dzieci) mają głębokość jeden, ich potomkowie — głębokość dwa, i tak dalej.

Zastosowanie tej reguły polega na ustaleniu limitu, jak "głęboko" drzewo może się rozrastać. Kiedy dany węzeł osiągnie tę maksymalną, zdefiniowaną wcześniej głębokość, jest automatycznie uznawany za węzeł końcowy i nie podlega dalszym podziałom, nawet jeśli podział mógłby poprawić model. Na przykład, jeśli maksymalna głębokość zostanie ustalona na dwa, wszystkie węzły na tym poziomie (czyli w trzeciej "generacji") staną się liśćmi drzewa.

---

## Szeregi czasowe

**Wybrane właściwości finansowych szeregów czasowych (stylizowane fakty)**

1. **Grube ogony**: Rozkład stóp zwrotu nie jest rozkładem normalnym. Charakteryzuje się tzw. "grubymi ogonami", co oznacza, że skrajne, bardzo wysokie lub bardzo niskie stopy zwrotu (gwałtowne wzrosty i spadki) występują znacznie częściej, niż przewidywałby to model oparty na rozkładzie normalnym. Jednocześnie obserwuje się wyższą koncentrację wyników wokół wartości średniej.

2. **Grupowanie się zmienności**: Zmienność stóp zwrotu nie jest stała w czasie. Obserwuje się okresy, w których wahania cen są niewielkie (niska zmienność), po których następują okresy o dużej amplitudzie wahań (wysoka zmienność). Innymi słowy, "dużym zmianom towarzyszą kolejne duże zmiany, a małym – małe".

3. **Brak autokorelacji stóp zwrotu, ale występowanie autokorelacji w wartościach bezwzględnych lub kwadratach stóp zwrotu**: Same stopy zwrotu są zazwyczaj nieskorelowane w czasie, co oznacza, że na podstawie przeszłych stóp zwrotu nie da się przewidzieć przyszłych. Jednak ich wartości bezwzględne (lub kwadraty), które są miarą zmienności, wykazują istotną, dodatnią i wolno wygasającą autokorelację. Jest to matematyczne potwierdzenie zjawiska grupowania się zmienności.

---

## Współczynnik V Cramera

Współczynnik V Cramera jest miarą siły związku (asocjacji) między dwiema zmiennymi, opartą na statystyce chi-kwadrat Pearsona z tablicy kontyngencji.

**Wartości i interpretacja**

Współczynnik V Cramera przyjmuje wartości w przedziale od 0 do 1. Interpretacja jego wartości jest następująca:
* **V = 0** oznacza całkowity brak zależności statystycznej (niezależność) między analizowanymi zmiennymi.
* **V = 1** oznacza doskonałą zależność, gdzie znajomość wartości jednej zmiennej pozwala w pełni przewidzieć wartość drugiej.
* **Wartości pośrednie** wskazują na siłę związku – im wyższa wartość, tym silniejsza zależność.

Współczynnik ten jest tak znormalizowany, aby jego wartość była niezależna od liczby obserwacji oraz wymiarów tablicy kontyngencji. Oblicza się go za pomocą wzoru:
$$V = \sqrt{\frac{\chi^2 / n}{\min(k_1 - 1, k_2 - 1)}}$$
gdzie:
* $\chi^2$ to statystyka chi-kwadrat Pearsona.
* $n$ to całkowita liczba obserwacji.
* $k_1$ i $k_2$ to odpowiednio liczba kategorii (poziomów) dla pierwszej i drugiej zmiennej.

**Zastosowanie i rodzaje zmiennych**

Współczynnik V Cramera jest szeroko stosowany do oceny korelacji między cechami, zwłaszcza gdy klasyczne miary, takie jak współczynnik korelacji Pearsona, nie są odpowiednie dla danych nieciągłych.

Nie jest on ograniczony wyłącznie do zmiennych jakościowych (kategorycznych). Może być również stosowany do zmiennych ilościowych (ciągłych), jednak wymaga to ich uprzedniej **dyskretyzacji** (nazywanej również grupowaniem lub "bandingiem"). Proces ten polega na podzieleniu dziedziny zmiennej ciągłej na rozłączne przedziały, co w efekcie przekształca ją w zmienną kategoryczną. Po takiej transformacji współczynnik V Cramera oblicza się w standardowy sposób, jak dla zmiennych, które pierwotnie były jakościowe.

---

## Gini indeks

Indeks Giniego jest miarą **zanieczyszczenia** (ang. *impurity*) lub niejednorodności w zbiorze danych. W kontekście drzew decyzyjnych służy jako kryterium do oceny, jak "dobry" jest potencjalny podział węzła na węzły potomne.

Główna zasada jest prosta: **dążymy do tworzenia podziałów, które skutkują jak najczystszymi węzłami potomnymi**. "Czysty" węzeł to taki, w którym większość (lub wszystkie) obserwacje należą do tej samej klasy.

1.  **Wartość indeksu:** Indeks Giniego przyjmuje wartości od 0 do 0.5 (dla problemu klasyfikacji binarnej).
    * $G = 0$ oznacza **idealną czystość** – wszystkie obserwacje w węźle należą do jednej klasy.
    * $G = 0.5$ oznacza **maksymalne zanieczyszczenie** – obserwacje rozkładają się po równo między dwie klasy (np. 50% "Tak", 50% "Nie").
2.  **Ocena podziału:** Dla każdej potencjalnej zmiennej, według której można dokonać podziału, algorytm oblicza średni ważony indeks Giniego dla węzłów potomnych, które by w wyniku tego podziału powstały.
3.  **Wybór najlepszego podziału:** Wybierany jest taki podział (czyli taka zmienna), który prowadzi do **najniższej wartości średniego ważonego indeksu Giniego**. Oznacza to, że ten podział najlepiej separuje klasy i tworzy najczystsze możliwe podgrupy.

---

## Estymacja jądrowa

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

---

## GARCH

**Definicja procesu GARCH(p, q)**

Niech $(Z_t)_{t \in \mathbb{Z}}$ będzie procesem typu **ścisły biały szum SWN(0, 1)**. Proces $(X_t)_{t \in \mathbb{Z}}$ jest procesem GARCH(p, q), jeśli jest ściśle stacjonarny i dla każdego $t \in \mathbb{Z}$ oraz dla pewnego procesu $(\sigma_t)_{t \in \mathbb{Z}}$ o wartościach dodatnich spełnia równania:

$X_t = \sigma_t Z_t$

$\sigma_t^2 = \alpha_0 + \sum_{i=1}^{p} \alpha_i X_{t-i}^2 + \sum_{j=1}^{q} \beta_j \sigma_{t-j}^2$

gdzie parametry spełniają warunki: $\alpha_0 > 0$, $\alpha_i \ge 0$ dla $i=1,...,p$ oraz $\beta_j \ge 0$ dla $j=1,...,q$. W tym modelu $\sigma_t^2$ jest warunkową wariancją procesu $X_t$.

**Zastosowanie modeli GARCH**

Modele klasy GARCH służą przede wszystkim do **modelowania i prognozowania zmienności** (ang. *volatility*) finansowych szeregów czasowych. Ich głównym celem jest uchwycenie kluczowych empirycznych właściwości danych finansowych, zwanych stylizowanymi faktami, których nie uwzględniają prostsze modele.

* **Modelowanie klasteryzacji zmienności**: Jest to tendencja obserwowana w danych finansowych, gdzie okresy dużych wahań cen następują po sobie, a okresy spokoju również występują w seriach. Modele GARCH odwzorowują to zjawisko, pozwalając, aby dzisiejsza wariancja warunkowa ($\sigma_t^2$) zależała od wczorajszych kwadratów obserwacji ($X_{t-1}^2$) oraz od wczorajszej wariancji warunkowej ($\sigma_{t-1}^2$).
* **Uchwycenie grubych ogonów (leptokurtozy)**: Nawet jeśli innowacje $(Z_t)$ w procesie GARCH pochodzą z rozkładu normalnego, stacjonarny rozkład samego procesu $(X_t)$ jest leptokurtyczny (ma "grubsze ogony" niż rozkład normalny), co jest zgodne z empirycznymi właściwościami stóp zwrotu z aktywów finansowych.
* **Prognozowanie zmienności i szacowanie miar ryzyka**: Dopasowane modele GARCH pozwalają na prognozowanie przyszłej zmienności warunkowej. Prognozy te są kluczowym elementem w szacowaniu miar ryzyka, takich jak **Value-at-Risk (VaR)** i **Expected Shortfall (ES)**, w ujęciu warunkowym, czyli uwzględniającym najnowsze informacje rynkowe.

## Reszty dwiancyjne 

Reszty dewiancyjne są często preferowaną formą w Uogólnionych Modelach Liniowych (GLM), ponieważ w przeciwieństwie do innych typów reszt, **uwzględniają one kształt rozkładu zmiennej odpowiedzi, w tym jego skośność**. Jest to kluczowe w zastosowaniach aktuarialnych, gdzie rozkłady rzadko są symetryczne.

Główne zalety ich wykorzystania w porównaniu z innymi rodzajami reszt to:

* **Lepsze dopasowanie do założeń GLM:** W przeciwieństwie do reszt Pearsona, które wywodzą się z modeli liniowych, reszty dewiancyjne są bezpośrednio powiązane z funkcją wiarygodności przyjętego rozkładu z rodziny wykładniczej, co czyni je bardziej odpowiednimi dla struktury GLM.
* **Wykrywanie obserwacji słabo dopasowanych:** Pozwalają zidentyfikować te obserwacje, które w największym stopniu przyczyniają się do wzrostu dewiancji, a więc wskazują na miejsca, w których model niedostatecznie dobrze dopasowuje się do danych.
* **Korekta na heteroskedastyczność:** Podobnie jak reszty Pearsona, ale w przeciwieństwie do reszt prostych (surowych), korygują one fakt, że wariancja w modelach GLM często zależy od wartości średniej. Reszty proste mogą być przez to mniej informatywne.
* **Lepsza interpretacja dla danych dyskretnych:** Chociaż indywidualne reszty dla danych dyskretnych (np. liczby szkód) mogą być trudne do interpretacji, reszty dewiancyjne obliczone dla zagregowanych grup ryzyka dają znacznie lepsze wskazówki co do poprawności dopasowania modelu.
