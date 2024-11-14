Tytuł zadania: Zaawansowana klasyfikacja z optymalizacją i obróbką danych.
# Opis

Twoim zadaniem jest stworzenie modelu klasyfikacji na rozszerzonym zbiorze danych. W tym zadaniu wykonasz następujące kroki:

## Przygotowanie danych

1. Na podstawie zbioru danych adult: https://archive.ics.uci.edu/dataset/2/adult (pliki w folderze 'adult')
2. Sprawdź, czy w danych występują brakujące wartości i odpowiednio je przetwórz (np. imputation, usunięcie).
3. Wykonaj normalizację/standaryzację cech numerycznych, aby wszystkie cechy miały porównywalną skalę.
4. Jeśli w zbiorze znajdują się zmienne kategoryczne, przeprowadź odpowiednie kodowanie (np. One-Hot Encoding).

## Optymalizacja hiperparametrów

Wykorzystaj Grid Search lub Random Search do znalezienia najlepszych hiperparametrów dla trzech algorytmów:

- **KNN** – dobór odpowiedniego parametru K oraz metryki odległości (np. Euclidean, Minkowski).
- **Drzewo decyzyjne** – wybór maksymalnej głębokości drzewa oraz innych hiperparametrów.
- **SVM** – dobór jądra (linear, poly, rbf) oraz parametrów C i gamma.

## Podział danych

Podziel dane na zbiór treningowy i testowy (np. 70% na trening, 30% na testy).

## Budowanie modeli

1. Zbuduj modele KNN, Decision Tree oraz SVM, używając optymalnych hiperparametrów uzyskanych w poprzednim kroku.
2. Przeprowadź klasyfikację na zbiorze testowym.

## Ocena modeli

Oblicz i porównaj metryki klasyfikacji, takie jak:

- Accuracy (dokładność)
- Precision (precyzja)
- Recall (czułość)
- Specificity (specyficzność)
- F1-score – średnia harmoniczna precyzji i czułości

Wybierz odpowiednią metrykę do oceny wydajności modelu w kontekście problemu (np. czy lepsza jest precyzja, czy recall).

## Macierz pomyłek

Wyświetl macierz pomyłek (confusion matrix) dla każdego z modelów.

## Wykresy

Zaimplementuj wykresy porównujące wyniki dla wszystkich trzech modeli (np. wykresy Precision-Recall, ROC curve, porównanie metryk).

## Dodatkowe wymagania

- **Eksperyment z hiperparametrami**: Pokaż, jak zmiana wartości parametrów (np. liczba sąsiadów w KNN lub wartość C w SVM) wpływa na wyniki.
- **Optymalizacja**: Pokaż, jak optymalizacja hiperparametrów wpływa na końcowy wynik klasyfikacji.
- **Kroki obróbki danych**: Zademonstruj, jak różne techniki obróbki danych (np. normalizacja vs. standaryzacja) mogą wpływać na wyniki klasyfikacji.
- **Analiza wyników**: Na podstawie wyników z różnych modeli i metryk dokonaj analizy, który model jest najlepszy w danym przypadku i dlaczego.