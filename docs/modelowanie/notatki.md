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

Estymator Hilla znajduje zastosowanie w sytuacjach, gdzie kluczowe jest modelowanieszkód ekstremalnych (tzn. zdarzeń rzadkich, ale potencjalnie o dużej wartości). Wubezpieczeniach majątkowych jego użycie pozwala na lepsze zarządzanie ryzykiem iwycenę produktów ubezpieczeniowych. Jako przykład można wskazać:

* Wyznaczanie wysokości składki reasekuracyjnej. Firma ubezpieczeniowa zawieraumowę reasekuracyjną, aby zabezpieczyć się przed nadmiernymi stratamiwynikającymi z ekstremalnych szkód (np. klęski żywiołowe). Estymator Hillasłuży do oszacowania parametru grubości ogona rozkładu strat. Pozwala to naokreślenie prawdopodobieństwa wystąpienia szkody powyżej ustalonego progu.

* Modelowanie katastroficznych szkód majątkowych. W regionach zagrożonychkatastrofami naturalnymi (huragany, powodzie) ubezpieczyciel musi oszacowaćwartość strat wynikających z rzadkich, ale ekstremalnych zdarzeń. EstymatorHilla pozwala na modelowanie ryzyka ekstremalnych szkód w oparciu o danehistoryczne.

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

## Wygładzanie wykładnicze

Wygładzanie wykładnicze to jedna z metod prognozowania i analizy szeregów czasowych, która nadaje większą wagę nowszym obserwacjom, jednocześnie stopniowo zmniejszając wpływ starszych danych. Jest to technika używana do wygładzania fluktuacji w danych, co ułatwia identyfikację trendów i wzorców. Główne zastosowania:

* Prognozowanie krótkoterminowe.
* Wygładzanie danych – redukcja szumów w danych poprzez eliminowanie nagłych skoków i anomalii.
* Modelowanie trendów i sezonowości – bardziej zaawansowane wersje, jak podwójne i potrójne wygładzanie wykładnicze (Holt-Winters), pozwalają uwzględniać trend i sezonowość w danych.

Rodzaje wygładzania wykładniczego:

* Proste wygładzanie wykładnicze – stosowane do danych bez wyraźnego trendu ani sezonowości.
* Wygładzanie podwójne (Holt's method) – uwzględnia zarówno poziom, jak i trend.
* Wygładzanie potrójne (Holt-Winters method) – dodatkowo uwzględnia sezonowość. Wygładzanie wykładnicze jest szczególnie cenione za swoją prostotę i skuteczność w prognozowaniu, zwłaszcza gdy dane wykazują krótkoterminowe fluktuacje.

## Interakcja czynników ryzyka

Interakcja w kontekście czynników ryzyka ubezpieczeniowego odnosi się do sytuacji, w której wpływ jednego czynnika ryzyka na prawdopodobieństwo wystąpienia szkody zależy od obecności innego czynnika ryzyka. Oznacza to, że efekty dwóch (lub więcej) zmiennych nie są jedynie sumą ich indywidualnych wpływów, ale mogą się wzmacniać lub osłabiać w zależności od ich wzajemnego oddziaływania. Różnica między interakcją a korelacją:

* Korelacja mierzy stopień współzmienności dwóch zmiennych, czyli na ile ich wartości są statystycznie powiązane (np. wzrost jednej zmiennej towarzyszy wzrostowi drugiej).
* Interakcja odnosi się do sposobu, w jaki jedna zmienna modyfikuje wpływ drugiej na określone zjawisko, np. ryzyko szkody. Może oznaczać, że efekt jednej zmiennej występuje tylko pod warunkiem obecności drugiej. 

Korelacja sama w sobie nie oznacza interakcji – dwie zmienne mogą być silnie skorelowane, ale nie muszą wpływać na siebie nawzajem w sposób interakcyjny. Dlatego w analizie ryzyka ubezpieczeniowego ważne jest stosowanie modeli, które uwzględniają nie tylko współzależności, ale także potencjalne efekty interakcji między czynnikami.

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

## Dendrogram

Dendrogram to drzewiasta struktura, która przedstawia sposób łączenia obiektów w grupy (skupienia, klastry) na różnych poziomach podobieństwa. Poziome cięcie na określonej wysokości oznacza usunięcie połączeń powyżej tej wartości, co prowadzi do podziału obiektów na skupienia. Ich liczba zależy od wysokości, na której wykonano cięcie – im niżej, tym więcej mniejszych skupień, im wyżej, tym mniej większych.

Wysokość połączenia odzwierciedla odległość (niepodobieństwo) między grupowanymi obiektami lub skupieniami. Im wyżej następuje połączenie, tym większe różnice między skupieniami. Pomaga to wybrać odpowiednią liczbę skupień oraz zrozumieć strukturę danych.