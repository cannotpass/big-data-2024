### Zadanie: **Implementacja ARIMA w MATLAB i porównanie z gotową funkcją**

**Narzędzie:** MATLAB
**Cel zadania:** Zaimplementuj model ARIMA(1,1,1) ręcznie w MATLAB i porównaj wyniki z wbudowaną funkcją `arima`.
---

### Opis zadania

W ramach tego zadania najpierw zaimplementujesz prosty model ARIMA(1,1,1) z podstawowymi krokami: różnicowaniem danych (dla stacjonarności), autoregresją (AR), i średnią ruchomą (MA). Następnie porównasz wyniki z modelem ARIMA utworzonym przy pomocy wbudowanej funkcji `arima` w MATLAB.

#### Krok 1: Generowanie danych szeregów czasowych

1. **Wygeneruj dane szeregów czasowych**  
   Stwórz sztuczny szereg czasowy z trendem i szumem, który będzie bazą dla naszego modelu ARIMA. Zastosuj trend liniowy oraz losowy szum normalny.

   ```matlab
   n = 100; % liczba punktów danych
   t = (1:n)'; % wektor czasu
   trend = 0.5 * t; % trend liniowy
   noise = randn(n, 1); % szum losowy
   y = trend + noise; % dane czasowe z trendem
   ```

2. **Wizualizacja danych**  
   Narysuj dane, aby zobaczyć ich trend i zachowanie w czasie.

   ```matlab
   figure;
   plot(t, y);
   title('Dane czasowe z trendem');
   xlabel('Czas');
   ylabel('Wartość');
   grid on;
   ```

#### Krok 2: Ręczna implementacja modelu ARIMA(1,1,1)

1. **Różnicowanie danych**  
   Różnicuj dane, aby usunąć trend i uzyskać szereg stacjonarny. To odpowiada części ARIMA (I=1).

   ```matlab
   dy = diff(y); % różnicowanie pierwszego rzędu
   ```

2. **Implementacja autoregresji (AR(1))**  
   Użyj metody regresji, aby oszacować współczynnik autoregresji \( \phi \) dla modelu AR(1).

   ```matlab
   phi = regress(dy(2:end), dy(1:end-1)); % współczynnik autoregresji
   ```

3. **Implementacja średniej ruchomej (MA(1))**  
   Oszacuj współczynnik MA(1) \( \theta \) jako średnią z reszt (błędów) w przewidywaniach.

   ```matlab
   errors = dy(2:end) - phi * dy(1:end-1); % błędy modelu AR(1)
   theta = mean(errors); % współczynnik średniej ruchomej
   ```

4. **Prognozowanie z modelem ARIMA(1,1,1)**  
   Użyj uzyskanych współczynników \( \phi \) i \( \theta \), aby przewidzieć kolejną wartość.

   ```matlab
   y_pred_manual = y(end) + phi * (y(end) - y(end-1)) + theta; % prognoza
   ```

#### Krok 3: Implementacja gotowego modelu ARIMA w MATLAB

1. **Zdefiniuj model ARIMA(1,1,1)** za pomocą funkcji `arima`:

   ```matlab
   model = arima(1,1,1); % ARIMA(1,1,1)
   ```

2. **Dopasuj model do danych i dokonaj prognozy**  
   Użyj funkcji `estimate` do dopasowania modelu i `forecast` do wykonania prognozy.

   ```matlab
   estimated_model = estimate(model, y);
   [y_pred_builtin, ~] = forecast(estimated_model, 1, 'Y0', y); % prognoza na 1 krok
   ```

#### Krok 4: Porównanie wyników

1. **Wyświetl przewidywane wartości**  
   Porównaj przewidywane wartości z obu metod: ręcznej implementacji i wbudowanej funkcji.

   ```matlab
   fprintf('Prognoza (implementacja ręczna): %.2f\n', y_pred_manual);
   fprintf('Prognoza (funkcja wbudowana): %.2f\n', y_pred_builtin);
   ```

2. **Wizualizacja porównania**  
   Dodaj prognozy do wykresu, aby zobaczyć, jak różnią się obie metody.

   ```matlab
   figure;
   plot(t, y, 'b');
   hold on;
   plot(n+1, y_pred_manual, 'ro', 'MarkerSize', 8, 'DisplayName', 'Prognoza ręczna');
   plot(n+1, y_pred_builtin, 'go', 'MarkerSize', 8, 'DisplayName', 'Prognoza funkcji wbudowanej');
   title('Porównanie prognoz ARIMA');
   legend;
   grid on;
   ```

---

### Podsumowanie i pytania do refleksji:

1. Jak duże są różnice między prognozami z obu metod? Co może być tego przyczyną?
2. Jakie elementy modelu ARIMA są łatwiejsze do zaimplementowania ręcznie, a które wymagają bardziej zaawansowanych narzędzi?

Zadanie to pomaga w lepszym zrozumieniu działania modelu ARIMA poprzez jego ręczną implementację i porównanie z gotową funkcją MATLAB, co pozwala lepiej zrozumieć, jak ARIMA wykorzystuje różnicowanie, autoregresję i średnią ruchomą w analizie szeregów czasowych.