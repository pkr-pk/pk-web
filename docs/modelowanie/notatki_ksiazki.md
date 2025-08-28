---
layout: math
title: Notatki z książek
parent: Modelowanie
nav_order: 100
---

## Wprowadzenie do Klasyfikacji Ryzyka

Działalność ubezpieczeniowa polega na sprzedaży obietnic pokrycia przyszłych strat w zamian za składkę płaconą z góry. Ponieważ ostateczny koszt usługi nie jest znany w momencie sprzedaży polisy, ubezpieczyciele opierają się na danych historycznych i modelach aktuarialnych, aby ustalić cenę. Centralnym elementem tej ceny jest **składka czysta** (*pure premium*), czyli najlepsze oszacowanie (wartość oczekiwana) przyszłych zobowiązań.

***

## Taryfa Techniczna a Cennik Komercyjny

### Cena sprzedaży a koszty operacyjne

Istnieje kluczowa różnica między dwoma rodzajami cenników w ubezpieczeniach:

* **Taryfa techniczna** ma na celu jak najdokładniejsze oszacowanie składki czystej dla każdego klienta i służy jako wewnętrzny punkt odniesienia do oceny ryzyka. Taryfa ta opiera się na **łącznym koszcie operacyjnym**, który obejmuje modelowane koszty szkód, koszty bieżące (personel, budynki), narzut na bezpieczeństwo i koszty reasekuracji oraz zysk dla akcjonariuszy.
* **Cennik komercyjny** to faktyczna cena sprzedaży oferowana klientom. Ma ona na celu optymalizację zysku ubezpieczyciela i musi być zgodna z przepisami prawa, a także uwzględniać czynniki takie jak ograniczenia systemów informatycznych czy kanały sprzedaży.

### Czynnik ryzyka a czynnik taryfikacyjny

* **Czynnik ryzyka** (*risk factor*) to każda obserwowalna cecha, która ma wpływ na poziom ryzyka, np. wiek, płeć, zawód klienta czy typ jego samochodu.
* **Czynnik taryfikacyjny** (*rating factor*) to czynnik ryzyka, który jest **faktycznie wykorzystywany** w cenniku komercyjnym. Nie wszystkie czynniki ryzyka stają się czynnikami taryfikacyjnymi z powodu regulacji prawnych lub decyzji handlowych.
    * **Przykład 1**: Płeć jest istotnym czynnikiem ryzyka, ale dyrektywy unijne zakazują jej używania jako czynnika taryfikacyjnego w UE.
    * **Przykład 2**: Status palacza w ubezpieczeniach na życie jest czynnikiem ryzyka, ale ubezpieczyciele nie zawsze przyznają zniżki palaczom przy rentach dożywotnich, mimo ich krótszej oczekiwanej długości życia.

### Wycena "Top-Down"

Aktuariusze zazwyczaj łączą dwa podejścia do wyceny:

1. **Analiza na poziomie portfela**: Prognozuje się ogólne przyszłe koszty szkód i ustala całkowitą kwotę składki potrzebną dla całego portfela.
2. **Analiza na poziomie indywidualnym**: Identyfikuje się profile ryzyka poszczególnych klientów, aby sprawiedliwie rozdzielić całkowitą składkę pomiędzy nich na podstawie ich względnej ryzykowności.

### Prewencja

Identyfikacja czynników ryzyka pomaga również w działaniach prewencyjnych. Ubezpieczyciele, informując klientów o ryzykownych zachowaniach (np. na podstawie danych telematycznych), mogą pomóc im zmniejszyć częstotliwość lub wartość szkód. Coraz częściej firmy udostępniają część swoich analiz, aby zwiększyć przejrzystość i akceptację klasyfikacji ryzyka przez klientów.

***

## Problem Klasyfikacji Ryzyka

### Dywersyfikacja Ryzyka i Prawo Wielkich Liczb

Ubezpieczenie opiera się na dywersyfikacji ryzyka, co jest możliwe dzięki **prawu wielkich liczb**. Jeśli $Y_i$ to losowa kwota świadczeń wypłaconych dla i-tej polisy, to dla dużego i jednorodnego portfela (o rozmiarze $n$), średnia wypłata na polisę ($\overline{Y}_{n}$) zbiega do wartości oczekiwanej $E[Y_1]$. Dlatego właśnie wartość oczekiwana jest najlepszym kandydatem na **składkę czystą**.

### Dlaczego Klasyfikacja Ryzyka jest Konieczna?

W praktyce portfele ubezpieczeniowe są **niejednorodne** – składają się z klientów o różnym poziomie ryzyka. Jeśli ubezpieczyciel stosuje jednolitą składkę dla wszystkich, naraża się na zjawisko **selekcji negatywnej (adwersyjnej)**. Polega ono na tym, że klienci o niższym ryzyku (którzy płacą zawyżoną składkę) odchodzą do konkurencji, a w portfelu pozostają klienci o wyższym ryzyku, co prowadzi do strat. Dlatego ubezpieczyciele muszą jak najdokładniej dopasowywać składki do indywidualnego profilu ryzyka każdego klienta.

Ze względu na dużą liczbę czynników ryzyka (demograficznych, ekonomicznych, behawioralnych), portfele stają się tak posegmentowane, że każda polisa staje się unikalna. W takiej sytuacji proste średnie nie działają, co prowadzi do konieczności stosowania **modeli regresyjnych**.

### Obserwowalne a Ukryte Czynniki Ryzyka i Solidarność

Klasyfikacja ryzyka jest zawsze niedoskonała, ponieważ ubezpieczyciel ma dostęp tylko do **obserwowalnych czynników ryzyka** (oznaczonych jako $X$), a nie do **ukrytych czynników** ($X^{+}$), takich jak umiejętności kierowcy czy jego awersja do ryzyka.

Ta niedoskonałość prowadzi do dwóch rodzajów solidarności w portfelu. Można to zilustrować za pomocą **dekompozycji wariancji** całkowitej kwoty świadczeń $Y$:

$$Var[Y]=E[Var[Y\mid X,X^{+}]]+E[Var[E[Y\mid X,X^{+}]\mid X]]+Var[E[Y\mid X]]$$

* **Solidarność losowa (zasada wzajemności)**: Pierwszy składnik, $E[Var[Y\mid X,X^{+}]]$, reprezentuje czystą losowość, której nie da się wyeliminować nawet przy doskonałej wiedzy o ryzyku. Jest to ryzyko pokrywane przez ubezpieczyciela zgodnie z zasadą wzajemności.
* **Solidarność subsydiowana**: Drugi składnik, $E[Var[E[Y\mid X,X^{+}]\mid X]]$, wynika z faktu, że ubezpieczyciel nie zna ukrytych czynników $X^{+}$. Oznacza to, że w obrębie tej samej klasy ryzyka (określonej przez $X$) klienci o niższym "prawdziwym" ryzyku subsydiują składki tych o wyższym ryzyku. Mimo to, globalna równowaga jest zachowana, ponieważ zachodzi równość $E[E[Y\mid X,X^{+}]\mid X]=E[Y\mid X]$.

### Wycena a Predykcja Strat

Celem taryfikacji ubezpieczeniowej nie jest przewidywanie faktycznej straty $Y$ dla danego klienta, ale jak najdokładniejsze oszacowanie **prawdziwej składki czystej**, czyli warunkowej wartości oczekiwanej $\mu(X)=E[Y\mid X]$.

### Zmienne *A Priori* a *A Posteriori*

* **Zmienne *a priori*** to informacje dostępne przed rozpoczęciem okresu ochrony (np. wiek, płeć, cechy pojazdu).
* **Zmienne *a posteriori*** to informacje dostępne w trakcie trwania umowy (np. historia szkodowa, dane telematyczne). Są one wykorzystywane do korygowania składek w kolejnych okresach w ramach **taryfikacji wiarygodnościowej (credibility)**.

***

## Dane Ubezpieczeniowe

### Dane o Roszczeniach (*Claim Data*)

Analizy aktuarialne opierają się na danych o **zgłoszonych roszczeniach**, a nie o wszystkich wypadkach. Dzieje się tak, ponieważ klienci nie zawsze zgłaszają drobne szkody, aby uniknąć wzrostu składki w przyszłości (np. z powodu systemu bonus-malus) lub jeśli kwota szkody jest niższa od franszyzy. Ponadto, dane często zawierają **straty poniesione (*incurred losses*)**, które są sumą dokonanych wypłat i rezerw na przyszłe płatności, ponieważ ostateczny koszt dużej szkody może być znany dopiero po kilku latach.

### Dekompozycja Częstotliwość-Wartość Szkody (*Frequency-Severity*)

Zamiast modelować bezpośrednio całkowitą roczną kwotę szkód ($Y$), aktuariusze zazwyczaj rozkładają ją na dwa komponenty: **liczbę szkód ($N$)** oraz **wartość (ciężkość) pojedynczej szkody ($C_k$)**. To podejście jest bardziej elastyczne i pozwala analizować wpływ np. franszyzy na pojedynczą szkodę. Matematycznie, dekompozycja ta jest zapisywana jako suma:

$$Y = \sum_{k=1}^{N} C_k$$

Modelowanie wartości szkody jest często trudniejsze niż modelowanie jej częstotliwości. Dzieje się tak z powodu mniejszej ilości danych (tylko 5-10% polis generuje szkody) oraz faktu, że koszt wypadku w dużej mierze zależy od czynników zewnętrznych (np. charakterystyk strony trzeciej), a nie od samego ubezpieczonego.

### Dane Obserwacyjne i Problem Korelacji

Dane ubezpieczeniowe mają charakter **obserwacyjny**, a nie eksperymentalny. Portfel klientów danej firmy nie jest losową próbą całej populacji, co oznacza, że należy ostrożnie podchodzić do generalizacji wyników.

Najważniejszą konsekwencją jest trudność w odróżnieniu **korelacji od związku przyczynowo-skutkowego**. Obserwowany związek między czynnikiem ryzyka a szkodowością może wynikać z **efektu zakłócającego (*confounding effect*)**, gdzie oba te czynniki są skorelowane z trzecim, ukrytym czynnikiem. Na przykład, posiadanie dzieci może być skorelowane z niższą szkodowością nie dlatego, że dzieci poprawiają umiejętności prowadzenia pojazdu, ale dlatego, że posiadanie dzieci jest skorelowane z większą awersją do ryzyka, która jest prawdziwą przyczyną ostrożniejszej jazdy.

### Format i Jakość Danych

Dane do analizy zazwyczaj składają się z połączonych informacji o polisach i szkodach na poziomie indywidualnego ryzyka (np. pojazdu w ubezpieczeniu komunikacyjnym). Każdy rekord w bazie danych powinien odpowiadać okresowi, w którym wszystkie czynniki ryzyka pozostały niezmienione.

Zmienne (cechy) mogą mieć różne formaty:
* **Kategoryczne**: np. płeć (mężczyzna/kobieta).
* **Dyskretne**: np. liczba pojazdów w gospodarstwie domowym.
* **Ciągłe**: np. wiek ubezpieczającego.

Zmienne kategoryczne są przekształcane na **zmienne zero-jedynkowe (*dummy variables*)**, aby mogły być użyte w modelach regresyjnych.

Należy podkreślić kluczowe znaczenie **jakości danych** i **eksploracyjnej analizy danych**. Bez starannego przygotowania i zrozumienia danych, nawet najbardziej zaawansowane modele mogą prowadzić do błędnych wniosków, zgodnie z zasadą "**śmieci na wejściu, śmieci na wyjściu**" (*garbage in, garbage out*).

***

## Wprowadzenie do Rozkładów Wykładniczych Dyspersji

W analizach ubezpieczeniowych zmienna $Y$ rzadko ma rozkład normalny. Typowe zmienne, takie jak liczba szkód, koszt szkody czy czas życia, nie spełniają założeń normalności, ponieważ:
* ich rozkłady są często **dodatnio skośne**, 
* koncentrują masę prawdopodobieństwa na niewielkim zbiorze liczb całkowitych, 
* ich wariancja zazwyczaj rośnie wraz ze średnią. 

Przykłady takich zmiennych to:
* Liczba szkód ($N$) 
* Skłonność do zgłaszania szkód ($I[N \ge 1]$) 
* Koszt pojedynczej szkody ($C_k$) 
* Całkowity roczny koszt szkód ($S$) 
* Czas do zdarzenia, np. długość życia ($T$) 

Z powodu tych specyficznych cech, aktuariusze często wybierają rozkład dla zmiennej objaśnianej z **rodziny wykładniczych rozkładów dyspersji (ED)**. 

W zależności od charakteru zmiennej, do jej modelowania używa się:
* Dla zmiennych zliczających (np. liczba szkód) – **funkcji masy prawdopodobieństwa**:

    $$p_Y(y) = P[Y=y]$$

* Dla zmiennych ciągłych (np. wysokość szkody) – **funkcji gęstości prawdopodobieństwa**:

    $$f_Y(y) = \frac{d}{dy}P[Y \le y]$$

***

## Od Rozkładu Normalnego do Rodziny ED

### Rozkład Normalny jako Punkt Wyjścia

Rozkład normalny $Y \sim \mathcal{N}(\mu, \sigma^2)$ jest opisany funkcją gęstości prawdopodobieństwa:

$$f_{Y}(y)=\frac{1}{\sigma\sqrt{2\pi}}\exp\left(-\frac{1}{2\sigma^{2}}(y-\mu)^{2}\right)$$

Jego kluczowe cechy to symetryczny, dzwonowaty kształt oraz niezależność wariancji ($Var[Y] = \sigma^2$) od wartości średniej ($E[Y] = \mu$). Chociaż te właściwości rzadko pasują do danych ubezpieczeniowych, struktura matematyczna tego rozkładu jest punktem wyjścia do uogólnień.

### Definicja Rodziny Wykładniczych Rozkładów Dyspersji (ED)

Aby przejść od rozkładu normalnego do rodziny ED, należy przekształcić jego funkcję gęstości, aby wyizolować parametry średniej $\mu$ i wariancji $\sigma^2$:

$$f_{Y}(y)=\exp\left(\frac{y\mu-\frac{\mu^{2}}{2}}{\sigma^{2}}\right)\frac{\exp(-\frac{y^{2}}{2\sigma^{2}})}{\sigma\sqrt{2\pi}}$$

Ta forma ujawnia strukturę, która jest następnie uogólniana do definicji rodziny ED. Rozkład należy do rodziny ED, jeśli jego funkcja masy lub gęstości prawdopodobieństwa ma postać:

$$\exp\left(\frac{y\theta - a(\theta)}{\phi/\nu}\right) c(y, \phi/\nu)$$

gdzie:
* $\theta$ to **parametr kanoniczny** (związany z lokalizacją).
* $\phi$ to **parametr dyspersji** (związany ze skalą).
* $\nu$ to znana stała, nazywana **wagą**.
* $a(\cdot)$ to funkcja zwana kumulantą.
* $c(\cdot)$ to funkcja normalizująca.

Dla rozkładu normalnego parametry te przyjmują wartości: $\theta = \mu$, $a(\theta) = \theta^2/2$, $\phi = \sigma^2$ oraz $\nu=1$. W ten sposób rozkład normalny staje się szczególnym przypadkiem znacznie ogólniejszej rodziny ED, która może opisywać rozkłady skośne i takie, w których wariancja zależy od średniej.

### Inne Rozkłady Związane z Rozkładem Normalnym

W sekcji wspomniano również o innych rozkładach wywodzących się z rozkładu normalnego, które są ważne w statystyce, takich jak rozkład **logarytmiczno-normalny**, **chi-kwadrat ($\chi^2$)**, **t-Studenta** oraz **F-Fishera**.

***

## Wybrane Rozkłady z Rodziny ED

### Rozkład Gamma

* **Zastosowanie**: Często używany do modelowania dodatnich i prawostronnie skośnych zmiennych, takich jak **wartości (ciężkości) szkód**.
* **Własność kluczowa**: Wariancja jest **kwadratową funkcją wartości średniej**: $Var[Y] = \frac{1}{\alpha}(E[Y])^2$. Oznacza to, że współczynnik zmienności pozostaje stały.
* **Funkcja gęstości prawdopodobieństwa** ($Y \sim Gam(\alpha, \tau)$):

    $$f_{Y}(y)=\frac{y^{\alpha-1}\tau^{\alpha}\exp(-\tau y)}{\Gamma(\alpha)}$$

### Rozkład Odwrotny Gaussa (*Inverse Gaussian*)

* **Zastosowanie**: Alternatywa dla rozkładu Gamma do modelowania dodatnich, prawostronnie skośnych danych.
* **Własność kluczowa**: Wariancja jest **sześcienną funkcją wartości średniej**: $Var[Y] = \frac{1}{\alpha}(E[Y])^3$. Oznacza to, że jego "ogon" jest cięższy niż w rozkładzie Gamma, ale lżejszy niż w rozkładzie logarytmiczno-normalnym.
* **Funkcja gęstości prawdopodobieństwa** ($Y \sim IGau(\mu, \alpha)$):

    $$f_{Y}(y)=\sqrt{\frac{\alpha}{2\pi y^{3}}}\exp\left(-\frac{\alpha(y-\mu)^{2}}{2y\mu^{2}}\right)$$

### Rozkład Dwumianowy (*Binomial*)

* **Zastosowanie**: Opisuje liczbę "sukcesów" w $m$ niezależnych próbach. W ubezpieczeniach na życie używany do modelowania **liczby zgonów** w zamkniętej grupie.
* **Własność kluczowa**: Charakteryzuje się **niedostateczną dyspersją (*underdispersion*)**, co oznacza, że jego wariancja jest mniejsza niż wartość średnia: $Var[Y] < E[Y]$.
* **Funkcja masy prawdopodobieństwa** ($Y \sim Bin(m, q)$):

    $$p_{Y}(y)=\binom{m}{y}q^{y}(1-q)^{m-y}$$

* **Pokrewne rozkłady**: Rozkład Pascala (Ujemny Dwumianowy), który modeluje liczbę porażek przed osiągnięciem $m$ sukcesów, charakteryzuje się **nadmierną dyspersją (*overdispersion*)**.

### Rozkład Poissona (*Poisson*)

* **Zastosowanie**: Jest to fundamentalny rozkład do modelowania **liczby (częstotliwości) szkód**. Powstaje jako graniczna forma rozkładu dwumianowego dla zdarzeń rzadkich.
* **Własność kluczowa**: Charakteryzuje się **równą dyspersją (*equidispersion*)**, co oznacza, że jego wariancja jest równa wartości średniej: $Var[Y] = E[Y]$.
* **Funkcja masy prawdopodobieństwa** ($Y \sim Poi(\lambda)$):

    $$p_{Y}(y)=\exp(-\lambda)\frac{\lambda^{y}}{y!}$$

* **Ekspozycja na ryzyko**: W praktyce, średnia Poissona jest skalowana przez **ekspozycję na ryzyko** ($e$), np. długość okresu obserwacji. Model przyjmuje wtedy postać $Y \sim Poi(\lambda e)$.

***

## Użyteczne Właściwości Rodziny ED

### Wartość Średnia, Wariancja i Funkcja Wariancji

Momenty rozkładu z rodziny ED są ściśle powiązane z pochodnymi funkcji kumulanty $a(\theta)$.

* **Wartość średnia** ($E[Y] = \mu$) jest równa pierwszej pochodnej funkcji $a(\theta)$:

    $$E[Y]=a^{\prime}(\theta)$$

* **Wariancja** ($Var[Y]$) jest proporcjonalna do drugiej pochodnej funkcji $a(\theta)$:

    $$Var[Y]=\frac{\phi}{\nu}a^{\prime\prime}(\theta)$$

Z tych relacji wynika kluczowe pojęcie **funkcji wariancji** $V(\mu)$, która opisuje, jak wariancja zależy od wartości średniej. Jest ona zdefiniowana jako druga pochodna funkcji kumulanty, wyrażona jako funkcja średniej $\mu$:

$$V(\mu) = a^{\prime\prime}(\theta)$$

Dzięki temu wariancję można zapisać w bardziej intuicyjnej formie:

$$Var[Y]=\frac{\phi}{\nu}V(\mu)$$

Funkcja wariancji jest unikalną cechą każdego rozkładu z rodziny ED i odgrywa centralną rolę w Uogólnionych Modelach Liniowych (GLM). Przykłady dla najważniejszych rozkładów to:
* **Normalny**: $V(\mu) = 1$ (wariancja stała)
* **Poissona**: $V(\mu) = \mu$ (wariancja równa średniej)
* **Gamma**: $V(\mu) = \mu^2$ (wariancja rośnie kwadratowo ze średnią)
* **Odwrotny Gaussa**: $V(\mu) = \mu^3$ (wariancja rośnie sześciennie ze średnią)

### Średnie i Wagi

Rodzina ED ma niezwykłą właściwość polegającą na tym, że jest **zamknięta ze względu na uśrednianie**. Oznacza to, że średnia arytmetyczna $n$ niezależnych zmiennych losowych o tym samym rozkładzie z rodziny ED (z wagą $\nu$) również ma ten sam typ rozkładu, ale z nową, większą wagą równą $n\nu$.

Ta właściwość jest niezwykle ważna w praktyce aktuarialnej, ponieważ pozwala na modelowanie danych zagregowanych (np. średnich szkód dla grup klientów) w ten sam sposób, co danych indywidualnych, po prostu przypisując odpowiednie wagi. Przykładem jest modelowanie proporcji w rozkładzie dwumianowym, gdzie liczba prób $m$ działa jako waga.

***

## Rozkłady Tweedie

### Potęgowa Funkcja Wariancji

Tym, co wyróżnia rozkłady Tweedie, jest ich **potęgowa funkcja wariancji**. Oznacza to, że relacja między wariancją a wartością średnią ma stałą, potęgową postać, zdefiniowaną przez parametr $\xi$:

$$V(\mu)=\mu^{\xi}$$

Wariancja zmiennej losowej $Y$ o rozkładzie Tweedie wynosi zatem $Var[Y] = \phi \mu^{\xi}$ (przy założeniu jednostkowej wagi).

Wiele kluczowych rozkładów używanych w ubezpieczeniach należy do tej rodziny:
* **Rozkład Normalny**: dla $\xi = 0$
* **Rozkład Poissona**: dla $\xi = 1$
* **Rozkład Gamma**: dla $\xi = 2$
* **Rozkład Odwrotny Gaussa**: dla $\xi = 3$

Istotną cechą jest fakt, że rozkłady Tweedie istnieją dla wszystkich wartości $\xi$ z wyjątkiem przedziału $(0, 1)$.

### Zamknięcie ze względu na Transformacje Skali

W przeciwieństwie do ogólnej rodziny ED, klasa rozkładów Tweedie jest **zamknięta ze względu na transformacje skali**. Oznacza to, że jeśli zmienna losowa $Y$ ma rozkład Tweedie, to przeskalowana zmienna $\delta Y$ (dla $\delta > 0$) również ma rozkład Tweedie z tym samym parametrem potęgowym $\xi$.

Zmieniają się jedynie parametry średniej i dyspersji:
* Nowa średnia: $\delta\mu$
* Nowy parametr dyspersji: $\phi(\delta)^{2-\xi}$

Ta właściwość jest niezwykle użyteczna w praktyce. Pozwala aktuariuszom na elastyczność w modelowaniu – mogą pracować zarówno z całkowitymi kosztami szkód, jak i ze wskaźnikami (np. kosztem szkody na jednostkę ekspozycji), a model wciąż będzie należał do tej samej, dobrze zdefiniowanej klasy rozkładów.

***

## Bootstrap

Bootstrap to metoda numeryczna, która pozwala ocenić dokładność estymatora (np. jego błąd standardowy lub przedział ufności), zwłaszcza gdy analityczne wzory są trudne lub niemożliwe do wyprowadzenia. Jest to technika oparta na symulacji komputerowej.

### Zasada Wtyczki (*Plug-in Principle*) i Procedura Bootstrap

Główną ideą bootstrapu jest **zasada wtyczki (*plug-in principle*)**. Ponieważ nie znamy prawdziwego rozkładu prawdopodobieństwa $F$, z którego pochodzi nasza próba, zastępujemy go jego najlepszym przybliżeniem, jakim dysponujemy – **empiryczną dystrybuantą** $\hat{F}_n$:

$$\hat{F}_n(x) = \frac{1}{n}\sum_{i=1}^{n} I[Y_i \le x]$$

Empiryczna dystrybuanta przypisuje każdej zaobserwowanej wartości $Y_i$ w próbie równe prawdopodobieństwo $\frac{1}{n}$.

Ponieważ analityczne obliczenia oparte na $\hat{F}_n$ są często zbyt skomplikowane, stosuje się symulację. Procedura bootstrap polega na wielokrotnym **losowaniu ze zwracaniem** z oryginalnej próby danych w celu utworzenia nowych, "bootstrapowych" prób danych.

1. **Tworzenie prób bootstrapowych**: Z oryginalnego zbioru danych o rozmiarze $n$ losuje się (ze zwracaniem) $n$ obserwacji. Proces ten powtarza się $B$ razy (np. $B=10000$), tworząc $B$ nowych prób, z których każda ma rozmiar $n$.
2. **Obliczanie statystyki**: Dla każdej z $B$ prób bootstrapowych oblicza się wartość interesującego nas estymatora (np. średniej, mediany, współczynnika regresji).
3. **Ocena dokładności**: Otrzymujemy w ten sposób $B$ wartości estymatora. Rozkład tych wartości (rozkład bootstrapowy) służy do oceny dokładności. Na przykład błąd standardowy oryginalnego estymatora można przybliżyć przez odchylenie standardowe $B$ wartości bootstrapowych.

### Bootstrap Nieparametryczny a Parametryczny

* **Bootstrap nieparametryczny**: Jest to standardowe podejście opisane powyżej, gdzie losowanie odbywa się bezpośrednio z oryginalnych danych.
* **Bootstrap parametryczny**: W tym podejściu najpierw dopasowuje się do danych model parametryczny (np. rozkład Poissona z estymowanym parametrem $\hat{\lambda}$), a następnie losowanie nowych prób odbywa się z tego dopasowanego rozkładu, a nie z surowych danych.

Metoda bootstrap jest szeroko stosowana do konstruowania przedziałów ufności i oceny stabilności modeli statystycznych.

***

## Wprowadzenie do Uogólnionych Modeli Liniowych (GLM)

Model GLM jest zdefiniowany przez dwa kluczowe komponenty:
1. **Rozkład zmiennej objaśnianej**: Zakłada się, że zmienna objaśniana (np. liczba szkód) pochodzi z **rodziny wykładniczych rozkładów dyspersji (ED)**.
2. **Funkcja łącząca**: Określa ona, w jaki sposób średnia wartość zmiennej objaśnianej jest powiązana z **kombinacją liniową cech (predyktorem liniowym lub *score*)**.

### Typowe Zastosowania GLM w Ubezpieczeniach

GLM są rutynowo stosowane w różnych obszarach działalności ubezpieczeniowej, takich jak underwriting, wycena czy zarządzanie szkodami. Do najważniejszych zastosowań należą:

* **Modelowanie liczby szkód**: Najczęściej wykorzystuje się rozkład Poissona, zakładając, że średnia częstotliwość szkód jest wykładniczą funkcją predyktora liniowego.
* **Modelowanie wartości szkód**: Ze względu na dodatnią i skośną naturę kosztów szkód, naturalnym wyborem są rozkłady Gamma lub Odwrotny Gaussa.
* **Graduacja stawek umieralności i zachorowalności**: Modele GLM oparte na rozkładach dwumianowym i Poissona pozwalają na klasyfikację ryzyka w ubezpieczeniach na życie i zdrowotnych.
* **Modelowanie elastyczności cenowej**: Modele te pomagają przewidywać, jak zmiany w składkach wpłyną na udział w rynku i rentowność.
* **Rezerwacja szkodowa**: Uogólniony model Poissona z nadmierną dyspersją (ODP) jest odpowiednikiem klasycznej metody Chain-Ladder. GLM można również stosować do rezerwacji indywidualnej, prognozując czas do zamknięcia szkody lub jej ostateczny koszt.
* **Analiza konkurencji**: GLM mogą być używane do odtworzenia (inżynierii odwrotnej) cenników konkurencji na podstawie zebranych ofert.

***

## Struktura Uogólnionych Modeli Liniowych (GLM)

Uogólniony Model Liniowy (GLM) to elastyczne narzędzie regresyjne, które oddziela systematyczne cechy danych od ich losowej zmienności. Jego struktura opiera się na trzech kluczowych komponentach.

### 1. Komponent Losowy: Rozkład Zmiennej Objaśnianej

Pierwszy element GLM dotyczy założeń o losowej naturze danych.

* **Rozkład z rodziny ED**: Zakłada się, że każda obserwacja zmiennej objaśnianej $Y_i$ pochodzi z **rodziny wykładniczych rozkładów dyspersji (ED)**. Oznacza to, że model jest w stanie obsłużyć zmienne, które nie mają rozkładu normalnego, takie jak liczba szkód (rozkład Poissona) czy ich wartość (rozkład Gamma).
* **Modelowanie wartości oczekiwanej**: Celem GLM w ubezpieczeniach nie jest przewidywanie dokładnej wartości straty $Y_i$, ale oszacowanie jej **warunkowej wartości oczekiwanej**, czyli składki czystej: $\mu(x) = E[Y \mid X = x]$.
* **Niezależność, ale niejednakowy rozkład**: Zakłada się, że obserwacje $Y_1, ..., Y_n$ są od siebie niezależne. Jednakże, nie mają one identycznego rozkładu, ponieważ ich wartość oczekiwana $\mu_i$ zależy od indywidualnych cech (predyktorów) $x_i$.
* **Wagi**: Model może uwzględniać wagi $\nu_i$ dla każdej obserwacji, co jest przydatne przy analizie danych zagregowanych, gdzie waga może odzwierciedlać np. liczbę polis w danej grupie.

### 2. Komponent Systematyczny: Predyktor Liniowy

Komponent systematyczny opisuje, w jaki sposób cechy (predyktory) wpływają na modelowaną wartość.

* **Definicja**: Jest to **predyktor liniowy**, w ubezpieczeniach często nazywany **score**. Stanowi on liniową kombinację cech $x_{ij}$ i estymowanych współczynników regresji $\beta_j$:

    $$score_i = x_i^T \beta = \beta_0 + \sum_{j=1}^{p} \beta_j x_{ij}$$

* **Liniowość względem parametrów**: Kluczowe jest zrozumienie, że termin "liniowy" odnosi się do liniowości względem **parametrów $\beta_j$**, a niekoniecznie samych cech. Oznacza to, że model może zawierać nieliniowe transformacje predyktorów (np. $x^2$ lub $\ln(x)$), a wciąż będzie traktowany jako GLM.

### 3. Funkcja Łącząca (*Link Function*)

Trzeci komponent to **funkcja łącząca** $g(\cdot)$, która stanowi pomost między komponentem systematycznym (predyktorem liniowym) a oczekiwaną wartością komponentu losowego ($\mu_i$).

* **Definicja**: Funkcja łącząca jest gładką i odwracalną transformacją, która wiąże wartość oczekiwaną $\mu_i$ z predyktorem liniowym:

    $$g(\mu_i) = score_i \quad \iff \quad \mu_i = g^{-1}(score_i)$$

* **Cel**: Jej głównym zadaniem jest odwzorowanie nieograniczonego zakresu predyktora liniowego (od $-\infty$ do $+\infty$) na ograniczony, dopuszczalny zakres wartości oczekiwanej $\mu_i$. Na przykład dla liczby szkód (rozkład Poissona) $\mu_i$ musi być dodatnie, a dla prawdopodobieństw (rozkład dwumianowy) $\mu_i$ musi należeć do przedziału $[0, 1]$.
* **Typowe funkcje łączące**:
    * **Logarytm (`log link`)**: $g(\mu_i) = \ln(\mu_i)$. Jest najczęściej stosowana dla liczby i wartości szkód. Prowadzi do **taryfy multiplikatywnej**, gdzie wpływ poszczególnych cech na składkę jest mnożony.
    * **Logit (`logit link`)**: $g(\mu_i) = \ln\left(\frac{\mu_i}{1-\mu_i}\right)$. Jest używana do modelowania prawdopodobieństw (np. prawdopodobieństwa wystąpienia szkody).
* **Kanoniczna funkcja łącząca**: Jest to szczególny przypadek, w którym funkcja łącząca jest taka, że predyktor liniowy staje się równy parametrowi kanonicznemu ($\theta_i = score_i$), co upraszcza estymację i interpretację modelu.

### Interakcje

GLM nie uwzględnia automatycznie interakcji między zmiennymi. Jeśli efekt jednego czynnika zależy od poziomu innego (np. wpływ wieku na ryzyko zależy od płci), taką **interakcję** należy jawnie dodać do modelu, najczęściej poprzez włączenie do predyktora liniowego iloczynu odpowiednich cech.

***

## Równania Estymacyjne w GLM

Po zdefiniowaniu struktury Uogólnionego Modelu Liniowego (GLM), jego parametry (współczynniki regresji $\beta$) są estymowane za pomocą **metody największej wiarygodności (Maximum Likelihood)**. Metoda ta polega na znalezieniu takich wartości parametrów, które maksymalizują prawdopodobieństwo zaobserwowania posiadanych danych.

### Ogólna Postać Równań Wiarygodności

Aby znaleźć estymatory największej wiarygodności, maksymalizuje się funkcję log-wiarygodności $L(\beta)$ poprzez przyrównanie jej pochodnych cząstkowych względem każdego parametru $\beta_j$ do zera. W przypadku GLM, po zastosowaniu reguły łańcuchowej, prowadzi to do następującego układu równań estymacyjnych:

$$\sum_{i=1}^{n} \frac{(y_i - \mu_i)x_{ij}}{Var[Y_i]} \frac{\partial \mu_i}{\partial s_i} = 0$$

gdzie:
* $y_i$ to obserwowana wartość, a $\mu_i$ to jej dopasowana (modelowana) wartość oczekiwana.
* $x_{ij}$ to wartość $j$-tej cechy dla $i$-tej obserwacji.
* $Var[Y_i]$ to wariancja $i$-tej obserwacji, która zależy od funkcji wariancji $V(\mu_i)$.
* $s_i$ to predyktor liniowy (*score*).
* $\frac{\partial \mu_i}{\partial s_i}$ to pochodna odwrotności funkcji łączącej.

Poza modelem normalnym z tożsamościową funkcją łączącą, ten układ równań **nie ma jawnego rozwiązania** i musi być rozwiązywany numerycznie, najczęściej za pomocą algorytmu iteracyjnego IRLS (Iteratively Re-weighted Least Squares).

### Rola Kanonicznej Funkcji Łączącej i Sumy Brzegowe

Sytuacja znacznie się upraszcza, gdy używana jest **kanoniczna funkcja łącząca**. W takim przypadku równania estymacyjne redukują się do postaci:

$$\sum_{i=1}^{n} (y_i - \hat{\mu}_i) x_{ij} = 0 \quad \text{dla każdego } j=0, 1, ..., p$$

Te uproszczone równania mają niezwykle ważną i intuicyjną interpretację w praktyce aktuarialnej:
* **Globalna równowaga**: Dla wyrazu wolnego ($j=0$, gdzie $x_{i0}=1$), równanie zapewnia, że suma wszystkich dopasowanych wartości jest równa sumie wszystkich obserwowanych wartości: $\sum \hat{\mu}_i = \sum y_i$.
* **Zachowanie sum brzegowych**: Dla zmiennych kategorycznych, równanie gwarantuje, że suma dopasowanych wartości w obrębie każdej kategorii (np. dla wszystkich mężczyzn lub dla wszystkich polis z danym zakresem ochrony) jest równa sumie obserwowanych wartości w tej kategorii.

Ta właściwość oznacza, że modele z kanoniczną funkcją łączącą (np. model Poissona z funkcją logarytmiczną) są zgodne z klasyczną aktuarialną **Metodą Sum Brzegowych (Method of Marginal Totals, MMT)** i zapobiegają wzajemnemu subsydiowaniu się różnych grup ryzyka. **Uwaga**: ta cecha nie obowiązuje, jeśli funkcja łącząca nie jest kanoniczna (np. w modelu Gamma z funkcją logarytmiczną).

### Offsety

**Offset** to znana zmienna, która jest dodawana do predyktora liniowego ze stałym, z góry narzuconym współczynnikiem (zazwyczaj równym 1). Predyktor liniowy przyjmuje wtedy postać:

$$score_i = offset_i + x_i^T \beta$$

Najczęstszym zastosowaniem offsetu w modelach aktuarialnych jest uwzględnienie **ekspozycji na ryzyko** ($e_i$). W modelu Poissona z funkcją logarytmiczną, gdzie średnia liczba szkód jest proporcjonalna do ekspozycji ($\mu_i = e_i \exp(x_i^T \beta)$), równanie na skali predyktora liniowego wygląda następująco: $\ln(\mu_i) = \ln(e_i) + x_i^T \beta$. W tym przypadku **logarytm ekspozycji** jest offsetem. Inne zastosowania offsetów obejmują m.in. narzucanie z góry ustalonych wartości dla niektórych czynników taryfikacyjnych lub wykorzystywanie referencyjnych tablic trwania życia w modelowaniu umieralności.

***

## Rozwiązywanie Równań Estymacyjnych w GLM

Ponieważ równania estymacyjne dla Uogólnionych Modeli Liniowych (GLM) zazwyczaj nie mają jawnego, analitycznego rozwiązania, do estymacji parametrów $\beta$ stosuje się metody numeryczne. Najważniejszą z nich jest algorytm **Iteracyjnie Ponownie Ważonych Najmniejszych Kwadratów (IRLS)**.

### Algorytm IRLS (*Iteratively Re-weighted Least Squares*)

Algorytm IRLS jest implementacją metody scoringu Fishera (odmiany metody Newtona-Raphsona) do maksymalizacji funkcji log-wiarygodności. W praktyce sprowadza się on do iteracyjnego dopasowywania serii ważonych modeli regresji liniowej.

Kluczowe elementy algorytmu to:
* **Odpowiedź Robocza (*Working Response*)**: W każdej iteracji, zamiast oryginalnej zmiennej $y_i$, model dopasowywany jest do tzw. "odpowiedzi roboczej" $z_i$. Jest to lokalna, liniowa aproksymacja transformowanej odpowiedzi $g(y_i)$:

    $$z_i = s_i + (y_i - \mu_i)\frac{\partial s_i}{\partial \mu_i}$$

    gdzie $s_i$ to predyktor liniowy, a $\mu_i$ to dopasowana wartość oczekiwana z poprzedniej iteracji.
* **Wagi Robocze (*Working Weights*)**: Każda obserwacja w regresji otrzymuje "wagę roboczą" $\tilde{\nu}_i$, która jest odwrotnie proporcjonalna do wariancji odpowiedzi roboczej. Wagi te zmieniają się w każdej iteracji, ponieważ zależą od dopasowanych wartości $\mu_i$:

    $$\tilde{\nu}_i = \frac{\nu_i}{V(\mu_i)\left(\frac{\partial s_i}{\partial \mu_i}\right)^2}$$

**Krok iteracyjny** algorytmu polega na aktualizacji wektora parametrów $\beta$ za pomocą standardowego wzoru na estymator w ważonej metodzie najmniejszych kwadratów:

$$\hat{\beta}^{(r+1)} = (X^T \tilde{W}^{(r)} X)^{-1}X^T \tilde{W}^{(r)} z^{(r)}$$

gdzie $z^{(r)}$ to wektor odpowiedzi roboczych, a $\tilde{W}^{(r)}$ to diagonalna macierz wag roboczych z $r$-tej iteracji. Proces jest powtarzany aż do osiągnięcia zbieżności.

### Praktyczne Aspekty Specyfikacji Modelu

#### Wybór Poziomu Bazowego dla Cech Kategorycznych

Przy kodowaniu zmiennych kategorycznych kluczowy jest wybór **poziomu bazowego (referencyjnego)**. Wyraz wolny $\beta_0$ w modelu odzwierciedla efekt tego poziomu, a pozostałe współczynniki mierzą różnice względem niego. Poziom bazowy powinien być wybrany tak, aby nie był rzadko obserwowany. Wybór kategorii o małej liczebności może prowadzić do prawie osobliwej macierzy projektowej $X$ i w konsekwencji do **niestabilnych numerycznie estymatorów**.

#### Współliniowość i Skorelowane Cechy

* **Współliniowość (*Collinearity*)** występuje, gdy istnieje silna liniowa zależność między predyktorami.
* **Dokładna współliniowość** (gdy jedna zmienna jest liniową kombinacją innych) sprawia, że macierz $X^T W X$ jest osobliwa i nieodwracalna, co uniemożliwia estymację modelu.
* **Przybliżona współliniowość** prowadzi do dużych błędów standardowych estymowanych współczynników, co oznacza, że są one bardzo niedokładne. Do diagnozowania tego problemu można użyć miary **V Craméra**, zdefiniowanej jako:

    $$V = \sqrt{\frac{\chi^2/n}{\min(k_1-1, k_2-1)}}$$

    gdzie $\chi^2$ to statystyka chi-kwadrat dla testu niezależności.

#### Problem Pominiętej Zmiennej (*Omitted Variable Bias*)

Jeśli w modelu zostanie pominięty istotny czynnik ryzyka, który jest skorelowany z czynnikami uwzględnionymi w modelu, estymatory współczynników dla tych uwzględnionych czynników będą **obciążone (*biased*)**. Oznacza to, że oszacowany współczynnik $\hat{\beta}_j$ nie będzie odzwierciedlał prawdziwego, izolowanego wpływu cechy $x_j$, ale mieszankę jej wpływu oraz wpływu pominiętej zmiennej. Z tego powodu modele GLM są lepsze w identyfikowaniu korelacji niż w ustalaniu związków przyczynowo-skutkowych.

***

## Dewiancja i Ocena Dopasowania Modelu

Dewiancja jest kluczową miarą służącą do oceny **jakości dopasowania (goodness-of-fit)** Uogólnionych Modeli Liniowych (GLM). Jest to uogólnienie sumy kwadratów reszt znanej z klasycznej regresji liniowej. Aby zdefiniować dewiancję, potrzebne są dwa modele referencyjne.

### Modele Referencyjne: Zerowy i Pełny

* **Model Zerowy (*Null Model*)**: To najprostszy możliwy model, który nie uwzględnia żadnych predyktorów. Zakłada on, że wszystkie obserwacje mają tę samą wartość oczekiwaną, równą średniej z próby ($\hat{\mu}_i = \bar{y}$). Model ten reprezentuje sytuację, w której dane są całkowicie losowe i nie ma w nich żadnej systematycznej struktury do wyjaśnienia.
* **Model Pełny lub Nasycony (*Saturated Model*)**: To najbardziej złożony model, posiadający tyle parametrów, ile jest obserwacji. Taki model **dopasowuje się do danych idealnie**, co oznacza, że wartość dopasowana dla każdej obserwacji jest równa jej wartości obserwowanej ($\hat{\mu}_i = y_i$). Stanowi on punkt odniesienia dla najlepszego możliwego dopasowania, jakie można osiągnąć przy danym rozkładzie zmiennej objaśnianej.

### Definicja i Właściwości Dewiancji

**Dewiancja resztowa** (*residual deviance*) modelu jest zdefiniowana jako dwukrotność różnicy między log-wiarygodnością modelu pełnego a log-wiarygodnością analizowanego modelu. Wzór ogólny dla rodziny ED ma postać:

$$D(y, \hat{\mu}) = 2\sum_{i=1}^{n} \nu_i \left[ y_i(\tilde{\theta}_i - \hat{\theta}_i) - a(\tilde{\theta}_i) + a(\hat{\theta}_i) \right]$$

gdzie $\tilde{\theta}_i$ i $\hat{\theta}_i$ to estymatory parametru kanonicznego odpowiednio w modelu pełnym i analizowanym.
* **Interpretacja**: Dewiancja mierzy rozbieżność między modelem dopasowanym a modelem nasyconym (czyli danymi). Im większa dewiancja, tym gorzej model pasuje do danych.
* **Dewiancja Skalowana**: Dla rozkładów z nieznanym parametrem dyspersji $\phi$ (np. Gamma), używa się **dewiancji skalowanej**: $\tilde{D} = D/\phi$. Przybliżony rozkład tej statystyki to **rozkład chi-kwadrat** z liczbą stopni swobody równą $n - p - 1$ (liczba obserwacji minus liczba estymowanych parametrów):

    $$\tilde{D} \approx \chi^2_{n-p-1}$$
    
    Pozwala to na formalne testowanie dopasowania modelu.

**Ważne Ostrzeżenie: Przypadek Rozkładu Bernoulliego**
W szczególnym, ale bardzo częstym przypadku modelu dla odpowiedzi binarnej (rozkład Bernoulliego) z kanoniczną funkcją łączącą (logit), wzór na dewiancję upraszcza się w taki sposób, że **zależy ona wyłącznie od wartości dopasowanych, a nie od obserwowanych**. W rezultacie, w tym scenariuszu dewiancja nie jest miarodajną miarą jakości dopasowania.

### Kryteria Informacyjne (AIC i BIC)

Do porównywania modeli, które nie są zagnieżdżone, lub modeli opartych na różnych rozkładach, używa się **kryteriów informacyjnych**. Wprowadzają one "karę" za złożoność modelu (liczbę parametrów). Modele o niższych wartościach kryterium są preferowane.

* **Kryterium Informacyjne Akaikego (AIC)**:

    $$AIC = -2L + 2 \times (\text{liczba parametrów})$$

* **Bayesowskie Kryterium Informacyjne (BIC)**:

    $$BIC = -2L + \ln(n) \times (\text{liczba parametrów})$$

Teoretycznym uzasadnieniem dla AIC są tzw. **kary kowariancyjne**. Pokazują one, że błąd predykcji modelu na nowych danych jest w przybliżeniu równy błędowi na danych treningowych (mierzonemu przez dewiancję) powiększonemu o karę za złożoność. W przypadku GLM z kanoniczną funkcją łączącą, kara ta jest w przybliżeniu równa $2(p+1)$, co prowadzi bezpośrednio do wzoru na AIC.

***

## Estymacja Parametru Dyspersji

W niektórych rozkładach z rodziny ED, takich jak rozkład normalny, Gamma czy odwrotny Gaussa, występuje nieznany **parametr dyspersji $\phi$**, który również wymaga estymacji.

### Procedura Estymacji

Kluczową cechą Uogólnionych Modeli Liniowych (GLM) jest to, że równania estymacyjne dla głównych współczynników regresji $\beta$ **nie zależą od wartości parametru dyspersji $\phi$**. Oznacza to, że estymacja może przebiegać dwuetapowo:
1.  Najpierw estymuje się współczynniki $\beta$ za pomocą algorytmu IRLS.
2.  Następnie, po uzyskaniu estymatorów $\hat{\beta}$ i dopasowanych wartości $\hat{\mu}_i$, estymuje się parametr $\phi$.

### Metoda Momentów

Chociaż parametr $\phi$ można estymować metodą największej wiarygodności, w praktyce znacznie częściej stosuje się prostszy **estymator oparty na metodzie momentów**. Podejście to wykorzystuje **statystykę chi-kwadrat Pearsona ($X^2$)**, która mierzy sumę kwadratów zważonych reszt.

Statystyka $X^2$ jest zdefiniowana jako:

$$X^2 = \sum_{i=1}^{n} \frac{(y_i - \hat{\mu}_i)^2}{V(\hat{\mu}_i)/\nu_i}$$

gdzie $y_i$ to obserwacje, $\hat{\mu}_i$ to dopasowane wartości oczekiwane, $V(\hat{\mu}_i)$ to funkcja wariancji, a $\nu_i$ to wagi.

Ponieważ dla dużych prób statystyka $X^2/\phi$ ma w przybliżeniu rozkład chi-kwadrat z $n - p - 1$ stopniami swobody (gdzie $n$ to liczba obserwacji, a $p+1$ to liczba parametrów $\beta$), jej wartość oczekiwana jest bliska $n-p-1$. To prowadzi do następującego estymatora dla $\phi$:

$$\hat{\phi} = \frac{X^2}{n - p - 1}$$

Estymator ten jest prosty do obliczenia i w niektórych przypadkach oferuje większą stabilność numeryczną niż estymator największej wiarygodności.

### Alternatywny Estymator Oparty na Dewiancji

Alternatywnie, do estymacji $\phi$ można wykorzystać **dewiancję resztową ($D$)**. Ponieważ dewiancja skalowana ($D/\phi$) również ma w przybliżeniu rozkład chi-kwadrat, estymator parametru dyspersji można zdefiniować jako:

$$\hat{\phi} = \frac{D}{n - p - 1}$$

Obie metody są powszechnie stosowane w praktyce do estymacji parametru dyspersji w modelach GLM.

***

## Rozkład z Próby dla Estymowanych Współczynników

Ta sekcja wyjaśnia, jak ocenić niepewność estymowanych współczynników regresji $\beta$ w Uogólnionych Modelach Liniowych (GLM). Ponieważ estymatory są wynikiem losowej próby danych, same są zmiennymi losowymi i posiadają swój własny rozkład, zwany **rozkładem z próby (*sampling distribution*)**.

### Asymptotyczna Normalność Estymatorów GLM

Najważniejszą właściwością estymatorów największej wiarygodności (MLE) w GLM, przy założeniu dużej próby, jest ich **asymptotyczna normalność**. Oznacza to, że rozkład z próby wektora estymowanych współczynników $\hat{\beta}$ można przybliżyć za pomocą wielowymiarowego rozkładu normalnego:

$$\hat{\beta} \approx \text{Nor}\left(\beta, \hat{\Sigma}(\hat{\beta})\right)$$

**Macierz wariancji-kowariancji** estymatora, $\hat{\Sigma}(\hat{\beta})$, jest kluczowa do oceny niepewności. Można ją oszacować na podstawie ostatniego kroku algorytmu IRLS:

$$\hat{\Sigma}(\hat{\beta}) = \hat{\phi} (X^T \tilde{W} X)^{-1}$$

gdzie:
* $\hat{\phi}$ to estymator parametru dyspersji (równy 1 np. dla rozkładu Poissona).
* $\tilde{W}$ to diagonalna macierz wag roboczych z ostatniej iteracji algorytmu IRLS.

**Błędy standardowe** poszczególnych estymatorów $\hat{\beta}_j$ są pierwiastkami kwadratowymi z elementów na diagonali tej macierzy.

### Wnioskowanie Statystyczne o Parametrach

Dzięki asymptotycznej normalności można konstruować przedziały ufności i testować hipotezy statystyczne.

#### Przedziały Ufności Walda

Przedział ufności na poziomie $1-\alpha$ dla pojedynczego współczynnika $\beta_j$ jest oparty na teście Walda i ma postać:

$$[\hat{\beta}_j - z_{\alpha/2} \cdot SE(\hat{\beta}_j), \quad \hat{\beta}_j + z_{\alpha/2} \cdot SE(\hat{\beta}_j)]$$

gdzie $SE(\hat{\beta}_j)$ to błąd standardowy estymatora. Przedział ten określa zakres wartości, w którym z zadanym prawdopodobieństwem znajduje się prawdziwa, nieznana wartość parametru $\beta_j$.

#### Testowanie Hipotez

1.  **Test Walda (dla pojedynczego współczynnika)**: Służy do testowania hipotezy, takiej jak $H_0: \beta_j = 0$. Statystyka testowa:

    $$z = \frac{\hat{\beta}_j}{SE(\hat{\beta}_j)}$$

    ma w przybliżeniu standardowy rozkład normalny. Oprogramowanie statystyczne zazwyczaj podaje **wartość p (*p-value*)** dla tego testu, która informuje o istotności statystycznej danego predyktora.

2. **Test Ilorazu Wiarygodności (dla modeli zagnieżdżonych)**: Służy do porównywania dwóch modeli zagnieżdżonych (gdzie model prostszy jest szczególnym przypadkiem modelu bardziej złożonego). Statystyka testowa opiera się na różnicy w dewiancjach obu modeli:

    $$\Delta = D_0 - D_1$$

    gdzie $D_0$ i $D_1$ to dewiancje odpowiednio modelu prostszego i bardziej złożonego. Statystyka ta ma w przybliżeniu rozkład **chi-kwadrat** ($\chi^2$) z liczbą stopni swobody równą różnicy w liczbie parametrów obu modeli. Jeśli w modelu występuje parametr dyspersji, zamiast testu chi-kwadrat stosuje się **test F**.

### Diagnostyka Modelu: Współczynnik Inflacji Wariancji (VIF)

**Współliniowość** (silna korelacja między predyktorami) jest poważnym problemem w modelach regresji, ponieważ prowadzi do "nadmuchiwania" wariancji estymatorów, czyniąc je niestabilnymi i trudnymi do interpretacji.

Do diagnozowania tego problemu służy **Współczynnik Inflacji Wariancji (VIF)**. Jest on zdefiniowany dla każdego predyktora $j$ jako:

$$VIF_j = \frac{1}{1 - R_j^2}$$

gdzie $R_j^2$ to współczynnik determinacji z regresji $j$-tego predyktora na wszystkie pozostałe.
* **Interpretacja**: VIF mierzy, o ile większa jest wariancja estymatora $\hat{\beta}_j$ z powodu jego współliniowości z innymi predyktorami.
* **Zasada praktyczna**: Wartość VIF **większa niż 10** jest powszechnie uznawana za sygnał poważnego problemu ze współliniowością.

***

## Miary Wpływu (*Influence Measures*)

Po dopasowaniu modelu GLM, ważne jest zidentyfikowanie **obserwacji wpływowych**, czyli takich punktów danych, których niewielka zmiana lub usunięcie mogłoby znacząco zmienić oszacowane parametry modelu. Ta sekcja przedstawia dwie główne metody oceny wpływu poszczególnych obserwacji.

### Miary Diagnostyczne Oparte na Macierzy Projekcji (*Hat Matrix*)

Jednym ze wskaźników potencjalnego wpływu obserwacji jest jej **dźwignia (*leverage*)**.

* **Definicja**: Wartości dźwigni, oznaczane jako $h_{ii}$, są elementami na diagonali **macierzy projekcji (*hat matrix*)**, która pochodzi z ostatniej iteracji algorytmu IRLS.
* **Interpretacja**: Wartość $h_{ii}$ mierzy, jak duży wpływ ma obserwowana wartość $y_i$ na swoją własną wartość dopasowaną $\hat{y}_i$. Wysoka wartość dźwigni oznacza, że obserwacja ma nietypowe wartości predyktorów (leży daleko od "centrum" danych) i przez to ma duży potencjał, by wpłynąć na dopasowanie modelu.
* **Identyfikacja punktów o wysokiej dźwigni**: Zazwyczaj za obserwacje o wysokiej dźwigni uważa się te, dla których $h_{ii}$ jest większe niż dwukrotność średniej wartości dźwigni, czyli $h_{ii} > 2(p+1)/n$, gdzie $n$ to liczba obserwacji, a $p+1$ to liczba parametrów.
* **Ograniczenie w GLM**: W przeciwieństwie do klasycznej regresji liniowej, w modelach GLM wartości dźwigni zależą nie tylko od predyktorów $x_i$, ale również od odpowiedzi $y_i$ (poprzez wagi w algorytmie IRLS), co nieco komplikuje ich interpretację.

### Estymatory "Leave-One-Out" i Odległość Cooka

Innym podejściem do mierzenia wpływu jest analiza tego, jak zmieniają się parametry modelu po usunięciu każdej obserwacji z osobna.

* **Estymatory "Leave-One-Out"**: Polega to na wielokrotnym dopasowywaniu modelu, za każdym razem pomijając jedną obserwację. Estymator uzyskany bez $i$-tej obserwacji oznaczany jest jako $\hat{\beta}_{(-i)}$.
* **Odległość Cooka (*Cook's Distance*)**: Jest to kluczowa miara, która agreguje wpływ usunięcia $i$-tej obserwacji na **wszystkie** współczynniki regresji. Mierzy ona "odległość" między wektorem parametrów oszacowanym na pełnym zbiorze danych ($\hat{\beta}$) a wektorem oszacowanym bez $i$-tej obserwacji ($\hat{\beta}_{(-i)}$).
* **Interpretacja**: Duża wartość odległości Cooka dla danej obserwacji sygnalizuje, że jest ona wysoce wpływowa i jej usunięcie znacząco zmieniłoby wyniki modelu.
* **Zastosowanie praktyczne**: Chociaż podejście "leave-one-out" jest obliczeniowo kosztowne dla dużych zbiorów danych (typowych w ubezpieczeniach), pozostaje ono użytecznym narzędziem diagnostycznym w przypadku mniejszych zbiorów, np. w analizie trójkątów rozwojowych w rezerwach szkodowych.

# Effective Statistical Learning Methods for Actuaries I

## **Rozdział 9: Modele Wartości Ekstremalnych**

### **9.1 Wprowadzenie**

Podobnie jak w innych dziedzinach wrażliwych na obserwacje ekstremalne, na przykład w hydrologii i klimatologii, standardowe techniki statystyczne zawodzą przy analizie dużych szkód znajdujących się daleko w ogonie rozkładu ciężkości szkód. Dzieje się tak, ponieważ aktuariusz chce wnioskować o ekstremalnym zachowaniu rozkładów szkód, czyli w obszarze próby, w którym jest bardzo mało punktów danych, jeśli w ogóle.

Teoria Wartości Ekstremalnych (w skrócie **EVT**), wraz z modelem „nadwyżek ponad próg” oraz Uogólnionym Rozkładem Pareto, oferuje zunifikowane podejście do modelowania ogona rozkładu szkód. Metoda ta nie opiera się wyłącznie na dostępnych danych, ale zawiera probabilistyczny argument dotyczący zachowania ekstremalnych wartości z próby, co pozwala na ekstrapolację poza zakres danych, czyli w obszary, w których w ogóle nie ma obserwacji.

Omówmy krótko typowe sytuacje, w których aktuariusze zajmują się wartościami ekstremalnymi. W ubezpieczeniach odpowiedzialności cywilnej aktuariusze często napotykają trudności podczas analizy ciężkości szkód, ponieważ:

* występuje ograniczona liczba obserwacji, jako że tylko polisy, z których zgłoszono szkody, dostarczają informacji o ich kosztach.
* likwidacja szkody może trwać długo, przez co ostateczny koszt szkody jest w tym okresie nieznany firmie.
* kwoty wypłacane przez firmę w dużej mierze zależą od cech charakterystycznych strony trzeciej, które są nieznane w momencie obliczania składki.

Co więcej, kilka dużych szkód w portfelu często stanowi znaczną część świadczeń ubezpieczeniowych wypłacanych przez firmę. Te ekstremalne zdarzenia są zatem przedmiotem szczególnego zainteresowania aktuariuszy. Stanowią one również materiał statystyczny do:

* wyceny umów reasekuracyjnych, takich jak traktaty **reasekuracji nadwyżki szkody** (w ramach których reasekurator musi zapłacić za nadwyżkę szkody ponad ustalony próg, zwany franszyzą redukcyjną).
* szacowania wysokich kwantyli (nazywanych również **Wartością Narażoną na Ryzyko** w zarządzaniu ryzykiem finansowym).
* wyznaczania **prawdopodobnej szkody maksymalnej** (w skrócie PML), która ma być używana jako robocza górna granica wielkości szkody w obliczaniu miar ryzyka.

Gdy głównym przedmiotem zainteresowania jest ogon rozkładu ciężkości szkód, kluczowe jest posiadanie dobrego modelu dla największych szkód. Rozkłady, które zapewniają dobre ogólne dopasowanie, takie jak rozkłady z rodziny wykładniczej (ED), mogą być szczególnie nieodpowiednie do modelowania ogonów. Teoria Wartości Ekstremalnych (EVT) koncentruje się właśnie na ogonach, opierając się na solidnych podstawach teoretycznych. Zasada leżąca u podstaw EVT polega na przeprowadzeniu analizy w oparciu o tę część próby, która niesie informację o zachowaniu ekstremalnym, czyli wyłącznie na największych wartościach z próby. W tym rozdziale przypomniano podstawy EVT, przydatne w zastosowaniach aktuarialnych.

***

## **9.5 Podejście POT (Peak Over Threshold)**

### **9.5.1 Zasada**

Tradycyjne podejście do EVT opiera się na granicznych rozkładach wartości ekstremalnych. W tym ujęciu model dla ekstremalnych strat bazuje na możliwej parametrycznej formie granicznego rozkładu maksimów. Bardziej elastyczny model jest znany jako metoda „Peak Over Threshold” (w skrócie POT). To podejście jest alternatywą dla analizy maksimów w badaniu zachowań ekstremalnych. Zasadniczo, POT analizuje serię nadwyżek ponad wysoki próg $u$. 

Okazuje się, że Uogólniony Rozkład Pareto stanowi dla aktuariusza przybliżenie rozkładu nadwyżek *Fu* ponad dostatecznie wysokie progi. 

**Twierdzenie 9.5.1 (Twierdzenie Pickandsa-Balkemy-de Haana)**
*Twierdzenie Fishera-Tippetta zachodzi z $H_\xi$ wtedy i tylko wtedy, gdy możemy znaleźć dodatnią funkcję $\tau(u)$ taką, że*

$$ \lim_{u \to \omega} \sup_{0 \le y \le \omega - u} |F_u(y) - G_{\xi, \tau(u)}(y)| = 0. $$

Twierdzenie 9.5.1 wskazuje, że rozkład $GPar(\xi, \tau)$ stanowi dobre przybliżenie rozkładu nadwyżek ponad dostatecznie wysokie progi $u$. W praktyce, dla pewnej funkcji $\tau(u)$ i pewnego indeksu Pareto $\xi$ zależnego od $F$, możemy użyć przybliżenia

$$ F_u(y) \approx 1 - G_{\xi; \tau(u)}(y), \quad y \ge 0, $$

pod warunkiem, że $u$ jest wystarczająco duże. Otrzymujemy wtedy użyteczne przybliżenie

$$ \bar{F}(u + z) \approx \bar{F}(u) [1 - G_{\hat{\xi}; \hat{\tau}}(z)] $$

które wydaje się być dokładne dla wystarczająco dużego progu $u$ i dowolnego $z \ge 0$. Wzory na ogon rozkładu oparte na Uogólnionym Rozkładzie Pareto, takie jak te wyprowadzone w następnej sekcji, okazują się więc użyteczne, gdy aktuariusz ma do czynienia z ekstremalnymi wartościami zmiennej odpowiedzi. 

---
### **9.5.2 Wzory na Ogon Rozkładu**

Jeśli ogon rozkładu Y jest Uogólnionym Rozkładem Pareto, aktuariusz jest w stanie wyprowadzić szereg użytecznych tożsamości, jak pokazano poniżej. Jeśli $F_u(y) = G_{\xi, \tau}(y)$ dla $0 \le y < \omega − u$, jak sugeruje twierdzenie Pickandsa-Balkemy-de Haana, to dla $y \ge u$,

$$ P[Y > y] = P[Y > u]P[Y > y|Y > u] \quad \text{dla } x \ge u $$

$$ = \bar{F}(u)P[Y - u > y - u|Y > u] $$

$$ = \bar{F}(u)\bar{F}_u(y - u) $$

$$ = \bar{F}(u) \left( 1 + \xi \frac{y - u}{\tau} \right)^{-1/\xi}. $$

Ten wzór jest użyteczny do obliczania wysokich kwantyli zmiennej odpowiedzi. Funkcja kwantylowa rozkładu $GPar(\xi, \tau)$ jest dana wzorem

$$ G^{-1}_{\xi;\tau}(p) = \frac{\tau}{\xi} \left[ (1 - p)^{-\xi} - 1 \right], \quad 0 < p < 1. $$

Teraz, dla $p \ge F(u)$, kwantyl $Y$ na poziomie prawdopodobieństwa $p$ (często nazywany Wartością Narażoną na Ryzyko w zarządzaniu ryzykiem) otrzymuje się jako rozwiązanie $z$ równania

$$ 1 - p = \bar{F}(u) \left( 1 + \xi \frac{z - u}{\tau} \right)^{-1/\xi}. $$

To daje

$$ F^{-1}_Y(p) = u + \frac{\tau}{\xi} \left[ \left( \frac{1 - p}{\bar{F}(u)} \right)^{-\xi} - 1 \right]. $$

Średnia wartość odpowiedzi, gdy Wartość Narażona na Ryzyko została przekroczona, jest również bardzo użytecznym wskaźnikiem w zarządzaniu ryzykiem, do kwantyfikacji strat w niekorzystnych scenariuszach. Wskaźnik ten jest znany jako warunkowa wartość oczekiwana ogona. Jeśli $\xi < 1$, to dla $p \ge F(u)$, warunkowa wartość oczekiwana ogona jest dana wzorem

$$ E[Y | Y > F^{-1}_Y(p)] = F^{-1}_Y(p) + E[Y - F^{-1}_Y(p) | Y > F^{-1}_Y(p)] $$

$$ = F^{-1}_Y(p) + E[Y - u - (F^{-1}_Y(p) - u) | Y - u > F^{-1}_Y(p) - u] $$

$$ = F^{-1}_Y(p) + \frac{\tau + \xi(F^{-1}_Y(p) - u)}{1 - \xi} $$

$$ = \frac{F^{-1}_Y(p)}{1 - \xi} + \frac{\tau - \xi u}{1 - \xi} $$

gdzie $F^{-1}_Y(p)$ zostało wyprowadzone we wcześniejszym wzorze. 

---
### **9.5.3 Estymatory Ogona**

Twierdzenie Pickandsa-Balkemy-de Haana pokazuje, że (pod warunkiem, że $u$ jest wystarczająco duże) potencjalnym estymatorem dla rozkładu nadwyżki szkody $Fu(x)$ jest $G_{\hat{\xi};\hat{\tau}}(x)$. Wybór odpowiedniego progu $u$ zostanie omówiony w następnych sekcjach. Zatem, $G_{\hat{\xi};\hat{\tau}}(x)$ przybliża warunkowy rozkład strat, pod warunkiem, że przekraczają one próg $u$. Estymatory kwantyli wyprowadzone z tej krzywej są warunkowymi estymatorami kwantyli, które wskazują na skalę strat, jakich można doświadczyć, gdyby próg $u$ został przekroczony. Gdy interesują nas estymatory bezwarunkowych kwantyli, konieczne jest powiązanie bezwarunkowej dystrybuanty $F$ z $G_{\hat{\xi};\hat{\tau}}$ poprzez $F_u$. 

Oznaczmy liczbę szkód powyżej progu $u$ jako

$$ N_u = \sum_{i=1}^n I[Y_i > u] \sim \text{Bin}(n, \bar{F}(u)). $$

Pod warunkiem, że mamy wystarczająco dużą próbę, możemy dokładnie oszacować $F(u)$ za pomocą jego empirycznego odpowiednika $N_u/n$. Dla $x > u$, $F(x) = F(u)F_u(x − u)$, więc możemy oszacować $F(x)$ za pomocą

$$ \hat{\bar{F}}(x) = \frac{N_u}{n} \left( 1 + \hat{\xi} \frac{x - u}{\hat{\tau}} \right)^{-1/\hat{\xi}}. $$

Wysokie kwantyle zawierają użyteczne informacje dla ubezpieczycieli na temat rozkładu kwot szkód. Zazwyczaj kwantyle można oszacować za pomocą ich empirycznych odpowiedników, ale gdy interesują nas bardzo wysokie kwantyle, to podejście przestaje być ważne, ponieważ estymacja oparta na niewielkiej liczbie dużych obserwacji byłaby bardzo nieprecyzyjna. Twierdzenie Pickandsa-Balkemy-de Haana sugeruje następujące estymatory. Dla $p \ge F(u)$, kwantyl na poziomie prawdopodobieństwa $p$ można oszacować z

$$ \hat{F}^{-1}(p) = u + \frac{\hat{\tau}}{\hat{\xi}} \left[ \left( \frac{n(1 - p)}{N_u} \right)^{-\hat{\xi}} - 1 \right]. $$

Jeśli $\xi < 1$, to warunkową wartość oczekiwaną ogona można oszacować z

$$ \hat{E}[Y | Y > F^{-1}(p)] = \frac{\hat{F}^{-1}(p)}{1 - \hat{\xi}} + \frac{\hat{\tau} - \hat{\xi}u}{1 - \hat{\xi}} $$

gdzie wstawiamy wyżej wymienione wyrażenie dla $\hat{F}^{-1}(p)$. 

---
### **9.5.4 Zastosowania do Pozostałego Czasu Życia**

Analiza pozostałego czasu życia w starszym wieku jest zgodna z metodą POT, gdzie próg $u$ odpowiada pewnemu zaawansowanemu wiekowi $x$. Przenosząc to na grunt ubezpieczeń na życie, pozostały czas życia $T − x$ w wieku $x$, pod warunkiem $T > x$, ma rozkład zgodny z

$$ s \to {}_s q_x = P[T - x \le s | T > x]. $$

Może się zdarzyć, że dla wysokich osiągniętych wieków $x$, ten warunkowy rozkład prawdopodobieństwa stabilizuje się po normalizacji, tzn. istnieje dodatnia funkcja $\tau(\cdot)$ taka, że

$$ \lim_{x \to \omega} P\left[\frac{T - x}{\tau(x)} > s \bigg| T > x\right] = 1 - G(s), \quad s > 0, $$

gdzie $G$ jest niezdegenerowaną dystrybuantą. Tylko ograniczona klasa dystrybuant jest dopuszczalna w (9.4), mianowicie Uogólnione Rozkłady Pareto $G_{\xi,\tau}$. Gdy $\xi = 0$, pozostały czas życia w starszym wieku staje się ostatecznie ujemnie wykładniczy, tak że siły wymierania stabilizują się. 

Dla pewnej odpowiedniej funkcji $\tau(\cdot)$, przybliżenie

$$ {}_s q_x \approx G_{\xi; \tau(x)}(s) \quad \text{dla } s \ge 0 $$

zachodzi dla wystarczająco dużego $x$. Przybliżenie (9.5) jest uzasadnione twierdzeniem Pickandsa-Balkemy-de Haana. W świetle (9.5) pozostały czas życia w wieku $x$ można traktować jako losową próbę z Uogólnionego Rozkładu Pareto, pod warunkiem że $x$ jest wystarczająco duże. 

Jeśli $\xi < 0$, tak że $\omega < \infty$, to odpowiednia transformacja indeksu wartości ekstremalnej $\xi$ ma intuicyjną interpretację. Przypomnijmy, że funkcja średniej nadwyżki

$$ e(x) = E[T - x | T > x] $$

pokrywa się z oczekiwanym dalszym trwaniem życia w wieku $x$, oznaczanym jako $ex$. Można wykazać, że dla $\xi < 0$, (9.1) jest równoważne z

$$ \lim_{x \to \omega} E\left[\frac{T - x}{\omega - x} \bigg| T > x\right] = \lim_{x \to \omega} \frac{e(x)}{\omega - x} = -\frac{\xi}{1 - \xi} = \alpha $$

Parametr $\alpha = \alpha(\xi)$ jest określany jako parametr perseweracji. Intuicyjna interpretacja parametru perseweracji jest następująca. Rozważmy osobę, która jest wciąż żywa w pewnym zaawansowanym wieku $x$. Stosunek $(T - x) / (\omega - x)$ reprezentuje procent faktycznego pozostałego czasu życia $T − x$ do maksymalnego pozostałego czasu życia $\omega − x$. Ten procent stabilizuje się średnio, gdy $x \to \omega$ i zbiega do $\alpha$, które zatem jawi się jako oczekiwany procent maksymalnego możliwego pozostałego czasu życia efektywnie wykorzystanego przez osobę. 

Pod warunkiem, że wybrany próg wiekowy $x^*$ jest wystarczająco duży, potencjalnym estymatorem dla rozkładu dalszego trwania życia ${}_s q_{x^*}$ jest $G_{\hat{\xi};\hat{\tau}}(s)$. Estymatory kwantyli wyprowadzone z tej krzywej są warunkowymi estymatorami kwantyli, które wskazują na potencjalne przeżycie ponad próg wiekowy $x^*$, gdy jest on osiągnięty. Jeśli $\hat{\xi} < 0$, to osoby mają ograniczony dalszy czas życia z oszacowanym wiekiem granicznym

$$ \hat{\omega} = x^* - \frac{\hat{\tau}}{\hat{\xi}}. $$

Gdy interesują nas estymatory kwantyli bezwarunkowych, możemy powiązać bezwarunkową dystrybuantę ${}_x q_0$ z $G_{\hat{\xi};\hat{\tau}}$ dla

$$ x^* < x \le \hat{\omega} = x^* - \frac{\hat{\tau}}{\hat{\xi}}, $$

poprzez

$$ {}_x q_0 = 1 - {}_x p_0 $$

$$ = 1 - {}_{x^*}p_0 \times {}_{x-x^*}p_{x^*} $$

$$ \approx 1 - {}_{x^*}p_0 [1 - G_{\hat{\xi};\hat{\tau}}(x - x^*)]. $$

Wysokie kwantyle odpowiadają wtedy rozwiązaniom $z$ równań

$$ {}_z q_0 = 1 - \epsilon $$

gdzie przybliżenie właśnie wyprowadzone jest użyteczne dla małych poziomów prawdopodobieństwa $\epsilon$. 

Pod warunkiem, że wielkość próby jest wystarczająco duża, możemy oszacować ${}_{x^*}p_0$ za pomocą jego empirycznego odpowiednika. W przykładzie rozważanym w tym rozdziale zaczynamy od osób w wieku 95 lat. Prawdopodobieństwo przeżycia do wieku $x$ takiego, że $x^* - \hat{\tau}/\hat{\xi} \ge x > x^*$, można wtedy oszacować przez

$$ {}_x \hat{p}_{95} = \frac{L_{x^*}}{L_{95}} [1 - G_{\hat{\xi};\hat{\tau}}(x - x^*)] $$

gdzie $L_{x^*}$ i $L_{95}$ to odpowiednio liczba osób, które przeżyły do wieku progowego $x^*$ i do wieku 95 lat (tj. całkowita liczba osób objętych badaniem dla danej kohorty). Wysokie kwantyle są wtedy szacowane jako

$$ \hat{F}^{-1}(\epsilon) = x^* + \frac{\hat{\tau}}{\hat{\xi}} \left[ \left( \frac{L_{95}}{L_{x^*}}(1 - \epsilon) \right)^{-\hat{\xi}} - 1 \right]. $$

Ponadto, dla wieków $x$ takich, że $x^* - \hat{\tau}/\hat{\xi} \ge x > x^*$, siłę wymierania można uzyskać ze wzoru Uogólnionego Rozkładu Pareto

$$ \hat{\mu}_x = \frac{1}{\hat{\tau} + \hat{\xi}(x - x^*)}. $$

Należy zauważyć, że $\hat{\mu}_x$ dąży do $\infty$, gdy wiek $x$ zbliża się do skończonego punktu końcowego $\hat{\omega}$, ponieważ żadna osoba nie może przeżyć poza wiek $\omega$. 

---
### **9.5.5 Wybór Progu dla Uogólnionego Rozkładu Pareto**

#### **9.5.5.1 Zasada**
Wybór odpowiedniego progu $u$, powyżej którego przybliżenie Uogólnionym Rozkładem Pareto ma zastosowanie, jest z pewnością bardzo trudnym zadaniem. W tej sekcji przedstawiamy czytelnikowi pewne ogólne zasady w tym zakresie, odsyłając do literatury po szczegółowe podejścia stosowane w konkretnych sytuacjach. Często techniki wyboru progu dostarczają jedynie zakresu rozsądnych wartości, dlatego zaleca się jednoczesne stosowanie kilku z nich w celu uzyskania bardziej wiarygodnych wyników. 

Przy wyborze optymalnego progu $u$, powyżej którego przybliżenie Uogólnionym Rozkładem Pareto jest słuszne dla rozkładu nadwyżek, należy wziąć pod uwagę dwa czynniki: 

* Zbyt duża wartość $u$ skutkuje małą liczbą nadwyżek, a w konsekwencji niestabilnymi estymatami górnych kwantyli. Aktuariusz traci również możliwość szacowania mniejszych kwantyli. 
* Zbyt mała wartość $u$ oznacza, że Uogólniony Rozkład Pareto nie jest właściwy dla umiarkowanych obserwacji, co prowadzi do obciążonych estymat kwantyli. Obciążenie to może być znaczne, ponieważ umiarkowane obserwacje zazwyczaj stanowią największą część próby. 

Naszym celem jest zatem określenie minimalnej wartości progu, powyżej którego Uogólniony Rozkład Pareto staje się rozsądnym przybliżeniem ogona rozkładu będącego przedmiotem badania. 

Wiemy, że Uogólniony Rozkład Pareto posiada wygodną właściwość stabilności progowej, która zapewnia, że

$$ Y \sim \text{GPar}(\xi, \tau) \implies P[Y - u > t | Y > u] = 1 - G_{\xi, \tau + \xi u}(t) $$

z tym samym parametrem indeksu $\xi$, dla dowolnego $u > 0$. Mówiąc prościej, jeśli $Y$ ma Uogólniony Rozkład Pareto, to nadwyżki $Y$ ponad dowolny próg nadal mają Uogólniony Rozkład Pareto. Ta właściwość jest wykorzystywana przez większość procedur wyboru optymalnego progu $u$, powyżej którego przybliżenie Uogólnionym Rozkładem Pareto ma zastosowanie. 

Właściwość stabilności (9.7) Uogólnionego Rozkładu Pareto zapewnia, że wykres estymatorów $\hat{\xi}$ obliczonych przy rosnących progach ujawnia estymacje, które stabilizują się, gdy osiągnięty zostanie najmniejszy próg, dla którego zachowanie Uogólnionego Rozkładu Pareto jest słuszne. Można to sprawdzić graficznie i pozwala to aktuariuszowi określić najmniejszy próg $u$, powyżej którego Uogólniony Rozkład Pareto stanowi dobre przybliżenie ogona. 

#### **9.5.5.2 Zastosowanie do Ciężkości Szkód**
Zgodnie z praktyką rynkową, koncentrujemy się na ciężkościach szkód przekraczających 1 000 000 franków belgijskich (około 25 000 €), co odpowiada 13,83-krotności obserwowanej średniej ciężkości szkody. Kwantyl 97,5% rozkładu Gamma o średniej i wariancji odpowiadających ich empirycznym odpowiednikom wynosi 360 481,7 franków belgijskich, podczas gdy kwantyle 99% i 99,5% wynoszą odpowiednio 1 937 007 i 4 004 094 franków belgijskich. Odpowiednie wartości dla rozkładu Odwrotnego Gaussa to 409 671,3 franków belgijskich, 1 403 344 franków belgijskich i 2 952 146 franków belgijskich. Widzimy więc, że rozkłady ED używane do modelowania umiarkowanych strat znacznie wykraczają poza najniższy rozważany próg, jeśli analiza POT rozpoczyna się od 1 000 000 franków belgijskich. 

Wykres indeksu Pareto dla ciężkości szkód w ubezpieczeniach komunikacyjnych przedstawiono na Rys. 9.7. Został on wygenerowany za pomocą funkcji `tcplot` z pakietu R `POT`. Widzimy tam, że oszacowane indeksy wydają się być względnie stabilne, co jest zgodne z twierdzeniem Pickandsa-Balkemy-de Haana. Przedziały ufności są jednak dość szerokie. Ogólnie rzecz biorąc, wykres ten nie dostarcza aktuariuszowi wielu wskazówek co do wyboru progu. 

Wykres Gertensgarbe'a to kolejne narzędzie graficzne, które można wykorzystać do oszacowania progu definiującego duże straty. Opiera się on na założeniu, że optymalny próg można znaleźć jako punkt zwrotny w serii odstępów między uporządkowanymi kosztami szkód. Kluczową ideą jest to, że można rozsądnie oczekiwać, iż zachowanie różnic odpowiadających obserwacjom ekstremalnym będzie inne niż to odpowiadające obserwacjom nieekstremalnym. Zatem powinien istnieć punkt zwrotny, jeśli analiza POT ma zastosowanie, a ten punkt zwrotny można zidentyfikować za pomocą sekwencyjnej wersji testu Manna-Kendalla jako punkt przecięcia znormalizowanych statystyk rang progresywnych i retrogradywnych. Jest on zaimplementowany w funkcji `ggplot` pakietu R `tea`. Dokładniej, biorąc pod uwagę serię różnic $\Delta_i = y_{(i)} − y_{(i−1)}$, punkt początkowy regionu ekstremalnego zostanie wykryty jako punkt zwrotny serii $\{\Delta_i, i = 2, 3,..., n\}$. W tym teście określa się dwie znormalizowane serie $U_p$ i $U_r$, najpierw na podstawie serii $\Delta_1, \Delta_2,...$ a następnie na podstawie serii różnic od końca do początku, $\Delta_n, \Delta_{n−1},...$, zamiast od początku do końca. Punkt przecięcia tych dwóch serii określa kandydata na punkt zwrotny, który będzie istotny, jeśli przekroczy wysoki percentyl rozkładu normalnego. 

Wykres Gertensgarbe'a przedstawiono na Rys. 9.8. Wskazuje on próg 2 471 312 franków belgijskich (co oznacza, że 29 szkód kwalifikuje się jako duże). Wartość $p$-value testu Manna-Kendalla wynosi $1.299018 \times 10^{−4}$, więc wynik jest istotny. Jest to zgodne z wnioskiem wyciągniętym z wykresu indeksu Pareto przedstawionego na Rys. 9.7, dlatego wybieramy próg $u = 2 471 312$ dla ciężkości szkód w ubezpieczeniach komunikacyjnych. 

Teraz, gdy wartość progu została wybrana, istnieje kilka metod szacowania odpowiednich parametrów Uogólnionego Rozkładu Pareto. Wymienić można metodę największej wiarygodności (z karą lub bez), (nieobciążone) ważone momenty probabilistyczne, momenty, estymatory Pickandsa, minimalnej dywergencji potęgowej gęstości, mediany i maksymalnej dobroci dopasowania, wszystkie dostępne w funkcji `fitgpd` pakietu R `POT`. Tutaj przyjmujemy podejście największej wiarygodności. Aby dopasować model Uogólnionego Rozkładu Pareto do nadwyżek ponad próg $u$, maksymalizujemy funkcję wiarygodności

$$ \mathcal{L}(\xi, \tau) = \prod_{i|y_i > u} \frac{1}{\tau} \left( 1 + \frac{\xi}{\tau}(y_i - u) \right)^{-1/\xi - 1} $$

lub odpowiadającą jej funkcję log-wiarygodności

$$ L(\xi, \tau) = \ln \mathcal{L}(\xi, \tau) = -N_u \ln \tau - \left( 1 + \frac{1}{\xi} \right) \sum_{i|y_i > u} \ln \left( 1 + \frac{\xi}{\tau}(y_i - u) \right) $$

gdzie $N_u = \#{y_i|y_i > u}$ jest liczbą dużych szkód zaobserwowanych w portfelu, jak wprowadzono wcześniej. 

Ten problem optymalizacyjny wymaga algorytmów numerycznych i odpowiednich wartości początkowych dla parametrów $\xi$ i $\tau$. Średnia i wariancja Uogólnionego Rozkładu Pareto wynoszą odpowiednio $\tau/(1 - \xi)$ pod warunkiem $\xi < 1$, oraz $\tau^2/((1 - \xi)^2(1 - 2\xi))$ pod warunkiem $ξ\xi < 1/2$. Wartości początkowe metodą momentów to

$$ \hat{\xi}_0 = \frac{1}{2} \left( 1 - \frac{\bar{y}^2}{s^2} \right) \quad \text{i} \quad \hat{\tau}_0 = \frac{1}{2} \bar{y} \left( \frac{\bar{y}^2}{s^2} + 1 \right), $$

gdzie $\bar{y}$ i $s^2$ są średnią i wariancją z próby. Można również wykorzystać wartości $\tau$ i $\xi$ pochodzące z dopasowania liniowego do prawej części wykresu empirycznej funkcji średniej nadwyżki. 

Przy progu ustalonym na 2 471 312 franków belgijskich, otrzymujemy $\hat{\xi} = 0,2718819$, co oznacza, że mamy do czynienia z rozkładem o grubym ogonie. Odpowiadające mu $\tau = 7 655 438$. Należy zauważyć, że $\hat{\xi}$ rzeczywiście odpowiada plateau widocznemu na wykresie indeksu Pareto przedstawionym na Rys. 9.7. 

#### **9.5.5.3 Zastosowanie w Ubezpieczeniach na Życie**
Przejdźmy teraz do modelowania skrajnych czasów życia. Wykresy indeksu Pareto dla czasów życia przedstawiono na Rys. 9.9, oddzielnie dla mężczyzn i kobiet. Narzędzia graficzne są trudniejsze do interpretacji w porównaniu z ciężkościami szkód. Odsyłamy czytelnika do Gbari i in. (2017a) w celu określenia progu wiekowego $x^*$, takiego że przybliżenie (9.5) jest wystarczająco dokładne dla $x \ge x^*$, za pomocą kilku zautomatyzowanych procedur. Zgodnie z ich wnioskami, możemy ustawić $x^*$ na 98.89 dla mężczyzn i 100.89 dla kobiet. Wartości te wydają się rozsądne, biorąc pod uwagę wykresy indeksu Pareto przedstawione na Rys. 9.9. Estymaty największej wiarygodności parametrów Uogólnionego Rozkładu Pareto można znaleźć w Tabeli 9.4 wraz z błędami standardowymi. 

Oszacowany wiek graniczny ω jest dany wzorem
$$ \hat{\omega} = x^* - \frac{\hat{\tau}}{\hat{\xi}} = \begin{cases} 114,82 & \text{dla mężczyzn,} \\ 122,73 & \text{dla kobiet.} \end{cases} $$

Populacja kobiet ma najwyższy oszacowany wiek graniczny. Estymacje są zgodne z najwyższymi zaobserwowanymi wiekami zgonu 112.58 dla kobiet i 111.47 dla mężczyzn dla rozważanych kohort urodzonych w Belgii. Wyniki te są spójne z maksymalnymi obserwowanymi na świecie wiekami zgonu. Co ciekawe, uzyskany wiek graniczny dla kobiet jest bliski rekordowi Jeanne Calment wynoszącemu 122.42 (122 lata i 164 dni, urodzona w Arles we Francji 21 lutego 1875 r., zmarła w tym samym miejscu 4 sierpnia 1997 r.). 

Każda miara dobroci dopasowania może być użyta w celu sprawdzenia, czy dane są zgodne z Uogólnionym Rozkładem Pareto powyżej wybranego progu. W tym celu często używa się wykresu kwantylowo-kwantylowego (QQ-plot) dla Uogólnionego Rozkładu Pareto. Na tym wykresie kwantyle empiryczne są przedstawione w odniesieniu do oszacowanych kwantyli Uogólnionego Rozkładu Pareto. Jeśli Uogólniony Rozkład Pareto skutecznie dopasowuje się do rozważanych danych, wykreślone pary powinny znajdować się blisko linii o nachyleniu 45 stopni. Funkcja `qqgpd` z pakietu R `tea` może być użyta do wykreślenia obserwacji empirycznych powyżej danego progu w odniesieniu do teoretycznych kwantyli Uogólnionego Rozkładu Pareto. Wykresy QQ dla Uogólnionego Rozkładu Pareto dla skrajnych czasów życia przedstawiono na Rys. 9.10. Wyraźnie liniowy wzorzec na wykresie QQ potwierdza, że model Uogólnionego Rozkładu Pareto adekwatnie opisuje rozkład pozostałego czasu życia powyżej $x^*$. 

Na zakończenie tego zastosowania w ubezpieczeniach na życie, omówmy różnicę w stosunku do analiz przeprowadzonych na zagregowanych danych o śmiertelności. W demografii poziomy śmiertelności są zwykle oceniane na podstawie danych statystycznych zagregowanych według osiągniętego wieku, a nie indywidualnych wieków zgonu. Dzieje się tak zwłaszcza w przypadku danych dotyczących populacji ogólnej. Aktuariusz zna jedynie obserwowane liczby $L_x$ osób osiągających wiek $x$, odpowiadające im liczby zgonów $D_x = L_x − L_{x+1}$ oraz odpowiadającą im ekspozycję $E_x$ w tym wieku. Dostępne dane są zatem takie, jak przedstawiono w Tabeli 9.5. 

Model Uogólnionego Rozkładu Pareto można estymować na danych zagregowanych $(L_x, D_x), x \ge \lceil x^* \rceil$, gdzie $\lceil x^*\rceil$ jest najniższą liczbą całkowitą większą lub równą $x^*$. Biorąc pod uwagę wiek $x \ge x^*$, jednoroczne prawdopodobieństwa przeżycia uzyskuje się z przybliżenia (9.5), co daje

$$ p_x = p_x(\xi, \tau) = \left( 1 + \frac{\xi}{\tau + \xi(x - x^*)} \right)^{-1/\xi}. $$

Parametry Uogólnionego Rozkładu Pareto można oszacować w modelu warunkowym

$$D_x \sim Bin(L_x, q_x), \text{ gdzie } q_x = q_x(\xi, \tau) = 1 − p_x(\xi, \tau). $$ 

Dokładniej, maksymalizujemy funkcję log-wiarygodności rozkładu dwumianowego

$$ L(\xi, \tau) = \sum_{x \ge x^*} [L_x \ln p_x(\xi, \tau) + D_x \ln q_x(\xi, \tau)]. $$

To daje
$$ \hat{\xi} = \begin{cases} -0,131 & \text{z błędem standardowym 0,016 dla mężczyzn,} \\ -0,096 & \text{z błędem standardowym 0,015 dla kobiet} \end{cases} $$

oraz

$$ \hat{\omega} = \begin{cases} 114,90 & \text{dla mężczyzn,} \\ 122,13 & \text{dla kobiet,} \end{cases} $$

co jest zgodne z wartościami w (9.8) uzyskanymi przy użyciu indywidualnych wieków zgonu. 

Główną trudnością przy pracy z danymi zagregowanymi jest wybór odpowiedniego wieku progowego, powyżej którego zachowanie Uogólnionego Rozkładu Pareto staje się widoczne.