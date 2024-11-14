% Załadowanie danych (np. zbiór Iris)
# Zadanie 1: Klasyfikacja danych iris

W tym zadaniu będziemy korzystać z różnych algorytmów klasyfikacji, aby przewidzieć gatunki irysów na podstawie cech kwiatów. Wykorzystamy trzy algorytmy: K-Nearest Neighbors (KNN), Drzewo Decyzyjne oraz Maszynę Wektorów Nośnych (SVM). Następnie ocenimy ich skuteczność.

## Przygotowanie danych

```matlab
load fisheriris;

% Przygotowanie danych
X = meas;  % cechy
Y = species;  % etykiety klas
```

## Podział danych na zbiór treningowy i testowy

Podzielimy dane na zbiór treningowy (70%) i testowy (30%).

```matlab
cv = cvpartition(length(Y), 'HoldOut', 0.3);
X_train = X(training(cv), :);
Y_train = Y(training(cv));
X_test = X(test(cv), :);
Y_test = Y(test(cv));
```

## Trening modeli

### 1. K-Nearest Neighbors (KNN)

```matlab
knn_model = fitcknn(X_train, Y_train);
knn_pred = predict(knn_model, X_test);
```

### 2. Drzewo Decyzyjne (Decision Tree)

```matlab
tree_model = fitctree(X_train, Y_train);
tree_pred = predict(tree_model, X_test);
```

### 3. Maszyna Wektorów Nośnych (SVM)

```matlab
svm_model = fitcsvm(X_train, Y_train);
svm_pred = predict(svm_model, X_test);
```

## Funkcja do obliczenia metryk

Stworzymy funkcję, która obliczy accuracy, recall i specificity dla każdego modelu.

```matlab
function [accuracy, recall, specificity] = evaluate_model(y_true, y_pred)
    % Obliczanie macierzy pomyłek
    cm = confusionmat(y_true, y_pred);
    
    % Liczba klas
    num_classes = size(cm, 1);
    
    % Obliczanie accuracy
    accuracy = sum(diag(cm)) / sum(cm(:));
    
    % Obliczanie recall (czułość) i specificity (specyficzność)
    recall = zeros(1, num_classes);
    specificity = zeros(1, num_classes);
    
    for i = 1:num_classes
        TP = cm(i,i);  % True Positives
        FN = sum(cm(i,:)) - TP;  % False Negatives
        FP = sum(cm(:,i)) - TP;  % False Positives
        TN = sum(cm(:)) - TP - FN - FP;  % True Negatives
        
        recall(i) = TP / (TP + FN);  % Czułość
        specificity(i) = TN / (TN + FP);  % Specyficzność
    end
end
```

## Ocena modeli

Ocenimy każdy model, obliczając accuracy, recall i specificity.

```matlab
fprintf('Model: KNN\n');
[knn_accuracy, knn_recall, knn_specificity] = evaluate_model(Y_test, knn_pred);
fprintf('Accuracy: %.2f\n', knn_accuracy);
fprintf('Recall: %.2f, %.2f, %.2f\n', knn_recall(1), knn_recall(2), knn_recall(3));
fprintf('Specificity: %.2f, %.2f, %.2f\n\n', knn_specificity(1), knn_specificity(2), knn_specificity(3));

fprintf('Model: Decision Tree\n');
[tree_accuracy, tree_recall, tree_specificity] = evaluate_model(Y_test, tree_pred);
fprintf('Accuracy: %.2f\n', tree_accuracy);
fprintf('Recall: %.2f, %.2f, %.2f\n', tree_recall(1), tree_recall(2), tree_recall(3));
fprintf('Specificity: %.2f, %.2f, %.2f\n\n', tree_specificity(1), tree_specificity(2), tree_specificity(3));

fprintf('Model: SVM\n');
[svm_accuracy, svm_recall, svm_specificity] = evaluate_model(Y_test, svm_pred);
fprintf('Accuracy: %.2f\n', svm_accuracy);
fprintf('Recall: %.2f, %.2f, %.2f\n', svm_recall(1), svm_recall(2), svm_recall(3));
fprintf('Specificity: %.2f, %.2f, %.2f\n\n', svm_specificity(1), svm_specificity(2), svm_specificity(3));
```

## Wyświetlanie macierzy pomyłek

Wyświetlimy macierze pomyłek dla każdego modelu.

```matlab
figure;
subplot(1,3,1);
confusionchart(Y_test, knn_pred);
title('KNN Confusion Matrix');

subplot(1,3,2);
confusionchart(Y_test, tree_pred);
title('Decision Tree Confusion Matrix');

subplot(1,3,3);
confusionchart(Y_test, svm_pred);
title('SVM Confusion Matrix');
```
