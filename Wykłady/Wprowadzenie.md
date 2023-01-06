# Wykład 1 - Wprowadzenie

### JDK - Java Development Kit
Pakiet oprogramowania, za pomocą którego można tworzyć aplikacje oparte na języku Java. Pakiet Java Development Kit jest niezbędny do tworzenia aplikacji Java.

### JRE - Java Runtime Development
Środowisko Java Runtime Environment to dodatek wymagany w celu uruchamiania programów Java.

### Kompilacja i uruchomienie programu
Aby to skompilować program posługujemy się komendą w terminalu: `javac HelloWorld.java` gdzie powstaje plik `HelloWorld.class`

Aby uruchomić program należy użyć komendę: `java HelloWorld`

### Podstawowe typy danych
##### Prymitywne typy danych:

byte (8-bit), short (16-bit), int (32-bit), long (64-bit)
float (32-bit), double (64-bit),
boolean (1-bit) - flaga
char (16-bit) – znak w unikodzie, np. `\u015b`

##### Obiektowe typy danych:

String, PrintStream, ... (wszystko inne).

### Przepływy sterowania - Instrukcje warunkowe
__if/else__ - sprawdzanie po kolei linijek kodu, wiadomo. Jeżeli w drabinie warunków coś bedzie w środku prawdziwe to kończy kompilowanie funkcji, tylko jeden blok bedzie uruchomiony. </br></br>
__switch__ - wykonanie danego bloku, może być ich więcej, tym się właśnie różni switch od if/else. Od Javy 7/8 możliwe jest wprowadzeniu argumentu typu String w switchu.</br>
### Przepływy sterowania - Pętle
__for__ - pętla która iteruje po danym argumencie.</br>
__while__ - Jeżeli jakiś warunek jest spełniony to wykonaj instrukcje.</br>
__do while__ - wykonaj jakąś instrukcje jeżeli spełniony jest jakiś warunek. </br>
### Przepływy sterowania - Zaburzenia przepływu
__break__ - ta instrukcja może być wykorzystywana do wyskoczenia z instrukcji `switch`, ale takze również może być używana przy wyskoczeniu z pętli. Przykład pokaże jak to działa: </br>
`for (int i = 0; i < 10; i++){
    if (i == 4) {
        break;
    }
    System.out.println(i);
}` i z tego wyjdzie w terminalu `0 1 2 3` </br> </br>
__continue__ - Instrukcja continue przerywa jedną iterację (w pętli), jeśli spełniony jest określony warunek, i kontynuuje z następną iteracją w pętli. </br> </br>
__return__ - Instrukcja return przypomina instrukcję break w pętli for, ponieważ przekierowuje program poza wykonanie tego bloku. Innymi słowy, instrukcja return natychmiast opuszcza bieżącą metodę i przekazuje kontrolę z powrotem do wywołującego. </br></br>

### Środowiska Developerskie:
Pełna różnorodność - VSCode, InteliJ, Eclipse itd.


