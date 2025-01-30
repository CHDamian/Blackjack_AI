# Blackjack_AI

Blacjack to popularna gra kasynowa, polegająca na uzyskaniu jak największej liczby punktów z dobranych kart, jednocześnie nie przekraczając wyniku 21. Jednakże przez te wszystkie lata matematycy stworzyli wiele strategii, pozwalających na znaczne zwiększenie szansy na wygranie, mimo dużej losowości. Zostało to na tyle przerobione, że kasyna uważnie analizują ruchy wykonywane przez graczy, rozpoznając, kto jest dla nich zagrożeniem, pozbywając się ich poprzez przerywanie im gier.

# Opis projektu

Celem projektu była symulacja rozgrywki, podając graczom wytrenowaną sieć neuronową jako algorytm sztucznej inteligencji. Do tego wykorzystałem strategie Hi-Low. Polega ona na klasyfikacji pojawiających się kart, w zależności, czy są one lepsze dla gracza, czy dla dealera. Szczegóły:
- Karty od 2 do 6 są lepsze dla dealera, stąd ich wartość przypisujemy + 1
- Karty od 7 do 9 są neutralne i nie mają żadnego większego wpłypu (wartość 0)
- Karty od 10 do A są lepsze dla gracza, stąd mają wartość -1

Wraz z pojawianiem się nowych kart na stole należy zsumować wartość wszystkich kart, co oznaczamy jako wartość prawdziwą. Jeżeli wartość ta jest dodatnia, wiadomo, że w talii znajduje się więcej kart lepszych dla gracza i odwrotnie. Do tego by ułatwić decyzje przy konkretnej sytuacji, powstały spisy ruchów w postaci tabel, co można przeczytać tutaj wraz z dokładniejszym opisem strategii: https://pl.wikipedia.org/wiki/Blackjack

# Algorytm
Jak model AI wykorzystałem sieć neuronową. Zamiast jednak skorzystać z gotowej biblioteki (jak np. PyTorch) użyłem modelu opisanego w książce "Python, Uczenie maszynowe w przykładach." autorstwa Yuxi (Hayden) Liu. Dane wejściowe reprezentują kolejno:
- Liczba punktów za karty w ręce
- Karta dealera
- Czy w ręce znajduje się AS, który jest teraz wart 11 pkt
- Wartość prawdziwa
Natomiast wyjście:
- Hit (dobrać karte)
- Stand (pass)
Są to podstawowe ruchy, jakie gracz może wykonać, ale nie jedyne. Poza nimi jest double down (dobranie jednej karty w ciemno, podwajając stawke), oraz split (w przypadku posiadania tych samych kart, można je rozdzielić i grać dwoma rękami). Jednakże zecydowałem się na uproszczenie zasad, gdyż symulacja nie uwzględnia stawek pieniężnych, czyli główny powód, dla którego korzysta się z tamtych ruchów.
Co do danych do nauki, przepisałem strategię do plików, by pasowała pod model, w następujący sposób:
- learning.csv: dane z tabel opisujących ruchy
- learning_in.csv: dane z learning.csv, ale tylko wejściowe
- learning_out.csv: dane z learning.csv, ale tylko wyjściowe
- strategy.json: dane z learning.csv, rzutowane na format JSON.
