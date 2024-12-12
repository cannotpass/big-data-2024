### Zadanie: Symulacja systemu kolejkowego w systemie IoT

#### **Cel:**
1. Symulacja działania systemu kolejkowego, który obsługuje dane przychodzące z urządzeń IoT (np. czujników temperatury).
2. Zrozumienie, jak dane są przechowywane w kolejce i obsługiwane przez serwer.
3. Analiza obciążenia systemu i efektywności przetwarzania danych.

#### **Opis zadania:**

W tym zadaniu studenci będą symulować system kolejkowy, w którym urządzenia IoT wysyłają dane do centralnego serwera (np. o temperaturze) w sposób losowy, a serwer przetwarza te dane w kolejności, w jakiej zostały odebrane. Zaimplementujemy prostą symulację kolejkowania żądań i przetwarzania tych danych.

---

### **Krok 1: Generowanie danych (symulacja urządzeń IoT)**

1. Generujemy dane o temperaturze z różnych urządzeń IoT (np. 5 czujników). Co 1 sekundę jedno z urządzeń wysyła dane do systemu (losowa liczba z zakresu 50-150°C).

```matlab
% Liczba urządzeń IoT (czujników)
liczbaUrządzeń = 5;
czasyPrzybycia = rand(1, liczbaUrządzeń);  % Losowe czasy przybycia danych

% Generowanie danych o temperaturze w zakresie 50-150°C
daneCzujników = randi([50, 150], 1, liczbaUrządzeń);  % Temperatury (w °C)

% Wyświetlenie danych
disp('Wygenerowane dane czujników (temperatura):');
disp(daneCzujników);
```

---

### **Krok 2: Symulacja kolejkowania danych**

2. Dane przychodzą z różnych urządzeń i muszą zostać umieszczone w kolejce, gdzie będą przetwarzane przez serwer.

   Stworzymy funkcję symulującą kolejkę, w której dane będą "czekać" na przetworzenie.

```matlab
% Kolejka (pierwsze przybyłe, pierwsze przetwarzane - FIFO)
kolejka = [];

% Dodanie danych do kolejki
for i = 1:liczbaUrządzeń
    kolejka = [kolejka, daneCzujników(i)];  % Dodanie nowego żądania do kolejki
    disp(['Dodano dane czujnika ', num2str(i), ' do kolejki: ', num2str(daneCzujników(i))]);
end

disp('Zawartość kolejki:');
disp(kolejka);
```

---

### **Krok 3: Przetwarzanie danych z kolejki**

3. System serwisowy (np. serwer IoT) przetwarza dane z kolejki, jedno po drugim, w tej samej kolejności, w jakiej zostały dodane. Symulujemy ten proces przez usuwanie danych z kolejki.

```matlab
% Przetwarzanie danych z kolejki
while ~isempty(kolejka)
    przetworzonaDane = kolejka(1);  % Przetwarzanie pierwszego elementu w kolejce
    kolejka = kolejka(2:end);  % Usunięcie przetworzonego elementu
    disp(['Przetworzono dane: ', num2str(przetworzonaDane)]);
end

disp('Kolejka po przetworzeniu danych:');
disp(kolejka);
```

---

### **Krok 4: Analiza obciążenia systemu**

4. Analizujemy, ile czasu zajmuje przetworzenie wszystkich danych oraz jakie obciążenie ma system (ile danych zostało przetworzonych w jednostce czasu).

```matlab
% Symulacja czasu przetwarzania (losowy czas opóźnienia dla każdego przetwarzania)
czasyPrzetwarzania = rand(1, liczbaUrządzeń) * 2;  % Losowy czas opóźnienia (w sekundach)

% Zliczanie czasu przetwarzania
czasPrzetwarzaniaCałość = sum(czasyPrzetwarzania);  % Łączny czas przetwarzania
disp(['Czas przetwarzania wszystkich danych: ', num2str(czasPrzetwarzaniaCałość), ' sekundy']);
```

---

### **Krok 5: Optymalizacja systemu kolejkowego**

5. Propozycja rozszerzenia zadania o optymalizację, np. poprzez równoczesne przetwarzanie danych (wielowątkowość) lub dostosowanie liczby urządzeń do obciążenia systemu.

```matlab
% Symulacja optymalizacji: Zwiększanie liczby urządzeń, gdy system jest mało obciążony
if czasPrzetwarzaniaCałość < 5
    liczbaUrządzeń = liczbaUrządzeń + 2;  % Zwiększenie liczby urządzeń
    disp(['Zwiększono liczbę urządzeń do: ', num2str(liczbaUrządzeń)]);
end
```

---

### **Rozszerzenia (opcjonalne):**
1. **Symulacja serwera z ograniczeniami**: Dodanie ograniczeń dotyczących liczby danych, które mogą być przetwarzane w danym czasie (np. maksymalna liczba danych w kolejce).
2. **Zastosowanie algorytmów priorytetowych**: Implementacja algorytmu, który obsługuje dane według priorytetu (np. czujniki z krytycznymi danymi mają wyższy priorytet).
3. **Symulacja obciążenia systemu**: Analiza, jak system zachowuje się w przypadku wzrastającego obciążenia (większa liczba urządzeń IoT).

---

### **Podsumowanie:**

To zadanie pozwala zrozumieć podstawy działania systemu kolejkowego w kontekście IoT.
