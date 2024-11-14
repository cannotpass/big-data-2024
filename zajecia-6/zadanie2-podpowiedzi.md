% Wczytanie i przygotowanie danych ("adult")
% (Zmienna 'X' to cechy, 'Y' to etykiety klas)

#tu wczytaj dane z pliku adult.data

% Sprawdzenie brakujących danych
summary(X);

% Normalizacja cech numerycznych
X = normalize(X);

% Kodowanie zmiennych kategorycznych (jeśli dotyczy)
% X = dummyvar(categorical(X));  % Przykład dla kategorycznych cech

% Podział danych na zbiór treningowy i testowy
cv = cvpartition(length(Y), 'HoldOut', 0.3);
X_train = X(training(cv), :);
Y_train = Y(training(cv));
X_test = X(test(cv), :);
Y_test = Y(test(cv));

% Grid Search dla KNN
knn_opts = optimizableVariable('NumNeighbors', [1, 50], 'Type', 'integer');
knn_model = fitcknn(X_train, Y_train, 'OptimizeHyperparameters', 'auto', ...
    'HyperparameterOptimizationOptions', struct('Optimizer', 'gridsearch'));

% Grid Search dla drzewa decyzyjnego
tree_opts = optimizableVariable('MaxDepth', [5, 50], 'Type', 'integer');
tree_model = fitctree(X_train, Y_train, 'OptimizeHyperparameters', 'auto', ...
    'HyperparameterOptimizationOptions', struct('Optimizer', 'gridsearch'));

% Grid Search dla SVM
svm_opts = optimizableVariable('BoxConstraint', [0.1, 10], 'Type', 'real');
svm_model = fitcsvm(X_train, Y_train, 'OptimizeHyperparameters', 'auto', ...
    'HyperparameterOptimizationOptions', struct('Optimizer', 'gridsearch'));

% Predykcja i ocena dla każdego modelu
knn_pred = predict(knn_model, X_test);
tree_pred = predict(tree_model, X_test);
svm_pred = predict(svm_model, X_test);

% Obliczanie metryk: accuracy, precision, recall, specificity
% (Analogiczne jak w poprzednim zadaniu)

% Wyświetlanie macierzy pomyłek i porównanie wyników
