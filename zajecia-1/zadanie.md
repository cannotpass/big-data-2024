
# **Warsztaty: Zbieranie i przetwarzanie danych w MATLAB**

## **Cel**:
Podczas tych warsztatów nauczysz się:
1. Zbierać i symulować dane (w tym dodawać szum).
2. Przetwarzać dane (obliczać podstawowe statystyki, wygładzać dane).
3. Tworzyć wykresy, aby wizualizować i porównywać różne zestawy danych.
4. Anotować kluczowe punkty na wykresach.

Pod koniec tego zadania będziesz umieć używać MATLAB do bardziej zaawansowanej analizy danych, uwzględniając szum i wygładzanie.

---

## **Krok 1: Symulacja zbierania danych z szumem**

W rzeczywistym świecie dane nie są zawsze idealne – mogą zawierać szum. Zasymulujemy temperatury, dodając losowy szum do odczytów.

### **Zadanie**: Symuluj 100 odczytów temperatury z szumem (w zakresie od 20 do 35 stopni Celsjusza).

Skopiuj i wklej poniższy kod do MATLAB:

```matlab
% Symulacja 100 odczytów temperatury z szumem
temperature_data = randi([20, 35], 1, 100);

% Dodajemy losowy szum (np. ±2°C) do odczytów temperatury
noise = randn(1, 100) * 2;
noisy_temperature_data = temperature_data + noise;

% Symulowany czas (załóżmy, że 1 odczyt na minutę)
time = 1:100;

% Wyświetlenie pierwszych 10 odczytów z szumem
disp('Pierwsze 10 odczytów temperatury z szumem:');
disp(noisy_temperature_data(1:10));
```

### **Wyjaśnienie**:
- `randn(1, 100) * 2` generuje 100 losowych wartości rozkładu normalnego z odchyleniem standardowym wynoszącym 2 (szum ±2°C).
- `noisy_temperature_data` to dane temperatury z dodanym szumem.

---

## **Krok 2: Przetwarzanie danych i wygładzanie**

Teraz, gdy mamy "zaszumione" dane, obliczymy statystyki i zastosujemy technikę wygładzania (np. średnia ruchoma) w celu ich oczyszczenia.

### **Zadanie**: Oblicz statystyki i wygładź dane za pomocą średniej ruchomej.

Skopiuj i wklej poniższy kod do MATLAB:

```matlab
% Podstawowe statystyki dla danych z szumem
mean_temp_noisy = mean(noisy_temperature_data);
median_temp_noisy = median(noisy_temperature_data);
min_temp_noisy = min(noisy_temperature_data);
max_temp_noisy = max(noisy_temperature_data);

% Wyświetlenie wyników
disp(['Średnia temperatura (z szumem): ', num2str(mean_temp_noisy)]);
disp(['Mediana temperatury (z szumem): ', num2str(median_temp_noisy)]);
disp(['Minimalna temperatura (z szumem): ', num2str(min_temp_noisy)]);
disp(['Maksymalna temperatura (z szumem): ', num2str(max_temp_noisy)]);

% Wygładzanie danych (średnia ruchoma na oknie 5 odczytów)
smoothed_temperature_data = movmean(noisy_temperature_data, 5);

% Wyświetlenie pierwszych 10 wygładzonych odczytów
disp('Pierwsze 10 wygładzonych odczytów temperatury:');
disp(smoothed_temperature_data(1:10));
```

### **Wyjaśnienie**:
- `movmean(data, window_size)` to funkcja MATLAB obliczająca średnią ruchomą z danych, z określonym rozmiarem okna (w tym przypadku 5 odczytów).

---

## **Krok 3: Porównanie i wizualizacja danych**

Stworzymy wykresy, które porównają dane zaszumione i wygładzone. Anotujemy również kluczowe punkty na wykresie (np. wartości maksymalne i minimalne).

### **Zadanie**: Stwórz wykresy i porównaj dane zaszumione oraz wygładzone.

Skopiuj i wklej poniższy kod do MATLAB:

```matlab
% Wykres temperatur zaszumionych i wygładzonych
figure;
plot(time, noisy_temperature_data, 'r-', 'DisplayName', 'Zaszumione dane');
hold on;
plot(time, smoothed_temperature_data, 'b-', 'LineWidth', 2, 'DisplayName', 'Wygładzone dane');
title('Porównanie zaszumionych i wygładzonych danych temperatury');
xlabel('Czas (minuty)');
ylabel('Temperatura (°C)');
legend show;
grid on;

% Anotowanie kluczowych punktów (wartości maksymalne i minimalne)
[max_temp_value, max_idx] = max(smoothed_temperature_data);
[min_temp_value, min_idx] = min(smoothed_temperature_data);
text(max_idx, max_temp_value, ['\leftarrow Max: ', num2str(max_temp_value)], 'Color', 'green');
text(min_idx, min_temp_value, ['\leftarrow Min: ', num2str(min_temp_value)], 'Color', 'blue');
```

### **Wyjaśnienie**:
- `plot()` tworzy wykres danych zaszumionych i wygładzonych.
- `text(x, y, label)` dodaje anotacje na wykresie, np. wskazując maksymalną i minimalną wartość temperatury.

---

## **Krok 4: Eksploracja większych zestawów danych**

Dla bardziej zaawansowanej eksploracji poproś studentów, aby:
1. Zmienili rozmiar symulowanych danych (np. 500 odczytów).
2. Porównali różne wielkości okien dla średniej ruchomej.
3. Przeanalizowali różne metody wygładzania (np. mediana ruchoma zamiast średniej ruchomej).

---

## **Podsumowanie**

W tej sesji nauczyłeś/aś się:
- Jak symulować dane z szumem.
- Jak przetwarzać i wygładzać dane przy użyciu średniej ruchomej.
- Jak tworzyć wykresy porównujące różne zestawy danych oraz anotować kluczowe punkty.

