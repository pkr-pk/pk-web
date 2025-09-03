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

## Dane ucięte

1. **Okrojenie z lewej strony** (ang. *left truncated*) występuje, gdy obserwacje poniżej pewnego progu `d` w ogóle nie są rejestrowane. W przypadku okrojenia nie wiedzielibyśmy nawet o istnieniu szkód, których wartość nie przekroczyła jakiegoś progu.

2. **Przykład dla danych uciętych** W przypadku polis sprzedanych przed rozpoczęciem okresu obserwacji, część ubezpieczonych umrze, podczas gdy inni dożyją, by rozpocząć obserwację. Nie tylko czasy ich zgonów nie zostaną zarejestrowane, ale nawet nie będziemy wiedzieć, ile ich było. Inną częstą sytuacją jest franszyza redukcyjna. Szkody poniżej franszyzy nie są rejestrowane i nie ma danych o tym, ile szkód było poniżej jej wartości.

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

* **Uzgodnienie z dokumentami finansowymi**: Porównanie danych z audytowymi sprawozdaniami finansowymi, zestawieniami obrotów i sald lub innymi odpowiednimi dokumentami, jeśli są dostępne.
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

## Redukcja wariancji w metodzie Monte Carlo

**Próbkowanie ważone (Importance Sampling - IS)** to technika redukcji wariancji w metodzie Monte Carlo, która polega na zastąpieniu oryginalnego rozkładu prawdopodobieństwa innym, który koncentruje większe prawdopodobieństwo w regionach o największym znaczeniu dla estymowanej wartości. Celem jest zwiększenie wydajności symulacji, zwłaszcza przy szacowaniu prawdopodobieństw zdarzeń rzadkich lub wartości w ogonach rozkładu.

---
**Kluczowe założenia**

Podstawowym problemem w prostej metodzie Monte Carlo jest jej niska wydajność, gdy wiele generowanych prób losowych nie trafia w interesujący nas obszar. Próbkowanie ważone rozwiązuje ten problem poprzez zmianę gęstości prawdopodobieństwa, z której losowane są próby, z oryginalnej $f_X(x)$ na nową gęstość $f̃_X(x)$.

Aby wynik pozostał nieobciążony, każda wylosowana próba musi zostać skorygowana przez pomnożenie jej przez **iloraz wiarygodności (likelihood ratio)**, dany wzorem $f_X(x) / f̃_X(x)$.

---
**Estymator i redukcja wariancji**

Wartość oczekiwaną $E(X)$ można przedstawić jako:
$$E(X) = \int x f_X(x)dx = \int \left(x \frac{f_X(x)}{f̃_X(x)}\right) f̃_X(x)dx = E\left(\tilde{X} \frac{f_X(\tilde{X})}{f̃_X(\tilde{X})}\right)$$
gdzie $\tilde{X}$ jest zmienną losową o gęstości $f̃_X(x)$.

**Estymator próbkowania ważonego** dla $n$ symulacji ma postać:
$$\hat{\mu}_{In} = \frac{1}{n} \sum_{i=1}^{n} \tilde{X}_i \frac{f_X(\tilde{X}_i)}{f̃_X(\tilde{X}_i)}$$
Estymator ten jest nieobciążony, a jego wariancja jest mniejsza niż wariancja standardowego estymatora Monte Carlo, jeśli nowa gęstość $f̃_X(x)$ jest dobrana tak, aby iloraz wiarygodności był mały tam, gdzie wartość $x^2 f_X(x)$ jest duża.

---
**Przykład zastosowania: Przechylanie wykładnicze**

Popularną techniką wyboru nowej gęstości dla rozkładów o lekkich ogonach jest **przechylanie wykładnicze (exponential twisting)**, które jest zastosowaniem transformaty Esschera. Nowa gęstość jest definiowana jako:
$$f̃_X(x) = \frac{e^{\theta x} f_X(x)}{E(e^{\theta X})}$$
Parametr $\theta$ dobiera się tak, aby przesunąć wartość oczekiwaną nowego rozkładu w kierunku interesującego nas obszaru (np. estymowanego kwantyla).

W dokumencie zilustrowano to na przykładzie szacowania kwantyla VaR dla zmiennej o rozkładzie gamma. Mimo że wstępne założenie co do wartości VaR było niedokładne, zastosowanie próbkowania ważonego z przechylaniem wykładniczym znacząco zwiększyło szybkość zbieżności i dokładność estymacji w porównaniu do prostej metody Monte Carlo (Rysunek 9.2 w dokumencie).

**Ograniczenia**
Technika przechylania wykładniczego nie ma zastosowania dla rozkładów o ciężkich ogonach (np. Pareto), ponieważ ich funkcja generująca momenty nie istnieje dla dodatnich argumentów. W takich przypadkach stosuje się inne metody, np. przechylanie funkcji hazardu.

## Algorytm aglomeracyjny

Grupowanie hierarchiczne to metoda analizy skupień, która buduje hierarchię klastrów. Podejście aglomeracyjne, zwane również podejściem "oddolnym" (bottom-up), jest najpowszechniejszą metodą grupowania hierarchicznego.

Proces ten tworzy wizualną reprezentację danych w postaci drzewa zwaną **dendrogramem**, który ilustruje, jak obserwacje są kolejno łączone w klastry.

---
**Algorytm grupowania aglomeracyjnego**

Algorytm przebiega iteracyjnie, łącząc obserwacje i klastry krok po kroku, od pojedynczych punktów aż do jednego, dużego klastra obejmującego cały zbiór danych.

**Krok 1: Inicjalizacja**

Proces rozpoczyna się od zdefiniowania miary odmienności (najczęściej odległości euklidesowej) między każdą parą obserwacji w zbiorze danych. Na tym etapie każda z `n` obserwacji jest traktowana jako osobny, jednoelementowy klaster.

---
**Krok 2: Iteracyjne łączenie klastrów**

Algorytm wykonuje `n-1` kroków, aby połączyć wszystkie obserwacje w jeden klaster. W każdej iteracji:
1.  **Identyfikacja najbliższych klastrów**: Algorytm identyfikuje dwa klastry, które są do siebie najbardziej podobne (najmniej odmienne).
2.  **Fuzja (łączenie) klastrów**: Te dwa najbliższe klastry są łączone w jeden nowy klaster.
3.  **Aktualizacja miar odmienności**: Obliczane są nowe miary odmienności między nowo powstałym klastrem a wszystkimi pozostałymi.

Proces ten jest kontynuowany, aż wszystkie obserwacje zostaną połączone w jeden klaster.

---
**Kluczowe pojęcia w algorytmie**

Aby algorytm mógł działać, należy zdefiniować dwie kluczowe miary:

**1. Miara odmienności (Dissimilarity Measure)**
Określa, jak "daleko" od siebie znajdują się dwie pojedyncze obserwacje. Najczęściej stosowaną miarą jest **odległość euklidesowa**, ale w zależności od zastosowania można użyć innych miar, takich jak **odległość oparta na korelacji**, która ocenia podobieństwo kształtów profili obserwacji, a nie ich wartości bezwzględnych.

**2. Metoda łączenia (Linkage)**
Ponieważ algorytm musi mierzyć odległość nie tylko między punktami, ale także między klastrami (które mogą zawierać wiele obserwacji), konieczne jest zdefiniowanie, w jaki sposób obliczana jest odmienność międzygrupowa. Służy do tego **metoda łączenia** (linkage). Główne typy to:

* **Łączenie pełne (Complete Linkage)**: Odmienność między dwoma klastrami to odmienność między *najdalszymi* od siebie obserwacjami z tych klastrów.
* **Łączenie pojedyncze (Single Linkage)**: Odmienność to odmienność między *najbliższymi* od siebie obserwacjami z tych klastrów.
* **Łączenie średnie (Average Linkage)**: Odmienność to średnia wszystkich odmienności między parami obserwacji pochodzących z różnych klastrów.
* **Łączenie oparte na centroidach (Centroid Linkage)**: Odmienność jest mierzona jako odległość między centroidami (średnimi wektorami) obu klastrów.

Wybór metody łączenia ma znaczący wpływ na ostateczny kształt dendrogramu. Łączenie pełne i średnie zazwyczaj prowadzą do bardziej zrównoważonych klastrów.

---
**Wynik: Dendrogram**

Wynikiem działania algorytmu jest **dendrogram** – struktura przypominająca drzewo, która wizualizuje proces łączenia.

* **Liście** na dole dendrogramu reprezentują poszczególne obserwacje.
* **Wysokość**, na której dwa klastry są łączone, reprezentuje stopień ich odmienności. Im niżej następuje połączenie, tym bardziej podobne są obserwacje.
* Aby uzyskać określoną liczbę klastrów, można "przeciąć" dendrogram na odpowiedniej wysokości. Liczba linii dendrogramu przeciętych przez tę poziomą linię cięcia odpowiada liczbie uzyskanych klastrów.











## Walidacja krzyżowa

**Wyjaśnij w jaki sposób przeprowadza się k-krotną walidację krzyżową.**

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
**Podaj na czym polega walidacja za pomocą metody LOOCV (Leave-one-out cross-validation).**

Walidacja krzyżowa z pominięciem jednej obserwacji (Leave-one-out cross-validation, LOOCV) to intensywna obliczeniowo, ale czasami użyteczna metoda szacowania błędu testowego modelu statystycznego. Jest to szczególny przypadek k-krotnej walidacji krzyżowej, w którym liczba podzbiorów $(k)$ jest równa liczbie obserwacji $(n)$ w zbiorze danych.

Proces polega na wielokrotnym dopasowywaniu modelu, gdzie za każdym razem jedna obserwacja jest wykluczana ze zbioru uczącego i używana do walidacji.

---
**Jakie są zalety i wady k-krotnej walidacji krzyżowej w porównaniu z:**
* **i. podejściem wykorzystującym jedynie jeden zbiór walidacyjny,**
* **ii. metodą LOOCV.**

**W odpowiedzi uwzględnij problem kompromisu między obciążeniem a wariancją modelu.**

Wybór $k$ w walidacji krzyżowej to kompromis między obciążeniem a wariancją.
* LOOCV $(k=n)$ ma niskie obciążenie, ale wysoką wariancję.
* Podejście z jednym zbiorem walidacyjnym (odpowiednik $k=2$) ma wysokie obciążenie, ale niską wariancję.

K-krotna walidacja krzyżowa z wartościami $k=5$ lub $k=10$ jest w praktyce złotym środkiem. Empirycznie wykazano, że takie wartości prowadzą do estymacji błędu testowego, które nie cechują się ani nadmiernie wysokim obciążeniem, ani bardzo wysoką wariancją.

## Uogólnione modele addytywne (GAMs)

**Krótko przedstaw ideę uogólnionych modeli addytywnych (Generalized Additive Models – GAM). Wskaż dlaczego weszły do zestawu narzędzi aktuariusza.**

Uogólnione modele addytywne (GAM) to rozszerzenie uogólnionych modeli liniowych (GLM), które pozwala na modelowanie nieliniowych zależności między predyktorami a zmienną odpowiedzi, zachowując przy tym addytywną strukturę. Zamiast zakładać, że każdy predyktor ma liniowy wpływ na odpowiedź (np. $\beta_1 x_1$), GAM dopasowuje gładką, nieliniową funkcję dla każdego predyktora (np. $f_1(x_1)$). Model końcowy jest sumą tych indywidualnych funkcji: $Y = \beta_0 + f_1(X_1) + f_2(X_2) + \dots + f_p(X_p) + \epsilon$. Taka budowa pozwala na dużą elastyczność w modelowaniu złożonych wzorców, jednocześnie zachowując możliwość interpretacji wpływu każdego predyktora z osobna.

Dzięki GAM aktuariusze mogą:
* Precyzyjnie modelować nieliniowe zależności i interakcje między zmiennymi, takimi jak wiek i płeć kierowcy czy dane geograficzne.
* Analizować indywidualne dane dotyczące śmiertelności przy użyciu regresji Poissona bez konieczności wstępnego, subiektywnego grupowania danych.

---
**Podaj definicję funkcji sklejanej stopnia 3 (splajnu kubicznego).**

Splajn sześcienny z $K$ węzłami można zamodelować jako:

$$y_i = \beta_0 + \beta_1 b_1(x_i) + \beta_2 b_2(x_i) + \dots + \beta_{K+3} b_{K+3}(x_i) + \epsilon_i,$$

dla odpowiedniego wyboru funkcji bazowych $b_1, b_2,...,b_{K+3}$. Najbardziej bezpośrednim sposobem reprezentacji splajnu sześciennego przy użyciu powyższej jest rozpoczęcie od bazy dla wielomianu sześciennego – mianowicie, $b_1(x_i) = x_i$, $b_2(x_i) = x_i^2$, i $b_3(x_i) = x_i^3$ a następnie dodanie jednej potęgowej funkcji bazowej na każdy węzeł. Potęgowa funkcja bazowa jest zdefiniowana jako:

$$h(x_i, \xi_i) = (x_i - \xi_i)^3_+ = \begin{cases} (x_i - \xi_i)^3 & \text{jeśli } x_i > \xi_i \\ 0 & \text{w przeciwnym razie}, \end{cases}$$

gdzie $\xi_i$ jest $i$-tym węzłem. Przykład:

$$y = \beta_0 + \beta_1 x + \beta_2 x^2 + \beta_3 x^3 + \beta_4 (x - \xi)^3_+$$

## Teoria wartości ekstremalnych

**Krótko opisz podejście Hilla do modelowania ogonów rozkładów (m in. podaj założenia odnośnie rozkładów i przedstaw odpowiedni estymator).**

Metoda Hilla jest podejściem stosowanym do modelowania i estymacji ogonów rozkładów prawdopodobieństwa, zwłaszcza tych o grubych ogonach (heavy-tailed). Służy do oszacowania parametru kształtu ogona, znanego jako indeks ogona.

Podstawowym założeniem metody Hilla jest to, że funkcja przeżycia (ogon) badanego rozkładu dla dużych wartości $x$ zachowuje się jak funkcja potęgowa:

$$\bar{F}(x) = x^{-\alpha}L(x)$$

gdzie:
* $\alpha > 0$ to indeks ogona, który opisuje "ciężkość" ogona (im mniejsze $\alpha$, tym grubszy ogon).
* $L(x)$ jest funkcją wolno zmienną, co oznacza, że zmienia się wolniej niż jakakolwiek funkcja potęgowa.

Estymator Hilla:

$$\hat{\alpha}^{(H)}_{k,n} = \left( \frac{1}{k} \sum_{j=1}^{k} \ln X_{j,n} - \ln X_{k,n} \right)^{-1}$$

gdzie:
* $k$ to liczba największych obserwacji użytych do estymacji ($2 \le k \le n$).
* $X_{j,n}$ to $j$-ta największa obserwacja w próbie.

---
**Przedstaw konstrukcję wykresu Hilla (Hill plot) i wskaż w jakim celu jest wykorzystywany.**

Aby wybrać optymalną wartość $k$, tworzy się tzw. wykres Hilla, który przedstawia wartości estymatora $\hat{\alpha}^{(H)}_{k,n}$ w funkcji $k$. Następnie poszukuje się na wykresie stabilnego regionu, w którym estymaty są względnie stałe, i na tej podstawie wybiera się ostateczne oszacowanie indeksu ogona $\alpha$.

Aby $k$-ty moment statystyczny (jak średnia czy wariancja) był skończony, wartość indeksu $\alpha$ musi być od tego $k$ większa. Np. wariancja (związana z 2 momentem, $k = 2$) jest skończona, jeśli $\alpha > 2$.

## Podstawy analizy szeregów czasowych

**Wymień etapy statystycznej analizy szeregów czasowych danych $y_1, y_2,..., y_t$. Krótko opisz jeden z nich.**

Etapy statystycznej analizy szeregów czasowych:
* Analiza wstępna
* Analiza w dziedzinie czasu
* Dopasowanie modelu
* Analiza reszt i porównanie modeli 

Analiza wstępna:

Jest to pierwszy etap, w którym dane są wizualizowane na wykresie w celu oceny, czy zastosowanie pojedynczego modelu stacjonarnego jest zasadne. Analiza wstępna obejmuje również rozważenie, czy konieczna jest wstępna obróbka danych, na przykład w celu usunięcia trendów lub sezonowości. Istotnym elementem tego etapu jest wybór odpowiedniej długości okna czasowego dla danych, co wiąże się z kompromisem między potrzebą korzystania z najbardziej aktualnych informacji a koniecznością posiadania wystarczająco dużej próbki do precyzyjnej estymacji statystycznej.

---
**Przedstaw sposób prognozowania szeregów czasowych za pomocą modeli ARMA. Podaj ogólne założenia i wskaż ideę.**

Podstawowym założeniem jest to, że dane pochodzą z odwracalnego modelu ARMA, a innowacje (błędy) procesu mają własność różnicy martyngałowej. Oznacza to, że oczekiwana wartość przyszłej innowacji, biorąc pod uwagę historię procesu, jest równa zero.

Główną ideą jest wykorzystanie warunkowej wartości oczekiwanej $E(X_{t+h} \mid \mathcal{F}_t)$ jako predyktora, gdzie $\mathcal{F}_t$ reprezentuje historię procesu do czasu $t$. Ten predyktor minimalizuje średniokwadratowy błąd prognozy. Prognozy oblicza się rekurencyjnie. Wartości losowe do czasu $t$ są traktowane jako "znane", a oczekiwane wartości przyszłych innowacji (dla $h \ge 1$) wynoszą zero. W praktyce, ponieważ pełna historia procesu nie jest znana, do obliczeń wykorzystuje się reszty z dopasowanego modelu. W miarę wydłużania horyzontu prognozy, przewidywana wartość zbiega do bezwarunkowej średniej procesu.

## Modele GARCH

**Podaj definicję procesu GARCH(p, q).**

Niech $(Z_t)_{t \in \mathbb{Z}}$ będzie procesem typu ścisły biały szum SWN(0, 1). Proces $(X_t)_{t \in \mathbb{Z}}$ jest procesem GARCH(p, q), jeśli jest ściśle stacjonarny i dla każdego $t \in \mathbb{Z}$ oraz dla pewnego procesu $(\sigma_t)_{t \in \mathbb{Z}}$ o wartościach dodatnich spełnia równania:

$X_t = \sigma_t Z_t$

$\sigma_t^2 = \alpha_0 + \sum_{i=1}^{p} \alpha_i X_{t-i}^2 + \sum_{j=1}^{q} \beta_j \sigma_{t-j}^2$

gdzie: $\alpha_0 > 0$, $\alpha_i \ge 0$ dla $i=1,...,p$ oraz $\beta_j \ge 0$ dla $j=1,...,q$.

---
**Do jakich celów służą modele klasy GARCH?**

Modele klasy GARCH służą przede wszystkim do modelowania i prognozowania zmienności szeregów czasowych, zwłaszcza w kontekście finansowym. Ich głównym celem jest uchwycenie kluczowych empirycznych właściwości finansowych szeregów czasowych, których nie potrafią opisać prostsze modele.

* Modelowanie zmienności warunkowej.
* Uchwycenie grupowania zmienności: jest to kluczowe zjawisko na rynkach finansowych, gdzie okresy dużej zmienności (dużych wahań cen) przeplatają się z okresami względnego spokoju.
* Prognozowanie przyszłej zmienności.
* Obliczanie miar ryzyka finansowego: prognozy zmienności uzyskane z modeli GARCH są kluczowym wkładem do estymacji miar ryzyka, takich jak Value-at-Risk (VaR) i Expected Shortfall (ES). Umożliwiają one tworzenie warunkowych miar ryzyka, które dostosowują się do aktualnej sytuacji na rynku.
* Opisywanie dynamiki szeregów czasowych zwrotów z aktywów.

## Estymacja empiryczna danych cenzurowanych prawostronnie

**Podaj definicję danych prawostronnie cenzurowanych (right censoring). Wskaż i omów co najmniej dwie sytuacje, w których aktuariusz analizuje tego typu dane.**

Obserwacja cenzurowana prawostronnie w punkcie $u$, jeśli gdy jest równa lub większa od $u$, jest zapisywana jako równa 
$u$, ale gdy jest poniżej $u$, jest zapisywana z jej obserwowaną wartością.

W danych dotyczących roszczeń ubezpieczeniowych, obecność limitu polisy może prowadzić do prawostronnie cenzurowanych obserwacji. Gdy kwota szkody jest równa lub przekracza limit 
$u$, świadczenia powyżej tej wartości nie są wypłacane, więc dokładna wartość zazwyczaj nie jest rejestrowana. Wiadomo jednak, że wystąpiła szkoda o wartości co najmniej $u$.

Podczas przeprowadzania badania śmiertelności ludzi, jeśli osoba żyje w momencie zakończenia badania, nastąpiło cenzurowanie prawostronne. Wiek osoby w chwili śmierci nie jest znany, ale wiadomo, że jest on co najmniej tak duży jak wiek w momencie zakończenia badania.

## Krajowy standard aktuarialny - praktyka aktuarialna

**Przedstaw wytyczne Krajowego Standardu Aktuarialnego w zakresie stosowania modeli (tj. wyboru, tworzenia, modyfikowania i przeliczania modeli) dotyczące:**
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

## PDP Partial Dependence Plot

**Przedstaw ideę i sposób konstrukcji wykresów PDP (Partial Dependence Plot).**

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

## Testowanie hipotez

**Przedstaw ideę i konstrukcję testu ilorazu wiarygodności. Zapisz hipotezę zerową i alternatywną i wskaż czy różnią się one od hipotez (zerowej i alternatywnej) stawianych w testach zgodności (np. chi-kwadrat, Kołmogorowa-Smirnowa). Podaj postać statystyki testowej i jej rozkład.**

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

## Drzewa regresyjne

**Wskaż co najmniej cztery reguły określające, kiedy węzeł w drzewie regresyjnym jest przyjmowany za końcowy (jest uznawany za liść).**

Węzeł jest uznawany za końcowy:
* jeśli zawiera mniej niż z góry określoną liczbę obserwacji.
* gdy jego głębokość (czyli odległość od korzenia drzewa) osiągnie ustalony limit.
* jeśli w wyniku tego podziału co najmniej jeden z nowo powstałych węzłów potomnych (liści) zawierałby mniej niż z góry określoną liczbę obserwacji.
* jeśli najlepszy możliwy podział tego węzła nie przynosi spadku dewiancji (miary błędu) o wartość większą niż ustalony próg.

---
**Na czym polega i w jakim celu stosuje się przycinanie drzewa regresyjnego?**

Przycinanie polega budowaniu maksymalnie rozbudowanego drzewa, pozwalając mu rosnąć aż do momentu, gdy dalsze podziały nie są możliwe (np. w liściach zostaje zbyt mało obserwacji lub wszystkie mają tę samą wartość). Takie drzewo jest bardzo złożone i idealnie dopasowane do danych treningowych. Następnie, w sposób systematyczny, usuwa się (przycina) całe gałęzie drzewa, czyli węzły wraz z ich potomkami. Celem jest znalezienie optymalnego poddrzewa, które stanowi najlepszy kompromis między prostotą a dokładnością predykcji.

## Bagging, Random Forests, Boosting, and Bayesian Additive Regression Trees (BART)

**Krótko przedstaw ideę statystycznych metod uczenia zespołowego (Ensemble Statistical Learning).**

Metody uczenia zespołowego to podejścia, które łączą wiele prostych modeli w celu uzyskania jednego, lepszego modelu predykcyjnego. Głównym celem jest zmniejszenie wariancji i poprawa dokładności predykcyjnej w porównaniu do pojedynczego modelu poprzez uśrednienie wyników z wielu modeli zbudowanych na różnych próbkach danych. Ogólny wynik staje się bardziej stabilny i mniej podatny na specyfikę pojedynczego zbioru treningowego.

---
**Wymień co najmniej trzy takie metody wykorzystujące drzewa (Tree Ensemble Methods)**

* Bagging (agregacja bootstrapowa).
* Lasy losowe (Random Forests).
* Boosting.
* Bayesowskie addytywne drzewa regresyjne (Bayesian Additive Regression Trees, BART).

---
**Opisz jedną metodę spośród Tree Ensemble Methods**

Bagging

Mechanizm działania opiera się na idei, że uśrednianie zbioru obserwacji redukuje wariancję. Ponieważ zazwyczaj nie mamy dostępu do wielu niezależnych zbiorów treningowych, Bagging tworzy je sztucznie za pomocą techniki bootstrapu, czyli losowania ze zwracaniem z oryginalnego zbioru danych.

Proces składa się z następujących kroków:
1.  Tworzenie zbiorów bootstrapowych: z oryginalnego zbioru treningowego o $n$ obserwacjach tworzy się $B$ nowych zbiorów treningowych, każdy o rozmiarze $n$, poprzez losowanie ze zwracaniem. Każdy z tych zbiorów jest nieco inny.
2.  Budowanie modeli: na każdym z $B$ "bootstrapowych" zbiorów danych budowane jest osobne, głębokie i nieprzycinane drzewo decyzyjne. Każde z tych drzew ma niskie obciążenie (bias), ale wysoką wariancję.
3.  Agregacja predykcji: aby uzyskać ostateczną predykcję dla nowej obserwacji, wyniki z $B$ drzew są łączone:
    * W przypadku regresji (odpowiedź ilościowa), predykcje są uśredniane.
    * W przypadku klasyfikacji (odpowiedź jakościowa), ostateczna predykcja jest wynikiem głosowania większościowego – wybierana jest klasa najczęściej wskazywana przez poszczególne drzewa.

## Jądrowe modele gęstości

**Jakie są najważniejsze zalety i ograniczenia jądrowej estymacji funkcji gęstości w porównaniu z innymi technikami, takimi jak histogramy czy estymatory parametryczne?**

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

## DGLM - Double Generalized Linear Model

**Przedstaw koncepcję modelu DGLM (Double Generalized Linear Model) oraz krótko omów sposób estymacji jego parametrów.**

W klasycznym modelu GLM zakłada się, że parametr dyspersji $\phi$ jest stały dla wszystkich obserwacji. DGLM znoszą to ograniczenie, pozwalając, aby parametr dyspersji $\phi$ również zależał od cech danej obserwacji. W efekcie DGLM składa się z dwóch powiązanych ze sobą modeli:
* modelu dla wartości średniej (tak jak w standardowym GLM),
* modelu dyspersji.

Dzięki temu model może lepiej dopasować się do danych, w których zmienność nie jest stała.

Estymacja parametrów jest procesem iteracyjnym:

1. Dopasowanie GLM dla średniej odpowiedzi, ze stałym $\phi$ dla wszystkich obserwacji.

2. Obliczenie wkładu każdej obserwacji do dewiacji i obliczenie kwadratu Pearsona lub dewiancji reszt $R_i^2$.

3. Dopasowanie GLM dla dyspersji, przyjmując jako zmienną objaśnianą $R_i^2$. Przyjmuje się rozkład Gamma i na tym etapie nie uwzględnia się wag. Dopasowane wartości stają się nowym parametrem dyspersji dla każdej obserwacji.

4. Dopasowanie GLM dla wartości średniej, ale tym razem z wykorzystaniem specyficznego dla każdej obserwacji parametru dyspersji (dzieląc wagę przez parametr dyspersji dla danej obserwacji uzyskany w poprzednim kroku).

5. Obliczenie kwadratu Pearsona lub dewiancji reszt $R_i^2$ i powtarzanie kolejnych kroków aż do osiągnięcia zbieżności parametrów.

## Reszty surowe, standaryzowane i "studentyzowane"

**W jaki sposób oblicza się reszty dewiancyjne (deviance residuals)?**

Reszty dewiancyjne ($r_{i}^D$) są zdefiniowane jako pierwiastek kwadratowy z wkładu i-tej obserwacji do łącznej dewiancji modelu, z uwzględnieniem znaku reszty prostej. Wzór:

$$r_{i}^D = \text{sign}(y_i - \hat{\mu}_i)\sqrt{d_i} \text{}$$

gdzie:
* $y_i$ to i-ta obserwowana wartość zmiennej odpowiedzi.
* $\hat{\mu}_i$ to i-ta dopasowana (przewidywana) wartość średnia z modelu.
* $d_i$ to wkład i-tej obserwacji do całkowitej dewiancji modelu, $D(y, \hat{\mu})$.
* $\text{sign}(y_i - \hat{\mu}_i) = \begin{cases} 1 & \text{jeżeli } y_i > \hat{\mu}_i \\ -1 & \text{w p.p.} \end{cases}$

---
**Dlaczego reszty dewiancyjne są często preferowaną formą reszt w modelach GLM? Jakie są główne zalety ich wykorzystania w porównaniu z innymi rodzajami reszt?**

Reszty dewiancyjne są często preferowaną formą w Uogólnionych Modelach Liniowych (GLM), ponieważ w przeciwieństwie do innych typów reszt, uwzględniają one kształt rozkładu zmiennej odpowiedzi, w tym jego skośność. Jest to kluczowe w zastosowaniach aktuarialnych, gdzie rozkłady rzadko są symetryczne.

Główne zalety ich wykorzystania w porównaniu z innymi rodzajami reszt to:

* Lepsze dopasowanie do założeń GLM: w przeciwieństwie do reszt Pearsona, które wywodzą się z modeli liniowych, reszty dewiancyjne są bezpośrednio powiązane z funkcją wiarygodności przyjętego rozkładu z rodziny wykładniczej, co czyni je bardziej odpowiednimi dla struktury GLM.
* Wykrywanie obserwacji słabo dopasowanych: pozwalają zidentyfikować te obserwacje, które w największym stopniu przyczyniają się do wzrostu dewiancji, a więc wskazują na miejsca, w których model niedostatecznie dobrze dopasowuje się do danych.
* Korekta na heteroskedastyczność: podobnie jak reszty Pearsona, ale w przeciwieństwie do reszt prostych (surowych), korygują one fakt, że wariancja w modelach GLM często zależy od wartości średniej. Reszty proste mogą być przez to mniej informatywne.
* Lepsza interpretacja dla danych dyskretnych: chociaż indywidualne reszty dla danych dyskretnych (np. liczby szkód) mogą być trudne do interpretacji, reszty dewiancyjne obliczone dla zagregowanych grup ryzyka dają znacznie lepsze wskazówki co do poprawności dopasowania modelu.