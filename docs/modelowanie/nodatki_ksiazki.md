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

1.  **Analiza na poziomie portfela**: Prognozuje się ogólne przyszłe koszty szkód i ustala całkowitą kwotę składki potrzebną dla całego portfela.
2.  **Analiza na poziomie indywidualnym**: Identyfikuje się profile ryzyka poszczególnych klientów, aby sprawiedliwie rozdzielić całkowitą składkę pomiędzy nich na podstawie ich względnej ryzykowności.

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

$$Var[Y]=E[Var[Y|X,X^{+}]]+E[Var[E[Y|X,X^{+}]|X]]+Var[E[Y|X]]$$

* **Solidarność losowa (zasada wzajemności)**: Pierwszy składnik, $E[Var[Y|X,X^{+}]]$, reprezentuje czystą losowość, której nie da się wyeliminować nawet przy doskonałej wiedzy o ryzyku. Jest to ryzyko pokrywane przez ubezpieczyciela zgodnie z zasadą wzajemności.
* **Solidarność subsydiowana**: Drugi składnik, $E[Var[E[Y|X,X^{+}]|X]]$, wynika z faktu, że ubezpieczyciel nie zna ukrytych czynników $X^{+}$. Oznacza to, że w obrębie tej samej klasy ryzyka (określonej przez $X$) klienci o niższym "prawdziwym" ryzyku subsydiują składki tych o wyższym ryzyku. Mimo to, globalna równowaga jest zachowana, ponieważ zachodzi równość $E[E[Y|X,X^{+}]|X]=E[Y|X]$.

### Wycena a Predykcja Strat

Celem taryfikacji ubezpieczeniowej nie jest przewidywanie faktycznej straty $Y$ dla danego klienta, ale jak najdokładniejsze oszacowanie **prawdziwej składki czystej**, czyli warunkowej wartości oczekiwanej $\mu(X)=E[Y|X]$.

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

Aby przejść od rozkładu normalnego do rodziny ED, autorzy przekształcają jego funkcję gęstości, aby wyizolować parametry średniej $\mu$ i wariancji $\sigma^2$:

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

## Bootstrap (Sekcja 3.7) 🔄

Bootstrap to metoda numeryczna, która pozwala ocenić dokładność estymatora (np. jego błąd standardowy lub przedział ufności), zwłaszcza gdy analityczne wzory są trudne lub niemożliwe do wyprowadzenia. Jest to technika oparta na symulacji komputerowej.

### Zasada Wtyczki (*Plug-in Principle*) i Procedura Bootstrap

Główną ideą bootstrapu jest **zasada wtyczki (*plug-in principle*)**. Ponieważ nie znamy prawdziwego rozkładu prawdopodobieństwa $F$, z którego pochodzi nasza próba, zastępujemy go jego najlepszym przybliżeniem, jakim dysponujemy – **empiryczną dystrybuantą** $\hat{F}_n$:

$$\hat{F}_n(x) = \frac{1}{n}\sum_{i=1}^{n} I[Y_i \le x]$$

Empiryczna dystrybuanta przypisuje każdej zaobserwowanej wartości $Y_i$ w próbie równe prawdopodobieństwo $\frac{1}{n}$.

Ponieważ analityczne obliczenia oparte na $\hat{F}_n$ są często zbyt skomplikowane, stosuje się symulację. Procedura bootstrap polega na wielokrotnym **losowaniu ze zwracaniem** z oryginalnej próby danych w celu utworzenia nowych, "bootstrapowych" prób danych.

1.  **Tworzenie prób bootstrapowych**: Z oryginalnego zbioru danych o rozmiarze $n$ losuje się (ze zwracaniem) $n$ obserwacji. Proces ten powtarza się $B$ razy (np. $B=10000$), tworząc $B$ nowych prób, z których każda ma rozmiar $n$.
2.  **Obliczanie statystyki**: Dla każdej z $B$ prób bootstrapowych oblicza się wartość interesującego nas estymatora (np. średniej, mediany, współczynnika regresji).
3.  **Ocena dokładności**: Otrzymujemy w ten sposób $B$ wartości estymatora. Rozkład tych wartości (rozkład bootstrapowy) służy do oceny dokładności. Na przykład błąd standardowy oryginalnego estymatora można przybliżyć przez odchylenie standardowe $B$ wartości bootstrapowych.

### Bootstrap Nieparametryczny a Parametryczny

* **Bootstrap nieparametryczny**: Jest to standardowe podejście opisane powyżej, gdzie losowanie odbywa się bezpośrednio z oryginalnych danych.
* **Bootstrap parametryczny**: W tym podejściu najpierw dopasowuje się do danych model parametryczny (np. rozkład Poissona z estymowanym parametrem $\hat{\lambda}$), a następnie losowanie nowych prób odbywa się z tego dopasowanego rozkładu, a nie z surowych danych.

Metoda bootstrap jest szeroko stosowana do konstruowania przedziałów ufności i oceny stabilności modeli statystycznych.