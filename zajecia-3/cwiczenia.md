
# Warsztaty: Analiza Danych w MATLAB

## Cel
Studenci przeanalizują zestaw danych zawierający pomiary systemu gazowego (np. ciśnienie gazu i przepływ w czasie). Warsztaty będą obejmować zadania takie jak importowanie danych, przeprowadzanie analizy, wizualizacja wyników, identyfikacja anomalii oraz prowadzenie głębszej analizy statystycznej. Celem jest zdobycie praktycznego doświadczenia w stosowaniu technik analizy danych przy użyciu MATLAB.

## Wymagania
- MATLAB (z podstawowymi toolboxami do analizy i wizualizacji danych).
- Plik z danymi (`gas_system_data.csv`), w którym znajdują się pomiary systemu gazowego:
  - `Time` (w minutach)
  - `Gas_Pressure` (w psi)
  - `Gas_Flow` (w metrach sześciennych na minutę)

## Instrukcje

### Krok 1: Import danych
1. **Pobieranie danych**  
   Pobierz dostarczony plik z danymi (`gas_system_data.csv`) i umieść go w swoim katalogu roboczym MATLAB.

2. **Importowanie danych do MATLAB**  
   Użyj poniższego kodu MATLAB, aby wczytać dane do tabeli:
   ```matlab
   data = readtable('gas_system_data.csv');
   ```
   - Zweryfikuj poprawność importu danych, wyświetlając pierwsze kilka wierszy:
   ```matlab
   head(data)
   ```

### Krok 2: Eksploracja i Czyszczenie Danych
1. **Inspekcja Danych**  
   - Sprawdź, czy w danych nie ma brakujących wartości za pomocą funkcji `ismissing`:
   ```matlab
   missingData = sum(ismissing(data));
   disp('Liczba brakujących wartości w każdej kolumnie:');
   disp(missingData);
   ```

2. **Obsługa Brakujących Danych (jeśli występują)**  
   - Jeśli są brakujące wartości, wybierz sposób ich obsługi (np. usunięcie wierszy lub uzupełnienie średnimi wartościami):
   ```matlab
   % Przykład: Usuwanie wierszy z brakującymi wartościami
   data = rmmissing(data);
   ```

### Krok 3: Statystyki Opisowe
1. **Oblicz Kluczowe Statystyki**  
   - Oblicz średnią i odchylenie standardowe dla `Gas_Pressure` i `Gas_Flow`:
   ```matlab
   meanPressure = mean(data.Gas_Pressure);
   stdPressure = std(data.Gas_Pressure);
   meanFlow = mean(data.Gas_Flow);
   stdFlow = std(data.Gas_Flow);

   fprintf('Średnie ciśnienie gazu: %.2f psi\n', meanPressure);
   fprintf('Odchylenie standardowe ciśnienia gazu: %.2f psi\n', stdPressure);
   fprintf('Średni przepływ gazu: %.2f m^3/min\n', meanFlow);
   fprintf('Odchylenie standardowe przepływu gazu: %.2f m^3/min\n', stdFlow);
   ```

### Krok 4: Wizualizacja Danych
1. **Wykres Ciśnienia i Przepływu Gazu w Czasie**  
   - Utwórz wykres szeregów czasowych pokazujący zarówno `Gas_Pressure`, jak i `Gas_Flow`:
   ```matlab
   figure;
   subplot(2, 1, 1);
   plot(data.Time, data.Gas_Pressure);
   title('Ciśnienie Gazu w Czasie');
   xlabel('Czas (minuty)');
   ylabel('Ciśnienie (psi)');

   subplot(2, 1, 2);
   plot(data.Time, data.Gas_Flow);
   title('Przepływ Gazu w Czasie');
   xlabel('Czas (minuty)');
   ylabel('Przepływ (m^3/min)');
   ```

2. **Wyróżnienie Anomalii**  
   - Zidentyfikuj wartości, które wypadają poza zakres `[mean ± 2*std]` i zaznacz je na wykresie:
   ```matlab
   anomalyIndicesPressure = (data.Gas_Pressure < meanPressure - 2*stdPressure) | ...
                            (data.Gas_Pressure > meanPressure + 2*stdPressure);
   anomalyIndicesFlow = (data.Gas_Flow < meanFlow - 2*stdFlow) | ...
                        (data.Gas_Flow > meanFlow + 2*stdFlow);

   hold on;
   plot(data.Time(anomalyIndicesPressure), data.Gas_Pressure(anomalyIndicesPressure), 'ro');
   plot(data.Time(anomalyIndicesFlow), data.Gas_Flow(anomalyIndicesFlow), 'ro');
   hold off;
   ```

### Krok 5: Analiza Korelacji
1. **Oblicz Korelację Między Ciśnieniem a Przepływem Gazu**  
   - Użyj funkcji `corr` MATLAB, aby określić, czy istnieje korelacja między ciśnieniem a przepływem gazu:
   ```matlab
   correlation = corr(data.Gas_Pressure, data.Gas_Flow);
   fprintf('Korelacja między ciśnieniem a przepływem gazu: %.2f\n', correlation);
   ```

2. **Interpretacja Korelacji**  
   - Zastanów się, czy istnieje istotna korelacja i co może ona oznaczać dla relacji między ciśnieniem a przepływem gazu.

### Krok 6: Zaawansowana Analiza - Średnie Ruchome
1. **Oblicz Średnie Ruchome dla Wygładzania Danych**  
   - Wygładź dane dotyczące ciśnienia i przepływu gazu za pomocą filtra średniej ruchomej:
   ```matlab
   windowSize = 5; % 5-minutowa średnia ruchoma
   smoothPressure = movmean(data.Gas_Pressure, windowSize);
   smoothFlow = movmean(data.Gas_Flow, windowSize);
   ```

2. **Wykres Wygładzonych Danych**  
   - Nałóż wygładzone dane na oryginalne wykresy w celu porównania:
   ```matlab
   figure;
   subplot(2, 1, 1);
   plot(data.Time, data.Gas_Pressure, 'b');
   hold on;
   plot(data.Time, smoothPressure, 'r');
   title('Ciśnienie Gazu w Czasie (Oryginalne vs. Wygładzone)');
   xlabel('Czas (minuty)');
   ylabel('Ciśnienie (psi)');
   legend('Oryginalne', 'Wygładzone');

   subplot(2, 1, 2);
   plot(data.Time, data.Gas_Flow, 'b');
   hold on;
   plot(data.Time, smoothFlow, 'r');
   title('Przepływ Gazu w Czasie (Oryginalne vs. Wygładzone)');
   xlabel('Czas (minuty)');
   ylabel('Przepływ (m^3/min)');
   legend('Oryginalne', 'Wygładzone');
   hold off;
   ```

### Krok 7: Analiza Predykcyjna
1. **Model Regresji Liniowej do Przewidywania Przepływu Gazu na Podstawie Ciśnienia**  
   - Dopasuj prosty model regresji liniowej do przewidywania `Gas_Flow` na podstawie `Gas_Pressure`:
   ```matlab
   mdl = fitlm(data.Gas_Pressure, data.Gas_Flow);
   disp(mdl);
   ```

2. **Wykres Linii Regresji**  
   - Narysuj dane i dopasowaną linię regresji:
   ```matlab
   figure;
   plot(data.Gas_Pressure, data.Gas_Flow, 'o');
   hold on;
   plot(data.Gas_Pressure, mdl.Fitted, '-');
   title('Regresja Liniowa: Przepływ Gazu vs. Ciśnienie Gazu');
   xlabel('Ciśnienie Gazu (psi)');
   ylabel('Przepływ Gazu (m^3/min)');
   legend('Dane', 'Linia Dopasowana');
   hold off;
   ```
