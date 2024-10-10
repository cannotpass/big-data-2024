# Zadanie
## Mapa plików, lokalna baza danych

Problemem do rozwiązania jest składowanie ogromnej ilości plików w jednym folderze, potrafi to zwolnić system i ograniczyć jej możliwości. 

Użytkownik ma za zadanie umieszczać pliki w katalogu wejściowym.

Program po uruchomieniu powinien mapować plik do podanej przez użytkownika nazwy, a później przenosić plik do specjalnego katalogu i zapisywać mapowanie. Użytkownik może uruchomić drugi program, który pozwoli mu wczytać zawartość wybranego pliku.
Program będzie składał się z dwóch skryptów. Ma za zadanie tworzyć bazę danych katalogów oraz plików i dbać o to, żeby katalogi były podobnej wielkości, a co za tym idzie wydajność i dostęp do plików nie był ograniczany.

W normalnym środowisku działa to trochę inaczej, jednak sama idea tworzenia drzewa katalogów jest wykorzystywana powszechnie w branży (np. sieć katalogów systemu kontroli wersji GIT). Mapy, zwane też tablicami asocjacyjnymi, dzięki szybkości działania, są jednymi z najczęściej wykorzystywanych struktur danych, które są spotykane w większości języków programowania i większości projektów programistycznych.

## Wstęp
1. Stwórz nowy projekt w MATLAB.
2. Stwórz dwa katalogi w wybranym katalogu roboczym (w którym będzie znajdował się
Twój skrypt), jeden nazwij „pliki_wejsciowe”, drugi „pliki wyjsciowe”.
3. W katalogu pliki_wejsciowe stwórz 3 pliki tekstowe, z których każdy będzie miał inną
nazwę i inną zawartość (przynajmniej 3 linijki tekstu, mogą być krótkie).

## Skrypt saver.m :
1. Zdefiniujmy dwa katalogi, które będą wykorzystywane w programie.
```
input_folder = ‘pliki_wejsciowe’;
output_folder = ‘pliki_wyjsciowe’;
```
2. Stwórzmy strukturę, która będzie zwierała w sobie informacje o strukturze katalogu roboczego:
```
input_files = dir(input_folder);
```
3. Jeżeli istnieje już plik z mapą przechowującą informację o położeniu przetworzonych plików wczytajmy go, jeśli nie, stwórzmy nowy obiekt mapy.
```
if exist(‘files_map.mat’, ‘dir’)
    files_map = load(“files_map.mat”);
else
    files_map = containers.Map;
end
```
4. Dla wszystkich plików w naszym katalogu „pliki_wejsciowe” wykonajmy następujące instrukcje:
```
for n = 1:numel(input_files)
    fname = string(input_files(n).name);
    if fname ~= “.” && fname ~= “..”
        fpath = fullfile(input_folder, fname);
        prompt = strcat(“To which name I should map:”, fpath, “? “);
        map_key = string(input(prompt, “s”));
        if isKey(files_map, map_key)
            error(“Key {“ + map_key + “} is already taken, retart the program.”)
        end
        [y,m,d] = ymd(datetime(“today”));
        file_path = generate_file_path(output_folder, y, m. d, fname);
        movefile(fpath, file_path);
        files_map(map_key) = file_path;
        save(“files_map.mat”, ‘files_map’)
    end
end
```
5. Stwórz funkcję, która wygeneruje ścieżkę do zapisu pliku:
```
function fp = generate_file_path(output_base_folder, y, m, d, n)
    fp = output_base_folder;
    forelem=[y,m,d,n]
        fp = fullfule(fp, elem);
        if (elem ~= n) && (~exists(fp, ‘dir’))
            mkdir(fp)
        end
    end
end
```

## Skrypt loader.m :
1. Wczytaj istniejącą mapę plików:
```
saved_map = load(„files_map.mat”);
```
2. Odczytaj klucze i wartości z mapy:
```
k = keys(files_map);
val = values(files_map);
```
3. Zapytaj użytkownika, który plik chce wczytać
```
disp(“Which file should I load? (type a number)”);
```
4. Wyświetl listę wszystkich dostępnych plików
```
for i = 1:length(files_map)
    fprintf(“%d - %s | %s\n”, i, k{i}, val{i})
end
```
5. Pobierz wybór użytkownika:
```
selection = input(“Enter number: “);
```
6. Wybierz ścieżkę do odpowiedniego pliku:
```
file_path = string(val(selection));
```
7. Wczytaj zawartość pliku oraz ją wyświetl
```
content = readlines(file_path);
disp(content);
```

## Zadania do zrealizowania indywidualnie:
Przerób program tak, żeby w przypadku podania już zajętej nazwy do mapy, prosił użytkownika o podanie nowej nazwy tak długo aż użytkownik nie wpisze poprawnej, lub nie wpisze QUIT. Ostrzeż użytkownika, że QUIT jest słowem, które kończy działanie programu.

Na podstawie skryptu saver.m zmodyfikuj skrypt loader.m w taki sposób, żeby nie kończył się błędem, jeżeli plik z mapą (files_map.mat) nie istanieje, a jedynie informował o tym użytkownika i kończył działanie.