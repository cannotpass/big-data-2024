### Zadanie: **Regresja wielomianowa i liniowa w MATLAB**

**Narzędzie:** MATLAB  
**Cel zadania:** Samodzielne wygenerowanie danych oraz implementacja prostych modeli regresji liniowej i wielomianowej w celu lepszego zrozumienia ich działania.

---

### Opis zadania

W ramach tego zadania najpierw wygenerujesz dane, które będą reprezentowały zależność między dwiema zmiennymi. Następnie zaimplementujesz własne funkcje do regresji liniowej oraz wielomianowej. W końcowej części zadania dokonasz wizualizacji wyników i porównasz, jak modele te różnią się między sobą w zależności od złożoności zależności w danych.

#### Krok 1: Generowanie danych

1. **Utwórz wektor zmiennej niezależnej** \( x \) — dla uproszczenia, zdefiniuj wartości od 1 do 100 (z krokiem co 1).

   ```matlab
   x = (1:100)'; % Wektor x od 1 do 100
   ```

2. **Utwórz zależność między zmienną niezależną \( x \) a zmienną zależną \( y \)** według wzoru:

   \[
   y = 3x + 15 + \text{szum}
   \]

   Dodaj losowy szum (`noise`), aby zasymulować rzeczywiste dane z pewnymi błędami. Skorzystaj z funkcji `randn` do wygenerowania szumu.

   ```matlab
   noise = 20 * randn(size(x)); % Generowanie losowego szumu
   y = 3 * x + 15 + noise; % Generowanie wartości y
   ```

3. **Wizualizacja danych:**  
   Narysuj wykres punktowy wygenerowanych danych, aby zobaczyć rozkład punktów.

   ```matlab
   figure;
   scatter(x, y);
   title('Wygenerowane dane');
   xlabel('x');
   ylabel('y');
   grid on;
   ```

#### Krok 2: Implementacja funkcji regresji liniowej

1. **Napisz funkcję `regresja_liniowa`, która obliczy współczynniki regresji liniowej** na podstawie danych. Funkcja powinna mieć strukturę:

   ```matlab
   function [a, b] = regresja_liniowa(x, y)
       n = length(x);
       a = (n*sum(x.*y) - sum(x)*sum(y)) / (n*sum(x.^2) - sum(x)^2);
       b = (sum(y) - a*sum(x)) / n;
   end
   ```

   Funkcja ta zwraca współczynniki \( a \) (nachylenie) oraz \( b \) (przesunięcie), które określają równanie prostej \( y = ax + b \).

2. **Wywołaj funkcję `regresja_liniowa`** na wygenerowanych danych \( (x, y) \), aby uzyskać współczynniki \( a \) i \( b \).

   ```matlab
   [a, b] = regresja_liniowa(x, y);
   ```

3. **Dodaj linię regresji liniowej do wykresu:**  
   Oblicz przewidywane wartości \( y \) dla prostej \( y = ax + b \) i narysuj je na wykresie danych.

   ```matlab
   y_pred_linear = a * x + b;
   hold on;
   plot(x, y_pred_linear, 'r', 'LineWidth', 2);
   legend('Dane', 'Regresja liniowa');
   ```

#### Krok 3: Implementacja funkcji regresji wielomianowej

1. **Napisz funkcję `regresja_wielomianowa`, która wykorzysta `polyfit` do regresji wielomianowej**. Funkcja powinna mieć możliwość dopasowania wielomianu dowolnego stopnia.

   ```matlab
   function p = regresja_wielomianowa(x, y, stopien)
       p = polyfit(x, y, stopien); % Regresja wielomianowa
   end
   ```

2. **Użyj funkcji `regresja_wielomianowa` na danych \( (x, y) \)**, aby dopasować wielomian drugiego stopnia (kwadratowy).

   ```matlab
   stopien = 2;
   p = regresja_wielomianowa(x, y, stopien);
   ```

3. **Dodaj wykres regresji wielomianowej do wykresu:**  
   Skorzystaj z `polyval`, aby obliczyć przewidywane wartości \( y \) na podstawie wielomianu, a następnie narysuj model na wykresie.

   ```matlab
   y_pred_poly = polyval(p, x);
   plot(x, y_pred_poly, 'g', 'LineWidth', 2);
   legend('Dane', 'Regresja liniowa', 'Regresja kwadratowa');
   ```

#### Krok 4: Porównanie modeli

1. **Przeanalizuj, który model lepiej dopasowuje się do danych:**  
   Zwróć uwagę, jak regresja liniowa i wielomianowa różnią się w dopasowaniu do wygenerowanych punktów. Wnioski warto wysnuć na podstawie wizualizacji.

2. **Eksperymenty z wyższymi stopniami wielomianów (opcjonalne):**  
   Jeśli masz więcej czasu, spróbuj zwiększyć stopień wielomianu w `regresja_wielomianowa` (np. do 3 lub 4) i zobacz, jak wpływa to na dopasowanie. Rozważ, czy wyższy stopień prowadzi do nadmiernego dopasowania.

---

### Dodatkowe pytania do refleksji:

1. Jak zmieni się dopasowanie, jeśli zwiększymy lub zmniejszymy zakres szumu w danych?
2. W jakich przypadkach regresja wielomianowa jest lepszym wyborem niż liniowa?
3. Jakie mogą być potencjalne problemy z używaniem regresji wielomianowej przy bardziej zaszumionych danych?
