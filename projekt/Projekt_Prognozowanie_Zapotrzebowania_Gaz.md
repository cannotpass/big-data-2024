
# Prognozowanie zapotrzebowania na gaz ziemny z wykorzystaniem analizy szeregów czasowych

## Opis projektu
Celem projektu jest opracowanie modelu predykcyjnego do prognozowania przyszłego zapotrzebowania na gaz ziemny, bazując na analizie danych szeregów czasowych. Zadanie polega na zastosowaniu różnych metod prognozowania w środowisku MATLAB w celu przewidzenia przyszłych wartości zapotrzebowania na podstawie historycznych danych. Studenci będą musieli przeanalizować dane, przetestować różne techniki predykcyjne oraz przedstawić wyniki w formie przystępnej dla zarządu firmy.

Należy przeanalizować znajdujące się w repozytorium dane dla rynku amerykańskiego, które zawierają miesięczne wartości.
Należy dodatkowo przeanalizować dane na poziomie stanów w celu końcowego przetestowania wybranych metod przewidywania.

## Wymagania
1. **Sposób dostarczenia:**  
   - Wyniki i wnioski powinny zostać przedstawione w formie raportu, prezentacji (np. PowerPoint), albo arkusza kalkulacyjnego (Excel), przygotowanego tak, aby był zrozumiały dla zarządu firmy, który nie musi posiadać wiedzy technicznej.  
   - W prezentacji lub raporcie należy jasno wyjaśnić zastosowane metody, wyniki oraz rekomendacje.

2. **Wstępna analiza**
   - Na wstępie naley przeprowadzić analizę eksploracyjną danych. Należy zbadać:
     - Trendy i sezonowość w danych
     - Wartości odstające i brakujące dane
     - Korelacje między zmiennymi
   - Wyniki analizy powinny być przedstawione w formie wykresów i tabel.

3. **Przegląd metod prognozowania:**  
   - Należy przetestować co najmniej 4 różne metody prognozowania. Przykładowe metody to:
     - Wygładzanie wykładnicze (np. metoda Holta-Wintersa)
     - Model autoregresji (ARIMA)
     - Sieci neuronowe do prognozowania szeregów czasowych
     - Drzewa decyzyjne lub inne techniki uczenia maszynowego
   - Każda z metod powinna być przystępnie opisana, a wyniki prognoz przedstawione graficznie.

3. **Obliczenia błędów prognoz:**  
   - Prognozy powinny być przeprowadzone dla okresu od 2015 roku (model uczony na wybranym zakresie danych do 2015, przewidywania dla lat kolejnych).
   - Dla każdej metody należy obliczyć błędy prognoz, takie jak:
     - Średni błąd absolutny (MAE)
     - Średni kwadratowy błąd (MSE)
     - Średni procentowy błąd bezwzględny (MAPE)
   - Wyniki błędów prognoz powinny być porównane w celu oceny dokładności poszczególnych metod.

4. **Analiza wyników i rekomendacje:**  
   - Na podstawie uzyskanych wyników należy sformułować rekomendacje dotyczące najlepszej metody prognozowania, wraz z uzasadnieniem.
   - Wskazać potencjalne korzyści biznesowe wynikające z zastosowania wybranego modelu oraz omówić ograniczenia i ewentualne ryzyko związane z prognozowaniem.
   - Dodatkowo, można pokusić się o analizę potencjalnych kosztów błędu.

5. **Wizualizacja danych:**  
   - Należy przedstawić dane historyczne oraz prognozowane w formie wykresów.
   - Wyniki poszczególnych metod prognozowania muszą być przedstawione na jednym wykresie w celu łatwego porównania.

6. **Opis zastosowanego podejścia:**  
   - Szczegółowo opisać proces przygotowania danych, w tym ich wstępne przetwarzanie, usuwanie brakujących wartości, agregację i normalizację - tutaj chodzi o spisanie kroków, a nie ich szczegółowy opis, np. dane zostały podzielone przez 20, potem dodano do nich 120, a nie "dane zostały przetworzone". 

7. **Wnioski:**  
   - Podsumowanie kluczowych obserwacji oraz wyciągniętych wniosków.
   - Ocena wpływu wybranej metody prognozowania na potencjalne decyzje biznesowe.

## Przewidywany rezultat
Projekt ma na celu nie tylko przygotowanie prognoz, ale także rozwinięcie umiejętności analitycznych, nauczenie krytycznego myślenia i podejmowania decyzji na podstawie danych.

Finalny rezultat powinien być zrozumiały dla zarządu firmy i wskazywać konkretne kroki, które można podjąć w celu optymalizacji zarządzania zapotrzebowaniem na gaz.

## Dane pochodzą z ogólnodostępnych źródeł
https://www.eia.gov/dnav/ng/ng_cons_sum_a_EPG0_VC0_mmcf_a.htm