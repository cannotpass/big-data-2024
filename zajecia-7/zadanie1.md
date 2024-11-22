### Zadanie: Klasteryzacja danych przy użyciu trzech popularnych algorytmów

**Cel zadania:**
Celem tego zadania jest zapoznanie się z trzema popularnymi algorytmami klasteryzacji: DBSCAN, hierarchiczną klasteryzacją oraz k-means. W ramach ćwiczenia studenci nauczą się, jak zaimplementować te algorytmy w MATLABie oraz jak analizować i interpretować wyniki.

---

### 1. **Wstęp teoretyczny**

#### **a) K-means (K-średnich)**

Algorytm K-means jest jednym z najpopularniejszych algorytmów klasteryzacji. Działa on na zasadzie podziału zbioru danych na `k` klastrów, które minimalizują sumę kwadratów odległości punktów do centrów klastrów. Algorytm jest iteracyjny i składa się z dwóch głównych kroków:

- **Przypisanie punktów**: Każdy punkt danych przypisywany jest do klastra, którego centrum (średnia) jest najbliższe.
- **Aktualizacja centrów**: Centrum klastra jest aktualizowane do średniej punktów przypisanych do tego klastra.

Algorytm wymaga wcześniejszego określenia liczby klastrów (`k`).

#### **b) DBSCAN (Density-Based Spatial Clustering of Applications with Noise)**

DBSCAN jest algorytmem klasteryzacji opartym na gęstości. Jego główną zaletą jest to, że nie wymaga określenia liczby klastrów z góry. Działa w następujący sposób:

- Punkty danych klasyfikowane są jako **rdzenne**, **osiowe** lub **szum**.
- Punkty rdzenne mają wystarczającą liczbę sąsiednich punktów w zadanym promieniu (parametr `epsilon`).
- Punkty osiowe są bliskie punktom rdzeniowym, ale nie mają wystarczającej liczby sąsiadów, aby same być punktami rdzeniowymi.
- Punkty, które nie należą do żadnej z powyższych kategorii, są uznawane za szum.

Zaletą DBSCAN jest to, że jest odporny na różne kształty klastrów i jest w stanie wykrywać szum.

#### **c) Hierarchiczna klasteryzacja**

Hierarchiczna klasteryzacja tworzy strukturę drzewa (dendrogram) przedstawiającą hierarchię klastrów. Istnieją dwa główne podejścia:

- **Agregacyjne (bottom-up)**: Zaczyna się od traktowania każdego punktu jako osobnego klastra i łączy je w większe klastry, aż do osiągnięcia jednego dużego klastra.
- **Dzielące (top-down)**: Rozpoczyna się od jednego dużego klastra i stopniowo dzieli go na mniejsze.

W tej metodzie nie musimy ustalać liczby klastrów z góry, ponieważ decyzję o liczbie klastrów podejmuje się na podstawie cięcia dendrogramu.

---

### 2. **Opis zadania**

#### **Zadanie 1: Przygotowanie danych**
W pierwszym kroku stwórzmy przykładowy zbiór danych, który będziemy klasteryzować. Skorzystaj z funkcji `make_blobs` w MATLABie, która generuje sztuczne dane w formie punktów podzielonych na klastry.

```matlab
% Generowanie przykładowych danych
rng(42); % Ustalenie ziarna generatora liczb losowych dla powtarzalności
[X, Y] = make_blobs(100, 2, 3); % 100 punktów w 2 wymiarach, 3 klastry
```

#### **Zadanie 2: K-means**
Zastosuj algorytm k-means do danych, aby podzielić je na 3 klastry. Wykorzystaj funkcję `kmeans` w MATLABie.

```matlab
% Klasteryzacja przy użyciu k-means
k = 3; % Liczba klastrów
[idx_kmeans, C] = kmeans(X, k);

% Wizualizacja wyników
figure;
scatter(X(:,1), X(:,2), 20, idx_kmeans, 'filled');
hold on;
scatter(C(:,1), C(:,2), 100, 'x', 'LineWidth', 2); % Centra klastrów
title('Klasteryzacja k-means');
xlabel('X1');
ylabel('X2');
```

#### **Zadanie 3: DBSCAN**
Teraz zastosuj algorytm DBSCAN. Użyj funkcji `dbscan` w MATLABie i spróbuj różnych wartości parametrów `epsilon` oraz `MinPts`.

```matlab
% Klasteryzacja przy użyciu DBSCAN
epsilon = 1.0;  % Promień sąsiedztwa
MinPts = 5;     % Minimalna liczba punktów w sąsiedztwie
[idx_dbscan] = dbscan(X, epsilon, MinPts);

% Wizualizacja wyników
figure;
scatter(X(:,1), X(:,2), 20, idx_dbscan, 'filled');
title('Klasteryzacja DBSCAN');
xlabel('X1');
ylabel('X2');
```

#### **Zadanie 4: Hierarchiczna klasteryzacja**
Zastosuj hierarchiczną klasteryzację i zwizualizuj dendrogram za pomocą funkcji `linkage` oraz `dendrogram`.

```matlab
% Klasteryzacja hierarchiczna
Z = linkage(X, 'ward');  % 'ward' – metoda minimalizacji wariancji
figure;
dendrogram(Z);
title('Dendrogram hierarchicznej klasteryzacji');
```

#### **Zadanie 5: Analiza wyników**

1. Porównaj wyniki trzech algorytmów klasteryzacji. Zastanów się, jak różnią się one pod względem jakości klasteryzacji oraz ich odporności na szum.
2. Spróbuj różnych wartości parametrów (`k` w k-means, `epsilon` i `MinPts` w DBSCAN), aby zobaczyć, jak wpływają na wyniki klasteryzacji.
3. Jakie są główne zalety i wady każdego z algorytmów? Kiedy który z nich może być szczególnie użyteczny?

---

### 3. **Wskazówki**

- Upewnij się, że masz odpowiednie narzędzia w MATLABie, takie jak `Statistics and Machine Learning Toolbox` (dla funkcji k-means i DBSCAN) oraz funkcje do hierarchicznej klasteryzacji (np. `linkage`, `dendrogram`).
- Warto przeprowadzić eksperymenty z różnymi parametrami, aby zobaczyć, jak zmieniają się wyniki.

### 4. **Podsumowanie**

W zadaniu zastosowano umiejętności dotyczące:
- Stosowania algorytmów klasteryzacji w praktycznych przykładach,
- Porównywania wyników różnych algorytmów,
- Rozumienia, kiedy i jak zastosować różne metody klasteryzacji w zależności od charakterystyki danych.