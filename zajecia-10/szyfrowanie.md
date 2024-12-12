### Zadanie: Symulacja czujnika IoT, szyfrowanie danych, zapis do pliku CSV, odszyfrowanie danych

#### **Cel:**
1. Symulacja danych czujnika IoT (np. pomiarów temperatury gazu).
2. Szyfrowanie danych przy użyciu algorytmu AES.
3. Zapisanie zaszyfrowanych danych do pliku CSV.
4. Odczytanie danych z pliku, odszyfrowanie i ich wyświetlenie.

#### **Opis zadania:**

W tym zadaniu stworzysz prostą symulację czujnika, który generuje dane (np. temperatury w zakresie 50-150°C). Następnie dane te zostaną zaszyfrowane za pomocą algorytmu AES, zapisane do pliku CSV i odszyfrowane w późniejszym kroku. Zadanie pozwoli zrozumieć, jak dane czujników IoT mogą być chronione przed nieautoryzowanym dostępem.

---

### **Krok 1: Generowanie danych czujnika (symulacja)**

1. Generujemy losowe dane (temperatury czujnika) w zakresie 50-150°C.
2. Przechowujemy te dane w tabeli MATLAB.

```matlab
% Generowanie danych - 10 próbek
temperatura = randi([50, 150], 1, 10);  % Temperatura w zakresie 50-150°C

% Wyświetlenie danych
disp('Wygenerowane dane czujnika:');
disp(temperatura);
```

---

### **Krok 2: Szyfrowanie danych**

1. Szyfrujemy dane przy użyciu algorytmu AES.
2. Klucz szyfrowania (16 znaków) oraz wektor inicjalizacji (16 znaków) są używane w procesie szyfrowania.

```matlab
% Klucz i wektor inicjalizacji
key = 'moje_tajna_haslo';  % Klucz szyfrowania (16 znaków)
iv = 'inicjalizacja_iv';   % Wektor inicjalizacji (16 znaków)

% Szyfrowanie danych
szyfrowaneDane = matlab.security.Cryptography.encrypt(temperatura, key, iv);

% Wyświetlenie zaszyfrowanych danych
disp('Zaszyfrowane dane:');
disp(szyfrowaneDane);
```

---

### **Krok 3: Zapisanie zaszyfrowanych danych do pliku CSV**

1. Zapisujemy zaszyfrowane dane do pliku CSV, gdzie każda zaszyfrowana próbka będzie w osobnej komórce.

```matlab
% Zapisanie zaszyfrowanych danych do pliku CSV
writematrix(szyfrowaneDane, 'dane_czujnika_zaszyfrowane.csv');

disp('Zaszyfrowane dane zapisane do pliku CSV.');
```

---

### **W NOWYM PLIKU MATLAB:**

### **Krok 4: Odczytanie zaszyfrowanych danych z pliku CSV**

1. Odczytujemy dane z pliku CSV, które zostały zapisane w poprzednim kroku.

```matlab
% Wczytanie zaszyfrowanych danych z pliku CSV
daneZPliku = readmatrix('dane_czujnika_zaszyfrowane.csv');

disp('Zaszyfrowane dane wczytane z pliku:');
disp(daneZPliku);
```

---

### **Krok 5: Odszyfrowanie danych**

1. Odszyfrowujemy dane za pomocą tego samego klucza i wektora inicjalizacji, które zostały użyte do szyfrowania.
2. Wyświetlimy oryginalne dane po odszyfrowaniu.

```matlab
% Odszyfrowanie danych
odszyfrowaneDane = matlab.security.Cryptography.decrypt(daneZPliku, key, iv);

% Wyświetlenie odszyfrowanych danych
disp('Odszyfrowane dane:');
disp(odszyfrowaneDane);
```

---

### **Krok 6: Porównanie danych**

1. Sprawdzamy, czy dane przed szyfrowaniem i po odszyfrowaniu są identyczne.

```matlab
% Porównanie danych przed i po odszyfrowaniu
if isequal(temperatura, odszyfrowaneDane)
    disp('Dane zostały poprawnie odszyfrowane.');
else
    disp('Błąd w procesie odszyfrowywania.');
end
```

---

### **Rozszerzenie (opcjonalne):**
1. **Symulacja ataków na dane** – zaprezentowanie, co się stanie, jeśli ktoś będzie miał dostęp do zaszyfrowanych danych, ale nie zna klucza.
2. **Generowanie kluczy dynamicznych** – implementacja generowania kluczy szyfrowania w systemie IoT (np. na podstawie danych urządzenia).
3. **Dodanie podpisu cyfrowego** – dodatkowe zabezpieczenie, które pozwoli upewnić się, że dane nie zostały zmodyfikowane w trakcie przesyłania.

---

### **Podsumowanie:**

To zadanie pokazuje, jak można zabezpieczyć dane czujników IoT przed nieautoryzowanym dostępem za pomocą szyfrowania. Użycie kluczy szyfrowania i wektorów inicjalizacji pozwala na skuteczną ochronę danych przed atakami.