---
layout: math
---

# Financial Enterprise Risk Management

## 7: Definicje Ryzyka

**Wyjaśnij pojęcie ryzyka systematycznego, podaj dwa przykłady ryzyka systematycznego, na które może być narażona firma ubezpieczeniowa, dwie metody zarządzania ryzykiem systematycznym oraz ich skuteczność w redukcji ryzyka systematycznego.**

### **1. Pojęcie ryzyka systematycznego**
**Ryzyko systematyczne (rynkowe / niedywersyfikowalne)** to ryzyko wynikające ze wspólnych czynników makroekonomicznych, rynkowych lub demograficznych wpływających równocześnie na cały rynek bądź sektor. 
Jego kluczową cechą jest **brak możliwości eliminacji poprzez prostą dywersyfikację portfela** (zwiększanie liczby niezależnych polis nie redukuje tego ryzyka).

### **2. Dwa przykłady dla zakładu ubezpieczeń**
1. **Ryzyko stóp procentowych:** Zmiana krzywej stóp wpływa jednocześnie na wycenę wszystkich aktywów oraz dyskontowanie pasywów (rezerw technicznych). Spadek stóp obniża rentowność lokat i skokowo podnosi wartość rezerw długoterminowych (np. rent).
2. **Ryzyko długowieczności (*longevity risk*) / pandemiczne:** Ogólnokrajowy lub globalny trend spadku umieralności wydłuża okres wypłaty rent dla całego portfela jednocześnie. Z kolei pandemia skokowo zwiększa szkodowość we wszystkich ubezpieczeniach na życie.

### **3. Dwie metody zarządzania i ich skuteczność**

#### **Metoda 1: Hedging finansowy / ALM (*Asset-Liability Matching*)**
* **Istota:** Dopasowanie duration aktywów i pasywów oraz wykorzystanie instrumentów pochodnych (np. IRS, swapy inflacyjne, swapy długowieczności).
* **Skuteczność:** 
  * *Wysoka* w neutralizacji pierwotnego ryzyka systematycznego (np. domknięcie luki duration redukuje ryzyko stóp procentowych niemal do zera).
  * *Ograniczenia:* Generuje nowe ryzyka – ryzyko kredytowe kontrahenta (*counterparty risk*), ryzyko płynności (wymogi depozytowe / *margin calls*) oraz ryzyko bazy (*basis risk* z powodu niedoskonałego dopasowania kontraktu do pasywów).

#### **Metoda 2: Transfer ryzyka (Reasekuracja i Sekurytyzacja / ILS)**
* **Istota:** Transfer ryzyka poza bilans spółki na rzecz reasekuratorów lub rynku kapitałowego (np. umowy *Stop Loss*, obligacje katastroficzne *CAT bonds*, obligacje pandemiczne).
* **Skuteczność:** 
  * *Wysoka* w fizycznym zdjęciu skrajnego ogona ryzyka z bilansu i uwolnieniu kapitału wymogowego (SCR).
  * *Ograniczenia:* Bardzo wysoki koszt transferu (wysokie premie za ryzyko systematyczne), ograniczona pojemność rynku (*market capacity*) oraz ryzyko niewypłacalności reasekuratora.

---

**Wyjaśnij pojęcia, podaj przykłady oraz metody zarządzania ryzykiem:**
* **a) Systematycznym i niesystematycznym.**
* **b) Negatywnej selekcji – adverse selection.**
* **c) Pokusy nadużycia – moral hazard.**
* **d) Operacyjnym.**

### **a) Ryzyko systematyczne i niesystematyczne**

#### **1. Ryzyko systematyczne (rynkowe / niedywersyfikowalne)**
* **Definicja:** Ryzyko wynikające z ogólnorynkowych czynników makroekonomicznych lub zdarzeń zewnętrznych oddziałujących jednocześnie na cały rynek. **Nie ulega redukcji poprzez prostą dywersyfikację portfela**.
* **Przykłady:** Zmiany stóp procentowych, skok inflacji, globalna pandemia, załamanie rynków finansowych (krach).
* **Metody zarządzania:** 
  * *Hedging finansowy / ALM:* Dopasowanie duration aktywów i pasywów, instrumenty pochodne (np. IRS, opcje, swapy).
  * *Transfer ryzyka:* Reasekuracja nieproporcjonalna (*Stop Loss*), sekurytyzacja ryzyka ubezpieczeniowego (*CAT bonds*).

#### **2. Ryzyko niesystematyczne (specyficzne / dywersyfikowalne)**
* **Definicja:** Ryzyko unikalne dla pojedynczego podmiotu, kontraktu lub wąskiej grupy aktywów, statystycznie niezależne od rynku. **Można je niemal całkowicie wyeliminować poprzez dywersyfikację**.
* **Przykłady:** Pożar w pojedynczej fabryce, bankructwo konkretnego emitenta obligacji, błąd medyczny ubezpieczonego lekarza.
* **Metody zarządzania:**
  * *Dywersyfikacja:* Budowa dużego portfela wzajemnie nieskorelowanych ryzyk (prawo wielkich liczb – *pooling of risks*).
  * *Limity koncentracji:* Nakładanie limitów ekspozycji na pojedynczego klienta, branżę lub emitenta.

### **b) Negatywna selekcja (*Adverse Selection*)**

* **Definicja:** Asymetria informacji występująca **przed zawarciem umowy** (*ex-ante*), w której podmioty o wyższym profilu ryzyka częściej kupują ubezpieczenie, co przy jednolitej składce wypycha z rynku podmioty niskiego ryzyka (spirala negatywnej selekcji).
* **Przykłady:** Zakup polisy na życie przez osoby ze zdiagnozowaną chorobą, zakup ubezpieczenia suszowego wyłącznie przez rolników z terenów suchych.
* **Metody zarządzania:**
  * *Screening / Underwriting:* Medyczna i finansowa ocena ryzyka (badania lekarskie, ankiety medyczne, weryfikacja historii szkodowej).
  * *Segmentacja taryfowa:* Różnicowanie składek według czynników ryzyka (wiek, stan zdrowia, lokalizacja).
  * *Pule grupowe i obowiązkowość:* Ubezpieczenia grupowe (np. pracownicze) lub ustawowy przymus ubezpieczeniowy (np. OC ppm), eliminujące dobrowolność wyboru.

### **c) Pokusa nadużycia (*Moral Hazard*)**

* **Definicja:** Asymetria informacji i zmiana zachowania ubezpieczonego **po zawarciu umowy** (*ex-post*). Posiadanie ochrony skłania do podejmowania większego ryzyka lub zaniechania ostrożności, gdyż koszt ewentualnej straty ponosi ubezpieczyciel.
* **Przykłady:** Brawurowa jazda po wykupieniu pełnego AC, brak dbałości o zabezpieczenia przeciwpożarowe w ubezpieczonym obiekcie, zawyżanie kosztów leczenia przy pełnym pakiecie medycznym.
* **Metody zarządzania:**
  * *Współpłacenie i retencja klienta:* Udział własny, franszyza redukcyjna, franszyza integralna.
  * *Systemy premiowo-karowe:* Systemy *Bonus-Malus* (wzrost składki po zgłoszeniu szkody).
  * *Monitoring i telematyka:* Wymogi instalacji zabezpieczeń (alarmy, zraszacze), monitoring stylu jazdy (telematyka).

### **d) Ryzyko operacyjne**

* **Definicja:** Zgodnie z dyrektywą *Wypłacalność II* (i Bazyleą II/III) jest to ryzyko straty wynikające z **nieodpowiednich lub zawodnych procedur wewnętrznych, błędów ludzkich, awarii systemów IT lub ze zdarzeń zewnętrznych** (obejmuje ryzyko prawne, wyklucza ryzyko strategiczne i reputacyjne).
* **Przykłady:** Błąd w arkuszu kalkulacyjnym aktuariusza przy kalkulacji rezerw, awaria bazy danych polisowych, wyciek danych (atak ransomware / phishing), nadużycie wewnętrzne (oszustwo pracownika).
* **Metody zarządzania:**
  * *Kontrola wewnętrzna i podział obowiązków:* Procedury "czterech oczu", audyt wewnętrzny, automatyzacja procesów.
  * *Zarządzanie ciągłością działania (BCM / BCP):* Plany odzyskiwania awaryjnego (*Disaster Recovery Plans*), zapasowe serwerownie, polityka kopii zapasowych.
  * *Transfer ryzyka:* Zakup polis ubezpieczeniowych od ryzyk operacyjnych (np. *Cyber Insurance*, ubezpieczenie D&O, polisy *Crime*).

---

**7.8 Ryzyko demograficzne** 

* **a) Wyjaśnij pojęcia ryzyka śmiertelności i długowieczności.**

* **b) Scharakteryzuj cztery rodzaje ryzyka śmiertelności i długowieczności związane z poziomem (level), zmiennością (volatility), trendem (trend) i zdarzeniami katastroficznymi (catastrophe), w szczególności wskaż kluczowe różnice pomiędzy czynnikami ryzyka level vs volatility, volatility vs catastrophe i level vs trend.**

### **a) Pojęcia ryzyka śmiertelności i długowieczności**

* **Ryzyko śmiertelności (*mortality risk*):** Ryzyko, że rzeczywista umieralność w portfelu ubezpieczonych okaże się **wyższa** od zakładanej. Zagrożenie dla produktów ochronnych na wypadek śmierci (np. terminowe ubezpieczenia na życie).
* **Ryzyko długowieczności (*longevity risk*):** Ryzyko, że rzeczywista umieralność okaże się **niższa** od zakładanej (ubezpieczeni żyją dłużej). Zagrożenie dla produktów wypłacających świadczenia dożywotnie (np. renty życiowe, fundusze emerytalne).

### **b) Charakterystyka czterech rodzajów ryzyka i kluczowe różnice**

#### **1. Charakterystyka:**
1. **Ryzyko poziomu (*level risk*):** Ryzyko, że bazowy, początkowy poziom natężenia zgonów przyjęty w modelu różni się od rzeczywistego poziomu w ubezpieczanej populacji (błąd kalibracji parametrów bazowych).
2. **Ryzyko zmienności (*volatility risk*):** Ryzyko losowych, przypadkowych wahań liczby zgonów wokół wartości oczekiwanej w danym roku, wynikające ze skończonej liczby ubezpieczonych w portfelu.
3. **Ryzyko katastroficzne (*catastrophe risk*):** Ryzyko nagłego, jednorazowego i ekstremalnego wzrostu zgonów wywołanego nadzwyczajnym zdarzeniem zewnętrznym (np. pandemia, wojna).
4. **Ryzyko trendu (*trend risk*):** Ryzyko niepewności co do tempa długookresowej zmiany (zazwyczaj spadku) umieralności w przyszłości (np. wpływ postępu medycyny).

#### **2. Kluczowe różnice:**

* **Level vs Volatility:**
  * **Level:** Ryzyko **systematyczne** (niedywersyfikowalne liczbą polis) – wynika z błędnego oszacowania parametrów populacyjnych; zwiększanie portfela go nie eliminuje.
  * **Volatility:** Ryzyko **niesystematyczne** (dywersyfikowalne) – wynika z procesu losowego i **zanika wraz ze wzrostem wielkości portfela** (zgodnie z prawem wielkich liczb).

* **Volatility vs Catastrophe:**
  * **Volatility:** Standardowe, ciągłe fluktuacje stochastyczne w warunkach normalnych (*attritional risk*), wpływające symetrycznie na obie strony (zarówno na śmiertelność, jak i renty).
  * **Catastrophe:** Zjawisko skrajne o grubym ogonie (*tail event*), o charakterze asymetrycznym – zagraża niemal wyłącznie produktom ze świadczeniem w razie śmierci (nagły spadek śmiertelności o skali katastroficznej w praktyce nie występuje).

* **Level vs Trend:**
  * **Level:** Błąd **statyczny** w punkcie wyjścia – dotyczy niedoszacowania obecnego poziomu śmiertelności na dzień wyceny.
  * **Trend:** Błąd **dynamiczny** w czasie – dotyczy niepewności co do pochodnej (stopy zmian) umieralności w długim horyzoncie czasowym (ujawnia się stopniowo na przestrzeni kolejnych dekad).

## 16: Odpowiedzi na ryzyko

**16.8, 16.9: Wytłumacz na czym polegają poniższe metody zarządzania ryzykiem w ubezpieczeniach majątkowych:**
* **a) Premium rating/prior rating.**
* **b) Experience rating/posterior rating.**
* **c) Dywersyfikacja.**
* **d) Reasekuracja.**
* **e) Sekurytyzacja.**

### **a) Premium rating / prior rating (Taryfikacja *a priori*)**
* **Istota:** Ustalenie wyjściowej składki technicznej **przed** rozpoczęciem okresu ochrony na podstawie obserwowalnych cech ubezpieczonego i przedmiotu ubezpieczenia (zmiennych taryfowych, np. wiek kierowcy, lokalizacja, moc silnika).
* **Narzędzia i cel:** Uogólnione modele liniowe (GLM) do modelowania częstości i dotkliwości szkód; podział portfela na homogeniczne klasy ryzyka w celu **ograniczenia negatywnej selekcji (*adverse selection*)**.

### **b) Experience rating / posterior rating (Taryfikacja *a posteriori*)**
* **Istota:** Modyfikacja składki bazowej na podstawie **rzeczywistej historii szkodowości** danego ubezpieczonego lub floty (doświadczenia szkodowego).
* **Narzędzia i cel:** Systemy *Bonus-Malus* (lub NCD – *No Claims Discount*), modele teorii wiarygodności (np. model Bühlmanna-Strauba). Służy korekcie asymetrii informacji oraz **redukcji pokusy nadużycia (*moral hazard*)**.

### **c) Dywersyfikacja**
* **Istota:** Łączenie w portfelu dużej liczby wzajemnie nieskorelowanych ryzyk, co zgodnie z prawem wielkich liczb redukuje wariancję jednostkowej straty (ryzyko specyficzne).
* **Wymiary w majątku:** Dywersyfikacja **geograficzna** (unikanie kumulacji ryzyk powodziowych/wichur), **między liniami biznesowymi** (łączenie np. komunikacji i ubezpieczeń mienia) oraz **sektorowa**.

### **d) Reasekuracja**
* **Istota:** Umowny transfer części ryzyka ubezpieczeniowego na inny podmiot (reasekuratora) w zamian za część składki.
* **Formy i cel:** Reasekuracja proporcjonalna (kwotowa, *surplus*) oraz nieproporcjonalna (*Excess of Loss*, *Stop Loss*). Zwiększa pojemność ubezpieczeniową (*underwriting capacity*), stabilizuje wynik techniczny i **obniża wymóg kapitałowy (SCR)**.

### **e) Sekurytyzacja (np. *CAT bonds* / ILS)**
* **Istota:** Transfer ryzyka ubezpieczeniowego (zazwyczaj ekstremalnego / katastroficznego) bezpośrednio na **rynki kapitałowe** poprzez emisję zbywalnych papierów wartościowych przez spółkę celową (SPV/SPI).
* **Mechanizm i cel:** Inwestorzy kupują obligacje katastroficzne; w przypadku wystąpienia zdefiniowanego kataklizmu kapitał z obligacji przechodzi na ubezpieczyciela na pokrycie szkód. Pozwala na ominięcie ograniczeń pojemności tradycyjnego rynku reasekuracji przy niemal zerowym ryzyku kredytowym kontrahenta (środki są zdeponowane w *collateral trust*).















# ROZPORZĄDZENIE DELEGOWANE KOMISJI (UE) 2015/35 z dnia 10 października 2014 r. uzupełniające dyrektywę Parlamentu Europejskiego i Rady 2009/138/WE w sprawie podejmowania i prowadzenia działalności ubezpieczeniowej i reasekuracyjnej (Wypłacalność II)

## Art. 44-47 

**Jakie dwa warunki muszą spełniać stopy struktury terminowej podstawowej stopy procentowej wolnej od ryzyka.**

1. Rynek tych instrumentów finansowych musi być głęboki, płynny i przejrzysty.
2. Muszą one pozwalać na wyznaczenie podstawowych stóp procentowych wolnych od ryzyka w wiarygodny sposób (dodatkowo, jak precyzuje ust. 1, muszą być one skorygowane o ryzyko kredytowe).

**Na podstawie jakich instrumentów finansowych ustalane są podstawowe stopy procentowe wolne od ryzyka.**

1. Podstawowym instrumentem są swapy stóp procentowych wyznaczane dla danej waluty.
2. Jeżeli dla danego terminu zapadalności (lub danej waluty) stopy swapów nie są dostępne na rynkach spełniających warunek głębokości, płynności i przejrzystości, wykorzystuje się stopy obligacji skarbowych (rządowych) emitowanych przez państwo, w którego walucie denominowane są zobowiązania.

**Wyjaśnij pojęcie ostatecznej stopy forward (Ultimate Forward Rate).**

Ostateczna stopa forward (UFR) to ustalona administracyjnie, długoterminowa stopa procentowa, do której asymptotycznie zmierza (jest ekstrapolowana) krzywa stóp procentowych wolnych od ryzyka dla bardzo długich terminów zapadalności (czyli takich, dla których na rynku brakuje już płynnych instrumentów finansowych.

Jej fundamentalną cechą jest to, że jest ona stabilna w czasie i zmienia się jedynie z powodu zmian długoterminowych oczekiwań makroekonomicznych (np. długoterminowej oczekiwanej inflacji i realnej stopy procentowej). Mechanizm UFR ma na celu ochronę zakładów ubezpieczeń przed nadmierną i sztuczną zmiennością wymogów kapitałowych dla długoterminowych zobowiązań ubezpieczeniowych (np. w ubezpieczeniach na życie).

## Art. 55 i Załącznik 1: Linie biznesowe

**W oparciu o Rozporządzenie Delegowane Komisji uzupełniające dyrektywę Wypłacalność II:**

* **a) Wymień dwie linie biznesowe w ramach zobowiązań z tytułu umów ubezpieczeń innych niż ubezpieczenia na życie.**

* **b) Wymień dwie linie biznesowe w ramach zobowiązań z tytułu ubezpieczeń na życie.**

* **c) Wymień jakie rodzaje zobowiązań, oprócz zobowiązań ubezpieczeń na życie i innych niż ubezpieczenia na życie, uwzględniamy jeszcze w ramach wyodrębniania linii biznesowych.**

* **d) W oparciu o jakie główne kryterium przypisywane są zobowiązania do linii biznesowych.**

* **e) W jaki sposób przypisywane są zobowiązania z tytułu ubezpieczeń zdrowotnych do linii biznesowych.**

a) Dwie linie biznesowe w ramach ubezpieczeń innych niż na życie (non-life):
* Ubezpieczenia pokrycia kosztów świadczeń medycznych.
* Ubezpieczenia na wypadek utraty dochodów

b) Dwie linie biznesowe w ramach ubezpieczeń na życie (life):
* Ubezpieczenia zdrowotne
* Ubezpieczenia z udziałem w zyskach

c) Zobowiązania z tytułu reasekuracji nieproporcjonalnej

d) Przypisanie zobowiązania ubezpieczeniowego lub reasekuracyjnego do określonej linii biznesowej musi odzwierciedlać charakter ryzyka związanego z tym zobowiązaniem.

e) O przypisaniu decydują zastosowane techniki ubezpieczeniowe (podstawa techniczna).

## Art. 114: Moduł ryzyka aktuarialnego w ubezpieczeniach innych niż ubezpieczenia na życie

**Wymień i scharakteryzuj krótko podmoduły ryzyka w obrębie modułu ryzyka aktuarialnego w ubezpieczeniach innych niż ubezpieczenia na życie zgodnie z Rozporządzeniem Delegowanym Wypłacalność II. Dla jednego wybranego podmodułu ryzyka opisz krótko jak wyznaczamy wymogi kapitałowe.**

1. Podmoduł ryzyka składek i rezerw (Premium and Reserve Risk)
   Jest to podstawowy i największy element ryzyka w ubezpieczeniach majątkowych. Łączy on w sobie dwa powiązane ryzyka, które oblicza się wspólnie:
   * Ryzyko składek: dotyczy przyszłości. Jest to ryzyko, że zarobione składki okażą się niewystarczające do pokrycia przyszłych szkód i kosztów, które z nich wynikną (np. z powodu złego oszacowania taryfy lub nieoczekiwanego wzrostu częstości/wartości szkód w przyszłym roku).
   * Ryzyko rezerw: dotyczy przeszłości. Jest to ryzyko, że obecne rezerwy techniczno-ubezpieczeniowe (już zawiązane na bilansie) okażą się niewystarczające na pokrycie ostatecznych kosztów likwidacji już zaistniałych szkód (tzw. ryzyko *run-off*).

2. Podmoduł ryzyka rezygnacji (Lapse Risk)
   Odnosi się do ryzyka straty finansowej wynikającej z nieoczekiwanej zmiany zachowań ubezpieczonych. Dotyczy sytuacji, w których klienci częściej niż zakładano rezygnują z polis, nie odnawiają ich, lub zmieniają warunki ubezpieczenia, co prowadzi do utraty oczekiwanych zysków wliczanych wcześniej w wartość portfela.

3. Podmoduł ryzyka katastroficznego (Catastrophe Risk)
   Odnosi się do ryzyka poniesienia ogromnych strat w wyniku ekstremalnych, rzadkich, ale bardzo dotkliwych zdarzeń, których nie ujmuje w pełni standardowe ryzyko składek. Dzieli się zazwyczaj na katastrofy naturalne (powodzie, wichury, trzęsienia ziemi), katastrofy spowodowane przez człowieka (terroryzm, pożary wielkich zakładów) oraz inne ryzyka katastroficzne.

Algorytm dla ryzyka składek i rezerw składa się z następujących kroków:

1. Wyznaczenie Miar Wolumenu (Volume Measures):
   Dla każdej linii biznesowej wyznacza się odrębnie "rozmiar" narażenia na ryzyko:
   * Miara wolumenu dla składek ($V_{prem}$) – oparta głównie na składkach zarobionych w kolejnym roku.
   * Miara wolumenu dla rezerw ($V_{res}$) – oparta na wartości najlepszego oszacowania rezerw szkodowych (Claims Provision).

2. Przypisanie Odchyleń Standardowych:
   Z rozporządzenia Wypłacalność II odczytuje się narzucone parametry rynkowe, czyli odchylenia standardowe przypisane do danej linii biznesowej: odchylenie dla składek ($\sigma_{prem}$) oraz odchylenie dla rezerw ($\sigma_{res}$).

3. Agregacja wewnątrz linii biznesowej:
   Dla każdej linii (np. OC komunikacyjne) łączy się ryzyko składek i rezerw, wyliczając łączne odchylenie standardowe dla tej linii, uwzględniając korelację między składkami a rezerwami (zazwyczaj korelacja wynosi 0.5).

4. Agregacja między liniami biznesowymi (Efekt dywersyfikacji):
   Łączy się wyniki ze wszystkich linii biznesowych, które oferuje ubezpieczyciel, używając do tego macierzy korelacji określonej w dyrektywie. Pozwala to wyznaczyć całkowity wolumen dla firmy ($V$) oraz całkowite zagregowane odchylenie standardowe ($\sigma$).

5. Obliczenie końcowego wymogu SCR:
   Wymóg kapitałowy dla tego podmodułu ($SCR_{nl\_pr}$) oblicza się zakładając logarytmiczno-normalny rozkład strat. W uproszczeniu (zgodnym z aproksymacją stosowaną w Solvency II dla VaR 99.5%), wymóg kapitałowy oblicza się jako trzykrotność odchylenia standardowego pomnożonego przez całkowity wolumen:
   **$$SCR = 3 \cdot \sigma \cdot V$$**

## Art. 164

**Wymień i scharakteryzuj krótko wszystkie podmoduły ryzyka w obrębie modułu ryzyka rynkowego zgodnie z Rozporządzeniem Delegowanym Wypłacalność II. Dla jednego wybranego podmodułu ryzyka opisz krótko jak wyznaczamy wymogi kapitałowe.**

1. Podmoduł ryzyka stopy procentowej: odzwierciedla wrażliwość wartości aktywów, zobowiązań oraz instrumentów finansowych na zmiany lub zmienność struktury terminowej stóp procentowych wolnych od ryzyka. Ryzyko to wynika z ewentualnego niedopasowania zapadalności aktywów i zobowiązań ubezpieczeniowych.

2. Podmoduł ryzyka cen akcji: odzwierciedla wrażliwość wartości na zmiany poziomu lub zmienność rynkowych cen akcji. W ramach formuły standardowej akcje dzieli się na różne typy (np. Typ 1 – akcje notowane na rynkach w EOG/OECD; Typ 2 – np. rynki wschodzące, akcje nienotowane), dla których stosuje się odmienne parametry ryzyka.

3. Podmoduł ryzyka cen nieruchomości: obejmuje wrażliwość wartości aktywów na zmiany poziomu lub zmienność rynkowych cen nieruchomości. Dotyczy to m.in. bezpośrednich inwestycji w grunty czy budynki.

4. Podmoduł ryzyka spreadu: odzwierciedla wrażliwość wartości aktywów (przede wszystkim dłużnych papierów wartościowych, takich jak obligacje korporacyjne) na zmiany poziomu lub zmienność spreadów kredytowych, czyli premii za ryzyko ponad stopę zwrotu wolną od ryzyka.

5. Podmoduł ryzyka walutowego: pokrywa ryzyko wrażliwości na zmiany poziomu lub zmienność kursów wymiany walut. Jest to kluczowe w sytuacji występowania niedopasowania walutowego (gdy zakład np. posiada zobowiązania ubezpieczeniowe w PLN, ale część aktywów inwestuje w EUR).

6. Podmoduł koncentracji ryzyka rynkowego: odzwierciedla dodatkowe ryzyko ponoszone przez zakład ubezpieczeń wynikające z braku odpowiedniej dywersyfikacji portfela inwestycyjnego lub z posiadania nadmiernej ekspozycji na jednego emitenta (lub grupę powiązanych emitentów), co w razie jego problemów finansowych grozi dużymi stratami.

Do wyznaczania wymogów kapitałowych (SCR) w standardowej formule Wypłacalność II powszechnie stosuje się metodę scenariuszową (szokową).

Opis na przykładzie podmodułu ryzyka cen nieruchomości.

1. Zastosowanie szoku rynkowego: analiza zakłada skrajny, niekorzystny scenariusz rynkowy. Dla rynku nieruchomości przepisy definiują ten szok jako natychmiastowy spadek rynkowej wartości wszystkich posiadanych nieruchomości o 25%.

2. Ocena wpływu: następnie oblicza się, jak tak zdefiniowany szok wpłynąłby na bilans ekonomiczny (aktywa i pasywa) zakładu ubezpieczeń.

3. Wynik (wymóg kapitałowy): wymóg kapitałowy dla tego podmodułu (oznaczany jako $SCR_{property}$) jest równy dokładnej kwocie spadku wartości podstawowych środków własnych, który nastąpiłby po zaaplikowaniu wspomnianego szoku (-25% na ceny nieruchomości).

## Art. 222-247: Kapitałowy wymóg wypłacalności

**Wymień i krótko opisz wymogi jakie powinien spełnić model wewnętrzny w świetle Dyrektywy Wypłacalność II, aby został zaakceptowany przez organ nadzoru. Należy opisać pięć standardów**

1. Test wykorzystania (Use test)

    Model wewnętrzny nie może być tworzony wyłącznie w celu obniżenia wymogów kapitałowych i raportowania do nadzoru ("model do szuflady"). Musi być faktycznie, na co dzień używany w firmie. Zakład ubezpieczeń musi udowodnić, że model odgrywa istotną rolę w systemie zarządzania ryzykiem, procesach decyzyjnych (np. przy ustalaniu cen, reasekuracji) oraz w procesie alokacji kapitału gospodarczego.

2. Standardy jakości statystycznej (Statistical quality standards)

    Wymóg ten dotyczy „matematycznego i danowego” fundamentu modelu. Metody wyznaczania rozkładów prawdopodobieństwa muszą być rzetelne i opierać się na powszechnie uznanych technikach aktuarialnych. Dane używane w modelu (zarówno historyczne dane własne, jak i rynkowe) muszą być odpowiedniej jakości – kompletne, dokładne i wiarygodne. Ponadto wszelkie przyjęte założenia eksperckie muszą być rzetelnie uzasadnione.

3. Standardy kalibracji (Calibration standards)

    Model wewnętrzny może wykorzystywać różne miary ryzyka czy horyzonty czasowe na potrzeby wewnętrzne firmy, ale na potrzeby wyliczenia Kapitałowego Wymogu Wypłacalności (SCR) dla nadzoru, musi być w stanie wykalibrować wynik do konkretnego, narzuconego prawem standardu. Wynik ten musi odpowiadać miarze Value-at-Risk (VaR) na poziomie ufności 99,5% w horyzoncie jednego roku (zabezpieczenie przed zdarzeniem, które występuje średnio raz na 200 lat).

4. Standardy walidacji (Validation standards)

    Zakład ubezpieczeń ma obowiązek wdrożyć niezależny i regularny proces oceny działania swojego modelu. Walidacja polega na sprawdzaniu, czy model nadal prawidłowo odzwierciedla profil ryzyka firmy. Obejmuje to m.in. *back-testing* (porównywanie wyników przewidywanych przez model z faktycznymi stratami z przeszłości), analizę wrażliwości oraz testy warunków skrajnych (stress-testy).

5. Standardy dokumentacji (Documentation standards)

    Każdy element modelu wewnętrznego musi być wyczerpująco udokumentowany. Dokumentacja musi szczegółowo opisywać budowę modelu, jego podstawy teoretyczne i matematyczne, architekturę systemów IT, ograniczenia modelu oraz proces jego zatwierdzania i wprowadzania w nim zmian. Dokumentacja musi być na tyle przejrzysta i kompletna, aby organ nadzoru lub niezależny audytor mógł w pełni zrozumieć i ocenić, jak działa model.

## Art. 260: Obszary zarządzania ryzykiem

**W oparciu o Rozporządzenie Delegowane Wypłacalność II wymień i krótko scharakteryzuj pięć obszarów zarządzania ryzykiem**

1. Ocena ryzyka przyjmowanego do ubezpieczenia i tworzenie rezerw.

    Działania mające na celu optymalny dobór ubezpieczanych ryzyk oraz prawidłowe ustalanie wysokości składek. Obszar ten obejmuje również zarządzanie ryzykiem strat wynikających z błędnych lub nieadekwatnych założeń przyjmowanych do wyceny zobowiązań i tworzenia rezerw techniczno-ubezpieczeniowych.

2. Zarządzanie aktywami i zobowiązaniami.

    Bieżąca ocena i zarządzanie ryzykiem wynikającym z niedopasowania aktywów zakładu ubezpieczeń do jego zobowiązań (pasywów). Obejmuje to analizowanie rozbieżności m.in. pod kątem terminów zapadalności, walut, czy też wrażliwości na zmiany stóp procentowych i inflacji.

3. Zarządzanie ryzykiem lokaty (inwestycyjnym).

    Działania ukierunkowane na zarządzanie ryzykiem rynkowym, ryzykiem kredytowym oraz płynnością portfela inwestycyjnego. Obejmuje to m.in. weryfikację, w jaki sposób instrumenty pochodne są wykorzystywane do ograniczania ryzyka ubezpieczeniowego lub do ułatwiania efektywnego zarządzania portfelem zgodnie z tzw. "zasadą ostrożnego inwestora".

4. Zarządzanie ryzykiem płynności.

    Obszar gwarantujący, że zakład ubezpieczeń utrzyma wystarczającą ilość płynnych środków do terminowego regulowania swoich wymagalnych zobowiązań (np. wypłat odszkodowań).

5. Zarządzanie ryzykiem operacyjnym

    Działania nakierowane na identyfikację, ocenę i ograniczanie ryzyka wystąpienia strat wynikających z nieodpowiednich lub zawodnych procesów wewnętrznych, błędów ludzkich, awarii systemów informatycznych, a także ze zdarzeń zewnętrznych (takich jak np. oszustwa, czy gwałtowne zmiany prawne).
