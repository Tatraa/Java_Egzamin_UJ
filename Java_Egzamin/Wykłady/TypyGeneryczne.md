# Typy generyczne

### Zalety typów generycznych
Kontrola typów już na etapie kompilacji, a nie dopiero w trakcie działania programu </br>
Brak potrzeby rzutowania </br>
Konstruowanie ogólnych algorytmów

ogólnie:
`class NazwaKlasy <T1, T2, T3, ... , Tn>` gdzie `T` oznaczy typ generyczny

### Konwencje
__T__ - typ </br>
__K__ - klucz </br>
__V__ - wartość</br>
__E__ - element (np. kolekcji) </br>
__N__ - liczba </br>

Przykład: </br>
`public interface Pair<K,V>{
public K getKey();
public V getValue()}` </br>
Interfejs również może być typowany generycznie np. Lista, Mapa.

Od Javy 7 nie trzeba w tworzeniu obiektu danej klasy deklarować wartości po prawej stronie: </br>
`Pair<String, Integer> p = new OrderedPair<String, Integer>("Even", 8);`
`Pair<String, Integer> p = new OrderedPair<>("Even", 8);`

### Typy surowe
`Box<String> typedBox = new Box<String>();`</br>
`Box rawBox = new Box();` // typ surowy <=> Box<Object>

`Box rawBox = typedBox;`</br>
`rawBox.set(8);` // warning: w trakcie działania programu może spowodować RuntimeException

Z reguły nie powinno się stosować typów surowych ze zględu na możliwość popełniania błedów, kompilator to przepuści ale nie kontroluje typów.

