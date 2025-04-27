# ML_endoscopy_dataset

1. Początek pliku 'budowa_krok_2_3_interpetability.ipynb' 
    a. pokazuje, że nasz początkowy model (uzyskany przy okazji w kroku 3, ale to nasz model z poprzedniego etapu) nauczony jest na pamięć, źle uogólnia i pomimo wysokich wyników (99% accuracy) nie jest możliwe praktyczne wykorzystanie
2. Plik 'budowa_krok_2_3_redundancja_danych.ipynb' 
    a. wykonana klasteryzacja
    b. dane znajdujące się w klastrach rzeczywiście identyczne (niektóre zdjęcia powielone nawet 30 razy), jednak zmniejszenie liczby zdjęć może utrudnić trenowanie (przypadek nauki na pamięć nie zostanie rozwiązany)
    c.  ponadto klasteryzacja nie zapewniła, że wybrane zdjęcia nie zawierają duplikatów
    d. jako wynik zapisane foldery output_samples, gdzie do klasteryzaci parametr eps = 5 oraz output_samples2 z parametrem eps=6.5
    e. output_samples2 bardziej zróżnicowane (w output_sampels pozostało za dużo duplikatów i nie widać róznicy w treningu modelu)
3. Plik 'budowa_krok_2_3_output_samples_test.ipynb'
    a. trening modeli na danych output_samples2 oraz referencyjnego na danych output
4. Plik 'budowa_krok_2_3_photo_area.ipynb'
    a. wycięcie fragmentów zdjęć, w przypadku klas AVM i Ulcer wycięcie fragmentu zawierającego zmianę, w przypadku Normal losowa część
    b. zmieniając radius można uzyskać różne wyniki
    c. plik cropped_out -> zawiera zdjęcia wycięte z promieniem 200 (za duży obszar brak róznicy w treningu)
    d. plik cropped_out_50 -> zawiera zdjęcia wycięte z promieniem 50 (mały obszar, model z mniejszym accuracy bo 96%, niektóre zdjęcia ciemne i niewyraźne, ciężka identyfikacja zmian w przypadku tych jaśniejszych lub bardziej rozległych)
    e.  plik cropped_out_100 -> zawiera zdjęcia wycięte z promieniem 100 (wyniki interpretacji omówione później nie są również zadowalające)
5. Plik 'budowa_krok_2_3_model_on_cropped_photos.ipynb'
    a. modele na danych uzyskanych w kroku 4
    b. do podziału na zbiory treningowe i testowe użyto klasyfikacji, aby nie usuwać podobnych zdjęć tylko zapewnić, że zdjęcia z jednego klastra znjadą się w całości w jednym zbiorze
    c. zmieniając folder wejściowy można otrzymać różne modele : wykonano model dla danych z trzech folderów z pkt 4.
6. Dalsza część pliku 'budowa_krok_2_3_interpetability.ipynb'
    a. pokazane na co zwracją uwagę modele wytrenowane na danych cropped_* (pkt 4) 
    b. wizualizacja na danych uciętych jak i pełnych obrazkach
    c. skuteczność na pełnych obrazkach nie jest dobra (klasyfikacja często błędna) -> czy można sprawdzać na pełnych??
    d. czyli żaden model nie dał zadowalającej skuteczność (rezygnując z wysokiego accuracy i tak nie uzyskaliśmy lepszych wyników)
    f. wniosek : za mało danych
7. Plik 'budowa_krok_2_3_shap_interpretability.ipynb'
    a. interpretacja modelu za pomocą biblioteki shap (dodatkowo inne spojrzenie)
    b. długi czas pracy (za długi żeby przeanalizować więcej zdjęć, lepiej po kilka losowo wybierać)
    c. potwierdziło wyniki uzysane za pomocą biblioteki lime i miejsca zmiany chorobowej czasami nawet zaznaczone na niebiesko, czyli wpływały na klasyfikację do innej klasy niż prawidłowa -> o poprawnej klasyfikacji decydowały miejsca na pograniczu obrazka i ramki (losowe?)