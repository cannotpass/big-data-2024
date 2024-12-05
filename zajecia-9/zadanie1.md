### **Zadanie: Symulacja Systemu IoT z Regulacją Temperatury**  

#### **Cel:**  
Zasymulowanie systemu monitorowania temperatury w trzech pomieszczeniach z wbudowanym regulatorem, który aktywuje się w momencie przekroczenia zakresu temperatury.  

#### **Opis:**  
1. Symuluj temperatury dla 3 pomieszczeń (np. salon, kuchnia, sypialnia).  
   - Temperatury powinny się zmieniać dynamicznie, na przykład na skutek losowych wahań (np. zmiany w porach dnia).  
2. Określ zakres temperatury: np. **18–26°C**.  
3. Stwórz **regulator**, który działa na zasadzie prostego sterowania:  
   - Jeśli temperatura spadnie poniżej 18°C → regulator podgrzewa pomieszczenie.  
   - Jeśli temperatura wzrośnie powyżej 26°C → regulator chłodzi pomieszczenie.  
4. Symulacja powinna działać przez określony czas (np. 24 godziny), a wyniki działania systemu (temperatury, włączenia regulatora) powinny być wizualizowane.

---

#### **Instrukcja:**  

1. **Generowanie danych temperatury:**  
   - Użyj generatora temperatur, który uwzględnia losowe fluktuacje (np. sinusoidalna zmiana w ciągu dnia z dodatkiem szumu losowego).  

2. **Regulacja temperatury:**  
   - W momencie wykrycia odchylenia od normy, regulator powinien zmieniać temperaturę w następnym kroku czasowym, aby przywrócić ją do normy.  

3. **Wizualizacja:**  
   - Pokaż wykres zmiany temperatury dla każdego pomieszczenia, z zaznaczeniem momentów, kiedy regulator działał (np. kolorowe punkty na wykresie).  

---

#### **Przykładowy kod MATLAB:**  
```matlab
% Parametry symulacji
num_rooms = 3; % Liczba pomieszczeń
time_hours = 24; % Liczba godzin do symulacji
temp_min = 18; % Minimalna dopuszczalna temperatura
temp_max = 26; % Maksymalna dopuszczalna temperatura
time_steps = time_hours; % Jeden krok na godzinę

% Generowanie początkowych temperatur
temperature_data = 20 + 5 * sin((1:time_steps) * 2 * pi / 24) + randn(time_steps, num_rooms);

% Tablica do śledzenia włączeń regulatora
heating = zeros(time_steps, num_rooms);
cooling = zeros(time_steps, num_rooms);

% Regulator
for t = 2:time_steps
    for room = 1:num_rooms
        if temperature_data(t-1, room) < temp_min
            % Podgrzewanie
            temperature_data(t, room) = temperature_data(t-1, room) + 1.5;
            heating(t, room) = 1; % Włączenie regulatora
        elseif temperature_data(t-1, room) > temp_max
            % Chłodzenie
            temperature_data(t, room) = temperature_data(t-1, room) - 1.5;
            cooling(t, room) = 1; % Włączenie regulatora
        else
            % Naturalne zmiany temperatury
            temperature_data(t, room) = temperature_data(t-1, room) + randn * 0.5;
        end
    end
end

% Wizualizacja
room_names = {'Salon', 'Kuchnia', 'Sypialnia'};
figure;
hold on;
for room = 1:num_rooms
    plot(1:time_steps, temperature_data(:, room), 'LineWidth', 1.5, 'DisplayName', room_names{room});
    scatter(find(heating(:, room)), temperature_data(heating(:, room) == 1, room), ...
        50, 'r', 'filled', 'HandleVisibility', 'off');
    scatter(find(cooling(:, room)), temperature_data(cooling(:, room) == 1, room), ...
        50, 'b', 'filled', 'HandleVisibility', 'off');
end
yline(temp_min, '--', 'Min Temp', 'Color', 'g');
yline(temp_max, '--', 'Max Temp', 'Color', 'm');
xlabel('Czas [godziny]');
ylabel('Temperatura [°C]');
title('Symulacja regulacji temperatury w pomieszczeniach');
legend('show');
grid on;
hold off;

% Wyświetlenie statystyk regulatora
disp('Działanie regulatora:');
for room = 1:num_rooms
    fprintf('%s: Podgrzewanie = %d razy, Chłodzenie = %d razy\n', ...
        room_names{room}, sum(heating(:, room)), sum(cooling(:, room)));
end
```

---

#### **Wyniki Symulacji:**  
1. Wykres przedstawia:  
   - Zmiany temperatur w czasie dla każdego pomieszczenia.  
   - Punkty, w których działał regulator (czerwone dla podgrzewania, niebieskie dla chłodzenia).  
2. W konsoli MATLAB-a wyświetlane są statystyki: liczba włączeń podgrzewania i chłodzenia dla każdego pomieszczenia.  

---

#### **Dodatkowe zadania:**  
1. Zmodyfikuj działanie regulatora, aby był bardziej precyzyjny (np. stopniowe zbliżanie się do normy).  
2. Dodaj nowy parametr: koszt energii zużytej przez regulator w zależności od liczby jego włączeń.  
3. Zaimplementuj możliwość symulacji różnych warunków zewnętrznych (np. nagłe spadki temperatury nocą).  
